---
session: s_25ad27db
date: 2026-09-09
words: 1207
turns: 7
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-09 · дай мне аудит всех наших подач на работу на вакансии меня

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_25ad27db` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

дай мне аудит всех наших подач на работу на вакансии меня

таблицу из всех вакансий куда мы подали и куда нет и почему

такая таблица уже вроде есть

---

**Claude:**

16:34, среда, 9 сентября 2026

Понял. Ищу существующую таблицу подач, а не строю с нуля.

---

> `Bash` -- {"command": "ls -la ~/.claude/skills/apply/ 2>/dev/null | head -40", "description": "Look at apply skill dir"}

---

> `Bash` -- {"command": "find /e/Obsidian/Vault-Knowledge -iname \"*applic*\" -o -iname \"*vacanc*\" -o -iname \"*vakans*\" -o -iname \"*job*appl*\" 2>/dev/null | head -40", "description": "Find application tracking files in vault"}

---

**Claude:**

Есть скилл `/apply` с реестром. Смотрю, где живёт истина.

---

> `Bash` -- {"command": "cd ~/.claude/skills/apply && ls -la tools/ && head -c 3000 SKILL.md", "description": "Inspect apply skill head and tools"}

---

**Claude:**

Истина = `jobs.db` + Google Sheets «Pipe-A Funnel». Локальный jobs.db в скилле пустой — ищу настоящий.

---

> `Bash` -- {"command": "find /e/Obsidian/_imports -name \"jobs.db\" -o -name \"jobs*.db\" 2>/dev/null | head; echo \"---\"; ls -la /e/Obsidian/_imports/jobs-watch/ 2>/dev/null | head -40", "description": "Locate jobs.db"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor r in c.execute(\\\"select name from sqlite_master where type='table'\\\"): print(r[0])\nprint('---')\nfor t in [r[0] for r in c.execute(\\\"select name from sqlite_master where type='ta

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor t in ['ats_jobs','jobs','sheet_shadow']:\n    print('==',t)\n    print([r[1] for r in c.execute(f'PRAGMA table_info({t})')])\n\"", "description": "Schema of jobs tables"}

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db'); c.row_factory=sqlite3.Row\nprint('-- status counts --')\nfor r in c.execute('select coalesce(status,\\\"(null)\\\") s, count(*) n from ats_jobs group by 1 order by n desc'): print(f'{r[0]:<28} {r[1]}')\nprint('-- applied not nu

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge/_Dashboards/ | grep -i -E \"pipe|job|apply|vacan|funnel\"; echo \"--- projects ---\"; ls /e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/ 2>/dev/null | tail -20", "description": "Look for existing dashboards"}

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint('applied by date:')\nfor r in c.execute(\\\"select substr(applied,1,10) d,count(*) from ats_jobs where status='applied' group by 1 order by 1\\\"): print(r[0],r[1])\nprint()\nprint('applied by ats:')\nfor r in c.execute(\

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint('== VIP tier by status ==')\nfor r in c.execute(\\\"select status,count(*) from ats_jobs where tier='vip' group by 1 order by 2 desc\\\"): print(f'{r[0]:<28}{r[1]}')\nprint()\nprint('== blocked/rejected/closed detail: top

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint('== NEW pool: by tier & score bucket ==')\nfor r in c.execute(\\\"select tier, case when score>=80 then '80+' when score>=60 then '60-79' when score>=40 then '40-59' else '<40' end b, count(*) from ats_jobs where status='

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint('score distinct:', list(c.execute('select score, count(*) from ats_jobs group by 1 order by 2 desc limit 10')))\nprint()\nprint('== TOP-10 LLM companies presence ==')\nnames=['openai','anthropic','deepmind','google','meta

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint('== interview ==')\nfor r in c.execute(\\\"select company,title,url,applied,answer from ats_jobs where status='interview'\\\"): print(r)\nprint()\nprint('== rejected ==')\nfor r in c.execute(\\\"select company,title,appli

---

> `Bash` -- {"command": "sed -n '1,60p' /e/Obsidian/_imports/jobs-watch/batch_daily.py", "description": "Read batch_daily caps"}

---

**Claude:**

Данные собраны. Кладу аудит вкладкой в уже существующую книгу «Pipe-A Funnel» (§2.4 — новые дашборды в Таблицы).

---

> `Bash` -- {"command": "ls ~/.claude/scripts/sheets.py /e/Obsidian/_imports/sheets.py 2>/dev/null; python -c \"import sys; sys.path.insert(0,r'C:\\Users\\dev\\.claude\\scripts'); import sheets; print([f for f in dir(sheets) if not f.startswith('_')])\" 2>&1 | tail -3", "description": "Check sheets helper"}

---

> `Bash` -- {"command": "mkdir -p \"$SCRATCH\" 2>/dev/null; cat > /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_25ad27db/scratchpad/audit_build.py <<'EOF'\n# -*- coding: utf-8 -*-\n\"\"\"Аудит подач Трубы А: собирает из jobs.db сводку по компаниям + причинам.\

---

> `Bash` -- {"command": "grep -n \"^def \\(ensure_tab\\|set_range\\|read_tab\\|list_tabs\\|freeze_header\\|share\\)\" -A6 /c/Users/dev/.claude/scripts/sheets.py", "description": "Sheets API signatures"}

---

> `Bash` -- {"command": "cat > /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_25ad27db/scratchpad/audit_push.py <<'EOF'\n# -*- coding: utf-8 -*-\nimport sys, json, sqlite3, collections, datetime\nsys.path.insert(0, r\"C:\\Users\\dev\\.claude\\scripts\")\nimpo

---

> `Bash` -- {"command": "python -c \"\nimport sys; sys.path.insert(0,r'C:\\Users\\dev\\.claude\\scripts'); import sheets\nSID='1nbVAXkQZxnWIBwOAEXs4hKN5XCtXDgYepoaMFPWOmIw'\nprint('tabs:',list(sheets.list_tabs(SID)))\na=sheets.read_tab(SID,'audit-companies'); print('rows companies:',len(a)); print(a[0]); prin

---

**Claude:**

Заметил: в книге уже были вкладки `podachi` / `oshibki` / `spornoe` — это и есть «та таблица». Сверяюсь с ней.

---

> `Bash` -- {"command": "python -c \"\nimport sys; sys.path.insert(0,r'C:\\Users\\dev\\.claude\\scripts'); import sheets\nSID='1nbVAXkQZxnWIBwOAEXs4hKN5XCtXDgYepoaMFPWOmIw'\nfor t in ['podachi','oshibki','spornoe','stats']:\n    v=sheets.read_tab(SID,t)\n    print('==',t,'rows',len(v))\n    for r in v[:3]: pr

---

> `Bash` -- {"command": "python -c \"\nimport sys; sys.path.insert(0,r'C:\\Users\\dev\\.claude\\scripts'); import sheets\nv=sheets.read_tab('1nbVAXkQZxnWIBwOAEXs4hKN5XCtXDgYepoaMFPWOmIw','podachi')[1:]\nd=sorted(r[0] for r in v if r and r[0])\nprint('podachi: строк',len(v),'| диапазон',d[0],'->',d[-1])\n\"", 

---

**Claude:**

**Аудит готов. Ты был прав — таблица есть, но она построчная; свода «куда не подали и почему» в ней не было. Я его добавил в ту же книгу.**

📊 [Pipe-A Funnel](https://docs.google.com/spreadsheets/d/1nbVAXkQZxnWIBwOAEXs4hKN5XCtXDgYepoaMFPWOmIw) — новые вкладки `audit-companies` (1604 компании) и `audit-why-not` (240 причин). Старые `podachi` / `oshibki` / `spornoe` не трогал.

## Цифры (истина = `jobs.db`, срез 09.09 16:35)

| | |
|---|---|
| Вакансий в базе | **6558** (447 VIP / 6104 mass) |
| **Реально подались** | **488** (453 живых + 33 отказа + 2 интервью) |
| Заблокировано на форме | **523** |
| Снято/мертво/пропуск | 92 |
| **Не подавали вообще** | **5455** (83%) |

Подачи идут с 01.09, пик 03.09 (122 за день). Рельса: Ashby 354 · Greenhouse 82 · HN 12 · Lever 2.

## Куда НЕ подали и почему

| Причина | Строк | Это стена или очередь? |
|---|---|---|
| Просто не дошла очередь | **5437** | 🟡 очередь: отбор берёт 20/день, ≤2 на компанию, ≤6 на кластер |
| Форма отбила («couldn't submit» / «needs corrections») | 110 | 🔴 стена: наши ответы не проходят валидацию |
| Анти-бот гейт / reCAPTCHA / код из письма | 124 | 🔴 стена: нужны руки человека |
| Нет канон-ответа на нестандартный вопрос | ~60 | 🟡 чинится дописыванием `answers-canon.md` |
| Дверь не та (url ведёт не на форму) | 40 | 🟡 чинится резолвером двери |
| Submit нажат, подтверждения не поймали | 23 | ⚠️ спорное — в `spornoe` 210 строк «письмом не доказано» |
| Сингапур, нет права на работу | 4 | 🟢 честный скип |

## Топ-10 LLM (миссия №1)

| Компания | Подали | Отказ | Открыто | Не тронуто |
|---|---|---|---|---|
| Anthropic | 8 | 3 | 5 | **134** |
| xAI | 8 | 2 | 6 | 1 |
| OpenAI | 4 | 0 | 4 | **153** (лимит 5/180д — остался 1) |
| Cohere | 5 | 0 | 5 | 24 |
| Mistral AI | 3 | 0 | 3 | 61 (лимит 3/90д — **выбран**) |
| Perplexity | 1 | 0 | 1 | 16 |
| Google DeepMind | **0** | — | — | 1 |
| Meta / NVIDIA / Microsoft | **0** | — | — | 8+ |

**Результат на сегодня: 2 интервью** — Lambda Labs (Senior Solution Engineer) и nango (Founding DevRel). Отказов 33, из них 11 приехали одним днём 08.09.

🎙 Майк: идём верно по объёму, но неверно по адресу. 5455 неподанных — это не очередь, это **фильтр отбора работает по скору, а не по миссии**: DeepMind у нас в базе 1 вакансия, Meta и NVIDIA — ноль подач при живых строках. Мы жжём 20 подач/день в mass-тир, пока VIP-пул в 361 строку стоит нетронутым. Вопрос: переворачиваем отбор на «сначала VIP, mass только добивкой» — или ты сознательно держишь широкий веер ради статистики отказов?

🧒 Простыми словами: мы разослали 488 анкет, из них 2 позвали поговорить, 33 отказали. Ещё 5455 анкет лежат нерассланные — просто руки не дошли, машина шлёт по 20 в день. И среди нерассланных лежат самые главные — Anthropic (134 штуки!) и OpenAI (153). Получается, мы старательно стучимся туда, куда не очень надо, а в главную дверь почти не стучали.
