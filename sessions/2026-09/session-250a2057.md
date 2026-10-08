**Антон:**

You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author. The author (Codex) wrote the two-repository change below. Review ONLY the supplied diffs; do not use tools or read other files. Be concrete and skeptical.

Task: local Windows Claude/Codex shared-file write protection. Required properties: two concurrent writers of one absolute file produce one owner and BUSY rc=7 naming the holder; foreign release and delayed old-turn release are harmless; old-schema migration is race-safe and token-aware Stop can release a migrated legacy row; real Codex shell/apply_patch hook wiring is tested; counters are attributable; child-script, relative-path, Windows-only, per-checkout and local-only boundaries are honest.

Check correctness, security bypasses, caller breakage, races, and whether tests really kill their named mutations. Prioritize real MED/HIGH defects; do not block on style.

CRITICAL OUTPUT CONTRACT: the VERY LAST line of your reply must be exactly
  ===VERDICT=== <value>
where <value> is one bare word: APPROVE (no blocking issues) or REQUEST_CHANGES (one or more MED/HIGH issues). No backticks, no bold, no brackets, nothing else on that line. State it exactly once, on that final line only.

Format before the final line:
SUMMARY: <one or two sentences>
FINDINGS:
- file:line | severity | issue | fix
(or `none`)

--- SCRIPTS DIFF START ---diff --git a/_test_codex_shared_workspace_safety.py b/_test_codex_shared_workspace_safety.py
deleted file mode 100644
index 4d7d597e5..000000000
--- a/_test_codex_shared_workspace_safety.py
+++ /dev/null
@@ -1,273 +0,0 @@
-# -*- coding: utf-8 -*-
-"""Integration acceptance for Claude/Codex shared-workspace safety.
-
-Purpose: prove the active Codex registry has one local shelf, both harness configs
-route writes through the same guard, canonical apply_patch is really parsed, and a
-Stop event releases the turn lease. Input: live configs plus an isolated temp DB.
-Output: PASS/FAIL and evidence; never edits a real workspace file.
-Caller: /tt after shared-workspace changes. Rail: local Python + codex debug, 0 LLM.
-updated: 2026-09-11
-"""
-from __future__ import annotations
-
-import json
-import os
-import re
-import shutil
-import subprocess
-import sys
-import tempfile
-import time
-
-HOME = os.path.expanduser("~")
-SCRIPTS = os.path.join(HOME, ".claude", "scripts")
-HOOKS = os.path.join(HOME, ".claude", "hooks")
-GUARD = os.path.join(HOOKS, "workspace_write_guard.py")
-CONSTITUTION = os.path.join(HOOKS, "constitution_guard.py")
-ORPHAN = os.path.join(HOOKS, "orphan_check_hook.py")
-TURNSTATE = os.path.join(HOOKS, "turnstate_hook.py")
-CODEX_HOOKS = os.path.join(HOME, ".codex", "hooks.json")
-CLAUDE_SETTINGS = os.path.join(HOME, ".claude", "settings.json")
-R1 = os.path.join(HOME, ".agents", "skills")
-RESULTS = []
-
-
-def check(name, ok, detail=""):
-    RESULTS.append((name, bool(ok), detail))
-    print("  %s %s%s" % ("OK  " if ok else "FAIL", name,
-                          (" -- " + str(detail)) if detail else ""))
-
-
-def _json(path):
-    with open(path, encoding="utf-8") as fh:
-        return json.load(fh)
-
-
-def _commands(entries):
-    out = []
-    for group in entries or []:
-        for hook in group.get("hooks") or []:
-            out.append((group.get("matcher") or "", hook.get("command") or ""))
-    return out
-
-
-def _run_guard(payload, phase="pre", env=None):
-    return subprocess.run([sys.executable, GUARD, "--phase", phase],
-                          input=json.dumps(payload), capture_output=True, text=True,
-                          encoding="utf-8", errors="replace", env=env, timeout=30)
-
-
-def _run_constitution(payload, env=None):
-    return subprocess.run([sys.executable, CONSTITUTION], input=json.dumps(payload),
-                          capture_output=True, text=True, encoding="utf-8",
-                          errors="replace", env=env, timeout=30)
-
-
-def _wait_until(ts):
-    while True:
-        left = float(ts) - time.time()
-        if left <= 0:
-            return
-        time.sleep(min(0.02, left / 2))
-
-
-def _guard_child(root, start, session, target):
-    env = dict(os.environ)
-    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "race.sqlite3")
-    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "race-counter.jsonl")
-    _wait_until(start)
-    payload = {"session_id": session, "cwd": root, "tool_name": "Write",
-               "tool_input": {"file_path": target}}
-    run = _run_guard(payload, env=env)
-    print("WIN" if run.returncode == 0 else "LOSE")
-    return 0
-
-
-def _guard_race(root, target, racers=8):
-    start = time.time() + 1.2
-    procs = [subprocess.Popen(
-        [sys.executable, os.path.abspath(__file__), "--guard-child", root,
-         "%.6f" % start, "hook-session-%d" % i, target],
-        stdout=subprocess.PIPE, stderr=subprocess.PIPE)
-        for i in range(racers)]
-    wins, errors = 0, []
-    for proc in procs:
-        out, err = proc.communicate(timeout=60)
-        answer = out.decode("utf-8", "replace").strip()
-        if answer.endswith("WIN"):
-            wins += 1
-        elif not answer.endswith("LOSE"):
-            errors.append("rc=%s out=%r err=%r" %
-                          (proc.returncode, answer, err.decode("utf-8", "replace")[:120]))
-    return wins, errors
-
-
-def main():
-    root = tempfile.mkdtemp(prefix="codex-shared-safety-test-")
-    env = dict(os.environ)
-    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "leases.sqlite3")
-    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
-    target = os.path.join(root, "shared file.md")
-    try:
-        r1_skills = []
-        if os.path.isdir(R1):
-            r1_skills = [n for n in os.listdir(R1)
-                         if os.path.isfile(os.path.join(R1, n, "SKILL.md"))]
-        check("r1/.agents не содержит активных копий SKILL.md", not r1_skills,
-              "active=%d first=%s" % (len(r1_skills), r1_skills[:5]))
-
-        check("общий workspace guard существует", os.path.isfile(GUARD), GUARD)
-        codex = _json(CODEX_HOOKS)
-        claude = _json(CLAUDE_SETTINGS)
-        cpre = _commands(codex.get("hooks", {}).get("PreToolUse"))
-        clpre = _commands(claude.get("hooks", {}).get("PreToolUse"))
-        check("Codex PreToolUse явно матчится на canonical apply_patch",
-              any("constitution_guard" in cmd and "apply_patch" in matcher
-                  for matcher, cmd in cpre), cpre[:3])
-        check("Codex shell тоже идёт через guard",
-              any("constitution_guard" in cmd and
-                  ("Bash" in matcher or "PowerShell" in matcher) for matcher, cmd in cpre), cpre[:3])
-        check("Claude file tools идут через тот же guard",
-              any("constitution_guard" in cmd and "Write" in matcher for matcher, cmd in clpre))
-        check("Claude shell идёт через тот же guard",
-              any("constitution_guard" in cmd and
-                  ("Bash" in matcher or "PowerShell" in matcher) for matcher, cmd in clpre))
-        cpost = _commands(codex.get("hooks", {}).get("PostToolUse"))
-        check("Codex PostToolUse явно матчится на canonical apply_patch",
-              any("orphan_check_hook" in cmd and "apply_patch" in matcher
-                  for matcher, cmd in cpost), cpost[:3])
-
-        if os.path.isfile(GUARD):
-            race_root = os.path.join(root, "parallel-hook")
-            os.makedirs(race_root, exist_ok=True)
-            race_target = os.path.join(race_root, "one-file.md")
-            wins, errors = _guard_race(race_root, race_target)
-            check("параллельный hook: 8 turn -> ровно один проходит", wins == 1,
-                  "wins=%d errors=%s" % (wins, errors))
-            patch = "*** Begin Patch\n*** Update File: %s\n@@\n-old\n+new\n*** End Patch" % target
-            p1 = {"session_id": "codex-A", "cwd": root, "tool_name": "apply_patch",
-                  "tool_input": {"command": patch}}
-            p2 = {"session_id": "claude-B", "cwd": root, "tool_name": "Edit",
-                  "tool_input": {"file_path": target}}
-            a = _run_guard(p1, env=env)
-            b = _run_guard(p2, env=env)
-            check("canonical apply_patch реально получает lease", a.returncode == 0,
-                  "rc=%s stderr=%s" % (a.returncode, a.stderr[:200]))
-            check("второй агент блокируется на том же файле", b.returncode == 2 and
-                  "codex-A" in b.stderr, "rc=%s stderr=%s" % (b.returncode, b.stderr[:300]))
-            codex_b = dict(p2)
-            codex_b.update({"tool_name": "apply_patch", "turn_id": "turn-B",
-                            "tool_use_id": "call-B",
-                            "tool_input": {"command": patch}})
-            structured = _run_constitution(codex_b, env)
-            try:
-                structured_json = json.loads(structured.stdout)
-                permission = structured_json["hookSpecificOutput"]["permissionDecision"]
-            except Exception:
-                permission = ""
-            check("Codex 0.147 получает structured deny, не hook Failed",
-                  structured.returncode == 0 and permission == "deny" and
-                  "codex-A" in structured.stdout,
-                  "rc=%s out=%s err=%s" % (structured.returncode,
-                  structured.stdout[:300], structured.stderr[:120]))
-            stop_payload = {"session_id": "codex-A", "cwd": root,
-                            "hook_event_name": "Stop"}
-            stop = subprocess.run([sys.executable, TURNSTATE], input=json.dumps(stop_payload),
-                                  capture_output=True, text=True, encoding="utf-8",
-                                  errors="replace", env=env, timeout=30)
-            after = _run_guard(p2, env=env)
-            check("реальный turnstate Stop освобождает turn-lease",
-                  stop.returncode == 0 and after.returncode == 0,
-                  "stop=%s after=%s" % (stop.returncode, after.returncode))
-            _run_guard({"session_id": "claude-B", "cwd": root}, "stop", env)
-            post_payload = dict(p1)
-            post_payload.update({"turn_id": "turn-post", "tool_use_id": "call-post",
-                                 "hook_event_name": "PostToolUse", "tool_response": {"ok": True}})
-            post = subprocess.run([sys.executable, ORPHAN], input=json.dumps(post_payload),
-                                  capture_output=True, text=True, encoding="utf-8",
-                                  errors="replace", env=env, timeout=30)
-            check("Codex PostToolUse no-op = пустой stdout, не invalid approve",
-                  post.returncode == 0 and not post.stdout.strip(),
-                  "rc=%s out=%r err=%r" % (post.returncode, post.stdout, post.stderr[:120]))
-            malformed = subprocess.run([sys.executable, GUARD, "--phase", "pre"],
-                                       input="not-json", capture_output=True, text=True,
-                                       env=env, timeout=30)
-            check("битый write-payload блокируется fail-closed", malformed.returncode == 2)
-            readonly = _run_guard({"session_id": "reader", "cwd": root,
-                                   "tool_name": "Bash",
-                                   "tool_input": {"command": "git status --short"}}, env=env)
-            check("read-only shell не берёт лишний замок", readonly.returncode == 0)
-            if HOOKS not in sys.path:
-                sys.path.insert(0, HOOKS)
-            import workspace_write_guard as guard_module
-            check("read-only whitelist не пропускает PowerShell script-block",
-                  not guard_module.shell_is_read_only(
-                      "Get-Content x | Where-Object { Remove-Item x; $true }"))
-            check("read-only whitelist не пропускает git --output",
-                  not guard_module.shell_is_read_only("git diff --output=stolen.patch"))
-            # 14.09.2026, класс lease-storm. ЗДЕСЬ БЫЛ ОБРАТНЫЙ ИНВАРИАНТ: `python mystery.py`
-            # лизовал cwd ЦЕЛИКОМ, и тест требовал, чтобы сосед после этого не мог править
-            # СВОЙ файл в той же папке. Это и есть шторм, записанный как «защита»: замер 14.09
-            # -- 198 блокировок, 69% из них запрос ПАПКИ, 36 пострадавших сессий, среди жертв
-            # чтение файла. Защита была ещё и мнимой: путь цели в такой команде не назван, так
-            # что от РЕАЛЬНОЙ гонки за файл папочная лиза не спасала -- она лишь запирала
-            # непричастных. Новый инвариант: неизвестная команда без признака записи не лизует
-            # ничего, а гонку за конкретный файл по-прежнему ловит файловый инструмент.
-            unknown_writer = _run_guard({"session_id": "script-A", "cwd": root,
-                                         "tool_name": "Bash",
-                                         "tool_input": {"command": "python mystery.py"}}, env=env)
-            neighbour = _run_guard({"session_id": "script-B", "cwd": root,
-                                    "tool_name": "Edit",
-                                    "tool_input": {"file_path": target}}, env=env)
-            check("неизвестный shell-процесс НЕ запирает соседей по папке",
-                  unknown_writer.returncode == 0 and neighbour.returncode == 0,
-                  "writer=%s neighbour=%s" % (unknown_writer.returncode, neighbour.returncode))
-            same_file = _run_guard({"session_id": "script-C", "cwd": root,
-                                    "tool_name": "Edit",
-                                    "tool_input": {"file_path": target}}, env=env)
-            check("гонка за ОДИН файл по-прежнему отбивается",
-                  same_file.returncode == 2, "same_file=%s" % same_file.returncode)
-            _run_guard({"session_id": "script-B", "cwd": root}, "stop", env)
-            _run_guard({"session_id": "script-A", "cwd": root}, "stop", env)
-            env_sid = dict(env)
-            env_sid["CODEX_THREAD_ID"] = "env-only-session"
-            env_target = os.path.join(root, "env-session.md")
-            env_acquire = _run_guard({"cwd": root, "tool_name": "Edit",
-                                      "tool_input": {"file_path": env_target}}, env=env_sid)
-            env_stop = subprocess.run([sys.executable, TURNSTATE],
-                                      input=json.dumps({"cwd": root, "hook_event_name": "Stop"}),
-                                      capture_output=True, text=True, encoding="utf-8",
-                                      errors="replace", env=env_sid, timeout=30)
-            env_after = _run_guard({"session_id": "after-env", "cwd": root,
-                                    "tool_name": "Edit",
-                                    "tool_input": {"file_path": env_target}}, env=env)
-            check("Stop использует тот же env fallback session-id",
-                  env_acquire.returncode == 0 and env_stop.returncode == 0 and
-                  env_after.returncode == 0,
-                  "acquire=%s stop=%s after=%s" % (env_acquire.returncode,
-                  env_stop.returncode, env_after.returncode))
-
-            help_run = subprocess.run([sys.executable, GUARD, "--help"],
-                                      capture_output=True, text=True, timeout=30)
-            bad_flag = subprocess.run([sys.executable, GUARD, "--wat"],
-                                      capture_output=True, text=True, timeout=30)
-            check("guard --help", help_run.returncode == 0 and "usage:" in help_run.stdout)
-            check("guard отвергает неизвестный флаг", bad_flag.returncode == 2)
-    finally:
-        shutil.rmtree(root, ignore_errors=True)
-
-    bad = [name for name, ok, _ in RESULTS if not ok]
-    print("\nВЕРДИКТ: %s" % ("PASS" if not bad else "FAIL: " + "; ".join(bad)))
-    return 0 if not bad else 1
-
-
-if __name__ == "__main__":
-    try:
-        sys.stdout.reconfigure(encoding="utf-8")
-        sys.stderr.reconfigure(encoding="utf-8")
-    except Exception:
-        pass
-    if len(sys.argv) > 1 and sys.argv[1] == "--guard-child":
-        sys.exit(_guard_child(sys.argv[2], sys.argv[3], sys.argv[4], sys.argv[5]))
-    sys.path.insert(0, SCRIPTS)
-    sys.exit(main())
diff --git a/_test_workspace_write_guard.py b/_test_workspace_write_guard.py
new file mode 100644
index 000000000..e2c264e78
--- /dev/null
+++ b/_test_workspace_write_guard.py
@@ -0,0 +1,830 @@
+# -*- coding: utf-8 -*-
+"""Integration acceptance for Claude/Codex shared-workspace safety.
+
+Purpose: prove both harness configs route canonical Bash/exec_command/shell and
+apply_patch through one guard, Codex turn_id becomes a fencing epoch, and a delayed
+old Stop cannot release the next turn. Input: live configs plus an isolated temp DB.
+Output: PASS/FAIL and evidence; never edits a real workspace file. A separate fresh
+Codex-session canary is still required to prove the harness actually invoked hooks.
+Caller: nightly regress grid and /tt after shared-workspace changes. Rail: local
+Python stdlib, 0 LLM/network.
+
+KILL-LIST (source/config mutation -> case that must fail):
+- remove Bash/PowerShell/exec_command/shell from Codex PreToolUse matcher ->
+  ``mutation: удаление shell matcher обязано стать красным``;
+- disable/remove the persisted Codex PreToolUse trust state ->
+  ``Codex PreToolUse trust state включён``;
+- replace the configured hook by a missing command, dropped stdin, or echo ->
+  ``live hooks.json command исполняется и три command mutants красные``;
+- release by session while ignoring turn_id ->
+  ``поздний Stop старого turn_id не снимает новую эпоху``;
+- keep ``agent/<id>`` distinct from ``<id>`` ->
+  ``Stop alias agent/session снимает lease plain session``;
+- remove/misroute Codex Stop -> turnstate_hook registration ->
+  ``Codex Stop зарегистрирован на fenced release``;
+- return allow instead of Codex structured deny ->
+  ``Codex 0.147 получает structured deny, не hook Failed``;
+- let a read-only-looking PowerShell script block mutate -> the two read-only
+  whitelist checks fail. The fresh-session canary covers the runtime boundary that
+  this direct-hook suite cannot prove.
+- scan quoted ``<input>`` or discard ``2>$null`` as output redirection ->
+  ``literal rg repro не лизует входные absolute roots``.
+- hide a quoted child-shell body from mutation detection ->
+  ``quoted PowerShell/cmd writers блокируются holder``.
+- ignore a quoted executable path (including PowerShell call-operator) ->
+  ``quoted executable path child writers блокируются holder``.
+- treat PowerShell backslash as a quote escape, or stop at an option value before
+  ``-Command`` -> ``PowerShell option/backslash/call variants блокируются holder``.
+- lease the quoted shell executable itself ->
+  ``один pwsh executable не сериализует разные output files``.
+- ignore `bash -c` text inside an rg pattern, or miss bash/sh combined `c` flags ->
+  ``quoted bash -lc/sh -ec writers видны, rg pattern остаётся reader``.
+updated: 2026-09-21
+"""
+from __future__ import annotations
+
+import json
+import os
+import re
+import shutil
+import sqlite3
+import subprocess
+import sys
+import tempfile
+import time
+
+HOME = os.path.expanduser("~")
+SCRIPTS = os.environ.get("WORKSPACE_LEASE_TEST_SCRIPTS") or os.path.join(
+    HOME, ".claude", "scripts")
+HOOKS = os.environ.get("WORKSPACE_LEASE_TEST_HOOKS") or os.path.join(
+    HOME, ".claude", "hooks")
+GUARD = os.path.join(HOOKS, "workspace_write_guard.py")
+CONSTITUTION = os.path.join(HOOKS, "constitution_guard.py")
+ORPHAN = os.path.join(HOOKS, "orphan_check_hook.py")
+TURNSTATE = os.path.join(HOOKS, "turnstate_hook.py")
+CODEX_HOOKS = os.path.join(HOME, ".codex", "hooks.json")
+CODEX_CONFIG = os.path.join(HOME, ".codex", "config.toml")
+CLAUDE_SETTINGS = os.path.join(HOME, ".claude", "settings.json")
+RESULTS = []
+
+
+def check(name, ok, detail=""):
+    RESULTS.append((name, bool(ok), detail))
+    print("  %s %s%s" % ("OK  " if ok else "FAIL", name,
+                          (" -- " + str(detail)) if detail else ""))
+
+
+def _json(path):
+    with open(path, encoding="utf-8") as fh:
+        return json.load(fh)
+
+
+def _commands(entries):
+    out = []
+    for group in entries or []:
+        for hook in group.get("hooks") or []:
+            out.append((group.get("matcher") or "", hook.get("command") or ""))
+    return out
+
+
+def _codex_pretool_contract(commands):
+    required = {"apply_patch", "Bash", "PowerShell", "exec_command", "shell"}
+    for matcher, command in commands:
+        tokens = {part.strip() for part in matcher.split("|") if part.strip()}
+        if "constitution_guard" in command and required.issubset(tokens):
+            return True
+    return False
+
+
+def _codex_pretool_trust_state(config_text):
+    """Read the exact persisted state; runtime canary still proves hash freshness."""
+    marker = "[hooks.state.'%s:pre_tool_use:0:0']" % CODEX_HOOKS
+    start = config_text.find(marker)
+    if start < 0:
+        return False
+    tail = config_text[start + len(marker):]
+    end = tail.find("\n[")
+    section = tail if end < 0 else tail[:end]
+    return (bool(re.search(r'(?m)^trusted_hash\s*=\s*"sha256:[0-9a-f]{64}"\s*$', section)) and
+            bool(re.search(r"(?m)^enabled\s*=\s*true\s*$", section)))
+
+
+def _file_size(path):
+    return os.path.getsize(path) if os.path.isfile(path) else 0
+
+
+def _new_matching_lines(path, offset, markers):
+    """Allow concurrent legitimate writers; return only rows attributable here."""
+    if not os.path.isfile(path):
+        return []
+    if os.path.getsize(path) < offset:
+        return ["production audit log shrank/rotated during the test"]
+    with open(path, "rb") as fh:
+        fh.seek(offset)
+        suffix = fh.read().decode("utf-8", "replace")
+    lowered = [marker.lower() for marker in markers]
+    return [line for line in suffix.splitlines()
+            if any(marker in line.lower() for marker in lowered)]
+
+
+def _lease_owner(db, target):
+    resource = os.path.normcase(os.path.realpath(os.path.abspath(target)))
+    con = sqlite3.connect(db)
+    try:
+        row = con.execute(
+            "SELECT session,epoch FROM leases WHERE resource=?", (resource,)).fetchone()
+        return {"session": row[0], "epoch": row[1]} if row else None
+    finally:
+        con.close()
+
+
+def _run_guard(payload, phase="pre", env=None):
+    return subprocess.run([sys.executable, GUARD, "--phase", phase],
+                          input=json.dumps(payload), capture_output=True, text=True,
+                          encoding="utf-8", errors="replace", env=env, timeout=30)
+
+
+def _run_constitution(payload, env=None):
+    return subprocess.run([sys.executable, CONSTITUTION], input=json.dumps(payload),
+                          capture_output=True, text=True, encoding="utf-8",
+                          errors="replace", env=env, timeout=30)
+
+
+def _run_hook_command(command, payload, env=None):
+    """Execute the exact hooks.json command, including its real .cmd shim."""
+    if os.name == "nt":
+        argv = [os.environ.get("COMSPEC") or "cmd.exe", "/d", "/s", "/c", command]
+    else:
+        argv = ["sh", "-c", command]
+    return subprocess.run(argv, input=json.dumps(payload), capture_output=True,
+                          text=True, encoding="utf-8", errors="replace",
+                          env=env, timeout=30)
+
+
+def _is_structured_deny(run, holder=""):
+    try:
+        parsed = json.loads(run.stdout)
+        output = parsed["hookSpecificOutput"]
+        reason = str(output.get("permissionDecisionReason") or "")
+        return (run.returncode == 0 and output.get("permissionDecision") == "deny" and
+                (not holder or holder in reason))
+    except Exception:
+        return False
+
+
+def _wait_until(ts):
+    while True:
+        left = float(ts) - time.time()
+        if left <= 0:
+            return
+        time.sleep(min(0.02, left / 2))
+
+
+def _guard_child(root, start, session, target):
+    env = dict(os.environ)
+    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "race.sqlite3")
+    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "race-counter.jsonl")
+    env["WORKSPACE_WRITE_LEASE_MODULE_DIR"] = SCRIPTS
+    _wait_until(start)
+    payload = {"session_id": session, "cwd": root, "tool_name": "Write",
+               "tool_input": {"file_path": target}}
+    run = _run_guard(payload, env=env)
+    if run.returncode == 0:
+        print("WIN %s" % session)
+        return 0
+    if (run.returncode == 2 and "BUSY:" in run.stderr and
+            "held by hook-session-" in run.stderr):
+        match = re.search(r"held by ([^.\r\n]+)", run.stderr)
+        if match:
+            print("LOSE BUSY held by %s" % match.group(1).strip())
+            return 0
+        print("ERROR BUSY without parseable holder: %r" % run.stderr[:500])
+        return 3
+    print("ERROR rc=%s out=%r err=%r" %
+          (run.returncode, run.stdout[:160], run.stderr[:500]))
+    return 3
+
+
+def _guard_race(root, target, racers=8):
+    start = time.time() + 1.2
+    procs = [subprocess.Popen(
+        [sys.executable, os.path.abspath(__file__), "--guard-child", root,
+         "%.6f" % start, "hook-session-%d" % i, target],
+        stdout=subprocess.PIPE, stderr=subprocess.PIPE)
+        for i in range(racers)]
+    winners, loser_holders, errors = [], [], []
+    for proc in procs:
+        out, err = proc.communicate(timeout=60)
+        answer = out.decode("utf-8", "replace").strip()
+        if answer.startswith("WIN "):
+            winners.append(answer[4:].strip())
+        elif answer.startswith("LOSE BUSY held by "):
+            loser_holders.append(answer[len("LOSE BUSY held by "):].strip())
+        else:
+            errors.append("rc=%s out=%r err=%r" %
+                          (proc.returncode, answer, err.decode("utf-8", "replace")[:120]))
+    if len(winners) == 1:
+        wrong = [holder for holder in loser_holders if holder != winners[0]]
+        if len(loser_holders) != racers - 1 or wrong:
+            errors.append("winner=%r loser_holders=%r" % (winners, loser_holders))
+    return len(winners), errors
+
+
+def main():
+    production_audit = os.path.join(HOME, ".claude", "hooks", "_constitution_guard.log")
+    production_audit_before = _file_size(production_audit)
+    production_usage = os.path.join(
+        os.environ.get("LOCALAPPDATA") or os.path.join(HOME, ".local"),
+        "AntonAgents", "workspace-write-leases", "usage.jsonl")
+    production_usage_before = _file_size(production_usage)
+    root = tempfile.mkdtemp(prefix="codex-shared-safety-test-")
+    env = dict(os.environ)
+    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "leases.sqlite3")
+    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
+    env["WORKSPACE_WRITE_LEASE_MODULE_DIR"] = SCRIPTS
+    env["USERPROFILE"] = root
+    env["HOME"] = root
+    isolated_audit_dir = os.path.join(root, ".claude", "hooks")
+    os.makedirs(isolated_audit_dir, exist_ok=True)
+    isolated_audit = os.path.join(isolated_audit_dir, "_constitution_guard.log")
+    env["CONSTITUTION_GUARD_LOG"] = isolated_audit
+    target = os.path.join(root, "shared file.md")
+    try:
+        check("общий workspace guard существует", os.path.isfile(GUARD), GUARD)
+        codex = _json(CODEX_HOOKS)
+        claude = _json(CLAUDE_SETTINGS)
+        with open(CODEX_CONFIG, encoding="utf-8") as fh:
+            codex_config = fh.read()
+        cpre = _commands(codex.get("hooks", {}).get("PreToolUse"))
+        clpre = _commands(claude.get("hooks", {}).get("PreToolUse"))
+        configured_pretool = next((command for matcher, command in cpre
+                                   if "constitution_guard" in command and
+                                   "apply_patch" in matcher), "")
+        check("Codex PreToolUse покрывает apply_patch и shell aliases",
+              _codex_pretool_contract(cpre), cpre[:3])
+        matcher_mutation_survivors = []
+        for removed in ("Bash", "PowerShell", "exec_command", "shell"):
+            mutated_cpre = []
+            for matcher, command in cpre:
+                kept = [part for part in matcher.split("|") if part != removed]
+                mutated_cpre.append(("|".join(kept), command))
+            if _codex_pretool_contract(mutated_cpre):
+                matcher_mutation_survivors.append(removed)
+        check("mutation: каждый shell matcher по одному обязан стать красным",
+              not matcher_mutation_survivors,
+              "survivors=%r" % matcher_mutation_survivors)
+        trust_state = _codex_pretool_trust_state(codex_config)
+        check("persisted PreToolUse state имеет enabled+hash; freshness проверяет canary",
+              trust_state, CODEX_CONFIG)
+        mutated_trust = codex_config.replace(
+            "[hooks.state.'%s:pre_tool_use:0:0']" % CODEX_HOOKS,
+            "[hooks.state.'%s:pre_tool_use:mutated:0']" % CODEX_HOOKS, 1)
+        check("mutation: удаление PreToolUse trust state обязано стать красным",
+              trust_state and not _codex_pretool_trust_state(mutated_trust))
+        check("Claude file tools идут через тот же guard",
+              any("constitution_guard" in cmd and "Write" in matcher for matcher, cmd in clpre))
+        check("Claude shell идёт через тот же guard",
+              any("constitution_guard" in cmd and
+                  ("Bash" in matcher or "PowerShell" in matcher) for matcher, cmd in clpre))
+        cpost = _commands(codex.get("hooks", {}).get("PostToolUse"))
+        check("Codex PostToolUse явно матчится на canonical apply_patch",
+              any("orphan_check_hook" in cmd and "apply_patch" in matcher
+                   for matcher, cmd in cpost), cpost[:3])
+        cstop = _commands(codex.get("hooks", {}).get("Stop"))
+        stop_registered = any("turnstate_hook" in command for _, command in cstop)
+        check("Codex Stop зарегистрирован на fenced release",
+              stop_registered, cstop[:3])
+        mutated_cstop = [(matcher, command) for matcher, command in cstop
+                         if "turnstate_hook" not in command]
+        check("mutation: удаление Codex Stop registration обязано стать красным",
+              stop_registered and not any(
+                  "turnstate_hook" in command for _, command in mutated_cstop),
+              mutated_cstop[:3])
+
+        if os.path.isfile(GUARD):
+            race_root = os.path.join(root, "parallel-hook")
+            os.makedirs(race_root, exist_ok=True)
+            race_target = os.path.join(race_root, "one-file.md")
+            wins, errors = _guard_race(race_root, race_target)
+            check("параллельный hook: 8 turn -> один win, 7 доказанных BUSY",
+                  wins == 1 and not errors,
+                   "wins=%d errors=%s" % (wins, errors))
+            patch = "*** Begin Patch\n*** Update File: %s\n@@\n-old\n+new\n*** End Patch" % target
+            p1 = {"session_id": "codex-A", "turn_id": "turn-A",
+                  "tool_use_id": "call-A", "cwd": root, "tool_name": "apply_patch",
+                  "tool_input": {"command": patch}}
+            p2 = {"session_id": "claude-B", "cwd": root, "tool_name": "Edit",
+                  "tool_input": {"file_path": target}}
+            a = _run_guard(p1, env=env)
+            b = _run_guard(p2, env=env)
+            check("canonical apply_patch реально получает lease", a.returncode == 0,
+                  "rc=%s stderr=%s" % (a.returncode, a.stderr[:200]))
+            check("второй агент блокируется на том же файле", b.returncode == 2 and
+                  "codex-A" in b.stderr, "rc=%s stderr=%s" % (b.returncode, b.stderr[:300]))
+            codex_b = dict(p2)
+            codex_b.update({"tool_name": "apply_patch", "turn_id": "turn-B",
+                            "tool_use_id": "call-B",
+                            "tool_input": {"command": patch}})
+            structured = _run_constitution(codex_b, env)
+            try:
+                structured_json = json.loads(structured.stdout)
+                permission = structured_json["hookSpecificOutput"]["permissionDecision"]
+            except Exception:
+                permission = ""
+            check("Codex 0.147 получает structured deny, не hook Failed",
+                  structured.returncode == 0 and permission == "deny" and
+                  "codex-A" in structured.stdout,
+                  "rc=%s out=%s err=%s" % (structured.returncode,
+                  structured.stdout[:300], structured.stderr[:120]))
+            live_hooks = os.path.normcase(os.path.realpath(
+                os.path.join(HOME, ".claude", "hooks")))
+            if os.path.normcase(os.path.realpath(HOOKS)) == live_hooks:
+                exact_env = dict(env)
+                exact_env["USERPROFILE"] = HOME
+                exact_env["HOME"] = HOME
+                exact = _run_hook_command(configured_pretool, codex_b, exact_env)
+                missing = _run_hook_command(
+                    configured_pretool + ".missing", codex_b, exact_env)
+                dropped_stdin = _run_hook_command(
+                    configured_pretool +
+                    (" < NUL" if os.name == "nt" else " < /dev/null"),
+                    codex_b, exact_env)
+                echoed = _run_hook_command(
+                    "echo constitution_guard", codex_b, exact_env)
+                check("live hooks.json command исполняется и три command mutants красные",
+                      _is_structured_deny(exact, "codex-A") and
+                      not _is_structured_deny(missing, "codex-A") and
+                      not _is_structured_deny(dropped_stdin, "codex-A") and
+                      not _is_structured_deny(echoed, "codex-A"),
+                      "exact=%s/%r missing=%s/%r no-stdin=%s/%r echo=%s/%r" %
+                      (exact.returncode, exact.stdout[:120],
+                       missing.returncode, missing.stdout[:80],
+                       dropped_stdin.returncode, dropped_stdin.stdout[:80],
+                       echoed.returncode, echoed.stdout[:80]))
+            else:
+                print("  INFO live hooks.json command deferred until mandatory live run")
+            check("constitution audit пишет только в тестовый профиль",
+                  os.path.isfile(isolated_audit) and
+                  "codex-A" in open(isolated_audit, encoding="utf-8").read(),
+                  isolated_audit)
+            stop_payload = {"session_id": "codex-A", "turn_id": "turn-A", "cwd": root,
+                            "hook_event_name": "Stop"}
+            stop = subprocess.run([sys.executable, TURNSTATE], input=json.dumps(stop_payload),
+                                  capture_output=True, text=True, encoding="utf-8",
+                                  errors="replace", env=env, timeout=30)
+            after = _run_guard(p2, env=env)
+            check("реальный turnstate Stop освобождает turn-lease",
+                  stop.returncode == 0 and after.returncode == 0,
+                  "stop=%s after=%s" % (stop.returncode, after.returncode))
+            _run_guard({"session_id": "claude-B", "cwd": root}, "stop", env)
+
+            alias_target = os.path.join(root, "session-alias.md")
+            alias_patch = ("*** Begin Patch\n*** Update File: %s\n@@\n-old\n+new\n"
+                           "*** End Patch" % alias_target)
+            alias_acquire = _run_guard({
+                "session_id": "codex-alias", "turn_id": "turn-alias",
+                "tool_use_id": "call-alias", "cwd": root, "tool_name": "apply_patch",
+                "tool_input": {"command": alias_patch}}, env=env)
+            alias_owner_before = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], alias_target)
+            alias_stop = subprocess.run(
+                [sys.executable, TURNSTATE],
+                input=json.dumps({"session_id": "agent/codex-alias",
+                                  "turn_id": "turn-alias", "cwd": root,
+                                  "hook_event_name": "Stop"}),
+                capture_output=True, text=True, encoding="utf-8", errors="replace",
+                env=env, timeout=30)
+            alias_owner_after = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], alias_target)
+            alias_challenger = _run_guard({
+                "session_id": "alias-challenger", "cwd": root, "tool_name": "Edit",
+                "tool_input": {"file_path": alias_target}}, env=env)
+            check("Stop alias agent/session снимает lease plain session",
+                  alias_acquire.returncode == 0 and not alias_acquire.stdout.strip() and
+                  alias_owner_before and
+                  alias_owner_before.get("session") == "codex-alias" and
+                  alias_stop.returncode == 0 and alias_owner_after is None and
+                  alias_challenger.returncode == 0,
+                  "acquire=%s/%r before=%r stop=%s after=%r challenger=%s" %
+                  (alias_acquire.returncode, alias_acquire.stdout[:100],
+                   alias_owner_before, alias_stop.returncode, alias_owner_after,
+                   alias_challenger.returncode))
+            _run_guard({"session_id": "alias-challenger", "cwd": root}, "stop", env)
+
+            epoch_target = os.path.join(root, "epoch-fence.md")
+            epoch_patch = "*** Begin Patch\n*** Update File: %s\n@@\n-old\n+new\n*** End Patch" % epoch_target
+            old_turn = {"session_id": "codex-same", "turn_id": "turn-old",
+                        "tool_use_id": "call-old", "cwd": root,
+                        "tool_name": "apply_patch",
+                        "tool_input": {"command": epoch_patch}}
+            new_turn = dict(old_turn)
+            new_turn.update({"turn_id": "turn-new", "tool_use_id": "call-new"})
+            first_old = _run_guard(old_turn, env=env)
+            old_stop_payload = {"session_id": "codex-same", "turn_id": "turn-old",
+                                "cwd": root, "hook_event_name": "Stop"}
+            first_old_stop = subprocess.run(
+                [sys.executable, TURNSTATE], input=json.dumps(old_stop_payload),
+                capture_output=True, text=True, encoding="utf-8", errors="replace",
+                env=env, timeout=30)
+            acquired_new = _run_guard(new_turn, env=env)
+            owner_after_new = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], epoch_target)
+            delayed_old_stop = subprocess.run(
+                [sys.executable, TURNSTATE], input=json.dumps(old_stop_payload),
+                capture_output=True, text=True, encoding="utf-8", errors="replace",
+                env=env, timeout=30)
+            owner_after_late_stop = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], epoch_target)
+            challenger = _run_guard(
+                {"session_id": "claude-challenger", "cwd": root,
+                 "tool_name": "Edit", "tool_input": {"file_path": epoch_target}},
+                env=env)
+            check("поздний Stop старого turn_id не снимает новую эпоху",
+                  first_old.returncode == 0 and first_old_stop.returncode == 0 and
+                  acquired_new.returncode == 0 and not acquired_new.stdout.strip() and
+                  owner_after_new and owner_after_new.get("epoch") == "turn-new" and
+                  delayed_old_stop.returncode == 0 and owner_after_late_stop and
+                  owner_after_late_stop.get("epoch") == "turn-new" and
+                  challenger.returncode == 2 and "codex-same" in challenger.stderr,
+                  "old=%s stop=%s new=%s/%r owner-new=%r late=%s owner-late=%r "
+                  "challenger=%s/%s" %
+                  (first_old.returncode, first_old_stop.returncode,
+                   acquired_new.returncode, acquired_new.stdout[:120], owner_after_new,
+                   delayed_old_stop.returncode, owner_after_late_stop,
+                   challenger.returncode, challenger.stderr[:160]))
+            _run_guard({"session_id": "codex-same", "turn_id": "turn-new",
+                        "cwd": root}, "stop", env)
+            post_payload = dict(p1)
+            post_payload.update({"turn_id": "turn-post", "tool_use_id": "call-post",
+                                 "hook_event_name": "PostToolUse", "tool_response": {"ok": True}})
+            post = subprocess.run([sys.executable, ORPHAN], input=json.dumps(post_payload),
+                                  capture_output=True, text=True, encoding="utf-8",
+                                  errors="replace", env=env, timeout=30)
+            check("Codex PostToolUse no-op = пустой stdout, не invalid approve",
+                  post.returncode == 0 and not post.stdout.strip(),
+                  "rc=%s out=%r err=%r" % (post.returncode, post.stdout, post.stderr[:120]))
+            malformed = subprocess.run([sys.executable, GUARD, "--phase", "pre"],
+                                       input="not-json", capture_output=True, text=True,
+                                       env=env, timeout=30)
+            check("битый write-payload блокируется fail-closed", malformed.returncode == 2)
+            readonly = _run_guard({"session_id": "reader", "cwd": root,
+                                   "tool_name": "Bash",
+                                   "tool_input": {"command": "git status --short"}}, env=env)
+            check("read-only shell не берёт лишний замок", readonly.returncode == 0)
+            read_target = os.path.join(root, "read-only", "absolute.txt")
+            read_parent = os.path.dirname(read_target)
+            absolute_reader_a = _run_guard({
+                "session_id": "reader-A", "cwd": root, "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'Get-Content -LiteralPath "%s"' % read_target}}, env=env)
+            absolute_reader_b = _run_guard({
+                "session_id": "reader-B", "cwd": root, "tool_name": "exec_command",
+                "tool_input": {"command":
+                    'Get-FileHash -LiteralPath "%s" -Algorithm SHA256' % read_target}},
+                env=env)
+            rg_with_null = _run_guard({
+                "session_id": "reader-C", "cwd": root, "tool_name": "exec_command",
+                "tool_input": {"command":
+                    ('rg -n --hidden "runtime.*(lease|hook)|<input>" "%s" '
+                     '2>$null | Select-Object -Last 160') % read_parent}}, env=env)
+            rg_with_quoted_angle = _run_guard({
+                "session_id": "reader-D", "cwd": root, "tool_name": "shell",
+                "tool_input": {"command":
+                    "rg -n -l '<input>session</input>' '%s'" % read_parent}}, env=env)
+            rg_with_child_text = _run_guard({
+                "session_id": "reader-E", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'rg -n "bash -c \'rm C:\\tmp\\x\'" "%s"' % read_parent}}, env=env)
+            writer_after_readers = _run_guard({
+                "session_id": "writer-after-readers", "cwd": root, "tool_name": "Edit",
+                "tool_input": {"file_path": read_target}}, env=env)
+            read_owner = _lease_owner(env["WORKSPACE_WRITE_LEASE_DB"], read_target)
+            parent_owner = _lease_owner(env["WORKSPACE_WRITE_LEASE_DB"], read_parent)
+            root_owner = _lease_owner(env["WORKSPACE_WRITE_LEASE_DB"], root)
+            check("absolute readers не лизуют файл или parent",
+                  absolute_reader_a.returncode == 0 and
+                  absolute_reader_b.returncode == 0 and
+                  rg_with_null.returncode == 0 and
+                  rg_with_quoted_angle.returncode == 0 and
+                  rg_with_child_text.returncode == 0 and
+                  writer_after_readers.returncode == 0 and
+                  read_owner and read_owner.get("session") == "writer-after-readers" and
+                  parent_owner is None and root_owner is None,
+                  "readA=%s readB=%s rg-null=%s rg-angle=%s rg-child-text=%s writer=%s "
+                  "file=%r parent=%r root=%r" %
+                  (absolute_reader_a.returncode, absolute_reader_b.returncode,
+                   rg_with_null.returncode, rg_with_quoted_angle.returncode,
+                   rg_with_child_text.returncode, writer_after_readers.returncode,
+                   read_owner, parent_owner, root_owner))
+            check("literal rg repro не лизует входные absolute roots",
+                  rg_with_null.returncode == 0 and
+                  rg_with_quoted_angle.returncode == 0 and
+                  rg_with_child_text.returncode == 0 and
+                  parent_owner is None and root_owner is None)
+            _run_guard({"session_id": "writer-after-readers", "cwd": root}, "stop", env)
+            if HOOKS not in sys.path:
+                sys.path.insert(0, HOOKS)
+            import workspace_write_guard as guard_module
+            check("read-only whitelist не пропускает PowerShell script-block",
+                  not guard_module.shell_is_read_only(
+                      "Get-Content x | Where-Object { Remove-Item x; $true }"))
+            check("read-only whitelist не пропускает git --output",
+                  not guard_module.shell_is_read_only("git diff --output=stolen.patch"))
+            quoted_target = os.path.join(root, "quoted-child-writer.txt")
+            quoted_holder = _run_guard({
+                "session_id": "quoted-holder", "cwd": root, "tool_name": "Edit",
+                "tool_input": {"file_path": quoted_target}}, env=env)
+            quoted_powershell = _run_guard({
+                "session_id": "quoted-powershell", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'powershell -Command "Set-Content -LiteralPath \'%s\' -Value y"' %
+                    quoted_target}}, env=env)
+            quoted_cmd = _run_guard({
+                "session_id": "quoted-cmd", "cwd": root, "tool_name": "exec_command",
+                "tool_input": {"command":
+                    'cmd /c "echo y > %s"' % quoted_target}}, env=env)
+            quoted_bash = _run_guard({
+                "session_id": "quoted-bash", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'bash -lc "echo y > %s"' % quoted_target}}, env=env)
+            quoted_sh = _run_guard({
+                "session_id": "quoted-sh", "cwd": root, "tool_name": "shell",
+                "tool_input": {"command":
+                    'sh -ec "echo y > %s"' % quoted_target}}, env=env)
+            quoted_path_pwsh = _run_guard({
+                "session_id": "quoted-path-pwsh", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    '& "C:\\Program Files\\PowerShell\\7\\pwsh.exe" -Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            quoted_path_cmd = _run_guard({
+                "session_id": "quoted-path-cmd", "cwd": root,
+                "tool_name": "exec_command",
+                "tool_input": {"command":
+                    '"C:\\Windows\\System32\\cmd.exe" /c "echo y > %s"' %
+                    quoted_target}}, env=env)
+            quoted_path_pwsh_options = _run_guard({
+                "session_id": "quoted-path-pwsh-options", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    '& "C:\\Program Files\\PowerShell\\7\\pwsh.exe" -NoProfile '
+                    '-ExecutionPolicy Bypass -Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            quoted_flag_pwsh = _run_guard({
+                "session_id": "quoted-flag-pwsh", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'powershell "-Command" '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            command_with_args = _run_guard({
+                "session_id": "command-with-args", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'pwsh -CommandWithArgs '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            working_directory = _run_guard({
+                "session_id": "working-directory", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'pwsh -WorkingDirectory \'%s\' -Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' %
+                    (root, quoted_target)}}, env=env)
+            quoted_call_cmdlet = _run_guard({
+                "session_id": "quoted-call-cmdlet", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'powershell -Command '
+                    '"& \'Set-Content\' -LiteralPath \'%s\' -Value y"' %
+                    quoted_target}}, env=env)
+            single_amp_chain = _run_guard({
+                "session_id": "single-amp-chain", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'echo ok & powershell -Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            backslash_quote = _run_guard({
+                "session_id": "backslash-quote", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'Get-ChildItem -LiteralPath "%s\\\\"; '
+                    'Set-Content -LiteralPath "%s" -Value y' %
+                    (root, quoted_target)}}, env=env)
+            check("quoted PowerShell/cmd writers блокируются holder",
+                  quoted_holder.returncode == 0 and
+                  quoted_powershell.returncode == 2 and
+                  "quoted-holder" in quoted_powershell.stderr and
+                  quoted_cmd.returncode == 2 and "quoted-holder" in quoted_cmd.stderr,
+                  "holder=%s powershell=%s/%s cmd=%s/%s" %
+                  (quoted_holder.returncode, quoted_powershell.returncode,
+                   quoted_powershell.stderr[:120], quoted_cmd.returncode,
+                   quoted_cmd.stderr[:120]))
+            check("quoted bash -lc/sh -ec writers видны, rg pattern остаётся reader",
+                  quoted_bash.returncode == 2 and "quoted-holder" in quoted_bash.stderr and
+                  quoted_sh.returncode == 2 and "quoted-holder" in quoted_sh.stderr and
+                  rg_with_child_text.returncode == 0,
+                  "bash=%s/%s sh=%s/%s rg=%s" %
+                  (quoted_bash.returncode, quoted_bash.stderr[:100],
+                   quoted_sh.returncode, quoted_sh.stderr[:100],
+                   rg_with_child_text.returncode))
+            check("quoted executable path child writers блокируются holder",
+                  quoted_path_pwsh.returncode == 2 and
+                  "quoted-holder" in quoted_path_pwsh.stderr and
+                  quoted_path_cmd.returncode == 2 and
+                  "quoted-holder" in quoted_path_cmd.stderr,
+                  "pwsh=%s/%s cmd=%s/%s" %
+                  (quoted_path_pwsh.returncode, quoted_path_pwsh.stderr[:120],
+                   quoted_path_cmd.returncode, quoted_path_cmd.stderr[:120]))
+            option_variants = [
+                ("options", quoted_path_pwsh_options),
+                ("quoted-flag", quoted_flag_pwsh),
+                ("command-with-args", command_with_args),
+                ("working-directory", working_directory),
+                ("quoted-call", quoted_call_cmdlet),
+                ("single-amp", single_amp_chain),
+                ("backslash-quote", backslash_quote),
+            ]
+            check("PowerShell option/backslash/call variants блокируются holder",
+                  all(run.returncode == 2 and "quoted-holder" in run.stderr
+                      for _name, run in option_variants),
+                  [(name, run.returncode, run.stderr[:100])
+                   for name, run in option_variants])
+            _run_guard({"session_id": "quoted-holder", "cwd": root}, "stop", env)
+            quoted_executable = r"C:\Program Files\PowerShell\7\pwsh.exe"
+            exec_target_a = os.path.join(root, "quoted-exec-output-a.txt")
+            exec_target_b = os.path.join(root, "quoted-exec-output-b.txt")
+            exec_a = _run_guard({
+                "session_id": "quoted-exec-A", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    '& "%s" -NoProfile -ExecutionPolicy Bypass -Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value a"' %
+                    (quoted_executable, exec_target_a)}}, env=env)
+            exec_b = _run_guard({
+                "session_id": "quoted-exec-B", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    '& "%s" -NoProfile -ExecutionPolicy Bypass -Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value b"' %
+                    (quoted_executable, exec_target_b)}}, env=env)
+            executable_owner = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], quoted_executable)
+            exec_owner_a = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], exec_target_a)
+            exec_owner_b = _lease_owner(
+                env["WORKSPACE_WRITE_LEASE_DB"], exec_target_b)
+            check("один pwsh executable не сериализует разные output files",
+                  exec_a.returncode == 0 and exec_b.returncode == 0 and
+                  executable_owner is None and exec_owner_a and exec_owner_b and
+                  exec_owner_a.get("session") == "quoted-exec-A" and
+                  exec_owner_b.get("session") == "quoted-exec-B",
+                  "a=%s b=%s exe=%r out-a=%r out-b=%r" %
+                  (exec_a.returncode, exec_b.returncode, executable_owner,
+                   exec_owner_a, exec_owner_b))
+            _run_guard({"session_id": "quoted-exec-A", "cwd": root}, "stop", env)
+            _run_guard({"session_id": "quoted-exec-B", "cwd": root}, "stop", env)
+            # 14.09.2026, класс lease-storm. ЗДЕСЬ БЫЛ ОБРАТНЫЙ ИНВАРИАНТ: `python mystery.py`
+            # лизовал cwd ЦЕЛИКОМ, и тест требовал, чтобы сосед после этого не мог править
+            # СВОЙ файл в той же папке. Это и есть шторм, записанный как «защита»: замер 14.09
+            # -- 198 блокировок, 69% из них запрос ПАПКИ, 36 пострадавших сессий, среди жертв
+            # чтение файла. Защита была ещё и мнимой: путь цели в такой команде не назван, так
+            # что от РЕАЛЬНОЙ гонки за файл папочная лиза не спасала -- она лишь запирала
+            # непричастных. Новый инвариант: неизвестная команда без признака записи не лизует
+            # ничего, а гонку за конкретный файл по-прежнему ловит файловый инструмент.
+            unknown_writer = _run_guard({"session_id": "script-A", "cwd": root,
+                                         "tool_name": "Bash",
+                                         "tool_input": {"command": "python mystery.py"}}, env=env)
+            neighbour = _run_guard({"session_id": "script-B", "cwd": root,
+                                    "tool_name": "Edit",
+                                    "tool_input": {"file_path": target}}, env=env)
+            check("неизвестный shell-процесс НЕ запирает соседей по папке",
+                  unknown_writer.returncode == 0 and neighbour.returncode == 0,
+                  "writer=%s neighbour=%s" % (unknown_writer.returncode, neighbour.returncode))
+            check("child-script/relative-path дыра названа поведением",
+                  unknown_writer.returncode == 0,
+                  "python mystery.py has no visible absolute write target")
+            relative_writer = _run_guard({
+                "session_id": "script-relative", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'Set-Content -LiteralPath ".\\shared file.md" -Value overwrite'}},
+                env=env)
+            check("direct relative shell-target тоже остаётся честной дырой",
+                  relative_writer.returncode == 0,
+                  "relative Set-Content target is not an extracted absolute path")
+            absolute_writer = _run_guard({
+                "session_id": "script-absolute", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'Set-Content -LiteralPath "%s" -Value overwrite' % target}}, env=env)
+            check("тот же direct shell с абсолютной целью блокируется holder",
+                  absolute_writer.returncode == 2 and "script-B" in absolute_writer.stderr,
+                  "rc=%s stderr=%s" %
+                  (absolute_writer.returncode, absolute_writer.stderr[:200]))
+            same_file = _run_guard({"session_id": "script-C", "cwd": root,
+                                    "tool_name": "Edit",
+                                    "tool_input": {"file_path": target}}, env=env)
+            check("гонка за ОДИН файл по-прежнему отбивается",
+                  same_file.returncode == 2, "same_file=%s" % same_file.returncode)
+            _run_guard({"session_id": "script-B", "cwd": root}, "stop", env)
+            _run_guard({"session_id": "script-A", "cwd": root}, "stop", env)
+            env_sid = dict(env)
+            env_sid["CODEX_THREAD_ID"] = "env-only-session"
+            env_target = os.path.join(root, "env-session.md")
+            env_acquire = _run_guard({"cwd": root, "tool_name": "Edit",
+                                      "tool_input": {"file_path": env_target}}, env=env_sid)
+            env_stop = subprocess.run([sys.executable, TURNSTATE],
+                                      input=json.dumps({"cwd": root, "hook_event_name": "Stop"}),
+                                      capture_output=True, text=True, encoding="utf-8",
+                                      errors="replace", env=env_sid, timeout=30)
+            env_after = _run_guard({"session_id": "after-env", "cwd": root,
+                                    "tool_name": "Edit",
+                                    "tool_input": {"file_path": env_target}}, env=env)
+            check("Stop использует тот же env fallback session-id",
+                  env_acquire.returncode == 0 and env_stop.returncode == 0 and
+                  env_after.returncode == 0,
+                  "acquire=%s stop=%s after=%s" % (env_acquire.returncode,
+                  env_stop.returncode, env_after.returncode))
+
+            help_run = subprocess.run([sys.executable, GUARD, "--help"],
+                                      capture_output=True, text=True, timeout=30)
+            bad_flag = subprocess.run([sys.executable, GUARD, "--wat"],
+                                      capture_output=True, text=True, timeout=30)
+            check("guard --help", help_run.returncode == 0 and "usage:" in help_run.stdout)
+            check("guard отвергает неизвестный флаг", bad_flag.returncode == 2)
+            audit_leaks = _new_matching_lines(
+                production_audit, production_audit_before, (root, "codex-A"))
+            check("тест не пишет production constitution audit", not audit_leaks,
+                  "test-attributed rows=%r; production bytes %d->%d" %
+                  (audit_leaks[:3], production_audit_before,
+                   _file_size(production_audit)))
+            counter = env["WORKSPACE_WRITE_LEASE_COUNTER"]
+            counter_rows = []
+            if os.path.isfile(counter):
+                with open(counter, encoding="utf-8") as fh:
+                    counter_rows = [json.loads(line) for line in fh if line.strip()]
+            def row_names_temp_resource(row):
+                resources = row.get("resources") or []
+                return any(
+                    os.path.normcase(os.path.realpath(str(resource))).startswith(
+                        os.path.normcase(os.path.realpath(root)) + os.sep)
+                    for resource in resources)
+            check("test usage-counter содержит hook acquired/blocked с temp resource",
+                  bool(counter_rows) and
+                  any(row.get("event") == "hook" and
+                      row.get("outcome") == "acquired" and
+                      row_names_temp_resource(row) for row in counter_rows) and
+                  any(row.get("event") == "hook" and
+                      row.get("outcome") == "blocked" and
+                      row_names_temp_resource(row) for row in counter_rows),
+                  "rows=%d path=%s" % (len(counter_rows), counter))
+            target_key = os.path.normcase(os.path.realpath(target))
+            acquired_epoch_rows = [
+                row for row in counter_rows
+                if row.get("event") == "hook" and
+                row.get("outcome") == "acquired" and
+                row.get("session") == "codex-A" and
+                row.get("epoch") == "turn-A" and
+                target_key in (row.get("resources") or [])]
+            blocked_fence_rows = [
+                row for row in counter_rows
+                if row.get("event") == "acquire" and
+                row.get("outcome") == "blocked" and
+                row.get("session") == "claude-B" and
+                row.get("epoch") == "" and
+                row.get("held_by") == ["codex-A"] and
+                row.get("held_epochs") == ["turn-A"] and
+                target_key in (row.get("resources") or [])]
+            check("telemetry хранит exact epoch + holder epoch",
+                  bool(acquired_epoch_rows) and bool(blocked_fence_rows),
+                  "acquired=%r blocked=%r" %
+                  (acquired_epoch_rows[:1], blocked_fence_rows[:1]))
+            usage_leaks = _new_matching_lines(
+                production_usage, production_usage_before,
+                (root, "codex-A", "codex-same", "hook-session-",
+                 "writer-after-readers"))
+            check("integration test не пишет production workspace usage",
+                  not usage_leaks,
+                  "test-attributed rows=%r; production bytes %d->%d" %
+                  (usage_leaks[:3], production_usage_before,
+                   _file_size(production_usage)))
+    finally:
+        shutil.rmtree(root, ignore_errors=True)
+
+    bad = [name for name, ok, _ in RESULTS if not ok]
+    print("\nВЕРДИКТ: %s" % ("PASS" if not bad else "FAIL: " + "; ".join(bad)))
+    return 0 if not bad else 1
+
+
+if __name__ == "__main__":
+    try:
+        sys.stdout.reconfigure(encoding="utf-8")
+        sys.stderr.reconfigure(encoding="utf-8")
+    except Exception:
+        pass
+    if len(sys.argv) > 1 and sys.argv[1] == "--guard-child":
+        sys.exit(_guard_child(sys.argv[2], sys.argv[3], sys.argv[4], sys.argv[5]))
+    sys.path.insert(0, SCRIPTS)
+    sys.exit(main())
diff --git a/_test_workspace_write_lease.py b/_test_workspace_write_lease.py
index cb6ffe73f..28bd06a99 100644
--- a/_test_workspace_write_lease.py
+++ b/_test_workspace_write_lease.py
@@ -1,19 +1,38 @@
 # -*- coding: utf-8 -*-
 """Red/green acceptance for workspace_write_lease.py.
 
-Purpose: prove that eight Claude/Codex sessions racing for one path produce exactly
-one owner, that parent/child paths conflict, and that an expired owner is reaped.
-Input/output: temporary local SQLite DB and JSONL counter; prints checks, rc 0/1.
-Caller: /tt for Codex Shared Workspace Safety and future regression runs.
-Rail: local Python stdlib, 0 LLM, 0 network.
-Test: this file; its naive read-then-write mutant must produce multiple winners.
-updated: 2026-09-11
+Purpose: prove atomic local contention and fenced release. Two real CLI writers of
+one absolute file must split rc=0/7, BUSY must name the winner, and neither a foreign
+release nor a delayed old epoch may remove a newer lease. Input/output: isolated
+SQLite DB + JSONL counter; prints checks, rc 0/1. Caller: /tt for Codex Shared
+Workspace Safety. Rail: local Python stdlib, 0 LLM, 0 network.
+
+KILL-LIST (source mutation -> case that must fail):
+- replace ``BEGIN IMMEDIATE`` acquisition with read-then-write ->
+  ``mutation: acquire без BEGIN IMMEDIATE обязана дать >1 winner``;
+- remove the serialized/rechecked epoch migration ->
+  ``mutation: migration без lock/recheck обязана стать красной``;
+- change owner identity from ``session + epoch`` to ``session`` ->
+  ``живая старая эпоха блокирует новую эпоху того же session``;
+- change fenced delete to ``DELETE ... WHERE session=?`` ->
+  ``mutation: unfenced release обязана стать красной``.
+- remove the token-aware Stop fallback for a migrated empty-epoch row ->
+  ``mutation: legacy migration handoff обязана стать красной``;
+- drop ``--epoch`` forwarding in either CLI acquire or CLI release ->
+  ``mutation: CLI обязан передавать epoch в acquire/release``.
+Each of the seven production-source mutations (plus the naive race model) is
+executed against an isolated copy/state; an honest gap is
+preferable to claiming a mutation that this suite does not kill.
+updated: 2026-09-21
 """
 from __future__ import annotations
 
 import json
