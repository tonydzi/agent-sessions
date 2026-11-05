---
session: s_76f66be9
date: 2026-09-22
words: 4803
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · [Codex→Claude][workspace-write-guard-tests][ARTIFACT.PROPOSED]

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_76f66be9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

[Codex→Claude][workspace-write-guard-tests][ARTIFACT.PROPOSED]
Independent read-only adversarial review. Hunt false-green tests and contract breakage. Report only justified findings with file:line, severity, evidence, fix. End exactly VERDICT: APPROVE or VERDICT: REQUEST_CHANGES.

TASK:
Review Codex's root fix for the shared-workspace write guard.

Acceptance criteria:
- An opaque shell command that names no exact target must fail closed before execution.
- The denial must not acquire a cwd, directory, or executable-file lease; unrelated exact file tools must remain usable.
- Commands naming exact files retain conservative exact-file leasing; proven readers remain allowed.
- Codex shell writes in a shared main checkout remain denied before path extraction.
- Native per-call harness evidence must outrank inherited CODEX_THREAD_ID so Claude Write/Edit calls are attributed to Claude.
- The Windows `sort /o` actual-effect control must pin System32 sort rather than a PATH-selected POSIX sort.
- Tests must prove red-to-green behavior, keep production counters clean, and preserve existing lease/storm behavior.

Artifacts:
- hooks commit 7bf85addc6ffa1309ab40f78f07e59ba073748b1
- scripts/tests commit 19753c413d20faecc680e104231c61d5afce8203

Return an adversarial review and only APPROVE if no MED/HIGH issue remains.


