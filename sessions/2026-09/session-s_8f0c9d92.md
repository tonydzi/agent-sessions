---
session: s_8f0c9d92
date: 2026-09-22
words: 4432
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · diff --git a/_test_lease_storm.py b/_test_lease_storm.py

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_8f0c9d92` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

diff --git a/_test_lease_storm.py b/_test_lease_storm.py
index 06873a46e..da02fc335 100644
--- a/_test_lease_storm.py
+++ b/_test_lease_storm.py
@@ -1,213 +1,188 @@
 # -*- coding: utf-8 -*-
-"""Красный-первым тест КЛАССА lease-storm (14.09.2026, второй заход).
-
-ЧТО СТЕРЕЖЁТ. Лиза записи бралась на ПАПКУ (cwd команды), а `overlaps()` матчит предка в обе
-стороны -- значит одна сессия, правящая ОДИН файл, запирала всю папку на TTL (30 мин) для всех
-остальных. Утренняя правка вывела из лизы только КОНТЕЙНЕРЫ (глубина<=1 + реестр home_dirs.json),
-но горячие ОБЩИЕ папки флота (`~/.claude/scripts`) контейнерами не считаются, и шторм остался.
-
-ЗАМЕР по usage.jsonl хаба ПОСЛЕ утренней правки (14.09, 07:27Z -> 13:20Z):
-  198 блокировок · 137 из них (69%) содержали ПАПКУ · 86 -- ровно `~/.claude/scripts`
-  · 36 пострадавших сессий · среди жертв ЧТЕНИЕ файла и `cd`, запиравший сессию насмерть.
-
-НОВЫЙ КОНТРАКТ (одна строка, чинится молотком): shell лизует ТОЛЬКО названные абсолютные
-файлы -- видимый writer явно, неизвестная non-reader форма консервативно. cwd и каталоги не
-лизуются никогда; доказанное чтение не лизует ничего; запускаемая программа целью записи не
-считается. Файловые инструменты лизуют свой файл как прежде.
-
-ПРОВЕРКИ (1-3 -- приёмка из наряда, 4-8 -- границы, 9 -- красный-мутант):
-  1. Сессия B ПИШЕТ другой файл в папке, которую заняла сессия A -> ПРОХОДИТ.
-  2. Сессия B ЧИТАЕТ третий файл в той же папке (`cd .. && cat ...`) -> ПРОХОДИТ.
-  3. Контрольный: сессия B пишет ТОТ ЖЕ файл -> BUSY.
-  4. cwd внутри занятой папки не запирает сессию (тот самый смертельный `cd`).
-  5. Запуск скрипта, который держит сосед, -> ПРОХОДИТ (запуск != запись).
-  5b. То же С редиректом: цель записи -- лог, а не запускаемый скрипт. Отдельная
-     проверка, потому что первого токена мало: в `python X.py > log` программа --
-     `python`, а по абсолютному пути назван X.py. Пробу написал `_probe_lease_scope.py`,
-     она и поймала эту дыру в первой версии починки.
-  6. Контейнер, названный в команде явно, не лизуется.
-  7. Файловый инструмент Write по чужому файлу -> BUSY (главная защита цела).
-  8. extract_paths() на нелизуемой команде возвращает ПУСТО, а не строку посимвольно
-     (живой баг утренней правки: Intent(False, "текст", []) -- аргументы перепутаны местами,
-     а .paths читают constitution_guard.py и orphan_check_hook.py).
-  9. КРАСНЫЙ-МУТАНТ: со старым хуком (LEASE_STORM_MUTANT=1 -> лизуем cwd, как до починки)
-     проверка 1 обязана ОТБИТЬСЯ. Тест, который не краснеет на сломанном коде, фальшивый.
-
-РЕЛЬСА: 0 LLM, 0 сети, stdlib. Гоняет реальный hooks/workspace_write_guard.py через stdin-контракт.
+"""Regression for lease-storm under the fail-closed shell contract.
+
+The storm root was directory-scoped locking. File tools must lease only their
+exact files, so neighboring writes remain independent. Unisolated shell is a
+separate unsafe rail and is denied before command classification.
+
+Rail: local Python stdlib, isolated SQLite/counter, 0 network/production writes.
 updated: 2026-09-22
 """
+from __future__ import annotations
+
 import json
 import os
 import shutil
+import sqlite3
 import subprocess
 import sys
 import tempfile
+from pathlib import Path
+
 
 HOOKS = os.environ.get("WORKSPACE_LEASE_TEST_HOOKS") or os.path.join(
     os.path.expanduser("~"), ".claude", "hooks")
-HOOK = os.path.join(HOOKS, "workspace_write_guard.py")
 SCRIPTS = os.path.dirname(os.path.abspath(__file__))
-sys.path.insert(0, SCRIPTS)
-import workspace_write_lease as lease  # noqa: E402
-
-MUTANT_SHIM = r"""
-import re, sys
-sys.path.insert(0, r"{hooks}")
-import workspace_write_guard as g
-
-def extract_intent(payload):           # поведение ДО починки: mutating shell лизует cwd
-    tool = g.tool_name(payload).lower()
-    if tool not in g.SHELL_TOOLS:
-        return _orig(payload)
-    inp = payload.get("tool_input") or {{}}
-    cwd = str(payload.get("cwd") or "")
-    command = str(inp.get("command") or "")
-    if g.SHELL_MUTATION.search(command) or re.search(r"(?:;|&&|\|\||[\r\n]|[{{}}])", command):
-        pass
-    elif all(g.READ_ONLY_COMMAND.match(s.strip()) for s in command.split("|") if s.strip()):
-        return g.Intent(False, [], "read-only-shell")
-    paths = [g._resolve(cwd, cwd)] if cwd else []
-    for rx in (g.ABS_QUOTED, g.ABS_BARE):
-        for m in rx.finditer(command):
-            try:
-                paths.append(g._resolve(m.group(1), cwd))
-            except Exception:
-                continue
-    return g.Intent(True, sorted(set(paths)), "mutating-shell") if paths else g.Intent(False, [], "x")
-
-_orig = g.extract_intent
-g.extract_intent = extract_intent
-sys.exit(g.main(["--phase", "pre"]))
-"""
+GUARD = os.path.join(HOOKS, "workspace_write_guard.py")
 
 
-def call_guard(command, cwd, session, env, tool="Bash", file_path=None,
-               include_epoch=True):
-    inp = {"file_path": file_path} if file_path else {"command": command}
-    payload = {"tool_name": tool, "tool_input": inp, "cwd": cwd, "session_id": session}
-    if include_epoch:
-        payload["prompt_id"] = "lease-storm-%s" % session
-    if env.get("LEASE_STORM_MUTANT"):
-        shim = MUTANT_SHIM.format(hooks=os.path.dirname(HOOK))
-        argv = [sys.executable, "-c", shim]
-    else:
-        argv = [sys.executable, HOOK, "--phase", "pre"]
-    proc = subprocess.run(argv, input=json.dumps(payload),
-                          capture_output=True, text=True, env=env)
-    return proc.returncode, (proc.stderr or "") + (proc.stdout or "")
-
-
-def _run(tmp):
-    container = os.path.join(tmp, "workdir")          # играет роль рабочей папки узла
-    hot = os.path.join(container, "scripts")          # горячая ОБЩАЯ папка (~/.claude/scripts)
-    os.makedirs(hot)
-    busy = os.path.join(hot, "busy.py")               # файл, который правит сосед
-    other = os.path.join(hot, "other.py")             # файл, который пишем мы
-    third = os.path.join(hot, "third.py")             # файл, который мы читаем
-    for path in (busy, other, third):
-        open(path, "w", encoding="utf-8").write("# fixture\n")
-
-    base = dict(os.environ,
-                WORKSPACE_WRITE_LEASE_DB=os.path.join(tmp, "leases.sqlite3"),
-                WORKSPACE_WRITE_LEASE_COUNTER=os.path.join(tmp, "usage.jsonl"),
-                WORKSPACE_WRITE_LEASE_MODULE_DIR=SCRIPTS,
-                WORKSPACE_WIDE_ROOTS=container)
-    for inherited_identity in ("CODEX_THREAD_ID", "CODEX_SESSION_ID",
-                               "CLAUDE_CODE_SESSION_ID", "CLAUDE_SESSION_ID"):
-        base.pop(inherited_identity, None)
-    os.environ.update({k: base[k] for k in
-                       ("WORKSPACE_WRITE_LEASE_DB", "WORKSPACE_WRITE_LEASE_COUNTER")})
-    mutant = dict(base, LEASE_STORM_MUTANT="1")
-
-    # Сосед (сессия A) держит ОДИН файл в горячей общей папке -- обычная картина живого узла.
-    got = lease.acquire_many([busy], "session-A", "claude", note="сосед правит один файл")
-    assert got.ok, "подготовка не удалась: сосед не смог взять свой файл"
-
-    fails = []
-
-    def expect(name, want_rc, command, cwd, env=base, **kw):
-        rc, out = call_guard(command, cwd, "session-B", env, **kw)
-        if rc != want_rc:
-            fails.append("%s: ждали rc=%s, получили rc=%s %s" % (name, want_rc, rc,
-                                                                 out.strip()[:170]))
-
-    # --- приёмка из наряда -------------------------------------------------------------
-    expect("1. запись ДРУГОГО файла в занятой папке", 0,
-           'sed -i "s/a/b/" "%s"' % other, hot)
-    expect("2. ЧТЕНИЕ третьего файла в занятой папке", 0,
-           'cd "%s" && cat "%s"' % (container, third), hot)
-    expect("3. КОНТРОЛЬ: запись в ТОТ ЖЕ файл", 2,
-           'sed -i "s/a/b/" "%s"' % busy, hot)
-
-    # --- границы -----------------------------------------------------------------------
-    expect("4. cwd внутри занятой папки не запирает сессию", 0, "python build.py", hot)
-    expect("5. ЗАПУСК скрипта соседа -- не запись", 0, 'python "%s" --flag' % busy, container)
-    # 5b. С признаком записи в команде путь скрипта всё равно не цель: замер 14.09 показал
-    # cron_heartbeat.py 5 отбоев и mcp_daemons_watchdog.ps1 6 -- это был ЗАПУСК с редиректом.
-    expect("5b. запуск соседского скрипта С редиректом: цель -- лог, не скрипт", 0,
-           'python "%s" > "%s"' % (busy, os.path.join(hot, "run.log")), container)
-    expect("6. контейнер, названный явно, не лизуется", 0,
-           'echo hi > "%s"' % os.path.join(container, "out.txt"), container)
-    expect("7. файловый инструмент по чужому файлу -> BUSY", 2,
-           "", container, tool="Write", file_path=busy)
-
-    # 8. extract_paths не должен разваливать строку на буквы (баг перепутанных аргументов)
-    probe = os.path.join(tmp, "probe.py")
-    open(probe, "w", encoding="utf-8").write(
-        "import json,sys,os\n"
-        "sys.path.insert(0, r'%s')\n" % os.path.dirname(HOOK) +
-        "import workspace_write_guard as g\n"
-        "p={'tool_name':'Bash','tool_input':{'command':'python build.py'},"
-        "'cwd':r'%s','session_id':'probe'}\n" % hot +
-        "print(json.dumps([str(x) for x in g.extract_paths(p)]))\n")
-    out = subprocess.run([sys.executable, probe], capture_output=True, text=True, env=base)
+def call(payload, env, phase="pre"):
+    return subprocess.run(
+        [sys.executable, GUARD, "--phase", phase],
+        input=json.dumps(payload), capture_output=True, text=True,
+        encoding="utf-8", errors="replace", env=env, timeout=30)
+
+
+def write_payload(session, epoch, cwd, target, tool="Write"):
+    return {
+        "session_id": session, "prompt_id": epoch, "cwd": cwd,
+        "tool_name": tool, "tool_input": {"file_path": target},
+    }
+
+
+def active_rows(db):
+    con = sqlite3.connect(db)
     try:
-        parsed = json.loads((out.stdout or "[]").strip().splitlines()[-1])
-    except Exception:
-        parsed = ["<не разобрать: %s>" % (out.stderr or "")[:120]]
-    if parsed:
-        fails.append("8. extract_paths вернул %d элемент(ов) вместо пустоты -> %s" %
-                     (len(parsed), parsed[:6]))
-
-    # A synthetic/old harness that omits the per-turn fencing token must be denied;
-    # weakening this would let a delayed Stop remove a later turn's lease.
-    rc, out = call_guard('sed -i "s/a/b/" "%s"' % other, hot,
-                         "session-no-epoch", base, include_epoch=False)
-    if rc != 2 or "turn_id/prompt_id" not in out:
-        fails.append("9. write без epoch не fail-closed: rc=%s out=%s" %
-                     (rc, out.strip()[:140]))
-
-    # --- 10. красный-мутант: старое поведение обязано провалить проверку 1 --------------
-    rc, out = call_guard('sed -i "s/a/b/" "%s"' % other, hot, "session-B", mutant)
-    if rc != 2:
-        fails.append("10. МУТАНТ НЕ ПОКРАСНЕЛ: старый хук обязан отбить запись в ДРУГОЙ файл "
-                     "занятой папки (rc=%s). Тест ничего не стережёт." % rc)
-    elif "BUSY" not in out:
-        fails.append("10. мутант отбил, но не по причине BUSY: %s" % out.strip()[:140])
-
-    lease.release_session("session-A")
-    lease.release_session("session-B", epoch="lease-storm-session-B")
-    leaked_test_owners = [
-        row for row in lease.active()
-        if row.get("session") in {"session-A", "session-B"}
-    ]
-    if leaked_test_owners:
-        fails.append("11. test leases не освобождены точно: %r" % leaked_test_owners)
-    if fails:
-        for line in fails:
-            print("FAIL " + line)
-        return 1
-    print("OK 11/11 lease-storm: папка не лизуется, чтение свободно, запуск != запись, "
-          "точечная защита цела, мутант краснеет")
-    return 0
+        return con.execute(
+            "SELECT session,epoch,resource FROM leases ORDER BY resource"
+        ).fetchall()
+    finally:
+        con.close()
 
 
 def main():
-    tmp = os.path.realpath(tempfile.mkdtemp(prefix="lease-storm-test-"))
+    root = os.path.realpath(tempfile.mkdtemp(prefix="lease-storm-test-"))
+    failures = []
     try:
-        return _run(tmp)
+        hot = os.path.join(root, "workdir", "scripts")
+        os.makedirs(hot)
+        busy = os.path.join(hot, "busy.py")
+        other = os.path.join(hot, "other.py")
+        third = os.path.join(hot, "third.py")
+        for target in (busy, other, third):
+            Path(target).write_text("# fixture\n", encoding="utf-8")
+
+        env = dict(os.environ)
+        env.update({
+            "WORKSPACE_WRITE_LEASE_DB": os.path.join(root, "leases.sqlite3"),
+            "WORKSPACE_WRITE_LEASE_COUNTER": os.path.join(root, "usage.jsonl"),
+            "WORKSPACE_WRITE_LEASE_MODULE_DIR": SCRIPTS,
+            "CODEX_THREAD_ID": "",
+            "CLAUDE_CODE_SESSION_ID": "",
+            "CLAUDE_SESSION_ID": "",
+        })
+
+        owner = call(write_payload("session-A", "turn-A", hot, busy), env)
+        neighbor = call(write_payload("session-B", "turn-B", hot, other), env)
+        same = call(write_payload("session-B", "turn-B", hot, busy, "Edit"), env)
+        third_run = call(write_payload("session-C", "turn-C", hot, third), env)
+
+        if owner.returncode != 0:
+            failures.append("1 owner could not acquire exact file: %s" %
+                            owner.stderr[:160])
+        if neighbor.returncode != 0:
+            failures.append("2 neighboring file was directory-blocked: %s" %
+                            neighbor.stderr[:160])
+        if same.returncode != 2 or "session-A" not in same.stderr:
+            failures.append("3 same file was not BUSY by session-A: %s/%s" %
+                            (same.returncode, same.stderr[:160]))
+        if third_run.returncode != 0:
+            failures.append("4 third exact file was blocked: %s" %
+                            third_run.stderr[:160])
+
+        rows = active_rows(env["WORKSPACE_WRITE_LEASE_DB"])
+        resources = {row[2] for row in rows}
+        hot_key = os.path.normcase(os.path.realpath(hot))
+        if hot_key in resources or len(resources) != 3:
+            failures.append("5 leases are not exactly three files: %r" % rows)
+
+        reader = call({
+            "session_id": "shell-reader", "prompt_id": "turn-reader",
+            "cwd": hot, "tool_name": "PowerShell",
+            "tool_input": {"command": 'Get-Content "%s"' % third},
+        }, env)
+        writer = call({
+            "session_id": "shell-writer", "prompt_id": "turn-writer",
+            "cwd": hot, "tool_name": "Bash",
+            "tool_input": {"command": 'printf x > "%s"' %
+                           other.replace("\\", "/")},
+        }, env)
+        if reader.returncode != 2 or "unisolated shell execution" not in reader.stderr:
+            failures.append("6 shell reader escaped fail-closed: %s/%s" %
+                            (reader.returncode, reader.stderr[:140]))
+        if writer.returncode != 2 or "unisolated shell execution" not in writer.stderr:
+            failures.append("7 shell writer escaped fail-closed: %s/%s" %
+                            (writer.returncode, writer.stderr[:140]))
+
+        no_epoch = call({
+            "session_id": "no-epoch", "cwd": hot, "tool_name": "Write",
+            "tool_input": {"file_path": os.path.join(hot, "new.py")},
+        }, env)
+        if no_epoch.returncode != 2 or "turn_id/prompt_id" not in no_epoch.stderr:
+            failures.append("8 file writer without epoch did not fail closed: %s/%s" %
+                            (no_epoch.returncode, no_epoch.stderr[:140]))
+
+        wrong_stop = call(
+            {"session_id": "session-A", "prompt_id": "wrong-turn", "cwd": hot},
+            env, "stop")
+        still_busy = call(
+            write_payload("session-D", "turn-D", hot, busy), env)
+        exact_stop = call(
+            {"session_id": "session-A", "prompt_id": "turn-A", "cwd": hot},
+            env, "stop")
+        after_stop = call(
+            write_payload("session-D", "turn-D", hot, busy), env)
+        if wrong_stop.returncode != 0 or still_busy.returncode != 2:
+            failures.append("9 wrong Stop released a fenced lease")
+        if exact_stop.returncode != 0 or after_stop.returncode != 0:
+            failures.append("10 exact Stop did not release fenced lease")
+
+        # Red control for the historical root: if a shell/guard mutant acquires
+        # the directory instead of the exact output file, a neighboring file is
+        # blocked. This proves the independence assertions above would redden.
+        provider = os.path.join(SCRIPTS, "workspace_write_lease.py")
+        mutant_hot = os.path.join(root, "mutant-directory-scope")
+        os.makedirs(mutant_hot)
+        directory_owner = subprocess.run(
+            [sys.executable, provider, "acquire", mutant_hot,
+             "--session", "mutant-directory", "--agent", "mutant",
+             "--epoch", "mutant-turn"],
+            capture_output=True, text=True, encoding="utf-8",
+            errors="replace", env=env, timeout=30)
+        directory_red = call(
+            write_payload("mutant-neighbor", "mutant-neighbor-turn", mutant_hot,
+                          os.path.join(mutant_hot, "mutant-neighbor.py")), env)
+        subprocess.run(
+            [sys.executable, provider, "release-session",
+             "--session", "mutant-directory", "--epoch", "mutant-turn"],
+            capture_output=True, text=True, encoding="utf-8",
+            errors="replace", env=env, timeout=30)
+        if (directory_owner.returncode != 0 or directory_red.returncode != 2 or
+                "mutant-directory" not in directory_red.stderr):
+            failures.append(
+                "10b directory-lease mutant did not turn neighbor red: %s/%s/%s" %
+                (directory_owner.returncode, directory_red.returncode,
+                 directory_red.stderr[:120]))
+
+        for session, epoch in (
+                ("session-B", "turn-B"), ("session-C", "turn-C"),
+                ("session-D", "turn-D")):
+            call({"session_id": session, "prompt_id": epoch, "cwd": hot},
+                 env, "stop")
+        leaked = [row for row in active_rows(env["WORKSPACE_WRITE_LEASE_DB"])
+                  if row[0].startswith("session-")]
+        if leaked:
+            failures.append("11 test owners leaked: %r" % leaked)
+
+        if failures:
+            for failure in failures:
+                print("FAIL " + failure)
+            return 1
+        print("OK 11/11 lease-storm: exact file independence, same-file BUSY, "
+              "fenced Stop, shell fail-closed, and directory mutant red")
+        return 0
     finally:
-        shutil.rmtree(tmp)
+        shutil.rmtree(root)
 
 
 if __name__ == "__main__":
@@ -216,4 +191,4 @@ if __name__ == "__main__":
         sys.stderr.reconfigure(encoding="utf-8")
     except Exception:
         pass
-    sys.exit(main())
+    raise SystemExit(main())
diff --git a/_test_workspace_write_guard.py b/_test_workspace_write_guard.py
index 542e80311..604ce8756 100644
--- a/_test_workspace_write_guard.py
+++ b/_test_workspace_write_guard.py
@@ -498,6 +498,42 @@ def _guard_race(root, target, racers=8):
 
 
 def main():
+    # The historical body below accepts a parsed shell subset. The 22.09 root
+    # contract removes that unsound rail entirely. Keep the old matrix usable
+    # for rollback branches, but route the fail-closed candidate to its focused
+    # acceptance so the standard test entrypoint follows the active contract.
+    with open(GUARD, encoding="utf-8") as fh:
+        guard_source = fh.read()
+    if "blocked-unisolated-shell" in guard_source:
+        focused = os.path.join(
+            SCRIPTS, "_test_workspace_write_guard_fail_closed.py")
+        focused_env = dict(os.environ)
+        codex_hooks = (focused_env.get("WORKSPACE_LEASE_TEST_CODEX_HOOKS") or
+                       os.path.join(HOME, ".codex", "hooks.json"))
+        claude_settings = (
+            focused_env.get("WORKSPACE_LEASE_TEST_CLAUDE_SETTINGS") or
+            os.path.join(HOME, ".claude", "settings.json"))
+        focused_env.update({
+            "WORKSPACE_LEASE_TEST_REQUIRE_PIN": "1",
+            "WORKSPACE_LEASE_TEST_CODEX_HOOKS": codex_hooks,
+            "WORKSPACE_LEASE_TEST_CLAUDE_SETTINGS": claude_settings,
+        })
+        for env_name, path in (
+                ("WORKSPACE_LEASE_TEST_EXPECTED_GUARD_SHA256", GUARD),
+                ("WORKSPACE_LEASE_TEST_EXPECTED_TEST_SHA256", focused),
+                ("WORKSPACE_LEASE_TEST_EXPECTED_CODEX_CONFIG_SHA256", codex_hooks),
+                ("WORKSPACE_LEASE_TEST_EXPECTED_CLAUDE_CONFIG_SHA256",
+                 claude_settings)):
+            if os.path.isfile(path):
+                focused_env[env_name] = _file_facts(path)["sha256"]
+        run = subprocess.run(
+            [sys.executable, focused], cwd=SCRIPTS, env=focused_env,
+            capture_output=True, text=True, encoding="utf-8",
+            errors="replace", timeout=120)
+        sys.stdout.write(run.stdout)
+        sys.stderr.write(run.stderr)
+        return run.returncode
+
     production_audit = os.path.join(HOME, ".claude", "hooks", "_constitution_guard.log")
     production_audit_before = _file_size(production_audit)
     production_usage = os.path.join(
diff --git a/_test_workspace_write_guard_fail_closed.py b/_test_workspace_write_guard_fail_closed.py
new file mode 100644
index id_c9083e08..f91190517
--- /dev/null
+++ b/_test_workspace_write_guard_fail_closed.py
@@ -0,0 +1,347 @@
+# -*- coding: utf-8 -*-
+"""Acceptance for the fail-closed unisolated-shell workspace guard.
+
+The guard is static: it cannot prove shell startup files, environment supplied
+functions/options, late stdin, descendants, or physical path aliases. Therefore
+every shell tool is denied before parsing. Exact file tools retain per-file leases.
+
+Rail: local Python stdlib, isolated SQLite/counter, 0 network, 0 production writes.
+"""
+from __future__ import annotations
+
+import hashlib
+import json
+import os
+import sqlite3
+import subprocess
+import sys
+import tempfile
+from concurrent.futures import ThreadPoolExecutor
+from pathlib import Path
+
+
+HOME = os.path.expanduser("~")
+SCRIPTS = os.environ.get("WORKSPACE_LEASE_TEST_SCRIPTS") or os.path.join(
+    HOME, ".claude", "scripts")
+HOOKS = os.environ.get("WORKSPACE_LEASE_TEST_HOOKS") or os.path.join(
+    HOME, ".claude", "hooks")
+GUARD = os.path.join(HOOKS, "workspace_write_guard.py")
+CODEX_HOOKS = (os.environ.get("WORKSPACE_LEASE_TEST_CODEX_HOOKS") or
+               os.path.join(HOME, ".codex", "hooks.json"))
+CLAUDE_SETTINGS = (os.environ.get("WORKSPACE_LEASE_TEST_CLAUDE_SETTINGS") or
+                   os.path.join(HOME, ".claude", "settings.json"))
+RESULTS = []
+
+
+def check(name, ok, detail=""):
+    RESULTS.append((name, bool(ok), detail))
+    print("  %s %s%s" % ("OK  " if ok else "FAIL", name,
+                          (" -- " + str(detail)) if detail else ""))
+
+
+def sha(path):
+    return hashlib.sha256(Path(path).read_bytes()).hexdigest()
+
+
+def rows(db):
+    con = sqlite3.connect(db)
+    try:
+        return con.execute(
+            "SELECT session,epoch,resource FROM leases ORDER BY resource"
+        ).fetchall()
+    except sqlite3.OperationalError:
+        return []
+    finally:
+        con.close()
+
+
+def new_matching_lines(path, offset, markers):
+    """Return only new production rows attributable to this synthetic run."""
+    if not os.path.isfile(path):
+        return []
+    if os.path.getsize(path) < offset:
+        return ["production log shrank during acceptance"]
+    with open(path, "rb") as fh:
+        fh.seek(offset)
+        tail = fh.read().decode("utf-8", errors="replace")
+    return [line for line in tail.splitlines()
+            if any(marker in line for marker in markers)]
+
+
+def run_guard(guard, payload, env, phase="pre"):
+    return subprocess.run(
+        [sys.executable, guard, "--phase", phase],
+        input=json.dumps(payload), capture_output=True, text=True,
+        encoding="utf-8", errors="replace", env=env, timeout=30)
+
+
+def codex_reason(run):
+    try:
+        return run.returncode, json.loads(run.stdout)["hookSpecificOutput"]
+    except Exception:
+        return run.returncode, {}
+
+
+def hook_commands(config, event):
+    out = []
+    for group in ((config.get("hooks") or {}).get(event) or []):
+        for hook in group.get("hooks") or []:
+            out.append((str(group.get("matcher") or ""),
+                        str(hook.get("command") or "")))
+    return out
+
+
+def main():
+    expected_guard = os.environ.get(
+        "WORKSPACE_LEASE_TEST_EXPECTED_GUARD_SHA256", "").lower()
+    expected_test = os.environ.get(
+        "WORKSPACE_LEASE_TEST_EXPECTED_TEST_SHA256", "").lower()
+    expected_codex_config = os.environ.get(
+        "WORKSPACE_LEASE_TEST_EXPECTED_CODEX_CONFIG_SHA256", "").lower()
+    expected_claude_config = os.environ.get(
+        "WORKSPACE_LEASE_TEST_EXPECTED_CLAUDE_CONFIG_SHA256", "").lower()
+    require_pin = os.environ.get("WORKSPACE_LEASE_TEST_REQUIRE_PIN") == "1"
+    this_file = os.path.realpath(__file__)
+    check("candidate roots are explicit",
+          os.path.realpath(GUARD).startswith(os.path.realpath(HOOKS) + os.sep) and
+          this_file.startswith(os.path.realpath(SCRIPTS) + os.sep),
+          "guard=%s test=%s" % (GUARD, this_file))
+    try:
+        actual_hashes = {
+            "guard": sha(GUARD), "test": sha(this_file),
+            "codex": sha(CODEX_HOOKS), "claude": sha(CLAUDE_SETTINGS),
+        }
+        codex_config = json.loads(Path(CODEX_HOOKS).read_text(encoding="utf-8"))
+        claude_config = json.loads(Path(CLAUDE_SETTINGS).read_text(encoding="utf-8"))
+    except (OSError, ValueError) as exc:
+        check("harness configs are readable JSON", False, repr(exc))
+        print("\nVERDICT: FAIL: harness configs are readable JSON")
+        return 1
+    check("candidate bytes are SHA-pinned", require_pin and
+          expected_guard == actual_hashes["guard"] and
+          expected_test == actual_hashes["test"] and
+          expected_codex_config == actual_hashes["codex"] and
+          expected_claude_config == actual_hashes["claude"],
+          json.dumps(actual_hashes, sort_keys=True))
+    codex_pre = hook_commands(codex_config, "PreToolUse")
+    claude_pre = hook_commands(claude_config, "PreToolUse")
+    claude_substop = hook_commands(claude_config, "SubagentStop")
+    required_codex = {
+        "Write", "Edit", "MultiEdit", "NotebookEdit", "apply_patch",
+        "Bash", "PowerShell", "exec_command", "shell",
+    }
+    codex_covered = {
+        token for matcher, command in codex_pre
+        if "constitution_guard" in command
+        for token in matcher.split("|") if token}
+    check("both harness configs route shell and file tools to the guard",
+          required_codex.issubset(codex_covered) and
+          any("Bash" in matcher and "PowerShell" in matcher and
+              "constitution_guard" in command
+              for matcher, command in claude_pre) and
+          any("Write" in matcher and "constitution_guard" in command
+              for matcher, command in claude_pre) and
+          any("workspace_write_guard.py" in command and "--phase stop" in command
+              for _matcher, command in claude_substop),
+          "codex=%r claude-settings=%s" %
+          (sorted(codex_covered), CLAUDE_SETTINGS))
+
+    production_audit = os.path.join(
+        HOME, ".claude", "hooks", "_constitution_guard.log")
+    production_usage = os.path.join(
+        os.environ.get("LOCALAPPDATA") or os.path.join(HOME, ".local"),
+        "AntonAgents", "workspace-write-leases", "usage.jsonl")
+    production_offsets = {
+        production_audit: (os.path.getsize(production_audit)
+                           if os.path.isfile(production_audit) else 0),
+        production_usage: (os.path.getsize(production_usage)
+                           if os.path.isfile(production_usage) else 0),
+    }
+
+    with tempfile.TemporaryDirectory(prefix="workspace-guard-closed-") as root:
+        db = os.path.join(root, "leases.sqlite3")
+        counter = os.path.join(root, "usage.jsonl")
+        env = dict(os.environ)
+        env.update({
+            "WORKSPACE_WRITE_LEASE_MODULE_DIR": SCRIPTS,
+            "WORKSPACE_WRITE_LEASE_DB": db,
+            "WORKSPACE_WRITE_LEASE_COUNTER": counter,
+            "CODEX_THREAD_ID": "",
+            "CLAUDE_CODE_SESSION_ID": "",
+            "CLAUDE_SESSION_ID": "",
+        })
+        victim = os.path.join(root, "victim.txt")
+        Path(victim).write_text("sentinel\n", encoding="utf-8")
+        before = sha(victim)
+
+        cases = [
+            ("PowerShell reader", "PowerShell", 'Get-Content "%s"' % victim),
+            ("PowerShell direct writer", "PowerShell",
+             'Set-Content -LiteralPath "%s" -Value changed' % victim),
+            ("opaque interpreter", "exec_command", "python child.py"),
+            ("nested shell", "PowerShell",
+             'powershell -NoProfile -Command "Get-Location"'),
+            ("persistent stdin", "PowerShell",
+             'powershell -NoProfile -NoExit -Command "Get-Location"'),
+            ("detached process", "PowerShell",
+             'Start-Process powershell -ArgumentList "-NoProfile"'),
+            ("Get-Command redirect", "PowerShell",
+             'Get-Command Get-AppLockerPolicy > "%s"' % victim),
+            ("rg dynamic option", "PowerShell",
+             'rg --no-config $env:RGOPT needle "%s"' % victim),
+            ("Bash reader", "Bash", "cat /dev/null"),
+            ("Bash read-write redirect", "Bash",
+             'cat 3<>"%s"' % victim.replace("\\", "/")),
+        ]
+        evidence = []
+        # Do not inspect SQLite before the first writer: sqlite3.connect would
+        # itself create a zero-byte/empty foreign DB and invalidate the provider's
+        # first-open schema transition. Shell denial must not create the DB.
+        baseline = []
+        for index, (name, tool, command) in enumerate(cases):
+            run = run_guard(GUARD, {
+                "session_id": "claude-shell-%d" % index,
+                "prompt_id": "prompt-shell-%d" % index,
+                "cwd": root, "tool_name": tool,
+                "tool_input": {"command": command},
+            }, env)
+            evidence.append((name, run.returncode, run.stderr[:120]))
+        check("all Claude shell shapes fail closed before execution",
+              all(rc == 2 and "unisolated shell execution" in err
+                  for _name, rc, err in evidence) and
+              sha(victim) == before and not os.path.exists(db),
+              evidence)
+
+        codex = run_guard(GUARD, {
+            "thread_id": "codex-shell", "turn_id": "turn-shell",
+            "tool_use_id": "call-shell", "cwd": root,
+            "tool_name": "exec_command",
+            "tool_input": {"command": "Get-Location"},
+        }, env)
+        codex_rc, codex_output = codex_reason(codex)
+        check("Codex shell receives structured deny",
+              codex_rc == 0 and
+              codex_output.get("permissionDecision") == "deny" and
+              "unisolated shell execution" in
+              str(codex_output.get("permissionDecisionReason") or ""),
+              (codex.returncode, codex.stdout[:180], codex.stderr[:100]))
+
+        source = Path(GUARD).read_text(encoding="utf-8")
+        needle = "    if tool in SHELL_TOOLS:\n        reason = ("
+        mutant_source = source.replace(
+            needle, "    if False and tool in SHELL_TOOLS:\n        reason = (", 1)
+        mutant = os.path.join(root, "workspace_write_guard_mutant.py")
+        Path(mutant).write_text(mutant_source, encoding="utf-8", newline="\n")
+        mutant_run = run_guard(mutant, {
+            "session_id": "mutant-reader", "prompt_id": "prompt-mutant",
+            "cwd": root, "tool_name": "PowerShell",
+            "tool_input": {"command": "Get-Location"},
+        }, env)
+        check("mutation: removing global shell gate turns acceptance red",
+              mutant_source != source and mutant_run.returncode == 0 and
+              not mutant_run.stderr.strip(),
+              (mutant_run.returncode, mutant_run.stdout[:100],
+               mutant_run.stderr[:160]))
+
+        owner = run_guard(GUARD, {
+            "session_id": "file-owner", "prompt_id": "prompt-owner",
+            "cwd": root, "tool_name": "Write",
+            "tool_input": {"file_path": victim},
+        }, env)
+        contender = run_guard(GUARD, {
+            "session_id": "file-contender", "prompt_id": "prompt-contender",
+            "cwd": root, "tool_name": "Edit",
+            "tool_input": {"file_path": victim},
+        }, env)
+        released = run_guard(GUARD, {
+            "session_id": "file-owner", "prompt_id": "prompt-owner",
+            "cwd": root}, env, "stop")
+        after_release = run_guard(GUARD, {
+            "session_id": "file-after", "prompt_id": "prompt-after",
+            "cwd": root, "tool_name": "Write",
+            "tool_input": {"file_path": victim},
+        }, env)
+        check("exact file tools retain acquire/conflict/fenced release",
+              owner.returncode == 0 and contender.returncode == 2 and
+              "file-owner" in contender.stderr and released.returncode == 0 and
+              after_release.returncode == 0,
+              (owner.returncode, contender.returncode, contender.stderr[:120],
+               released.returncode, after_release.returncode))
+
+        alias = os.path.join(root, "hardlink-alias.txt")
+        os.link(victim, alias)
+        hardlink_run = run_guard(GUARD, {
+            "session_id": "hardlink", "prompt_id": "prompt-hardlink",
+            "cwd": root, "tool_name": "Write",
+            "tool_input": {"file_path": alias},
+        }, env)
+        namespace_runs = []
+        for spelling in (
+                r"\\localhost\C$\Users\dev\victim.txt",
+                r"\\?\Volume{s_28aca884}\victim.txt",
+                r"\Device\HarddiskVolume1\victim.txt"):
+            namespace_runs.append(run_guard(GUARD, {
+                "session_id": "namespace", "prompt_id": "prompt-namespace",
+                "cwd": root, "tool_name": "Write",
+                "tool_input": {"file_path": spelling},
+            }, env))
+        check("path aliases fail closed before pathname leasing",
+              hardlink_run.returncode == 2 and
+              "hardlink aliases" in hardlink_run.stderr and
+              all(run.returncode == 2 and "unsafe-path-namespace" in run.stderr
+                  for run in namespace_runs) and sha(victim) == before,
+              (hardlink_run.returncode, hardlink_run.stderr[:120],
+               [(run.returncode, run.stderr[:100]) for run in namespace_runs]))
+
+        usage = [json.loads(line) for line in Path(counter).read_text(
+            encoding="utf-8").splitlines() if line.strip()]
+        blocked_shell = [row for row in usage
+                         if row.get("outcome") == "blocked-unisolated-shell"]
+        check("counter exposes every blocked shell call",
+              len(blocked_shell) == len(cases) + 1,
+              "blocked=%d expected=%d" %
+              (len(blocked_shell), len(cases) + 1))
+
+        race_target = os.path.join(root, "race.txt")
+        Path(race_target).write_text("race\n", encoding="utf-8")
+
+        def race(index):
+            return run_guard(GUARD, {
+                "session_id": "race-%d" % index,
+                "prompt_id": "race-turn-%d" % index,
+                "cwd": root, "tool_name": "Write",
+                "tool_input": {"file_path": race_target},
+            }, env)
+
+        with ThreadPoolExecutor(max_workers=8) as pool:
+            race_runs = list(pool.map(race, range(8)))
+        winners = [index for index, run in enumerate(race_runs)
+                   if run.returncode == 0]
+        losers = [run for run in race_runs if run.returncode == 2 and
+                  "BUSY" in run.stderr]
+        check("concurrent exact-file acquisition has exactly one winner",
+              len(winners) == 1 and len(losers) == 7,
+              [(run.returncode, run.stderr[:80]) for run in race_runs])
+        if winners:
+            winner = winners[0]
+            run_guard(GUARD, {
+                "session_id": "race-%d" % winner,
+                "prompt_id": "race-turn-%d" % winner,
+                "cwd": root}, env, "stop")
+
+        markers = [root, "claude-shell-", "codex-shell", "file-owner",
+                   "file-contender", "file-after", "hardlink", "namespace",
+                   "race-"]
+        production_leaks = []
+        for path, offset in production_offsets.items():
+            production_leaks.extend(new_matching_lines(path, offset, markers))
+        check("acceptance writes no attributable production telemetry",
+              not production_leaks, production_leaks[:5])
+
+    bad = [name for name, ok, _detail in RESULTS if not ok]
+    print("\nVERDICT: %s" % ("PASS" if not bad else "FAIL: " + "; ".join(bad)))
+    return 1 if bad else 0
+
+
+if __name__ == "__main__":
+    raise SystemExit(main())

---

**Claude:**

[⏰ 14:46, вторник, 22 сентября 2026]

🎙 Майк: это код-ревью запрос по diff — отвечаю прямо как независимый ревьюер, без флотской церемонии.

Review of the diff on stdin (lease-storm test rewrite + fail-closed shell acceptance test + entrypoint routing):

**Confirming the stated fixes:**
1. Config hashes (`sha(GUARD)`, `sha(this_file)`, `sha(CODEX_HOOKS)`, `sha(CLAUDE_SETTINGS)`) are computed inside the `try/except (OSError, ValueError)` block — a missing/unreadable config now fails clean via `check("harness configs are readable JSON", False, ...)` and an explicit early `return 1`, rather than throwing an unhandled exception. Confirmed.
2. Missing configs → clean FAIL: yes, the guarded block catches and reports before any pin comparison happens.
3. `_test_workspace_write_guard.py::main()` now computes and forwards all four SHA pins (`WORKSPACE_LEASE_TEST_EXPECTED_GUARD_SHA256/TEST/CODEX_CONFIG/CLAUDE_CONFIG_SHA256`) unconditionally before invoking the focused test as a subprocess, and the focused test compares them via `WORKSPACE_LEASE_TEST_REQUIRE_PIN=1`. Confirmed — `require_pin and expected_guard == actual_hashes["guard"] and ...` correctly requires all four to match.

These three items look solid and match what was asked.

**Remaining defects found:**

1. **Silent pin bypass when a config file doesn't exist.** In `_test_workspace_write_guard.py::main()`, the pin env vars are only set `if os.path.isfile(path)`. If `CODEX_HOOKS`/`CLAUDE_SETTINGS` don't exist on a given node, `WORKSPACE_LEASE_TEST_EXPECTED_CODEX_CONFIG_SHA256` is simply never set (stays empty string via `.lower()` default in the focused test). Meanwhile the focused test's own guarded `sha(CODEX_HOOKS)` call will throw `OSError` on the same missing file, hit the `except (OSError, ValueError)` branch, and correctly FAIL with "harness configs are readable JSON" — so in practice this is caught downstream, not a live hole. But it's fragile: the entrypoint's `isfile` guard silently produces an empty expected-hash string instead of failing itself, so the failure signal comes from the wrong layer (the focused test, not the caller that's supposed to snapshot pins). Low severity given the downstream catch, but worth tightening for clarity — not blocking.

2. **`new_matching_lines` marker collision risk is still theoretical but present.** Markers list includes bare `root` (a tempdir path) plus short tokens like `"race-"`, `"namespace"`, `"hardlink"`. If any *unrelated* concurrent production process happens to log a line containing the substring `"namespace"` or `"hardlink"` during the acceptance run, it gets misattributed as a leak. This is a minor false-positive risk in a shared-host CI, not a correctness defect in the fix under review — pre-existing pattern, not introduced by this diff's core changes.

3. **Mutant patch string match is brittle but self-checking.** The `source.replace(needle, ...)` in the fail-closed test asserts `mutant_source != source` before running, so if `GUARD`'s source ever reformats and the needle stops matching, the check itself fails loudly (mutation red-check becomes unreachable rather than silently passing) — this is correct fail-closed design, not a defect.

Neither #2 nor #3 rises to blocking; #1 is a minor robustness gap already covered by a downstream catch, not a live correctness bug. No high/medium defects survive review of the three specific fixes requested.

FINAL_VERDICT: APPROVE
