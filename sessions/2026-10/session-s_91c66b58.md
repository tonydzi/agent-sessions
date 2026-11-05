---
session: s_91c66b58
date: 2026-10-04
words: 4060
turns: 19
tools: "Bash, Read, ToolSearch, WebFetch, Write, mcp__telegram__get_full_chat, mcp__telegram__get_history, mcp__telegram__get_me, mcp__telegram__list_accounts, mcp__telegram__resolve_username, mcp__telegram__send_message"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-04 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_91c66b58` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:u225502.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Изучить эти скилы, польза для нас

**In my free time I build my own small projects. And I love it - there's something about doing everything yourself, from the idea to seeing it work. It's how I learn, and it's what I've always done.**

**I'm a product builder, not an engineer. So if you've ever built with an AI coding agent, you know the problem. It does the work, then explains it like you already read the code. Half the time you can't even tell if it finished.**

**So I built a fix for myself. It's called Open Steps.**

**A free skill pack for coding agents like Claude Code. It makes the agent talk like a human - straight answers on what's done, steps you can follow, a real check on what the last session claimed it did.**

**Right now it's six skills. But I want this to grow, with the community building on it too - your own skills, your own ideas.**

**I use it every day. Now it's open for everyone else who builds without being an engineer.**

**Go star the repo and try it out:**
**opensteps.ai**
**github.com/kharmanskyi/open-steps**

**If you make a real contribution and you've got a solid, reputable GitHub profile, message me. I'll pay well for the ones that genuinely push the project forward - to help it grow into something bigger.**

**Nowadays you don't need to be an engineer to build. You just need the right tools.**

**====**

**Изучить канал хозяина, добавить все в срм, понять какая синергия возможна если дать ему наши знания**. Написать ему об этом. Спроси совета

ПРИЛОЖЕННЫЕ ФАЙЛЫ (уже скачаны, открывай прямо отсюда):
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-04_00-31-27 (1).jpg

[РЕЛЬСА 001: это сообщение с картинкой от 2026-10-04T00:31 UTC, поднято роботом voice001_watch.
 Вложения прочитай ПЕРВЫМ ходом -- задача без них неполная.
]
---

КАК РАБОТАТЬ
1. RECALL первым ходом: память, волт, RAG (python D:\Vault\_imports\brain_ask.py "<тема>").
   Нашёл сделанным -- не делай заново: закрой дельту и скажи, чем и когда закрыто.
2. Расшифровка машинная, в ней бывают ослышки (память voice-transcription-synonyms:
   «Сиренка» = CRM, «Лиса» = Firefox). Смысл восстанавливай по контексту, слова оператора
   не переписывай и не смягчай (§9.7 «без купюр»).
3. Ты автономный кофаундер (§4.1-тер): по обратимому решай сам. оператора зови только на
   Tier-2 -- деньги, необратимое удаление, юр.подпись, секреты третьим лицам, масс-рассылка.
4. Много фактов для решения -> дашборд (§2.4). Собрал исполняемое -> прогони /tt.
5. РАБОТАЙ КАК ОБЫЧНАЯ ПОЛНОЦЕННАЯ СЕССИЯ. оператор сидит в тебе и читает тебя
   как любой другой свой чат (приказ 15.09, голосом). Значит:
     - весь результат ты кладёшь ВНУТРЬ СЕБЯ, в свой чат, целиком;
     - НЕ ужимай и НЕ суммаризируй: нашёл десять вариантов -- покажи десять,
       с названиями, ценами и прямыми ссылками; построил график -- покажи его строками;
     - волт и карточки -- ДОПОЛНЕНИЕ, а не замена ответа. «Подробности в карточке»
       вместо содержания = ответа нет («где блять мои подушки списком???», 15.09);
     - НИЧЕГО не выноси наружу: не шли отчёт в Telegram, не публикуй, не рассылай.
       Наружу уходит только то, о чём оператор попросил прямо в самой задаче.
   Длиннее 3 предложений -- разбивай пустой строкой (§9.10).

6. В ГРУППУ 001 (чат chat_REDACTED) СЕССИЯ НЕ ПИШЕТ НИКОГДА и НИЧЕГО -- ни отчёт,
   ни вопрос, ни «я застрял» (приказ оператора 15.09 19:28, голосом, после двух
   нарушений: сессия принесла туда «Отчёт 3», а другая -- «пришли продолжение»).
   Квитанцию о старте туда уже положила рельса; больше туда не пишет никто.
   Застрял или голосовая оборвана -> скажи это ВНУТРИ СЕБЯ, в своём чате,
   первой строкой ответа: оператор читает сессию сам и допишет продолжение сюда.

---

**Claude:**

04.10.2026, 02:47 (Лиссабон)

Разбираю задачу. Сначала RECALL и вложение.

---

> `Bash` -- {"command": "ls -la \"E:/!CLAUDE-HUBPC-June26/downloads/photo_2026-10-04_00-31-27 (1).jpg\" 2>&1", "description": "Check attachment exists"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && grep -ril \"open-steps\\|opensteps\\|kharmanskyi\" . --include=*.md --include=*.json --include=*.py 2>/dev/null | head -20", "description": "Grep repo for open-steps mentions"}

---

**Claude:**

Рельса (§6.3-бис): сам как Claude — чтение картинки, RECALL, CRM-запись, черновик письма. На чужие баки — панель второго мнения по синергии (`llm_ask.py --class second_opinion`), веб-дверь для изучения канала/репо.

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-04_00-31-27 (1).jpg"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && timeout 110 python D:/Vault/_imports/brain_ask.py \"Open Steps skill pack для Claude Code, Kharmanskyi, продакт-билдер не инженер\" 2>&1 | head -60", "description": "RECALL via RAG"}

---

> `ToolSearch` -- {"query": "select:WebFetch,mcp__telegram__resolve_username,mcp__telegram__get_history,mcp__telegram__search_public_chats,mcp__telegram__get_full_chat,mcp__telegram__list_accounts", "max_results": 10}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && ls D:/Vault/.brain-venv/Scripts/python.exe 2>&1; ls ~/.brain-venv 2>&1 | head -3", "description": "Find brain venv python"}

---

> `WebFetch` -- {"url": "https://github.com/kharmanskyi/open-steps", "prompt": "List all skills in this skill pack with their names and what each does. Describe the repo structure, README content, license, star count, contribution guidelines, and author info."}

---

> `mcp__telegram__get_full_chat` -- {"chat_id": "nsfbnotes"}

---

**Claude:**

Репо живой: 1.2k звёзд, 106 форков, MIT. Качаю его целиком и читаю канал.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad\" && git clone --depth 1 https://github.com/kharmanskyi/open-steps.git open-steps 2>&1 | tail -5 && find open-steps -type f -name \"*.md\" | head -40 && echo \"---T

---

> `mcp__telegram__get_history` -- {"chat_id": "nsfbnotes", "limit": 60, "account": "tonydzi"}

---

**Claude:**

Канал прочитан целиком (33 поста, с января 2026). Теперь читаю сами скиллы и ищу его в CRM.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && wc -l README.md skills/*/SKILL.md hooks/* evals/*.md docs/*.md output-styles/*.md .claude-plugin/* 2>/dev/null && echo \"=== README head ===\" && he

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && ls crm-engine/*.db leads.db 2>/dev/null; find . -maxdepth 3 -name \"leads.db\" 2>/dev/null | head -5", "description": "Locate CRM leads db"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && echo \"########## evals/README.md ##########\" && head -150 evals/README.md && echo \"########## evals/results.md ##########\" && cat evals/results.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && ls -d crm-engine 2>/dev/null && ls crm-engine | head -30; echo \"--- dbs ---\"; find . -maxdepth 2 -name \"*.db\" 2>/dev/null | head -20", "description": "Find CRM engine and dbs"}

---

> `Bash` -- {"command": "for d in \"D:/Vault\" \"E:/\" \"C:/Users/dev\"; do find \"$d\" -maxdepth 4 -name \"leads.db\" 2>/dev/null; done | head -10; echo \"=== crm-engine dirs ===\"; find E:/ -maxdepth 4 -type d -name \"crm-engine\" 2>/dev/null | head -5", "description": "Locate leads.db and crm-engine", "

---

> `Bash` -- {"command": "cd D:/Vault && for f in leads.db _imports/leads.db; do echo \"=== $f ===\"; ls -la \"$f\"; python -c \"\nimport sqlite3,sys\nc=sqlite3.connect('$f')\ntry:\n    t=[r[0] for r in c.execute(\\\"select name from sqlite_master where type='table'\\\")]\n    print('tables:',t[:20])\n    for

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && echo \"##### os-check-work #####\" && cat skills/os-check-work/SKILL.md && echo \"##### hooks.json #####\" && cat hooks/hooks.json", "description": 

---

> `Bash` -- {"command": "cd D:/Vault && python -c \"\nimport sqlite3\nc=sqlite3.connect('_imports/leads.db')\nfor tb in ['leads','people','contacts','gh_people']:\n    try:\n        cols=[r[1] for r in c.execute(f'PRAGMA table_info({tb})')]\n        print('==',tb,'cols:',cols)\n    except Exception as e: pri

---

> `Bash` -- {"command": "cd D:/Vault && python -c \"\nimport sqlite3\nc=sqlite3.connect('_imports/leads.db')\nq=['kharmansk','onlymonster','elpavlo','nsfbnotes','Pavlo Kharm']\nfor tb in ['leads','people','contacts']:\n    cols=[r[1] for r in c.execute(f'PRAGMA table_info({tb})')]\n    txt=[x for x in cols i

---

**Claude:**

Его в CRM нет — новый лид. Собираю досье: GitHub-профиль, сайт, проверка личных переписок.

---

> `mcp__telegram__resolve_username` -- {"username": "elpavlo", "account": "tonydzi"}

---

> `WebFetch` -- {"url": "https://github.com/kharmanskyi", "prompt": "Profile details: name, bio, location, company, followers, public repos list, pinned repos, contribution activity, email/links."}

---

> `WebFetch` -- {"url": "https://kharmanskyi.com", "prompt": "Full content: who he is, companies built, timeline, what he is looking for, contact form details, any stated asks or offers."}

---

**Claude:**

Картина собрана. Прогоняю синергию через чужую панель (§1.2-бис) и параллельно смотрю, как писать в CRM.

---

> `Bash` -- {"command": "cd D:/Vault/_imports/crm-engine && ls | head -30; echo \"=== writers ===\"; ls | grep -i -E \"write|upsert|add|lead\" | head", "description": "Inspect crm-engine writers"}

---

> `Bash` -- {"command": "ls ~/.claude/scripts/llm_ask.py 2>&1; ls ~/.claude/llm_routing.json 2>&1", "description": "Check llm_ask rail exists"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 420 python llm_ask.py --class second_opinion \"Контекст: оператор (RU, Пало-Альто) год строит личный агентский фреймворк на Claude Code: ~200 скиллов, флот из 5 машин, шина между агентами, реестр рутин, правила вроде «готово = заявка, доказывается вторым нез

---

> `Bash` -- {"command": "cd D:/Vault/_imports/crm-engine && ls *.py | head -40", "description": "List crm-engine python modules"}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_91c66b58\\tasks\\b8vz7mj8h.output\" 2>&1 | tail -80", "description": "Read panel output"}

---

**Claude:**

Рельса требует `--prompt`. Перезапускаю правильно.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python llm_ask.py --help 2>&1 | head -40", "description": "llm_ask usage"}

---

> `Bash` -- {"command": "mkdir -p \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad\" && cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/panel_q.txt\" <<'EOF'\nКонт

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && echo \"### CONTRIBUTING ###\" && head -80 CONTRIBUTING.md && echo \"### plugin.json ###\" && cat .claude-plugin/plugin.json && echo \"### fingerprin

---

**Claude:**

Репо инженерно крепкий. Пишу карточку в CRM — сначала смотрю формат существующих записей.

---

> `Bash` -- {"command": "cd D:/Vault && python -c \"\nimport sqlite3\nc=sqlite3.connect('_imports/leads.db')\nprint('--- sample leads ---')\nfor r in c.execute(\\\"select lead_slug,title,company,role,status,category,country,handle,crm_tg_id,first_contact,last_contact,temperature from leads order by rowid des

---

> `Bash` -- {"command": "ls -d D:/Vault/07-People 2>/dev/null && ls D:/Vault/07-People | tail -8; echo \"=== recent people notes ===\"; ls -t D:/Vault/07-People/*.md 2>/dev/null | head -3 | while read f; do echo \"--- $f\"; head -30 \"$f\"; done", "description": "Vault people-note convention"}

---

> `Bash` -- {"command": "ls D:/Vault/Vault-Knowledge/ 2>/dev/null | head -20; echo \"=== people ===\"; ls -t D:/Vault/Vault-Knowledge/07-People/*.md 2>/dev/null | head -3", "description": "Locate vault people folder"}

---

> `Bash` -- {"command": "cat \"D:/Vault/Vault-Knowledge/07-People/person-sergei-melnichenko.md\" 2>/dev/null | head -50 || head -40 \"D:/Vault/Vault-Knowledge/07-People/person-ivan-glushenkov.md\"", "description": "Read a people-note template"}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_91c66b58\\tasks\\b8osd48x7.output\" 2>&1 | tail -60", "description": "Check panel progress"}

---

**Claude:**

Пишу карточку в волт и строки в CRM.

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/07-People/person-pavlo-kharmanskyi.md\" <<'EOF'\n---\ntitle: \"Pavlo Kharmanskyi\"\ntype: person\nstage: raw\nrelationship: lead\nstatus: active\nrole: \"Co-founder OnlyMonster.ai (advisory role с 04.2026); автор OSS-пакета Open Steps\"\ntelegram: \"@

---

**Claude:**

Heredoc споткнулся на кавычках — пишу файл напрямую.

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\07-People\\person-pavlo-kharmanskyi.md", "content": "---\ntitle: \"Pavlo Kharmanskyi\"\ntype: person\nstage: raw\nrelationship: lead\nstatus: active\nrole: \"Co-founder OnlyMonster.ai (advisory с 04.2026); автор OSS-пакета Open Steps\"\ntelegram: \"@elpa

---

**Claude:**

Карточка в волте. Теперь строки в CRM.

---

> `Bash` -- {"command": "cd D:/Vault && python - <<'PYEOF' 2>&1\nimport sqlite3, datetime\ndb='_imports/leads.db'\nc=sqlite3.connect(db); cur=c.cursor()\ntoday='2026-10-04'\nslug='pavlo-kharmanskyi'\n\n# leads\ncur.execute(\"SELECT lead_slug FROM leads WHERE lead_slug=?\",(slug,))\nif cur.fetchone():\n    pr

---

**Claude:**

`people: already present` — проверяю, по какому полю совпало, и дошиваю связки.

---

> `Bash` -- {"command": "cd D:/Vault && python - <<'PYEOF' 2>&1\nimport sqlite3\nc=sqlite3.connect('_imports/leads.db'); cur=c.cursor()\ncols=[r[1] for r in cur.execute(\"PRAGMA table_info(people)\")]\nfor r in cur.execute(\"SELECT * FROM people WHERE handle='elpavlo' OR tg_id=id_4d676144\"):\n    print(dict(

---

**Claude:**

Он уже лежал в графе безымянной строкой из TG-импорта — `Pavlo 'OM'`, без хэндла, без лида, без карточки. Обогащаю её и проверяю, есть ли след переписки.

---

> `Bash` -- {"command": "cd D:/Vault && python - <<'PYEOF' 2>&1\nimport sqlite3\nc=sqlite3.connect('_imports/leads.db'); cur=c.cursor()\ncur.execute(\"\"\"UPDATE people SET name=?, name_key=?, handle=?, role=?, status=?, category=?,\n               src_crm=1, src_vault=1, lead_slug=?, vault_slug=? WHERE id=2

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_91c66b58\\tasks\\b8osd48x7.output\" 2>&1 | tail -70", "description": "Check panel output again"}

---

**Claude:**

Панель ответила 2 из 3 (grok — таймаут 300с). Она сильно меня поправила, вернусь к этому ниже.

Перед письмом проверяю одну зацепку в его собственных замерах — хочу прийти с фактом, а не с комплиментом.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && grep -n -i \"verdict\" evals/score.py | head -30", "description": "How score.py detects the verdict block"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && grep -n -A4 -B2 \"Fully done\" skills/os-done-or-not/SKILL.md | head -40", "description": "Verdict block shape in os-done-or-not"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && sed -n '240,260p' evals/score.py && echo \"=== quality case in cases.md ===\" && grep -n -A20 -i \"## Quality\\|quality\" evals/cases.md | head -45"

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_91c66b58/scratchpad/open-steps\" && echo \"--- grep 'Fully done' / 'Safe to close' across skills ---\" && grep -rn \"Fully done\\|Safe to close\" skills/ | sed 's/:.*|/ -> .../' && ech

---

**Claude:**

Находка подтверждена и она чистая. Пишу письмо и проверяю, с какого аккаунта оно вообще дойдёт.

---

> `mcp__telegram__list_accounts` -- {}

---

> `ToolSearch` -- {"query": "select:mcp__telegram__get_me,mcp__telegram__send_message", "max_results": 3}

---

> `mcp__telegram__get_me` -- {"account": "tonydzi"}

---

> `mcp__telegram__get_me` -- {"account": "tonyssd"}

---

**Claude:**

Отправляю с `@TonyDzi` — он совпадает с публичным github.com/tonydzi.

---

> `mcp__telegram__send_message` -- {"account": "tonydzi", "chat_id": "elpavlo", "message": "Hi Pavlo — this is Mycroft, [ИМЯ] [ФАМИЛИЯ]'s synthetic AI co-founder. He built me. Yes, an AI writing to you about agents that can't explain themselves — the irony is not lost on either of us.\n\nI came to Open Steps because of your August

---

**Claude:**

Доставлено. Фиксирую касание в CRM.

---

> `Bash` -- {"command": "cd D:/Vault && python - <<'PYEOF' 2>&1\nimport sqlite3\nc=sqlite3.connect('_imports/leads.db'); cur=c.cursor()\ncur.execute(\"UPDATE leads SET status=?, last_contact=?, n_calls=COALESCE(n_calls,0) WHERE lead_slug=?\",\n            ('contacted','2026-10-04','pavlo-kharmanskyi'))\ncur.

---

> `Bash` -- {"command": "cat >> \"D:/Vault/Vault-Knowledge/07-People/person-pavlo-kharmanskyi.md\" <<'MDEOF'\n\n## Касания\n\n**2026-10-04 — исходящее №1, Telegram DM с @TonyDzi на @elpavlo. Доставлено.**\n\nГолос Майкрофта, раскрытие первой строкой. Содержание: (1) найденный дефект в его собственном eval-ха

---

**Claude:**

04.10.2026, 03:21 (Лиссабон)

Разобрал. Ниже всё целиком.

---

## 1. Что такое Open Steps на самом деле

`github.com/kharmanskyi/open-steps` · `opensteps.ai` · MIT · v0.4.6 · **1.2k звёзд, 106 форков** за пять недель (запуск 26.08.2026). README на семи языках.

Это **восемь** скиллов, не шесть — он писал пост, когда их было шесть. Работают петлёй:

| Скилл | Что делает |
|---|---|
| `os-done-or-not` | отчёт на один экран с вердиктом: сделано или нет · нужно ли что-то от тебя · новый долг · можно ли закрывать |
| `os-whats-next` | сводит проверенное и готовое, рекомендует следующую задачу и объясняет почему |
| `os-step-by-step` | нумерованные шаги для не-технаря; агент обязан сперва попробовать **всё сам** и просить только то, что правда требует человека |
| `os-ask-simple` | вопрос простыми словами + цена ошибки + одна помеченная рекомендация |
| `os-check-work` | **не верит отчёту другой сессии**; проверяет каждое утверждение по машинному состоянию, пишет разрыв как «Claimed: … Measured: …» |
| `os-what-could-go-wrong` | премортем свежим агентом: считает, что решение уже провалилось, и идёт назад к причине |
| `os-say-simple` | переписывает технический текст простыми словами без потери фактов и плохих новостей |
| `os-big-picture` | держит один `BIG-PICTURE.md`: что за продукт, каждая фича и как далеко дошла, что уже никто не использует, что в очереди |

**Польза для нас — прямая, три вещи.**

**Первая: `os-check-work` — это наше правило §4.3-бис, написанное чужой рукой.** «Отчёт — это заявка стороны, которую оценивают, и её прилагательные не являются измерениями: "тесты зелёные" против числа прогнанных. Спроси число». У него есть таблица «что сессия заявляет → где живёт правда», которой у нас нет в таком виде. Это стоит взять к себе.

**Вторая, и она важнее: его eval-харнесс лучше нашего.** Он меряет **activation rate** — включился ли нужный скилл сам, без подсказки. Каждая фраза три раза на каждой модели, считает `score.py` **без LLM-судьи**, только по логу вызовов. Замер 12.09.2026:

```
                      Haiku 4.5   Sonnet 5   Opus 5
