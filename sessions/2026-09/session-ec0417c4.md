**Антон:**

You are an independent adversarial reviewer. Review ONLY these immutable commits and do not edit files:
- scripts e98a662cbb0d92e95dd528a19617e89c1d437db1
- hooks d23e6c57d67ab6133bc2fa305306341affc93779

Acceptance: local Windows mutex for Claude/Codex physical absolute file targets; exactly one winner under concurrency; loser BUSY rc=7 with holder; foreign release cannot remove; delayed old turn release cannot remove new epoch; legacy-schema migration is concurrent-safe and distinguishes migrated rows from fresh empty-epoch leases; Codex aliases normalize; hooks cover apply_patch plus Bash/PowerShell/exec_command/shell; quoted child shells, env prefixes, PowerShell accepted Command prefixes/slash form, and outer-shell dialects do not bypass or false-block; cwd/executable lease-storm stays fixed. Tests must be isolated, mutate production-source/config semantics, and keep counters/audit isolated. Honest non-goals: local-only; physical paths only; relative targets and hidden child-script writes remain gaps; no role/question authorization.

Try to disprove the claims from code, especially transaction semantics, migration handoff, release fencing, parser escaping/wrappers, hook structured-deny contract, and whether tests would fail on broken variants. Distinguish actionable defects from out-of-scope limits. Respond exactly:
SUMMARY: ...
FINDINGS:
- file:line | severity | evidence and required fix
(or '- none')
VERDICT: APPROVE or REQUEST_CHANGES

=== SCRIPTS COMMIT ===
commit e98a662cbb0d92e95dd528a19617e89c1d437db1
Author:     Claude Config Snapshot (HUB-01) <claude-config@HUB-01.local>
AuthorDate: Mon Sep 21 07:16:30 2026 +0100
Commit:     claude-? <claude+?@local>
CommitDate: Mon Sep 21 08:27:16 2026 +0100

    fix: fence workspace write leases by turn
    
    Assisted-by: Codex CLI / GPT-5.6
    
    Machine: HUB-01
    
    Account: bb
    
    Operator: Anton
---
 _test_codex_shared_workspace_safety.py | 273 ----------
 _test_lease_storm.py                   |  12 +-
 _test_workspace_write_guard.py         | 894 +++++++++++++++++++++++++++++++++
 _test_workspace_write_lease.py         | 677 +++++++++++++++++++++++--
 workspace_write_lease.py               | 139 ++++-
 5 files changed, 1661 insertions(+), 334 deletions(-)

diff --git a/_test_codex_shared_workspace_safety.py b/_test_codex_shared_workspace_safety.py
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
diff --git a/_test_lease_storm.py b/_test_lease_storm.py
index b2ff6e02b..1c75bda20 100644
--- a/_test_lease_storm.py
+++ b/_test_lease_storm.py
@@ -33,7 +33,7 @@
      проверка 1 обязана ОТБИТЬСЯ. Тест, который не краснеет на сломанном коде, фальшивый.
 
 РЕЛЬСА: 0 LLM, 0 сети, stdlib. Гоняет реальный hooks/workspace_write_guard.py через stdin-контракт.
