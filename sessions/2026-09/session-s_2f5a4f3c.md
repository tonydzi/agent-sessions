---
session: s_2f5a4f3c
date: 2026-09-23
words: 5365
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2f5a4f3c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
diff --git a/codex/_test_external_agent_import_filter.py b/codex/_test_external_agent_import_filter.py
index aa66001d..d6b96ce6 100644
--- a/codex/_test_external_agent_import_filter.py
+++ b/codex/_test_external_agent_import_filter.py
@@ -1,5 +1,5 @@
 # -*- coding: utf-8 -*-
-"""Regression: Claude sessions imported by Codex Harness never enter the Codex lane."""
+"""Regression: Claude/Grok/Cursor sessions imported by Harness never enter the Codex lane."""
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
+    print("PASS: Claude/Grok/Cursor Harness imports are excluded and quarantined")
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
index 00000000..649b059d
--- /dev/null
+++ b/cursor/_test_cursor.py
@@ -0,0 +1,90 @@
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
+def fixture(root, sid, question="проверь синк", answer="Смотрю."):
+    d = root / "proj-x" / "agent-transcripts" / sid
+    d.mkdir(parents=True, exist_ok=True)
+    p = d / (sid + ".jsonl")
+    rows = [
+        {"role": "user", "message": {"content": [{"type": "text", "text":
+            "<timestamp>Tuesday, Sep 22, 2026, 12:48 PM (UTC+1)</timestamp>"
+            "<user_query>%s</user_query>" % question}]}},
+        {"role": "assistant", "message": {"content": [{"type": "text", "text": answer}]}},
+    ]
+    p.write_text("\n".join(json.dumps(x, ensure_ascii=False) for x in rows), encoding="utf-8")
+    return p
+
+
+try:
+    C.VAULT = TMP / "vault"
+    C.DB = TMP / "cursor.db"
+    C.FRESHNESS_ROOT = TMP / "freshness"
+    source = TMP / "source"
+    sid = "same-session-id"
+    fixture(source, sid)
+
+    C.machine_name = lambda: "Node-A"
+    check("Node-A import", C.do_import(source, db=C.DB) == 0)
+    C.machine_name = lambda: "Node-B"
+    check("Node-B import", C.do_import(source, db=C.DB) == 0)
+
+    con = sqlite3.connect(C.DB)
+    check("same session id stays two machine-scoped rows",
+          con.execute("SELECT COUNT(*) FROM sessions").fetchone()[0] == 2)
+    C.machine_name = lambda: "node-a"
+    C.do_import(source, db=C.DB)
+    check("machine-name case drift does not create a third producer",
+          con.execute("SELECT COUNT(*) FROM sessions").fetchone()[0] == 2)
+    C.machine_name = lambda: "Node-B"
+    check("notes are in separate producer lanes",
+          len(list((C.VAULT / "01-Conversations" / "Cursor" / "Node-A").glob("*.md"))) == 1
+          and len(list((C.VAULT / "01-Conversations" / "Cursor" / "Node-B").glob("*.md"))) == 1)
+    check("freshness is per machine",
+          C.freshness_path("Node-A").exists() and C.freshness_path("Node-B").exists()
+          and C.freshness_path("Node-A") != C.freshness_path("Node-B"))
+    f = json.loads(C.freshness_path("Node-B").read_text(encoding="utf-8"))
+    check("freshness proves input=DB=notes", f["unique_input_sessions"] == 1
+          and f["durable_db_sessions"] == 1 and f["durable_notes"] == 1
+          and f["mismatch"] == 0)
+
+    # Same message count, changed bytes: msg_count-only comparison used to lie unchanged.
+    fixture(source, sid, answer="Уже проверил.")
+    C.do_import(source, db=C.DB)
+    body = next((C.VAULT / "01-Conversations" / "Cursor" / "Node-B").glob("*.md")).read_text(encoding="utf-8")
+    check("same-count content change rewrites raw note", "Уже проверил." in body)
+    check("user text is not falsely attributed to dev", "driver: unknown" in body
+          and "account: unknown" in body)
+
+    # Linked note becomes human-owned and must survive a later source refresh.
+    note = next((C.VAULT / "01-Conversations" / "Cursor" / "Node-B").glob("*.md"))
+    linked = note.read_text(encoding="utf-8").replace("related_concepts: []",
+                                                       "related_concepts: [kept]")
+    note.write_text(linked, encoding="utf-8")
+    fixture(source, sid, answer="Третья версия.")
+    C.do_import(source, db=C.DB)
+    check("linked note is preserved", "related_concepts: [kept]" in note.read_text(encoding="utf-8")
+          and "Третья версия." not in note.read_text(encoding="utf-8"))
+finally:
+    shutil.rmtree(TMP, ignore_errors=True)
+
+if FAILS:
+    raise SystemExit("FAIL: " + ", ".join(FAILS))
+print("PASS: Cursor producer lanes and provenance")
diff --git a/cursor/cursor_lib.py b/cursor/cursor_lib.py
index 3a3579fb..1a428532 100644
--- a/cursor/cursor_lib.py
+++ b/cursor/cursor_lib.py
@@ -16,8 +16,8 @@ session_meta нет; id сессии = имя папки, дата = тег <tim
 ЧТО РОЖДАЕТСЯ (те же 4 шага, что у всех трубн волта, §8.3):
     1. оригинал verbatim -> _originals/cursor-sessions/<МАШИНА>/ (идемпотентно);
     2. заметка -> 01-Conversations/Cursor/<МАШИНА>/<дата>-<slug>-<id12>.md;
