---
session: s_5cba2997
date: 2026-09-15
words: 12445
turns: 33
tools: "Bash, SendUserFile, Skill, ToolSearch, Write, mcp__97420a88-50ae-4ab1-99f6-f5ec547aebd8__search_threads, mcp__be573d85-3efd-4883-8eee-7095a4943f74__create_event, mcp__be573d85-3efd-4883-8eee-7095a4943f74__list_calendars, mcp__be573d85-3efd-4883-8eee-7095a4943f74__list_events, mcp__ccd_session_mgmt__list_sessions, mcp__ccd_session_mgmt__set_session_title, mcp__claude-in-chrome__list_connected_browsers"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-15 · Должен быть рутина. Потому что он рутина, которая проверяет э, все наши подачи на вакансии…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5cba2997` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Должен быть рутина. Потому что он рутина, которая проверяет э, все наши подачи на вакансии и если люди ответили, я приглашаю от них на спросы беседоваться. А если предлагают собеседоваться, давай э, букать. Давай букать, дай мне список сейчас. Всех тех, вакансий, на которые ты уже ответил. Либо дай мне список тех вакансий, где приглашается на собеседование.

---

**Claude:**

[⏰ вторник, утро, 07:41, 15 сентября 2026]

Иду смотреть реальный леджер подач, а не по памяти.

---

> `Bash` -- {"command": "ls ~/.claude/skills/apply/ 2>/dev/null; echo \"---\"; find /e/Obsidian/Vault-Knowledge /c/Users/dev/.claude -maxdepth 4 -iname \"*apply*\" 2>/dev/null | head -50", "description": "Find apply skill and ledger files"}

---

> `Bash` -- {"command": "ls -R ~/.claude/skills/apply/tools/ 2>/dev/null | head -40; echo \"=== SKILL head ===\"; sed -n '1,80p' ~/.claude/skills/apply/SKILL.md", "description": "Inspect apply skill tools and head"}

---

> `Bash` -- {"command": "cd ~/.claude/skills/apply/tools && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint([r[0] for r in c.execute(\\\"select name from sqlite_master where type='table'\\\")])\nfor t in [r[0] for r in c.execute(\\\"select name from sqlite_master where type='table'\\\")]:\n   

---

> `Bash` -- {"command": "find /e/Obsidian/_imports -maxdepth 3 -name \"jobs.db\" -o -maxdepth 3 -name \"*outcome*\" 2>/dev/null | head; echo \"--- jobs-watch ls ---\"; ls /e/Obsidian/_imports/jobs-watch/ 2>/dev/null | head -60", "description": "Locate real jobs.db and outcome detector"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3\nc=sqlite3.connect('file:jobs.db?mode=ro',uri=True)\nfor r in c.execute(\\\"select name from sqlite_master where type='table'\\\"):\n    n=r[0]; print('==',n, c.execute(f'select count(*) from \\\"{n}\\\"').fetchone()[0])

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('file:jobs.db?mode=ro',uri=True)\nprint('--- status counts ats_jobs ---')\nfor r in c.execute('select status,count(*) from ats_jobs group by 1 order by 2 desc'): print(r)\nprint('--- answer counts (non-empty) ---')\nfor r in c.execute(\\\"

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('file:jobs.db?mode=ro',uri=True)\nprint('=== INTERVIEW ===')\nfor r in c.execute(\\\"select company,title,location,applied,answer,url from ats_jobs where status='interview' order by applied\\\"): print(r)\nprint()\nprint('=== REJECTED (las

---

> `Bash` -- {"command": "sed -n '1,45p' /e/Obsidian/_imports/jobs-watch/pipe_a_inbox_watch.py; echo \"=== reports ===\"; ls -lt /e/Obsidian/_imports/jobs-watch/reports/ | head -20", "description": "Read inbox watch routine and recent reports"}

---

> `Bash` -- {"command": "sed -n '1,60p' /e/Obsidian/_imports/jobs-watch/reports/inbox-watch-2026-09-14.md", "description": "Read latest inbox watch report"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/skills/apply/tools/ | grep -i outcome; echo \"--- grep interview in verify/reconcile ---\"; grep -rn \"interview\" /e/Obsidian/_imports/jobs-watch/apply_verify.py /e/Obsidian/_imports/jobs-watch/apply_reconcile.py /c/Users/dev/.claude/skills/apply/tools/*.py 

---

> `Bash` -- {"command": "head -30 /c/Users/dev/.claude/skills/apply/tools/_test_outcome_detector.py", "description": "Check orphan test for outcome detector"}

---

**Claude:**

Леджер прочитал. Теперь проверяю почту напрямую — детектора приглашений в рутине нет, значит база могла их пропустить.

---

> `ToolSearch` -- {"query": "select:mcp__s_8e110270__search_threads,mcp__s_8e110270__get_thread", "max_results": 2}

---

> `mcp__s_8e110270__search_threads` -- {"query": "newer_than:30d (subject:(interview OR \"schedule\" OR \"next steps\" OR \"chat\" OR \"call\") OR \"schedule a time\" OR \"would love to chat\" OR \"set up a call\" OR \"interview\") -subject:(unfortunately OR \"not moving forward\")", "pageSize": 50}

---

**Claude:**

Gmail-коннектор смотрит в a2@, а подачи шли с a@. Иду рельсой прибора, которая в a@ умеет.

---

> `Bash` -- {"command": "grep -n \"def \\|IMAP\\|imap\\|MAILBOX\\|account\\|a@\" apply_verify.py | head -40", "description": "Inspect apply_verify mail rail"}

---

> `Bash` -- {"command": "sed -n '505,560p' apply_verify.py; echo \"=== gmail_check ===\"; find /e/Obsidian/_imports /c/Users/dev/.claude -name \"gmail_check.py\" 2>/dev/null | head", "description": "See classifier and gmail rail"}

---

> `Bash` -- {"command": "grep -n \"GMAIL_HOME\" apply_verify.py | head -3; find /e/Obsidian /c/Users/dev -maxdepth 5 -name \"gmail_check.py\" 2>/dev/null | head", "description": "Find gmail_check path"}

---

**Claude:**

Есть живая рельса в a@. Ищу приглашения на собеседование прямо в ящике подач.

---

> `Bash` -- {"command": "cd \"/c/Users/dev/!CLAUDE-NODE-0X May26/gmail\" && python gmail_check.py search 'newer_than:45d (subject:(\"interview\" OR \"next steps\" OR \"schedule\" OR \"chat with\" OR \"moving forward\" OR \"availability\" OR \"meet\") OR \"schedule a call\" OR \"set up a time\" OR \"like to speak

---

> `Bash` -- {"command": "cd \"/c/Users/dev/!CLAUDE-NODE-0X May26/gmail\" && python gmail_check.py search 'newer_than:45d (from:kong OR \"Kong\" OR from:konghq.com)' --label a --max 50 2>&1 | head -20; echo \"=== calendar-ish invites ===\"; python gmail_check.py search 'newer_than:45d (subject:Invitation OR subje

---

> `Bash` -- {"command": "cd \"/c/Users/dev/!CLAUDE-NODE-0X May26/gmail\" && for id in 1a0a06b2cfc0334b 1a0a06a63a9a2493 1a096d759297b25e 1a08a8f003590ff8; do echo \"########## $id\"; python gmail_check.py read $id --label a 2>&1 | head -45; done", "description": "Read invitation bodies"}

---

> `Bash` -- {"command": "cd \"/c/Users/dev/!CLAUDE-NODE-0X May26/gmail\" && python gmail_check.py read --help 2>&1 | head -20", "description": "Check read subcommand args"}

---

> `Bash` -- {"command": "cd \"/c/Users/dev/!CLAUDE-NODE-0X May26/gmail\" && for id in 1a0a06b2cfc0334b 1a0a06a63a9a2493 1a096d759297b25e 1a08a8f003590ff8; do echo \"########## $id\"; python gmail_check.py read a $id 2>&1 | head -40; done", "description": "Read invitation bodies correctly"}

---

**Claude:**

Нашёл главное — и оно срочное. Проверяю расписание рутины.

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__list_scheduled_tasks", "max_results": 1}

---

> `mcp__scheduled-tasks__list_scheduled_tasks` -- {}

---

> `ToolSearch` -- {"query": "select:mcp__s_2292b084__list_events", "max_results": 1}

---

> `mcp__s_2292b084__list_events` -- {"startTime": "2026-09-15T00:00:00Z", "endTime": "2026-09-17T00:00:00Z", "orderBy": "startTime", "timeZone": "Europe/Lisbon"}

---

> `ToolSearch` -- {"query": "select:mcp__s_2292b084__list_calendars", "max_results": 1}

---

> `mcp__s_2292b084__list_calendars` -- {}

---

**Claude:**

Интервью нашёл — но они лежат в календаре a@, а твой рабочий календарь bb@ о них не знает. Дублирую, чтобы не пропустить.

---

> `ToolSearch` -- {"query": "select:mcp__s_2292b084__create_event", "max_results": 1}

---

[СКРЫТО]

---

[СКРЫТО]

---

**Claude:**

Теперь собираю полный список подач в файл.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3,collections\nc=sqlite3.connect('file:jobs.db?mode=ro',uri=True)\nrows=list(c.execute(\\\"select company,title,location,substr(applied,1,10),url,ats from ats_jobs where status='applied' order by applied desc, company\\\")

---

> `SendUserFile` -- {"__unparsedToolInput": {"raw": "{\"files\": C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_5cba2997\\scratchpad\\applied-list.md, \"caption\": \"Все 465 поданных заявок, сгруппированы по дате подачи (204 компании).\", \"status\": \"normal\"

---

> `SendUserFile` -- {"files": ["C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5cba2997/scratchpad/applied-list.md"], "caption": "Все 465 поданных заявок, сгруппированы по дате подачи (204 компании).", "status": "normal", "display": "attach"}

---

**Claude:**

[СКРЫТО]

---

**User:**

recall + чини корни!!

---

**Claude:**

[⏰ вторник, утро, 08:12]

---

> `Bash` -- {"command": "grep -ril \"apply_verify\\|pipe-a-inbox\\|интервью\\|interview\\|подач\" /c/Users/dev/.claude/projects/*/memory/*.md 2>/dev/null | head -20", "description": "Recall memory on apply pipeline"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && cat apply-proof-of-delivery.md; echo \"==========\"; grep -l \"интервью\\|interview\\|собеседован\\|календар\" *.md 2>/dev/null | head -20", "description": "Read apply memory and find interview-related notes"}

---

> `Bash` -- {"command": "for f in calendar-agenda-stopped.md two-step-calendly-after-reply.md dev-calendly-two-accounts.md; do echo \"##### $f\"; sed -n '8,40p' $f; done", "description": "Read calendar-related memories"}

---

> `Bash` -- {"command": "cat \"/c/Users/dev/.claude/scheduled-tasks/pipe-a-inbox-watch/SKILL.md\"", "description": "Read inbox watch routine instruction"}

---

> `Bash` -- {"command": "f=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5cba2997/tool-results/bkjttt3i1.txt\"; grep -n -i \"календар\\|calendar\\|interviews\\|approval.py ask\" \"$f\" | head -30", "description": "Grep routine for calendar handling"}

---

> `Bash` -- {"command": "f=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5cba2997/tool-results/bkjttt3i1.txt\"; sed -n '26,45p' \"$f\"", "description": "Read interviews step in detail"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"приглашение на интервью не доехало до календаря оператора, потребитель не увидел\" 2>&1 | head -25", "description": "Count class family for this defect"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -rn \"inbox-watch\\|inbox_watch\" _shared/output_freshness.py green_gap_exempt.json cron_watchdog.py 2>/dev/null | head -10; echo \"=== ARTIFACTS decl ===\"; grep -rn \"ARTIFACTS\" \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/a3e99f03-5a6d-

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls | grep -i \"freshness\\|green_gap\\|cron_watch\" ; echo \"=== where ===\"; find ~/.claude -maxdepth 3 -name \"output_freshness.py\" -o -maxdepth 3 -name \"green_gap*\" 2>/dev/null | head", "description": "Locate freshness watchdog"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"pipe.a.inbox\\|pipe_a_inbox\" _shared/output_freshness.py output_freshness.py cron_watchdog.py 2>/dev/null | head; echo \"--- watchdog registry keys sample ---\"; grep -n \"REGISTRY_MCP\" -A4 cron_watchdog.py | head -20; echo \"--- green_gap on this rou

---

**Claude:**

Появился скилл `/job-inbox`, которого час назад не было — проверяю, не чинит ли то же параллельная сессия.

---

> `Bash` -- {"command": "ls -la ~/.claude/skills/job-inbox/ 2>/dev/null; echo \"=== ON AIR ===\"; cat /e/Obsidian/Vault-Knowledge/_onair/ACTIVE_NOW.md 2>/dev/null | head -30; echo \"=== mtime SKILL рутины ===\"; ls -la \"/c/Users/dev/.claude/scheduled-tasks/pipe-a-inbox-watch/SKILL.md\"", "description": "Chec

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__list_sessions", "max_results": 1}

---

> `mcp__ccd_session_mgmt__list_sessions` -- {"limit": 12}

---

> `Bash` -- {"command": "cat ~/.claude/skills/job-inbox/SKILL.md", "description": "Read the new job-inbox skill"}

---

> `Bash` -- {"command": "find /c/Users/dev -maxdepth 4 \\( -iname \"*calendar*.py\" -o -iname \"*gcal*\" \\) 2>/dev/null | grep -v node_modules | head -10; echo \"=== token scopes a ===\"; python -c \"\nimport json;d=json.load(open(r'C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\gmail\\tokens\\token_a.json'));print(d

---

> `Bash` -- {"command": "ls -la ~/.claude/state/pipe_a_inbox_pregate.json 2>/dev/null; echo \"=== ledger/логи прогонов ===\"; grep -rl \"pipe-a-inbox-watch\" ~/.claude/scripts/_logs/ 2>/dev/null | head -5; echo \"=== TG-03 доклады? ищем в леджере рутин ===\"; ls ~/.claude/scripts/_logs/ 2>/dev/null | grep -i \"

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python routine_cost_audit.py --days 9 2>&1 | grep -i \"inbox\\|прогон\" | head -10", "description": "Check actual run count for the routine"}

---

**Claude:**

Второй заход поправил мой же вывод: рутина бежала **8 раз за 9 дней** — пропусков почти нет, отчёт просто не пишется в «чистые» дни. Снимаю этот «корень», он был мой артефакт чтения. Остальные два — живые.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone jobs-pipe-a --mode collab --note \"корни: интервью не доезжает в календарь bb@, статусы scheduled\" 2>&1 | head -5 || python onair.py zones 2>&1 | head -20", "description": "Declare coordination zone"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py zones 2>&1 | head -25", "description": "List valid onair zones"}

---

[СКРЫТО]

---

**Claude:**

Зона объявлена. Корень 2 — статусы, из-за которых рутина через час разбудит тебя ложной тревогой:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cp jobs.db jobs.db.bak-scheduled-20260915 && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nrows=[('https://jobs.ashbyhq.com/lambda/s_b1c08bc6','2026-09-15 16:30 Lisbon (8:30 PDT) · [ИМЯ] [ИМЯ], recruiter scre

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"interview\\|scheduled\" pipe_a_inbox_pregate.py | head -15", "description": "Verify pregate reads interview status"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python pipe_a_inbox_pregate.py 2>&1 | tail -20; echo \"EXIT=$?\"", "description": "Run pregate to verify interview list shrank"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python -c \"\nimport pipe_a_inbox_pregate as p\nold=p.open_interviews(r'D:\\Vault\\_imports\\jobs-watch\\jobs.db.bak-scheduled-20260915')\nnew=p.open_interviews()\nprint('ДО правки (бэкап):', len(old[0]), [x.get('company') for x in old[0]])\nprint('ПОСЛЕ правк

---

**Claude:**

Корень 1 — главный. Вписываю в канон скилла:

---

> `Bash` -- {"command": "cd ~/.claude/skills/job-inbox && cp SKILL.md SKILL.md.bak-calendar-20260915 && python - <<'PY'\nimport io\np='SKILL.md'\ns=io.open(p,encoding='utf-8').read()\nanchor=\"5. Запустить `/interview-prep` для этой компании.\"\nadd = \"\"\"4-бис. ⭐ **СОБЫТИЕ В КАЛЕНДАРЬ, КОТОРЫЙ оператор ОТКРЫВАЕ

---

**Claude:**

Правило без прибора не работает. Строю сторож — сначала тест, который должен покраснеть:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cat > interview_calendar_guard.py <<'PY'\n#!/usr/bin/env python3\nr\"\"\"interview_calendar_guard.py -- сторож: забуканное собеседование обязано жить в календаре bb@.\n\nЗачем\n-----\nКорень 15.09.2026 (3-й датированный случай класса «последний шаг 

---

**Claude:**

Сторож покраснел на живых данных. Вписываю id событий, которые создал утром:

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor u,eid in [('https://jobs.ashbyhq.com/lambda/s_b1c08bc6','t0p1orcjdqpegslnlnh29cplno'),\n              ('https://jobs.ashbyhq.com/nango/s_7c4bab47','slhsss7jrm5pr7u2tat7b4f

---

**Claude:**

Красный → зелёный на живых данных. Теперь тест, который останется после меня:

---

> `Bash` -- {"command": "cat > _test_interview_calendar_guard.py <<'PY'\n\"\"\"Сетка сторожа «забуканное собеседование обязано жить в календаре bb@».\n\nКласс, который она держит: работа доведена до последнего метра и отдана оператору -- а он\nеё не видит, потому что артефакт лежит в доме, куда он не ходит (календ

---

**Claude:**

Тест обязан краснеть на сломанном коде — проверяю мутацией:

---

> `Bash` -- {"command": "cp interview_calendar_guard.py /tmp/g.bak && python - <<'PY'\nimport io\np='interview_calendar_guard.py'\ns=io.open(p,encoding='utf-8').read()\ns=s.replace('    m = CAL_RE.search(answer or \"\")\\n    return m.group(1) if m else None',\n            '    return \"always-ok\"  # MUTANT')\

---

> `Bash` -- {"command": "cp interview_calendar_guard.py /tmp/g.bak && sed -i 's/^    m = CAL_RE.search(answer or \"\")$/    return \"always-ok\"  # MUTANT/' interview_calendar_guard.py && python _test_interview_calendar_guard.py; echo \"MUTANT_EXIT=$?\"; cp /tmp/g.bak interview_calendar_guard.py; echo \"--- вос

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_5cba2997\\scratchpad\\patch_door.py", "content": "\"\"\"Патч двери: сторож interview_calendar_guard вызывается рутиной + маркер cal:<id> в каноне.\"\"\"\nimport io\nimport shutil\

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5cba2997/scratchpad/patch_door.py\"", "description": "Apply door patch to skill and routine"}

---

**Claude:**

Второй заход — проверяю с диска и у потребителя, не по памяти:

---

> `Bash` -- {"command": "grep -n \"5-бис\\|interview_calendar_guard\" \"/c/Users/dev/.claude/scheduled-tasks/pipe-a-inbox-watch/SKILL.md\" | head -5; echo \"=== прогон по пути ИЗ рутины ===\"; python \"D:\\Vault\\_imports\\jobs-watch\\interview_calendar_guard.py\"; echo \"EXIT=$?\"; echo \"=== журнал класс

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2026-09-15T12:00:00Z", "endTime": "2026-09-16T00:00:00Z", "orderBy": "startTime", "fullText": "ИНТЕРВЬЮ"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\booked-interview-must-reach-dev-calendar.md", "content": "---\nname: booked-interview-must-reach-dev-calendar\ndescription: \"Забуканное собеседование обязано жить в календаре bb@, а не только в почте a@ и 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && python - <<'PY'\nimport io\np='MEMORY.md'\ns=io.open(p,encoding='utf-8').read()\nline=\"- [Забуканное интервью → календарь bb@](booked-interview-must-reach-dev-calendar.md) — ⭐15.09 приглашение падает в a@, Анто

---

[СКРЫТО]

---

[СКРЫТО]

---

[СКРЫТО]

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

[СКРЫТО]

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close --zone scheduled-tasks/pipe-a-inbox-watch 2>&1 | tail -2; cd /e/Obsidian/_imports/jobs-watch && python _test_apply_verify.py 2>&1 | tail -3", "description": "Close zone and check neighbour tests still green"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2026-09-15T071701Z-HUB-01-a3e99f03-scheduled-tasks-pipe-a-inbox-watch 2>&1 | tail -2", "description": "Close onair declaration"}

---

**Claude:**

[СКРЫТО]

---

**User:**

ретро

---

**Claude:**

[⏰ вторник, день, 13:26]

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

**⏳ Measure the time-gap FIRST.** Check when this session's work actually happened (turnstate ledger / the digest's day-span) vs **now**. Old session → widen every lookup below to cover *"what changed SINCE"* — don't recall only the session's own window.

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
3. **Neighboring chats (lexical, 0 tok):** `/search <topic words>` (search_catalog.db, ~99k Telegram/FB/ChatGPT/Claude) — what did dev or another session **dictate elsewhere** about this topic?
4. **Vault meaning (RAG):** `/ask <topic>` (`$IMPORTS_ROOT/brain_ask.py`) — what does the Second Brain already hold / already decide on this?
5. **Memory + vault grep** for every rule/concept/decision this session touched — already captured? **superseded / changed** since?
6. **Peers & cross-machine:** `/inbox` + `_machine-bus` + consensus commits — "всё, о чём мы договорились" on the OTHER machines; did a peer already decide, or undo, this?
7. **Declined journal:** skill `/declined` — did we already reject something this session quietly re-did?

**Attribution guard:** the Step-1 inventory is machine-wide and WILL include other sessions' artifacts (skills/scripts/commits from the fleet). Treat anything NOT created in THIS conversation as **someone else's** — flag it, never claim or re-route it.

**Output of Step 0 — one tight «🔎 сверка» block up front** (checked + verdict):
- **checked:** what I actually looked at (N retros / chats / vault / peers).
- **✅ aligned** — this session's calls match the collaboration; or
- **⚠️ drift** — session did X but [[note/decision]] elsewhere says Y (superseded / contradicts / already undone) → flag for dev; or
- **🔗 to propagate** — session's durable work not yet in vault / peers / Bible → route it in Step 4.
If a parallel session already captured the durable item, **SKIP re-capturing** — just cross-link.

## Step 1 — Inventory (deterministic first; AK-47, ~free)
Ground the recap in facts, not memory alone — run the SHARED inventory script (same one the daily sweep uses, so the logic never drifts):
- `python "$IMPORTS_ROOT/retro_inventory.py" 1`  (arg = days; widen for a multi-day session)
- It prints `BUILT_ARTIFACTS <n>` and writes `$IMPORTS_ROOT/retro_candidates/digest-latest.md` — Read that digest: new/changed **skills**, **_imports scripts/sidecars**, **durable notes** (Protocols + Concepts), and recent **descriptive vault commits**.
- (⚠️ a concurrent Claude-Desktop fleet may interleave vault commits — its are descriptive; the terse `pre-intervention` ones are auto-backups.)
- **Cross-check** with what you (the agent) created/edited in THIS conversation: skills, scripts, vault notes, memory entries, `CLAUDE.md` edits, decisions made, rules captured, things flagged for dev.

## Step 1🧠 — ПАМЯТЬ СЕССИИ: сироты по worktree + машинно-невидимые опровержения (дверь §8.6; добавлена 2026-09-02)
Сессия из worktree пишет память в СВОЮ проектную папку, домашний индекс о ней не знает — замер 02.09 на NODE-0X: 20 таких заметок, одна несла вердикт, опровергнутый через девять дней в соседней папке. Два прогона, 0 LLM, 0 сети:
- `python ~/.claude/scripts/memory_harvest.py --scan` → есть ORPHAN → `python ~/.claude/scripts/memory_harvest.py --harvest` (копия домой + указатель в `MEMORY-archive.md`; оригинал НЕ трогается). Exit 3 = `NEEDS-HUMAN` (тёзки припаркованы, ничего не потеряно) → строкой оператору, не молча.
- ⚠️ **Прибор даёт ложное «чисто» (замер 10.09.2026, NODE-0X):** `--scan` напечатал «0 missing pointer(s) to repair», а указатель на свежую заметку (`zenodo-publish-rail`, дописан 07.09) из `MEMORY.md` за ночь исчез — сироту он не увидел, потому что сверяет не ту пару папок. Поэтому ПОМИМО прогона сверь руками указатели на заметки, которые ЭТА сессия и пара прошлых записали: `grep -c "<слаг>" <проектная-папка>/memory/MEMORY.md` → 0 = дописать строку тем же заходом. Класс = `memory-index-line-lost-overnight`, 4 датированных случая, корень чинится отдельной сессией.
- `python ~/.claude/scripts/memory_inject_lint.py --scan` → анти-инъекция и секрет-паттерны memory-стора (порт bb plugins/memory, 05.09.2026): exit 1 = НОВАЯ находка против baseline — разобрать тем же заходом (чужая закладка? секрет в памяти → в secrets-стор); старый долг молчит ратчетом. Это ЕДИНСТВЕННАЯ дверь линта ([[rule-needs-a-door-quota]]).
- `python ~/.claude/scripts/memory_epistemic.py --lint` → `SELF-TOMBSTONE` (заметка сама пишет, что устарела, а машина этого не видит) закрыть тем же заходом: `--close <слаг> --superseded-by <слаг-преемника>`. Отмена закрывается ПОЛЯМИ (`status`/`valid_to`/`superseded_by`/`refuted_on`/`refuted_by`) во ВСЕХ копиях слага, а не переписыванием одной: CLAUDE.md §8.4-бис + [[memory-records-close-by-fields-not-rewrite]].
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже) и на каждую — ОДНА строка ЧЕРЕЗ ДВЕРЬ `python ~/.claude/scripts/selfheal.py journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Затем СЧЁТЧИК по классу — **не грепом по имени, а прибором** (замер 03.09.2026: в журнале 503 пронумерованных случая, из них **299 записаны как «1-й датированный»**, уникальных слагов всего 72; счёт вёлся по ИМЕНИ, имя сочинялось заново под каждую поломку, и порог «третьей поломки» был структурно недостижим — семья «вывод по одной поверхности» набрала 72 случая с 27.07 и ни разу не дошла до 3):
```
python ~/.claude/scripts/prior_art.py class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный → отдельная сессия починки** (5 почему по серии → ТРИЗ → АК-47). Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым». Канон: память `class-counted-by-name-never-reaches-three` + CLAUDE.md §5.10.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · fail-closed гейты.
- ⚠️ **Дедуп двери отбивает УТОЧНЕНИЕ к своему же классу** (замер 10.09.2026, NODE-0X, дважды за один
  заход): `selfheal.py journal` отвечает «СТРОКА НЕ ЗАПИСАНА (дедуп: этот класс уже журналился
  недавно). Поправку к своей строке правь в журнале явно» — а прямая правка `Breakage-Journal.md`
  ЗАПРЕЩЕНА хуком `breakage_write_guard` (см. абзац выше). Инструкция сама себе противоречит.
  Пока корень не починен, обход: уточнение 2-го случая (условия, свежие цифры, порог третьего)
  кладётся в **задачу реестра** класса и в **ретро-заметку**, а в отчёте пишется честно
  «дедуп отбил, уточнение легло в <адрес>». ⛔ Молча проглотить отбой нельзя — иначе
  уточнение условий теряется, и следующая сессия снова считает случай первым.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- Канон: Библия `reglament-mekhanizm-tolko-posle-tretey-polomki` + CLAUDE.md §5.10 + `reglament-pyat-pochemu-koren-po-serii-sessiy` §«Три инструмента»; проверка двери — `python ~/.claude/scripts/rule_home_guard.py mekhanizm-tolko-posle-tretey-polomki`.

## Step 2 — Summarize the arc ("сегодня мы поняли")
3–7 beats: starting idea → what got built → key realizations → what was decided. Honest, concise, his voice. This is the "Stan at the end of South Park" recap.

## Step 2🎙 — Вердикт кофаундера (Майк) — canon 2026-07-07, applied 2026-07-31
Right after the arc, Майк speaks as co-founder — 4 строки, без воды (canon `reglament-*` voice-through-line; восстановлен из потерянного сообщения шины, 23 дня в призраке; НЕ театр — работает ПОВЕРХ механики 28.07: если сессия дала стратегический выбор, мемо/адвокат-дьявола из [[cofounder-decision-artifact-gate]] главнее и уже сделаны):
- 💰 **деньги-линза** — что из сегодняшнего приближает выручку/оффер (цель №1/№2), одной строкой;
- 🔪 **что убил бы** — самая слабая трата времени сессии, которую завтра не повторяем;
- 🤺 **спарринг-аудит** — где я сегодня поддакнул вместо спора (провал роли §1.2) либо «спорил честно»;
- ❓ **вопрос** — один направляющий вопрос оператору на завтра.
Пустышку не писать: сессия чисто механическая без бизнес-среза → строка «🎙 Майк: бизнес-среза нет, чисто инфра» и дальше.

## Step 3 — Classify each artifact (Keep / Drop / Try) + tested? audit
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]).
⭐⭐ **И ВТОРАЯ КОЛОНКА — перепроверено? ✅/❌** (dev 13.09.2026, CLAUDE.md §4.3-бис): «протестировано» и «перепроверено вторым, ДРУГИМ заходом» — разные вещи, и ложное «готово» живёт именно в зазоре между ними. Артефакт, у которого первый прогон зелёный, а второго захода не было, ретро помечает ⚠️, а НЕ ✅, и предлагает прогнать Шаг 4.9 скилла `/tt` сейчас. Замер архива 15.08→14.09: 21 раз за месяц оператор спрашивал «ты точно починил?» сразу после моего «готово». Канон: [[done-is-a-claim-recheck-twice]]. Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3📋 — Journal sync (реестр задач; dev's decree 2026-07-04)
Retro is the SAFETY NET of the task journal ([[task-journal-done-undone-linking]]): the in-session reflex («сформулировал → сразу в реестр») catches tasks at birth; retro catches what slipped. Two moves, both against the ONE journal ([[task-backlog-registry]] — **v2 markdown-first, SHIPPED 2026-07-07**):
- **Источник истины = markdown-заметки** `$OBSIDIAN_VAULT/10-Tasks/task-*.md` (шаблон `_Task-Template.md`, MOC `_Tasks-MOC.md`). Синкаются флоту, поэтому работают с ЛЮБОЙ машины без шины и без движка. Завести задачу = новый файл `task-ГГГГ-ММ-ДД-слаг.md`; закрыть = правка frontmatter (`state`/`status` + evidence). Схема строгая: неизвестный `state`/`prio` → `schema_errors` в аудите, а не тихий дефолт.
- **Витрину и аудит строит индексатор** `tasks_index.py` (markdown → `_Dashboards/Task-Backlog.html` + `10-Tasks/_audit/audit-latest.json`). Он крутится ночью на Маяке как ЕДИНСТВЕННЫЙ писатель — руками на хабе/ноуте его НЕ запускать (два писателя одного синкаемого дерива = sync-conflict).
- ⛔ Старый SQLite-движок task-registry (жил на ноуте NODE-0X) = **аварийный fallback, снят с вооружения**; на хабе его нет и не должно быть. Не зови его и не «восстанавливай» — v2 его заменил. (Имя намеренно без code-формата: backtick = «это надо запускать».)

Две операции ретро:
- **Сессия рождена из сида Task-Now?** (первое сообщение начинается «Продолжи задачу task-…» или «Реши СУДЬБУ задачи task-…») → обнови frontmatter ЭТОЙ задачи прямо сейчас: state/touched_at, при done — evidence+outcome; сид без обновлённого frontmatter = петля Task-Now разорвана (v4, dev 2026-08-20).
- **Closed this session** → mark `done` **with evidence** (the /tt proof, commit, counter) + link what it unblocked. Claimed-done without proof → flag, don't close.
- **Still open** (every «📌 Open item», seed prompt, deferred tail, «потом») → ensure it EXISTS in the registry with a link to where it was born + prio/type. Nothing from the open-items list may live only in the chat transcript.
- ⏱ **РАЗРЕЗ ОЖИДАНИЯ (добавлено 07.09 после того, как этот шаг сам породил долг):** у каждого открытого пункта вида «ждём замера / ещё копим / не проверено» спроси — **какая его часть НЕ требует времени?** Почти всегда внутри склеены два вопроса: УСТРОЙСТВО («работает ли конструкция») проверяется детерминированным прибором за минуты, СПРОС («пользуемся ли мы этим») действительно требует недель. Часть про устройство закрывается **в этом же заходе**, а не переносится в реестр. Замер, из-за которого пункт появился: ретро 06.09 записало «гипотеза ДР не проверена, урожай 08.09» — на деле 5 ног гипотезы закрылись прибором за пару минут 07.09, а ждать надо было только спроса. Обязательные подпорки при таком закрытии: **красный контроль** (зелёная нога пустая, пока не показано, что прибор видит поломку) и **независимая линза чужим кодом**, если вывод тебе выгоден. Канон: память [[architecture-proves-in-minutes-demand-needs-weeks]], CLAUDE.md §5.4.
Announce the delta in one line: «📋 журнал: +N новых · ✅M закрыто · без изменений K». Don't duplicate neighbor registries (DR-реестр, improvements-backlog, declined) — link, не копируй.

## Step 3🗺 — Roadmap checkpoint (dev's decree 2026-07-16: «в каждом ретро — как мы продвинулись по roadmap»)
Канон = `$OBSIDIAN_VAULT/04-Projects/ROADMAP.md` (живой публичный роадмап для фолловеров). Три движения, все против ЭТОГО файла:
- **Продвинулись** → отметить чекбоксы/статусы, веху уровня «фолловеру интересно» → строка в Ship log с датой.
- **Появилось новое направление в сессии** → добавить в NOW/NEXT/LATER (не дублируя детальные планы — ссылкой).
- **Ничего не двинулось** → честно сказать это в отчёте (тоже сигнал).
Announce одной строкой: «🗺 roadmap: ✅N продвинуто · ➕M добавлено · ⏸ без движения». Публичная проекция файла наружу — только через контент-гейт (Нора), ретро наружу не постит.

## Step 3🔗 — Connect check (построено → передано → ИСПОЛЬЗУЕТСЯ?) — dev 2026-07-04
Правило Connect ([[connect-rule-pipeline-ownership]]) на подведении итогов: для КАЖДОГО артефакта этой сессии довести цепочку до конца — **«собрали» это ещё НЕ финиш**. Финиш = построено → передано потребителю → **реально используется**. Три исхода на артефакт:
- ✅ **используется** — есть потребитель и он потребляет (скилл вызывают, рутина читает выход, поле CRM читают, дашборд открывают, данные доехали и применены). **Назвать потребителя** — иначе это не ✅.
- 🔗 **передано, потребления пока нет** — доехало, но никто ещё не читает/не применяет → на доску висячих, назначить потребителя/срок.
- ⚠️ **построено «в воздух»** — собрали и бросили, потребителя нет вовсе (dead-letter без consumer — как релинк-очередь: 29k сирот, 0 применено) → **ПОДСВЕТИТЬ оператору явно**: «построили X, но это никем не используется» → решить: подключить потребителя ИЛИ признать выброшенным.

Молчание ≠ используется. «Построили» без названного потребителя = недоделанный Connect, НЕ «done». Строкой: «🔗 Connect: ✅N используется · 🔗M передано-ждёт · ⚠️K в воздух».
⭐ **🌍 МИРОВОЙ ПОТРЕБИТЕЛЬ (dev 24.08, голосом):** у каждой закрытой за сессию починки КЛАССА — четвёртый исход Connect: раздали ли миру? Сеть-ловушка: строки Breakage-Journal этой сессии «класс закрыт» без вердикта 🌍 = долг → прогнать скилл **`/share-fix`** (порог переносимости, реверс-поиск по симптому, 3-5 лучших живых тредов, gist, вахта — вся механика там). Вердикт в отчёте обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
⚠️ **Грабля 10.09 (NODE-0X):** `fleet_fix_audit.py` стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — второй заход за день отбивается. Уже гоняли сегодня → бери вывод ночной карты / `deploy_check.py`, `--force` только с названной оператору причиной. Отбитый гейтом аудит НЕ повод молчать: проверь `PENDING-<узел>` и скажи честно, что доказана РЕГИСТРАЦИЯ, а не применение.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🔄 — Outcome-аудит ПРОШЛЫХ правил (взято у netresearch/retro-skill «outcome mode», adopted 2026-08-26; наш обмен — issue #78 их репо)
Door-audit (Step 3🔗) судит правило при РОЖДЕНИИ; этот шаг судит СУДЬБУ уже записанных — родился с дверью ≠ живёт (замеры: 19/25 без двери, «5 почему» 42 дня без применения, Firefox-first умер тихо за 13 дней). Дёшево, ЧИТАЕМ ночные выходы, сканы руками НЕ гоняем (§10.0):
1. Возьми правила, ТЕМАТИЧЕСКИ близкие этой сессии + до 5 самых старых нетронутых из ночной карты `rule_liveness` (HTML/JSON выход ночного прогона; руками `--scan` не запускать).
2. По каждому три вопроса: применялось ли с прошлого ретро (счётчик §5.8 / упоминание в транскриптах)? нарушалось ли (Breakage-Journal)? актуально ли ещё (не superseded)?
3. Вердикт-строка в отчёт: «🔄 outcome: N проверено · M живут · K мертвы» — каждому мёртвому РЕШЕНИЕ в том же заходе: утиль (в архив с причиной) / дверь построить / отдать сессии-починке. Молча пропустить шаг нельзя; сессия без тематических правил → «🔄 outcome: чужих правил не трогал» одной строкой.

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` — ТОЛЬКО из двери `python ~/.claude/scripts/_shared/fireat_now.py --in 15`, руками время не писать: класс из 6 случаев 11.08-09.09, часы шелла врали до 11 ч; разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro). ⚠️ Грабля 10.09 (NODE-0X): этот прибор ТОЖЕ стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — на 5-м заходе за сутки он отбивается, и «доказать счётчиком» становится нечем. Тот же класс, что каветат про `fleet_fix_audit.py` в Step 3🔗. Отбило → либо `--force` с названной оператору причиной, либо честная строка в отчёте «дверь проверена глазами, счётчик отбит суточным гейтом» — молча пропускать проверку нельзя.

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 кандидата/ночь, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.
**⭐ HN-кандидат (dev «+++» 10.09):** тот же проход задаёт ВТОРОЙ вопрос ровно один раз на артефакт — «это годится в Hacker News?». Годится ТОЛЬКО жанр «мы померили и показываем цифры» (post-mortem · замер · разбор поломки) и ТОЛЬКО как самостоятельная публичная страница с данными, не пост из ежедневного девлога. Да → строка в `$OBSIDIAN_VAULT/_outreach/hn_candidates.jsonl` (added·from·artifact·title·url·numbers·genre·status:ready|needs-page·blocked_by). Нет → молча, вердикт не нужен. ⛔ Потолок лейна: **своя ссылка на HN не чаще 1 раза в 2 недели** (ежедневный поток туда = профиль спамера, теневой бан накрывает аккаунт И домен); регулярное присутствие = комментарии в ЧУЖИХ тредах 1-3/нед. ⛔ Подача идёт ТОЛЬКО с хаба, ТОЛЬКО после «+» оператора и ОК Норы, ноль организованного голосования. Пока нет входа в HN на хабе — очередь копится, наружу не уходит ничего.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].
**⭐ Мини-тизер обязателен (dev 01.09):** every retro with a substantive arc births ≥1 mini-teaser (200-250 chars, «грабли → правило» so the READER gets use, not a status report) → `python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук>" --note "<тизер>" --tier teaser`. Verdict «no teaser» is legal ONLY with a named reason (empty routine session). Canon: `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`.

