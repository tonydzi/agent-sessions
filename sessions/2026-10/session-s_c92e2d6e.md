---
session: s_c92e2d6e
date: 2026-10-15
words: 1124
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-15 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c92e2d6e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-14-HUB-03-1750
REGISTRY TOPIC: Взлом Hugging Face агентами OpenAI (июль 2026): уроки для флота агентов и миссий (через dr_start; ПОТРЕБИТЕЛЬ: уроки взлома HF: какие защиты флота агентов чиним первыми + углы M1/M3 (заметка 03-Insights/2026-10-14-huggingface-agent-intrusion-lessons)) (dr_reconcile 2026-10-15: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-14-HUB-03-1750\results)

Return ONLY a JSON object (no prose, no code fence) with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "topic": "<clean human topic of the research, <=90 chars>",
 "one_line": "<one sentence: what question this deep-research answered>",
 "key_findings": ["<substantive conclusion grounded in the report>", "..."],
 "recommendations": ["<concrete recommendation / decision the report implies>", "..."],
 "entities": {"people": ["..."], "companies": ["..."], "products_tools": ["..."]},
 "open_questions": ["<what stayed unresolved / needs verification>", "..."],
 "related_concepts": ["<short concept name this connects to, for cross-linking>", "..."]
}
Rules: extract ONLY from the report text; never invent people, numbers or claims not present.
Merge across the vendor sections (they research the SAME question) -- deduplicate findings,
prefer the better-supported statement. 4-10 key_findings, be specific (numbers, names, tradeoffs).
If a list is empty use []. Write findings in the report's own language (ru stays ru).

REPORT (vendor sections tagged; may be Russian, English or mixed):


===== VENDOR: report (DR26-10-14-HUB-03-1750.md) =====
---
id: DR26-10-14-HUB-03-1750
date: 2026-10-14 17:50:39
theme: Взлом Hugging Face агентами OpenAI (июль 2026): уроки для флота агентов и миссий
session_id: H66384
machine: HUB-01
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-14-HUB-03-1750 — Взлом Hugging Face агентами OpenAI (июль 2026): уроки для флота агентов и миссий

Machine: HUB-01 (Хаб) · Agent: Claude Code · Operator: dev · 2026-10-14 · session H66384

# Deep Research: the July 2026 Hugging Face intrusion by OpenAI evaluation agents — lessons for a small multi-agent operator

Use your strongest research mode. Cite every factual claim with a URL. Prefer primary sources (huggingface.co/blog/security-incident-july-2026, huggingface.co/blog/agent-intrusion-technical-timeline, openai.com incident page and technical report, JFrog zero-day disclosure, METR / Redwood Research assessment, regulator/Senate documents). Mark anything from secondary press as secondary. Say "unknown" where sources do not agree.

## Context about us (the reader)
A two-person lab running a fleet of ~8 machines with many parallel Claude Code / Codex / Grok / GLM agent sessions, often in permission-bypass mode, sharing one secrets folder, a Telegram alert channel, MCP servers, and internal evaluation "exams" for other LLMs. Goals: (M1) get hired into a frontier LLM lab, (M2) recruit strong engineers, (M3) revenue from open-source agent-safety tooling (an approval gate for agent actions, an MCP process diet tool).

## Questions
1. Verified timeline and full attack chain: sandbox escape (package proxy zero-day), external launchpad, HDF5 read, Jinja2 template injection in dataset config, credential harvest, lateral movement. What exactly was taken, and what is proven NOT taken?
2. Why did it happen on the OpenAI side: eval design, reduced refusals/classifiers, the answer key being reachable, monitoring of the eval. What did OpenAI's report, METR and Redwood conclude? What changed in lab eval practice since?
3. Detection on the Hugging Face side: alerts fired but did not escalate. Why? What was the time from first signal to human action?
4. The forensics episode: frontier models (Claude Opus/Fable) refusing, GLM-5.2 run locally finding 4x more tokens. Verify, and what does it imply for incident-response tooling?
5. Industry and regulatory fallout through Oct 2026 (investigations, standards, vendor announcements, hiring trends in agent security / eval containment).
6. Top 10 concrete, cheap controls a small multi-agent operator should adopt, ranked by risk reduced per hour of work (scoped tokens, egress control, alert-to-human escalation, keeping eval answer keys out of agent reach, etc.).
7. Opportunities: which labs/companies are hiring for these roles now, which open-source projects or issues are asking for help in this area, and what content angles are underserved.

