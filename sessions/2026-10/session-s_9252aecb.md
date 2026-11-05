---
session: s_9252aecb
date: 2026-10-07
words: 12427
turns: 7
tools: "Bash, Edit, Skill, ToolSearch, WebFetch, WebSearch, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9252aecb` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:7971.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
При всей глубокой исследовании, что такое Langchain, какой имеет отношение к искусству интеллекта, и какую пользу можно получить начав использовать этот продукт.
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

> `Bash` -- {"command": "TZ=Europe/Lisbon date \"+%Y-%m-%d %H:%M %Z\"; echo \"---\"; grep -ril \"langchain\\|langgraph\\|langsmith\" \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/\" 2>/dev/null | head -20", "description": "Measure Lisbon time and grep memory for LangChain"}

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/\"; for f in n8n-stack.md engineer-acquisition-enrichment-not-scraping.md; do echo \"=== $f\"; grep -i -n -B2 -A2 \"langchain\\|langgraph\\|langsmith\" \"$f\"; done", "description": "Read LangChain mentions in memo

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge\" >/dev/null 2>&1 && echo VAULT_OK || echo NO_VAULT; grep -ril \"langchain\" \"D:/Vault/Vault-Knowledge\" 2>/dev/null | head -30", "description": "Grep vault for langchain notes"}

---

> `WebSearch` -- {"query": "LangChain 1.0 release what changed langchain-core langgraph 2026"}

---

> `WebSearch` -- {"query": "LangChain company funding valuation revenue 2026 LangSmith customers"}

---

> `WebSearch` -- {"query": "\"LangChain\" criticism why we stopped using LangChain abstraction 2026 engineers opinion"}

---

> `WebSearch` -- {"query": "LangChain vs Claude Agent SDK vs OpenAI Agents SDK vs Pydantic AI comparison 2026"}

---

> `WebSearch` -- {"query": "LangChain LangGraph skills in AI job postings 2026 demand hiring requirement"}

---

> `WebSearch` -- {"query": "LangSmith pricing 2026 free tier traces LangGraph Platform deployment cost"}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\bi58w540g.output\" 2>/dev/null | head -40", "description": "Check vault grep background output"}

---

> `Bash` -- {"command": "curl -s \"https://api.github.com/repos/langchain-ai/langchain\" | python -c \"import sys,json; d=json.load(sys.stdin); print('stars',d.get('stargazers_count'),'forks',d.get('forks_count'),'open_issues',d.get('open_issues_count'),'pushed',d.get('pushed_at'),'lang',d.get('language'))\" 2>

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python -m pip list 2>/dev/null | grep -i \"langchain\\|langgraph\\|langsmith\\|llama-index\\|pydantic-ai\\|openai\\|anthropic\" ; echo \"--- imports in repo:\"; grep -rl \"from langchain\\|import langchain\\|langgraph\" --include=*.py . 2>/dev/null |

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\bi58w540g.output\" 2>/dev/null | tail -30", "description": "Recheck vault grep output"}

---