-    3. SQLite cursor_sessions.db (upsert по session_id, обновление по msg_count);
-    4. _freshness.json -- пульс для сторожей.
+    3. SQLite cursor_sessions.db (upsert по machine+session_id и content_hash);
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
@@ -45,21 +45,31 @@ except Exception:
 
 CURSOR_ROOT = Path(os.path.expanduser('~/.cursor/projects'))
 DB = _HERE / 'cursor_sessions.db'
-FRESHNESS = _HERE / '_freshness.json'
+FRESHNESS_ROOT = _HERE / '_freshness'
 
 
 def machine_name():
-    """MACHINE_NAME из ~/.claude/machine.env -- та же истина, что у codex_lib/_paths."""
+    """MACHINE_KEY from machine.env is the canonical fleet identity."""
+    if os.environ.get('MACHINE_KEY'):
+        return os.environ['MACHINE_KEY'].strip()
     p = os.path.expanduser('~/.claude/machine.env')
     try:
         with open(p, encoding='utf-8') as fh:
-            for line in fh:
-                line = line.strip()
-                if line.startswith('MACHINE_NAME=') and not line.startswith('#'):
-                    return line.split('=', 1)[1].split('#', 1)[0].strip().strip('\'"')
+            rows = list(fh)
+            for wanted in ('MACHINE_KEY', 'MACHINE_NAME'):
+                for line in rows:
+                    line = line.strip()
+                    if line.startswith(wanted + '=') and not line.startswith('#'):
+                        return line.split('=', 1)[1].split('#', 1)[0].strip().strip('\'"')
     except OSError:
         pass
-    return os.environ.get('COMPUTERNAME') or os.uname().nodename
+    return os.environ.get('COMPUTERNAME') or socket.gethostname()
+
+
+def freshness_path(machine):
+    """Один producer = один файл; общий heartbeat в Syncthing снова сделал бы last-writer-wins."""
+    safe = re.sub(r'[^A-Za-z0-9._-]+', '-', (machine or 'unknown')).strip('.-')
+    return FRESHNESS_ROOT / ('%s.json' % (safe or 'unknown'))
 
 
 def _clean(s):
@@ -91,7 +101,7 @@ def _date_of(ts_text, path):
 
 
 def parse_transcript(path):
-    """-> dict(session_id, date, title, project, body_md, msg_count) или None (пустой)."""
+    """-> нормализованная сессия или None. Инъекции Cursor не выдаём за слова оператора."""
     p = Path(path)
     sid = p.stem
     project = p.parent.parent.parent.name if p.parent.parent.parent else '?'
