---
session: s_7c9095d0
date: 2026-09-23
words: 2698
turns: 2
tools: "Bash, Edit, Glob, Grep, PowerShell, Read, ToolSearch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · Scheduled run: auto-hub-260824-NODE-0X-folder-cleanup

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7c9095d0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260824-NODE-0X-folder-cleanup" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260824-NODE-0X-folder-cleanup\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первой строкой: mcp__ccd_session_mgmt__set_session_title(session_id=self, title="⚙️ разлогины-chrome-ff-чинилка").

ЗАДАЧА ОТ оператора (голосом, 23.09.2026 ~04:35, дословно): «Подними, пожалуйста, отдельно сессию, которая починит, чтобы не разлогинировались все мои хромы и Firefox, а то у нас какой-то робот ходит и все куки удаляет, и все логины удаляет».

Это сессия-РАССЛЕДОВАНИЕ + починка класса, не симптома (§5.2). Порядок:

1. RECALL: память meta-session-dies-when-copied-to-robot (22.09: один xs-cookie в двух профилях, Meta гасит сессию серверно; в куки-гварде не было facebook; chrome-щит слеп из-за BOM), память hub-browser-identities-bb-and-robots, grep памяти по "разлогин|logout|cookie|куки". brain_ask.py по теме.

2. СВЕРЬСЯ, ЧТО УЖЕ В РАБОТЕ, НЕ ДУБЛИРУЙ: сегодня 06:15 стоит one-time задача auto-hub-260903-warmth-lead-scale-delta «Доустановка сторожа robot-profile-scrub (ChatGPT-разлогин 22.09)» — прочитай её SKILL.md (C:\Users\dev\.claude\scheduled-tasks\auto-hub-260903-warmth-lead-scale-delta\SKILL.md). Твоя работа шире её, но не вместо неё.

3. СОБЕРИ УЛИКИ: какие роботы трогают браузерные профили. Подозреваемые (проверь каждого, не гадай): (а) роботы, копирующие/восстанавливающие куки (~/.claude/secrets/browser-cookie-backups/, скрипты с cookie в имени в ~/.claude/scripts и D:\Vault\_imports); (б) chatgpt-token-guard-nightly (добывает accessToken из системного Firefox); (в) claudeai-sync-daily (робо-профиль _chrome_profile_a2; живой Chrome оператора Default трогать НЕЛЬЗЯ с 30.08); (г) любой скрипт, который логинится/разлогинивается или чистит профили — grep по logout|Sign out|clear.*cookie|delete.*cookie. Сверь ВРЕМЕНА реальных разлогинов (оператор видел массовые разлогины Chrome И Firefox) с расписаниями рутин и change_ledger.

4. КОРЕНЬ: класс скорее всего «копирование живой куки в робо-профиль → вендор гасит сессию серверно НА ОБОИХ» (доказано на Meta 22.09). Проверь, кто ещё так делает и с какими куками (Google/OpenAI/FB). Почини класс: робо-профили живут своими логинами, живые куки оператора не копируются; куки-гвард пополни слепыми зонами (facebook и что найдёшь), почини BOM-слепоту chrome-щита.

5. Каждую починку — красный тест на сломанном коде, потом зелёный (§4.3-бис). Сторожа не селить в том, что он сторожит (§5.5).

6. ДОЛОЖИ: в TG чат 03 (dual-send bus_send.py) и оператору итог: кто был роботом-убийцей кук, что починено, чем доказано, какие сторожа стоят. Строка в Breakage-журнал (selfheal.py journal --class browser-logout-robot).

Границы: Tier-2 (деньги/необратимое/секреты) → пауза + аск в 02. Пароли символами не набирать. Живой Chrome оператора (Default) — не разлогинивать, не переключать аккаунты. Перед правкой общих файлов — onair declare.

Блок STOP-DUP: прочитай и исполни $OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md (D:\Vault\Vault-Knowledge\08-Templates\seed-stop-dup-block.md).
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory 2>/dev/null && ls | head -50; echo \"---GREP---\"; grep -ril \"разлогин\\|logout\\|cookie\\|куки\" . 2>/dev/null | head -30", "description": "RECALL: list memory + grep logout/cookie"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ разлогины-chrome-ff-чинилка"}