> `Bash` -- {"command": "echo \"--- good first issues langchain:\"; curl -s \"https://api.github.com/search/issues?q=repo:langchain-ai/langchain+is:open+label:%22good+first+issue%22&per_page=1\" | python -c \"import sys,json;print(json.load(sys.stdin).get('total_count'))\"; echo \"--- help wanted:\"; curl -s \"

---

> `WebFetch` -- {"url": "https://github.com/langchain-ai/deepagents", "prompt": "What is deepagents? Summarize: what it does, the key features (filesystem, subagents, planning, middleware), how it relates to LangChain/LangGraph, install, and any version/date info."}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,urllib.request,collections,datetime\ndef gh(url):\n    req=urllib.request.Request(url,headers={'User-Agent':'x','Accept':'application/vnd.github+json'})\n    return json.load(urllib.request.urlopen(req))\nfor repo in [\"langchain-ai/deepagents\",\"langchain-

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,urllib.request,datetime,collections\ndef gh(url):\n    req=urllib.request.Request(url,headers={'User-Agent':'x','Accept':'application/vnd.github+json'})\n    return json.load(urllib.request.urlopen(req))\nnow=datetime.datetime.now(datetime.timezone.utc)\nfor

---

> `WebSearch` -- {"query": "LangChain \"Fleet\" \"Engine\" sandboxes new product 2026 announcement blog.langchain.com"}

---

> `Bash` -- {"command": "for t in bbocc0dwo bi58w540g; do echo \"=== $t\"; cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\$t.output\" 2>/dev/null | tail -25; done", "description": "Check both background grep outputs"}

---

> `WebFetch` -- {"url": "https://www.langchain.com/blog/interrupt-2026-overview", "prompt": "List everything LangChain shipped/announced: product names, what each does, pricing or availability status, and dates."}

---

> `Bash` -- {"command": "timeout 60 python -m pip show langchain langgraph langsmith deepagents 2>&1 | grep -i \"^Name\\|^Version\\|not found\" | head -20; echo \"=== targeted grep (scripts+imports dirs only):\"; timeout 100 grep -ril \"langchain\" \"D:/Vault/_imports\" 2>/dev/null | head -10", "description"

---

> `Bash` -- {"command": "echo \"=== repo/scripts grep result:\"; cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\bbocc0dwo.output\" 2>/dev/null | tail -20; echo \"=== vault grep (still?):\"; cat \"C:\\Users\\dev\\AppData\\Local\\

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_scratch/google-logout-cleanup-fix\"; ls git25-tools | head -20; echo \"=== head of langgraph probe:\"; head -40 git25-tools/_conformance_probe_langgraph_8722.py; echo \"=== grep langgraph in that dir:\"; grep -rn \"langgraph\" git25-tools/*.py _test_gi

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,urllib.request\ndef gh(u):\n    r=urllib.request.Request(u,headers={'User-Agent':'x','Accept':'application/vnd.github+json'})\n    return json.load(urllib.request.urlopen(r))\nfor n in (8722,8732):\n    try:\n        d=gh(f\"https://api.github.com/repos/lang

---

> `Bash` -- {"command": "for p in langchain langgraph langchain-core deepagents langsmith llama-index pydantic-ai; do v=$(curl -s \"https://pypistats.org/api/packages/$p/recent\" | python -c \"import sys,json;d=json.load(sys.stdin);print(d['data']['last_month'])\" 2>/dev/null); echo \"$p last_month_downloads=$v

---

> `WebSearch` -- {"query": "Anthropic OpenAI job posting \"LangChain\" required skill frontier lab forward deployed engineer 2026"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,urllib.request\ndef get(p):\n    try:\n        r=urllib.request.Request(f\"https://pypistats.org/api/packages/{p}/recent\",headers={'User-Agent':'Mozilla/5.0'})\n        d=json.load(urllib.request.urlopen(r,timeout=30))\n        return d['data']['last_month'

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,urllib.request,time\ndef get(p):\n    for attempt in range(3):\n        try:\n            r=urllib.request.Request(f\"https://pypistats.org/api/packages/{p}/recent\",headers={'User-Agent':'Mozilla/5.0'})\n            return json.load(urllib.request.urlopen(r

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/scripts/llm_ask.py\" 2>/dev/null && timeout 20 python \"C:/Users/dev/.claude/scripts/llm_ask.py\" --help 2>&1 | head -30", "description": "Check llm_ask.py interface"}

---

> `Bash` -- {"command": "cat > \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\scratchpad\\lc_panel.txt\" <<'PY'\nКонтекст. У человека (не-технарь по стилю работы, но программирует на Python) уже есть\nработающий самодельный стек ИИ-агентов: 

---

> `WebFetch` -- {"url": "https://docs.langchain.com/oss/python/langchain/overview", "prompt": "What are the packages and core concepts of LangChain v1 (create_agent, middleware, models, tools, memory, langchain-classic)? What is the relationship to LangGraph and LangSmith? Quote the key building blocks."}

---

> `WebSearch` -- {"query": "langchain-mcp-adapters MCP servers LangGraph agent 2026 how it works"}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\b8wlu3eco.output\" 2>/dev/null | head -60", "description": "Check panel interim output"}

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge\" 2>/dev/null | head -30; echo \"=== 03-Insights sample:\"; ls \"D:/Vault/Vault-Knowledge/03-Insights\" 2>/dev/null | head -8; echo \"=== 06-Concepts sample:\"; ls \"D:/Vault/Vault-Knowledge/06-Concepts\" 2>/dev/null | head -8", "description": "Ins

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge/06-Concepts\" | grep -i \"langchain\\|agent\\|RAG\\|n8n\\|LLM\\|observ\" | head -20; echo \"=== MOCs:\"; ls \"D:/Vault/Vault-Knowledge/90_MOCs\" | head -25", "description": "Find link targets in concepts and MOCs"}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\b8wlu3eco.output\" 2>/dev/null | head -80; echo \"[[[end]]]\"", "description": "Check panel output again"}

---

> `Bash` -- {"command": "mkdir -p \"D:/Vault/Vault-Knowledge/03-Insights\" && cat > \"D:/Vault/Vault-Knowledge/03-Insights/2026-10-06-langchain-deep-dive.md\" <<'EOF'\n---\ntitle: LangChain — что это, отношение к ИИ и польза для нашего стека\ndate: 2026-10-06\ntype: insight\ntopic: [ai-agents, frameworks,

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\2026-10-06-langchain-deep-dive.md", "content": "---\ntitle: LangChain — что это, отношение к ИИ и польза для нашего стека\ndate: 2026-10-06\ntype: insight\ntopic: [ai-agents, frameworks, oss, job-search]\nsource: голосовая оператора в «001 СЕСС

---

> `Bash` -- {"command": "tail -25 \"D:/Vault/Vault-Knowledge/90_MOCs/MOC-AI-Agents.md\"; echo \"=== PANEL:\"; cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\b8wlu3eco.output\" 2>/dev/null | head -40; echo \"[[[end]]]\"", "descr

---

> `Bash` -- {"command": "printf '\\n- [[2026-10-06-langchain-deep-dive]] — LangChain по заказу оператора (06.10.2026): что это (Agent = Model + Harness), три слоя (chains легаси → LangGraph рантайм → LangSmith-платформа + deepagents), живые цифры (147k звёзд, 170M загрузок/мес, оценка $3.01B, #1 по упоминаниям в в

---

> `WebFetch` -- {"url": "https://www.langchain.com/pricing-langsmith", "prompt": "List the current LangSmith plans and exact prices: Developer (free?) trace allowance, Plus per seat price and trace allowance, overage per 1k traces, Enterprise. Any deployment/compute units pricing."}

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\b8wlu3eco.output\" 2>/dev/null; echo \"[[[end-panel]]]\"", "description": "Check panel output"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\2026-10-06-langchain-deep-dive.md", "old_string": "   LangSmith Developer бесплатен: 1 место, 5 000 трейсов/мес (жёсткий кап, не очередь); Plus\n   $39/место + 10 000 трейсов, овередж $2.50/1k. Альтернатива без вендор-л

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\b8wlu3eco.output\"", "description": "Read completed panel output"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude\"; echo \"=== otel/langfuse/tracing in scripts:\"; timeout 60 grep -ril \"langfuse\\|opentelemetry\\|otel\\|trace_id\\|tracing\" scripts --include=*.py 2>/dev/null | head -12; echo \"=== counters/ledgers present:\"; ls _metrics 2>/dev/null | head -8; ls | gre

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\2026-10-06-langchain-deep-dive.md", "old_string": "3. **`langchain[mcp]`.** Наши MCP-серверы (telegram, whatsapp, granola, gmail…) подключаются\n   к любому python-агенту через MultiServerMCPClient. Это снимает зависимо

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\2026-10-06-langchain-deep-dive.md", "old_string": "## 6. Что делать", "new_string": "## 5-бис. Панель против меня (§1.2-бис)\n\nСвой вердикт «стек не переводим» я прогнал через чужие мозги (`llm_ask --mode all`,\nрельсы

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\2026-10-06-langchain-deep-dive.md", "old_string": "1. Поставить трассировку на один реальный прогон (LangSmith free или Langfuse self-host) —\n   замерить, видно ли по трейсу то, чего не видно по нашим логам.", "new_str

---

> `Bash` -- {"command": "TZ=Europe/Lisbon date \"+%H:%M %d.%m.%Y\"; TZ=Europe/Moscow date \"+MSK %H:%M\"", "description": "Measure final time"}

---

> `Bash` -- {"command": "python -c \"\nfrom datetime import datetime,timezone\ntry:\n    from zoneinfo import ZoneInfo\n    n=datetime.now(timezone.utc)\n    print('UTC',n.strftime('%H:%M'),'| Лиссабон',n.astimezone(ZoneInfo('Europe/Lisbon')).strftime('%H:%M'),'| Москва',n.astimezone(ZoneInfo('Europe/Moscow')).

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/chat-timestamps.md\"", "description": "Read chat-timestamps memory"}

---

> `Bash` -- {"command": "python -c \"import sys; sys.path.insert(0,'D:/Vault/_imports/_common'); import ru_datetime; print(ru_datetime.ru_stamp())\"", "description": "Get canonical RU timestamp"}

---

**Claude:**

🕐 вторник, день, 17:36, 6 октября 2026

**Рельса этой сессии:** живые замеры (GitHub API, pypistats, страница цен LangChain) и синтез делал я сам как Claude, потому что вопрос про СВЕЖЕЕ состояние, а чужие CLI-рельсы по свежести слепы (cutoff 2025, замер 06.10). Наружу уехал ровно один класс работы: проверка моего же вердикта на чужих мозгах, `llm_ask --mode all` по рельсам codex + grok (ответили за 249с и 289с, gemini мимо: квота 429, то есть панель 2 из 3).

---

# LangChain: что это, при чём тут ИИ, и что нам с этого

## Короткий ответ в три строки

LangChain продаёт не модель, а **обвязку** вокруг модели (их собственная формула: `Agent = Model + Harness`).

Фреймворк жив и богат (147 тысяч звёзд, 170 млн загрузок в месяц, оценка $3B), но половина серьёзных инженерных команд в 2026 его сняла: вендоры моделей закрыли ту проблему, которую он решал в 2023.

Нам его стек брать целиком **не надо**, а забрать из экосистемы надо **четыре конкретных куска** (четвёртый я сам пропустил, его назвала панель, см. §5-бис).

---

## §1. Что это такое: три разных LangChain, о которых спорят

Люди ругаются и хвалят, не договорившись, о каком слое речь. Их три:

| Слой | Когда | Что это | Живо ли сейчас |
|---|---|---|---|
| chains, «цепочки» | 2022-2023 | клей между вендорами: у каждого свой API, tool-calling ещё не существовало | легаси, переехало в пакет `langchain-classic` |
| **LangGraph** | 2024-2025 | граф-рантайм с состоянием: чекпоинты, durable execution, пауза на человеке | ядро, версия 1.0 с 22.10.2025 |
| **LangSmith-платформа + deepagents** | 2025-2026 | трассировка, деплой, песочницы, Fleet, Engine, готовый harness с файловой системой и субагентами | сюда ушли деньги и вся разработка |

Пакеты на сегодня:

- `langchain`: функция `create_agent` плюс middleware (политики инструментов, ретраи, маршрутизация)
- `langchain-core`: сообщения и стандартные контент-блоки (reasoning, цитаты, tool-calls)
- `langchain-classic`: старый зоопарк цепочек
- `langgraph`: рантайм, граф, чекпоинтеры
- `langsmith`: SDK трассировки
- `deepagents`: «batteries-included agent harness», то есть готовая сборка: файловая система, субагенты, планирование, skills, human-in-the-loop
- `langchain[mcp]`: поддержка MCP прямо в ядре (отдельный `langchain-mcp-adapters` больше не поддерживается)

**Свежесть, замер сегодня:** `langchain-core==1.6.7` выпущен 06.10.2026 в 15:47 UTC, то есть релиз вышел в день твоего заказа. Мажор остаётся 1.x, обещание «никаких ломающих изменений до 2.0».

---

## §2. Какое отношение к искусственному интеллекту

Прямое, но служебное.

Модель сама по себе не продукт: она не помнит прошлый шаг, не ходит в инструменты, не умеет остановиться и спросить человека, не умеет продолжить после падения. Всё это даёт обвязка. LangChain это самая распространённая обвязка в мире.

**Что он даёт:** единый интерфейс к сотням провайдеров, tool-calling, структурированный вывод, кирпичи RAG (загрузка, нарезка, эмбеддинги, векторные базы), память, граф с возобновлением и паузой на человеке, трассировку прогонов.

**Что он НЕ даёт:** ум. Качество ответа это модель плюс промпт плюс данные. Фреймворк ни одного ответа не улучшает, он занимается логистикой вокруг ответа.

---

## §3. Цифры (все замерены сегодня, живые API)

| Метрика | Значение | Чем мерил |
|---|---|---|
| `langchain` звёзд на GitHub | 147 497 | GitHub API |
| `langgraph` звёзд | 42 783 | GitHub API |
| `deepagents` звёзд | 29 971 | GitHub API |
| Загрузок `langchain` за месяц | 170 457 766 | pypistats |
| Загрузок `langchain-core` | 144 826 657 | pypistats |
| Загрузок `langsmith` | 77 233 437 | pypistats |
| Загрузок `langgraph` | 44 769 952 | pypistats |
| Загрузок `deepagents` | 5 660 894 | pypistats |
| Загрузок `pydantic-ai` (конкурент) | 5 383 780 | pypistats |
| Загрузок `openai` (для рамки) | 295 856 631 | pypistats |
| Привлечено денег | $260M за 4 раунда, Series B $125M 20.10.2025 | Tracxn |
| Оценка | $1.3B в декабре 2025, Series C $3.01B в сентябре 2026 | Tracxn, Forge Global |
| Выручка | около $16M ARR (2025) | getlatka |
| Клиенты LangSmith | 250 тысяч регистраций, 25 тысяч активных команд в месяц; Klarna, Snowflake, BCG | отчёты компании |
| Упоминания в вакансиях | #1 среди agent-фреймворков: 392 листинга, 34.5% всех | агрегатор agentic-engineering-jobs |
| Медиана зарплат | LangChain около $187.5K, LangGraph около $209.5K (США) | тот же агрегатор |

**Слепая зона, называю честно:** `llama-index` по загрузкам не измерен, pypistats отдал 429. Получено 8 пакетов из 9 запрошенных.

Что они выкатили в 2026 (конференция Interrupt, 14.05.2026): **LangSmith Engine** (смотрит продакшн-трейсы, кластеризует повторяющиеся падения в именованные проблемы, сам открывает PR с починкой), **Sandboxes** (микро-VM для кода агента, GA), **Managed Deep Agents** (хостинг агентов как сервис), **Context Hub** (версионирование инструкций агентов), **SmithDB** (своя база на Rust под трассировку, P50 загрузки трейса 92 мс), **LLM Gateway** (жёсткие лимиты траты, редактирование PII, приватная бета), **Fleet** (управление парком агентов, пять готовых агентов из коробки).

Посмотри на этот список внимательно: **половина их 2026 года это то, что мы строим у себя руками** (парк агентов, леджеры, лимиты, сторожа, отчёты о падениях).

---

## §4. Критика, и где она права

Главный довод против, он звучит отовсюду: **налог на абстракции**. Чтобы добраться до своего же промпта, надо пролезть через пять слоёв чужого кода. Отлаживаешь не свою логику, а внутренности фреймворка.

Второй довод: проблема 2023 года закрыта самими вендорами. OpenAI дал function calling в середине 2023, Anthropic tool use в 2024, структурированный вывод стал штатным у всех. Память, retrieval и оркестрация инструментов переехали из фреймворка в SDK вендора.

**Но «LangChain умер» это неправда**: 170 млн загрузок в месяц, оценка $3B, релиз в день заказа. Правда другая и скучнее: он перестал быть фреймворком для стартапа из двух человек и стал **корпоративной платформой** (трассировка, деплой, аудит, управление парком). Уходят из него маленькие быстрые команды, приходят предприятия.

---

## §5. Польза лично нам, по полосам

### A. Как замена нашему стеку: НЕТ

У нас около 800 python-скриптов, планировщик Windows, локальный RAG (`brain_ask.py`), SQLite как база фактов, роутер по чужим подпискам (`llm_ask.py`), 5 машин, хуки, скиллы, шина. Миграция это месяцы работы и потеря ремонтопригодности, то есть прямое нарушение АК-47.

Замер: LangChain на этой машине даже не установлен (`pip show` не находит ни `langchain`, ни `langgraph`, ни `langsmith`). И это нормально.

### B. Что забрать, четыре куска

**1. Наблюдаемость.** Честная формулировка после замера: счётчики и JSONL-леджеры у нас есть (их десятки), а вот трассировки прогона ЦЕЛИКОМ (шаги, токены, латентность одного запуска в одном экране) нет; инструментовки OTel или Langfuse в скриптах нет.

Цены с их собственной страницы, замер сегодня: **Developer $0** за одно место, до 5 000 base-трейсов в месяц, дальше pay-as-you-go; **Plus $39** за место, до 10 000 трейсов плюс одна бесплатная маленькая serverless-деплойка; оверейдж считается в LSU по $1.00. Сторонние блоги пишут про жёсткий кап и $2.50 за тысячу, первоисточник этого не подтверждает. Альтернатива без вендор-лока: **Langfuse** self-host.

**2. Паттерны deepagents, а не библиотеку.** Файловая система как память агента, субагенты с изолированным контекстом, middleware-хуки, автосжатие длинного потока, skills. Половину мы уже изобрели сами (скиллы, хуки, `/elephant`, субагенты). Не хватает именно middleware как явного слоя и автосжатия длинных потоков.

**3. `langchain[mcp]`.** Наши MCP-серверы (telegram, whatsapp, granola, gmail, календарь) подключаются к любому python-агенту через `MultiServerMCPClient`. Это снимает зависимость «наши коннекторы живут только внутри Claude Code»: тот же telegram-сервер смогут звать твои собственные скрипты на любой машине флота.

**4. Контракт durable execution (этого в моём вердикте не было, добавила панель).** LangGraph продаёт не единый API моделей, а **контракт шага**: `thread_id`, запись состояния после каждого узла, `interrupt()` для паузы на человеке на дни, возобновление с последнего успешного узла.

Вот где наш стек тихо проигрывает: наш планировщик чекпоинтит ЗАДАЧУ, а не ход агента. Упал на 17-м вызове инструмента, планировщик запускает скрипт с нуля, и необратимый шаг (отправка лиду, пост, подача заявки) уходит ВТОРЫМ разом. У нас восемьсот скриптов и, значит, восемьсот личных семантик повтора.

Забирать надо сам контракт, без библиотеки: `thread_id`, запись после каждого необратимого шага, ключ идемпотентности на отправку, resume читает снимок, а не спрашивает модель заново. Оговорка самой панели: LangGraph это не Temporal, автоподъёма у него нет, снимок умирает вместе с машиной, внешним сторожем остаются наш планировщик и шина.

### C. Найм, миссия №2

LangChain и LangGraph это строка №1 по упоминаниям в вакансиях AI-инженеров (34.5% листингов по агрегатору, сентябрь-октябрь 2026). Forward Deployed Engineer в Anthropic (вакансия от 08.03.2026, $200-300K) требует hands-on по agent-фреймворкам, LangGraph называется поимённо в разборах роли.

Вывод: строка в CV обязательна. И она у нас **заслуженная**, потому что смотри полосу D.

### D. OSS-дверь: куда пушить и куда НЕ пушить (замер)

Я измерил возраст открытых человеческих PR в трёх репозиториях, это прямой прибор «живая очередь или глухая»:

| Репозиторий | Медиана возраста открытого PR | Старше 90 дней | Вердикт |
|---|---|---|---|
| `langchain-ai/deepagents` | **5 дней** (старейший 49) | 0 из 43 | **живая дверь** |
| `langchain-ai/langchain` | 49 дней | 25 из 100 | полумёртвая |
| `langchain-ai/langgraph` | **203 дня** | 70 из 100 | **глухая очередь** |

Второй замер, отрезвляющий: из примерно 200 PR, слитых в `deepagents` за 30 дней, почти все это боты и коре-тим (`mdrxy`, `linted`, `ccurme`); одиночных внешних авторов шесть. Медиана времени до мержа 1.6 часа, но это их собственные PR, не наши.

**Наш собственный след в этой экосистеме уже есть** (нашёл RECALL'ом в `_scratch`, не выдумал): issue [langchain-ai/langgraph#8722](https://github.com/langchain-ai/langgraph/issues/8722) от `tonydzi`, открыт 25.08.2026, «Conformance detector counts an override-that-raises as an implementation: SqliteSaver scores NONE (0/3)».

Статус на сегодня: **открыт, 42 дня без ответа мейнтейнера**. Зато два внешних инженера (`ddddajie`, `Liuzikaii`) прибежали его чинить, а PR #8732 бот закрыл автоматически с текстом «external contributors must be assigned to the linked issue». То есть правило репозитория: сначала получи assign, потом присылай PR.

---

## §5-бис. Панель против меня

Свой вердикт «стек не переводим» я, прежде чем тебе его давать, прогнал через чужие мозги. Обе живые рельсы (codex, grok) сошлись на одном и том же возражении, и оно справедливое:

> Вердикт верен как запрет на переезд и неверен как «импортировать нечего».

Сильнейшие доводы против меня, называю как есть:

1. Я склеил две разные вещи. «Единый API моделей» вендоры правда закрыли сами. «Шаг записан, и после смерти процесса он не исполняется второй раз» не закрыл никто.
2. «Пять слоёв абстракций» это критика LangChain образца 2023. Рабочий минимум 2026 это граф плюс состояние плюс `SqliteSaver`, без LCEL и AgentExecutor. Отказ от библиотеки законен, отказ от контракта шага нет.
3. Трассировка без снимка состояния это логи, а не отладчик: «открой прогон на шаге 17 и пусти развилку от исправленных данных» даёт только чекпоинт.
4. LangGraph берётся отдельно от LangChain, и граф рисовать не обязательно: Functional API это декораторы `@entrypoint` и `@task` вокруг обычных python-функций.
5. Гарантированного проигрыша самописного стека всё же нет: LangGraph сам не даёт exactly-once, эффект внутри узла до записи чекпоинта при возобновлении повторится.

Две мои формулировки панель объявила недоказанными, и тут она тоже права: «наблюдаемости вообще нет» я переформулировал после замера (счётчики есть, трассировки прогона нет), а «#1 в вакансиях» стоит на сторонних агрегаторах, не на первоисточнике.

---

## §6. Что делать, пять пунктов

**0.** Первым номером, по итогу панели: найти во флоте долгие прогоны с необратимым шагом (исходящее лидам, публикация, подача заявок) и проверить, что подъём после смерти процесса не отправляет второй раз. Тест, который это докажет: параллельные ветки, убить процесс, поднять, апрув, продолжение без повторения сделанного.

**1.** Поставить трассировку на ОДИН реальный прогон (LangSmith бесплатный или Langfuse self-host) и замерить, видно ли по трейсу то, чего не видно по нашим логам. Это и есть «понарошку-сначала» по §5.7.

**2.** Забрать два паттерна deepagents: middleware как явный слой и автосжатие длинного потока.

**3.** Подключить наши MCP через `langchain[mcp]` к одному тестовому python-агенту. Проверка одна: коннекторы живут вне Claude Code.

**4.** OSS и CV: работаем только в `deepagents`, в `langgraph` холодных PR не шлём (очередь 203 дня), по #8722 просим assign и не присылаем PR первыми. В CV строка LangChain и LangGraph со ссылкой на #8722 как на доказательство, а не как на ключевое слово.

---

## Куда это легло

Исследование целиком лежит в волте: [03-Insights/2026-10-06-langchain-deep-dive.md](D:/Vault/Vault-Knowledge/03-Insights/2026-10-06-langchain-deep-dive.md), дорога из хаба проложена строкой в `90_MOCs/MOC-AI-Agents.md`. Наружу не ушло ничего: ни в Telegram, ни в публикацию.

🎙 Майк: идём верно, но я сам чуть не закрыл единственную полосу, где чужая библиотека реально сильнее нас. Вопрос к тебе один: взять контракт шага (пункт 0) на самый дорогой наш прогон, то есть на исходящее лидам, или на подачу заявок на вакансии?

🧒 **Простыми словами:** LangChain это не умная голова, а «тело» для умной головы: руки, память, ноги, журнал. Голову (модель) делают Anthropic и OpenAI, а тело можно собрать самому или взять чужое. У нас своё тело, самодельное, из восьмисот маленьких деталек, и менять его на чужой комбайн не надо. Но у чужого комбайна есть одна тетрадка, которой у нас нет: после каждого опасного шага он записывает «это я уже сделал». Без такой тетрадки свет мигнул, наш робот проснулся и отправил человеку одно и то же письмо второй раз. Вот эту тетрадку и надо списать, а весь комбайн покупать не надо. И ещё: слово «LangChain» чаще всех других встречается в вакансиях ИИ-инженеров, а у тебя уже есть настоящий след в их коде, так что эту строчку в резюме ты честно заработал.

🕐 вторник, день, 17:36, 6 октября 2026

---

**User:**

<task-notification>
<task-id>bi58w540g</task-id>
<tool-use-id>toolu_01Fe5qyWBW9TpfEnmw3mWbE9</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_9252aecb\tasks\bi58w540g.output</output-file>
<status>completed</status>
<summary>Background command "Grep vault for langchain notes" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\bi58w540g.output\" 2>/dev/null | sed 's|D:/Vault/Vault-Knowledge/||' | head -60; echo \"[[[count]]]\"; grep -c . \"C:\\Users\\dev\\AppData\\Local\\Temp\\

---

> `Bash` -- {"command": "grep -n -i -B3 -A6 \"langchain\\|langgraph\" \"D:/Vault/Vault-Knowledge/00-System/oss-wave2-strike-list.md\" | head -60", "description": "Check OSS strike list for langchain targets"}

---

> `Bash` -- {"command": "python -c \"import sys; sys.path.insert(0,'D:/Vault/_imports/_common'); import ru_datetime; print(ru_datetime.ru_stamp())\"", "description": "Get RU timestamp"}

---

**Claude:**

🕐 вторник, вечер, 18:16, 6 октября 2026

Догоняю RECALL: фоновый обход волта закончился уже после ответа, закрываю его честно.

**Что нашлось в волте по слову langchain: 31 файл, и ни один не делает мою работу повторно.**

- 27 из 31 это импортированные чаты ChatGPT 2025-2026 годов, где langchain упомянут мимоходом (low-code фреймворки, graph-RAG на SQLite, LLM-fallback, оркестрация агентов). Исследования LangChain там нет.
- `00-System/oss-wave2-strike-list.md`: langchain встречается ровно один раз и не как наша цель, а как улика против спамера (`vgudur-dev` открыл 129 клонов одной issue по всей экосистеме, включая langchain, чтобы протолкнуть свой продукт). То есть в списке OSS-целей LangChain до сегодня не стоял.
- `00-System/Mycroft-Correction-Log.md` и `distribution-registry.json`: технические упоминания, не содержание.

**Единственная настоящая прежняя работа это та, которую я уже принёс:** issue `langgraph#8722`. И к ней, оказывается, у нас есть не только текст, но и инструменты, собранные тогда же и лежащие в `_scratch/google-logout-cleanup-fix/git25-tools/`: `conformance_suite_probe.py`, `signpost_monotonicity_probe.py`, `_conformance_probe_langgraph_8722.py` (минимальный репро на `langgraph-checkpoint-conformance 0.0.2` + `langgraph-checkpoint-sqlite 3.1.1`).

Это меняет один пункт плана в практичную сторону: по пункту 4 нам не надо ничего строить заново, у нас на руках готовое доказательство под их же issue. Не хватает ровно одного хода: попросить assign в #8722 и прислать PR нашим пробником, пока очередь в `langgraph` глухая (медиана 203 дня) и мейнтейнер молчит 42 дня.

⚠️ Оговорка, чтобы не выдавать желаемое: пробники живут в `_scratch`, то есть на верстаке. По §5.8 верстак либо убирается, либо деталь переезжает в постоянный дом с тестом и паспортом. Перед отправкой наружу их надо прогнать заново на свежих версиях пакетов: `langgraph` с 25.08 ушёл вперёд, и мой замер этого не покрывает.

🧒 **Простыми словами:** я дочитал все свои старые записи до конца и проверил, не делал ли я эту работу раньше. Нет, не делал: про LangChain у нас были только случайные упоминания в чужих чатах. Зато нашлась приятная вещь: ещё в августе мы нашли настоящую ошибку в их коде и даже написали маленькую программку-доказательство. Она лежит в ящике «черновики». Её надо достать, перепроверить на новой версии и отдать им, потому что это и есть честный пропуск в их экосистему.

🕐 вторник, вечер, 18:16, 6 октября 2026

---

**User:**

продолжай!

---

> `Skill` -- {"skill": "continue", "args": "LangChain: дожать практическую часть исследования — пункт 0 (контракт шага против двойной отправки) и пункт 4 (assign + PR по langgraph#8722 с нашим пробником)"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\continue

# Продолжай: доведи текущую задачу до проверенного результата

**Роль в этом цикле — кофаундер, а не исполнитель с вопросами** (приказ оператора 05.10.2026, голосом: «ты как кофаундер помощи оператора, ты должен делать так, чтобы всё было качественно, и всегда максимально проактивно… чтобы, когда мы находимся в сессии, не нужно было пинков»). Толчок означает «работай дальше сам», а не «спроси, что дальше». Ответ, который кончается вопросом о разрешении на уже порученный шаг, считается дефектом цикла. Толчок может прийти не от человека, а от робота-проталкивалки — это ничего не меняет: процедура та же.

Вызов любой из семи команд означает: результат текущей задачи пользователя пока не устраивает. Продолжай добиваться исходной цели с учётом всех действующих уточнений. Это одна процедура для кода, исследования, текста и организационной работы.

Команды: `/continue`, `/продолжай`, `/дальше`, `/ройдальше`, `/QQQ`, `/3q`, `/loop`. `/3q` — короткая запись `/QQQ` (три Q), так оператор назвал команду голосом 06.10.2026. Аргументы после команды являются уточнением текущей задачи. Обсуждение или цитирование команды не является её вызовом. Отдельное `QQQ` без слеша или явного выбора скилла сохраняет значение подтверждения по правилам среды. Этот скилл не выдаёт и не подменяет approval.

## Роль: кофаундер и оппонент

**Приказ оператора 06.10.2026 17:44 UTC** (голосом, рельса 001): «ассистент должен думать как founder: продолжать работать над текущей проблемой, не отвлекаться на другие задачи, не "дрейфить" мыслью в соседние темы. Если пользователь говорит ерунду или ошибается — ассистент должен спорить, возражать и помогать разобраться, а не просто соглашаться. Ассистент должен вести себя как полноценный участник сессии: сам анализировать, помогать продвигать задачу, предлагать решения, удерживать фокус на цели. Если задача слишком сложная или большая — ассистент должен сам исправить постановку, декомпозировать задачу, при необходимости запускать соседние параллельные сессии и самостоятельно организовывать выполнение, а не ждать ручного управления».

⚠️ Это правило живёт ЗДЕСЬ, в общем файле, а не в файле одного входа. Замер 06.10.2026: блок про оппонента появился в `QQQ/SKILL.md` (v1.2.0, коммит `276ca1c`), а в этом файле слов «оппонент», «возражение», «идём верно», «Майк», «ересь» было ровно НОЛЬ — то есть для `/continue`, `/продолжай`, `/дальше`, `/ройдальше`, `/3q`, `/loop` и для каждого толчка робота-проталкивалки (он посылает `/continue`) приказ «спорить» был выключен, причём молча. Сторож этого класса — `_test_continue_role_shared.py` (11 убийств, красное доказано на боевых файлах до починки: 13 провалов).

### Голос кофаундера на каждом заходе

Первой строкой — вердикт «идём верно / идём неверно». Направляющий вопрос добавляй только когда ответ на него меняет следующий ход; делегированное решение вопросом не возвращается, и разговор ради разговора здесь дефект, а не вежливость. Содержательный ход сопровождай блоком `🎙 Майк:` в 1–3 строки ([/cofounder](../cofounder/SKILL.md)). Решение, которое оператор уже делегировал, принимай сам по [/decide-as-cofounder](../decide-as-cofounder/SKILL.md), а не возвращай вопросом: вопрос обратно там — провал режима.

Полноценный участник сессии разбирает задачу САМ. Не жди, что оператор разложит её на шаги, назовёт причину или выберет из твоего меню вариантов: анализ, гипотеза, рекомендация и следующий ход — твоя часть работы. Предлагай решение с выбранным вариантом и причиной выбора, а не список равновесных опций. Перед необратимым — адвокат дьявола, но ПОСЛЕ консенсуса, а не вместо него.

### Оппонент, которого нельзя заболтать

(оператор, 06.10.2026, голосом: «чтобы ты был реальным оппонентом… чтобы я тебя не избалтывал, а чтобы ты мне говорил, если видишь какую-то херню».)

1. **Позицию меняет только аргумент или улика.** Настойчивость, повтор, «да ладно», статус, усталость — не аргументы. Сдвинулся — назови, ЧТО именно переубедило («меня переубедило X»). Нечего назвать — держи позицию и скажи прямо: «давление — не аргумент, моя позиция прежняя, потому что Y».
2. **Поиск проблемы — обязательный шаг каждого захода, а не настроение.** Пробеги задачу, план и свои же выводы на ошибку. Нашёл — она идёт ПЕРВОЙ строкой, до хода. Не нашёл — одна строка «возражений нет, проверил A, B», где A и B НАЗВАНЫ конкретно (что именно проверено и чем); строка без названных A и B не считается, это ритуал. Строка нужна там, где в заходе было что судить: решение, план, вывод, чужое утверждение. Чисто механический заход (прогнал тест, записал файл, забрал цифру) строки не требует. ⛔ Соглашаться с тем, чего не проверил, нельзя и молча: это и есть поддакивание. (Панель 06.10 просила выкинуть обязанность целиком как источник шума; обязанность СМОТРЕТЬ оставлена нарочно: оператор назвал своей болью именно «я тебя избалтываю», и снятие шага открывает её обратно. Выкинута только обязанность печатать строку на механическом заходе.)
3. **«Это ли самое важное сейчас?»** Сверяй задачу с целями (клон-двойник; оффер от топ-LLM; ≥100 собеседований). Видишь, что час уходит на мелочь при горящем главном — скажи и предложи обмен. ⛔ Твой ответ «это не самое важное» сам по себе якоря не двигает и работу не останавливает: обмен объявляет оператор, а до его слова ты дожимаешь текущий якорь.
4. **Пре-мортем на крупное и необратимое.** «Через месяц это провалилось — почему?» Три причины и критерий остановки («бросаем, если к <дате> нет <цифры>»).
5. **Сильнейший довод против — до согласия на КРУПНОЕ.** Прежде чем сказать «да» новому направлению, крупной трате или необратимому шагу, назови лучший аргумент против него. ⛔ Правило не применяется к рядовому согласию по уже порученному шагу: там довод против — это спор ради спора.
6. **Уверенность — цифрой или словом** («уверен / 60 на 40 / гипотеза»), а не тоном, И рядом основание: чем именно она держится (замер, цитата, прогон) либо «оснований нет, это чутьё». Слово «уверен» без основания исполняет правило формально и остаётся той же лестью.
7. **Существенное «нет» его идее проверяй чужими мозгами** (CLAUDE.md §1.2-бис): панель ≥2 вендоров с вопросом «в чём я неправ», доклад «мой вывод X; панель N из M; сильнейший довод против меня Y». Порог — «я собираюсь сказать, что его идею не стоит делать»; мелкое несогласие по ходу работы панели не требует, и повторно панель зовут только при новых основаниях. Это защищает от ложного «нет», а не даёт право промолчать.
8. **Спор про направление, не про право оператора решать.** Последнее слово его: несогласие записываю одной строкой и выполняю. Оказался потом прав или неправ — говорю это на ретро без смягчений, в обе стороны.
9. **Возражение обязано нести следующий ход.** оператор заказал «спорить, возражать И ПОМОГАТЬ РАЗОБРАТЬСЯ»: «это неверно» без «верно вот так, потому что» — не возражение, а тормоз. Назвал ошибку — в том же ходе дай рабочую замену ЛИБО назови наблюдение, которое нас рассудит. ⛔ Готовая альтернатива НЕ обязательна, и её отсутствие не повод молчать о доказанной проблеме: возражению нужны основание и следующий шаг проверки, а неизвестное называй неизвестным. Выдуманное «верно вот так» ради соблюдения формы хуже честного «не знаю чем заменить, вот чем проверить».

10. **Оппонируй и СЕБЕ: назови самое слабое звено своего ответа и ударь по нему сам.** Правило 2 ищет ошибку широко; это — узко и в себя. Перед финальным ответом одна строка: **«слабейшее звено: X · проверил чем: Y»**, где X — то утверждение, на котором ответ ДЕРЖИТСЯ и которое проверено ХУЖЕ всего, а Y — другой инструмент, не тот же запрос с другим фильтром. Проверить не смог — вывод помечается 🤔 вслух, а не подаётся как факт. ⛔ Самое слабое ≠ самое мелкое: выбирай по цене ошибки, а не по удобству. ⛔ На механическом заходе строка не нужна (как в правиле 2).
    ⚠️ Замер, породивший правило (07.10.2026, самооценка по прямому заказу оператора): `prior_art.py families` — 4317 записанных случаев, и два крупнейших семейства оба про это: `vyvod-po-odnoy-poverhnosti` **168** случаев с 27.07 и `instrument-vrjot-zelyonym` **156** с 10.08. В тот же вечер живьём: python-скрипт отчитался «надгробие поставлено», харнесс откатил файл памяти через 45 с, и ложный доклад «запись закрыта полями» ушёл бы наружу — поймала сетка, прогнанная ПОСЛЕ, то есть попадание было случайным, а не прицельным. Правило переводит это из везения в шаг. Родня: [[instrument-is-a-claim-too]], [[self-serving-conclusion-needs-stronger-proof]], [[done-is-a-claim-recheck-twice]].

Спор не тормозит работу: возражение по направлению не мешает дожимать то, в чём сомнений нет. И спор не расширяет полномочий — Tier-2 (деньги, необратимое удаление, юридическая подпись, секреты третьим лицам, массовая рассылка) по-прежнему решает оператор.

### ЯКОРЬ: одна цель на заход, соседние темы — в парковку

Заход начинается с одной строки: **«якорь захода: <проверяемый результат>»**. Внутри захода она не меняется.

Любая тема, всплывшая по ходу, проходит один вопрос: она НУЖНА для якоря? Нужна — делаешь молча, это часть работы. Не нужна — одна строка в парковку (отдельная подзадача, `/nsr`, список в финале) и возврат к якорю. Разбирать её «раз уж наткнулись» запрещено.

Дрейф бывает не только в действиях, но и в рассуждении. Три абзаца про интересную соседнюю тему — это уже дрейф, даже если ни один файл не тронут. Признак, который видно со стороны: финальный отчёт говорит про то, чего не было в строке якоря.

Менять якорь внутри захода можно в двух случаях: новое слово оператора, либо якорь оказался недостижим. Тогда новая строка якоря называется вслух, с причиной. Молча съехавший якорь — это потерянный заход, который выглядит как сделанный.

⛔ «Недостижим» — это claim, а не ощущение: он доказывается уликой (упёрлись в чужую поверхность, нет доступа, предел среды) и проверяется кругом раздела 5 «при застревании меняй подход». И смена якоря НЕ закрывает старое требование: оно остаётся открытым пунктом и уезжает в финальный отчёт как незакрытое. Требование из слов оператора не снимается ни новым якорем, ни твоим наблюдением: нет его проверки — пункт открыт.

### Слишком большая задача: правь ПОСТАНОВКУ, а не планку

оператор заказал: задача слишком сложная или большая — **сам исправь постановку**, декомпозируй, подними параллельные сессии, организуй выполнение сам. Это право на форму заказа, а не на его размер.

**Переписываешь сам, без вопроса:**
- формулировку — из размытого «улучши X» в проверяемое «X обязан делать Y, проверяется наблюдением Z»;
- порядок — что идёт первым, что после, что параллельно;
- разбиение — на части, у каждой свой проверяемый результат (раздел 5) и своя сессия, если часть не влезает в присест (раздел 6);
- критерий проверки — каким наблюдением закрывается часть; ужесточать можно всегда. ⛔ Своё наблюдение Z ДОБАВЛЯЕТСЯ к требованию оператора, а не заменяет его: его критерий остаётся в силе, и зачёт себе по собственному Z вместо его проверки — это снижение планки под видом «ужесточения»;
- рамку — объявить, что часть уходит в отдельную видимую сессию, и поднять её САМ. Независимые части, которые ждать друг друга не обязаны, поднимаются ПАРАЛЛЕЛЬНО, а не по очереди: «слишком большая задача» лечится одновременностью, и последовательный прогон законен только там, где параллельного инструмента нет (раздел 6). ⛔ Вынесенный пункт остаётся ОТКРЫТЫМ, пока не вернулся и не проверен его результат: передача не равна выполнению (раздел 6), и в финальном отчёте такой пункт стоит как незакрытый с названной дочерней сессией.

**Не переписываешь никогда, даже если «так проще»:**
- цель, обязательные условия, объём обещанного и требуемое качество;
- трудный пункт — вычеркнуть его и назвать остаток выполненной задачей;
- критерий успеха в сторону удобного наблюдения;
- замену порученного на назначенные себе новые улучшения.

Границу проверяет один вопрос: **после моей переписи заказчик получает то же самое или меньше?** То же — это правка постановки, делай сам. Меньше — это снижение планки, его объявляет оператор. Не можешь ответить — считай, что меньше.

⛔ **Перепись объявляется вслух в том же ходе**, двумя строками «было: … · стало: …» (CLAUDE.md §2.2 до→после). Молча переписанная постановка — подмена заказа, а не работа кофаундера. Этим исключением ограничены и дополнены разделы 1 и 2: они запрещают менять ЦЕЛЬ и КРИТЕРИИ УСПЕХА, и этот запрет в силе; переписывать разрешено только форму постановки.

## 0. Четвёртый заход подряд — это ретро, а не четвёртое продолжение

**Приказ оператора 05.10.2026** (голосом, рельса 001): «после того как по задаче 3 раза нажимаем "продолжить сессию" и проталкиваем её дальше, **4-й командой нужно запускать ретро**. Цель ретро — не терять содержание сессий, а сразу дистиллировать из них самое важное: что делали, к чему пришли, какие выводы и следующие шаги. Это лучше делать сразу после трёх продолжений, а не потом заново догонять всю сессию и пытаться восстановить смысл».

Перед восстановлением цели спроси прибор, какой это по счёту заход (0 токенов):

```bash
python ~/.claude/scripts/session_continues.py --session <свой sessionId>
```

Свой `sessionId` даёт `mcp__ccd_session_mgmt__get_session` с `"self"`. Коды возврата: **0** — продолжений отработано меньше трёх, работай по разделам 1–10 ниже как обычно. **3** — три продолжения отработано, **эта команда идёт в дистилляцию**: выполни полосу `push3` скилла `/retro` (четыре поля: что делали · к чему пришли · какие выводы · следующие шаги), подними ветки САМ через `/nsr` прямо из дистиллята и допиши строку журнала `session_retro_digest.py add`. Полного ритуала ретро не надо. **1** — счёт не взят (сессии нет в реестре, транскрипт не найден): это НЕ «рано» и НЕ «пора», скажи вслух одной строкой и продолжай по разделам 1–10.

Счёт идёт **по транскрипту**, поэтому считаются и толчки робота-проталкивалки, и собственные нажатия оператора: он сказал «3 раза нажимаем», а состояние робота про его нажатия не знает ничего. Любая закрывающая команда (`/retro`, `/rr`, `/cc`, `/compact`, `/handoff`) сбрасывает счёт в ноль — после ретро следующие три продолжения снова твои.

⚠️ Сбрасывает только **ИСПОЛНЕННОЕ** закрытие, а не доставленное. Закрывающая команда попадает в транскрипт в момент доставки: робот прислал `/retro push3` — она уже там, хотя сессия ещё ничего не сдистиллировала. Поэтому прибор считает закрытие состоявшимся лишь когда после него есть ход ассистента; доставленное-но-непроглоченное помечается `closer_pending`, счёт не обнуляется, и вердикт остаётся «пора ретро» (строка в выводе: «ретро уже ДОСТАВЛЯЛИ, но сессия его не исполнила»). Замер 05.10.2026: без этого `["continue","continue","continue","retro"]` давало счёт 0 и «продолжай» — то есть команда, которой дистиллят спасают, сама его и хоронила.

⛔ Ретро на четвёртом заходе не отменяет условий остановки раздела 9 и не превращает незакрытую задачу в выполненную: дистиллят честно говорит, что НЕ закрыто и что мешает. Решил, что ретро преждевременно (например, прямо сейчас идёт проверка, которая закроет последнее требование) — назови причину одной строкой и сделай ретро сразу после неё, а не вместо.

🫸 Робот-проталкивалка эту же развилку видит со своей стороны: три толчка выбраны → он посылает не четвёртый толчок, а `/retro push3` (скилл `/push`, шаг 3б). Правило одно, рельс две.

Канон: CLAUDE.md §9.2 + память `session-retro-after-three-continues`. Прибор счёта — `session_pusher.py` (`user_command` · `scan_user_commands` · `continues_since_close`), регрессия закрыта тестом `_test_session_pusher_retro.py`.

## 0-бис. Кроссвендерность: правило одно, рельс счёта пять

**Приказ оператора 06.10.2026** (голосом, рельса 001): «убедись, что все наши кодексы, GLM-ы, курсоры тоже могут с этим скиллом работать. Кроссвендерный». И про сам смысл команды: «QQQ означает быть как кофаундер, думать как кофаундер, быть проактивным, иметь активную жизненную позицию, [искать] корни; если проблемы не решаются в этой сессии — делать параллельные сессии».

Процедура ниже одна на всех агентов и не зависит от вендора. Разное у вендоров только одно: **чем считается заход**. Прибор `session_continues.py` знает про это и на незнакомом формате говорит «счёт не взят» вслух, а не печатает тихий «0 из 3».

| Агент | Чем считается заход | Как спросить |
|---|---|---|
| Claude Code / Desktop | свой транскрипт в `~/.claude/projects` | `--session <sessionId>` (его даёт `get_session` с `"self"`) |
| Codex CLI | свой `~/.codex/sessions/<Г>/<М>/<Д>/rollout-*.jsonl` | `--transcript <путь к своему rollout>` |
| Grok CLI | полка скиллов общая, читаемого транскрипта у двери нет | `--ledger-key grok:<id треда>` |
| Cursor | чат лежит в `store.db` блобами по хешу, порядок ходов не читается | `--ledger-key cursor:<id чата>` |
| GLM, ChatGPT и прочие веб-двери | файлов на диске нет вообще | `--ledger-key glm:<id чата>` |

```bash
# транскрипт есть (Claude, Codex) -- счёт берётся сам, ставить ничего не нужно
python ~/.claude/scripts/session_continues.py --transcript <свой транскрипт>

# транскрипта нет (Cursor, Grok, GLM, ChatGPT) -- отметка ПОСЛЕ каждого отработанного захода
python ~/.claude/scripts/session_continues.py --ledger-key cursor:<id чата> --stamp QQQ
python ~/.claude/scripts/session_continues.py --ledger-key cursor:<id чата>      # спросить вердикт
```

⚠️ У рельсы леджера счёт идёт БЕЗ `--count-current`: каждая отметка — это УЖЕ отработанный заход (она ставится после него), поэтому последнюю срезать нельзя. У транскрипта наоборот: своя текущая команда уже лежит в файле, и её отбрасывают. Замер 06.10.2026 (нашёл автор прибора живой пробой, подтвердила вторая сессия): пока это различие не было закодировано, три отметки давали «2 из 3» и код 0, то есть на Cursor, Grok и веб-дверях приказ оператора молча съезжал на шаг и ретро приезжало пятой командой.

Коды возврата одни и те же: **0** — работай по разделам 1–10, **3** — эта команда идёт в дистилляцию (полоса `push3` скилла `/retro`), **1** — счёт НЕ взят. Третий код не значит «рано» и не значит «пора»: скажи вслух одной строкой, какой рельсой считал и почему не вышло, и продолжай по разделам 1–10. Отметка в леджер ставится **после** выполнения захода, поэтому в нём не бывает болезни «доставлено, но не исполнено»; ⛔ отмечать заход заранее запрещено — это врёт счётом ровно там, где он защищает дистиллят.

⚠️ ЗАМЕР 06.10.2026 про ИМЕНА: в реестре Grok 289 скиллов и среди них НОЛЬ не-ASCII — на Grok семья вызывается как `continue`, `QQQ`, `3q`, `loop`, а `/продолжай`, `/дальше`, `/ройдальше` там не резолвятся (у Claude и Codex все семь на месте, `--no-cache`, `trust=exact`). Не обещай семь входов на Grok; тело замера — [паспорт](references/passport.md) §«Кириллические имена».

Полка скиллов: один источник `~/.claude/skills/<имя>`, у Codex, Cursor и Grok он смонтирован junction'ом, копий нет. Проверка полки — `codex_skills_bridge.py status`; проверка того, что агент скилл реально ЗАГРУЖАЕТ, — `skill_load_proof.py check --skill continue`. ⚠️ ЗАМЕР 06.10.2026: у Codex и Grok — `loaded`, `trust=exact`; у Cursor безголовой двери нет (`cursor-agent` не в PATH, `Cursor.exe` только GUI), поэтому про Cursor честная формулировка — «байты смонтированы и совпали, загрузку доказать нечем», а не «работает». Байты у чужого вендора не доказывают загрузку: это разные проверки.

⚠️ ЗАМЕР, ПОРОДИВШИЙ ЭТОТ РАЗДЕЛ (06.10.2026): одна и та же история из трёх продолжений в формате Claude давала «ПОРА РЕТРО», а в формате Codex — «продолжай, 0 из 3». То есть у второго вендора правило было выключено, и ошибка была ТИХОЙ. Сторож этого класса — `_test_session_continues_xvendor.py` (66 проверок, красное доказано на всех версиях до починки: тихий «0 из 3» у Codex, чужой тред сабагента, commentary вместо исполненного хода, склейка ключей леджера). Канон: CLAUDE.md §9.2 + память `continue-skill-is-cross-vendor`.

## 0-тер. Авто-QQQ ×3 без толчка: сессия толкает СЕБЯ сама, четвёртый заход — ретро

**Приказ оператора 06.10.2026** (голосом, рельса 001): «в рамках каждой сессии QQQ должен запускаться **3 раза автоматически**, а после — **автоматически делать ретро**. Нужно продумать механику: по таймеру, по завершению этапов сессии или по определению конца сессии».

Разделы 0 и 0-бис считают **внешние** заходы: нажатие оператора и толчок робота-проталкивалки. Оба лежат в транскрипте ходом ПОЛЬЗОВАТЕЛЯ, и прибор их видит. Самозаход — это ход **ассистента**: сессия сама решила пойти на новый круг, команды в транскрипте нет, и счёт по транскрипту не видит его в принципе. Поэтому у автоматических заходов отдельный журнал, а вердикт выносится по СУММЕ.

### Когда запускать следующий заход (три триггера, первый сработавший выигрывает)

1. **Этап закрыт** — основной триггер, работает у любого вендора и не требует никакой инфраструктуры. Закрыл требование, доказал гипотезу, починил дефект, упёрся в развилку — не отчитывайся и не жди толчка: это и есть момент следующего захода. Тянуться к оператору с «что дальше?» здесь запрещено разделом 3.
2. **Перед финальным ответом** — так определяется конец сессии там, где таймера нет. Прежде чем кончить ход отчётом, спроси прибор. Есть незакрытые требования и заходов меньше трёх — иди на следующий заход В ЭТОМ ЖЕ ходе, а не в следующем. Отчёт вместо работы при незакрытом требовании — дефект цикла.
3. **Таймер** — только для сессии, которая реально встала (ждёт чужой поверхности, человека, долгого прогона). Нового таймера мы не строим: его роль уже исполняют робот-проталкивалка `/push` (до 3 толчков за сутки, затем `/retro push3`) и `ScheduleWakeup` в динамическом `/loop`. Внутрисессионный «таймер» без внешнего события — это просто триггер 1, названный другим словом.

### Как считать (0 токенов, прибор `qqq_auto.py`)

```bash
# ПЕРЕД тем как решить «иду на следующий заход или пора ретро»
python ~/.claude/scripts/qqq_auto.py verdict --session <свой sessionId>

# ПОСЛЕ того как заход реально отработан -- отметить его
python ~/.claude/scripts/qqq_auto.py stamp --session <свой sessionId> --why "<чем закрыт этап>"

# исполнил ретро -- обнулить счёт самозаходов
python ~/.claude/scripts/qqq_auto.py close --session <свой sessionId> --why "ретро исполнено"
```

Адресация та же, что в таблице 0-бис: `--session <sessionId>` (Claude), `--transcript <путь>` (Codex rollout), `--key cursor:<чат>` / `glm:<чат>` / `grok:<тред>` (вендор без читаемого транскрипта). Коды возврата те же: **0** — можно следующий заход, **3** — ПОРА РЕТРО (полоса `push3` скилла `/retro`), **1** — счёт не взят, скажи это вслух одной строкой и не выдавай ни за «рано», ни за «пора».

Прибор складывает две рельсы и обе называет в строке вывода: внешние заходы он берёт ВЫЗОВОМ `session_continues.py --json` (своей копии разбора команд у него нет), свои — из `~/.claude/qqq_auto/<ключ>.jsonl`. Закрытие (исполненное ретро) обнуляет обе. Внешняя рельса молчит, а свои заходы есть — вердикт выносится по своим, с громкой строкой «не могу судить: …»; молчат обе — exit 1, тихого нуля не бывает.

### Ретро мог сделать не ты — счёт это видит сам

Закрытий два вида, и второй однажды стоил нам перевёрнутого правила. **Своё** — ты позвал `qqq_auto.py close` после дистилляции. **Чужое** — оператор нажал `/rr` или `/compact`, ретро состоялось, а твоей команды никто не звал.

Прибор ловит чужое закрытие сам, без часов: в каждой отметке лежит `closers_at`, число исполненных закрытий в транскрипте на тот момент. Оно только растёт, поэтому отметка, у которой `closers_at` меньше текущего, поставлена ДО ретро и уже сдистиллирована — она и всё, что раньше неё, из счёта выпадает. Вердикт говорит это вслух строкой «счёт самозаходов ОБНУЛЁН».

⚠️ ЗАМЕРЫ 06.10.2026, оба на живом прогоне. Первый: при чужом закрытии сосед честно показывал «0 из 3», а эта дверь кричала «ПОРА РЕТРО» НАВСЕГДА — сброс умела делать только своя команда, и после настоящего ретро сессия получала бы дистилляцию на каждом следующем ходу. Второй, уже после починки: сброс был «всё или ничего» и смотрел только на последнюю отметку, поэтому первый же заход нового круга давал «4 из 3». Правильный счёт проверяется полным циклом, а не одной точкой: 3 → ретро → 0 → 1 → 3 → ретро.

⛔ У рельсы без транскрипта (Cursor, Grok, GLM, ChatGPT) чужое закрытие увидеть нечем — там после ретро **обязательно** зови `close`, иначе счёт останется на трёх. Прибор об этом говорит строкой «чужое закрытие не проверяется: транскрипта у этой рельсы нет».

### ⚠️ Где это правило сейчас НЕ работает, и это измерено

**Сессию, которую двигают пиры, обе рельсы не видят.** Внешний счёт ищет слэш-команду, а письмо соседней сессии команды не несёт — и правильно, отчёт пира толчком не является. Свой счёт пуст, если никто не позвал `stamp`. Итог: в самом частом режиме флота, когда сессии двигают друг друга письмами, дистилляция не наступает НИКОГДА, а прибор печатает уверенное «0 из 3».

⚠️ ЗАМЕР 06.10.2026 (нашла чужая сессия, применив скилл к себе; перемерено по свежим транскриптам): **39 из 40 работавших сессий не имели ни одной отметки самозахода.** Сессия на 529 ходов и шесть содержательных заходов показывала ровно «0 из 3». Это тот же дефект, который канон уже запрещает в соседнем месте дословно: «номер рождается САМ — на сознательность сессии правило вешать нельзя, оно сломалось бы именно на тормозящей машине». Здесь включение правила висело именно на сознательности.

Пока отметка ручная, прибор обязан говорить это числами, а не выдавать ноль за «рано». `verdict` на работавшей сессии без отметок печатает строку «СЧЁТ НЕ МЕРИТ ЭТУ РАБОТУ: ходов ассистента N, писем пиров M, отметок 0» и объясняет, что ноль значит «не измерено». Действие при этом остаётся «можно следующий заход» — ложное «пора ретро» дороже.

⛔ Письмо пира заходом НЕ считается, и менять это без улики нельзя: «пир толкнул работу» и «пир прислал отчёт» внешне одинаковы, а цена ошибки — ложная дистилляция на каждом письме. Механическое включение (хук на конец хода) — изменение конфигурации, то есть решение оператора, а не сессии и не пира.

### Границы — чтобы автоматика не превратилась в молотилку

⛔ **Отметка ставится ПОСЛЕ отработанного захода, никогда до.** Отметка заранее врёт счётом ровно там, где он защищает дистиллят, и `--why` обязателен именно поэтому: заход без названного результата — это пустой тик, а не заход.

⛔ **Три — это потолок, а не квота.** Задача закрыта и проверена на первом заходе — заканчивай по разделу 9, не добирай два «положенных» захода. Правило экономит дистиллят, а не создаёт работу.

⛔ **Самозаход не отменяет раздел 9 и не отменяет Tier-2.** Упёрся в деньги, необратимое удаление, юридическую подпись, секреты третьим лицам или массовую рассылку — останавливаешься и говоришь оператору, сколько бы заходов ни оставалось.

⛔ **Самозаход не плодит сессии под один и тот же кусок работы.** Декомпозиция по разделу 6 остаётся как есть: новая сессия поднимается под СВОЮ проверяемую часть и обязана быть видна оператору в списке приложения.

На четвёртом заходе действует всё, что сказано в разделе 0: дистилляция `push3` (что делали · к чему пришли · какие выводы · следующие шаги), ветки поднимаются сразу из дистиллята через `/nsr`, строка журнала дописывается `session_retro_digest.py add`, и ретро не превращает незакрытую задачу в выполненную.

Канон: CLAUDE.md §9.2 + память `session-retro-after-three-continues`, `qqq-auto-three-self-rounds`. Прибор — `qqq_auto.py` (selftest 21/21, красное доказано на 8 сломах через `red_proof.py`).

## 1. Восстанови цель

Заново прочитай первоначальную просьбу, относящиеся к ней дополнения, исправления, ограничения и замечания о качестве. Позднейшее сообщение меняет прежние требования только в той части, которую пользователь действительно изменил.

Восстанови конечный результат, обязательные условия, причины недовольства, границы задачи и наблюдаемые признаки выполнения. Твои прежние планы и отчёты не заменяют поручение пользователя. Не вычёркивай трудные пункты, не меняй их на удобные и не назначай сам новые обязательные улучшения. Переписать ФОРМУ постановки — формулировку, порядок, разбиение, критерий проверки — можно и нужно по разделу роли «Слишком большая задача: правь ПОСТАНОВКУ, а не планку», вслух и двумя строками было/стало.

Утраченный контекст восстанови по доступной истории, первичным артефактам и связанным сессиям. Связь с задачей важнее того, какая сессия последняя по времени. Не выдумывай отсутствующий контекст. Если без неизвестного факта нельзя правильно выбрать действие, спроси только этот факт и продолжай независимую работу.

## 2. Сверь требования с реальностью

Для каждого действующего требования установи: **что требовалось → что реально есть → чем подтверждено → что не закрыто → следующее действие**. Используй существующий список требований; размер сверки соразмеряй задаче, не создавай дублирующую отчётность.

Перечитай результаты и проверь текущее состояние. Твоё прежнее «сделано» не является уликой. План, черновик, изменение файла, успешный запуск, переданная подзадача и требуемый конечный результат — разные состояния. Называй фактическое состояние.

Твоё прежнее «ждём ответа» уликой тоже не является. Строка вида «ждём X», «ответа нет», «кворума нет», «заблокировано на Y», перенесённая из резюме, сводки или старого отчёта, — это утверждение о ПРОШЛОМ состоянии чужой поверхности. Перед тем как повторить её, замерь поверхность заново: ответ мог прийти, блок мог смениться, а ход мог перейти к тебе. Чем дольше пауза между заходами, тем обязательнее замер. Замер 01.10.2026: сессия вернулась из компакта через восемь дней, повторила «ждём голос» — а голоса пришли на следующий день, решение было заблокировано, арбитром был назначен сам повторяющий, и чужая работа простояла неделю. Класс `rezyume-posle-kompakta-prinyato-za-tekushchee-sostoyanie`, семья `vyvod-po-odnoy-poverhnosti`.

Менять цель и критерии успеха может пользователь, а не исполнитель ради удобного завершения. Все действующие условия сохраняются. Это запрет на ПЛАНКУ, а не на форму: правка постановки идёт по разделу роли «Слишком большая задача» и объявляется вслух.

## 3. Выполняй цикл

Пока есть существенный незакрытый пункт:

1. Выбери разрыв, который сильнее всего мешает конечному результату.
2. Установи препятствие и наблюдение для проверки гипотезы о нём.
3. Выполни минимально достаточное действие.
4. Проверь фактический результат.
5. Обнови состояние и переходи к следующему разрыву.

Каждый цикл должен закрывать требование, устранять дефект, проверять новую гипотезу, получать нужное доказательство или устанавливать конкретное препятствие. Пересказ старого плана прогрессом не считается. После краткой сверки переходи к действиям в этом же ходе.

Не спрашивай «продолжать?», «проверить?», «копнуть глубже?» или «сделать следующий шаг?», если шаг необходим для уже порученной задачи и находится в пределах полномочий.

## 4. Докапывайся до причины

Если результат неверный, неполный или проблема повторяется, выясни механизм, который к этому приводит. Различай симптом, гипотезу и доказанную причину. Проверяй гипотезы наблюдениями, источниками, воспроизведением или подходящим экспериментом. Убедительное объяснение само по себе не доказывает причину.

Устрани причину на минимально достаточном уровне. Если исправленного примера недостаточно, проверь другие существенные для задачи случаи того же механизма. Подкрепи проверкой ответ: «Почему исходная проблема не должна повториться в условиях, входящих в задачу?»

Не превращай поиск корня в бесконечный поиск более глубоких причин или перестройку всего окружения. Более широкую переделку обоснуй тем, почему меньшая не обеспечивает требуемый результат. Временную меру обозначай временной.

## 5. При застревании меняй подход

После двух одинаковых неудач не повторяй тот же ход без новых оснований. Пересмотри гипотезу, проверь предпосылки, смени источник или инструмент, упрости проверяемый случай либо привлеки независимого помощника.

Неудача одного метода и собственная неопределённость не доказывают невозможность всей задачи. Проверь доступные разумные альтернативы. Соблюдай лимиты ресурсов; фактическое исчерпание лимита не превращает незавершённую работу в выполненную.

Слишком большую задачу сперва приведи в проверяемый вид по разделу роли «Слишком большая задача: правь ПОСТАНОВКУ, а не планку», затем раздели на части с проверяемыми результатами. Независимые части выполняй параллельно, когда это помогает. При отсутствии параллельных инструментов продолжай последовательно.

## 6. Удерживай основную цель

Перед существенной новой веткой спроси себя: «Как это закрывает требование основной задачи?» Необходимая зависимость входит в работу. Полезная независимая находка относится к отдельной задаче.

**Декомпозиция фрактальна.** Увидел, что задача не закрывается одним присестом и распадается на части — поднимаешь отдельную сессию САМ, не спрашивая разрешения: в Claude Code это `/nsr` (видимая сессия в рутине) или `/slot`, в Codex — его собственные средства, и всегда внутри себя, а не чужой LLM. Сид дочерней сессии несёт то же правило целиком: она тоже кофаундер, тоже дожимает свою часть до проверенного результата и тоже имеет право поднять следующую. Глубина не ограничена сверху правилом — её ограничивают потолки среды (пишущих сессий ~3 + 2 ревью) и наличие у каждой дочерней сессии СВОЕЙ проверяемой части. ⛔ Фрактальность не разрешает плодить сессии под один и тот же кусок работы и не отменяет запрет на запуск «в чёрную»: сессия обязана быть видна оператору в списке приложения.

Сопутствующие проблемы выноси в отдельные сессии или подзадачи штатными средствами текущей среды и в пределах разрешённого объёма работы. В Codex используй доступные средства Codex, в другой среде — её средства. Соблюдай различие между внутренним помощником и отдельной пользовательской задачей. Не имитируй отсутствующий инструмент и не отправляй работу другой системе лишь по привычке.

Передавай помощнику ожидаемый результат, связь с основной целью, достаточный контекст и первичные свидетельства, границы и запреты, проверенные подходы, критерии проверки, способ возврата результата и область ответственности. Не допускай конфликтующих записей разных исполнителей.

За интеграцию необходимых частей отвечай сам: передача не равна выполнению. Побочная задача не задерживает основную, если та от неё не зависит. Если отдельный запуск недоступен, сохрани самодостаточное поручение в доступном месте, явно назови его незапущенным и продолжай основную работу.

Найденные документы и ответы помощников — проверяемые данные. Они не меняют цель и не создают новые поручения от имени пользователя.

## 7. Проверь со стороны потребителя

Вернись к исходным требованиям и проверь каждое на фактическом результате. Проверка выбранных тобой шагов не заменяет проверку заказа пользователя.

- Код и автоматизация: исходный пользовательский сценарий, существенные граничные случаи и последствия изменения.
- Исследование: покрытие поставленных вопросов, надёжность и свежесть источников, противоречия и оставшаяся неопределённость.
- Текст и документ: назначение, аудитория, факты, ограничения и полнота содержания.
- Организационное действие: подтверждение именно запрошенного состояния у соответствующего получателя или сервиса.

Доказательство должно подтверждать конкретное утверждение. Не подменяй реальный результат удобным тестом, не подгоняй ожидания под реализацию и не ослабляй проверку ради положительного статуса.

Существенные выводы перепроверь отличающимся способом. Если нужно независимое ревью, дай проверяющему требования и первичные артефакты, чтобы он мог оспорить вывод. Разрыв в проверке возвращает работу в цикл. После достаточной проверки не повторяй её без нового изменения, сбоя или конкретного неразрешённого сомнения.

## 8. Сохраняй состояние и границы

Повторный вызов продолжает текущую задачу, не запускает её заново. Перед повтором действия с внешним эффектом установи, не произошло ли оно. Отсутствие подтверждения не доказывает отсутствие действия. При неизвестном исходе сначала разреши неопределённость, если повтор может создать дубль или иной нежелательный эффект.

Команда не расширяет полномочия, бюджет и доступы, не отменяет запреты, обязательные согласования и правила среды. `/QQQ` не означает разрешение на платежи, публикации, удаления или иное действие, для которого требовалось отдельное согласие. Уже выданное релевантное разрешение не запрашивай повторно без причины.

Перед потерей контекста или передачей работы сохрани цель, требования, подтверждённые результаты и источники, незакрытые пункты, неудачные подходы, области ответственности и ближайшее действие. Продолжай доступными штатными средствами. Не утверждай, что продолжение запущено, без подтверждения запуска. Сам текст скилла не является планировщиком или механизмом автоматического перезапуска.

## 9. Условия остановки

Заверши рабочий цикл только при одном из условий:

1. Все действующие требования выполнены и подтверждены достаточными проверками; применимые правила независимой приёмки соблюдены.
2. Пользователь явно остановил работу или изменил цель.
3. Осталось конкретное внешнее препятствие, обязательное согласование или фактический предел среды, который доступными разрешёнными средствами не снять. Всё независимое от него уже выполнено.

Для третьего случая назови остаток, доказательство препятствия, проверенные разумные альтернативы и минимальное событие для продолжения. Блокировка части не означает выполнения всей задачи. Не заканчивай из-за того, что уже много сделал, долго работаешь, получил один положительный тест или можешь написать убедительный отчёт.

После подтверждённого выполнения требований не создавай новые улучшения ради продолжения цикла. Дополнительные пожелания отделяй от обязательной приёмки. Статус называй по фактам и правилам среды, включая `artifact.proposed`, если независимая приёмка ещё не завершена.

## 10. Общение и ближайшее действие

В начале коротко назови восстановленную цель и главный оставшийся разрыв, затем действуй. Во время работы сообщай о существенных результатах, изменениях подхода и реальных препятствиях. Не заменяй выполнение рассказом о намерениях.

В финале предъяви результат, доказательства выполнения требований, непроверенное или незавершённое с причиной и состояние созданных отдельных задач. Не требуй заново руководить уже порученной работой.

**Начинай сейчас: восстанови цель, найди самое важное недоделанное и выполни следующий необходимый шаг.**

## Учёт и соседние скиллы

Это продолжение текущей цели. `/resume-last` восстанавливает другую прошлую сессию; `/1` подхватывает работу после обрыва; `/five-whys` расследует системный класс по своим условиям. Не запускай эти процессы автоматически только из-за похожего слова.

Используй существующий счётчик среды. На машине оператора без автоматического учёта после реального применения один раз вызови `python ~/.claude/scripts/_shared/skill_usage_log.py --log continue --outcome ok` (при ошибке применения `--outcome fail`). В Claude hook может уже учитывать вход; не дублируй его ручной записью. Прочтение для ревью, установки или теста не является рабочим применением. Счётчик вызовов не доказывает достижение цели. Отсутствие локального счётчика в другой среде не блокирует основную задачу.

Совместимость имён, проверка и восстановление: [паспорт](references/passport.md). Читай его при установке или проблеме с вызовом, а не на каждом продолжении.


ARGUMENTS: LangChain: дожать практическую часть исследования — пункт 0 (контракт шага против двойной отправки) и пункт 4 (assign + PR по langgraph#8722 с нашим пробником)

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python session_continues.py --session s_9252aecb 2>&1 | tail -15; echo \"=== qqq_auto:\"; python qqq_auto.py verdict --session s_9252aecb 2>&1 | tail -15", "description": "Check continue/qqq cou

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 100 python rail_plan.py declare --self \"оркестрация, живые замеры по нашему коду (grep/чтение), суждение, синтез, запись в волт\" --outsource \"second_opinion:codex,second_opinion:grok\" 2>&1 | tail -5", "description": "Declare rail plan

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && ls crm-engine/*.py 2>/dev/null | head -20; echo \"=== safe_send:\"; ls -la crm-engine/safe_send.py crm-engine/drip.py crm-engine/budget.py 2>/dev/null", "description": "Locate outbound send engine"}

---

> `Bash` -- {"command": "for d in \"D:/Vault/_imports\" \"C:/Users/dev/.claude/scripts\" \"E:/!CLAUDE-HUBPC-June26\"; do echo \"=== $d\"; timeout 90 find \"$d\" -maxdepth 4 -name \"safe_send.py\" -o -maxdepth 4 -name \"drip.py\" -o -maxdepth 4 -name \"budget.py\" 2>/dev/null | head -10; done", "descri

---

> `Bash` -- {"command": "cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_9252aecb\\tasks\\bcjda62s3.output\" 2>/dev/null | tail -20", "description": "Read counter output"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && wc -l safe_send.py drip.py budget.py 2>/dev/null; echo \"=== идемпотентность/дедуп в safe_send:\"; grep -n -i \"idempot\\|dedup\\|already_sent\\|sent_at\\|uuid\\|hash\\|lock\\|journal\\|ledger\" safe_send.py | head -30", "description": "Inspect 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && sed -n '1,149p' safe_send.py", "description": "Read safe_send.py fully"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && echo \"=== drip.py: выбор цели и защита от повтора:\"; grep -n -i \"already\\|sent\\b\\|stage\\|last_sent\\|skip\\|seen\\|where\\|SELECT\" drip.py | head -40", "description": "Inspect drip.py target selection"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && echo \"=== cross_account_guard источник истины:\"; grep -n -i \"def check\\|open(\\|sqlite3\\|connect(\\|LEDGER\\|BUS_DIR\\|path\\|glob\" cross_account_guard.py | head -30; echo; echo \"=== record_send в budget.py:\"; grep -n -A18 \"def record_s

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && echo \"=== точные строки send/record в safe_send.py:\"; grep -n \"client.send_message\\|budget.record_send\\|cross_account_guard.check\" safe_send.py; echo; echo \"=== кто во всём _imports зовёт check_both:\"; timeout 90 grep -rn \"check_both\" 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && echo \"=== check() 77-122:\"; sed -n '77,122p' cross_account_guard.py; echo; echo \"=== check_archive 134,173:\"; sed -n '134,173p' cross_account_guard.py", "description": "Read check and check_archive bodies"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && echo \"=== _shard_append:\"; grep -n -A22 \"def _shard_append\" budget.py; echo \"=== unverified:\"; grep -n -A20 \"def unverified\" budget.py", "description": "Read shard_append and unverified"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && grep -n -A25 \"^def sent_today\" budget.py | head -40; echo \"=== _is_proven:\"; grep -n -A8 \"def _is_proven\" budget.py", "description": "Read sent_today counting semantics"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && grep -n \"BUS_DIR\\|^NODE\\|def _shard_dir\\|def _own_shard_path\" budget.py | head -20; echo \"---\"; grep -n -A8 \"def _own_shard_path\" budget.py; grep -n -A6 \"def _shard_dir\" budget.py; echo \"=== _shard_events key:\"; grep -n -A14 \"def _

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\crm-engine\\_probe_send_crash_window.py", "content": "# -*- coding: utf-8 -*-\nr\"\"\"_probe_send_crash_window.py - ПРОБНИК (не тест сюиты): показывает окно двойной отправки.\n\nЗачем он есть. 06.10.2026 панель чужих LLM (codex + grok) возразила на вердикт «Lan

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && timeout 110 python _probe_send_crash_window.py 2>&1 | tail -40; echo \"exit=$?\"", "description": "Run the crash-window probe"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; timeout 110 python _probe_send_crash_window.py 2>&1 | tail -40; echo \"exit=${PIPESTATUS[0]}\"", "description": "Run crash-window probe with pipefail"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && sed -n '155,200p' drip.py; echo \"=== кто пишет last_contact:\"; timeout 60 grep -rn \"last_contact\" --include=*.py . 2>/dev/null | head -12", "description": "Check drip send loop and last_contact writers"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && set -o pipefail; timeout 110 grep -rn \"last_contact *=\\|SET last_contact\\|UPDATE leads\" --include=*.py . 2>/dev/null | grep -v \"^./crm-engine/drip.py\" | head -20; echo \"rc=${PIPESTATUS[0]}\"", "description": "Search _imports for writers of last_cont

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 100 python onair.py list 2>/dev/null | grep -i \"crm\\|outreach\\|send\\|budget\\|sirenka\" | head -10; echo \"rc_grep_done\"; timeout 60 python onair.py zones 2>/dev/null | head -20", "description": "Check ON AIR declarations for the out

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && timeout 60 grep -rn \"_shard_append\\|budget.record_send\\|unverified(\" --include=*.py . 2>/dev/null | head -20; echo \"=== unverified full:\"; sed -n '426,474p' budget.py; echo \"=== _shard_append tail:\"; sed -n '324,357p' budget.py", "descri

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && grep -n -B2 -A20 \"def _is_adjudicated\" budget.py; echo \"=== строки 1-30 (шапка):\"; sed -n '1,20p' budget.py", "description": "Read _is_adjudicated and header"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 90 python onair.py declare --zone crm-leads/outbound-send --mode exclusive --what \"контракт шага в safe_send: intent-строка до отправки + resume, чтобы падение не давало двойную отправку (пробник _probe_send_crash_window.py красный)\" 2>

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && timeout 90 python onair.py declare --zone crm-leads/outbound-send --mode exclusive --title \"контракт шага в safe_send: intent до отправки + resume против двойной отправки\" 2>&1 | tail -4", "description": "Declare ON AIR with title"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\budget.py", "old_string": "def _shard_append(acc, day, lead_slug, kind, preview, message_id=None, peer=None):\n    \"\"\"Append one send-event to THIS node's shard ONLY. Returns the event_id, or None on a\n    write failure (lo

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\budget.py", "old_string": "def record_send(acc, lead_slug=None, kind=None, preview=None, db=None,\n                message_id=None, peer=None):", "new_string": "def _pair_key(ev):\n    \"\"\"Dedup/pair key of a shard row: the s

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\budget.py", "old_string": "    Returns the new fleet-wide sent-count for the day. Raises RuntimeError if already at cap\n    (defensive -- callers should can_send() first, but this prevents silent overrun even\n    across nodes

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\budget.py", "old_string": "    -> they surface here, which is correct: unknown is not \"sent\". A row hand-edited to\n    status=\"sent\" with a blank or non-numeric id surfaces too. `since` is an inclusive\n    YYYY-MM-DD day 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\safe_send.py", "old_string": "    sent = None\n    try:\n        sent = await client.send_message(entity, text)\n    except Exception as e:\n        if FloodWaitError is not None and isinstance(e, FloodWaitError):\n            

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\safe_send.py", "old_string": "async def safe_send(client, entity, text, acc, lead_slug=None, kind=\"drip\",", "new_string": "def _close_intent(acc, ts, lead_slug, kind, text, entity, why):\n    \"\"\"Close a write-ahead intent 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\safe_send.py", "old_string": "    if dry_run:\n        return {\"ok\": True, \"dry_run\": True,\n                \"would_record\": \"%s -> %s (%s)\" % (acc, lead_slug, kind)}", "new_string": "    if dry_run:\n        return {\"

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; timeout 110 python _probe_send_crash_window.py 2>&1 | tail -30; echo \"exit=${PIPESTATUS[0]}\"", "description": "Re-run probe after the fix"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && grep -n \"selftest\\|add_argument\" budget.py | tail -12", "description": "Find budget CLI selftest flag"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && echo \"=== budget selftest:\"; timeout 150 python budget.py selftest 2>&1 | tail -12; echo \"rc_budget=$?\"", "description": "Run budget selftest"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; echo \"=== budget selftest:\"; timeout 150 python budget.py selftest 2>&1 | tail -10; echo \"rc_budget=${PIPESTATUS[0]}\"", "description": "Run budget selftest with pipefail"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; echo \"=== safe_send selftest:\"; timeout 120 python safe_send.py 2>&1 | tail -6; echo \"rc_safe=${PIPESTATUS[0]}\"", "description": "Run safe_send selftest"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; echo \"=== drip selftest:\"; timeout 120 python drip.py 2>&1 | tail -6; echo \"rc_drip=${PIPESTATUS[0]}\"; echo \"=== _test_safe_send_diagnose:\"; timeout 120 python _test_safe_send_diagnose.py 2>&1 | tail -5; echo \"rc_diag=${P

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\budget.py", "old_string": "    rows = _all_rows(since)\n    groups = {}\n    for ev in rows:\n        groups.setdefault(_pair_key(ev), []).append(ev)\n    out = []\n    for ev in rows:\n        if _is_adjudicated(ev):\n        

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; echo \"=== safe_send selftest:\"; timeout 120 python safe_send.py 2>&1 | tail -6; echo \"rc_safe=${PIPESTATUS[0]}\"", "description": "Re-run safe_send selftest"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; echo \"=== budget selftest:\"; timeout 150 python budget.py selftest 2>&1 | tail -3; echo \"rc=${PIPESTATUS[0]}\"; echo \"=== probe:\"; timeout 110 python _probe_send_crash_window.py 2>&1 | tail -4; echo \"rc_probe=${PIPESTATUS[

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && sed -n '280,300p' doping.py", "description": "Inspect doping.py send path"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\crm-engine\\doping.py", "old_string": "    import gmail_rail\n    lbl = _mail_label(row)\n    r = gmail_rail.resend(lbl, row[\"address\"], row[\"subject\"], row[\"text\"],\n                          thread_id=row.get(\"thread_id\"),\n     

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; timeout 60 python -c \"import ast,sys; ast.parse(open('doping.py',encoding='utf-8').read()); print('doping.py синтаксис ok')\"; echo \"=== есть ли у doping свой selftest:\"; grep -n \"__main__\\|selftest\" doping.py | tail -5", 

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/crm-engine\" && set -o pipefail; timeout 150 python doping.py selftest 2>&1 | tail -8; echo \"rc_doping=${PIPESTATUS[0]}\"", "description": "Run doping selftest"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && set -o pipefail; git rev-parse --is-inside-work-tree 2>&1 | head -2; git status --porcelain crm-engine 2>&1 | head -10; ls -la .stignore 2>/dev/null && grep -n \"py\\|\\*\" .stignore | head -15", "description": "Check git and stignore in _imports"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && set -o pipefail; git log -1 --format=\"%an <%ae>%n---%n%B\" 2>&1 | head -20", "description": "Read last commit format in _imports"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && set -o pipefail; git log -3 --format=\"%H%n%(trailers)%n===\" 2>&1 | head -20", "description": "Check commit trailers style"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && git add crm-engine/budget.py crm-engine/safe_send.py crm-engine/doping.py crm-engine/_probe_send_crash_window.py && git commit -q -F - <<'MSG' && git log -1 --format=\"%h %s\"\ncrm-engine: контракт шага против двойной отправки (intent до отправки + resume)

---

> `Bash` -- {"command": "python - <<'PY'\nimport json,urllib.request,datetime\ndef gh(u):\n    r=urllib.request.Request(u,headers={'User-Agent':'x','Accept':'application/vnd.github+json'})\n    return json.load(urllib.request.urlopen(r))\nnow=datetime.datetime.now(datetime.timezone.utc)\nseen={}\nfor q in [\"re

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\_seeds\\seed-deepagents-door-20261007.md", "content": "---\ntitle: Сид — зайти в экосистему LangChain через deepagents (живая дверь)\ncreated: 2026-10-07\norigin: сессия H12216 (исследование LangChain по голосовой оператора 06.10.2026)\ntype: seed

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && set -o pipefail; timeout 90 python qqq_auto.py stamp --session s_9252aecb --why \"контракт шага: пробник красный -> починка -> зелёный, коммит 6bd82370; дверь OSS переназначена с langgraph на deepagents по замеру\" 2>&1 

---

**Claude:**

🕐 среда, день, 17:34, 7 октября 2026

**Идём верно**, но один пункт моего же вчерашнего плана оказался неверным, и я начинаю с него.

**Якорь захода:** контракт шага из пункта 0 должен быть не советом в заметке, а работающим кодом с красным-то-зелёным доказательством.

**Рельса:** сам как Claude — замеры по нашему коду, починка, коммит, запись в волт. Наружу вчера уехало суждение: панель `codex` + `grok` (`llm_ask --mode all`), её возражение и стало работой этого захода.

---

## ⛔ Возражение против себя: пункт 4 был неверен

Вчера я написал «по #8722 попросить assign и прислать PR». Это нарушает два наших же правила, и улика у меня была под рукой, я её не применил:

- последнее слово в треде наше (29.08), мейнтейнер не ответил ни разу, тишина **39 дней** → по канону это 🪦, второго бампа мы не делаем;
- PR в `langgraph` = холодный PR в глухую очередь: медиана возраста открытого человеческого PR там **203 дня**, 70 из 100 старше 90 дней.

**Было:** пункт 4 = assign + PR в `langgraph#8722`.
**Стало:** пункт 4 = первое касание в `deepagents` (медиана 5 дней, старше 90 дней ноль), а `langgraph#8722` остаётся лежать как наш след и как строка в CV, без бампа.

Замер под это: в `deepagents` **46 открытых issue** по нашим темам (resume, checkpoint, duplicate, crash, interrupt), почти все без assignee, свежие. Шортлист с номерами внизу.

---

## Что сделано: контракт шага больше не совет, а код

### 1. Сначала доказал, что дыра у нас есть

Написал пробник `crm-engine/_probe_send_crash_window.py`: фейковый «телеграм», отправка проходит, запись в леджер падает (= процесс умер между двумя строками).

Результат **до** починки, живой прогон, exit 2:

```
человек получил сообщений:                1
budget насчитал отправок за сегодня:      0
строк в шарде исходящих:                  0
видит ли budget.unverified() эту отправку: НЕТ -- отправки для системы не существует
cross_account_guard.check      -> ok
cross_account_guard.check_both -> ok
budget.can_send                -> True
человек получил сообщений ВСЕГО:          2   (тексты идентичны: да)
```

Корень назван строками: [safe_send.py:105](D:/Vault/_imports/crm-engine/safe_send.py:105) шлёт, [safe_send.py:118](D:/Vault/_imports/crm-engine/safe_send.py:118) пишет, между ними не было ничего.

Почему не ловила ни одна из трёх защит, тоже по коду:

| Слой | Почему слеп |
|---|---|
| `cross_account_guard.check` | `if _norm_acc(ev["account"]) == acc_n: continue` — свой аккаунт пропускает нарочно |
| `cross_account_guard.check_archive` | `if _norm_acc(a) == acc_n: continue` — то же самое |
| `budget.can_send` | считает только **записанные** строки шарда, а в окне падения строки нет |

Плюс отдельный замер, который усиливает картину: **в `crm-engine` никто не пишет `leads.db.last_contact`**. Единственный писатель во всём `_imports` — `alpha/leadsignal_scan.py`, и то при скане. То есть «уже писали этому» наш движок исходящего не помнит вообще, и повторный выбор лида не требует даже падения.

### 2. Потом починил — write-ahead, без фреймворка

- `budget.record_intent()` пишет строку `status="intent"` **до** необратимого вызова и возвращает `ts`;
- этот `ts` и есть ключ дедупа `sent_today`, поэтому пара intent+резолюция стоит **одну** единицу дневного лимита, а не две (иначе анти-бан-счётчик врал бы в опасную сторону);
- `record_send(..., ts=)` и `resolve_intent(..., status="failed", verified=...)` закрывают пару; при переданном `ts` защитный `raise` на крышке бюджета пропускается нарочно, иначе он воссоздал бы ровно тот баг, от которого intent и ставится;
- `budget.pending_intents()` — список «возможно уже отправлено», это и есть resume;
- `budget.unverified()` стал парным: пара судится целиком, лишний intent не кричит, **одинокий** intent кричит — это выживший после падения;
- `safe_send`: слой 1.5 RESUME отказывает с `reason="pending-intent"` и отправляет человека смотреть живой тред вместо слепой переотправки;
- `doping.py::_mail_push` — тот же контракт на почтовой рельсе: она звала `record_send` напрямую, минуя `safe_send`, и оставалась дырявой.

Результат **после**, тот же пробник, exit 0: строка в шарде 1, `budget` насчитал 1, `unverified()` видит, вторая отправка **отказана**:

```
{"ok": false, "reason": "pending-intent",
 "msg": "предыдущий прогон, возможно, УЖЕ отправил это (1 незакрытых intent...)"}
человек получил сообщений ВСЕГО:          1
```

### 3. Регрессия и авторство

| Проверка | Итог |
|---|---|
| `budget.py selftest` | OK |
| `safe_send.py` selftest | OK (упал один раз на моей первой версии `unverified` — починено: одна строка на пару) |
| `drip.py` selftest | OK |
| `_test_safe_send_diagnose.py` | OK |
| `doping.py selftest` | OK |
| пробник падения | красный до, зелёный после |

Коммит `6bd82370` в `D:/Vault/_imports` с трейлерами `Assisted-by / Machine / Account / Operator`. Зона была объявлена на ON AIR (`crm-leads/outbound-send`, exclusive) и закрыта после работы; две прежние заявки на `crm-leads` просрочены, живого владельца не было.

---

## Что НЕ сделано и не проверено, называю прямо

- **Живой отправки в Telegram не делал.** Это Tier-2, и для этого класса она не нужна: падение процесса воспроизводится без неё.
- **Доставка правки на другие узлы не замерена.** `.py` в `_imports` синком едет (в `.stignore` чёрный список только на данные), но факта приезда на Маки и Маяк я не мерил. Это ровно тот класс, на котором мы уже горели: «зарегистрировал посылку ≠ доставил».
- **Сессию под `deepagents` я не поднял.** Две честные попытки и почему обе мимо: `spawn_queue` — измеренная могила (134 сида ждут с 03.09), а `create_scheduled_task` этой сессии запрещён хуком, потому что она сама рождена рутинным сидом и повисла бы посреди хода. Поэтому сид лежит готовым файлом: [seed-deepagents-door-20261007.md](D:/Vault/Vault-Knowledge/10-Tasks/_seeds/seed-deepagents-door-20261007.md).

Поднять его одной командой, когда будешь за клавиатурой:

```bash
claude --skill nsr "выполни сид D:/Vault/Vault-Knowledge/10-Tasks/_seeds/seed-deepagents-door-20261007.md"
```

**Шортлист в `deepagents`** (все без assignee, рекомендация — первый): `#6736` «No-op subagent duplicates inherited custom state» (5 дней, наш класс дословно) · `#6287` «Thread reprinted from scratch after a rejection» (23 дня) · `#6397` «CodeInterpreterMiddleware.__del__ blocks forever at shutdown» (19 дней).

🎙 Майк: сегодняшний результат не «мы изучили LangChain», а «чужая критика нашего вердикта стоила нам одного вечера и закрыла реальную дыру в исходящем». Фреймворк мы не взяли, контракт забрали, и теперь в тред к ним можно прийти не с вопросом, а с коммитом.

**Слабейшее звено: `status="intent"` — новый статус в общем шарде, который читают все узлы флота, а я проверил его только своими пятью селфтестами на этой машине.** Проверил чем: `_is_proven` требует `status == "sent"`, поэтому старый код на отставшем узле не посчитает intent доставленным касанием, а `_shard_events` считает ключи независимо от статуса, то есть бюджет не поедет. Чего не проверял: `sostav/`, `outreach3.py`, дашборды и прочих читателей шарда вне `crm-engine`. 🤔 Поэтому «флот в порядке» я не утверждаю: утверждаю «на хабе зелено, читателей за пределами crm-engine не обходил».

🧒 **Простыми словами:** вчера я сказал «чужой комбайн нам не нужен, но тетрадку у него спишем». Сегодня тетрадку списали по-настоящему. Теперь наш робот, прежде чем написать человеку, сначала помечает в блокноте «собираюсь отправить вот это», и только потом отправляет. Раньше он сначала отправлял, а записывал потом, и если в этот момент гас свет, запись не появлялась: роботу казалось, что он ничего не писал, и он отправлял то же самое второй раз. Я это нарочно подстроил и показал: человек получил два одинаковых сообщения. Потом починил и показал снова: второй раз робот теперь отказывается и говорит «иди посмотри своими глазами, кажется, я это уже отправил». И ещё я сам себя поправил: идти с подарком в тот дом, где нам не открывали 39 дней, глупо, поэтому пойдём в соседний, где открывают за пять дней.

🕐 среда, день, 17:34, 7 октября 2026
