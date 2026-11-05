---
session: s_78a620ce
date: 2026-09-21
words: 5777
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are an INDEPENDENT senior code reviewer. The diff below was written by a

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_78a620ce` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are an INDEPENDENT senior code reviewer. The diff below was written by a
DIFFERENT AI coding agent (OpenAI Codex). Your job is to catch what it got wrong,
acting as an adversarial second pair of eyes. Be specific and grounded in the diff.

Review for, in priority order:
1. CORRECTNESS bugs (logic errors, off-by-one, wrong conditions, broken edge cases,
   null/empty/overflow, race conditions, resource leaks).
2. SECURITY (injection, unsafe input, secret handling, auth/permission gaps).
3. BREAKAGE (does it break existing behavior, contracts, or callers?).
4. SIMPLIFICATION / reuse (clearly over-complex code that should be simpler).

Rules:
- Only report issues you can justify from the diff. No vague "consider maybe".
- For each finding: file:line (best effort) - severity [HIGH/MED/LOW] - what's wrong - the fix.
- If the change is clean, say so plainly. Do not invent problems.

End with exactly one VERDICT line:
VERDICT: APPROVE   (no blocking issues)
or
VERDICT: REQUEST_CHANGES   (1+ MED/HIGH issues)

Output clean Markdown. Start with a one-line summary, then findings, then the VERDICT line.

## TASK Codex was asked to do
Adversarially review the local shared-file lease provider and exact tests.
Try to falsify these claims: corrupt or mixed-generation SQLite is rejected
byte-identically before DDL; only exact legacy/current schemas migrate under one
serialized transaction; schema and header stamps are read from one snapshot;
foreign and delayed releases cannot remove another epoch; mutation tests really
turn red on broken variants. Scope must exclude workclaim and Telegram code.
Return concrete blocking findings or approve. Do not edit files.

## DIFF (Codex's change), source: git diff 8e2bd22e7..213be6928
```diff
diff --git a/_test_lease_storm.py b/_test_lease_storm.py
index 1c75bda20..1e9b037f1 100644
--- a/_test_lease_storm.py
+++ b/_test_lease_storm.py
@@ -79,9 +79,12 @@ sys.exit(g.main(["--phase", "pre"]))
 """
 
 
-def call_guard(command, cwd, session, env, tool="Bash", file_path=None):
+def call_guard(command, cwd, session, env, tool="Bash", file_path=None,
+               include_epoch=True):
     inp = {"file_path": file_path} if file_path else {"command": command}
     payload = {"tool_name": tool, "tool_input": inp, "cwd": cwd, "session_id": session}
+    if include_epoch:
+        payload["prompt_id"] = "lease-storm-%s" % session
     if env.get("LEASE_STORM_MUTANT"):
         shim = MUTANT_SHIM.format(hooks=os.path.dirname(HOOK))
         argv = [sys.executable, "-c", shim]
@@ -108,6 +111,9 @@ def main():
                 WORKSPACE_WRITE_LEASE_COUNTER=os.path.join(tmp, "usage.jsonl"),
                 WORKSPACE_WRITE_LEASE_MODULE_DIR=SCRIPTS,
                 WORKSPACE_WIDE_ROOTS=container)
+    for inherited_identity in ("CODEX_THREAD_ID", "CODEX_SESSION_ID",
+                               "CLAUDE_CODE_SESSION_ID", "CLAUDE_SESSION_ID"):
+        base.pop(inherited_identity, None)
     os.environ.update({k: base[k] for k in
                        ("WORKSPACE_WRITE_LEASE_DB", "WORKSPACE_WRITE_LEASE_COUNTER")})
     mutant = dict(base, LEASE_STORM_MUTANT="1")
@@ -162,13 +168,21 @@ def main():
         fails.append("8. extract_paths вернул %d элемент(ов) вместо пустоты -> %s" %
                      (len(parsed), parsed[:6]))
 
-    # --- 9. красный-мутант: старое поведение обязано провалить проверку 1 ---------------
+    # A synthetic/old harness that omits the per-turn fencing token must be denied;
+    # weakening this would let a delayed Stop remove a later turn's lease.
+    rc, out = call_guard('sed -i "s/a/b/" "%s"' % other, hot,
+                         "session-no-epoch", base, include_epoch=False)
+    if rc != 2 or "turn_id/prompt_id" not in out:
+        fails.append("9. write без epoch не fail-closed: rc=%s out=%s" %
+                     (rc, out.strip()[:140]))
+
+    # --- 10. красный-мутант: старое поведение обязано провалить проверку 1 --------------
     rc, out = call_guard('sed -i "s/a/b/" "%s"' % other, hot, "session-B", mutant)
     if rc != 2:
-        fails.append("9. МУТАНТ НЕ ПОКРАСНЕЛ: старый хук обязан отбить запись в ДРУГОЙ файл "
+        fails.append("10. МУТАНТ НЕ ПОКРАСНЕЛ: старый хук обязан отбить запись в ДРУГОЙ файл "
                      "занятой папки (rc=%s). Тест ничего не стережёт." % rc)
     elif "BUSY" not in out:
-        fails.append("9. мутант отбил, но не по причине BUSY: %s" % out.strip()[:140])
+        fails.append("10. мутант отбил, но не по причине BUSY: %s" % out.strip()[:140])
 
     lease.release_session("session-A")
     lease.release_session("session-B")
@@ -176,7 +190,7 @@ def main():
         for line in fails:
             print("FAIL " + line)
         return 1
-    print("OK 10/10 lease-storm: папка не лизуется, чтение свободно, запуск != запись, "
+    print("OK 11/11 lease-storm: папка не лизуется, чтение свободно, запуск != запись, "
           "точечная защита цела, мутант краснеет")
     return 0
 
diff --git a/_test_workspace_write_guard.py b/_test_workspace_write_guard.py
index 1afd81a80..d49b1cdc8 100644
--- a/_test_workspace_write_guard.py
+++ b/_test_workspace_write_guard.py
@@ -24,8 +24,9 @@ KILL-LIST (source/config mutation -> case that must fail):
   turn_id/prompt_id блокируется fail-closed``;
 - keep ``agent/<id>`` distinct from ``<id>`` ->
   ``Stop alias agent/session снимает lease plain session``;
-- prefer the Codex subagent's trusted ``CODEX_THREAD_ID`` over a shared root
-  payload session -> ``два Codex sibling не схлопываются в одного holder``;
+- prefer top-level ``agent_id`` (Claude/Codex subagent) or Codex's trusted
+  ``CODEX_THREAD_ID`` over a shared root payload session -> sibling separation
+  checks for both harnesses;
 - remove/misroute Codex Stop -> turnstate_hook registration ->
   ``Codex Stop зарегистрирован на fenced release``;
 - return allow instead of Codex structured deny ->
@@ -270,6 +271,11 @@ def main():
     production_usage_before = _file_size(production_usage)
     root = tempfile.mkdtemp(prefix="codex-shared-safety-test-")
     env = dict(os.environ)
+    # Synthetic identities must not collapse into the real Codex task running this
+    # test. Individual env-fallback/sibling cases add the exact harness variables.
+    for inherited_identity in ("CODEX_THREAD_ID", "CODEX_SESSION_ID",
+                               "CLAUDE_CODE_SESSION_ID", "CLAUDE_SESSION_ID"):
+        env.pop(inherited_identity, None)
     env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "leases.sqlite3")
     env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
     env["WORKSPACE_WRITE_LEASE_MODULE_DIR"] = SCRIPTS
@@ -487,6 +493,60 @@ def main():
                         "turn_id": "root-turn-shared", "cwd": root,
                         "hook_event_name": "Stop"}, "stop", sibling_b_env)
 
+            claude_sibling_target = os.path.join(root, "claude-sibling-fence.md")
+            claude_sibling_a = {
+                "session_id": "claude-root-shared",
+                "prompt_id": "claude-prompt-shared",
+                "agent_id": "claude-agent-A",
+                "agent_type": "Explore",
+                "tool_use_id": "toolu-claude-sibling-a",
+                "cwd": root,
+                "tool_name": "Write",
+                "tool_input": {"file_path": claude_sibling_target},
+            }
+            claude_a = _run_guard(claude_sibling_a, env=env)
+            claude_owner_a = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], claude_sibling_target)
+            claude_sibling_b = dict(claude_sibling_a)
+            claude_sibling_b.update({
+                "agent_id": "claude-agent-B",
+                "agent_type": "general-purpose",
+                "tool_use_id": "toolu-claude-sibling-b",
+            })
+            claude_b_blocked = _run_guard(claude_sibling_b, env=env)
+            claude_a_stop = _run_guard({
+                "session_id": "claude-root-shared",
+                "prompt_id": "claude-prompt-shared",
+                "agent_id": "claude-agent-A",
+                "agent_type": "Explore",
+                "cwd": root,
+                "hook_event_name": "Stop",
+            }, "stop", env)
+            claude_owner_after_stop = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], claude_sibling_target)
+            claude_b_after = _run_guard(claude_sibling_b, env=env)
+            claude_owner_b = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], claude_sibling_target)
+            check("два Claude sibling по agent_id не схлопываются в holder",
+                  claude_a.returncode == 0 and claude_owner_a and
+                  claude_owner_a.get("session") == "claude-agent-A" and
+                  claude_b_blocked.returncode == 2 and
+                  "claude-agent-A" in claude_b_blocked.stderr and
+                  claude_a_stop.returncode == 0 and
+                  claude_owner_after_stop is None and
+                  claude_b_after.returncode == 0 and claude_owner_b and
+                  claude_owner_b.get("session") == "claude-agent-B",
+                  "a=%s owner-a=%r blocked=%s/%r stop=%s after-stop=%r "
+                  "b-after=%s owner-b=%r" %
+                  (claude_a.returncode, claude_owner_a,
+                   claude_b_blocked.returncode, claude_b_blocked.stderr[:180],
+                   claude_a_stop.returncode, claude_owner_after_stop,
+                   claude_b_after.returncode, claude_owner_b))
+            _run_guard({"session_id": "claude-root-shared",
+                        "prompt_id": "claude-prompt-shared",
+                        "agent_id": "claude-agent-B", "cwd": root,
+                        "hook_event_name": "Stop"}, "stop", env)
+
             epoch_target = os.path.join(root, "epoch-fence.md")
             epoch_patch = "*** Begin Patch\[ФАМИЛИЯ] Update File: %s\n@@\n-old\n+new\[ФАМИЛИЯ] End Patch" % epoch_target
             old_turn = {"session_id": "codex-same", "turn_id": "turn-old",
diff --git a/_test_workspace_write_lease.py b/_test_workspace_write_lease.py
index ef2f53cf1..a4e837fda 100644
--- a/_test_workspace_write_lease.py
+++ b/_test_workspace_write_lease.py
@@ -22,6 +22,8 @@ KILL-LIST (source mutation -> case that must fail):
   ``mutation: CLI обязан передавать epoch в acquire/release``.
 - delete the read-only integrity preflight ->
   ``mutation: bypass integrity preflight принимает mixed-generation DB``.
+- remove the read transaction around schema/header preflight ->
+  ``mutation: schema preflight без read snapshot видит mixed-era state``.
 Each production-source mutation (plus the naive race model) is
 executed against an isolated copy/state; an honest gap is
 preferable to claiming a mutation that this suite does not kill.
@@ -360,6 +362,88 @@ def _integrity_mutant(source_file, destination):
     return destination
 
 
+def _snapshot_mutant(source_file, destination):
+    """Remove the read transaction and pause between schema/header reads."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    start = source.index("def _open_readonly(")
+    end = source.index("\n\ndef _migrate_epoch(", start)
+    block = source[start:end]
+    guarded = '        con.execute("BEGIN")\n'
+    if block.count(guarded) != 1:
+        raise AssertionError("snapshot mutation did not match read transaction")
+    block = block.replace(guarded, "", 1)
+    source = source[:start] + block + source[end:]
+    schema_read = (
+        '    table_info = tuple(tuple(row) for row in '
+        'con.execute("PRAGMA table_info(leases)"))\n')
+    pause = schema_read + (
+        '    snapshot_marker = os.environ.get("WORKSPACE_LEASE_SNAPSHOT_MARKER")\n'
+        '    snapshot_release = os.environ.get("WORKSPACE_LEASE_SNAPSHOT_RELEASE")\n'
+        '    if snapshot_marker and snapshot_release:\n'
+        '        with open(snapshot_marker, "wb"):\n'
+        '            pass\n'
+        '        deadline = time.time() + 20.0\n'
+        '        while not os.path.exists(snapshot_release):\n'
+        '            if time.time() >= deadline:\n'
+        '                raise RuntimeError("snapshot mutation release timed out")\n'
+        '            time.sleep(0.01)\n')
+    if source.count(schema_read) != 1:
+        raise AssertionError("snapshot mutation did not match schema read")
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source.replace(schema_read, pause, 1))
+    return destination
+
+
+def _snapshot_mutation_is_red(lease, root):
+    """Force a migration between table_info and header-stamp reads."""
+    os.makedirs(root, exist_ok=True)
+    db = os.path.join(root, "snapshot.sqlite3")
+    preserved = os.path.join(root, "preserved.md")
+    migrated_target = os.path.join(root, "migrated.md")
+    _create_legacy_db(lease, db, preserved)
+    mutant_file = _snapshot_mutant(
+        lease.__file__, os.path.join(root, "workspace_write_lease_snapshot_mutant.py"))
+    marker = os.path.join(root, "table-info-read.marker")
+    release = os.path.join(root, "migration-committed.marker")
+    env = dict(os.environ)
+    env.update({
+        "WORKSPACE_WRITE_LEASE_DB": db,
+        "WORKSPACE_WRITE_LEASE_COUNTER": os.path.join(root, "counter.jsonl"),
+        "WORKSPACE_LEASE_SNAPSHOT_MARKER": marker,
+        "WORKSPACE_LEASE_SNAPSHOT_RELEASE": release,
+    })
+    proc = subprocess.Popen(
+        [sys.executable, mutant_file, "status", "--json"],
+        stdout=subprocess.PIPE, stderr=subprocess.PIPE, env=env)
+    deadline = time.time() + 20.0
+    while not os.path.exists(marker) and proc.poll() is None and time.time() < deadline:
+        time.sleep(0.01)
+    original_db = os.environ["WORKSPACE_WRITE_LEASE_DB"]
+    migrated = None
+    try:
+        if not os.path.exists(marker):
+            raise AssertionError("snapshot mutant never reached the split point")
+        os.environ["WORKSPACE_WRITE_LEASE_DB"] = db
+        migrated = lease.acquire_many(
+            [migrated_target], "snapshot-migrator", "test", 60,
+            epoch="snapshot-migration")
+    finally:
+        os.environ["WORKSPACE_WRITE_LEASE_DB"] = original_db
+        with open(release, "wb"):
+            pass
+    out, err = proc.communicate(timeout=30)
+    decoded_out = out.decode("utf-8", "replace")
+    decoded_err = err.decode("utf-8", "replace")
+    return {
+        "ok": bool(migrated and migrated.ok and proc.returncode != 0 and
+                   "stamped DB has legacy columns" in decoded_err),
+        "rc": proc.returncode,
+        "out": decoded_out[:300],
+        "err": decoded_err[:1000],
+    }
+
+
 def _production_counter_leaks(path, offset, root):
     """Return rows attributable to this isolated test, tolerating other live writers."""
     if not os.path.isfile(path):