+import importlib.util
+import inspect
 import os
 import shutil
+import sqlite3
 import subprocess
 import sys
 import tempfile
@@ -39,19 +58,38 @@ def _wait(ts):
         time.sleep(min(0.02, left / 2))
 
 
-def _child(mode, root, start, holder, target):
+def _load_candidate(path, label):
+    name = "workspace_write_lease_%s_%d" % (label, os.getpid())
+    spec = importlib.util.spec_from_file_location(name, path)
+    module = importlib.util.module_from_spec(spec)
+    sys.modules[name] = module
+    spec.loader.exec_module(module)
+    return module
+
+
+def _child(mode, root, start, holder, target, candidate=""):
     os.environ["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "leases.sqlite3")
     os.environ["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
     _wait(start)
-    if mode == "atomic":
+    if mode in {"atomic", "candidate"}:
         try:
-            import workspace_write_lease as lease
+            if mode == "candidate":
+                lease = _load_candidate(candidate, "race")
+            else:
+                import workspace_write_lease as lease
         except Exception as exc:
             print("ERROR import %r" % (exc,))
             return 3
         result = lease.acquire_many([target], holder, "race-test", ttl_sec=600)
-        print("WIN" if result.ok else "LOSE")
-        return 0
+        if result.ok:
+            print("WIN %s" % holder)
+            return 0
+        owners = sorted({str(row.get("session") or "") for row in result.conflicts})
+        if owners:
+            print("LOSE BUSY held by %s" % ",".join(owners))
+            return 0
+        print("ERROR blocked without holder")
+        return 3
     marker = os.path.join(root, "naive.marker")
     if os.path.exists(marker):
         print("LOSE")
@@ -63,26 +101,345 @@ def _child(mode, root, start, holder, target):
     return 0
 
 
-def _race(mode, root, target):
+def _race(mode, root, target, candidate=""):
     start = time.time() + LEAD_SEC
     ps = [subprocess.Popen(
         [sys.executable, os.path.abspath(__file__), "--child", mode, root,
-         "%.6f" % start, "session-%d" % i, target],
+         "%.6f" % start, "session-%d" % i, target, candidate],
         stdout=subprocess.PIPE, stderr=subprocess.PIPE)
         for i in range(RACERS)]
-    wins, errors = 0, []
+    winners, loser_holders, errors = [], [], []
     for proc in ps:
         out, err = proc.communicate(timeout=60)
         text = out.decode("utf-8", "replace").strip()
-        if text.endswith("WIN"):
-            wins += 1
-        elif not text.endswith("LOSE"):
+        if mode == "naive" and text == "WIN":
+            winners.append("naive")
+        elif mode == "naive" and text == "LOSE":
+            pass
+        elif text.startswith("WIN "):
+            winners.append(text[4:].strip())
+        elif text.startswith("LOSE BUSY held by "):
+            loser_holders.append(text[len("LOSE BUSY held by "):].strip())
+        else:
             errors.append("rc=%s out=%r err=%r" %
                           (proc.returncode, text, err.decode("utf-8", "replace")[:160]))
-    return wins, errors
+    if mode != "naive" and len(winners) == 1:
+        wrong = [holder for holder in loser_holders if holder != winners[0]]
+        if len(loser_holders) != RACERS - 1 or wrong:
+            errors.append("winner=%r loser_holders=%r" % (winners, loser_holders))
+    return len(winners), errors
+
+
+def _cli_contention(lease_file, root, target):
+    """Run two actual CLI acquire processes against one absolute file."""
+    env = dict(os.environ)
+    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "cli.sqlite3")
+    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "cli-counter.jsonl")
+    sessions = ("cli-writer-A", "cli-writer-B")
+    procs = []
+    for index, session in enumerate(sessions):
+        cmd = [sys.executable, lease_file, "acquire", target,
+               "--session", session, "--agent", "cli-race",
+               "--epoch", "cli-turn-%d" % index, "--ttl-sec", "600"]
+        procs.append((session, subprocess.Popen(
+            cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE, env=env)))
+    runs = []
+    for session, proc in procs:
+        out, err = proc.communicate(timeout=60)
+        runs.append({"session": session, "rc": proc.returncode,
+                     "out": out.decode("utf-8", "replace").strip(),
+                     "err": err.decode("utf-8", "replace").strip()})
+    return runs
+
+
+def _cli_run(lease_file, env, *args):
+    run = subprocess.run([sys.executable, lease_file] + list(args),
+                         capture_output=True, text=True, encoding="utf-8",
+                         errors="replace", env=env, timeout=30)
+    return {"args": list(args), "rc": run.returncode,
+            "out": run.stdout.strip(), "err": run.stderr.strip()}
+
+
+def _cli_epoch_lifecycle(lease_file, root, target):
+    """Exercise CLI acquire/release fencing with one session and two epochs."""
+    os.makedirs(root, exist_ok=True)
+    env = dict(os.environ)
+    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "cli-epoch.sqlite3")
+    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
+    session = "cli-same-session"
+    steps = [
+        _cli_run(lease_file, env, "acquire", target, "--session", session,
+                 "--agent", "cli-fence", "--epoch", "cli-old"),
+        _cli_run(lease_file, env, "acquire", target, "--session", session,
+                 "--agent", "cli-fence", "--epoch", "cli-new"),
+        _cli_run(lease_file, env, "release-session", "--session", session,
+                 "--epoch", "cli-old"),
+        _cli_run(lease_file, env, "acquire", target, "--session", session,
+                 "--agent", "cli-fence", "--epoch", "cli-new"),
+        _cli_run(lease_file, env, "release-session", "--session", session,
+                 "--epoch", "cli-old"),
+        _cli_run(lease_file, env, "check", target),
+        _cli_run(lease_file, env, "release-session", "--session", session,
+                 "--epoch", "cli-new"),
+        _cli_run(lease_file, env, "check", target),
+    ]
+    expected = [0, 7, 0, 0, 0, 7, 0, 0]
+    ok = [step["rc"] for step in steps] == expected
+    ok = ok and "RELEASED 1" in steps[2]["out"]
+    ok = ok and "RELEASED 0" in steps[4]["out"]
+    ok = ok and '"epoch": "cli-new"' in steps[5]["out"]
+    ok = ok and "RELEASED 1" in steps[6]["out"]
+    ok = ok and steps[7]["out"] == "FREE"
+    return ok, steps
+
+
+def _late_release_invariant(lease, target, *, mutant):
+    """Return True only if a late old-epoch release preserves the new epoch."""
+    lease.release_all_for_tests()
+    first = lease.acquire_many([target], "same-session", "codex", 1,
+                               now=100.0, epoch="turn-old")
+    second = lease.acquire_many([target], "same-session", "codex", 60,
+                                now=102.0, epoch="turn-new")
+    if mutant:
+        con = sqlite3.connect(lease.db_path())
+        try:
+            con.execute("DELETE FROM leases WHERE session=?", ("same-session",))
+            con.commit()
+        finally:
+            con.close()
+    else:
+        lease.release_session("same-session", epoch="turn-old")
+    owner = lease.owner_of(target, now=102.0)
+    return bool(first.ok and second.ok and owner and
+                owner.get("session") == "same-session" and
+                owner.get("epoch") == "turn-new")
+
+
+def _file_size(path):
+    return os.path.getsize(path) if os.path.isfile(path) else 0
+
+
+def _production_counter_leaks(path, offset, root):
+    """Return rows attributable to this isolated test, tolerating other live writers."""
+    if not os.path.isfile(path):
+        return []
+    if os.path.getsize(path) < offset:
+        return ["production counter shrank/rotated during the test"]
+    with open(path, "rb") as fh:
+        fh.seek(offset)
+        suffix = fh.read().decode("utf-8", "replace")
+    markers = [root.lower(), "cli-writer-", "same-session", "race-test",
+               "post-migration", "migration-mutant"]
+    return [line for line in suffix.splitlines()
+            if any(marker in line.lower() for marker in markers)]
+
+
+def _create_legacy_db(lease, path, preserved):
+    con = sqlite3.connect(path)
+    try:
+        con.execute("""CREATE TABLE leases(
+            resource TEXT PRIMARY KEY, session TEXT NOT NULL, agent TEXT NOT NULL,
+            host TEXT NOT NULL, cwd TEXT, acquired REAL NOT NULL,
+            expires REAL NOT NULL, note TEXT)""")
+        con.execute("INSERT INTO leases VALUES(?,?,?,?,?,?,?,?)",
+                    (lease.norm_path(preserved), "pre-migration", "legacy", "host",
+                     "", 100.0, 9999999999.0, "keep"))
+        con.commit()
+    finally:
+        con.close()
+
+
+def _migration_child(root, start, lease_file):
+    env = dict(os.environ)
+    env["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "legacy.sqlite3")
+    env["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
+    _wait(start)
+    run = subprocess.run([sys.executable, lease_file, "status", "--json"],
+                         capture_output=True, text=True, encoding="utf-8",
+                         errors="replace", env=env, timeout=30)
+    if run.returncode == 0:
+        print("OK")
+        return 0
+    print("ERROR rc=%s out=%r err=%r" %
+          (run.returncode, run.stdout[:120], run.stderr[:2000]))
+    return 1
+
+
+def _migration_wave(lease, lease_file, root, racers=24):
+    os.makedirs(root, exist_ok=True)
+    _create_legacy_db(lease, os.path.join(root, "legacy.sqlite3"),
+                      os.path.join(root, "preserved.md"))
+    start = time.time() + LEAD_SEC
+    procs = [subprocess.Popen(
+        [sys.executable, os.path.abspath(__file__), "--migration-child", root,
+         "%.6f" % start, lease_file], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
+        for _ in range(racers)]
+    errors = []
+    for proc in procs:
+        out, err = proc.communicate(timeout=60)
+        text = out.decode("utf-8", "replace").strip()
+        if proc.returncode != 0 or not text.endswith("OK"):
+            errors.append("rc=%s out=%r err=%r" %
+                          (proc.returncode, text, err.decode("utf-8", "replace")[:200]))
+    con = sqlite3.connect(os.path.join(root, "legacy.sqlite3"))
+    try:
+        columns = {row[1] for row in con.execute("PRAGMA table_info(leases)")}
+        preserved = con.execute(
+            "SELECT session,epoch FROM leases WHERE session=?", ("pre-migration",)
+        ).fetchone() if "epoch" in columns else None
+    finally:
+        con.close()
+    if "epoch" not in columns or preserved != ("pre-migration", ""):
+        errors.append("post-migration state invalid columns=%r preserved=%r" %
+                      (sorted(columns), preserved))
+    return errors
+
+
+def _migration_mutant(source_file, destination):
+    """Create an isolated broken copy: no migration lock/recheck, widened race."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    start = source.index("def _migrate_epoch(con):")
+    end = source.index("\n\ndef _connect():", start)
+    block = source[start:end]
+    lock = '    con.execute("BEGIN IMMEDIATE")\n'
+    check = ('        if "epoch" not in columns:\n'
+             '            con.execute("ALTER TABLE leases ADD COLUMN epoch TEXT NOT NULL DEFAULT \'\'")')
+    widened = ('        if "epoch" not in columns:\n'
+               '            time.sleep(0.20)\n'
+               '            con.execute("ALTER TABLE leases ADD COLUMN epoch TEXT NOT NULL DEFAULT \'\'")')
+    if block.count(lock) != 1 or block.count(check) != 1:
+        raise AssertionError("migration mutation did not match exactly once")
+    block = block.replace(lock, "", 1).replace(check, widened, 1)
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source[:start] + block + source[end:])
+    return destination
+
+
+def _acquire_mutant(source_file, destination):
+    """Create an isolated production-code mutant with the acquisition lock removed."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    start = source.index("def acquire_many(")
+    end = source.index("\n\ndef release_session(", start)
+    block = source[start:end]
+    lock = '        con.execute("BEGIN IMMEDIATE")\n'
+    read = "        live = _rows(con, now)\n"
+    if block.count(lock) != 1 or block.count(read) != 1:
+        raise AssertionError("acquire mutation did not match exactly once")
+    block = block.replace(lock, "", 1).replace(
+        read, read + "        time.sleep(0.20)\n", 1)
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source[:start] + block + source[end:])
+    return destination
+
+
+def _owner_identity_mutant(source_file, destination):
+    """Create a copy that treats session alone, not session+epoch, as ownership."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    start = source.index("def acquire_many(")
+    end = source.index("\n\ndef release_session(", start)
+    block = source[start:end]
+    guarded = ('                same_owner = row["session"] == session and '
+               'row.get("epoch", "") == epoch')
+    broken = '                same_owner = row["session"] == session'
+    if block.count(guarded) != 1:
+        raise AssertionError("owner-identity mutation did not match exactly once")
+    block = block.replace(guarded, broken, 1)
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source[:start] + block + source[end:])
+    return destination
+
+
+def _release_mutant(source_file, destination):
+    """Create a copy whose delayed release deletes every epoch of a session."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    start = source.index("def release_session(")
+    end = source.index("\n\ndef reap(", start)
+    block = source[start:end]
+    guarded = ('        n = con.execute("DELETE FROM leases WHERE session=? AND epoch=?",\n'
+               '                        (session, exact_epoch)).rowcount')
+    broken = ('        n = con.execute("DELETE FROM leases WHERE session=?",\n'
+              '                        (session,)).rowcount')
+    if block.count(guarded) != 1:
+        raise AssertionError("release mutation did not match exactly once")
+    block = block.replace(guarded, broken, 1)
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source[:start] + block + source[end:])
+    return destination
+
+
+def _legacy_handoff_mutant(source_file, destination):
+    """Create a copy that strands pre-upgrade empty-epoch rows until TTL."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    guarded = ("        legacy_handoff = 0\n"
+               "        if not n and epoch is not None and exact_epoch:\n"
+               "            legacy_handoff = con.execute(\n"
+               "                \"DELETE FROM leases WHERE session=? AND epoch=''\", "
+               "(session,)).rowcount\n"
+               "            n += legacy_handoff\n")
+    broken = "        legacy_handoff = 0\n"
+    if source.count(guarded) != 1:
+        raise AssertionError("legacy handoff mutation did not match exactly once")
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source.replace(guarded, broken, 1))
+    return destination
+
+
+def _cli_epoch_mutant(source_file, destination, operation):
+    """Create a CLI mutant that accepts --epoch but drops it before the API."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    if operation == "acquire":
+        guarded = "cwd=args.cwd, note=args.note, epoch=args.epoch)"
+        broken = "cwd=args.cwd, note=args.note, epoch=None)"
+    elif operation == "release":
+        guarded = "release_session(args.session, epoch=args.epoch)"
+        broken = "release_session(args.session, epoch=None)"
+    else:
+        raise AssertionError("unknown CLI mutation %r" % operation)
+    if source.count(guarded) != 1:
+        raise AssertionError("CLI %s mutation did not match exactly once" % operation)
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source.replace(guarded, broken, 1))
+    return destination
+
+
+def _old_schema_migrates(lease, root):
+    """Build the pre-epoch schema and require an in-place, data-safe upgrade."""
+    os.makedirs(root, exist_ok=True)
+    original = os.environ["WORKSPACE_WRITE_LEASE_DB"]
+    legacy_db = os.path.join(root, "legacy-schema.sqlite3")
+    _create_legacy_db(lease, legacy_db, os.path.join(root, "preserved.md"))
+    os.environ["WORKSPACE_WRITE_LEASE_DB"] = legacy_db
+    try:
+        before = lease.owner_of(os.path.join(root, "preserved.md"))
+        acquired = lease.acquire_many([os.path.join(root, "new.md")],
+                                      "post-migration", "test", 60,
+                                      epoch="turn-migrated")
+        con = sqlite3.connect(legacy_db)
+        try:
+            columns = {row[1] for row in con.execute("PRAGMA table_info(leases)")}
+        finally:
+            con.close()
+        released = lease.release_session("pre-migration", epoch="turn-after-upgrade")
+        after_release = lease.owner_of(os.path.join(root, "preserved.md"))
+        return bool(before and before.get("epoch") == "" and
+                    before.get("session") == "pre-migration" and
+                    acquired.ok and "epoch" in columns and
+                    released == 1 and after_release is None)
+    finally:
+        os.environ["WORKSPACE_WRITE_LEASE_DB"] = original
 
 
 def main():
+    production_counter = os.path.join(
+        os.environ.get("LOCALAPPDATA") or os.path.join(os.path.expanduser("~"), ".local"),
+        "AntonAgents", "workspace-write-leases", "usage.jsonl")
+    production_counter_before = _file_size(production_counter)
     root = tempfile.mkdtemp(prefix="workspace-write-lease-test-")
     os.environ["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "leases.sqlite3")
     os.environ["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
@@ -97,21 +454,54 @@ def main():
         else:
             check("lease-модуль существует", True)
 
+        epoch_supported = bool(lease is not None and
+            "epoch" in inspect.signature(lease.acquire_many).parameters and
+            "epoch" in inspect.signature(lease.release_session).parameters)
+        check("API заморожен с fencing epoch", epoch_supported)
+
         print("== RED-FIRST: тест обязан ловить старую read-then-write гонку ==")
         mutant_wins, mutant_errors = _race("naive", root, target)
-        check("мутант даёт больше одного победителя", mutant_wins > 1,
+        check("мутант даёт >1 winner без crashes",
+              mutant_wins > 1 and not mutant_errors,
               "wins=%d errors=%s" % (mutant_wins, mutant_errors))
 
         if lease is not None:
+            acquire_mutant = _acquire_mutant(
+                lease.__file__, os.path.join(root, "workspace_write_lease_acquire_mutant.py"))
+            acquire_mutant_root = os.path.join(root, "acquire-mutant")
+            os.makedirs(acquire_mutant_root, exist_ok=True)
+            acquire_mutant_wins, acquire_mutant_errors = _race(
+                "candidate", acquire_mutant_root,
+                os.path.join(acquire_mutant_root, "same.txt"), acquire_mutant)
+            check("mutation: acquire без BEGIN IMMEDIATE обязана дать >1 winner",
+                  acquire_mutant_wins > 1 and not acquire_mutant_errors,
+                  "wins=%d errors=%s" %
+                  (acquire_mutant_wins, acquire_mutant_errors))
             try:
                 os.remove(os.environ["WORKSPACE_WRITE_LEASE_DB"])
             except OSError:
                 pass
             print("== GREEN TARGET: настоящая параллельная гонка ==")
             wins, errors = _race("atomic", root, target)
-            check("8 процессов -> ровно один владелец", wins == 1,
+            check("8 процессов -> один владелец, 7 доказанных losers",
+                  wins == 1 and not errors,
                   "wins=%d errors=%s" % (wins, errors))
 
+            cli_root = os.path.join(root, "cli-race")
+            os.makedirs(cli_root, exist_ok=True)
+            cli_target = os.path.abspath(os.path.join(cli_root, "same-absolute.txt"))
+            cli_runs = _cli_contention(lease.__file__, cli_root, cli_target)
+            winners = [run for run in cli_runs if run["rc"] == 0]
+            losers = [run for run in cli_runs if run["rc"] == 7]
+            check("2 CLI-писателя -> один rc=0, второй BUSY rc=7",
+                  len(winners) == 1 and len(losers) == 1, cli_runs)
+            if len(winners) == 1 and len(losers) == 1:
+                check("CLI BUSY называет настоящего holder",
+                      "BUSY" in losers[0]["out"] and
+                      winners[0]["session"] in losers[0]["out"], cli_runs)
+            else:
+                check("CLI BUSY называет настоящего holder", False, cli_runs)
+
             lease.release_all_for_tests()
             a = lease.acquire_many([os.path.join(root, "tree")], "A", "claude", 600)
             b = lease.acquire_many([os.path.join(root, "tree", "file.md")],
@@ -125,16 +515,158 @@ def main():
 
             lease.release_session("A")
             lease.release_session("B")
-            first = lease.acquire_many([target], "old", "claude", 1, now=100.0)
-            second = lease.acquire_many([target], "new", "codex", 60, now=102.0)
-            check("TTL/reaper освобождает мёртвую лизу", first.ok and second.ok)
-            check("после перехвата владелец новый",
-                  lease.owner_of(target, now=102.0).get("session") == "new")
-            check("чужой release не снимает",
-                  lease.release_session("old") == 0 and
-                  lease.owner_of(target, now=102.0).get("session") == "new")
-            check("свой release снимает", lease.release_session("new") == 1 and
-                  lease.owner_of(target, now=102.0) is None)
+            if epoch_supported:
+                cli_epoch_ok, cli_epoch_steps = _cli_epoch_lifecycle(
+                    lease.__file__, os.path.join(root, "cli-epoch-live"),
+                    os.path.join(root, "cli-epoch-target.txt"))
+                check("CLI same-session epoch acquire/release fenced",
+                      cli_epoch_ok, cli_epoch_steps)
+                cli_mutation_results = []
+                for operation in ("acquire", "release"):
+                    cli_mutant = _cli_epoch_mutant(
+                        lease.__file__, os.path.join(
+                            root, "workspace_write_lease_cli_%s_mutant.py" % operation),
+                        operation)
+                    survived, steps = _cli_epoch_lifecycle(
+                        cli_mutant, os.path.join(root, "cli-%s-mutant" % operation),
+                        os.path.join(root, "cli-%s-target.txt" % operation))
+                    cli_mutation_results.append((operation, survived, steps))
+                check("mutation: CLI обязан передавать epoch в acquire/release",
+                      all(not survived for _operation, survived, _steps
+                          in cli_mutation_results),
+                      [(operation, survived, [step["rc"] for step in steps])
+                       for operation, survived, steps in cli_mutation_results])
+                check("старая DB мигрирует и token-aware Stop снимает legacy row",
+                      _old_schema_migrates(
+                          lease, os.path.join(root, "legacy-handoff-live")))
+                handoff_mutant_file = _legacy_handoff_mutant(
+                    lease.__file__, os.path.join(
+                        root, "workspace_write_lease_handoff_mutant.py"))
+                handoff_mutant = _load_candidate(handoff_mutant_file, "handoff")
+                check("mutation: legacy migration handoff обязана стать красной",
+                      not _old_schema_migrates(
+                          handoff_mutant, os.path.join(root, "legacy-handoff-mutant")))
+                migration_errors = []
+                for attempt in range(3):
+                    migration_errors.extend(_migration_wave(
+                        lease, lease.__file__, os.path.join(root, "migration-live-%d" % attempt)))
+                check("3x24 конкурентных first-open безопасно мигрируют старую DB",
+                      not migration_errors, migration_errors[:3])
+                mutant_file = _migration_mutant(
+                    lease.__file__, os.path.join(root, "workspace_write_lease_mutant.py"))
+                mutant_errors = _migration_wave(
+                    lease, mutant_file, os.path.join(root, "migration-mutant"))
+                check("mutation: migration без lock/recheck обязана стать красной",
+                      bool(mutant_errors) and any(
+                          "duplicate column name: epoch" in error for error in mutant_errors),
+                      mutant_errors[:3])
+                original_db = os.environ["WORKSPACE_WRITE_LEASE_DB"]
+                owner_mutant_file = _owner_identity_mutant(
+                    lease.__file__, os.path.join(root, "workspace_write_lease_owner_mutant.py"))
+                os.environ["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(
+                    root, "owner-mutant.sqlite3")
+                try:
+                    owner_mutant = _load_candidate(owner_mutant_file, "owner")
+                    mutant_old = owner_mutant.acquire_many(
+                        [target], "same-session", "codex", 60,
+                        now=90.0, epoch="turn-live-old")
+                    mutant_new = owner_mutant.acquire_many(
+                        [target], "same-session", "codex", 60,
+                        now=91.0, epoch="turn-live-new")
+                    check("mutation: session-only owner обязана стать красной",
+                          mutant_old.ok and mutant_new.ok,
+                          "old=%s new=%s" % (mutant_old.ok, mutant_new.ok))
+                finally:
+                    os.environ["WORKSPACE_WRITE_LEASE_DB"] = original_db
+                lease.release_all_for_tests()
+                alive_old = lease.acquire_many([target], "same-session", "codex", 60,
+                                               now=90.0, epoch="turn-live-old")
+                blocked_new = lease.acquire_many([target], "same-session", "codex", 60,
+                                                 now=91.0, epoch="turn-live-new")
+                check("живая старая эпоха блокирует новую эпоху того же session",
+                      alive_old.ok and not blocked_new.ok and
+                      bool(blocked_new.conflicts) and
+                      blocked_new.conflicts[0].get("epoch") == "turn-live-old",
+                      blocked_new.conflicts)
+                lease.release_session("same-session", epoch="turn-live-old")
+                admitted_new = lease.acquire_many([target], "same-session", "codex", 60,
+                                                 now=91.0, epoch="turn-live-new")
+                check("новая эпоха проходит после точного release старой",
+                      admitted_new.ok)
+                lease.release_session("same-session", epoch="turn-live-new")
+                first = lease.acquire_many([target], "same-session", "codex", 1,
+                                           now=100.0, epoch="turn-old")
+                second = lease.acquire_many([target], "same-session", "codex", 60,
+                                            now=102.0, epoch="turn-new")
+                owner = lease.owner_of(target, now=102.0)
+                check("TTL/reaper даёт тому же session новую эпоху",
+                      first.ok and second.ok and owner and
+                      owner.get("epoch") == "turn-new", owner)
+                foreign = lease.release_session("intruder", epoch="turn-new")
+                check("чужой release не снимает новую эпоху",
+                      foreign == 0 and
+                      lease.owner_of(target, now=102.0).get("epoch") == "turn-new")
+                stale = lease.release_session("same-session", epoch="turn-old")
+                check("поздний release старой эпохи не снимает новую",
+                      stale == 0 and
+                      lease.owner_of(target, now=102.0).get("epoch") == "turn-new")
+                check("точный release новой эпохи снимает",
+                      lease.release_session("same-session", epoch="turn-new") == 1 and
+                      lease.owner_of(target, now=102.0) is None)
+
+                check("mutation: unfenced release обязан стать красным",
+                      not _late_release_invariant(lease, target, mutant=True))
+                release_mutant_file = _release_mutant(
+                    lease.__file__, os.path.join(root, "workspace_write_lease_release_mutant.py"))
+                os.environ["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(
+                    root, "release-mutant.sqlite3")
+                try:
+                    release_mutant = _load_candidate(release_mutant_file, "release")
+                    check("mutation-copy: unfenced release обязана стать красной",
+                          not _late_release_invariant(
+                              release_mutant, target, mutant=False))
+                finally:
+                    os.environ["WORKSPACE_WRITE_LEASE_DB"] = original_db
+                check("fenced release проходит тот же detector",
+                      _late_release_invariant(lease, target, mutant=False))
+
+                lease.release_all_for_tests()
+                tokened = lease.acquire_many([target], "legacy", "hook-caller", 60,
+                                             epoch="tokened-turn")
+                broad = lease.release_session("legacy")
+                check("legacy release без token не снимает fenced lease",
+                      tokened.ok and broad == 0 and
+                      lease.owner_of(target).get("epoch") == "tokened-turn")
+                lease.release_session("legacy", epoch="tokened-turn")
+                legacy = lease.acquire_many([target], "legacy", "direct-caller", 60)
+                check("legacy API без epoch остаётся совместим",
+                      legacy.ok and lease.release_session("legacy") == 1)
+            else:
+                check("старая DB мигрирует in-place и сохраняет lease", False,
+                      "old module has no epoch parameter")
+                check("3x24 конкурентных first-open безопасно мигрируют старую DB", False,
+                      "old module has no epoch migration")
+                check("mutation: migration без lock/recheck обязана стать красной", False,
+                      "old module has no epoch migration")
+                check("живая старая эпоха блокирует новую эпоху того же session", False,
+                      "old module has no epoch parameter")
+                check("новая эпоха проходит после точного release старой", False,
+                      "old module has no epoch parameter")
+                check("TTL/reaper даёт тому же session новую эпоху", False,
+                      "old module has no epoch parameter")
+                check("чужой release не снимает новую эпоху", False,
+                      "old module has no epoch parameter")
+                check("поздний release старой эпохи не снимает новую", False,
+                      "old module has no epoch parameter")
+                check("точный release новой эпохи снимает", False,
+                      "old module has no epoch parameter")
+                check("mutation: unfenced release обязан стать красным", False,
+                      "detector requires epoch-aware API")
+                check("fenced release проходит тот же detector", False,
+                      "detector requires epoch-aware API")
+                check("legacy release без token не снимает fenced lease", False,
+                      "old module has no epoch parameter")
+                check("legacy API без epoch остаётся совместим", True)
 
             help_run = subprocess.run([sys.executable, lease.__file__, "--help"],
                                       capture_output=True, text=True, timeout=30)
@@ -147,9 +679,20 @@ def main():
                   os.path.isfile(counter) and os.path.getsize(counter) > 0)
             if os.path.isfile(counter):
                 rows = [json.loads(line) for line in open(counter, encoding="utf-8") if line.strip()]
-                check("counter содержит allow и blocked",
+                check("counter содержит acquired и blocked",
                       any(r.get("outcome") == "acquired" for r in rows) and
                       any(r.get("outcome") == "blocked" for r in rows))
+                check("counter различает released и epoch-mismatch",
+                      any(r.get("event") == "release" and
+                          r.get("outcome") == "released" for r in rows) and
+                      any(r.get("event") == "release" and
+                          r.get("outcome") == "epoch-mismatch" for r in rows))
+            leaks = _production_counter_leaks(
+                production_counter, production_counter_before, root)
+            check("тест не пишет боевой usage-counter", not leaks,
+                  "test-attributed rows=%r; production bytes %d->%d" %
+                  (leaks[:3], production_counter_before,
+                   _file_size(production_counter)))
     finally:
         shutil.rmtree(root, ignore_errors=True)
 
@@ -165,5 +708,8 @@ if __name__ == "__main__":
     except Exception:
         pass
     if len(sys.argv) > 1 and sys.argv[1] == "--child":
-        sys.exit(_child(sys.argv[2], sys.argv[3], sys.argv[4], sys.argv[5], sys.argv[6]))
+        sys.exit(_child(sys.argv[2], sys.argv[3], sys.argv[4], sys.argv[5],
+                        sys.argv[6], sys.argv[7] if len(sys.argv) > 7 else ""))
+    if len(sys.argv) > 1 and sys.argv[1] == "--migration-child":
+        sys.exit(_migration_child(sys.argv[2], sys.argv[3], sys.argv[4]))
     sys.exit(main())
diff --git a/workspace_write_lease.py b/workspace_write_lease.py
index f0719abb3..876ce377f 100644
--- a/workspace_write_lease.py
+++ b/workspace_write_lease.py
@@ -8,9 +8,10 @@
     подписывает снапшоты) и не advisory `onair.py`.
 
 Вход/выход
-    Python API `acquire_many(paths, session, agent)` / `release_session(session)`;
+    Python API `acquire_many(..., epoch=turn_id)` / `release_session(..., epoch=turn_id)`;
     CLI `acquire|release-session|check|status|reap`. Успех rc=0, занято rc=7,
     ошибка аргументов rc=2. Состояние -- локальная SQLite DB под LOCALAPPDATA.
+    Вызов без epoch оставлен только для совместимости прямых legacy-потребителей.
 
 Кто дёргает
     `hooks/workspace_write_guard.py` из общего PreToolUse; `turnstate_hook.py`
@@ -21,18 +22,20 @@
     не лежит в Syncthing: это mutex одного узла. Между машинами остаётся onair/шина.
 
 Страховка
-    TTL хранится epoch UTC и чистится в той же транзакции до захвата. Упавшая
-    сессия не запирает файл навсегда; штатный Stop снимает лизу немедленно.
+    TTL хранится как Unix time и чистится в той же транзакции до захвата. Fencing
+    epoch не даёт запоздалому Stop старого turn_id снять новую лизу той же сессии.
+    Упавшая сессия не запирает файл навсегда; штатный Stop снимает точную эпоху.
 
 Счётчик
     `%LOCALAPPDATA%/AntonAgents/workspace-write-leases/usage.jsonl`; тесты обязаны
     перенаправлять его через WORKSPACE_WRITE_LEASE_COUNTER.
 
 Тест
-    `_test_workspace_write_lease.py`: 8 реальных процессов, red-first мутант,
-    parent/child, TTL/reaper, чужой release, CLI flags.
+    `_test_workspace_write_lease.py`: 8 API-процессов, 2 реальных CLI-писателя,
+    BUSY rc=7 + holder, TTL/fencing, чужой release, конкурентная миграция,
+    наивная модель и семь production-source мутантов.
 
-updated: 2026-09-11
+updated: 2026-09-21
 """
 from __future__ import annotations
 
@@ -171,6 +174,28 @@ def is_wide_root(path):
     return value in wide_roots()
 
 
+def _migrate_epoch(con):
+    """Add the fencing column once, even when many first-openers race.
+
+    The first PRAGMA is the cheap steady-state path.  A legacy database enters a
+    SQLite write transaction and then *rechecks* the schema after obtaining the
+    lock.  Without that second check, two processes can both observe the old
+    schema and the loser raises ``duplicate column name: epoch``.
+    """
+    columns = {str(row["name"]) for row in con.execute("PRAGMA table_info(leases)")}
+    if "epoch" in columns:
+        return
+    con.execute("BEGIN IMMEDIATE")
+    try:
+        columns = {str(row["name"]) for row in con.execute("PRAGMA table_info(leases)")}
+        if "epoch" not in columns:
+            con.execute("ALTER TABLE leases ADD COLUMN epoch TEXT NOT NULL DEFAULT ''")
+        con.commit()
+    except Exception:
+        con.rollback()
+        raise
+
+
 def _connect():
     path = db_path()
     os.makedirs(os.path.dirname(path), exist_ok=True)
@@ -185,16 +210,20 @@ def _connect():
         cwd TEXT,
         acquired REAL NOT NULL,
         expires REAL NOT NULL,
-        note TEXT
+        note TEXT,
+        epoch TEXT NOT NULL DEFAULT ''
     )""")
+    _migrate_epoch(con)
     con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_expires ON leases(expires)")
     con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_session ON leases(session)")
+    con.execute("CREATE INDEX IF NOT EXISTS ix_workspace_leases_owner "
+                "ON leases(session,epoch)")
     return con
 
 
 def _rows(con, now):
     return [dict(row) for row in con.execute(
-        "SELECT resource,session,agent,host,cwd,acquired,expires,note "
+        "SELECT resource,session,agent,host,cwd,acquired,expires,note,epoch "
         "FROM leases WHERE expires>? ORDER BY resource", (float(now),))]
 
 
@@ -205,12 +234,19 @@ class LeaseResult:
     conflicts: list[dict] = field(default_factory=list)
     reaped: int = 0
     reason: str = ""
+    epoch: str = ""
+
 
+def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, note="",
+                 now=None, epoch=None):
+    """Атомарно взять ВЕСЬ набор путей или ни одного (`BEGIN IMMEDIATE`).
 
-def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, note="", now=None):
-    """Атомарно взять ВЕСЬ набор путей или ни одного (`BEGIN IMMEDIATE`)."""
+    `epoch` -- fencing token одной попытки/turn. None сохраняет legacy-владение с
+    пустой эпохой; hooks всегда передают epoch явно, даже если он пустой.
+    """
     session = str(session or "").strip()
     agent = str(agent or "unknown").strip() or "unknown"
+    epoch = str(epoch or "").strip()
     if not session:
         raise ValueError("session is required")
     ttl_sec = int(ttl_sec)
@@ -229,7 +265,8 @@ def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, no
         conflicts = []
         for wanted in resources:
             for row in live:
-                if row["session"] != session and overlaps(wanted, row["resource"]):
+                same_owner = row["session"] == session and row.get("epoch", "") == epoch
+                if not same_owner and overlaps(wanted, row["resource"]):
                     item = dict(row)
                     item["wanted"] = wanted
                     conflicts.append(item)
@@ -239,49 +276,77 @@ def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, no
             # claim work that rollback silently undid.
             con.commit()
             count_event("acquire", "blocked", {"session": session, "agent": agent,
-                        "resources": resources, "held_by": sorted({c["session"] for c in conflicts})})
-            return LeaseResult(False, resources, conflicts, reaped, "busy")
+                        "epoch": epoch, "resources": resources,
+                        "held_by": sorted({c["session"] for c in conflicts}),
+                        "held_epochs": sorted({c.get("epoch", "") for c in conflicts})})
+            return LeaseResult(False, resources, conflicts, reaped, "busy", epoch)
         expiry = now + ttl_sec
         for resource in resources:
             own = next((r for r in live if r["resource"] == resource and
-                        r["session"] == session), None)
+                        r["session"] == session and r.get("epoch", "") == epoch), None)
             acquired = own["acquired"] if own else now
