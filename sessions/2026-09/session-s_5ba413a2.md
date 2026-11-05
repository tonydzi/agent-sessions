---
session: s_5ba413a2
date: 2026-09-03
words: 2463
turns: 17
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-03 · Scheduled run: auto-hub-260811-retro-lost-nightly

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5ba413a2` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260811-retro-lost-nightly" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260811-retro-lost-nightly\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: auto-hub-260811-retro-lost-nightly
description: Ночная догонялка - ретро для 10 брошенных сессий (>5 дн, ретро не делалось) по скиллу /retro-lost
model: opus
---

МОДЕЛЬ (канон §6.2): вердикты ретро пишутся в канон-дома — работать на Opus-классе или сильнее. Проверь модель сессии первым делом (системный промпт, «You are powered by...»); если Sonnet/Haiku — НЕ делать ретро, доложить в 03 «retro-lost: пропуск, модель ниже Opus» и закончить.

ПРОФИЛЬ: ХАБ-ПОЛНЫЙ (секция «ДВА ПРОФИЛЯ» скилла). Строка профиля обязательна — сид без неё по канону скилла падает в ПИР-ЛАЙТ, и хаб молча резал бы себе ретро вдвое.

Задача: закрыть ретро для 10 ЕДИНИЦ работы по скиллу /retro-lost (батч сессий одной рутины по полю hint = одна единица, mark-done всем участникам батча; правка 22.08). В конце прогона шаг 9 скилла (личинка спотыканий) обязателен. Инструкция целиком в C:\Users\dev\.claude\skills\retro-lost\SKILL.md — прочитай её первой и следуй ей, это единственный источник логики (не воспроизводи по памяти).

Конвейер:
1. `python %USERPROFILE%\.claude\scripts\retro_lost_scan.py list --top 10` — очередь кандидатов (свежие первыми).
2. Для каждого: шаги 0-8 скилла. Ключевое: транскрипт читать экономно (голова+хвост+grep, >2МБ целиком никогда); RECALL-сверка перед каждым выводом (урок уже записан → дубль не создаём); тесты живых артефактов — внешней панелью secondop, не своими токенами; дока — docstring в код, не отдельные .md; финал каждой сессии = ретро-заметка в волт + `retro_lost_scan.py mark-done <sessionId> --note "..."`.
3. Не успел 10 до 06:00 — остановись на целых сессиях (mark-done только полностью закрытым).
4. ⏰ УРОЖАЙ ТЕНИ (одноразово, в прогоне 29.08 или первом после): собрать итог личинки шага 9 (строки журнала за 7 ночей, дошёл ли хоть один класс до счёта 3 или опровержения), вписать вердикт в Shadow-First-Queue строку «личинка-спотыканий» и добавить его в строку отчёта в 03. 0 строк при видимых спотыканиях = личинка мертва, снять шаг 9 из скилла.

В конце ОДНА строка в 03 через `python %USERPROFILE%\.claude\scripts\bus_send.py`: «retro-lost: закрыто N из 10, очередь M, контрибьют-кандидатов K».

Границы: код брошенных сессий не чинить (карв-ауты Breakage-Journal — исключение); дочерние сессии не поднимать без RECALL-доказательства; Tier-2 находки (секреты в транскриптах) → аск в 02 немедленно.
</scheduled-task>

---

**Claude:**

I'll start by reading the skill that defines this task's logic.

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/skills/retro-lost/SKILL.md\"", "description": "Read retro-lost skill"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python retro_lost_scan.py list --top 10 2>&1 | head -60", "description": "List retro-lost queue"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && for s in s_64b78a0b s_a71372e1 s_cdb5b08c s_733bc04f s_f0ecd93c s_5f3c0b9b e535e209-54a6-4

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -n \"retro_mode\\|MIN_AGE\\|MAX_AGE\" retro_lost_scan.py | head -20; echo ---; ls retro_lost_extract.py && head -30 retro_lost_extract.py", "description": "Check scanner modes and extractor"}

---

**Claude:**

All 10 claimed. Ages 5.0–5.5 дн → по оси возраста в основном `lite`. Читаю транскрипты экстрактором.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && for s in s_f0ecd93c s_5f3c0b9b s_8c344b9a; do echo \"=== $s ===\"; python retro_lost_extract.py \"C:\\\\Users\\\\dev\\\\.claude\\\\projects\\\\E--Obsidian--imports-al

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== f54d7f97 ===\"; python retro_lost_extract.py \"C:\\\\Users\\\\dev\\\\.claude\\\\projects\\\\E--Obsidian--imports-sostav\\\\s_786bc3f4.jsonl\" 5 2>&1 | head -60; echo \"=== 5cb0bd00 fbcomments ===\"; python r

---

**Claude:**

Опечатка в моей команде (экранированный `$`), повторяю:

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && for s in s_f0ecd93c s_5f3c0b9b s_8c344b9a; do echo \"=== $s ===\"; python retro_lost_extract.py \"C:/Users/dev/.claude/projects/E--Obsidian--imports-alpha/${s}.jsonl\

---

**Claude:**

Батч SOSTAV-судьи вскрыл реальный инцидент. Читаю остальные пять.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== 99f84df7 inbox-processor ===\"; python retro_lost_extract.py \"C:/Users/dev/.claude/projects/C--Users-dev/s_a71372e1.jsonl\" 3 2>&1 | tail -35; echo; echo \"=== 77908637 token-watchdog ===\"; python retro_

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== eb9728c0 n8n-voice ===\"; python retro_lost_extract.py \"C:/Users/dev/.claude/projects/C--Users-dev/s_733bc04f.jsonl\" 3 2>&1 | tail -45", "description": "Extract n8n voice session"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== e535e209 (9MB) ===\"; python retro_lost_extract.py \"C:/Users/dev/.claude/projects/C--Users-dev--CLAUDE-NODE-0X-May26/s_d1c65808.jsonl\" 3 2>&1 | tail -50", "description": "Extract 9MB DR session"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && echo \"=== faebe6fc (PR chip) ===\"; python retro_lost_extract.py \"C:/Users/dev/.claude/projects/C--Users-dev--CLAUDE-NODE-0X-May26/s_a92e7320.jsonl\" 3 2>&1 | tail -45", "description": "Extract PR chip session"}

---

**Claude:**

Все 10 разобраны на 7 единиц. Теперь RECALL-сверка судьбы каждой находки с СЕГОДНЯШНИМ состоянием диска.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/alpha/candidates\" 2>/dev/null && ls -la --time-style=long-iso sostav-judged-latest.md fbcomments-judged-latest.md 2>&1 | head; echo \"=== свежие sostav-nightly ===\"; ls -t sostav-nightly-*-report.md 2>/dev/null | head -3; echo \"=== задачи планировщика по sos

---

> `Bash` -- {"command": "ls -la --time-style=long-iso \"D:/Vault/_imports/n8n/big_video_bridge.py\" \"D:/Vault/_imports/n8n/_test_big_video_bridge.py\" 2>&1; echo \"=== планы шины ===\"; ls -t \"D:/Vault/Vault-Knowledge/_machine-bus/_plans/\" 2>/dev/null | head -6; echo \"=== heartbeat рутин ===\"; ls 

---

> `Bash` -- {"command": "ls -d \"C:/Users/dev/.claude/_cron_heartbeat\" \"D:/Vault/_imports/_cron_heartbeat\" 2>&1; find \"C:/Users/dev/.claude\" \"D:/Vault/_imports\" -maxdepth 2 -name \"_cron_heartbeat\" -type d 2>/dev/null; echo \"=== SostavJudgeDigest: команда и промпт ===\"; powershell -NoProfile

---

> `Bash` -- {"command": "grep -rl \"big_video_bridge\" \"C:/Users/dev/.claude\" \"D:/Vault/_imports\" 2>/dev/null | head -10; echo \"=== есть ли задача в планировщике вообще про n8n/audio/voice ===\"; powershell -NoProfile -Command \"Get-ScheduledTask | Where-Object {\\$_.TaskName -match 'n8n|audio|Voice|b

---

> `Bash` -- {"command": "cat \"D:/Vault/_imports/sostav/sostav_judge.cmd\" 2>&1 | head -30; echo \"=== ищу файл промпта судьи ===\"; ls -la --time-style=long-iso \"D:/Vault/_imports/sostav/\" 2>/dev/null | grep -iE \"judge|prompt\" | head", "description": "Inspect sostav judge task command"}

---

> `Bash` -- {"command": "ls -t \"C:/Users/dev/.claude/scripts/_cron_heartbeat/\" 2>/dev/null | head -20; echo \"=== возраст ключевых ===\"; ls -la --time-style=long-iso \"C:/Users/dev/.claude/scripts/_cron_heartbeat/\" 2>/dev/null | grep -iE \"sostav|fbcomment|token|inbox|video\" | head", "description": "Ch

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/sostav\" && grep -n \"settlement\\|OTC\\|cash-to-crypto\\|opus\\|sonnet\\|--model\" sostav_judge.cmd | head -20; echo \"=== ЧТО ИЗМЕНИЛОСЬ 28.08 20:34 -> 20:37 ===\"; diff <(cat sostav_judge.cmd.bak-pre-opus-20260828) <(cat sostav_judge.cmd) | head -40", "descr

---

**Claude:**

Ключевая находка батча: исправление 28.08 **доехало в рутину** (бриф + модель sonnet→opus). Проверяю судьбу самого лида.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/sostav\" && tail -25 _judge_log.txt; echo \"=== доставка: есть ли рот ===\"; ls -la --time-style=long-iso sostav_deliver.py 2>&1; grep -c \"deliver\" sostav_judge.cmd", "description": "Check judge log freshness and delivery leg"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5ba413a2/tasks/bgxd7q34u.output\" 2>/dev/null | head -20", "description": "Read background grep result"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,io\np=r\"C:\\Users\\dev\\.claude\\.stversions\\scripts\\_shared\\_orphan_engines_state.json\"\ntry:\n    d=json.load(open(p,encoding=\"utf-8\"))\nexcept Exception as e:\n    print(\"ERR\",e); raise SystemExit\ns=json.dumps(d,ensure_ascii=False)\nimport re\

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && ls -t 07-People/ 2>/dev/null | head -5; echo \"=== карточки лидов с 29.08 ===\"; find 07-People 10-Tasks -name \"*.md\" -newermt \"2026-08-29\" 2>/dev/null | head -10; echo \"=== упоминания судейских лидов ===\"; grep -rl \"Till\\|Nik\\b\" 07-People

---

> `Bash` -- {"command": "ls -la --time-style=long-iso \"D:/Vault/_imports/n8n/big_video_bridge.cmd\" 2>&1; echo \"=== задачи планировщика (полный список, фильтр) ===\"; powershell -NoProfile -Command \"Get-ScheduledTask | Select-Object -ExpandProperty TaskName\" 2>&1 | grep -iE \"video|bridge|n8n|audio\" ; e

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/sostav\" && grep -n \"leads.db\\|crm\\|card\\|карточк\" sostav_deliver.py | head -10; echo \"=== рот = только Saved Messages? ===\"; grep -n \"def \\|Saved\" sostav_deliver.py | head -15", "description": "Check whether judge delivery has a CRM leg"}

---

**Claude:**

Проверяю обе находки вторым прибором, прежде чем записывать вывод.

---

> `Bash` -- {"command": "cat \"D:/Vault/_imports/n8n/big_video_bridge.cmd\"; echo \"=== кто ссылается на big_video_bridge (узко) ===\"; grep -rl \"big_video_bridge\" \"D:/Vault/_imports/n8n\" \"C:/Users/dev/.claude/scripts\" \"C:/Users/dev/.claude/skills\" 2>/dev/null | head; echo \"=== задача 'Claude

---

> `Bash` -- {"command": "grep -rl \"sostav-judged-latest\" \"C:/Users/dev/.claude/scripts\" \"D:/Vault/_imports/sostav\" \"D:/Vault/_imports/alpha\" \"C:/Users/dev/.claude/skills\" 2>/dev/null | head -10; echo \"=== leads.db: есть ли что-то из клуба за 29.08-03.09 ===\"; python - <<'PY'\nimport sqlite

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/alpha\" && grep -n \"sostav-judged\" -A4 -B4 alpha_harvest.py | head -30; echo \"=== запускается ли harvest ===\"; ls -la --time-style=long-iso \"C:/Users/dev/.claude/scripts/_cron_heartbeat/\" 2>/dev/null | grep -iE \"alpha|harvest|sostav\" | head", "descrip

---

> `Bash` -- {"command": "ls -la --time-style=long-iso \"D:/Vault/_imports/crm-engine/\"*.db 2>/dev/null | head; find \"D:/Vault/_imports\" -maxdepth 2 -name \"leads.db\" 2>/dev/null | head -3", "description": "Locate leads.db"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && find . -iname \"*Sostav*MOC*\" -o -iname \"*Sostav-Community*\" -maxdepth 4 2>/dev/null | grep -v stversions | head -5; echo \"=== свежесть домашних заметок клуба ===\"; ls -la --time-style=long-iso \"05-Resources/Sostav-Community/\" 2>/dev/null | h

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/alpha/candidates\" && head -20 fbcomments-judged-latest.md; echo \"=== кто потребляет CREDIT/LEAD строки ===\"; grep -rl \"CREDIT:\" \"C:/Users/dev/.claude/scripts\" \"D:/Vault/_imports/alpha\" 2>/dev/null | head -5", "description": "Check fbcomments verdi

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_plans\" && echo \"=== план 29.08 (наш) — статус ===\"; grep -iE \"статус|status|ждал|выполнен|done|\\+\" PLAN-HUB-01-2026-08-29.md 2>/dev/null | head -8; echo \"=== сколько планов всего / за неделю ===\"; ls | wc -l; ls | grep -c \"2

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python selfheal.py repairs --json 2>/dev/null | head -40; echo \"EXIT=$?\"", "description": "Check open repair classes before creating diggers"}

---

> `Bash` -- {"command": "grep -c \"WA=locked\" \"C:/Users/dev/.claude/scripts/_token-spend-watchdog.log\" 2>/dev/null || true; for f in \"C:/Users/dev/.claude/scripts/\"*token*watchdog*.log; do echo \"--- $f\"; grep -oE \"WA=[a-z()-]+\" \"$f\" 2>/dev/null | sort | uniq -c | head; done 2>/dev/null; echo \"==

---

> `Bash` -- {"command": "grep -n \"личинк\\|retro-lost\" \"D:/Vault/Vault-Knowledge/00-System/Shadow-First-Queue.md\" 2>/dev/null | head -10; echo \"=== строки журнала класса за 7 ночей (личинка) ===\"; grep -c \"retro-lost\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" 2>/dev/null; tail -3 

---

**Claude:**

Урожай тени личинки **уже снят 29.08** (Shadow-First-Queue стр. 107, продлён до 30.09) — дубль не делаю. Проверяю, нет ли уже карточек под найденные хвосты.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/10-Tasks\" && grep -ril \"whatsapp\" . 2>/dev/null | head -5; echo \"--- big_video / n8n видео ---\"; grep -ril \"big_video\\|тяжёлые видео\\|big video\" . 2>/dev/null | head -5; echo \"--- открытые классы (имена) ---\"; cd \"C:/Users/dev/.claude/scrip

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros\" && ls -t | head -4; echo \"--- MOC/индекс ретро ---\"; ls | grep -iE \"moc|index|_\" | head -5; echo \"--- шапка соседней заметки ---\"; head -14 \"$(ls -t | grep '^retro-lost' | head -1)\"", "description": "Inspect retro

---

**Claude:**

Пишу ретро-заметку по образцу соседних.

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-lost-2026-09-03-hub-desyat-poteryashek.md\" <<'EOF'\n---\ntitle: \"retro-lost ХАБ-ПОЛНЫЙ 03.09.2026, узел HUB-01: десять потеряшек, семь единиц\"\ntype: retro\nstage: distilled\ncreated: 2026-09-03\nmachine:

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros\" && grep -n \"系统\" retro-lost-2026-09-03-hub-desyat-poteryashek.md; python - <<'PY'\nimport io\np=r\"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-lost-2026-09-03-hub-desyat-poteryashek.md\"\nt=io.

---

**Claude:**

Заметка на месте и целая. Завожу две карточки под найденные хвосты.

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/10-Tasks/task-2026-09-03-big-video-bridge-no-runner.md\" <<'EOF'\n---\ntitle: \"big_video_bridge собран, протестирован и никем не заводится (нет задачи планировщика)\"\ntype: task\nstate: open\npriority: P2\ncreated: 2026-09-03\nmachine: HUB-01

---

**Claude:**

Карточка без решателя — жалоба. Ставлю копателя в очередь подъёма (из рутинной сессии `create_scheduled_task` вызывать нельзя — даст апрув-окно оператору, канон §9.2 от 02.09).

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python spawn_queue.py --help 2>&1 | head -25", "description": "Check spawn_queue usage"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python spawn_queue.py add --help 2>&1 | head -20", "description": "Check spawn_queue add args"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && cat \"$OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md\" 2>/dev/null | head -20 || cat \"D:/Vault/Vault-Knowledge/08-Templates/seed-stop-dup-block.md\" 2>/dev/null | head -20", "description": "Read mandatory seed STOP-DUP block"}

---

> `Bash` -- {"command": "sed -n '20,60p' \"D:/Vault/Vault-Knowledge/08-Templates/seed-stop-dup-block.md\"", "description": "Read the seed block body"}

---

> `Bash` -- {"command": "SCR=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5ba413a2/scratchpad\"; mkdir -p \"$SCR\"; cat > \"$SCR/seed_bvb.md\" <<'EOF'\nТы Claude Code на хабе HUB-01. СЕССИЯ-КОПАТЕЛЬ по карточке, заведённой ночным ретро потеряшек 03.0

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\np=r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_5ba413a2\\scratchpad\\seed_bvb.md\"\nt=io.open(p,encoding=\"utf-8\").read()\nt=t.replace(\"такой же claim, как вырод\",\"такой же claim, как вывод\"

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python spawn_queue.py add --task-id auto-hub-260903-dig-big-video-bridge-runner --description \"Копатель: big_video_bridge собран и протестирован 28.08, но задачи планировщика нет — завести прогон либо честно объявить разовым\" --prompt-file \"C:

---

**Claude:**

Копатель в очереди. Закрываю все 10 сессий маркерами.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && for s in s_f0ecd93c s_5f3c0b9b s_8c344b9a s_786bc3f4; do python retro_lost_scan.py mark-done $s --note \"батч SOSTAV-судья 28.08: 4 прогона в 

---

**Claude:**

Шаг 9 — личинка: свои спотыкания за прогон, по одной строке на семью.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python selfheal.py journal --help 2>&1 | head -20", "description": "Check journal door usage"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python selfheal.py journal --class bash-tool-eats-windows-backslashes --what \"retro-lost 03.09 хаб: в цикле по sessionId путь собран как \\\"...\\\\\\\\projects\\\\\\\\E--Obsidian--imports-alpha\\\\\\\\\\$s.jsonl\\\" — обратный слэш экранировал 

---

**Claude:**

Дедуп двери сработал штатно. Вторая семья — расхождение скилла с каноном и прибором.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python selfheal.py journal --class skill-otstal-ot-kanona-i-pribora --what \"retro-lost 03.09 хаб: у скилла /retro-lost ДВА расхождения, обнаружены при исполнении. (1) Скилл в шапке и в оси возраста утверждает 'потеряшка = сессия без касания >24 

---

**Claude:**

Отчёт в шину.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python retro_lost_scan.py list --top 1 2>&1 | head -2", "description": "Get remaining queue size"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python bus_send.py \"retro-lost ХАБ-ПОЛНЫЙ (HUB-01): закрыто 10 сессий = 7 единиц, очередь 580, контрибьют-кандидатов 0. Батч судьи СОСТАВ (4 прогона 28.08): инцидент с похороненной заявкой \\$5M cash→USDT — исправление УЖЕ въехало в рутин

---

**Claude:**

четверг, ночь, 04:03

Прогон закрыт: **10 сессий = 7 единиц**, очередь 590 → 580.

## Что нашлось

**Батч судьи СОСТАВ (4 прогона 28.08 в одну единицу).** Четыре сессии судили один отчёт и писали в один файл. Прогон 20:30 выбросил как «покрыто в базе» живую заявку **$5 млн кэш → USDT** с названным контрагентом — худшая из возможных ошибок для бизнеса оператора. RECALL-сверка показала главное: **исправление уже въехало в саму рутину тем же вечером**, а не осталось в чате — `sostav_judge.cmd` правлен 28.08 20:37 (бэкап в 20:34), в живом промпте стоит абзац приоритета settlement-dealflow с дословной уликой инцидента, модель поднята `sonnet → opus`. Труба кормит: прогон 01.09 дал 3 alpha, доставка в Saved с msg_id. Урок не дублировал.

**Два настоящих обрыва → карточки:**

1. [task-2026-09-03-big-video-bridge-no-runner.md](D:/Vault/Vault-Knowledge/10-Tasks/task-2026-09-03-big-video-bridge-no-runner.md) — сессия 28.08 пробила стену «20 МБ» (это лимит ботов, не Telegram), построила мост, тест, обёртку, прогнала вживую. Регистрацию задачи планировщика отбил гейт, сессия честно не стала обходить — и шесть суток спустя мост **никто не запускает**, файл висит в списке сирот. Копатель поставлен в `spawn_queue`.
2. [task-2026-09-03-token-watchdog-wa-leg-dead.md](D:/Vault/Vault-Knowledge/10-Tasks/task-2026-09-03-token-watchdog-wa-leg-dead.md) — вторая нога алертов сторожа токенов мертва месяцами: порт 8768 закрыт прямо сейчас, в логе 13 разных формулировок отказа. Не тихий ложный зелёный — кричит каждый прогон, только в пустоту.

Две сессии (`e535e209`, `faebe6fc`) **уже имели своё ретро** внутри себя 28.08 — сверил артефакты и закрыл без дубля.

## Два расхождения самого скилла (записал дверью, строка 1/3)

- Скилл заявляет «потеряшка = >24ч, `MIN_AGE_DAYS=1`, поле `retro_mode`» — живой сканер имеет `MIN_AGE_DAYS=5` и `retro_mode` не отдаёт вовсе.
- Шаг 7-бис велит поднимать копателя через `create_scheduled_task` — канон §9.2 от 02.09 это из рутинной сессии **запрещает** (даёт оператору принудительное апрув-окно). Пошёл через `spawn_queue`.

Урожай тени «личинка» из пункта 4 сида **не повторял**: он снят 29.08 (7 строк за 7 ночей, продлён до 30.09) — RECALL поймал, что работа уже сделана.

🧒 Простыми словами: разобрал десять брошенных ночных работ. Самое важное — робот-судья один раз выкинул в мусор просьбу обменять 5 миллионов долларов, но ту ошибку в тот же вечер зашили в самого робота, я проверил и убедился. Нашёл две недоделки: построили «мостик» для тяжёлых видео и забыли включить, и у сторожа расходов отвалился второй громкоговоритель. На обе завёл записки, на первую — отдельного помощника.