---

> `Bash` -- {"command": "M=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\"; grep -ril \"разлогин\\|logout\\|cookie\\|куки\" \"$M\" 2>/dev/null | head -30", "description": "Grep memory for logout/cookie"}

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/workspace_write_lease.py\" status 2>&1 | head -30", "description": "Check workspace lease status"}

---

> `Grep` -- {"pattern": "разлогин|logout|cookie|куки|Cookies", "path": "C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory", "output_mode": "files_with_matches", "-i": true}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\robot-profile-holds-human-session.md"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\meta-session-dies-when-copied-to-robot.md"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\hub-browser-identities-bb-and-robots.md"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\auto-hub-260903-warmth-lead-scale-delta\\SKILL.md"}

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/rail_plan.py\" declare --self \"расследование класса разлогинов, чтение памяти/скриптов, правка гвардов и сторожей, красные тесты, доклад в 03\" --outsource \"second_opinion:codex,code_read:codex\" 2>&1 | tail -5", "description": "Declare rail pla

---

> `Bash` -- {"command": "S=\"C:/Users/dev/.claude/scripts\"; ls -la \"$S/_shared/robot_profile_scrub.py\" \"$S/_shared/_test_robot_profile_scrub.py\" \"$S/chrome_login_shield.py\" \"$S/firefox_login_shield.py\" \"$S/_shared/firefox_selenium.py\" \"C:/Users/dev/.claude/robot_profile_scope.json\" 2>&1", "desc

---

> `Bash` -- {"command": "find \"C:/Users/dev/.claude\" \"D:/Vault/_imports\" -maxdepth 3 -iname \"*login_shield*\" -o -maxdepth 3 -iname \"*cookie*\" -o -maxdepth 3 -iname \"*profile*guard*\" 2>/dev/null | head -40", "description": "Find login shield and cookie scripts"}

---

> `Bash` -- {"command": "grep -rln \"_ROTATING_SESSION_HOSTS\\|rotating_session\" \"C:/Users/dev/.claude/scripts\" \"D:/Vault/_imports\" 2>/dev/null | head -20", "description": "Find rotating session hosts guard"}

---

> `Grep` -- {"pattern": "_ROTATING_SESSION_HOSTS", "path": "C:/Users/dev/.claude/scripts", "output_mode": "content", "-n": true, "head_limit": 40}

---

> `Glob` -- {"pattern": "**/*login_shield*", "path": "C:/Users/dev/.claude"}

---

> `Bash` -- {"command": "sed -n '165,230p' \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py\"", "description": "Read rotating session hosts region"}

---

> `Bash` -- {"command": "grep -n \"utf-8-sig\\|utf8-sig\\|encoding=\\|BOM\\|lstrip.*ufeff\\|\\\\\\\\ufeff\" \"C:/Users/dev/.claude/scripts/_shared/chrome_login_shield.py\" | head -30", "description": "Check BOM handling in chrome shield"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/robot_profile_scope.json\"; echo \"=== scrub log/backups ===\"; ls -la \"C:/Users/dev/.claude/secrets/robot-profile-scrub/\" 2>&1 | head -20", "description": "Read scrub scope + backups"}

---

> `Grep` -- {"pattern": "delete from moz_cookies|DELETE FROM cookies|Network[/\\\\\\\\]Cookies|Clear browsing|clear_cookies|delete_cookie|rmtree.*[Pp]rofile|del .*Cookies", "path": "C:/Users/dev/.claude/scripts", "output_mode": "content", "-n": true, "head_limit": 60}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python robot_profile_scrub.py --check 2>&1 | head -40; echo \"EXIT=$?\"", "description": "Run scrub check"}

---

> `Bash` -- {"command": "ls -1 \"C:/Users/dev/.claude/browser-profiles/\" 2>&1 | head -40", "description": "List robo profiles"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python chrome_login_shield.py --check 2>&1 | head -60; echo \"EXIT=$?\"", "description": "Chrome login shield check"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python ff_login_shield.py --check 2>&1 | head -60; echo \"EXIT=$?\"", "description": "Firefox login shield check"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python chrome_login_shield.py --help 2>&1 | head -40", "description": "Chrome shield help"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python chrome_login_shield.py 2>&1 | head -60; echo \"EXIT=$?\"", "description": "Run chrome login shield verify+backup"}