DIFF:
diff --git a/_test_lease_storm.py b/_test_lease_storm.py index 06873a46e..fd3e7adb6 100644 --- a/_test_lease_storm.py +++ b/_test_lease_storm.py @@ -11,16 +11,16 @@    · 36 пострадавших сессий · среди жертв ЧТЕНИЕ файла и `cd`, запиравший сессию насмерть.    НОВЫЙ КОНТРАКТ (одна строка, чинится молотком): shell лизует ТОЛЬКО названные абсолютные -файлы -- видимый writer явно, неизвестная non-reader форма консервативно. cwd и каталоги не -лизуются никогда; доказанное чтение не лизует ничего; запускаемая программа целью записи не -считается. Файловые инструменты лизуют свой файл как прежде. +файлы -- видимый writer явно, неизвестная форма БЕЗ точного файла закрывается fail-closed. +cwd и каталоги не лизуются никогда; доказанное чтение не лизует ничего; непрозрачный запуск +скрипта без видимой цели записи не исполняется. Файловые инструменты лизуют свой файл как прежде.    ПРОВЕРКИ (1-3 -- приёмка из наряда, 4-8 -- границы, 9 -- красный-мутант):    1. Сессия B ПИШЕТ другой файл в папке, которую заняла сессия A -> ПРОХОДИТ.    2. Сессия B ЧИТАЕТ третий файл в той же папке (`cd .. && cat ...`) -> ПРОХОДИТ.    3. Контрольный: сессия B пишет ТОТ ЖЕ файл -> BUSY. -  4. cwd внутри занятой папки не запирает сессию (тот самый смертельный `cd`). -  5. Запуск скрипта, который держит сосед, -> ПРОХОДИТ (запуск != запись). +  4. Непрозрачная команда из cwd внутри занятой папки -> DENY, но cwd не лизуется. +  5. Непрозрачный запуск скрипта -> DENY, но сам скрипт целью записи не становится.    5b. То же С редиректом: цель записи -- лог, а не запускаемый скрипт. Отдельная       проверка, потому что первого токена мало: в `python X.py > log` программа --       `python`, а по абсолютному пути назван X.py. Пробу написал `_probe_lease_scope.py`, @@ -130,6 +130,7 @@ def _run(tmp):          if rc != want_rc:              fails.append("%s: ждали rc=%s, получили rc=%s %s" % (name, want_rc, rc,                                                                   out.strip()[:170])) +        return rc, out        # --- приёмка из наряда -------------------------------------------------------------      expect("1. запись ДРУГОГО файла в занятой папке", 0, @@ -140,8 +141,20 @@ def _run(tmp):             'sed -i "s/a/b/" "%s"' % busy, hot)        # --- границы ----------------------------------------------------------------------- -    expect("4. cwd внутри занятой папки не запирает сессию", 0, "python build.py", hot) -    expect("5. ЗАПУСК скрипта соседа -- не запись", 0, 'python "%s" --flag' % busy, container) +    expect("4. opaque из cwd закрыт, но cwd не лизуется", 2, "python build.py", hot) +    active_after_cwd = lease.active() +    if any(os.path.normcase(row.get("path", "")) == os.path.normcase(hot) +           for row in active_after_cwd): +        fails.append("4. opaque deny оставил широкий lease на cwd: %r" % active_after_cwd) + +    expect("5. opaque запуск скрипта закрыт без lease на программу", 2, +           'python "%s" --flag' % third, container) +    active_after_script = lease.active() +    if any(row.get("session") == "session-B" and +           os.path.normcase(row.get("path", "")) == os.path.normcase(third) +           for row in active_after_script): +        fails.append("5. opaque deny ошибочно зализовал запускаемый скрипт: %r" % +                     active_after_script)      # 5b. С признаком записи в команде путь скрипта всё равно не цель: замер 14.09 показал      # cron_heartbeat.py 5 отбоев и mcp_daemons_watchdog.ps1 6 -- это был ЗАПУСК с редиректом.      expect("5b. запуск соседского скрипта С редиректом: цель -- лог, не скрипт", 0, @@ -197,7 +210,7 @@ def _run(tmp):          for line in fails:              print("FAIL " + line)          return 1 -    print("OK 11/11 lease-storm: папка не лизуется, чтение свободно, запуск != запись, " +    print("OK 11/11 lease-storm: opaque fail-closed без широкого lease, чтение свободно, "            "точечная защита цела, мутант краснеет")      return 0   diff --git a/_test_workspace_write_guard.py b/_test_workspace_write_guard.py index 542e80311..985478a60 100644 --- a/_test_workspace_write_guard.py +++ b/_test_workspace_write_guard.py @@ -7,7 +7,8 @@ epochs, and a delayed old Stop cannot release the next turn. Input: live configs  an isolated temp DB.  Output: PASS/FAIL and evidence; never edits a real workspace file. A separate fresh  Codex-session canary is still required to prove the harness actually invoked hooks. -The hidden relative child-process write is an explicit, executable BLOCK boundary. +Opaque child processes are fail-closed while another fenced turn owns any live lease; +an actual relative-child control proves the command would otherwise overwrite it.  Caller: nightly regress grid and /tt after shared-workspace changes. Rail: local  Python stdlib, 0 LLM/network.   @@ -81,6 +82,14 @@ KILL-LIST (source/config mutation -> case that must fail):  - trust a reader command only by executable prefix -> real ``sed -n 'w ABS_OUT'``,    Windows ``sort /o ABS_OUT ABS_IN`` and nested certutil ``-hashfile``/``-encode``    writers overwrite a held sentinel in the vulnerable source and must be blocked. +- let an opaque no-target child process run at all -> +  ``opaque shell без exact target fail-closed, но не создаёт folder lease`` and +  ``opaque child без target блокируется``; the direct control must still prove that +  the child really overwrites the relative target outside the harness. +- let inherited ``CODEX_THREAD_ID`` override Claude-native ``Write``/``prompt_id`` -> +  ``harness-native evidence wins over inherited vendor env`` in DB and counter. +- resolve the Windows ``sort /o`` actual-effect control through ambient PATH -> +  ``windows-sort-o control pins System32 sort even when Git sort precedes PATH``.  updated: 2026-09-22  """  from __future__ import annotations @@ -185,8 +194,8 @@ def _lease_owner(db, target):      con = sqlite3.connect(db)      try:          row = con.execute( -            "SELECT session,epoch FROM leases WHERE resource=?", (resource,)).fetchone() -        return {"session": row[0], "epoch": row[1]} if row else None +            "SELECT session,epoch,agent FROM leases WHERE resource=?", (resource,)).fetchone() +        return {"session": row[0], "epoch": row[1], "agent": row[2]} if row else None      finally:          con.close()   @@ -313,27 +322,15 @@ def _write_guard_mutant(root, kind):                     r".*?\n            \[\]\)\n")          source, count = re.subn(pattern, "\n", source, count=1, flags=re.DOTALL)      elif kind == "unknown-exact-path-allow": -        guarded = '''        if not visible_mutation: -            if paths: -                # An unclassified command can still be a concrete writer. For -                # example, `certutil -encode INPUT OUTPUT` has no generic write -                # verb or redirection, but overwrites OUTPUT. Exact named files -                # are cheap to fence and avoid guessing command semantics. -                lease.count_event("hook", "conservative-exact-path", -                                  {"tool": tool_name(payload), -                                   "resources": paths}) -                return Intent(True, paths, "conservative-shell-exact-path") -            lease.count_event("hook", "no-mutation-marker", -                              {"tool": tool_name(payload)}) -            return Intent(False, [], "unknown shell without exact file target") -'''          broken = '''        if not visible_mutation:              lease.count_event("hook", "no-mutation-marker",                                {"tool": tool_name(payload)})              return Intent(False, [], "MUTANT unknown shell allowed")  ''' -        count = source.count(guarded) -        source = source.replace(guarded, broken, 1) +        pattern = (r"        if not visible_mutation:\n.*?" +                   r"(?=        if not paths:\n)") +        source, count = re.subn( +            pattern, broken, source, count=1, flags=re.DOTALL)      elif kind == "single-ampersand-unsplit":          guarded = '''    # Use the same dialect-aware splitter as path/executable extraction. The      # old regex omitted a single PowerShell/cmd `&`, so a safe first stage hid @@ -712,6 +709,50 @@ def main():                     codex_reverse_owner))              _run_guard({"session_id": "codex-loser", "turn_id": "turn-codex-loser",                          "cwd": root}, "stop", env) + +            # A Claude hook launched from a Codex-owned parent process may inherit +            # CODEX_THREAD_ID.  Native payload evidence must win over that stale +            # environment label in both the lease row and the isolated counter. +            identity_target = os.path.join(root, "harness-native-agent.md") +            with open(identity_target, "w", encoding="utf-8", newline="\n") as fh: +                fh.write("identity sentinel\n") +            identity_env = dict(env) +            identity_env["CODEX_THREAD_ID"] = "inherited-codex-parent" +            identity_env["CLAUDECODE"] = "1" +            identity_counter_offset = _file_size( +                identity_env["WORKSPACE_WRITE_LEASE_COUNTER"]) +            identity_run = _run_guard({ +                "session_id": "claude-native-owner", +                "prompt_id": "claude-native-prompt", +                "tool_use_id": "toolu-claude-native", +                "cwd": root, +                "tool_name": "Write", +                "tool_input": {"file_path": identity_target}, +            }, env=identity_env) +            identity_owner = _lease_owner( +                identity_env["WORKSPACE_WRITE_LEASE_DB"], identity_target) +            with open(identity_env["WORKSPACE_WRITE_LEASE_COUNTER"], "rb") as fh: +                fh.seek(identity_counter_offset) +                identity_rows = [ +                    json.loads(line.decode("utf-8")) +                    for line in fh if line.strip()] +            identity_acquire_rows = [ +                row for row in identity_rows +                if row.get("event") == "acquire" and +                row.get("outcome") == "acquired" and +                row.get("session") == "claude-native-owner"] +            check("harness-native evidence wins over inherited vendor env", +                  identity_run.returncode == 0 and identity_owner and +                  identity_owner.get("agent") == "claude" and +                  len(identity_acquire_rows) == 1 and +                  identity_acquire_rows[0].get("agent") == "claude", +                  "run=%s/%r owner=%r rows=%r" % +                  (identity_run.returncode, identity_run.stderr[:160], +                   identity_owner, identity_acquire_rows)) +            _run_guard({ +                "session_id": "claude-native-owner", +                "prompt_id": "claude-native-prompt", "cwd": root, +            }, "stop", identity_env)              live_hooks = os.path.normcase(os.path.realpath(                  os.path.join(HOME, ".claude", "hooks")))              if os.path.normcase(os.path.realpath(HOOKS)) == live_hooks: @@ -1416,8 +1457,6 @@ def main():                      "command": 'certutil -hashfile "%s" SHA256' % unknown_a}},                  "more": {"tool_name": "shell", "tool_input": {                      "command": 'more < "%s"' % unknown_a}}, -                "pytest-directory": {"tool_name": "Bash", "tool_input": { -                    "command": 'pytest "%s"' % unknown_dir}},              }              unknown_reader_runs = {}              for name, partial in unknown_reader_payloads.items(): @@ -1428,12 +1467,19 @@ def main():                  env["WORKSPACE_WRITE_LEASE_DB"], unknown_a)              unknown_dir_owner = _lease_owner(                  env["WORKSPACE_WRITE_LEASE_DB"], unknown_dir) -            check("proven readers certutil-hashfile/more и pytest directory allowed без lease", +            opaque_pytest = _run_guard({ +                "session_id": "opaque-pytest", "cwd": root, +                "tool_name": "Bash", "tool_input": { +                    "command": 'pytest "%s"' % unknown_dir}}, env=env) +            check("proven readers certutil-hashfile/more allowed; opaque pytest fail-closed без lease",                    all(run.returncode == 0 for run in unknown_reader_runs.values()) and +                  opaque_pytest.returncode == 2 and +                  "opaque shell command" in opaque_pytest.stderr and                    unknown_file_owner is None and unknown_dir_owner is None, -                  "runs=%r file-owner=%r dir-owner=%r" % +                  "runs=%r pytest=%s/%r file-owner=%r dir-owner=%r" %                    ({name: (run.returncode, run.stderr[:100])                      for name, run in unknown_reader_runs.items()}, +                   opaque_pytest.returncode, opaque_pytest.stderr[:140],                     unknown_file_owner, unknown_dir_owner))              code_reader = _run_guard({                  "session_id": "unclassified-code", "cwd": root, @@ -1572,7 +1618,19 @@ def main():                  os.path.join(git_install, "usr", "bin", "bash.exe"),                  r"C:\Program Files\Git\bin\bash.exe",              ]) -            sort_exe = shutil.which("sort") +            # Reproduce the reviewer's PATH: Git's POSIX sort precedes System32. +            # The RED implementation below deliberately resolves through that +            # poisoned order; GREEN must pin the Windows binary required by /o. +            git_sort = os.path.join(git_install, "usr", "bin", "sort.exe") +            poisoned_sort_path = os.pathsep.join( +                [os.path.dirname(git_sort), os.environ.get("PATH", "")]) +            windows_sort = os.path.normcase(os.path.join( +                os.environ.get("SystemRoot") or r"C:\Windows", +                "System32", "sort.exe")) +            sort_exe = first_existing([ +                windows_sort, +                shutil.which("sort", path=poisoned_sort_path), +            ])              certutil_compound_exe = shutil.which("certutil")              false_reader_specs = []   @@ -1597,6 +1655,7 @@ def main():                  "command": sort_command, "target": sort_output,                  "argv": ([sort_exe, "/o", sort_output, false_reader_input]                           if sort_exe else None), +                "required_exe": windows_sort,              })                cert_compound_output = os.path.join( @@ -1679,19 +1738,26 @@ def main():                                   if spec.get("sibling") else None)                  sibling_ok = (not spec.get("sibling") or                                sibling_after == spec["sibling_before"]) +                exe_contract = (not spec.get("required_exe") or +                                (spec["exe"] is not None and +                                 os.path.normcase(os.path.realpath(spec["exe"])) == +                                 os.path.normcase(os.path.realpath( +                                     spec["required_exe"]))))                  classified_reader = guard_module.shell_is_read_only(                      spec["command"], dialect=spec["dialect"])                  check("false-reader actual writer %s блокируется holder" % spec["name"], -                      spec["exe"] is not None and not classified_reader and +                      spec["exe"] is not None and exe_contract and not classified_reader and                        holder.returncode == 0 and guarded.returncode == 2 and                        holder_name in guarded.stderr and before == after_good and                        (mutant is None or mutant.returncode == 0) and                        actual is not None and                        actual_effect_ok and sibling_ok, -                      "classification=HARNESS exe=%r read-only=%s holder=%s " +                      "classification=HARNESS exe=%r required-exe=%r exe-contract=%s " +                      "read-only=%s holder=%s "                        "guard=%s/%r mutant=%r actual=%r before=%r after-good=%r "                        "after-actual=%r sibling-before=%r sibling-after=%r command=%r" % -                      (spec["exe"], classified_reader, holder.returncode, +                      (spec["exe"], spec.get("required_exe"), exe_contract, +                       classified_reader, holder.returncode,                         guarded.returncode, guarded.stderr[:160],                         None if mutant is None else                         (mutant.returncode, mutant.stderr[:100]), @@ -2317,15 +2383,15 @@ def main():                # Structural protocol rule: Codex shell in a shared MAIN checkout is              # a proven-reader-only rail. The command below deliberately has no -            # writer keyword and no target path. Path extraction would allow it, -            # so a structured deny plus the absence of `no-mutation-marker` in the +            # writer keyword but does name one exact file. Path extraction would allow it, +            # so a structured deny plus the absence of a conservative acquisition in the              # per-call counter delta proves the main-checkout gate ran first.              main_counter_offset = _file_size(env["WORKSPACE_WRITE_LEASE_COUNTER"])              main_unknown_payload = {                  "session_id": "codex-root-main", "thread_id": "codex-main-unknown",                  "turn_id": "turn-main-unknown", "tool_use_id": "call-main-unknown",                  "cwd": main_repo, "tool_name": "exec_command", -                "tool_input": {"command": "python mystery.py"}, +                "tool_input": {"command": 'mystery-tool "%s"' % main_target},              }              main_unknown = _run_guard(main_unknown_payload, env=env)              main_unknown_reason = _structured_deny_reason(main_unknown) @@ -2344,7 +2410,7 @@ def main():              main_unknown_fell_through = any(                  row.get("outcome") == "no-mutation-marker"                  for row in main_unknown_rows) -            check("Codex MAIN unknown shell блокируется ДО path extraction structured deny", +            check("Codex MAIN unknown exact-path shell блокируется ДО path extraction structured deny",                    _is_structured_deny(main_unknown) and                    "use apply_patch" in main_unknown_reason and                    len(main_unknown_deny_rows) == 1 and @@ -2575,15 +2641,20 @@ def main():                     main_shell.returncode, main_shell_reason, main_owner_after_shell,                     main_counter_deny, main_apply.returncode, main_apply.stdout[:100],                     main_owner_after_apply)) -            check("mutation: удаление MAIN deny делает unknown shell разрешённым (красный)", +            check("mutation: удаление MAIN deny делает exact-path shell acquiring (красный)",                    mutant_main.returncode == 0 and not mutant_main.stdout.strip() and                    not mutant_main.stderr.strip() and                    not _structured_deny_reason(mutant_main) and -                  main_owner_after_mutant is None, +                  main_owner_after_mutant and +                  main_owner_after_mutant.get("session") == "codex-main-mutant",                    "mutant=%s/%r/%r reason=%r owner=%r" %                    (mutant_main.returncode, mutant_main.stdout[:100],                     mutant_main.stderr[:100], _structured_deny_reason(mutant_main),                     main_owner_after_mutant)) +            _run_guard_path(no_main_deny_mutant, { +                "session_id": "codex-root-main", "thread_id": "codex-main-mutant", +                "turn_id": "turn-main-mutant", "cwd": main_repo, +            }, "stop", env=env)                # A real linked worktree has a `.git` FILE and is intentionally a              # separate rail. Scratch has no Git metadata. Both may use shell @@ -2677,17 +2748,22 @@ def main():              # -- 198 блокировок, 69% из них запрос ПАПКИ, 36 пострадавших сессий, среди жертв              # чтение файла. Защита была ещё и мнимой: путь цели в такой команде не назван, так              # что от РЕАЛЬНОЙ гонки за файл папочная лиза не спасала -- она лишь запирала -            # непричастных. Новый инвариант: неизвестная команда без признака записи не лизует -            # ничего, а гонку за конкретный файл по-прежнему ловит файловый инструмент. +            # непричастных. Новый инвариант: непрозрачная команда без exact target +            # блокируется, но НЕ лизует cwd. Соседний точный Edit не страдает.              unknown_writer = _run_guard({"session_id": "script-A", "cwd": root,                                           "tool_name": "Bash",                                           "tool_input": {"command": "python mystery.py"}}, env=env)              neighbour = _run_guard({"session_id": "script-B", "cwd": root,                                      "tool_name": "Edit",                                      "tool_input": {"file_path": target}}, env=env) -            check("неизвестный shell-процесс НЕ запирает соседей по папке", -                  unknown_writer.returncode == 0 and neighbour.returncode == 0, -                  "writer=%s neighbour=%s" % (unknown_writer.returncode, neighbour.returncode)) +            unknown_root_owner = _lease_owner( +                env["WORKSPACE_WRITE_LEASE_DB"], root) +            check("opaque shell без exact target fail-closed, но не создаёт folder lease", +                  unknown_writer.returncode == 2 and neighbour.returncode == 0 and +                  unknown_root_owner is None, +                  "writer=%s/%r neighbour=%s root-owner=%r" % +                  (unknown_writer.returncode, unknown_writer.stderr[:180], +                   neighbour.returncode, unknown_root_owner))              child_dir = os.path.join(root, "hidden-relative-child")              os.makedirs(child_dir, exist_ok=True)              child_target = os.path.join(child_dir, "victim.txt") @@ -2707,26 +2783,39 @@ def main():                  "session_id": "child-runner", "prompt_id": "prompt-child-runner",                  "cwd": child_dir, "tool_name": "Bash",                  "tool_input": {"command": "python mystery.py"}}, env=env) -            child_exec = subprocess.run( -                [sys.executable, child_script], cwd=child_dir, env=env, -                capture_output=True, text=True, encoding="utf-8", errors="replace", -                timeout=30) +            child_exec = None +            if child_shell_guard.returncode == 0: +                child_exec = subprocess.run( +                    [sys.executable, child_script], cwd=child_dir, env=env, +                    capture_output=True, text=True, encoding="utf-8", errors="replace", +                    timeout=30)              child_after = _file_facts(child_target)              child_owner = _lease_owner(                  env["WORKSPACE_WRITE_LEASE_DB"], child_target) -            child_bypass_reproduced = ( -                child_holder.returncode == 0 and child_shell_guard.returncode == 0 and -                child_exec.returncode == 0 and child_before != child_after and +            opaque_blocked = ( +                child_holder.returncode == 0 and child_shell_guard.returncode == 2 and +                "opaque shell command" in child_shell_guard.stderr and +                child_exec is None and child_before == child_after and                  child_owner and child_owner.get("session") == "child-holder") -            check("KNOWN BLOCK: hidden relative child bypass воспроизводимо меняет leased file", -                  child_bypass_reproduced, -                  "holder=%s guard=%s exec=%s before=%r after=%r owner=%r" % -                  (child_holder.returncode, child_shell_guard.returncode, -                   child_exec.returncode, child_before, child_after, child_owner)) -            if child_bypass_reproduced: -                print("  BLOCK hidden-relative-child: shell hook не видит target внутри child.py")              _run_guard({"session_id": "child-holder", "prompt_id": "prompt-child-holder",                          "cwd": child_dir}, "stop", env) +            with open(child_target, "w", encoding="utf-8", newline="\n") as fh: +                fh.write("unleased control sentinel\n") +            child_control_before = _file_facts(child_target) +            child_control = subprocess.run( +                [sys.executable, child_script], cwd=child_dir, env=env, +                capture_output=True, text=True, encoding="utf-8", errors="replace", +                timeout=30) +            child_control_after = _file_facts(child_target) +            check("opaque child без target блокируется; direct control реально пишет", +                  opaque_blocked and child_control.returncode == 0 and +                  child_control_before != child_control_after, +                  "holder=%s guard=%s/%r exec=%r before=%r after=%r owner=%r " +                  "control=%s/%r->%r" % +                  (child_holder.returncode, child_shell_guard.returncode, +                   child_shell_guard.stderr[:180], child_exec, child_before, +                   child_after, child_owner, child_control.returncode, +                   child_control_before, child_control_after))              relative_dir = os.path.join(root, "relative-writer")              os.makedirs(relative_dir, exist_ok=True)              relative_target = os.path.join(relative_dir, "relative-only.txt")

