---
session: s_ece117da
date: 2026-10-08
words: 1319
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-08 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ece117da` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-07-HUB-04-1222
REGISTRY TOPIC: Параллельные воркфлоу и параллельный Deep Research в n8n: реальный параллелизм, долгие внешние вызовы, кворум и добор, чужой опыт против Temporal/Prefect/asyncio (dr_reconcile 2026-10-07: на диске 1/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-07-HUB-04-1222\results)

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


===== VENDOR: report (DR26-10-07-HUB-04-1222.md) =====
---
id: DR26-10-07-HUB-04-1222
date: 2026-10-07 12:22:26
theme: Параллельные воркфлоу и параллельный Deep Research в n8n: реальный параллелизм, долгие внешние вызовы, кворум и добор, чужой опыт против Temporal/Prefect/asyncio
session_id: 32b4d561@HUB-01
machine: HUB-01
targets: chatgpt,gemini,grok,glm,mistral
---

# Deep Research: параллельные воркфлоу и параллельный Deep Research в n8n

Контекст заказчика: self-hosted n8n (n8n.palo-alto.ai, ~98 воркфлоу, 68 активных, queue-mode неизвестен). Задача — выяснить, годится ли n8n как ОРКЕСТРАТОР параллельной веерной работы (в частности веера Deep Research по 5-6 внешним LLM-вендорам одновременно), и как это строят те, кто уже это сделал.

Нужны ответы с ссылками на документацию/исходники/посты практиков, с датами, и с явной пометкой где это замер, а где чужое утверждение.

## 1. Параллелизм в n8n: что есть на самом деле
- Как n8n исполняет ветки воркфлоу: действительно параллельно или по очереди (порядок веток, Merge-нода, SplitInBatches)? Что меняет queue mode (Redis + воркеры), `N8N_CONCURRENCY_PRODUCTION_LIMIT`, `EXECUTIONS_MODE=queue`, число воркеров?
- Sub-workflow (Execute Workflow): синхронный/асинхронный вызов, «Execute Once», wait-for-sub-workflow; как сделать fan-out из N параллельных подворкфлоу и собрать результаты (fan-in) без потери ветки.
- Потолки: сколько одновременных HTTP-запросов/исполнений держит один инстанс; где ломается (память, таймауты вебхука, pruning истории исполнений).
- Wait-нода: точность срабатывания, лимиты числа ожидающих исполнений, что происходит при рестарте n8n (переживают ли ожидания), и чем это отличается от Schedule Trigger.

## 2. Долгие и ненадёжные внешние вызовы (ровно наш кейс Deep Research)
- Паттерны для вызова, который длится 5-40 минут (deep research у вендоров): polling, webhook-callback, Wait-until, разбиение на два воркфлоу.
- Идемпотентность и дедупликация повторных запусков; retry с backoff; DLQ (dead-letter) в n8n; как не заказать один и тот же ДР дважды.
- Частичный результат: как собрать кворум «4 из 6 ответили, 2 опоздали» и потом добрать опоздавших, не блокируя синтез.
- Наблюдаемость: единый run-ledger по исполнениям, алерт на упавшую ветку, экран «что сейчас в полёте».

## 3. Кто это уже сделал — чужой опыт, не теория
- Публичные примеры/шаблоны n8n для веера по нескольким LLM-провайдерам одновременно (OpenAI/Anthropic/Gemini/Grok/Mistral/DeepSeek), с кодом или экспортом воркфлоу.
- Сравнение с альтернативами по ЭТОЙ задаче: Temporal, Prefect, Dagster, Windmill, Airflow, Inngest, Trigger.dev, обычный Python asyncio + cron. Где n8n объективно хуже и где лучше.
- Известные грабли практиков: Code-нода (Pyodide, нет pip), размер payload между нодами, бинарные данные, секреты, версионирование воркфлоу в git, миграция.

## 4. Вердикт, который нужен заказчику
- Для веера Deep Research по 6 вендорам раз в сутки: n8n — да или нет, и почему. Если да — минимальная схема нод. Если нет — что вместо.
- Что НЕ переносить в n8n ни при каких условиях (файловая система, git, GUI, локальные процессы Windows/macOS).
- Три самых дешёвых улучшения, которые дают 80% пользы.

Формат ответа: выводы списком, под каждым — источник и дата. Отдельной строкой: чего ты НЕ смог проверить и почему.


===== VENDOR: gemini (DR26-10-07-HUB-04-1222-n8n-parallel-workflows-REJECTED-echo-gemini.md) =====
Gemini
New chat
Search chats
Images
Videos
Library
Notebooks
New notebook
Recent
КОНТЕНТ ЗАВОД
Запрос порівняння та аналізу даних
--- id: DR26-10-06-HUB-02-1359 date: 2026-10-06 13:59:54 theme: Organic un-fried vegetable-rich brea
AI Startup Fundraising Team Research
Экономика и защита AI-стартапов для SMB в США
Оценка мультиагентных рабочих пространств
LLM Comparison for X Posts
Ошибка отказа языковой модели
Стратегия OSS-контрибьютинга для ИИ-оффера
Стратегия OSS-экспертизы для ИИ-оффера
AI Security Career Path for Senior Engineer
Anthropic Fellows Program Security Stream Analysis
AI Security Career Doors for dev
Anthropic Fellows Program Application Strategy
Стратегия OSS-контрибьютинга для ИИ-оффера
bb Orchestrator Fleet Setup and Practices
Окестрация агентов с bb
Критика архитектуры второго мозга
Анализ внедрения Jev в агентский флот
Анализ и улучшение CV для Silicon Valley AI Landing Lead
Идеальное CV AI Deployment Strategist 2026
Анализ и оптимизация венчурного CV
Идеальное CV 2026: Стейблкоин Strategy & BD
Идеальное CV для Stablecoin & BD
Activity
CryptoPunk Dz2
Work
•
Expanded
Rio de Mouro, Portugal
From your IP address
Update location
Conversation with Gemini
You said --- id: DR26-10-07-HUB-04-1222 date: 2026-10-07 12:22:26 theme: Параллельные воркфлоу и параллельный…

---

id: DR26-10-07-HUB-04-1222

date: 2026-10-07 12:22:26

theme: Параллельные воркфлоу и параллельный Deep Research в n8n: реальный параллелизм, долгие внешние вызовы, кворум и добор, чужой опыт против Temporal/Prefect/asyncio

session_id: 32b4d561@HUB-01

machine: HUB-01

targets: chatgpt,gemini,grok,glm,mistral

---




# Deep Research: параллельные воркфлоу и параллельный Deep Research в n8n




Контекст заказчика: self-hosted n8n (n8n.palo-alto.ai, ~98 воркфлоу, 68 активных, queue-mode неизвестен). Задача — выяснить, годится ли n8n как ОРКЕСТРАТОР параллельной веерной работы (в частности веера Deep Research по 5-6 внешним LLM-вендорам одновременно), и как это строят те, кто уже это сделал.




Нужны ответы с ссылками на документацию/исходники/посты практиков, с датами, и с явной пометкой где это замер, а где чужое утверждение.




## 1. Параллелизм в n8n: что есть на самом деле

- Как n8n исполняет ветки воркфлоу: действительно параллельно или по очереди (порядок веток, Merge-нода, SplitInBatches)? Что меняет queue mode (Redis + воркеры), `N8N_CONCURRENCY_PRODUCTION_LIMIT`, `EXECUTIONS_MODE=queue`, число воркеров?

- Sub-workflow (Execute Workflow): синхронный/асинхронный вызов, «Execute Once», wait-for-sub-workflow; как сделать fan-out из N параллельных подворкфлоу и собрать результаты (fan-in) без потери ветки.

- Потолки: сколько одновременных HTTP-запросов/исполнений держит один инстанс; где ломается (память, таймауты вебхука, pruning истории исполнений).

- Wait-нода: точность срабатывания, лимиты числа ожидающих исполнений, что происходит при рестарте n8n (переживают ли ожидания), и чем это отличается от Schedule Trigger.




## 2. Долгие и ненадёжные внешние вызовы (ровно наш кейс Deep Research)

- Паттерны для вызова, который длится 5-40 минут (deep research у вендоров): polling, webhook-callback, Wait-until, разбиение на два воркфлоу.

- Идемпотентность и дедупликация повторных запусков; retry с backoff; DLQ (dead-letter) в n8n; как не заказать один и тот же ДР дважды.

- Частичный результат: как собрать кворум «4 из 6 ответили, 2 опоздали» и потом добрать опоздавших, не блокируя синтез.

- Наблюдаемость: единый run-ledger по исполнениям, алерт на упавшую ветку, экран «что сейчас в полёте».




## 3. Кто это уже сделал — чужой опыт, не теория

- Публичные примеры/шаблоны n8n для веера по нескольким LLM-провайдерам одновременно (OpenAI/Anthropic/Gemini/Grok/Mistral/DeepSeek), с кодом или экспортом воркфлоу.

- Сравнение с альтернативами по ЭТОЙ задаче: Temporal, Prefect, Dagster, Windmill, Airflow, Inngest, Trigger.dev, обычный Python asyncio + cron. Где n8n объективно хуже и где лучше.

- Известные грабли практиков: Code-нода (Pyodide, нет pip), размер payload между нодами, бинарные данные, секреты, версионирование воркфлоу в git, миграция.




## 4. Вердикт, который нужен заказчику

- Для веера Deep Research по 6 вендорам раз в сутки: n8n — да или нет, и почему. Если да — минимальная схема нод. Если нет — что вместо.

- Что НЕ переносить в n8n ни при каких условиях (файловая система, git, GUI, локальные процессы Windows/macOS).

- Три самых дешёвых улучшения, которые дают 80% пользы.




Формат ответа: выводы списком, под каждым — источник и дата. Отдельной строкой: чего ты НЕ смог проверить и почему.




Pro

Gemini is AI and can make mistakes, including about people. Your privacy and Gemini
Opens in a new window

---

**Claude:**

You've hit your weekly limit · resets Oct 10, 4am (Europe/London)