-            con.execute("""INSERT INTO leases(resource,session,agent,host,cwd,acquired,expires,note)
-                VALUES(?,?,?,?,?,?,?,?)
+            con.execute("""INSERT INTO leases(
+                    resource,session,agent,host,cwd,acquired,expires,note,epoch)
+                VALUES(?,?,?,?,?,?,?,?,?)
                 ON CONFLICT(resource) DO UPDATE SET
                   session=excluded.session, agent=excluded.agent, host=excluded.host,
                   cwd=excluded.cwd, acquired=excluded.acquired,
-                  expires=excluded.expires, note=excluded.note""",
+                  expires=excluded.expires, note=excluded.note, epoch=excluded.epoch""",
                 (resource, session, agent, host, norm_path(cwd) if cwd else "",
-                 acquired, expiry, str(note or "")))
+                 acquired, expiry, str(note or ""), epoch))
         con.commit()
         count_event("acquire", "acquired", {"session": session, "agent": agent,
-                    "resources": resources, "ttl_sec": ttl_sec, "reaped": reaped})
+                    "epoch": epoch, "resources": resources, "ttl_sec": ttl_sec,
+                    "reaped": reaped, "note": str(note or "")})
         return LeaseResult(True, resources, [], reaped, "own" if any(
-            r["session"] == session for r in live) else "new")
+            r["session"] == session and r.get("epoch", "") == epoch for r in live)
+            else "new", epoch)
     except Exception:
         try:
             con.rollback()
         except Exception:
             pass
