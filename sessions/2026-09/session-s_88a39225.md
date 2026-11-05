---
session: s_88a39225
date: 2026-09-22
words: 3475
turns: 4
tools: "Bash, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · Ты независимый старший ревьюер. Этот diff написал Codex. Ищи только доказуемые проблемы: c…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_88a39225` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты независимый старший ревьюер. Этот diff написал Codex. Ищи только доказуемые проблемы: correctness, security, breakage, unsafe mass migration, tests. Для каждой: file:line, severity HIGH/MED/LOW, проблема, исправление. Если блокеров нет, скажи прямо. Заверши ровно VERDICT: APPROVE или VERDICT: REQUEST_CHANGES.
diff --git a/codex/_test_external_agent_import_filter.py b/codex/_test_external_agent_import_filter.py
new file mode 100644
index 00000000..0d2de3fb
--- /dev/null
+++ b/codex/_test_external_agent_import_filter.py
@@ -0,0 +1,134 @@
+# -*- coding: utf-8 -*-
+"""Regression: Claude sessions imported by Codex Harness never enter the Codex lane."""
+import importlib.util
+import json
+import sqlite3
+import tempfile
+from pathlib import Path
+
+
+HERE = Path(__file__).resolve().parent
+SPEC = importlib.util.spec_from_file_location("codex_lib_under_test", HERE / "codex_lib.py")
+codex_lib = importlib.util.module_from_spec(SPEC)
+SPEC.loader.exec_module(codex_lib)
+
+
+def rollout(path, sid, prompt):
+    rows = [
+        {"timestamp": "2026-09-22T10:00:00Z", "type": "session_meta",
+         "payload": {"session_id": sid, "timestamp": "2026-09-22T10:00:00Z",
+                     "cwd": "C:/work", "cli_version": "0.test", "originator": "codex_tui"}},
+        {"timestamp": "2026-09-22T10:00:01Z", "type": "response_item",
+         "payload": {"type": "message", "role": "user",
+                     "content": [{"type": "input_text", "text": prompt}]}},
+    ]
+    path.parent.mkdir(parents=True, exist_ok=True)
+    path.write_text("\n".join(json.dumps(x) for x in rows), encoding="utf-8")
+
+
+def registry(path, imported_sid):
+    path.write_text(json.dumps({"records": [{
+        "source_path": "C:/Users/dev/.claude/projects/source.jsonl",
+        "imported_thread_id": imported_sid,
+    }]}), encoding="utf-8")
+
+
+def run():
+    genuine = "s_546cd47d"
+    imported = "s_4942c078"
+    with tempfile.TemporaryDirectory() as td_raw:
+        td = Path(td_raw)
+        root = td / ".codex"
+        sessions = root / "sessions"
+        vault = td / "vault"
+        rollout(sessions / "2026/09/22/rollout-genuine.jsonl", genuine, "genuine Codex")
+        rollout(sessions / "2026/09/22/rollout-imported.jsonl", imported, "from Claude")
+        registry(root / "external_agent_session_imports.json", imported)
+        (root / "config.toml").write_text(
+            "external-agent-import-sync-enabled = false\n"
+            "external-agent-import-sync-item-types = { SESSIONS = false }\n",
+            encoding="utf-8")
+
+        saved = (codex_lib.DB, codex_lib.FRESHNESS, codex_lib.VAULT,
+                 codex_lib.SESSIONS_DIR, codex_lib.archive_originals,
+                 codex_lib.machine_name, codex_lib.account_email)
+        codex_lib.DB = td / "codex.db"
+        codex_lib.FRESHNESS = td / "freshness.json"
+        codex_lib.VAULT = vault
+        codex_lib.SESSIONS_DIR = sessions
+        codex_lib.archive_originals = lambda files, machine: (len(files), td / "originals")
+        codex_lib.machine_name = lambda: "TestNode"
+        codex_lib.account_email = lambda path=None: "[EMAIL]"
+        try:
+            first = codex_lib.do_import(sessions)
+            assert first[2] == 0, first
+            con = sqlite3.connect(codex_lib.DB)
+            assert {r[0] for r in con.execute("SELECT session_id FROM sessions")} == {genuine}
+            con.close()
+            notes = list((vault / "01-Conversations/Codex/TestNode").glob("*.md"))
+            assert len(notes) == 1 and f"session_id: {genuine}" in notes[0].read_text(encoding="utf-8")
+            fresh = json.loads(codex_lib.FRESHNESS.read_text(encoding="utf-8"))
+            assert fresh["unique_sessions_on_disk"] == 1
+            assert fresh["external_agent_sessions_excluded"] == 1
+
+            # Historical contamination must be moved, never deleted, and removed from DB.
+            con = codex_lib.connect()
+            imported_row = dict(
+                session_id=imported, machine="TestNode", account="[EMAIL]",
+                title="from Claude", start_iso="2026-09-22T10:00:00Z", day="2026-09-22",
+                month="2026-09", cwd="C:/work", cli_version="0.test",
+                originator="codex_tui", git_repo="", content_hash="x", n_turns=1,
+                turns=[{"role": "user", "text": "from Claude", "ts": "", "kind": "message"}],
+                src_file="rollout-imported.jsonl")
+            codex_lib.upsert(con, [imported_row])
+            con.close()
+            contaminated = vault / "01-Conversations/Codex/TestNode/2026-09-22-from-claude-000000000002.md"
+            contaminated.write_text(
+                "---\nsource: codex\nsession_id: %s\nrelated_concepts: []\n---\nClaude body\n" % imported,
+                encoding="utf-8")
+            second = codex_lib.do_import(sessions)
+            assert second[2] == 0, second
+            con = sqlite3.connect(codex_lib.DB)
+            assert con.execute("SELECT COUNT(*) FROM sessions WHERE session_id=?", (imported,)).fetchone()[0] == 0
+            con.close()
+            assert not contaminated.exists()
+            quarantined = list((contaminated.parent / "_external-agent-imports").glob("*.md"))
+            assert len(quarantined) == 1 and "Claude body" in quarantined[0].read_text(encoding="utf-8")
+
+            # A vanished native rollout must not survive forever as a green DB/note ghost.
+            genuine_file = sessions / "2026/09/22/rollout-genuine.jsonl"
+            genuine_file.unlink()
+            third = codex_lib.do_import(sessions)
+            assert third[2] == 0, third
+            con = sqlite3.connect(codex_lib.DB)
+            assert con.execute("SELECT COUNT(*) FROM sessions WHERE session_id=?", (genuine,)).fetchone()[0] == 0
+            con.close()
+            assert not list((vault / "01-Conversations/Codex/TestNode").glob("*.md"))
+            missing = list((vault / "01-Conversations/Codex/TestNode/_missing-source").glob("*.md"))
+            assert len(missing) == 1 and f"session_id: {genuine}" in missing[0].read_text(encoding="utf-8")
+
+            # Malformed provenance must fail closed before it can pollute DB/notes.
+            (root / "external_agent_session_imports.json").write_text("{broken", encoding="utf-8")
+            try:
+                codex_lib.do_import(sessions)
+            except codex_lib.ExternalImportRegistryError:
+                pass
+            else:
+                raise AssertionError("malformed external import registry did not fail closed")
+
+            # Harness drift back to ON is a visible non-zero health result.
+            registry(root / "external_agent_session_imports.json", imported)
+            (root / "config.toml").write_text(
+                "external-agent-import-sync-enabled = true\n"
+                "external-agent-import-sync-item-types = { SESSIONS = true }\n",
+                encoding="utf-8")
+            assert codex_lib.do_import(sessions)[2] != 0
+        finally:
+            (codex_lib.DB, codex_lib.FRESHNESS, codex_lib.VAULT,
+             codex_lib.SESSIONS_DIR, codex_lib.archive_originals,
+             codex_lib.machine_name, codex_lib.account_email) = saved
+
+
+if __name__ == "__main__":
+    run()
+    print("PASS: external-agent imports are excluded and quarantined")
diff --git a/codex/codex_lib.py b/codex/codex_lib.py
index 93415762..9813c54d 100644
--- a/codex/codex_lib.py
+++ b/codex/codex_lib.py
@@ -128,7 +128,7 @@ def _sid_of_file(path):
     return ""
 
 
