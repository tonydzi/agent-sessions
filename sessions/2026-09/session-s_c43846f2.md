---
session: s_c43846f2
date: 2026-09-23
words: 8329
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c43846f2` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
diff --git a/_paths.py b/_paths.py
index 7f910a70..016a5ffd 100644
--- a/_paths.py
+++ b/_paths.py
@@ -23,7 +23,10 @@ on a Mac/other-user box.
 починку и вводила в заблуждение при планировании раскатки ([[prose-about-code-outlives-the-fix]]).
 One-time import scripts are FROZEN historical artifacts (won't run cross-OS) -> not refactored.
 """
+import json
 import os
+import re
+import socket
 
 
 def _home():
@@ -82,6 +85,41 @@ PYTHON_EXE = get("PYTHON_EXE", "python")
 SECRETS = get("SECRETS_DIR", os.path.join(_home(), "!CLAUDE-NODE-0X May26", "secrets"))
 
 
+def canonical_machine(value):
+    """Resolve key/hostname/alias to the fleet registry key; unknown safe keys use lowercase."""
+    raw = (value or "").strip()
+    safe = re.compile(r"[A-Za-z0-9][A-Za-z0-9._-]*\Z")
+    if not raw or raw in (".", "..") or not safe.fullmatch(raw):
+        raise ValueError("unsafe MACHINE_KEY: %r" % value)
+    folded = raw.casefold()
+    registry = os.path.join(_home(), ".claude", "fleet_nodes.json")
+    try:
+        with open(registry, encoding="utf-8") as fh:
+            doc = json.load(fh)
+    except FileNotFoundError:
+        return raw.lower()
+    except json.JSONDecodeError as exc:
+        raise ValueError("corrupt fleet_nodes.json: %s" % exc) from exc
+    if not isinstance(doc, dict) or not isinstance(doc.get("nodes", {}), dict):
+        raise ValueError("corrupt fleet_nodes.json: nodes must be an object")
+    for key, meta in doc.get("nodes", {}).items():
+        if not isinstance(meta, dict):
+            raise ValueError("corrupt fleet node %r: metadata must be an object" % key)
+        names = [key, meta.get("hostname", "")] + list(meta.get("aliases") or [])
+        if any(str(name).casefold() == folded for name in names if name):
+            if key in (".", "..") or not safe.fullmatch(str(key)):
+                raise ValueError("unsafe registry MACHINE_KEY: %r" % key)
+            return str(key).lower()
+    return raw.lower()
+
+
+def machine_key():
+    """One machine identity for DB keys, note/original lanes, and freshness filenames."""
+    raw = os.environ.get("MACHINE_KEY") or _ENV.get("MACHINE_KEY") \
+        or os.environ.get("COMPUTERNAME") or socket.gethostname()
+    return canonical_machine(raw)
+
+
 # --- ORIGINALS: hub CANON vs peer DELIVERY WINDOW (root fix 2026-07-28) ---------------
 # D:\Vault\_originals (== dirname(VAULT)/_originals) is HUB-LOCAL and is NOT a Syncthing
 # share on ANY machine -- verified live on the hub 2026-07-28 (10 folders, none of them
diff --git a/codex/_test_external_agent_import_filter.py b/codex/_test_external_agent_import_filter.py
index aa66001d..60e948f9 100644
--- a/codex/_test_external_agent_import_filter.py
+++ b/codex/_test_external_agent_import_filter.py
@@ -1,5 +1,5 @@
 # -*- coding: utf-8 -*-
-"""Regression: Claude sessions imported by Codex Harness never enter the Codex lane."""
+"""Regression: every thread ID recorded by Harness as external stays out of the Codex lane."""
 import importlib.util
 import json
 import sqlite3
@@ -26,16 +26,23 @@ def rollout(path, sid, prompt):
     path.write_text("\n".join(json.dumps(x) for x in rows), encoding="utf-8")
 
 
-def registry(path, imported_sid):
-    path.write_text(json.dumps({"records": [{
-        "source_path": "C:/Users/dev/.claude/projects/source.jsonl",
-        "imported_thread_id": imported_sid,
-    }]}), encoding="utf-8")
+def registry(path, records):
+    path.write_text(json.dumps({"records": [
+        {"source_path": source_path, "imported_thread_id": sid}
+        for source_path, sid in records
+    ]}), encoding="utf-8")
 
 
 def run():
     genuine = "s_546cd47d"
     imported = "s_4942c078"
+    imported_grok = "s_0c39ebc0"
+    imported_cursor = "s_4aa7422b"
+    foreign = [
+        ("C:/Users/dev/.claude/projects/source.jsonl", imported),
+        ("C:/Users/dev/.grok/sessions/source.jsonl", imported_grok),
+        ("C:/Users/dev/.cursor/projects/source.jsonl", imported_cursor),
+    ]
     with tempfile.TemporaryDirectory() as td_raw:
         td = Path(td_raw)
         root = td / ".codex"
@@ -44,7 +51,9 @@ def run():
         rollout(sessions / "2026/09/22/rollout-genuine.jsonl", genuine, "genuine Codex")
         rollout(sessions / "2026/09/22/rollout-imported.jsonl", imported, "from Claude")
         rollout(sessions / "2026/09/22/rollout-imported-resume.jsonl", imported, "from Claude resumed")
-        registry(root / "external_agent_session_imports.json", imported)
+        rollout(sessions / "2026/09/22/rollout-imported-grok.jsonl", imported_grok, "from Grok")
+        rollout(sessions / "2026/09/22/rollout-imported-cursor.jsonl", imported_cursor, "from Cursor")
+        registry(root / "external_agent_session_imports.json", foreign)
         (root / "config.toml").write_text(
             "external-agent-import-sync-enabled = false\n"
             "external-agent-import-sync-item-types = { SESSIONS = false }\n",
@@ -70,7 +79,8 @@ def run():
             assert len(notes) == 1 and f"session_id: {genuine}" in notes[0].read_text(encoding="utf-8")
             fresh = json.loads(codex_lib.freshness_path("TestNode").read_text(encoding="utf-8"))
             assert fresh["unique_sessions_on_disk"] == 1
-            assert fresh["external_agent_sessions_excluded"] == 1
+            assert fresh["external_agent_registry_ids"] == 3
+            assert fresh["external_agent_sessions_excluded"] == 3
             assert fresh["unimported_sessions"] == 0
 
             # Historical contamination must be moved, never deleted, and removed from DB.
@@ -132,7 +142,7 @@ def run():
                 raise AssertionError("malformed external import registry did not fail closed")
 
             # Harness drift back to ON is a visible non-zero health result.
-            registry(root / "external_agent_session_imports.json", imported)
+            registry(root / "external_agent_session_imports.json", foreign)
             (root / "config.toml").write_text(
                 "external-agent-import-sync-enabled = false\n"
                 "[external-agent-import-sync-item-types]\nSESSIONS = true\n",
@@ -150,4 +160,4 @@ def run():
 
 if __name__ == "__main__":
     run()
-    print("PASS: external-agent imports are excluded and quarantined")
+    print("PASS: all Harness external-thread IDs are excluded and quarantined")
diff --git a/codex/codex_lib.py b/codex/codex_lib.py
index 27c65581..bf3cac34 100644
--- a/codex/codex_lib.py
+++ b/codex/codex_lib.py
@@ -198,7 +198,7 @@ def external_import_ids(codex_root):
 
 
 def harness_session_import_enabled(config_path):
-    """Cheap drift guard for the two Harness switches that can import Claude sessions."""
+    """Cheap drift guard for Harness switches that can import another agent's sessions."""
     p = Path(config_path)
     if not p.exists():
         return False
@@ -778,7 +778,7 @@ def do_import(sessions_dir=None):
         harness_import_enabled=harness_enabled, unimported_sessions=unimported)
     print(f"codex import [{machine} / {account or 'unknown'}]: файлов {len(files)}, "
           f"без session_meta пропущено {skipped}")
-    print(f"  provenance: Claude/Harness исключено {len(excluded_ids_on_disk)} сессий на диске / "
+    print(f"  provenance: external-agent/Harness исключено {len(excluded_ids_on_disk)} сессий на диске / "
           f"{purged} строк БД / {quarantined} заметок в обратимый карантин")
     print(f"  DB: +{new} новых / {upd} обновлено / {unch} без изменений | всего {total}")
     print(f"  заметки: {written} -> {notes_dir(machine)}")
diff --git a/cursor/_test_cursor.py b/cursor/_test_cursor.py
new file mode 100644
index 00000000..3ffe5d6c
--- /dev/null
+++ b/cursor/_test_cursor.py
@@ -0,0 +1,198 @@
+# -*- coding: utf-8 -*-
+"""Isolated regression for Cursor provenance: two machines, same id, no clobber."""
+import json
+import os
+import shutil
+import sqlite3
+import tempfile
+from pathlib import Path
+
+import cursor_lib as C
+REAL_MACHINE_NAME = C.machine_name
+
+
+TMP = Path(tempfile.mkdtemp(prefix="cursor-provenance-"))
+FAILS = []
+
+
+def check(name, condition):
+    print(("  ok " if condition else "FAIL ") + name)
+    if not condition:
+        FAILS.append(name)
+
+
+def fixture(root, sid, question="проверь синк", answer="Смотрю.", with_timestamp=True):
+    d = root / "proj-x" / "agent-transcripts" / sid
+    d.mkdir(parents=True, exist_ok=True)
+    p = d / (sid + ".jsonl")
+    prefix = "<timestamp>Tuesday, Sep 22, 2026, 12:48 PM (UTC+1)</timestamp>" if with_timestamp else ""
+    rows = [
+        {"role": "user", "message": {"content": [{"type": "text", "text":
+            prefix + "<user_query>%s</user_query>" % question}]}},
+        {"role": "assistant", "message": {"content": [{"type": "text", "text": answer}]}},
+    ]
+    p.write_text("\n".join(json.dumps(x, ensure_ascii=False) for x in rows), encoding="utf-8")
+    return p
+
+
+try:
+    C.VAULT = TMP / "vault"
+    C.ORIGINALS_ROOT = TMP / "originals"
+    C.DB = TMP / "cursor.db"
+    C.DB_ROOT = TMP / "db-shards"
+    C.FRESHNESS_ROOT = TMP / "freshness"
+    C.FRESHNESS = TMP / "legacy-freshness.json"
+    old_machine_env = os.environ.get("MACHINE_KEY")
+    try:
+        os.environ["MACHINE_KEY"] = "Node-A"
+        check("machine resolver canonicalizes case", REAL_MACHINE_NAME() == C._paths.canonical_machine("Node-A"))
+        os.environ["MACHINE_KEY"] = ".."
+        try:
+            REAL_MACHINE_NAME()
+        except ValueError:
+            pass
+        else:
+            check("machine resolver rejects traversal", False)
+    finally:
+        if old_machine_env is None:
+            os.environ.pop("MACHINE_KEY", None)
+        else:
+            os.environ["MACHINE_KEY"] = old_machine_env
+    source = TMP / "source"
+    sid = "same-session-id"
+    fixture(source, sid)
+
+    node_a = C._paths.canonical_machine("Node-A")
+    node_b = C._paths.canonical_machine("Node-B")
+    db_a, db_b = TMP / "node-a.db", TMP / "node-b.db"
+    C.machine_name = lambda: node_a
+    check("Node-A import", C.do_import(source, db=db_a) == 0)
+    C.machine_name = lambda: node_b
+    check("Node-B import", C.do_import(source, db=db_b) == 0)
+
+    con_a, con_b = sqlite3.connect(db_a), sqlite3.connect(db_b)
+    check("same session id stays in two producer DB shards",
+          con_a.execute("SELECT COUNT(*) FROM sessions").fetchone()[0] == 1
+          and con_b.execute("SELECT COUNT(*) FROM sessions").fetchone()[0] == 1)
+    C.machine_name = lambda: C._paths.canonical_machine("node-a")
+    C.do_import(source, db=db_a)
+    check("machine-name case drift stays in one DB and one path lane",
+          con_a.execute("SELECT COUNT(*) FROM sessions").fetchone()[0] == 1
+          and len(list((C.VAULT / "01-Conversations" / "Cursor" / node_a).glob("*.md"))) == 1)
+    C.machine_name = lambda: node_b
+    check("notes are in separate producer lanes",
+          len(list((C.VAULT / "01-Conversations" / "Cursor" / node_a).glob("*.md"))) == 1
+          and len(list((C.VAULT / "01-Conversations" / "Cursor" / node_b).glob("*.md"))) == 1)
+    check("freshness is per machine",
+          C.freshness_path(node_a).exists() and C.freshness_path(node_b).exists()
+          and C.freshness_path(node_a) != C.freshness_path(node_b))
+    try:
+        C.freshness_path("Node A")
+    except ValueError:
+        unsafe_rejected = True
+    else:
+        unsafe_rejected = False
+    check("unsafe machine key fails closed", unsafe_rejected)
+    for unsafe in (".", ".."):
+        try:
+            C.freshness_path(unsafe)
+        except ValueError:
+            pass
+        else:
+            check("dot path rejected: " + unsafe, False)
+    f = json.loads(C.freshness_path(node_b).read_text(encoding="utf-8"))
+    check("freshness proves input=DB=notes", f["unique_input_sessions"] == 1
+          and f["durable_db_sessions"] == 1 and f["durable_notes"] == 1
+          and f["mismatch"] == 0)
+
+    # Same message count, changed bytes: msg_count-only comparison used to lie unchanged.
+    fixture(source, sid, answer="Уже проверил.")
+    C.do_import(source, db=db_b)
+    body = next((C.VAULT / "01-Conversations" / "Cursor" / node_b).glob("*.md")).read_text(encoding="utf-8")
+    check("same-count content change rewrites raw note", "Уже проверил." in body)
+    check("user text is not falsely attributed to dev", "driver: unknown" in body
+          and "account: unknown" in body)
+
+    note = next((C.VAULT / "01-Conversations" / "Cursor" / node_b).glob("*.md"))
+    note.unlink()
+    C.do_import(source, db=db_b)
+    check("missing Cursor note self-heals from unchanged source", note.exists())
+
+    # Linked note becomes human-owned and must survive a later source refresh.
+    linked = note.read_text(encoding="utf-8").replace("related_concepts: []",
+                                                       "related_concepts: [kept]")
+    note.write_text(linked, encoding="utf-8")
+    fixture(source, sid, answer="Третья версия.")
+    linked_rc = C.do_import(source, db=db_b)
+    linked_fresh = json.loads(C.freshness_path(node_b).read_text(encoding="utf-8"))
+    check("linked note is preserved", "related_concepts: [kept]" in note.read_text(encoding="utf-8")
+          and "Третья версия." not in note.read_text(encoding="utf-8"))
+    check("linked stale note is visible and red",
+          linked_rc == 3 and sid in linked_fresh["stale_note_ids"])
+    note.write_text(note.read_text(encoding="utf-8") + "\nrelated_concepts: []\n", encoding="utf-8")
+    fixture(source, sid, answer="Четвёртая версия.")
+    C.do_import(source, db=db_b)
+    check("body marker cannot overwrite human-owned note",
+          "Четвёртая версия." not in note.read_text(encoding="utf-8"))
+
+    # Old seven-column DB had no content hash. First upgrade adopts the current raw note.
+    legacy_db = TMP / "legacy.db"
+    legacy_source = TMP / "legacy-source"
+    legacy_sid = "legacy-session-id"
+    legacy_file = fixture(legacy_source, legacy_sid, answer="source answer")
+    parsed = C.parse_transcript(legacy_file)
+    C.machine_name = lambda: "LegacyNode"
+    legacy_note_dir = C.VAULT / "01-Conversations" / "Cursor" / "LegacyNode"
+    legacy_note_dir.mkdir(parents=True)
+    legacy_note = legacy_note_dir / ("%s-%s-%s.md" %
+                                     (parsed["date"], C._slug(parsed["title"]), legacy_sid[-12:]))
+    legacy_note.write_text("---\nsource: cursor\nrelated_concepts: []\n---\nKEEP HUMAN TEXT\n",
+                           encoding="utf-8")
+    legacy = sqlite3.connect(legacy_db)
+    legacy.execute("CREATE TABLE sessions(session_id TEXT PRIMARY KEY,machine TEXT,date TEXT,"
+                   "title TEXT,project TEXT,msg_count INT,src_file TEXT)")
+    legacy.execute("INSERT INTO sessions VALUES(?,?,?,?,?,?,?)",
+                   (legacy_sid, "LegacyNode", parsed["date"], parsed["title"], "proj-x", 2,
+                    str(legacy_file)))
+    legacy.commit(); legacy.close()
+    legacy_rc = C.do_import(legacy_source, db=legacy_db)
+    migrated = sqlite3.connect(legacy_db)
+    stored_hash = migrated.execute("SELECT content_hash FROM sessions").fetchone()[0]
+    migrated.close()
+    check("legacy migration records hash without rewriting existing raw note",
+          bool(stored_hash) and "KEEP HUMAN TEXT" in legacy_note.read_text(encoding="utf-8"))
+    check("unverified legacy note is visible and red", legacy_rc == 3)
+
+    fallback_source = TMP / "fallback-source"
+    fallback_sid = "fallback-date-session"
+    fallback_file = fixture(fallback_source, fallback_sid, answer="first", with_timestamp=False)
+    fallback_db = TMP / "fallback.db"
+    C.machine_name = lambda: "fallback-node"
+    C.do_import(fallback_source, db=fallback_db)
+    import os as _os, time as _time
+    fixture(fallback_source, fallback_sid, answer="second", with_timestamp=False)
+    _os.utime(fallback_file, (_time.time() + 172800, _time.time() + 172800))
+    C.do_import(fallback_source, db=fallback_db)
+    check("Cursor mtime fallback cannot fork one session into two notes",
+          len(list((C.VAULT / "01-Conversations" / "Cursor" / "fallback-node").glob("*.md"))) == 1)
+
+    legacy_db = TMP / "legacy-shared.db"
+    legacy = sqlite3.connect(legacy_db)
+    legacy.execute("CREATE TABLE sessions(machine TEXT, session_id TEXT, date TEXT, title TEXT, "
+                   "project TEXT, msg_count INT, src_file TEXT, PRIMARY KEY(machine,session_id))")
+    legacy.execute("INSERT INTO sessions VALUES(?,?,?,?,?,?,?)",
+                   ("seed-node", "legacy-id", "2026-09-20", "old", "p", 1, "old.jsonl"))
+    legacy.commit(); legacy.close()
+    C.DB = legacy_db
+    seeded = C._production_db("seed-node")
+    migrated = C._connect(seeded)
+    check("legacy shared DB is preserved and seeds producer shard",
+          legacy_db.exists() and seeded.exists()
+          and migrated.execute("SELECT COUNT(*) FROM sessions").fetchone()[0] == 1)
+    migrated.close()
+finally:
+    shutil.rmtree(TMP, ignore_errors=True)
+
+if FAILS:
+    raise SystemExit("FAIL: " + ", ".join(FAILS))
+print("PASS: Cursor producer lanes and provenance")
diff --git a/cursor/cursor_lib.py b/cursor/cursor_lib.py
index 3a3579fb..4e30d065 100644
--- a/cursor/cursor_lib.py
+++ b/cursor/cursor_lib.py
@@ -16,8 +16,8 @@ session_meta нет; id сессии = имя папки, дата = тег <tim
 ЧТО РОЖДАЕТСЯ (те же 4 шага, что у всех трубн волта, §8.3):
     1. оригинал verbatim -> _originals/cursor-sessions/<МАШИНА>/ (идемпотентно);
     2. заметка -> 01-Conversations/Cursor/<МАШИНА>/<дата>-<slug>-<id12>.md;
-    3. SQLite cursor_sessions.db (upsert по session_id, обновление по msg_count);
-    4. _freshness.json -- пульс для сторожей.
+    3. SQLite _db/<MACHINE_KEY>.db (один producer, один writer; content_hash);
+    4. _freshness/<МАШИНА>.json -- отдельный пульс каждого producer-узла.
 Индексы подхватывают сами: brain_evidence ночью (сырьё), brain_sessions_index
 (Книга чатов, корень добавлен 22.09), distill_queue (SESSION_SOURCES).
 
@@ -26,7 +26,7 @@ USAGE
     python cursor_lib.py stats        # что в базе
     python cursor_lib.py selftest     # на синтетическом транскрипте, волт не трогает
 """
-import os, re, sys, json, glob, sqlite3, shutil, datetime
+import os, re, sys, json, glob, sqlite3, shutil, datetime, hashlib, socket
 from pathlib import Path
 
 try:
@@ -37,29 +37,68 @@ except Exception:
 
 _HERE = Path(__file__).resolve().parent
 sys.path.insert(0, str(_HERE.parent))
+sys.path.insert(0, str(Path.home() / '.claude' / 'scripts' / '_shared'))
 try:
-    from _paths import VAULT as _VAULT
-    VAULT = Path(_VAULT)
+    import menv
+    VAULT = Path(menv.vault())
 except Exception:
-    VAULT = Path(r'D:\Vault\Vault-Knowledge')
+    menv = None
+    try:
+        from _paths import VAULT as _VAULT
+        VAULT = Path(_VAULT)
+    except Exception:
+        VAULT = Path(r'D:\Vault\Vault-Knowledge')
+try:
+    import _paths
+    ORIGINALS_ROOT = Path(_paths.originals_root())
+except Exception:
+    ORIGINALS_ROOT = VAULT / '_originals'
 
 CURSOR_ROOT = Path(os.path.expanduser('~/.cursor/projects'))
 DB = _HERE / 'cursor_sessions.db'
-FRESHNESS = _HERE / '_freshness.json'
+DB_ROOT = _HERE / '_db'
+FRESHNESS_ROOT = _HERE / '_freshness'
+FRESHNESS = _HERE / '_freshness.json'  # deprecated sentinel path; must stay absent
 
 
 def machine_name():
-    """MACHINE_NAME из ~/.claude/machine.env -- та же истина, что у codex_lib/_paths."""
-    p = os.path.expanduser('~/.claude/machine.env')
-    try:
-        with open(p, encoding='utf-8') as fh:
-            for line in fh:
-                line = line.strip()
-                if line.startswith('MACHINE_NAME=') and not line.startswith('#'):
-                    return line.split('=', 1)[1].split('#', 1)[0].strip().strip('\'"')
-    except OSError:
-        pass
-    return os.environ.get('COMPUTERNAME') or os.uname().nodename
+    """Use the fleet-wide resolver; one precedence order for every agent exporter."""
+    resolver = getattr(globals().get('_paths'), 'machine_key', None)
+    if resolver:
+        return resolver()
+    if menv is not None:
+        raw = menv.machine_key(socket.gethostname())
+    else:
+        raw = os.environ.get('MACHINE_KEY') or os.environ.get('COMPUTERNAME') or socket.gethostname()
+    if not re.fullmatch(r'[A-Za-z0-9._-]+', raw):
+        raise ValueError('unsafe MACHINE_KEY: %r' % raw)
+    return raw.lower()
+
+
+def db_path(machine):
+    # One SQLite writer per file. Notes sync fleet-wide; databases are producer shards.
+    return DB_ROOT / (machine + '.db')
+
+
+def freshness_path(machine):
+    """Один producer = один файл; общий heartbeat в Syncthing снова сделал бы last-writer-wins."""
+    raw = (machine or '').strip()
+    if not raw or raw in ('.', '..') or not re.fullmatch(r'[A-Za-z0-9][A-Za-z0-9._-]*', raw):
+        raise ValueError('unsafe MACHINE_KEY for freshness path: %r' % machine)
+    return FRESHNESS_ROOT / (raw + '.json')
+
+
+def _same_file(src, dst):
+    """Compare exact bytes; synced filesystems do not preserve nanosecond mtimes reliably."""
+    if not dst.exists() or dst.stat().st_size != src.stat().st_size:
+        return False
+    def digest(path):
+        h = hashlib.sha256()
+        with open(path, 'rb') as fh:
+            for chunk in iter(lambda: fh.read(1024 * 1024), b''):
+                h.update(chunk)
+        return h.digest()
+    return digest(src) == digest(dst)
 
 
 def _clean(s):
@@ -91,7 +130,7 @@ def _date_of(ts_text, path):
 
 
 def parse_transcript(path):
-    """-> dict(session_id, date, title, project, body_md, msg_count) или None (пустой)."""
+    """-> нормализованная сессия или None. Инъекции Cursor не выдаём за слова оператора."""
     p = Path(path)
     sid = p.stem
     project = p.parent.parent.parent.name if p.parent.parent.parent else '?'
@@ -132,81 +171,242 @@ def parse_transcript(path):
         return None
     title = (first_user or 'cursor session')[:120]
     body = '\n\n'.join('%s\n\n%s' % (who, what) for who, what in turns if what)
+    content_hash = hashlib.sha256(body.encode('utf-8')).hexdigest()
     return dict(session_id=sid, date=_date_of(ts_text, path), title=title,
-                project=project, body_md=body, msg_count=len(turns), src_file=str(p))
+                project=project, body_md=body, msg_count=len(turns),
+                content_hash=content_hash, src_file=str(p))
 
 
 def note_text(r, machine):
     return ('---\n'
             'title: "%s"\n'
             'type: ai-conversation\nstage: raw\nsource: cursor\n'
-            'machine: %s\norigin: mixed\nauthored_by: hybrid\n'
+            'machine: %s\naccount: unknown\norigin: mixed\nauthored_by: hybrid\n'
             'session_id: %s\ndate_recorded: %s\ndate_added: %s\n'
-            'project: "%s"\ndriver: human\nlanguage: ru\n'
+            'project: "%s"\ndriver: unknown\nlanguage: ru\n'
             'tags: [ai-conversation, archive, cursor]\nmsg_count: %d\n'
+            'source_hash: %s\n'
             'related_concepts: []\n---\n\n# %s\n\n%s\n'
             % (r['title'].replace('"', "'"), machine, r['session_id'], r['date'],
                datetime.date.today().isoformat(), r['project'], r['msg_count'],
-               r['title'], r['body_md']))
+               r['content_hash'], r['title'], r['body_md']))
+
+
+def _connect(db=None):
+    """Открыть DB и атомарно поднять старую одноузловую схему до machine+session_id."""
+    target = Path(db or DB)
+    target.parent.mkdir(parents=True, exist_ok=True)
+    con = sqlite3.connect(str(target))
+    con.execute('PRAGMA journal_mode=DELETE')
+    cols = {row[1] for row in con.execute('PRAGMA table_info(sessions)')}
+    schema_row = con.execute(
+        "SELECT sql FROM sqlite_master WHERE type='table' AND name='sessions'").fetchone()
+    schema_sql = (schema_row[0] if schema_row else '') or ''
+    machine_nocase = bool(re.search(r'(?i)\bmachine\s+TEXT\s+COLLATE\s+NOCASE\b', schema_sql))
+    needs_migration = cols and ('content_hash' not in cols or 'exported_at' not in cols
+                                or not machine_nocase)
+    if needs_migration:
+        if con.execute("SELECT 1 FROM sqlite_master WHERE type='table' AND name='sessions_legacy'").fetchone():
+            raise RuntimeError('sessions_legacy already exists; refusing ambiguous DB migration')
+        try:
+            con.execute('BEGIN IMMEDIATE')
+            con.execute('ALTER TABLE sessions RENAME TO sessions_legacy')
+            con.execute('CREATE TABLE sessions ('
+                        'machine TEXT COLLATE NOCASE NOT NULL, session_id TEXT NOT NULL, date TEXT, title TEXT, '
+                        'project TEXT, msg_count INT, content_hash TEXT, src_file TEXT, exported_at TEXT, '
+                        'PRIMARY KEY(machine, session_id))')
+            legacy = {row[1] for row in con.execute('PRAGMA table_info(sessions_legacy)')}
+            if {'content_hash', 'exported_at'} <= legacy:
+                con.execute('INSERT OR REPLACE INTO sessions '
+                            '(machine,session_id,date,title,project,msg_count,content_hash,src_file,exported_at) '
+                            "SELECT machine,session_id,date,title,project,msg_count,content_hash,src_file,exported_at "
+                            "FROM sessions_legacy ORDER BY CASE WHEN COALESCE(content_hash,'')='' THEN 0 ELSE 1 END")
+            else:
+                con.execute('INSERT OR IGNORE INTO sessions '
+                            '(machine,session_id,date,title,project,msg_count,content_hash,src_file,exported_at) '
+                            "SELECT machine,session_id,date,title,project,msg_count,'',src_file,'' "
+                            'FROM sessions_legacy')
+            con.execute('DROP TABLE sessions_legacy')
+            con.commit()
+        except Exception:
+            con.rollback()
+            raise
+    elif not cols:
+        con.execute('CREATE TABLE sessions ('
+                    'machine TEXT COLLATE NOCASE NOT NULL, session_id TEXT NOT NULL, date TEXT, title TEXT, '
+                    'project TEXT, msg_count INT, content_hash TEXT, src_file TEXT, exported_at TEXT, '
+                    'PRIMARY KEY(machine, session_id))')
+        con.commit()
+    return con
+
+
+def _raw_note_ids(machine):
+    d = VAULT / '01-Conversations' / 'Cursor' / machine
+    if not d.exists():
+        return set()
+    ids = set()
+    for p in d.glob('*.md'):
+        frontmatter = _frontmatter(p)
+        if not re.search(r'(?m)^source:\s*cursor\s*$', frontmatter):
+            continue
+        match = re.search(r'(?m)^session_id:\s*(\S+)\s*$', frontmatter)
+        if match:
+            ids.add(match.group(1))
+    return ids
+
+
+def _frontmatter(path):
+    """Read only YAML frontmatter, without mistaking transcript-body markers for metadata."""
+    lines = []
+    with open(path, encoding='utf-8', errors='ignore') as fh:
+        if fh.readline().strip() != '---':
+            return ''
+        for line in fh:
+            if line.strip() == '---':
+                return ''.join(lines)
+            lines.append(line)
+            if sum(map(len, lines)) > 65536:
+                return ''
+    return ''
+
+
+def _machine_owned_note(path):
+    frontmatter = _frontmatter(path)
+    return bool(re.search(r'(?m)^source:\s*cursor\s*$', frontmatter)
+                and re.search(r'(?m)^stage:\s*raw\s*$', frontmatter)
+                and re.search(r'(?m)^related_concepts:\s*\[\]\s*$', frontmatter))
 
 
-def do_import(root=None):
+def _note_session_id(path):
+    match = re.search(r'(?m)^session_id:\s*(\S+)\s*$', _frontmatter(path))
+    return match.group(1) if match else ''
+
+
+def _note_source_hash(path):
+    match = re.search(r'(?m)^source_hash:\s*([0-9a-f]{64})\s*$', _frontmatter(path))
+    return match.group(1) if match else ''
+
+
+def _collision_safe_note(preferred, session_id):
+    if not preferred.exists() or _note_session_id(preferred) in ('', session_id):
+        return preferred
+    suffix = hashlib.sha256(session_id.encode('utf-8')).hexdigest()[:8]
+    return preferred.with_name(preferred.stem + '-' + suffix + preferred.suffix)
+
+
+def _production_db(machine):
+    """Seed a producer shard once; keep the historical shared DB untouched."""
+    target = db_path(machine)
+    if not target.exists() and DB.exists():
+        target.parent.mkdir(parents=True, exist_ok=True)
+        shutil.copy2(DB, target)
+    return target
+
+
+def do_import(root=None, *, db=None):
     src = Path(root) if root else CURSOR_ROOT
     machine = machine_name()
     if not src.is_dir():
         print('cursor: НЕТ каталога %s -- Cursor на этой машине не ставился (узлу нечего отдавать)' % src)
         return 0
     files = sorted(glob.glob(str(src / '*' / 'agent-transcripts' / '*' / '*.jsonl')))
-    con = sqlite3.connect(DB)
-    con.execute('CREATE TABLE IF NOT EXISTS sessions (session_id TEXT PRIMARY KEY, machine TEXT,'
-                ' date TEXT, title TEXT, project TEXT, msg_count INT, src_file TEXT)')
+    con = _connect(db or _production_db(machine))
+    # NOCASE prevents a duplicate identity; keep the displayed spelling equal to MACHINE_KEY.
+    con.execute('UPDATE sessions SET machine=? WHERE machine=? COLLATE NOCASE', (machine, machine))
+    con.commit()
     d_notes = VAULT / '01-Conversations' / 'Cursor' / machine
-    d_orig = VAULT.parent / '_originals' / 'cursor-sessions' / machine
+    d_orig = ORIGINALS_ROOT / 'cursor-sessions' / machine
     d_notes.mkdir(parents=True, exist_ok=True)
     d_orig.mkdir(parents=True, exist_ok=True)
     new = upd = unch = copied = 0
+    input_ids = set()
     for f in files:
         r = parse_transcript(f)
         if r is None:
             continue
+        input_ids.add(r['session_id'])
         # оригинал verbatim (идемпотентно, по имени файла)
         dst = d_orig / Path(f).name
-        if not dst.exists() or dst.stat().st_size != os.path.getsize(f):
+        if not _same_file(Path(f), dst):
             shutil.copy2(f, dst)
             copied += 1
-        old = con.execute('SELECT msg_count FROM sessions WHERE session_id=?',
-                          (r['session_id'],)).fetchone()
-        if old and old[0] == r['msg_count']:
+        old = con.execute('SELECT content_hash,date,title FROM sessions WHERE machine=? AND session_id=?',
+                          (machine, r['session_id'])).fetchone()
+        if old and old[1]:
+            r['date'] = old[1]
+        if old and old[2]:
+            r['title'] = old[2]
+        preferred = d_notes / ('%s-%s-%s.md' % (r['date'], _slug(r['title']), r['session_id'][-12:]))
+        note = _collision_safe_note(preferred, r['session_id'])
+        if (old and old[0] == r['content_hash'] and note.exists()
+                and _note_source_hash(note) == r['content_hash']):
             unch += 1
             continue
-        con.execute('INSERT INTO sessions VALUES (?,?,?,?,?,?,?) ON CONFLICT(session_id) DO UPDATE'
-                    ' SET msg_count=excluded.msg_count, title=excluded.title',
-                    (r['session_id'], machine, r['date'], r['title'], r['project'],
-                     r['msg_count'], r['src_file']))
-        note = d_notes / ('%s-%s-%s.md' % (r['date'], _slug(r['title']), r['session_id'][-12:]))
+        now = datetime.datetime.now(datetime.timezone.utc).isoformat()
+        con.execute('INSERT INTO sessions VALUES (?,?,?,?,?,?,?,?,?) '
+                    'ON CONFLICT(machine,session_id) DO UPDATE SET '
+                    'date=excluded.date,title=excluded.title,project=excluded.project,'
+                    'msg_count=excluded.msg_count,content_hash=excluded.content_hash,'
+                    'src_file=excluded.src_file,exported_at=excluded.exported_at',
+                    (machine, r['session_id'], r['date'], r['title'], r['project'],
+                     r['msg_count'], r['content_hash'], r['src_file'], now))
+        if note.exists():
+            if not _machine_owned_note(note):
+                # Linked/enriched note is human-owned; DB still records the fresh source.
+                new += 0 if old else 1
+                upd += 1 if old else 0
+                continue
         note.write_text(note_text(r, machine), encoding='utf-8')
         new += 0 if old else 1
         upd += 1 if old else 0
     con.commit()
-    newest = con.execute('SELECT MAX(date) FROM sessions').fetchone()[0] or ''
-    total = con.execute('SELECT COUNT(*) FROM sessions').fetchone()[0]
+    newest = con.execute('SELECT MAX(date) FROM sessions WHERE machine=?', (machine,)).fetchone()[0] or ''
+    total = con.execute('SELECT COUNT(*) FROM sessions WHERE machine=?', (machine,)).fetchone()[0]
     stale = (datetime.date.today() - datetime.date.fromisoformat(newest)).days if newest else -1
-    FRESHNESS.write_text(json.dumps(dict(
+    db_hashes = dict(con.execute(
+        'SELECT session_id,content_hash FROM sessions WHERE machine=?', (machine,)))
+    db_ids = set(db_hashes)
+    note_ids = _raw_note_ids(machine)
+    durable_notes = len(db_ids & note_ids)
+    note_by_id = {}
+    for candidate in d_notes.glob('*.md'):
+        sid = _note_session_id(candidate)
+        if sid in db_ids:
+            note_by_id.setdefault(sid, candidate)
+    missing_ids = sorted(db_ids - set(note_by_id))
+    stale_ids = sorted(sid for sid, path in note_by_id.items()
+                       if _note_source_hash(path) and _note_source_hash(path) != db_hashes[sid])
+    unverified_ids = sorted(sid for sid, path in note_by_id.items()
+                            if not _note_source_hash(path) and not _machine_owned_note(path))
+    fresh = freshness_path(machine)
+    fresh.parent.mkdir(parents=True, exist_ok=True)
+    fresh.write_text(json.dumps(dict(
         checked_at=datetime.datetime.now().isoformat(timespec='seconds'), machine=machine,
-        newest_day=newest, total_sessions=total, stale_days=stale), ensure_ascii=False, indent=2),
+        unique_input_sessions=len(input_ids),
+        durable_db_sessions=total, durable_notes=durable_notes,
+        mismatch=total - durable_notes, newest_day=newest, stale_days=stale,
+        missing_note_ids=missing_ids, stale_note_ids=stale_ids,
+        human_owned_unverified_ids=unverified_ids),
+        ensure_ascii=False, indent=2),
         encoding='utf-8')
+    FRESHNESS.unlink(missing_ok=True)
     print('cursor import [%s]: файлов %d | DB: +%d новых / %d обновлено / %d без изменений | всего %d'
           % (machine, len(files), new, upd, unch, total))
     print('  заметки -> %s | оригиналы +%d -> %s | newest %s (stale %sd)'
           % (d_notes, copied, d_orig, newest, stale))
+    if missing_ids or stale_ids or unverified_ids:
+        print('  RED: missing=%s stale=%s human-unverified=%s'
+              % (missing_ids, stale_ids, unverified_ids))
+        return 3
     return 0
 
 
 def stats():
-    if not DB.exists():
+    target = _production_db(machine_name())
+    if not target.exists():
         print('базы нет, сначала: python cursor_lib.py import')
         return 3
-    con = sqlite3.connect(DB)
+    con = _connect(target)
     for m, n, d in con.execute('SELECT machine, COUNT(*), MAX(date) FROM sessions GROUP BY machine'):
         print('%s: %d сессий, newest %s' % (m, n, d))
     return 0
diff --git a/grok/_test_grok.py b/grok/_test_grok.py
index 89350f65..d7366f33 100644
--- a/grok/_test_grok.py
+++ b/grok/_test_grok.py
@@ -16,11 +16,37 @@ from pathlib import Path
 
 _TMP = Path(tempfile.mkdtemp(prefix="groktest_"))
 os.environ["CLAUDE_VAULT_ROOT"] = str(_TMP / "vault")
+os.environ["OBSIDIAN_VAULT"] = str(_TMP / "vault")
 sys.path.insert(0, str(Path(__file__).resolve().parent))
 import grok_lib as G
+REAL_MACHINE_NAME = G.machine_name
 G.DB = _TMP / "test.db"
+G.VAULT = _TMP / "vault"
+G.ORIGINALS_ROOT = _TMP / "originals"
 G.NOTES_DIR = Path(os.environ["CLAUDE_VAULT_ROOT"]) / "01-Conversations" / "Grok" / "conversations"
-G.FRESHNESS = _TMP / "_freshness.json"
+G.FRESHNESS_ROOT = _TMP / "freshness"
+G.FRESHNESS = _TMP / "legacy-freshness.json"
+G.MOC = G.VAULT / "01-Conversations" / "Grok" / "_Grok-MOC.md"
+G.machine_name = lambda: "TestNode"
+
+old_machine_env = os.environ.get("MACHINE_KEY")
+try:
+    G.machine_name = REAL_MACHINE_NAME
+    os.environ["MACHINE_KEY"] = "Node-A"
+    check_resolver_case = REAL_MACHINE_NAME() == G._paths.canonical_machine("Node-A")
+    os.environ["MACHINE_KEY"] = ".."
+    try:
+        REAL_MACHINE_NAME()
+    except ValueError:
+        check_resolver_unsafe = True
+    else:
+        check_resolver_unsafe = False
+finally:
+    if old_machine_env is None:
+        os.environ.pop("MACHINE_KEY", None)
+    else:
+        os.environ["MACHINE_KEY"] = old_machine_env
+    G.machine_name = lambda: "TestNode"
 
 # prod-grok-backend.json shape: conversation (ISO times) + responses[] (BSON/ISO times)
 FIXTURE = [
@@ -48,6 +74,9 @@ def check(name, cond):
     print(("  ok " if cond else "FAIL ") + name)
     if not cond: fails.append(name)
 
+check("machine resolver canonicalizes case", check_resolver_case)
+check("machine resolver rejects traversal", check_resolver_unsafe)
+
 # 1) parse
 rows = G.normalize_grok(FIXTURE)
 check("parse 2 conversations", len(rows) == 2)
@@ -92,6 +121,116 @@ check("conversation with no id -> skipped", G.normalize_grok([{"conversation": {
 newest, total, stale = G.write_freshness(con)
 check("freshness newest day", newest == "2026-07-02")
 check("freshness total 2", total == 2)
+check("web freshness is producer-scoped", G.freshness_path("web", "TestNode").exists())
+
+# 7) local Grok CLI: injected system/rules/reminders are excluded; same id on two nodes is separate.
+cli_root = _TMP / "grok-sessions"
+session = cli_root / "E%3A%5Cwork" / "same-cli-id"
+session.mkdir(parents=True)
+chat = session / "chat_history.jsonl"
+
+
+def write_cli(answer):
+    rows = [
+        {"type": "system", "content": "system prompt must stay out"},
+        {"type": "user", "content": [{"type": "text", "text":
+            "<user_info>machine</user_info><rules>secret rules</rules>"
+            "<user_query>Проверь общий волт</user_query>"}], "prompt_index": 0},
+        {"type": "user", "content": [{"type": "text", "text": "reminder"}],
+         "synthetic_reason": "system_reminder"},
+        {"type": "user", "content": [{"type": "text", "text":
+            "<project_context>future wrapper must stay out</project_context>"}]},
+        {"type": "user", "content": [{"type": "text", "text":
+            "How do I escape <script> in documentation?"}]},
+        {"type": "reasoning", "summary": "private reasoning"},
+        {"type": "assistant", "content": answer, "model_id": "grok-test"},
+    ]
+    chat.write_text("\n".join(json.dumps(x, ensure_ascii=False) for x in rows), encoding="utf-8")
+
+
+write_cli("Проверил.")
+node_a = G._paths.canonical_machine("Node-A")
+node_b = G._paths.canonical_machine("Node-B")
+cli_db_a, cli_db_b = _TMP / "grok-node-a.db", _TMP / "grok-node-b.db"
+G.machine_name = lambda: node_a
+check("CLI Node-A import", G.import_cli(cli_root, db=cli_db_a) == 0)
+G.machine_name = lambda: node_b
+check("CLI Node-B import", G.import_cli(cli_root, db=cli_db_b) == 0)
+cli_a, cli_b = sqlite3.connect(cli_db_a), sqlite3.connect(cli_db_b)
+check("same Grok id stays in two producer DB shards",
+      cli_a.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0] == 1
+      and cli_b.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0] == 1)
+G.machine_name = lambda: G._paths.canonical_machine("node-a")
+G.import_cli(cli_root, db=cli_db_a)
+check("Grok machine-name case drift stays in one DB and one path lane",
+      cli_a.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0] == 1
+      and len(list((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_a).glob("*.md"))) == 1)
+G.machine_name = lambda: node_b
+note_a = next((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_a).glob("*.md"))
+note_a.unlink()
+G.machine_name = lambda: node_a
+G.import_cli(cli_root, db=cli_db_a)
+check("missing Grok note self-heals from unchanged source", note_a.exists())
+lost_db = _TMP / "grok-lost-db.db"
+import os as _os, time as _time
+_os.utime(chat, (_time.time() + 259200, _time.time() + 259200))
+G.import_cli(cli_root, db=lost_db)
+check("Grok DB loss recovers durable note date",
+      len(list((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_a).glob("*.md"))) == 1)
+G.machine_name = lambda: node_b
+body_a = note_a.read_text(encoding="utf-8")
+check("Grok CLI note excludes injected context", "system prompt must stay out" not in body_a
+      and "secret rules" not in body_a and "reminder" not in body_a
+      and "future wrapper must stay out" not in body_a
+      and "private reasoning" not in body_a and "Проверь общий волт" in body_a
+      and "escape <script>" in body_a)
+check("Grok CLI provenance is honest", "source: grok-cli" in body_a
+      and "machine: node-a" in body_a and "driver: unknown" in body_a)
+fresh_a = json.loads(G.freshness_path("cli", node_a).read_text(encoding="utf-8"))
+fresh_b = json.loads(G.freshness_path("cli", node_b).read_text(encoding="utf-8"))
+check("Grok CLI freshness is per machine", fresh_a["mismatch"] == 0
+      and fresh_b["mismatch"] == 0
+      and G.freshness_path("cli", node_a) != G.freshness_path("cli", node_b))
+check("known injected wrapper drops are visible", fresh_a["dropped_injected_user_turns"] == 1)
+try:
+    G.freshness_path("cli", "Node A")
+except ValueError:
+    unsafe_rejected = True
+else:
+    unsafe_rejected = False
+check("unsafe Grok machine key fails closed", unsafe_rejected)
+for unsafe in (".", ".."):
+    try:
+        G.freshness_path("cli", unsafe)
+    except ValueError:
+        pass
+    else:
+        check("dot Grok path rejected: " + unsafe, False)
+
+write_cli("Изменённый ответ той же длины сообщений.")
+_os.utime(chat, (_time.time() + 172800, _time.time() + 172800))
+G.import_cli(cli_root, db=cli_db_b)
+note_b = next((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_b).glob("*.md"))
+check("same-count Grok content change is detected",
+      "Изменённый ответ" in note_b.read_text(encoding="utf-8"))
+check("later file mtime does not fork one session into two notes",
+      len(list((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_b).glob("*.md"))) == 1)
+stale = note_b.with_name("stale-duplicate-" + note_b.name)
+import shutil as _shutil
+_shutil.copy2(note_b, stale)
+G.import_cli(cli_root, db=cli_db_b)
+fresh_b = json.loads(G.freshness_path("cli", node_b).read_text(encoding="utf-8"))
+check("stale raw duplicate moves to reversible quarantine",
+      not stale.exists() and fresh_b["quarantined_stale_notes_this_run"] == 1
+      and fresh_b["quarantined_stale_notes_total"] == 1)
+
+saved_import_cli, saved_argv = G.import_cli, list(sys.argv)
+try:
+    G.import_cli = lambda root=None: 3
+    sys.argv = ["grok_lib.py", "cli-import"]
+    check("CLI dispatcher propagates red exit code", G.main() == 3)
+finally:
+    G.import_cli, sys.argv = saved_import_cli, saved_argv
 
 print()
 if fails:
diff --git a/grok/grok_export.cmd b/grok/grok_export.cmd
new file mode 100644
index 00000000..bdf2fe9e
--- /dev/null
+++ b/grok/grok_export.cmd
@@ -0,0 +1,22 @@
+@echo off
+REM Nightly local Grok CLI session export. Each machine owns its note/original/freshness lane.
+setlocal
+set "PY="
+for /f "usebackq tokens=1,* delims==" %%A in ("%USERPROFILE%\.claude\machine.env") do for /f "tokens=1" %%K in ("%%A") do if /i "%%K"=="PYTHON_EXE" for /f "tokens=* delims= " %%V in ("%%B") do set "PY=%%V"
+for /f "tokens=1 delims=#" %%A in ("%PY%") do set "PY=%%~A"
+set "PY=%PY:"=%"
+if not defined PY (
+  echo ERROR: PYTHON_EXE missing in %%USERPROFILE%%\.claude\machine.env 1>&2
+  exit /b 2
+)
+if not exist "%PY%" (
+  where "%PY%" >nul 2>&1
+  if errorlevel 1 (
+    echo ERROR: PYTHON_EXE not found: %PY% 1>&2
+    exit /b 2
+  )
+)
+set "LOGDIR=%LOCALAPPDATA%\claude-grok-export"
+if not exist "%LOGDIR%" mkdir "%LOGDIR%"
+"%PY%" "%~dp0grok_lib.py" cli-import > "%LOGDIR%\export.log" 2>&1
+exit /b %ERRORLEVEL%
diff --git a/grok/grok_lib.py b/grok/grok_lib.py
index 1eff4dee..349ae063 100644
--- a/grok/grok_lib.py
+++ b/grok/grok_lib.py
@@ -24,11 +24,18 @@ EXPORT SHAPE (prod-grok-backend.json = array of wrappers):
                       message, create_time (ISO or BSON {"$date":{"$numberLong":"ms"}}),
                       model, thinking_trace, ...} } ] }
 
+LOCAL GROK CLI (same-vault contract, 2026-09-23):
+  `~/.grok/sessions/**/<session-id>/chat_history.jsonl` is a machine-local lane, like
+  Codex and Cursor. It must never be mixed with the account-wide web export above.
+  `cli-import` writes originals, DB rows and notes under a machine-owned path and emits
+  `_freshness/cli-<machine>.json`; injected system/rules/reminder blocks are excluded.
+
 USAGE:
   python grok_lib.py import <path-to-prod-grok-backend.json>   # -> DB + notes
+  python grok_lib.py cli-import [sessions-root]                 # local CLI sessions
   python grok_lib.py stats
 """
-import os, re, sys, json, sqlite3, hashlib, datetime
+import os, re, sys, json, sqlite3, hashlib, datetime, glob, shutil, socket, urllib.parse
 from pathlib import Path
 
 # encoding guard (cp1252 print-crash class)
@@ -39,13 +46,33 @@ except Exception:
 
 HERE = Path(os.path.dirname(os.path.abspath(__file__)))
 DB = HERE / "grok_conversations.db"
+CLI_DB_ROOT = HERE / "_db" / "cli"
 
-VAULT = Path(os.environ.get("CLAUDE_VAULT_ROOT")
-             or os.environ.get("OBSIDIAN_VAULT")
-             or os.path.expanduser("~/Obsidian/Vault-Knowledge"))
+sys.path.insert(0, str(HERE.parent))
+sys.path.insert(0, str(Path.home() / ".claude" / "scripts" / "_shared"))
+try:
+    import menv
+    VAULT = Path(menv.vault())
+except Exception:
+    menv = None
+    try:
+        from _paths import VAULT as _VAULT
+        VAULT = Path(os.environ.get("CLAUDE_VAULT_ROOT")
+                     or os.environ.get("OBSIDIAN_VAULT") or _VAULT)
+    except Exception:
+        VAULT = Path(os.environ.get("CLAUDE_VAULT_ROOT")
+                     or os.environ.get("OBSIDIAN_VAULT")
+                     or os.path.expanduser("~/Obsidian/Vault-Knowledge"))
+try:
+    import _paths
+    ORIGINALS_ROOT = Path(_paths.originals_root())
+except Exception:
+    ORIGINALS_ROOT = VAULT / "_originals"
 NOTES_DIR = VAULT / "01-Conversations" / "Grok" / "conversations"
 MOC = VAULT / "01-Conversations" / "Grok" / "_Grok-MOC.md"
-FRESHNESS = HERE / "_freshness.json"
+FRESHNESS_ROOT = HERE / "_freshness"
+FRESHNESS = HERE / "_freshness.json"  # deprecated sentinel path; must stay absent
+GROK_CLI_ROOT = Path(os.path.expanduser("~/.grok/sessions"))
 
 SCHEMA = """
 CREATE TABLE IF NOT EXISTS conversations(
@@ -71,6 +98,30 @@ def _clean(s):
     return s.replace("\xa0", " ").strip()
 
 
+def machine_name():
+    resolver = getattr(globals().get('_paths'), 'machine_key', None)
+    if resolver:
+        return resolver()
+    if menv is not None:
+        raw = menv.machine_key(socket.gethostname())
+    else:
+        raw = os.environ.get("MACHINE_KEY") or os.environ.get("COMPUTERNAME") or socket.gethostname()
+    if not re.fullmatch(r"[A-Za-z0-9._-]+", raw):
+        raise ValueError("unsafe MACHINE_KEY: %r" % raw)
+    return raw.lower()
+
+
+def cli_db_path(machine):
+    return CLI_DB_ROOT / (machine + ".db")
+
+
+def freshness_path(kind, machine):
+    raw = (machine or "").strip()
+    if not raw or raw in (".", "..") or not re.fullmatch(r"[A-Za-z0-9][A-Za-z0-9._-]*", raw):
+        raise ValueError("unsafe MACHINE_KEY for freshness path: %r" % machine)
+    return FRESHNESS_ROOT / ("%s-%s.json" % (kind, raw))
+
+
 def _parse_time(v):
     """Grok mixes ISO strings and BSON {"$date":{"$numberLong":"ms"}} (and plain ms int).
     Returns (iso_string, day, month) best-effort; ('', '', '') if unparseable."""
@@ -261,13 +312,324 @@ def write_freshness(con):
             stale_days = (datetime.date.today() - datetime.date.fromisoformat(newest)).days
         except ValueError:
             pass
-    FRESHNESS.write_text(json.dumps({
+    target = freshness_path("web", machine_name())
+    target.parent.mkdir(parents=True, exist_ok=True)
+    target.write_text(json.dumps({
         "checked_at": datetime.datetime.now().isoformat(timespec="seconds"),
+        "machine": machine_name(), "lane": "grok-web-export",
         "newest_day": newest, "total_conversations": total, "stale_days": stale_days,
     }, ensure_ascii=False, indent=2), encoding="utf-8")
+    FRESHNESS.unlink(missing_ok=True)
     return newest, total, stale_days
 
 
+# ------------------------------------------------------------------ local CLI sessions
+
+_USER_QUERY = re.compile(r"<user_query>\s*(.*?)\s*</user_query>", re.S | re.I)
+_LEADING_WRAPPER = re.compile(r"^\s*<([A-Za-z][\w:-]*)\b[^>]*>.*?</\1>", re.I | re.S)
+
+
+def _content_text(content):
+    if isinstance(content, str):
+        return content
+    if not isinstance(content, list):
+        return ""
+    return "\n".join(str(item.get("text", "")) for item in content
+                     if isinstance(item, dict) and item.get("type") == "text").strip()
+
+
+def parse_cli_session(path):
+    """Parse only real prompt/answer turns; never archive harness rules as dev's words."""
+    p = Path(path)
+    sid = p.parent.name
+    project = urllib.parse.unquote(p.parent.parent.name)
+    turns = []
+    dropped_turns = 0
+    first_user = ""
+    try:
+        with open(p, encoding="utf-8", errors="replace") as fh:
+            for line in fh:
+                try:
+                    row = json.loads(line)
+                except ValueError:
+                    continue
+                kind = row.get("type")
+                if kind == "user":
+                    if row.get("synthetic_reason"):
+                        continue
+                    raw = _content_text(row.get("content"))
+                    match = _USER_QUERY.search(raw)
+                    text = _clean(match.group(1) if match else raw)
+                    if not text:
+                        continue
+                    # Unknown whole-turn wrappers are harness context: fail closed.
+                    if not match and _LEADING_WRAPPER.match(raw):
+                        dropped_turns += 1
+                        continue
+                    if turns and turns[-1].get("role") == "user" and turns[-1].get("text") == text:
+                        continue
+                    first_user = first_user or text
+                    turns.append({"role": "user", "text": text})
+                elif kind == "assistant":
+                    text = _clean(_content_text(row.get("content")))
+                    if text:
+                        turns.append({"role": "assistant", "text": text,
+                                      "model": _clean(row.get("model_id"))})
+    except OSError:
+        return None
+    if not turns:
+        return None
+    day = datetime.date.fromtimestamp(p.stat().st_mtime).isoformat()
+    title = (first_user or "grok cli session")[:120]
+    canonical = json.dumps(turns, ensure_ascii=False, sort_keys=True)
+    return {"session_id": sid, "machine": machine_name(), "project": project,
+            "day": day, "title": title, "turns": turns, "n_turns": len(turns),
+            "dropped_turns": dropped_turns,
+            "content_hash": hashlib.sha256(canonical.encode("utf-8")).hexdigest(),
+            "src_file": str(p)}
+
+
+def _cli_connect(db=None):
+    target = Path(db or cli_db_path(machine_name()))
+    target.parent.mkdir(parents=True, exist_ok=True)
+    con = sqlite3.connect(str(target))
+    con.execute("PRAGMA journal_mode=DELETE")
+    con.execute("CREATE TABLE IF NOT EXISTS cli_sessions("
+                "machine TEXT COLLATE NOCASE NOT NULL, session_id TEXT NOT NULL, day TEXT, title TEXT, "
+                "project TEXT, n_turns INT, content_hash TEXT, turns_json TEXT, src_file TEXT, "
+                "exported_at TEXT, PRIMARY KEY(machine, session_id))")
+    con.commit()
+    return con
+
+
+def _cli_note_path(row):
+    slug = re.sub(r"[^a-z0-9]+", "-", row["title"].lower())[:40].strip("-") or "grok"
+    return (VAULT / "01-Conversations" / "Grok" / "CLI" / row["machine"] /
+            ("%s-%s-%s.md" % (row["day"], slug, row["session_id"][-12:])))
+
+
+def _cli_note_text(row):
+    lines = ["---", 'title: "%s"' % row["title"].replace('"', "'"),
+             "type: ai-conversation", "stage: raw", "source: grok-cli",
+             "machine: %s" % row["machine"], "account: unknown", "origin: mixed",
+             "authored_by: hybrid", "session_id: %s" % row["session_id"],
+             "date_recorded: %s" % row["day"],
+             "date_added: %s" % datetime.date.today().isoformat(),
+             'project: "%s"' % row["project"].replace('"', "'"), "driver: unknown",
+             "language: ru", "tags: [ai-conversation, archive, grok, cli]",
+             "msg_count: %d" % row["n_turns"], "source_hash: %s" % row["content_hash"],
+             "related_concepts: []", "---", "",
+             "# %s" % row["title"], ""]
+    for turn in row["turns"]:
+        lines.extend(["**Запрос**" if turn["role"] == "user" else "**Grok**", "", turn["text"], ""])
+    return "\n".join(lines)
+
+
+def _cli_note_count(machine):
+    d = VAULT / "01-Conversations" / "Grok" / "CLI" / machine
+    if not d.exists():
+        return 0
+    count = 0
+    for p in d.glob("*.md"):
+        frontmatter = _frontmatter(p)
+        count += bool(re.search(r"(?m)^source:\s*grok-cli\s*$", frontmatter))
+    return count
+
+
+def _frontmatter(path):
+    lines = []
+    with open(path, encoding="utf-8", errors="ignore") as fh:
+        if fh.readline().strip() != "---":
+            return ""
+        size = 0
+        for line in fh:
+            if line.strip() == "---":
+                return "".join(lines)
+            lines.append(line)
+            size += len(line)
+            if size > 65536:
+                return ""
+    return ""
+
+
+def _machine_owned_cli_note(path):
+    fm = _frontmatter(path)
+    return bool(re.search(r"(?m)^source:\s*grok-cli\s*$", fm)
+                and re.search(r"(?m)^stage:\s*raw\s*$", fm)
+                and re.search(r"(?m)^related_concepts:\s*\[\]\s*$", fm))
+
+
+def _note_meta(path):
+    fm = _frontmatter(path)
+    def field(name):
+        match = re.search(r"(?m)^%s:\s*(.*?)\s*$" % re.escape(name), fm)
+        return (match.group(1).strip().strip('"') if match else "")
+    return {"session_id": field("session_id"), "day": field("date_recorded"),
+            "title": field("title"), "source_hash": field("source_hash")}
+
+
+def _collision_safe_cli_note(preferred, session_id):
+    if not preferred.exists() or _note_meta(preferred)["session_id"] in ("", session_id):
+        return preferred
+    suffix = hashlib.sha256(session_id.encode("utf-8")).hexdigest()[:8]
+    return preferred.with_name(preferred.stem + "-" + suffix + preferred.suffix)
+
+
+def _existing_cli_meta(machine):
+    root = VAULT / "01-Conversations" / "Grok" / "CLI" / machine
+    found = {}
+    if root.exists():
+        for note in root.glob("*.md"):
+            if not _machine_owned_cli_note(note):
+                continue
+            meta = _note_meta(note)
+            if meta["session_id"]:
+                found.setdefault(meta["session_id"], meta)
+    return found
+
+
+def _same_file(src, dst):
+    if not dst.exists() or dst.stat().st_size != src.stat().st_size:
+        return False
+    def digest(path):
+        h = hashlib.sha256()
+        with open(path, "rb") as fh:
+            for chunk in iter(lambda: fh.read(1024 * 1024), b""):
+                h.update(chunk)
+        return h.digest()
+    return digest(src) == digest(dst)
+
+
+def _quarantine_stale_cli_notes(con, machine):
+    """Move only machine-owned duplicate paths; curated notes and DB stay untouched."""
+    expected = {}
+    for sid, day, title in con.execute(
+            "SELECT session_id,day,title FROM cli_sessions WHERE machine=?", (machine,)):
+        preferred = _cli_note_path({"machine": machine, "session_id": sid,
+                                    "day": day, "title": title})
+        expected[sid] = _collision_safe_cli_note(preferred, sid)
+    source = VAULT / "01-Conversations" / "Grok" / "CLI" / machine
+    quarantine = VAULT / "_external-agent-imports" / "Grok-CLI-stale-notes" / machine
+    moved = 0
+    for note in source.glob("*.md"):
+        if not _machine_owned_cli_note(note):
+            continue
+        match = re.search(r"(?m)^session_id:\s*(\S+)\s*$", _frontmatter(note))
+        wanted = expected.get(match.group(1)) if match else None
+        if not wanted or note == wanted or not wanted.exists():
+            continue
+        quarantine.mkdir(parents=True, exist_ok=True)
+        dest = quarantine / note.name
+        if dest.exists():
+            suffix = hashlib.sha256(note.read_bytes()).hexdigest()[:10]
+            dest = quarantine / (note.stem + "-" + suffix + note.suffix)
+        shutil.move(str(note), str(dest))
+        moved += 1
+    total = len(list(quarantine.glob("*.md"))) if quarantine.exists() else 0
+    return moved, total
+
+
+def import_cli(root=None, *, db=None):
+    src = Path(root) if root else GROK_CLI_ROOT
+    machine = machine_name()
+    if not src.is_dir():
+        print("grok cli: НЕТ каталога %s -- узлу нечего отдавать" % src)
+        return 0
+    files = sorted(glob.glob(str(src / "**" / "chat_history.jsonl"), recursive=True))
+    con = _cli_connect(db or cli_db_path(machine))
+    con.execute("UPDATE cli_sessions SET machine=? WHERE machine=? COLLATE NOCASE", (machine, machine))
+    con.commit()
+    new = updated = unchanged = copied = 0
+    input_ids = set()
+    originals = ORIGINALS_ROOT / "grok-cli-sessions" / machine
+    originals.mkdir(parents=True, exist_ok=True)
+    dropped_turns = 0
+    existing_meta = _existing_cli_meta(machine)
+    for filename in files:
+        row = parse_cli_session(filename)
+        if not row:
+            continue
+        input_ids.add(row["session_id"])
+        dropped_turns += row.get("dropped_turns", 0)
+        raw_dest = originals / (row["session_id"] + ".jsonl")
+        if not _same_file(Path(filename), raw_dest):
+            shutil.copy2(filename, raw_dest)
+            copied += 1
+        old = con.execute("SELECT content_hash,day,title FROM cli_sessions WHERE machine=? AND session_id=?",
+                          (machine, row["session_id"])).fetchone()
+        if old and old[1]:
+            # The session can grow for days; its first archived day and note path stay stable.
+            row["day"] = old[1]
+        if old and old[2]:
+            row["title"] = old[2]
+        if not old and row["session_id"] in existing_meta:
+            durable = existing_meta[row["session_id"]]
+            row["day"] = durable["day"] or row["day"]
+            row["title"] = durable["title"] or row["title"]
+        preferred = _cli_note_path(row)
+        note = _collision_safe_cli_note(preferred, row["session_id"])
+        if (old and old[0] == row["content_hash"] and note.exists()
+                and _note_meta(note)["source_hash"] == row["content_hash"]):
+            unchanged += 1
+            continue
+        now = datetime.datetime.now(datetime.timezone.utc).isoformat()
+        con.execute("INSERT INTO cli_sessions VALUES(?,?,?,?,?,?,?,?,?,?) "
+                    "ON CONFLICT(machine,session_id) DO UPDATE SET day=excluded.day,"
+                    "title=excluded.title,project=excluded.project,n_turns=excluded.n_turns,"
+                    "content_hash=excluded.content_hash,turns_json=excluded.turns_json,"
+                    "src_file=excluded.src_file,exported_at=excluded.exported_at",
+                    (machine, row["session_id"], row["day"], row["title"], row["project"],
+                     row["n_turns"], row["content_hash"],
+                     json.dumps(row["turns"], ensure_ascii=False), row["src_file"], now))
+        note.parent.mkdir(parents=True, exist_ok=True)
+        if not note.exists() or _machine_owned_cli_note(note):
+            note.write_text(_cli_note_text(row), encoding="utf-8")
+        new += 0 if old else 1
+        updated += 1 if old else 0
+    con.commit()
+    quarantined, quarantined_total = _quarantine_stale_cli_notes(con, machine)
+    total = con.execute("SELECT COUNT(*) FROM cli_sessions WHERE machine=?", (machine,)).fetchone()[0]
+    newest = con.execute("SELECT MAX(day) FROM cli_sessions WHERE machine=?", (machine,)).fetchone()[0]
+    db_hashes = dict(con.execute(
+        "SELECT session_id,content_hash FROM cli_sessions WHERE machine=?", (machine,)))
+    note_by_id = {}
+    note_root = VAULT / "01-Conversations" / "Grok" / "CLI" / machine
+    for candidate in note_root.glob("*.md"):
+        meta = _note_meta(candidate)
+        if meta["session_id"] in db_hashes:
+            note_by_id.setdefault(meta["session_id"], (candidate, meta))
+    notes = len(set(db_hashes) & set(note_by_id))
+    missing_ids = sorted(set(db_hashes) - set(note_by_id))
+    stale_ids = sorted(sid for sid, (_, meta) in note_by_id.items()
+                       if meta["source_hash"] and meta["source_hash"] != db_hashes[sid])
+    unverified_ids = sorted(sid for sid, (path, meta) in note_by_id.items()
+                            if not meta["source_hash"] and not _machine_owned_cli_note(path))
+    target = freshness_path("cli", machine)
+    target.parent.mkdir(parents=True, exist_ok=True)
+    target.write_text(json.dumps({"checked_at": datetime.datetime.now().isoformat(timespec="seconds"),
+                                  "machine": machine, "lane": "grok-cli",
+                                  "unique_input_sessions": len(input_ids),
+                                  "durable_db_sessions": total, "durable_notes": notes,
+                                  "mismatch": total - notes, "newest_day": newest,
+                                  "dropped_injected_user_turns": dropped_turns,
+                                  "quarantined_stale_notes_this_run": quarantined,
+                                  "quarantined_stale_notes_total": quarantined_total,
+                                  "missing_note_ids": missing_ids,
+                                  "stale_note_ids": stale_ids,
+                                  "human_owned_unverified_ids": unverified_ids},
+                                 ensure_ascii=False, indent=2), encoding="utf-8")
+    FRESHNESS.unlink(missing_ok=True)
+    print("grok cli import [%s]: input %d | DB +%d/%d updated/%d unchanged | total %d | "
+          "notes %d | originals +%d | quarantined %d | mismatch %d" %
+          (machine, len(input_ids), new, updated, unchanged, total, notes, copied,
+           quarantined, total - notes))
+    if missing_ids or stale_ids or unverified_ids:
+        print("grok cli RED: missing=%s stale=%s human-unverified=%s" %
+              (missing_ids, stale_ids, unverified_ids))
+        return 3
+    return 0
+
+
 # ------------------------------------------------------------------ cli
 
 def _load_json(path):
@@ -283,7 +645,7 @@ def do_import(path):
     newest, total, stale = write_freshness(con)
     print(f"grok import: +{new} new / {upd} updated / {unch} unchanged | notes: {w} written "
           f"| DB total {total} | newest {newest} (stale {stale}d)")
-    return new, upd
+    return 0
 
 
 def do_stats():
@@ -291,6 +653,14 @@ def do_stats():
     total = con.execute("SELECT COUNT(*) FROM conversations").fetchone()[0]
     turns = con.execute("SELECT COALESCE(SUM(n_turns),0) FROM conversations").fetchone()[0]
     print(f"grok DB: {total} conversations, {turns} turns | {DB}")
+    target = cli_db_path(machine_name())
+    if target.exists():
+        cli = _cli_connect(target)
+        cli_total = cli.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0]
+        print("grok CLI DB [%s]: %d sessions | %s" % (machine_name(), cli_total, target))
+    else:
+        print("grok CLI DB: 0 sessions")
+    return 0
 
 
 def main():
@@ -300,12 +670,14 @@ def main():
     if cmd == "import":
         if len(sys.argv) < 3:
             print("usage: grok_lib.py import <prod-grok-backend.json>"); sys.exit(2)
-        do_import(sys.argv[2])
+        return do_import(sys.argv[2])
+    elif cmd == "cli-import":
+        return import_cli(sys.argv[2] if len(sys.argv) > 2 else None)
     elif cmd == "stats":
-        do_stats()
+        return do_stats()
     else:
-        print(__doc__); sys.exit(1)
+        print(__doc__); return 1
 
 
 if __name__ == "__main__":
-    main()
+    sys.exit(main())

--- DIFF END ---

---

**Claude:**

⏰ среда, утро, 09:21, 23 сентября 2026

SUMMARY: The direction (producer-sharded DBs, content hashes, honest provenance) is right, but the Cursor lane has a real correctness hole — a changed source can leave the DB updated and the note never rewritten in the same run, plus `_paths.canonical_machine` accepts an env-injected `MACHINE_KEY` that never matches the registry and silently forks a node's identity.

FINDINGS:

- `cursor/cursor_lib.py` (`do_import`, the `if note.exists(): if not _machine_owned_note(note): ... continue` branch) | **high** | When a note exists but is *machine-owned*, the code falls through and rewrites it — correct. But when the note exists and is *human-owned*, it `continue`s **after** the `con.execute(INSERT ... ON CONFLICT ... content_hash=excluded.content_hash)` has already stored the fresh hash. On the next run `old[0] == r['content_hash']` is true, `note.exists()` is true, and `_note_source_hash(note)` is the *stale* hash — so the "unchanged" fast path is not taken (good), and we re-enter the same branch and `continue` again (also good, note preserved). So far consistent. The actual defect is in the **freshness accounting** on that same path: `stale_ids` only flags notes whose `source_hash` is non-empty and differs. A human-owned note that never had a `source_hash` (e.g. hand-authored, or pre-`source_hash` legacy) lands in `unverified_ids` only if `not _machine_owned_note(path)` — but a note that *is* machine-owned yet lacks `source_hash` (written by the pre-hash version of this very script) is counted as **durable and green** while its body is stale. | Treat "machine-owned note with no `source_hash`" as stale, not green: in the `unverified_ids`/`stale_ids` computation, add `sid for sid, path in note_by_id.items() if not _note_source_hash(path)` to a red bucket unconditionally, and let the write path rewrite machine-owned hash-less notes (it already does, since the hash check requires `_note_source_hash(note) == r['content_hash']`). The metric, not the writer, is what lies here.

- `cursor/cursor_lib.py` (`do_import`, `if old and old[1]: r['date'] = old[1]`) | **med** | The stored `date` is pinned from the DB, but `_collision_safe_note` / `preferred` is built from `_slug(r['title'])` where `title` is pinned from `old[2]` — so far stable. However the **DB row is then written with `date=excluded.date`**, i.e. `r['date']` (the pinned old date) — fine — but `title=excluded.title` likewise writes back the pinned old title, meaning a session whose first user prompt changes can *never* update its title in the DB, even on a genuine content change. Worse, the note body is regenerated with the old title in the H1 while `msg_count`/body are fresh. That's a silent, permanent divergence between note title and actual first prompt. | Either drop the pin (keep path stability by hashing the *session_id* into the filename rather than the slug), or keep the pin for the **path** only and let `r['title']` used in `note_text`/DB be the fresh parse: `path_title = old[2] or r['title']` used solely in `preferred`.

- `_paths.py:88-110` (`canonical_machine`) | **med** | On registry miss it returns `raw.lower()`. Combined with `machine_key()`'s precedence (`os.environ['MACHINE_KEY']` first), any stray/typo'd `MACHINE_KEY` in the environment silently creates a **new producer identity** — a new DB shard, a new note lane, a new freshness file — with no error and no warning. The registry lookup exists precisely to catch this, then the fallback defeats it. The test suite even relies on this (`MACHINE_KEY=Node-A` with no registry entry) so the failure mode is baked in. | Make the fallback loud rather than silent: when `fleet_nodes.json` exists and the value matches no key/hostname/alias, print a one-line warning to stderr naming the unknown key and the registry path. Keep returning `raw.lower()` (fail-open is right for a new node), but the operator must see the fork. Root cause is "unknown identity is indistinguishable from known identity"; a stderr line is the AK-47 fix.

- `grok/grok_lib.py` (`parse_cli_session`, `day = datetime.date.fromtimestamp(p.stat().st_mtime)`) | **med** | The session day comes from file mtime, which is exactly the fork source the tests try to pin down. The pin works only via `old[1]` (DB) or `existing_meta` (durable note). If **both** the shard DB and the note are absent — the genuine cold-start case on a new machine, or after a shard is rebuilt while notes live in a quarantine dir — a session archived weeks ago gets today's mtime-derived day, and the note is filed under the wrong date with no signal. The test `"Grok DB loss recovers durable note date"` only covers DB-loss-with-note-present. | Prefer an in-file timestamp when one exists (Grok CLI rows carry no explicit time, so the honest fix is: use `min(mtime, ctime)` is not it either) — instead record the first-seen day in the **original** copy's name or a sidecar under `_originals/grok-cli-sessions/<machine>/`, which is the durable artifact that survives both DB and note loss. At minimum, emit the derived-from-mtime fact into freshness (`day_source: "mtime"`) so a wrong date is visible rather than asserted.

- `grok/grok_lib.py` (`_LEADING_WRAPPER` drop rule in `parse_cli_session`) | **med** | The rule is: no `<user_query>` match **and** the raw text *starts* with any `<tag>…</tag>` → drop the whole turn as harness context. A genuine user turn that opens with a tag-looking construct — e.g. a message that begins with `<div class="x">…</div> why does this render wrong?` — is silently discarded, counted only as an anonymous `dropped_injected_user_turns` integer. That is real user content lost from the archive with no recoverable trace in the note. The test's `"How do I escape <script> in documentation?"` passes only because the tag is *not* leading. | Fail closed on the *lane*, not the content: keep the turn out of the note body but record the dropped turns' first 80 chars in the freshness JSON (or a `dropped/` sidecar under originals), so a false positive is diagnosable. Alternatively, restrict the drop to a known wrapper allow-list (`user_info|rules|project_context|system_reminder|…`) rather than "any leading tag" — an allow-list is both simpler and has no false-positive class.

- `grok/grok_export.cmd:5-7` | **low** | The `PYTHON_EXE` parse chain assumes `machine.env` exists; if it doesn't, the `for /f "usebackq"` over a missing file emits a cmd error to stderr before the `if not defined PY` check produces the intended message. Also the nested `for` over `%%A` with `tokens=1` means a line like `# PYTHON_EXE=...` (commented) would be skipped correctly, but `PYTHON_EXE = C:\py.exe` (spaces around `=`) sets `%%K` to `PYTHON_EXE` with a trailing space and the `if /i` comparison fails silently. | Add `if not exist "%USERPROFILE%\.claude\machine.env" (echo ERROR: machine.env missing 1>&2 & exit /b 2)` before the loop; the spacing case is not worth handling if the file is machine-generated, but say so in the REM.

- `grok/grok_lib.py:645` (`do_import` now `return 0`) | **low** | The signature changed from `return new, upd` to `return 0`. Any existing caller that unpacked the tuple (`n, u = do_import(...)`) now raises `TypeError: cannot unpack non-sequence int`. The diff doesn't show such a caller, but the diff also doesn't show the whole repo. | If no caller exists, fine — state it. If one might, return the exit code from `main()` and keep `do_import` returning the counts, since `main()` is the only thing that needs a process code.

Noting one thing the diff gets right and that I'd keep: `_same_file` comparing bytes instead of mtime, and `FRESHNESS.unlink(missing_ok=True)` turning the old shared-heartbeat path into an actively-enforced absent sentinel. Both close real last-writer-wins classes.

🧒 Простыми словами: тетрадки теперь у каждого компьютера свои — это хорошо. Но в тетрадке Cursor можно записать «всё свежее», а сама страница останется старой, и никто не крикнет. И если компьютеру дать чужое имя по ошибке, он молча заведёт себе новую тетрадку вместо того, чтобы сказать «я такого имени не знаю».

===VERDICT=== REQUEST_CHANGES