-        count_event("acquire", "error", {"session": session, "agent": agent})
+        count_event("acquire", "error", {"session": session, "agent": agent,
+                    "epoch": epoch})
         raise
     finally:
         con.close()
 
 
-def release_session(session):
+def release_session(session, *, epoch=None):
+    """Release one fenced epoch; `epoch=None` means the legacy empty epoch.
+
+    Hooks must pass an explicit epoch (possibly ``""`` for a legacy harness).
+    Mapping None to ``""`` preserves non-hook callers such as the skill bridge
+    without giving them a broad delete that could remove a tokened hook lease.
+    During the one-time schema handoff, a token-aware Stop may encounter only the
+    preserved empty-epoch row created by the old engine. If no exact token exists,
+    that same-session legacy row is released; a non-empty newer epoch is never touched.
+    """
     session = str(session or "").strip()
     if not session:
         return 0
+    exact_epoch = str(epoch or "").strip()
     con = _connect()
     try:
         con.execute("BEGIN IMMEDIATE")
-        n = con.execute("DELETE FROM leases WHERE session=?", (session,)).rowcount
+        n = con.execute("DELETE FROM leases WHERE session=? AND epoch=?",
+                        (session, exact_epoch)).rowcount
+        legacy_handoff = 0
+        if not n and epoch is not None and exact_epoch:
+            legacy_handoff = con.execute(
+                "DELETE FROM leases WHERE session=? AND epoch=''", (session,)).rowcount
+            n += legacy_handoff
+        mismatch = not n and bool(con.execute(
+            "SELECT 1 FROM leases WHERE session=? LIMIT 1", (session,)).fetchone())
         con.commit()
     finally:
         con.close()