-def unique_sessions_on_disk(sessions_dir=None):
+def unique_sessions_on_disk(sessions_dir=None, exclude_ids=None):
     """Сколько РАЗНЫХ сессий лежит на диске. Считать ФАЙЛЫ нельзя: возобновлённая сессия
     (`codex resume`) пишет НОВЫЙ rollout-файл с тем же session_id. ЗАМЕР 14.08 на хабе:
     421 файл против 408 сессий — все 13 «пропавших» оказались резюмами уже учтённых.
@@ -139,6 +139,7 @@ def unique_sessions_on_disk(sessions_dir=None):
     if not d.exists():
         return 0
     seen = set()
+    excluded = set(exclude_ids or ())
     for p in d.glob("**/rollout-*.jsonl"):
         try:
             with open(p, encoding="utf-8", errors="ignore") as fh:
@@ -149,6 +150,8 @@ def unique_sessions_on_disk(sessions_dir=None):
                         sid = (json.loads(line).get("payload") or {}).get("session_id")
                     except ValueError:
                         sid = None
+                    if sid and sid in excluded:
+                        break
                     seen.add(sid or str(p))
                     break
                 else:
@@ -158,6 +161,56 @@ def unique_sessions_on_disk(sessions_dir=None):
     return len(seen)
 
 
+class ExternalImportRegistryError(RuntimeError):
+    """The Harness provenance registry exists but cannot be trusted."""
+
+
+def external_import_ids(codex_root):
+    """Return Harness-imported thread ids from the sibling provenance registry.
+
+    Missing means this Codex installation never used the importer. Existing but malformed
+    means STOP: silently treating those sessions as native Codex would contaminate the
+    archive again.
+    """
+    path = Path(codex_root) / "external_agent_session_imports.json"
+    if not path.exists():
+        return set()
+    try:
+        data = json.loads(path.read_text(encoding="utf-8"))
+        records = data.get("records")
+        if not isinstance(records, list):
+            raise ValueError("records is not a list")
+        ids = set()
+        for i, rec in enumerate(records):
+            if not isinstance(rec, dict):
+                raise ValueError(f"records[{i}] is not an object")
+            sid = rec.get("imported_thread_id")
+            if not isinstance(sid, str) or not sid.strip():
+                raise ValueError(f"records[{i}] has no imported_thread_id")
+            ids.add(sid.strip())
+        return ids
+    except (OSError, ValueError, TypeError) as exc:
+        raise ExternalImportRegistryError(
+            f"битый реестр происхождения {path}: {exc}; импорт остановлен fail-closed") from exc
+
+
+def harness_session_import_enabled(config_path):
+    """Cheap drift guard for the two Harness switches that can import Claude sessions."""
+    p = Path(config_path)
+    if not p.exists():
+        return False
+    try:
+        text = p.read_text(encoding="utf-8", errors="replace")
+    except OSError:
+        return False
+    live = "\n".join(line.split("#", 1)[0] for line in text.splitlines())
+    master = re.search(r"(?mi)^\s*external-agent-import-sync-enabled\s*=\s*true\s*$", live)
+    sessions = re.search(
+        r"(?mi)^\s*external-agent-import-sync-item-types\s*=\s*\{[^}\n]*\bSESSIONS\s*=\s*true\b",
+        live)
+    return bool(master or sessions)
+
+
 def _machine_env_name(path=None):
     """MACHINE_NAME из ~/.claude/machine.env — тот же файл, по которому _paths.py решает,
     где волт. Один машинно-локальный факт вместо гуляющего хостнейма."""
@@ -494,6 +547,72 @@ def sweep_stale_notes(d, sid, keep):
             pass
 
 
+def quarantine_notes(session_ids, quarantine_name, machine=None):
+    """Move selected notes out of the Codex lane, preserving every byte.
+
+    The exact frontmatter session_id is the authority. Filename tails and titles are only
+    hints and are unsafe for a mass move. Quarantine stays beside the owning machine so a
+    rollback is a plain move, while non-recursive consumers stop indexing it as Codex.
+    """
+    ids = set(session_ids or ())
+    root = VAULT / "01-Conversations" / "Codex"
+    if not ids or not root.exists():
+        return 0
+    moved = 0
+    for node in root.iterdir():
+        if not node.is_dir() or node.name.startswith("_"):
+            continue
+        if machine and node.name != machine:
+            continue
+        for p in node.glob("*.md"):
+            body = p.read_text(encoding="utf-8", errors="replace")
+            match = re.search(r"(?m)^session_id:\s*([^\s]+)\s*$", body)
+            if not match or match.group(1) not in ids:
+                continue
+            dest_dir = node / quarantine_name
+            dest_dir.mkdir(exist_ok=True)
+            dest = dest_dir / p.name
+            if dest.exists():
+                stamp = datetime.datetime.now().strftime("%Y%m%d-%H%M%S-%f")
+                dest = dest_dir / f"{p.stem}.{stamp}{p.suffix}"
+            p.rename(dest)
+            moved += 1
+    return moved
+
+
+def quarantine_external_notes(session_ids):
+    """Move misclassified Claude notes to a reversible, non-indexed quarantine."""
+    return quarantine_notes(session_ids, "_external-agent-imports")
+
+
+def purge_external_sessions(con, session_ids):
+    """Remove external-import rows from the derived DB after their notes are quarantined."""
+    ids = list(set(session_ids or ()))
+    removed = 0
+    for start in range(0, len(ids), 500):
+        chunk = ids[start:start + 500]
+        marks = ",".join("?" for _ in chunk)
+        cur = con.execute(f"DELETE FROM sessions WHERE session_id IN ({marks})", chunk)
+        removed += cur.rowcount
+    con.commit()
+    return removed
+
+
+def reconcile_missing_sources(con, machine, live_session_ids):
+    """Quarantine derived notes/rows whose native rollout disappeared from this node."""
+    known = {r[0] for r in con.execute(
+        "SELECT session_id FROM sessions WHERE machine=?", (machine,))}
+    missing = known - set(live_session_ids or ())
+    moved = quarantine_notes(missing, "_missing-source", machine=machine)
+    if missing:
+        marks = ",".join("?" for _ in missing)
+        con.execute(
+            f"DELETE FROM sessions WHERE machine=? AND session_id IN ({marks})",
+            (machine, *missing))
+        con.commit()
+    return len(missing), moved
+
+
 def archive_originals(files, machine):
     """Raw rollouts kept verbatim (canon §8.3 step 1). Peer nodes must NOT write to the
     hub's canon originals path — _paths.originals_root() picks the right one per role;