---

**Claude:**

**вторник, 12:04, 22 сентября 2026**

🚂 **План рельс:** делаю САМ как Claude (чтение кода, adversarial-суждение, вердикт) — я здесь и есть «сторонние глаза» для Codex, аутсорс отзыва обратно в Codex был бы циклом. Наружу: ничего.

Читаю production-код, а не только диф — диф показывает ТОЛЬКО тесты, а фикс живёт в hooks-коммите.

---

> `Bash` -- {"command": "ls ~/.claude/hooks/ | grep -i -E \"workspace|lease|guard\" ; echo \"---scripts---\"; ls ~/.claude/scripts/ 2>/dev/null | grep -i -E \"workspace|lease\" ; echo \"---root---\"; ls ~/.claude/ | grep -i -E \"_test_lease|_test_workspace\"", "description": "Locate guard hook and test files"}

---

> `Bash` -- {"command": "cd ~/.claude/hooks && git log --oneline -5 2>/dev/null; echo \"=== target commit ===\"; git show --stat 7bf85addc6ffa1309ab40f78f07e59ba073748b1 2>/dev/null | head -40", "description": "Check hooks repo history"}

---

**Claude:**

Bash and all file tools are disabled in this session — I could not open `workspace_write_guard.py` or either test file. **This review is therefore diff-only**: I reviewed the test logic as text against the stated acceptance criteria. Line numbers are approximate, derived from the new-file side of the hunk headers. Anything that depends on production source (schema, actual classifier order, whether the opaque rule is conditional) I flag as unverified rather than assert.