-    count_event("release", "released" if n else "absent", {"session": session, "count": n})
+    outcome = "released" if n else ("epoch-mismatch" if mismatch else "absent")
+    count_event("release", outcome, {"session": session, "epoch": exact_epoch,
+                "scope": ("legacy-empty" if epoch is None else
+                          "fenced+legacy-handoff" if legacy_handoff else "fenced"),
+                "count": n})
     return n
 
 
@@ -343,8 +408,12 @@ def main(argv=None):
     acq.add_argument("--cwd", default=None)
     acq.add_argument("--ttl-sec", type=int, default=DEFAULT_TTL_SEC)
     acq.add_argument("--note", default="")
+    acq.add_argument("--epoch", default=None,
+                     help="fencing token/turn_id; omit only for legacy callers")
     rel = sub.add_parser("release-session", help="снять все свои пути")
     rel.add_argument("--session", required=True)
+    rel.add_argument("--epoch", default=None,
+                     help="release only this fencing token; omitted = legacy empty epoch")
     chk = sub.add_parser("check", help="кто держит путь")
     chk.add_argument("path")
     chk.add_argument("--cwd", default=None)
@@ -354,7 +423,7 @@ def main(argv=None):
     args = ap.parse_args(argv)
     if args.command == "acquire":
         result = acquire_many(args.paths, args.session, args.agent, args.ttl_sec,
-                              cwd=args.cwd, note=args.note)
+                              cwd=args.cwd, note=args.note, epoch=args.epoch)
         if result.ok:
             print("ACQUIRED %d path(s) by %s" % (len(result.resources), args.session))
             return 0