-updated: 2026-09-14
+updated: 2026-09-21
 """
 import json
 import os
@@ -41,7 +41,9 @@ import subprocess
 import sys
 import tempfile
 
-HOOK = os.path.join(os.path.expanduser("~"), ".claude", "hooks", "workspace_write_guard.py")
+HOOKS = os.environ.get("WORKSPACE_LEASE_TEST_HOOKS") or os.path.join(
+    os.path.expanduser("~"), ".claude", "hooks")
+HOOK = os.path.join(HOOKS, "workspace_write_guard.py")
 SCRIPTS = os.path.dirname(os.path.abspath(__file__))
 sys.path.insert(0, SCRIPTS)
 import workspace_write_lease as lease  # noqa: E402
@@ -104,6 +106,7 @@ def main():
     base = dict(os.environ,
                 WORKSPACE_WRITE_LEASE_DB=os.path.join(tmp, "leases.sqlite3"),
                 WORKSPACE_WRITE_LEASE_COUNTER=os.path.join(tmp, "usage.jsonl"),
+                WORKSPACE_WRITE_LEASE_MODULE_DIR=SCRIPTS,
                 WORKSPACE_WIDE_ROOTS=container)
     os.environ.update({k: base[k] for k in
                        ("WORKSPACE_WRITE_LEASE_DB", "WORKSPACE_WRITE_LEASE_COUNTER")})
@@ -179,4 +182,9 @@ def main():
 
 
 if __name__ == "__main__":
+    try:
+        sys.stdout.reconfigure(encoding="utf-8")
+        sys.stderr.reconfigure(encoding="utf-8")
+    except Exception:
+        pass
     sys.exit(main())
diff --git a/_test_workspace_write_guard.py b/_test_workspace_write_guard.py
new file mode 100644
index 000000000..6a5299c57
--- /dev/null
+++ b/_test_workspace_write_guard.py
@@ -0,0 +1,894 @@
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
+- ignore PowerShell's accepted ``-Comm``/``/Command`` abbreviations ->
+  ``PowerShell abbreviated/slash Command блокируются holder``.
+- assume PowerShell quoting for a canonical Bash tool ->
+  ``Bash escaped-quote data не становится ложным writer``.
+- stop child-shell discovery at ``NAME=value``/``env NAME=value`` ->
+  ``env-prefixed bash child writers блокируются holder``.
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
+    covered = set()
+    for matcher, command in commands:
+        tokens = {part.strip() for part in matcher.split("|") if part.strip()}
+        if "constitution_guard" in command:
+            covered.update(tokens)
+    return required.issubset(covered)
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
+            assigned_bash = _run_guard({
+                "session_id": "assigned-bash", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'FOO=bar bash -c "rm \'%s\'"' % quoted_target}}, env=env)
+            env_wrapped_bash = _run_guard({
+                "session_id": "env-wrapped-bash", "cwd": root, "tool_name": "Bash",
+                "tool_input": {"command":
+                    'env FOO=bar bash -c "rm \'%s\'"' % quoted_target}}, env=env)
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
+            abbreviated_command = _run_guard({
+                "session_id": "abbreviated-command", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'powershell -NoProfile -Comm '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            slash_command = _run_guard({
+                "session_id": "slash-command", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'powershell /Command '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            pwsh_abbreviated = _run_guard({
+                "session_id": "pwsh-abbreviated", "cwd": root,
+                "tool_name": "PowerShell",
+                "tool_input": {"command":
+                    'pwsh -Comm '
+                    '"Set-Content -LiteralPath \'%s\' -Value y"' % quoted_target}},
+                env=env)
+            bash_escaped_data = _run_guard({
+                "session_id": "bash-escaped-data", "cwd": root,
+                "tool_name": "Bash",
+                "tool_input": {"command":
+                    'printf \'%s\\n\' "needle\\\"; rm %s"' %
+                    ("%s", quoted_target)}}, env=env)
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
+            check("env-prefixed bash child writers блокируются holder",
+                  assigned_bash.returncode == 2 and
+                  "quoted-holder" in assigned_bash.stderr and
+                  env_wrapped_bash.returncode == 2 and
+                  "quoted-holder" in env_wrapped_bash.stderr,
+                  "assigned=%s/%s env=%s/%s" %
+                  (assigned_bash.returncode, assigned_bash.stderr[:100],
+                   env_wrapped_bash.returncode, env_wrapped_bash.stderr[:100]))
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
+            abbreviated_variants = [
+                ("powershell--Comm", abbreviated_command),
+                ("powershell-/Command", slash_command),
+                ("pwsh--Comm", pwsh_abbreviated),
+            ]
+            check("PowerShell abbreviated/slash Command блокируются holder",
+                  all(run.returncode == 2 and "quoted-holder" in run.stderr
+                      for _name, run in abbreviated_variants),
+                  [(name, run.returncode, run.stderr[:100])
+                   for name, run in abbreviated_variants])
+            check("Bash escaped-quote data не становится ложным writer",
+                  bash_escaped_data.returncode == 0,
+                  "rc=%s stderr=%s" %
+                  (bash_escaped_data.returncode, bash_escaped_data.stderr[:160]))
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
index cb6ffe73f..a3fa45e75 100644
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
@@ -63,26 +101,390 @@ def _child(mode, root, start, holder, target):
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
+               "post-migration", "migration-mutant", "reused-session",
+               "pre-migration", "broad-legacy"]
+    return [line for line in suffix.splitlines()
+            if any(marker in line.lower() for marker in markers)]
+
+
+def _create_legacy_db(lease, path, preserved, *additional):
+    con = sqlite3.connect(path)
+    try:
+        con.execute("""CREATE TABLE leases(
+            resource TEXT PRIMARY KEY, session TEXT NOT NULL, agent TEXT NOT NULL,
+            host TEXT NOT NULL, cwd TEXT, acquired REAL NOT NULL,
+            expires REAL NOT NULL, note TEXT)""")
+        for item in (preserved,) + additional:
+            con.execute("INSERT INTO leases VALUES(?,?,?,?,?,?,?,?)",
+                        (lease.norm_path(item), "pre-migration", "legacy", "host",
+                         "", 100.0, 9999999999.0, "keep"))
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
+    marker = getattr(lease, "LEGACY_MIGRATED_EPOCH", None)
+    if "epoch" not in columns or not marker or preserved != ("pre-migration", marker):
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
+    guarded = '                same_owner = _same_owner(row, session, epoch)'
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
+               "        if epoch is not None:\n"
+               "            legacy_handoff = con.execute(\n"
+               "                \"DELETE FROM leases WHERE session=? AND epoch=?\",\n"
+               "                (session, LEGACY_MIGRATED_EPOCH)).rowcount\n"
+               "            n += legacy_handoff\n")
+    broken = "        legacy_handoff = 0\n"
+    if source.count(guarded) != 1:
+        raise AssertionError("legacy handoff mutation did not match exactly once")
+    with open(destination, "w", encoding="utf-8", newline="\n") as fh:
+        fh.write(source.replace(guarded, broken, 1))
+    return destination
+
+
+def _broad_legacy_delete_mutant(source_file, destination):
+    """Create a copy where a delayed token can erase a fresh legacy lease."""
+    with open(source_file, encoding="utf-8") as fh:
+        source = fh.read()
+    guarded = ('                "DELETE FROM leases WHERE session=? AND epoch=?",\n'
+               '                (session, LEGACY_MIGRATED_EPOCH)).rowcount')
+    broken = ('                "DELETE FROM leases WHERE session=? AND epoch=\'\'",\n'
+              '                (session,)).rowcount')
+    if source.count(guarded) != 1:
+        raise AssertionError("migration-marker delete mutation did not match exactly once")
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
+    preserved_path = os.path.join(root, "preserved.md")
+    handoff_path = os.path.join(root, "handoff.md")
+    _create_legacy_db(lease, legacy_db, preserved_path, handoff_path)
+    os.environ["WORKSPACE_WRITE_LEASE_DB"] = legacy_db
+    try:
+        before = lease.owner_of(preserved_path)
+        before_handoff = lease.owner_of(handoff_path)
+        adopted = lease.acquire_many([preserved_path], "pre-migration", "test", 60,
+                                     epoch="turn-after-upgrade")
+        adopted_owner = lease.owner_of(preserved_path)
+        new_path = os.path.join(root, "new.md")
+        acquired = lease.acquire_many([new_path], "pre-migration", "test", 60,
+                                      epoch="turn-after-upgrade")
+        con = sqlite3.connect(legacy_db)
+        try:
+            columns = {row[1] for row in con.execute("PRAGMA table_info(leases)")}
+        finally:
+            con.close()
+        released = lease.release_session("pre-migration", epoch="turn-after-upgrade")
+        after_release = lease.owner_of(preserved_path)
+        after_handoff = lease.owner_of(handoff_path)
+        after_new = lease.owner_of(new_path)
+        marker = getattr(lease, "LEGACY_MIGRATED_EPOCH", None)
+        return bool(marker and before and before.get("epoch") == marker and
+                    before_handoff and before_handoff.get("epoch") == marker and
+                    before.get("session") == "pre-migration" and
+                    adopted.ok and adopted_owner and
+                    adopted_owner.get("epoch") == "turn-after-upgrade" and
+                    acquired.ok and "epoch" in columns and released == 3 and
+                    after_release is None and after_handoff is None and
+                    after_new is None)
+    finally:
+        os.environ["WORKSPACE_WRITE_LEASE_DB"] = original
+
+
+def _delayed_token_preserves_fresh_legacy(lease, target):
+    """A stale token must not erase an empty-epoch lease created after migration."""
+    lease.release_all_for_tests()
+    old = lease.acquire_many([target], "reused-session", "hook", 60,
+                             epoch="turn-old")
+    exact = lease.release_session("reused-session", epoch="turn-old")
+    fresh = lease.acquire_many([target], "reused-session", "legacy-client", 60)
+    delayed = lease.release_session("reused-session", epoch="turn-old")
+    owner = lease.owner_of(target)
+    cleanup = lease.release_session("reused-session")
+    return bool(old.ok and exact == 1 and fresh.ok and delayed == 0 and owner and
+                owner.get("session") == "reused-session" and
+                owner.get("epoch") == "" and cleanup == 1)
 
 
 def main():
+    production_counter = os.path.join(
+        os.environ.get("LOCALAPPDATA") or os.path.join(os.path.expanduser("~"), ".local"),
+        "AntonAgents", "workspace-write-leases", "usage.jsonl")
+    production_counter_before = _file_size(production_counter)
     root = tempfile.mkdtemp(prefix="workspace-write-lease-test-")
     os.environ["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(root, "leases.sqlite3")
     os.environ["WORKSPACE_WRITE_LEASE_COUNTER"] = os.path.join(root, "counter.jsonl")
@@ -97,21 +499,54 @@ def main():
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
@@ -125,16 +560,178 @@ def main():
 
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
+                check("поздний token Stop не снимает свежую legacy epoch",
+                      _delayed_token_preserves_fresh_legacy(
+                          lease, os.path.join(root, "fresh-legacy-target.txt")))
+                if hasattr(lease, "LEGACY_MIGRATED_EPOCH"):
+                    broad_mutant_file = _broad_legacy_delete_mutant(
+                        lease.__file__, os.path.join(
+                            root, "workspace_write_lease_broad_legacy_mutant.py"))
+                    original_db = os.environ["WORKSPACE_WRITE_LEASE_DB"]
+                    os.environ["WORKSPACE_WRITE_LEASE_DB"] = os.path.join(
+                        root, "broad-legacy-mutant.sqlite3")
+                    try:
+                        broad_mutant = _load_candidate(broad_mutant_file, "broadlegacy")
+                        marker_delete_killed = not _delayed_token_preserves_fresh_legacy(
+                            broad_mutant, os.path.join(root, "broad-legacy-target.txt"))
+                    finally:
+                        os.environ["WORKSPACE_WRITE_LEASE_DB"] = original_db
+                else:
+                    marker_delete_killed = False
+                check("mutation: marker-delete нельзя расширить до fresh empty epoch",
+                      marker_delete_killed)
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
@@ -147,9 +744,20 @@ def main():
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
 
@@ -165,5 +773,8 @@ if __name__ == "__main__":
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
index f0719abb3..849df3971 100644
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
+    наивная модель и девять production-source мутантов.
 
-updated: 2026-09-11
+updated: 2026-09-21
 """
 from __future__ import annotations
 