@@ -516,7 +635,8 @@ def archive_originals(files, machine):
     return copied, dest
 
 
-def write_freshness(con, machine):
+def write_freshness(con, machine, exclude_ids=None, excluded_on_disk=0,
+                    harness_import_enabled=False):
     row = con.execute("SELECT MAX(day) FROM sessions WHERE machine=? AND day<>''",
                       (machine,)).fetchone()
     newest = row[0] if row and row[0] else None
@@ -536,7 +656,7 @@ def write_freshness(con, machine):
     # ⚠️ 14.08: сравнивать БД с заметками МАЛО — оба числа считаются под ОДНИМ ярлыком узла,
     # поэтому при плавающем хостнейме они сходятся, а 41 сессия лежит под другими ярлыками.
     # Истина входа — ФАЙЛЫ НА ДИСКЕ. Прибор, который не видит вход, врёт зелёным.
-    rollouts = unique_sessions_on_disk()
+    rollouts = unique_sessions_on_disk(exclude_ids=exclude_ids)
     mismatch = (rollouts - notes) if rollouts else (total - notes)
     # ⚠️ 07.09: ОТРИЦАТЕЛЬНЫЙ mismatch прибор обязан объяснить сам, а не оставлять загадкой.
     # Заметок БОЛЬШЕ, чем сессий, бывает ровно по одной причине: два файла на один