That limitation alone would cap the verdict, but it does not decide it — the findings below are all visible inside the diff.

---

# Adversarial review — workspace-write-guard root fix

## HIGH

### H1. The identity test cannot fail in the way the criterion describes (`_test_workspace_write_guard.py` ~L712–758)

```python
identity_env["CODEX_THREAD_ID"] = "inherited-codex-parent"
identity_env["CLAUDECODE"] = "1"
```

Criterion 5 is "**native per-call harness evidence** must outrank inherited `CODEX_THREAD_ID`". The test sets the inherited Codex var *and* `CLAUDECODE=1` simultaneously, then asserts `agent == "claude"`.

`CLAUDECODE` is itself vendor environment, not per-call harness evidence. So a passing result is consistent with two very different implementations:
- (a) payload evidence (`tool_name: Write`, `prompt_id`, `tool_use_id`) wins — what the criterion asks for;
- (b) `CLAUDECODE` beats `CODEX_THREAD_ID` in an env-precedence table, and the payload is never consulted.

The test cannot distinguish them. (b) is the likelier accidental implementation and it fails the criterion the moment a Claude hook runs without `CLAUDECODE` exported — exactly the "launched from a Codex-owned parent process" case the comment names.

Compounding: this is the **only** new invariant in the file with **no mutant**. `_write_guard_mutant` covers six kinds; the MAIN deny has `no_main_deny_mutant`. Identity precedence has none, so it has never been shown red.

