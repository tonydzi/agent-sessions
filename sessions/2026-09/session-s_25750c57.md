---
session: s_25750c57
date: 2026-09-22
words: 932
turns: 2
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are an INDEPENDENT senior code reviewer. Review the Codex diff adversarially for corre…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_25750c57` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are an INDEPENDENT senior code reviewer. Review the Codex diff adversarially for correctness, security, breakage, races, and fail-open attribution. Only justified findings. For each: file:line, severity HIGH/MED/LOW, defect, fix. End exactly VERDICT: APPROVE or VERDICT: REQUEST_CHANGES.

TASK:
Review the test-only change for the Telegram doorbell suite. Production is now an enabled one-minute Windows Scheduled Task. The old final invariant required the live SQLite DB and usage JSONL to remain byte-identical during a roughly 30-second isolated suite, producing false failures whenever the real scheduler overlapped. Immutable source/config must still remain byte-identical. Runtime drift may be accepted only when Task Scheduler proves an overlapping registered run, the usage counter remains append-only, and any visible new rows are complete robot rows inside the suite window. Find race conditions or fail-open attribution, especially cases where the suite itself could mutate production but the new guard would pass.


DIFF:
diff --git a/scripts/_test_tg_doorbell.py b/scripts/_test_tg_doorbell.py
--- a/scripts/_test_tg_doorbell.py
+++ b/scripts/_test_tg_doorbell.py
@@
 import shutil
+import socket
 import sqlite3
@@
-_PROD_TRACKED = (
+_PROD_IMMUTABLE = (
     _PROD_SOURCE,
     _SUITE_FILE,
     os.path.join(_PROD_HOME, ".claude", "doorbell_doors.json"),
+ )
+_PROD_RUNTIME = (
     os.path.join(_PROD_HOME, ".claude", "usage", "tg_doorbell.jsonl"),
     _PROD_DB,
     _PROD_DB + "-wal",
     _PROD_DB + "-shm",
     _PROD_DB + "-journal",
     _PROD_DB + ".mutex",
 )
+_PROD_TRACKED = _PROD_IMMUTABLE + _PROD_RUNTIME
+
+
+def _read_bytes(path):
+    if not os.path.isfile(path):
+        return b""
+    with io.open(path, "rb") as fh:
+        return fh.read()
+
+
+def _production_scheduler_observation():
+    """Return registration, live state, and last-run UTC from Task Scheduler."""
+    if os.name != "nt":
+        return {"registered": False, "state": "", "last_run": None}
+    script = (
+        "$ErrorActionPreference='Stop';"
+        "$t=Get-ScheduledTask -TaskName 'Claude-Codex Telegram Doorbell';"
+        "$i=$t|Get-ScheduledTaskInfo;"
+        "$lr=$null;if($i.LastRunTime.Year -gt 1900){"
+        "$lr=[DateTimeOffset]$i.LastRunTime;};"
+        "[pscustomobject]@{registered=$true;state=[string]$t.State;"
+        "last_run=if($lr){$lr.ToUniversalTime().ToUnixTimeSeconds()}else{$null}}"
+        "|ConvertTo-Json -Compress")
+    flags = getattr(subprocess, "CREATE_NO_WINDOW", 0)
+    try:
+        proc = subprocess.run(
+            ["powershell.exe", "-NoProfile", "-NonInteractive", "-Command",
+             script], stdout=subprocess.PIPE, stderr=subprocess.DEVNULL,
+            creationflags=flags, timeout=15, text=True)
+        if proc.returncode != 0:
+            raise RuntimeError("scheduler query failed")
+        row = json.loads(proc.stdout)
+        return {"registered": bool(row.get("registered")),
+                "state": str(row.get("state", "")),
+                "last_run": row.get("last_run")}
+    except (OSError, subprocess.SubprocessError, RuntimeError, ValueError,
+            TypeError):
+        return {"registered": False, "state": "", "last_run": None}
+
+
+def _runtime_drift_attributed(before_usage, after_usage, started, ended,
+                              scheduler_before, scheduler_after,
+                              expected_node):
+    """Prove concurrent runtime drift; otherwise fail closed."""
+    if not (scheduler_before.get("registered")
+            and scheduler_after.get("registered")):
+        return False, "production scheduler not registered at both boundaries"
+    last_before = scheduler_before.get("last_run")
+    last_after = scheduler_after.get("last_run")
+    running = (scheduler_before.get("state", "").casefold() == "running"
+               or scheduler_after.get("state", "").casefold() == "running")
+    ran_in_window = (isinstance(last_after, (int, float))
+                     and started - 2 <= last_after <= ended + 2
+                     and last_after != last_before)
+    if not (running or ran_in_window):
+        return False, "runtime moved without an overlapping scheduled task"
+    if not after_usage.startswith(before_usage):
+        return False, "production usage counter was not append-only"
+    delta = after_usage[len(before_usage):]
+    if not delta:
+        return True, "scheduler overlap proved; usage receipt pending"
+    if not delta.endswith(b"\n"):
+        return False, "production usage append is incomplete"
+    try:
+        rows = [json.loads(line.decode("utf-8"))
+                for line in delta.splitlines() if line.strip()]
+    except (UnicodeDecodeError, ValueError, TypeError) as exc:
+        return False, "invalid production usage delta: %s" % type(exc).__name__
+    machine = str(expected_node or "").casefold()
+    if not machine or not rows:
+        return False, "missing machine identity or usage rows"
+    for row in rows:
+        try:
+            ts = calendar.timegm(time.strptime(row.get("ts", ""),
+                                               "%Y-%m-%dT%H:%M:%SZ"))
+        except (TypeError, ValueError, OverflowError):
+            return False, "usage row has invalid timestamp"
+        if not (started - 2 <= ts <= ended + 2):
+            return False, "usage row falls outside suite window"
+        if row.get("actor") != "robot":
+            return False, "usage delta contains a non-robot writer"
+    own_ticks = sum(1 for row in rows
+                    if str(row.get("node", "")).casefold() == machine
+                    and row.get("event") == "deliver"
+                    and row.get("outcome") == "tick")
+    return True, "scheduler overlap proved; rows=%d own_ticks=%d" % (
+        len(rows), own_ticks)
@@
 _RUN_STARTED_UTC = time.time()
+_PROD_NODE = os.environ.get("COMPUTERNAME") or socket.gethostname()
 _PROD_BEFORE = {p: _file_snapshot(p) for p in _PROD_TRACKED}
+_PROD_USAGE_PATH = _PROD_RUNTIME[0]
+_PROD_USAGE_BEFORE = _read_bytes(_PROD_USAGE_PATH)
+_PROD_SCHEDULER_BEFORE = _production_scheduler_observation()
@@
 _PROD_AFTER = {p: _file_snapshot(p) for p in _PROD_TRACKED}
 _PROD_DRIFT = {p: {"before": _PROD_BEFORE[p], "after": _PROD_AFTER[p]}
                for p in _PROD_TRACKED if _PROD_BEFORE[p] != _PROD_AFTER[p]}
-check("GREEN: production source/config/state/counter bytes unchanged",
-      not _PROD_DRIFT, str(_PROD_DRIFT))
+_PROD_IMMUTABLE_DRIFT = {p: _PROD_DRIFT[p] for p in _PROD_IMMUTABLE
+                         if p in _PROD_DRIFT}
+_PROD_RUNTIME_DRIFT = {p: _PROD_DRIFT[p] for p in _PROD_RUNTIME
+                       if p in _PROD_DRIFT}
+_RUNTIME_OK, _RUNTIME_DETAIL = (True, "stable")
+if _PROD_RUNTIME_DRIFT:
+    _RUNTIME_OK, _RUNTIME_DETAIL = _runtime_drift_attributed(
+        _PROD_USAGE_BEFORE, _read_bytes(_PROD_USAGE_PATH),
+        _RUN_STARTED_UTC, time.time(), _PROD_SCHEDULER_BEFORE,
+        _production_scheduler_observation(), _PROD_NODE)
+check("GREEN: immutable production unchanged; runtime drift externally attributed",
+      not _PROD_IMMUTABLE_DRIFT and _RUNTIME_OK,
+      "immutable=%s runtime=%s attribution=%s" %
+      (_PROD_IMMUTABLE_DRIFT, _PROD_RUNTIME_DRIFT, _RUNTIME_DETAIL))

---

**Claude:**

[⏰ вторник, 12:23, 22 сентября 2026]

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/.claude/scripts/_test_tg_doorbell.py\" 2>/dev/null && wc -l \"C:/Users/dev/.claude/scripts/_test_tg_doorbell.py\"", "description": "Locate the doorbell test file"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "limit": 120}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "offset": 120, "limit": 180}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -n \"_PROD_DB\\|_PROD_RUNTIME\\|_PROD_IMMUTABLE\\|_production_scheduler_registered\\|_PROD_USAGE\\|_RUN_STARTED_UTC\\|_PROD_NODE\" _test_tg_doorbell.py", "description": "Grep production-path references in suite"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "offset": 4090, "limit": 80}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -n \"usage\" tg_doorbell.py | head -40", "description": "Find usage-counter write sites in production script"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -n \"USAGE\\|def _usage\\|_usage(\" tg_doorbell.py | head -30", "description": "Find usage writer function and call sites"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && sed -n '305,335p' tg_doorbell.py && echo \"=== callers ===\" && grep -n \"usage_row\\|use_row\\|_note_usage\\|note_usage\" tg_doorbell.py | head -30", "description": "Inspect usage writer and its callers"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -n \"count(\" tg_doorbell.py | head -40", "description": "Find count() call sites"}
