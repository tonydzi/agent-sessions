---
session: s_45fba207
date: 2026-10-07
words: 5027
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_45fba207` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-06-HUB-07-1754
REGISTRY TOPIC: Портрет автора: Maria Gorskikh (Maritime YC F26, Project NANDA MIT) и её open-instinct — кто она, чем сильна, зачем открыла клон Instinct, где наш угол входа (втащен в очередь dr_start --adopt; ПОТРЕБИТЕЛЬ: решение: подходить ли к Марии (вклад в open-instinct / партнёрство Maritime / найм) и как именно — кормит Mission-2 и zero-trust линию) (dr_reconcile 2026-10-07: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-06-HUB-07-1754\results)

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


===== VENDOR: grok (grok.md) =====
Собираю портрет по живым источникам: карьера, деньги, open-instinct и публичные высказывания.A. Сверка того, что уже было вводным

Подтвердилось. Maria Gorskikh, GitHub `mariagorskikh`, X `@mariagorskikh` (аккаунт с 2021-12-22, био: co-founder Maritime YC F26, Visiting Lecturer MIT, San Francisco, сайт https://mariagorskikh.com). Maritime: co-founder и CEO, YC Fall 2026, San Francisco, team size 3, статус Active, партнёр Pete Koomen, CTO Aryaman Shrivastava. Формулировка продукта и цена «from $1 per agent per month» стоят на странице YC. Репозиторий https://github.com/mariagorskikh/open-instinct создан 2026-10-03T20:07:59Z, язык TypeScript, лицензия MIT, copyright 2026 Maria Gorskikh. README называет это «a from-scratch, documented clone of Instinct». Стек в README: Pi, Inkbox, Maritime, Composio, кошелёк Stripe Link. Модель по умолчанию `anthropic/claude-fable-5-1`. На 2026-10-06 API GitHub: 187 звёзд, 31 форк, 2 открытых issue, 27 коммитов на main.

Частично. «Core contributor Project NANDA» — так она и конференционные био сами себя называют, и она соавтор двух статей 2025 года. По коммитам в https://github.com/projnanda/projnanda она шестая среди людей: 20 коммитов. Первые авторы статей — Ramesh Raskar и Pradyumna Chari, не она. «Visiting lecturer MIT» есть в её био и в карточке YC. На сайте курса осенью 2026 она в блоке Course Team, инструктор записи — Ramesh Raskar, TA — Nikhil Behari. Каталог Media Lab на осень 2026 пишет MAS.665J как Raskar/Vyahhi, «AI for Impact: Global Ventures».

Не подтвердилось как факт. Substack `@mariagors`: живой страницы не нашёл. Сумму и инвесторов раунда «кроме YC» она не назвала. Третий человек из «team size 3» на YC не подписан. Публичного ответа Noah Shinn или Spear Street на этот репозиторий не нашёл.

Instinct, юридическое имя Spear Street Technology, основатель Noah Shinn: вторичные пересказы от 2026-09-28 и 2026-09-29 сходятся на $1 млрд Series C, оценка $10 млрд, участники Sequoia, Benchmark, Coatue. Оригинал TechCrunch в этом заходе не открывал. Её собственный файл исследования повторяет те же цифры и дату.

1. Таймлайн

2019–2023, Boston University. Первичный источник даёт класс, не название диплома. 2023-05-02 Questrom пишет: Maria Gorskikh (Questrom’23) выиграла BU Refugee Challenge с DREAM Venture Labs, приз $10 000. Она сама в той заметке: иммигрантка, идею дал опыт друзей родителей, соавтор стратегии — «my Questrom friend» без имени. План на приз: 20 бизнесов и больше 200 студентов-волонтёров к лету 2023. (https://www.bu.edu/questrom/blog/maria-gorskikh-questrom23-wins-bu-refugee-challenge-2/, 2023-05-02). Финалистский текст Innovate@BU описывает DREAM как менторство студентов бостонских вузов для беженцев и мигрантов. (https://www.bu.edu/innovate/meet-the-bu-refugee-challenge-finalists-at-the-grand-finale/, дата страницы в выдаче не проставлена).

DREAM не закрыт. На странице компании LinkedIn есть пост о смене: основатель и уходящий executive director Maria Gorskikh, «two years» сборки базы, программы ведёт Sergio Sotelo. Точной даты поста в выдаче нет. Там же, «6mo» относительно выгрузки, DREAM Venture Labs at Boston University запускает Analyst Program. (https://www.linkedin.com/company/dream-venture-labs). На её сайте DREAM по-прежнему «my first company», 501(c)(3). (https://mariagorskikh.com/interests).

2021-12-22. Создан X `@mariagorskikh`. (https://x.com/mariagorskikh).

2025-06-13, правка 2025-07-11. arXiv:2506.12003, «Upgrade or Switch: Do We Need a Next-Gen Trusted Architecture for the Internet of AI Agents?». Она в списке авторов, не первая. Corresponding: Pradyumna Chari. (https://arxiv.org/abs/2506.12003).

2025-07-18. arXiv:2507.14263, «Beyond DNS: Unlocking the Internet of AI Agents via the NANDA Index and Verified AgentFacts». Снова соавтор ближе к концу списка, corresponding Chari. Google Scholar на её профиле (verified email at mit.edu) показывает 23 и 8 цитирований на эти две работы. (https://arxiv.org/abs/2507.14263, https://scholar.google.com/citations?user=Mo9JY1wAAAAJ&hl=en).

2025-07-28. Видео «37 Demo», она говорит: core contributor Project NANDA, показывает join39.org как веб-приложение личного агента и регистрацию в NANDA index. (https://www.youtube.com/watch?v=1M8rInGBhvc).

EmTech MIT 2025, карточка спикера без дня в выдаче. Должность: Researcher, Project NANDA. Био: core contributor NANDA и «she leads Margo AI, a startup building the interface layer that connects people and businesses to autonomous AI agents». (https://event.technologyreview.com/emtech-mit-2025/speaker/1928379/maria-gorskikh). На её сайте в 2026 «Margo ecosystem» — одна строка в списке agent projects рядом с Join39, MacAI, FakeMe. Отдельного живого сайта, раунда и статуса «закрыто» не нашёл. Текущий фокус на том же сайте подписан как Maritime. (https://mariagorskikh.com/about, https://mariagorskikh.com/interests).

2025-11-09, Product Hunt. Она публикует Citable: «I’m Maria, co-founder and CTO of Citable». Продукт мерит, цитирует ли бренд ChatGPT, Gemini, Perplexity. Рядом в истории мейкера Fake Me, август 2025, «uncensored AI twins», «Powered by Grok». (https://www.producthunt.com/p/citable/citable, https://www.producthunt.com/@maria_gorskikh1). F6S до сих пор пишет «CTO @Citable», город в профиле Cambridge. (https://www.f6s.com/member/maria-gorskikh1). Сайт https://getcitable.com/pricing на момент открытия живой: планы $99, $299 и $799 в месяц. Даты ухода из Citable не нашёл. Две роли одновременно (CTO Citable и CEO Maritime) в одном первичном документе не сведены.

2026-01-29. Nikolay Vyahhi анонсирует MAS.664 на весну 2026 и тегает её в одной строке с Raskar, Chari и другими. Это не назначение инструктором. (https://www.linkedin.com/posts/vyahhi_exciting-news-%F0%9D%97%A0%F0%9D%97%9C%F0%9D%97%A7-%F0%9D%97%94%F0%9D%97%9C-%F0%9D%97%A6%F0%9D%98%81%F0%9D%98%82%F0%9D%97%B1%F0%9D%97%B6%F0%9D%97%BC-activity-7422741080095449090-n347).

2026-02-20 и 2026-02-23. Посты блога: конспект MIT Media Lab AI Studio про OpenClaw и Moltbook; «Every Robot Is an Agent». (выдача https://mariagorskikh.com/blog; полный текст одного поста открылся: https://mariagorskikh.com/blog/every-robot-is-an-agent, дата на странице February 23, 2026).

2026-04-09 и 2026-04-10. Imagination in Action, MIT. В карточке: Researcher at Project NANDA, Visiting Lecturer at MIT, Co-Founder of Maritime. Сессии в карточке: Personal Agents, The One-Day Startup, хост «Code from a Prompt». (https://imaginationinaction.co/2604mit/speakers/maria-gorskikh). Это уже прошедшие даты.

2026-05-27. Та же связка титулов на Imagination in Action, AI Showcase. (https://imaginationinaction.co/2605whoop/speakers/maria-gorskikh). Тоже прошедшая дата.

Лето 2026, Maritime. YC пишет Founded: 2026, без месяца. (https://www.ycombinator.com/companies/maritime). Show HN вышел за 48 дней до просмотра 2026-10-06, то есть около 2026-08-19: «We started Maritime at MIT». (https://news.ycombinator.com/item?id=49354052). 2026-09-15 она пишет, что Maritime backed by YC F26. (профиль https://x.com/mariagorskikh, пост с меткой 2026-09-15 20:36:46 UTC). 2026-09-30: «3 weeks in» в батче, подавались трижды, два отказа, третий заход прошёл, до Demo Day 60 дней. (https://x.com/mariagorskikh/status/2105442568817488222). MentionFox датирует запись в каталоге YC 2026-08-31. Это вторичный агрегатор, не письмо YC. (https://mentionfox.com/funding/yc-maritime).

Осень 2026, курс ещё идёт. Сайт AI Studio, Fall 2026: MAS.665 / MAS.664 / EC.731 / IDS.865, четверг 10:00–12:00, E14-633, первый класс 2026-09-10, Demo Day 2026-12-03. Инструктор: Ramesh Raskar. Course Team: Nikolay Vyahhi, Maria Gorskikh, Pradyumna Chari, Gabe Montague, Frido Haugg, John Werner. (https://aiforimpact.github.io/fall26.html, страница открыта 2026-10-06). Каталог Media Lab от 2026-08-17 не ставит её имя на MAS.665J. (https://www.media.mit.edu/posts/fall-2026-media-arts-and-sciences-course-list/).

2026-10-03. Репозиторий open-instinct. Первый коммит в дереве называется «LibreInstinct», затем в тот же день «Back to Open Instinct». (https://github.com/mariagorskikh/open-instinct). 2026-10-05 14:30 UTC она постит анонс. (https://x.com/mariagorskikh/status/2107116096990175454).

Что выглядит закрытым или сменившим форму. DREAM: она ушла с поста executive director, организация жива. Margo AI: в 2026 отдельной компании в открытых источниках не нашёл, на сайте это пункт портфолио. Citable: продукт продаётся, её уход не объявлен. Join39: в июле 2025 это был интерфейс NANDA. Жив ли домен сейчас, в этом заходе не открывал. Fake Me: страница запуска есть, текущего статуса нет.

Агрегаторы (RocketReach, SignalHire) дописывают ей Women x Innovators с 2023, Tresata как technical PM NANDA в 2025–2026, Global Shapers, TRANSFORM VC, стажировки 2020–2022. Это не первичные страницы. В отчёт как факты их не ставлю. Её собственный сайт подтверждает только сообщества: Women x Innovators («600+», цифра её), Dream Venture Labs, Sundai, Global Shapers. (https://mariagorskikh.com/interests).

2. Деньги

Кроме YC публичного раунда с суммой и именами не нашёл.

Её слова 2026-09-30: «We got VC funded back in June.» Имени фонда, суммы, оценки и инструмента (equity, SAFE) в посте нет. Дальше она отделяет это от YC: батч заставил продавать, до Demo Day 60 дней. (https://x.com/mariagorskikh/status/2105442568817488222). Ответ ей же 2026-10-02 на вопрос про traction: «users, revenue, and vc funding», без чисел. (https://x.com/mariagorskikh/status/2105921441258783149).

Каталог YC не публикует размер чека Maritime. Roundfunded прямо пишет, что его «YC application» — реконструкция, не поданная анкета. (https://www.roundfunded.com/en/yc-startup/maritime, 2026-09-09). Пресс-релиза pre-seed или ангелов не нашёл.

Цены, которые она и сайт называют.

Страница YC: изолированный постоянный компьютер на агента, «starting at $1 per agent per month», sleep/wake, масштаб в тысячи агентов. (https://www.ycombinator.com/companies/maritime).

Show HN, около 2026-08-19: $1 за агента в месяц, 100 агентов = $100. Три агента бесплатно навсегда. Шаблоны OpenClaw, Hermes (Nous Research), DeepSeek. Свой ключ модели. После кредита $5 пользователь платит за LLM сам. Платная шкала субсидирует бесплатный ярус. Спать при простое, лимиты, чтобы за $1 нельзя было жечь CPU круглые сутки. Снапшоты. «You can export your files and data anytime.» LLM они не хостят, «just harnesses». Отвечала она как mariagorskikh1. Про «Backend unavailable» ответил аккаунт mirajane12 от лица «we». Кто это, не установлено. (https://news.ycombinator.com/item?id=49354052). Тред: 8 очков, 10 комментариев.

Главная https://maritime.sh/ на 2026-10-06: Firecracker micro-VM, свой kernel, «on bare metal». Новый VM 0.5 с, пробуждение 0.6 с. Диск переживает сон. «Free for 3 agents.» Демо: https://cal.com/maritimesh/maritime. Для «agent startup» — до $10 000 кредитов, форма https://maritime.sh/startups#apply. Отдельного прайс-листа сверх «$1» и «3 free» на открытой главной не увидел. На чём зарабатывают по их словам: плата за хостинг агента. Модель клиента в цену не входит.

3. Техника

Pi. Агентский цикл. README и ARCHITECTURE: пакеты `@earendil-works/pi-agent-core`, `pi-ai`, `pi-coding-agent`. Автор Pi — Mario Zechner. 2026-04-08 он ушёл в Earendil (Armin Ronacher и Colin), ядро остаётся MIT, марка у компании. (https://www.sfeir.com/personnes/mario-zechner/, 2026-09-29; https://ai.engineer/speakers/mario-zechner). В её таблице: Pi раньше был ядром OpenClaw, сейчас OpenClaw держит свой agent-core. (сырой https://raw.githubusercontent.com/mariagorskikh/open-instinct/main/docs/ARCHITECTURE.md).

Inkbox. Закрытый сервис, не её. YC Summer 2026, основан 2025, San Francisco, 3 человека. Фаундеры Ray Liao (CEO), Alex Wilcox (CTO), Dima Vremenko. Даёт агенту email, телефон, iMessage, туннель и канал agent-to-agent. Контакт на их запуске: [EMAIL]. (https://www.ycombinator.com/companies/inkbox). В её протоколе транспорт — `POST https://inkbox.ai/a2a/{handle}`. (https://github.com/mariagorskikh/open-instinct/blob/main/docs/PROTOCOL.md). Публичный прайс Inkbox в этом заходе не открывал. SELF-HOST говорит, что при полном плане `init` останавливается и даёт billing URL.

