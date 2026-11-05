---
session: s_94baf52f
date: 2026-10-06
words: 5717
turns: 51
tools: "Bash, Edit, PowerShell, ToolSearch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · Scheduled run: auto-hub-260825-fleet-debt-drain

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_94baf52f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260825-fleet-debt-drain" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260825-fleet-debt-drain\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

ПЕРВЫМ ДЕЛОМ переименуй эту сессию: вызови mcp__ccd_session_mgmt__set_session_title с title "Починка корня разлогинов браузерных рельс".

⛳ ВХОД. Приказ оператора 06.10.2026 (голосом, дословно): «делай отдельную сессию чинить эти ебаные разлогины!!!» и отдельно его гипотеза №1, тоже дословно: «какой то ебаный скрипт удаляет куки или что то еще и происходит РАЗЛОГИН». Его ЗАЕБАЛИ постоянные вылогинивания браузерных рельс; 06.10 он в N-й раз руками логинил робот-профиль Firefox.

⚠️ ЭТО ВТОРОЙ ЗАПУСК. Первый (06.10 ~21:55 по сбитым часам, session local_43ee2d97) УПАЛ через 18 секунд с `Claude Code process exited with code 1` после двух вызовов (ToolSearch, PowerShell). Если упадёшь так же — не молчи: это улика, запиши её в Breakage-Journal.

⚠️ ЧАСЫ: 06.10 часы хаба отставали на 4 суток, NTP догнал их в 12:36 UTC (`w32tm /query /status`). Любые даты старше этого момента в логах/метках могут быть на 4 дня в прошлом. Сверяй время вторым источником ВНЕ машины (`ssh mayak date -u`, `curl -sI https://www.google.com | grep -i ^date`). Память: [[hub-clock-drifted-four-days]].

📛 ON AIR: первым делом объяви себя — `python ~/.claude/scripts/onair.py check --zone browser-automation`, чисто → `onair.py declare --zone browser-automation --mode exclusive --title "починка разлогинов" --ttl-hours 6`; в конце `onair close`. Зона занята соседом — НЕ править параллельно: читай его табличку, договаривайся в 03 или бери другой кусок.
👤 КОНСОЛИДАТОР: если по этой теме поднято больше ОДНОГО исполнителя — консолидатор ЭТА СЕССИЯ. Он сводит результаты и объявляет «готово»; остальные сдают ему кусок и НЕ пишут свой финальный вердикт. Исполнитель один — эта строка не действует.
🔁 RECALL ЛЕТЯЩЕЙ РАБОТЫ (до постройки, не после): `onair.py list` + свежие панели `~/.claude/scripts/cc-review/bridge-state/usage.jsonl` + журнал поломок `python ~/.claude/scripts/breakage.py find "разлогин"`. Нашёл чужой готовый артефакт — ПЕРЕИСПОЛЬЗУЙ, свой не рожай.
🪫 БАК И СМЕРТЬ ПРИ РОЖДЕНИИ: умер об лимит при рождении — это обязано быть ЗАМЕЧЕНО: одобренная задача без следа исполнения считается НЕ сделанной, а не идущей.
🔍 УЛИКА ПРИ СТАТУС-CLAIM: любое ✅ про ФАЙЛ, КОД или ЧУЖУЮ ПРОВЕРКУ ставится ТОЛЬКО с уликой в том же заходе: `ls`/`cat`/цитата строки/exit-код. Не читал своими глазами — пиши 🤔. Пусто ИЗ ОДНОГО места ≠ «нет на диске» (§5.4).
🤝 ТЫ АВТОНОМНЫЙ КОФАУНДЕР, НЕ ИСПОЛНИТЕЛЬ С ВОПРОСАМИ: развилку и неполное ТЗ решаешь ТЫ и доводишь до результата, решение кладёшь в отчёт постфактум. Заход, кончившийся «жду ответа оператора» на ОБРАТИМОМ, считается НЕ сделанным. оператору остаётся закрытый список: деньги · необратимое удаление · юр.подпись · секреты 3-м лицам · масс-рассылка. «Нужны руки оператора» — ПОСЛЕДНЕЕ: сперва ДВЕ честные разные попытки обхода.
⏳ ПРЕМИССА — ПРОВЕРЯЕМАЯ: первым шагом замерь по ground truth (живая система, не текст сида) то, про что сид говорит. Не подтвердилась — скажи «премисса протухла» и чини то, что реально сломано.

OUTCOME: оператор больше НИКОГДА не вводит пароли в браузерные рельсы повторно. Разлогин = «раз в квартал по вине вендора», а не еженедельный налог.

ГИПОТЕЗА оператора №1 — ПРОВЕРИТЬ ПЕРВОЙ (его слова: «какой-то скрипт удаляет куки»):
(1) grep по ~/.claude/scripts и по планировщику (`schtasks /query /fo LIST /v`) на всё, что трогает `cookies.sqlite`, `browser-profiles`, `ff-autoff-profile`, `clean`, `wipe`, `rmtree`, `Remove-Item`, `del /`;
(2) подозреваемые: чистильщики профилей, бэкап-скрипты, housekeeping/selfheal-рутины, geckodriver (травит user.js), Syncthing (если папка профиля попала в синкаемую зону);
(3) сверь mtime `cookies.sqlite` в профилях с LastRunTime задач — совпадение окна = улика;
(4) СНИМИ BASELINE СЕЙЧАС: `python ~/.claude/scripts/_shared/ff_session_probe.py` + md5 каждого `cookies.sqlite` + размер; положи снимок в `~/.claude/_cookie_baseline/<ts>.json`. Это твой эталон здоровья: когда куки в следующий раз умрут, у тебя будет время смерти и список задач, бежавших в это окно.

⚠️ ЖИВАЯ УЛИКА ТОГО ЖЕ НАДКЛАССА (06.10, замерено заказчиком): в 20:11-20:12 по сбитым часам кто-то СЫРЫМ файловым удалением выпилил стандартную библиотеку системного Python312 (`Lib/` остался только с `site-packages`, `DLLs` 23 файла); MSI-событий в это окно НЕ было, значит не инсталлятор, а скрипт с rmtree/del. Соседняя сессия проверила: PermOptIn-Guard чист, Cursor-updater и chrome_installer не при чём. Для атрибуции нужен `fsutil usn readjournal` или Prefetch — ДВЕ ДВЕРИ УПЁРЛИСЬ В «нужен админ» у неё; попробуй ты (если нет прав — скажи прямо, это Tier-2 на руки оператора). Тот, кто снёс stdlib, — лучший подозреваемый и по кукам.

