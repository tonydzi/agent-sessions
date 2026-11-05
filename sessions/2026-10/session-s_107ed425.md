---
session: s_107ed425
date: 2026-10-03
words: 1622
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-03 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_107ed425` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
# artifact.proposed: vault-core pilot safety repair

Owner: codex-pilot-facts. Reviewer: Claude (parent coordinates). Date: 2026-10-03.
Scope: only scripts/vault_core_export.py and scripts/vault_core_pull.py.

Source: dev authorized fixing audit findings via parent task. No live run, network
push, scheduler/config mutation, peer rollout, canonical changes or repository deletion.

Acceptance: missing/unreadable source and failed Git operations must abort; scan and
copy identical immutable bytes; preserve dirty local core; stage only own outputs;
replication event must say sync, never imply useful knowledge consumption.

Implementation: exporter snapshots bytes before clone mutation and checks required
folders, UTF-8 and configured token patterns. Dirty checkout or pull failure aborts.
Only core, manifest and own usage path are staged. Pull preserves dirty worktrees,
checks Git outcomes, records sync only after a successful pull, retries push once
after successful rebase. Useful use still requires separate task/document evidence.

Tests: python -X utf8 test_safety.py (from this directory). Uses temporary local Git
repos including bare remote; no network. TEST_BEFORE=1 selects backed-up originals.
red.txt and green.txt preserve output. Seven original regression contracts were red;
expanded suite has 10 tests including local roundtrip and leak/dirty staging guards.
hashes.json and patch.diff identify bytes. Backups are *.before.py.

Permanent scripts; test/doc here are one-time review artifacts pending integration.
рельса: deterministic local Python/Git; Codex subscription for changes, Claude review.
Usage: existing export counter retained; pull counter now sync (not useful consumption).

Limits: no live scheduled tick or peer consumer verification performed. Regex leak
scan is not exhaustive DLP. Simultaneous processes in one clone remain unsupported;
scheduler serialization is required. Existing README/remote tools still describe old
read metric and need coordinated update after review; outside this ownership.

Rollback: restore ONLY the two scripts from *.before.py under their file leases.
Do not revert other files or touch live clone. No deployment claim.

Attribution: Codex / GPT-6; Machine HUB-01; Account local dev; Operator dev.

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
--- a/scripts/vault_core_export.py
+++ b/scripts/vault_core_export.py
@@ -10,10 +10,13 @@
     (reglament-*/protocol-*), decisions, MOCs. Target budget: ~1000 files, a few MB.
   * Messages/bus do NOT live here (breaker verdict 02.10: hot+cold in one repo = heresy).
   * Consumers run vault_core_pull.py (same dir) 2x/day: git pull + usage log.
-  * KILL CRITERION (harvest 16.10.2026): zero peer reads in usage/ for 2 weeks -> kill repo.
+  * Harvest 16.10.2026 needs evidence of useful consumption. Pull/sync events alone
+    do not establish that a peer used any knowledge.
 
 SAFETY:
-  * leak-scan before every push (fail-closed: any hit aborts the commit).
+  * Read the source once, scan those bytes, and export that exact snapshot.
+  * Missing source folders, unreadable files, dirty clone or failed pull abort.
+  * Only generated core, manifest and this node's usage file are staged.
   * excluded always: .stversions, *sync-conflict*, secrets never live in these folders anyway.
 
 USAGE:
@@ -76,7 +79,10 @@
         if r.returncode != 0:
             log(f"[core-export] clone failed: {r.stderr.strip()[:400]}"); sys.exit(2)
     # export side may pull fast-forward only; it never merges content back into the vault
-    git("pull", "--ff-only", "origin", BRANCH, check=False)
+    if git("status", "--porcelain").stdout.strip():
+        log("[core-export] dirty clone; preserve local changes and resolve before retry")
+        sys.exit(2)
+    git("pull", "--ff-only", "origin", BRANCH)
 
 
 def select_core():
@@ -84,7 +90,7 @@
     for sub, pat in CORE_RULES:
         base = VAULT / sub
         if not base.is_dir():
-            continue
+            raise OSError(f"required source directory missing: {base}")
         for p in sorted(base.rglob("*")):
             if not p.is_file():
                 continue
@@ -96,12 +102,10 @@
 
 
 def leak_scan(files):
+    """Scan (relative path, bytes) snapshot; never reread mutable source files."""
     hits = []
-    for src, rel in files:
-        try:
-            text = src.read_text(encoding="utf-8", errors="ignore")
-        except OSError:
-            continue
+    for rel, data in files:
+        text = data.decode("utf-8-sig")
         for rx in LEAK_PATTERNS:
             m = rx.search(text)
             if m:
@@ -115,9 +119,15 @@
     ap.add_argument("--no-push", action="store_true")
     args = ap.parse_args()
 
-    files = list(select_core())
-    total_bytes = sum(s.stat().st_size for s, _ in files)
-    hits = leak_scan(files)
+    try:
+        files = [(rel, src.read_bytes()) for src, rel in select_core()]
+        if not files:
+            raise OSError("source selection is empty")
+        total_bytes = sum(len(data) for _, data in files)
+        hits = leak_scan(files)
+    except (OSError, UnicodeError) as exc:
+        log(f"[core-export] source snapshot rejected: {exc}")
+        sys.exit(3)
     if hits:
         log("[core-export] ⛔ LEAK-SCAN HIT, export ABORTED (fail-closed):")
         for h in hits[:20]:
@@ -132,8 +142,8 @@
 
     # mirror: build the wanted set, delete strays, copy changed
     wanted = {}
-    for src, rel in files:
-        wanted[rel.as_posix()] = src
+    for rel, data in files:
+        wanted[rel.as_posix()] = data
     added = changed = deleted = 0
     if core_dir.is_dir():
         for p in core_dir.rglob("*"):
@@ -141,10 +151,9 @@
                 relp = p.relative_to(CLONE).as_posix()
                 if relp not in wanted:
                     p.unlink(); deleted += 1
-    for relp, src in wanted.items():
+    for relp, sb in wanted.items():
         dst = CLONE / relp
         dst.parent.mkdir(parents=True, exist_ok=True)
-        sb = src.read_bytes()
         if not dst.exists():
             dst.write_bytes(sb); added += 1
         elif hashlib.md5(dst.read_bytes()).digest() != hashlib.md5(sb).digest():
@@ -161,13 +170,13 @@
         f.write(json.dumps({"ts": now, "node": MACHINE, "actor": "vault_core_export",
                             "event": "export", "outcome": f"{len(wanted)}f/{added}a/{changed}c/{deleted}d"}) + "\n")
 
-    git("add", "-A")
+    git("add", "--", "core", "manifest.json", f"usage/{MACHINE}.jsonl")
     st = git("status", "--porcelain").stdout.strip()
     if not st:
         log(f"[core-export] no changes: {len(wanted)} files, repo already current")
         return
     git("commit", "-m", f"core: export {now} {len(wanted)} files (+{added} ~{changed} -{deleted}) from {MACHINE}",
-        "-m", "Assisted-by: Claude Code / claude-fable-5\nMachine: " + MACHINE)
+        "-m", "Actor: vault_core_export\nMachine: " + MACHINE)
     pushed = "skipped"
     if not args.no_push:
         r = git("push", "origin", BRANCH, check=False)
--- a/scripts/vault_core_pull.py
+++ b/scripts/vault_core_pull.py
@@ -2,12 +2,13 @@
 # -*- coding: utf-8 -*-
 """vault_core_pull.py -- consumer side of the vault-core pilot (DR26-10-02-HUB-02).
 
-Runs on PEERS 2x/day: git pull the core replica + log a READ event into usage/<MACHINE>.jsonl
-(committed+pushed: single-writer file per machine => no merge conflicts). The usage log is the
-pilot's harvest metric (16.10.2026): zero peer reads in 2 weeks -> the repo is killed.
+Runs on PEERS 2x/day: git pull the core replica + log a SYNC event into usage/<MACHINE>.jsonl.
+This proves replication only, not reading or useful application of knowledge. Harvest
+16.10.2026 needs separate evidence of useful consumption. Failed pull records no success.
 
-The clone is a READ REPLICA: peers never edit core/ (any local drift is hard-reset to origin --
-core/ holds generated copies, the vault stays the single source of truth).
+The clone is a READ REPLICA. Dirty worktrees are preserved and rejected, never discarded.
+Git failures abort; only this node's usage file is staged. Concurrent processes sharing a
+clone are unsupported: the scheduler must serialize access. Vault stays the source of truth.
 
 USAGE:
   python vault_core_pull.py          # pull + log usage + push the log line
@@ -26,8 +27,12 @@
 MACHINE = os.environ.get("COMPUTERNAME") or socket.gethostname()
 
 
-def git(*args):
-    return subprocess.run(["git", "-C", str(CLONE), *args], capture_output=True, text=True)
+def git(*args, check=True):
+    r = subprocess.run(["git", "-C", str(CLONE), *args], capture_output=True, text=True)
+    if check and r.returncode:
+        print(f"[core-pull] git {args[0]} failed: {r.stderr.strip()[:300]}")
+        sys.exit(3)
+    return r
 
 
 def main():
@@ -37,22 +42,26 @@
         if r.returncode != 0:
             print(f"[core-pull] clone failed: {r.stderr.strip()[:300]}"); sys.exit(2)
 
-    # read replica: local edits under core/ are not ours to keep
-    git("checkout", "--", "core")
-    r = git("pull", "--rebase", "--autostash", "origin", BRANCH)
-    pull = "OK" if r.returncode == 0 else f"FAIL: {r.stderr.strip()[:200]}"
+    if git("status", "--porcelain").stdout.strip():
+        print("[core-pull] dirty clone; preserve local changes and resolve before retry")
+        sys.exit(3)
+    git("pull", "--rebase", "origin", BRANCH)
+    if not (CLONE / "core").is_dir():
+        print("[core-pull] missing core directory; sync not recorded")
+        sys.exit(3)
+    pull = "OK"
 
     now = datetime.now(timezone.utc).isoformat(timespec="seconds")
     usage = CLONE / "usage"; usage.mkdir(exist_ok=True)
     n_files = sum(1 for p in (CLONE / "core").rglob("*") if p.is_file()) if (CLONE / "core").is_dir() else 0
     with open(usage / f"{MACHINE}.jsonl", "a", encoding="utf-8") as f:
         f.write(json.dumps({"ts": now, "node": MACHINE, "actor": "vault_core_pull",
-                            "event": "read", "outcome": f"pull {pull}; core {n_files} files"}) + "\n")
-    git("add", "usage")
-    git("commit", "-m", f"usage: read {now} @ {MACHINE}")
-    p = git("push", "origin", BRANCH)
+                            "event": "sync", "outcome": f"pull {pull}; core {n_files} files"}) + "\n")
+    git("add", "--", f"usage/{MACHINE}.jsonl")
+    git("commit", "-m", f"usage: sync {now} @ {MACHINE}")
+    p = git("push", "origin", BRANCH, check=False)
     if p.returncode != 0:
-        # someone pushed in between: rebase (usage/<MACHINE>.jsonl is single-writer, no conflict possible) and retry once
+        # Another node may have pushed. Retry once; any rebase conflict is an error.
         git("pull", "--rebase", "origin", BRANCH)
         p = git("push", "origin", BRANCH)
     push = "OK" if p.returncode == 0 else f"FAIL: {p.stderr.strip()[:200]}"

--- DIFF END ---

---

**Claude:**

You've hit your weekly limit · resets 5am (Europe/London)
