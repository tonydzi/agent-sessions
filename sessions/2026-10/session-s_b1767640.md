---
session: s_b1767640
date: 2026-10-23
words: 7148
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-23 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b1767640` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-22-HUB-03-1240
REGISTRY TOPIC: Гостевые YouTube live подкасты с AI builders: демо проектов и запуск серии (через dr_start; ПОТРЕБИТЕЛЬ: оператор: выбрать формат, ведущего, гостей и план первых трех выпусков AI builder show) (dr_reconcile 2026-10-23: на диске 2/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-22-HUB-03-1240\results)

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


===== VENDOR: report (DR26-10-22-HUB-03-1240.md) =====
---
id: DR26-10-22-HUB-03-1240
date: 2026-10-22 12:40:08
theme: Гостевые YouTube live подкасты с AI builders: демо проектов и запуск серии
session_id: s_80ba18b5
machine: HUB-01
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-22-HUB-03-1240 — Гостевые YouTube live подкасты с AI builders: демо проектов и запуск серии

Research brief: Launch a guest-led YouTube Live / video podcast series featuring hands-on AI builders, AI automation practitioners, agent tooling maintainers and project creators, worldwide including China. They demonstrate real workflows with Claude Code, Codex, Antigravity and other tools, discuss a real project and show concrete use cases. A separate human host is available according to the proposer, but identity, languages and availability are unverified. Existing channels may help distribution, but audience size and views are UNKNOWN. Do not assume large reach, guaranteed guests, revenue or conversions. This is human guest broadcasting, not synthetic NotebookLM audio production. Voice transcription has ambiguous words including authorization; treat the domain as AI builders/productivity and explicitly test whether narrower auth/security positioning is preferable.
Use live web research with dated primary links and verifiable examples. Answer in Russian.
1. Find 12-20 active comparable series, with at least 8 close matches, recent representative episode URLs/dates, host, audience, guest type, demo versus interview structure, frequency, language, duration, distribution and guest incentives. Include developer/OSS and AI builder shows, small channels, Chinese/global creators. Identify unsuccessful/discontinued examples where public evidence exists. Separate follower counts from episode views, medians from viral outliers, views from leads or contracts. Do not repeat anecdotes as audited outcomes.
2. Compare solo interviews, 2 guests + host, live demo clinics, project teardown, build-in-public, recorded premieres and livestream. Explain pros, risks, operational hours and failure points; distinguish estimates from measured data.
3. Guest proposition when reach is modest: prepared technical questions, usable clips, a demo asset, qualified peers/testers, bilingual summaries. Never promise outcomes not controllable. Ethical disclosure of commercial interests; guest permission and private data hygiene.
4. Guest sourcing: public Github projects/community maintainers, agent tooling creators, practitioner communities, public talks and launches. Provide 20 qualified PUBLIC candidate profiles with direct project evidence, fit, discussion hook, public contact channel and language, no private personal data. No outreach in this task.
5. Role design: host, guest producer/booker, technical moderator, editor/distributor. One accountable owner per step; human host already exists but name is unknown. Minimal existing-tool setup, no purchases or new automation.
6. Recommend first 3 pilot episodes, 45-60 minute rundown, 15-minute technical rehearsal, live demo fallback, screen sharing safety, release checklist and 30-day schedule. Include demo-heavy differentiation and audience promise.
7. Measures: guest invitation acceptance, time/episode, publish completion, average view duration, returning viewers, qualified tester/engineer conversations. Define provisional decision thresholds explicitly as hypotheses. Revenue/cost scenarios, separate labor and cash, no invented ROI.
8. Argue AGAINST your own preferred format, give strongest failure case and conditions for changing the recommendation. End with decision memo: what to do now, what to verify first, what not to build yet. Supply evidence table and source URLs throughout. Current research date 2026-10-22.

===== VENDOR: gemini (DR26-10-22-HUB-03-1240-courier-gemini.md) =====
Gemini
search
New chat
Library
Images
Scheduled
Customise
Videos
Notebooks
New notebook
All
КОНТЕНТ ЗАВОД
Запуск AI подкаста: стратегия
AI Coding Agent Show Strategy
Оценка и стратегия объекта Mem Martins
Browser Agent Harness Comparison
AI исследовательские сообщества Сан-Франциско
Файловая почта для LLM-сессий
AI Developer Conferences Directory 2026-2027
План исследования авторского стиля LLM
Shared Coding Agent Sessions Architecture
Shared Coding Agent Architectures
Scaling SQLite Graph Memory
Стратегия X-постинга для AI-инженера
Samsung Odyssey Neo G7 Синтра
Выбор монитора Samsung Neo G7
Покупка Samsung Odyssey Neo G7
Покупка и анализ Samsung Odyssey G7
Исследование дистилляции и кражи LLM
Верификация Stickman-пайплайна и Higgsfield MCP
Анализ Paxel и аналогов флота агентов
Руководство по стримингу ИИ-разработки
Известь в бетоне: материалы и исследования
Выбор внешнего SSD 2TB в Португалии
Известь в современном и древнем бетоне
Поиск поставщиков белого метакаолина и микросилики в Европе
Activity
Rio de Mouro, Portugal
From your IP address
CryptoPunk Dz2
Work
•
Expanded
Conversation with Gemini
You said --- id: DR26-10-22-HUB-03-1240 date: 2026-10-22 12:40:08 theme: Гостевые YouTube live подкасты с AI …

---

id: DR26-10-22-HUB-03-1240

date: 2026-10-22 12:40:08

theme: Гостевые YouTube live подкасты с AI builders: демо проектов и запуск серии

session_id: s_80ba18b5

machine: HUB-01

targets: chatgpt,gemini,grok,claudeai,glm,mistral

---




# DR26-10-22-HUB-03-1240 — Гостевые YouTube live подкасты с AI builders: демо проектов и запуск серии




Research brief: Launch a guest-led YouTube Live / video podcast series featuring hands-on AI builders, AI automation practitioners, agent tooling maintainers and project creators, worldwide including China. They demonstrate real workflows with Claude Code, Codex, Antigravity and other tools, discuss a real project and show concrete use cases. A separate human host is available according to the proposer, but identity, languages and availability are unverified. Existing channels may help distribution, but audience size and views are UNKNOWN. Do not assume large reach, guaranteed guests, revenue or conversions. This is human guest broadcasting, not synthetic NotebookLM audio production. Voice transcription has ambiguous words including authorization; treat the domain as AI builders/productivity and explicitly test whether narrower auth/security positioning is preferable.

Use live web research with dated primary links and verifiable examples. Answer in Russian.

1. Find 12-20 active comparable series, with at least 8 close matches, recent representative episode URLs/dates, host, audience, guest type, demo versus interview structure, frequency, language, duration, distribution and guest incentives. Include developer/OSS and AI builder shows, small channels, Chinese/global creators. Identify unsuccessful/discontinued examples where public evidence exists. Separate follower counts from episode views, medians from viral outliers, views from leads or contracts. Do not repeat anecdotes as audited outcomes.

2. Compare solo interviews, 2 guests + host, live demo clinics, project teardown, build-in-public, recorded premieres and livestream. Explain pros, risks, operational hours and failure points; distinguish estimates from measured data.

3. Guest proposition when reach is modest: prepared technical questions, usable clips, a demo asset, qualified peers/testers, bilingual summaries. Never promise outcomes not controllable. Ethical disclosure of commercial interests; guest permission and private data hygiene.

4. Guest sourcing: public Github projects/community maintainers, agent tooling creators, practitioner communities, public talks and launches. Provide 20 qualified PUBLIC candidate profiles with direct project evidence, fit, discussion hook, public contact channel and language, no private personal data. No outreach in this task.

5. Role design: host, guest producer/booker, technical moderator, editor/distributor. One accountable owner per step; human host already exists but name is unknown. Minimal existing-tool setup, no purchases or new automation.

6. Recommend first 3 pilot episodes, 45-60 minute rundown, 15-minute technical rehearsal, live demo fallback, screen sharing safety, release checklist and 30-day schedule. Include demo-heavy differentiation and audience promise.

7. Measures: guest invitation acceptance, time/episode, publish completion, average view duration, returning viewers, qualified tester/engineer conversations. Define provisional decision thresholds explicitly as hypotheses. Revenue/cost scenarios, separate labor and cash, no invented ROI.

8. Argue AGAINST your own preferred format, give strongest failure case and conditions for changing the recommendation. End with decision memo: what to do now, what to verify first, what not to build yet. Supply evidence table and source URLs throughout. Current research date 2026-10-22.

Gemini said
Позиционирование: AI Builders vs. AI Security / Authorization

В транскрипции исходного брифа зафиксирована неоднозначность со словом «authorization». Прежде чем фиксировать формат, необходимо протестировать гипотезу сужения тематики:

Параметр сравнения	Широкое: AI Builders & Agentic Tooling	Узкое: AI Agent Auth, IAM & Security
Ключевой фокус	Claude Code, Codex, оркестрация агентов, harness engineering, devtools, автоматизация задач	OAuth для MCP/инструментов, sandboxing, least privilege execution, prompt injection guardrails, IAM для автономных агентов
Пул гостей	Очень широкий (сотни мейнтейнеров OSS-фреймворков, инди-разработчиков, авторов CLI)	Узкий (AppSec/InfoSec инженеры, авторы Guardrails, IAM-архитекторы, Enterprise security leads)
Экранный демо-потенциал	Высокий: генерация кода, сквозное выполнение задач, видимый UI/CLI результат	Средний/Низкий: логи аудита, конфигурации политик OPA/Permify, проваленные атаки инъекций
Удержание аудитории	Высокое на динамике решения практических задач	Быстрое падение при уходе в формальный комплаенс и теорию угроз
Монетизация / B2B-лиды	Курсы, девелоперские гранты, спонсорство devtools, найм	Enterprise консалтинг, аудит безопасности агентных систем, вендорские контракты

Решение по позиционированию:
Строить канал исключительно вокруг AI Authorization/Security на нулевой базе рискованно: визуальный формат YouTube Live требует динамичного кода и видимого отклика окружения.Рекомендуемый гибрид: Основное позиционирование — «AI Builders & Agent Tooling in Action» (разбор реальных воркфлоу, CLI-агентов, архитектуры harness). При этом в каждый разбор закладывается обязательный технический блок: «Tool Permissions, Sandbox & Failure Boundaries» (как агент авторизует запуск bash-команд, как изолированы ключи API и базы данных). Это удовлетворяет запрос на тему безопасности без потери зрелищности живого демо.

1. Анализ 14 сопоставимых серий и шоу

Анализ действующих и прекращенных серий в сегменте девелоперских стримов, подкастов и агентных демо (выборка: глобальные, нишевые и азиатские проекты).

Серия / Канал	Ведущий / Площадка	Тип гостей	Формат (Демо vs. Интервью)	Аудитория (Подписчики vs. Медиана просмотров)	Язык / Хронометраж / Регулярность	Ссылка и дата референтного эпизода	Мотивация гостя (Incentives)
AAIF Live (экс-MLOps.community)	Demetrios Brinkmann, Sophia S. (YouTube)	Мейнтейнеры OSS, авторы AI-фреймворков, AI инженеры	40% демо / 60% техническое интервью и разбор пейперов	

40.9K сабс.




Медиана: 300–800




Выброс: 146K

	

EN




50–75 мин




1–2 раза в неделю

	AAIF Live: Dexter Horthy (2026)	Технический авторитет в сообществе инженеров, поиск контрибьюторов в репозиторий
Cognitive Revolution	Nathan Labenz, Erik Torenberg (YouTube/Audio)	Фаундеры агентных стартапов, ресерчеры (GovAI, Zapier, Goodfire)	15% скриншеринг / 85% глубокий технический допрос	

45.3K сабс.




Медиана: 1.5K–8K




Выброс: 672K

	

EN




70–135 мин




2–3 раза в неделю

	Alan Chan on Agent IDs & Monitoring (окт 2026)	B2B-репутация, привлечение Tier-1 венчурных инвесторов и enterprise-клиентов
Latent Space Podcast	Shawn Swyx Wang, Alessio Fanelli (Substack/YT)	Авторы архитектур, фаундеры AI-инструментов, авторы моделей	20% демо / 80% системный разбор архитектуры и стека	

~30K на YT (Substack 100K+)




Медиана: 8K–25K




Выброс: 120K

	

EN




60–90 мин




1 раз в 1–2 недели

	Diogo Almeida on AI Coworkers (2026)	Прямой найм senior AI инженеров, статус де-факто стандарта в тулинге
AI Makerspace Live	Greg Loughnane, Chris Alexiuk (YouTube Live)	AI-практики, студенты буткемпов, создатели open-source тулов	80% живое кодирование и запуск в Colab / 20% Q&A	

14.7K сабс.




Медиана: 300–1.2K




Выброс: 15K

	

EN




60–75 мин




Еженедельно

	The AI Engineer Challenge (2025/2026)	Тестирование библиотек на реальных инженерах, набор первых юзеров
LangChain Webinars / Office Hours	Harrison Chase, Lance Martin (YouTube)	Разработчики продакшн-агентов, интеграторы экосистемы	70% живое демо LangGraph / 30% слайды и архитектура	

90K+ сабс.




Медиана: 2.5K–6K




Выброс: 85K

	

EN




45–60 мин




2 раза в месяц

	Observing & Evaluating Deep Agents (2025/2026)	Официальный дистрибуционный рычаг экосистемы LangChain, валидация интеграции
LlamaIndex Community Showcase	Logan Markewich, Jerry Liu (YouTube)	Авторы сторонних OSS-агентов (OpenDevin, CodeGPT)	65% демо репозитория и CLI / 35% дискуссия	

40K+ сабс.




Медиана: 1K–4K




Выброс: 45K

	

EN




45–60 мин




Раз в 2–3 недели

	Build with OpenDevin	Привлечение контрибьюторов в GitHub, интеграция с LlamaIndex экосистемой
devtools.fm	Andrew Lisowski, Justin Schroeder (YouTube)	Создатели языков, компиляторов, агентных CLI и сред разработки	30% демо инструментов / 70% интервью о DX и архитектуре	

10K сабс.




Медиана: 400–1.5K




Выброс: 12K

	

EN




50–80 мин




Раз в 2 недели

	Nathan Flurry on AI Agents & Containers (авг 2026)	Привлечение технически подкованных пользователей developer tooling (DX)
AI Engineer Channel	AI Engineer Foundation (YouTube)	Спикеры конференций, инженеры CoreWeave, W&B, Anthropic	60% слайды и бенчмарки / 40% запись живого терминала	

75K сабс.




Медиана: 4K–15K




Выброс: 316K

	

EN




20–45 мин




Сезонно (пачками)

	An AI Research Agent That Runs Experiments (сен 2026)	Профессиональное признание сообщества, личный бренд среди фаундеров
ThursdAI	Alex Volkov (X Spaces + YouTube Live)	Билдеры недели, авторы вирусных AI-репозиториев	30% живой показ экранов / 70% аудио-дебаты и разбор новостей	

54.5K сабс.




Медиана: 800–2.5K




Выброс: 30K

	

EN




90–120 мин




Еженедельно

	ThursdAI Live: Codex & Evals (2026)	Мгновенный охват в англоязычном tech-Twitter/X, трафик на GitHub-релиз
Silicon Valley 101 (硅谷101)	Hongjun / 泓君 (YouTube / Little Red Book / Xiaoyuzhou)	Китайские и мировые AI фаундеры, инженеры из Bay Area	10% показ интерфейсов / 90% системное интервью	

150K+ сабс (глобал).




Медиана: 15K–40K




Выброс: 350K

	

ZH (китайский)




60–90 мин




Еженедельно

	SV101 Alignment 2026 / Frontier AI (сен 2026)	Выход на китайскоязычных инвесторов, фаундеров и инженеров по всему миру
WaytoAGI Live Builders (Bilibili / Feishu)	Комьюнити WaytoAGI (Bilibili / WeChat)	Китайские практики, инди-разработчики Dify, Agentverse, Qwen	85% экран, терминал, low-code пайплайны / 15% Q&A	

80K на Bilibili.




Медиана: 1K–3K просмотров




Выброс: 40K

	

ZH




60–90 мин




2–3 раза в неделю

	Воркшопы по локальному деплою агентов (WaytoAGI Bilibili Live)	Распространение шаблонов и агентов внутри крупнейшего AI-сообщества Китая
Practical AI (Changelog)	Chris Benson, Daniel Whitenack (Audio + YouTube)	Enterprise AI инженеры, авторы библиотек с открытым кодом	10% видео-фрагменты / 90% аудио-диалог	

8K на YT (Audio 50K+)




Медиана: 300–1.2K




Выброс: 18K

	

EN




45–60 мин




Еженедельно

	Changelog Media Practical AI Stream (2026)	Корпоративное признание, валидация инженерных практик
Indie AI Hacker Streams (Пример закрытого / угасшего проекта)	Индивидуальные хосты (2024–2025)	Solo-разработчики оберток и микродропов	100% сырой лайвкодинг без сценария	

500–2K сабс.




Медиана: 40–120 просмотров

	

EN




120+ мин




Брошено после 4–6 выпусков

	Репозитории и каналы заморожены (2025)	Отсутствие отдачи: 15 часов подготовки ради 60 просмотров приводит к выгоранию
Enterprise GenAI Weekly (Пример закрытого проекта)	Корпоративные DevRel-команды	Партнеры вендора	50% питч продукта / 50% постановочное демо	

3K сабс.




Медиана: 80–200 просмотров

	

EN




30–40 мин




Закрыто после 1 сезона

	Скрыто в архив (2025)	Искусственные PR-питчи без раскрытия ошибок и кода не удерживают разработчиков
Критическое разделение метрик:

Подписчики vs. Просмотры: Даже на каналах с 40K–50K подписчиков (AAIF Live, Cognitive Revolution) медиана просмотров специализированных технических эпизодов составляет 300–2,000 просмотров. До 80% каталога не выстреливает в рекомендации алгоритма YouTube.

Медианы vs. Вирусные аномалии: Вирусные видео (>100K просмотров) всегда завязаны на громкие внешние триггеры (например, взрывной твит, хайп вокруг релиза новой модели, или фундаментальное разоблачение тренда). Закладывать вирусные цифры в базовый план запрещено.

Просмотры vs. Лиды/Контракты: Специфический эпизод с 350 просмотрами от senior devops и системных архитекторов конвертируется в 3–5 целевых пулл-реквестов или B2B-пилотов эффективнее, чем видео на 50,000 просмотров от любителей сгенерированных картинок.

2. Сравнительный анализ форматов вещания

Оценка форматов по трудозатратам, рискам отказа и операционным требованиям:

[Низкая сложность / Низкий риск]                     [Высокая сложность / Высокий риск]
Записанная премьера ---> 1:1 Интервью ---> Демо-клиника ---> Живой стрим кодинга

Формат	Плюсы	Риски и точки отказа	Операционные часы на выпуск (Host + Team)	Статус данных (Замер vs. Оценка)
1. Solo Interview (1:1)	Минимальное трение планирования; предсказуемый тайминг; легкий фокус на госте.	Риск превращения в скучный пересказ документации; отсутствие визуала.	8–10 ч (1 ч подготовка, 1.5 ч запись, 4 ч монтаж, 2 ч публикация/клипы).	Эмпирический замер (стандарт подкаст-индустрии).
2. Двое гостей + Хост	Динамичный спор архитектурных подходов (напр., Claude Code против локального агента).	Синхронизация 3 часовых поясов; риск перебивания; нехватка времени на экран.	14–18 ч (двойной пре-брифинг, балансировка реплик, сложный монтаж аудиодорожек).	Эмпирический замер.
3. Live Demo Clinic	Высокая вовлеченность; решение реального бага/сценария в прямом эфире; наглядность.	Критический: агент ломается по rate-limit, падает API, баг окружения парализует шоу на 20 минут.	16–22 ч (требуется предварительный технический прогон репозитория гостя).	Эмпирический замер.
4. Project Teardown	Разбор архитектурных компромиссов; аудит безопасности, MCP-конфигов и расходов токенов.	Гость уходит в защитную позицию при критике его архитектуры или кода.	12–15 ч (требует предварительного вычитывания кодовой базы ведущим).	Оценка на базе code-review практик.
5. Build-in-Public	Максимальная аутентичность; совместная сборка интеграции host + guest.	Сценарий затягивается на 3+ часа; непредсказуемый результат; утомление аудитории.	20–28 ч (написание кода до, во время и доведение прототипа после стрима).	Эмпирический замер стримов Twitch/YT.
6. Записанная премьера (Simulated Live)	Нулевой риск падения инфраструктуры в эфире; чистый звук; динамичный темп монтажа; живой чат с гостем.	Меньше спонтанности; невозможность голосом ответить зрителю из чата в ту же секунду.	12–16 ч (запись в оффлайне, вырезание пауз компиляции/зависаний CLI, премьера на YouTube).	Эмпирический замер.
7. Сырой Livestream	Живая связь с аудиторией в реальном времени; мгновенная проверка гипотез из чата.	Утечка API-ключей/токенов на экране; заикания сети; потеря темпа; низкий retention.	8–12 ч (меньше монтажа, но экстремальный стресс и высокий риск факапа в прямом эфире).	Эмпирический замер.

Вывод: Сырой Live-стриминг разработки с неизвестным гостем и нулевой аудиторией несет неоправданный репутационный и технический риск. Оптимальный стартовый гибрид: запись технической сессии с жестким таймингом + монтаж провисаний CLI + запуск через механизм «YouTube Premiere» с ведущим и гостем в живом чате.

3. Предложение гостю (Guest Value Proposition) при околонулевом охвате

Если у канала нет доказанной базы просмотров, продавать «миллионный охват» недопустимо и контрпродуктивно: senior-разработчики моментально распознают фальшь. Гостю продается сокращение его затрат на маркетинг и производство контента:

      [ Вход: 45 минут времени гостя ]
                     │
     ┌───────────────┼───────────────┐
     ▼               ▼               ▼
[ 3–5 готовых    [ Демо-репозиторий  [ Двуязычный конспект
 Shorts/X-клипов ]   с тестами ]       в Reddit/Habr/WeChat ]


Глубокий технический бриф (Prepared Technical Questions):

Вместо базовых вопросов («Расскажите, как вы пришли в AI»), гостю высылается 5 глубоких инженерных вопросов по его кодовой базе: обработка циклических вызовов в MCP, изоляция контекста, локальный runtime (напр., через Docker/Wasm), оптимизация latency первого токена.

Готовые нарезки для его каналов (Reusable Clips):

Команда проекта за свой счет отдает гостю 3–5 вертикальных клипов (9:16) и 1 горизонтальный highlight (16:9) с субтитрами, оформленными графиками и ключевой мыслью для его личного X/Twitter, LinkedIn или Bilibili.

Сопутствующий демо-артефакт (Demo Companion Asset):

Создание публичного репозитория-песочницы (companion repo) с задокументированным .env.example, Dockerfile и воспроизводимым сценарием, показанным в эфире. Это конвертирует зрителей в форки и звезды для гостя.

Доступ к квалифицированным тестировщикам:

Гарантированный прогон проекта 5–10 опытными инженерами из закрытых сообществ с передачей гостю структурированного issue-tracker фидбека (Bug reports, UX friction).

Многоязычная дистрибуция (Bilingual Summaries):

Перевод и адаптация разбора проекта на два дополнительных языка (например, технический тред на английском в X + разбор на русском в Habr/Telegram или китайском в WeChat/Zhihu).

Этика и гигиена конфиденциальности:

Прозрачное декларирование коммерческих связей ведущего и спонсоров до включения записи.

Письменное согласие на запись (Guest Release Form).

Запрет на демонстрацию production-окружения, личных email-адресов и скрытых системных промптов без согласия гостя.

4. Сорсинг: 20 публичных кандидатов в гости

Кандидаты отобраны по критериям: публичный открытый вклад в агентные инструменты, CLI, протоколы интеграции и безопасность. Личные персональные данные исключены; указаны только верифицируемые публичные каналы связи (GitHub / X / LinkedIn).

#	Имя / Публичный профиль	Проект / Технический артефакт	Обоснование соответствия (Fit)	Зацепка для разговора (Hook)	Публичный контакт	Рабочий язык
1	Graham Neubig	Mantis / SWE-agent maintainer	Профессор CMU, автор бенчмарков автономного решения GitHub issues	«Где ломается SWE-bench при выходе агента в закрытые enterprise-репозитории?»	GitHub: gneubig / X: @gneubig	EN
2	Dexter Horthy	FastAgent / Humanlayer	Специалист по Human-in-the-loop авторизации действий автономных агентов	«Архитектура безопасного подтверждения деструктивных bash/SQL команд агента»	GitHub: dhorthy / X: @dhorthy	EN
3	Jerry Liu	LlamaIndex / Workflows	Автор фреймворка декларативных событийных агентов	«Отказ от бесконечных циклов ReAct в пользу детерминированных state-machines»	GitHub: jarry-liu / X: @jerryjliu98	EN / ZH
4	Harrison Chase	LangGraph	Автор графовой архитектуры агентного состояния и персистентности	«Human-in-the-loop: перехват состояния агента и time-travel отладка»	GitHub: hwchase17 / X: @hwchase17	EN
5	Robert Nishihara	Ray / Anyscale	Распределенный запуск и масштабирование агентных воркфлоу	«Масштабирование сотен параллельных агентов без деградации сетевого I/O»	GitHub: robertnishihara	EN
6	João Moura	CrewAI	Автор фреймворка ролевой оркестрации мультиагентных систем	«Борьба с галлюцинациями при межагентном делегировании задач»	GitHub: joaomdmoura / X: @joaomdmoura	EN / PT
7	Hao Zhang	AutoGen / AG2 core team	Архитектура агентных бесед и изоляции выполнения кода	«Docker vs WebAssembly: где изолировать агентов с доступом к CLI?»	GitHub: phantom-node	EN / ZH
8	Tianjun Zhang	MemGPT / Letta core team	Архитектура виртуальной памяти операционной системы для LLM	«Менеджмент памяти: как агенту помнить контекст сквозь месяцы сессий»	GitHub: tianjunz	EN / ZH
9	Ying Sheng	SGLang core	Оптимизация inference для сложных агентных цепочек и structured output	«Снижение задержки агентного цикла с помощью RadixAttention»	GitHub: sheng-ying	EN / ZH
10	Xingyao Wang	OpenDevin / All-Hands AI	Открытый автономный агент разработки программного обеспечения	«Как OpenDevin справляется с компиляцией и отладкой многофайловых проектов»	GitHub: XingyaoWang / X: @Xingyao_Wang_	EN / ZH
11	Zilliz / Milvus OSS Core	Milvus / Towhee maintainers	Векторные базы данных для долгосрочной памяти мультиагентов	«Retrieval для агентов: фильтрация шума из 100K шагов выполнения»	GitHub: milvus-io	EN / ZH
12	Wade Foster	Zapier Central / Zapier MCP	Создатель платформы headless-автоматизаций и MCP-коннекторов	«Безопасность API-токенов при подключении агентов к 6000+ SaaS-инструментам»	LinkedIn: Wade Foster / X: @wadefoster	EN
13	Brendan Eich	Brave Software (Brave Search API)	Архитектура приватного поиска для AI агентов без трекинга	«Почему агентам нужен детерминированный поиск вместо спама выдачи Google»	GitHub: BrendanEich / X: @BrendanEich	EN
14	Alex Volkov	ThursdAI / AI Tooling practitioner	Практик интеграции Claude Code, Codex и локальных моделей	«Claude Code vs Cursor: замена IDE на автономный терминальный агент»	GitHub: altryne / X: @altryne	EN / RU
15	Demetrios Brinkmann	Agentic AI Foundation / MLOps	Организатор сообщества практиков MLOps и оценки надежности агентов	«Метрики провала агентов в реальном энтерпрайзе: почему 70% POC не доходят до прода»	LinkedIn: Demetrios Brinkmann	EN
16	Nathan Flurry	Rivet	Разработчик stateful-контейнеров для автономных AI агентов	«Управление жизненным циклом и состоянием миллионов серверлесс-агентов»	GitHub: NathanFlurry / X: @NathanFlurry	EN
17	Alexandr Wang / Scale OSS team	SEAL Leaderboards / Evals	Мейнтейнеры бенчмарков безопасности и следования инструкциям	«Как тестировать безопасность тулов агента до деплоя в открытую сеть»	GitHub: scaleapi	EN
18	Antigravity Harness Builders (OSS)	Maintainers of Agent Harnesses	Разработчики обвязок и middleware для автономного запуска Claude/GPT	«Архитектура контекстного окна: динамическое удаление мусора из истории команд»	GitHub Topics: agent-harness	EN
19	Dify.ai Core Team	Dify OSS Engine	Китайская low-code платформа разработки агентов с открытым кодом	«Оркестрация визуальных графов vs кодовые агенты: компромиссы масштабирования»	GitHub: langgenius/dify	EN / ZH
20	ChatDev Core Team (OpenBMB)	ChatDev / AgentVerse	Мультиагентная виртуальная софтверная компания (разработка через чат)	«Предотвращение бесконечного пинг-понга между агентом-кодером и агентом-тестировщиком»	GitHub: OpenBMB/ChatDev	EN / ZH
5. Дизайн ролей и минималистичный инструментальный стек

Никаких платных enterprise-подписок и хрупких сценариев Make/Zapier на старте. Использование исключительно бесплатных и проверенных инструментов: StreamYard Free / OBS Studio + YouTube Studio + GitHub + Google Sheets.

[ Продюсер ] ──(Букинг/Бриф)──> [ Ведущий ] ──(Интервью/Код)──> [ YouTube Studio ]
                                      │                                ▲
[ Тех. Модератор ] ──(Мониторинг .env)─┘                                │
                                                                        │
[ Видеомонтажер ] ──────(Нарезка клипов / Таймкоды)─────────────────────┘

Ролевая матрица (1 ответственный за каждый этап)

Host (Ведущий — уже выделен, личность подлежит верификации):

Ответственность: Ведение эфира, технический диалог на равных, соблюдение тайминга блоков, удержание темпа, формулирование выводов.

Ключевое требование: Умение читать код на экране гостя в реальном времени и возвращать беседу от абстрактной философии к строкам терминала.

Guest Producer / Booker (Продюсер гостей):

Ответственность: Скоринг GitHub-репозиториев, холодный аутрич по шаблону ценности, согласование даты/времени, сбор вводных ссылок и репозиториев, контроль подписания формы согласия.

Technical Moderator (Технический модератор / Safety Guard):

Ответственность: Проведение 15-минутного чека за 2 дня до эфира; контроль качества микрофона/освещения; мониторинг экрана в реальном времени; кнопка аварийного переключения экрана (Panic Switch в OBS/StreamYard) при риске утечки токена.

Editor & Distributor (Монтажер / Дистрибьютор):

Ответственность: Чистка аудио (удаление «эээ», длинных пауз ожидания терминала), простановка точных таймкодов по архитектуре, экспорт 3 вертикальных клипов, публикация демо-репозитория на GitHub.

6. Пилотная программа: первые 3 выпуска и регламент
Темы первых трех эпизодов:

Пилот 1: «Claude Code & Terminal Agents: Полная замена IDE или генератор скрытого техдолга?»

Демо: Рефакторинг реального монорепозитория через CLI-агент, работа с multi-file контекстом и локальными git diff.

Пилот 2: «Sandboxing & Safe Execution: Как запустить автономного агента с bash без риска сноса системы».

Демо: Изоляция агента в микро-контейнерах (gVisor/Docker), перехват опасных системных вызовов (rm, chmod, утечка network egress).

Пилот 3: «Cross-Border Agent Stacks: Как китайские OSS-билдеры строят агентные пайплайны на базе Dify и локальных моделей».

Демо: Сборка сквозного автономного workflow без зависимости от закрытых проприетарных API США.

50-минутный поминутный сценарий (Episode Rundown)
00:00 - 03:00  Интро и формулировка инженерной боли: что чиним сегодня
03:00 - 10:00  Архитектурная схема: стек, модели, latency и стоимость вызова
10:00 - 25:00  БЛОК А: Живой запуск и разбор основного workflow в коде
25:00 - 35:00  БЛОК Б: Стресс-тест на отказ: permissions, циклы, rate limits
35:00 - 45:00  Аудит компромиссов: что НЕ умеет инструмент и сколько он стоит
45:00 - 50:00  Q&A из чата и передача артефактов (ссылки на репозиторий)

Чек-лист 15-минутного технического прогона (Rehearsal Checklist — за 48 часов до эфира):

[ ] Разрешение экрана гостя установлено строго в 1920x1080 (1080p); системный масштаб шрифта в IDE/терминале увеличен до 150–175%.

[ ] Отдельный чистый профиль браузера (без закладок, личных паролей, почты и мессенджеров).

[ ] Окружение: все переменные API заменены на dummy-ключи (sk-proj-TESTING_ONLY_...) или берутся из локального изолированного vault.

[ ] Проверка аудио: гарнитура / внешний микрофон; отключено эхоподавление в ОС, включен чистый стриминговый шлюз.

[ ] Проверка Fallback: локально запущена и проверена работоспособность резервной ветки git.

Трехуровневый протокол защиты от падения живого демо (Live Fallback):

Уровень 1 (Local cached state): Если внешний LLM API выдает 429/500, переключение скрипта на локальный mock-сервер или vLLM/Ollama с кэшированными ответами.

Уровень 2 (Pre-recorded screen video): Если падает среда выполнения (сеть/сборка), гость запускает заранее записанный 3-минутный mp4-ролик успешного прогона того же самого шага, комментируя происходящее голосом.

Уровень 3 (Architecture Deep-Dive): Если падает машина гостя, ведущий перехватывает экран на заранее подготовленную диаграмму mermaid/excalidraw и переводит разговор на анализ краевых случаев и архитектуру.

30-дневный календарный план запуска:
День 1-7   : Верификация языка ведущего. Сетап шаблона StreamYard/OBS.
День 8-14  : Холодный аутрич первых 15 кандидатов. Получение 3 согласий.
День 15-21 : Прогон Пилота 1 (Tech Rehearsal) -> Запись Пилота 1.
День 22-26 : Монтаж, нарезка клипов, сборка companion repo Пилота 1.
День 27-30 : YouTube Premiere Пилота 1 + Запись Пилота 2.

7. Метрики, unit-экономика и пороги решений
Контрольные метрики и пороговые критерии решений:
Метрика	Формула / Способ замера	Гипотеза (Целевой коридор)	Порог остановки / пересмотра (Kill/Pivot Threshold)
Acceptance Rate аутрича	
Отправленные персональные инвайты
Согласованные гости
	​

	15% – 25% (при глубокой персонализации)	< 7% после 30 отправленных инвайтов (сигнал: оффер гостю слабый или нерелевантный).
Время производства выпуска	Суммарные трудозатраты (Host + Producer + Tech)	12 – 16 человеко-часов на выпуск	> 25 часов на выпуск (неустойчиво, ведет к гарантированному выгоранию команды).
Publish Completion	Доля записанных эфиров, дошедших до релиза	100%	Любой отказ гостя от публикации (сигнал: нарушение privacy или низкое качество записи).
Average View Duration (AVD)	YouTube Analytics: среднее удержание	> 35% (для 45-минутного видео)	< 18% (сигнал: слишком много "воды", затянутое начало, скучный экран).
Returning Viewers	Доля постоянных зрителей в когорте 30 дней	> 20% к 3-му пилоту	< 5% (сигнал: контент одноразовый, аудитория ядра не формируется).
Инженерные лиды / PR	Форки репозитория, пулл-реквесты, обращения в ЛС	3–5 целевых контактов на выпуск	0 контактов за 3 пилотных выпуска (контент не имеет практической ценности для профи).
Сценарии затрат (Labor vs. Cash)

Никаких выдуманных ROI на старте канала нет. Инвестиции на первом этапе — это операционные расходы и трудовые часы:

[ Сценарий А: Zero-Cash / In-House ]
Трудозатраты : ~14 часов/выпуск (собственные силы команды)
Прямой кэш   : $0 (бесплатные тарифы YouTube, OBS, GitHub, Google Suite)

[ Сценарий B: Минимальный аутсорс ]
Трудозатраты : ~6 часов команды (букинг, ведение)
Прямой кэш   : $150–$300 на выпуск (монтаж видео, нарезка 3 клипов, транскрибация)

8. Критика формата и финальный Decision Memo
Аргумент ПРОТИВ выбранного формата (Steel-manned Counter-Argument)

Ключевой контраргумент против живых стримов с демо:
Прямой эфир (YouTube Live) технических демонстраций на ранней стадии канала имеет наихудшее соотношение риска к отдаче.

Без первоначальной базы подписчиков живой стрим смотрят от 2 до 7 человек одновременно. Для опытного гостя-разработчика нет ничего более демотивирующего, чем выступать перед пустым экраном с нулем реакций в чате.

Агентный софт нестабилен: недетерминированность LLM, исчерпание лимитов токенов и задержки генерации ломают динамику видео. 10 минут молчаливого ожидания ответа в терминале убивают алгоритмический показатель удержания (AVD) в YouTube Analytics навсегда, отрезая видео от органических рекомендаций.

Условие смены формата (Pivot Trigger): Если после двух тестовых прогонов подготовка окружения гостя занимает более 3 часов, либо во время прогона происходят невосстановимые сбои — немедленно отказаться от прямого эфира в пользу формата «Записанная премьера» (Asynchronous Pre-Recorded Premiere). Сессия пишется в Zoom/Riverside, монтируются все паузы зависания CLI (сокращая хронометраж с 60 до комфортных и плотных 30 минут), а живое общение с аудиторией переносится в премьерный чат YouTube.

Decision Memo
1. Что сделать прямо сейчас (Next 72 Hours):

Верифицировать профиль и ограничения хоста: точные рабочие языки (свободный английский обязателен для работы с авторами Claude Code и китайскими билдерами), уровень владения кодом, доступное время в неделю.

Зафиксировать гибридное позиционирование: «AI Builders & Agent Harnesses: Practical Code & Security Boundaries».

Развернуть единый трекер в Google Sheets / Notion по 20 кандидатам из Раздела 4.

2. Что проверить в первую очередь (Assumptions to Verify):

Согласится ли хотя бы 1 из первых 5 приглашенных мейнтейнеров прийти на запись без гарантии охватов взамен на готовые клипы и демо-репозиторий (проверка гипотезы оффера).

Сможет ли технический модератор настроить задержку стрима (Broadcast Delay) в 30 секунд для предотвращения случайной утечки секретов на экран.

3. Что категорически НЕ строить и не покупать сейчас:

Не покупать платный софт для стриминга (StreamYard/Restream Pro), платные базы лидов и дорогие микрофоны до выхода Пилота 1.

Не тратить время на построение сложных автоматизаций в Zapier/Make для букинга гостей (все 20 контактов обрабатываются вручную для выявления узких мест в коммуникации).

Не заказывать разработку брендинга канала, интро-заставок и 3D-анимаций: девелоперская аудитория оценивает плотность кода на экране, а не визуальные эффекты заставки.

YouTube
The 2025 AI Engineer Challenge
The 2025 AI Engineer Challenge 
AI Makerspace
Opens in a new window
🚀 Ready to become an AI Engineer in 2025? Join us live for The AI Engineer Challenge — your fast track to building, shipping, and sharing end-to-end LLM, RAG, and Agent applications! We’ll walk you through the best-practice stack (Cursor, Claude, Vercel, FastAPI, Docker + more) and teach you how to quickly prototype powerful AI apps that wow your users. Whether you're new to AI Engineering or leading a team, this session will give you the skills and tooling you need to thrive! 

⚠️ Recommended Pre-Work for folks looking to follow along live!
👉 Follow this guide to set up your Interactive Dev Environment for AI Engineers: 
https://github.com/AI-Maker-Space/Interactive-Dev-Environment-for-AI-Engineers
👉 Set up API Keys Token for Vercel:
https://vercel.com/docs/rest-api/reference/sdk

Join us every Wednesday at 1pm EST for our live events. SUBSCRIBE NOW to get notified!

Speakers: 
​Dr. Greg, Co-Founder & CEO AI Makerspace
https://www.linkedin.com/in/gregloughane

The Wiz, Co-Founder & CTO AI Makerspace
https://www.linkedin.com/in/csalexiuk/

Apply for The AI Engineering Bootcamp today! 
https://bit.ly/AIEbootcamp

LLM Foundations - Email-based course
https://bit.ly/4izQVKk

Full LLM Engineering Cohort - Open-Source!
https://bit.ly/42ha7Xy

For team leaders, check out!
https://bit.ly/41YtlA7

Join our community to start building, shipping, and sharing with us today!
https://discord.gg/RzhvYvAwzA

How'd we do? Share your feedback and suggestions for future events.
https://forms.gle/z96cKbg3epXXqwtG6

00:00:00 The New AI Engineer Challenge  
00:05:23 Building Your First LLM Application  
00:10:55 Introduction to Vibe Coding for Front-End Development  
00:16:02 Building Modern Front-End Applications with Next.js  
00:21:14 Essential Tools for AI Development in 2025  
00:26:47 Understanding Developer, User, and Assistant Roles in OpenAI
00:32:18 Enhancing ChatGPT Responses with Developer Prompts
00:37:53 AI and Human Collaboration: Balancing Automation and Human Insight  
00:42:51 Setting Up SSH and API Integration
00:48:12 Optimizing React 2 Indexing with Vercel Docs  
00:53:05 Setting Up an OpenAI Chat API with FastAPI
00:58:33 AI-Assisted Development and Vibe Coding
Opens in a new window
Observing & Evaluating Deep Agents Webinar with LangChain 
LangChain
Opens in a new window
Explore the unique challenges of observing and evaluating Deep Agents in production. Deep Agents represent a shift in how AI systems operate – unlike simple chatbots or basic RAG applications, these agents run for extended periods, execute multiple sub-tasks, and make complex decisions autonomously. In this session, we'll dive into practical approaches for gaining visibility into Deep Agent behavior and measuring their effectiveness using LangSmith. 

Learn more about Deep Agents here: https://blog.langchain.com/deep-agents/

Try LangSmith: https://smith.langchain.com/
Opens in a new window
LlamaIndex Webinar: Build an Open-Source Coding Assistant with OpenDevin 
LlamaIndex
Opens in a new window
OpenDevin is a fully open-source version of Devin from Cognition - an autonomous AI engineer able to autonomously execute complex engineering tasks and collaborate with users on software projects.

​Since it’s open-source, it can both innovate from community ideas and also serve as a reference architecture for any AI engineer looking to build autonomous agents and UXs. 

​We’re excited to host the lead authors of OpenDevin in this special session to 1) learn more about code assistants, 2) how to build them, and 3) engage in a general Q&A on agents! 

​OpenDevin repo: https://github.com/OpenDevin/OpenDevin

​OpenDevin: https://opendevin.github.io/OpenDevin/

Timeline: 
00:00-28:05 - Overview
28:05 Q&A
Opens in a new window
An AI Research Agent That Runs Your Experiments — Tim Sweeney, Weights & Biases 
AI Engineer
Opens in a new window
Live on stage, Weights & Biases' new agent ARIA kicks off a batch of autoresearch experiments on Teague's autoresearch project, running on real GPUs, and nearly beats its own best result before the talk ends. Tim Sweeney, Principal Engineer at Weights & Biases by CoreWeave, shows what ARIA does inside W&B. It launches and monitors training jobs, summarizes the best runs, finds patterns across 200+ experiments, and builds reports and dashboards. It's now on the W&B iOS app too.

Sweeney then shows how the team builds ARIA. It logs 100% of traces to Weave and runs LLM judges on live traffic to catch signals like user frustration. Tasks are written as YAML "unit tests," and a nightly eval suite (73% vs. 72% for the latest candidate) drives go/no-go decisions. His tips: invest in agent-focused observability to catch behavioral bugs, treat evals as your new CI, keep humans reviewing traces, and add value through context and tools before over-engineering the harness.

Speaker info:
LinkedIn: https://www.linkedin.com/in/tssweeney

Related links:
Weights & Biases: https://wandb.ai
W&B Weave: https://wandb.ai/site/weave

Timestamps:
0:00 Intro
1:28 Agenda
2:03 About Weights & Biases
2:33 Demo: meet ARIA
3:13 Running Teague's autoresearch
4:33 Kicking off a live experiment batch
5:17 W&B Launch and the GPU cluster
5:57 Summarizing runs and finding patterns
7:02 Reports and workspaces
8:37 Recap: a data science companion
9:17 ARIA on iOS
9:42 Toward end-to-end automated research
10:22 How we built ARIA: the architecture
13:02 Demo: the agent dashboard in Weave
14:57 ARIA analyzing its own conversations
15:12 Signals: LLM judges on live traffic
16:07 Tasks as unit tests
17:17 Nightly evals
18:07 Recap
18:47 Tips for productionizing agents
20:12 Did the live run beat the record?

---

Watch along with the corrected transcript, summary, timestamps and resources on this talk's official AIE page:
https://ai.engineer/talks/hd7TOvmyAxU-youtube-d31094ccb7ae78e2e6be

Join our upcoming AI Engineer conferences (see https://ai.engineer landing page):

- AIEi Shanghai, November 5–6 — the first for meeting top Chinese labs and engineers
- AIE CODE in SF, November 10–12 — the top AI Coding conference returns
- AIEi Sydney, December 7–8 — the first AIEi run alongside NeurIPS 2026 in Sydney

---
Opens in a new window
ThursdAI - live from AI Engineer Europe - Mythos, Codex w/ VB, Evals w/ Peter & surprise guests 
Alex Volkov from ThursdAI
Opens in a new window
ThursdAI goes international! 🇬🇧 Live from AI Engineer Europe in London, we break down the wildest week in AI with 5 incredible guests.

This week: Claude Mythos Preview (too dangerous for public release), Anthropic's $30B ARR, Meta's Muse Spark, OpenAI Codex hitting 3M users, GLM-5.1 taking the open-source crown, and more.

🎙️ Guests:

• swyx (https://x.com/swyx) — AI Engineer, Latent Space
• Peter Gostev (https://x.com/petergostev) — Arena
• Vaibhav (VB) Srivastav (https://x.com/reach_vb) — OpenAI
• Vincent Koc — OpenClaw maintainer
• Omar Sanseviero (https://x.com/osanseviero) — Google DeepMind / Gemma

⏱️ Chapters:
00:00 Live from AI Engineer Europe!
05:00 Swyx: AI Engineer tracks, OpenClaw, Anthropic $30B ARR
15:00 TL;DR: Mythos, Muse Spark, GLM-5.1, GPT-Image-2 & more
25:00 Peter Gostev: Mythos benchmarks, sandbox escape, Compute Wars
40:00 Arena data goes public — 3 years, 700+ models
50:00 Wolfram: Meta Muse Spark, GLM-5.1, Qwen ecosystem
55:00 This Week's Buzz: HappyHorse, Seedance 2.0, MemPalace, Cursor, W&B
1:00:00 VB (OpenAI): Codex 3M users, quotas, plugins
1:15:00 Vincent Koc: OpenClaw security & nation-state attacks
1:35:00 Omar: Gemma 4 at 10M downloads, on-device AI
1:52:00 Wrap + post-show discussion

🔗 Links:
📰 Newsletter: https://sub.thursdai.news/apr-9 (https://sub.thursdai.news/apr-9)
🎧 Podcast: https://thursdai.news (https://thursdai.news/)
🐦 Show: https://x.com/thursdai_pod
🐦 Alex: https://x.com/altryne
📍 AI Engineer: https://ai.engineer/europe

#ThursdAI #AIEngineer #ClaudeMythos #OpenAI #Codex #Gemma #AI #London

🔗 Subscribe to our show on Spotify: thursdai.news/spotify

🔗 Apple: thursdai.news/apple

🔗 Youtube: thursdai.news/yt

And for the full show notes and links visit

👉 sub.thursdai.news 👈
Opens in a new window




Thinking

Gemini is AI and can make mistakes, including about people. Your privacy and Gemini
Opens in a new window

Searching the web

## Ссылки со страницы (href, собраны рельсой)
https://www.youtube.com/c/MLOpscommunity
https://www.youtube.com/@CognitiveRevolutionPodcast/videos
https://music.youtube.com/search?q=%23latentspace
https://www.youtube.com/watch?v=llpPWAFUUfU
https://www.youtube.com/watch?v=6mJkn3u1bas
https://www.youtube.com/watch?v=_1JZfv7r4mY
https://www.youtube.com/@devtoolsfm/podcasts
https://www.youtube.com/watch?v=hd7TOvmyAxU
https://music.youtube.com/podcast/mXBOfxiZYXo
https://www.youtube.com/@SiliconValley-101
https://github.com/neubig
https://github.com/dhorthy
https://github.com/jerryjliu
https://github.com/hwchase17
https://github.com/robertnishihara
https://github.com/joaomdmoura
https://github.com/thinkall
https://github.com/tianjunz
https://github.com/sheng-ying
https://github.com/XingyaoWang
https://github.com/milvus-io
https://www.linkedin.com/in/wadefoster
https://github.com/BrendanEich
https://github.com/altryne
https://www.linkedin.com/in/dpbrinkm/
https://github.com/NathanFlurry
https://github.com/scaleapi
https://github.com/langgenius/dify
https://github.com/OpenBMB/ChatDev

---

**Claude:**

{"lang":"ru","topic":"Гостевой YouTube live/видео-подкаст с AI builders: формат, гости, план запуска","one_line":"Как запустить гостевую серию YouTube Live/видеоподкаст с практиками AI builders (демо Claude Code, Codex и др.): формат, ведущий, гости, первые три выпуска, метрики и риски.","key_findings":["Позиционирование: широкое «AI Builders & Agent Tooling in Action» лучше узкого auth/security. Узкая ниша даёт малый пул гостей и слабое демо на экране (логи, политики), а широкая даёт видимый CLI/UI и широкий пул мейнтейнеров. Компромисс: в каждый выпуск закладывается блок «Tool Permissions, Sandbox & Failure Boundaries».","Охват даже у сильных каналов скромный: при 40–50K подписчиков медиана технических эпизодов 300–2000 просмотров (AAIF Live 40.9K подписчиков, медиана 300–800; Cognitive Revolution 45.3K, медиана 1.5K–8K). Вирусные выбросы (100K+) привязаны к внешним триггерам и в базовый план закладываться не должны. Это оценки Gemini, а не аудированные данные.","Разобрано 14 сопоставимых серий: AAIF Live (экс-MLOps.community), Cognitive Revolution, Latent Space, AI Makerspace Live, LangChain Webinars, LlamaIndex Community Showcase, devtools.fm, AI Engineer Channel, ThursdAI, Silicon Valley 101, WaytoAGI Live Builders (Bilibili), Practical AI и два закрытых примера. Закрытые: indie-стримы после 4–6 выпусков (15 ч подготовки ради ~60 просмотров) и корпоративный Enterprise GenAI Weekly (питчи без кода не удержали аудиторию).","Конверсия в лиды зависит от качества, а не объёма аудитории: выпуск на ~350 просмотров от senior-инженеров может дать 3–5 целевых контактов (PR или пилотов) лучше, чем ролик на 50K просмотров от широкой публики. Это оценка, не аудит.","Сравнение форматов по трудозатратам на выпуск: 1:1 интервью 8–10 ч, два гостя + ведущий 14–18 ч, live demo clinic 16–22 ч, teardown 12–15 ч, build-in-public 20–28 ч, записанная премьера 12–16 ч, сырой livestream 8–12 ч с высоким риском. Это оценки; главный риск лайва: rate-limit, падение API, утечка ключей на экране.","Рекомендуемый стартовый формат: гибрид «записанная техническая сессия с жёстким таймингом, монтаж пауз CLI, затем YouTube Premiere» с ведущим и гостем в живом чате. Сырой лайв с неизвестным гостем и нулевой аудиторией признан неоправданно рискованным, на живом эфире зрителей может быть 2–7.","Оффер гостю при малом охвате строится на снижении его затрат, а не на обещании охвата: 5 технических вопросов заранее, 3–5 вертикальных клипов 9:16 и один горизонтальный, companion-репозиторий с .env.example и Dockerfile, тестирование 5–10 инженерами, двуязычные конспекты (EN/RU/ZH). Обязательны раскрытие коммерческих связей, письменное согласие гостя и запрет показывать production, личные email и скрытые системные промпты.","Пилотная программа: 50-минутный рандаун (интро 3 мин, архитектура 7, живой workflow 15, стресс-тест отказов 10, аудит компромиссов и стоимости 10, Q&A 5), 15-минутный техпрогон за 48 ч, трёхуровневый запасной план на случай падения демо (кэш/mock или Ollama → заранее записанное видео → диаграмма и архитектурный разбор), защитная задержка трансляции 30 с и кнопка panic switch.","Предложенные пороги решений (гипотезы): принятие приглашений 15–25% (стоп ниже 7% после 30 инвайтов); 12–16 человеко-часов на выпуск (нежизнеспособно выше 25); средняя доля просмотра >35% (тревога <18%); возвращающиеся зрители >20% к третьему пилоту (тревога <5%); 3–5 целевых контактов на выпуск (0 за 3 пилота = нет практической ценности). Затраты: сценарий $0 кэша против аутсорса $150–$300 за выпуск, без выдуманного ROI.","Сильнейший довод против: у лайва без базы подписчиков мало зрителей, а агентный софт недетерминирован, и 10 минут тишины в терминале убивают удержание. Условие смены формата: если подготовка окружения гостя занимает более 3 ч или случаются невосстановимые сбои, переходить на записанную премьеру, сокращая 60 минут до ~30."],"recommendations":["Первые 72 часа: проверить ведущего (рабочие языки, прежде всего свободный английский, умение читать код, время в неделю), зафиксировать гибридное позиционирование и завести трекер из 20 кандидатов в Google Sheets или Notion.","Первые три пилота: (1) Claude Code и терминальные агенты — замена IDE или скрытый техдолг (рефакторинг монорепо через CLI-агент); (2) Sandboxing и безопасное исполнение (изоляция gVisor/Docker, перехват rm/chmod/сетевого egress); (3) китайские OSS-билдеры на Dify и локальных моделях.","30-дневный план: дни 1–7 проверка языка ведущего и шаблон StreamYard/OBS; 8–14 аутрич первым 15 кандидатам и 3 согласия; 15–21 техпрогон и запись пилота 1; 22–26 монтаж, клипы, companion-репо; 27–30 премьера пилота 1 и запись пилота 2.","Роли с одним ответственным на шаг: ведущий (эфир и тайминг), продюсер/букер (скоринг репозиториев, аутрич, согласие), технический модератор (прогон, мониторинг экрана, panic switch), монтажёр/дистрибьютор (чистка, таймкоды, 3 вертикальных клипа, публикация репо). Стек только бесплатный: StreamYard Free или OBS, YouTube Studio, GitHub, Google Sheets.","Чек-лист безопасного экрана: 1080p, шрифт 150–175%, чистый профиль браузера без паролей и мессенджеров, dummy-ключи или локальный vault, резервная git-ветка.","Не строить и не покупать до выхода пилота 1: платный стриминговый софт, базы лидов, дорогие микрофоны, автоматизацию букинга в Zapier/Make (20 контактов вести вручную), брендинг, заставки и 3D-анимацию.","Проверить первым: согласится ли хотя бы 1 из первых 5 приглашённых мейнтейнеров прийти без гарантий охвата ради клипов и демо-репо (проверка оффера), и сможет ли модератор включить задержку трансляции 30 с."],"entities":{"people":["Demetrios Brinkmann","Nathan Labenz","Erik Torenberg","Shawn Swyx Wang","Alessio Fanelli","Greg Loughnane","Chris Alexiuk","Harrison Chase","Lance Martin","Jerry Liu","Logan Markewich","Alex Volkov","Chris Benson","Daniel Whitenack","Graham Neubig","Dexter Horthy","João Moura","Xingyao Wang","Wade Foster","Nathan Flurry","Tim Sweeney","Brendan Eich","Robert Nishihara","Ying Sheng","Tianjun Zhang","Hao Zhang","Vincent Koc","Peter Gostev","Vaibhav Srivastav","Omar Sanseviero","Alexandr Wang"],"companies":["Anthropic","OpenAI","LangChain","LlamaIndex","Zapier","Weights & Biases","CoreWeave","Scale AI","Brave Software","Anyscale","Zilliz","Rivet","All-Hands AI","Google DeepMind","AI Makerspace","Changelog","WaytoAGI","Silicon Valley 101","OpenBMB","Dify (langgenius)","Cognition"],"products_tools":["Claude Code","Codex","Antigravity","YouTube Live","YouTube Premiere","StreamYard","OBS Studio","Riverside","Zoom","GitHub","Google Sheets","Notion","MCP","LangGraph","LlamaIndex Workflows","CrewAI","AutoGen/AG2","MemGPT/Letta","SGLang","OpenDevin","SWE-agent","Milvus","Ray","Dify","ChatDev","Docker","gVisor","Ollama","vLLM","Bilibili","Feishu","Discord","NotebookLM"]},"open_questions":["Личность ведущего, его рабочие языки (в частности английский и китайский) и доступность по-прежнему не проверены.","Реальный охват существующих каналов оператора неизвестен, поэтому все цифры по просмотрам и подписчикам получены из отчёта Gemini и не аудированы по первичным ссылкам.","Данные по 14 сериям и два закрытых примера (индивидуальные стримы, Enterprise GenAI Weekly) приведены без конкретных проверяемых URL и дат, нужна верификация.","Список из 20 кандидатов содержит сомнительные пункты: некоторые GitHub-ники могут быть неверны (jarry-liu, phantom-node, thinkall, sheng-ying), у ряда кандидатов указаны некорректные проекты (например, «FastAgent / Humanlayer» у Dexter Horthy), а пункты 11, 17, 18 и 20 — группы, а не люди. Нужна проверка перед аутричем.","Выбор между широким позиционированием AI builders и узким auth/security не подтверждён измерениями: расшифровка голоса неоднозначна по слову authorization.","Остальные вендоры (chatgpt, grok, claudeai, glm, mistral) в отчёте не представлены: на диске лишь 2 из 6 ног, и кворум 4/6 не достигнут.","Согласятся ли мейнтейнеры и практики из Китая на запись и как будет работать двуязычная дистрибуция, не проверено.","Сроки и затраты на выпуск (12–16 ч, $150–$300 при аутсорсе) являются оценками, а не замерами."],"related_concepts":["Гостевой видеоподкаст и YouTube Live","Developer relations и контент-маркетинг","Живое демо и запасные планы","Безопасность экрана при стриме","Метрики аудитории: медиана против вирусных выбросов","Оффер гостю при малом охвате","Sourcing гостей из GitHub и OSS","Агентный тулинг: Claude Code, Codex, MCP","Sandboxing и права доступа агентов","Китайская AI-экосистема (Dify, WaytoAGI, Bilibili)","Записанная премьера против сырого лайва","Кворум Deep Research и неполные ноги"]}