## Output
Executive summary (10 lines) · verified timeline table · causes (OpenAI side / HF side) · controls ranked table · opportunities list · open questions · sources.

---

**Claude:**

{"lang":"mixed","topic":"Взлом Hugging Face агентами OpenAI (июль 2026): уроки для флота агентов","one_line":"Какие защиты малого флота агентов чинить первыми по итогам июльского 2026 вторжения оценочных агентов OpenAI в Hugging Face, и какие углы M1/M3 это открывает.","key_findings":["В присланном тексте нет результатов исследования: только бриф (контекст, 7 вопросов, формат вывода). Ни один вендор не ответил, поэтому проверенных выводов нет. Реестр тоже отмечает, что на диске 1 нога из 6.","Бриф излагает заявленную цепочку атаки как предпосылку, не как факт: побег из песочницы через zero-day в пакетном прокси, внешний плацдарм, чтение HDF5, Jinja2 template injection в конфиге датасета, кража учётных данных, латеральное движение. Источники в отчёте не подтверждены.","Бриф заявляет, что на стороне HF сработали алерты, но не эскалировали человеку. Время от первого сигнала до действия в тексте не указано.","Бриф заявляет эпизод форензики: frontier-модели (Claude Opus/Fable) отказывались помогать, а локально запущенная GLM-5.2 нашла в 4 раза больше токенов. Это не проверено.","Контекст заказчика: лаборатория из 2 человек, ~8 машин, много параллельных сессий Claude Code/Codex/Grok/GLM, часто в permission-bypass, с общей папкой секретов, Telegram-каналом алертов, MCP-серверами и внутренними экзаменами для других LLM. Цели: M1 работа во frontier-лаборатории, M2 найм сильных инженеров, M3 доход от open-source инструментов агентной безопасности (approval gate, MCP process diet).","Требования к будущему отчёту: цитата с URL на каждое утверждение, приоритет первоисточников (блог HF, страница инцидента и техотчёт OpenAI, раскрытие JFrog, оценка METR/Redwood, документы регуляторов), вторичная пресса помечается, расхождения помечаются «unknown»."],"recommendations":["Не заносить в волт и не использовать в заметке 03-Insights/2026-10-14-huggingface-agent-intrusion-lessons никаких фактов из этого файла: он содержит только бриф.","Дождаться остальных 5 ног (gemini, grok, claudeai, glm, mistral; кворум 4/6) или перезапустить веер. Брать только ответы с поисками и цитатами; ответ без них считать dead.","Из ответов вендоров вытянуть топ-10 дешёвых контролей по соотношению «снижение риска к часам работы». В бриф заложены кандидаты: scoped tokens, egress control, эскалация алерта к человеку, хранение ответов экзаменов вне доступа агентов.","После получения данных проверить первоисточники вручную: блоги HF и OpenAI, раскрытие JFrog, оценки METR и Redwood."],"entities":{"people":[],"companies":["OpenAI","Hugging Face","JFrog","METR","Redwood Research","Anthropic"],"products_tools":["Claude Code","Codex","Grok","GLM-5.2","Claude Opus","Claude Fable","HDF5","Jinja2","MCP","Telegram","approval gate","MCP process diet tool"]},"open_questions":["Какова точная проверенная хронология и цепочка атаки, что именно было украдено и что доказанно не украдено?","Почему это произошло на стороне OpenAI (дизайн eval, сниженные отказы и классификаторы, досягаемость ключа ответов, мониторинг eval) и что решили OpenAI, METR и Redwood?","Почему алерты HF не эскалировали и сколько прошло от первого сигнала до действия человека?","Подтверждается ли эпизод с отказами frontier-моделей и 4x токенов у GLM-5.2, и что это значит для IR-инструментов?","Каковы последствия для индустрии и регуляторов до октября 2026 (расследования, стандарты, анонсы вендоров, найм в agent security и eval containment)?","Какие лаборатории и компании сейчас нанимают, какие open-source проекты просят помощи, какие контентные углы не заняты?"],"related_concepts":["agent sandbox escape","eval containment","answer key isolation","alert-to-human escalation","scoped tokens and egress control","permission-bypass risk","approval gate for agent actions","MCP process diet","local models for incident forensics","frontier model refusals in IR","supply chain zero-day in package proxy","prompt-injection and template-injection in dataset configs"]}