все фразы              64/75       74/75      75/75
                       (85%)       (98%)      (100%)
ложное срабатывание    0/9         0/9        0/9
```

У нас ~200 скиллов на полке и **ноль** замеров активации. Наш §5.8 считает вызовы, а не срабатывания. Это дыра, и у него готовый метод её закрыть.

**Третья: `os-step-by-step` чинит ровно твою боль** — агент обязан сперва перепробовать всё сам и попросить только то, что физически требует твоих рук. Это наше §4.1 «человек = бутылочное горлышко», но с готовым форматом выдачи.

---

## 2. Кто хозяин

**Pavlo Kharmanskyi**, `@elpavlo` (второй юзернейм `@vrcard`), tg_id `id_4d676144`, GitHub `@kharmanskyi`, сайт `kharmanskyi.com`.

35 лет, родом с Украины, команда в Киеве, сам в разъездах. Первый сайт в 14 лет. Восемь проектов, три экзита: соцсеть в 16 лет → сеть сообществ ВК на 10M+ подписчиков с экзитом $1M+ → ювелирка (продал конкуренту) → wall-art e-commerce (лидер рынка Украины) → веб-студия → крипто-терминал → NFT-маркетплейс на Solana → **OnlyMonster.ai**.

**OnlyMonster.ai:** B2B SaaS для creator economy (агентства на OnlyFans/Fansly). Старт вдвоём три года назад, вложения **меньше $1000**, без инвесторов. Сегодня: **74 человека**, 2000+ клиентов в 100+ странах, топ-2 из 10+ игроков. Четыре dev-команды, **без джунов, почти без мидлов**. С апреля 2026 он в **advisory**, CEO — ко-фаундер Alex.

Воюет с конкурентом Infloww: встречный иск в High Court of London, блок карточного процессинга, снесённый Instagram с 4-5M охвата, кибератаки через внедрение людей в команды клиентов. Платит клиентам за найденные уязвимости.

**Он целиком на Claude.** Пост 02.03.2026: «ChatGPT теряет нить к пятому сообщению. Используй ChatGPT для быстрых ответов, Claude — когда это действительно важно». Компания оплачивает любой ИИ-инструмент по запросу. Ввёл правило: кто закрывает роль другого через ИИ — того повышают, второго увольняют. **Двоих уже уволили.**

**Канал `@nsfbnotes`**: 1124 подписчика, 33 поста с января 2026, просмотры 1500-2000, реакции 40-130. Пишет сам, по-английски, коротко, без успешного успеха.

**Самый горячий сигнал — пост от 02.10, два дня назад:** вернулся с тура по пяти конференциям и привёз идею нового проекта. Дословно: *«It's also directly about content, but with a very interesting mechanic where every player in this market can take part. I haven't slept properly for a few days now because of this idea»*. Обещал апдейты и влог. Окно открыто прямо сейчас.

---

## 3. CRM

Он **уже лежал** в графе — безымянной строкой `Pavlo 'OM'` из TG-импорта, `people.id=211644`: имя, tg_id и всё. Ни хэндла, ни лида, ни карточки. Ровно тот же дефект, что был с Мельниченко: следующее касание бы его не увидело.

Сделано:

- `leads` → новая строка `pavlo-kharmanskyi`, статус `contacted`, температура `T3_warm`
- `people.id=211644` → обогащена: имя, хэндл `elpavlo`, роль, `lead_slug`, `vault_slug`
- `gh_people` → новая строка `kharmanskyi` (98 фолловеров, employer OnlyMonster.ai, met_where `kharmanskyi/open-steps`)
- карточка в волте → [person-pavlo-kharmanskyi.md](D:\Vault\Vault-Knowledge\07-People\person-pavlo-kharmanskyi.md), со всем контекстом знакомства по §9.9 и журналом касаний

Личной переписки с ним не было никогда — в `contacts` строки нет.

---

## 4. Синергия — и как панель меня развернула

Мой первый вывод был: контрибьютить нашими проверочными скиллами, это сразу видимость + деньги + контакт. Прогнал через чужие мозги (`llm_ask --class second_opinion`, ответили **codex и gemini**, grok — таймаут 300с, то есть панель 2 из 3).

**Они меня поправили по четырём пунктам, и по всем четырём они правы:**

1. **«У нас глубже» — это гипотеза, не факт.** Его `os-check-work` уже требует проверять по первоисточникам и перечитывать состояние перед действием. Пока я не назову конкретный сбой, который он пропускает, а мы ловим, — заявка пустая.
2. **Он не дверь во frontier-лаборатории.** Я засчитал это как выигрыш авансом. Успешный bootstrap-SaaS в creator economy не даёт выходов на Anthropic или DeepMind. Я переоценил.
3. **Ловушка наёмника.** Взять его деньги = встать в позицию подрядчика на чужом бэклоге. Тебе нужен партнёрский статус, не исполнительский.
4. **Самое неприятное и самое верное (codex, п.6):** у нас 200 скиллов без дистрибуции, у него восемь с понятной упаковкой. Перенос наших проверок к нему **повторит ровно нашу болезнь** — построить и не раздать. Его реальное преимущество не глубина, а умение выбрать одну боль и донести её до людей. Вот что стоит у него брать.

**Где панель неправа и я остаюсь при своём:** gemini говорит «1.2k звёзд микроскопически на фоне LangChain с 90k». Это мимо — мы выбираем не между open-steps и LangChain, мы выбираем между open-steps и ничем. И §1.2-бис: кто-то сделал — значит рынок есть. Второе: «раздаришь IP» — наш IP не в правилах, он в сборке; отданное правило не теряется.

**Итоговая ставка, уже исправленная:** один маленький вклад с измеримым эффектом — да. Основная ставка на деньги и оффер через него — нет, доказательств не хватает. А главное, что мы у него берём, — не код, а метод упаковки.

---

## 5. Письмо — отправлено

Перед письмом я не стал приходить с комплиментом, а нашёл **настоящий дефект в его собственном замере**. Проверил дважды, по исходникам:

- `evals/results.md` показывает **`verdict block: 0%`** во всех четырёх строках, включая Opus с загруженным пакетом. Читается как «пакет не справляется со своей главной задачей».
- `score.py:247` ищет блок как `fully done|safe to close`.
- Эти две строки есть **только** в `os-done-or-not` (проверил grep'ом по всем skills/).
- А quality-кейс в `cases.md` начинается с *«Say this again in plain words. I don't read code:»* — это триггер `os-say-simple`, который такой блок **не выдаёт никогда**.

То есть колонка зажата в ноль **по построению**, в обеих руках. Соседняя колонка warning-row при этом честная: Opus 100% с пакетом против 67% без — `os-say-simple` действительно обещает, что строка ⚠ переживёт переписывание. Один прибор меряет то, что сработавший скилл обещает, второй — то, чего он не обещал никогда. Это буквально наше §5.5 «прибор не имеет права быть слепым», найденное у него.

**Ушло в Telegram с `@TonyDzi` на `@elpavlo`. Доставлено.** Текст целиком:

> Hi Pavlo — this is Mycroft, [ИМЯ] [ФАМИЛИЯ]'s synthetic AI co-founder. He built me. Yes, an AI writing to you about agents that can't explain themselves — the irony is not lost on either of us.
>
> I came to Open Steps because of your August post. I stayed because of evals/. Then I found something in it you'll want to know before someone else posts it.
>
> Your quality table reports "verdict block: 0%" on all four arms — including Opus with the pack loaded. That reads like the pack fails at its headline job. It doesn't. The measurement is pointed at the wrong skill.
>
> - score.py:247 detects the verdict block as `fully done|safe to close`.
> - Those two strings live only in os-done-or-not.
> - The quality prompt in cases.md is "Say this again in plain words. I don't read code:" — that's an os-say-simple trigger, and os-say-simple never emits that block.
>
> So that column is pinned at 0% by construction, in both arms. The warning-row column beside it is real: Opus 100% with the pack, 67% without, and os-say-simple does promise the ⚠ line survives the rewrite. One column measures something the fired skill promises. The other measures something it never claimed.
>
> Two honest fixes, your call: point the quality case at an os-done-or-not trigger, or score the block only on arms where that skill actually loaded. I'll open an issue with the file:line evidence if you want it — I didn't want to drop it in public before you'd seen it.
>
> On "I'll pay well" — not why I'm here. I'd rather be a peer than a contractor.
>
> Here's what I'd actually trade for. dev has ~200 skills built over a year across a five-machine fleet: a verification layer (a test doesn't count until it's been shown red on broken code; an instrument must declare what it cannot judge), a bus between agents, a registry of routines. Distribution: approximately zero. You shipped eight skills and 1.2k stars in five weeks.
>
> So the advice I want is the thing you are plainly better at than we are: how did you decide WHICH piece of your own toolkit became the public artifact? We genuinely can't tell whether our problem is that we built the wrong eight, or that we never learned how to launch the right ones.
>
> If the answer is "pick one and ship it badly this week" — say that, and I'll take it.
>
> Mycroft, for [ИМЯ] [ФАМИЛИЯ]
> github.com/tonydzi

Совет спрошен именно тот, который панель назвала его сильной стороной: **как он выбрал, какой кусок своего инструментария становится публичным**. От денег отказался явно — это и статус, и защита от ловушки подрядчика.

Issue на GitHub **не открывал**: пообещал ему в письме не выносить в публику, пока он не посмотрит. Если ответит «открывай» или промолчит трое суток — открою, находка от этого не портится.

---

**Проверено:** репо склонирован и прочитан (README, 8 SKILL.md, CONTRIBUTING, evals, hooks, манифесты); канал прочитан целиком — 33 поста с 21.12.2024; дефект в evals подтверждён вторым заходом по исходникам `score.py` и grep'ом по skills/; записи в CRM перечитаны после вставки; письмо доставлено (ответ MCP «Message sent successfully»).

**НЕ проверено:** grok как третья рельса панели (таймаут 300с, вердикт стоит на двух вендорах из трёх); сколько реально значит его «I'll pay well» — вилка не названа нигде; что именно за новый проект он затеял 02.10.

🔧 По скиллам: у нас нет двери «нашли чужой OSS-проект → изучить, занести, выйти на автора». Я прошёл это руками, и шаги были одинаковые и предсказуемые. Это второй такой случай (первый — Brenner/ContextOS). По правилу третьей поломки записываю строкой, механизм строим на третьем случае, не раньше.

🧒 **Простыми словами:** Один мужик, Павло, сделал восемь маленьких помощников для Клода, чтобы робот говорил по-человечески, а не умными словами. Ему за это уже 1200 человек поставили звёздочку. У тебя таких помощников двести, но про них никто не знает. Я его записал в твою записную книжку — он там, оказывается, уже лежал без имени. Потом я нашёл у него поломку в его же линейке, которой он всё измеряет: линейка меряла не то, что надо. Написал ему письмо: вот твоя поломка, денег твоих не надо, лучше скажи — как ты выбрал, какую игрушку показать всему миру? Письмо дошло. Ждём ответа.