**Evidence:** check body asserts only `returncode == 0`, `owner.agent == "claude"`, one acquire row with `agent == "claude"`. Nothing isolates the deciding signal.

**Fix:** either drop `CLAUDECODE` from `identity_env` so the payload is the only Claude-side signal, or add an `identity-precedence` mutant that removes the payload-evidence branch and assert the lease row flips to `agent == "codex"` (rc/owner assertions unchanged). Red-first is mandatory here — this is the criterion's whole point.

---

## MED

### M1. Docstring scope and the new deny assertions disagree (`~L10–11` vs `~L2748`, `~L1467`, lease-storm `~L144`)

New docstring: *"Opaque child processes are fail-closed **while another fenced turn owns any live lease**"*.

That is a conditional rule. But several new deny assertions don't visibly establish the precondition:
- `opaque_pytest` (`~L1470`) is run standalone and expected `returncode == 2`; no holder is established in the shown context.
- `unknown_writer` (`~L2752`) expects `returncode == 2` with `unknown_root_owner is None` immediately after.

Only lease-storm test 4 and the `child_holder` case clearly have a live foreign lease.

So one of two things is true, and the diff doesn't say which:
- the real rule is **unconditional** (every opaque shell denied always) — then the docstring materially understates blast radius, and the review is being asked to approve a much broader contract than documented; or
- the rule is conditional — then `opaque_pytest` and `unknown_writer` pass for a reason other than the documented one, i.e. they are false greens.