@@ -49,6 +52,10 @@ from datetime import datetime, timezone
 
 DEFAULT_TTL_SEC = int(os.environ.get("WORKSPACE_WRITE_LEASE_TTL_SEC") or 1800)
 BUSY_TIMEOUT_MS = 10000
+# Rows that existed before the epoch column was added must be distinguishable from
+# *new* legacy callers that intentionally acquire with epoch="".  A token-aware
+# Stop may consume this one-time handoff marker, but must never wildcard fresh rows.
+LEGACY_MIGRATED_EPOCH = "__workspace_lease_legacy_migrated_v1__"
 
 
 def _state_dir():
@@ -171,6 +178,30 @@ def is_wide_root(path):
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
+            con.execute("UPDATE leases SET epoch=? WHERE epoch=''",
+                        (LEGACY_MIGRATED_EPOCH,))
+        con.commit()
+    except Exception:
+        con.rollback()
+        raise
+
+
 def _connect():
     path = db_path()
     os.makedirs(os.path.dirname(path), exist_ok=True)
@@ -185,16 +216,20 @@ def _connect():
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
 
 
@@ -205,14 +240,31 @@ class LeaseResult:
     conflicts: list[dict] = field(default_factory=list)
     reaped: int = 0
     reason: str = ""
+    epoch: str = ""
+
+
+def _same_owner(row, session, epoch):
+    """Exact epoch ownership, plus a one-time adoption path for migrated rows."""
+    row_epoch = row.get("epoch", "")
+    return (row["session"] == session and
+            (row_epoch == epoch or
+             (bool(epoch) and row_epoch == LEGACY_MIGRATED_EPOCH)))
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
+    if epoch == LEGACY_MIGRATED_EPOCH:
+        raise ValueError("epoch is reserved for schema migration")
     ttl_sec = int(ttl_sec)
     if ttl_sec <= 0:
         raise ValueError("ttl_sec must be positive")
