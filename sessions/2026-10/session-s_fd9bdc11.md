---
session: s_fd9bdc11
date: 2026-10-19
words: 7763
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-19 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fd9bdc11` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-18-HUB-03-0602
REGISTRY TOPIC: Криптаны ушли в AI: люди, компании, деньги + куда крипто-VC инвестируют в AI и почему (двери найма для оператора) (веер: Chrome хаба завис (CDP 45s), заказ пирам peer_help #DR26-10-18-HUB-03-0602) (втащен в очередь dr_start --adopt; ПОТРЕБИТЕЛЬ: Карта работодателей для оператора через криптобэкграунд) (Проверенный ограниченный срез сохранен: Claude 65883 bytes и Mistral 108193 bytes attach PASS, strict gate PASS; очередь collecting 2/6, кворум 4/6 НЕ достигнут. HTML D:/Vault/_Dashboards/Crypto-AI-20261018.html. ChatGPT web еще working; GLM5.3 capacity, Gemini unsupported country, Grok Heavy paywall. Самые практичные двери Prime Intellect, Ema, OpenRouter; Sam Blackshear->Anthropic найден независимо. Полный done не заявлен.) (dr_reconcile 2026-10-19: на диске 3/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-18-HUB-03-0602\results)

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


===== VENDOR: report (insight-DR26-10-18-HUB-03-crypto-ai.md) =====
---
type: research
stage: distilled
date: 2026-10-18
status: preliminary
dr_id: DR26-10-18-HUB-03-0602
related:
  - "[[2026-10-16--poisk-vakansiy-v-kompaniyah-llm-bezopasnosti-zaschita-ot-distillyacii]]"
---

# Крипто → AI: карта людей, капитала и входов для оператора

Machine: HUB-01 (Хаб) · Agent: Codex · Operator: dev · 2026-10-18

Исследование: DR26-10-18-HUB-03-0602. Дубль DR26-10-18-HUB-07-1033 припаркован. Статус этого документа: проверенный срез, не завершенный консенсус 4/6. Исследовательский материал подготовлен Claude.ai и Mistral; Codex собрал, проверил отдельные первичные источники и внес ограничения ниже. Рельса: браузерные подписки; платные API не использованы.

## Вывод для решения

Начать с Prime Intellect и OpenRouter как конкретных бизнесов, где криптобэкграунд руководителей соединяется с продаваемой AI-инфраструктурой. Отдельно рассматривать Ritual, Catena и компании из портфелей криптофондов. Общее прошлое дает повод для предметного знакомства; доказанного личного знакомства или warm intro эта карта не устанавливает.

История про VitaDAO соответствует Vincent Weisser: VitaDAO называет его founding steward, а профессиональная страница AI Engineer связывает с Prime Intellect. Вторая компания и сам выпуск подкаста пока UNKNOWN. Не утверждаем, что найден именно прослушанный эпизод.

Источники: [VitaDAO](https://www.vitadao.com/blog/vitadao-letter-the-first-dao-with-a-biotech-spinoff), [Vincent Weisser, AI Engineer](https://ai.engineer/speakers/vincent-weisser).

## Перепроверено по первичным источникам

| Объект | Факт | Ограничение | Источник |
|---|---|---|---|
| Prime Intellect | Объявлен $130M Series A 08.07.2026; суммарное финансирование свыше $150M | Не складывать $130M и >$150M; второе уже включает раунд | [Объявление компании](https://www.primeintellect.ai/blog/series-a) |
| Prime Intellect | Компания сообщает >$100M annualized revenue и >6 тыс. клиентов | Темп выручки со слов компании, не аудированная годовая выручка, не прибыль и не доказанный SaaS ARR | [Компания](https://www.primeintellect.ai/blog/series-a) |
| Prime Intellect | Careers перечисляет 35 вакансий; есть Solutions Architect, Technical Partnerships, Production Engineering и Open Application | Наличие карточки не доказывает соответствие кандидата или приглашение | [Careers](https://www.primeintellect.ai/careers) |
| Prime Intellect | Forward Deployed AI Strategy Lead: стратегические клиенты, evals, post-training, внедрение, коммерческий результат | Карточка доступна отдельно; список вакансий может обновляться с иной скоростью | [Конкретная роль](https://www.primeintellect.ai/careers/s_80fd5982) |
| OpenRouter / Stripe | 19.08.2026 опубликовано соглашение о приобретении; OpenRouter остается модельным шлюзом | В объявлении сказано customary closing conditions; финальное закрытие и цена первичным источником здесь не подтверждены | [Stripe](https://stripe.com/newsroom/news/stripe-agrees-to-acquire-openrouter), [OpenRouter](https://openrouter.ai/blog/announcements/openrouter-is-joining-stripe/) |
| Hyperbolic | $12M раунд led by Variant и Polychain, общий объем $20M, 10.12.2024 | Историческое объявление, не свежий баланс; нельзя складывать $12M и $20M | [Компания](https://www.hyperbolic.xyz/blog/hyperbolic-secures-20m-total-funding-with-latest-series-a) |
| Catena | Компания объявила $18M led by a16z crypto | Подтвержден seed; более свежие раунды из сырого отчета отдельно не приняты | [Пост компании](https://www.linkedin.com/posts/catenalabs_catena-labs-secures-18m-to-build-first-ai-native-activity-7330563695988703233-8P99) |
| Ritual | Archetype опубликовал инвестиционную записку и описал команду/AI-инфраструктуру | Записка 2023 года доказывает происхождение и тезис, не текущее финансовое состояние | [Archetype](https://www.archetype.fund/media/announcing-our-investment-in-ritual) |
| Pluralis | USV объясняет инвестиционную гипотезу открытого распределенного обучения | Инвестиционная гипотеза не доказательство коммерческой окупаемости | [USV](https://www.usv.com/writing/pluralis-towards-actually-open-ai) |
| Pluralis | USV и CoinFund co-led $7.6M seed, 19.03.2025; участвовал Variant | Величина всего раунда, не чек одного фонда; историческое финансирование, не текущая выручка | [USV](https://www.usv.com/writing/pluralis-towards-actually-open-ai) |
| Venice | Компания объявила $65M Series A led by Dragonfly при $1B valuation, 01.07.2026; среди участников Coinbase Ventures | Компания одновременно описывает VVV token economy; нельзя классифицировать как no-token. Прибыль в первичном объявлении не раскрыта | [Компания](https://venice.ai/blog/venice-raises-65-million-series-a) |

## Люди: кого считать переходом, а кого соседством

| Человек | Криптоконтекст → AI | Как использовать | Статус |
|---|---|---|---|
| Vincent Weisser | VitaDAO → Prime Intellect | DeSci, распределенные системы, RL/agents; первый работодатель для проверки | Криптороль подтверждена VitaDAO; AI роль указана AI Engineer |
| Alex Atallah | OpenSea → OpenRouter | Инфраструктура моделей, маршрутизация, надежность, стоимость и взаимодействие с разработчиками | Кандидат из внешнего отчета; текущий CEO подтвержден Stripe |
| Erik Voorhees | ShapeShift → Venice | Приватность AI, инфраструктура и эксплуатация | Внешний отчет; финансовые цифры требуют отдельного разбора |
| Niraj Pant | Polychain → Ritual | Переход от инвестирования к проверяемому AI execution | Инвестиционная записка Archetype |
| Akilesh Potti | Polychain → Ritual | ML systems и верификация | Инвестиционная записка Archetype |
| Sean Neville | Circle → Catena | Финансовая инфраструктура AI-агентов, риски, операционная деятельность | Переход указан внешним отчетом; финансирование подтверждено компанией |
| Sandeep Nailwal | Polygon → Sentient | AI open source, ecosystem, партнерства | Параллельная деятельность, не доказанный уход из крипты |
| Illia Polosukhin | NEAR / NEAR AI | Confidential inference и пользовательские AI-сервисы | AI→crypto→AI/параллельный путь; не простой crypto→AI |
| Val Vavilov | Bitfury → инвестиции в Gonka и новые технологии | Капитал и инфраструктурная сеть | Инвестор/оператор, не доказанный переход на работу в AI-лабу |
| Ben Fielding | Gensyn | Распределенное обучение и проверка работы | Строитель AI×crypto; отдельная прежняя криптокарьера в сыром отчете не показана |
| Karan Malhotra, Roux Quesnelle, Teknium, Shivani Mitra | Nous / Psyche | Open models, agents, обучение | Нельзя автоматически считать мигрантами: криптопрошлое в нескольких строках не подтверждено |
| Holt Long | Pluralis | Распределенные ML-системы | AI-исследователь с криптоинвесторами, не подтвержденный мигрант |
| Jasper Zhang, Yuchen Jin | Hyperbolic | GPU marketplace и inference | AI×crypto; прежняя криптороль второго не подтверждена |
| Kevin Weil | Libra/Novi → OpenAI | Историческая траектория для понимания рынка | Внешний отчет сообщает уход из OpenAI в 2026; не считать текущим внутренним контактом |
| Sam Altman | OpenAI и Worldcoin | Пересечение двух сфер | Не пример последовательного перехода из крипты в AI |
| Sam Blackshear | Move / Meta Diem / Mysten Labs → Anthropic defensive security | Прямой пример технического перехода в frontier lab | Mistral нашел сообщение от 05.08.2026; независимо подтверждено публикациями CryptoBriefing и Crypto.news, которые цитируют его заявление |
| Surojit Chatterjee | Coinbase CPO → Ema founder/CEO | Enterprise agents, продукт и внедрение; сильный дополнительный кандидат | Обе роли прямо подтверждены [биографией компании Ema](https://www.ema.ai/about-us), прежняя также Coinbase |
| Jason Zhao | Story Protocol → Poseidon | Данные и AI research | Новая связь Mistral, пока отчет прессы, не подтвержденный нами текущий работодатель |

Полная исходная таблица содержит 45 строк, включая инвесторов. Это 45 кандидатов/связей, а не 45 доказанных переходов.

## Фонды: где искать компании и профессиональные связи

Ниже карта из внешнего исследования. Она подходит для поиска портфельных компаний; это не инвестиционная рекомендация. Размер раунда компании не равен чеку фонда.

| Фонд | Выбранные компании/связи | Почему это полезно | Уровень проверки |
|---|---|---|---|
| Paradigm | Nous; EVMbench с OpenAI; расширение в AI/robotics | Партнеры и компании с общей криптосетью | $50M Nous / $1B token valuation в прессе; не обычная equity valuation |
| a16z crypto | Gensyn; Catena | AI compute и деньги для агентов | Catena $18M подтвержден компанией |
| CoinFund | Prime Intellect; Pluralis; Catena | Наиболее прямой мост криптокапитал → AI infrastructure | Исходный отчет; Pluralis также записка USV |
| Polychain | Ritual; Hyperbolic; Sahara | Распределенные вычисления и проверяемый AI | Hyperbolic подтвержден первичным объявлением |
| Variant | Hyperbolic; Pluralis; autonomy thesis | GPU-инфраструктура и автономные агенты | Hyperbolic подтвержден компанией; остальные связи из отчета |
| Archetype | Ritual | Криптография и верификация AI | Первичная инвестиционная записка |
| USV | Pluralis; Nous | Открытые модели и распределенное обучение | Записка USV о Pluralis |
| Pantera | Sentient; Sahara; Surf | AI для крипторынка и открытого интеллекта | Внешний отчет, выборочная проверка не завершена |
| Framework | Sentient; Mecka AI; USD.AI | AI/robotics/data и финансовый слой | Внешний отчет, требует проверки сделок |
| Dragonfly | Venice; Sapiom; MyShell | Inference и расходы AI-агентов | Внешний отчет, текущие суммы не приняты без первичных документов |
| Coinbase Ventures | Catena; Venice; Surf; Sapiom; Skyfire/Payman | Agent commerce и инфраструктура | Внешний отчет; не смешивать портфель Coinbase с продуктами самой Coinbase |
| Hack VC | Grass; Sentient; 375ai | Данные для моделей и сети инфраструктуры | Внешний отчет |
| Delphi | Nous; Sentient; Inference Labs и др. | Протоколы и AI | Часть связей только агрегаторы, повышенная неопределенность |
| 1kx | Olas | Экосистема автономных агентов | Внешний отчет |
| Robot Ventures | Nous; Ritual; Sentient | Портфельный поиск | Внешний отчет, суммы/инструменты требуют сверки |
| Haun Ventures | AI agents в расширенной стратегии | Пока маршрут к партнерам, а не доказанный список подходящих AI-компаний | Исходный отчет не назвал конкретные сделки |

Из этой карты нельзя выводить, что все криптофонды ушли в AI. Для Electric Capital, Placeholder, Galaxy Ventures, Jump, OKX, Animoca, Lemniscap, Blockchain Capital, Mechanism и ряда других полнота проверки недостаточна.

## Приоритеты трудоустройства

1. **Prime Intellect:** Forward Deployed AI Strategy Lead; затем Senior Technical Partnerships Manager, Solutions Architect, Open Application. Называемая роль и страница careers проверены. Подготовить один разбор реального agent-workflow с evals, trace, затратами и ограничениями; это предметнее общего знакомства «мы оба из крипты».
2. **OpenRouter:** solutions/deployment, model routing, operations; использовать опыт мультивендорных систем. Сделка со Stripe подтверждена как соглашение; текущие вакансии и завершение сделки проверить отдельно.
3. **Ritual:** systems/verification, технические партнерства; сильное пересечение с криптографией. Конкретная вакансия UNKNOWN.
4. **Catena:** agent commerce, технические операции, product/partnerships. Конкретная вакансия UNKNOWN.
5. **Nous:** agents и distributed training; хороший технический контекст, но не считать всю команду выходцами из крипты. Конкретная вакансия UNKNOWN.
6. **Hyperbolic / Pluralis / Gensyn:** инфраструктурная линия. Проверить стадию продукта, заказчиков и финансовый горизонт, а не ориентироваться на сумму токенов.
7. **Sentient / Venice / Gonka / Olas:** отдельный список AI×crypto. Должность, качество бизнеса и токенэкономику оценивать отдельно.

**Дополнение после независимой проверки: Ema поставить рядом с OpenRouter в верхнюю группу.** Это подтвержденный путь Coinbase → AI Employees для HR/IT/Finance. На [careers Ema](https://www.ema.ai/careers) доступны AI Resident UK/EMEA (remote), Software Engineer Full-Stack (US), Devops Engineer US, IT Engineer US remote и другие роли. Это наблюдение на момент проверки, не доказательство совместимости со всеми условиями кандидата. Для оператора наиболее близок рассказ о внедренных агентах, сложных интеграциях и измеримых бизнес-результатах. Выручка, прибыль и актуальный runway Ema в этом срезе UNKNOWN.

Не отправлять заявки или сообщения из этого отчета автоматически: исходный заказ относится к исследованию. Не выдавать тематическое родство за личную рекомендацию.

## Почему люди и деньги идут туда

Рабочие объяснения из внешнего исследования: перенос навыков распределенных систем, криптографии и incentive design; более крупный рынок AI; инфраструктурная нехватка compute; появление агентов, которым нужны платежи и лимиты; перенос капитала и деловых сетей. У каждого объяснения есть альтернативы, поэтому это не доказательство особой «чуйки криптанов».

Проверяемый положительный пример: Prime Intellect продает стек compute/RL/evals/sandboxes клиентам и сообщает выручку. Hyperbolic объясняет спрос стоимостью и доступностью GPU. Catena прямо описывает ограничения человеческой финансовой инфраструктуры для AI-агентов. Отрицательные кейсы из отчета включают ElizaOS и конфликт Covenant/Bittensor; они требуют первичных историй и не позволяют объявить весь класс неработающим.

## Исправления к исходному отчету и слепые зоны

- **Независимый Mistral добавил 55 строк людей и 24 строки фондов. Это второй список кандидатов, не еще 55 уникальных переходов.** Значительная часть пересекается с Claude.
- **Существенное расхождение разрешено первичным источником:** Claude не подтвердил 61% мирового VC в AI за 2025 год; Mistral нашел OECD. OECD действительно публикует 61%, $258.7B из $427.1B, на данных Preqin. Источник: [OECD, 17.02.2026](https://www.oecd.org/en/publications/venture-capital-investments-in-artificial-intelligence-through-2025_a13752f5-en/full-report.html). Нельзя переносить этот процент на иную выборку Crunchbase/PitchBook.
- **Существенное расширение карты:** Claude сделал слишком широкий вывод о слабом присутствии криптолюдей в frontier labs. Mistral нашел Sam Blackshear → Anthropic. Два независимых сообщения цитируют его собственное заявление: [CryptoBriefing](https://cryptobriefing.com/mysten-labs-co-founder-sam-blackshear-joins-anthropic-to-focus-on-defensive-security-research/), [Crypto.news](https://crypto.news/mysten-labs-cto-sam-blackshear-joins-anthropic/). Это опровергает практическую установку искать только криптооснованные стартапы.
- **Ошибка Mistral не принята:** Venice в одной строке фондов назван pure AI/no token, хотя оба отчета описывают VVV. Наличие equity-раунда не отменяет токен. Обобщение «победители только без токенов» слишком сильное.
- Падение числа криптокоммитов на 75%, фигурирующее у Mistral, само по себе не доказывает, куда ушли конкретные разработчики. Без отслеживания людей это корреляция, а не измеренная миграция в AI.
- «45 crypto→AI migrants» завышает доказанную популяцию: туда включены инвесторы, люди без подтвержденной криптороли и параллельные проекты.
- Prime Intellect: >$100M annualized revenue нельзя переименовывать в аудированную выручку за год, чистую прибыль или гарантированный recurring ARR.
- OpenRouter: соглашение о приобретении не доказывает финальное закрытие сделки. Цена в первичных объявлениях не раскрыта; медийные $7–8B+ не принимаются как точная цена.
- Nous: сообщаемая token valuation не является автоматически оценкой обыкновенного equity. SAFT/токенные права нельзя писать в чистый equity-столбец без условий раунда.
- Историческое финансирование не доказывает cash runway. Долг/прибыль большинства частных компаний UNKNOWN.
- Наличие AI в портфеле не доказывает, что фонд полностью сменил мандат; отсутствие найденной сделки не доказывает нулевой портфель.
- Проверены отдельные первичные источники, не все 150 URL исходного отчета. Заявленные 348 sources в интерфейсе не равны 348 независимо проверенным источникам.
- Кворум 4/6 пока не достигнут: два полных файла прикреплены (Claude и Mistral), оба прошли dr_leg_gate --strict; ChatGPT работает. GLM-5.3 ответил capacity, Gemini сообщил unsupported country, Grok Heavy требует SuperGrok. Это не причины для скрытого перехода на Flash/Fast.

## Корпус и воспроизводимая проверка

[Claude, исходный чат](https://claude.ai/chat/s_f0191bd0). [ChatGPT, продолжающийся анализ](https://chatgpt.com/c/s_c18e8369). [Mistral](https://chat.mistral.ai/work/s_e260c815).

`python C:\Users\dev\.claude\scripts\dr_queue.py status DR26-10-18-HUB-03-0602` показывает фактически прикрепленные результаты. Пока отчет нельзя объявлять итогом независимых четырех вендоров.


Дашборд: D:\Vault\_Dashboards\Crypto-AI-20261018.html


===== VENDOR: grok (DR26-10-18-HUB-03-0602-dr-grok.md) =====
Ищу первичные источники по связке VitaDAO и RL, затем по переходам людей, раундам и фондам.A. Краткий вывод для решения потребует свежих первичных страниц. Сначала открываю источники по VitaDAO, RL-компаниям, фондам и деньгам.A. Краткий вывод для решения

На 18 октября 2026 года единственная подтвержденная цепочка «DeSci/VitaDAO, затем RL-компания» ведет к Vincent Weisser и Prime Intellect. Вторая RL-компания и выпуск подкаста, где обе компании названы вместе, не опознаны. Подгонять пару не стал.

Для опытного операционного руководителя и программиста из крипты рабочая дверь сейчас одна: Prime Intellect, Сан-Франциско, платный стек compute, RL, environments, sandboxes, evals и deployment. Компания 8 июля 2026 пишет о найме и о более чем $100 млн годового темпа выручки. Это слова компании, не отчетность. Оценка $1 млрд есть у TechCrunch и отсутствует в посте компании.

Вторая живая дверь: Venice Эрика Вурхиса. Это потребительский и API-продукт приватного AI плюс токен VVV. Equity и токен нельзя складывать. Третья, узкая: Anthropic, куда в августе 2026 ушел операционный CTO Mysten Сэм Блэкшир. Это security research, не кресло COO, и знакомство с ним не доказано.

Крупные криптофонды в 2026 году пишут, что остаются в крипте и добавляют AI. Чек фонда не равен бизнесу: Yupp закрылся 31 марта 2026 после seed $33 млн от a16z crypto.

Подтверждены 3 человека с крипторолью и последующей AI-ролью, 4 компании с открытым продуктом или сделкой, 7 криптофондов с открытым текстом тезиса или сделки, 4 размерные сделки этих фондов. Из 28 денежных полей таблицы 19 неизвестны, доля 68%.

Простыми словами. Искать работу логично через Prime Intellect: человек из той же DeSci-среды уже строит там платформу, на которой компании учат своих агентов. Venice подходит, если нужен приватный AI и криптоаудитория. В большую лабораторию криптобэкграунд сам по себе дверь не открывает. Теплое интро никто не обещает.

B. Опознание истории VitaDAO

Искомое: подкаст, две компании reinforcement learning, один основатель раньше связан с VitaDAO, longevity/DeSci, на слух «Витадава».

Что подтверждено, и чем.

1. Vincent Weisser. Биография конференции AI Engineer: учился в CODE University of Applied Sciences, сооснователь dex.blue, помогал строить DeSci вокруг VitaDAO, включая Fast Grants Fellowship и Longevity Prize, затем вместе с Johannes Hagemann основал Prime Intellect. https://ai.engineer/speakers/vincent-weisser

2. Прежняя операционная роль, не только «помогал DAO». The Block, 23 апреля 2024: Weisser ранее был Chief of Ecosystem and AI в Molecule, платформе токенизации и финансирования IP для биотеха. Второй сооснователь, Hagemann, два года до этого строил большие языковые модели в немецкой AI-компании Aleph Alpha. https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476

3. Компания. Wikipedia, страница просмотрена 18 октября 2026: Prime Intellect, Inc., основана в январе 2024, штаб в Сан-Франциско, CEO Vincent Weisser, немецкий DeSci-предприниматель, CTO Johannes Hagemann, ранее ML-инженер Aleph Alpha. Продукты: Compute Exchange, PRIME, PRIME-RL, prime CLI/SDK, Prime Agent, модели INTELLECT. https://en.wikipedia.org/wiki/Prime_Intellect

4. Это RL-компания, не только «децентрализованный тренинг». Пост компании о раунде $15 млн, февраль 2025: compute marketplace, INTELLECT-1 на 10 млрд параметров через три континента, INTELLECT-MATH на RL, GENESYS и SYNTHETIC-1 как распределенный RL и синтетические рассуждения, TOPLOC для проверяемого inference. https://www.primeintellect.ai/blog/fundraise
Пост Series A, 8 июля 2026: тезис компании в том, что RL позволяет заказчику владеть циклом оптимизации модели. Стек: compute, large-scale RL, environments, sandboxes, evals, deployment. https://www.primeintellect.ai/blog/series-a
AI Engineer добавляет даты моделей: INTELLECT-1 в ноябре 2024, INTELLECT-2 в мае 2025 как асинхронный RL, INTELLECT-3 как MoE 106 млрд параметров при 12 млрд активных, Environments Hub с наградами и критериями оценки, Lab как связка eval, RL, deployment и inference. https://ai.engineer/speakers/vincent-weisser

Уверенность, что Weisser и есть человек из подсказки: высокая. Совпадают VitaDAO, longevity/DeSci, Molecule и действующая RL-компания.

Что не подтверждено.

Вторая RL-компания. Hagemann это второй человек в той же компании, не вторая компания. Открытые страницы дают ему Aleph Alpha, не VitaDAO. Утверждение, что он был советником VitaDAO, в этом проходе первичным источником не подтверждено. Его личный сайт в этом проходе не открывался.

Выпуск, где рядом стоят две разные RL-компании. Поиск 18 октября 2026 показал интервью Вайссера, полные страницы выпусков не открывались, цитат из них нет:

https://www.cognitiverevolution.ai/distributed-training-decentralized-ai-prime-intellects-master-plan-to-make-ai-too-cheap-to-meter/
https://www.podpage.com/the-index-podcast/building-training-open-ai-intelligence-prime-intellect-co-founder-vincent-weisser/
https://www.listennotes.com/podcasts/the-generalist/why-one-superintelligence-is-eXYEzuPOshk/
https://podcasts.apple.com/us/podcast/vincent-weisser-and-era-qian-building-toward-open/id6813642428?i=id_1d7d0e23

Сниппеты описывают Prime Intellect, распределенный тренинг и RL. Второй отдельной RL-компании в них нет. Mechanize в том же поиске всплыла как работодатель RL-environments, страница не открыта, связи с VitaDAO нет. В кандидаты второй компании она не ставится.

Итог опознания: человек и первая компания найдены. Пара компаний и выпуск не найдены.

C. Люди и компании

Проверка таблиц: 18 октября 2026. Квота 30–50 человек не набрана. Ниже только те, у кого роль подтверждена открытой в этом проходе страницей. Остальные имена в выборку не включены.

| Человек | Класс | Криптороль и дата | AI-роль и дата | Продукт и применение | Команда, география, стадия | Найм и публичный канал | Источник |
|---|---|---|---|---|---|---|---|
| Vincent Weisser | Полный операционный переход в AI-компанию. В 2024 компания еще описывала будущий протокол собственности на совместно обученные модели. В открытых текстах 2026 токен не является продуктом. | Сооснователь dex.blue, дата не указана. Помогал VitaDAO: Fast Grants Fellowship, Longevity Prize. До апреля 2024: Chief of Ecosystem and AI, Molecule. | Сооснователь и CEO Prime Intellect с января 2024. | Платный стек: биржа GPU, RL и post-training, environments, sandboxes, evals, inference. Кейс Ramp: модель 35 млрд для поиска по таблицам, быстрее и дешевле закрытой модели. Компания пишет о более чем 6 тыс. клиентов. | Сан-Франциско. Частная компания после Series A. Размер команды страница не дает, пост называет ее маленькой. | Пост 8 июля 2026: нанимают в RL, inference, distributed systems, compute. Ссылка на доску есть, список вакансий в этом проходе не разобран. Канал компании: https://x.com/primeintellect и https://discord.gg/primeintellect | https://ai.engineer/speakers/vincent-weisser https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476 https://en.wikipedia.org/wiki/Prime_Intellect https://www.primeintellect.ai/blog/series-a https://www.primeintellect.ai/blog/fundraise |
| Erik Voorhees | Переход оператора в AI-продукт при сохранении токена. Это не выход из криптоэкономики. | Криптопредприниматель, в материале The Block связан с ShapeShift. В апреле 2024 назван инвестором Prime Intellect как Erik Voorhees of Shapeshift. | Основатель Venice. The Block 1 июля 2026 пишет, что продукт запущен более двух лет назад. Схема сайта ставит дату основания 2024. | Приватный чат, картинки, видео, аудио, код и API для агентов. Цены на сайте: Pro $18, Pro+ $68, Max $200 в месяц. Компания через The Block: 3 млн пользователей в апреле, прибыль в Q1, чужая оценка ARR выше $70 млн. | Юридический адрес в схеме сайта: [АДРЕС], Ste 14343, Sheridan, [АДРЕС]. Это адрес организации, не домашний адрес. Размер команды неизвестен. Стадия: Series A. | Ссылка Careers видна на главной. Страница вакансий не открыта, открытые роли неизвестны. Публичные каналы: [EMAIL], https://x.com/AskVenice/, https://discord.gg/askvenice, https://venice.ai/careers | https://www.theblock.co/news/deals/2026-07-01-venice-ai-funding-equity-valuation-dragonfly-406934 https://venice.ai/ https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476 |
| Sam Blackshear | Частичный переход. Операционную роль в криптокомпании оставил, советником остался. | Создатель языка Move для Libra/Diem в Meta. Сооснователь и CTO Mysten Labs с 2021, архитектура Sui и вклад в Walrus. | 5 августа 2026 объявил уход из операционной роли Mysten в defensive security research в Anthropic. Должность, дата выхода и линия подчинения в статье не названы. | Anthropic делает Claude. Конкретный продукт Блэкшира внутри лаборатории не описан. | Mysten остается криптокомпанией, техническое направление после него ведет CEO Evan Cheng. География новой работы неизвестна. У Anthropic большинство сотрудников в Bay Area, это политика компании, не факт про него. | Доска Anthropic жива: https://www.anthropic.com/careers и https://www.anthropic.com/careers/jobs. Рекрутеры только с адресов @anthropic.com. Интро через Блэкшира не следует из источников. | https://cryptobriefing.com/mysten-labs-co-founder-sam-blackshear-joins-anthropic-to-focus-on-defensive-security-research/ https://www.anthropic.com/careers |

Рядом, но не переход криптанина в AI.

Johannes Hagemann, CTO Prime Intellect. Предыдущий работодатель Aleph Alpha, AI-лаборатория. В подтвержденную криптовыборку не входит. https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476 https://en.wikipedia.org/wiki/Prime_Intellect

Pankaj Gupta и Gilad Mishne, сооснователи Yupp. TechCrunch подтверждает компанию и закрытие. Прежнюю криптороль открытая статья не дает. В люди «из крипты» не записаны. https://techcrunch.com/2026/03/31/yupp-ai-shuts-down-33m-a16z-crypto-chris-dixon/

Полезных для трудоустройства из подтвержденных людей: Weisser как узел входа в Prime Intellect, Voorhees как узел входа в Venice, Blackshear как доказательство узкой двери в security Anthropic. Пятнадцати отдельных полезных людей с открытыми источниками нет.

Что компании продают.

Prime Intellect продает инфраструктуру, чтобы компания сама крутила цикл улучшения модели, а не только арендовала закрытую модель. Покупатель: AI-стартапы, «neolabs» и предприятия. Именные клиенты у TechCrunch: Ramp, Zapier, Flapping Airplanes. Зачем покупателю: свой workflow, свои данные, скорость и цена на узкой задаче. Пример Ramp приведен сооснователем Ramp Каримом Атийе. Ров, словами партнера Radical Дэвида Каца: собрали куски лаборатории в один доступный стек. Это слова инвестора. Независимый аудит клиентской базы и выручки не открыт.

Разложение RL у Prime Intellect:

- Environments. Environments Hub: среды задач, критерии оценки и сигналы награды. Источник биографии AI Engineer.
- Verifiers. TOPLOC, февраль 2025: схема для проверяемого inference. Отдельная линейка verifiers в 2026 названа Wikipedia со ссылкой на материалы компании.
- Reward и данные. GENESYS и SYNTHETIC-1: синтетические рассуждения из распределенного RL.
- Post-training. Series A описывает large-scale RL и post-training. Lab связывает оценку, обучение, выкладку и inference. INTELLECT-3, по Wikipedia, обучен через SFT и крупный RL.
- Evaluation. Стек Series A включает evals. В феврале 2025 компания писала, что запускает hosted evaluations.
- Agent training. Series A говорит об agentic training, Recursive Language Models и continual learning. Wikipedia описывает Prime Agent как открытый harness, форк pi-mono, с постоянным IPython-ядром.
- Compute. Compute Exchange агрегирует GPU облаков и дата-центров. Series A говорит о расширении кластеров.

Класс бизнеса Prime Intellect на 2026 год: чистый AI-стек, который продается за деньги. Блокчейн для текущего счета клиенту открытыми страницами не показан как необходимое условие. Ранний план протокола с криптоэкономикой, апрель 2024, в продуктах июля 2026 не подтвержден как запущенный. Статус того плана: неизвестен.

Venice продает приватный доступ к чужим и своим моделям: чат, медиа, код и OpenAI-совместимый API для агентов. Покупатель: потребитель и разработчик агентов. Зачем: не хранить промпты и ослабить модерацию. На сайте четыре уровня: анонимизация чужих моделей, нулевое хранение на своих открытых моделях, TEE, сквозное шифрование. Ров в открытых страницах: эта архитектура плюс уже платящая аудитория. Альтернатива, которую страницы не закрывают: confidential computing у обычных облаков.

Класс Venice: сам inference может работать без блокчейна. Токен при этом не выглядит чистым маркетингом. The Block передает слова Вурхиса: казначейские VVV не продавались, инвесторы получили грант 1,5 млн VVV и варранты на 5 млн, DIEM дает не сгорающий API-кредит на $1, часть выручки идет на выкуп и сжигание VVV. Это экономическая надстройка над рабочим AI-продуктом. Необходимости блокчейна для чата страницы не доказывают.

Yupp продавал краудсорсное сравнение около 800 моделей и хотел продавать предпочтения лабораториям. Были 1,3 млн пользователей и несколько лабораторий-клиентов. Основатели сказали, что product-market fit не случился: лаборатории платят узким экспертам внутри RL, а не массовой потребительской оценке. Закрытие 31 марта 2026. Токен в открытой статье не фигурирует. Класс: чистый AI-продукт оценки, деньги пришли от криптофонда, бизнес не выжил. Пользователи не стали выручкой в тексте статьи.

Mecka AI известна только как компания, чей Series A на $60 млн возглавил Framework. Продукт, клиенты и ров в открытой статье не описаны. Для трудоустройства не рекомендуется, пока нет страницы продукта.

Nous Research назван Paradigm как пример «keeping AI open», создатели Hermes Agent. Раунд, выручка и криптобэкграунд основателей в открытом посте фонда не даны. В деньги и в работодатели не ставится.

Anthropic продает Claude. Для этого исследования это работодатель назначения Блэкшира, не криптокомпания.

D. Деньги

Проверка: 18 октября 2026. Раунды показаны по отдельности. Фраза компании «всего больше $150 млн» совпадает с суммой трех раундов 5,5 + 15 + 130 = 150,5 и четвертым раундом не считается. AUM, TVL, FDV и объем торгов в таблицу не входят.

| Компания | Equity / convertible | Token sale | Grants | Долг | Оценка | Выручка / ARR | Прибыль |
|---|---|---|---|---|---|---|---|
| Prime Intellect | Seed $5,5 млн, 23 апреля 2024, co-lead CoinFund и Distributed Global. Участники по The Block: Compound, Collab+Currency, Protocol Labs, Erik Voorhees, Worldcoin DCBuilder, «Coinbase's Joe Lallouz» в формулировке статьи, Clem Delangue, Dylan Patel, Shivani Mitra из Nous. Затем $15 млн, февраль 2025, lead Founders Fund, участники Menlo Ventures, Teague, Delangue, Patel, Tri Dao, Emad Mostaque, Jake Medwell. Затем Series A $130 млн, 8 июля 2026, lead Radical Ventures, участники по посту компании: NVIDIA Ventures, Intel Capital, Dell Technologies Capital и прежние инвесторы. Надежность сумм seed: оценка СМИ по заявлению раунда. $15 млн и $130 млн: слова компании. | Неизвестен. В апреле 2024 фирма планировала протокол. В открытых постах 2025–2026 завершенной продажи токена нет. | Неизвестны | Неизвестен | $1 млрд на Series A пишет TechCrunch 8 июля 2026. Пост компании оценку не называет. Надежность: оценка СМИ. Отчетности нет. | Больше $100 млн annualized менее чем за год, слова компании 8 июля 2026. TechCrunch в тот же день пишет run-rate $100 млн. Не аудит. | Неизвестна |
| Venice | Series A $65 млн, 1 июля 2026, первая внешняя equity-продажа. Lead Dragonfly. Участники: North Island Ventures, Coinbase Ventures, F-Prime, Archetype, Liquid2 Ventures, Morgan Creek. За $65 млн инвесторы получили 8,98% equity. Надежность: слова основателя через The Block. | Казначейские VVV не продавались, слова Вурхиса. Одновременно выдан вестимый грант 1,5 млн VVV и варранты на 5 млн VVV на 8 лет. Исполнение варрантов стоило бы около $66,5 млн и довело бы привлеченное примерно до $131,5 млн. Это условие, не закрытая продажа. Лок 1 год, затем вестинг 3 года. Грант и варранты не прибавляются к equity как уже полученные деньги. | Исследовательские гранты неизвестны. Токеновый грант инвесторам стоит в соседней колонке, это не grant на исследования. | Неизвестен | $1 млрд equity, слова основателя через The Block. | The Block пишет «reportedly» ARR больше $70 млн и отсылает к TechCrunch. Сама статья TechCrunch про Venice в этом проходе не открыта. Надежность: оценка СМИ. | Компания сказала, что в Q1 стала прибыльной. Доллары прибыли неизвестны. Надежность качественного утверждения: слова компании через The Block. |
| Yupp, закрыта | Seed $33 млн в 2024, lead Chris Dixon, a16z crypto, плюс более 45 ангелов, среди них Jeff Dean, Biz Stone, Evan Sharp, Aravind Srinivas. Надежность: слова компании через TechCrunch. | Неизвестен, в статье нет | Неизвестны | Неизвестен | Неизвестна | Неизвестна. Названы пользователи и несколько лабораторий, долларов нет. | Неизвестна. Компания закрылась 31 марта 2026. |
| Mecka AI | Series A $60 млн, lead Framework. Точная дата закрытия неизвестна. К 26 июня 2026 фонд уже называет эту сделку начатой из нового фонда. Чек самого Framework неизвестен и в сумму раунда не подменяет ее. Надежность: слова фирмы через The Block. | Неизвестен | Неизвестны | Неизвестен | Неизвестна | Неизвестна | Неизвестна |

Конфликт по инвесторам Prime Series A. Пост компании не называет Iconiq. TechCrunch называет Iconiq и среди ангелов Aravind Srinivas. Списки не склеены. https://www.primeintellect.ai/blog/series-a https://techcrunch.com/2026/07/08/prime-intellect-raises-130m-series-a-to-help-enterprises-build-their-own-ai-agents/

E. Фонды и сделки

Проверка: 18 октября 2026. Криптопроисхождение подтверждено открытой страницей. Чистый AI отделен от сделки, где блокчейн остается предметом фонда. Чек фонда внутри раунда почти везде неизвестен. В таблице сумма раунда и роль фонда разведены.

| Фонд и партнеры | Откуда криптопроисхождение | Сделка, дата, сумма всего раунда, роль | Что фонд говорит сам | Наша интерпретация, отдельно |
|---|---|---|---|---|
| Paradigm. Matt Huang, Alana Palmedo | Фонд с 2018, сначала крипта. Пост 8 июля 2026. | Четвертый фонд $1,2 млрд. Именные направления без сумм раундов: Nous Research / Hermes, Zipline, SendCutSend, True Anomaly, Hyperliquid, Tempo вместе со Stripe, Kalshi, Centaur, EVMbench. Размеры этих раундов в посте неизвестны. | «Сначала крипта, теперь еще AI, робототехника и другие фронтиры». Крипту не закрывают: Hyperliquid, Tempo, Kalshi остаются в тексте. | Это расширение мандата, не уход из крипты. Nous здесь единственное прямо названное AI-имя, и по нему нет ни суммы, ни доказательства, что основатели пришли из крипты. |
| Haun Ventures. Katie Haun | В том же эссе: независимый директор Coinbase в период появления нового класса активов. 4 мая 2026 объявлен $1 млрд новых фондов. | Именной AI-компании и суммы ее раунда в эссе нет. | Три зоны: новая финансовая инфраструктура шире криптоинструментов, новые активы и рынки, агентная экономика. Криптографические инструменты названы важными для агентов. Фразы «мы ушли из крипты» нет. | Агенты для Haun это заказчики финансовых услуг. Эссе не доказывает переход фонда в чистый AI. |
| a16z crypto. Chris Dixon, Ali Yahya, Guy Wuollet, Eddy Lazzarin | Собственный Crypto Fund 5, пост 5 мая 2026, $2,2 млрд. | Yupp, seed $33 млн, 2024, lead Dixon / a16z crypto. Компания закрыта 31 марта 2026. Другие AI-суммы Fund 5 в открытом посте не названы. | Тезис фонда: стейблкоины, ончейн-рынки, регулирование. AI объясняет, почему прозрачность и проверяемость криптосетей становятся ценнее. Агенты названы роем, который покупает compute, данные и услуги. | Фонд использует AI как аргумент в пользу крипты. Yupp показывает, что крупный seed в около-AI продукт может закончиться закрытием меньше чем за год после запуска. |
| Framework Ventures. Horvat Anderson, Vance Spencer. Rajiv Patel-O'Connor повышен до GP. Ryan Barney пришел из Pantera, Nick Trileski из DRW. | Основан в 2019 как блокчейн-фонд. Прежние фонды около $15 млн в 2019, $100 млн в 2021, $400 млн в 2022. Делал имя на Aave и Chainlink. | FVIV $400 млн, новость 26 июня 2026. Чеки $1–50 млн, от pre-seed до Series A, плюс ликвидные активы и часть публичных бумаг. Уже возглавили Series A Mecka AI на $60 млн и вложились в Daylight. Чек Framework в $60 млн неизвестен. Параллельно держат Hyperliquid, Sky, Plasma. | Anderson: блокчейн был контрарианской ставкой, теперь к нему добавлены AI, роботы, энергия, fintech. Spencer: следующие компании смешают AI, блокчейн-рельсы, роботов и энергию. | Самое ясное из открытых расширений в чистый или околочистый AI, но продукт Mecka неизвестен, а криптопортфель фонд не продал в тексте статьи. |
| CoinFund | Криптоиздание The Block описывает его как со-лида крипто-AI seed и цитирует его тезис о децентрализованном тренинге. Отдельная страница стратегии 2026 в этом проходе не открыта. | Prime Intellect seed $5,5 млн, 23 апреля 2024, co-lead вместе с Distributed Global. Участие CoinFund в Series A 2026 пост компании поименно не подтверждает. | В пересказе The Block: централизованный контроль уже узкое место, Prime дает распределенный тренинг и собственность вкладчиков. | Ранний тезис был про протокол и собственность на модели. Живой бизнес 2026 года, по самой компании, продает стек предприятиям. Стратегия CoinFund на 2026 этим seed не описывается. |
| Distributed Global | Подтвержден как co-lead того же seed. Собственная страница тезиса не открыта. | Тот же Prime seed, $5,5 млн, 23 апреля 2024, co-lead. | Собственный текст 2026 не открыт. | Роль в сделке подтверждена. Текущая AI-стратегия неизвестна. |
| Dragonfly | В этом проходе подтвержден как lead equity-раунда криптопредпринимателя на криптодеске The Block. Собственный пост фонда не открыт. | Venice Series A $65 млн, 1 июля 2026, lead. Сумма раунда известна, чек Dragonfly неизвестен. | Собственное объяснение стратегии 2026 не открыто. | Нельзя из одной сделки выводить, что фонд ушел в чистый AI. Сделка смешанная: equity AI-компании плюс токеновый грант и варранты. |

Участники без открытой страницы стратегии: Coinbase Ventures и Archetype в раунде Venice. Они не посчитаны как отдельно подтвержденные фонды с тезисом.

Не криптофонды, хотя стоят в раундах: Founders Fund, Menlo Ventures, Radical Ventures, NVIDIA Ventures, Intel Capital, Dell Technologies Capital. Их присутствие важно для другого вывода: большие поздние деньги Prime пришли не из криптофондов.

F. Граф ребер

Проверка: 18 октября 2026.

VitaDAO и Molecule, прежняя работа, Vincent Weisser. Источники: https://ai.engineer/speakers/vincent-weisser и https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476

Vincent Weisser, CEO и сооснователь с января 2024, Prime Intellect. https://en.wikipedia.org/wiki/Prime_Intellect

Aleph Alpha, прежний работодатель, Johannes Hagemann, CTO Prime Intellect. Крипторебра нет. https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476

CoinFund, co-lead seed $5,5 млн, 23 апреля 2024, Prime Intellect.

Distributed Global, co-lead того же seed, Prime Intellect.

Erik Voorhees, ангел того же seed, Prime Intellect.

Erik Voorhees, основатель, Venice. https://www.theblock.co/news/deals/2026-07-01-venice-ai-funding-equity-valuation-dragonfly-406934

Founders Fund, lead $15 млн, февраль 2025, Prime Intellect. Это не криптофонд. https://www.primeintellect.ai/blog/fundraise

Radical Ventures и Brandt Katz, lead $130 млн, 8 июля 2026, Prime Intellect. Не криптофонд. https://techcrunch.com/2026/07/08/prime-intellect-raises-130m-series-a-to-help-enterprises-build-their-own-ai-agents/

Karim Atiyeh, Ramp, ангел Series A и заказчик кейса, Prime Intellect. https://www.primeintellect.ai/blog/series-a

Dragonfly, lead $65 млн, 1 июля 2026, Venice.

Coinbase Ventures, участник, Venice.

Archetype, участник, Venice.

Chris Dixon, a16z crypto, lead seed $33 млн, 2024, Yupp.

Yupp, закрытие 31 марта 2026. https://techcrunch.com/2026/03/31/yupp-ai-shuts-down-33m-a16z-crypto-chris-dixon/

Matt Huang и Alana Palmedo, Paradigm, четвертый фонд $1,2 млрд, 8 июля 2026, именные компании Nous, Zipline, Tempo, Hyperliquid, Kalshi. Суммы раундов не названы. https://www.paradigm.xyz/writing/announcing-our-fourth-fund

Katie Haun, Haun Ventures, $1 млрд новых фондов, 4 мая 2026, тезис агентной экономики. Ребро в конкретную AI-компанию открытым текстом не задано. https://www.haun.co/writing/fundii

Horvat Anderson и Vance Spencer, Framework, lead Series A $60 млн, Mecka AI, к 26 июня 2026. https://www.theblock.co/news/deals/2026-06-26-framework-ventures-400-million-fourth-fund-crypto-ai-robotics-406344

Framework, действующие позиции, Hyperliquid, Sky, Plasma.

Meta Diem и Move, прежняя работа, Sam Blackshear, сооснователь и бывший CTO Mysten Labs.

Sam Blackshear, уход из операционной роли 5 августа 2026 и роль советника, Mysten Labs и Sui.

Sam Blackshear, defensive security research, Anthropic. https://cryptobriefing.com/mysten-labs-co-founder-sam-blackshear-joins-anthropic-to-focus-on-defensive-security-research/

Chris Dixon, эссе 1 января 2025, тезис «AI нужен блокчейн для собственности, личности и следа контента». Это аргумент инвестора, не доказательство устройства бизнеса. https://a16zcrypto.com/posts/article/blockchain-ai-internet

G. Почему переходят

Наблюдения, только по открытым страницам.

Распределенные системы. Weisser перенес координацию DeSci и Molecule в компанию, чей продукт распределяет GPU и RL. Blackshear унес язык безопасных активов и опыт L1 в security лаборатории, не в тренинг моделей. Альтернатива: CTO Prime Intellect пришел из Aleph Alpha, то есть RL-стек собирает человек без подтвержденной криптооперационной биографии. Навык распределенных систем общий для инфраструктуры.

Дизайн механизмов. Dixon в эссе и в Fund 5 говорит, что агентам нужны проверяемые платежи, личность и собственность. Haun пишет, что агентам нужны родные версии кредита, страховки, личности и репутации, и что криптография здесь важна. Venice реально связала токен с API-кредитом и выкупом. Альтернатива: Series A Prime покупают Radical, NVIDIA, Intel и Dell под обычный корпоративный стек, без токена в описании продукта. Значит, механизм токена не является условием спроса на RL-инфраструктуру.

Рынки compute. У Prime есть Compute Exchange, слова компании, февраль 2025 и июль 2026. Framework одновременно держит крипторынки и инвестирует в энергию Daylight. Альтернатива в виде выручки майнинговых пивотов в облако в этом проходе первичными страницами не проверена и в доказательство не берется.

Сообщество и дистрибуция. Prime публикует модели, среды и инструменты. Ангелом был CEO Hugging Face. Сообщество открытых моделей существует и без крипты. У Venice дистрибуция в криптоаудиторию видна по структуре раунда и токену, размер этой аудитории в выручке не разложен.

Сбор капитала. Криптофонды действительно проводят размерные AI-сделки: seed Prime, seed Yupp, Series A Venice, Series A Mecka. Альтернатива: основной Series A Prime ведут не криптофонды. Крупный чек a16z crypto не спас Yupp.

Скорость бизнеса. Прямого замера нет. От основания Prime в январе 2024 до заявления о $100 млн годового темпа в июле 2026 прошло около двух с половиной лет. Это одна компания и слова компании. Класс «криптаны быстрее» из одного случая не следует.

Гипотеза «у криптанов чуйка и деньги».

Что видно: у части людей есть и навык координации, и доступ к криптокапиталу на ранней стадии. Weisser собрал криптоангелов и криптофонды в seed, потом компанию профинансировали общие технологические фонды.

Что бьет гипотезу. Yupp собрал $33 млн у очень известного криптопартнера и закрылся, имея 1,3 млн пользователей. Выживший пример Prime одновременно пример того, что поздние деньги пришли из другого круга инвесторов. Фонды, которых легче всего принять за «ушедших в AI», в собственных текстах оставляют крипту основной или равной линией: Paradigm, a16z crypto, Haun, Framework.

Survivorship и PR. Громко видны компания, которая объявляет $100 млн темпа, и фонд, который объявляет миллиардный фонд. Люди VitaDAO, которые никуда не ушли, в этом проходе по открытым страницам не посчитаны. Доля переходов неизвестна. Цикл тоже виден без психологической гипотезы: в мае 2026 a16z crypto описывает более тихий криптомомент и рост полезности стейблкоинов, а в июле 2026 AI-инфраструктура закрывает раунд $130 млн. Это совместимо с перетоком капитала. Это не доказательство особого чутья.

Неизвестно. Сколько операторов остались в крипте. Прибыль Prime и доллары прибыли Venice. Выручка Mecka и Nous. Стратегии CoinFund, Distributed Global и Dragonfly их собственными текстами 2026 года.

H. Приоритет работодателей

Веса равные, по 0,2: соответствие роли COO, CTO, operations, product, partnerships, infrastructure или agent systems; полезность криптобэкграунда; подтвержденный найм; финансовая устойчивость; доступность входа без личного знакомства. Каждый балл от 0 до 5. Проверка ссылок: 18 октября 2026. Теплое интро не обещано. Писем никто не пишет.

| Место | Компания | Роль, которая здесь полезна | Баллы: роль, криптобэкграунд, найм, устойчивость, вход | Взвешенно | Уверенность | Ссылка | Общий контекст и польза до просьбы о работе |
|---|---|---|---|---|---|---|---|
| 1 | Prime Intellect | Операции compute-маркетплейса, partnerships вокруг RL-стека, продукт environments и evals, инфраструктура распределенного тренинга. Исследовательская ML-роль не обязательна. | 5, 5, 3, 3, 3 | 3,8 | Средне-высокая по человеку и продукту. Средняя по выручке: это заявление компании. | Доска указана компанией: https://jobs.ashbyhq.com/PrimeIntellect. Список позиций 18 октября не разобран, поэтому найм не 5. Публичный канал: https://x.com/primeintellect | Общий фон: координация открытой сети, рынок compute, DeSci. Полезная вещь до найма: публичная среда или verifier для конкретного операционного workflow на Environments Hub, либо разбор отказа длинного агента на их же стеке. Просить работу после артефакта. |
| 2 | Venice | Partnerships и GTM приватного API, операционка агентного API, инфраструктура приватности. Токеновая структура означает, что операционисту понадобится аккуратность с equity и VVV. | 4, 5, 2, 3, 3 | 3,4 | Средняя. Прибыль качественная, ARR газетный, вакансии не открыты. | https://venice.ai/careers видна на главной 18 октября 2026, содержимое не открыто. Канал: [EMAIL] и https://x.com/AskVenice/ | Общий фон: криптоаудитория, приватность, API. Полезная вещь: публичное сравнение, что агентскому стеку нужно для нулевого хранения промптов и tool use, на их публичном API. Это разговор о продукте, не просьба о работе. |
| 3 | Anthropic | Узко: defensive security, злоупотребление инструментами агентов, надежность систем. Общее кресло COO из криптобэкграунда источниками не показано. | 2, 2, 4, 2, 2 | 2,4 | Средняя по тому, что дверь для security существует. Низкая по тому, что она подходит операционному руководителю. Финансовые цифры Anthropic не открыты, поэтому устойчивость специально занижена до 2. | https://www.anthropic.com/careers и https://www.anthropic.com/careers/jobs живы 18 октября 2026. Контакт рекрутера только @anthropic.com. | Их собственная страница просит независимую работу, текст или open source в начале резюме. Полезная вещь: публичный разбор защитной задачи для агентов с инструментами. Письмо Блэкширу из этого отчета не следует. |

Дальше список не дополнен. Mecka и Nous не набрали открытого продукта и вакансии. Yupp как работодатель имеет ноль: компания закрыта. Три работодателя вместо пятнадцати, потому что у остальных нет одновременно живой ссылки и подтвержденного криптоследя.

I. Пробелы и противоречия

Пара RL-компаний и конкретный выпуск не найдены. Уверенность в Вайссере высокая, уверенность в любой второй компании низкая.

Советничество Hagemann в VitaDAO первичным источником не подтверждено и в отчет как факт не вошло.

TechCrunch добавляет к Series A Prime оценку $1 млрд, Iconiq и ангела Srinivas. Пост компании оценку и Iconiq не называет.

Доска https://jobs.ashbyhq.com/PrimeIntellect в этом проходе по позициям не разобрана. Факт найма опирается на фразу компании от 8 июля 2026.

Страница https://venice.ai/careers не открыта. ARR Venice опирается на пересказ The Block, исходный TechCrunch не открыт.

Собственный пост Блэкшира не открыт. CryptoBriefing ссылается на него и пересказывает. Точная должность в Anthropic неизвестна.

Четвертый фонд Paradigm назвал компании без сумм и дат раундов. Пост Haun не назвал ни одной AI-портфельной компании. Тезисы Dragonfly, CoinFund и Distributed Global на 2026 их собственными страницами не открыты.

Mecka: известны лид и $60 млн, неизвестны дата закрытия, чек фонда, продукт, выручка, люди из крипты.

Квоты 30–50 человек и 15–25 фондов сознательно не заполнены. Добор из памяти или из неоткрытых сниппетов дал бы ложную плотность.

J. Источники, открытые 18 октября 2026

https://www.primeintellect.ai/blog/series-a
https://www.primeintellect.ai/blog/fundraise
https://techcrunch.com/2026/07/08/prime-intellect-raises-130m-series-a-to-help-enterprises-build-their-own-ai-agents/
https://en.wikipedia.org/wiki/Prime_Intellect
https://www.theblock.co/news/deals/2024-04-23-coinfund-and-distributed-global-lead-5-5-million-seed-round-for-decentralized-ai-firm-prime-intellect-290476
https://ai.engineer/speakers/vincent-weisser
https://www.theblock.co/news/deals/2026-07-01-venice-ai-funding-equity-valuation-dragonfly-406934
https://venice.ai/
https://www.anthropic.com/careers
https://cryptobriefing.com/mysten-labs-co-founder-sam-blackshear-joins-anthropic-to-focus-on-defensive-security-research/
https://techcrunch.com/2026/03/31/yupp-ai-shuts-down-33m-a16z-crypto-chris-dixon/
https://www.paradigm.xyz/writing/announcing-our-fourth-fund
https://www.haun.co/writing/fundii
https://a16zcrypto.com/posts/article/fund-5
https://a16zcrypto.com/posts/article/blockchain-ai-internet
https://www.theblock.co/news/deals/2026-06-26-framework-ventures-400-million-fourth-fund-crypto-ai-robotics-406344

K. Счет

Подтвержденные люди с крипторолью и последующей AI-ролью: 3. Vincent Weisser, Erik Voorhees, Sam Blackshear.

Подтвержденные компании с открытым продуктом или размерной сделкой: 4. Prime Intellect, Venice, Yupp, Mecka AI. Anthropic открыт как работодатель назначения, не как компания криптопроисхождения, и в эту четверку не входит.

Подтвержденные криптофонды с открытым тезисом или сделкой: 7. Paradigm, Haun Ventures, a16z crypto, Framework, CoinFund, Distributed Global, Dragonfly.

Подтвержденные размерные сделки этих фондов: 4. Prime seed $5,5 млн, Venice Series A $65 млн, Yupp seed $33 млн, Mecka Series A $60 млн.

Всего размерных раундов компаний в денежной таблице, включая некриптофонды: 6.

Денежные поля: 4 компании на 7 полей, 28 ячеек. Полностью неизвестны 19. Доля неизвестных 68%. Заполненными считаются и газетная оценка, и заявление компании. Отчетности среди открытых источников нет.

---

**Claude:**

{"lang":"ru","topic":"Крипто→AI: переходы людей, капитал криптофондов и двери найма для оператора","one_line":"Кто из криптоинтересантов, компаний и фондов реально перешёл в AI, куда идут деньги криптоVC и в какие компании оператору стоит заходить с криптобэкграундом.","key_findings":["История про VitaDAO и RL-компанию однозначно ведёт к Vincent Weisser (VitaDAO/Molecule → сооснователь и CEO Prime Intellect с января 2024). Вторая RL-компания и конкретный выпуск подкаста не найдены; Hagemann (CTO) пришёл из Aleph Alpha, а не из крипты, его советничество в VitaDAO не подтверждено.","Prime Intellect: Series A $130M (08.07.2026, lead Radical Ventures), суммарно свыше $150M (5,5+15+130=150,5, не складывать повторно). Компания заявляет >$100M annualized revenue и >6 тыс. клиентов (слова компании, не аудит); оценка $1B только у TechCrunch. Careers: 35 вакансий, включая Forward Deployed AI Strategy Lead, Solutions Architect, Technical Partnerships, Open Application. Поздние деньги пришли не от криптофондов (Founders Fund, Radical, NVIDIA, Intel, Dell), а криптофонды CoinFund и Distributed Global вели только seed $5,5M (апрель 2024).","Продукт Prime Intellect по классу — платный AI-стек (compute exchange, RL, environments hub, sandboxes, evals, deployment); токен/блокчейн в продукте 2026 как условие не подтверждён. Это бизнес, где операционный опыт и опыт мультивендорных систем применимы напрямую.","Венерация других дверей: OpenRouter (соглашение о приобретении Stripe от 19.08.2026, закрытие и цена не подтверждены), Ema (Surojit Chatterjee, Coinbase CPO → AI Employees; открыты AI Resident EMEA, Full-Stack, DevOps), Ritual, Catena ($18M led by a16z crypto), Hyperbolic ($12M/$20M, Variant+Polychain), Pluralis ($7.6M seed USV+CoinFund), Venice ($65M Series A led by Dragonfly при $1B, ARR >$70M по пересказу The Block, токен VVV сохраняется, прибыль в Q1 по словам компании).","Прямой переход в frontier-лабораторию существует, но узкий: Sam Blackshear (Move, Meta Diem, сооснователь/CTO Mysten Labs) → Anthropic defensive security research (05.08.2026), независимо подтверждено CryptoBriefing и Crypto.news. Это security research, а не операционное кресло; личное знакомство не доказано.","Криптофонды расширяют мандат, а не уходят из крипты: Paradigm (фонд IV $1,2B, 'сначала крипта, теперь ещё AI, робототехника'), a16z crypto (Fund 5 $2,2B), Haun ($1B новых фондов, тезис агентной экономики), Framework (FVIV $400M, Mecka AI Series A $60M). Крупный чек не гарантирует выживания: Yupp (seed $33M, a16z crypto) закрылся 31.03.2026 при 1,3 млн пользователей.","Гипотеза 'у криптанов чуйка и деньги' не доказана: выживший пример Prime привлёк поздний капитал вне криптокруга, Yupp — контрпример, видна survivorship-ошибка. Объяснения (навыки распределённых систем, дизайн механизмов, рынок compute, перенос капитала) имеют альтернативы. Падение крипто-коммитов на 75% — корреляция, а не измеренная миграция; OECD: 61% мирового VC ($258,7B из $427,1B) ушло в AI в 2025.","Расхождения вендоров: 'Venice — pure AI/no token' ошибочно (есть VVV, грант 1,5M VVV и варранты 5M); '45 crypto→AI migrants' завышено (включены инвесторы и люди без подтверждённой криптороли); Mistral добавил 55 людей и 24 фонда как второй список кандидатов, а не новых уникальных переходов; Grok подтвердил лишь 3 человека, 4 компании, 7 фондов и оставил 68% денежных полей неизвестными."],"recommendations":["Начинать с Prime Intellect: роль Forward Deployed AI Strategy Lead, затем Technical Partnerships, Solutions Architect, Open Application; заходить через артефакт (публичный environment/verifier или разбор отказа агентного workflow с evals, trace, затратами), а не через 'мы оба из крипты'.","Поставить рядом в верхнюю группу OpenRouter и Ema: проверить текущие вакансии и статус сделки со Stripe, использовать рассказ о внедрённых агентах и мультивендорных системах.","Вторым эшелоном рассматривать Ritual, Catena, Venice (с осторожностью к токен-экономике и equity), Nous, Hyperbolic/Pluralis/Gensyn; перед откликом проверять стадию продукта, заказчиков и финансовый горизонт, а не сумму раунда.","Использовать карту фондов (CoinFund, Polychain, Variant, Archetype, USV, a16z crypto, Framework, Dragonfly) как инструмент поиска портфельных компаний, не как рекомендацию; Anthropic рассматривать узко (security), письмо Blackshear не следует из отчёта.","Не отправлять заявки и сообщения автоматически: исходный заказ — исследование; не выдавать тематическое родство за личную рекомендацию и не писать про теплое интро, которого нет.","Довести ДР до кворума: дождаться ChatGPT, повторить упавшие рельсы (GLM capacity, Gemini unsupported country, Grok Heavy paywall) и сверить расхождения по числам и фондам по первичным документам."],"entities":{"people":["Vincent Weisser","Johannes Hagemann","Alex Atallah","Erik Voorhees","Niraj Pant","Akilesh Potti","Sean Neville","Sandeep Nailwal","Illia Polosukhin","Val Vavilov","Ben Fielding","Karan Malhotra","Roux Quesnelle","Teknium","Shivani Mitra","Holt Long","Jasper Zhang","Yuchen Jin","Kevin Weil","Sam Altman","Sam Blackshear","Surojit Chatterjee","Jason Zhao","Evan Cheng","Chris Dixon","Matt Huang","Alana Palmedo","Katie Haun","Horvat Anderson","Vance Spencer","Karim Atiyeh","Brandt Katz","Pankaj Gupta","Gilad Mishne"],"companies":["Prime Intellect","VitaDAO","Molecule","OpenRouter","Stripe","Ema","Ritual","Catena","Venice","Hyperbolic","Pluralis","Gensyn","Nous Research","Sentient","Gonka","Olas","Yupp","Mecka AI","Mysten Labs","Anthropic","Aleph Alpha","Paradigm","a16z crypto","CoinFund","Distributed Global","Polychain","Variant","Archetype","USV","Pantera","Framework Ventures","Dragonfly","Coinbase Ventures","Hack VC","Delphi","1kx","Robot Ventures","Haun Ventures","Radical Ventures","Founders Fund","OECD"],"products_tools":["Compute Exchange","Environments Hub","INTELLECT-3","PRIME-RL","TOPLOC","Prime Agent","VVV token","DIEM","Move","Sui","Hermes Agent","dr_queue.py","dr_leg_gate"]},"open_questions":["Вторая RL-компания и конкретный эпизод подкаста про VitaDAO не опознаны; советничество Hagemann в VitaDAO не подтверждено первичным источником.","Закрыта ли сделка OpenRouter/Stripe и по какой цене; какие вакансии открыты сейчас у OpenRouter, Ritual, Catena, Nous, Venice.","Список позиций на jobs.ashbyhq.com/PrimeIntellect и страница venice.ai/careers не разобраны; реальное соответствие вакансий оператору не проверено.","Выручка и прибыль Prime Intellect (>$100M annualized — заявление компании), Venice (ARR >$70M — пересказ The Block), Ema, Mecka, Nous не подтверждены отчётностью; 19 из 28 денежных полей неизвестны.","Стратегии CoinFund, Distributed Global, Dragonfly на 2026 по их собственным страницам не открыты; для Electric Capital, Placeholder, Galaxy, Jump, OKX, Animoca и др. полнота проверки недостаточна.","Кворум 4/6 не достигнут (есть Claude и Mistral, плюс частичный Grok; ChatGPT в работе); расхождения по токен-оценке Nous и составу инвесторов Prime Series A (Iconiq, Srinivas) требуют сверки.","Какова доля криптолюдей, оставшихся в крипте, и реальная скорость миграции — без отслеживания конкретных людей измерить нельзя."],"related_concepts":["Crypto-to-AI migration","DeSci / VitaDAO","Reinforcement learning environments и post-training","Decentralized AI compute","Crypto VC thesis expansion","Agent commerce и платежи для AI-агентов","Survivorship bias в венчурных нарративах","Карта работодателей для оператора","Forward Deployed Engineering","AI×crypto token economics","Frontier lab security hiring"]}