---

> `Grep` -- {"pattern": "user-data-dir|user_data_dir|--profile-directory|chrome_profile", "path": "C:/Users/dev/.claude/scripts", "output_mode": "content", "-n": true, "head_limit": 60, "glob": "*.py"}

---

> `Bash` -- {"command": "ls -1 \"C:/Users/dev/AppData/Local/Google/Chrome/User Data/\" 2>&1 | head -30; echo \"=== FF profiles ===\"; ls -1 \"C:/Users/dev/AppData/Roaming/Mozilla/Firefox/Profiles/\" 2>&1 | head -20", "description": "List Chrome and Firefox profiles"}

---

> `Bash` -- {"command": "sed -n '1,60p' \"C:/Users/dev/.claude/scripts/agent_chrome_hypothesis.py\"; echo \".....\"; sed -n '170,270p' \"C:/Users/dev/.claude/scripts/agent_chrome_hypothesis.py\"", "description": "Read agent_chrome_hypothesis.py"}

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/.agent-chrome/\" 2>&1 | head; echo \"=== find other chrome robo profiles ===\"; ls -d \"C:/Users/dev/.claude/browser-profiles\"/* \"C:/Users/dev/.agent-chrome\"/* 2>/dev/null; echo \"=== _chrome_profile_a2 ===\"; ls -d D:/Vault/_imports/claude-ai/_chrome_p

---

> `Bash` -- {"command": "schtasks /query /fo csv /nh 2>/dev/null | grep -i \"chrome\\|firefox\\|cookie\\|login\\|shield\\|scrub\\|browser\" | cut -d, -f1,2,3 | head -40", "description": "List browser-related scheduled tasks"}

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/.agent-chrome\" 2>&1 | head -5", "description": "Check agent-chrome profile"}

---

> `PowerShell` -- {"command": "schtasks /query /fo csv /nh | Select-String -Pattern \"chrome|firefox|cookie|login|shield|scrub|browser|rail\" | Select-Object -First 40", "description": "List browser-related scheduled tasks"}

---

> `Grep` -- {"pattern": "(rmtree|os\\.remove|unlink|Remove-Item).{0,80}(profile|Profile|Cookies|cookies\\.sqlite|sessionstore)", "path": "C:/Users/dev/.claude/scripts", "output_mode": "content", "-n": true, "head_limit": 50, "glob": "*.py"}

---

> `Grep` -- {"pattern": "(rmtree|os\\.remove|unlink|Remove-Item).{0,80}(profile|Profile|Cookies|cookies\\.sqlite|sessionstore)", "path": "D:/Vault/_imports", "output_mode": "content", "-n": true, "head_limit": 50, "glob": "*.py"}

---

> `Bash` -- {"command": "sed -n '295,340p' \"D:/Vault/_imports/fb-comments/fb_comments_pipeline.py\"", "description": "Read fb pipeline cookie deletion context"}

---

> `Grep` -- {"pattern": "copy_profile_from|copy2\\(.{0,60}[Cc]ookies|shutil\\.copy.{0,60}[Cc]ookies|Default.{0,20}Network.{0,20}Cookies", "path": "C:/Users/dev/.claude/scripts", "output_mode": "content", "-n": true, "head_limit": 50, "glob": "*.py"}

---

> `Bash` -- {"command": "grep -n \"ensure_profile\\|copytree\\|FBREAD\\|системн\\|SYSTEM_PROFILE\\|def .*profile\" \"D:/Vault/_imports/fb-comments/fb_comments_pipeline.py\" | head -40", "description": "Find ensure_profile in fb pipeline"}

---

> `Bash` -- {"command": "sed -n '230,300p' \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py\"", "description": "Read clone_profile and _resolve_profile"}

---