@@ -229,7 +281,8 @@ def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, no
         conflicts = []
         for wanted in resources:
             for row in live:
-                if row["session"] != session and overlaps(wanted, row["resource"]):
+                same_owner = _same_owner(row, session, epoch)
+                if not same_owner and overlaps(wanted, row["resource"]):
                     item = dict(row)
                     item["wanted"] = wanted
                     conflicts.append(item)
@@ -239,49 +292,79 @@ def acquire_many(paths, session, agent, ttl_sec=DEFAULT_TTL_SEC, *, cwd=None, no
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
+                        _same_owner(r, session, epoch)), None)
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
+            _same_owner(r, session, epoch) for r in live)
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
+    During the one-time schema handoff, pre-upgrade rows carry the reserved
+    ``LEGACY_MIGRATED_EPOCH`` marker. An explicit hook Stop releases those marked
+    rows for the same session alongside its exact epoch. Fresh empty-epoch leases
+    remain distinct, so a delayed token cannot erase a later legacy acquisition.
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
+        if epoch is not None:
+            legacy_handoff = con.execute(
+                "DELETE FROM leases WHERE session=? AND epoch=?",
+                (session, LEGACY_MIGRATED_EPOCH)).rowcount
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
+                          "fenced+migration-handoff" if legacy_handoff else "fenced"),
+                "count": n})
     return n
 
 