@@ -362,7 +431,7 @@ def main(argv=None):
         print("BUSY: held by %s" % owners)
         return 7
     if args.command == "release-session":
-        print("RELEASED %d" % release_session(args.session))
+        print("RELEASED %d" % release_session(args.session, epoch=args.epoch))
         return 0
     if args.command == "check":
         row = owner_of(args.path, cwd=args.cwd)
--- SCRIPTS DIFF END ---
--- HOOKS DIFF START ---diff --git a/constitution_guard.py b/constitution_guard.py
index 0b454c3..a90ea51 100644
--- a/constitution_guard.py
+++ b/constitution_guard.py
@@ -19,7 +19,8 @@ from __future__ import annotations
 import json, os, sys, time
 from pathlib import Path
 
-LOG = Path(os.path.expanduser(r"~\.claude\hooks\_constitution_guard.log"))
+LOG = Path(os.environ.get("CONSTITUTION_GUARD_LOG") or
+           os.path.expanduser(r"~\.claude\hooks\_constitution_guard.log"))
 
 # Protected = the constitution codex + the vault git internals. Substring match on the
 # resolved path, case-insensitive. EXTEND this list as the constitution grows.
diff --git a/turnstate_hook.py b/turnstate_hook.py
index 8b9852c..a68bcf0 100644
--- a/turnstate_hook.py
+++ b/turnstate_hook.py
@@ -76,20 +76,23 @@ FILE_TOOLS = {"Write", "Edit", "MultiEdit", "NotebookEdit"}
 
 
 def release_workspace_write_lease(data):