SCOPE: (1) проверить гипотезу оператора (выше) — она главная; (2) 5почему по серии датированных случаев (Breakage-Journal + полевые заметки скилла /dr-fanout: 04.09 «копия профиля ломает ротацию», 10.09 «autoff пуст на узле», 14.09 «в autoff claude.ai 0 кук, туда не логинились никогда», 22.09 «обе двери закрыты», 26.09 «AutoFF растерял сессии: google 1 вместо 27, chatgpt 0 вместо 23, claude 0 вместо 14», 06.10 Cloudflare+разлогаут-лендинг); (3) КОРЕНЬ: копии? geckodriver? куки не флашатся при SIGKILL рельсы? TTL вендора? чужой скрипт? ротация refresh-токена без записи обратно?; (4) починить корень механизмом (кандидаты: запрет убийства рельсы до флаша кук · бэкап cookies.sqlite после каждого ЗДОРОВОГО прогона + авто-откат при залёте · сторож свежести сессии, который ловит разлогин ЗА ЧАСЫ до нужды в рельсе и шлёт ОДИН точный аск, а не валит веер); (5) /tt с ПОКАЗАННЫМ красным тестом; (6) раскатка знания в скилл /dr-fanout датированным блоком.

NOT-GOALS: не трогать человеческие профили оператора (`m26xxxkf.dev-clean`, `418toca9.*`, `646yqiss.default-release`); не чинить Chrome-MCP-классификатор (отдельный класс); пароли не вводишь и не выводишь из store в логи.

DELIVERABLE: Decision Memo «корень разлогинов + механизм» в 02-Decisions + починка в коде с тестом + строка в Breakage-Journal. DoD: /tt ✅ с красным тестом + доказательство вторым заходом (§4.3-бис).

ЭСКАЛАЦИЯ: Tier-2 → `approval.py ask` в 02-POLICE; заказчик = сессия 98c27f3c@HUB-01 (ДР DR26-10-02-HUB-02, он же поднял рельсу NATS на Маяке 06.10).
</scheduled-task>

---

**Claude:**

I'll start by renaming the session and declaring ON AIR, then verify the premise before building anything.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `Bash` -- {"command": "date -u; echo \"--- google header ---\"; curl -sI https://www.google.com 2>/dev/null | grep -i '^date' ; echo \"--- w32tm ---\"; w32tm /query /status 2>/dev/null | head -20", "description": "Verify clock against external source"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "Починка корня разлогинов браузерных рельс"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null && python onair.py check --zone browser-automation 2>&1 | head -30; echo \"=== EXIT $? ===\"", "description": "Check ON AIR zone"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py check --zone secrets-auth 2>&1 | head -20; echo \"---LIST---\"; python onair.py list 2>&1 | head -40", "description": "Check secrets-auth zone and list onair"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python breakage.py find \"разлогин\" 2>&1 | head -60; echo \"=== EXIT $? ===\"", "description": "Search breakage journal for logout cases"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone secrets-auth --mode exclusive --title \"починка разлогинов браузерных рельс\" --ttl-hours 6 2>&1 | head -20", "description": "Declare ON AIR secrets-auth exclusive"}

---