@@ -397,7 +481,9 @@ def _migration_child(root, start, lease_file):
     env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "legacy.sqlite3")
     env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
     _wait(start)
-    run = subprocess.run([sys.executable, lease_file, "status", "--json"],
+    # Diagnostics are deliberately read-only; a real mutator must own the one-time
+    # schema migration. `reap` is the smallest write path and preserves live rows.
+    run = subprocess.run([sys.executable, lease_file, "reap"],
                          capture_output=True, text=True, encoding="utf-8",
                          errors="replace", env=env, timeout=30)
     if run.returncode == 0:
@@ -750,6 +836,11 @@ def main():
                 check("mutation: bypass integrity preflight принимает mixed-generation DB",
                       False, "candidate has no _assert_integrity preflight")
 
+            snapshot_mutation = _snapshot_mutation_is_red(
+                lease, os.path.join(root, "snapshot-consistency-mutant"))
+            check("mutation: schema preflight без read snapshot видит mixed-era state",
+                  snapshot_mutation["ok"], snapshot_mutation)
+
         print("== RED-FIRST: тест обязан ловить старую read-then-write гонку ==")
         mutant_wins, mutant_errors = _race("naive", root, target)
         check("мутант даёт >1 winner без crashes",
@@ -1018,6 +1109,11 @@ def main():
                           r.get("outcome") == "released" for r in rows) and
                       any(r.get("event") == "release" and
                           r.get("outcome") == "epoch-mismatch" for r in rows))
