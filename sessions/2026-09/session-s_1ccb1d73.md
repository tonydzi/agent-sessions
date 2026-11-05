---
session: s_1ccb1d73
date: 2026-09-23
words: 6461
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1ccb1d73` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
index 7f910a70..de25330e 100644
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
@@ -82,6 +85,31 @@ PYTHON_EXE = get("PYTHON_EXE", "python")
 SECRETS = get("SECRETS_DIR", os.path.join(_home(), "!CLAUDE-NODE-0X May26", "secrets"))
 
 
+def canonical_machine(value):
+    """Resolve key/hostname/alias to the fleet registry key; unknown safe keys use lowercase."""
+    raw = (value or "").strip()
+    if not raw or not re.fullmatch(r"[A-Za-z0-9._-]+", raw):
+        raise ValueError("unsafe MACHINE_KEY: %r" % value)
+    folded = raw.casefold()
+    try:
+        registry = os.path.join(_home(), ".claude", "fleet_nodes.json")
+        nodes = json.loads(open(registry, encoding="utf-8").read()).get("nodes", {})
+        for key, meta in nodes.items():
+            names = [key, meta.get("hostname", "")] + list(meta.get("aliases") or [])
+            if any(str(name).casefold() == folded for name in names if name):
+                return key
+    except (OSError, ValueError, TypeError):
+        pass
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
index 00000000..dbf7bc73
--- /dev/null
+++ b/cursor/_test_cursor.py
@@ -0,0 +1,143 @@
+# -*- coding: utf-8 -*-
+"""Isolated regression for Cursor provenance: two machines, same id, no clobber."""
+import json
+import shutil
+import sqlite3
+import tempfile
+from pathlib import Path
+
+import cursor_lib as C
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
+    C.FRESHNESS_ROOT = TMP / "freshness"
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
+    # Linked note becomes human-owned and must survive a later source refresh.
+    note = next((C.VAULT / "01-Conversations" / "Cursor" / node_b).glob("*.md"))
+    linked = note.read_text(encoding="utf-8").replace("related_concepts: []",
+                                                       "related_concepts: [kept]")
+    note.write_text(linked, encoding="utf-8")
+    fixture(source, sid, answer="Третья версия.")
+    C.do_import(source, db=db_b)
+    check("linked note is preserved", "related_concepts: [kept]" in note.read_text(encoding="utf-8")
+          and "Третья версия." not in note.read_text(encoding="utf-8"))
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
+    C.do_import(legacy_source, db=legacy_db)
+    migrated = sqlite3.connect(legacy_db)
+    stored_hash = migrated.execute("SELECT content_hash FROM sessions").fetchone()[0]
+    migrated.close()
+    check("legacy migration records hash without rewriting existing raw note",
+          bool(stored_hash) and "KEEP HUMAN TEXT" in legacy_note.read_text(encoding="utf-8"))
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
+finally:
+    shutil.rmtree(TMP, ignore_errors=True)
+
+if FAILS:
+    raise SystemExit("FAIL: " + ", ".join(FAILS))
+print("PASS: Cursor producer lanes and provenance")
diff --git a/cursor/cursor_lib.py b/cursor/cursor_lib.py
index 3a3579fb..008593dc 100644
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
@@ -37,29 +37,54 @@ except Exception:
 
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
+    if '_paths' in globals():
+        return _paths.machine_key()
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
+    if not raw or not re.fullmatch(r'[A-Za-z0-9._-]+', raw):
+        raise ValueError('unsafe MACHINE_KEY for freshness path: %r' % machine)
+    return FRESHNESS_ROOT / (raw + '.json')
 
 
 def _clean(s):
@@ -91,7 +116,7 @@ def _date_of(ts_text, path):
 
 
 def parse_transcript(path):
-    """-> dict(session_id, date, title, project, body_md, msg_count) или None (пустой)."""
+    """-> нормализованная сессия или None. Инъекции Cursor не выдаём за слова оператора."""
     p = Path(path)
     sid = p.stem
     project = p.parent.parent.parent.name if p.parent.parent.parent else '?'
@@ -132,17 +157,19 @@ def parse_transcript(path):
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
             'related_concepts: []\n---\n\n# %s\n\n%s\n'
             % (r['title'].replace('"', "'"), machine, r['session_id'], r['date'],
@@ -150,63 +177,153 @@ def note_text(r, machine):
                r['title'], r['body_md']))
 
 
-def do_import(root=None):
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
+    needs_migration = cols and ('content_hash' not in cols or 'exported_at' not in cols
+                                or 'COLLATE NOCASE' not in schema_sql.upper())
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
+            if 'content_hash' in legacy:
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
+def _raw_note_count(machine):
+    d = VAULT / '01-Conversations' / 'Cursor' / machine
+    if not d.exists():
+        return 0
+    count = 0
+    for p in d.glob('*.md'):
+        head = p.read_text(encoding='utf-8', errors='ignore')[:1200]
+        frontmatter = head.split('---', 2)[1] if head.startswith('---') and head.count('---') >= 2 else ''
+        count += bool(re.search(r'(?m)^source:\s*cursor\s*$', frontmatter))
+    return count
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
+    con = _connect(db or db_path(machine))
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
+        src_stat = os.stat(f)
+        if (not dst.exists() or dst.stat().st_size != src_stat.st_size
+                or dst.stat().st_mtime_ns != src_stat.st_mtime_ns):
             shutil.copy2(f, dst)
             copied += 1
-        old = con.execute('SELECT msg_count FROM sessions WHERE session_id=?',
-                          (r['session_id'],)).fetchone()
-        if old and old[0] == r['msg_count']:
+        old = con.execute('SELECT content_hash,date FROM sessions WHERE machine=? AND session_id=?',
+                          (machine, r['session_id'])).fetchone()
+        if old and old[0] == r['content_hash']:
             unch += 1
             continue
-        con.execute('INSERT INTO sessions VALUES (?,?,?,?,?,?,?) ON CONFLICT(session_id) DO UPDATE'
-                    ' SET msg_count=excluded.msg_count, title=excluded.title',
-                    (r['session_id'], machine, r['date'], r['title'], r['project'],
-                     r['msg_count'], r['src_file']))
+        if old and old[1]:
+            r['date'] = old[1]
+        now = datetime.datetime.now(datetime.timezone.utc).isoformat()
+        con.execute('INSERT INTO sessions VALUES (?,?,?,?,?,?,?,?,?) '
+                    'ON CONFLICT(machine,session_id) DO UPDATE SET '
+                    'date=excluded.date,title=excluded.title,project=excluded.project,'
+                    'msg_count=excluded.msg_count,content_hash=excluded.content_hash,'
+                    'src_file=excluded.src_file,exported_at=excluded.exported_at',
+                    (machine, r['session_id'], r['date'], r['title'], r['project'],
+                     r['msg_count'], r['content_hash'], r['src_file'], now))
         note = d_notes / ('%s-%s-%s.md' % (r['date'], _slug(r['title']), r['session_id'][-12:]))
+        adopt_existing = bool(note.exists() and (old is None or not old[0]))
+        if adopt_existing:
+            # Legacy DB had no hash. Adopt the current note without a mass rewrite.
+            upd += 1
+            continue
+        if note.exists():
+            current = note.read_text(encoding='utf-8', errors='ignore')
+            if 'related_concepts: []' not in current:
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
+    durable_notes = _raw_note_count(machine)
+    fresh = freshness_path(machine)
+    fresh.parent.mkdir(parents=True, exist_ok=True)
+    fresh.write_text(json.dumps(dict(
         checked_at=datetime.datetime.now().isoformat(timespec='seconds'), machine=machine,
-        newest_day=newest, total_sessions=total, stale_days=stale), ensure_ascii=False, indent=2),
+        unique_input_sessions=len(input_ids),
+        durable_db_sessions=total, durable_notes=durable_notes,
+        mismatch=total - durable_notes, newest_day=newest, stale_days=stale),
+        ensure_ascii=False, indent=2),
         encoding='utf-8')
+    FRESHNESS.unlink(missing_ok=True)
     print('cursor import [%s]: файлов %d | DB: +%d новых / %d обновлено / %d без изменений | всего %d'
           % (machine, len(files), new, upd, unch, total))
     print('  заметки -> %s | оригиналы +%d -> %s | newest %s (stale %sd)'
           % (d_notes, copied, d_orig, newest, stale))
-    return 0
+    return 3 if total != durable_notes else 0
 
 
 def stats():
-    if not DB.exists():
+    target = db_path(machine_name())
+    if not target.exists():
         print('базы нет, сначала: python cursor_lib.py import')
         return 3
-    con = sqlite3.connect(DB)
+    con = _connect(target)
     for m, n, d in con.execute('SELECT machine, COUNT(*), MAX(date) FROM sessions GROUP BY machine'):
         print('%s: %d сессий, newest %s' % (m, n, d))
     return 0
diff --git a/grok/_test_grok.py b/grok/_test_grok.py
index 89350f65..0879e525 100644
--- a/grok/_test_grok.py
+++ b/grok/_test_grok.py
@@ -16,11 +16,16 @@ from pathlib import Path
 
 _TMP = Path(tempfile.mkdtemp(prefix="groktest_"))
 os.environ["CLAUDE_VAULT_ROOT"] = str(_TMP / "vault")
+os.environ["OBSIDIAN_VAULT"] = str(_TMP / "vault")
 sys.path.insert(0, str(Path(__file__).resolve().parent))
 import grok_lib as G
 G.DB = _TMP / "test.db"
+G.VAULT = _TMP / "vault"
+G.ORIGINALS_ROOT = _TMP / "originals"
 G.NOTES_DIR = Path(os.environ["CLAUDE_VAULT_ROOT"]) / "01-Conversations" / "Grok" / "conversations"
-G.FRESHNESS = _TMP / "_freshness.json"
+G.FRESHNESS_ROOT = _TMP / "freshness"
+G.MOC = G.VAULT / "01-Conversations" / "Grok" / "_Grok-MOC.md"
+G.machine_name = lambda: "TestNode"
 
 # prod-grok-backend.json shape: conversation (ISO times) + responses[] (BSON/ISO times)
 FIXTURE = [
@@ -92,6 +97,83 @@ check("conversation with no id -> skipped", G.normalize_grok([{"conversation": {
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
+
+write_cli("Изменённый ответ той же длины сообщений.")
+import os as _os, time as _time
+_os.utime(chat, (_time.time() + 172800, _time.time() + 172800))
+G.import_cli(cli_root, db=cli_db_b)
+note_b = next((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_b).glob("*.md"))
+check("same-count Grok content change is detected",
+      "Изменённый ответ" in note_b.read_text(encoding="utf-8"))
+check("later file mtime does not fork one session into two notes",
+      len(list((G.VAULT / "01-Conversations" / "Grok" / "CLI" / node_b).glob("*.md"))) == 1)
 
 print()
 if fails:
diff --git a/grok/grok_export.cmd b/grok/grok_export.cmd
new file mode 100644
index 00000000..13f7667a
--- /dev/null
+++ b/grok/grok_export.cmd
@@ -0,0 +1,13 @@
+@echo off
+REM Nightly local Grok CLI session export. Each machine owns its note/original/freshness lane.
+setlocal
+set "PY="
+for /f "usebackq tokens=1,* delims==" %%A in ("%USERPROFILE%\.claude\machine.env") do if /i "%%A"=="PYTHON_EXE" set "PY=%%B"
+if not defined PY (
+  echo ERROR: PYTHON_EXE missing in %%USERPROFILE%%\.claude\machine.env 1>&2
+  exit /b 2
+)
+set "LOGDIR=%LOCALAPPDATA%\claude-grok-export"
+if not exist "%LOGDIR%" mkdir "%LOGDIR%"
+"%PY%" "%~dp0grok_lib.py" cli-import >> "%LOGDIR%\export.log" 2>&1
+exit /b %ERRORLEVEL%
diff --git a/grok/grok_lib.py b/grok/grok_lib.py
index 1eff4dee..85a11a39 100644
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
@@ -71,6 +98,29 @@ def _clean(s):
     return s.replace("\xa0", " ").strip()
 
 
+def machine_name():
+    if '_paths' in globals():
+        return _paths.machine_key()
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
+    if not raw or not re.fullmatch(r"[A-Za-z0-9._-]+", raw):
+        raise ValueError("unsafe MACHINE_KEY for freshness path: %r" % machine)
+    return FRESHNESS_ROOT / ("%s-%s.json" % (kind, raw))
+
+
 def _parse_time(v):
     """Grok mixes ISO strings and BSON {"$date":{"$numberLong":"ms"}} (and plain ms int).
     Returns (iso_string, day, month) best-effort; ('', '', '') if unparseable."""
@@ -261,13 +311,205 @@ def write_freshness(con):
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
+_INJECTED_WRAPPER = re.compile(
+    r"<\s*(user_info|rules|project_context|system-reminder|system_reminder|"
+    r"environment_details|environment_context|recommended_plugins|permissions|"
+    r"multi_agent_mode|plan_mode)\b", re.I)
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
+                    if not match and _INJECTED_WRAPPER.search(raw):
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
+             "msg_count: %d" % row["n_turns"], "related_concepts: []", "---", "",
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
+        head = p.read_text(encoding="utf-8", errors="ignore")[:1200]
+        frontmatter = head.split("---", 2)[1] if head.startswith("---") and head.count("---") >= 2 else ""
+        count += bool(re.search(r"(?m)^source:\s*grok-cli\s*$", frontmatter))
+    return count
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
+    for filename in files:
+        row = parse_cli_session(filename)
+        if not row:
+            continue
+        input_ids.add(row["session_id"])
+        dropped_turns += row.get("dropped_turns", 0)
+        raw_dest = originals / (row["session_id"] + ".jsonl")
+        src_stat = os.stat(filename)
+        if (not raw_dest.exists() or raw_dest.stat().st_size != src_stat.st_size
+                or raw_dest.stat().st_mtime_ns != src_stat.st_mtime_ns):
+            shutil.copy2(filename, raw_dest)
+            copied += 1
+        old = con.execute("SELECT content_hash,day FROM cli_sessions WHERE machine=? AND session_id=?",
+                          (machine, row["session_id"])).fetchone()
+        if old and old[0] == row["content_hash"]:
+            unchanged += 1
+            continue
+        if old and old[1]:
+            # The session can grow for days; its first archived day and note path stay stable.
+            row["day"] = old[1]
+        now = datetime.datetime.now(datetime.timezone.utc).isoformat()
+        con.execute("INSERT INTO cli_sessions VALUES(?,?,?,?,?,?,?,?,?,?) "
+                    "ON CONFLICT(machine,session_id) DO UPDATE SET day=excluded.day,"
+                    "title=excluded.title,project=excluded.project,n_turns=excluded.n_turns,"
+                    "content_hash=excluded.content_hash,turns_json=excluded.turns_json,"
+                    "src_file=excluded.src_file,exported_at=excluded.exported_at",
+                    (machine, row["session_id"], row["day"], row["title"], row["project"],
+                     row["n_turns"], row["content_hash"],
+                     json.dumps(row["turns"], ensure_ascii=False), row["src_file"], now))
+        note = _cli_note_path(row)
+        note.parent.mkdir(parents=True, exist_ok=True)
+        if note.exists() and old is None:
+            new += 1
+            continue
+        if not note.exists() or "related_concepts: []" in note.read_text(encoding="utf-8", errors="ignore"):
+            note.write_text(_cli_note_text(row), encoding="utf-8")
+        new += 0 if old else 1
+        updated += 1 if old else 0
+    con.commit()
+    total = con.execute("SELECT COUNT(*) FROM cli_sessions WHERE machine=?", (machine,)).fetchone()[0]
+    newest = con.execute("SELECT MAX(day) FROM cli_sessions WHERE machine=?", (machine,)).fetchone()[0]
+    notes = _cli_note_count(machine)
+    target = freshness_path("cli", machine)
+    target.parent.mkdir(parents=True, exist_ok=True)
+    target.write_text(json.dumps({"checked_at": datetime.datetime.now().isoformat(timespec="seconds"),
+                                  "machine": machine, "lane": "grok-cli",
+                                  "unique_input_sessions": len(input_ids),
+                                  "durable_db_sessions": total, "durable_notes": notes,
+                                  "mismatch": total - notes, "newest_day": newest,
+                                  "dropped_injected_user_turns": dropped_turns},
+                                 ensure_ascii=False, indent=2), encoding="utf-8")
+    FRESHNESS.unlink(missing_ok=True)
+    print("grok cli import [%s]: input %d | DB +%d/%d updated/%d unchanged | total %d | "
+          "notes %d | originals +%d | mismatch %d" %
+          (machine, len(input_ids), new, updated, unchanged, total, notes, copied, total - notes))
+    return 3 if total != notes else 0
+
+
 # ------------------------------------------------------------------ cli
 
 def _load_json(path):
@@ -291,6 +533,13 @@ def do_stats():
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
 
 
 def main():
@@ -301,6 +550,8 @@ def main():
         if len(sys.argv) < 3:
             print("usage: grok_lib.py import <prod-grok-backend.json>"); sys.exit(2)
         do_import(sys.argv[2])
+    elif cmd == "cli-import":
+        import_cli(sys.argv[2] if len(sys.argv) > 2 else None)
     elif cmd == "stats":
         do_stats()
     else:

--- DIFF END ---

---

**Claude:**

⏰ среда, утро, 08:48, 23 сентября 2026

SUMMARY: The provenance sharding idea is right (one producer = one DB + one freshness file + one note lane), but the new mismatch alarm never reaches the process exit code, the "human-owned note" heuristic can silently overwrite curated notes, the machine-key validator still admits `.`/`..` as path components, and the Cursor DB move orphans the existing `cursor_sessions.db` plus the consumers named in its own docstring.

FINDINGS:
- grok/grok_lib.py:~553 (`main`, `cli-import` branch) | high | `import_cli()` returns `3` on `total != notes`, but `main()` discards it and never calls `sys.exit`, so the process always exits 0. `grok_export.cmd`'s `exit /b %ERRORLEVEL%` therefore always reports success and the scheduled task can never go red — the entire mismatch alarm built in this diff is dead on the real rail. Fix: `sys.exit(import_cli(...))` (and likewise for `do_import`/`do_stats` if they return codes). Cursor's dispatcher isn't in the diff — check it has the same `sys.exit` wiring, since `do_import`/`stats` there also return 3.
- cursor/cursor_lib.py:~250 (`do_import`) and grok/grok_lib.py:~470 (`import_cli`) | med | Human ownership is detected with `'related_concepts: []' in note.read_text()` — a substring test over the **whole file**, body included. A curated note whose transcript body happens to contain that literal string (these are Cursor/Grok sessions about this very vault code, so it is likely, not hypothetical) is classified as machine-owned and gets `write_text`-overwritten, destroying the human's links. Fix: test the frontmatter block only — you already have that logic in `_raw_note_count`/`_cli_note_count`; factor it out and reuse it (or key on an explicit `stage: raw` marker).
- _paths.py:89 (`canonical_machine`) | med | `re.fullmatch(r"[A-Za-z0-9._-]+")` accepts `.` and `..`, and the result is concatenated straight into paths (`DB_ROOT / (machine + '.db')`, `VAULT/'01-Conversations'/'Cursor'/machine`, `ORIGINALS_ROOT/...`). `MACHINE_KEY=..` writes notes one directory up and makes `_raw_note_count` scan the wrong tree — in a function whose stated job is failing closed. Fix: require the first char to be alphanumeric (`[A-Za-z0-9][A-Za-z0-9._-]*`) and reject `.`/`..` explicitly.
- _paths.py:95 (`canonical_machine`, registry block) | med | Two holes in the same block: (a) `json.loads(...).get(...)` raises `AttributeError` if `fleet_nodes.json` ever holds a list/scalar, and `AttributeError` is not in the `except (OSError, ValueError, TypeError)` tuple — a malformed registry crashes every caller instead of falling back; (b) the returned `key` comes from the file and is never re-validated against the safe-char regex, so an unsafe registry key bypasses the guard entirely. Fix: add `AttributeError` to the except tuple and run `key` through the same `fullmatch` before returning it.
- cursor/cursor_lib.py:~205 (`do_import` → `_connect(db or db_path(machine))`) | med | Production always opens the new shard `_db/<machine>.db`, so the existing `cursor_sessions.db` is silently orphaned: its history stops being visible in `stats()`, and the whole `_connect` legacy-migration block (including the `sessions_legacy` guard) is unreachable except via the test's explicit `db=` argument — i.e. the migration is tested but never actually runs. The module docstring also still promises `brain_evidence` / `brain_sessions_index` / `distill_queue` pick it up, and nothing in this diff repoints them at the new path. Fix: on first run, if the shard file is absent and `cursor_sessions.db` exists, move it to `db_path(machine)` and let `_connect` migrate it; update (or at minimum name in the commit) the downstream readers.
- cursor/cursor_lib.py:~62 and grok/grok_lib.py:~101 (`machine_name`) | med | `if '_paths' in globals(): return _paths.machine_key()` — the name `_paths` is bound by `import _paths` even when the *next* statement (`_paths.originals_root()`) raises, and a peer still running an older `_paths.py` has no `machine_key`, so this raises `AttributeError` with no fallback and takes the whole importer down. On a fleet where rollout skew is the normal state, this fails open in the wrong direction. Fix: `fn = getattr(_paths, 'machine_key', None)` and fall through to the `menv`/env branch when it's missing.
- cursor/cursor_lib.py:~230 / grok/grok_lib.py:~310 (`FRESHNESS.unlink(missing_ok=True)`) | med | The old `_freshness.json` is deleted, but nothing in this diff repoints the watchdogs that consume it. If any `output_freshness`-style watcher keys on that filename, it goes from "stale" to "file gone" — which usually reads as no signal, not as red. Fix: land the watcher change in the same commit, or leave a one-line pointer JSON (`{"moved_to": "_freshness/<machine>.json"}`) instead of unlinking.
- grok/grok_export.cmd:5 | low | The `for /f` reader takes `PYTHON_EXE`'s value verbatim; the Python-side parser this replaces did `.strip().strip('\'"')` and stripped trailing `# comment`, which is evidence that quoted/commented values occur in `machine.env`. A quoted value makes `"%PY%"` expand to `""C:\...\python.exe""` and the task dies with a confusing error. Fix: strip surrounding quotes (`set PY=%PY:"=%`) and trailing comment, or drop the parsing and call `python -c` via an already-resolved launcher.
- grok/grok_lib.py:~330 (`_INJECTED_WRAPPER`) | low | The injection filter is a denylist of known wrapper tags, so any *new* harness wrapper is archived verbatim as dev's words — the opposite of the docstring's promise. Your own test only proves the denylist covers the tags already in it. Fix: invert the default for turns that contain no `<user_query>` but do contain a leading `<tag>…</tag>` wrapper at position 0, and count them in `dropped_injected_user_turns` so the drop stays visible.
- cursor/_test_cursor.py:~30 and grok/_test_grok.py:~20 | low | Neither test patches `FRESHNESS`, so running them calls `FRESHNESS.unlink(missing_ok=True)` on the **real** repo files `cursor/_freshness.json` and `grok/_freshness.json`. Harmless today only because those files are meant to be absent; still, a test that mutates the working tree outside its tmpdir. Fix: patch `C.FRESHNESS` / `G.FRESHNESS` into `_TMP` like every other path.
- cursor/cursor_lib.py:~195 (`_connect`, legacy branch) | low | `needs_migration` fires when *either* `content_hash` or `exported_at` is missing, but the copy branch is chosen on `'content_hash' in legacy` alone and then SELECTs `exported_at` — an intermediate schema with a hash but no `exported_at` raises `OperationalError` and aborts the import. Fix: gate the branch on both columns being present.
- cursor/cursor_lib.py:~215 | low | `dst.stat().st_mtime_ns != src_stat.st_mtime_ns` will mismatch forever on filesystems that round mtime (FAT/SMB targets), re-copying every original on every run and inflating the `copied` count. Size+`st_mtime` with a ~1s tolerance, or a content hash, is the AK-47 form here.

===VERDICT=== REQUEST_CHANGES