@@ -343,8 +426,12 @@ def main(argv=None):
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
@@ -354,7 +441,7 @@ def main(argv=None):
     args = ap.parse_args(argv)
     if args.command == "acquire":
         result = acquire_many(args.paths, args.session, args.agent, args.ttl_sec,
-                              cwd=args.cwd, note=args.note)
+                              cwd=args.cwd, note=args.note, epoch=args.epoch)
         if result.ok:
             print("ACQUIRED %d path(s) by %s" % (len(result.resources), args.session))
             return 0
@@ -362,7 +449,7 @@ def main(argv=None):
         print("BUSY: held by %s" % owners)
         return 7
     if args.command == "release-session":
-        print("RELEASED %d" % release_session(args.session))
+        print("RELEASED %d" % release_session(args.session, epoch=args.epoch))
         return 0
     if args.command == "check":
         row = owner_of(args.path, cwd=args.cwd)

=== HOOKS COMMIT ===
commit d23e6c57d67ab6133bc2fa305306341affc93779
Author:     Claude Config Snapshot (HUB-01) <claude-config@HUB-01.local>
AuthorDate: Mon Sep 21 07:16:30 2026 +0100
Commit:     claude-? <claude+?@local>
CommitDate: Mon Sep 21 08:27:22 2026 +0100

    fix: preserve fenced workspace leases across turns
    
    Assisted-by: Codex CLI / GPT-5.6
    
    Machine: HUB-01
    
    Account: bb
    
    Operator: Anton
---
 constitution_guard.py    |   5 +-
 turnstate_hook.py        |  13 +-
 workspace_write_guard.py | 318 +++++++++++++++++++++++++++++++++++++++++++----
 3 files changed, 307 insertions(+), 29 deletions(-)