> `Grep` -- {"pattern": "clone_profile", "path": "D:/Vault/_imports", "output_mode": "content", "-n": true, "head_limit": 40, "glob": "*.py"}

---

> `Bash` -- {"command": "for f in run_one.py coinbase_submit.py ashby_submit.py; do echo \"=== $f ===\"; sed -n '1,30p' \"D:/Vault/_imports/jobs-watch/apply_engines/$f\"; done", "description": "Read SRC in apply engines"}

---

> `Bash` -- {"command": "grep -n \"def clone_profile\" -A 40 \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py\"", "description": "Read clone_profile"}

---

> `Grep` -- {"pattern": "copytree.{0,80}(User Data|Chrome|Default)|User Data.{0,40}copytree", "path": "D:/Vault/_imports", "output_mode": "content", "-n": true, "head_limit": 20}

---

> `Bash` -- {"command": "grep -n \"_PROFILE_KEEP\" -A 12 \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py\" | head -25", "description": "Read _PROFILE_KEEP"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts && python onair.py expire 2>&1 | tail -3; echo \"=== zones ===\"; python onair.py zones 2>&1 | head -20; echo \"=== check fleet-code ===\"; python onair.py check --zone fleet-code 2>&1 | head -20", "description": "ON AIR expire and check fleet-code"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts && python onair.py declare --zone fleet-code --mode exclusive --what \"Класс разлогинов: гвард внутрь clone_profile (4 прямых вызова в обход _resolve_profile)\" 2>&1 | tail -5", "description": "Declare ON AIR fleet-code"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts && python onair.py declare --zone fleet-code --mode exclusive --title \"Класс разлогинов: гвард внутрь clone_profile\" 2>&1 | tail -5", "description": "Declare ON AIR fleet-code"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_test_clone_profile_session_strip.py", "content": "#!/usr/bin/env python3\n\"\"\"КРАСНЫЙ-СНАЧАЛА тест: clone_profile обязан снимать ротируемые сессии С КОПИИ.\n\nПОЧЕМУ (замер 23.09.2026, хаб HUB-01, жалоба оператора «робот ходит и все\

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python _test_clone_profile_session_strip.py 2>&1 | tail -15; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "RED run of new test before fix"}

---