@@ -132,17 +142,19 @@ def parse_transcript(path):
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
@@ -150,50 +162,115 @@ def note_text(r, machine):
                r['title'], r['body_md']))
 
 
-def do_import(root=None):
+def _connect(db=None):
+    """Открыть DB и атомарно поднять старую одноузловую схему до machine+session_id."""
+    con = sqlite3.connect(str(db or DB))
+    con.execute('PRAGMA journal_mode=WAL')
+    cols = {row[1] for row in con.execute('PRAGMA table_info(sessions)')}
+    schema_row = con.execute(
+        "SELECT sql FROM sqlite_master WHERE type='table' AND name='sessions'").fetchone()
+    schema_sql = (schema_row[0] if schema_row else '') or ''
+    needs_migration = cols and ('content_hash' not in cols or 'exported_at' not in cols
+                                or 'COLLATE NOCASE' not in schema_sql.upper())
+    if needs_migration:
+        if con.execute("SELECT 1 FROM sqlite_master WHERE type='table' AND name='sessions_legacy'").fetchone():
+            raise RuntimeError('sessions_legacy already exists; refusing ambiguous DB migration')
+        con.execute('ALTER TABLE sessions RENAME TO sessions_legacy')
+        cols = set()
+    if not cols:
+        con.execute('CREATE TABLE IF NOT EXISTS sessions ('
+                    'machine TEXT COLLATE NOCASE NOT NULL, session_id TEXT NOT NULL, date TEXT, title TEXT, '
+                    'project TEXT, msg_count INT, content_hash TEXT, src_file TEXT, exported_at TEXT, '
+                    'PRIMARY KEY(machine, session_id))')
+        legacy = {row[1] for row in con.execute('PRAGMA table_info(sessions_legacy)')}
+        if legacy:
+            if 'content_hash' in legacy:
+                con.execute('INSERT OR REPLACE INTO sessions '
+                            '(machine,session_id,date,title,project,msg_count,content_hash,src_file,exported_at) '
+                            "SELECT machine,session_id,date,title,project,msg_count,content_hash,src_file,exported_at "
+                            "FROM sessions_legacy ORDER BY CASE WHEN content_hash='' THEN 0 ELSE 1 END")
+            else:
+                con.execute('INSERT OR IGNORE INTO sessions '
+                        '(machine,session_id,date,title,project,msg_count,content_hash,src_file,exported_at) '
+                        "SELECT machine,session_id,date,title,project,msg_count,'',src_file,'' "
+                        'FROM sessions_legacy')
+            con.execute('DROP TABLE sessions_legacy')
+        con.commit()
+    return con
+
+
+def _raw_note_count(machine):
+    d = VAULT / '01-Conversations' / 'Cursor' / machine
+    if not d.exists():
+        return 0
+    return sum(1 for p in d.glob('*.md')
+               if 'source: cursor' in p.read_text(encoding='utf-8', errors='ignore'))
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
+    con = _connect(db)
+    # NOCASE prevents a duplicate identity; keep the displayed spelling equal to MACHINE_KEY.
+    con.execute('UPDATE sessions SET machine=? WHERE machine=? COLLATE NOCASE', (machine, machine))
+    con.commit()
     d_notes = VAULT / '01-Conversations' / 'Cursor' / machine
     d_orig = VAULT.parent / '_originals' / 'cursor-sessions' / machine
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
         if not dst.exists() or dst.stat().st_size != os.path.getsize(f):
             shutil.copy2(f, dst)
             copied += 1
-        old = con.execute('SELECT msg_count FROM sessions WHERE session_id=?',
-                          (r['session_id'],)).fetchone()
-        if old and old[0] == r['msg_count']:
+        old = con.execute('SELECT content_hash FROM sessions WHERE machine=? AND session_id=?',
+                          (machine, r['session_id'])).fetchone()
+        if old and old[0] == r['content_hash']:
             unch += 1
             continue