-    """Stop/UserPromptSubmit boundary: hand the files to the next agent immediately.
+    """Stop/UserPromptSubmit boundary: release only this turn's fenced epoch.
 
     TTL remains the crash reaper, but a healthy turn must not make Claude or Codex wait.
-    This runs before transcript checks because Codex Stop can omit transcript_path.
+    Codex supplies turn_id on PreToolUse and Stop; matching it prevents a delayed old
+    Stop from deleting the next turn's lease. Claude currently uses explicit legacy
+    epoch "". This runs before transcript checks because Stop can omit transcript_path.
     """
     try:
-        scripts = os.path.join(os.path.expanduser("~"), ".claude", "scripts")
+        scripts = os.environ.get("WORKSPACE_WRITE_LEASE_MODULE_DIR") or os.path.join(
+            os.path.expanduser("~"), ".claude", "scripts")
         if scripts not in sys.path:
             sys.path.insert(0, scripts)
         import workspace_write_lease
-        from workspace_write_guard import session_id
+        from workspace_write_guard import lease_epoch, session_id
         sid = session_id(data)
         if sid:
-            workspace_write_lease.release_session(sid)
+            workspace_write_lease.release_session(sid, epoch=lease_epoch(data))
     except Exception:
         pass
 
diff --git a/workspace_write_guard.py b/workspace_write_guard.py
index 1ac31b5..2b8482b 100644
--- a/workspace_write_guard.py
+++ b/workspace_write_guard.py
@@ -15,15 +15,20 @@ reports canonical `apply_patch`; Claude reports Write/Edit/MultiEdit/NotebookEdi
 одну правку в получасовой замок на всю папку. Замер 14.09 после половинчатой утренней
 правки: 198 блокировок, 137 (69%) -- запрос ПАПКИ, 86 из них `~/.claude/scripts`,
 36 пострадавших сессий, включая ЧТЕНИЕ файла и `cd`, который запирал сессию насмерть.
-Честная дыра: запись по ОТНОСИТЕЛЬНОМУ пути из скрипта (`python build.py`) не ловится.
-Её не ловили и раньше -- при контейнерной cwd, то есть в обычном случае.
-
-Input: hook JSON on stdin. Output: silence on allow; stderr + rc=2 on deny.
+Честные дыры: shell-команда с относительной целью (`Set-Content ./x`) не ловится,
+потому что guard извлекает только названные абсолютные пути; файл, который скрыто
+пишет дочерний скрипт (`python build.py`), тем более не виден. Межмашинной защиты
+здесь нет: SQLite -- mutex только этого узла; между машинами остаются
+On Air/шина/worktree ownership. Извлечение абсолютного пути здесь Windows-only
+(`C:\\...`); перенос этого hook на Unix без отдельного path-parser не защищает `/tmp/...`.
+
+Input: hook JSON on stdin. Output: silence on allow; Claude deny is stderr + rc=2,
+while Codex payloads with turn/tool ids receive structured deny on stdout + rc=0.
 Caller: trusted `constitution_guard.cmd` (PreToolUse) and `turnstate_hook.py` (Stop).
 Rail: local Python + `scripts/workspace_write_lease.py`, 0 LLM, 0 network.
-Test: `_test_lease_storm.py` (класс), `_test_codex_shared_workspace_safety.py`,
+Test: `_test_lease_storm.py` (класс), `_test_workspace_write_guard.py`,
 `_test_workspace_write_lease.py`.
-updated: 2026-09-14
+updated: 2026-09-21
 """
 from __future__ import annotations
 
@@ -35,7 +40,8 @@ import sys
 from dataclasses import dataclass, field
 from pathlib import Path
 
-SCRIPTS = os.path.join(os.path.expanduser("~"), ".claude", "scripts")
+SCRIPTS = os.environ.get("WORKSPACE_WRITE_LEASE_MODULE_DIR") or os.path.join(
+    os.path.expanduser("~"), ".claude", "scripts")
 if SCRIPTS not in sys.path:
     sys.path.insert(0, SCRIPTS)
 import workspace_write_lease as lease  # noqa: E402
@@ -50,6 +56,14 @@ SHELL_MUTATION = re.compile(
     r"copy-item|rename-item|clear-content|tee-object|tee|rm|del|erase|mv|cp|touch|"
     r"truncate)\b|\bsed\s+-[^\r\n]*i\b|\bperl\s+-[^\r\n]*p?i\b|"
     r"\bgit\s+apply\b|(?:^|\s)patch(?:\s|$)|(?<![<>])>{1,2}(?![>&]))")