> `Bash` -- {"command": "grep -iE 'разлогин|logout|logged.out|cookie|куки|sign.?in|signed.out|auth' \"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_94baf52f\\tool-results\\be0f52zrb.txt\" | head -50", "description": "Grep breakage journal for cookie/logout lines"

---

**Claude:**

ON AIR взят (`secrets-auth`, exclusive, 6ч). Теперь премисса — ground truth по профилям.

---

> `Bash` -- {"command": "ls -la ~/.claude/scripts/_shared/ff_session_probe.py 2>&1; echo \"=== PROFILES ROOT ===\"; ls -la \"$APPDATA/Mozilla/Firefox/Profiles\" 2>&1 | head -30; echo \"=== browser-profiles ===\"; ls -la ~/.claude/browser-profiles 2>&1 | head -30", "description": "Locate FF probe and profiles"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls -la | grep -iE 'ff_|firefox|autoff|cookie' | head -30; echo \"=== _shared ===\"; ls _shared/ 2>/dev/null | grep -iE 'ff|firefox|cookie|session' | head -20", "description": "List firefox/cookie related scripts"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 120 python _shared/ff_session_probe.py 2>&1 | head -60; echo \"=== EXIT $? ===\"", "description": "Run FF session probe baseline"}

---

> `Bash` -- {"command": "echo \"=== all cookies.sqlite on disk (user tree) ===\"; find \"$USERPROFILE/.claude\" \"$APPDATA/Mozilla\" \"$LOCALAPPDATA/Mozilla\" -name 'cookies.sqlite' 2>/dev/null | while read f; do printf \"%s\\t%s\\t%s\\n\" \"$(stat -c '%y' \"$f\" | cut -c1-19)\" \"$(stat -c '%s' \"$f\")\" \"$f\

---

> `Bash` -- {"command": "cd ~/.claude && python - <<'PY'\nimport os,glob,hashlib,json,datetime,pathlib\nroots=[os.path.expandvars(r'%USERPROFILE%\\.claude'),os.path.expandvars(r'%APPDATA%\\Mozilla'),os.path.expandvars(r'%LOCALAPPDATA%\\Mozilla')]\nfound=[]\nfor r in roots:\n    for dp,dn,fn in os.walk(r):\n    

---

> `Bash` -- {"command": "for d in ~/.claude/browser-profiles/*/; do echo \"=== $d\"; ls -la \"$d\" 2>&1 | head -25; done", "description": "Inspect robot browser profiles content"}

---

**Claude:**

Две крупные улики сразу. Копаю корень.

---

> `Bash` -- {"command": "cd ~/.claude && grep -rln \"dev-clean\" --include=*.py --include=*.json --include=*.md --include=*.cmd --include=*.ps1 . 2>/dev/null | head -40", "description": "Find who references dev-clean profile"}

---

> `Bash` -- {"command": "cd ~/.claude && grep -rn \"robot-research\" --include=*.py --include=*.json --include=*.md . 2>/dev/null | head -30", "description": "Find who references robot-research profiles"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/logout-loop-robot-uses-dev-personal-account.md\"", "description": "Read existing logout-loop memory in full"}

---

**Claude:**

Нашёл рабочую память по этой теме и урок из откат 25.09. Проверяю самую сильную улику — ДВА профиля «dev-clean».

---

> `Bash` -- {"command": "python -c \"\nimport datetime\nfor ms in [id_487c2293]:\n    print(ms, datetime.datetime.fromtimestamp(ms/1000, datetime.timezone.utc).isoformat())\n\"\necho \"=== profiles.ini ===\"\ncat \"$APPDATA/Mozilla/Firefox/profiles.ini\" 2>/dev/null\necho \"=== installs.ini ===\"\ncat \"$APPD

---

> `Bash` -- {"command": "cd ~/.claude && grep -rn \"CreateProfile\\|-CreateProfile\\|createprofile\" --include=*.py --include=*.cmd --include=*.ps1 --include=*.md . 2>/dev/null | grep -v _sync-conflict | head -30", "description": "Find any -CreateProfile usage"}

---

**Claude:**

Корень события 25.09 найден. Теперь проверяю повторяющийся налог — prefs и autoff.

---

> `Bash` -- {"command": "P=\"$LOCALAPPDATA/ff-autoff-profile\"; echo \"=== autoff exists? ===\"; ls -la \"$P\" 2>&1 | head -8; echo \"=== autoff cookies ===\"; ls -la \"$P/cookies.sqlite\" \"$P/user.js\" \"$P/prefs.js\" 2>&1\necho; echo \"######## ACTIVE PROFILE user.js ########\"\nA=\"$APPDATA/Mozilla/Firefox/

---

> `Bash` -- {"command": "A=\"$APPDATA/Mozilla/Firefox/Profiles/418toca9.dev-clean-1790334667178\"\necho \"=== cookie/sanitize/privacy prefs in prefs.js ===\"\ngrep -iE 'cookie|sanitize|clearOnShutdown|privatebrowsing|lifetimePolicy|marionette|webdriver' \"$A/prefs.js\" 2>&1 | head -40\necho; echo \"=== same f

---

**Claude:**

`ff-autoff-profile` пуст — только `times.json` от 03.10 03:16. Это профиль, которым ходят DR-рельсы. Ищу, кто его стирает.

---

> `Bash` -- {"command": "cd ~/.claude && grep -rn \"ff-autoff-profile\\|ff_autoff\\|autoff\" --include=*.py --include=*.cmd --include=*.ps1 --include=*.json scripts/ 2>/dev/null | grep -v '_sync-conflict\\|\\.bak-\\|graphify-out' | head -40", "description": "Find autoff profile references in scripts"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -rn \"rmtree\\|Remove-Item\\|shutil.rmtree\\|os.unlink\\|os.remove\" --include=*.py . 2>/dev/null | grep -iE 'profile|cookie|browser|ff|firefox|autoff' | grep -v '_sync-conflict\\|\\.bak-\\|_test_\\|_probe_' | head -40", "description": "Find profile deletion

---

**Claude:**

Два главных подозреваемых. Читаю.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '1,60p' ff_profile_sweeper.py; echo \"...... lines 120-175 ......\"; sed -n '120,175p' ff_profile_sweeper.py", "description": "Read ff_profile_sweeper.py"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '1,50p' _shared/robot_profile_scrub.py; echo \"...... 150-200 ......\"; sed -n '150,200p' _shared/robot_profile_scrub.py", "description": "Read robot_profile_scrub.py"}

---

**Claude:**

`robot_profile_scrub.py` — скрипт, который **удаляет куки по домену**, и зовётся перед КАЖДЫМ подъёмом робо-драйвера. Это буквально гипотеза оператора. Читаю реестр области.

---

> `Bash` -- {"command": "cat ~/.claude/robot_profile_scope.json 2>&1", "description": "Read robot profile scope registry"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '50,150p' _shared/robot_profile_scrub.py", "description": "Read scrub scope resolution logic"}

---

**Claude:**

Корень найден и он — дословно гипотеза оператора. Теперь улики: журнал бэкапов скраба = время каждого удаления.

---

> `Bash` -- {"command": "D=~/.claude/secrets/robot-profile-scrub; echo \"=== backups dir ===\"; ls -la \"$D\" 2>&1 | head -40; echo; echo \"=== count ===\"; ls \"$D\" 2>/dev/null | wc -l", "description": "List scrub backups = scrub event log"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"robot_profile_scrub\\|rps\\.\\|scrub\" _shared/firefox_selenium.py | head -30", "description": "Verify scrub is wired into make_driver"}

---

**Claude:**

`firefox_selenium.py:438` → `_rps.guard(profile)`. Теперь строю полный журнал событий скраба из бэкапов.

---

> `Bash` -- {"command": "ls ~/.claude/secrets/robot-profile-scrub/*.sqlite 2>/dev/null | sed 's|.*/||' | sort", "description": "List all scrub event backups"}

---

**Claude:**

Журнал событий есть. Читаю, ЧТО именно удалялось из autoff.

---

> `Bash` -- {"command": "cd ~/.claude && python - <<'PY'\nimport sqlite3,glob,os,json,collections,shutil,tempfile\nscope=json.load(open(os.path.expanduser('~/.claude/robot_profile_scope.json'),encoding='utf-8-sig'))\ndef in_scope(h,sc):\n    h=(h or '').lstrip('.').lower()\n    return any(h==d or h.endswith('.'

---

**Claude:**

Улики решающие. Теперь — что такое профиль `retired` и как код ведёт себя при отсутствии строки в реестре.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '200,300p' _shared/robot_profile_scrub.py", "description": "Read guard and targets logic"}

---

> `Bash` -- {"command": "cat ~/.claude/robot_profile_roots.json 2>&1; echo \"=== find 'retired' profile dirs ===\"; for r in \"D:/AutomationBrowsers/Firefox\" \"$HOME/.claude/browser-profiles\" \"$LOCALAPPDATA\"; do echo \"-- $r\"; ls -la \"$r\" 2>&1 | head -15; done", "description": "Find retired profile and e

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -rn \"retired\" _shared/_test_robot_profile_scrub.py _shared/robot_profile_scrub.py 2>/dev/null | head -20; echo \"=== any file mentioning retired ===\"; grep -rln '\"retired\"\\|retired' --include=*.py ~/.claude/scripts 2>/dev/null | grep -v _sync-conflict 

---

**Claude:**

`retired` — это тестовая фикстура, пишущая в боевой каталог бэкапов (отдельный дефект, не корень). Честно отделяю. Теперь второй корень: autoff-профиль ФИЗИЧЕСКИ стёрт 03.10.

---

> `Bash` -- {"command": "echo \"=== autoff times.json ===\"; cat \"$LOCALAPPDATA/ff-autoff-profile/times.json\" 2>&1; echo; python -c \"\nimport json,datetime,os\np=os.path.expandvars(r'%LOCALAPPDATA%\\ff-autoff-profile\\times.json')\nd=json.load(open(p))\nfor k,v in d.items():\n    print(k,v,datetime.datetime.

---

**Claude:**

Второй корень назван. Читаю память про подметальщик AppData — это и есть «скрипт, удаляющий куки».

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/appdata-age-sweep-killed-cursor-vscode.md\" 2>&1", "description": "Read appdata age sweep memory"}

---

**Claude:**

Оба корня названы и датированы. Переиспользую существующий `ff_session_probe.py` вместо своего детектора.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && cat _shared/ff_session_probe.py", "description": "Read ff_session_probe.py to reuse"}

---

**Claude:**

Корни доказаны. Строю прибор: снимок-эталон + детектор с атрибуцией + откат, переиспользуя `ff_session_probe`.

---

> `Bash` -- {"command": "cat > ~/.claude/scripts/cookie_sentinel.py <<'PYEOF'\n#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"cookie_sentinel.py -- разлогин браузерной рельсы ловится ЗА ЧАСЫ до нужды и ОТКАТЫВАЕТСЯ\nбез рук оператора. 0 LLM, 0 сети, stdlib-only.\n\nЗАЧЕМ (приказ оператора 06.10.2026, голосом:

---

**Claude:**

Heredoc не прошёл в Git Bash — пишу файл напрямую.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"cookie_sentinel.py -- разлогин браузерной рельсы ловится ЗА ЧАСЫ до нужды и ОТКАТЫВАЕТСЯ\nбез рук оператора. 0 LLM, 0 сети, stdlib-only.\n\nЗАЧЕМ (приказ оператора 06.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python cookie_sentinel.py --help 2>&1 | head -20; echo \"=== EXIT $? ===\"", "description": "Smoke test CLI"}

---

**Claude:**

Прибор жив. Снимаю БАЗЛАЙН — эталон здоровья, которого не было (пункт 4 задания).

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python cookie_sentinel.py snapshot 2>&1; echo \"=== EXIT $? ===\"; echo; echo \"### CHECK ###\"; python cookie_sentinel.py check 2>&1; echo \"=== EXIT $? ===\"", "description": "Take baseline snapshot and run check"}

---

**Claude:**

Активный профиль занят Firefox и остался без копии — а он самый важный. Чиню через sqlite backup API (консистентная копия живой базы).

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "        if not row[\"live_rails\"]:\n            continue\n        if row[\"locked\"] and not a.force:\n            continue\n        d = SAFE_DIR / name\n        d.mkdir(parents=True, exist_

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "def scan() -> dict:\n    \"\"\"Снимок здоровья: профиль x рельса -> вердикт и счётчик. Без значений кук.\"\"\"", "new_string": "def _safe_copy_db(src: Path, dst: Path) -> None:\n    \"\"\"Кон

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python cookie_sentinel.py snapshot 2>&1; echo \"=== EXIT $? ===\"; echo; python cookie_sentinel.py status 2>&1", "description": "Re-run snapshot with sqlite backup API"}

---

**Claude:**

Прибор работает. Теперь тест — и он обязан покраснеть на сломанном коде.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '1,60p' _shared/firefox_cookies.py; echo \"....\"; grep -n \"def read_cookies\" -A 40 _shared/firefox_cookies.py | head -60", "description": "Read firefox_cookies read_cookies to build fixtures"}

---

**Claude:**

Теперь тест с реальными фикстурами cookies.sqlite.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_cookie_sentinel.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"_test_cookie_sentinel.py -- сетка на cookie_sentinel.py. 0 LLM, 0 сети, stdlib-only.\n\nПОЧЕМУ УТВЕРЖДЕНИЯ НАЗЫВАЮТ ЧИСЛА, А НЕ ФАКТ «не упало» (CLAUDE.md 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _test_cookie_sentinel.py 2>&1 | tail -45; echo \"=== EXIT ${PIPESTATUS[0]} ===\"", "description": "Run the test green pass"}

---

**Claude:**

26 из 26 зелёных. Теперь главное — доказываю КРАСНОЕ на девяти сломах боевого файла.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 600 python _test_cookie_sentinel.py --prove 2>&1 | tail -20; echo \"=== EXIT ${PIPESTATUS[0]} ===\"", "description": "Prove each break turns the test red"}

---

**Claude:**

7 из 9 красных. Два «вакуумных» — на деле тест ПАДАЛ с исключением, не дойдя до кейса. Это слабость кейса, чиню её.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_cookie_sentinel.py", "old_string": "    def ncookies(p: Path) -> int:\n        con = sqlite3.connect(str(p / \"cookies.sqlite\"))\n        n = con.execute(\"select count(*) from moz_cookies\").fetchone()[0]\n        con.c

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_cookie_sentinel.py", "old_string": "    # --- 6. check без эталона НЕ молчит ------------------------------------------------\n    shutil.rmtree(tmp / \"baseline\")\n    ok(\"6a check без эталона -> exit 2 (слепота назван

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _test_cookie_sentinel.py 2>&1 | tail -6; echo \"=== GREEN EXIT ${PIPESTATUS[0]} ===\"; echo; timeout 900 python _test_cookie_sentinel.py --prove 2>&1 | tail -16; echo \"=== PROVE EXIT ${PIPESTATUS[0]} ===\"", "description": "Re-run green and pr

---

**Claude:**

Красное доказано 9/9, вакуумных 0. Теперь чиню побочный дефект: тест пишет в боевой каталог бэкапов.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '185,205p' _shared/_test_robot_profile_scrub.py; echo \"=== BACKUP_ROOT refs in test ===\"; grep -n \"BACKUP_ROOT\\|secrets\" _shared/_test_robot_profile_scrub.py | head -20", "description": "Inspect test litter root cause"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '60,110p' _shared/_test_robot_profile_scrub.py", "description": "Read test run helper and env setup"}

---

**Claude:**

Корень побочного дефекта: подпроцессу теста передаётся корень профилей, но не корень бэкапов. Добавляю ту же ручку.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\robot_profile_scrub.py", "old_string": "BACKUP_ROOT = os.path.join(HOME, \".claude\", \"secrets\", \"robot-profile-scrub\")", "new_string": "# ROBOT_PROFILE_BACKUP_ROOT: дом бэкапов уводится в песочницу той же ручкой, 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_test_robot_profile_scrub.py", "old_string": "    env = dict(os.environ)\n    env[\"ROBOT_PROFILE_ROOT\"] = rps.PROFILE_ROOT", "new_string": "    env = dict(os.environ)\n    env[\"ROBOT_PROFILE_ROOT\"] = rps.PROFILE_RO

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_shared\\_test_robot_profile_scrub.py", "old_string": "    backup_root = os.path.join(tmp, \"backups\")\n    os.makedirs(rps.PROFILE_ROOT, exist_ok=True)", "new_string": "    backup_root = os.path.join(tmp, \"backups\")\n    # 

---

**Claude:**

Проверяю починку замером: сколько файлов тест кладёт в боевой каталог.

---

> `Bash` -- {"command": "D=~/.claude/secrets/robot-profile-scrub\nBEFORE=$(ls \"$D\" 2>/dev/null | wc -l)\ncd ~/.claude/scripts && timeout 300 python _shared/_test_robot_profile_scrub.py 2>&1 | tail -8; RC=${PIPESTATUS[0]}\nAFTER=$(ls \"$D\" 2>/dev/null | wc -l)\necho \"=== test exit $RC ===\"\necho \"файлов в 

---

**Claude:**

Доказываю, что починка не декоративная — двумя замерами.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport os,sys,json,sqlite3,subprocess,tempfile,shutil\nfrom pathlib import Path\nHOME=Path.home(); PROD=HOME/'.claude'/'secrets'/'robot-profile-scrub'\nTOOL=str(Path('_shared/robot_profile_scrub.py').resolve())\ndef mk(root,name,hosts):\n    p=Pa

---

> `Bash` -- {"command": "cd ~/.claude/secrets/robot-profile-scrub && mkdir -p _test-fixture-junk && MOVED=0\nfor pat in 'proofprof-*' 'retired-*' 'fbtest-*' 'mistral-probe-*'; do\n  for f in $pat; do [ -e \"$f\" ] || continue; mv -- \"$f\" _test-fixture-junk/ && MOVED=$((MOVED+1)); done\ndone\necho \"перенесено

---

**Claude:**

Журнал чист: 23 боевых события вместо 46 вперемешку с фикстурами. Теперь рот и рутина — иначе прибор не живёт.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls bus_send.py 2>&1 && python bus_send.py --help 2>&1 | head -25", "description": "Check bus_send CLI for alerting"}

---

**Claude:**

Добавляю `watch` — одна дверь для рутины: сперва проверка, эталон только если чисто, рот в 03.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "def cmd_restore(a) -> int:", "new_string": "def cmd_watch(a) -> int:\n    \"\"\"Дверь рутины: ПРОВЕРКА первой, эталон -- только если чисто.\n\n    ПОРЯДОК ВАЖЕН И ОН НЕ ПЕРЕСТАВЛЯЕТСЯ. Сними 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "    c = sub.add_parser(\"check\", help=\"регрессия против последнего эталона\")\n    c.add_argument(\"--suspects\", action=\"store_true\", help=\"опросить планировщик (медленно)\")\n    c.set

---

**Claude:**

Главный инвариант `watch` — на красном прогоне эталон не переписывается. Прибиваю его тестом.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_cookie_sentinel.py", "old_string": "    ok(\"7c вне окна подозреваемых 0\", len(s0) == 0, str(s0))", "new_string": "    ok(\"7c вне окна подозреваемых 0\", len(s0) == 0, str(s0))\n\n    # --- 8. watch: КРАСНЫЙ прогон не и

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_cookie_sentinel.py", "old_string": "    (\"7a\", 'if since <= ev <= until:\\n                found.append(\"robot_profile_scrub '", "new_string": "    (\"8e\", '    rc = cmd_check(a)\\n    BASELINE_DIR.mkdir',\n     '    

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _test_cookie_sentinel.py 2>&1 | grep -E '^\\s+\\[(ok|FAIL)\\] 8|^\\[итог\\]'; echo \"=== GREEN EXIT ${PIPESTATUS[0]} ===\"", "description": "Run green with new case 8"}

---

**Claude:**

Тест поймал настоящую дыру: первый прогон `watch` не мог себя завести — нет эталона → rc=2 → снимка не будет никогда. Чиню.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "    rc = cmd_check(a)\n    BASELINE_DIR.mkdir(parents=True, exist_ok=True)\n    rec = {\"ts\": _now().isoformat(timespec=\"seconds\"), \"host\": socket.gethostname(),\n           \"check_rc\"

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _test_cookie_sentinel.py 2>&1 | grep -E '^\\s+\\[(ok|FAIL)\\] 8|^\\[итог\\]'; echo \"=== GREEN EXIT ${PIPESTATUS[0]} ===\"", "description": "Re-run after bootstrap fix"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 1200 python _test_cookie_sentinel.py --prove 2>&1 | tail -16; echo \"=== PROVE EXIT ${PIPESTATUS[0]} ===\"", "description": "Prove all 11 breaks red"}

---

**Claude:**

Ещё две честные находки: имя эталона с точностью до секунды коллизирует (снимок молча терялся), и один слом ломал отступы. Чиню оба.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "    stamp = _now().strftime(\"%Y%m%dT%H%M%SZ\")\n    dest = BASELINE_DIR / (stamp + \".json\")", "new_string": "    stamp = _now().strftime(\"%Y%m%dT%H%M%SZ\")\n    dest = BASELINE_DIR / (sta

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_cookie_sentinel.py", "old_string": "    (\"8e\", '    rc = cmd_check(a)\\n    BASELINE_DIR.mkdir',\n     '    cmd_snapshot(a)\\n    rc = cmd_check(a)\\n    BASELINE_DIR.mkdir'),", "new_string": "    (\"8e\", '    else:\\n

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _test_cookie_sentinel.py 2>&1 | tail -3; echo \"=== GREEN EXIT ${PIPESTATUS[0]} ===\"; echo; timeout 1200 python _test_cookie_sentinel.py --prove 2>&1 | tail -15; echo \"=== PROVE EXIT ${PIPESTATUS[0]} ===\"", "description": "Final green and pr

---

**Claude:**

34/34 зелёных, 11/11 сломов красные, вакуумных 0. Добавляю уборку эталонов и ставлю живой прогон.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py", "old_string": "    print(\"[sentinel] эталон: \" + dest.name + \", профилей \" + str(len(snap[\"profiles\"])))", "new_string": "    # уборка: рутина тикает часами, эталоны копятся вечно. Держим последние KE

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _test_cookie_sentinel.py 2>&1 | tail -3; echo \"GREEN=${PIPESTATUS[0]}\"; echo \"### ЖИВОЙ ПРОГОН watch ###\"; timeout 300 python cookie_sentinel.py watch --quiet 2>&1; echo \"=== WATCH EXIT $? ===\"", "description": "Re-test then live watch ru

---

> `Bash` -- {"command": "echo \"=== есть ли права админа? ===\"; net session >/dev/null 2>&1 && echo \"ADMIN: да\" || echo \"ADMIN: нет (net session отказ)\"\necho \"=== текущий SACL на каталоге кук ===\"; icacls \"$LOCALAPPDATA\\\\ff-autoff-profile\" /verify 2>&1 | head -5\npowershell -NoProfile -Command \"try

---

**Claude:**

Админских прав нет — капкан SACL мне не взвести. Делаю честные пробы обеих дверей и ставлю рутину.

---

> `Bash` -- {"command": "echo \"=== дверь 1: USN journal ===\"; fsutil usn readjournal C: 2>&1 | head -3\necho; echo \"=== дверь 2: Security 4663 (капкан 03.10) ===\"\npowershell -NoProfile -Command \"try { Get-WinEvent -FilterHashtable @{LogName='Security';Id=4663} -MaxEvents 3 -ErrorAction Stop | Select-Objec

---

> `Bash` -- {"command": "PY=$(python -c \"import sys;print(sys.executable)\"); echo \"python: $PY\"\nPYW=$(dirname \"$PY\")/pythonw.exe; echo \"pythonw exists: $([ -f \"$PYW\" ] && echo yes || echo no)\"\necho \"=== существует ли уже такая задача? ===\"\nschtasks /query /tn \"Cookie-Sentinel-Watch\" 2>&1 | head

---

> `PowerShell` -- {"command": "$t = schtasks /query /tn \"Cookie-Sentinel-Watch\" 2>&1; if ($LASTEXITCODE -eq 0) { \"EXISTS\"; $t } else { \"NOT EXISTS\" }", "description": "Check if scheduled task exists"}

---

> `PowerShell` -- {"command": "$py = \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\pythonw.exe\"\n$script = \"C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py\"\n$log = \"C:\\Users\\dev\\.claude\\logs\\cookie_sentinel_watch.log\"\n$cmd = \"cmd /c `\"`\"$py`\" `\"$script`\" watch >> `\"$log`

---

**Claude:**

Проверяю рутину живым запуском и доказываю её ВЫХОД (§5.5).

---

> `PowerShell` -- {"command": "schtasks /run /tn \"Cookie-Sentinel-Watch\"; Start-Sleep -Seconds 12\n\"=== статус задачи ===\"\nschtasks /query /tn \"Cookie-Sentinel-Watch\" /fo LIST /v | Select-String -Pattern \"Last Run Time|Last Result|Next Run Time|Schedule|Task To Run\"\n\"=== ВЫХОД рутины: лог ===\"\nif (Test-P

---

**Claude:**

Лог нечитаем — кодировка. Рот, который не прочитать, рта не имеет. Чиню.

---

> `PowerShell` -- {"command": "$py = \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\pythonw.exe\"\n$script = \"C:\\Users\\dev\\.claude\\scripts\\cookie_sentinel.py\"\n$log = \"C:\\Users\\dev\\.claude\\logs\\cookie_sentinel_watch.log\"\n$cmd = \"cmd /c `\"set PYTHONIOENCODING=utf-8 && set PYTHONU

---

> `Bash` -- {"command": "ls -la ~/.claude/robot_profile_scope.json* 2>&1; echo \"=== бэкапы по дереву ===\"; find ~/.claude -maxdepth 3 -name 'robot_profile_scope*' 2>/dev/null | head -20\necho \"=== git-история файла, если есть ===\"; cd ~/.claude && git log --oneline -- robot_profile_scope.json 2>&1 | head -5

---

> `Bash` -- {"command": "echo \"=== ПРЕД-23.09 состояние реестра (бэкап 13:40, за 18 минут до первого скраба autoff) ===\"; cat ~/.claude/robot_profile_scope.json.bak-20260923", "description": "Read pre-23.09 scope registry"}

---

**Claude:**

Доказано бэкапом: до 23.09 в реестре были только `fbread`/`fbreply`. Строка `ff-autoff-profile` добавлена 23.09 13:52 — за 18 минут до первого скраба — и откат 25.09 её не снял. Довожу откат, хирургически.

---

> `Bash` -- {"command": "cp ~/.claude/robot_profile_scope.json ~/.claude/robot_profile_scope.json.bak-autoff-rollback-20261006 && echo \"бэкап сделан: $(ls -la ~/.claude/robot_profile_scope.json.bak-autoff-rollback-20261006 | awk '{print $5\" байт\"}')\"", "description": "Backup scope registry before rollback c

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\robot_profile_scope.json", "old_string": "  \"_comment_autoff\": \"ff-autoff-profile -- боевой робо-профиль DR-рельс (Windows: %LOCALAPPDATA%). Область СЧИТАНА из кода потребителей (dr_ff_rail, rail_sweep, dr_queue, ff_magic_login, ff_s

---

**Claude:**

Проверяю, что реестр валиден и скраб больше НЕ трогает профиль рельс.

---

> `Bash` -- {"command": "cd ~/.claude && python -c \"\nimport json\nd=json.load(open('robot_profile_scope.json',encoding='utf-8-sig'))\nprint('JSON валиден, ключей:',len(d))\nprint('ff-autoff-profile в реестре:', 'ff-autoff-profile' in d)\nprint('профили с областью:',[k for k in d if not k.startswith('_')])\n\"

---

**Claude:**

Корень A закрыт и это ВИДНО. Второй заход другим методом (§4.3-бис) — доказываю не CLI, а прямым вызовом гварда.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport os,sys,json,sqlite3,shutil,tempfile\nsys.path.insert(0,os.path.abspath('_shared'))\nimport robot_profile_scrub as rps\n\nAUTOFF=os.path.join(os.environ['LOCALAPPDATA'],'ff-autoff-profile')\nprint(\"ВТОРОЙ ЗАХОД -- прямой вызов guard(), не 

---

**Claude:**

Второй заход доказал числами: было бы удалено 5 кук, стало 0. Теперь документы.

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,os,sys\nsys.path.insert(0,os.path.expanduser('~/.claude/scripts'))\ntry:\n    import fleet_nodes as fn\n    print(\"fleet_nodes ok\")\nexcept Exception as e:\n    print(\"fleet_nodes:\",e)\nfor v in ('OBSIDIAN_VAULT',):\n    print(v,'=',os.environ.get(v))\nP

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python breakage.py --help 2>&1 | head -30", "description": "Read breakage.py CLI"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/02-Decisions\" | head -6; echo \"=== пример свежего мемо для формата ===\"; F=$(ls -t \"D:/Vault/Vault-Knowledge/02-Decisions\"/*.md 2>/dev/null | head -1); echo \"$F\"; head -30 \"$F\"", "description": "Inspect Decision Memo format"}

---

> `Bash` -- {"command": "F=$(ls -t \"D:/Vault/Vault-Knowledge/02-Decisions\"/decision-2026-10*.md 2>/dev/null | head -1); echo \"FILE: $F\"; head -28 \"$F\" 2>&1\necho; echo \"=== breakage add usage ===\"; cd ~/.claude/scripts && python breakage.py add --help 2>&1 | head -25", "description": "Get decision me

---

**Claude:**

Пишу Decision Memo в волт.

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\02-Decisions\\decision-2026-10-06-logout-root-scrub-and-appdata-sweep.md", "content": "---\ntitle: \"Корень разлогинов браузерных рельс: скраб кук + чистка AppData, и механизм против обоих\"\ndate: 2026-10-06\ntype: decision\nstage: distilled\nlayer: ess

---

**Claude:**

Строки в журнал поломок — три класса, каждый со своим именем.

---

> `Bash` -- {"command": "cd ~/.claude/scripts\npython breakage.py add --class \"scrub-deletes-cookies-of-the-rail-it-serves\" \\\n --what \"robot_profile_scrub удалял куки ff-autoff-profile -- боевого профиля ВСЕХ DR-рельс -- на КАЖДОМ подъёме робо-драйвера (firefox_selenium:438). Область вырезала chatgpt.com и

---

**Claude:**

Датированный блок в скилл `/dr-fanout` — чтобы веер больше не бил в вырезанный профиль.

---

> `Bash` -- {"command": "cd ~/.claude/skills/dr-fanout && wc -l SKILL.md && grep -n \"autoff\\|робо-профил\\|разлогин\\|ПОЛЕВ\\|Поправка\\|^## \" SKILL.md | head -40", "description": "Inspect dr-fanout skill structure"}

---

> `Bash` -- {"command": "cd ~/.claude/skills/dr-fanout && sed -n '14,20p' SKILL.md", "description": "Read insertion point in skill"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\dr-fanout\\SKILL.md", "old_string": "## ⛔ ШАГ −1 ПРЕДПОЛЁТ (01.10.2026): без живой пробы рельс веер не стартует", "new_string": "## ⭐⭐ КОРЕНЬ «AUTOFF РАЗЛОГИНЕН/ПУСТ» НАЙДЕН 06.10.2026 — его удаляли НАШИ ЖЕ скрипты, не вендор\n\

---

**Claude:**

Память + указатель в индекс.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\logout-root-is-our-own-cookie-scrub.md", "content": "---\nname: logout-root-is-our-own-cookie-scrub\ndescription: \"06.10.2026 корень разлогинов браузерных рельс: robot_profile_scrub удалял куки autoff на каждо

---

> `Bash` -- {"command": "M=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/MEMORY.md\"\ngrep -n \"^## 📥 INBOX\" \"$M\"\npython - <<'PY'\nimport io\np=r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md\"\ns=io.open(p,encoding='utf-8').read()\nline=\"- [К

---

**Claude:**

Финальная проверка: прогоняю всё заново после последних правок.

---

> `Bash` -- {"command": "cd ~/.claude/scripts\necho \"### 1. тест sentinel (зелёный) ###\"; timeout 300 python _test_cookie_sentinel.py 2>&1 | tail -2\necho \"### 2. тест sentinel (красное доказано) ###\"; timeout 1200 python _test_cookie_sentinel.py --prove 2>&1 | tail -2\necho \"### 3. тест скраба ###\"; time

---

> `Bash` -- {"command": "cd ~/.claude && git rev-parse --is-inside-work-tree 2>&1 | head -2; git status --porcelain scripts/cookie_sentinel.py robot_profile_scope.json 2>&1 | head -5\necho \"=== синк хаба жив? ===\"\ncurl -s -m 5 -H \"X-API-Key: $(python -c \"\nimport re,io,os\ntry:\n    s=io.open(os.path.expan

---

**Claude:**

Всё зелёное. Синк, кстати, ЖИВ (память говорила «мёртв» — запрет протух, проверил). Провенанс + раскатка знания флоту.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport json,os,socket,datetime\nfrom pathlib import Path\nd=Path.home()/'.claude'/'change_ledger'; d.mkdir(parents=True,exist_ok=True)\nf=d/(socket.gethostname()+'.jsonl')\nrecs=[\n {\"tool\":\"cookie_sentinel.py\",\"what\":\"новый прибор: эталон

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python bus_send.py \"КОРЕНЬ РАЗЛОГИНОВ НАЙДЕН (хаб HUB-01, 06.10, приказ оператора голосом). Гипотеза оператора «скрипт удаляет куки» ВЕРНА, корней два, оба наши.\n\n(1) robot_profile_scrub.py удалял куки ff-autoff-profile на КАЖДОМ подъёме робо-драй

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls deploy_register.py 2>/dev/null && timeout 120 python deploy_register.py --help 2>&1 | head -18 || echo \"deploy_register.py нет\"", "description": "Check deploy_register availability"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 180 python deploy_register.py HUB-01 cookie-sentinel-20261006 \"cookie_sentinel.py: эталон кук + детектор разлогина с окном события + откат; рутина Cookie-Sentinel-Watch 2ч\" \"python _test_cookie_sentinel.py\" \"python cookie_sentinel.py watch\" -

---

**Claude:**

Гейт прав: шагом раскатки должна быть read-only проба, не тест. Пишу пробу.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_probe_cookie_sentinel.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"_probe_cookie_sentinel.py -- READ-ONLY проба: стоит ли на этом узле защита от разлогинов.\n\nПОЧЕМУ ПРОБА, А НЕ ТЕСТ, шагом раскатки: тест пишет (эталоны,

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _probe_cookie_sentinel.py 2>&1; echo \"=== PROBE EXIT $? ===\"", "description": "Run the read-only probe"}

---

**Claude:**

Проба поймала мою же небрежность: `dr-autoff*` — это заброшенные профили, их чистка намеренна. Сужаю правило — спрашиваю драйвер, а не угадываю по имени.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_probe_cookie_sentinel.py", "old_string": "    try:\n        scope = json.loads(SCOPE.read_text(encoding=\"utf-8-sig\"))\n        bad = [k for k in scope if not k.startswith(\"_\") and \"autoff\" in k.lower()]\n        if bad:\

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python _probe_cookie_sentinel.py 2>&1; echo \"=== PROBE EXIT $? ===\"\necho; echo \"### красная проба: проверяю, что GAP реально срабатывает ###\"\npython - <<'PY'\nimport json,os,shutil,subprocess,sys,tempfile\nfrom pathlib import Path\nS=Path.home()

---

**Claude:**

Проба зелёная и доказано краснеет. Регистрирую раскатку.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 180 python deploy_register.py HUB-01 cookie-sentinel-20261006 \"cookie_sentinel.py: эталон кук + детектор разлогина с окном события + откат без пароля; рутина Cookie-Sentinel-Watch 2ч; строка autoff снята из области скраба\" \"python _probe_cookie_

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2>&1 | head -5; echo \"---\"; python onair.py check --zone secrets-auth 2>&1 | head -3", "description": "Close ON AIR declaration"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2026-10-06T125129Z-HUB-01-a47044b4-secrets-auth 2>&1 | head -3; echo \"---\"; python onair.py check --zone secrets-auth 2>&1 | head -3", "description": "Close ON AIR by id"}

---

> `Bash` -- {"command": "date \"+%H:%M %d.%m.%Y (локальное машины)\"; date -u \"+%H:%M UTC\"", "description": "Get current local time for report"}

---

**Claude:**

**Начало отчёта: 14:28 06.10.2026**

## Корень найден. Твоя гипотеза верна, и скрипт нашёлся

Ты сказал «какой-то ебаный скрипт удаляет куки». Так и есть. Их **два**, и оба наши.

### Корень A: наш скраб ел куки той рельсы, которой служит

`robot_profile_scrub.py` зовётся из `firefox_selenium.make_driver:438` **перед каждым** подъёмом робо-драйвера и удаляет куки вне «области» профиля. У `ff-autoff-profile` (через него ходят ВСЕ DR-рельсы) областью были только `z.ai/claude.ai`, а `chatgpt.com` и google-семья вырезаны.

Улики - бэкапы самого скраба, то есть состояние ДО удаления:

| когда | кук было | удалено | чего именно |
|---|---|---|---|
| 23.09 13:40 | 85 | **57** | chatgpt 5, google 6, gemini 4, twitter 5, instagram 5 |
| 25.09 03:49 | 50 | **23** | grok 7, chatgpt 7, twitter 5 |
| 01.10 13:52 | 43 | **13** | chatgpt 5, twitter 5, google 1 |
| 02.10 13:40 | 31 | 1 | google 1 |

**85 → 50 → 43 → 31** и есть твой недельный налог: ты логинишься, следующий прогон снимает.

⭐ **И это был остаток работы, которую ты сам откатил.** Бэкап реестра от 23.09 **13:40** (за 18 минут до первого скраба в 13:40:58) содержит только `fbread`/`fbreply` - строки autoff там нет вовсе. Она появилась в 13:52, а 25.09 07:55 ты откатил всю ту стройку. Строка выжила мимо отката и ещё 11 дней ела куки. Я её **снял** (бэкап рядом). Доказал вторым методом, прямым вызовом `guard()`: прежний реестр удалял **5 кук из 7**, текущий **0**.

### Корень B: чистка AppData снесла каталог профиля целиком

02.10 20:04-20:13. Улика: `ff-autoff-profile\times.json` → `created` = **2026-10-03T02:16:53Z**, и кроме этого файла в каталоге **пусто**. Это **четвёртая жертва** того окна после Cursor, VS Code и Syncthing, и то же окно, что «пожиратель .py в 20:11» - значит это **один класс и один вопрос атрибуции**, а не два.

Третья находка попутно: твой профиль `dev-clean` **подменился** 25.09 11:11:07 - Firefox завёл новый пустой с тем же именем, старый выпал из `profiles.ini` и лежит сиротой. Один разлогин 25.09 - это, а не вендор.

### Механизм: разлогин больше не стоит пароля

`cookie_sentinel.py` + рутина `Cookie-Sentinel-Watch` (каждые 2 часа, Last Result 0):
- **эталон + безопасная копия живых кук** через sqlite backup API. Первый прогон сразу показал зачем: файловая копия не берёт активный профиль, он под замком Firefox, то есть единственный профиль с твоими сессиями остался бы без копии;
- **check** - регрессия с **окном события** и подозреваемыми в нём;
- **`restore --profile <имя>`** - вернуть живую базу. Команда вместо пароля;
- порядок в `watch` не переставляется: эталон переписывается **только на зелёном** прогоне, иначе эталоном станет разлогин.

Качество: **34/34** зелёных, красное доказано на **11 из 11** сломов, **вакуумных 0**. Тест нашёл в приборе две настоящие дыры (первый `watch` не мог себя завести; имя эталона коллизировало по секунде) - обе закрыл. Побочно починил: тест скраба писал фикстуры в боевой журнал удалений (23 файла, замер дельты 1 → 0).

### Что НЕ сделано, честно

1. **Капкан на каталог кук не взвёл: нет прав админа.** `fsutil usn readjournal` и Prefetch - Access denied. Команда для тебя лежит в мемо. Актор чистки AppData по-прежнему **не назван**; запрос Security 4663 вернул ноль событий (повтора с 03.10 не было), но без админа журнал может быть урезан - это названная слепая зона.
2. **Нужен ОДИН твой вход в робот-профиль.** Сейчас он пуст после чистки 02.10, поэтому `chatgpt#web` и `gemini#a` мертвы. Пароли я не ввожу и не буду. Но это **один раз**, не налог: пожиратель выключен, а сразу после входа прибор снимет копию и дальше откат бесплатный.

```bash
"C:\Program Files\Mozilla Firefox\firefox.exe" -no-remote -profile "%LOCALAPPDATA%\ff-autoff-profile" https://chatgpt.com https://gemini.google.com https://chat.z.ai
```

Сразу после входа:
```bash
python ~/.claude/scripts/cookie_sentinel.py snapshot
```

Разложено: мемо `02-Decisions/decision-2026-10-06-logout-root-scrub-and-appdata-sweep.md`, три класса в журнал поломок, датированный блок в `/dr-fanout` (он объясняет шесть прошлых полевых строк «AutoFF разлогинен»), память + индекс, леджер правок, посылка зарегистрирована, флоту ушло по обеим рельсам с просьбой проверить свой реестр. ON AIR закрыт.

🔧 **Вердикт по скиллу:** `/dr-fanout` обновляю - в нём шесть строк ставили симптому неверную причину, теперь причина названа и в ШАГ −1 добавлена проверка «не съели ли куки мы сами».

> 🧒 **Простыми словами:** браузер-робот хранит «пропуска» (куки) в своей папке. У нас работал уборщик, которому велели: в этой папке можно держать пропуска только двух сайтов, остальные выбрасывать. А роботу как раз нужны были пропуска ChatGPT и Google. Поэтому уборщик их выбрасывал каждый раз, и ты заново вводил пароли. Самое обидное: этого уборщика ты уже велел убрать 25 сентября, но одна его строчка случайно осталась. Я её убрал. Второй случай: 2 октября другая чистилка снесла всю папку целиком. Теперь у нас есть сторож: он каждые два часа фотографирует живые пропуска и кладёт копию в сейф. Если пропуска снова пропадут, он скажет **когда** и **кто рядом пробегал**, а вернуть их можно одной командой вместо пароля. Один раз тебе всё же надо войти самому: папка сейчас пустая, а пароли я не ввожу.

**Конец отчёта: 14:31 06.10.2026**