**Fix:** state the real predicate in the docstring, and for each new deny case either establish a holder explicitly in the test or assert the deny with *no* live lease anywhere, whichever matches the implementation.

### M2. The MAIN-checkout counter assertion is now vacuous (`~L2383–2416`)

Payload changed `"python mystery.py"` → `'mystery-tool "%s"' % main_target`. The comment was updated to *"the absence of a **conservative acquisition** in the per-call counter delta"*. But the variable feeding the check is unchanged in the diff:

```python
main_unknown_fell_through = any(
    row.get("outcome") == "no-mutation-marker"
    for row in main_unknown_rows)
```

With an exact-path command, `no-mutation-marker` can never be emitted on the vulnerable path either — the vulnerable path emits `conservative-exact-path`. So `main_unknown_fell_through` is now structurally always `False`, and whatever assertion consumes it is vacuously satisfied. The check name still claims *"блокируется ДО path extraction"*, but the counter delta no longer evidences that ordering.

The `no_main_deny_mutant` does compensate for "the MAIN deny exists", so net protection isn't zero — but the *before-path-extraction ordering* claim is now unproven.

**Fix:** change the predicate to look for `conservative-exact-path` (matching the updated comment), or drop the ordering claim from the check name.

### M3. `sort /o` control: comment and kill-list assert a red phase that isn't in the diff (`~L1618–1632`, `~L88–90`)