@@ -553,6 +673,9 @@ def write_freshness(con, machine):
         "machine": machine, "account": account_email(),
         "newest_day": newest, "unique_sessions_on_disk": rollouts, "total_sessions": total,
         "notes_on_disk": notes, "mismatch": mismatch, "stale_days": stale,
+        "external_agent_registry_ids": len(set(exclude_ids or ())),
+        "external_agent_sessions_excluded": excluded_on_disk,
+        "harness_session_import_enabled": bool(harness_import_enabled),
         "duplicate_note_sessions": dupes,
         "mismatch_note": ("лишних заметок-двойников: %d — это и есть отрицательный mismatch"
                           % dupes) if mismatch < 0 else "",
@@ -565,6 +688,8 @@ def write_freshness(con, machine):
 def do_import(sessions_dir=None):
     src = Path(sessions_dir) if sessions_dir else SESSIONS_DIR
     machine = machine_name()
+    external_ids = external_import_ids(src.parent)
+    harness_enabled = harness_session_import_enabled(src.parent / "config.toml")
     # auth.json is the SIBLING of sessions/, not a fixed ~/.codex path: on Mayak the
     # sessions live under /home/dev/.codex while ssh (and therefore this script) runs
     # as root, so a "~"-anchored lookup silently yields account='' and the archive loses