+CHILD_SHELL_AT_START = re.compile(
+    r"(?is)^\s*&?\s*(?:"
+    r'"(?:[^"\r\n]*[\\/])?(?P<shell_dq>powershell|pwsh|cmd|sh|bash)(?:\.exe)?"|'
+    r"'(?:[^'\r\n]*[\\/])?(?P<shell_sq>powershell|pwsh|cmd|sh|bash)(?:\.exe)?'|"
+    r"(?:\S*[\\/])?(?P<shell_bare>powershell|pwsh|cmd|sh|bash)(?:\.exe)?"
+    r")\s+(?P<args>.*)$")
+NULL_REDIRECTION = re.compile(
+    r"(?i)(?<!\S)(?:\d|\*)?>\s*(?:\$null\b|nul\b|/dev/null\b)")
 ABS_QUOTED = re.compile(r"[\"']([A-Za-z]:[\\/][^\"'\r\n]+)[\"']")
 ABS_BARE = re.compile(r"(?<![\w])([A-Za-z]:[\\/][^\s\"'|&;<>]+)")
 SEGMENT_SPLIT = re.compile(r"\|\||&&|[;|\r\n]")
@@ -93,18 +107,31 @@ def tool_name(payload):
     return str(payload.get("tool_name") or payload.get("tool") or "").strip()
 
 
+def canonical_session_id(value):
+    """Collapse Codex runtime aliases so PreToolUse and Stop name one owner."""
+    value = str(value or "").strip()
+    while value.lower().startswith("agent/"):
+        value = value[6:].strip()
+    return value
+
+
 def session_id(payload):
     for key in ("session_id", "thread_id", "conversation_id"):
-        value = str(payload.get(key) or "").strip()
+        value = canonical_session_id(payload.get(key))
         if value:
             return value
     for key in ("CODEX_THREAD_ID", "CLAUDE_CODE_SESSION_ID", "CLAUDE_SESSION_ID"):
-        value = str(os.environ.get(key) or "").strip()
+        value = canonical_session_id(os.environ.get(key))
         if value:
             return value
     return ""
 
 
+def lease_epoch(payload):
+    """Codex turn_id is the fencing token; other harnesses use legacy epoch ""."""
+    return str(payload.get("turn_id") or "").strip()
+
+
 def agent_name(payload):
     explicit = str(payload.get("agent") or payload.get("agent_name") or "").strip()
     if explicit:
@@ -129,6 +156,197 @@ def _safe_resolve(value, cwd):
         return ""
 
 
+def _top_level_segments(command, dialect="powershell"):
+    """Split control operators with the quoting rules of the executing shell."""
+    out, start, quote = [], 0, ""
+    command = str(command or "")
+    index = 0
+    while index < len(command):
+        char = command[index]
+        if quote:
+            if dialect == "powershell" and char == "`" and index + 1 < len(command):
+                index += 2
+                continue
+            if (dialect == "powershell" and quote == "'" and char == "'" and
+                    index + 1 < len(command) and command[index + 1] == "'"):
+                index += 2
+                continue
+            if (dialect == "posix" and quote == '"' and char == "\\" and
+                    index + 1 < len(command)):
+                index += 2
+                continue
+            if dialect == "cmd" and char == "^" and index + 1 < len(command):
+                index += 2
+                continue
+            if char == quote:
+                quote = ""
+            index += 1
+            continue
+        if ((dialect == "powershell" and char == "`") or
+                (dialect == "posix" and char == "\\") or
+                (dialect == "cmd" and char == "^")):
+            index += 2 if index + 1 < len(command) else 1
+            continue
+        if char in ("'", '"'):
+            quote = char
+            index += 1
+            continue
+        width = 0
+        if char in ";|\r\n":
+            width = 1
+        elif char == "&" and index + 1 < len(command) and command[index + 1] == "&":
+            width = 2
+        elif char == "&" and command[start:index].strip():
+            # cmd.exe / PowerShell chain separator. A leading `& 'tool'` is instead
+            # PowerShell's call operator and stays in this segment.
+            width = 1
+        if width:
+            if command[start:index].strip():
+                out.append(command[start:index].strip())
+            start = index + width
+            index += width
+            continue
+        index += 1
+    if command[start:].strip():
+        out.append(command[start:].strip())
+    return out
+
+
+def _shell_args(value, dialect="powershell"):
+    """Tokenize enough shell syntax to retain quoted bodies and option values."""
+    value = str(value or "")
+    out, token, quote, quoted = [], [], "", False
+    index = 0
+    while index < len(value):
+        char = value[index]
+        if quote:
+            if dialect == "powershell" and char == "`" and index + 1 < len(value):
+                token.append(value[index + 1])
+                index += 2
+                continue
+            if (dialect == "powershell" and quote == "'" and char == "'" and
+                    index + 1 < len(value) and value[index + 1] == "'"):
+                token.append("'")
+                index += 2
+                continue
+            if (dialect == "posix" and quote == '"' and char == "\\" and
+                    index + 1 < len(value)):
+                token.append(value[index + 1])
+                index += 2
+                continue
+            if dialect == "cmd" and char == "^" and index + 1 < len(value):
+                token.append(value[index + 1])
+                index += 2
+                continue
+            if char == quote:
+                quote = ""
+            else:
+                token.append(char)
+            index += 1
+            continue
+        if char.isspace():
+            if token or quoted:
+                out.append(("".join(token), quoted))
+                token, quoted = [], False
+            index += 1
+            continue
+        if char in ("'", '"'):
+            quote, quoted = char, True
+            index += 1
+            continue
+        if ((dialect == "powershell" and char == "`") or
+                (dialect == "posix" and char == "\\") or
+                (dialect == "cmd" and char == "^")) and index + 1 < len(value):
+            token.append(value[index + 1])
+            index += 2
+            continue
+        token.append(char)
+        index += 1
+    if token or quoted:
+        out.append(("".join(token), quoted))
+    return out
+
+
+def _mask_quoted_literals(value, dialect="powershell"):
+    """Blank data literals without applying Bash backslash rules to PowerShell."""
+    value = str(value or "")
+    out, quote, index = [], "", 0
+    while index < len(value):
+        char = value[index]
+        if quote:
+            if dialect == "powershell" and char == "`" and index + 1 < len(value):
+                index += 2
+                continue
+            if (dialect == "powershell" and quote == "'" and char == "'" and
+                    index + 1 < len(value) and value[index + 1] == "'"):
+                index += 2
+                continue
+            if (dialect == "posix" and quote == '"' and char == "\\" and
+                    index + 1 < len(value)):
+                index += 2
+                continue
+            if dialect == "cmd" and char == "^" and index + 1 < len(value):
+                index += 2
+                continue
+            if char == quote:
+                quote = ""
+            index += 1
+            continue
+        if char in ("'", '"'):
+            quote = char
+            out.append("''")
+            index += 1
+            continue
+        out.append(char)
+        index += 1
+    return "".join(out)
+
+
+def _child_command_bodies(command, dialect="powershell"):
+    for segment in _top_level_segments(command, dialect):
+        match = CHILD_SHELL_AT_START.match(segment)
+        if not match:
+            continue
+        shell = next(value for value in (
+            match.group("shell_dq"), match.group("shell_sq"),
+            match.group("shell_bare")) if value).lower()
+        args = _shell_args(match.group("args"), dialect)
+        for index, (value, _quoted) in enumerate(args):
+            flag = value.lower()
+            valid = ((shell in {"powershell", "pwsh"} and
+                      flag in {"-command", "-commandwithargs", "-c"}) or
+                     (shell == "cmd" and flag == "/c") or
+                     (shell in {"sh", "bash"} and
+                      bool(re.fullmatch(r"-[a-z]*c[a-z]*", flag))))
+            if valid and index + 1 < len(args) and args[index + 1][1]:
+                child_dialect = ("powershell" if shell in {"powershell", "pwsh"}
+                                 else "cmd" if shell == "cmd" else "posix")
+                yield args[index + 1][0], child_dialect
+                break
+
+
+def shell_scan_text(command, _depth=0, dialect="powershell"):
+    """Syntax outside data literals, plus quoted ``-Command``/``/c`` bodies.
+
+    A quoted grep pattern such as ``'<input>'`` is data, not redirection.  In
+    contrast, the quoted body passed to another shell is executable syntax and
+    must remain visible (``powershell -Command "Set-Content ..."``).
+    """
+    command = str(command or "")
+    child_scans = []
+    if _depth < 2:
+        for body, child_dialect in _child_command_bodies(command, dialect):
+            child_scans.append(shell_scan_text(body, _depth + 1, child_dialect))
+    call_targets = []
+    for segment in _top_level_segments(command, dialect):
+        tokens = _shell_args(segment, dialect)
+        if len(tokens) >= 2 and tokens[0][0] == "&" and tokens[1][1]:
+            call_targets.append(tokens[1][0])
+    unquoted = _mask_quoted_literals(command, dialect)
+    combined = "\n".join([unquoted] + child_scans + call_targets)
+    return NULL_REDIRECTION.sub(" ", combined)
+
+
 def shell_is_read_only(command):
     """Читающая команда лизы НЕ берёт -- ни на файл, ни тем более на папку.
 
@@ -141,10 +359,11 @@ def shell_is_read_only(command):
     command = str(command or "").strip()
     if not command:
         return True
-    if (SHELL_MUTATION.search(command) or
-            re.search(r"(?i)(?:^|\s)--output(?:=|\s)", command)):
+    scan = shell_scan_text(command)
+    if (SHELL_MUTATION.search(scan) or
+            re.search(r"(?i)(?:^|\s)--output(?:=|\s)", scan)):
         return False
-    stages = [stage.strip() for stage in SEGMENT_SPLIT.split(command) if stage.strip()]
+    stages = [stage.strip() for stage in SEGMENT_SPLIT.split(scan) if stage.strip()]
     return bool(stages) and all(READ_ONLY_COMMAND.match(stage) for stage in stages)
 
 
@@ -163,9 +382,10 @@ def executable_tokens(command):
     интерпретатора снимаем ещё и первый нефлаговый аргумент. Цель записи (`log`) остаётся.
     """
     out = set()
-    for segment in SEGMENT_SPLIT.split(str(command or "")):
-        tokens = re.findall(r"\"([^\"]+)\"|'([^']+)'|(\S+)", segment.strip())
-        tokens = [next(g for g in t if g) for t in tokens]
+    for segment in _top_level_segments(command):
+        tokens = [value for value, _quoted in _shell_args(segment)]
+        if tokens and tokens[0] == "&":
+            tokens = tokens[1:]
         if not tokens:
             continue
         out.add(tokens[0])
@@ -211,7 +431,7 @@ def extract_intent(payload):
         # флота: сессия, правящая ОДИН скрипт, запирала все остальные на 30 минут.
         # Новый контракт в одну строку: shell лизует ТОЛЬКО файлы, которые НАЗЫВАЕТ, и только
         # когда ВИДИМО пишет. cwd не лизуется никогда -- ни широкая, ни узкая.
-        if not SHELL_MUTATION.search(command):
+        if not SHELL_MUTATION.search(shell_scan_text(command)):
             # Не читающая (словарь не признал), но и признака записи нет: `python build.py`,
             # `node x.js`, heredoc. Лизовать нечего -- цели записи в тексте команды нет.
             # Честная дыра: такая команда может писать по относительному пути, и мы её не
@@ -255,24 +475,32 @@ def guard_pre(payload):
         lease.count_event("hook", "blocked-no-session", {"tool": tool_name(payload)})
         return Decision(False, "write hook has no session_id; cannot own a lease", intent.paths)
     try:
+        epoch = lease_epoch(payload)
         result = lease.acquire_many(intent.paths, sid, agent_name(payload),
                                     cwd=str(payload.get("cwd") or ""),
-                                    note="PreToolUse %s" % tool_name(payload))
+                                    note="PreToolUse %s" % tool_name(payload),
+                                    epoch=epoch)
     except Exception as exc:
         lease.count_event("hook", "blocked-error", {"tool": tool_name(payload),
                           "session": sid, "error": type(exc).__name__})
         return Decision(False, "lease engine failed: %s" % type(exc).__name__, intent.paths)
     if result.ok:
+        lease.count_event("hook", "acquired", {"tool": tool_name(payload),
+                          "session": sid, "epoch": epoch,
+                          "resources": intent.paths})
         return Decision(True, "lease acquired", intent.paths)
     owners = sorted({str(row.get("session") or "?") for row in result.conflicts})
     held = sorted({str(row.get("resource") or "?") for row in result.conflicts})
+    lease.count_event("hook", "blocked", {"tool": tool_name(payload),
+                      "session": sid, "epoch": epoch, "resources": intent.paths,
+                      "held_by": owners})
     return Decision(False, "BUSY: %s held by %s" % (", ".join(held), ", ".join(owners)),
                     intent.paths)
 
 
 def release_payload(payload):
     sid = session_id(payload)
-    return lease.release_session(sid) if sid else 0
+    return lease.release_session(sid, epoch=lease_epoch(payload)) if sid else 0
 
 
 def emit_codex_deny(payload, reason):
--- HOOKS DIFF END ---

---

**Claude:**

SUMMARY: A large, well-engineered diff adding fencing-epoch semantics to the workspace write lease plus a much stronger integration test suite (real CLI contention, live hooks.json execution, concurrent schema migration, and multiple production-source mutants with self-verifying string matches). The core atomic-acquire/BUSY/fencing logic looks correct and is genuinely exercised, but the "legacy migration handoff" fallback in `release_session` is a standing (not migration-scoped) broad-delete path that can consume the wrong lease.

FINDINGS:
- workspace_write_lease.py:~(release_session, legacy_handoff block) | MED | `release_session(session, epoch=<real-token>)` falls back to `DELETE FROM leases WHERE session=? AND epoch=''` whenever the exact `(session, epoch)` match misses. The docstring frames this as a "one-time schema handoff," but nothing in the code scopes it to migration time — it runs on every release call, forever. Any caller that legitimately holds a lease under the legacy empty epoch (the code's own comment names "the skill bridge" as such a caller) can have that lease silently stolen/released by an unrelated tokened Stop for a session string that happens to match, even long after migration is complete. The test suite proves the intended forward case (`_old_schema_migrates`) and proves the *other* direction is safe (`release_session(session)` without a token can't touch a tokened lease), but never tests the reverse risk this asymmetric fallback introduces (a tokened release wiping a live, non-stale empty-epoch lease of a different logical owner sharing the session string). Fix: gate the handoff to true migration state (e.g., only when the row's `acquired` timestamp predates the epoch column's introduction, or drop the fallback once a companion "migration complete" marker is set) rather than leaving it as a permanent wildcard match on `epoch=''`.
- _test_workspace_write_guard.py:_codex_pretool_contract | LOW | The contract requires all of `{apply_patch, Bash, PowerShell, exec_command, shell}` to appear in a single hook-entry's matcher (pipe-joined). If the live `hooks.json` is ever reorganized into multiple `PreToolUse` entries that jointly cover the same tools (functionally equivalent, arguably cleaner config), this check and its "mutation: each shell matcher must go red" companion would both fail even though wiring is intact — a maintainability trap, not a wiring bug today.
- _test_codex_shared_workspace_safety.py (deleted) | LOW | The old check "r1/.agents не содержит активных копий SKILL.md" (skill-duplication regression guard) was dropped along with the file rename/rewrite, with no replacement or note. Unrelated to workspace-lease safety, but it's a silent coverage loss that should at least be acknowledged or relocated.

===VERDICT=== REQUEST_CHANGES