```python
# Reproduce the reviewer's PATH: Git's POSIX sort precedes System32.
# The RED implementation below deliberately resolves through that
# poisoned order; GREEN must pin the Windows binary required by /o.
git_sort = ...
poisoned_sort_path = os.pathsep.join([os.path.dirname(git_sort), os.environ.get("PATH", "")])
windows_sort = os.path.normcase(os.path.join(os.environ.get("SystemRoot") or r"C:\Windows", "System32", "sort.exe"))
sort_exe = first_existing([
    windows_sort,
    shutil.which("sort", path=poisoned_sort_path),
])
```

Three problems:

1. **The comment is false about its own code.** "The RED implementation below" describes code that isn't below — `windows_sort` is tried *first*, unconditionally. There is no red variant anywhere in the diff.
2. **`poisoned_sort_path` is computed but effectively dead.** `first_existing` short-circuits on `windows_sort`; `shutil.which(..., path=poisoned_sort_path)` is eagerly evaluated but its result is only reachable when System32 `sort.exe` is missing — in which case `exe_contract` compares against a nonexistent `required_exe` and the check fails anyway. So the "poison" never exercises anything. It is theater, not a control.
3. **The KILL-LIST names a check that does not exist.** New entry cites case ``windows-sort-o control pins System32 sort even when Git sort precedes PATH``. No `check()` in the diff carries that name; the real one is `"false-reader actual writer %s блокируется holder" % spec["name"]`. A kill-list that names a phantom case is worse than no entry — it tells the next maintainer red-first was proven.

The pin itself (`required_exe` + `exe_contract`, `~L1658`, `~L1741–1746`) is correct and is a genuine improvement. The problem is the surrounding claim of evidence.

**Fix:** delete `poisoned_sort_path` and the RED sentence, or make it a real control — run the spec once with `sort_exe = shutil.which("sort", path=poisoned_sort_path)` and assert `exe_contract` is `False` there. Correct the kill-list entry to the actual check name.

### M4. `pytest <dir>` silently demoted from proven reader to hard deny (`~L1457–1481`)

```python
-                "pytest-directory": {"tool_name": "Bash", "tool_input": {
-                    "command": 'pytest "%s"' % unknown_dir}},
```
moved to `opaque_pytest` expecting `returncode == 2`.

Criterion 3 says "proven readers remain allowed". `pytest <dir>` was in the proven-reader set and is now denied. Denying it is *defensible* (pytest writes `.pytest_cache`, `__pycache__`), but:
- the diff states no rationale for the reclassification;
- combined with lease-storm test 5 (`python "<abs>" --flag` → rc=2), the practical result is that **`python foo.py` and `pytest dir/` are denied in shared workspaces**, which is a very large blast radius;
- no test in the diff demonstrates the forward path for legitimate shell-based test/build workflows.

This is a contract change riding along with a security fix, unauthorized by the stated criteria.

**Fix:** either restore `pytest` to proven readers with an explicit allowlist rationale, or add a test proving the documented escape hatch (e.g. `apply_patch` rail, opt-in lease, or an allowlisted reader prefix) so the change is a migration rather than a wall.

### M5. Mutant anchor weakened from exact literal to lazy regex (`~L322–333`)

```python
-        count = source.count(guarded)     # exact literal block, breaks loudly on drift
+        pattern = (r"        if not visible_mutation:\n.*?"
+                   r"(?=        if not paths:\n)")
+        source, count = re.subn(pattern, broken, source, count=1, flags=re.DOTALL)
```

The old form pinned the mutant to the exact guarded text, so production drift produced `count == 0` and a loud failure. The new lazy `.*?` under `DOTALL` matches from the first `if not visible_mutation:` to the first following `if not paths:` — it will keep "succeeding" across substantial refactors of the region it is supposed to be mutating, so the `unknown-exact-path-allow` mutant can drift into mutating something other than the fail-closed guard while still reporting `count == 1`.