## 🛠 ВЕРДИКТ О СКИЛЛЕ, КОТОРЫМ ПОЛЬЗОВАЛИСЬ (dev 07.09, голосом — обязателен, молчание = нарушение)
Применил в этой работе скилл — вынеси вердикт об ЕГО обновлении. Одной строкой, с причиной в обе стороны:
`🔧 обновляю /X — <что споткнулось>` (чинить В ТОМ ЖЕ заходе) · `📝 обновлю не сейчас — <причина>, строка легла в <адрес>` · `✅ /X обновлять не надо — <почему именно: прошло без заминки / заминка разовая и внешняя / правка дороже боли>`.

⭐ **ВЕРДИКТОВ ДВА, НЕ ОДИН** (dev 13.09, голосом). Второй вердикт: **собственная инструкция того, кто сейчас работал** (рутина `scheduled-tasks/<имя>/SKILL.md`, сид, хук): «не стоит ли переписать мою инструкцию на будущее, чтобы она была качественнее?». Та же тройка `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, всегда с причиной. ⚠️ Замер 13.09: рутина `devto-publish-rhythm` починила СВОЙ файл и смолчала про скилл `/comments`, где висел ПРОТИВОПОЛОЖНЫЙ гейт, правило исполнилось наполовину, и спрашивать пришлось оператору. Канон живёт в СКИЛЛЕ, рутина держит только специфику прогона: разошлись, значит правду в скилл, а из рутины указатель. Канон: [[routine-judges-its-own-instruction-too]], CLAUDE.md §9.3-бис.
Пустое «не надо» вердиктом не является. ⛔ Не путать с `/skill-gap` (тот про скилл, которого НЕТ) и не право раздувать: АК-47 в силе — правка снимает ПЕРЕЖИТУЮ боль, не гипотетическую.
Канон: Библия `reglament-polzuemsya-skillom-srazu-sudim-nado-li-ego-obnovit` · CLAUDE.md §9.3-бис · [[skill-used-judge-if-it-needs-update]].

## Step 4★ — The «repeats → make a skill» reflex (milestone closeout)
This is the step dev asked for (2026-06-18): at a finished milestone, don't just *note* a repeating action — **offer to turn it into a skill**. It's the retro-time expression of the standing rule `evaluate-recurring-into-routine` (повторяющаяся задача → оцени «на рутину?»). Mirror of [[capture-rules-into-bible]] (that catches *rules*; this catches *tasks-to-automate*).

**Trigger (catch it, don't wait to be asked):** any action that **repeated ≥2–3×** this session/milestone, OR that we'll **clearly return to** later (a manual sequence I re-typed, a multi-step procedure, a recurring check).

**Procedure — 4 cheap moves:**
1. **RECALL first — don't duplicate.** Skim the available skills + memory `automation-inventory` for an existing skill/routine/hook that already covers it. If one exists, point dev to it instead of building a twin. **⛳ И тут же второй вопрос (dev hub:5090, 2026-08-04): скилл ЕСТЬ — не проапгрейдить ли его?** «Есть» ≠ «закрыто»: назови, чего ему не хватило ИМЕННО в этой сессии (шаг, который я делал руками поверх скилла / грабли, которых в нём нет / устаревшая строка) → правка в тот же заход, и это тоже строка в 🔁→🛠 (`built/proposed/declined`). Нечего добавить — скажи это словом, молчание = проверка не сработала. Дословный текст вопроса и формат ответа — единственный источник в `/skill-gap` §⛳ (там же — вход-конец рефлекса).
2. **⚠️ AK-47 guard — a skill is just a `SKILL.md`.** One markdown file with a procedure, NOT a server / DB / webhook / external service. (This is the exact trap the Codex milestone-retro report fell into — over-engineered for a SWE team; rejected 2026-06-18.) If the thing genuinely needs more than a markdown procedure, flag it **⚠️ УСЛОЖНЕНИЕ** and let dev decide.
3. **OFFER as ДО→ПОСЛЕ** (per `show-before-after`) — one compact block:
   > **ЧТО:** собрать `/<имя-скилла>` · **ДО:** как делаю руками сейчас (на реальном примере этой сессии) · **ПОСЛЕ:** одна команда `/<имя>` · **что сломается:** ничего (надстройка) · **делаем? да/нет**
4. **On dev's «+» → build it via `skill-creator`.** Pick the right home by SHAPE (per `operating-agreement` → «Where durable rules go»):
   - on-demand ritual I run when asked → **skill** (`skill-creator`).
   - «каждый раз автоматически когда X» → **hook** (skill `update-config`), not a skill.
   - time-based «каждый понедельник / каждое утро» → **scheduled task / routine** (skill `schedule`).
   - «рутина» ≠ обязательно 24/7-робот — часто правильное = простой полуавто + напоминание.
   - ⭐ **СПИСОЧНАЯ работа на N кусков (N велико) → КОНЕЧНАЯ рутина, «слон»** (dev 23.08, §4.5-бис).
     Признак: в сессии я перебирал однотипные элементы (видео / заметки / карточки / островá графа /
     ссылки), список не кончился, и он не кончится и в следующий раз; либо задача уже месяцами
     спотыкается об участие оператора, лимиты вендора или баны. Это НЕ задача и НЕ героическая сессия —
     это слон: `python ~/.claude/scripts/elephant.py new <slug> --title T --quota N --os-task <ЗадачаWindows>`,
     дальше рабочий скрипт на каждом прогоне делает `next` → работа → `mark` → `tick`.
     `tick` сам ловит конец (выключает OS-задачу + доклад в TG-03) и затык (5 пустых прогонов → `blocked`).
     ⛔ Журнал слона НИКОГДА не кладём в синкаемую папку — затрётся, и слон не кончится никогда.
     Живой пример: [[yt-watch-history-drip]]. Канон: [[finite-routines-eat-the-elephant]].
   Then route/link it normally (Step 4) and mention it in the final report (post-hoc, not for permission).
5. **⭐ Скилл уходит в мир (dev 01.09, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** любой собранный/существенно обновлённый скилл в том же заходе получает (а) тизер-пост в наши соцсети (через content-factory / каскад) и (б) публикацию самого скилла на нашем публичном GitHub (дефолт `tonydzi/clawrush` `artifacts/`) ПОСЛЕ leak-scan, с пометкой в шапке «built for dev's fleet — adapt paths/names to your setup». Заточен под оператора / сырой / «на тормозке» — публикуем всё равно, честно пометив. Скип — только с названной причиной (leak-scan red / чистая кухня CRM).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
4б. **🔄 Outcome** — «N проверено · M живут · K мертвы + решения» (Step 3🔄).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the FULL enriched `/compact` block printed inline (Step 6b; указатель на файл запрещён).
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Write a clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- ⚠️ **Хук `orphan_check_hook` отобьёт запись: новое ретро рождается сиротой.** Дом входящей ссылки один и он известен: `01-Conversations/Claude/_Claude-Sessions-MOC.md`, секция «Свежие ретро» (плюс на ретро ссылаются `DayLedgers/day-ledger-*.md` и `00-System/Breakage-Journal.md`). Впиши строку `- [[retro-...]] · <в чём суть>` ТУДА, сразу после 6a, не дожидаясь отбоя.
  ⚠️ Грабля замера 14.09.2026: искать дом грепом по всему волту НЕ надо, `grep -rl` по `D:\Vault\Vault-Knowledge` уходит в таймаут 120с. На таймауте я объявил «ретро не линкует никто» и вписал этот вывод сюда как факт; фоновый прогон досчитался и вывод ОПРОВЕРГ. Ровно [[prichina-kak-claim]]: незавершённый поиск даёт «я не нашёл», а не «этого нет».
  Вторая ссылка из содержательного дома (реглумент/концепт/решение, к которому ретро относится) полезна и закрывает заодно Step 4, но обязательной является ссылка из MOC.
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- The nightly **Brain Reindex @04:00** makes it `/ask`-searchable — no manual reindex needed.

**6a-бис. Снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- Команда: `python ~/.claude/scripts/retro_lost_scan.py mark-done <sessionId> --note "ретро: <имя заметки>"`
  ⚠️ Путь через `~`, НЕ через `%USERPROFILE%`: в Bash-инструменте (Git Bash) cmd-переменная не раскрывается и склеивается в мусорный путь `%USERPROFILE%.claudescripts…` — сессия остаётся в очереди, а ты думаешь, что снял (замер 10.09.2026, хаб).
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6a-тер. Переименуй сессию: префикс «Р+» в видимом имени — СРАЗУ после 6a-бис** (⭐ dev 02.09.2026, голосом: «когда я вижу Р+, я понимаю, что дошёл в этой сессии до крупного milestone»).
- Вызови `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → возьми текущий `title`. Если он УЖЕ начинается с `Р+`/`р+`/`рр+` — шаг закрыт, второй префикс не лепить.
- Иначе `mcp__ccd_session_mgmt__set_session_title` с `session_id: "self"` и `title: "Р+<старое имя без изменений>"`. Меняется ТОЛЬКО человекочитаемое имя в приложении (titleSource=tool), системный id не трогается; имя, данное оператором, сохраняется целиком после префикса.
- MCP session_mgmt недоступен (headless `claude -p`, чужой харнес) → одна строка в отчёте «Р+ не поставлен: нет session_mgmt», не молчи.