+                check("DB fail-closed counter несёт stage и forensic hashes",
+                      any(r.get("event") == "database" and
+                          r.get("outcome") == "blocked" and r.get("stage") and
+                          r.get("db_sha256") and r.get("provider_sha256")
+                          for r in rows))
             leaks = _production_counter_leaks(
                 production_counter, production_counter_before, root)
             check("тест не пишет боевой usage-counter", not leaks,
diff --git a/workspace_write_lease.py b/workspace_write_lease.py
index c7c7d4a82..9971d3dea 100644
--- a/workspace_write_lease.py
+++ b/workspace_write_lease.py
@@ -10,7 +10,7 @@
 Вход/выход
     Python API `acquire_many(..., epoch=turn_id)` / `release_session(..., epoch=turn_id)`;
     CLI `acquire|release-session|check|status|reap`. Успех rc=0, занято rc=7,
-    ошибка аргументов rc=2. Состояние -- локальная SQLite DB под LOCALAPPDATA.
+    небезопасная DB rc=9, ошибка аргументов rc=2. Состояние -- локальная SQLite DB под LOCALAPPDATA.
     Вызов без epoch оставлен только для совместимости прямых legacy-потребителей.
 
 Кто дёргает
@@ -33,13 +33,14 @@
 Тест
     `_test_workspace_write_lease.py`: 8 API-процессов, 2 реальных CLI-писателя,
     BUSY rc=7 + holder, TTL/fencing, чужой release, конкурентная миграция,
-    наивная модель и десять production-source мутантов.
+    наивная модель и production-source мутанты всех критичных инвариантов.
 
 updated: 2026-09-21
 """
 from __future__ import annotations
 
 import argparse
+import hashlib
 import io
 import json
 import os
@@ -49,13 +50,57 @@ import sys
 import time
 from dataclasses import dataclass, field
 from datetime import datetime, timezone
+from pathlib import Path
 
 DEFAULT_TTL_SEC = int(os.environ.get("WORKSPACE_WRITE_LEASE_TTL_SEC") or 1800)
 BUSY_TIMEOUT_MS = 10000
+APPLICATION_ID = 0x57574C53  # ASCII "WWLS" -- Workspace Write Lease Store
+SCHEMA_VERSION = 1
+DB_ERROR_RC = 9
 # Rows that existed before the epoch column was added must be distinguishable from
 # *new* legacy callers that intentionally acquire with epoch="".  A token-aware
 # Stop may consume this one-time handoff marker, but must never wildcard fresh rows.
 LEGACY_MIGRATED_EPOCH = "__workspace_lease_legacy_migrated_v1__"
+LEGACY_COLUMNS = ("resource", "session", "agent", "host", "cwd",
+                  "acquired", "expires", "note")
+CURRENT_COLUMNS = LEGACY_COLUMNS + ("epoch",)
+EXPECTED_INDEXES = {
+    "sqlite_autoindex_leases_1": ("resource",),
+    "ix_workspace_leases_expires": ("expires",),
+    "ix_workspace_leases_session": ("session",),
+    "ix_workspace_leases_owner": ("session", "epoch"),
+}
+EXPECTED_LEGACY_TABLE_INFO = (
+    (0, "resource", "TEXT", 0, None, 1),
+    (1, "session", "TEXT", 1, None, 0),
+    (2, "agent", "TEXT", 1, None, 0),
+    (3, "host", "TEXT", 1, None, 0),
+    (4, "cwd", "TEXT", 0, None, 0),
+    (5, "acquired", "REAL", 1, None, 0),
+    (6, "expires", "REAL", 1, None, 0),
+    (7, "note", "TEXT", 0, None, 0),
+)
+EXPECTED_CURRENT_TABLE_INFO = EXPECTED_LEGACY_TABLE_INFO + (
+    (8, "epoch", "TEXT", 1, "''", 0),
+)
+EXPECTED_INDEX_META = {
+    "sqlite_autoindex_leases_1": (1, "pk", 0),
+    "ix_workspace_leases_expires": (0, "c", 0),
+    "ix_workspace_leases_session": (0, "c", 0),
+    "ix_workspace_leases_owner": (0, "c", 0),
+}
+
+
+class LeaseDatabaseError(RuntimeError):
+    """The local mutex store is unsafe to read or mutate."""
+
+
+class LeaseDatabaseCorruptError(LeaseDatabaseError):
+    """SQLite opened the file, but integrity_check did not return one `ok`."""
+
+
+class LeaseDatabaseContractError(LeaseDatabaseError):
+    """The DB is structurally valid SQLite but not this provider's exact schema."""
 
 
 def _state_dir():
@@ -178,24 +223,239 @@ def is_wide_root(path):
     return value in wide_roots()
 
 
+def _sha256_file(path):
+    digest = hashlib.sha256()
+    with open(path, "rb") as fh:
+        for chunk in iter(lambda: fh.read(1024 * 1024), b""):
+            digest.update(chunk)
+    return digest.hexdigest()
+
+
+def _db_error_facts(path, stage, detail):
+    facts = {
+        "stage": stage,
+        "path": os.path.abspath(path),
+        "detail": str(detail)[:2000],
+        "pid": os.getpid(),
+        "ppid": os.getppid(),
+        "python": sys.version.split()[0],
+        "sqlite": sqlite3.sqlite_version,
+        "executable": sys.executable,
+    }
+    try:
+        stat = os.stat(path)
+        facts.update({"size": stat.st_size, "mtime_ns": stat.st_mtime_ns,
+                      "db_sha256": _sha256_file(path)})
+    except Exception as exc:
+        facts["stat_error"] = "%s: %s" % (type(exc).__name__, exc)
+    for suffix in ("-wal", "-shm", "-journal"):
+        sidecar = path + suffix
+        try:
+            stat = os.stat(sidecar)
+            facts[suffix[1:] + "_size"] = stat.st_size
+            facts[suffix[1:] + "_mtime_ns"] = stat.st_mtime_ns
+        except FileNotFoundError:
+            facts[suffix[1:] + "_size"] = 0
+        except Exception as exc:
+            facts[suffix[1:] + "_error"] = "%s: %s" % (type(exc).__name__, exc)
+    try:
+        facts["provider_sha256"] = _sha256_file(__file__)
+    except Exception as exc:
+        facts["provider_hash_error"] = "%s: %s" % (type(exc).__name__, exc)
+    return facts
+
+
+def _raise_db_error(error_type, path, stage, detail):
+    facts = _db_error_facts(path, stage, detail)
+    count_event("database", "blocked", facts)
+    raise error_type("%s: %s" % (stage, detail))
+
+
+def _assert_integrity(con, stage, path=None):
+    path = path or db_path()
+    try:
+        rows = [str(row[0]) for row in con.execute("PRAGMA integrity_check")]
+    except sqlite3.DatabaseError as exc:
+        _raise_db_error(LeaseDatabaseCorruptError, path, stage,
+                        "integrity_check failed: %s" % exc)
+    if rows != ["ok"]:
+        _raise_db_error(LeaseDatabaseCorruptError, path, stage,
+                        "integrity_check=%r" % rows[:20])
+
+
+def _schema_snapshot(con):
+    table_info = tuple(tuple(row) for row in con.execute("PRAGMA table_info(leases)"))
+    indexes = {}
+    for row in con.execute("PRAGMA index_list(leases)"):
+        name = str(row[1])
+        columns = tuple(str(item[2]) for item in con.execute(
+            "SELECT seqno,cid,name FROM pragma_index_info(?) ORDER BY seqno", (name,)))
+        indexes[name] = {
+            "columns": columns,
+            "meta": (int(row[2]), str(row[3]), int(row[4])),
+        }
+    tables = tuple(str(row[0]) for row in con.execute(
+        "SELECT name FROM sqlite_master WHERE type='table' "
+        "AND name NOT LIKE 'sqlite_%' ORDER BY name"))
+    extras = tuple((str(row[0]), str(row[1])) for row in con.execute(
+        "SELECT type,name FROM sqlite_master WHERE type IN ('view','trigger') "
+        "AND name NOT LIKE 'sqlite_%' ORDER BY type,name"))
+    return {
+        "application_id": int(con.execute("PRAGMA application_id").fetchone()[0]),
+        "user_version": int(con.execute("PRAGMA user_version").fetchone()[0]),
+        "table_info": table_info,
+        "tables": tables,
+        "extras": extras,
+        "indexes": indexes,
+    }
+
+
+def _validate_index_shapes(snapshot, path, stage, *, require_all):
+    indexes = snapshot["indexes"]
+    unknown = sorted(set(indexes) - set(EXPECTED_INDEXES))
+    if unknown:
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "unknown indexes: %r" % unknown)
+    if "sqlite_autoindex_leases_1" not in indexes:
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "primary-key autoindex is absent")
+    if require_all and set(indexes) != set(EXPECTED_INDEXES):
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "index set=%r expected=%r" %
+                        (sorted(indexes), sorted(EXPECTED_INDEXES)))
+    for name, value in indexes.items():
+        if (value["columns"] != EXPECTED_INDEXES[name] or
+                value["meta"] != EXPECTED_INDEX_META[name]):
+            _raise_db_error(LeaseDatabaseContractError, path, stage,
+                            "index %s shape=%r" % (name, value))
+
+
+def _validate_preflight_state(snapshot, path, stage, *, allow_empty=False):
+    if not snapshot["tables"] and not snapshot["table_info"]:
+        if (allow_empty and snapshot["application_id"] == 0 and
+                snapshot["user_version"] == 0 and not snapshot["extras"]):
+            return "new"
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "non-new DB has no leases table")
+    if snapshot["tables"] != ("leases",) or snapshot["extras"]:
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "objects tables=%r extras=%r" %
+                        (snapshot["tables"], snapshot["extras"]))
+    table_info = snapshot["table_info"]
+    if table_info == EXPECTED_LEGACY_TABLE_INFO:
+        shape = "legacy"
+    elif table_info == EXPECTED_CURRENT_TABLE_INFO:
+        shape = "current"
+    else:
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "table_info=%r" % (table_info,))
+    app_id = snapshot["application_id"]
+    version = snapshot["user_version"]
+    if app_id == APPLICATION_ID and version == SCHEMA_VERSION:
+        if shape != "current":
+            _raise_db_error(LeaseDatabaseContractError, path, stage,
+                            "stamped DB has legacy columns")
+        _validate_index_shapes(snapshot, path, stage, require_all=True)
+        return "final"
+    if app_id != 0 or version != 0:
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "foreign/partial stamp application_id=%d user_version=%d" %
+                        (app_id, version))
+    _validate_index_shapes(snapshot, path, stage, require_all=False)
+    return shape
+
+
+def _validate_final_schema(con, path, stage):
+    snapshot = _schema_snapshot(con)
+    state = _validate_preflight_state(snapshot, path, stage)
+    if state != "final":
+        _raise_db_error(LeaseDatabaseContractError, path, stage,
+                        "schema remained in %s state" % state)
+
+
+def _open_readonly(path=None):
+    path = path or db_path()
+    con = None
+    try:
+        if not os.path.isfile(path) or os.path.getsize(path) == 0:
+            return None
+    except OSError as exc:
+        _raise_db_error(LeaseDatabaseCorruptError, path, "readonly-stat", exc)
+    uri = Path(path).resolve().as_uri() + "?mode=ro"
+    try:
+        con = sqlite3.connect(uri, uri=True, timeout=BUSY_TIMEOUT_MS / 1000.0,
+                              isolation_level=None)
+        con.row_factory = sqlite3.Row
+        con.execute("PRAGMA query_only=ON")
+        con.execute("PRAGMA busy_timeout=%d" % BUSY_TIMEOUT_MS)
+        # Every PRAGMA below must describe one SQLite snapshot. In autocommit mode
+        # a concurrent migrator can otherwise commit between table_info and the
+        # header stamps, producing a false "stamped legacy" mixture.
+        con.execute("BEGIN")
+        _assert_integrity(con, "readonly-preflight", path)
+        snapshot = _schema_snapshot(con)
+        _validate_preflight_state(snapshot, path, "readonly-preflight")
+        return con
+    except LeaseDatabaseError:
+        try:
+            if con is not None:
+                con.close()
+        except Exception:
+            pass
+        raise
+    except (sqlite3.DatabaseError, OSError) as exc:
+        try:
+            if con is not None:
+                con.close()
+        except Exception:
+            pass
+        _raise_db_error(LeaseDatabaseCorruptError, path, "readonly-open", exc)
+
+
 def _migrate_epoch(con):