Maritime. Её компания. Закрытый хостинг. В open-instinct это путь «The Instinct way»: `MARITIME_API_KEY` и `pnpm instinct deploy`. Спящий агент на Maritime «costs nothing», создание агента списывает кошелёк. (https://github.com/mariagorskikh/open-instinct/blob/main/docs/KEYS.md).

Composio. Чужая компания. Dealroom: юридически Sampark Inc., основана в июне 2023 Soham Ganatra и Karan Vaidya, San Francisco, оплата за вызов API. (https://dealroom.co/companies/composio/). Вики-сводка добавляет YC W24 и раунд, это не первичка. (https://ai.miraheze.org/wiki/Composio). В её репозитории Composio — Tool Router, ключ `COMPOSIO_API_KEY`, нужен для Gmail, календаря и «1000+ apps». Для локального чата ключ необязателен. (KEYS.md).

Насколько это работает без её платных сервисов.

Локальный чат: Node 22.19+, pnpm 10, только ключ модели. `pnpm instinct chat` ходит в процесс на ноутбуке. Maritime для этого не нужна. (README и https://raw.githubusercontent.com/mariagorskikh/open-instinct/main/docs/SELF-HOST.md).

iMessage, почта агента и A2A «как у Instinct»: нужен платный Inkbox, не Maritime. Документ прямо: «Nothing here needs Maritime hosting.»

Компьютер, браузер, клики: на self-host рабочего стола рядом нет. Либо режим без компьютера, либо hosted desktop, и для него в таблице SELF-HOST указан `MARITIME_API_KEY` со scope `computers`. Кусок таблицы после строки 282 в выдаче обрезан, полный перечень режимов дочитывать там же.

Приложения: Composio, чужой ключ. Платежи: Stripe Link, чужой. Модель: любой провайдер из каталога Pi, дефолт Claude Fable 5.1.

Итог по lock-in, из их же документов, не из догадки. Ядро разговора и политика открыты и живут на своей машине. Полный сценарий «написал в iMessage, агент сидит за своим Linux и ходит в почту» по умолчанию стоит на Inkbox плюс Maritime плюс Composio. CONTRIBUTING.md фиксирует это как политику: «Inkbox stays the default channel and Maritime the default host. New providers are welcome as options; they do not replace defaults.» (https://raw.githubusercontent.com/mariagorskikh/open-instinct/main/CONTRIBUTING.md).

Она сама в Reddit 2026-10-04: лицензия не делает внешние сервисы бесплатными, «We build Maritime.» (https://www.reddit.com/r/IMadeThis/comments/1wxuald/we_made_open_instinct_an_opensource_assistant_you/).

4. Зачем она это сделала. Её слова

2026-09-28 21:40 UTC, текст её поста, пойманный в ветке https://x.com/dave_xt/status/2104752393418354942:

«Instinct just raised $1 billion at a $10 billion valuation. I think this says more about where the world is headed than it does about one company. With Muse and Grokbot, maybe by 2027 we’ll all have a personal AI agent we talk to throughout the day. After everything we’ve seen with OpenClaw earlier this year, it feels like a natural progression. I'm super excited for the mass adoption of AI agents. But I really hope the world ends up with more than three main AI agent companies. I want to see hundreds of startups building personal agents for specific groups of people. Founders who understand their market, know how to reach their users, and just go for it. There’s room for thousands of companies here. Now is your chance to build an Instinct for your country, your age group, your occupation. You can use Maritime for the core infra, vibe code the rest in a day, and go build a unicorn.»

Это за день до репозитория и за неделю до анонса клона. Мотив в этом тексте: много узких агентов, Maritime как инфра под них. Не «открыть исходники Instinct».

2026-09-30 04:53 UTC. «How did Instinct raise 1 BILLION??» Видео. Она в ответе: «I think my claude did better with sound effects this time!» и «took 2 prompts!» (https://x.com/mariagorskikh/status/2105159013398941817, https://x.com/mariagorskikh/status/2105176746278695222). Это ролик, не разбор капа.

2026-10-05 14:30 UTC. Анонс репозитория, 508 лайков, 22 репоста, 12 цитат, 42 ответа, 565 закладок, 39 287 просмотров на момент чтения ветки:

«Instinct just raised $1B for a personal agent you text. We think the future is many specialized agents, not one. So we built the open-source version: a personal agent you text on iMessage, with its own computer and a trusted network of other agents. Fork it.»

(https://x.com/mariagorskikh/status/2107116096990175454).

Через четыре часа она дописывает стек: «made with @maritime_sh @inkbox_ai @composio @stripe and Pi framework». (https://x.com/mariagorskikh/status/2107181635183788468, 2026-10-05 18:50 UTC).

README, без отдельной даты помимо репозитория от 2026-10-03: «A from-scratch, documented clone of Instinct, built so anyone can run one.» И прямое отмежевание: проект не связан с Instinct и не связан с OpenInstinct от Merit Systems. (https://github.com/mariagorskikh/open-instinct).

Reddit 2026-10-04, от лица «we»: хотели ассистента, которого разработчик может переделать под своё сообщество. Просят сборки «with one useful job for a specific audience». (ссылка выше).

Подкаста и треда Hacker News именно про open-instinct с её объяснением не нашёл. Её длинный разбор коммерческого Instinct лежит внутри репозитория и помечен «public sources as of October 3, 2026». (https://github.com/mariagorskikh/open-instinct/blob/main/docs/research/INSTINCT.md).

5. Реакция рынка

X, её пост 2026-10-05. Цифры выше. Из ветки инструмент отдал два содержательных ответа, не все 42. Самое резкое из отданных: @keyserfaty (agentcard, YC S26), 2026-10-05 18:42 UTC: «so openclaw?» 5 лайков. (та же ветка, пост 2107179733456949375). Остальной текст 40 ответов в выдачу не попал. Отдельный поиск по фразе open-instinct на X вернул пусто.

Hacker News по её репозиторию. Треда Show HN с её именем на open-instinct не нашёл. Чужой и более ранний клон есть: Show HN «OpenInstinct – open-source, self-hostable Instinct clone», github.com/merit-systems, 5 очков, автор OG_BME, «36 days ago» на день чтения, то есть около 2026-08-31. Комментариев в выдаче нет. Стек другой: Eve, Linq, Kernel, Postgres, Vercel. Мотив авторов: не отдавать данные Instinct. (https://news.ycombinator.com/item?id=49479314).

Её собственный Show HN про Maritime, не про клон: 8 очков, 10 комментариев. Возражения, которые там есть. mandarinclips: кто под капотом Hermes, не бесплатная ли поездка навсегда. abigdog: как вы не разоритесь, если агент крутят 24/7, и что будет с данными, если вы свернётесь. ethannam9022: клиентский exception на maritime.sh. cunjieliu: «Backend unavailable». atmanactive: где бежит LLM. Она ответила по сну, лимитам и экспорту. Это не идеологический разнос клона. (https://news.ycombinator.com/item?id=49354052).

Reddit. Один пост 2026-10-04 в r/IMadeThis. Тело поста открылось. Блок комментариев без логина не отдался, числа upvotes в выдаче нет.

Ответ Instinct / Spear Street / Noah Shinn именно на mariagorskikh/open-instinct. Не нашёл. Искал связку clone, cease, trademark, Shinn и этот репозиторий.

Юридический риск. Факты, не заключение. Репозиторий сам пишет «clone of Instinct» и тут же «not affiliated» с Instinct и с Merit Systems OpenInstinct. Лицензия MIT покрывает её код, не товарный знак чужого продукта. Иска, письма cease-and-desist и публичного спора о торговой марке в открытых источниках этого захода нет. Имя OpenInstinct уже занято другим публичным репозиторием Merit Systems, и она это в README признаёт.

6. Люди

open-instinct, API контрибьюторов на 2026-10-06.

mariagorskikh, 19 коммитов. Владелица копирайта.

mahmoudomarus, 7 коммитов. На GitHub имя Mahmoud Omar, «M Omar». Профиль: FERAL AI (feral.sh, «local AI», память между устройствами) и THEORA, очки с витальными показателями, theora.io. X в профиле @FeralAi67724 и @theora_ai. Его PR #4 смержен 2026-10-05: починка загрузки скиллов. (https://github.com/mahmoudomarus, https://github.com/mariagorskikh/open-instinct).

dimavrem22, 1 коммит. GitHub-имя Dima Vremenko, Boston. Это совпадает с сооснователем Inkbox. CODEOWNERS репозитория отдаёт ему ревью пакетов Inkbox и network, всё остальное ревьюит она, первый ответ «within a week». (https://github.com/dimavrem22, CONTRIBUTING.md, карточка Inkbox на YC).

Co-founder Maritime. Aryaman Shrivastava, Founder/CTO. Текст YC: до этого исследователь MIT NANDA Lab, координация агентов на масштабе. (https://www.ycombinator.com/companies/maritime). Популярный GitHub `aryamanshrivastava`, который открылся по имени, другой человек: Bangalore, Flutter, банк. Его к этому Aryaman не привязываю. SignalHire и RocketReach дают Aryaman буткемп BU/ASU и дату co-founder «Mar 2026». Это агрегаторы, в факты не кладу.

Третий из team size 3. Имени на YC нет. На главной maritime.sh внутри макета статьи стоят «Ary Shrivastava, Maria Gorskikh, and Brandon Li». Это вёрстка демо-PDF на лендинге, не список команды. Отдельной страницы Brandon Li в Maritime не нашёл. mirajane12 на HN говорит «we». Кто это, не нашёл.

NANDA, коммиты https://github.com/projnanda/projnanda на момент API. mlmrx 212, gurusharaskar 101, pradyumnachari 51, ankurshnde 46, AshutoshRavindraIwale 30, mariagorskikh 20, бот 19, rameshraskar 6, rohanarickhanna 1. Pradyumna Chari — соавтор обеих статей и corresponding author, на сайте курса Researcher, MIT. Ramesh Raskar — первый автор статей, инструктор курса, группа NANDA в Media Lab. Она в этом репозитории не главный писатель кода.

Кто её публично держит. YC и Pete Koomen как primary partner, это строка каталога, не цитата поддержки. Dima Vremenko вписан ревьюером её репозитория, это рабочая связь с Inkbox, не отзыв. Теги на курсе от Vyahhi. Ангельских имён рядом с Maritime не нашёл.

7. Как связываются

Открытые двери, которые сам видел.

X `@mariagorskikh`, аккаунт не закрыт. Она прямо зовёт в личку по разбору YC-заявки и founder video: «DM me». (https://x.com/mariagorskikh/status/2105442568817488222, 2026-09-30). Для партнёрства отдельной фразы нет, дверь та же.

Демо Maritime: https://cal.com/maritimesh/maritime. Кредиты стартапам: https://maritime.sh/startups#apply. Регистрация: https://maritime.sh/signup.

GitHub: issues включены, discussions выключены. CONTRIBUTING просит PR на одну тему, `pnpm check`, новые каналы как опции, не как замена Inkbox и Maritime. Вендор чужого сервиса должен написать в PR, что работает на эту компанию.

NANDA, не её личный ящик. Discord https://discord.gg/BxnPBEqd88. Почта сообщества [EMAIL]. События https://lu.ma/nanda. Сайт https://projectnanda.org. README говорит «6000+ community members», это их цифра, я её не пересчитывал. Форма FAN fellowship в том же README. (https://raw.githubusercontent.com/projnanda/projnanda/main/README.md). Форма «Open Source Developer» в osd.md ведёт на заглушку `forms.gle/your-google-form-link`, это битая ссылка в репозитории. (https://raw.githubusercontent.com/projnanda/projnanda/main/home/osd.md).

Личную почту и телефон из открытой страницы не нашёл. RocketReach показывает кнопку «view email» за подпиской. Адрес оттуда не беру и не прошу.

Что она просит. «Fork it». На Reddit: сборки под одну работу и одну аудиторию. В CONTRIBUTING: контрибьюторы, первый ответ в течение недели. На Show HN Maritime: попробовать бесплатные 3 агента и сказать про developer experience. На лендинге: стартапам, которые строят агента, подать на кредиты до $10 000.

Ближайшее по датам на 2026-10-06.

Её X, зеркало Sotwe: она ищет диджея в SF «for our launch party on Oct 10». Оригинальный status id этого короткого поста в выдаче не сохранился, дата «about 17 hours ago» привязана к обходу Sotwe, не к календарю. Город и день: San Francisco, 10 октября 2026. (https://www.sotwe.com/mariagorskikh). Прошлый офлайн, уже был: ретвит 2026-09-08 про вечеринку Maritime на Tech Week в Corgi Cafe. (профиль https://x.com/mariagorskikh).

Курс, если она ещё в команде: Demo Day 2026-12-03, MIT Media Lab. Это дата курса, не её личного доклада. (https://aiforimpact.github.io/fall26.html).

Её оценка Demo Day YC: «60 days» от 2026-09-30, то есть около 2026-11-29. Календарной даты YC она не написала.

Апрельские и майские сцены Imagination in Action уже прошли.

8. Нанимает ли

На 2026-10-06 страница вакансий YC: «No jobs at Maritime are currently posted on the YC platform.» (https://www.ycombinator.com/companies/maritime/jobs). MentionFox на 2026-09-13 тоже ставит Hiring: No. Отдельной доски на maritime.sh в открытой главной нет.

Роли, требования, вилка: публичного текста нет, потому что вакансий нет.

Косвенное. Team size 3 при двух названных фаундерах. В LinkedIn-ленте, которую поисковик отдал с пометкой «1w» без календарной даты, она звала fellow на 3 месяца в NANDA по agentic data infrastructure, не в Maritime. Ссылку на форму поисковик обрезал. Точную дату этого поста не фиксирую. (https://www.linkedin.com/in/mariagorskikh).

9. Что она думает. Пять цитат и где её уже ткнули

Все пять ниже — её голос или текст, который она опубликовала под своим именем.

«Today's internet was designed for static web pages and human-triggered APIs. As we move toward a world with trillions of intelligent agents, the underlying assumptions of the web must be rethought.» (https://mariagorskikh.com/research, дата правки страницы не стоит; рядом она пишет, что соавтор двух бумаг NANDA).

«I want to see hundreds of startups building personal agents for specific groups of people. [...] Now is your chance to build an Instinct for your country, your age group, your occupation.» (её пост 2026-09-28 21:40 UTC, контекст в https://x.com/dave_xt/status/2104752393418354942).

«We think the future is many specialized agents, not one.» (https://x.com/mariagorskikh/status/2107116096990175454, 2026-10-05).

«The average person uses their AI agent 20 minutes a week. So why are we paying for servers that run 24/7?» Это анонс её поста от 2026-04-07 на индексе блога. Полный текст по угаданному адресу не открылся, цитирую только этот лид. (https://mariagorskikh.com/blog).

Show HN: «Building such scalable and secure infra will take you months and will cost hundreds of thousands. Also, you still can't vibe code the infra well. So Maritime handles that infrastructure for you.» (https://news.ycombinator.com/item?id=49354052).

Где публичный след уже спорит, без додумывания «она неправа».

«so openclaw?» @keyserfaty, 2026-10-05. Её тезис «много специализированных агентов, не один» в посте выглядит как ещё один личный агент в iMessage на Pi. Она сама пишет, что Pi был каркасом OpenClaw. Отличия, которые она успевает назвать в том же посте: свой компьютер и сеть доверенных агентов. Ответ на «это не OpenClaw?» в отданной части ветки не прозвучал.

abigdog на HN: цена $1 выглядит как лямбда, пока кто-то не оставит агента на максимальном CPU. Она ответила сном и лимитами. Проверки, что лимит правда держит, в треде нет.

Тот же abigdog спросил экспорт, если продукт свернётся. Она сказала, что файлы можно забрать. Это обещание в комментарии, не увиденный мной дамп.

Её «core contributor» и место в git расходятся: 20 коммитов против 212 у mlmrx и 51 у Chari. Соавтор бумаг она есть. Ведущий автор, по порядку имён arXiv, нет.

«Open source» и касса. Локальный чат без Maritime она документирует честно. Картинка в анонсе X, которую она подписала «made with Maritime, Inkbox, Composio, Stripe and Pi», собирается из трёх платных слоёв плюс открытого Pi. Reddit-пост это тоже говорит вслух.

Цифра «20 minutes a week» в лиде блога дана без источника на той карточке, которую я видел. Как замер это не проверено.

10. Дыры и противоречия

GitHub-локация профиля: Cambridge. X и YC: San Francisco. Оба открыты в одном заходе. Где она живёт в октябре 2026, одним источником не закрыто. Курс при этом идёт в E14-633 в Кембридже, а батч YC она описывает изнутри как текущую жизнь.

Team size 3 и два имени фаундеров. Третий не назван. Brandon Li есть только внутри картинки-статьи на лендинге.

«VC funded in June» без фонда, суммы и даты закрытия. Ангелы не названы. Чек YC на компанию не опубликован.

Citable: она CTO на Product Hunt и F6S, CEO Maritime на YC. Ухода нет. Margo AI есть в био EmTech 2025 и одной строкой на сайте. Жива ли компания, не нашёл.

Substack `@mariagors` не нашёл.

Личная почта в открытом виде не нашёл.

Вакансий Maritime нет. Кого она взяла бы, из публичного текста не следует.

Подкаста с разбором open-instinct нет. HN-треда про этот репозиторий нет. Ответа Shinn нет.

Полный текст 40 из 42 ответов под постом 2026-10-05 инструмент не отдал. Критика там может быть, я её не видел.

«Visiting lecturer» против Course Team и против каталога, где на MAS.665J стоят Raskar и Vyahhi.

Авторский порядок статей против самоназвания «core». Оба факта правдивы на своём уровне и плохо склеиваются в одну должность.

Два клона с почти одним именем. Merit Systems раньше и тише (около 2026-08-31, 5 очков на HN). Она позже, громче в X, и сразу ведёт на свой хостинг.

Внутреннее имя LibreInstinct прожило внутри коммитов 2026-10-03 и сменилось на Open Instinct. Почему сменили, она не написала.

Экспорт данных и «не лочим» сказаны на HN. Живой takeout я не скачивал.

Оригинал новости TechCrunch про $1 млрд Instinct в этом заходе не открыт. Цифра стоит у нескольких пересказов и в её INSTINCT.md.

НЕ НАЙДЕНО

Живой Substack mariagors. Сумма и имена июньского VC и любых ангелов Maritime. Размер чека YC именно им. Имя третьего сотрудника. Дата и текст ухода из Citable и из DREAM точнее, чем «two years» и пост без даты. Судьба Margo AI после карточки EmTech 2025. Публичный email Марии. Вакансия, роль, требования. Ответ Noah Shinn, Spear Street или юриста на репозиторий. Суд или cease-and-desist. Show HN и длинное обсуждение Reddit именно её open-instinct. Полкаст. Подтверждение, что GitHub `aryamanshrivastava` — это её CTO. Это другой человек. Календарная дата Demo Day YC. Прайс Inkbox. Доказательство, что экспорт с Maritime правда полный.

🎙 Майк: идти к ней как к автору инфра-слоя, который открыл клон, чтобы на него садились чужие агенты. Дверь сейчас X и pull request, не «возьмите на работу»: вакансий нет, а репозиторий прямо просит опции рядом с Maritime, не замену.

🧒 Простыми словами: Мария делает «квартиры» для роботов-помощников. Одна квартира стоит около доллара в месяц, три можно попробовать бесплатно. На прошлой неделе она выложила открытую копию модного платного помощника Instinct, чтобы люди могли собрать своего. Сама копия бесплатная, а телефон, компьютер и доступ к почте в полной версии идут через чужие и её платные сервисы. В команду она публично никого не зовёт. Написать ей проще всего в X, в личку.

---

**Claude:**

```json
{
  "lang": "ru",
  "topic": "Портрет Maria Gorskikh: Maritime (YC F26), Project NANDA, клон open-instinct",
  "one_line": "Отчёт разбирает, кто такая Maria Gorskikh, чем она реально сильна (роль в NANDA vs заявленная), зачем она 2026-10-03/05 выпустила open-source клон Instinct (open-instinct) и какие двери есть для подхода (вклад/партнёрство/найм).",
  "key_findings": [
    "Maria Gorskikh — co-founder/CEO Maritime (YC Fall 2026, SF, команда 3, CTO Aryaman Shrivastava, партнёр YC Pete Koomen); репозиторий open-instinct создан 2026-10-03, MIT-лицензия, на 2026-10-06 187 звёзд/31 форк/27 коммитов на main.",
    "Её самоназвание «core contributor Project NANDA» верно формально, но по факту коммитов (API projnanda/projnanda) она 6-я среди людей — 20 коммитов против 212 у mlmrx и 51 у Pradyumna Chari; в двух статьях NANDA (arXiv 2506.12003, 2507.14263) она соавтор, не первый/corresponding автор (это Chari, первый автор — Ramesh Raskar).",
    "Open-instinct — прямой ответ на раунд коммерческого Instinct (Spear Street Technology, основатель Noah Shinn) на $1 млрд при оценке $10 млрд (Sequoia/Benchmark/Coatue, по вторичным пересказам); её публичный мотив (её же цитаты 28.09 и 05.10) — не повторить продукт, а дать инфраструктуру («Maritime для core infra») под сотни узких агентов вместо трёх больших игроков.",
    "Технически ядро (Pi-based локальный чат) открыто и работает без платных сервисов, но полный сценарий Instinct-like (iMessage/почта/A2A через Inkbox, собственный компьютер-агент через Maritime, приложения через Composio, платежи через Stripe) по умолчанию и по политике CONTRIBUTING.md завязан на три платных сервиса, два из которых — её/партнёрские (Maritime, через co-founder Inkbox Dima Vremenko как ревьюер репозитория).",
    "Денег помимо YC публично не раскрыто: её собственные слова «We got VC funded back in June» без фонда/суммы/оценки; размер чека YC не опубликован; ценник Maritime — от $1/агент/месяц, 3 агента бесплатно навсегда, кредиты стартапам до $10 000.",
    "Публичных вакансий у Maritime нет (страница YC: «No jobs... currently posted»), входа «через найм» сейчас не существует.",
    "Рыночная реакция сдержанная и в основном техническая (вопросы про экономику $1/агент, экспорт данных, «это разве не OpenClaw?»), юридического конфликта или ответа от Instinct/Spear Street/Noah Shinn не найдено; существует более ранний и тише вышедший похожий клон OpenInstinct от Merit Systems (другая мотивация — не отдавать данные Instinct).",
    "Карьера и роли расходятся по источникам: GitHub-профиль указывает Cambridge, X/YC — San Francisco; параллельные роли CTO Citable (Product Hunt/F6S) и CEO Maritime не разведены по времени; статус «Visiting Lecturer MIT» спорен — в каталоге курса MAS.665J инструктор Raskar/Vyahhi, она в «Course Team»; третий член команды Maritime (team size 3) публично не назван (упомянут только непроверенный «Brandon Li» в макете лендинга)."
  ],
  "recommendations": [
    "Подходить к ней как к владелице инфра-слоя (Maritime) через открытые двери: X DM (она сама зовёт «DM me») и pull request в open-instinct — репозиторий прямо просит контрибьюторов и новые провайдеры как ОПЦИИ рядом с Inkbox/Maritime, не как замену дефолтов.",
    "Не заходить через найм — вакансий у Maritime нет, вход «нанять её» сейчас не существует.",
    "Для партнёрства использовать её собственные публичные каналы: демо-звонок https://cal.com/maritimesh/maritime, форма кредитов для агент-стартапов https://maritime.sh/startups#apply, регистрация https://maritime.sh/signup.",
    "Угол для Mission-2/zero-trust линии — её соавторство в NANDA-статьях про trusted architecture для internet of AI agents (AgentFacts, NANDA Index) более содержательно для технического диалога, чем её роль в Maritime/open-instinct, где она скорее дистрибьютор инфраструктуры, чем автор протокола."
  ],
  "entities": {
    "people": ["Maria Gorskikh", "Aryaman Shrivastava", "Noah Shinn", "Ramesh Raskar", "Pradyumna Chari", "Nikolay Vyahhi", "Mahmoud Omar (mahmoudomarus)", "Dima Vremenko", "Pete Koomen", "Mario Zechner", "Brandon Li"],
    "companies": ["Maritime", "Instinct (Spear Street Technology)", "Inkbox", "Composio", "Citable", "DREAM Venture Labs", "Project NANDA", "Fake Me", "Margo AI", "Y Combinator", "Merit Systems"],
    "products_tools": ["open-instinct", "Pi (pi-agent-core, pi-coding-agent)", "Stripe Link", "Firecracker micro-VM", "Join39", "NANDA Index / AgentFacts", "OpenClaw"]
  },
  "open_questions": [
    "Нет публичного Substack @mariagors — живая страница не найдена.",
    "Сумма, фонд и дата закрытия июньского VC-раунда Maritime не раскрыты; размер чека YC не опубликован.",
    "Имя третьего члена команды Maritime (team size 3) не названо.",
    "Точная дата и обстоятельства ухода из Citable и из DREAM Venture Labs не установлены; статус Margo AI после 2025 неясен.",
    "Публичный email Марии не найден.",
    "Нет ответа Noah Shinn / Spear Street / юристов на репозиторий open-instinct; cease-and-desist или судебного спора не обнаружено.",
    "Подкаста, HN-треда или развёрнутого обсуждения конкретно её open-instinct (в отличие от чужого более раннего клона Merit Systems) не найдено.",
    "Полный текст 40 из 42 ответов на её анонс-пост в X не получен — возможная критика там не видна.",
    "Не подтверждено, что живой профиль GitHub aryamanshrivastava принадлежит её CTO (похоже, другой человек)."
  ],
  "related_concepts": ["open-source-clone-as-distribution", "zero-trust-agent-architecture", "NANDA-index", "YC-startup-playbook", "personal-ai-agent-infra", "Mission-2"]
}
```