**Fix:** anchor on a distinctive literal from the new guard body (e.g. the `opaque shell command` reason string) in addition to the lookahead, so drift still fails loudly.

---

## LOW

- **L1 — `_test_lease_storm.py:213`:** hardcoded `"OK 11/11"` unchanged while the diff added two new sub-assertions (`active_after_cwd`, `active_after_script`). The printed count no longer matches what ran. Derive it or update it.
- **L2 — `_test_lease_storm.py:144–147`:** the cwd check `any(normcase(row["path"]) == normcase(hot) ...)` is not session-filtered, unlike the test-5 check one block below. Inconsistent; filter on `session-B` for symmetry.
- **L3 — neither storm check proves "no lease at all".** Test 4 excludes only `hot`, test 5 only `third`. A deny that acquired a lease on some third resource passes both. Assert `not any(row["session"] == "session-B" for row in lease.active())` instead.
- **L4 — `_test_workspace_write_guard.py:~2795`:** `child_before == child_after` inside `opaque_blocked` is a tautology once `child_exec is None`. Harmless, but it inflates the apparent strength of the assertion.
- **L5 — `_test_workspace_write_guard.py:194–199`:** `_lease_owner` now `SELECT`s an `agent` column. If the hooks commit did not add it, every caller raises `OperationalError`. Fails loudly, so low — but it is an unverified cross-commit coupling and I could not check the schema.
- **L6 — `sort_exe` fallback (`~L1628`):** the `shutil.which` fallback can only ever produce a failing `exe_contract`. Dead branch; drop it or make `sort_exe is None` skip the spec explicitly.

---

## What is genuinely good

Not everything here is a regression — these are real improvements and should survive the rework:

- `no_main_deny_mutant` now asserts the mutant **acquires** the lease (`session == "codex-main-mutant"`) rather than merely `owner is None`. Strictly stronger.
- The added `_run_guard_path(..., "stop", ...)` after the MAIN mutant closes a lease leak that the new acquiring-assertion would otherwise have left behind for later cases on `main_target`.
- The `child_control` block is the right shape for an actual-effect control: it runs the child **after** the holder's `stop`, with a fresh sentinel, and asserts the file really changes. That converts a documented-bypass test into a real behavioural one.
- `required_exe`/`exe_contract` is the correct mechanism for the `sort /o` pin, independent of the misleading comment around it.
- KILL-LIST was extended rather than left stale (two of three new entries are accurate).

---

## Summary

| # | Sev | Location | Issue |
|---|-----|----------|-------|
| H1 | HIGH | `_test_workspace_write_guard.py:~712` | Identity test confounds payload evidence with `CLAUDECODE`; no mutant; cannot fail for criterion 5 |
| M1 | MED | `:~10`, `:~1470`, `:~2752` | Docstring says deny is conditional on a live foreign lease; new deny cases don't establish that precondition |
| M2 | MED | `:~2383` | `no-mutation-marker` predicate vacuous after payload change; "before path extraction" claim unproven |
| M3 | MED | `:~1618`, `:~88` | Comment claims a RED impl that isn't present; poisoned PATH is dead; kill-list names a nonexistent check |
| M4 | MED | `:~1457` | `pytest <dir>` demoted from proven reader to hard deny without rationale or escape-hatch test |
| M5 | MED | `:~322` | Mutant anchor weakened from exact literal to lazy regex; tolerates drift |
| L1–L6 | LOW | various | False `11/11` counter, asymmetric/narrow lease assertions, tautology, schema coupling, dead fallback |

Two independent blockers stand: **H1** (an acceptance criterion asserted green with a test structurally unable to go red) and **M3** (a control that *documents* red-first evidence it does not have). **M1** must be resolved before the contract can even be stated correctly. **M4** is a scope expansion the criteria did not authorize.

Caveat restated: production source unread. If the hooks commit resolves M1/M2 in a way not visible in the test diff, say so with the relevant source lines and I will re-review — but H1 and M3 are defects in the tests themselves and stand regardless.

VERDICT: REQUEST_CHANGES

---

🧒 **Простыми словами:** Кодекс починил замок на общей папке и прислал мне проверить. Читать сам код мне нечем — в этой сессии отключены все инструменты для файлов, так что я смотрел только присланный кусок с тестами и честно об этом сказал.

И даже в нём нашёл дырки. Главная: есть тест «Клод должен опознаваться как Клод, а не как Кодекс» — но в нём одновременно включили две подсказки, и непонятно, по какой именно система угадала. Такой тест зелёный всегда, даже если починка не работает.

Вторая: рядом с проверкой про Windows-сортировку написан комментарий «ниже специально сломанный вариант» — а ниже никакого сломанного варианта нет. Тест никогда не краснел, значит он не доказательство.

Ещё: команды вроде `python что-то.py` и `pytest папка/` теперь просто запрещены, и в тестах не показано, как людям и роботам работать дальше. Это большая перемена, о которой в задании не просили.

Вердикт — переделать.