-    """Add the fencing column once, even when many first-openers race.
+    """Serialize the only accepted legacy/current-unstamped migration.
 
-    The first PRAGMA is the cheap steady-state path.  A legacy database enters a
-    SQLite write transaction and then *rechecks* the schema after obtaining the
-    lock.  Without that second check, two processes can both observe the old
-    schema and the loser raises ``duplicate column name: epoch``.
+    Integrity and exact schema are rechecked *after* the write lock is held.
+    Therefore an existing corrupt or foreign file is rejected before any DDL,
+    while concurrent first-openers cannot both ALTER the legacy table.
     """
-    columns = {str(row["name"]) for row in con.execute("PRAGMA table_info(leases)")}
-    if "epoch" in columns:
-        return
+    path = db_path()
     con.execute("BEGIN IMMEDIATE")
     try:
+        _assert_integrity(con, "migration-pre-ddl", path)
+        snapshot = _schema_snapshot(con)
+        state = _validate_preflight_state(
+            snapshot, path, "migration-pre-ddl", allow_empty=True)
+        if state == "final":
+            con.commit()
+            return
+        if state == "new":
+            con.execute("""CREATE TABLE leases(
+                resource TEXT PRIMARY KEY,
+                session TEXT NOT NULL,
+                agent TEXT NOT NULL,
+                host TEXT NOT NULL,
+                cwd TEXT,
+                acquired REAL NOT NULL,
+                expires REAL NOT NULL,
+                note TEXT,
+                epoch TEXT NOT NULL DEFAULT ''
+            )""")
         columns = {str(row["name"]) for row in con.execute("PRAGMA table_info(leases)")}
         if "epoch" not in columns:
             con.execute("ALTER TABLE leases ADD COLUMN epoch TEXT NOT NULL DEFAULT ''")
             con.execute("UPDATE leases SET epoch=? WHERE epoch=''",
                         (LEGACY_MIGRATED_EPOCH,))
+        con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_expires "
+                    "ON leases(expires)")
+        con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_session "
+                    "ON leases(session)")
+        con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_owner "
+                    "ON leases(session,epoch)")
+        con.execute("PRAGMA application_id=%d" % APPLICATION_ID)
+        con.execute("PRAGMA user_version=%d" % SCHEMA_VERSION)
+        _validate_final_schema(con, path, "migration-post-ddl")
+        _assert_integrity(con, "migration-post-ddl", path)
         con.commit()
     except Exception:
         con.rollback()
@@ -204,30 +464,63 @@ def _migrate_epoch(con):
 
 def _connect():
     path = db_path()
-    os.makedirs(os.path.dirname(path), exist_ok=True)
-    con = sqlite3.connect(path, timeout=BUSY_TIMEOUT_MS / 1000.0, isolation_level=None)
-    con.row_factory = sqlite3.Row
-    con.execute("PRAGMA busy_timeout=%d" % BUSY_TIMEOUT_MS)
-    con.execute("""CREATE TABLE IF NOT EXISTS leases(
-        resource TEXT PRIMARY KEY,
-        session TEXT NOT NULL,
-        agent TEXT NOT NULL,
-        host TEXT NOT NULL,
-        cwd TEXT,
-        acquired REAL NOT NULL,
-        expires REAL NOT NULL,
-        note TEXT,
-        epoch TEXT NOT NULL DEFAULT ''
-    )""")
-    _migrate_epoch(con)
-    con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_expires ON leases(expires)")
-    con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_session ON leases(session)")
-    con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_owner "
-                "ON leases(session,epoch)")
-    return con
+    parent = os.path.dirname(path)
+    if parent:
+        os.makedirs(parent, exist_ok=True)
+    state = "new"
+    readonly = _open_readonly(path)
+    if readonly is not None:
+        try:
+            state = _validate_preflight_state(
+                _schema_snapshot(readonly), path, "readonly-preflight")
+        finally:
+            readonly.close()
+    con = None
+    try:
+        con = sqlite3.connect(path, timeout=BUSY_TIMEOUT_MS / 1000.0,
+                              isolation_level=None)
+        con.row_factory = sqlite3.Row
+        con.execute("PRAGMA busy_timeout=%d" % BUSY_TIMEOUT_MS)
+        if state == "final":
+            _assert_integrity(con, "writable-open", path)
+            _validate_final_schema(con, path, "writable-open")
+        else:
+            _migrate_epoch(con)
+        return con
+    except LeaseDatabaseError:
+        try:
+            if con is not None:
+                con.close()
+        except Exception:
+            pass
+        raise
+    except (sqlite3.DatabaseError, OSError) as exc:
+        try:
+            if con is not None:
+                con.close()
+        except Exception:
+            pass
+        _raise_db_error(LeaseDatabaseCorruptError, path, "writable-open", exc)
+
+
+def _prepare_write(con, stage):
+    path = db_path()
+    _assert_integrity(con, stage, path)
+    _validate_final_schema(con, path, stage)
 
 
 def _rows(con, now):
+    columns = tuple(str(row["name"]) for row in con.execute("PRAGMA table_info(leases)"))
+    if columns == LEGACY_COLUMNS:
+        rows = [dict(row) for row in con.execute(
+            "SELECT resource,session,agent,host,cwd,acquired,expires,note "
+            "FROM leases WHERE expires>? ORDER BY resource", (float(now),))]
+        for row in rows:
+            row["epoch"] = LEGACY_MIGRATED_EPOCH
+        return rows
+    if columns != CURRENT_COLUMNS:
+        _raise_db_error(LeaseDatabaseContractError, db_path(), "row-read",
+                        "column names=%r" % (columns,))
     return [dict(row) for row in con.execute(
         "SELECT resource,session,agent,host,cwd,acquired,expires,note,epoch "
         "FROM leases WHERE expires>? ORDER BY resource", (float(now),))]
@@ -276,6 +569,7 @@ def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, no
     con = _connect()
     try:
         con.execute("BEGIN IMMEDIATE")
+        _prepare_write(con, "acquire-prewrite")
         reaped = con.execute("DELETE FROM leases WHERE expires<=?", (now,)).rowcount
         live = _rows(con, now)
         conflicts = []
@@ -348,6 +642,7 @@ def release_session(session, *, epoch=None):
     con = _connect()
     try:
         con.execute("BEGIN IMMEDIATE")
+        _prepare_write(con, "release-prewrite")
         n = con.execute("DELETE FROM leases WHERE session=? AND epoch=?",
                         (session, exact_epoch)).rowcount
         legacy_handoff = con.execute(
@@ -372,6 +667,7 @@ def reap(now=None):
     con = _connect()
     try:
         con.execute("BEGIN IMMEDIATE")
+        _prepare_write(con, "reap-prewrite")
         n = con.execute("DELETE FROM leases WHERE expires<=?", (now,)).rowcount
         con.commit()
     finally:
@@ -383,7 +679,9 @@ def reap(now=None):
 def owner_of(path, *, cwd=None, now=None):
     wanted = norm_path(path, cwd)
     now = float(time.time() if now is None else now)
-    con = _connect()
+    con = _open_readonly()
+    if con is None:
+        return None
     try:
         for row in _rows(con, now):
             if overlaps(wanted, row["resource"]):
@@ -395,7 +693,9 @@ def owner_of(path, *, cwd=None, now=None):
 
 def active(now=None):
     now = float(time.time() if now is None else now)
-    con = _connect()
+    con = _open_readonly()
+    if con is None:
+        return []
     try:
         return _rows(con, now)
     finally:
@@ -409,6 +709,7 @@ def release_all_for_tests():
     con = _connect()
     try:
         con.execute("BEGIN IMMEDIATE")
+        _prepare_write(con, "test-cleanup-prewrite")
         con.execute("DELETE FROM leases")
         con.commit()
     finally:
@@ -476,4 +777,9 @@ if __name__ == "__main__":
         sys.stderr.reconfigure(encoding="utf-8")
     except Exception:
         pass
-    sys.exit(main())
+    try:
+        exit_code = main()
+    except LeaseDatabaseError as exc:
+        print("LEASE DB BLOCK: %s" % exc, file=sys.stderr)
+        exit_code = DB_ERROR_RC
+    sys.exit(exit_code)

```

---

**Claude:**

[⏰ оператор написал: понедельник, утро, 09:29, 21 сентября 2026 — начни свой ответ этой меткой времени]

---

> `Bash` -- {"command": "sed -n '1,120p' workspace_write_lease.py", "description": "Read lease provider header"}

---

> `Bash` -- {"command": "grep -n \"def \\|count_event\\|_connect()\\|_open_readonly\" workspace_write_lease.py | head -80", "description": "List functions"}

---

> `Bash` -- {"command": "git cat-file -p 213be6928:workspace_write_lease.py > /tmp/wwl_new.py 2>&1; wc -l /tmp/wwl_new.py; git log --oneline -1 213be6928", "description": "Extract post-change file"}

---

> `Bash` -- {"command": "sed -n '220,560p' /tmp/wwl_new.py", "description": "Read new provider core"}

---

> `Bash` -- {"command": "sed -n '560,790p' /tmp/wwl_new.py", "description": "Read acquire/release/main"}

---

> `Bash` -- {"command": "git show 213be6928 --stat | head -20; echo ---; git cat-file -p 213be6928:hooks/workspace_write_guard.py > /tmp/wg.py 2>/dev/null && grep -n \"LeaseDatabaseError\\|owner_of\\|active(\\|acquire_many\\|release_session\\|except \\|import lease\\|_lease\\b\" /tmp/wg.py | head -60", "descrip

---

> `Bash` -- {"command": "ls hooks/workspace_write_guard.py 2>/dev/null || find . -maxdepth 3 -name \"workspace_write_guard.py\" 2>/dev/null | head", "description": "Locate guard hook"}

---

> `Bash` -- {"command": "find \"C:/Users/dev/.claude\" -maxdepth 3 -name \"workspace_write_guard.py\" 2>/dev/null; find \"C:/Users/dev/.claude\" -maxdepth 3 -name \"turnstate_hook.py\" 2>/dev/null", "description": "Find guard hook on disk"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/hooks\" && grep -n \"LeaseDatabase\\|owner_of\\|acquire_many\\|release_session\\|except Exception\\|def _lease\\|sys.exit\\|return 0\\|return 2\" workspace_write_guard.py | head -60", "description": "Inspect guard hook error handling"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/hooks\" && sed -n '245,338p' workspace_write_guard.py", "description": "Read guard hook decision path"}

---

> `Bash` -- {"command": "cd /tmp && cat > hotjournal_writer.py <<'EOF'\nimport os, sqlite3, sys\ndb = sys.argv[1]\ncon = sqlite3.connect(db, isolation_level=None)\ncon.execute(\"PRAGMA journal_mode=delete\")\ncon.execute(\"PRAGMA synchronous=FULL\")\ncon.execute(\"PRAGMA cache_size=50\")\ncon.execute(\"BEGIN IM

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; rm -rf \"$W\"; mkdir -p \"$W\"; cp /tmp/wwl_new.py \"$W/wwl_new.py\" 2>/dev/null || git cat-file -p 213be6928:workspace_write_lease.py > \"$W/wwl_new.py\"; cat > \"$W/hotjournal_writer.py\" <<'EOF'\nimport os, sqlite3, sys\ndb = sys.a

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_DB=\"$W/leases.sqlite3\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\";\npython -c \"\nimport importlib.util\nspec=importlib.util.spec_from_file_location('wwl',r'$W/wwl_new.py'); m=importlib.uti

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_DB=\"$W/leases.sqlite3\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"; rm -f \"$W/leases.sqlite3\"*\npython -c \"\nimport sys; sys.path.insert(0,r'$W')\nimport wwl_new as m\nc=m._connect(); c.c

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_DB=\"$W/leases.sqlite3\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"\ncp \"$W/leases.sqlite3\" \"$W/bak.db\"; cp \"$W/leases.sqlite3-journal\" \"$W/bak.db-journal\"\npython -c \"\nimport sys; 

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; git cat-file -p 8e2bd22e7:workspace_write_lease.py > \"$W/wwl_old.py\"\ncp \"$W/bak.db\" \"$W/leases.sqlite3\"; cp \"$W/bak.db-journal\" \"$W/leases.sqlite3-journal\"\nexport WORKSPACE_WRITE_LEASE_DB=\"$W/leases.sqlite3\"; export WORK

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; git cat-file -p 213be6928^:workspace_write_lease.py > \"$W/wwl_old.py\" && head -3 \"$W/wwl_old.py\"\ncp \"$W/bak.db\" \"$W/leases.sqlite3\"; cp \"$W/bak.db-journal\" \"$W/leases.sqlite3-journal\"\nexport WORKSPACE_WRITE_LEASE_DB=\"$W

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"\ncp \"$W/bak.db\" \"$W/leases.sqlite3\"; cp \"$W/bak.db-journal\" \"$W/leases.sqlite3-journal\"\npython -c \"\nimport sqlite3\ndb=r'$W/leases.sqlite3'\ncon=sqlite3.connect(db, timeout=10, isolation_level=None)   # the pre-change _conne

---

> `Bash` -- {"command": "git cat-file -p 213be6928:_test_lease_storm.py | sed -n '1,60p'", "description": "Check which hook the storm test targets"}

---

> `Bash` -- {"command": "git rev-parse 213be6928 2>&1; git cat-file -p 213be692812ade69cf57783c50771213e30bbfd7:_test_lease_storm.py 2>&1 | sed -n '1,45p'", "description": "Re-resolve commit and read storm test"}

---

> `Bash` -- {"command": "C=213be692812ade69cf57783c50771213e30bbfd7; git ls-tree --name-only $C | grep -i \"lease\\|write_guard\" ; echo \"--- prefix?\"; git rev-parse --show-prefix", "description": "List tree entries for lease files"}

---

> `Bash` -- {"command": "C=213be692812ade69cf57783c50771213e30bbfd7; for i in 1 2 3; do git cat-file -t $C && break; sleep 1; done; git cat-file -p $C 2>&1 | head -5", "description": "Retry reading commit object"}

---

> `Bash` -- {"command": "grep -n \"^HOOK\\|HOOK =\\|SCRIPTS =\\|hooks\" _test_lease_storm.py | head -20; echo \"=== guard test ===\"; grep -n \"^HOOK\\|HOOK =\\|SCRIPTS =\\|GUARD\" _test_workspace_write_guard.py | head -20", "description": "Find hook paths used by tests"}

---

> `Bash` -- {"command": "ls _test_workspace_write*.py _test_lease*.py workspace_write_lease.py 2>&1; echo \"---\"; grep -n \"turn_id\\|prompt_id\\|epoch\" \"C:/Users/dev/.claude/hooks/workspace_write_guard.py\" | head -20", "description": "Check which test/hook files exist locally"}

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"\n# (a) header-only DB with no tables\nrm -f \"$W/a.db\"*; export WORKSPACE_WRITE_LEASE_DB=\"$W/a.db\"\npython -c \"\nimport sqlite3,os,sys; sys.path.insert(0,r'$W')\nc=sqlite3.co

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; grep -n \"def _open_readonly\\|con.execute(\\\"BEGIN\\\")\\|_raise_db_error(LeaseDatabaseCorruptError, path, \\\"readonly-open\\\"\\|readonly = _open_readonly(path)\\|if state == \\\"final\\\":\\|_validate_final_schema(con, path, \\\"

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"; rm -f \"$W/p.db\"*; export WORKSPACE_WRITE_LEASE_DB=\"$W/p.db\"\npython -c \"\nimport sys,os,time,sqlite3; sys.path.insert(0,r'$W')\nimport wwl_new as new, wwl_old as old\nfor m

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"\npython -c \"\nimport sys,os,time; sys.path.insert(0,r'$W')\nimport wwl_new as m\ndb=r'$W/big.db'; os.environ['WORKSPACE_WRITE_LEASE_DB']=db\nfor f in os.listdir(r'$W'):\n    if 

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"\npython -c \"\nimport sys,os,time,sqlite3; sys.path.insert(0,r'$W')\nimport wwl_new as m\ndb=r'$W/big.db'; os.environ['WORKSPACE_WRITE_LEASE_DB']=db\norig=m._assert_integrity\nm.

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"\npython -c \"\nimport sys,os,time; sys.path.insert(0,r'$W')\nimport wwl_new as m\nos.environ['WORKSPACE_WRITE_LEASE_DB']=r'$W/big.db'\norig=m._assert_integrity\ndef bench(n=30):\

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/usage.jsonl\"\npython -c \"\nimport sys,os,time,sqlite3; sys.path.insert(0,r'$W')\nimport wwl_new as m\nos.environ['WORKSPACE_WRITE_LEASE_DB']=r'$W/big.db'; db=r'$W/big.db'\ndef t(fn,n=40):\n 

---

> `Bash` -- {"command": "W=\"C:/Users/dev/AppData/Local/Temp/leasereview\"; export WORKSPACE_WRITE_LEASE_COUNTER=\"$W/brick.jsonl\"; export WORKSPACE_WRITE_LEASE_DB=\"$W/leases.sqlite3\"\ncp \"$W/bak.db\" \"$W/leases.sqlite3\"; cp \"$W/bak.db-journal\" \"$W/leases.sqlite3-journal\"; rm -f \"$W/brick.jsonl\"\n

---

**Claude:**

Codex's hardening is real and mostly well-built, but the new read-only preflight turns recoverable SQLite states into a permanent machine-wide write block, and I reproduced two of them.

## Findings

### 1. `workspace_write_lease.py:376-412` + `:465-471` — **HIGH** — a crashed writer permanently bricks the whole mutex

`_open_readonly()` opens the DB with `mode=ro` and immediately runs `PRAGMA integrity_check`. A read-only SQLite connection **cannot roll back a hot rollback journal** — it returns `SQLITE_READONLY_ROLLBACK`. That `sqlite3.OperationalError` is caught at `:407` and converted to `LeaseDatabaseCorruptError`. Because `_connect()` calls `_open_readonly()` *first* (`:471`), every entry point dies: `acquire_many`, `release_session`, `reap`, `owner_of`, `active`, CLI `status`/`check`.

Reproduced end to end (crashed writer with a spilled page cache, then the same file through both paths):

```
active  RAISED LeaseDatabaseCorruptError readonly-preflight: integrity_check failed: attempt to write a readonly database
acquire RAISED LeaseDatabaseCorruptError readonly-preflight: integrity_check failed: attempt to write a readonly database

# same file, plain read-write connect (the pre-change path):
rw integrity: [('ok',)]   rows: (0,)   # journal recovered, file healthy, 0 ms
```

The DB is not corrupt. The pre-change code recovered it automatically. Worse, this is the *exact* scenario the mutex exists for — a killed AI session — and `guard_pre()` catches `Exception` and returns `Decision(False)`, so a single crashed writer denies **every** Write/Edit/patch on the machine until a human deletes the file by hand.

**Fix:** don't let the read-only probe be authoritative about corruption. Either (a) catch `SQLITE_READONLY_ROLLBACK` / `SQLITE_READONLY_RECOVERY` / `SQLITE_BUSY_RECOVERY` specifically and fall through to the writable path (which re-runs the same integrity + exact-schema checks under `BEGIN IMMEDIATE` anyway), or (b) do the recovery open first (read-write, no DDL) and only then run the contract preflight. Add a red-first test: crash a writer mid-transaction, assert the next `acquire_many` succeeds.

### 2. `workspace_write_lease.py:333, 339, 471` — **MED** — `_connect()` can never reach its own `state == "new"` self-heal branch

`_migrate_epoch()` handles an existing-but-table-less DB via `allow_empty=True` (`:429-441`) — but `_open_readonly()` validates first with the default `allow_empty=False`, so that branch is dead for any file larger than 0 bytes. An empty-but-structurally-fine DB (header written, `leases` absent — reachable from an aborted DDL, a restored backup, or a diagnostic `sqlite3` shell) is treated as hostile:

```
size 8192
active  RAISED LeaseDatabaseContractError readonly-preflight: non-new DB has no leases table
acquire RAISED LeaseDatabaseContractError readonly-preflight: non-new DB has no leases table
```

The honest answer is "no leases, create the table" — the code already knows how. **Fix:** pass `allow_empty=True` at `readonly-preflight` and let `state == "new"` flow to `_migrate_epoch`, which re-validates under the write lock.

### 3. Contract break — **MED** — `owner_of` / `active` / `release_session` / `reap` went from total to raising, and only the CLI was updated

`:777-782` wraps `main()` in `except LeaseDatabaseError → rc 9`. Nothing else was. In-process importers get a new unchecked exception type. The PreToolUse path survives by accident (`guard_pre` catches bare `Exception`), but the Stop path calls `lease.release_session(sid)` with no guard, so the **only** mechanism that frees leases dies on exactly the DB state that blocks acquisition. Combined with finding 1 there is no release valve at all: acquire is denied, Stop traces back, leases leak.

**Fix:** either make Stop/release degrade to a logged no-op on `LeaseDatabaseError`, or ship the caller updates in this same commit. Shipping a new exception class without touching its consumers is the breakage.

### 4. `workspace_write_lease.py:484-486` — **LOW/MED** — the "one snapshot" invariant is enforced in only one of the two places that need it

The new `con.execute("BEGIN")` at `:394` and the new kill-list entry both assert that schema and header stamps come from one snapshot. But the `state == "final"` fast path calls `_assert_integrity` and `_validate_final_schema` on a plain autocommit connection — `_schema_snapshot` reads `table_info`, then `application_id`, then `user_version` as three separate read transactions. That is the identical split the comment at `:391-393` says must not happen. Not currently exploitable (final→final is monotone), but `_snapshot_mutant` only patches `_open_readonly`, so the kill-list claim is one-sided. **Fix:** wrap the `writable-open` validation in `BEGIN` too, or drop it and rely on `_prepare_write`, which is already inside `BEGIN IMMEDIATE`.

### 5. `workspace_write_lease.py:234-263` — **LOW** — forensics amplify the outage

`_db_error_facts` SHA-256s the entire DB *and* the provider file on every single blocked call, then appends the result to `usage.jsonl`. Measured on the bricked 1.4 MB DB from finding 1: **7.4 ms and 753 bytes per denied tool call**, unbounded for as long as the brick lasts. **Fix:** hash once and memoize per process, or cap by file size.

### 6. `workspace_write_lease.py:465-486` — **LOW** — two connections and two full `integrity_check` per `_connect()`

Measured on an 11.3 MB DB holding **zero** live rows (SQLite never shrinks and this provider never `VACUUM`s): `_connect()+close` = 3.74 ms vs 0.28 ms for a plain connect. `integrity_check` itself was ~1 ms warm, so the cost is mostly the duplicated connection — but it scales with a file that only grows, on a hook that runs on every tool call.

### 7. `workspace_write_lease.py:394, 682, 696` — **LOW** — read transaction held across the whole read

`_open_readonly` leaves `BEGIN` open for the connection's lifetime, and `owner_of`/`active` keep it across the `_rows` loop. A concurrent writer's `BEGIN IMMEDIATE` still gets RESERVED, but its **COMMIT** now waits on that SHARED lock, up to the 10 s busy timeout. These were autocommit reads before.

### 8. `_test_workspace_write_lease.py` `_snapshot_mutation_is_red` — **LOW** — test crashes instead of reporting red

`proc.communicate(timeout=30)` sits *outside* the `try/finally`. If the parent's `acquire_many` raises (a plausible outcome if the mutation ever stops matching), the exception propagates past the `finally` and the child is never reaped — the suite dies rather than printing a clean failure. Move `communicate` into the `finally` or a second `try`.

### On the claims you asked me to falsify

- *"corrupt or mixed-generation SQLite is rejected byte-identically before DDL"* — holds for genuinely corrupt files, but **over-rejects**: findings 1 and 2 show two healthy states classified as unsafe.
- *"only exact legacy/current schemas migrate under one serialized transaction"* — holds; `BEGIN IMMEDIATE` + post-DDL revalidation is correct.
- *"schema and header stamps are read from one snapshot"* — holds in `_open_readonly`, **false at `writable-open`** (finding 4).
- *"foreign and delayed releases cannot remove another epoch"* — **not fully true.** `release_session` (`:648-652`) deletes every `LEGACY_MIGRATED_EPOCH` row for the session regardless of the caller's epoch, so during the migration window a delayed Stop from an older turn does remove a row written by a different turn. It is documented as intentional in the docstring, so I'm not calling it a bug — but nothing in the new tests pins that boundary.
- *"mutation tests turn red on broken variants"* — `_snapshot_mutant` is well-constructed and self-asserting on drift, but it is one-sided (see 4) and no test covers the crash-recovery regression in finding 1.
- Scope: clean. The diff touches only the lease provider and its three tests — no workclaim, no Telegram.

> 🧒 Простыми словами: Codex поставил на замок «проверку на порчу», но проверяет он через замочную скважину — только посмотреть, не потрогать. А после аварийного вылета сессии SQLite оставляет файлик-черновик, который надо *дописать*, чтобы починить. Посмотреть-не-трогая этого не умеет → замок кричит «файл сломан», хотя он целый, и после этого запись на всей машине встаёт намертво, пока человек руками не удалит базу. Я это воспроизвёл. И вторая дверь — снятие замка на Stop — умирает от той же ошибки, то есть выхода из тупика нет вообще.

VERDICT: REQUEST_CHANGES