> `Bash` -- {"command": "cp \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py\" \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py.bak-clonestrip-20260923\" && echo \"backup ok\"", "description": "Backup firefox_selenium.py"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\firefox_selenium.py", "old_string": "def clone_profile(src: str, dst: str | None = None) -> str:\n    \"\"\"Скопировать нужные файлы залогиненного профиля во ВРЕМЕННЫЙ (реальный под GUI-lock).\n    Возвращает путь копи

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && head -30 firefox_selenium.py | grep -n \"^import\\|^from\"; echo \"=== GREEN RUN ===\"; python _test_clone_profile_session_strip.py 2>&1 | tail -12; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Check imports and run test after fix"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && echo \"--- inplace guard ---\" && python _test_firefox_inplace_guard.py 2>&1 | tail -12; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Regression: inplace guard test"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python _test_robot_profile_scrub.py 2>&1 | tail -8; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Regression: robot profile scrub test"}

---

> `Bash` -- {"command": "ls -d \"C:/Users/dev/AppData/Local/Temp\"/ff_* 2>/dev/null | head -20; echo \"--- count ---\"; ls -d \"C:/Users/dev/AppData/Local/Temp\"/ff_* 2>/dev/null | wc -l", "description": "Look for leftover cloned FF profiles in temp"}

---

> `Grep` -- {"pattern": "cookies\\.sqlite|Network.Cookies|logins\\.json|key4\\.db", "path": "C:/Users/dev/.claude/scheduled-tasks", "output_mode": "content", "-n": true, "head_limit": 25}

---

> `PowerShell` -- {"command": "Get-ChildItem -Path $env:TEMP -Directory -Filter \"ff_*\" -ErrorAction SilentlyContinue | Select-Object Name, LastWriteTime | Sort-Object LastWriteTime -Descending | Select-Object -First 15; \"count: \" + (Get-ChildItem -Path $env:TEMP -Directory -Filter \"ff_*\" -ErrorAction SilentlyCo

---

> `PowerShell` -- {"command": "$p = Join-Path $env:TEMP \"ff_ats_5c5qf0np\"; Get-ChildItem $p -ErrorAction SilentlyContinue | Select-Object Name, Length | Format-Table -AutoSize", "description": "Inspect a cloned ats profile contents"}

---

> `Grep` -- {"pattern": "ff_ats", "path": "D:/Vault/_imports", "output_mode": "content", "-n": true, "head_limit": 20}

---

> `Bash` -- {"command": "sed -n '1,60p' \"D:/Vault/_imports/jobs-watch/selenium_apply/ats_lib.py\"", "description": "Read ats_lib driver creation"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport os,sqlite3,glob,collections\nt=os.environ.get(\"TEMP\") or os.path.expanduser(\"~/AppData/Local/Temp\")\ndirs=sorted(glob.glob(os.path.join(t,\"ff_ats_*\")))\nprint(\"ff_ats profiles:\",len(dirs))\ntot=collections.Counter()\nchecked=0\nfor d in dirs[-8:]:\n    db

---

> `Bash` -- {"command": "python - <<'PY'\nimport os,sqlite3,glob\nt=os.environ.get(\"TEMP\")\nfor pat in (\"ff_safe_*\",\"ff_auto_profile\"):\n    for d in glob.glob(os.path.join(t,pat)):\n        db=os.path.join(d,\"cookies.sqlite\")\n        if not os.path.isfile(db):\n            print(os.path.basename(d),\"

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\firefox_selenium.py", "old_string": "        return any(h == v or h.endswith(\".\" + v) for h in hosts for v in _ROTATING_SESSION_HOSTS)\n    except Exception:\n        return False\n    finally:\n        shutil.rmtree

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python _test_clone_profile_session_strip.py 2>&1 | tail -4 && python _test_firefox_inplace_guard.py 2>&1 | tail -2", "description": "Re-run both tests after warning edit"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python - <<'PY'\nimport os,glob,sys\nsys.path.insert(0,\".\")\nimport firefox_selenium as fs\nt=os.environ[\"TEMP\"]\nfor d in sorted(glob.glob(os.path.join(t,\"ff_safe_*\"))+glob.glob(os.path.join(t,\"ff_auto_profile\"))):\n    n=fs._strip_r

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts && python selfheal.py journal --class browser-logout-robot --what \"Клон человеческого профиля Firefox мимо гварда: clone_profile звали НАПРЯМУЮ 4 потребителя (fb_comments_pipeline, jobs-watch/apply_engines x3) с профиля Ct3iOc7B.Profile 1; вторая живая

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts && ls deploy_register.py deploy_check.py 2>&1; python deploy_register.py --help 2>&1 | head -25", "description": "Check deploy parcel tooling"}

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts && python selfheal.py journal --class browser-logout-robot --what \"Клон человеческого профиля FF мимо гварда: clone_profile звали НАПРЯМУЮ 4 потребителя (fb_comments_pipeline, jobs-watch/apply_engines x3) с Ct3iOc7B.Profile 1; вторая копия живой сессии

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/workspace_write_lease.py\" --help 2>&1 | head -20", "description": "Lease tool help"}

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/workspace_write_lease.py\" check \"C:/Users/dev/.claude/scripts\" 2>&1 | head -10", "description": "Who holds the scripts lease"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev\" && python \"C:/Users/dev/.claude/scripts/selfheal.py\" journal --class browser-logout-robot --what \"Клон человеческого профиля FF мимо гварда: clone_profile звали НАПРЯМУЮ 4 потребителя (fb_comments_pipeline, jobs-watch/apply_engines x3) с Ct3iOc7B.Profile 1; вт

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_test_clone_profile_session_strip.py", "old_string": "LIVE = [\".google.com\", \".facebook.com\", \"chatgpt.com\", \".ashbyhq.com\", \"boards.greenhouse.io\"]", "new_string": "LIVE = [\".google.com\", \".facebook.com\"

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python _test_clone_profile_session_strip.py 2>&1 | grep -E \"^  (OK|FAIL) 1 |ИТОГ\"; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Red run for new vendor hosts"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\firefox_selenium.py", "old_string": "_ROTATING_SESSION_HOSTS = (\"google.com\", \"claude.ai\", \"z.ai\", \"chatgpt.com\", \"openai.com\",\n                           \"facebook.com\", \"messenger.com\", \"instagram.com

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python _test_clone_profile_session_strip.py 2>&1 | grep -E \"^  (OK|FAIL)|ИТОГ\"; echo \"---inplace---\"; python _test_firefox_inplace_guard.py 2>&1 | tail -2; echo \"---scrub---\"; python _test_robot_profile_scrub.py 2>&1 | tail -2", "descri

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python - <<'PY'\nimport os,sqlite3,sys,tempfile,shutil\nsys.path.insert(0,\".\")\nimport firefox_selenium as fs\nsrc=os.path.join(os.environ[\"APPDATA\"],\"Mozilla\",\"Firefox\",\"Profiles\",\"646yqiss.default-release\")\ndef rot(db):\n    if

---

> `Bash` -- {"command": "cd \"C:/Users/dev\" && python \"C:/Users/dev/.claude/scripts/deploy_register.py\" all clone-strip-rotating-session-20260923 \"Класс browser-logout-robot: гвард переехал ВНУТРЬ clone_profile (4 прямых вызова шли мимо _resolve_profile); +x.com/grok.com/mistral.ai в список ротируемых\"

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_probe_clone_strip.py", "content": "#!/usr/bin/env python3\n\"\"\"ПРОБА (read-only для боевого состояния): доехал ли на этот узел гвард clone_profile.\n\nПОЧЕМУ проба, а не тест: verify посылки бежит на КАЖДОМ узле флота, а тест вправе\nпис

---

> `Bash` -- {"command": "cd C:/Users/dev/.claude/scripts/_shared && python _probe_clone_strip.py 2>&1 | tail -3; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Run the probe"}

---

> `Bash` -- {"command": "cd C:/Users/dev/AppData/Local/Temp && rm -rf probered && mkdir probered && cp \"C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py.bak-clonestrip-20260923\" probered/firefox_selenium.py && cp \"C:/Users/dev/.claude/scripts/_shared/_probe_clone_strip.py\" probered/ && cd prob

---

> `Bash` -- {"command": "python - <<'PY'\nimport os,shutil,subprocess,sys,tempfile\ntd=tempfile.mkdtemp(prefix=\"probered_\")\nsh=r\"C:\\Users\\dev\\.claude\\scripts\\_shared\"\nshutil.copy2(os.path.join(sh,\"firefox_selenium.py.bak-clonestrip-20260923\"),os.path.join(td,\"firefox_selenium.py\"))\nshutil.copy

---

> `Bash` -- {"command": "cd \"C:/Users/dev\" && python \"C:/Users/dev/.claude/scripts/bus_send.py\" --to 03 --text \"ЧИНИЛКА РАЗЛОГИНОВ (хаб HUB-01, 23.09 05:1x) — корень найден и закрыт, класс browser-logout-robot 1/3.\nРОБОТ-УБИЙЦА: не чистильщик кук, а КЛОНЕР. Гвард против «вторая живая копия сесс

---

> `Bash` -- {"command": "cd \"C:/Users/dev\" && for f in tg_bus_send.py routine_runlog.py cron_heartbeat.py; do echo \"=== $f ===\"; python \"C:/Users/dev/.claude/scripts/$f\" --help 2>&1 | head -12; done", "description": "Usage of the three closing tools"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev\" && python \"C:/Users/dev/.claude/scripts/tg_bus_send.py\" --to 03 \"ЧИНИЛКА РАЗЛОГИНОВ (хаб HUB-01, 23.09 05:2x) — корень найден и закрыт; класс browser-logout-robot 1/3.\nРОБОТ-УБИЙЦА — не чистильщик кук, а КЛОНЕР. Гвард «вторая живая копия сессии = вендо

---

> `Bash` -- {"command": "cd \"C:/Users/dev\" && python \"C:/Users/dev/.claude/scripts/onair.py\" close --zone fleet-code 2>&1 | tail -3", "description": "Close ON AIR claim"}

---

**Claude:**

[⏰ 05:2x, среда, 23 сентября 2026]

## Робот-убийца найден. Это не чистильщик кук — это **клонер**

**Корень.** Гвард «вторая живая копия сессии = вендор гасит ту, что осталась у человека» стоял в `firefox_selenium._resolve_profile` — то есть на **одной двери**, `make_driver`. А сама `clone_profile` — публичная функция без замка, и её зовут **напрямую, мимо гварда**, четверо:

- [fb_comments_pipeline.py:250](D:/Vault/_imports/fb-comments/fb_comments_pipeline.py:250)
- [run_one.py:16](D:/Vault/_imports/jobs-watch/apply_engines/run_one.py:16)
- [ashby_submit.py:21](D:/Vault/_imports/jobs-watch/apply_engines/ashby_submit.py:21)
- [coinbase_submit.py:18](D:/Vault/_imports/jobs-watch/apply_engines/coinbase_submit.py:18)

Все четверо копируют **человеческий** профиль `Ct3iOc7B.Profile 1` — намеренно, ради «cookie-rich» анти-бот отпечатка. Труба А клонирует его пачками → Google/Meta/OpenAI видят вторую живую сессию и гасят серверно ту, что у тебя. Один Google-килл выбивает и Chrome — отсюда «все хромы И Firefox». Живые клонеры сидят на **NODE-0X**, не на хабе.

**Второй дефект, независимый.** `has_rotating_session` — **fail-open**: база кук под замком живого Firefox → `except` → «сессий нет» → `_resolve_profile` спокойно снимал полную копию. Улика на диске: `%TEMP%\ff_safe_646yqiss.default-release` и `ff_safe_m26xxxkf.dev-clean` от 15.09 несли **155 и 162** ротируемых куки.

**Починено** ([firefox_selenium.py](C:/Users/dev/.claude/scripts/_shared/firefox_selenium.py)):
1. Замок переехал **внутрь** `clone_profile` — одна дверь вместо четырёх, пятый потребитель закрыт заранее. Источник не трогается никогда.
2. Слепые зоны добраны: `+x.com +grok.com +mistral.ai` (было 8 вендоров, стало 11).
3. Индикатор перестал молчать при нечитаемой базе.
4. С 4 залежавшихся temp-клонов снят **321 живой кук**.

**Доказано:** новый [тест](C:/Users/dev/.claude/scripts/_shared/_test_clone_profile_session_strip.py) **красный** на старом коде (кейс 1 FAIL) → зелёный 6/6. Регрессии: inplace-guard 7/7, robot-profile-scrub GREEN. **Второй заход другим методом**, на твоём живом профиле: источник 344 куки / 187 ротируемых **до и после**, клон — 157 / **0**.

**Не сделано** (гейт срезал прогон на 81 вызове из 80):
- красный прогон пробы `_probe_clone_strip.py` на старом коде не показан;
- флот-посылка `clone-strip-rotating-session-20260923` не зарегистрирована (файл едет Syncthing'ом сам, но verify по узлам не записан) — **NODE-0X проверить первым**;
- табличка ON AIR `fleet-code` осталась висеть, снимется по TTL через 12ч;
- чужие рельсы (codex) — 0 вызовов, причина: бюджет кончился до панели /tt.
- `fb_comments_pipeline` теперь получит клон без FB-кук → честный LOGIN-WALL exit 3. Чтобы fbread читал стену, ему нужен **свой собственный вход твоими руками** — иначе он снова упрётся в тот же класс.

🧒 **Простыми словами:** у тебя есть робот, который перед работой делал **копию твоего браузера вместе с ключами от всех дверей** — от почты, фейсбука, чатгпт. А охранник у сайтов простой: увидел один и тот же ключ в двух руках — сломал замок у обоих. Поэтому тебя выкидывало отовсюду. Я поставил вахтёра прямо у копировальной машины: копию делать можно, но ключи из неё вынимаются — остаётся только бумага. Твой настоящий ключ не трогали: пересчитал до и после, 187 штук как лежали, так и лежат.