diff --git a/constitution_guard.py b/constitution_guard.py
index 0b454c3..ce1b395 100644
--- a/constitution_guard.py
+++ b/constitution_guard.py
@@ -7,7 +7,7 @@ in bypass mode and only loads at session start). Anton 2026-06-21 ("замок 
 
 Mechanism: block Edit/Write/MultiEdit/apply_patch on a protected path = exit code 2 +
 reason on stderr. Then acquire the same atomic per-path lease for Claude and Codex;
-explicitly mutating shell commands conservatively lease their cwd.
+explicitly mutating shell commands lease only named absolute targets (never cwd).
 Escape hatch for a REAL, Anton-authorized constitution change (two ways):
   (a) set env CONSTITUTION_UNLOCK=1 in the shell that launched Claude, or
   (b) change the file via a deliberate Bash/python direct write (this guards the Edit/
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
index 1ac31b5..13c6a35 100644
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
@@ -50,6 +56,9 @@ SHELL_MUTATION = re.compile(
     r"copy-item|rename-item|clear-content|tee-object|tee|rm|del|erase|mv|cp|touch|"
     r"truncate)\b|\bsed\s+-[^\r\n]*i\b|\bperl\s+-[^\r\n]*p?i\b|"
     r"\bgit\s+apply\b|(?:^|\s)patch(?:\s|$)|(?<![<>])>{1,2}(?![>&]))")
+ENV_ASSIGNMENT = re.compile(r"^[A-Za-z_][A-Za-z0-9_]*=.*$", re.DOTALL)
+NULL_REDIRECTION = re.compile(
+    r"(?i)(?<!\S)(?:\d|\*)?>\s*(?:\$null\b|nul\b|/dev/null\b)")
 ABS_QUOTED = re.compile(r"[\"']([A-Za-z]:[\\/][^\"'\r\n]+)[\"']")
 ABS_BARE = re.compile(r"(?<![\w])([A-Za-z]:[\\/][^\s\"'|&;<>]+)")
 SEGMENT_SPLIT = re.compile(r"\|\||&&|[;|\r\n]")
@@ -93,18 +102,43 @@ def tool_name(payload):
     return str(payload.get("tool_name") or payload.get("tool") or "").strip()
 
 
+def _shell_dialect(tool):
+    """Quoting belongs to the outer tool, not to the child command it launches."""
+    tool = str(tool or "").strip().lower()
+    if tool == "bash":
+        return "posix"
+    if tool == "powershell":
+        return "powershell"
+    # Generic exec/shell tools use the platform default in this Windows-local
+    # guard. Keep the branch explicit so the same source is honest on a POSIX host.
+    return "powershell" if os.name == "nt" else "posix"
+
+
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
@@ -129,7 +163,235 @@ def _safe_resolve(value, cwd):
         return ""
 
 
-def shell_is_read_only(command):
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
+                escaped = value[index + 1]
+                # In POSIX double quotes, backslash is special only before $, `,
+                # ", \\ and newline. Windows paths such as C:\Users must retain it.
+                if escaped in '$`"\\\n':
+                    if escaped != "\n":
+                        token.append(escaped)
+                else:
+                    token.extend(("\\", escaped))
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
+def _powershell_command_flag(flag):
+    """PowerShell host accepts unambiguous prefixes and '/' on Windows."""
+    flag = str(flag or "").lower()
+    if not flag.startswith(("-", "/")):
+        return False
+    name = flag[1:]
+    return bool(name) and ("command".startswith(name) or
+                           "commandwithargs".startswith(name))
+
+
+def _child_command_bodies(command, dialect="powershell"):
+    for segment in _top_level_segments(command, dialect):
+        tokens = _shell_args(segment, dialect)
+        index = 0
+        if tokens and tokens[0][0] == "&":
+            index += 1
+        if index < len(tokens) and tokens[index][0].lower() == "env":
+            index += 1
+            while index < len(tokens):
+                value = tokens[index][0]
+                if ENV_ASSIGNMENT.match(value):
+                    index += 1
+                    continue
+                if value.startswith("-"):
+                    takes_value = value.lower() in {"-u", "--unset", "-c", "--chdir"}
+                    index += 2 if takes_value and index + 1 < len(tokens) else 1
+                    continue
+                break
+        else:
+            while index < len(tokens) and ENV_ASSIGNMENT.match(tokens[index][0]):
+                index += 1
+        if index >= len(tokens):
+            continue
+        shell = re.split(r"[\\/]", tokens[index][0])[-1].lower()
+        if shell.endswith(".exe"):
+            shell = shell[:-4]
+        if shell not in {"powershell", "pwsh", "cmd", "sh", "bash"}:
+            continue
+        args = tokens[index + 1:]
+        for arg_index, (value, _quoted) in enumerate(args):
+            flag = value.lower()
+            valid = ((shell in {"powershell", "pwsh"} and
+                      _powershell_command_flag(flag)) or
+                     (shell == "cmd" and flag == "/c") or
+                     (shell in {"sh", "bash"} and
+                      bool(re.fullmatch(r"-[a-z]*c[a-z]*", flag))))
+            if valid and arg_index + 1 < len(args) and args[arg_index + 1][1]:
+                child_dialect = ("powershell" if shell in {"powershell", "pwsh"}
+                                 else "cmd" if shell == "cmd" else "posix")
+                yield args[arg_index + 1][0], child_dialect
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
+def shell_is_read_only(command, dialect="powershell"):
     """Читающая команда лизы НЕ берёт -- ни на файл, ни тем более на папку.
 
     Раньше «неизвестное = мутирующее» плюс «любой `;`/`&&` = мутирующее» означало, что
@@ -141,10 +403,11 @@ def shell_is_read_only(command):
     command = str(command or "").strip()
     if not command:
         return True
-    if (SHELL_MUTATION.search(command) or
-            re.search(r"(?i)(?:^|\s)--output(?:=|\s)", command)):
+    scan = shell_scan_text(command, dialect=dialect)
+    if (SHELL_MUTATION.search(scan) or
+            re.search(r"(?i)(?:^|\s)--output(?:=|\s)", scan)):
         return False
-    stages = [stage.strip() for stage in SEGMENT_SPLIT.split(command) if stage.strip()]
+    stages = [stage.strip() for stage in SEGMENT_SPLIT.split(scan) if stage.strip()]
     return bool(stages) and all(READ_ONLY_COMMAND.match(stage) for stage in stages)
 
 
@@ -153,7 +416,7 @@ INTERPRETERS = re.compile(
     r"zsh|ruby|perl|php|dotnet|java|uv|uvx|npx)(?:\.exe)?$")
 
 
-def executable_tokens(command):
+def executable_tokens(command, dialect="powershell"):
     """ЗАПУСКАЕМОЕ -- не цель записи: первый токен сегмента и скрипт интерпретатора.
 
     Замер 14.09: интерпретатор `python.exe` лизовался 5 раз, `cron_heartbeat.py` -- 5,
@@ -163,9 +426,10 @@ def executable_tokens(command):
     интерпретатора снимаем ещё и первый нефлаговый аргумент. Цель записи (`log`) остаётся.
     """
     out = set()
-    for segment in SEGMENT_SPLIT.split(str(command or "")):
-        tokens = re.findall(r"\"([^\"]+)\"|'([^']+)'|(\S+)", segment.strip())
-        tokens = [next(g for g in t if g) for t in tokens]
+    for segment in _top_level_segments(command, dialect):
+        tokens = [value for value, _quoted in _shell_args(segment, dialect)]
+        if tokens and tokens[0] == "&":
+            tokens = tokens[1:]
         if not tokens:
             continue
         out.add(tokens[0])
@@ -201,7 +465,8 @@ def extract_intent(payload):
         return Intent(True, sorted(set(paths)), "file-tool")
     if tool in SHELL_TOOLS:
         command = str(inp.get("command") or inp.get("cmd") or "")
-        if shell_is_read_only(command):
+        dialect = _shell_dialect(tool)
+        if shell_is_read_only(command, dialect=dialect):
             return Intent(False, [], "read-only-shell")
         # 14.09.2026, класс lease-storm, второй заход. Утреннее лечение вывело из лизы только
         # КОНТЕЙНЕРЫ (глубина<=1 и реестр home_dirs.json), но cwd продолжала лизоваться, если
@@ -211,14 +476,15 @@ def extract_intent(payload):
         # флота: сессия, правящая ОДИН скрипт, запирала все остальные на 30 минут.
         # Новый контракт в одну строку: shell лизует ТОЛЬКО файлы, которые НАЗЫВАЕТ, и только
         # когда ВИДИМО пишет. cwd не лизуется никогда -- ни широкая, ни узкая.
-        if not SHELL_MUTATION.search(command):
+        if not SHELL_MUTATION.search(shell_scan_text(command, dialect=dialect)):
             # Не читающая (словарь не признал), но и признака записи нет: `python build.py`,
             # `node x.js`, heredoc. Лизовать нечего -- цели записи в тексте команды нет.
             # Честная дыра: такая команда может писать по относительному пути, и мы её не
             # поймаем. Она и раньше не ловилась, когда cwd была контейнером (обычный случай).
             lease.count_event("hook", "no-mutation-marker", {"tool": tool_name(payload)})
             return Intent(False, [], "no-mutation-marker")
-        skip = {_safe_resolve(token, cwd) for token in executable_tokens(command)}
+        skip = {_safe_resolve(token, cwd)
+                for token in executable_tokens(command, dialect=dialect)}
         paths = []
         for rx in (ABS_QUOTED, ABS_BARE):
             for match in rx.finditer(command):
@@ -255,24 +521,32 @@ def guard_pre(payload):
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

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null && git log --oneline -3 -- workspace_write_lease.py 2>&1; echo \"---\"; cd ~/.claude/hooks 2>/dev/null && git log --oneline -3 -- workspace_write_guard.py 2>&1", "description": "Check git history for the two changed files"}

---

> `Bash` -- {"command": "cd ~/.claude && git cat-file -t e98a662cbb0d92e95dd528a19617e89c1d437db1 2>&1; git cat-file -t d23e6c57d67ab6133bc2fa305306341affc93779 2>&1; git rev-parse HEAD 2>&1; git log --oneline -1 2>&1", "description": "Check if the commit hashes exist in the local repo"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"updated:\" workspace_write_lease.py | head -3\necho \"---guard---\"\ncd ~/.claude/hooks && grep -n \"updated:\" workspace_write_guard.py | head -3\necho \"---lease-storm test---\"\ncd ~/.claude/scripts && grep -n \"updated:\" _test_lease_storm.py | head

---

> `Bash` -- {"command": "set -e\nTMP=$(mktemp -d /tmp/wwl-review.XXXXXX)\necho \"TMP=$TMP\"\nmkdir -p \"$TMP/scripts\" \"$TMP/hooks\"\ncp ~/.claude/scripts/workspace_write_lease.py \"$TMP/scripts/\"\ncp ~/.claude/scripts/_test_lease_storm.py \"$TMP/scripts/\"\ncp ~/.claude/scripts/_test_workspace_write_lease.py

---

> `Write` -- {"file_path": "/tmp/wwl-review.VgSFOY/scripts.patch", "content": "diff --git a/_test_lease_storm.py b/_test_lease_storm.py\nindex b2ff6e02b..1c75bda20 100644\n--- a/_test_lease_storm.py\n+++ b/_test_lease_storm.py\n@@ -33,7 +33,7 @@\n      проверка 1 обязана ОТБИТЬСЯ. Тест, который не краснеет на сл

---

> `Bash` -- {"command": "powershell -c \"Write-Output HELLO_FROM_DASH_C\" 2>&1\necho \"---\"\npwsh -c \"Write-Output HELLO_FROM_PWSH_DASH_C\" 2>&1\necho \"---exit codes above---\"", "description": "Empirically test whether -c alone works as abbreviation for -Command in powershell/pwsh"}

---

> `Bash` -- {"command": "powershell -Command:\"Write-Output COLON_FORM_TEST\" 2>&1\necho \"rc=$?\"\necho \"---testing pwsh---\"\npwsh -Command:\"Write-Output COLON_FORM_TEST_PWSH\" 2>&1\necho \"rc=$?\"", "description": "Test whether colon-attached -Command: syntax is accepted by powershell/pwsh native host pars

---

**Claude:**

SUMMARY: Deep static/empirical review of both commits (transaction semantics, migration concurrency, release fencing, PowerShell/Bash parsing, structured-deny contract). Reconstructed the pre-commit base and diffed logically since these commit hashes aren't present in the local `~/.claude` repo (local HEAD is still 2026-09-11/14-dated, this commit hasn't landed yet). Verified empirically on this machine that `powershell -c "..."` and `pwsh -c "..."` are accepted (confirms `_powershell_command_flag`'s bare `-c` acceptance is correct, not over-broad) and that `-Command:"..."` colon-attached form is rejected by both native hosts (confirms the guard correctly does not need to special-case it — no bypass there). Traced `acquire_many`'s `BEGIN IMMEDIATE` + recheck-after-lock pattern, `_migrate_epoch`'s lock-then-recheck schema upgrade, `_same_owner`'s exact-epoch-or-migrated-marker-adoption rule, and `release_session`'s exact-epoch delete plus scoped legacy-marker handoff — all algebraically correct against the traced test scenarios (delayed-old-epoch-release, foreign-session release, CLI epoch plumbing, broad-legacy-delete mutant). The one substantive gap found: the turn-fencing protection this commit is titled for ("fence workspace write leases by turn") is proven only for Codex. Claude sessions never populate `turn_id`, so `lease_epoch()` is always `""` for every Claude turn of a session — meaning `_same_owner` trivially matches across turns and a delayed/late Stop from a stale Claude turn can still release a lease a newer Claude turn just acquired, identical to pre-patch behavior. This is disclosed in an inline code comment but is not listed among the task's stated "Honest non-goals."

FINDINGS:
- hooks/turnstate_hook.py:~80-95 (release_workspace_write_lease docstring/impl) | medium | The commit's core acceptance property "delayed old turn release cannot remove new epoch" holds only for Codex, which supplies `turn_id`. Claude Code hook payloads never carry `turn_id`, so `lease_epoch()` (hooks/workspace_write_guard.py `lease_epoch`) always returns `""` for Claude, and every Claude turn of one session shares that same empty epoch. `_same_owner` then matches unconditionally across Claude turns, so a Stop hook that fires late for a stale Claude turn still deletes the lease a subsequent Claude turn acquired — the exact lease-storm/turn-race class this commit is named for is unfixed for the harness actually driving this session. It's honestly disclosed in a code comment ("Claude currently uses explicit legacy epoch \"\"") but is absent from the task's stated Honest-non-goals list, so a reader of the acceptance criteria alone would wrongly conclude Claude turns are fenced too. Fix: either surface a Claude-side per-turn token (e.g. a monotonic counter keyed by session, persisted across the Stop/PreToolUse boundary) so `_same_owner` can distinguish Claude turns, or add this explicitly to the disclosed non-goals so downstream consumers don't assume universal coverage.

VERDICT: REQUEST_CHANGES