@@ -575,7 +700,7 @@ def do_import(sessions_dir=None):
               f"(это не ошибка, узлу просто нечего отдавать)")
         return 0, 0
     files = sorted(glob.glob(str(src / "**" / "*.jsonl"), recursive=True))
-    rows, skipped = [], 0
+    rows, kept_files, skipped, excluded_on_disk = [], [], 0, 0
     for f in files:
         try:
             with open(f, encoding="utf-8", errors="replace") as fh:
@@ -585,14 +710,28 @@ def do_import(sessions_dir=None):
         if r is None:
             skipped += 1
             continue
+        if r["session_id"] in external_ids:
+            excluded_on_disk += 1
+            continue
         rows.append(r)
+        kept_files.append(f)
+    quarantined = quarantine_external_notes(external_ids)
     con = connect()
+    purged = purge_external_sessions(con, external_ids)
+    missing_rows, missing_notes = reconcile_missing_sources(
+        con, machine, {r["session_id"] for r in rows})
     new, upd, unch = upsert(con, rows)
     written = build_notes(con, machine)
-    copied, dest = archive_originals(files, machine)
-    newest, total, stale = write_freshness(con, machine)
+    copied, dest = archive_originals(kept_files, machine)
+    newest, total, stale = write_freshness(
+        con, machine, exclude_ids=external_ids, excluded_on_disk=excluded_on_disk,
+        harness_import_enabled=harness_enabled)
     print(f"codex import [{machine} / {account or 'unknown'}]: файлов {len(files)}, "
           f"без session_meta пропущено {skipped}")
+    print(f"  provenance: Claude/Harness исключено {excluded_on_disk} на диске / "
+          f"{purged} строк БД / {quarantined} заметок в обратимый карантин")
+    print(f"  reconciliation: исчезнувших native-источников {missing_rows} / "
+          f"заметок в _missing-source {missing_notes}")
     print(f"  DB: +{new} новых / {upd} обновлено / {unch} без изменений | всего {total}")
     print(f"  заметки: {written} -> {notes_dir(machine)}")
     print(f"  оригиналы: +{copied} -> {dest}")
@@ -607,9 +746,11 @@ def do_import(sessions_dir=None):
     unimported = 0
     for f in files:
         sid = _sid_of_file(f)
+        if sid in external_ids:
+            continue
         if sid and sid not in known_sids:
             unimported += 1
-    uniq_in = unique_sessions_on_disk(src)
+    uniq_in = unique_sessions_on_disk(src, exclude_ids=external_ids)
     if unimported:
         print(f"  ⚠️ НЕ ДОЕХАЛО: {unimported} сессий из {src} нет в БД "
               f"(файлов просмотрено {len(files)}, сессий на диске {uniq_in}, заметок {notes_now}).")
@@ -621,7 +762,12 @@ def do_import(sessions_dir=None):
               f"(разница {total - notes_now}). Обычная причина — старые имена/коллизии; "
               f"снеси сырые лишние заметки и прогони import заново.")
     # ненулевой код = ЛЮБОЕ расхождение: и «БД vs заметки», и «файлы на диске vs заметки»
-    return new, upd, max(abs(total - notes_now), abs(gap_in_out))
+    if harness_enabled:
+        print("  ⚠️ HARNESS DRIFT: импорт внешних SESSIONS снова включён в config.toml; "
+              "примесь отфильтрована, но задача красная до выключения переключателя.")
+    result = (new, upd, max(abs(total - notes_now), abs(gap_in_out), int(harness_enabled)))
+    con.close()
+    return result
 
 
 def do_stats():

---

**Claude:**

14:07, вторник, 22 сентября 2026

Читаю реальный файл, а не только diff — иначе вердикт будет claim'ом без улики.

---

> `Bash` -- {"command": "sed -n '1,60p' codex/codex_lib.py", "description": "Read codex_lib.py header"}