-        con.execute('INSERT INTO sessions VALUES (?,?,?,?,?,?,?) ON CONFLICT(session_id) DO UPDATE'
-                    ' SET msg_count=excluded.msg_count, title=excluded.title',
-                    (r['session_id'], machine, r['date'], r['title'], r['project'],
-                     r['msg_count'], r['src_file']))
+        now = datetime.datetime.now(datetime.timezone.utc).isoformat()
+        con.execute('INSERT INTO sessions VALUES (?,?,?,?,?,?,?,?,?) '
+                    'ON CONFLICT(machine,session_id) DO UPDATE SET '
+                    'date=excluded.date,title=excluded.title,project=excluded.project,'
+                    'msg_count=excluded.msg_count,content_hash=excluded.content_hash,'
+                    'src_file=excluded.src_file,exported_at=excluded.exported_at',
+                    (machine, r['session_id'], r['date'], r['title'], r['project'],
+                     r['msg_count'], r['content_hash'], r['src_file'], now))
         note = d_notes / ('%s-%s-%s.md' % (r['date'], _slug(r['title']), r['session_id'][-12:]))
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
     print('cursor import [%s]: файлов %d | DB: +%d новых / %d обновлено / %d без изменений | всего %d'
           % (machine, len(files), new, upd, unch, total))
@@ -206,7 +283,7 @@ def stats():
     if not DB.exists():
         print('базы нет, сначала: python cursor_lib.py import')
         return 3
-    con = sqlite3.connect(DB)
+    con = _connect()
     for m, n, d in con.execute('SELECT machine, COUNT(*), MAX(date) FROM sessions GROUP BY machine'):
         print('%s: %d сессий, newest %s' % (m, n, d))
     return 0
diff --git a/grok/_test_grok.py b/grok/_test_grok.py
index 89350f65..f7583251 100644
--- a/grok/_test_grok.py
+++ b/grok/_test_grok.py
@@ -20,7 +20,8 @@ sys.path.insert(0, str(Path(__file__).resolve().parent))
 import grok_lib as G
 G.DB = _TMP / "test.db"
 G.NOTES_DIR = Path(os.environ["CLAUDE_VAULT_ROOT"]) / "01-Conversations" / "Grok" / "conversations"
