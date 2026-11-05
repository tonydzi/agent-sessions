---
session: s_5229da00
date: 2026-10-21
words: 3341
turns: 18
tools: "Agent, Bash, Glob, Grep, Read, ToolSearch, mcp__be573d85-3efd-4883-8eee-7095a4943f74__create_event, mcp__be573d85-3efd-4883-8eee-7095a4943f74__list_calendars, mcp__be573d85-3efd-4883-8eee-7095a4943f74__list_events, mcp__be573d85-3efd-4883-8eee-7095a4943f74__search_events"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-21 · Нужно провести глубокие исследования на все конференции, похожие на NVIDIA GTC на 2026-202…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5229da00` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Нужно провести глубокие исследования на все конференции, похожие на NVIDIA GTC на 2026-2027 год, и добавить их в календарь. Но не только конференции NVIDIA GTC, а и любые конференции AI в Европе и США, похожие на NVIDIA GTC, или же просто любые AI-конференции для разработчиков. Мы уже делали такое исследование. Нужно провести рекорд, что мы делаем, чтобы заново не сказать лишнего. И на 2027 год надо точно провести исследование и поставить все в календарь. Возможно, у нас есть рутина, которая ставится в календарь, но я не уверен. Возможно, есть рутина, которая ищет, а потом есть рутина, которая ставится в календарь. Если такого еще нет, то на МакПро надо бы сделать такую рутину. Оправить ему задачу, или по SSH подключиться. Значит, одна рутина ищет ивенты, на сонете пусть она работает, другая рутина ставит в календарь ее ивенты. Европа, Америка, Канада, Европа, США, Канада, Дубай, Лондон, Швейцария, Африка, Гонконг, Сингапур. И Австралия. Гонконг, Сингапур, Малайзия. Талант. И Австралия. И ставим все в календарь. Вот почему сейчас после этой сессии. Если ты работаешь одновременно с кодексом, то вы коллаборируете друг с другом, чтобы разделить обязанности и сделать работу параллельной.

---

**Claude:**

Начинаю с RECALL: что уже делали по конференциям и календарю.

---

> `Grep` -- {"pattern": "GTC|конференци", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "files_with_matches", "-i": true, "head_limit": 30}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports 2>/dev/null; python brain_ask.py \"конференции AI разработчиков календарь GTC 2026 2027 рутина\" 2>&1 | head -60", "description": "RAG-поиск по волту про конференции", "timeout": 90000}

---

> `Glob` -- {"pattern": "**/*conference*", "path": "D:\\Vault\\Vault-Knowledge"}

---

**Claude:**

Нашёл прошлый ДР «ai-conferences-world-map» (01.10) и два ретро 06.10. Читаю их и ищу существующие рутины.

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\insight-DR-DR26-10-01-HUB-01-1434-ai-conferences-world-map.md"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-10-06-ai-conferences-map-and-eu-meetups.md"}

---

> `Bash` -- {"command": "cd ~/.claude 2>/dev/null; ls scripts | grep -i -E \"conf|event|calendar|valley|luma\" | head -40; echo ---; grep -il -E \"conference|конференц\" scheduled-tasks/*/SKILL.md 2>/dev/null | head; ls scheduled-tasks 2>/dev/null | grep -i -E \"conf|event|cal|luma\" | head -30", "description":

---

> `Bash` -- {"command": "cd ~/.claude; ls scripts | grep -i -E \"^cv_|cv-event|events_|calendar|gcal\" | head -30; echo ---TASKS; ls scheduled-tasks | grep -i -E \"cv|event|conf|valley|calendar|invite\" ; echo ---SKILLS; ls skills | grep -i -E \"cv-|event|luma|conf\"; echo ---VAULT; ls /e/Obsidian/_imports | gr

---

> `mcp__s_2292b084__list_calendars` -- {}

---

> `Bash` -- {"command": "cd ~/.claude; cat scheduled-tasks/cv-outreach-executor/SKILL.md | head -60; echo ======; head -40 skills/cv-outreach/SKILL.md; echo =====; grep -rIl -i -E \"conference-watch|conf_watch|events_discover|conference_calendar|ai-conferences\" scripts scheduled-tasks 2>/dev/null | head", "des

---

> `mcp__s_2292b084__search_events` -- {"query": "GTC", "calendarId": "[EMAIL]"}

---

> `ToolSearch` -- {"query": "select:mcp__s_2292b084__search_events,mcp__s_2292b084__list_events,mcp__s_2292b084__create_event", "max_results": 5}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; ls | grep -i -E \"peer_help|machine_bus|bus_send|ssh\" | head; python machine_stamp.py line --agent \"Claude\" 2>&1 | head -2; python peer_help.py alive 2>&1 | head -20", "description": "Проверить живость NODE-0X по шине", "timeout": 60000}

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2026-10-21T00:00:00", "endTime": "2027-12-31T00:00:00", "fullText": "Добавил Claude Code", "orderBy": "startTime", "pageSize": 250}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5229da00/tool-results/; python - <<'E'\nimport json,glob,collections\nf=glob.glob('mcp-be573d85*list_events*.txt')[0]\nd=json.load(open(f,encoding='utf-8'))\nev=d['events'];print(len(ev))\nc=coll

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2027-01-01T00:00:00", "endTime": "2027-12-31T00:00:00", "orderBy": "startTime", "pageSize": 100, "fullText": "GTC"}

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2027-01-01T00:00:00", "endTime": "2027-12-31T00:00:00", "orderBy": "startTime", "pageSize": 10}

---

> `Bash` -- {"command": "mkdir -p \"/e/Obsidian/Vault-Knowledge/05-Resources/conf-radar/_raw\"; cat > \"/e/Obsidian/Vault-Knowledge/05-Resources/conf-radar/SCHEMA.md\" <<'E'\n# conf-radar: реестр AI-конференций для разработчиков (схема)\nMachine: HUB-01 (Хаб) · Agent: Claude · Operator: dev · 2026-10-2

---

> `Agent` -- {"description": "Поиск конференций США и Канада", "model": "sonnet", "prompt": "Задача: найти ВСЕ AI/ML-конференции для разработчиков и инженеров (аналоги NVIDIA GTC, AI Engineer, PyTorch Conf, KubeCon-AI, ODSC, QCon AI, vendor-саммиты, крупные хакатоны, академические NeurIPS/ICLR-уровня) в США и Ка

---

> `Agent` -- {"description": "Поиск конференций Европа Дубай", "model": "sonnet", "prompt": "Задача: найти ВСЕ AI/ML-конференции для разработчиков и инженеров (аналоги NVIDIA GTC, AI Engineer, PyTorch Conf, KubeCon, QCon, vendor-саммиты, крупные хакатоны, академические) в Европе (вкл. Лондон/UK, Швейцария, Герма

---

> `Agent` -- {"description": "Поиск конференций Азия Африка Австралия", "model": "sonnet", "prompt": "Задача: найти ВСЕ AI/ML-конференции для разработчиков и инженеров (аналоги NVIDIA GTC, AI Engineer, крупные вендорские саммиты, академические, хакатоны) в Гонконге, Сингапуре, Малайзии (Куала-Лумпур), Австралии 

---

**Claude:**

Пока агенты ищут, отправляю NODE-0X задачу на две постоянные рутины.

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python bus_send.py --help 2>&1 | head -25", "description": "Посмотреть синтаксис отправки по шине"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python bus_send.py NODE-0X \"TASK: Построить пару рутин conf-radar (приказ оператора 21.10, сессия 59126, хаб). ЦЕЛЬ: все AI-конференции для разработчиков (аналоги NVIDIA GTC) в США, Канаде, Европе, Лондоне, Швейцарии, Дубае, Африке, Гонконге, Сингапуре, Малайзии, А

---

**Claude:**

Задача ушла на NODE-0X (шина: Syncthing и TG-03, оба OK). Три Sonnet-агента ищут по регионам. Когда вернутся, я солью результат в единый реестр и поставлю события в календарь bb@. Дальше пойдёт проверка дат у Codex.

**Что нашёл:**
- Прошлый ДР от 01.10 покрывает окт 2026 – апр 2027, в основном США и ЕС. В календаре bb@ уже стоят GTC 2027 и около 125 событий окт–дек 2026.
- Автоматической пары «рутина ищет → рутина ставит в календарь» нет. `cv-events` покрывает только события Долины из Luma.
- Не покрыты Азия, Африка, Австралия и Канада, а 2027 год покрыт неполно.

**Что сделано:**
- Заведён реестр `conf-radar/conferences.jsonl` в волте, схема лежит рядом.
- NODE-0X строит две рутины. Поисковик на Sonnet раз в неделю ищет новое и перепроверяет даты. Календарная рутина раз в сутки ставит подтверждённые события в bb@ без дублей.

🧒 **Простыми словами:** Раньше конференции искали и вносили в календарь вручную, один раз. Теперь я собираю один общий список, а на втором компьютере будут две «няни»: одна каждую неделю ищет новые конференции по миру, другая сама вносит их тебе в календарь.

---

**User:**

<task-notification>
<task-id>ac4fdfc55eede1bba</task-id>
<tool-use-id>toolu_017B5Vo91vQTj1w5wyseXBVL</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_5229da00\tasks\ac4fdfc55eede1bba.output</output-file>
<status>completed</status>
<summary>Agent "Поиск конференций Азия Африка Австралия" finished</summary>
<note>A task-notification fires each time this agent stops with no live background children of its own. The user can send it another message and resume it, so the same task-id may notify more than once.</note>
<result>Файл `D:\Vault\Vault-Knowledge\05-Resources\conf-radar\_raw\apac_af_au.jsonl`: 34 строки, 16 verified.

Покрытие неполное, проверял в одном заходе:
- **Не нашёл подтверждённых дат 2027:** KubeCon Japan, India и China, AWS Summit Sydney, Google Cloud Summit Sydney, SXSW Sydney, AI Everything Kenya, Connected Africa, GTC Taipei.
- **Deep Learning Indaba 2027, AI Engineer Singapore 2027, AI Engineer India 2027, Africa Tech Festival 2027** в файле с датой null, verified=false. Официально даты ещё не объявлены.
- **Продолжить следовало бы с:** Австралия (PyCon AU 2027, DevOpsDays, Data Innovation), Брисбен, Кигали, Кейптаун, хакатоны.
- **Выкинул как мусор:** платные академические площадки вроде ICAISE Сидней и ICAIHI Мельбурн.
- **Вне регионов:** ICLR 2027 (Сан-Франциско), KDD 2027 (Сан-Хосе), WWW 2027 (Дублин), AAAI 2027 (Монреаль), ICML 2027 (Южная Америка).
- **Вне диапазона по дате:** OpenAI DevDay Токио 20.10.2026.</result>
<usage><subagent_tokens>175358</subagent_tokens><tool_uses>74</tool_uses><duration_ms>193666</duration_ms></usage>
</task-notification>

---

**Claude:**

Азия, Африка и Австралия готовы: 34 строки, 16 подтверждены официальными страницами. Ждём США/Канаду и Европу, потом слияние и календарь.

---

**User:**

<task-notification>
<task-id>a7c6d3b0783ad40d9</task-id>
<tool-use-id>toolu_01EQSize5rK4atcjDe3QHFKA</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_5229da00\tasks\a7c6d3b0783ad40d9.output</output-file>
<status>completed</status>
<summary>Agent "Поиск конференций Европа Дубай" finished</summary>
<note>A task-notification fires each time this agent stops with no live background children of its own. The user can send it another message and resume it, so the same task-id may notify more than once.</note>
<result>Файл `D:\Vault\Vault-Knowledge\05-Resources\conf-radar\_raw\eu_uk_ch_ae.jsonl`: 64 строки, verified=true у 50; JSON проверен парсером.

Что стоит знать:
- **Без дат (14 строк, verified=false, start и end равны null):** GTC Paris 2027, GITEX Global 2027, Web Summit Lisbon 2027, NeurIPS 2027 (город не объявлен), Dubai AI Week 2027, AI Engineer Paris 2027, EuroPython 2027, Devoxx UK 2027, GITEX Europe Berlin 2027, LEAP 2027 (в агрегаторах даты расходятся, официальный сайт отдал 403) и Data Innovation Summit MEA (известен только месяц, сентябрь 2027).
- **С датами, но не подтверждены:** Black Hat Europe 2026 (официальная страница отдала 403, даты из поиска), Jfokus 2027 (даты из sessionize, на jfokus.se их нет), Junction 2026 (даты из поиска).
- **Не вошли:** ICML 2027 (Южная Америка), CVPR 2027 (Сиэтл), ICLR 2027 (Западное побережье Северной Америки), IJCAI 2027 (Киото), KDD, SIGIR, ICCV и Interspeech 2027 вне региона. ACL 2027 официальный сайт не показал. ODSC Europe и AWS Summit 2027 на официальных страницах не нашёл. PyTorch Conference Europe нет в календаре Linux Foundation на 2026-2027, PyData Europe тоже.
- **Region для Дохи:** у Web Summit Qatar поставил `AE` с `country=QA`, потому что в схеме нет отдельного значения для Залива.
- **Города, которых нет на странице:** Devoxx Greece указан как Athens, на странице города нет. У GITEX AI Mediterranean город пустой.

Файл: `D:\Vault\Vault-Knowledge\05-Resources\conf-radar\_raw\eu_uk_ch_ae.jsonl`

64 строки, 50 verified.</result>
<usage><subagent_tokens>201703</subagent_tokens><tool_uses>122</tool_uses><duration_ms>316470</duration_ms></usage>
</task-notification>

---

**Claude:**

Европа готова: 64 строки, 50 подтверждены. Жду агента по США и Канаде.

---

**User:**

<task-notification>
<task-id>aef0dd571695cee06</task-id>
<tool-use-id>toolu_014fQL73YRNMZpuEFFebTMVU</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_5229da00\tasks\aef0dd571695cee06.output</output-file>
<status>completed</status>
<summary>Agent "Поиск конференций США и Канада" finished</summary>
<note>A task-notification fires each time this agent stops with no live background children of its own. The user can send it another message and resume it, so the same task-id may notify more than once.</note>
<result>61 строка, 44 verified. Файл: `D:\Vault\Vault-Knowledge\05-Resources\conf-radar\_raw\us_ca.jsonl`.

Заметки по неподтверждённому и по расхождениям с вашим списком:

- **verified=false, даты есть, официальная страница недоступна или без дат (10):** Oracle AI World, Microsoft Ignite 2026, AISTATS 2027, Toronto Tech Week 2027, Datadog DASH 2027, OCP Global Summit 2027, SC27, а также три без дат на официальной странице.
- **verified=false, дат нет (start и end = null, 8 строк):** Google I/O 2027, Microsoft Build 2027, re:Invent 2027, Ignite 2027, OpenAI DevDay 2027, TechCrunch Disrupt 2027, Hot Chips 2027, PyCon US 2027. Даты из агрегаторов я не вписывал.
- **Расхождения с вашим списком:**
  - HumanX 2027 проходит в Лас-Вегасе 8-10 марта, не 7-10 (по официальной странице).
  - World's Fair 2027 идёт 29 июня - 1 июля.
  - GTC DC в 2026 году, 30 ноября - 3 декабря.
- **Не попали в файл как не из США и Канады:**
  - ICML 2027: Южная Америка.
  - NeurIPS 2027: Европа.
  - ICCV 2027: Гонконг.
  - ACL 2027: Киото.
  - GTC Paris и AIE Europe.
- **Не нашёл, не проверено:** анонсы Anthropic и Meta на 2027 год, Ray Summit 2027, Interrupt 2027, хакатоны (TreeHacks, Cal Hacks, HackMIT) на 2027 год.</result>
<usage><subagent_tokens>214537</subagent_tokens><tool_uses>110</tool_uses><duration_ms>326969</duration_ms></usage>
</task-notification>

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/05-Resources/conf-radar; python - <<'E'\nimport json,glob,re,datetime\nrows=[];seen=set()\nfor f in sorted(glob.glob('_raw/*.jsonl')):\n    for l in open(f,encoding='utf-8'):\n        l=l.strip()\n        if not l: continue\n        r=json.loads(l)\n      

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2026-10-21T00:00:00", "endTime": "2027-12-31T00:00:00", "fullText": "Ссылка", "orderBy": "startTime", "pageSize": 250}

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2027-01-01T00:00:00", "endTime": "2027-12-31T00:00:00", "orderBy": "startTime", "pageSize": 250}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5229da00/tool-results/; python - <<'E'\nimport json,glob\nev=[]\nfor f in glob.glob('mcp-be573d85*list_events-17925*.txt'):\n    d=json.load(open(f,encoding='utf-8'))\n    for e in d['events']:\n

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5229da00/tool-results/; python - <<'E'\nimport json,glob,re\nev=[]\nfor f in glob.glob('mcp-be573d85*list_events-17925*.txt'):\n    for e in json.load(open(f,encoding='utf-8'))['events']:\n      

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/05-Resources/conf-radar; python - <<'E'\nimport json,datetime,re\nnew=json.load(open('_new.json',encoding='utf-8'))\nready=json.load(open('_ready.json',encoding='utf-8'))\nextra=[r for r in ready if re.search(r'DevDay Exchange Paris|^Web Summit Lisbon 2026

---

> `Bash` -- {"command": "cd ~/.claude/scripts; grep -l -E \"calendar/v3|googleapiclient.*calendar|events\\(\\)\\.insert\" *.py 2>/dev/null | head; ls /e/Obsidian/_imports | grep -i -E \"gcal|calendar|google_cal\" | head", "description": "Найти готовый код записи в Google Calendar"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/05-Resources/conf-radar; python - <<'E'\nimport json\no=json.load(open('_to_create.json',encoding='utf-8'))\nrows={json.loads(l)['id']:json.loads(l) for l in open('conferences.jsonl',encoding='utf-8')}\ndrop={25,37,48,54}\no=[x for i,x in enumerate(o) if i

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] AI Engineer Sydney 2026 (Web Directions)", "startTime": "2026-12-07T00:00:00", "endTime": "2026-12-09T00:00:00", "allDay": true, "location": "Sydney, Australia", "description": "Ссылка: https://webdirections.org/ai-engineer\nЦена: A

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] AI Engineer Melbourne 2027 (Web Directions)", "startTime": "2027-06-09T00:00:00", "endTime": "2027-06-11T00:00:00", "allDay": true, "location": "Melbourne, Australia", "description": "Ссылка: https://webdirections.org/ai-engineer\nc

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Asia Tech x Singapore 2027 (ATxSummit)", "startTime": "2027-05-26T00:00:00", "endTime": "2027-05-29T00:00:00", "allDay": true, "location": "Singapore", "description": "Ссылка: https://asiatechxsg.com\nconf-radar:atxsg-2027\nMachine:

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] GITEX AI Asia 2027", "startTime": "2027-04-29T00:00:00", "endTime": "2027-05-01T00:00:00", "allDay": true, "location": "Singapore", "description": "Ссылка: https://www.gitexasia.com\nconf-radar:gitex-ai-asia-2027\nMachine: A-2022BAY

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] SuperAI Singapore 2027", "startTime": "2027-09-08T00:00:00", "endTime": "2027-09-10T00:00:00", "allDay": true, "location": "Singapore", "description": "Ссылка: https://www.superai.com\nconf-radar:superai-singapore-2027\nMachine: A-2

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] WSDM 2027", "startTime": "2027-02-15T00:00:00", "endTime": "2027-02-20T00:00:00", "allDay": true, "location": "Hong Kong", "description": "Ссылка: https://wsdm-conference.org/2027/\nCFP: short papers 2026-11-17, industry day 2026-10

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] World AI Show Malaysia 2027", "startTime": "2027-10-12T00:00:00", "endTime": "2027-10-14T00:00:00", "allDay": true, "location": "Kuala Lumpur, Malaysia", "description": "Ссылка: https://worldaishow.com/malaysia/\nconf-radar:world-ai

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Africa Tech Summit Nairobi 2027", "startTime": "2027-02-10T00:00:00", "endTime": "2027-02-12T00:00:00", "allDay": true, "location": "Nairobi, Kenya", "description": "Ссылка: https://www.africatechsummit.com\nconf-radar:africa-tech-s

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] GITEX Africa 2027", "startTime": "2027-04-26T00:00:00", "endTime": "2027-04-29T00:00:00", "allDay": true, "location": "Marrakech, Morocco", "description": "Ссылка: https://www.gitexafrica.com\nconf-radar:gitex-africa-2027\nMachine: 

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Africa Tech Festival 2026 + AI Summit", "startTime": "2026-11-17T00:00:00", "endTime": "2026-11-20T00:00:00", "allDay": true, "location": "Cape Town, South Africa", "description": "Ссылка: https://www.africatechfestival.com\nconf-ra

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] COMPUTEX Taipei 2027 (GTC Taipei не объявлен)", "startTime": "2027-06-01T00:00:00", "endTime": "2027-06-05T00:00:00", "allDay": true, "location": "Taipei, Taiwan", "description": "Ссылка: https://www.computextaipei.com.tw/en/index.h

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] ACL 2027", "startTime": "2027-08-17T00:00:00", "endTime": "2027-08-23T00:00:00", "allDay": true, "location": "Kyoto, Japan", "description": "Ссылка: https://2027.aclweb.org/\nCFP: ARR 2027-01-04\nconf-radar:acl-2027\nMachine: A-2022

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] IJCAI-27 (Kyoto)", "startTime": "2027-08-07T00:00:00", "endTime": "2027-08-14T00:00:00", "allDay": true, "location": "Kyoto, Japan", "description": "Ссылка: https://www.ijcai.org/future_conferences\nconf-radar:ijcai-2027-kyoto\nMach

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] OpenAI DevDay Exchange Seoul (по заявке)", "startTime": "2026-10-22T00:00:00", "endTime": "2026-10-23T00:00:00", "allDay": true, "location": "Seoul, South Korea", "description": "Ссылка: https://events.openai.com/devdayexchange2026/

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Dubai AI Festival 2026", "startTime": "2026-10-26T00:00:00", "endTime": "2026-10-28T00:00:00", "allDay": true, "location": "Dubai, UAE", "description": "Ссылка: https://dubaiaifestival.com/event-dates/\nconf-radar:dubai-ai-festival-

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Snowflake World Tour Rotterdam", "startTime": "2026-10-27T00:00:00", "endTime": "2026-10-28T00:00:00", "allDay": true, "location": "Rotterdam, Netherlands", "description": "Ссылка: https://www.snowflake.com/en/world-tour/\nconf-rada

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Databricks Data + AI World Tour Munich", "startTime": "2026-11-04T00:00:00", "endTime": "2026-11-05T00:00:00", "allDay": true, "location": "Munich, Germany", "description": "Ссылка: https://www.databricks.com/dataaisummit/worldtour\

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Databricks Data + AI World Tour Amsterdam", "startTime": "2026-11-10T00:00:00", "endTime": "2026-11-11T00:00:00", "allDay": true, "location": "Amsterdam, Netherlands", "description": "Ссылка: https://www.databricks.com/dataaisummit/

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Databricks Data + AI World Tour London", "startTime": "2026-11-11T00:00:00", "endTime": "2026-11-12T00:00:00", "allDay": true, "location": "London, UK", "description": "Ссылка: https://www.databricks.com/dataaisummit/worldtour\nЦена

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] MLcon Berlin 2026", "startTime": "2026-11-16T00:00:00", "endTime": "2026-11-21T00:00:00", "allDay": true, "location": "Berlin, Germany", "description": "Ссылка: https://mlconference.ai/\nconf-radar:mlcon-berlin-2026\nMachine: A-2022

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Databricks Data + AI World Tour Milan", "startTime": "2026-11-24T00:00:00", "endTime": "2026-11-25T00:00:00", "allDay": true, "location": "Milan, Italy", "description": "Ссылка: https://www.databricks.com/dataaisummit/worldtour\nЦен

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Databricks Data + AI World Tour Zurich", "startTime": "2026-12-01T00:00:00", "endTime": "2026-12-02T00:00:00", "allDay": true, "location": "Zurich, Switzerland", "description": "Ссылка: https://www.databricks.com/dataaisummit/worldt

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Databricks Data + AI World Tour Stockholm", "startTime": "2026-12-02T00:00:00", "endTime": "2026-12-03T00:00:00", "allDay": true, "location": "Stockholm, Sweden", "description": "Ссылка: https://www.databricks.com/dataaisummit/world

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] GITEX Global 2026", "startTime": "2026-12-07T00:00:00", "endTime": "2026-12-12T00:00:00", "allDay": true, "location": "Dubai, UAE", "description": "Ссылка: https://www.gitex.com/\nconf-radar:gitex-global-2026\nMachine: HUB-01

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] NDC London 2027", "startTime": "2027-01-25T00:00:00", "endTime": "2027-01-30T00:00:00", "allDay": true, "location": "London, UK", "description": "Ссылка: https://ndclondon.com/\nconf-radar:ndc-london-2027\nMachine: HUB-01 (Ха

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] FOSDEM 2027", "startTime": "2027-01-30T00:00:00", "endTime": "2027-02-01T00:00:00", "allDay": true, "location": "Brussels, Belgium", "description": "Ссылка: https://fosdem.org/2027/\nЦена: бесплатно\nconf-radar:fosdem-2027\nMachine:

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] MWC Barcelona 2027", "startTime": "2027-03-01T00:00:00", "endTime": "2027-03-05T00:00:00", "allDay": true, "location": "Barcelona, Spain", "description": "Ссылка: https://www.mwcbarcelona.com/\nconf-radar:mwc-barcelona-2027\nMachine

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Applied Machine Learning Days (AMLD) 2027", "startTime": "2027-03-09T00:00:00", "endTime": "2027-03-12T00:00:00", "allDay": true, "location": "Lausanne, Switzerland", "description": "Ссылка: https://appliedmldays.org/\nconf-radar:am

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] EACL 2027", "startTime": "2027-03-09T00:00:00", "endTime": "2027-03-15T00:00:00", "allDay": true, "location": "Athens, Greece", "description": "Ссылка: https://2027.eacl.org/\nconf-radar:eacl-2027\nMachine: HUB-01 (Хаб) · Age

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] Devoxx France 2027", "startTime": "2027-04-07T00:00:00", "endTime": "2027-04-10T00:00:00", "allDay": true, "location": "Paris, France", "description": "Ссылка: https://devoxx.fr/\nconf-radar:devoxx-france-2027\nMachine: A-2022BAYARE

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] World AI Expo Dubai 2027", "startTime": "2027-04-07T00:00:00", "endTime": "2027-04-10T00:00:00", "allDay": true, "location": "Dubai, UAE", "description": "Ссылка: https://worldaiexpo.io/event-details/\nconf-radar:world-ai-expo-dubai

---

> `Agent` -- {"description": "Создать 49 событий в календаре", "model": "sonnet", "prompt": "Задача: создать в Google Calendar [EMAIL] события конференций из JSON-файла D:\\Vault\\Vault-Knowledge\\05-Resources\\conf-radar\\_to_create2.json, ТОЛЬКО элементы с индексами 32..80 включительн

---

**Claude:**

Параллельно прошу Codex второй парой глаз проверить даты по официальным страницам.

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python llm_ask.py --help 2>&1 | head -20", "description": "Посмотреть синтаксис llm_ask"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/05-Resources/conf-radar; cat > _codex_review_prompt.md <<'E'\nТы независимый ревьюер (Codex). Пытайся ОПРОВЕРГНУТЬ даты. Файл D:\\Vault\\Vault-Knowledge\\05-Resources\\conf-radar\\conferences.jsonl: строки с verified=true, start между 2026-10-21 и 2027-

---

**Claude:**

Ревью дат запущено, календарный субагент работает. Жду завершения обоих.

---

**User:**

<task-notification>
<task-id>a68a5618c5d50d297</task-id>
<tool-use-id>toolu_01VcjyGdDb8KYTPrigs5U39j</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_5229da00\tasks\a68a5618c5d50d297.output</output-file>
<status>completed</status>
<summary>Agent "Создать 49 событий в календаре" finished</summary>
<note>A task-notification fires each time this agent stops with no live background children of its own. The user can send it another message and resume it, so the same task-id may notify more than once.</note>
<result>Создано 49, пропущено 0, ошибок 0. Дублей среди индексов 32..80 не нашлось: в календаре были только события из первых 32. Соответствия id и cal_event_id (49 строк) записаны в `D:\Vault\Vault-Knowledge\05-Resources\conf-radar\_created_batch2.jsonl`.

Для некоторых конференций в `conferences.jsonl` нет цены или CFP, поэтому в описании только ссылка.

🧒 Простыми словами: я добавил в календарь 49 конференций, повторов не было. Список "что куда попало" лежит в файле.</result>
<usage><subagent_tokens>187705</subagent_tokens><tool_uses>53</tool_uses><duration_ms>153308</duration_ms></usage>
</task-notification>

---

**Claude:**

Проверяю независимо: считаю события с меткой `conf-radar:` прямо в календаре.

---

> `mcp__s_2292b084__list_events` -- {"calendarId": "[EMAIL]", "startTime": "2026-10-21T00:00:00", "endTime": "2027-12-31T00:00:00", "fullText": "conf-radar:", "pageSize": 250}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5229da00/tool-results/; python - <<'E'\nimport json,re,collections\nd=json.load(open('mcp-s_2292b084-list_events-1792568325387.txt',encoding='utf-8'))\nids=[re.search(r'

---

**Claude:**

В календаре 80 из ожидаемых 81. Ищу, какого события не хватает.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/05-Resources/conf-radar; python - <<'E'\nimport json\no=json.load(open('_to_create2.json',encoding='utf-8'))\nrows={json.loads(l)['id']:json.loads(l) for l in open('conferences.jsonl',encoding='utf-8')}\nfor i,x in enumerate(o):\n    if not rows[x['id']]['

---

**Claude:**

Я сам пропустил IJCAI Hengqin в первой пачке. Создаю.

---

> `mcp__s_2292b084__create_event` -- {"calendarId": "[EMAIL]", "summary": "[конф] IJCAI-27 (Hengqin site)", "startTime": "2027-08-15T00:00:00", "endTime": "2027-08-18T00:00:00", "allDay": true, "location": "Hengqin, China", "description": "Ссылка: https://www.ijcai.org/future_conferences\nconf-radar:ijcai-2027-he

---

**Claude:**

Теперь фиксирую в волте и памяти, чтобы следующая сессия не начинала с нуля.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge; cat > \"03-Insights/insight-conf-radar-registry-2026-10-21.md\" <<'E'\n---\ntitle: \"conf-radar: реестр AI-конференций мира и пара рутин (поиск + календарь)\"\ndate: 2026-10-21\ntype: insight\nstage: distilled\ntags: [conferences, calendar, routines, conf

---

**Claude:**

Конференции за пределами уже стоявших в календаре теперь добавлены, но две вещи не закрыты: постоянные рутины ещё не построены, а независимая проверка дат не вернулась.

**Календарь bb@**
- Добавил 81 событие с метками `conf-radar:<id>` в описании. Пересчёт по календарю дал 80, не хватало IJCAI Hengqin, его я дозавёл отдельно; повторный пересчёт после этого не делал.
- Поиск шёл по трём регионам: США и Канада, Европа с Лондоном, Швейцарией и Дубаем, Азия с Африкой и Австралией. Охвачены Гонконг, Сингапур, Малайзия, Австралия, Найроби, Кейптаун и Марракеш.
- В календаре уже стояли 27 пересекающихся событий (GTC, AI Engineer, QCon и другие), их я не трогал.
- Отсеял 4 нерелевантных: GISEC, LF Energy, Expand North Star, Open Source in Finance.

**Реестр**
- Это общий список в `conf-radar/conferences.jsonl`, 158 строк, схема лежит рядом.
- Около 50 строк без подтверждённых дат или страниц в календарь не попали: Google I/O, Build и re:Invent 2027, GTC Paris, Web Summit 2027 и другие.
- Задачу «добить даты по неподтверждённым» я рутине-поисковику пока не ставил, ни в реестре, ни в задаче NODE-0X.

**Что было раньше**
- Ручной ДР от 01.10 (`DR26-10-01-HUB-01-1434`) покрывал окт 2026 – апр 2027 в основном по США и Европе.
- Постоянной рутины «ищет → ставит в календарь» не было. `cv-events` занимается только событиями Долины.
- Добавлять в календарь можно только через календарный коннектор внутри сессии Claude, готового скрипта API нет.

**Рутины на NODE-0X**
- Задача на две рутины отправлена по шине, Syncthing и TG-03 приняли её. Подтверждения от NODE-0X я не получил, рутины не построены.
- Первая рутина (Sonnet, раз в неделю) ищет новые конференции и перепроверяет даты. Вторая (раз в сутки) ставит подтверждённые события в календарь без дублей.

**Проверка дат**
- Я запустил независимую проверку дат (`llm_ask`, класс `second_opinion`, рельсы codex, grok и gemini), но ответа ещё нет. Результат появится в `_codex_review_out.md`.
- Пока даты проверяли только сами поисковые агенты.
- Даты уже в календаре могут содержать ошибки. Прошлый ДР нашёл у поисковых агентов путаницу вроде «NeurIPS в Сан-Диего».

**Решения для оператора**
- Билеты ни на что не покупал, это отдельное решение оператора.

Реестр, заметка и память записаны: `03-Insights/insight-conf-radar-registry-2026-10-21.md` и `conf-radar-registry.md`.

🧒 **Простыми словами:** Я собрал все большие AI-конференции мира в один список и поставил 81 из них в твой календарь. Ещё ~50 в списке пока без точных дат, их дособерёт будущий «помощник-искатель» на другом компьютере. Сам этот помощник пока не построен, я только отправил ему задание. Даты проверяли только те, кто их искал, а независимая проверка ещё идёт.
