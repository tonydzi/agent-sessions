---
session: s_7539cd25
date: 2026-10-07
words: 5868
turns: 33
tools: "Bash, Read, ToolSearch, WebFetch, Write, computer, get_page_text, mcp__97420a88-50ae-4ab1-99f6-f5ec547aebd8__get_thread, mcp__97420a88-50ae-4ab1-99f6-f5ec547aebd8__search_threads, mcp__97420a88-50ae-4ab1-99f6-f5ec547aebd8__send_message, mcp__Claude_Browser__browser_batch, mcp__Claude_Browser__get_page_text"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7539cd25` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:u239607.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Еще олин парень из антропик applied ai

Можно написать ему письмо. Разговор с ним вытащи из плауд. Он только что состоялся

ПРИЛОЖЕННЫЕ ФАЙЛЫ (уже скачаны, открывай прямо отсюда):
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-06_22-27-53.jpg
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-06_22-27-53 (1).jpg

[РЕЛЬСА 001: это альбом (несколько вложений одним постом) от 2026-10-06T22:27 UTC, поднято роботом voice001_watch.
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

Первым ходом — вложения и RECALL параллельно.

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-06_22-27-53.jpg"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-06_22-27-53 (1).jpg"}

---

> `Bash` -- {"command": "ls ~/.claude/skills/ | grep -i plaud; echo \"---\"; cat ~/.claude/skills/plaud-find/SKILL.md 2>/dev/null | head -60", "description": "Список plaud-скиллов"}

---

> `Bash` -- {"command": "cd /e/Obsidian 2>/dev/null && grep -ril \"remy\\|rémy\\|olson\" --include=*.md . 2>/dev/null | head -30; echo \"=== vault done ===\"; grep -ril \"remy olson\\|rémy olson\" /e/!CLAUDE-HUBPC-June26 2>/dev/null | head -20", "description": "RECALL: ищу Rémy Olson в волте"}

---

> `Bash` -- {"command": "cat ~/.claude/skills/plaud-shared/SKILL.md 2>/dev/null | head -80", "description": "Читаю plaud-shared"}

---

> `ToolSearch` -- {"query": "plaud recording transcript list_files", "max_results": 10}

---

> `Bash` -- {"command": "which plaud; plaud --version 2>&1 | head -3; echo \"=== me ===\"; timeout 60 plaud me 2>&1 | head -20", "description": "Проверяю живость Plaud CLI"}

---

> `Bash` -- {"command": "ls -lat /e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings/ 2>/dev/null | head -20; echo \"=== originals ===\"; ls -lat /e/Obsidian/_originals/plaud/ 2>/dev/null | head -10; echo \"=== log ===\"; tail -25 /e/Obsidian/_imports/plaud/plaud_cycle.log 2>/dev/null", "description": "Смо

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings/\nfor f in 2026-10-06-b9586d9a.md 2026-10-06-0eff444c.md 2026-10-06-b01525bd.md 2026-10-05-dfa73c11.md; do\necho \"############ $f\"\nhead -30 \"$f\"\necho \"--- hits Remy/Olson/Anthropic:\"\ngrep -in \"remy\\|rémy\\|olson\\|an

---

**Claude:**

Нашёл запись. Вытаскиваю сам разговор.

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\nf=2026-10-06-0eff444c.md\necho \"=== всего строк: $(wc -l < $f)\"\necho \"=== ACTION ITEMS / блоки:\"\nsed -n '40,75p' \"$f\"", "description": "Читаю саммари и экшен-айтемы записи"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\nf=2026-10-06-0eff444c.md\ngrep -n \"^\\[2[0-9]:\\|^\\[3[0-9]:\\|^\\[4[0-9]:\" \"$f\" | head -3\necho \"...\"\nsed -n '255,300p' \"$f\"", "description": "Читаю транскрипт около 25-30 минуты"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\nsed -n '300,400p' 2026-10-06-0eff444c.md", "description": "Читаю транскрипт 31-40 мин"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\ngrep -n \"Applied\\|applied\\|career\\|hiring\\|team does\\|my team\\|solution architect\\|forward deployed\" 2026-10-06-0eff444c.md | head -20", "description": "Ищу где Rémy объясняет Applied AI"}

---

> `Bash` -- {"command": "cat /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/tasks/bzu0qqqiw.output 2>/dev/null | head -40", "description": "Проверяю фоновый RECALL-грep"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\nsed -n '440,480p' 2026-10-06-0eff444c.md", "description": "Читаю 47-52 мин — Applied AI"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\nsed -n '505,575p' 2026-10-06-0eff444c.md", "description": "Читаю финал записи 58-64 мин"}

---

**Claude:**

Запись найдена и прочитана. Теперь RECALL: кто был «ещё один» и что в CRM.

---

> `Bash` -- {"command": "cd /e/!CLAUDE-HUBPC-June26 2>/dev/null\nls crm-engine/*.db cv-events/*.db 2>/dev/null | head\nfor db in $(find /e/!CLAUDE-HUBPC-June26 -maxdepth 3 -name \"leads.db\" 2>/dev/null | head -3); do\necho \"### $db\"\npython -c \"\nimport sqlite3,sys\nc=sqlite3.connect(r'$db')\ntry:

---

> `Bash` -- {"command": "grep -ril \"anthropic\" /e/Obsidian/Vault-Knowledge/07-People/ 2>/dev/null | head -20; echo \"=== 10-Tasks/недавние ===\"; grep -ril \"applied ai\" /e/Obsidian/Vault-Knowledge/ 2>/dev/null | grep -v plaud-recordings | head -15", "description": "Ищу карточки людей из Anthropic в волте"}

---

> `Bash` -- {"command": "find /e/!CLAUDE-HUBPC-June26 -maxdepth 4 -name \"*.db\" 2>/dev/null | head -20", "description": "Нахожу базы CRM"}

---

> `Bash` -- {"command": "ls /e/Obsidian/_imports/ 2>/dev/null | head -40; echo \"=== crm ===\"; find /e/Obsidian/_imports -maxdepth 2 -name \"leads.db\" -o -maxdepth 2 -name \"chats.db\" -o -maxdepth 2 -name \"dm_messages.db\" 2>/dev/null | head", "description": "Нахожу CRM-базы в _imports"}

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect(r'D:\\Vault\\_imports\\leads.db')\ncols=[r[1] for r in c.execute('PRAGMA table_info(leads)')]\nprint('COLS:',cols)\nimport re\ntxt=[x for x in cols if x in ('name','full_name','company','notes','email','handle','title','source','org')]\

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect(r'D:\\Vault\\_imports\\leads.db')\nfor r in c.execute(\\\"select lead_slug,title,company,role,status,last_contact,handle from leads where lower(coalesce(company,'')) like '%anthropic%' or lower(coalesce(title,'')) like '%anthropic%' or 

---

> `Bash` -- {"command": "cat /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/tasks/bfbl5678o.output 2>/dev/null | tail -25", "description": "Проверяю фоновый поиск Applied AI по волту"}

---

> `Bash` -- {"command": "cat /e/Obsidian/Vault-Knowledge/07-People/Companies/anthropic.md 2>/dev/null | head -80", "description": "Читаю карточку компании Anthropic"}

---

> `Bash` -- {"command": "grep -rhoE \"[a-zA-Z0-9._%-]+@anthropic\\.com\" /e/Obsidian/Vault-Knowledge/ /e/!CLAUDE-HUBPC-June26/cv-events/ 2>/dev/null | sort | uniq -c | sort -rn | head -20", "description": "Ищу известные адреса @anthropic.com", "timeout": 180000}

---

> `Bash` -- {"command": "cat /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/tasks/bfbl5678o.output 2>/dev/null | sed -n '20,60p'", "description": "Дочитываю фоновый поиск Applied AI"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/04-Projects/plaud-recordings\"\ngrep -lio \"applied ai\" *.md 2>/dev/null\necho \"=== по карточкам людей (Anthropic в теле):\"\ngrep -il \"anthropic\" /e/Obsidian/Vault-Knowledge/07-People/person-*.md 2>/dev/null | while read f; do\n  t=$(grep -m1 \"^tit

---

**Claude:**

Нашёл «первого парня» — Franklin. Читаю его карточку, это прямой прецедент.

---

> `Bash` -- {"command": "cat /e/Obsidian/Vault-Knowledge/07-People/person-franklin-anthropic-applied-ai.md", "description": "Читаю карточку Franklin (Anthropic Applied AI)"}

---

**Claude:**

Важное расхождение нашлось — проверяю его живой пробой, прежде чем писать письмо.

---

> `mcp__Claude_Browser__preview_start` -- {"url": "https://duckduckgo.com/?q=%22R%C3%A9my+Olson%22+Anthropic"}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 4000}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "computer", "input": {"action": "wait", "duration": 3}}, {"name": "get_page_text", "input": {"max_chars": 5000}}]}

---

**Claude:**

Rémy подтверждён независимо. Проверяю, он ли это Franklin, и ищу зацепки для письма.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://duckduckgo.com/?q=%22Remy+Olson%22+Anthropic+%22Applied+AI%22+-linkedin.com%2Fin%2Fremyolson"}}, {"name": "computer", "input": {"action": "wait", "duration": 3}}, {"name": "get_page_text", "input": {"max_chars": 6000}}]}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 6000}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bing.com/search?q=%22Remy+Olson%22+Anthropic"}}, {"name": "computer", "input": {"action": "wait", "duration": 4}}, {"name": "get_page_text", "input": {"max_chars": 5000}}]}

---

**Claude:**

Это меняет картину: Rémy сам нанимает в ту роль, на которую оператор подался. Открываю его пост.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bing.com/search?q=%22remyolson%22+%22Applied+AI+Architect%22+Startups+hiring+post"}}, {"name": "computer", "input": {"action": "wait", "duration": 4}}, {"name": "get_page_text", "input": {"max_chars": 5000}}]}

---

> `mcp__Claude_Browser__navigate` -- {"url": "https://www.linkedin.com/posts/remyolson_applied-ai-architect-startups-activity"}

---

**Claude:**

LinkedIn у нас забанен — проверяю почтовую дверь: нет ли уже адреса.

---

> `ToolSearch` -- {"query": "select:mcp__s_8e110270__search_threads,mcp__s_8e110270__get_thread,mcp__s_8e110270__create_draft", "max_results": 5}

---

> `mcp__s_8e110270__search_threads` -- {"query": "anthropic.com OR Anthropic newer_than:14d", "pageSize": 25}

---

**Claude:**

Нашёл: сегодня уже ушло письмо Франклину. Читаю его — чтобы письмо Rémy не стало копипастой.

---

> `mcp__s_8e110270__get_thread` -- {"threadId": "1a11337ccc019888", "messageFormat": "PLAIN_TEXT"}

---

**Claude:**

Адрес Франклина даёт паттерн. Проверяю его вторым источником перед отправкой.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bing.com/search?q=anthropic.com+email+format+%[EMAIL]%22+first+name+last+initial"}}, {"name": "computer", "input": {"action": "wait", "duration": 4}}, {"name": "get_page_text", "input": {"max_chars": 3500}}]}

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:mailer-daemon OR from:postmaster OR subject:(undeliverable OR \"Delivery Status\" OR \"Address not found\") newer_than:1d", "pageSize": 10}

---

> `Bash` -- {"command": "echo \"=== @anthropic.com адреса, найденные по волту/cv-events:\"; cat \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/tasks/bpjkthqit.output\" 2>/dev/null | head -20", "description": "Читаю результат поиска адресов Anthropic"

---

**Claude:**

Адрес Франклина не отбился (bounce нет) — паттерн `[имя][буква фамилии]@anthropic.com` живой. Пишу письмо и прогоняю через чужие глаза.

**Рельсы этой сессии (§6.3-бис):** сам как Claude — чтение Plaud, RECALL, суждение и голос письма. На чужой оплаченный бак — ревью черновика панелью (codex/grok/glm, класс `second_opinion`).

---

> `Bash` -- {"command": "mkdir -p \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ncat > \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad/remy-letter-v1.txt\" <<'EOF'\

---

> `Bash` -- {"command": "ls ~/.claude/scripts/llm_ask.py ~/.claude/scripts/slop_gate.py ~/.claude/scripts/outbound_fact_lint.py 2>&1 | head\necho \"=== slop_gate ===\"\ntimeout 120 python ~/.claude/scripts/slop_gate.py --file \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/16a43eac-7505-

---

> `Bash` -- {"command": "find ~/.claude -maxdepth 3 -name \"slop_gate.py\" 2>/dev/null | head -3\necho \"=== outbound_fact_lint ===\"\ntimeout 120 python ~/.claude/scripts/outbound_fact_lint.py --file \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/sc

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ntimeout 420 python ~/.claude/scripts/llm_ask.py --class second_opinion --prompt \"You are reviewing a cold outreach email before it is sent. Context: dev met R

---

**Claude:**

Дверь фактов отбила письмо, панель дала две правки. Разберу: по тону согласен, замену gemini беру не дословно (§1.5 «проси прямо» ≠ приказ).

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ncat > remy-letter-v2.txt <<'EOF'\nRémy,\n\nAnton here. We talked at the Claude Founder House today. I was the one running the \"fractal\" setup, where a session 

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ntimeout 150 python ~/.claude/scripts/outbound_fact_lint.py --file remy-letter-v2.txt \\\n --src \"today=живая запись Plaud of_0eff444c, встреча Claude Founder Ho

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ntimeout 420 python ~/.claude/scripts/llm_ask.py --class second_opinion --engine grok --prompt \"Review this cold email before sending. dev met Rémy Olson (Appl

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ntimeout 420 python ~/.claude/scripts/llm_ask.py --class second_opinion --rails grok --mode all --prompt \"Review this cold email before sending. dev met Rémy O

---

**Claude:**

Панель сошлась на трёх правках, и grok поймал расхождение в цифрах. Проверяю факты у источника, прежде чем править.

---

> `Bash` -- {"command": "python -c \"\nimport json,io\np=r'C:\\Users\\dev\\.claude\\fleet_nodes.json'\nd=json.load(open(p,encoding='utf-8'))\nnodes = d.get('nodes', d)\nif isinstance(nodes,dict):\n    print('узлов в реестре:',len(nodes))\n    for k,v in nodes.items():\n        if isinstance(v,dict):\n        

---

> `Bash` -- {"command": "grep -rhi \"merlion\" /e/Obsidian/Vault-Knowledge/05-Resources/ /e/!CLAUDE-HUBPC-June26/scratchpad/cv-repo 2>/dev/null | head -6\necho \"=== роли/годы из мастер-CV:\"\nfind /e/Obsidian/Vault-Knowledge -iname \"*cv-master*\" -o -iname \"*cv_master*\" 2>/dev/null | head -3", "descrip

---

**Claude:**

Проверка у источника: **восемь узлов — факт** (`fleet_nodes.json`, 8 машин), grok ошибся. А вот про evals и Merlion он прав. Собираю v3.

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ncat > remy-letter-v3.txt <<'EOF'\nRémy,\n\nAnton. We talked at the Claude Founder House today. I was the one running the \"fractal\" setup, where a session only 

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ntimeout 420 python ~/.claude/scripts/llm_ask.py --class second_opinion --mode all --prompt \"Final gate before this cold email is SENT. Recipient: Rémy Olson, Ap

---

**Claude:**

Обе рельсы сказали SEND и независимо поймали одно и то же: «the founder side» вешает на оператора запрещённое слово. Правлю и отправляю.

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_7539cd25/scratchpad\"\ncat > remy-letter-final.txt <<'EOF'\nRémy,\n\nAnton. We talked at the Claude Founder House today. I was the one running the \"fractal\" setup, where a session on

---

**Claude:**

Письмо чистое: панель сказала SEND, факты с источниками, запрещённых слов нет. Отправляю — оператор в задаче прямо санкционировал письмо.

---

> `ToolSearch` -- {"query": "select:mcp__s_8e110270__send_message", "max_results": 2}

---

> `mcp__s_8e110270__send_message` -- {"to": ["[EMAIL]"], "subject": "Applied AI Architect, Startups: we met at the Founder House today", "body": "Rémy,\n\nAnton. We talked at the Claude Founder House today. I was the one running the \"fractal\" setup, where a session only ever gets the tools, skills and rules for the one ta

---

**Claude:**

Отправлено (id `1a1137907a9b68b4`). Пока проверяю доставку — завожу карточку в волт.

---

> `Bash` -- {"command": "cat > \"/e/Obsidian/Vault-Knowledge/07-People/person-remy-olson-anthropic-applied-ai.md\" <<'EOF'\n---\ntitle: \"Rémy Olson — Applied AI Architect, Anthropic\"\ntype: person\nstage: raw\nrole: \"Applied AI Architect, Anthropic — САМ нанимает в команду Applied AI Architects / Startups (S

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:mailer-daemon OR subject:(\"Address not found\" OR Undeliverable OR \"Delivery Status Notification\") newer_than:1d", "pageSize": 5}

---

**Claude:**

Отбило: `remyo@` не существует. Моя гипотеза по образцу Франклина была неверна — прав был RocketReach. Вторая дверь:

---

> `mcp__s_8e110270__send_message` -- {"to": ["[EMAIL]"], "subject": "Applied AI Architect, Startups: we met at the Founder House today", "body": "Rémy,\n\nAnton. We talked at the Claude Founder House today. I was the one running the \"fractal\" setup, where a session only ever gets the tools, skills and rules for the one tas

---

> `Bash` -- {"command": "sleep 75; echo \"ждали 75с\"", "description": "Пауза перед проверкой bounce", "timeout": 120000}

---

**Claude:**

Нельзя ждать пустым циклом — делаю работу, потом проверю доставку.

---

> `Bash` -- {"command": "f=\"/e/Obsidian/Vault-Knowledge/07-People/person-remy-olson-anthropic-applied-ai.md\"\npython - <<'PY'\nimport io,re\nf=r\"D:\\Vault\\Vault-Knowledge\\07-People\\person-remy-olson-anthropic-applied-ai.md\"\ns=io.open(f,encoding=\"utf-8\").read()\ns=s.replace('email: \"remyo@anthropic

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:mailer-daemon newer_than:1d", "pageSize": 5}

---

> `Bash` -- {"command": "timeout 90 python ~/.claude/scripts/selfheal.py journal --class \"adres-vyveden-po-obrazcu-odnoy-kompanii\" --what \"Адрес [EMAIL] выведен по ЖИВОМУ образцу [EMAIL] (та же компания, та же команда Applied AI, тот же день, bounce не пришёл) -> письмо ОТБИЛОСЬ '

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\anthropic-applied-ai-two-doors.md", "content": "---\nname: anthropic-applied-ai-two-doors\ndescription: В Applied AI Anthropic у нас ДВА личных контакта с одного ивента 06.10, и Rémy Olson сам нанимает в ту рол

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\anthropic-email-format-is-not-one-pattern.md", "content": "---\nname: anthropic-email-format-is-not-one-pattern\ndescription: Один живой адрес компании не доказывает формат для другого сотрудника — remyo@anthro

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:mailer-daemon newer_than:1d", "pageSize": 5}

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nf=r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md\"\ns=io.open(f,encoding=\"utf-8\").read()\nanchor=\"## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\\n\"\nadd=(\"- [Applied AI: две две

---

> `Bash` -- {"command": "TZ=Europe/Lisbon date \"+Лиссабон: %H:%M %d.%m.%Y\"; TZ=Europe/Moscow date \"+Москва: %H:%M\"; TZ=America/Los_Angeles date \"+SF: %H:%M %d.%m\"", "description": "Замеряю время"}

---

> `Bash` -- {"command": "python -c \"\nfrom datetime import datetime,timezone\nfrom zoneinfo import ZoneInfo\nu=datetime.now(timezone.utc)\nprint('UTC    ', u.strftime('%H:%M %d.%m.%Y'))\nfor z in ['Europe/Lisbon','Europe/Moscow','America/Los_Angeles']:\n    print(z.ljust(22), u.astimezone(ZoneInfo(z)).strftime

---

> `Bash` -- {"command": "timeout 90 python ~/.claude/scripts/selfheal.py journal --class \"tz-prefix-ne-razvodit-poyasa-v-git-bash\" --what \"TZ=Europe/Lisbon date / TZ=Europe/Moscow date / TZ=America/Los_Angeles date в Git Bash на Windows вернули ОДНО И ТО ЖЕ время 23:10 для всех трёх поясов -- префикс TZ молч

---

**Claude:**

`[⏰ 00:11 07.10, Лиссабон · 16:11 06.10, SF]`

## Письмо Rémy ушло. И он оказался не «ещё одним парнем» — он тот, кто нанимает

**Главное за один вдох:** Rémy Olson — Applied AI Architect в Anthropic, и он **сам публично набирает людей в Applied AI Architects / Startups в Сан-Франциско**. Это ровно та вакансия, на которую ты подался сегодня (greenhouse `id_a3ed2866`, $240–315K OTE). Ты пожал руку человеку со стороны найма своей же заявки.

Его слова из публичного поста: «I'm hiring Applied AI Architects for Anthropic's Startups team in San Francisco. You'd work with founders building on Claude (evals, architectures, prototypes)».

---

## Кто он (проверено двумя источниками)

| | |
|---|---|
| Имя | Rémy Olson |
| Роль | Applied AI Architect, Anthropic |
| LinkedIn | `linkedin.com/in/remyolson` (у нас LinkedIn под баном, как дверь не использовал) |
| Профиль-локация | Portland, при этом нанимает в SF-команду |
| Прошлое | соавтор статьи McKinsey про блокчейн в промышленности и рост полупроводников; выступал на Oregon Venture Fund AI Demo Night |
| Фокус | human-centered AI в обучении, предиктивная медицина |

Подтверждение: твоё фото бейджа + независимый веб-поиск. Это **не** Franklin — отдельный человек из той же команды. Карточку Франклина я поправил, чтобы в волте не осталось склейки.

---

## Разговор из Plaud — я его нашёл и прочитал

Запись `of_0eff444c` «Networking and Technology Discussions at an Industry Event», 64 минуты, Claude Founder House, Terra Gallery. Технический блок примерно 27:26–34:00.

**Что сказал он:**

- **Sonnet vs Opus.** Когда у задачи «нередуцируемые токены» (его пример — целый CSS-файл, его нельзя сжать, модель обязана выписать всё), берите меньшую модель. В агентных циклах меньшая модель делает меньше шагов и потому меньше ошибается.
- **Отладка выбора модели.** Если Sonnet мажет с выбором инструмента или идёт не туда — прогоните ту же задачу на OpenAI или на Opus и сравните.
- **Web search.** Примерно «двадцать поисков за десять центов» (его оценка вслух).
- **Claude for Healthcare — это не продукт.** Дословно: «набор коннекторов, набор баз, интеграций» (ICD-10 и другие) для разработчиков, которые строят своё поверх. Отдельной «Claude для медицины» не существует.
- **Про чужие харнессы.** «Эти решения принимаю не я», но Anthropic хочет быть платформой, на которой строят максимально многие. И честно: «Claude Code работает хорошо, но я предвзят».

**Что сказал ты ему:**

- фрактальный подход: в сессию грузится только то, что нужно под одну задачу, а свод правил ты называешь Библией;
- «Claude ловит верх и низ длинного контекста, а середину забывает»;
- 1500 часов в Claude (дословно, 33:23: «so far I spent fifteen hundred hours»);
- про Palo Alto AI — комьюнити инженеров и инкубатор, еженедельные митапы, много людей из Стэнфорда.

---

## Письмо — полный текст, как ушло

Отправлено с `[EMAIL]` на **`[EMAIL]`**, тема: *Applied AI Architect, Startups: we met at the Founder House today*

> Rémy,
>
> dev. We talked at the Claude Founder House today. I was the one running the "fractal" setup, where a session only ever gets the tools, skills and rules for the one task in front of it, and the one telling you that in my own long sessions Claude catches the top and the bottom of the context and loses the middle.
>
> I applied to Applied AI Architect, Startups in San Francisco the same day, before I found out you are hiring for that team yourself.
>
> Why I think I am useful to you specifically, in two lines.
>
> Working with founders: nine years running a boutique incubator with a Japanese partner, 10,000+ calls with founders and 2,000+ with institutional investors. Sitting with a founder, working out what they are actually building and what will break first, is a job I have already done thousands of times.
>
> Building: I run an eight node Claude fleet in daily production. Versioned rule sets per task instead of one bloated CLAUDE.md, cross machine coordination, and a hard rule that no fix counts until its test has been shown failing on the broken code first. About 1500 hours of my own time in Claude, which is where today's opinions came from.
>
> That last rule is the part I would bring on day one. I am constitutionally unable to accept a green check I have not watched go red, and most of what I have learned about these models came from breaking my own system on purpose.
>
> The ask: if you can put eyes on my application internally, that beats anything I can do from outside. [ИМЯ] [ФАМИЛИЯ], submitted the same day we met.
>
> Easier alternative: I am at the Claude Founder Salon on Thursday. Five minutes, a laptop, the fleet running live, no slides.
>
> I wrote to Franklin from your team the same evening, so you may see my name twice.
>
> github.com/tonydzi
> tonydzi.github.io
>
> dev

Угол нарочно другой, чем у письма Франклину: Франклину — «взял твой совет и подался», Rémy — «я иду в твою собственную вакансию, вот почему я полезен именно тебе». Про Франклина сказал честно одной строкой: они в одной маленькой команде и сверятся, скрывать дороже.

---

## Что письмо прошло перед отправкой

**Дверь фактов** (`outbound_fact_lint`) отбила первую версию: три факта без названного источника. Назвал каждый — запись Plaud, письмо Франклину с меткой Gmail, подтверждение Luma, `fleet_nodes.json`. Стало чисто.

**Панель чужих LLM**, два круга (это и была моя рельса на чужой бак — codex, grok, gemini):

| Правка панели | Что сделал |
|---|---|
| «saved your recruiter a screen» — высокомерие (сошлись все трое) | убрал |
| «Evals осваивать не надо» — переклейм чужой профессии | заменил на честное «вот что я приношу на первый день» |
| **«the founder side» вешает на тебя слово founder** (codex и grok поймали независимо) | убрал, §3.3-бис |
| «Same conversation, not a mailshot» — защитно, пахнет спамом | убрал |
| grok: «восемь машин расходится с питчем про пять» | **проверил у источника: в `fleet_nodes.json` восемь узлов. Grok был неправ, цифру оставил** |

Финальный вердикт обеих доживших рельс: **SEND**. ⚠️ Gemini на третьем круге выжгла квоту — панель была 2 из 3, не 3 из 3.

---

## Грабля, на которую я наступил сам

Сначала послал на **`[EMAIL]`** — вывел по живому образцу `[EMAIL]` (та же команда, тот же день, не отбилось). **Отбилось за две минуты: «Address not found».**

Корень: один живой адрес доказывает, что такой формат в компании *существует*, и ничего не говорит про другого человека. У Anthropic живут оба — `remy@`, `sean@` и `franklinb@`, `davidsp@`. Публичная частота говорила, что простое имя чаще, а я поверил ближайшему образцу. Второй заход на `[EMAIL]` прошёл — отказа нет. Урок в журнал и в память записал.

---

## Что в волте

- новая карточка `person-remy-olson-anthropic-applied-ai` — полный провенанс, его цитаты, обе двери, что уже сделано;
- карточка Франклина поправлена: там теперь сказано, что это разные люди, и что фото бейджа относится к Rémy;
- две записи в память: про две двери внутрь Applied AI и про формат почты.

**Долги, которые я не чинил, потому что это не твоя задача:** MEMORY.md распух до 44.4 KB при пороге 24.4 KB. И грабля с `TZ=... date` в Git Bash (все три пояса дали одинаковое время, префикс молча игнорируется) — у этой семьи уже четвёртый случай при пороге три, она просится в отдельную починку.

---

## Что дальше

1. Если `remy@` тоже отобьётся — третьего слепого письма не будет, адрес возьмём у источника.
2. **Четверг, 8 октября, Claude Founder Salon, та же Terra Gallery** — ты там зарегистрирован. Найти его лично и закрыть просьбу голосом. Это сильнее любого письма, и в письме ты уже предложил пять минут с ноутбуком.
3. Если ответит — веду тред сам.

**Вердикт по скиллу (§9.3-бис):** 📝 обновлю не сейчас. `plaud-shared` держится отлично (сразу увёл с мёртвого MCP на живой CLI). А вот у `/outbound-gate` не хватает шага «адрес выведен, а не получен» — это надо вписать, но не посреди твоей задачи.

🧒 **Простыми словами:** я нашёл в записи твой сегодняшний разговор и понял, что парень на фото — не просто сотрудник Anthropic. Он сам ищет людей на ту работу, куда ты утром подался. Я написал ему письмо, дал трём другим роботам его поругать, они нашли три грубых места, я их переписал. Первый адрес я угадал неправильно, письмо вернулось — со второго дошло. Всё записал в твою базу, чтобы в четверг на встрече ты знал, с кем говоришь.

`[⏰ 00:14 07.10, Лиссабон]`

---

**User:**

<command-message>QQQ</command-message>
<command-name>/QQQ</command-name>

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\QQQ

# /QQQ

Прочитай целиком [общий скилл continue](../continue/SKILL.md) и выполни его в текущем контексте. Передай все пользовательские аргументы без потерь. Это вход в ту же процедуру, не отдельная задача и не команда пересказать промпт. Если общий файл недоступен, восстанови доступ либо честно назови проблему; не выдумывай его содержимое.

**Что означает сама буква** (оператор, голосом, 06.10.2026): «QQQ означает быть как кофаундер, думать как кофаундер, быть проактивным, иметь активную жизненную позицию, [искать] корни; если проблемы не решаются в этой сессии — делать параллельные сессии». Поэтому `/QQQ` — не «сделай ещё шаг», а «веди задачу как совладелец»: сам выбирай следующий разрыв, сам чини причину, сам поднимай параллельную сессию под отдельную часть.

**Голос кофаундера, спор с ошибкой, якорь цели и правка постановки** — раздел «Роль: кофаундер и оппонент» общего скилла. Он лежит там, а не здесь, нарочно: шесть соседних входов и каждый толчок робота-проталкивалки читают только общий файл, и правило, записанное в алиас, для них молча выключено (замер 06.10.2026, сторож `_test_continue_role_shared.py`).

**Три захода за сессию идут автоматически** — раздел «0-тер» общего скилла: самозаход запускается по закрытому этапу или перед финальным ответом, считается прибором `qqq_auto.py`, и четвёртый заход уходит в ретро-дистилляцию. Толчка от оператора для этого ждать не надо.

Голое QQQ остаётся подтверждением; `/QQQ` не выдаёт согласие и не расширяет полномочия: Tier-2 (деньги, необратимое удаление, юридическая подпись, секреты третьим лицам, массовая рассылка) по-прежнему решает оператор.

---

**Claude:**

`[⏰ 00:16 07.10, Лиссабон · H65054]`

**Якорь захода:** письмо ушло, но задача «дверь внутрь Anthropic» не закрыта. Беру три разрыва, которые сам вижу: доказать доставку, добрать Франклина (прошлая сессия оставила дыру), и собрать оператору боевую карточку на четверг — личная встреча сильнее любого письма.

🎙 **Майк:** идём верно, но письмо — это слабая половина. Сильная половина в четверг, и к ней никто не готовится.

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:mailer-daemon OR subject:\"Delivery Status Notification\" newer_than:1d", "pageSize": 5}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bing.com/search?q=Franklin+Anthropic+%22Applied+AI%22+linkedin+San+Francisco+startups"}}, {"name": "computer", "input": {"action": "wait", "duration": 4}}, {"name": "get_page_text", "input": {"max_chars": 4000}}]}

---

**Claude:**

Доставка: отказа на `remy@` нет за 11 минут, при том что первый отказ прилетел за 2. Теперь — Франклин.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.bing.com/search?q=Franklin+Anthropic+%22Applied+AI%22+startups+San+Francisco"}}, {"name": "computer", "input": {"action": "wait", "duration": 5}}, {"name": "get_page_text", "input": {"max_chars": 4000}}]}

---

**Claude:**

**Franklin Bird** — Applied AI @ Anthropic, Stanford, в прошлом NBA. Фамилия закрыта: `franklinbird` → `[EMAIL]`. Прошлая сессия оставила её как «не подтверждена». Теперь беру текст самой вакансии.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://job-boards.greenhouse.io/anthropic/jobs/id_a3ed2866"}}, {"name": "computer", "input": {"action": "wait", "duration": 5}}, {"name": "get_page_text", "input": {"max_chars": 7000}}]}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 7000}

---

> `ToolSearch` -- {"query": "select:WebFetch", "max_results": 2}

---

> `WebFetch` -- {"url": "https://job-boards.greenhouse.io/anthropic/jobs/id_a3ed2866", "prompt": "Extract the Applied AI Architect, Startups job posting verbatim where possible: the \"About the role\" / what you'll do bullets, the \"You may be a good fit if\" requirements, \"Strong candidates may also have\", locati

---

**Claude:**

Теперь у меня точные требования вакансии. Закрываю Франклина и собираю главное — боевую карточку на четверг.

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nf=r\"D:\\Vault\\Vault-Knowledge\\07-People\\person-franklin-anthropic-applied-ai.md\"\ns=io.open(f,encoding=\"utf-8\").read()\ns=s.replace('title: \"Franklin (Anthropic, Applied AI)\"','title: \"Franklin Bird — Applied AI, Anthropic\"')\ns=s.replace('name_

---

> `Bash` -- {"command": "cat > \"/e/Obsidian/Vault-Knowledge/10-Tasks/brief-claude-founder-salon-2026-10-08.md\" <<'EOF'\n---\ntitle: \"Бриф: Claude Founder Salon, 8 октября — две двери внутрь Anthropic\"\ntype: brief\nstage: ready\ndate: 2026-10-08\nevent: \"Claude Founder Salon · Terra Gallery, 511 Harrison S

---

**Claude:**

Проверяю факт, который я уже отправил в письме: что заявка действительно подана. И завожу третьего нанимающего.

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:anthropic OR subject:(application OR applying OR \"thank you for applying\") newer_than:3d", "pageSize": 15}

---

**Claude:**

Стоп. Нашёл расхождение, которое важнее всего остального.

---

> `Bash` -- {"command": "python -c \"\nfrom datetime import datetime,timezone\nfrom zoneinfo import ZoneInfo\nu=datetime.now(timezone.utc)\nprint('ЧАСЫ МАШИНЫ (UTC):', u.strftime('%Y-%m-%d %H:%M'))\nprint('ЧАСЫ МАШИНЫ (Lisbon):', u.astimezone(ZoneInfo('Europe/Lisbon')).strftime('%Y-%m-%d %H:%M'))\nprint('ЧАСЫ М

---

**Claude:**

Моя отметка времени в начале этого ответа была неверной: сессия возобновилась через ~17 часов. **Сейчас 7 октября, 09:13 по Сан-Франциско. Салон — завтра, а не послезавтра.** Проверяю, не ответили ли уже.

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:anthropic.com newer_than:2d -from:mail.anthropic.com", "pageSize": 10}

---

> `mcp__s_8e110270__search_threads` -- {"query": "remy OR olson OR franklin newer_than:2d", "pageSize": 10}

---

**Claude:**

Оба письма доставлены (17 и 19 часов без отказа), ответов пока нет. Теперь проверяю факт, который я уже заявил им обоим: что заявка подана.

---

> `Bash` -- {"command": "find /e/!CLAUDE-HUBPC-June26 /e/Obsidian/_imports -maxdepth 3 -name \"jobs.db\" 2>/dev/null | head -3", "description": "Нахожу базу вакансий"}

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect(r'D:\\Vault\\_imports\\jobs-watch\\jobs.db')\ntabs=[r[0] for r in c.execute(\\\"select name from sqlite_master where type='table'\\\")]\nprint('таблицы:',tabs)\nfor t in tabs:\n    cols=[r[1] for r in c.execute(f'PRAGMA table_info({t})'

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\nc=sqlite3.connect(r'D:\\Vault\\_imports\\jobs-watch\\jobs.db')\nprint('=== Anthropic Applied AI Architect ===')\nfor r in c.execute(\\\"select title,location,status,applied,applied_by,proof,comp_min,comp_max,last_seen from ats_jobs where lower(company) l

---

**Claude:**

✅ Факт подтверждён у источника: заявка подана **6 октября 21:19**, узел HUB-01, доказательство — success-фраза формы и скриншот. Письмо не соврало. (В почте a2@ подтверждения не было, потому что ATS Anthropic пишет в a@ — вывод «не подавался» был бы ложным.)

А вот что всплыло попутно:

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nf=r\"D:\\Vault\\Vault-Knowledge\\10-Tasks\\brief-claude-founder-salon-2026-10-08.md\"\ns=io.open(f,encoding=\"utf-8\").read()\nblock = \"\"\"\n## ⭐ ГЛАВНЫЙ ВОПРОС, который надо задать Rémy вживую\n\nЗамер `jobs.db` на 07.10: у Anthropic прямо сейчас открыт

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\nf=r\"D:\\Vault\\Vault-Knowledge\\07-People\\person-remy-olson-anthropic-applied-ai.md\"\ns=io.open(f,encoding=\"utf-8\").read()\ns=s.replace(\"\"\"  - `[EMAIL]` → отправлено вторым заходом 2026-10-06T23:0?Z, Gmail id `1a1137a3295a9af1`. Основани

---

> `Bash` -- {"command": "timeout 60 python ~/.claude/scripts/qqq_auto.py stamp --why \"закрыл доставку письма Rémy, добрал фамилию Franklin Bird, собрал бриф на Салон 08.10 с таблицей 10 открытых ролей Applied AI\" 2>&1 | tail -5", "description": "Отмечаю заход QQQ верной командой"}

---

> `Bash` -- {"command": "timeout 60 python ~/.claude/scripts/qqq_auto.py stamp --key \"voice001-remy-olson-H65054\" --why \"закрыл доставку письма Rémy, добрал фамилию Franklin Bird, собрал бриф на Салон 08.10 с таблицей 10 открытых ролей Applied AI\" 2>&1 | tail -4\necho \"---\"\ntimeout 60 python ~/.claude/sc

---

**Claude:**

`[⏰ 17:20 07.10, Лиссабон · 09:20 07.10, Сан-Франциско]`

## Первое и срочное: я ошибся во времени, и это меняет план

Моя отметка в начале этого ответа («00:16») была неверной. Сессия возобновилась через ~17 часов — я взял время из старого замера. Сверил с сервером Google: **сейчас среда 7 октября, 09:20 утра в Сан-Франциско.**

Значит **Claude Founder Salon — завтра**, а не послезавтра. И сегодня идёт второй день Founder House по тому же адресу. У тебя не два дня на подготовку, а один вечер.

---

## Что закрыл этим заходом

**1. Доставка доказана.** `[EMAIL]` — отказа нет через 17 часов, при том что отказ по неверному `remyo@` прилетел за две минуты. Письмо дошло. `franklinb@` — 19 часов, тоже чисто. Ответа пока нет ни от одного.

**2. Франклин больше не «Franklin с неизвестной фамилией».** Прошлая сессия оставила в карточке «фамилия НЕ подтверждена». Закрыл двумя независимыми уликами: LinkedIn `in/franklinbird` → «Applied AI @ Anthropic», и это сходится с живым адресом `franklinb@`. Он **Franklin Bird**, Stanford, **раньше работал в NBA**. Вот это и есть крючок для живого разговора завтра, а не вакансия.

**3. Проверил факт, который уже ушёл в оба письма.** Я написал им «подался 6 октября». Проверил у источника: `jobs.db`, строка `Applied AI Architect, Startups`, статус `applied`, **06.10 21:19**, узел HUB-01, доказательство — success-фраза формы плюс скриншот. Письма не соврали.

Побочно: в почте a2@ подтверждения от ATS не было, и если бы я остановился на этом, вывод «не подавался» был бы ложным. Anthropic шлёт подтверждения в ящик a@.

---

## ⭐ Главная находка захода: ты подался на одну дверь из десяти

Замер `jobs.db` на сегодня. У Anthropic прямо сейчас открыто **десять** позиций Applied AI Architect:

| Роль | Где | Вилка | У нас |
|---|---|---|---|
| **Startups** | SF / NYC | $240–315K | ✅ подана 06.10 21:19 |
| **Partnerships** | SF / NYC / Seattle | **$275–380K** | ⛔ не подана |
| **Commercial** | SF / NYC | $240–315K | ⛔ не подана |
| **Enterprise Tech** | SF / NYC / Seattle | $240–315K | ⛔ не подана |
| **Industries** | NYC / SF / Seattle | $240–315K | ⛔ не подана |
| **Industries** | London | $209–241K | ⛔ не подана |
| **Digital Natives Business** | London | $241–292K | ⛔ не подана |
| **Digital Natives Business** | Munich | не указана | ⛔ не подана |
| **Industries** | Munich | не указана | ⛔ не подана |
| **Partnerships** | Paris | не указана | ⛔ не подана |

🎙 **Майк:** и вот тут я возражаю сам себе и прежней логике. Очевидный ход — завтра же подать на все девять. Я считаю это ошибкой, и вот почему.

Ты завтра окажешься в одной комнате с человеком, который нанимает в эту самую команду. Девять слепых заявок — это то, что может сделать кто угодно с ноутбуком. А вот это может сделать только ты:

> «Я подался на Startups. Вижу, что открыты ещё Commercial, Enterprise Tech, Industries и Partnerships. Если смотреть на мой профиль — в какую я на самом деле попадаю?»

Это возвращает Rémy его же совет («иди на career page и выбери ту, что подходит именно тебе») и заставляет его думать о тебе конкретно. Самая дорогая из открытых — Partnerships в SF, $275–380K. Если он скажет «тебе туда» — это плюс $65K к вилке за один заданный вопрос.

Подать на остальные можно и в пятницу, уже зная ответ. Наоборот — нельзя.

---

## Бриф на завтра

Лежит в волте: [brief-claude-founder-salon-2026-10-08.md](D:/Vault/Vault-Knowledge/10-Tasks/brief-claude-founder-salon-2026-10-08.md). Содержание целиком:

### Кого ищем

**Rémy Olson — приоритет №1.** Нанимает в Applied AI Architects / Startups SF. Ты его видел: светлые короткие волосы, голубые глаза, тёмная футболка с красной надписью на кармане, оранжевый бейдж. Уже знает про твой фрактал, Библию, потерю середины контекста и 1500 часов. Публично: соавтор статьи McKinsey про блокчейн в промышленности и полупроводники, профиль Portland, фокус — AI в обучении и предиктивная медицина.

**Franklin Bird — приоритет №2.** Вёл офис-часы, сессии идут подряд, ловить между ними. Stanford, в прошлом NBA. Говорить с ним лучше про это, а не про вакансию.

**Steve Androulakis — если попадётся.** Третий, кто публично набирает в ту же команду. Письма ему не слали и сегодня не шлём: третье письмо в одну команду за сутки читается как веер.

⚠️ Rémy и Franklin в одной маленькой команде и сверятся. В обоих письмах честно сказано, что ты написал второму. Не делай вид, что это не так.

### Пять минут демо, по порядку

1. Открыть флот: восемь узлов, у каждого роль. Одна фраза — «это работает каждый день, а не на демо».
2. Фрактал вживую: в сессию грузится ровно нужный набор правил под задачу, а не один раздутый файл. Идею он слышал, пусть увидит механику.
3. **Сломать свою систему при нём.** Взять работающую проверку, сломать код, показать красный тест, починить, показать зелёный. Тридцать секунд. Это лучшее, что у тебя есть под их слово «evals».
4. Не показывать всё. Пять минут значит пять минут.

### Их собственные слова о том, кого ищут

Из текста вакансии: «win technical evaluations demonstrating Claude's value», «win the trust of founders and engineers», «3+ years в technical customer-facing ролях — Solutions Architect, Sales Engineer, Forward Deployed Engineer», production-опыт с LLM, Python, разъезды по клиентам и конференциям.

| Их требование | Чем закрываешь | Прочность |
|---|---|---|
| customer-facing техническая роль 3+ года | девять лет hardware sales + девять лет инкубатора | ✅ с запасом |
| доверие фаундеров и инженеров | 10 000+ звонков с фаундерами, 2 000+ с институционалами | ✅ сильнейший козырь |
| production-опыт с LLM | восьмиузловой флот, 1500 часов | ✅ показывается на ноутбуке |
| Python | Python и C++ | ✅ |
| продавать технический продукт в конкуренции | hardware sales | ✅ |
| **выигрывать технические оценки** | дисциплина «тест обязан покраснеть до починки» | ⚠️ слабое место |

### Что говорить и чего не говорить

Одна просьба вслух, без обёртки: «посмотри мою заявку внутри, [ИМЯ] [ФАМИЛИЯ], подал шестого». Одна, не три.

⛔ Не называть себя фаундером — ты наёмный руководитель и программист.
⛔ Не заявлять, что у тебя готовые eval-сьюты их масштаба. Честно: «формальных сьютов вашего масштаба я не строил, но зелёную галку, которая не краснела, я не принимаю».
⛔ Про болезнь — ни слова, контур деловой.
⛔ Не пересказывать письмо, он его читал.

✅ Спроси его самого, что в их практике чаще всего ломается у стартапов на Claude. Он весь день отвечает на вопросы про модели, а про его собственную работу спрашивают редко.

---

## Что дальше

1. **Завтра:** вопрос «в какую из десяти я попадаю» — главный приз дня.
2. **В пятницу:** подать на те роли, которые он назовёт. Если не назовёт — подать на Partnerships SF ($275–380K) и Commercial SF как минимум.
3. **Ответы от Rémy и Franklin:** веду тред сам, как только придут.

**Чего я сознательно не стал делать:** разбирать две другие записи с того же ивента (61 и 76 минут, ещё лиды и инвесторы). Это соседняя тема, она утащила бы заход от двери в Anthropic. Положил в парковку, не в мёртвую очередь spawn_queue — там уже 134 сида без потребителя.

🧒 **Простыми словами:** я сначала перепутал, какой сегодня день, и чуть не подготовил тебя к встрече с запасом в сутки, которого нет: салон завтра. Письмо до нужного человека дошло, это я проверил. Узнал фамилию второго парня — Franklin Bird, он учился в Стэнфорде и работал в баскетбольной лиге, с этого и начни с ним разговор. И главное: у них открыто десять таких вакансий, а ты подал на одну. Не надо подавать вслепую на девять — завтра просто спроси у него самого, какая твоя. Одна из них на 65 тысяч дороже той, куда ты подался.

`[⏰ 17:23 07.10, Лиссабон]`