**6a-кватер. Проверь ИКОНКУ группы в заголовке — сразу после Р+** (⭐ dev 07.09.2026 «кладёшь её в нужную группу»; ⭐ dev 10.09.2026, голосом: «мало пикселей на экране, нужна иконка», и «переименовывать НА СТАРТЕ»).
- Иконка ставится НЕ здесь, а на СТАРТЕ сессии (скилл `/session-groups`). Ретро только ПЕРЕПРОВЕРЯЕТ: тема сессии за день могла уехать в другую группу.
- `get_session self` уже вызван в 6a-тер. Заголовок начинается с иконки из алфавита? 💰 $$$ (деньги/оффер/витрины/статьи наружу) · 🧠 2мозг (волт/RAG/память/клон) · ✍️ content (посты/соцсети/Майкрофт) · 🎯 Лиды-CRM · ⚙️ Инфра (скрипты/флот/синк/канон/браузеры) · 🔬 ДРы · 🏠 личное · 📥 SINK (инбокс/шина/посылки) · ❓ не понял.
- Иконки нет ЛИБО она уже не про эту сессию → `set_session_title self` в форму `<иконка> Р+ <имя>`. Веха `Р+` живёт ПОСЛЕ иконки. Гадать запрещено: тема не читается — ставь ❓, оператор разнесёт сам.
- Строка в отчёт: «иконка: <какая>, флаг ccd_sidebar OFF». Молчать нельзя.
- Рычаг настоящего переноса = MCP `ccd_sidebar.move_sessions`, появляется только когда приложение его отдаёт: проверка `python ~/.claude/scripts/claude_desktop_gate_probe.py` (exit 0 = флаг id_0bae24da ON) → тогда переноси по-настоящему, а иконка больше не нужна. Замер 07-10.09: флага в выдаче фич нет, issue anthropics/claude-code#92621.
- ⛔ Правка `claude_desktop_config.json` руками НЕ рельса: приложение файл живьём не перечитывает и перепишет из памяти (замер 07.09).
- Канон: память `session-group-at-retro`; движок и алфавит — скилл `/session-groups`; публичная копия github.com/tonydzi/claude-session-icons.

