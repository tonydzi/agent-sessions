---
session: s_27f02388
date: 2026-10-09
words: 6527
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-09 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_27f02388` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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


===== VENDOR: gemini (gemini.md) =====
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
Стратегия X-контента для инженера
--- id: DR26-10-07-HUB-04-1222 date: 2026-10-07 12:22:26 theme: Параллельные воркфлоу и параллельный Deep Research в n8n: реальн
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

Analyzing Parallelism in n8n
Gemini said
Answer now




Pro

Gemini is AI and can make mistakes, including about people. Your privacy and Gemini
Opens in a new window

Analyzing Parallelism in n8n

===== VENDOR: grok (grok.md) =====
Собираю первичные источники по параллелизму n8n, queue mode, Wait и вееру LLM. Отчёт будет одним сообщением после проверки живых страниц.A. Параллелизм в n8n: ветки одного исполнения идут по очереди, параллельность появляется только между отдельными исполнениями

1. Воркфлоу, созданный с n8n 1.0, исполняет ветки по очереди: одну до конца, потом следующую. Порядок веток задаёт холст, сверху вниз; на одной высоте раньше идёт левая. Это настройка Execution order = v1 (recommended). Старый v0 (до 1.0, его можно включить в настройках) чередует «первый узел каждой ветки, потом второй», но это всё ещё один проход, а не отдельные процессы.
Источник, док, страница открыта 2026-10-07: https://docs.n8n.io/build/flow-logic/understand-execution-order.md
Та же формулировка v1/v0 в настройках воркфлоу: https://docs.n8n.io/workflows/settings/

2. Практик 1 декабря 2025 на двух HTTP-ветках замерил своими глазами: верхний HTTP отрабатывает, примерно через 10 секунд стартует второй, Merge срабатывает после обоих. Его вывод дословно: ветки не исполняются асинхронно. Это чужое наблюдение одного воркфлоу, не бенчмарк n8n.
https://community.n8n.io/t/async-parallel-execution/229201

3. Merge ждёт данные всех подключённых входов и только потом идёт дальше. Режим Append с n8n 1.49.0 умеет больше двух входов; до этого было только два, и люди гнездили Merge в Merge. Кворума «хватит 4 из 6» у ноды нет: не пришедшая ветка держит всю сборку.
Док, открыта 2026-10-07: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.merge/
Чужое, 31 марта 2025, «Merge как раз для того, чтобы подождать все ветки»: https://community.n8n.io/t/best-practice-to-wait-for-multiple-branches-before-continuing/95103

4. Loop Over Items (старое имя Split in Batches) режет список на пачки и гоняет пачки по кругу, потом склеивает результат на выходе done. Это очередь пачек, не веер.
Док, страница с датой публикации в индексе 2026-06-26: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.splitinbatches

5. Внутри одной HTTP Request-ноды несколько входных items могут уйти одновременно. Разбор issue от 18 мая 2026: запросы стартуют в цикле и собираются через `Promise.allSettled`; опция Batching вставляет паузу только на индексах, кратных размеру пачки (дефолт пачки в том разборе 50). Без Batching паузы нет. Это чтение исходника автором issue, я сам файл HTTP-ноды в этом заходе не открывал.
https://github.com/n8n-io/n8n/issues/30652
Официальная опция Batching (Items per Batch + Batch Interval в миллисекундах) и отдельная опция Timeout: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest.md
Числовой дефолт Timeout в этой доке не назван. Чужое, 11 августа 2026: встроенный axios-дефолт 300000 мс (5 минут), и значение выше него на той версии «срезалось». Это не замер на вашем инстансе. https://community.n8n.io/t/how-to-increase-the-default-timeout-of-300000ms-when-using-node-http-request/307122

6. Queue mode (`EXECUTIONS_MODE=queue`) параллелит исполнения, не ветки. Main принимает таймеры и вебхуки и сам исполнение не бежит. Он кладёт id исполнения в Redis (Bull). Воркер забирает id, читает воркфлоу из базы, пишет результат обратно. Каждый воркер — свой процесс Node.js и может держать несколько исполнений сразу. SQLite с queue mode дока не рекомендует, распределённая схема на SQLite не поддерживается. Бинарные файлы в режиме filesystem с queue mode не поддерживаются: нужен S3, база или другой общий стор. Ключ `N8N_ENCRYPTION_KEY` обязан быть одним и тем же на main и на всех воркерах, иначе креды не расшифровываются.
Док, открыта 2026-10-07: https://docs.n8n.io/deploy/host-n8n/configure-n8n/scaling/enable-queue-mode.md
Таблица Redis и таймаутов (в том числе `N8N_GRACEFUL_SHUTDOWN_TIMEOUT` по умолчанию 30 секунд, `QUEUE_WORKER_LOCK_DURATION` 60000 мс, проверка зависших джобов каждые 30000 мс, максимум 1 повтор зависшего): https://docs.n8n.io/hosting/configuration/environment-variables/queue-mode/
Число воркеров дока не фиксирует. Это ваши процессы: один воркер, пять, десять.

7. Сколько джобов один воркер берёт одновременно, задаёт `n8n worker --concurrency`. Выдержка доки, снятая в этом заходе со страницы queue mode: дефолт 10; рекомендация n8n — 5 или выше, потому что много воркеров с маленьким concurrency выжигают пул соединений к базе.
https://docs.n8n.io/hosting/scaling/queue-mode/
Та же механика на странице, которую я открыл целиком: в queue mode `N8N_CONCURRENCY_PRODUCTION_LIMIT`, если он не `-1`, подменяет флаг `--concurrency`.
https://docs.n8n.io/deploy/host-n8n/configure-n8n/scaling/control-concurrency

8. В обычном режиме (не queue) лимита одновременных production-исполнений нет, пока вы сами не поставите `N8N_CONCURRENCY_PRODUCTION_LIMIT`. Дефолт переменной `-1`, то есть выключено. Пример из доки: `=20`. Лишние встают в FIFO. Лимит считается только для production, то есть запуск с вебхука или триггера. Не считаются ручной запуск, sub-workflow, error-workflow и запуск из CLI. Стоящее в этой очереди исполнение нельзя retry. После рестарта n8n добирает очередь до лимита, остаток кладёт обратно.
Та же страница control-concurrency, открыта 2026-10-07.
Переменные целиком (`EXECUTIONS_MODE` дефолт `regular`, `EXECUTIONS_TIMEOUT` дефолт `-1` = без общего таймаута, `EXECUTIONS_TIMEOUT_MAX` дефолт 3600 секунд, `N8N_AI_TIMEOUT_MAX` дефолт 3600000 мс и это только ноды OpenAI/Anthropic/Mistral/Ollama, не голый HTTP Request): https://docs.n8n.io/deploy/host-n8n/configure-n8n/basic-configuration/use-environment-variables/executions

9. Execute Sub-workflow. Режим «Run once with all items» — один вызов на весь список. «Run once for each item» — по очереди, «in turn», не пачкой одновременно. Опция Wait for Sub-Workflow Completion: включена — родитель стоит и получает выход последней ноды ребёнка; выключена — родитель идёт дальше и выхода ребёнка не видит. Связка parent/child в UI есть (View sub-execution), но только у этого вызова.
Док, открыта 2026-10-07: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executeworkflow.md
Опция приехала в 1.26.0, PR смёржен 19–24 января 2024: https://github.com/n8n-io/n8n/issues/8389
Чужое, 10 июля 2025: автор ждал, что один Execute Workflow на списке людей дождётся всех подворкфлоу. Не дождался: узел уходит дальше, как только вернулся первый. Ответ сообщества: нода отдаёт весь список одним вызовом, «дождаться N штук» она не умеет; ближайший обход — вебхук на каждого плюс свой шаблон с гонками по времени. https://community.n8n.io/t/using-execute-workflow-with-run-once-with-all-items-and-wait-for-sub-workflow-completion/147024
Чужое, 10 сентября 2024, n8n 1.57.0: Wait for Sub-Workflow = false вместе с On Error = «Continue (using error output)» поднимал ребёнка и тут же его обрывал. Обход через HTTP на вебхук у них работал. https://community.n8n.io/t/execute-workflow-wait-for-sub-workflow-false-sub-workflow-aborts/53771
Является ли ребёнок с wait=false отдельным джобом в Redis, страницы, которые я открыл, не говорят. Это дырка, она в блоке E.

10. Потолок одного инстанса дока не даёт числом «N одновременных HTTP». Она говорит другое: слишком много одновременных исполнений молотит event loop, процесс перестаёт отвечать. Память нода не квотирует: её едят объём JSON, бинарные данные, число нод, Code-нода и ручной запуск (для UI делается копия данных). Лекарство из доки: резать на куски, не таскать лишнее между нодами, тяжёлое уносить в sub-workflow и возвращать родителю маленький результат.
https://docs.n8n.io/hosting/scaling/memory-errors/
Бинарное по умолчанию живёт в памяти (`N8N_DEFAULT_BINARY_DATA_MODE=default`). Для больших файлов дока велит `filesystem`, а в queue mode filesystem запрещён, нужен `database` / `s3` / `azure`. Колонка базы режет один файл дефолтом 512 МиБ, потолок 1024 МиБ.
https://docs.n8n.io/deploy/host-n8n/configure-n8n/scaling/handle-binary-data
https://docs.n8n.io/deploy/host-n8n/configure-n8n/basic-configuration/use-environment-variables/binary-data.md
`N8N_PAYLOAD_SIZE_MAX` по умолчанию 16 МиБ. Дока говорит это в контексте загрузки пакета, и там же: переменная не только про пакеты. Превышение даёт 413.
https://docs.n8n.io/build/manage-workflows/n8n-packages/limits-and-permissions
В queue mode ответ вебхука едет от воркера к main через Redis. `N8N_WEBHOOK_RESPONSE_RELAY_SIZE_MAX` дефолт 64 МиБ; больше этого без offload нода падает. Offload тела в стор есть с n8n 2.34.0.
Та же страница enable-queue-mode, раздел Large webhook responses.

11. История исполнений чистится сама. Дефолт: включено. Условие «или»: старше 336 часов (14 суток), или всего исполнений больше 10000 (тогда удаляют со старых). Статусы `new`, `running`, `waiting` не чистятся. Помеченные (тег, оценка) не чистятся. Буфер жёсткого удаления 1 час.
https://docs.n8n.io/hosting/scaling/execution-data/
Следствие для леджера ДР: экран исполнений n8n — не архив. Через две недели успешного прогона сырого ответа там может не быть.

12. Wait и Schedule Trigger — разные механизмы. Wait ставит на паузу уже идущее исполнение и пишет его в базу; когда условие наступает, исполнение поднимают с теми же данными. Режимы: интервал, конкретное время, вебхук (`$execution.resumeUrl`, уникален на исполнение), форма. Для интервала дока пишет: часы сервера n8n, таймзона воркфлоу на Wait не влияет.
Док ноды, баннер «обновлено 3 месяца назад», открыта 2026-10-07: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait
Короткая страница логики: https://docs.n8n.io/build/flow-logic/wait

13. Расхождение доки и исходника, оба открыты сегодня. Дока всё ещё пишет: ожидание короче 65 секунд не сбрасывается в базу, процесс просто спит в `setTimeout`; длиннее 65 секунд уходит в базу. В текущем `master` файла `Wait.node.ts` ветки `65000` больше нет: и интервал, и вебхук, и форма вызывают `putExecutionToWait`. PR #27066 смёржен 2 апреля 2026 и описывает, зачем: старый порог 65 секунд существовал из-за опроса базы раз в 60 секунд; опрос уменьшили, короткие ожидания тоже стали переживать крэш. Issue от 12 апреля 2026 привязывает это к n8n 2.14.0 и жалуется на побочный эффект: пока Wait висит, UI не показывает выход предыдущих нод.
Исходник, открыт 2026-10-07: https://raw.githubusercontent.com/n8n-io/n8n/master/packages/nodes-base/nodes/Wait/Wait.node.ts
PR: https://github.com/n8n-io/n8n/issues/27066
Issue: https://github.com/n8n-io/n8n/issues/28372
Точность срабатывания после этого PR, со слов автора PR, а не из доки: опрос WaitTracker около 5 секунд, джиттер короткого ожидания до ~5 секунд. Сам `wait-tracker.ts` я не открывал.

14. Переживают ли ожидания рестарт. Механизм: пауза лежит в базе, чистка waiting не трогает. Тест в описании того же PR: убить n8n посреди Wait и поднять — исполнение должно продолжиться. Чужое, 3 января 2026, n8n 1.122.5, Docker: ответ сообщества «да, если том с базой пережил `docker compose down`». Обратные жалобы тоже есть: 17 апреля 2026, с 2.16 Wait зависал в Waiting, пока рестарт или смена базы на Postgres не отпускали пачку сразу. Значит «лежит в базе» не равно «само проснётся», если сломан трекер, часы базы или воркер queue mode.
https://community.n8n.io/t/if-i-restart-the-docker-instance-are-the-workflows-currently-in-waiting-status-resume-after-that/244543
https://community.n8n.io/t/since-2-16-nodes-are-stuck-in-waiting/288762

15. Schedule Trigger поднимает новое исполнение по часам, а не будит старое. Таймзона: таймзона воркфлоу, иначе `GENERIC_TIMEZONE`, иначе дефолт self-hosted `America/New_York`. С n8n 2.36 у ноды есть политика пропущенного запуска (не запускать / один догон / догон на каждое правило), и она работает только на durable scheduler. Дефолтный in-memory планировщик пропущенные запуски не исполняет вообще. Значение переменной в кроне читается в момент публикации, не при каждом тике.
https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.scheduletrigger

B. Вызов на 5–40 минут, повтор, кворум, экран «что в полёте»

16. Синхронно держать HTTP 40 минут — плохой каркас. Таймаут всего воркфлоу по умолчанию выключен (`EXECUTIONS_TIMEOUT=-1`), но потолок, который можно выставить на один воркфлоу, по умолчанию 3600 секунд, и пока нода не закончилась, soft timeout в главном процессе не срабатывает. Отдельный сокет HTTP Request дока позволяет задать в миллисекундах, а чужой замер августа 2026 упирается в 5 минут. Ноды LLM имеют свой потолок `N8N_AI_TIMEOUT_MAX` = 1 час. Воркер при этом занят всё это время: слот concurrency не отпускается, пока исполнение running.
Док таймаута: https://docs.n8n.io/hosting/configuration/configuration-examples/execution-timeout/
Док переменных: ссылка из пункта 8.

17. OpenAI прямо пишет, что deep research занимает десятки минут, и велит `background: true`, потом poll `GET /v1/responses/{id}`, пока статус `queued` или `in_progress`, либо вебхук о готовности. В примере SDK таймаут клиента на синхронный путь выставлен в 3600 секунд. Фоновый режим хранит ответ примерно 10 минут ради poll и несовместим с Zero Data Retention. Модели `o3-deep-research` и `o4-mini-deep-research` в этой же доке помечены на выключение 23 июля 2026, замена названа `gpt-5.6-sol`; примеры со старыми id оставлены как справка. Страница открыта 2026-10-07.
https://developers.openai.com/api/docs/guides/deep-research
https://developers.openai.com/api/docs/guides/background
Для n8n из этого следует схема из двух шагов, а не одна длинная нода: HTTP «старт» (секунды, в ответе id) и отдельно Wait на вебхук вендора либо цикл «Wait несколько минут → HTTP статус». Короткий Wait на актуальном master тоже пишется в базу, так что рестарт n8n этот цикл не убивает. Если инстанс старше 2.14, Wait короче 65 секунд в базе не лежит и рестарт его съедает. Версию n8n.palo-alto.ai я не смотрел.

18. Встроенного DLQ в n8n нет. Есть три слоя, и это разные вещи. Слой ноды: Settings → Retry on Fail, Max Tries и Wait Between Tries в миллисекундах, пауза фиксированная, не экспонента. Дока HTTP common issues: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/common-issues/
Слой воркфлоу: в настройках выбирается Error Workflow, он стартует с Error Trigger и получает id исполнения, url, текст ошибки, последнюю ноду, id и имя воркфлоу. Один такой воркфлоу можно повесить на много боевых. Дока: https://docs.n8n.io/flow-logic/error-handling/
Слой «мертвое письмо» люди собирают сами: Error Trigger пишет payload в Postgres или таблицу, отдельный расписание-воркфлоу переигрывает строку, после N попыток ставит статус dead. Это чужой паттерн, не примитив продукта. Шаблон n8n с Google Sheets + Slack, страница шаблона говорит «обновлён 14 дней назад» относительно выгрузки около 2026-10-01: https://n8n.io/workflows/19599-manage-dead-letter-retries-with-google-sheets-and-slack-alerts/
Разбор на форуме 4 июня 2026, та же схема через свою таблицу и `POST /api/v1/executions/...` retry: https://community.n8n.io/t/way-to-handle-dead-letter-queues-in-n8n-for-failed-jobs/298210
Чужое предупреждение про идемпотентность, 10 июня 2026: Retry on Fail при потерянном ответе (запрос прошёл, n8n думает что нет) создаёт дубль. https://abhiman.io/blog/n8n-error-handling/

19. Ключа идемпотентности у триггера n8n в открытых доках нет. Единственный способ не заказать один и тот же ДР дважды: до HTTP-старта прочитать внешнюю таблицу по ключу `(дата, вендор, хеш промпта)` и не стартовать, если строка уже `started` или `done`. Повторный тик Schedule и ручной Retry этого сами не понимают. Retry из UI есть и умеет «со старыми данными» или «с текущей версией воркфлоу»: https://docs.n8n.io/workflows/executions/all-executions/

20. Кворум «4 из 6, двоих добрать потом» готовой ноды не имеет. Merge ждёт все входы. Если ветка упала без Continue, Merge не наступает и синтез не начинается. Рабочая схема, это сборка из доков, а не найденный шаблон: каждый вендор пишет строку во внешнюю таблицу (`pending` / `done` / `error`, текст ответа, id исполнения). Синтезатор — отдельный воркфлоу по расписанию или по записи строки — считает `done` и при `>= 4` пишет синтез, не читая опоздавших. Второй проход тем же ключом забирает строки, которые доехали позже, и дописывает их в уже существующий синтез. Опоздавший не имеет права заказывать ДР заново: строка уже есть.

21. Экран «что в полёте» из коробки — список исполнений со статусами `running` и `waiting`, фильтр в UI и API. `GET /api/v1/executions` принимает `status` из набора `canceled`, `crashed`, `error`, `new`, `running`, `success`, `unknown`, `waiting`, плюс `workflowId` и окно `startedAfter`/`startedBefore`. Лимит страницы до 250. Страница API с датой в индексе 2026-10-06: https://docs.n8n.io/connect/n8n-api/executions
Этого мало для одного логического прогона из 6 вендоров: у каждого своё execution id. Связка parent/child видна только если родитель вызывал Execute Sub-workflow и ждал. Единый run-ledger — снова внешняя таблица с вашим `run_id`. Custom data на исполнении (`$exec.customData`, нода Execution Data) есть, но дока ограничивает её Cloud Pro/Enterprise и self-hosted Enterprise или registered Community: https://docs.n8n.io/build/work-with-data/transform-data/expression-reference/execdata
Алерт на упавшую ветку, которая не уронила всё исполнение, Error Trigger не даст: он стреляет, когда исполнение закончилось ошибкой. Ветку, которая тихо не доехала, ловит только леджер (строка старше N минут всё ещё `pending`). В queue mode у воркера есть `/metrics`, если включить: это сказано на странице enable-queue-mode. Страницу стриминга логов в внешнюю систему я не открывал.

C. Кто уже сделал веер LLM, и чем это отличается от нормального оркестратора

22. Шаблон «четыре модели сразу, потом консенсус»: OpenAI, Anthropic, Gemini, Groq. Текст шаблона обещает, что вопрос уходит четырём моделям одновременно и ни одна не видит ответ другой, а упавший провайдер не роняет весь ответ. Как добавить пятого: новая ветка и число входов Merge. Я JSON шаблона не импортировал и настройку Execution order внутри него не видел. По доку из пункта 1 четыре ветки v1 исполняются последовательно, и слово «at the same time» в описании шаблона с этим доку спорит, пока в шаблоне не включён v0 или вызов через отдельные исполнения.
https://n8n.io/workflows/14497-combine-answers-from-openai-anthropic-gemini-and-groq-into-one-consensus/
Зеркало с пересказом, 29 сентября 2026: https://n8nworkflows.xyz/workflows/combine-answers-from-openai-anthropic-gemini-and-groq-into-one-consensus-14497

23. Шаблон роутера на Anthropic / Gemini / Mistral / OpenAI — это Switch в одного провайдера, не веер. Sub-workflow, на выходе нормализованный ответ и оценка токенов. Страница пишет «last update 4 months ago» относительно выгрузки 2026-10-07, то есть правка около июня 2026.
https://n8n.io/workflows/16330-route-ai-prompts-between-anthropic-google-gemini-mistral-and-openai/
Шаблона, где один прогон ждёт кворум 4 из 6 и потом добирает опоздавших, я среди открытых страниц не нашёл. DeepSeek и xAI/Grok как отдельные ветки долгого research в этих двух шаблонах не разобраны.

24. Сравнение по этой задаче (6 долгих внешних вызовов, частичный результат, добор). Это не таблица бенчмарков: чужие сайты сравнений я помечаю как чужое, первичные доки как док.

Windmill, док: шаг «branch all» запускает все ветки, и их можно включить параллельно; «skip failure» роняет одну ветку, не весь flow. For-loop умеет parallel и потолок parallelism. Каждый шаг — отдельный job воркера. При достатке воркеров время flow равно самой длинной ветке, а не сумме. Это прямо противоположно v1-веткам n8n.
https://www.windmill.dev/docs/flows/flow_branches
https://www.windmill.dev/docs/flows/architecture
https://windmill.dev/docs/flows/flow_loops

Inngest, док: `step.waitForEvent` ставит run на паузу без живого процесса. Fan-out — отдельные функции на одно событие, падение одной не останавливает другую, ретрай поштучный. `Promise.all` по шагам внутри одной функции отдаёт все результаты в одно место, но если шаг умер после ретраев, умирает вся функция. Ждущий run слот concurrency не держит.
https://www.inngest.com/docs/durable-execution/primitives/step-waitforevent
https://www.inngest.com/docs/durable-execution/guides-and-advanced/patterns/fan-out
https://www.inngest.com/docs/durable-execution/primitives/group-parallel

Trigger.dev, док, страницы с датой 2026-08-07: `wait.for` / `wait.until` длиннее нескольких секунд не считаются в compute; слот concurrency отпускается после снимка машины, для временного ожидания это 60 секунд от старта паузы. У wait есть idempotency key. Короткий poll в цикле слот не отпускает, дока прямо советует интервал заметно больше 60 секунд.
https://trigger.dev/docs/wait-for
https://trigger.dev/docs/queue-concurrency

Temporal и Prefect я по первичным докам в этом заходе не открывал. Чужое, Automation Atlas, 6 мая 2026: Temporal рассчитан на исполнения неделями и на переживание падения инфраструктуры; Prefect назван оркестратором Python-пайплайнов и «не спроектирован под длинные процессы». Цифры цен и звёзд оттуда я не пересказываю как замер. https://automationatlas.io/answers/temporal-vs-prefect-2026/
Чужое, 28 июля 2026, тот же сайт ставит n8n на 6.9/10 и пишет «параллельного исполнения нет, ветки depth-first, упавший run помечается crashed и retry идёт с начала». Первая половина совпадает с докой v1. Вторая слишком грубая: waiting на текущем master лежит в базе и рестарт обязан его поднять; crashed — это оборванный running, не пауза. https://automationatlas.io/answers/best-process-orchestration-tools-2026/
Страница n8n про Prefect — маркетинг n8n, не независимый разбор: https://n8n.io/vs/prefect/

Где n8n по этой задаче хуже, из открытых доков, не из рейтингов. Ветка холста не является единицей ретрая, кворума и рестарта. Длинное ожидание либо занимает слот воркера (если висеть в HTTP), либо требует внешней таблицы, потому что Merge не умеет «достаточно». Код внутри ноды не ходит в сеть и не в файлы. Где n8n лучше тех же инструментов: уже стоит, уже тащит остальные ~98 воркфлоу, визуальный разбор одного упавшего HTTP, готовые креды вендоров, Error Trigger в чат, и для шести запусков в сутки queue mode не обязателен.

25. Грабли, которые дока или исходник подтверждают, а не пересказ блога. Code-нода не имеет доступа к файловой системе и не делает HTTP; для этого отдельные ноды Read/Write File и HTTP Request. Python через Pyodide снят в n8n 2.0. Нативный Python с 1.111.0, стабилен в n8n 2: только `_items` / `_item`, чужие модули только если образ `n8nio/runners` их содержит и они в allowlist; на Cloud импортов нет. Раннер: дефолт 5 одновременных задач, таймаут задачи 300 секунд, payload между брокером и раннером до id_b0bbd8e1 байт.
https://docs.n8n.io/build/code-in-n8n/using-the-code-node.md
https://docs.n8n.io/hosting/configuration/environment-variables/task-runners/
Секреты: креды лежат в базе зашифрованными. Внешний сейф (AWS, Azure, GCP, Vault, 1Password Connect) дока отдаёт только Enterprise, и секрет резолвится в поле креда, не в произвольном выражении. Обновление раз в 300 секунд.
https://docs.n8n.io/administer/manage-credentials/use-external-secret-stores
https://docs.n8n.io/deploy/host-n8n/configure-n8n/basic-configuration/use-environment-variables/external-secrets
Git: самовывоз JSON есть у self-hosted без Enterprise, `n8n export:workflow --backup` и импорт обратно. Встроенные Environments поверх Git дока описывает противоречиво: страница раздела говорит Enterprise, туториал говорит Business и Enterprise. В git уезжают воркфлоу, теги и заглушки кредов и переменных, не значения секретов. Конфликт на воркфлоу n8n сам не детектит, при push/pull легко затереть правку.
https://docs.n8n.io/deploy/host-n8n/configure-n8n/use-the-command-line
https://docs.n8n.io/source-control-environments/
https://docs.n8n.io/source-control-environments/create-environments/
https://docs.n8n.io/source-control-environments/using/push-pull/
Чужое про очередь mode и память, 27 сентября 2025: на 8 ГБ VPS in-memory бинарники роняли прогон примерно после 50 файлов; filesystem на одном хосте с общим томом у них ожил, хотя дока для разнохостовых воркеров это запрещает. https://community.n8n.io/t/handling-large-binary-data-transfers-by-off-loading-to-filesystem-storage/195557

D. Вердикт для веера Deep Research на 6 вендоров раз в сутки

26. n8n годится как диспетчер этого веера и не годится как его система записи. Да, если собрать так, и только так.

Раз в сутки Schedule Trigger. Первая нода читает внешнюю таблицу: ключ уже есть и не в ошибке, значит сегодня этот вендор не стартуем. Дальше не шесть веток одного холста. Шесть отдельных исполнений: либо шесть вебхуков, либо Execute Sub-workflow с выключенным ожиданием только как запал, а результат ребёнок пишет в таблицу сам. Каждое исполнение: короткий HTTP «создай фоновую задачу» (у OpenAI это `background: true` и id ответа), запись `vendor_job_id` в таблицу, Wait на колбэк вендора с Limit Wait Time, либо цикл Wait на несколько минут и HTTP-проверка статуса. По готовности строка становится `done` или `error`, в строке лежит текст, а не «всё исполнение n8n». Синтез — седьмой воркфлоу: если `done >= 4`, собрать отчёт и поставить `synthesized_at`. Добор — тот же синтезатор следующим тиком: новые `done` дописать, старые не перезаказывать. На всех шести и на синтезаторе один Error Workflow в чат. Retry on Fail только на коротких HTTP статуса и старта, не на шаге, который уже создал задачу у вендора.

Queue mode ради шести суточных задач не нужен. Обычный режим и так пускает несколько production-исполнений сразу, лимит по умолчанию выключен. Queue mode имеет смысл, когда этих долгих ожиданий станут десятки одновременно или основной процесс начнёт тупить на редакторе. Тогда Postgres, Redis, общий encryption key, бинарное не на локальном диске воркера.

27. Не переносить в n8n. Файлы хоста и общий диск между воркерами: Code-нода туда не ходит, queue mode с filesystem-бинарниками дока запрещает, воркеры могут жить на разных машинах. Git как действие воркфлоу: экспорт JSON есть, клиента git и ревью веток нет, значения секретов в репозиторий не едут, конфликт воркфлоу молчаливый. GUI, браузер, клики по экрану вендора, локальные процессы Windows и macOS, сессии пользователя, пути `E:\` и `C:\Users\dev`. Воркер n8n этого окружения не видит, а при втором воркере оно разъедется. Туда же не класть сырой текст длинного ДР в items между нодами: лимит payload и память процесса, плюс чистка исполнений через 14 дней или 10000 записей сотрёт улику. Текст живёт в вашей таблице или в файле вне n8n, в исполнении остаётся id и статус.

28. Три дешёвых шага, которые забирают большую часть пользы, без queue mode и без нового оркестратора.

Первый. Таблица на пять колонок: `run_date`, `vendor`, `status`, `vendor_job_id`, `execution_id`. Уникальный ключ на `(run_date, vendor)`. Проверка до любого платного вызова. Это и защита от двойного заказа, и кворум, и добор опоздавших.

Второй. Один вендор — одно исполнение, старт через свой вебхук. Параллельность даёт сам n8n между исполнениями. Холст с шестью ветками и Merge даёт очередь и стоп на первом молчуне.

Третий. Один Error Workflow на эти воркфлоу плюс Retry on Fail на коротких HTTP. Синтезатор по расписанию читает таблицу, а не ждёт Merge. Пока строк `done` меньше четырёх, он молчит. На четвёртой пишет синтез.

E. Чего я не проверил, и почему

Версию, режим (`regular` или `queue`), базу и число воркеров на n8n.palo-alto.ai я не открывал: в задании стоит «queue-mode неизвестен», а ходить в боевой инстанс этот заход не включал. От версии зависит, какой у вас Wait: дока всё ещё описывает порог 65 секунд, исходник master от 2026-10-07 уже всегда пишет паузу в базу, issue связывает смену с 2.14.0.

Я не импортировал JSON шаблона 14497, поэтому не знаю, стоит ли там Execution order v0. Утверждение «четыре LLM одновременно» остаётся текстом автора шаблона.

Я не открывал `wait-tracker.ts`, поэтому интервал опроса ~5 секунд — формулировка смёрженного PR, не строка, которую я прочитал в файле сегодня. Сам `Wait.node.ts` я прочитал: порога 65000 там нет.

Я не подтверждал в исходнике, уходит ли Execute Sub-workflow с wait=false в отдельный джоб Redis или бежит внутри процесса родителя. Дока описывает только семантику «не ждать и не получить выход».

Дефолт Timeout у HTTP Request в официальной странице не назван. 300000 мс — сообщение на форуме 11 августа 2026.

Первичные доки Temporal, Prefect, Dagster, Airflow и страницу Python `asyncio` я в этом заходе не открывал. Сравнение с ними в пункте 24 опирается на доки Windmill, Inngest и Trigger.dev плюс две обзорные статьи, которые помечены как чужие. Бенчмарка «6 вендоров, 40 минут, на вашем железе» нет ни у кого из открытых источников, и я его не ставил.

Страницу стрима логов n8n во внешнюю систему я только увидел ссылкой из queue mode и не читал. Покрытие Prometheus на вашем инстансе неизвестно.

Поведение Wait после рестарта я не воспроизводил. Есть механизм в исходнике, тест в тексте PR и два противоречивых треда форума. На вашей базе это не прогонялось.

Длинные API Anthropic, Gemini, Grok, Mistral и DeepSeek на предмет «фоновый id + вебхук, как у OpenAI» я в этом заходе не открывал. Схема из пункта 26 для них верна только там, где вендор умеет отдать id и статус. Кто умеет только синхронный ответ на 40 минут, тот в n8n упрётся в сокет HTTP и в слот воркера; это надо смотреть по доке каждого вендора отдельно.


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

{"lang":"ru","topic":"n8n как оркестратор параллельного Deep Research: параллелизм, долгие вызовы, кворум","one_line":"Годится ли self-hosted n8n как оркестратор суточного веера Deep Research по 5-6 LLM-вендорам: реальный параллелизм, долгие внешние вызовы, кворум и добор, сравнение с Temporal/Prefect/Windmill/Inngest/Trigger.dev.","key_findings":["Ветки одного исполнения n8n идут по очереди (Execution order v1: одна до конца, затем следующая; сверху вниз, на одной высоте слева направо). Реальная параллельность возникает только между отдельными исполнениями. Практик 01.12.2025 замерил на двух HTTP-ветках: второй стартует примерно через 10 с после первого. Это чужое наблюдение одного воркфлоу, не бенчмарк.","Queue mode (EXECUTIONS_MODE=queue) параллелит исполнения, а не ветки: main кладёт id в Redis (Bull), воркеры забирают. Дефолт worker --concurrency 10 (рекомендация n8n: 5 и выше). В обычном режиме лимита нет, пока не задан N8N_CONCURRENCY_PRODUCTION_LIMIT (дефолт -1). Для 6 суточных задач queue mode не нужен. В queue mode нужны Postgres, Redis, общий N8N_ENCRYPTION_KEY, бинарные данные не в filesystem.","Merge ждёт все входы и кворума «4 из 6» не умеет: упавшая или молчащая ветка блокирует синтез. Execute Sub-workflow с wait=false не отдаёт родителю результат ребёнка. Опция есть с 1.26.0. По отчётам сообщества на «Run once with all items» нода не дожидается всех подворкфлоу, а на 1.57.0 wait=false вместе с Continue on error обрывал ребёнка.","Wait: дока всё ещё пишет, что ожидание короче 65 с не уходит в базу, но в master Wait.node.ts порога 65000 уже нет (PR #27066, смёржен 02.04.2026; связан с n8n 2.14.0). Waiting-исполнения лежат в базе и не чистятся. Отчёты о переживании рестарта противоречивы: «да, если жив том с БД» (январь 2026) против зависания Waiting с версии 2.16 (апрель 2026). Поведение на нашей базе не воспроизводилось. Версия инстанса не проверена.","Deep research у вендоров длится десятки минут. OpenAI предписывает background:true и poll GET /v1/responses/{id} или вебхук; ответ хранится около 10 мин, режим несовместим с ZDR. Модели o3/o4-mini-deep-research помечены на выключение 23.07.2026. Держать HTTP 40 минут в одной ноде плохо: слот воркера занят, у HTTP Request чужой замер дефолтного таймаута 300000 мс, N8N_AI_TIMEOUT_MAX равен 1 часу. Правильный каркас: старт (секунды) + Wait на вебхук либо цикл Wait → HTTP-статус.","В n8n нет встроенных DLQ, ключа идемпотентности и кворума. Есть Retry on Fail (фиксированная пауза, без экспоненты), Error Workflow с Error Trigger и шаблоны DLQ на Google Sheets или Postgres. Предупреждение от 10.06.2026: Retry при потерянном ответе создаёт дубль платного заказа. Идемпотентность, кворум и добор строятся только внешней таблицей со статусами pending/done/error и ключом (run_date, vendor).","История исполнений чистится по умолчанию: старше 336 часов (14 суток) или больше 10000 записей; waiting/running/new и помеченные не удаляются. Экран исполнений n8n не архив, сырые ответы ДР надо хранить вне n8n. Единого run_id на 6 вендоров нет: у каждой ветки свой execution id. Execution Data (customData) ограничена планами Pro/Enterprise. Алерт на тихо не доехавшую ветку даёт только леджер (строка старше N минут в pending).","Публичные шаблоны не закрывают задачу: шаблон 14497 (консенсус OpenAI/Anthropic/Gemini/Groq) заявляет «одновременно», но при Execution order v1 ветки идут по очереди; шаблон 16330 — роутер-Switch, а не веер. Шаблона с кворумом 4 из 6 и добором опоздавших найдено не было. Windmill (branch all, parallel for-loop, каждый шаг — отдельный job), Inngest (waitForEvent без живого процесса, fan-out отдельными функциями), Trigger.dev (wait.for не считается в compute, idempotency key) устроены под такую задачу лучше.","Грабли n8n: Code-нода без доступа к ФС и HTTP; Pyodide-Python снят в 2.0, нативный Python с 1.111.0 с allowlist модулей, раннер по умолчанию 5 одновременных задач, таймаут 300 с. N8N_PAYLOAD_SIZE_MAX 16 МиБ; бинарные в памяти по умолчанию, filesystem в queue mode не поддерживается. Внешние секрет-сторы только Enterprise. Environments/Git описаны противоречиво (Enterprise или Business), конфликты воркфлоу не детектируются, значения секретов в git не уезжают.","Вердикт: n8n годится как диспетчер веера, но не как система записи. Схема: Schedule Trigger (раз в сутки) → проверка внешней таблицы → шесть отдельных исполнений (вебхук на вендора) → короткий HTTP-старт с background-режимом, запись vendor_job_id → Wait на колбэк или цикл Wait + статус → синтезатор по расписанию (done >= 4 пишет синтез, следующий тик дописывает опоздавших) → один Error Workflow в чат. Retry on Fail только на коротких HTTP.","Не переносить в n8n: файловую систему хоста и общий диск воркеров, git как действие воркфлоу, GUI/браузер и клики, локальные процессы Windows/macOS и пути E:\\ и C:\\Users, сырой текст длинных ДР в items между нодами. Три дешёвых улучшения: таблица из 5 колонок с уникальным ключом (run_date, vendor); один вендор = одно исполнение через свой вебхук вместо холста с Merge; один Error Workflow плюс Retry на коротких HTTP и синтезатор, читающий таблицу."],"recommendations":["Завести внешнюю таблицу-леджер (run_date, vendor, status, vendor_job_id, execution_id) с уникальным ключом (run_date, vendor) и проверять её до любого платного вызова: это даёт защиту от двойного заказа, кворум и добор.","Не строить веер шестью ветками одного холста с Merge: запускать отдельное исполнение на каждого вендора (вебхук либо Execute Sub-workflow с выключенным ожиданием как запал).","Для долгих вызовов использовать двухшаговую схему: короткий HTTP-старт с id задачи (у OpenAI background:true), затем Wait на вебхук с Limit Wait Time или цикл Wait + HTTP-статус; не держать сокет на 40 минут.","Синтез вынести в отдельный воркфлоу по расписанию: при done >= 4 писать синтез, следующим тиком дописывать опоздавших без перезаказа.","Повесить один Error Workflow на все воркфлоу веера и синтезатор; Retry on Fail включать только на короткие HTTP статуса и старта, не на шаг, создающий задачу у вендора.","Сырой текст ответов хранить в таблице или файле вне n8n (в исполнении только id и статус) из-за pruning через 14 суток и лимитов payload.","Не включать queue mode ради 6 суточных задач; рассматривать его, когда одновременных ожиданий станут десятки или основной процесс начнёт тормозить редактор.","До внедрения проверить версию n8n.palo-alto.ai (поведение Wait, порог 65 с, срок политики пропущенных запусков Schedule) и воспроизвести рестарт при Wait на своей базе.","Если вендор не умеет фоновый id + вебхук, либо оставлять его вне n8n, либо рассматривать Windmill/Inngest/Trigger.dev/Temporal или Python asyncio + cron."],"entities":{"people":[],"companies":["n8n","OpenAI","Anthropic","Google (Gemini)","xAI (Grok)","Mistral","DeepSeek","Groq","Windmill","Inngest","Trigger.dev","Temporal","Prefect","Dagster","Airflow","Automation Atlas"],"products_tools":["n8n","n8n queue mode (Redis/Bull)","Wait node","Schedule Trigger","Merge node","Loop Over Items (Split in Batches)","Execute Sub-workflow","HTTP Request node","Error Trigger / Error Workflow","Execution Data","Code node (Pyodide / native Python)","n8nio/runners","OpenAI Responses API (background mode)","o3-deep-research / o4-mini-deep-research","Windmill","Inngest (step.waitForEvent)","Trigger.dev (wait.for)","Temporal","Prefect","Redis","Postgres","Google Sheets","Prometheus /metrics","asyncio + cron"]},"open_questions":["Версия, режим (regular или queue), база и число воркеров на n8n.palo-alto.ai не проверены, а от версии зависит поведение Wait (порог 65 с).","Поведение Wait после рестарта на нашей базе не воспроизводилось; отчёты сообщества противоречивы (в том числе зависания с 2.16).","Уходит ли Execute Sub-workflow с wait=false в отдельный джоб Redis или бежит внутри процесса родителя, не подтверждено по исходнику.","Стоит ли в шаблоне 14497 Execution order v0 и реально ли четыре ветки идут одновременно, не проверено (JSON не импортировался).","Интервал опроса WaitTracker (около 5 с) взят из описания PR, сам wait-tracker.ts не открывался.","Дефолт Timeout у HTTP Request в официальной доке не назван; 300000 мс — сообщение форума от 11.08.2026.","Какие вендоры (Anthropic, Gemini, Grok, Mistral, DeepSeek) умеют фоновый id + вебхук как OpenAI, не проверено; для умеющих только синхронный ответ схема не годится.","Первичные доки Temporal, Prefect, Dagster, Airflow и Python asyncio не открывались; сравнение опирается на доки Windmill, Inngest, Trigger.dev и две обзорные статьи, бенчмарка «6 вендоров, 40 минут» нет.","Стриминг логов n8n во внешнюю систему не читался; покрытие /metrics на инстансе неизвестно.","Секция Gemini в отчёте содержит только повтор заказа без ответа по существу (вторая секция помечена REJECTED echo), поэтому вклад этого вендора отсутствует."],"related_concepts":["Deep Research fan-out и кворум 4 из 6","Идемпотентность и run-ledger","Dead-letter queue и retry с backoff","Durable execution (Temporal / Inngest / Trigger.dev)","Webhook callback против polling","n8n queue mode и масштабирование","Pruning истории исполнений","Оркестратор против системы записи","Альфа-протокол Recall + DR","Windmill как альтернатива оркестрации"]}
