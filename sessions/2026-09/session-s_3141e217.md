---
session: s_3141e217
date: 2026-09-24
words: 1881
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3141e217` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author.
The author (Codex) wrote the change below. Review it on its own merits. Do NOT use any tools
or read other files; review ONLY the diff provided. Be concrete and skeptical.

CRITICAL OUTPUT CONTRACT: the VERY LAST line of your reply must be exactly
  ===VERDICT=== <value>
where <value> is one bare word: APPROVE (no blocking issues) or
REQUEST_CHANGES (one or more MED/HIGH issues). No backticks, no bold, no
brackets, nothing else on that line. State it exactly once, on that final
line only -- do not repeat the marker anywhere else in your reply.

Write your review first, then the contract line last.

## What Codex was asked to do (context)
Review exact current CV resolver attachment repair. 8 offline tests pass; real19 rendering in progress. No submissions. Windows broker failed due cmd argument limit so prompt is passed stdin. Only new import+preflight change auto_apply. Return verdict contract.

Check, in priority order:
1. CORRECTNESS bugs (logic errors, off-by-one, wrong conditions, unhandled cases, races).
2. SECURITY (injection, secrets in code, unsafe input, path/permission issues).
3. BREAKAGE (does it break callers, contracts, or existing behavior?).
4. SIMPLIFICATION / dead code (is there a simpler, equally-correct form? AK-47).

Rules:
- Fix the ROOT cause, not the symptom. If you propose a fix, make it the simplest correct one.
- Only report REAL issues. If the diff is clean, say so plainly.
- For each finding give: `file:line` | severity (high/med/low) | what's wrong | the fix.

Format:
SUMMARY: <one or two sentences>
FINDINGS:
- file:line | severity | issue | fix
(repeat; write "none" if no findings)
Then the contract line from the output contract above, last.

--- DIFF START ---
diff --git a/jobs-watch/selenium_apply/auto_apply.py b/jobs-watch/selenium_apply/auto_apply.py
index c6d69178..f4202bed 100644
--- a/jobs-watch/selenium_apply/auto_apply.py
+++ b/jobs-watch/selenium_apply/auto_apply.py
@@ -41,14 +41,7 @@ import gh_lib  # noqa: E402
 import lever_lib  # noqa: E402
 import answers_canon as A  # noqa: E402
 
-CV_DIR = r"D:\Vault\Vault-Knowledge\04-Projects\Pipe-A-Batches\sent-2026-09-01"
-CV_MAP = {"fde": "FDE", "product": "Product", "founder-bd": "BD-Partnerships",
-          "security": "Security", "scholar": "Writer", "devrel": "DevRel",
-          "startup-ecosystem": "Startup-Ecosystem", "stablecoin": "BD-Partnerships",
-          "exchange": "BD-Partnerships",
-          # 23.09: кластер «Silicon Valley landing lead» (иностранные AI/compute-компании, заходящие
-          # в Долину); PDF собран из cv_forge sv-landing и лежит в CV_DIR рядом с остальными
-          "sv-landing": "Silicon-Valley-Landing-Lead"}
+from cv_attachment import resolve as cv_path  # current source + hash-verified PDF cache
 
 # company-hosted GH wrappers -> embed door (плейбук: block.xyz/nebius приём)
 GH_EMBED_SLUGS = {"legalist.com": "legalist", "careers.withwaymo.com": "waymo",
@@ -88,10 +81,6 @@ GH_EMBED_SLUGS = {"legalist.com": "legalist", "careers.withwaymo.com": "waymo",
                   "careers.upstart.com": "upstart"}
 
 
-def cv_path(cluster):
-    return os.path.join(CV_DIR, f"[ИМЯ]-[ФАМИЛИЯ]-CV-{CV_MAP.get(cluster, 'Startup-Ecosystem')}.pdf")
-
-
 def safe(fn, *args, **kw):
     """одно упавшее поле не валит подачу — финальный EMPTY-REQUIRED всё равно поймает дыру.
     StaleElement = гонка ре-рендера (autofill) — один повтор после паузы (eliseai 04.09)."""
@@ -524,6 +513,12 @@ def main():
     os.makedirs(RUNS, exist_ok=True)   # каталог создаём в main(), не при импорте
     entry = json.load(open(sys.argv[1], encoding="utf-8"))
     do_submit = "--submit" in sys.argv
+    if "--dump-only" not in sys.argv:
+        try:
+            cv_path(entry.get("cluster"))  # fail closed before browser/form interaction
+        except Exception as e:
+            print("OUTCOME: missing:CV-attachment:", str(e)[:300], flush=True)
+            return
     url = entry["url"] if entry["ats"] != "greenhouse" else gh_target_url(entry["url"])
     if entry["ats"] == "ashby" and "ashbyhq.com" in url and not url.rstrip("/").endswith("/application"):
         url = url.rstrip("/") + "/application"  # форма живёт на вкладке Application, не на Overview
--- /dev/null
+++ cv_attachment.py
@@ -0,0 +1,145 @@
+"""Current CV-Variants -> verified text PDF. See CV_ATTACHMENT.md. No LLM."""
+import hashlib
+import html
+import json
+import os
+from pathlib import Path
+import re
+import subprocess
+import socket
+import sys
+import tempfile
+from datetime import datetime, timezone
+
+HERE = Path(__file__).resolve().parent
+sys.path.insert(0, str(HERE.parent))
+from jobs_discover import CV_FILE
+sys.path.insert(0, str(HERE.parent.parent))
+from make_resume_pdf import find_chrome
+
+CV_MAP = dict(CV_FILE, **{"sv-landing": "[ИМЯ]-[ФАМИЛИЯ]-CV-Silicon-Valley-Landing-Lead.md"})
+RENDERER = "chrome-single-column-v1"
+CSS = """@page { size:A4; margin:16mm; } body {font:10pt Arial,sans-serif;color:#111;line-height:1.3}
+h1 {font-size:17pt} h2 {font-size:12pt;break-after:avoid} p,li {orphans:3;widows:3}
+a {color:#111;text-decoration:none} ul {padding-left:18px} li {margin-bottom:3px}"""
+
+
+class AttachmentError(RuntimeError):
+    pass
+
+
+def sha(data):
+    return hashlib.sha256(data).hexdigest()
+
+
+def record_use(folder, cluster, key, outcome):
+    event = {"ts": datetime.now(timezone.utc).isoformat(),
+             "node": os.environ.get("COMPUTERNAME") or socket.gethostname(),
+             "actor": "cv_attachment", "event": "resolve", "outcome": outcome,
+             "cluster": cluster, "key": key}
+    with (folder / "usage.jsonl").open("a", encoding="utf-8") as log:
+        log.write(json.dumps(event) + "\n")
+
+
+def source_dir():
+    vault = os.environ.get("OBSIDIAN_VAULT")
+    if not vault and sys.platform == "win32":
+        vault = r"D:\Vault\Vault-Knowledge"
+    if not vault:
+        raise AttachmentError("set OBSIDIAN_VAULT for this machine")
+    return Path(vault) / "05-Resources" / "CV-Variants"
+
+
+def cache_dir():
+    return Path(os.environ.get("CV_ATTACHMENT_CACHE", str(HERE / "runs" / "cv-cache")))
+
+
+def validate_pdf(path, source):
+    from pypdf import PdfReader
+    if not path.is_file() or not path.read_bytes().startswith(b"%PDF-"):
+        raise AttachmentError("missing or invalid PDF")
+    reader = PdfReader(path)
+    text = "\n".join(page.extract_text() or "" for page in reader.pages)
+    if not reader.pages or len(text.strip()) < 500:
+        raise AttachmentError("PDF has no usable text layer")
+    words = set(re.findall(r"[a-z]{4,}", source.lower()))
+    extracted = set(re.findall(r"[a-z]{4,}", text.lower()))
+    if len(words - extracted) > max(3, len(words) * .03):
+        raise AttachmentError("PDF text does not cover source CV")
+    for keyword in ("Python", "C++"):
+        if keyword in source and keyword not in text:
+            raise AttachmentError("PDF lost source skill: " + keyword)
+    return len(reader.pages)
+
+
+def render_pdf(source, dest, work):
+    import markdown
+    chrome = find_chrome()
+    if not chrome:
+        raise AttachmentError("Chrome missing; check CHROME_BIN")
+    body = markdown.markdown(html.escape(source), extensions=[])
+    body = re.sub(r"<img\b[^>]*>", "", body)
+    page = work / "resume.html"
+    page.write_text('<meta charset="utf-8"><style>' + CSS + "</style>" + body, encoding="utf-8")
+    result = subprocess.run([
+        chrome, "--headless", "--disable-gpu", "--no-pdf-header-footer",
+        "--disable-background-networking", "--no-first-run",
+        "--user-data-dir=" + str(work / "chrome-profile"),
+        "--print-to-pdf=" + str(dest), page.as_uri()],
+        capture_output=True, timeout=120,
+        creationflags=subprocess.CREATE_NO_WINDOW if os.name == "nt" else 0)
+    if result.returncode:
+        raise AttachmentError("Chrome PDF failed rc=" + str(result.returncode))
+
+
+def resolve(cluster, sources=None, cache=None):
+    """Exact cluster; rebuild stale cache; never fall back to another CV."""
+    if cluster not in CV_MAP:
+        raise AttachmentError("unknown CV cluster: " + str(cluster))
+    source = Path(sources or source_dir()) / CV_MAP[cluster]
+    if not source.is_file():
+        raise AttachmentError("missing CV source: " + str(source))
+    data = source.read_bytes()
+    text = data.decode("utf-8-sig")
+    if len(text.strip()) < 500:
+        raise AttachmentError("empty/incomplete CV source: " + str(source))
+    identity = {"source": str(source.resolve()), "source_sha256": sha(data),
+                "renderer": RENDERER, "renderer_sha256": sha(Path(__file__).read_bytes())}
+    key = sha(json.dumps(identity, sort_keys=True).encode())
+    folder = Path(cache or cache_dir())
+    pdf = folder / (source.stem + "-" + key[:16] + ".pdf")
+    manifest = pdf.with_suffix(".json")
+    if pdf.is_file() and manifest.is_file():
+        try:
+            saved = json.loads(manifest.read_text(encoding="utf-8"))
+            if all(saved.get(k) == v for k, v in identity.items()) and saved.get("pdf_sha256") == sha(pdf.read_bytes()):
+                validate_pdf(pdf, text)
+                record_use(folder, cluster, key, "cache-hit")
+                print("CV-CACHE-HIT:", cluster, key[:16], flush=True)
+                return str(pdf)
+        except (ValueError, OSError, AttachmentError):
+            pass
+    folder.mkdir(parents=True, exist_ok=True)
+    with tempfile.TemporaryDirectory(prefix="cv-build-", dir=folder) as tmp:
+        work = Path(tmp)
+        built = work / "resume.pdf"
+        render_pdf(text, built, work)
+        pages = validate_pdf(built, text)
+        if source.read_bytes() != data:
+            raise AttachmentError("CV source changed during render; retry")
+        record = dict(identity, pdf_sha256=sha(built.read_bytes()), pages=pages)
+        ready = work / "manifest.json"
+        ready.write_text(json.dumps(record, indent=2), encoding="utf-8")
+        os.replace(built, pdf)
+        os.replace(ready, manifest)
+    print("CV-BUILT:", cluster, key[:16], "pages=" + str(pages), flush=True)
+    record_use(folder, cluster, key, "built")
+    return str(pdf)
+
+
+if __name__ == "__main__":
+    requested = list(CV_MAP) if sys.argv[1:] == ["--all"] else sys.argv[1:]
+    if not requested:
+        sys.exit("usage: cv_attachment.py CLUSTER | --all")
+    for name in requested:
+        print(resolve(name))
--- /dev/null
+++ _test_cv_attachment.py
@@ -0,0 +1,89 @@
+"""Offline regression: exact mapping, freshness, corruption and failure gates."""
+import json
+from pathlib import Path
+import tempfile
+import unittest
+from unittest.mock import patch
+import cv_attachment as C
+
+
+class AttachmentTests(unittest.TestCase):
+    def setUp(self):
+        self.tmp = tempfile.TemporaryDirectory()
+        self.addCleanup(self.tmp.cleanup)
+        self.root = Path(self.tmp.name)
+        self.sources = self.root / "sources"
+        self.sources.mkdir()
+        self.cache = self.root / "cache"
+        self.source = self.sources / C.CV_MAP["research"]
+        self.source.write_text("Research Python C++ " * 50, encoding="utf-8")
+        self.render = patch.object(C, "render_pdf", side_effect=lambda src, dest, work: dest.write_bytes(b"%PDF-test"))
+        self.renderer = self.render.start()
+        self.addCleanup(self.render.stop)
+        self.validation = patch.object(C, "validate_pdf", return_value=2)
+        self.validation.start()
+        self.addCleanup(self.validation.stop)
+
+    def resolve(self, cluster="research"):
+        return Path(C.resolve(cluster, self.sources, self.cache))
+
+    def test_unknown_and_missing_fail_closed(self):
+        for cluster in ("typo", "", None, "FDE"):
+            with self.assertRaises(C.AttachmentError):
+                self.resolve(cluster)
+        with self.assertRaises(C.AttachmentError):
+            self.resolve("product")
+        self.renderer.assert_not_called()
+
+    def test_cache_hit_and_source_change(self):
+        first = self.resolve()
+        self.assertEqual(first, self.resolve())
+        self.assertEqual(1, self.renderer.call_count)
+        self.source.write_text(self.source.read_text() + "\nNew truthful evidence", encoding="utf-8")
+        second = self.resolve()
+        self.assertNotEqual(first, second)
+        self.assertEqual(2, self.renderer.call_count)
+
+    def test_pdf_corruption_rebuilds(self):
+        first = self.resolve()
+        first.write_bytes(b"bad")
+        self.assertEqual(first, self.resolve())
+        self.assertEqual(2, self.renderer.call_count)
+
+    def test_renderer_failure_no_manifest(self):
+        self.renderer.side_effect = C.AttachmentError("Chrome missing")
+        with self.assertRaises(C.AttachmentError):
+            self.resolve()
+        self.assertEqual([], list(self.cache.glob("*.json")))
+        self.assertEqual([], list(self.cache.glob("*.pdf")))
+
+    def test_source_changes_during_render(self):
+        def changing(src, dest, work):
+            dest.write_bytes(b"%PDF-test")
+            self.source.write_text(src + " changed")
+        self.renderer.side_effect = changing
+        with self.assertRaisesRegex(C.AttachmentError, "changed during"):
+            self.resolve()
+        self.assertEqual([], list(self.cache.glob("*.pdf")))
+
+    def test_renderer_version_change(self):
+        first = self.resolve()
+        with patch.object(C, "RENDERER", "test-next-version"):
+            self.assertNotEqual(first, self.resolve())
+
+    def test_live_mapping_covers_all_variants(self):
+        files = {p.name for p in C.source_dir().glob("[ИМЯ]-[ФАМИЛИЯ]-CV-*.md")}
+        self.assertEqual(files, set(C.CV_MAP.values()))
+        self.assertEqual(19, len(C.CV_MAP))
+
+    def test_preflight_stops_before_browser(self):
+        import auto_apply as A
+        entry = self.root / "entry.json"
+        entry.write_text(json.dumps({"cluster": "typo", "company": "Test"}))
+        with patch.object(A.sys, "argv", ["auto_apply.py", str(entry), "--submit"]), patch.object(A, "new_driver") as browser:
+            A.main()
+            browser.assert_not_called()
+
+
+if __name__ == "__main__":
+    unittest.main()
--- /dev/null
+++ CV_ATTACHMENT.md
@@ -0,0 +1,19 @@
+# Current CV attachment resolver
+
+Status: artifact.proposed, 2026-09-24. Owner: Codex; named reviewer: Claude Opus via cc_review.
+
+Consumer: auto_apply.py (called by run_slice.py). Before form interaction it resolves the exact cluster to a fresh PDF. All three existing ATS upload paths use that resolver. Original sent archives are untouched.
+
+Before: a dated sent-2026-09-01 directory, ten aliases, unknown clusters silently got Startup-Ecosystem. After: jobs_discover.CV_FILE plus the current sv-landing variant, nineteen exact sources in CV-Variants. Unknown/missing/incomplete source blocks before opening the browser. Old cache is never used after a source or renderer hash changes; a failed renderer blocks the application.
+
+Input: OBSIDIAN_VAULT/05-Resources/CV-Variants/*.md (same platform default as cv_forge). Facts are never rewritten. Output: runs/cv-cache/<source>-<hash>.pdf and matching JSON containing source hash, renderer hash, PDF hash and page count. CV_ATTACHMENT_CACHE can redirect generated artifacts for isolated tests.
+
+Format: single column, A4, selectable text; Markdown converted with installed markdown, printed through local Chrome found by existing make_resume_pdf.find_chrome. Separate temporary Chrome profile; no login or user browsing profile. Installed pypdf verifies text coverage and Python/C++ retention. Text extraction is a local check, not proof of a specific employer's ATS ranking.
+
+рельса: local Python + headless Chrome, 0 LLM/API spend. Permanent repair, test+passport included.
+
+Usage counter: runs/cv-cache/usage.jsonl, fields ts/node/actor/event/outcome plus cluster/key. A resolve is attachment preparation, not proof of upload or submission. Existing run_slice logs retain CV-BUILT/CV-CACHE-HIT lines.
+
+Repair: missing Chrome -> set CHROME_BIN; missing Python library -> use the environment with existing markdown and pypdf. Missing source -> regenerate through cv_forge only after checking master. Text validation failure -> inspect the source and generated PDF; do not use the dated archive as fallback. Corrupt cache rebuilds automatically. No old PDF deletion is required.
+
+Validation: `python _test_cv_attachment.py` (offline negative controls), `python cv_attachment.py --all` (real local rendering/extraction, no form or submission). Review generated pages visually when changing the renderer. Rollback: restore auto_apply.py's original attachment block from the accompanying patch; keep generated cache for evidence.

--- DIFF END ---

---

**Claude:**

You've hit your weekly limit · resets Sep 27, 5am (Europe/London)