**6b. PRINT the READY enriched paste-line INLINE — обязательный выход КАЖДОГО ретро (⭐ dev 26.08, голосом: «каждый раз давай готовый текст компакта; иди-в-файлик — неудобно»).**
- ⚠️ Fact base (2026-07-22): bare `/compact` does NOT read our format — 354/354 past compacts fell back to the DEFAULT English template; PreCompact hooks cannot inject (issue #14160). The 7-header format applies ONLY pasted inline: `/compact <text>`.
- **Procedure = same enrichment as `/cc` Steps 2-3** (single source of mechanics — don't duplicate, read `~/.claude/skills/cc/SKILL.md`): take the skeleton from `$USERPROFILE/.claude/compact-prompt.md` § «Готовая строка», FILL all 7 headers with THIS session's real facts — reuse the distillation already written into the 6a vault note, don't re-derive — and PRINT one fenced ```code``` block starting with `/compact `, со строкой над ним: «➤ Скопируй блок целиком и вставь следующим сообщением». Then the fork:
> **«Готово, всё в волте. Остаёшься в сессии — вставь блок ниже целиком (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — просто уходи, всё уже заархивировано.»**
- ⛔ **Указатель вместо блока ЗАПРЕЩЁН.** «Вставь блок из `~/.claude/compact-prompt.md`» / «возьми текст в файле» = нарушение правила (ровно эта формулировка — жалоба оператора 26.08). Пустой скелет с `<...>` — тоже нарушение: блок обязан быть обогащён сессией. Канон: память `compact-dev-prefers-zero-touch` §Поправка 26.08 + `compact-format-delivery-gotcha`.
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; printing the ready line is my half, the paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

## ⭐ Полнота списка потребителей (dev 10.09.2026)

Первый найденный потребитель почти никогда не единственный — он просто лежал на поверхности. Поиск закончен не когда кто-то найден, а когда **две оси подряд дали ноль новых имён**; внутренний потребитель (узел флота, робот, наш же скилл с костылём) ищется ПЕРВЫМ. Девять осей перебора и обязательный вердикт с числом («осей N/9 · адресов M · насыщение да/нет») — `/consumer-hunt` §Шаг 1-бис. ⚠️ Исчерпывающим обязан быть ПОИСК, адресация идёт по правилам двери: найденный адрес не выбрасывается, а получает статус и дату (🟢 постучались · ⏸ глухая очередь по замеру · 🪦 непереносимо). Канон: `reglament-vypustil-funkcional-naydi-potrebiteley-i-pridi-k-nim` §Поправка 10.09 + [[consumers-are-a-set-not-the-first-one]].

---

> `Bash` -- {"command": "python \"D:\\Vault\\_imports\\turnstate\\turnstate_show.py\" 2>&1 | tail -25", "description": "Session black box spine"}

---

> `Bash` -- {"command": "ls -t /e/Obsidian/Vault-Knowledge/01-Conversations/Claude/Retros/ 2>/dev/null | head -8; echo \"=== inventory ===\"; python \"D:\\Vault\\_imports\\retro_inventory.py\" 1 2>&1 | tail -6", "description": "Recent retros and inventory"}

---

> `Bash` -- {"command": "grep -n -i \"job-inbox\\|interview_calendar\\|pipe.a.inbox\" /e/Obsidian/_imports/retro_candidates/digest-latest.md | head -10; echo \"=== память: сироты ===\"; python ~/.claude/scripts/memory_harvest.py --scan 2>&1 | tail -3; echo \"=== указатель на месте? ===\"; grep -c \"booked-inter

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"отсутствие файла-артефакта принято за отсутствие работы: судил по наличию отчётов вместо счётчика прогонов\" 2>&1 | head -12", "description": "Count class for my wrong inference"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python selfheal.py journal --class \"routine-judged-by-artifact-not-by-runcount\" --what \"Объявил оператору, что рутина pipe-a-inbox-watch пропускала прогоны 08,11,12,13.09 — судил по наличию файлов reports/inbox-watch-*.md. Они пишутся только в дни с живыми письма

---

**Claude:**

Дверь для этого класса — в самом /retro, в шаге RECALL, где я и споткнулся:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_5cba2997\\scratchpad\\patch_retro.py", "content": "\"\"\"Дверь класса routine-judged-by-artifact-not-by-runcount: строка в recall-стек /retro.\"\"\"\nimport io\nimport shutil\n\nP

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5cba2997/scratchpad/patch_retro.py\" && grep -n \"2в\\.\" ~/.claude/skills/retro/SKILL.md | head -2; echo \"=== onair ===\"; python ~/.claude/scripts/onair.py list 2>&1 | grep -i \

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-15-kong-glider-screening.md", "content": "---\ntitle: \"Kong: пройти скрининг Glider (Forward Deployed Engineer)\"\ndate: 2026-09-15\ntype: task\nstate: open\nprio: P1\nowner: dev\nborn_in: \"[[retro-2026-09-15-interview-reached-

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-15-kong-glider-screening.md", "content": "---\ntitle: \"Kong: пройти скрининг Glider (Forward Deployed Engineer)\"\ndate: 2026-09-15\ntype: task\nstate: open\npriority: P1\nprio: P1\nowner: dev\nborn_in: \"retro-2026-09-15-interv

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && grep -n \"task-2026-09-1\" _Tasks-MOC.md 2>/dev/null | tail -3; ls | grep -i \"MOC\"", "description": "Find tasks MOC to wire the new task"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\np='_Tasks-MOC.md'\ns=io.open(p,encoding='utf-8').read()\nanchor=\"- [[task-2026-09-15-cron-watchdog-dead-twin]]\"\nline=(\"- [[task-2026-09-15-kong-glider-screening]] — P1 (руки оператора): Kong зовёт на скрининг Glider по Forward Deployed Engineer с 09.09, \"\n

---

**Claude:**

Теперь заметка ретро в волт и тизер:

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-09-15-interview-reached-antons-calendar.md", "content": "---\ntitle: \"Два собеседования нашлись за 8 часов до звонка: бронь была, календаря не было\"\naliases: [\"Ретро 15.09.2026 — интервью доехало до календ

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/01-Conversations/Claude && python - <<'PY'\nimport io\np='_Claude-Sessions-MOC.md'\ns=io.open(p,encoding='utf-8').read()\nline=\"- [[retro-2026-09-15-interview-reached-antons-calendar]] · два собеседования были забуканы и потеряны: приглашение падает в кал

---

> `Bash` -- {"command": "python ~/.claude/scripts/retro_lost_scan.py mark-done s_5cba2997 --note \"ретро: retro-2026-09-15-interview-reached-antons-calendar\" 2>&1 | tail -2; echo \"=== тизер ===\"; python \"D:\\Vault\\_imports\\content-factory\\content_miner.py\" capture --title \"

---

[СКРЫТО]

---

**Claude:**

Снёс твой «+++» из заголовка — возвращаю:

---

[СКРЫТО]

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python interview_calendar_guard.py; echo \"guard=$?\"; python _test_interview_calendar_guard.py; echo \"test=$?\"; python \"D:\\Vault\\_imports\\jobs-watch\\pipe_a_ball.py\" 2>/dev/null | head -3; cd ~/.claude/scripts && python pipe_a_inbox_prega

---

**Claude:**

[СКРЫТО]

---

**User:**

Stop hook feedback:
СТОП: ты объявляешь недоступность, не обойдя ВСЕ поверхности.
  фрагмент: …чисто · 2 бронь без календаря · 3 база недоступна; судит НАШУ отметку cal:, а не Google (у токена a@ только gmail-скоупы, кален…
(последний обход: claude_ai, 155 мин назад — не тот вендор или устарел)

Класс замерен трижды за трое суток (29-31.07): вывод «Google мёртв» делался по ОДНОМУ
профилю, пока живая сессия лежала в Chrome на другом аккаунте. Каждый повтор = ложный
аск оператору + день не той работы.

Сделай ДО вывода:
    python3 ~/.claude/scripts/rail_sweep.py google
Он перечислит ВСЕ места (профили рельсы · системный Firefox · профили Chrome · Chrome-MCP)
и назовёт те, что с диска не читаются — их проверяют ЖИВОЙ вкладкой, а не файлом.
Вывод «доступа нет» законен, только когда пусты ВСЕ поверхности из списка.
Если место одно и ты это знаешь — так и напиши: «в профиле X сессии нет» (per-профиль),
а не «X недоступен» (про весь мир).

---

**Claude:**

[⏰ вторник, день, 13:48]

Хук прав — я объявил «локальной рельсы календаря нет» по одному токену. Обхожу все поверхности.

---

> `Bash` -- {"command": "python ~/.claude/scripts/rail_sweep.py google 2>&1 | head -40", "description": "Sweep all Google rail surfaces"}

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers", "max_results": 1}

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

**Claude:**

Обход меняет формулировку. Правлю во всех трёх домах, где я её записал:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_5cba2997\\scratchpad\\fix_rail_claim.py", "content": "\"\"\"Сузить вывод «локальной рельсы календаря НЕТ» до проверенного: нет СКРИПТОВОЙ, браузерная есть.\n\nОбход rail_sweep.py 

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5cba2997/scratchpad/fix_rail_claim.py\"", "description": "Apply narrowed rail claim to all three homes"}

---

**Claude:**

Проверка в моём же скрипте дала ложное совпадение — ретро-заметка не поправилась. Чиню:

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/01-Conversations/Claude/Retros && grep -c \"Поправка 13:48\" retro-2026-09-15-interview-reached-antons-calendar.md", "description": "Confirm retro note was not patched"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_5cba2997\\scratchpad\\fix_retro_note.py", "content": "\"\"\"Дописать в ретро-заметку поправку 13:48 (обход поверхностей опроверг «рельсы нет»).\"\"\"\nimport io\n\nP = r\"E:\\Obsi

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_5cba2997/scratchpad/fix_retro_note.py\" && cd ~/.claude/scripts && python selfheal.py journal --class \"rail-verdict-wider-than-instrument-sight\" --what \"Записал в скилл, память 

---

**Claude:**

[⏰ вторник, день, 13:52]

## Хук поймал вторую ошибку того же класса

Я написал «локальной рельсы Google Calendar на узле нет», проверив **один** OAuth-токен. Обход `rail_sweep.py google` назвал **5 поверхностей**: 4 профиля Firefox с Google-куками на диске плюс подключённый Chrome-MCP (два браузера, один локальный). Браузерный путь к `calendar.google.com` существует — он просто дороже, и живость куки доказывается запросом, а не файлом.

Что осталось верным: у токена `a@` действительно только `gmail.modify` и `gmail.send` — это я читал. Что было неверным: **масштаб вывода**. Законная формулировка — «в скриптовой рельсе двери нет», а не «рельсы нет». Разница практическая: второй агент (Codex) теперь не скажет «рельса мимо» там, где у него есть selenium через залогиненный профиль.

Поправлено во всех трёх домах, где я это записал: скилл `/job-inbox`, память, ретро-заметка. Класс `rail-verdict-wider-than-instrument-sight` в журнале.

**Оба промаха сессии — один корень: вывод шире, чем зрение прибора.** Утром судил работу рутины по наличию файлов вместо счётчика прогонов. Днём судил доступность Google по одному токену вместо обхода поверхностей. Первый поймал сам, второй поймал хук. Семья этого класса в `prior_art` — 6 прежних случаев; неприятно, что я дал ей седьмой и восьмой за один день.

Заодно всплыл мелкий баг в моём же патч-скрипте: проверка «уже поправлено» сравнивала первую строку нового текста, которая совпадала со старым, и молча пропустила ретро-заметку. Поймал грепом, дописал.

**Замени в компакт-блоке последний абзац на этот:**

```
- ИНСТРУМЕНТЫ И КОНТРАКТЫ — interview_calendar_guard.py: exit 0 чисто · 2 бронь без календаря · 3 база недоступна; судит НАШУ отметку cal:, а не Google. У токена a@ только gmail-скоупы, СКРИПТОВОЙ рельсы календаря не нашёл — но rail_sweep.py google назвал 5 поверхностей (4 профиля Firefox с Google-куками + живой Chrome-MCP), значит браузерный путь есть, он просто дороже; «рельсы нет» говорить запрещено, законно только «в скриптовой рельсе двери нет». routine_cost_audit.py --days N колонка «прог.» отвечает «бежала ли рутина»; файлы отчётов НЕ отвечают, они пишутся только в дни с живыми письмами. pipe_a_inbox_pregate.open_interviews() — будилка по status='interview'. gmail_check.py: search берёт аккаунт флагом --label a, read — позиционно (read a <id>).
```

🧒 **Простыми словами:** я во второй раз за день сказал «этого нет», проверив только одно место. Сторож меня остановил и заставил обойти все пять — оказалось, дорога есть, просто длиннее. Исправил везде, где успел записать неправду, и записал сам урок: прежде чем говорить «нельзя», надо обойти все двери, а не первую.