-G.FRESHNESS = _TMP / "_freshness.json"
+G.FRESHNESS_ROOT = _TMP / "freshness"
+G.machine_name = lambda: "TestNode"
 
 # prod-grok-backend.json shape: conversation (ISO times) + responses[] (BSON/ISO times)
 FIXTURE = [
@@ -92,6 +93,60 @@ check("conversation with no id -> skipped", G.normalize_grok([{"conversation": {
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
+        {"type": "reasoning", "summary": "private reasoning"},
+        {"type": "assistant", "content": answer, "model_id": "grok-test"},
+    ]
+    chat.write_text("\n".join(json.dumps(x, ensure_ascii=False) for x in rows), encoding="utf-8")
+
+
+write_cli("Проверил.")
+G.machine_name = lambda: "Node-A"
+check("CLI Node-A import", G.import_cli(cli_root, db=G.DB) == 0)
+G.machine_name = lambda: "Node-B"
+check("CLI Node-B import", G.import_cli(cli_root, db=G.DB) == 0)
+cli_con = sqlite3.connect(G.DB)
+check("same Grok id stays two machine-scoped rows",
+      cli_con.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0] == 2)
+G.machine_name = lambda: "node-a"
+G.import_cli(cli_root, db=G.DB)
+check("Grok machine-name case drift does not create a third producer",
+      cli_con.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0] == 2)
+G.machine_name = lambda: "Node-B"
+note_a = next((G.VAULT / "01-Conversations" / "Grok" / "CLI" / "Node-A").glob("*.md"))
+body_a = note_a.read_text(encoding="utf-8")
+check("Grok CLI note excludes injected context", "system prompt must stay out" not in body_a
+      and "secret rules" not in body_a and "reminder" not in body_a
+      and "private reasoning" not in body_a and "Проверь общий волт" in body_a)
+check("Grok CLI provenance is honest", "source: grok-cli" in body_a
+      and "machine: Node-A" in body_a and "driver: unknown" in body_a)
+fresh_a = json.loads(G.freshness_path("cli", "Node-A").read_text(encoding="utf-8"))
+fresh_b = json.loads(G.freshness_path("cli", "Node-B").read_text(encoding="utf-8"))
+check("Grok CLI freshness is per machine", fresh_a["mismatch"] == 0
+      and fresh_b["mismatch"] == 0
+      and G.freshness_path("cli", "Node-A") != G.freshness_path("cli", "Node-B"))
+
+write_cli("Изменённый ответ той же длины сообщений.")
+G.import_cli(cli_root, db=G.DB)
+note_b = next((G.VAULT / "01-Conversations" / "Grok" / "CLI" / "Node-B").glob("*.md"))
+check("same-count Grok content change is detected",
+      "Изменённый ответ" in note_b.read_text(encoding="utf-8"))
 
 print()
 if fails:
diff --git a/grok/grok_export.cmd b/grok/grok_export.cmd
new file mode 100644
index 00000000..185362e8
--- /dev/null
+++ b/grok/grok_export.cmd
@@ -0,0 +1,4 @@
+@echo off
+REM Nightly local Grok CLI session export. Each machine owns its note/original/freshness lane.
+set PY=C:\Users\dev\AppData\Local\Programs\Python\Python312\python.exe
+"%PY%" "D:\Vault\_imports\grok\grok_lib.py" cli-import >> "D:\Vault\_imports\grok\_cli_export.log" 2>&1
diff --git a/grok/grok_lib.py b/grok/grok_lib.py
index 1eff4dee..9f8d36d2 100644
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
@@ -40,12 +47,18 @@ except Exception:
 HERE = Path(os.path.dirname(os.path.abspath(__file__)))
 DB = HERE / "grok_conversations.db"
 
-VAULT = Path(os.environ.get("CLAUDE_VAULT_ROOT")
-             or os.environ.get("OBSIDIAN_VAULT")
-             or os.path.expanduser("~/Obsidian/Vault-Knowledge"))
+sys.path.insert(0, str(HERE.parent))
+try:
+    from _paths import VAULT as _VAULT
+    VAULT = Path(_VAULT)
+except Exception:
+    VAULT = Path(os.environ.get("CLAUDE_VAULT_ROOT")
+                 or os.environ.get("OBSIDIAN_VAULT")
+                 or os.path.expanduser("~/Obsidian/Vault-Knowledge"))
 NOTES_DIR = VAULT / "01-Conversations" / "Grok" / "conversations"
 MOC = VAULT / "01-Conversations" / "Grok" / "_Grok-MOC.md"
-FRESHNESS = HERE / "_freshness.json"
+FRESHNESS_ROOT = HERE / "_freshness"
+GROK_CLI_ROOT = Path(os.path.expanduser("~/.grok/sessions"))
 
 SCHEMA = """
 CREATE TABLE IF NOT EXISTS conversations(
@@ -71,6 +84,28 @@ def _clean(s):
     return s.replace("\xa0", " ").strip()
 
 
+def machine_name():
+    if os.environ.get("MACHINE_KEY"):
+        return os.environ["MACHINE_KEY"].strip()
+    p = os.path.expanduser("~/.claude/machine.env")
+    try:
+        with open(p, encoding="utf-8") as fh:
+            rows = list(fh)
+            for wanted in ("MACHINE_KEY", "MACHINE_NAME"):
+                for line in rows:
+                    line = line.strip()
+                    if line.startswith(wanted + "=") and not line.startswith("#"):
+                        return line.split("=", 1)[1].split("#", 1)[0].strip().strip("'\"")
+    except OSError:
+        pass
+    return os.environ.get("COMPUTERNAME") or socket.gethostname()
+
+
+def freshness_path(kind, machine):
+    safe = re.sub(r"[^A-Za-z0-9._-]+", "-", (machine or "unknown")).strip(".-")
+    return FRESHNESS_ROOT / ("%s-%s.json" % (kind, safe or "unknown"))
+
+
 def _parse_time(v):
     """Grok mixes ISO strings and BSON {"$date":{"$numberLong":"ms"}} (and plain ms int).
     Returns (iso_string, day, month) best-effort; ('', '', '') if unparseable."""
@@ -261,13 +296,188 @@ def write_freshness(con):
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
     return newest, total, stale_days
 
 
+# ------------------------------------------------------------------ local CLI sessions
+
+_USER_QUERY = re.compile(r"<user_query>\s*(.*?)\s*</user_query>", re.S | re.I)
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
+                    if not text or (not match and ("<user_info>" in raw or "<rules>" in raw)):
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
+            "content_hash": hashlib.sha256(canonical.encode("utf-8")).hexdigest(),
+            "src_file": str(p)}
+
+
+def _cli_connect(db=None):
+    con = sqlite3.connect(str(db or DB))
+    con.execute("PRAGMA journal_mode=WAL")
+    schema_row = con.execute(
+        "SELECT sql FROM sqlite_master WHERE type='table' AND name='cli_sessions'").fetchone()
+    schema_sql = (schema_row[0] if schema_row else '') or ''
+    if schema_sql and "COLLATE NOCASE" not in schema_sql.upper():
+        if con.execute("SELECT 1 FROM sqlite_master WHERE type='table' AND name='cli_sessions_legacy'").fetchone():
+            raise RuntimeError("cli_sessions_legacy already exists; refusing ambiguous DB migration")
+        con.execute("ALTER TABLE cli_sessions RENAME TO cli_sessions_legacy")
+    con.execute("CREATE TABLE IF NOT EXISTS cli_sessions("
+                "machine TEXT COLLATE NOCASE NOT NULL, session_id TEXT NOT NULL, day TEXT, title TEXT, "
+                "project TEXT, n_turns INT, content_hash TEXT, turns_json TEXT, src_file TEXT, "
+                "exported_at TEXT, PRIMARY KEY(machine, session_id))")
+    if con.execute("SELECT 1 FROM sqlite_master WHERE type='table' AND name='cli_sessions_legacy'").fetchone():
+        con.execute("INSERT OR REPLACE INTO cli_sessions SELECT * FROM cli_sessions_legacy "
+                    "ORDER BY CASE WHEN content_hash='' THEN 0 ELSE 1 END")
+        con.execute("DROP TABLE cli_sessions_legacy")
+        con.commit()
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
+    return sum(1 for p in d.glob("*.md")
+               if "source: grok-cli" in p.read_text(encoding="utf-8", errors="ignore"))
+
+
+def import_cli(root=None, *, db=None):
+    src = Path(root) if root else GROK_CLI_ROOT
+    machine = machine_name()
+    if not src.is_dir():
+        print("grok cli: НЕТ каталога %s -- узлу нечего отдавать" % src)
+        return 0
+    files = sorted(glob.glob(str(src / "**" / "chat_history.jsonl"), recursive=True))
+    con = _cli_connect(db)
+    con.execute("UPDATE cli_sessions SET machine=? WHERE machine=? COLLATE NOCASE", (machine, machine))
+    con.commit()
+    new = updated = unchanged = copied = 0
+    input_ids = set()
+    originals = VAULT.parent / "_originals" / "grok-cli-sessions" / machine
+    originals.mkdir(parents=True, exist_ok=True)
+    for filename in files:
+        row = parse_cli_session(filename)
+        if not row:
+            continue
+        input_ids.add(row["session_id"])
+        raw_dest = originals / (row["session_id"] + ".jsonl")
+        if not raw_dest.exists() or raw_dest.stat().st_size != os.path.getsize(filename):
+            shutil.copy2(filename, raw_dest)
+            copied += 1
+        old = con.execute("SELECT content_hash FROM cli_sessions WHERE machine=? AND session_id=?",
+                          (machine, row["session_id"])).fetchone()
+        if old and old[0] == row["content_hash"]:
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
+        note = _cli_note_path(row)
+        note.parent.mkdir(parents=True, exist_ok=True)
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
+                                  "mismatch": total - notes, "newest_day": newest},
+                                 ensure_ascii=False, indent=2), encoding="utf-8")
+    print("grok cli import [%s]: input %d | DB +%d/%d updated/%d unchanged | total %d | "
+          "notes %d | originals +%d | mismatch %d" %
+          (machine, len(input_ids), new, updated, unchanged, total, notes, copied, total - notes))
+    return 0
+
+
 # ------------------------------------------------------------------ cli
 
 def _load_json(path):
@@ -291,6 +501,11 @@ def do_stats():
     total = con.execute("SELECT COUNT(*) FROM conversations").fetchone()[0]
     turns = con.execute("SELECT COALESCE(SUM(n_turns),0) FROM conversations").fetchone()[0]
     print(f"grok DB: {total} conversations, {turns} turns | {DB}")
+    try:
+        cli_total = con.execute("SELECT COUNT(*) FROM cli_sessions").fetchone()[0]
+        print("grok CLI DB: %d sessions" % cli_total)
+    except sqlite3.OperationalError:
+        print("grok CLI DB: 0 sessions")
 
 
 def main():
@@ -301,6 +516,8 @@ def main():
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

SUMMARY: The provenance/multi-producer rework is directionally right (machine-scoped PK, content_hash instead of msg_count, per-producer freshness, human-owned-note guard), but it ships several real defects: the new Grok test writes into the LIVE vault because `VAULT` now comes from `_paths` and the test never stubs it; freshness output was relocated with no consumer/watchdog migration; Grok CLI note filenames are keyed to file mtime so one session grows duplicate notes and the `mismatch` invariant goes negative; and the "don't archive harness injections as dev's words" filter is a two-tag denylist.

FINDINGS:

- grok/_test_grok.py:117 | high | The CLI test stubs `G.DB` and `G.FRESHNESS_ROOT` into `_TMP` but never stubs `G.VAULT`. With the new `from _paths import VAULT` (grok_lib.py:51) taking precedence over `CLAUDE_VAULT_ROOT`, the previous env-based redirection no longer applies, so `import_cli` writes real notes to `<real vault>/01-Conversations/Grok/CLI/Node-A|Node-B/` and real originals to `<vault>/../_originals/grok-cli-sessions/`. The test then asserts on those live paths and leaves them behind (no cleanup of the vault side). Compare cursor/_test_cursor.py:36, which correctly sets `C.VAULT`. Fix (root, two parts): keep env precedence — try `CLAUDE_VAULT_ROOT`/`OBSIDIAN_VAULT` FIRST and fall back to `_paths.VAULT` — and add `G.VAULT = _TMP / "vault"` in the test before the CLI section.

- grok/grok_lib.py:60, cursor/cursor_lib.py:48 | med | `FRESHNESS = <dir>/_freshness.json` was deleted and replaced by `_freshness/<lane>-<machine>.json`. Nothing in this diff updates the watchdogs/consumers that read the old path (the cursor docstring itself calls `_freshness.json` "пульс для сторожей", and the grok test had to be edited because it referenced `G.FRESHNESS`). Two failure modes: any module importing `cursor_lib.FRESHNESS` / `grok_lib.FRESHNESS` now raises AttributeError, and any age-watchdog still stat-ing the old file will read a frozen, never-updated file forever — i.e. it silently reports the old truth instead of going red. Fix: in the same change, update the consumers (or keep a one-line compatibility write to the legacy path plus a dated removal), and delete the stale `_freshness.json` so no watcher can read it.

- grok/grok_lib.py:362 (`parse_cli_session`, `day = datetime.date.fromtimestamp(p.stat().st_mtime)`) | med | The note filename is `<day>-<slug>-<id12>.md`, and `day` is derived from the source file's mtime. A CLI session that is appended to on a later day changes `day`, so `_cli_note_path` points at a NEW file while the old note stays: one session_id → two notes, one DB row. `_cli_note_count` then exceeds `total`, so `mismatch = total - notes` goes negative — the very invariant the test asserts as 0. (Cursor avoids this by using the transcript's embedded `<timestamp>`, not mtime.) Fix: persist the note path (or a frozen `day`) in the `cli_sessions` row on first insert and reuse it on subsequent imports, instead of recomputing the filename from mutable filesystem metadata.

- grok/grok_lib.py:345 (`parse_cli_session`, user branch) | med | The guard against archiving injected context is `not match and ("<user_info>" in raw or "<rules>" in raw)` — a denylist of exactly two tags. Any other harness-injected user-role block that does not set `synthetic_reason` (e.g. `<system-reminder>`, `<environment_details>`, `<project_context>`, future tags) has no `<user_query>` and no listed tag, so it is archived verbatim as dev's words — exactly the class this change claims to close, and the test only exercises the two known tags. Fix: invert to an allowlist — if `raw` contains any `<...>` harness wrapper and no `<user_query>`, skip the row; only unwrapped plain text or the `<user_query>` capture is admitted.

- cursor/cursor_lib.py:53 and grok/grok_lib.py:87 (`machine_name`) | med | Both now prefer `MACHINE_KEY` (env, then machine.env) over `MACHINE_NAME`, and the cursor docstring line asserting "та же истина, что у codex_lib/_paths" was removed rather than made true. If a node's machine.env carries both keys with different values, cursor/grok file under one producer identity while codex_lib/_paths still uses another — two note lanes, two freshness files, two DB identities for one physical node, which defeats the purpose of the change. Fix: pick one canonical resolver and share it (e.g. import the existing `_paths`/`codex_lib` machine resolver in both modules) rather than duplicating a second precedence order in two places.

- grok/grok_export.cmd:3 | med | Hardcodes `C:\Users\dev\AppData\...\python.exe` and `D:\Vault\_imports\...` in a file that lives inside the fleet-synced `_imports` tree, so it syncs to peers where neither path exists and fails silently into a log. It also appends the log to the synced folder, which is the standard sync-conflict generator. Fix: read the pinned interpreter from `machine.env` (`PYTHON_EXE`) and resolve the script dir with `%~dp0`; write `_cli_export.log` to a machine-local, non-synced path.

- cursor/cursor_lib.py:165 (`_connect`) and grok/grok_lib.py:400 (`_cli_connect`) | med | The docstring says "атомарно", but `ALTER TABLE ... RENAME` and `CREATE TABLE` run in autocommit (Python's sqlite3 only opens implicit transactions for DML), while the copy is committed later. A crash between CREATE and the copy leaves an empty `sessions` plus a populated `sessions_legacy`; the next run sees a complete new schema, skips the copy entirely, and any later migration is permanently blocked by the `refusing ambiguous DB migration` guard. Fix: wrap rename+create+copy+drop in one explicit transaction (`con.execute('BEGIN')` … `con.commit()`) — SQLite DDL is transactional, so this is the one-line correct fix.

- grok/grok_lib.py:412 | low | `INSERT OR REPLACE INTO cli_sessions SELECT * FROM cli_sessions_legacy` relies on identical column count and order between old and new schemas — fragile precisely in the case migrations exist for. Cursor does this correctly with an explicit column list. Fix: name the columns explicitly, mirroring `_connect`.

- cursor/cursor_lib.py:196 | low | After migration every legacy row gets `content_hash=''`, so the first post-upgrade import sees `old[0] != r['content_hash']` for every session and rewrites every existing cursor note in the vault in one pass. Notes a human edited but that still contain `related_concepts: []` are silently overwritten. Fix: either backfill hashes from the existing note bodies during migration, or treat empty `content_hash` as "adopt current note, record hash, do not rewrite".

- cursor/cursor_lib.py:205 (`_raw_note_count`) | low | Reads the full text of every `.md` in the machine's note folder on every import just to count a frontmatter line, and will also count any note that merely quotes `source: cursor` in its body. Fix: read only the frontmatter head (e.g. first 400 bytes) and require the match before the closing `---`.

- cursor/cursor_lib.py:56 / grok/grok_lib.py:104 (`freshness_path`) | low | The sanitizer maps distinct machine names to one filename (`Node A` and `Node-A` → `Node-A.json`), reintroducing the last-writer-wins collision the function exists to prevent. Fix: append a short hash of the raw machine string to the sanitized stem.

- codex/_test_external_agent_import_filter.py:82 | low | The new assertion `fresh["external_agent_registry_ids"] == 3` depends on a freshness key that this diff does not add to `codex_lib` (only a docstring and two print strings changed there). If that key is not already emitted, the test dies with KeyError rather than a useful failure. Worth confirming the producer emits it before merge.

===VERDICT=== REQUEST_CHANGES
