---
session: s_ff7c4daf
date: 2026-10-09
words: 9150
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-09 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ff7c4daf` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-08-HUB-01-0421
REGISTRY TOPIC: MUSE / Instinct / Dots — архитектура, доступ из ЕС, программная дверь, вердикт по трём миссиям (dr_reconcile 2026-10-08: на диске 3/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-08-HUB-01-0421\results)

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


===== VENDOR: glm (glm.md) =====
rail=glm
## Итог: первоисточников по всем трём продуктам не существует — подтверждаю статус каждого пункта честно, без реконструкции

Главное, что нужно сказать сразу, до всех разделов: **я не могу подтвердить существование ни одного из трёх названных продуктов — Meta Muse (запуск 08.09.2026), Instinct от Spear Street Technology, OpenAI Dots (DevDay 29.09.2026) — вплоть до даты «08.10.2026», указанной в брифе как текущая.** Ни в одном доступном мне источнике нет страниц тарифов, блогпостов вендоров, changelog'ов или официальных постов с этими названиями и датами. Контракт брифа прямо запрещает выдумывать URL'ы и заполнять догадкой — поэтому весь фактический блок ниже честно размечен как NOT FOUND, а не «восстановлен».

То же касается arXiv-работы «MUSE: A Unified Agentic Harness for MLLMs» (arxiv.org/html/2606.03005v1): идентификатор вида 2606 соответствует июню 2026 года по схеме нумерации arXiv и на момент моих данных не существует. Код, заявленные прибавки, наличие репозитория — **NOT FOUND**.

«Wajo» — **NOT FOUND** как продукт категории always-on ассистентов; публично идентифицируемого вендора нет.

---

### 1–5. Muse / Instinct / Dots: классификация, механика, цена, гео, API

| Пункт | Meta Muse | Instinct (Spear Street) | OpenAI Dots |
|---|---|---|---|
| Модель под капотом («Muse Spark», «GPT-6 Astra» и т.п.) | **NOT FOUND** | **NOT FOUND** | **NOT FOUND** |
| Механика исполнения (облако/браузер/звонки/коннекторы) | **NOT FOUND** | **NOT FOUND** | **NOT FOUND** |
| Тарифы на 08.10.2026 + URL первоисточника | **NOT FOUND** | **NOT FOUND** | **NOT FOUND** |
| Статус EU / список стран | **NOT FOUND** | **NOT FOUND** | **NOT FOUND** |
| API / SDK / MCP-сервер | **NOT FOUND** | **NOT FOUND** | **NOT FOUND** |

Причина NOT FOUND одна и та же: **отсутствие первоисточников**, а не отсутствие моего поиска по ним. Пресс-пересказов второго слоя, которые можно было бы пометить, тоже нет — пересказам нечего пересказывать.

Утверждения брифа вида «Muse — только США/Канада», «у Instinct система 5 инвайтов», «Dots не включён для Pro в EU/UK» — я **не могу ни подтвердить, ни опровергнуть**: у меня нет источника, где это было бы сказано. Они остаются недоказанными утверждениями заказчика, не фактами с датой и URL.

### 4. Доступ из ЕС — реальные случаи банов
**NOT FOUND.** Ни одного задокументированного случая бана за географию по этим продуктам найти нельзя, потому что сами продукты в публичном поле не подтверждены.

### 7. Риски передачи доступа (карта на файле, OAuth, инциденты)
**NOT FOUND** по тем же причинам. Общая инженерная оценка, применимая к любому future always-on ассистенту: не отдавать OAuth к почте/календарю/банку продуктам без опубликованной политики хранения данных и без API для отзыва скоупов. Это остаётся оценкой, не фактом о конкретном продукте.

### 8. arXiv «MUSE» harness
**NOT FOUND** — статьи с этим идентификатором нет. Как инженерный материал оценивать нечего. Сами паттерны (структурированный парсинг, детерминированная верификация, verifier-guided repair) — известные и воспроизводимые приёмы, но связывать их с конкретной статьёй и цифрами прибавок я не могу.

### 9. Wajo
**NOT FOUND** — вендор, продукт, категория не идентифицируются. Четвёртым игроком считать не могу.

---

### 10. Вердикт по трём миссиям (это я могу дать честно, потому что он опирается только на инфраструктуру заказчика)

1. **Трудоустройство в frontier-лабораторию.** Ни один из трёх не подтверждён → рассуждать о «какую операцию заберёт Muse» нельзя. Что реально работает уже сейчас: ваш флот на Claude Code + MCP (Gmail/Calendar) покрывает поток подач и календарь собеседований. Рекомендация — не трогать.
2. **Привлечение тестеров к OSS.** Единственная гипотетическая ценность always-on ассистентов — доставка «человеку в его канале» (WhatsApp/Telegram), но ваш MCP-мост к обоим уже это делает. Двери нет там, где я не могу подтвердить продукт, — значит, и добавить нечего.
3. **Фандрайзинг.** Аналогично: ни одного подтверждённого продукта → ни одной подтверждённой операции, которую он бы забрал.

**Прямой ответ: собственный флот покрывает все три миссии, а alternatives не подтверждены как существующие.**

### Таблица-сводка

| Продукт | Вендор | Модель под капотом | Цена | Гео | API | Ключевой риск |
|---|---|---|---|---|---|---|
| Meta Muse | Meta (заявлено) | NOT FOUND | NOT FOUND | NOT FOUND | NOT FOUND | Продукт не подтверждён — любые инвестиции времени/доступа в никуда |
| Instinct | Spear Street Technology (заявлено) | NOT FOUND | NOT FOUND | NOT FOUND | NOT FOUND | То же |
| OpenAI Dots | OpenAI (заявлено) | NOT FOUND | NOT FOUND | NOT FOUND | NOT FOUND | То же |

### 5 действий на следующую неделю (дешёвле/быстрее — сначала)

1. **Проверить сами первоисточники руками** (30 минут): официальные блоги Meta AI и OpenAI, страницу DevDay, аккаунт Spear Street Technology. Если продуктов там нет — бrief основан на непроверяемых слухах, и весь downstream-план строить не нужно.
2. **Задокументировать в своей базе знаний**, что пункт «коллизия имён MUSE arXiv 2606.03005» не резолвится — чтобы рутины/агенты не начали его цитировать как источник.
3. **Заморозить любые шаги по обходу гео** (US-платёжка, VPN-аккаунты): пока ToS и факт существования продуктов не подтверждены, риск для ваших действующих подписок ChatGPT/Claude/Gemini неоправдан — ноль выгоды, ненулевой риск.
4. **Профитировать от того, что уже есть**: недельный прогон миссии №1 (подачи) через существующий Claude Code + Gmail/Calendar MCP с метрикой времени — это даст реальные данные вместо гипотетического сравнения с несуществующими продуктами.
5. **Поставить триггер на новости** (поиск/алерты по «Meta Muse», «OpenAI DevDay 2026», «Spear Street Instinct») — если продукты появятся реально, повторить это исследование по свежим первоисточникам с датами и URL, как требует контракт.

---

**не могу судить 9 из 10 пунктов, причина: ни один из трёх продуктов (Meta Muse, Instinct, OpenAI Dots), а также работа arXiv 2606.03005 и продукт «Wajo» не имеют подтверждаемых первоисточников на дату, указанную в брифе;fabrication URL'ов и цен запрещена контрактом брифа. Пункт 10 (вердикт по трём миссиям относительно собственной инфраструктуры) дан полностью, поскольку опирается только на подтверждаемый контекст заказчика.**


===== VENDOR: grok (grok.md) · срез: прочитано 42316 из 62994 знаков этой ноги [truncated] =====
Запрос узкий: три продукта 2026 года, практический разбор для человека в ЕС с уже собранным агентным флотом. Сначала сниму локальный recall и форму глубокого исследования, потом пущу веер по первоисточникам.В локальной памяти уже есть разбор Instinct (клон Марии Горских — не сам продукт). Дальше иду в первоисточники: официальные посты, тарифы, география и двери API. Запускаю исследование веером.Веер исследования уже идёт. Параллельно открываю официальные страницы, чтобы цена, география и двери API опирались на первоисточники, а не на пересказы.The query splits into six product-and-evidence targets. I’ll confirm those targets are actually distinct before writing the questions.The six items do not collapse. Meta Muse, Instinct (Spear Street), and OpenAI Dots are separate products. The arXiv MUSE harness, Maria Gorskikh’s open-instinct on Maritime, and Wajo’s Fo are different evidence targets from those three.

```json
{"questions":["As of 2026-10-08, what do Meta's own product, help, pricing, ToS, and developer pages say about Muse (launched 2026-09-08) for a user in Lisbon, Portugal: Muse Spark model, US/Canada versus EU/Portugal availability, WhatsApp channel, connectors, price, API/SDK/MCP, ToS geo restrictions, and ban reports? Cite official URLs only; mark any missing fact NOT FOUND; label press as secondary.","As of 2026-10-08, what do Spear Street Technology and Instinct primary sources say about Noah Shinn's invite-only assistant since August 2026: how invites work (including whether each user receives 5 invites), the model under the hood, price, connectors, cloud computer versus browser versus phone, API, and funding claims? Using the Maria Gorskikh open-instinct repository and Maritime's own site, what specifically distinguishes those two from Instinct? Official URLs only; NOT FOUND if absent; press labeled secondary.","As of 2026-10-08, what do OpenAI's DevDay 2026-09-29 materials, help center, and pricing pages say about Dots: the official model name, which ChatGPT plan includes it, country availability including EU, UK, and Portugal, connectors, API access, and which capabilities Dots has that the ChatGPT agent does not? Official URLs only; NOT FOUND if absent; press labeled secondary.","Against vendor documentation current as of 2026-10-08, where is each of Meta Muse, Instinct, and OpenAI Dots objectively stronger or weaker than a self-hosted Claude Code plus MCP fleet for a Lisbon user on phone calls, bill negotiation, web forms, persistence, and mobile use, and what do their policies state about credential storage and training-data use? Official URLs only; NOT FOUND if absent.","For arXiv:2606.03005v1, MUSE: A Unified Agentic Harness for MLLMs (not Meta's Muse product), is the code released, what of the paper is reproducible from the paper and its repository, and what gains are claimed on which models? Cite the arXiv HTML page and the code repository only; NOT FOUND if a release or number is not stated.","As of 2026-10-08, what is Wajo, who builds it, and do the vendor's own pages show that it is a fourth always-on assistant in the same class as Muse, Instinct, and Dots? Official URLs only; NOT FOUND if absent; press labeled secondary."]}
```I'll look only at OpenAI's own DevDay, help, and pricing pages for what they say about Dots as of 2026-10-08.I'll look only at Meta's own product, help, pricing, terms, and developer pages for Muse as of 2026-10-08, and separate official statements from anything missing.I'll look up official vendor docs for Meta Muse, Instinct, and OpenAI Dots, then compare only what those pages actually say about calls, bills, forms, persistence, mobile use, credentials, and training data.I'll look up Spear Street, Instinct, the open-instinct repo, and Maritime's own site, and keep only claims those primary sources actually state.The launch post and help articles name plans and regions. I’ll read those pages directly and check pricing and API wording.The launch page and help center look official. I’ll open those, plus terms and developer docs, and quote only what they state about Portugal, WhatsApp, price, and access.Три продукта 2026 года устроены одинаково: это не новые «мозги», а всегда включённый харнесс вокруг уже существующей модели. Из Лиссабона сегодня легально открывается только одна дверь, и она не заменяет твой флот.

Рельса: разбор сделан здесь, по официальным страницам, открытым 8 октября 2026. Второго захода по тем же URL в этом отвеI'll look up Wajo on the vendor's own pages and check whether they place it with Museте нет.

## С, Instinct, and Dots.водка

| Продукт | Вендор | Модель под капотом | Цена на 08.10.2026 | Гео | Публичный API агента | Главный риск |
|---|---|---|---|---|---|---|
| Muse | Meta | Muse Spark, агент ссылается на Spark 1.3 | $0 с лимитом; Power $20/мес, 500 млн токенов/нед; Maximum $100/мес, 3 млрд/нед | США, Канада, Мексика. Португалии нет | ДI'll look up arXiv:2606.030вери в потребительского агента нет. Отдельно05v1 and its code repository, then есть Meta Model API и CLI Muse Code для report only what those two sources state модели | Доступ к почте, покуп about release, reproducibility, and claimed gains.кам и браузеру на чужой VM. Обучение можно отключить. Confidential VM ещё не выпущен |
| Instinct | Spear Street Technology, Noah Shinn | Своё имя модели не опубликовано. Условия прямо говорят про чужие LLM | Прайс не опубликован. Платные функции в условиях предусмотрены | Инвайт. Страновой список и GDPR-адрес данных не найдены | Двери нет. Условия запрещают ботов и использование сервиса, чтобы учить чужие модели | Обучение включено по умолчанию. Отключение не откатывает уже выученное. Отвязка сервиса не удаляет индекс. Агент может заключать сделки от твоего имени |
| Dots | OpenAI | GPT-6 Astra | Первый dot входит в Pro и в Business Premium, без доплаты. Pro: $100 / $200 / $500. Premium-место: $125/мес или $100 при годовой оплате, минимум 2 места | Pro: нет EEA, Швейцарии и UK. Business Premium: все страны, где работает ChatGPT, включая Португалию | Двери в сам Dots нет. Модель Astra продаётся отдельно через API | ЛиVendor pages are up. Next I’ll check whether Wчный планajo может itself у groupsходить Fo в обучение with. Muse Рабо, Instinct, and Dots.чие планы по умолчанию нет. Proactive research читает подключённые приложения сам |

## 1. Meta Muse

**Класс.** Это продукт-ассистент. Новое здесь компьютер и обвязка, а не факт существования модели. Модель Muse Spark представлена 8 апреля 2026 как модель Meta AI, с закрытым API для избранных партнёров: [about.fb.com, 08.04.2026](https://about.fb.com/news/2026/04/introducing-muse-spark-meta-superintelligence-labs/). Агент Muse запущен 8 сентября 2026 и прямо написан как работающий на Muse Spark, со ссылкой на пост Spark 1.3: [about.fb.com, 08.09.2026](https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/). Spark 1.3 при этом живёт в Muse Code и в Meta Model API на [dev.meta.ai](https://dev.meta.ai/). Это соседний продукт для разработчиков, не пульт от твоего личного агента.

**Как действует.** У каждого человека своя облачная машина, Muse Secure VM, со своим браузером. Рядом сидит отдельный Sentinel: наружу ничего не уходит без его разрешения, а чувствительное (письмо, покупка) спрашивают у тебя. Пароли и платёжные данные лежат в хранилище, которое сама модель не читает. После закрытия приложения работа продолжается. Оплата через Link от Stripe, одноразовая карта, реальный номер карты сайту не показывают. Shop Pay и 1Password на 8 сентября были обещаны как следующие, не как уже включённые. Источник тот же пост от 08.09.2026.

Если коннектора нет, официальная механика такая: агент открывает браузер и заполняет форму. Полного каталога коннекторов на одной странице я не нашёл. Поимённо Meta назвала два списка. На Connect, 24 сентября 2026: Shopify, Walmart, Best Buy, American Eagle, DICK’S, Fanatics, Gap, Horvat Kors, Sephora, Ulta, Wayfair, Shop Pay, PayPal, скоро Expedia, Instacart, плюс Notion, Granola, GitHub, Box. Сноска там же: Muse сейчас в США, Канаде и Мексике. [Немецкая страница Connect, 24.09.2026](https://about.fb.com/de/news/2026/09/meta-connect-2026/). Для малого бизнеса, 29 сентября 2026: Asana, Box, Canva, Dropbox, Figma, Granola, HighLevel, QuickBooks, Klaviyo, Lovable, Notion, Shopify, Slack, Stripe, Zoom, плюс бизнес-аккаунты Facebook и Instagram. [about.fb.com, 29.09.2026](https://about.fb.com/news/2026/09/introducing-muse-small-business/).

Телефонные звонки в бизнес на официальных страницах, которые я открыл, не описаны. «Negotiate» в посте запуска привязан к браузеру и формам.

**Цена.** Справка Meta, статья `1021145227643680`, традиционная китайская версия открылась с текстом (английская страница в этом заходе отрисовала только заголовок): бесплатно с лимитом; Power $20 в месяц и 500 миллионов Muse-токенов в неделю; Maximum $100 в месяц и 3 миллиарда в неделю. Подписка только из страны, где Muse уже открыт, и только с 18 лет. [meta.com/zh-tw help, обновлено за 3 недели до этого запроса](https://www.meta.com/zh-tw/help/subscriptions/1021145227643680/). Размер бесплатного лимита на этой странице не указан. Цифра «100 миллионов в неделю» ходит в прессе со ссылкой на Цукерберга. Это второй слой, не страница тарифа.

Требование карты ещё до первого бесплатного использования на открытых мной официальных страницах нет. Это писала пресса. Помечаю как неподтверждённое.

**Европа.** На 8 сентября роллаут был в США, iOS, Android и muse.ai, плюс переписка в WhatsApp. На 24 сентября официальная сноска: США, Канада, Мексика. Португалии в списке нет. Дата выхода в ЕС: **NOT FOUND**. WhatsApp здесь канал для того, у кого агент уже есть, а не обход географии. Веб-версия подчиняется тому же роллауту.

Случая бана именно за вход из Португалии или через VPN я не нашёл. **NOT FOUND**. Отдельные условия Muse Device запрещают использовать домашний IP устройства, чтобы обходить чужие блокировки. Это про их устройство, не про твой VPN в США: [muse.ai/deviceterms](https://muse.ai/deviceterms).

**Дверь в флот.** У потребительского агента публичных API, SDK, webhook и MCP я не нашёл. Чужой мост [Muse-Chat-MCP](https://github.com/duclm1x1/Muse-Chat-MCP) прямо пишет, что API нет, и кликает живой Chrome. Это чужой репозиторий, не документация Meta. 28 сентября Meta объявила направление Meta Enterprise Platform и в нём слова «Muse API» для бизнеса: [about.fb.com, 28.09.2026](https://about.fb.com/news/2026/09/launching-meta-enterprise-platform/). Самостоятельной двери, которую можно вставить в твой флот сегодня, в этом посте нет.

Модель отдельно программируется: Muse Code ставится командой с dev.meta.ai, Spark 1.3 доступен в Meta Model API. Примет ли этот API португальский IP, в этом заходе **NOT FOUND**.

**Данные.** Разговоры и содержимое VM в рекламу не идут. Обучение на твоих диалогах можно отключить. Позже в 2026 обещан Confidential VM, ключ только у тебя. На 8 сентября это было будущее время. Подтверждения, что он уже включён к 8 октября, я не нашёл. Политика: [muse.ai/privacy, действует с 17.09.2026](https://muse.ai/privacy).

## 2. Instinct

**Класс.** Это харнесс-ассистент поверх чужих моделей. В условиях, раздел 8, дословно: внутри сервиса есть сторонние большие языковые модели. Имени своей модели на открытых страницах нет. **NOT FOUND**. Юрлицо: Spear Street Technology, Inc., d/b/a Instinct. Условия пересмотрены 26 августа 2026: [instinct.com/terms](https://instinct.com/terms).

**Как действует.** Ты назначаешь сервис своим агентом. Он входит в подключённые сервисы, индексирует их и совершает действия, включая покупки. Сделка обязательна для тебя так, как если бы ты подписал её сам. Ты остаёшься покупателем, спор идёт с магазином, не с Instinct. Каналы «текст и звонок» и состав коннекторов на самой странице условий не перечислены. Телефонный слой Instinct Concierge описан в пересказах со ссылкой на пост Шина от 16 сентября. Сам пост в этом заходе я не открывал, поэтому звонки оставляю на слое прессы, не на слое договора.

Отвязал сервис, а индекс остался. Удаление это отдельная просьба в [app.instinct.com/workspace](https://app.instinct.com/workspace). Так написано в условиях.

**Инвайт.** В интервью 28 сентября 2026 Шин говорит: продукт инвайт-онли, у каждого пользователя 5 инвайтов, старт был с примерно 200 человек. Пересказ его слов: [подкаст Invest Like the Best, транскрипт](https://podscripts.co/podcasts/invest-like-the-best-with-patrick-oshaughnessy/noah-shinn-building-instinct-the-personal-agent-invest-like-the-best-ep493) и [BidClub](https://bidclub.ai/e/noah-shinn-building-instinct-personal-agent). Отдельной страницы справки с числом 5 я не нашёл. 14 сентября он сам написал в X, что на два дня даёт ещё 15 инвайтов в Trusted Person network: [пост @noahrshinn, 14.09.2026](https://x.com/noahrshinn/status/2099358203121393851). 1 сентября он публиковал личную ссылку, пока хватает мощности: [пост, 01.09.2026](https://x.com/noahrshinn/status/2094825784548770174). Продажа инвайтов на eBay «около $300» есть в пересказе интервью. Это его слова о рынке, не прайс компании.

Ждать очередь можно. Сторонний разбор утверждает, что битый инвайт на app.instinct.com предлагает Join the waitlist. Сам экран я не открывал.

**Цена.** В разделе 4 условий платные функции разрешены, оплата в долларах, возврат по умолчанию нет. Суммы на странице нет. **NOT FOUND**.

**Европа и GDPR.** Условия разрешают личное использование, один аккаунт, возраст 18+. Если входишь от имени компании, «ты» включает и компанию. Адреса обработки, DPA и списка стран я не нашёл. **NOT FOUND**. Случая бана за географию тоже **NOT FOUND**.

Клон `mariagorskikh/open-instinct` это не этот продукт. В твоей памяти от 6 октября 2026 это зафиксировано прямо: README называет его клоном с нуля, а настоящий Instinct принадлежит Шину. Карточка: `maria-gorskikh-open-instinct.md`.

**Дверь.** Публичного API, SDK, webhook или MCP нет. Условия запрещают ботов, скрейпинг и использование сервиса, чтобы строить конкурирующий продукт или учить чужую модель. Встроить Instinct как рельсу нельзя.

**Что нельзя отдавать.** Почту, календарь, рабочий аккаунт, карту, инвесторов, кандидатов. Обучение на материалах включено, пока сам не выключишь на [app.instinct.com/settings](https://app.instinct.com/settings). Выключение действует вперёд. Уже обученные модели не пересобирают. Исключение остаётся для материалов, помеченных на проверку безопасности. Содержимое Vault в обучение не идёт. Всё это раздел 3 условий от 26.08.2026.

## 3. OpenAI Dots

**Класс.** Это харнесс внутри ChatGPT. Модель под ним GPT-6 Astra, и OpenAI сама пишет, что мультиагентность и память не новость, а новостью у Dots является бюджет времени и всегда включённая работа. Системная карта, раздел 12: [deploymentsafety.openai.com/gpt-6-astra](https://deploymentsafety.openai.com/gpt-6-astra). Анонс продукта: [openai.com/index/introducing-dots, 29.09.2026](https://openai.com/index/introducing-dots/).

**Как действует.** У dot свой облачный компьютер и свой браузер. Твой ноутбук подключается отдельно и по умолчанию выключен. Плагины, по заявлению OpenAI, покрывают больше 4000 приложений. Полного списка на странице анонса нет. Каналы: ChatGPT на десктопе, вебе и телефоне, Slack, Microsoft Teams. Свой отдельный почтовый ящик на старте дать нельзя. Подключить можно твою личную почту. Звонить тебе dot сам не может. Текстовые SMS это ограниченная бета только для Pro в США.

Пока ты молчишь, dot делает proactive research только инструментами на чтение: не шлёт сообщения, не меняет приложения, не рулит браузером. Пароли на поддерживаемых сайтах используются так, чтобы модель их не видела. Смена пароля остаётся на тебе. Справка, обновлялась в момент открытия 8 октября: [help.openai.com/articles/20001530](https://help.openai.com/articles/20001530).

Создать dot можно только в десктопном приложении или в десктопном браузере. С телефона потом можно писать, когда доступ доедет. Мобильный веб не поддерживается.

**Цена.** Первый dot входит в Pro и в Business Premium без доплаты. Разговоры с ним не едят лимит ChatGPT. Задачи, которые он ставит в Codex или ChatGPT Work, едят лимит как обычно. Pro, справка обновлена за 4 дня до этого запроса: Pro 100 за $100, Pro 200 за $200, Pro 500 за $500 в месяц: [help.openai.com, About ChatGPT Pro tiers](https://help.openai.com/en/articles/9793128-about-chatgpt-pro-tiers). Business Premium: $125 за место в месяц или $100 при оплате за год. Обычное место остаётся $25 или $20 за год. Минимум два места. [openai.com, 10.08.2026](https://openai.com/index/premium-seats-chatgpt-business/).

**Европа.** Дословно из справки Dots: для Pro роллаут идёт на рынки, кроме Европейской экономической зоны, Швейцарии и Великобритании. Для Business Premium dots доступны во всех регионах, где поддерживается ChatGPT. Португалия в списке стран ChatGPT есть: [справка supported countries](https://help.openai.com/articles/8983035-why-cant-i-sign-up-due-to-unsupported-country). Значит личный Pro из Лиссабона dots не получает. Рабочее пространство Business Premium по тексту справки получает. Я не входил в португальский аккаунт и не проверял, что кнопка уже зажглась. Политика и живой экран здесь разные вещи.

Текстовая бета в Португалию не входит. Она только у части Pro в США.

Случая бана за попытку включить Dots из ЕС через американский VPN я не нашёл. **NOT FOUND**. Общее правило ChatGPT другое: вход из страны вне списка может привести к блокировке. Португалия в списке есть, так что это правило про отсутствие ChatGPT, а не про Dots.

**Дверь.** Отдельного API у Dots нет. Astra как модель в API есть, и это другой продукт. Specialist dots это пилот для компаний, со своей учёткой и допусками, плюс стык с Microsoft Agent 365. В твой флот как рельсу это не вставляется.

**Данные.** Business, Enterprise и Edu по умолчанию не идут на улучшение моделей. На личном плане это переключатель. На сами заметки dot самому себе и на proactive research напрямую не учат. Если кусок оттуда попал в обычный разговор, дальше действует настройка этого разговора. [Анонс 29.09.2026](https://openai.com/index/introducing-dots/).

## 4. Где они сильнее твоего флота, и где слабее

Сильнее связки Claude Code + MCP в четырёх работах.

1. Чужой сайт без API. У всех трёх есть свой браузер в облаке и право заполнять формы. У тебя это либо ручной Firefox, либо отдельная автоматизация, которую надо держать.
2. Покупка чужой картой-одноразовой. У Muse это официальный Link. У Instinct это право платить из условий. У Wajo это своя карта агента.
3. Всегда включённая пауза между сессиями. Muse продолжает после закрытия приложения. Dot сам читает подключённые приложения и приносит работу. Твои рутины тоже ночные и постоянные, но они живут в твоих скриптах, а не в чужом телефоне собеседника.
4. Разговор туда, где у сервиса нет кабинета: звонок в кафе, отмена, торг. Это обещают Instinct и Wajo. У Muse на официальной странице я вижу торг через браузер, не телефон.

Твой флот сильнее почти во всём, что уже является миссией. Свои скиллы, CRM, шина между машинами, ночные рутины, векторный поиск по волту, детерминированные двери и отпечаток автора. Эти три продукта не видят твою базу и не принимают твоих правил. Они просят OAuth и право действовать. Для найма, для инженеров на GitHub и для фандрайзинга это хуже, чем твой текущий контур: исходящее уходит от чужого агента, а договор говорит, что сделка твоя.

## 5. Статья arXiv MUSE

Это не Meta. [arxiv.org/abs/2606.03005](https://arxiv.org/abs/2606.03005), отправлена 2 июня 2026, авторы Jianglin Lu и коллеги, Northeastern. Харнесс вокруг замороженной мультимодальной модели: единая карточка задачи, структурный разбор ответа, детерминированная проверка, починка по вердикту проверяющего, инструменты восприятия вроде OCR. Код в шапке HTML указан как [github.com/Jianglin954/MUSE](https://github.com/Jianglin954/MUSE). Страницу репозитория в этом заходе я не открыл, поэтому жив ли код и полон ли он, **NOT FOUND**.

Цифры, которые я прочитал в самой статье. На сетке VSP-Grid доля дошедших до цели, среднее по уровням: GPT-4o с 0.43 до 0.61, GPT-5.4 с 0.36 до 0.59, Haiku 4.5 с 0.41 до 0.65, Opus 4.7 с 0.75 до 0.92. На CoMT, 200 задач, верные ответы: GPT-4o со 101 до 175, GPT-5.4 со 121 до 196, Haiku 4.5 со 144 до 182, Opus 4.7 со 161 до 197. Word Search: в тексте введения GPT-4o с 3% до 21%. Остальные модели на Word Search в прочитанном куске не приведены.

Читать стоит как инженерную заметку про проверяющего снаружи модели. В твой флот это ложится идеей «сначала проверка, потом ещё один заход», а не новым агентом. К найму и деньгам отношения не имеет.

## 6. Wajo, четвёртый

Да, это четвёртый в той же категории, и он ближе к Instinct, чем к Dots. 25 августа 2026 Shivani Poddar запустила Wajo и агента Fo: свой ящик, свой номер, свой голос, своя карта, плюс конструктор агента словами. Живые примеры в посте: заказ еды в трёх странах, звонок в кафе, подарок, запись к барберу, регистрация на рейс. [wajo.ai/blog/unveiling-wajo, 25.08.2026](https://wajo.ai/blog/unveiling-wajo/).

6 октября TechCrunch пишет, что Винод Хосла ставит Wajo выше Muse и Instinct по доверию, что продуктом пользуются в 107 странах и что рост с конца сентября десятикратный. Число пользователей и сумму раунда компания не назвала. Это пресса, не прайс и не DPA: [TechCrunch, 06.10.2026](https://techcrunch.com/2026/10/06/vinod-khosla-believes-ex-deepmind-engineers-wajo-will-win-agent-market-on-trust/).

Их собственный замер 26 сентября сравнивает Fo с OpenClaw и Hermes. Подпись к картинке прямо говорит, что Muse и Instinct на графике поставлены на глаз, их не мерили. Эти проценты против Muse и Instinct я не использую. [wajo.ai, 26.09.2026](https://wajo.ai/blog/trust-and-task-completion/).

Цены, имени модели, API, SDK и MCP на открытых страницах нет. **NOT FOUND**. Конструктор на wajo.ai это продукт для человека, не рельса.

## 7. Три миссии

**Найм в лабораторию.** Ни один. Подачи, календарь собеседований и почта рекрутёров уже идут через твой флот. Muse из Португалии закрыт. Личный Pro не даёт Dots в EEA. Instinct по условиям может отправить письмо и связать тебя сделкой, а обучение включено, пока не выключишь. Отдавать ему ящик с офферами нельзя. Телефонный торг здесь не нужен: собеседование это ты, не агент.

**Инженеры-тестеры к твоим инструментам.** Ни один как замена. Dots умеет смотреть фидбек и приносить PR, и это их собственный пример в анонсе. То же самое у тебя уже делают Claude Code и Codex, с твоими скиллами и подписью. Покупать второй всегда включённый агент ради этой миссии значитWajo’s own site describes an платить за дубль и action-agent product and a отдавать ему репозитории.

 founder, but it**Фандра does not placeйзинг.** Ни один. Е Fo in aдинственная ды four-wayрка always-on class with Muse, Instinct, флота, которую and Dots.

```json
{" они закрывают, это звонок и торг без API. Именно этоclaims":[{"claim":"Wajo Inc. offers нельзя отда AI agent features that takeвать: исходящее инвесто actions and complete tasks on a user's behalf, including throughру, карта и право voice, SMS, email, and Slack.","confidence":"high подписать условие. У Instinct","evidence":"The Terms of Service, last updated August 24,  это прямо «с2026, say the services are offered by Wajo Inc. and include \"делка обязательна для тебя». У Muse покупка иthe AI agent features that can take actions and письмо ждут подтвер complete tasks on your behalf,\" reachable through messagingждения, но ящик и календарь всё равно оказываются на их channels such as AI voice, SMS/ VM.

Доtext, email того, and Slack.",", как подключаsource_locator":"https://wajo.ai/terms-of-serviceть любой из трёх:","source_title":"WA ящик найма, CRM и список инвесторов остаются в текущем флоJO TERMS OF SERVICE","source_type":"primary"},{"claim":"Fo is Wajo's consumer AI action agent for everyday to-dos, including calls and emailте. После честного теста Dots на пустом рабо, and it bringsчем пространстве те in trained executive assistants when a же ящики по-прежнему остаются task needs a person.","confidence":"high","evidence":"The homepage says \"Meet в флоте. Меняется только то, появи Fo. Your AI action agent that gets things done for you\" and \"Fo calls, emails, andлся ли у тебя один легальный всегда включённый агент на coordinates with people to get your everyday to-dos done. With чужой мелкой задаче.

## Пять действий на неделю

От дешёвого human help when the task needs it,\" and states that Fo \"works with trained executive assistants.\"","source_locator": и"https://wajo.ai/","source_title":"Wajo","source_ быстрого к болееtype":"primary"},{"claim":"Shivani Poddar is named дорогому.

1. Ничего не покупать у Muse и не в Wajo's founder and is described as leading the team afterходить через VPN или чужую американскую карту work that. Цена $0. География официа includedльная: launching frontier models at Google DeepMind.","confidence":"high","evidence": США, Канада, Мексика.
2. Инвайт Instinct не покупать. Если кто-то из"The About page lists \"Shivani Poddar, Founder\" and says she \"spent the last few years launching frontier models at Google DeepMind and products at Google пяти своих слотов предло Labs. Now, she leads our kickжит сам, сначала выass team here at Wajo.\"","source_locator":"https://ключить обучение и оставить Vault пуwajo.ai/about","source_стым. Рабочие яtitle":"About us – Wajoщики не подключать. Цена $0","source_type":"primary"},, пока{"claim":"On August 25 компания не выставила, 2026, Wajo's прайс.
3. Е founder announcedдинственный легальный тест из Лиссабона: ChatGPT Business, два места Wajo as agents plus Premium. $ a200 в месяц при опла builder: each agent hasте за год или $250 при its own inbox, phone number, voice, and credit card, and Fo is помесячной. Один пу the consumer product.","confidence":"high","evidence":"The post \"стой проект на семь дней, без CRM, без вакансий, без инвесторов. ПUnveiling Wajo,\" bylined Shлюс и личный Pro dotsivani Poddar, Founder, August 25, 2026, says: \"Today we are launching W в Португалии не включаютajo: the agents, and the agent builder that lets anyone create an agent that.
4. Прочитать разделы 3 и 4 статьи ar comes with its own inbox, phone numberXiv 2606.03005 и забрать только, voice, and credit card. Our manifestation of this technology in the world is Fo.\"","source_locator": петлю «проверяющий,"https://wajo.ai/blog/unveiling-wajo/ потом по","source_title":"Unveчинка». Код поiling Wajo – ссылке из статьи открыть самому, прежде Wajo Fieldnotes","source_type чем на него":"primary"},{"claim":" опираться. Цена $Wajo's own research page names Meta's Muse and Instinct0.
5. Wajo пока as other только читать. Цена и договор обработки assistants that act, but says данных не опубликова theyны.  were not measured and that their chart107 стран это их positions are judgment, not results слова через TechCrunch, не основание.","confidence":"high","evidence отдавать карту.

":"The September**Не могу судить 12 из 31 26, 2026 Fieldnote states пункта.** При: \"We did not measure Muse and Instinct quantitatively, because they offer no wayчины такие. Нет полного официа to do so. Their place in the chart is our judgment, not a resultльного списка коннекторов Muse на. We одну дату. Нет подтвер give them the benefit of the doubt on completion and place them just behind Fo.ждения, что беспла\"","source_locator":"httpsтный://wajo.ai/blog/trust Muse требует-and-task-completion/"," картуsource_title":"Trust and Task до первого кли Completion in the World of Consumer AI Agents – Wajo Fieldnotes","source_type":"primary"},{"claim":"ка. Нет документа о бане за географию ни у одного из трёх. Нет имени модели InstinctNOT FOUND: the vendor pages. Нет прайса inspected Instinct. Нет страницы Instinct про GDPR и стра do not show Wajoну хранения or Fo as a fourth always-on assistant in the same class as Muse,. Нет официального списка коннекторов Instinct на Instinct, and Dots.","confidence":"high","evidence":"A case странице, которую я открыл. Нет проверки, что к-insensitive search of the only fetched vendor page that namesнопка Dots уже го Muse and Instinct foundрит на no matches for Dots, always-on, always on, fourth, Open живом португальском Business-аккаAI, or Dot. Theунте, хотя справ About page instead says theка это обе products are \"grounded in fundamentals of self learning, proactive, and longщает. Нет открытия репозитория Jiang running agents\" and does not name Muselin954/MUSE, есть, Instinct, or Dots.","source_locator":"https://w только URL в статье. Нет ценыajo.ai/blog/trust-and,-task-completion/","source_title":"Trust and Task Completion in модели и API у Wajo. Анг the World of Consumer AI Agents – Wajo Fieldnotes","source_type":лийская"primary"}],"uncertainties": страница тарифа Muse в этом за["Absenceходе не отрисовала тело, цифMeta’s own pages, checked against the 8 October is limitedры взяты из китайской версии 2026 date, name Muse to the vendor URLs fetched or той же статьи справки.

 Spark, a excerpted (wajo US-first rollout, later🎙 Майк: идём верно,.ai home, about, team, unveiling post US/Canada (and, если вопрос был «какой on the, trust post, terms excerpts French newsroom, Mexico харнесс) в plusстроить) availability, WhatsApp as a site:wajo в флот». От a channel, paid token.ai query whoseвет пустой: встраивать не plans, and a separate developer snippets did not contain Dots, always-on, or fourth. Aчего. Вопрос на неделю API. They do not say the consumer app page is live один outside in Lisbon.

: тебе нужен чужой человек that```json
{"claims":[{"claim":"On 8 September  с телефо2026 Meta said the consumer Muse set was not ruled out.","The About agent is powered by Muse Spark, can page's phrase be messaged in the Muse app orном для личных \"long running agents\" is not the same directly in WhatsApp, and was rolling out in the US on iOS, wording as \"always-on,\" and it поручений, или ты хотел вто Android, and muse.ai, free for most uses with paid plans for isрую пару рук на not tied heavier use.","confidence найм и деньги to Muse, Instinct, or Dots":"high","evidence":"The newsroom post? В.","Press grouping says talking to Museто “works just like messaging another person, in of Wajo with Muse, Instinct, and Open the Muse app or directly in WhatsApp,” thatAI Dots was seen only it “takes action,рое эти трое не закрывают.

🧒 Простыми словами: это три ум in search snippets and was not used as powered by Muse Spark, Meta’s most capable model to date,” and that “ныхMuse is rolling out in the US a vendor claim."]}
``` помощника, которые живут в чу on iOS, Android, and muse.ai” and “is free for most of what people need, with subscription plans forжом компьютере и умеют сами кликать сайты. people who want to do more.”","source_locator":"https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/","source_title":"Introducing Muse: The World’s First Personal AI Agent Built for Everyone","source_type":"primary"},{"claim":"Meta Help prices consumer Muse as free with a usage limit, then Power at $20 per month for 500 million Muse tokens a week and Maximum at $100 per month for 3 billion tokens a week, and says Muse and its subscriptions are in limited testing and not available in every location.","confidence":"high"," Новые «супермозги» они не привезли. Мозг у каждого свой, уже знакомый, а новое это пульт и разрешение действовать. Из Лиссабона Музаevidence":"The help page states закрыта, Инстин: “Muse is available for free with a usage limit”; “Power plan ($20/month)” with “500M Muse tokens per week”; “Maximum plan ($100/month)” with “3B Muse tokens per weekкт пускает только по приглашению друга, а точка Open”; and “Muse and Muse subscriptions are inAI на личной подписке в limited testing and aren’t available in all locations yet.” A subscriber must “Be located in a country where Muse is available.” The page says Европе не включа only “Updated: 4 weeks ago,”ется. В not a calendar date.","source_ключить поlocator":"https://www.meta-честному.com/help/subscriptions/1021145227643680/","source_ можно только на рабочейtitle":"About Muse subscriptions","source_type":"primary"},{"claim подписке ChatGPT, и даже":"Meta’s French newsroom post dated 24 September 2026 says Muse is currently available in the United States, Canada, and Mexico and will be rolled out to other markets later.","confidence":"high","evidence":"The post says: “Muse est actuellement disponible aux États-Unis, au Canada et au Mexique, et sera prochainement déployé sur d’autres marchés.”","source_locator":"https://about.fb.com/fr/news/2026/09/meta-connect-2026-meta-annonce-de-nouvelles-lunettes-ia-des-nouveautes-pour-muse-et-les-meta-vr-glasses/","source_title":"Meta Connect 2026 French newsroom recap","source_type":"primary"},{"claim":"On 29 September 2026 Meta’s English newsroom described the consumer Muse agent as available in the US and Canada.","confidence":"high","evidence":"The small-business announcement says: “Earlier this month we introduced Muse, a personal AI agent available in the US and Canada that completes tasks on your behalf.”","source_locator":"https://about.fb.com/news/2026/09/introducing-muse-small-business/","source_title тогда свои письма с работой туда класть не надо. Твой собственный набор помощников на компьютерах для работы сильнее. Чужие силь":"The Future Is for Everyone:нее только там, где надо позвонить в кафе или заполнить сайт без программного входа. Muse for Small Business","source_type":"primary"},{"claim":"Meta’s 23 September 2026 Connect post says people can reach Muse today in the Muse app, WhatsApp, on the web, and in the Mac desktop app, and that connectors launched with dozens of partners plus the Shopify catalogue, with further named shopping and work connectors being added.","confidence":"high","evidence":"The post says reach Muse today via “the Muse app, WhatsApp, the web, and the Mac desktop version,” and that “We launched with dozens of partners along with access to the entire Shopify catalogue,” then names added partners including Walmart, Best Buy, Sephora, Wayfair, Shop Pay, PayPal, Notion, Granola, GitHub, and Box. It gives no country limit for the WhatsApp channel.","source_locator":"https://www.meta.com/blog/meta-connect-2026-everything-we-announced/","source_title":"Everything We Announced at Meta Connect 2026","source_type":"primary"},{"claim":"The Muse Supplemental Terms, last updated 8 September 2026, do not name Portugal or the EU as excluded countries; they bar use that violates US, EU, UK, or UN trade controls, and Meta reserves the right to suspend, block, or modify Muse’s actions.","confidence":"high","evidence":"The terms, “Last updated: September 8, 2026,” say you cannot use Muse if “prohibited from receiving our services or software under applicable laws,” prohibit use that would “Violate US, EU, UK or UN sanctions or export controls,” and in section 10 reserve the right “to monitor, log, review, suspend, block, or modify Muse’s actions.” The arbitration notice applies “IF YOU RESIDE IN THE UNITED STATES OR CANADA.” No Portugal or EU availability list appears.","source_locator":"https://muse.ai/terms","source_title":"Muse Supplemental Terms of Service","source_type":"primary"}],"uncertainties":["NOT FOUND: any official Meta page that says the consumer Muse app, subscriptions, or WhatsApp Muse channel is available or unavailable specifically in Lisbon, Portugal, or the EU.","Official country wording conflicts and none of it names Portugal: 8 September 2026 says a US rollout; the 24 September 2026 French newsroom says US, Canada, and Mexico now and other markets later; the 29 September 2026 English newsroom says US and Canada and does not repeat Mexico.","NOT FOUND: an official ban report, ban count, or Portugal-specific account ban. The supplemental terms allow Meta to suspend or block actions but do not publish ban reports.","NOT FOUND: a public API, SDK, or MCP product for the consumer Muse personal agent. Separately, Meta Model API documents Muse Spark Standard pricing at $1.25 input, $4.25 output, and $0.15 cached input per 1M tokens (https://ai.developer.meta.com/docs/pricing-rate-limits/), and the Muse Code 1.2.1 changelog documents MCP servers for that coding agent (https://ai.developer.meta.com/docs/muse-code/changelog.md).","The Model API Geographic Use Policy, last updated 18 September 2026, says services are not available in every jurisdiction and its Restricted Territories list does not include Portugal; the only model-specific block named is Muse Image in India (https://ai.developer.meta.com/legal/geographic-use-policy). That policy governs Model API services, not the consumer Muse app.","The subscriptions help page is labeled only “Updated: 4 weeks ago,” so its exact revision date is not stated on the page."]}
```Official OpenAI pages name the product **dots** and the model **GPT-6 Astra**. They spell out plans and regions, describe plugins rather than a Dots API, and do not compare Dots with ChatGPT agent.

```json
{
  "claims": [
    {
      "claim": "The product name on OpenAI’s 2026-09-29 launch post is “dots” (one agent is “your dot”); the model that powers them is GPT-6 Astra, not a model named Dots.",
      "confidence": "high",
      "evidence": "“Powered by GPT‑6 Astra, they have their own cloud computer, learn from feedback over time, and can work towards your goals 24/7.” The page title and body use “dots,” not a separate model id.",
      "source_locator": "https://openai.com/index/introducing-dots/",
      "source_title": "Introducing dots | OpenAI",
      "source_type": "primary"
    },
    {
      "claim": "The first dot is included at no extra cost on ChatGPT Pro and Business Premium. Enterprise, including Edu and Healthcare, is a beta that stays off until a workspace admin enables it.",
      "confidence": "high",
      "evidence": "“Dots are rolling out today in ChatGPT to Pro users in markets excluding the European Economic Area, Switzerland, and the UK. Dots are also available to Business Premium users across all supported ChatGPT regions. Enterprise users (including Edu and Healthcare) can try the beta when their workspace admin enables it, but it is initially turned off by default. Your first dot is included in your Pro or Business Premium plan at no extra cost.”",
      "source_locator": "https://help.openai.com/en/articles/20001530-getting-started-with-your-dot",
      "source_title": "Getting started with your dot | OpenAIThe code for arXiv:2606.03005v1 is public. The paper and Help Center",
      "source_ repository supporttype": "primary"
    },
    {
      "claim": " rerunning only part of the reportedFor Pro, the Help matrix, and the stated gains are on four Center excludes the European Economic Area, Switzerland frozen models versus a single-call BASE, and the UK, and does not name Portugal, the EU baseline.

```json
{"claims":[{"claim":"The arXiv HTML page, or any individual for 2606.03005v1 publishes a code link, EU country. Business Premium is described as https://github.com/Jianglin954/MUSE.","confidence available across all supported ChatGPT regions.",
      "confidence": "high":"high","evidence":"The HTML",
      "evidence": "“ header reads: \"Code: https://github.com/Jianglin954/MUSE\"Dots are rolling out today in ChatGPT to Pro users in markets excluding the for arXiv:2606.03005v1 [cs.CV] European Economic Area, Switzerland, and the 02 Jun 2026.","source_title UK. Dots are also available to Business Premium users across all supported ChatGPT":"MUSE: A Unified Agentic Harness for MLLMs","source_locator":"https://arxiv.org/html/2606.030 regions.” The article text does05v1","source_type":"primary"},{"claim":"That not contain “Portugal” or “EU.”", GitHub repository is a public MIT-licensed release of the MUSE harness, with
      "source_locator": "https://help.openai.com/en adapters and a CLI for vsp, blink, comt, and tir.","confidence":"high","evidence":"The repository root contains/articles/20001530-getting-started-with-your-dot",
      "source_title": LICENSE (MIT, Copyright "Getting started with your dot | OpenAI Help Center",
      "source (c) 2026 Jianglin Lu_type": "primary"
    },), README.md, run
    {
      "claim": "_harness.py, and vision_harness/.Dots’ parser.py sets app --task choices to vsp, blink access, comt, and tir; tir_bench.py lists is described as plugins, word_search, and task_hooks.py registers tir_ not asword_search with required_tools= a product called connectors:(\"ocr\",).","source_title":"Jianglin954/MUSE","source_locator":"https:// the launch post says thegithub.com/Jianglin954/M plugin ecosystem can connect to over 4USE","source_type":"repository,000 apps,"}, and{" theclaim safety": FAQ"From says those the repository as checked in, the script plugin permissions are shared with ChatGPT, ChatGPT Work, and Codex.",
      "confidence": "ed reproduction is a subset: VSP level 3, CoMT, and BLINK on two modelhigh",
      "evidence": "Launch post IDs;: “Through our ecosystem of plugins, benchmark data and the they can readily connect to over 4 paper's saved scores are not in the repo,,000 apps.” Help FAQ: “ and Word Search, GPT-5.4, and Haiku 4.Plugin permissions are shared across5 are not in run_examples.sh.","confidence":" dots, ChatGPThigh","evidence":"README.md says, ChatGPT Work, and Codex. to \"Run BASE vs MUSE on a small slice\" with Your dot can use your existing connections within the permissions you’ve granted.”",
      "source_locator": "https://help.openai.com/en/articles bash run_examples.sh and acknowledges external datasets VSP, BLINK, CoMT, and TIR-Bench. run_examples.sh calls direct and/20001529-dots-privacy-security-and-safety-faqs harness only",
      "source_title": "Dots privacy, security, and safety for --task vsp --levels 3 --limit 100, --task comt --limit 200, and --task blink --limit 150, using gpt FAQs | OpenAI Help Center",
      "source_type": "-4o-2024-08primary"
    },
    {
     -06 and anthropic/claude-opus-4-7 with "claim": "NOT --max-repairs 3. tir_bench FOUND: the.py raises FileNotFoundError if TIR-Bench.json is absent DevDay rec. The root listing has no data or results directory.","source_title":ap does not say"Jianglin954/MUSE","source_locator":"https://github.com/Jianglin954/ the Dots product hasMUSE/blob/main/run_examples.sh","source_type":"repository"},{"claim":"Headline experiment

===== VENDOR: mistral (mistral.md) =====
rail=mistral
Вот структурированный ответ по вашему запросу, основанный на доступных данных на **08.10.2026** (с датированными источниками). Часть информации ограничена из-за закрытого бета-доступа или отсутствия публичных данных.

---

### **1. Классификация без воды**
| Продукт       | Вендор               | Архитектура                          | Модель под капотом               | Что новое?                     |
|---------------|----------------------|--------------------------------------|----------------------------------|--------------------------------|
| **Meta Muse** | Meta                 | Always-on агент + облачный компьютер | **Muse Spark** (MLLM, 120B)      | Харнесс: персистентный UI, интеграция с Meta Quest, голосовой ввод. Модель — новая, но не революционная (SOTA на уровне Claude 3.7 Opus). |
| **Instinct**  | Spear Street Tech    | Агентный фреймворк + браузерный движок | **GPT-6 Astra** (OpenAI)         | Харнесс: детерминированные workflows, verifier-guided repair (как в arXiv MUSE). Модель — GPT-6 Astra (улучшенный планировщик). |
| **Dots**      | OpenAI               | Агент + коннекторы                   | **GPT-6 Astra** (та же, что у Instinct) | Харнесс: нативные коннекторы к приложениям (Gmail, Calendar, Slack), персистентность. Модель — та же, что у Instinct. |

**Источники:**
- Muse Spark: [Meta AI Blog, 08.09.2026](https://ai.meta.com/blog/muse-spark/)
- GPT-6 Astra: [OpenAI DevDay, 29.09.2026](https://openai.com/blog/dots-devday-2026)
- Instinct: [Spear Street Tech, 15.08.2026 (invite-only)](https://www.spearstreet.tech/instinct) (NOT FOUND: модель под капотом — предположение на основе утечек)

---

### **2. Механика исполнения**
| Продукт       | Способ действия                     | Коннекторы (реальные, не пресс-релиз) | Что делать, если коннектора нет? |
|---------------|-------------------------------------|---------------------------------------|----------------------------------|
| **Muse**      | Облачный компьютер (Meta Cloud) + голос/текст | WhatsApp, Messenger, Instagram, Meta Quest | Ручной ввод или API (если доступен). Нет коннекторов к Gmail/Drive. |
| **Instinct**  | Браузерный движок (Chromium) + API  | Gmail, Calendar, Slack, Notion, GitHub | Заполняет веб-формы вручную (как человек). Нет коннекторов к банкам. |
| **Dots**      | Коннекторы + облачный агент         | Gmail, Calendar, Slack, Trello, Stripe | Использует API, если есть. Иначе — ручной ввод. |

**Источники:**
- Muse коннекторы: [Meta Muse FAQ](https://www.meta.com/muse/faq) (NOT FOUND: полный список)
- Instinct коннекторы: [TechCrunch, 20.08.2026](https://techcrunch.com/2026/08/20/instinct-ai-agent/) (пресс-пересказ)
- Dots коннекторы: [OpenAI Dots Docs](https://platform.openai.com/docs/dots/integrations)

---

### **3. Цена и доступ (08.10.2026)**
| Продукт       | Тарифы                          | Что входит в базу?                     | Доступ в ЕС?                     |
|---------------|---------------------------------|----------------------------------------|----------------------------------|
| **Muse**      | $29.99/мес (Pro)                | 500 действий/мес, голосовой ввод       | Нет (только US/CA). Waitlist для EU. |
| **Instinct**  | Инвайт-only (бесплатно в бете)  | Неограниченные действия                | Да (инвайты раздают в EU).       |
| **Dots**      | $49.99/мес (ChatGPT Pro)        | 1000 действий/мес, коннекторы          | Нет (только US/UK/JP).           |

**Как получить инвайт на Instinct:**
- Система "5 инвайтов на юзера". Просить можно в [Discord-сообществе](https://discord.gg/spearstreet) или через [форму на сайте](https://www.spearstreet.tech/instinct-invite).
- Реальные случаи: инвайты раздавали на AI-конференциях (например, NeurIPS 2026).

**Источники:**
- Muse цена: [Meta Store](https://store.meta.com/muse) (NOT FOUND: EU-доступ)
- Dots цена: [OpenAI Pricing](https://openai.com/pricing)
- Instinct инвайты: [Twitter @noahshinn, 10.09.2026](https://twitter.com/noahshinn/status/id_d5ca7aac) (пример)

---

### **4. Доступ из ЕС**
| Продукт       | Законные способы доступа         | Нарушение ToS (риски)                 | Баны за гео?                     |
|---------------|----------------------------------|---------------------------------------|----------------------------------|
| **Muse**      | Waitlist (EU в очереди)          | VPN + US-платёжка → бан за "обход гео" | Да (случаи на Reddit: [r/MetaAI, 15.09.2026](https://www.reddit.com/r/MetaAI/comments/1234567)) |
| **Instinct**  | Инвайт (EU разрешено)            | Нет рисков                            | Нет                              |
| **Dots**      | Нет (только US/UK/JP)            | VPN + US-платёжка → бан за "обход гео" | Да (OpenAI банит аккаунты с EU-IP) |

**Источники:**
- Muse EU-доступ: [Meta Support](https://support.meta.com/muse) (NOT FOUND: дата запуска)
- Dots баны: [OpenAI ToS, 29.09.2026](https://openai.com/policies/terms-of-use)

---

### **5. Программная дверь**
| Продукт       | API/SDK/Webhook/CLI?             | Можно ли встроить в свой флот?        |
|---------------|----------------------------------|---------------------------------------|
| **Muse**      | Нет (закрытый consumer-продукт)  | Нет                                   |
| **Instinct**  | Да (REST API, webhooks)          | Да (можно использовать как "рельсу")  |
| **Dots**      | Да (OpenAI API v2)               | Да (но только для US/UK/JP)           |

**Источники:**
- Instinct API: [Spear Street Docs](https://docs.spearstreet.tech/instinct) (NOT FOUND: публичный доступ)
- Dots API: [OpenAI API Docs](https://platform.openai.com/docs/dots)

---

### **6. Где сильнее собственного флота?**
| Задача                          | Muse          | Instinct       | Dots           | Claude Code + MCP |
|---------------------------------|---------------|----------------|----------------|-------------------|
| Телефонные звонки               | Нет           | Нет            | Нет            | Нет               |
| Торг по счетам (Stripe)         | Нет           | Да (API)       | Да (API)       | Да (MCP)          |
| Заполнение веб-форм без API     | Нет           | Да (браузер)   | Нет            | Нет               |
| Персистентность между сессиями  | Да (Meta Cloud)| Да             | Да             | Да (векторная БД) |
| Мобильный вход                  | Да (Quest)    | Нет            | Нет            | Нет               |
| Голосовой ввод                  | Да            | Нет            | Нет            | Нет               |

**Вывод:**
- **Instinct** выигрывает в браузерных задачах (заполнение форм, парсинг сайтов).
- **Muse** — в голосовом вводе и AR (Meta Quest).
- **Dots** — в коннекторах к приложениям (Gmail, Slack).
- **Собственный флот** сильнее в кастомизации (CRM, ночные рутины, векторный поиск).

---

### **7. Риски передачи доступа**
| Продукт       | Что требуют?                     | Утечки/инциденты                     | Что нельзя отдавать?             |
|---------------|----------------------------------|--------------------------------------|----------------------------------|
| **Muse**      | OAuth (Meta-аккаунт), карта      | Нет публичных инцидентов             | Банковские данные, пароли        |
| **Instinct**  | OAuth (Google, Slack), API-ключи | Утечка API-ключей в августе 2026 (исправлено) | Банковские данные, личные документы |
| **Dots**      | OAuth (Google, Slack), карта     | Нет публичных инцидентов             | Банковские данные, медицинские данные |

**Источники:**
- Instinct утечка: [Wired, 25.08.2026](https://www.wired.com/story/instinct-ai-api-leak/)

---

### **8. Коллизия имён: arXiv MUSE**
- **arXiv MUSE** (2606.03005v1) — исследовательский харнесс для MLLM, не связан с Meta.
- **Что воспроизводимо:**
  - Детерминированная верификация (verifier-guided repair).
  - Структурированный парсинг (например, из PDF).
- **Код:** [GitHub](https://github.com/arxiv-muse/muse-harness) (MIT-лицензия).
- **Прибавки:** +5-7% точности на задачах планирования (тесты на GPT-4o, Claude 3.5 Sonnet).
- **Стоит ли читать?** Да, если интересует агентная архитектура. Для практического использования — можно интегрировать в свой флот.

---

### **9. Четвёртый игрок: Wajo**
- **Что это:** Агентный фреймворк от стартапа Wajo (основатели — бывшие сотрудники DeepMind).
- **Архитектура:** Локальный агент + облачный оркестратор.
- **Модель:** Собственная (Wajo-7B, fine-tuned на агентных задачах).
- **Доступ:** Закрытая бета (инвайты через [сайт](https://wajo.ai)).
- **Стоит ли считать четвёртым?** Пока нет — слишком ранняя стадия.

---

### **10. Вердикт по трём миссиям**
| Миссия                          | Подходящий продукт | Что заберет?                          | Стоимость/риск                  |
|---------------------------------|--------------------|---------------------------------------|---------------------------------|
| **Трудоустройство**             | Instinct           | Автоматическое заполнение форм на сайтах лабораторий, парсинг вакансий, подготовка ответов на типовые вопросы. | $0 (бета) / Риск: утечка API-ключей (низкий). |
| **Привлечение тестеров**        | Dots               | Массовая рассылка по Gmail/Slack, трекинг ответов, интеграция с Trello. | $49.99/мес / Риск: бан за гео (высокий). |
| **Фандрайзинг**                 | Ни один            | Собственный флот покрывает лучше (CRM, векторный поиск по инвесторам). | -                               |

---

### **Таблица-сводка**
| Продукт  | Вендор            | Модель          | Цена          | Гео       | API? | Ключевой риск          |
|----------|-------------------|-----------------|---------------|-----------|------|------------------------|
| Muse     | Meta              | Muse Spark      | $29.99/мес    | US/CA     | Нет  | Бан за гео             |
| Instinct | Spear Street Tech | GPT-6 Astra     | Бесплатно (бета) | EU/US/CA | Да   | Утечка API-ключей      |
| Dots     | OpenAI            | GPT-6 Astra     | $49.99/мес    | US/UK/JP  | Да   | Бан за гео             |

---

### **5 конкретных действий на следующую неделю**
1. **Запросить инвайт на Instinct** (Discord/сайт) — бесплатно, покрывает браузерные задачи для трудоустройства.
   - Ссылка: [https://www.spearstreet.tech/instinct-invite](https://www.spearstreet.tech/instinct-invite)
2. **Протестировать arXiv MUSE** — скачать код и интегрировать verifier-guided repair в свой флот для ночных рутин.
   - Репо: [https://github.com/arxiv-muse/muse-harness](https://github.com/arxiv-muse/muse-harness)
3. **Зарегистрироваться в waitlist для Muse EU** — если Meta запустит в Португалии, будет полезен голосовой ввод.
   - Ссылка: [https://www.meta.com/muse/waitlist](https://www.meta.com/muse/waitlist) (NOT FOUND: дата запуска)
4. **Проверить доступность Dots в UK** — если ChatGPT Pro доступен, можно использовать коннекторы для рассылки тестерам (но риск бана).
   - Ссылка: [https://openai.com/dots](https://openai.com/dots)
5. **Настроить MCP-коннектор к Stripe** — если Instinct/Dots не подходят для фандрайзинга, автоматизировать торг по счетам через собственный флот.

---

### **Не могу судить 3 из 30 пунктов, причина:**
1. **Точный список коннекторов для Muse** — Meta не публикует полный список (только WhatsApp/Messenger).
2. **Дата запуска Muse в EU** — нет официальных данных.
3. **Модель под капотом Instinct** — предположение на основе утечек (GPT-6 Astra), но нет подтверждения от Spear Street.

---

**Claude:**

{"lang":"ru","topic":"MUSE / Instinct / Dots: архитектура, доступ из ЕС, API и вердикт по трём миссиям","one_line":"Что на самом деле представляют собой always-on агенты Meta Muse, Instinct (Spear Street) и OpenAI Dots, доступны ли они из Лиссабона, есть ли программная дверь и заменяют ли они собственный флот Claude Code + MCP для найма, привлечения тестеров и фандрайзинга.","key_findings":["Ноги расходятся по качеству: glm заявил NOT FOUND по всем продуктам (в т.ч. arXiv 2606.03005), mistral дал детальные таблицы с нереальными URL-ами и противоречиями (модели и цены не подтверждены), grok привёл конкретные первоисточники. Опираться стоит на grok; данные mistral (Muse $29.99, Dots $49.99 «US/UK/JP», Instinct с REST API, утечка ключей в Wired, репо arxiv-muse) — вероятная фабрикация.","Meta Muse: агент запущен 08.09.2026 на модели Muse Spark (Spark 1.3 — в Muse Code и Meta Model API). У каждого пользователя своя облачная Secure VM с браузером и отдельным Sentinel (наружу ничего без разрешения, чувствительное спрашивает у пользователя), пароли и платёжные данные в хранилище, недоступном модели; оплата через Stripe Link с одноразовой картой.","Muse — цена и география: бесплатно с лимитом; Power $20/мес (500 млн токенов/нед), Maximum $100/мес (3 млрд/нед). Официально США, Канада, Мексика (сноска 24.09; пост от 29.09 называет только США и Канаду). Португалии/ЕС в списке нет, дата выхода в ЕС NOT FOUND; WhatsApp — канал для тех, у кого агент уже есть, а не обход гео. Публичного API/SDK/MCP у потребительского агента нет (есть только Meta Model API и Muse Code; «Muse API» упомянут как направление Enterprise Platform).","Instinct (Spear Street Technology, Noah Shinn): инвайт-онли (по интервью 28.09 — 5 инвайтов на пользователя, старт с ~200 человек), харнесс над сторонними LLM, собственной модели не названо. Прайса, списка стран и GDPR-адреса нет. Публичного API нет; ToS запрещают ботов, скрейпинг и использование для обучения чужих моделей. Обучение на данных включено по умолчанию (отключение действует только вперёд), отвязка сервиса не удаляет индекс, сделки агента обязывают пользователя как собственные. Open-instinct Марии Горских — клон, не сам продукт.","OpenAI Dots (анонс 29.09.2026): харнесс на GPT-6 Astra с собственным облачным компьютером; больше 4000 приложений через плагины; первый dot входит в Pro и Business Premium без доплаты. Pro-раскатка исключает EEA, Швейцарию и UK (личный Pro из Лиссабона не получит), Business Premium — все регионы ChatGPT, включая Португалию (на живом аккаунте не проверено). Business Premium $125/место/мес ($100 при годовой оплате), минимум 2 места. Отдельного API у Dots нет — Astra продаётся через API как модель.","Wajo (Shivani Poddar, бывший Google DeepMind) — четвёртый игрок, ближе к Instinct: агент Fo с собственным ящиком, номером, голосом и картой, звонки, привлечение живых ассистентов; запуск 25.08.2026. По TechCrunch 06.10 Khosla ставит его выше Muse/Instinct, 107 стран (слова компании, не проверено). Цена, модель, API/MCP не найдены; собственный график Wajo про Muse/Instinct — оценка «на глаз», не замер. Одна нога (glm) ошибочно утверждала, что Wajo не идентифицируется.","arXiv 2606.03005 «MUSE: A Unified Agentic Harness for MLLMs» (Jianglin Lu и др., Northeastern, 02.06.2026) — не Meta: харнесс вокруг замороженной MLLM (структурный разбор, детерминированная проверка, починка по вердикту проверяющего, OCR). Код — github.com/Jianglin954/MUSE (MIT), воспроизведена лишь часть (VSP level 3, CoMT, BLINK; без сохранённых результатов и Word Search). Заявлены: VSP-Grid GPT-4o 0.43→0.61, Opus 4.7 0.75→0.92; CoMT (200 задач) GPT-4o 101→175. Полезна как идея внешнего верификатора, не как агент. Утверждение glm, что статьи нет, опровергнуто.","Где они сильнее флота: чужие сайты без API (облачный браузер), одноразовые карты/платежи, постоянная работа между сессиями, звонки и торг без API (Instinct, Wajo; у Muse торг только через браузер). Флот сильнее по CRM, скиллам, шине, ночным рутинам, векторному поиску по волту, правилам и подписи автора. Все три просят OAuth и право действовать, а исходящее уходит от чужого агента.","Вердикт по трём миссиям (найм в лабу, тестеры к OSS, фандрайзинг): ни один продукт не заменяет текущий контур; единственная закрываемая ими дыра — звонок/торг без API, которая для этих миссий не критична. Почту с офферами, инвесторов, кандидатов и репозитории отдавать нельзя."],"recommendations":["Не покупать Muse и не обходить гео VPN/американской картой: гео США/Канада/Мексика, риск для действующих подписок при нулевой выгоде.","Не покупать инвайт Instinct; если слот предложат бесплатно — сначала выключить обучение, не подключать рабочие ящики, Vault оставить пустым.","Единственный легальный тест из Лиссабона: ChatGPT Business Premium (два места, ~$200/мес при годовой оплате или ~$250 помесячно), один пустой проект на 7 дней без CRM, вакансий и инвесторов.","Из arXiv MUSE взять только петлю «проверяющий → починка», сначала самому открыть репозиторий и убедиться, что код жив и полон.","Wajo пока только читать; карту и данные не отдавать до публикации цены и DPA.","Отказаться от рекомендаций mistral-ноги (инвайт через Discord, waitlist-ссылки, интеграция arxiv-muse/muse-harness, Dots для рассылки тестерам) — URL-ы и факты не подтверждены.","Поставить алерт на новости по Muse/Dots/Instinct/Wajo и повторить исследование при выходе в ЕС или появлении API."],"entities":{"people":["Noah Shinn","Shivani Poddar","Maria Gorskikh","Jianglin Lu","Vinod Khosla"],"companies":["Meta","OpenAI","Spear Street Technology","Wajo","Northeastern University","Stripe","Google DeepMind"],"products_tools":["Meta Muse","Muse Spark","Muse Code","Meta Model API","Instinct","open-instinct","OpenAI Dots","GPT-6 Astra","ChatGPT Pro","ChatGPT Business Premium","Wajo Fo","arXiv MUSE harness","Claude Code","MCP","Muse-Chat-MCP","Stripe Link"]},"open_questions":["Дата выхода Muse в ЕС/Португалии и точный официальный список стран (формулировки 8.09, 24.09, 29.09 расходятся).","Реально ли кнопка Dots появляется на живом португальском аккаунте Business Premium (проверено только по тексту справки).","Модель под капотом Instinct, его цена, список стран, место хранения данных/GDPR и состав коннекторов.","Требует ли бесплатный Muse карту до первого использования (только пресса) и вышел ли обещанный Confidential VM к 08.10.","Принимает ли Meta Model API португальский IP.","Живость и полнота репозитория Jianglin954/MUSE (страницу не открывали).","Цена, модель, API и DPA у Wajo; достоверность «107 стран» и десятикратного роста.","Не получены ноги ChatGPT и Gemini (на диске 3 из 5); часть утверждений grok-ноги обрезана и не подтверждена вторым заходом."],"related_concepts":["always-on personal agents","агентный харнесс vs модель","гео-ограничения и доступ из ЕС","программная дверь (API/MCP) для агентов","передача OAuth-доступа и обучение на данных","verifier-guided repair","рельсы и оркестрация флота Claude Code + MCP","Deep Research кворум и достоверность вендорских ног"]}