---

> `Bash` -- {"command": "sed -n '120,200p' codex/codex_lib.py", "description": "Read unique_sessions_on_disk"}

---

> `Bash` -- {"command": "grep -n \"def connect\\|def notes_dir\\|def build_notes\\|def upsert\\|def parse\\|sessions-dir\\|def main\\|do_import(\" codex/codex_lib.py | head -40"}

---

> `Bash` -- {"command": "sed -n '440,560p' codex/codex_lib.py"}

---

> `Bash` -- {"command": "sed -n '686,790p' codex/codex_lib.py; echo ---; sed -n '985,1015p' codex/codex_lib.py; echo ---; sed -n '370,430p' codex/codex_lib.py"}

---

> `Bash` -- {"command": "grep -rn \"codex_lib\\|do_import\\|unique_sessions_on_disk\\|write_freshness\" --include=*.py --include=*.cmd --include=*.ps1 --include=*.md -l . 2>/dev/null | head -20; echo ===; python -c \"import sqlite3;print(sqlite3.sqlite_version)\""}

---

> `Bash` -- {"command": "cat > /tmp/probe.py <<'EOF'\nimport importlib.util, json, sqlite3, tempfile\nfrom pathlib import Path\nHERE = Path(\"codex\").resolve()\nSPEC = importlib.util.spec_from_file_location(\"cl\", HERE/\"codex_lib.py\")\ncl = importlib.util.module_from_spec(SPEC); SPEC.loader.exec_module(cl)\

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\_scratch\\probe_codex_review.py", "content": "import importlib.util, json, sqlite3, tempfile\nfrom pathlib import Path\nHERE = Path(\"D:/Vault/_imports/codex\")\nSPEC = importlib.util.spec_from_file_location(\"cl\", HERE / \"codex_lib.py\")\ncl = importlib.u

---

> `Bash` -- {"command": "python _scratch/probe_codex_review.py 2>&1 | tail -30", "description": "Run destructive-scenario probe"}

---

**Claude:**

Confirmed one failure empirically. Now the cross-machine / two-homes angle and line numbers.

---

> `Bash` -- {"command": "grep -n \"два дома Codex\\|Маяка\\|mayak\" codex/codex_lib.py | head; echo ===; grep -n \"def reconcile_missing_sources\\|def quarantine_notes\\|def quarantine_external_notes\\|def purge_external_sessions\\|def harness_session_import_enabled\\|def external_import_ids\\|excluded_on_disk\

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\_scratch\\probe_codex_review2.py", "content": "import importlib.util, json, tempfile\nfrom pathlib import Path\nHERE = Path(\"D:/Vault/_imports/codex\")\nSPEC = importlib.util.spec_from_file_location(\"cl\", HERE / \"codex_lib.py\")\ncl = importlib.util.modu

---

> `Bash` -- {"command": "python _scratch/probe_codex_review2.py 2>&1 | tail -10", "description": "Probe cross-machine and body-match quarantine"}

---

> `Bash` -- {"command": "python codex/_test_external_agent_import_filter.py 2>&1 | tail -15; echo \"exit=$?\"", "description": "Run the new test"}

---

> `Bash` -- {"command": "cd D:/Vault/_imports/codex && python codex_lib.py --selftest 2>&1 | tail -6", "description": "Run existing selftest grid"}

---

> `Bash` -- {"command": "cd D:/Vault/_imports && rm -f _scratch/probe_codex_review.py _scratch/probe_codex_review2.py && echo cleaned", "description": "Clean scratch probes"}

---

**Claude:**

**Рельсы:** ревью делаю сам как Claude (суждение + чтение кода); `second_opinion>codex` мимо — автор диффа и есть Codex, отдавать ему ревью его же работы бессмысленно.

# Ревью диффа Codex: `codex_lib.py` + новый тест

Проверял не глазами, а прогонами: запускал новый тест, существующий `--selftest` (32/32 зелёных) и два своих ломателя. Ниже только то, что воспроизвёл.

---

## 🔴 HIGH-1 — `codex/codex_lib.py:601` (`reconcile_missing_sources`) — один прогон по пустому каталогу стирает ВЕСЬ архив узла, и выходит ЗЕЛЁНЫМ

`live_session_ids` — это сессии, распаршенные **в этом прогоне**. Всё, чего в нём не было, удаляется из БД и уносится из полосы. Гарда «сколько допустимо потерять за раз» нет.

Мой прогон (1200 сессий, затем `~/.codex/sessions` опустел):

```
reconciliation: исчезнувших native-источников 1200 / заметок в _missing-source 1200
DB: всего 0        rows left: 0     notes left: 0
import#2: (0, 0, 0)   ← mismatch 0 → main() НЕ даёт exit 3. Тишина.
```

Смысл этого архива — пережить сырые роллауты (`§8.3`, и сам Codex CLI свою историю подчищает). Сейчас архив умирает вместе с ними, молча и с зелёным кодом. Плюс попутно унесло заметку, которую «связал человек» (проверил отдельно — ушла).

**Чинить:** реконсиляция должна судить не по одному проходу, а по факту исчезновения источника (`src_file` строки + возраст), с обязательным капом: если пропало больше N% / > K сессий — НЕ трогать ничего, напечатать красное и вернуть ненулевой код. И `missing_rows > 0` обязан поднимать exit-код, а не печататься в ноль.

## 🔴 HIGH-2 — `codex_lib.py:721` + `main():997` — на Маяке два дома Codex под одной меткой машины → взаимное затирание каждый прогон

Файл сам это документирует на строке 741: *«у Маяка два дома Codex (/root и /home/dev каждый прогон видит свой»*. `machine` при этом один. Значит прогон по `--sessions-dir /root/.codex/sessions` объявит все сессии из `/home/dev` «исчезнувшими» и снесёт их, а следующий прогон снесёт обратные. Это HIGH-1, но не гипотетический, а прямо предсказанный комментарием в том же файле.

**Чинить:** реконсиляцию гейтить по тому же ключу, каким размечен вход (например, только строки, чей `src_file` лежит под текущим `src`), либо не выполнять её вовсе при явном `--sessions-dir`.

## 🟠 HIGH/MED-3 — `codex_lib.py:583` (`quarantine_external_notes`) — карантин без фильтра по машине лезет в папки ЧУЖИХ узлов

`quarantine_notes(..., machine=None)` идёт по всем `01-Conversations/Codex/*`. Проверено: узел `TestNode` унёс заметку из `PeerNode/`.

```
moved pass1: 1
quarantined under PeerNode: ['2026-09-22-peer-note-000000000002.md']
```

Дальше хуже: у PeerNode строка в его БД жива, `build_notes` пересоздаёт заметку при отсутствии файла — и наш узел уносит её снова, каждый раз с новым timestamp-именем (ветка `if dest.exists()`), т.е. бесконечное размножение файлов через Syncthing. Это ломает инвариант, записанный в докстринге этого же файла (строки 11–13): *«Two nodes never write the same note path → no clobber, no lease needed»*. Реестр происхождения локален — значит и карантин обязан быть локален.

**Чинить:** `quarantine_external_notes(ids)` → `quarantine_notes(ids, "_external-agent-imports", machine=machine_name())`.

## 🟠 MED-4 — `codex_lib.py:550` — карантин игнорирует контракт «обогащённое не трогаем», который соседняя функция соблюдает

`sweep_stale_notes:528` проверяет `related_concepts: []` и пропускает связанные человеком заметки («решает человек, не робот»); `--selftest` это прямо закрепляет: *«✅ обогащённого призрака НЕ уносим»*. Новый `quarantine_notes` такой проверки не делает, а `build_notes` перезаписывает только сырые — значит унесённая обогащённая заметка не вернётся сама никогда.

**Чинить:** тот же гейт `related_concepts: []` для `_missing-source` (для `_external-agent-imports` — осознанное исключение, но тогда это надо назвать в докстринге).

## 🟠 MED-5 — `codex_lib.py:568` — `p.read_text` без `try/except OSError` роняет весь импорт

Одна залоченная/нечитаемая `.md` (Windows + Syncthing держит файл) — и `do_import` падает ещё до `connect()`. Соседний `sweep_stale_notes:528` тот же вызов обёрнут. Непоследовательно.

**Чинить:** обернуть тело цикла в `try/except OSError: continue`.

## 🟠 MED-6 — `codex_lib.py:197` (`harness_session_import_enabled`) — сторож дрейфа fail-open на обычном TOML

Регэксп требует `SESSIONS` в той же строке (`[^}\n]*`). Штатная табличная форма проходит мимо:

```toml
[external-agent-import-sync-item-types]
SESSIONS = true
```

Сторож скажет «выключено». Примесь при этом всё ещё фильтруется реестром, поэтому не HIGH — но индикатор врёт зелёным, а это ровно тот класс, против которого написан весь остальной файл.

**Чинить:** `tomllib.load` (stdlib с 3.11), регэксп оставить фолбэком для битого TOML.

## 🟡 MED-7 — `codex_lib.py:703/714/677` — `external_agent_sessions_excluded` считает ФАЙЛЫ, а не сессии

Инкремент идёт в цикле по файлам, а в `_freshness.json` число публикуется как «сессий исключено». `codex resume` даёт несколько файлов на один `session_id` — ровно тот замер (421 файл = 408 сессий), из-за которого написан докстринг `unique_sessions_on_disk:128`.

**Чинить:** копить `set()` исключённых `session_id`, публиковать `len()`.

## 🟡 LOW-8 — `codex_lib.py:601-612` — IN(...) без чанкинга, в отличие от соседа

`purge_external_sessions` бьёт по 500, `reconcile_missing_sources` — нет. На локальном sqlite 3.49 (лимит 32766) 1200 параметров прошли, но на узле с sqlite <3.32 лимит 999 — а сценарий массовой пропажи как раз генерирует сотни id. Честно: на этой машине не воспроизвёл.

## 🟡 LOW-9 — `codex_lib.py:659` (pre-existing, но диффом затронуто) — `unique_sessions_on_disk(exclude_ids=...)` без `src`

Вызов берёт глобальный `SESSIONS_DIR`, поэтому при `--sessions-dir` свежесть мерится по другому каталогу. Дифф добавил сюда `exclude_ids` и мог заодно передать `src`.

## 🟡 LOW-10 — `codex/_test_external_agent_import_filter.py:97-108` — тест закрепляет разрушительное поведение как желаемое

Блок «A vanished native rollout must not survive forever» утверждает, что исчезновение роллаута обязано удалить сессию из БД и унести заметку. Это и есть HIGH-1, зафиксированный как контракт. Нет кейса на обогащённую заметку, нет кейса на заметку чужой машины, нет кейса на кап массового удаления. Сам тест проходит (`PASS`), существующий `--selftest` тоже зелёный — регрессий в старой сетке не внёс.

Также: `do_import:700` возвращает 2-кортеж (`return 0, 0`), а `main():1001` делает `do_import(d)[2]` → IndexError на узле без Codex. Не этот дифф внёс, но теперь это единственная ветка-исключение.

---

**Что в диффе хорошее, чтобы не потерять при переделке:** фильтрация по реестру происхождения с fail-closed на битом JSON (`external_import_ids:168`) — правильная и проверяемая; перенос вместо удаления; сверка по точному `session_id` из фронтматтера, а не по хвосту имени (мой ломатель на «id упомянут в теле заметки» её НЕ унёс — регэксп берёт первое вхождение, т.е. фронтматтер; опасение не подтвердилось).

**Блокеры для мержа:** HIGH-1, HIGH-2, HIGH/MED-3.

⚠️ Два моих ломателя остались в `_imports/_scratch/probe_codex_review*.py` — стереть не дал workspace-lease (`WORKSPACE LEASE BLOCK`). Убрать, когда лиза освободится.

🎙 **Майк:** фильтр примеси — правильная половина работы. Вторая половина, реконсиляция, написана как «истина = этот прогон», и при живом `--sessions-dir` и двух домах Маяка она превращается в рубильник «снести архив», причём зелёный. Это не полировка, это переписать ядро функции.

🧒 **Простыми словами:** Codex сделал фильтр, который не пускает чужие (клодовские) разговоры в папку Codex — это хорошо и работает. Но заодно он добавил уборщика, который рассуждает так: «чего я сегодня не увидел на столе — того больше не существует, выкидываю». Я спрятал все бумажки со стола и запустил: он выкинул все 1200 записей и сказал «всё в порядке». А ещё он лезет убираться в комнату соседнего компьютера, откуда бумажки тут же появляются обратно — и так по кругу.

VERDICT: REQUEST_CHANGES
