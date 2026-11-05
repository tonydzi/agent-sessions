---
session: s_7e4784c7
date: 2026-10-23
words: 5333
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-23 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7e4784c7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-22-HUB-04-1359
REGISTRY TOPIC: Mem Martins Rua Jose Sampayo e Castro 19: realistic sale price and strategy (втащен в очередь dr_start --adopt; ПОТРЕБИТЕЛЬ: dev deciding asking price, achieved price range and house sale strategy) (Claude Research Max original received and structural gate passed (58 source URLs), substantive correction pending. 1 of 4 received; three remaining browser rails requested through peer_help mem-martins-dr-20261022 and signed TASK to NODE-0X; no claim yet. No final valuation accepted.) (1/4 vendor reports received. Claude targeted correction received: confidence LOW, EUR850k only hypothesis conditional on legal 500m2 gross area; no reserve/minimum established, A1 price history unproven, asking land is not floor. Four direct Idealista listings independently checked, area definitions corrected. Review saved _scratch/mem-martins-20261022/review.md; dashboard Mem-Martins-Sale-20261022.html. Remaining three browser rails blocked/unconfirmed; peer_help request open, signed TASK delivered to NODE-0X with no claim/ACK yet. Four-rail research incomplete.) (dr_reconcile 2026-10-23: на диске 2/4 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-22-HUB-04-1359\results)

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


===== VENDOR: gemini (DR26-10-22-HUB-04-1359-mem-martins-valuation-gemini.md) =====
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
Отчет по поставщикам метакаолина и микросилики
Исследование извести в строительных растворах
Activity
Rio de Mouro, Portugal
From your IP address
CryptoPunk Dz2
Work
•
Expanded
Conversation with Gemini
You said --- id: DR26-10-22-HUB-04-1359 date: 2026-10-22 14:03:02 theme: Mem Martins property sale valuation …

---

id: DR26-10-22-HUB-04-1359

date: 2026-10-22 14:03:02

theme: Mem Martins property sale valuation

session_id: s_fb5a2923

machine: HUB-01

targets: chatgpt,claudeai,gemini,mistral

adopted: долг реестра, втащен dr_start --adopt

---




Machine: HUB-01 (Хаб) · Agent: Codex · Operator: dev · 2026-10-22




# DR26-10-22-HUB-04-1359: Mem Martins property valuation and sale strategy




Authorisation: dev voice request 001:d85f0ca6b8, 22 October 2026. Consumer: dev deciding asking price, realistic achieved price, defensible minimum and how to sell. Exactly FOUR independent browser vendor rails: ChatGPT Pro Deep Research, Claude Research Max, Gemini Deep Research, Mistral Deep Research (Grok Heavy may substitute if inaccessible). Coding CLI/headless agents are not research rails. Do not publish a listing, contact agencies, order paid data or spend money.




Conduct independent thorough web research as of 22 October 2026. Answer in Russian; use Portuguese queries. Property: Rua Jose Sampayo e Castro 19 (also search Sampaio), Mem Martins, Sintra, Portugal. Owner states plot 3000m2; restored building after about 20 years abandoned; historically five dwellings for elderly people; new windows, landscaping, near-finished interiors with cosmetic work remaining; quiet cul-de-sac with convenient newly asphalted access near highway and good neighboring houses. Earlier owner-conversation note gives about 500m2 building and two floors, but CURRENT VOICE IS AMBIGUOUS: 500m2 is only a working assumption, NOT surveyed or licensed area. Bedrooms, legally registered units, usage licence, electricity certification, legal gross/private areas, PDM/REN/RAN/AUGI constraints and development rights UNKNOWN. Historic five units does not prove five legal units or care-home approval. Condition is owner description, not technical inspection. Do not anchor on prior AI price estimates. No clarification questions; complete using conditional scenarios and mark uncertainties.




Deliver:

1. Verify address and micro-location. Distinguish suburban Mem Martins from premium Sintra/Colares estates.

2. Seek 12-20 UNIQUE current comparable listings, nearest first: houses/estates with roughly 2000-5000m2 plots and 300-700m2 buildings; near-finished, restored or multiunit. Table: direct listing URL, observation date, locality/distance or unknown, asking EUR, building gross/private area with exact definition, plot, condition, units/legal evidence, time listed only if evidenced, comparability/adjustments. Deduplicate cross-agency listings. Separate secondary comparables and land/development comparables. Asking prices are NOT realised sales. Use official statistics and actual transaction evidence where obtainable; never invent sold prices.

3. Transparent adjusted-comparable valuation: justified achievable PRICE RANGE and confidence; suggested asking price; quick sale 30-90d; normal 3-6mo; patient 6-12mo; defensible minimum scenario (NOT owners authorised reserve). Show numerical sensitivity to legal/surveyed area, works remaining, utilities/licence gaps and market liquidity. Do not multiply all 3000m2 by urban land asking EUR/m2 or double-count full land value on top of house comparables.

4. Compare sale as restored family house, multi-family property ONLY if lawful, and development land ONLY conditional on verified PDM, REN/RAN/AUGI, access/PIP/buildability. Residual development calculation deducts construction, demolition, infrastructure, time, financing and developer profit; hypothetical top scenario is not current value. Explicitly distinguish feasibility from speculation.

5. Selling strategy: buyer segment, AMI agency verification, exclusivity tradeoffs, Idealista/Imovirtual/Casa Sapo, legal documentation and snagging, worthwhile improvements versus waste, PT/EN marketing, price-test and repricing based on qualified demand. Photography plan: light/weather, staged garden/rooms, honest unfinished areas, aerial drone legal checks. Sale expenses, commission plus VAT, net BEFORE capital gains tax; taxes conditional on unknown seller residency/acquisition basis. Current PRIMARY legal sources for legal/document claims, no legal certainty without documents.

6. Decision memo: ask/achievable/minimum or explicit inability to substantiate; strongest 5 comparables; top facts that change valuation; prioritised document checklist; 30-day preparation plan. Full linked sources. Separate observed fact / owner report / assumption / unknown / inference. State actual research mode and show real web search evidence.




Claude rail already submitted locally in Codex in-app browser with Research selected and Fable 5.1 Max. Remaining three need browser access; do not duplicate Claude. Submission alone is not complete research. Return report text, direct conversation URL, mode proof, unique-source count and actual status per rail.

Gemini said
DR26-10-22-HUB-04-1359: Независимая оценка и стратегия реализации объекта недвижимости в Mem Martins (Sintra)
1. Верификация адреса, микролокация и градостроительный контекст
1.1. Идентификация адреса и географические координаты

Адрес: Rua José Sampayo e Castro, n.º 19 (в реестрах и картографии встречаются орфографические варианты: Rua José Sampayo e Castro и Rua José Sampaio e Castro).   
Idealista

Почтовый индекс: [АДРЕС] Martins.

Фрегезия/Муниципалитет: Freguesia de Algueirão-Mem Martins, Concelho de Sintra, Distrito de Lisboa.   
www.cttcodigopostal.pt

Координаты улицы: ~38.7885° N, -9.3492° W.

Микрорайон: Bairro de São Carlos / южная граница с зоной Casais de Mem Martins и Coopalme.   
Idealista

Статус подъезда: Тупиковая улица (cul-de-sac), асфальтированный заезд, локальное соседство представлено жилой застройкой (индивидуальные дома, малоэтажные таунхаусы и многоквартирные жилые блоки 1980–2000-х годов постройки).

1.2. Фундаментальное различие: Mem Martins vs. элитные зоны Синтры / Колареша

Критическая ошибка продавцов и оценщиков на периферии Большого Лиссабона — перенос ценовых мультипликаторов престижных усадеб Синтры на урбанизированные пригороды Синтры.

       MEM MARTINS / ALGUEIRÃO                СИНТРА / COLARES / QUINTA DA BELOURA
┌──────────────────────────────────────┐    ┌──────────────────────────────────────┐
│ • Спальный/рабочий пригород Лиссабона│    │ • Международный ландшафтно-парковый  │
│ • Высокая плотность застройки        │    │   заповедник (Parque Natural)        │
│ • Целевой покупатель: португальский  │    │ • Элитный сегмент, экспаты, HNWI,    │
│   средний класс, локальный бизнес    │    │   международные школы (TASIS, CAISL) │
│ • Зависимость от IC19 / ж/д вокзала  │    │ • Премия за статус, приватность, вид │
│ • Ценовой потолок вилл: €600k–€900k  │    │ • Цены: от €1,5M до €5M+             │
└──────────────────────────────────────┘    └──────────────────────────────────────┘


Инфраструктура и логистика Mem Martins: Локация обладает отличной транспортной доступностью (быстрый выезд на магистрали IC19 и A16, близость ж/д станции Linha de Sintra Algueirão-Mem Martins), развитой сетью ритейла и коммунальных сервисов. Однако здесь отсутствует историко-ландшафтная премия, присущая São Pedro de Penaferrim, Janas, Galamares, Colares или закрытым кондоминиумам Quinta da Beloura.

Проблема крупного участка в 3000 м²: В плотной городской среде Mem Martins участок площадью 3000 м² представляет собой аномалию. Для классического покупателя семейного дома 3000 м² в черте Mem Martins — это обременение по уходу и налогам (IMI), а не романтический парк. Для девелопера этот участок ценен исключительно при условии возможности многоквартирного межевания или коммерческого девелопмента (дом престарелых, клиника, частный детский сад).

2. Анализ рынка и сопоставимые аналоги (Comparables)

Методологическое предупреждение: Цены предложения (Asking Prices) на порталах Idealista, Casa Sapo, Remax, ERA и Imovirtual отражают субъективные ожидания продавцов и регулярно подвергаются дисконту на стадии закрытия сделки (реальный спред в данном сегменте составляет 8–18%). По данным INE (Instituto Nacional de Estatística) и SIR (Sistema de Informação Residencial), медианная стоимость закрытых сделок вторичного жилья в Algueirão-Mem Martins варьируется в диапазоне €1 700 – €2 200/м² общей площади.

2.1. Таблица сравнительных объектов (Primary, Secondary & Land/Development)
№	Источник / URL	Локация / Дистанция	Цена предложения (€)	Площадь здания (Gross/Private)	Участок (м²)	Состояние объекта	Легальный статус / Назначение	Время на рынке	Аналитические корректировки к объекту
1	Idealista 34863319	N250-1, Algueirão-Velho (~2,2 км)	€765 000	~220 м² ABC (T3)	3 100 м²	Жилое / среднее (нуждается в модернизации)	1 жилой дом, городской участок (urbano)	>180 дн. (снижение с €785k)	Прямой аналог по земле (3100 м²). Участок идентичен, здание меньше, но полностью лицензировано.
2	Idealista 33988882	Av. Bombeiros Voluntários, Mem Martins (~0,8 км)	€890 000	516 м² ABC / 258 м² ABP (T5)	870 м²	Вторичное / хорошее, постройка 1993 г.	1 вилла (1 caderneta)	>120 дн.	Прямой аналог по площади здания (~500 м²). Участок существенно меньше (870 м²), но дом полностью автономен и с документами.
3	Casa Sapo ZMPT589482	Raposeiras, Algueirão (~1,9 км)	€625 000	92 м² ABP / ~150 м² ABC	1 450 м²	Требует ремонта / реконструкции	Жилое	>90 дн.	Премия за потенциал расширения участка; дом существенно меньше.
4	Idealista 35389232	Av. Marginal, Algueirão (~1,4 км)	€580 000	168 м² ABC (T5)	380 м²	Капитально отремонтирован	Сблокированный дом (Geminada)	<60 дн.	Отремонтированный объект, но стандартный малый участок пригорода.
5	Casa Sapo 36-Sintra	Mem Martins Poente (~1,1 км)	€648 000	370 м² ABC (T5)	650 м²	Жилое / хорошее состояние	Индивидуальный дом	>150 дн.	Крупный метраж в черте Mem Martins без земельного избытка.
6	Casa Sapo Algueirão	Rua Gil Eanes, Mem Martins (~0,9 км)	€605 000	200 м² ABC (T4)	420 м²	Полный ремонт 2024–2025 гг.	Жилой сектор	~45 дн.	Стандарт качественного готового жилья без юридических дефектов.
7	Idealista Estrada Mem Martins	Estrada Algueirão, Mem Martins (~1,0 км)	€845 000	262 м² ABC (T7)	740 м²	Полная реконструкция (2024 г.)	Многокомнатная вилла	>90 дн.	Демонстрирует верхнюю границу спроса на готовые виллы в черте поселка.
8	Idealista Baratã	Baratã / Casal da Mata (~2,5 км)	€895 000	202 м² ABC (T3)	743 м²	Новостройка / современный хай-тек	Лицензия 2024 г.	>120 дн.	Премия за современную архитектуру «под ключ».
9	Idealista Rua Vasco Santana	Bairro de São Carlos (соседняя улица, ~150 м)	€650 000	266 м² ABC (T5)	490 м²	Жилое / хорошее состояние	Сблокированный дом	>90 дн.	Микролокационный эталон. Та же инфраструктура и подъезд.
10	Idealista Bairro São Carlos	Bairro de São Carlos (~200 м)	€290 000	102 м² ABC (T2)	127 м²	Под реконструкцию	Отдельный дом с двориком	~60 дн.	Базовый уровень цен на дома без ремонта в микрорайоне.
11	Remax 182-Algueirao	Algueirão-Mem Martins	€585 000	310 м² ABC	510 м²	Среднее / под косметику	Вилла	>180 дн.	Показывает сопротивление рынка при слабом косметическом состоянии.
12	Remax Algueirão	Ouressa, Mem Martins (~1,2 км)	€690 000	200 м² ABC (T7)	600 м²	Жилое / под сдачу по комнатам	Вилла	>100 дн.	Альтернативное коммерческое использование (комнаты в аренду).
13	Idealista Terreno Padre Américo	Casais de Mem Martins (~1,1 км)	€850 000	Проект ERPI (1 943 м² надземной пл.)	3 990 м²	Земельный участок с проектом дома престарелых	Aprovado ERPI (58 коек)	>200 дн.	Аналог коммерческого назначения. Участок 4000 м² с готовым одобренным проектом ERPI стоит €850k. Без лицензии дисконт 40–50%.
14	Idealista Terreno Central	Mem Martins Centro (~0,9 км)	€600 000	Потенциал застройки	2 965 м²	Земля городская (terreno urbano)	В зоне консолидированной застройки	>180 дн.	Аналог стоимости «голой» городской земли. €202/м² участка без готовых лицензий.
15	Idealista Terreno Gago Coutinho	Ouressa, Mem Martins (~1,3 км)	€600 000	Назначение: Equipamento Social	2 700 м²	Земля под социальные объекты	Социальная инфраструктура	>365 дн.	Показывает ликвидность участков с ограничением по назначению (equipamento social).
16	ERA id_a4091e09	Periferia Mem Martins (~2,0 км)	€400 000	Сельхоз/рустикальные постройки	11 000 м²	Смешанный участок (terreno misto)	Ограничения RAN/REN	>240 дн.	Иллюстрирует падение цены до €36/м², если земля имеет статус rustico/misto.
3. Расчет скорректированной стоимости и ценовые сценарии
3.1. Анализ рисков и дисконтирующих факторов объекта

Неопределенность легальной площади (Legal ABC vs. Working Assumption):

Заявленные ~500 м² — это исключительно слова владельца. Если по Caderneta Predial Urbana зарегистрировано 180–220 м², а остальное возведено или перестроено самовольно, банк покупателя не выдаст ипотечный кредит на незарегистрированную площадь.

Отсутствие действующей лицензии на эксплуатацию (Licença de Utilização):

Здание стояло заброшенным ~20 лет. По португальскому праву (DL 10/2024 — Simplex Urbanístico) отменено обязательное предоставление Licença de Utilização при нотариальной сделке (escritura), НО банки при выдаче ипотеки требуют подтверждения легальности или технического соответствия. Незаконные пристройки не кредитуются.

Статус 5 автономных фракций:

Историческое проживание 5 пожилых людей не означает юридического режима горизонтальной собственности (Propriedade Horizontal). Без регистрации 5 автономных долей (fracções autónomas) объект продается юридически как единое здание (Prédio em Propriedade Total), что отсекает розничных покупателей квартир.

Незавершенность отделки и инженерии:

Риск отсутствия сертификата CERTIF / DGEG на электроустановку, сертификата ITED (связь), сертификации водопровода и канализации. Доведение до финиша 500 м² требует от €40 000 до €90 000.

Недопустимость механического суммирования (Double Counting Fallacy):

Нельзя умножать 500 м² дома на рыночные €2 500/м² (€1 250 000) и прибавлять к этому 3000 м² земли по €200/м² (€600 000), получая фиктивные €1,85M. Рынок вилл в черте Algueirão-Mem Martins имеет жесткий «психологический и платежеспособный потолок» в районе €700 000 – €900 000. Любой объект дороже €900k конкурирует с виллами в престижных зонах Синтры, Кашкайша и Оэйраша.

3.2. Матрица чувствительности стоимости
Сценарий легального статуса	Легальная площадь (ABP)	Статус лицензий и сетей	Оценка чистой стоимости (€)	Вероятность сценария
Худший (Baseline)	По документам числится <200 м² (руина/старый склад)	Требуется полный проект легализации в Câmara Municipal de Sintra	€480 000 – €560 000	30%
Рабочий (Moderate)	Зарегистрировано ~300–350 м² жилья	Единый дом (Propriedade Total), электричество подключено	€650 000 – €750 000	50%
Оптимальный (Bull)	Все 500 м² узаконены, 5 юридических фракций	Отдельные счетчики, действующие сертификаты	€880 000 – €1 050 000	20%
3.3. Финансовые горизонты продажи и рекомендованные цены
ДИАПАЗОН СТОИМОСТИ И СТРАТЕГИЯ ЦЕНООБРАЗОВАНИЯ (€)
0k          200k        400k        600k        800k        1000k
├───────────┼───────────┼───────────┼───────────┼───────────┤
                        [=== A ===]                                 A: Быстрая продажа (€550k–€630k)
                                [======= B =======]                 B: Реалистичная сделка (€680k–€760k)
                                        [===== C =====]             C: Оптимистичная (€790k–€890k)
                                                ▲
                                                Asking Price: €795 000 (старт)


Рекомендованная цена предложения (Asking Price):

€795 000 (при условии подтверждения площади от 350 м² и наличия света/воды). Данная цена оставляет психологический люфт для торга вниз до реального диапазона.

Реалистичный диапазон достижения сделки (Achievable Price Range):

€680 000 – €760 000 (уверенность: Medium-High, основана на закрытии аналогов с участками 1000–3000 м² в Algueirão).

Быстрая продажа (Liquidation, 30–90 дней):

€550 000 – €630 000. На этом уровне объект становится безусловно привлекательным для локальных строителей-флипперов или инвесторов в доходную аренду, готовых взять на себя все риски доделок и лицензирования.

Нормальный срок экспозиции (3–6 месяцев):

€680 000 – €740 000. Выход на целевого покупателя (большая семья или локальный предприниматель).

Терпеливый сценарий (6–12 месяцев):

€780 000 – €840 000. Возможен только при условии, что продавец доведет отделку до 100%, устранит строительные огрехи и получит полный пакет инженерных сертификатов.

Обоснованный расчетный минимум (Defensible Minimum):

€540 000. Ниже этой отметки опускаться нецелесообразно: ликвидационная стоимость одной лишь городской земли 3000 м² в этой локации составляет не менее €350 000 – €420 000 (по €120–€140/м²), а восстановленная коробка 500 м² с крышей и остеклением стоит не менее €150 000 – €180 000 в ценах стройматериалов.

4. Сравнительный анализ сценариев использования и девелопмента
4.1. Сценарий А: Единая семейная вилла (Single-Family Estate)

Целевой рынок: Состоятельные португальские семьи, семьи экспатов, ищущие просторную приватную территорию с садом и бассейном недалеко от Лиссабона.

Плюсы: Минимальные юридические барьеры. Продажа «как есть» в режиме единой собственности.

Минусы: Избыточная земля. Среднестатистический покупатель в Mem Martins не готов содержать 3000 м² сада в урбанизированном районе. Ограниченный круг клиентов.

4.2. Сценарий B: Мультисемейный доходный дом (Multi-Unit / 5 Fracções)

Юридическое требование: Оформление режима Propriedade Horizontal в Câmara Municipal de Sintra и регистрация в Conservatória do Registo Predial. Требует:

Независимых входов для каждой единицы;

Выделенных парковочных мест по нормам PDM Sintra;

Автономных счетчиков воды, электричества, телекоммуникаций;

Звуко- и теплоизоляции между фракциями по стандартам RGEU / RJUE.

Экономика: Если объект делится на 5 полноценных квартир (например, 3xT2 + 2xT1):

Арендный доход: T2 в Mem Martins сдается за €950–€1 100/мес, T1 — за €750–€850/мес.

Валовый арендный поток: ~€4 500/мес = €54 000/год.

При требуемой доходности инвестора 7% Gross Yield капитальная стоимость объекта для инвестора составляет:

Value=€54 0000,07≈€770 000
Value=
0,07
€54000
	​

≈€770000

Затраты на завершение и разделение сетей: ~€60 000 – €80 000.

Чистая цена покупки сырого объекта: ~€690 000 – €710 000.

4.3. Сценарий C: Девелопмент / Резидуальный расчет земли (Residual Land Value)

Оценка возможности сноса или разделения участка под строительство нового таунхаус-комплекса или малоэтажного кондоминиума.

Ограничение: Возможно только в случае подтверждения статуса Espaço Residencial Consolidado / Moradias в PDM Sintra и отсутствия обременений RAN (Reserva Agrícola Nacional) или REN (Reserva Ecológica Nacional).

Резидуальный расчет девелопмента (Hypothetical Subdivision: 6 таунхаусов):

Допустим, PDM позволяет построить 6 таунхаусов общей площадью 
6×160 м²=960 м²
6×160 м²=960 м² ABC.

Прогнозная выручка (Gross Development Value, GDV):

6×€380 000=€2 280 000
6×€380000=€2280000

Затраты девелопера:

Строительство и благоустройство: 
960 м²×€1 400/м²=€1 344 000
960 м²×€1400/м²=€1344000

Снос / демонтаж / земляные работы: €40 000

Проектирование, согласование PIP/Licenciamento, муниципальные сборы (Taxas Urbanísticas): €85 000

Финансовые затраты и проценты по кредиту: €110 000

Маркетинг, брокеридж, налоги девелопера: €120 000

Норма прибыли девелопера (Developer’s Profit 18% от GDV): €410 000

Итого затраты и прибыль девелопера: €2 109 000

Резидуальная стоимость земли (Residual Land Value):

€2 280 000−€2 109 000=€171 000
€2280000−€2109000=€171000

Вывод: Из-за высоких текущих затрат на строительство (€1 400 – €1 600/м²) и умеренных розничных цен на жилье в Mem Martins снос существующего строения под проект застройки экономически нецелесообразен. Существующее восстановленное здание представляет основную ценность объекта. Продавать объект следует как готовую усадьбу / резиденцию с земельным резервом, а не как пятно под застройку.

5. Стратегия реализации, маркетинг и юридические аспекты
5.1. Целевой покупатель

Мультигенерационная семья (местная или иностранная): Совместное проживание родителей, детей и внуков на одной приватной территории в черте городской инфраструктуры.

Локальный инвестор в арендный бизнес: Сдача в долгосрочную или среднесрочную аренду (комнаты / квартиры / коливинг).

Коммерческий профиль (Social / Services): Частная медицинская клиника, детский сад, реабилитационный центр, пансион для пожилых людей (ERPI).

5.2. Агентство и условия договора

Лицензирование: Работать строго через сертифицированные агентства с действующей лицензией AMI (Associação dos Mediadores e Imobiliários de Portugal), проверяемой в базе IMPIC.

Эксклюзивность vs. Открытый листинг:

Рекомендуется эксклюзивный мандат на 4–6 месяцев с крупным сетевым агентством (Remax Collection, ERA, Keller Williams или Century 21).

Условие эксклюзива: Включение пункта о кросс-листинге во всех национальных базах и обязательная профессиональная фотосъемка/видеосъемка за счет агентства.

Комиссия агентства: стандартная ставка составляет 5% + IVA (23%) (эффективная комиссия — 6,15%).

5.3. Маркетинг и каналы продвижения

Национальные порталы: Idealista.pt (№1 в Португалии, обязательно пакет Highlight/Destaque), Imovirtual, Casa Sapo.

Международные площадки: Green-Acres, SennEdition, Kyero, Tranio (для европейских покупателей, ищущих крупные площади).

Языковые версии: Презентация и брошюра должны быть подготовлены на португальском и английском языках.

Фотосъемка и медиа-план:

Фотосъемка строго в солнечный день (золотой час);

Homestaging: виртуальный или базовый физический рендеринг незавершенных комнат;

Честная фиксация недоделок (не скрывать незаконченные узлы, чтобы не срывать просмотры на стадии инспекции);

Аэросъемка с дрона: Критически важна, чтобы подчеркнуть масштаб участка 3000 м², асфальтированный тупиковый подъезд и качественное соседство;

Юридическое требование к полетам: Согласно нормам ANAC (Autoridade Nacional da Aviação Civil), дрон должен быть зарегистрирован, а в зоне военного сектора авиабазы Синтра (Sintra Air Base / Granja do Marquês) может требоваться согласование AAN (Autoridade Aeronáutica Nacional).

5.4. Необходимые доделки vs. лишние траты
         ЧТО СДЕЛАТЬ ОБЯЗАТЕЛЬНО                   ОТ ЧЕГО СТОИТ ОТКАЗАТЬСЯ
┌────────────────────────────────────────┐ ┌────────────────────────────────────────┐
│ 1. Сертификация электрики (CERTIF/DGEG)│ │ 1. Монтаж дорогой элитной кухни        │
│ 2. Покраска фасада и цоколей в белый/  │ │ 2. Укладка премиального паркета        │
│    светло-серый нейтральный цвет       │ │ 3. Капитальный ландшафтный дизайн на   │
│ 3. Покос травы, обрезка кустарников,   │ │    всех 3000 м² (хватит простого покоса│
│    вывоз строительного мусора          │ │    и гравийных дорожек)                │
│ 4. Установка розеток, выключателей и   │ │ 4. Попытка строительства капитального  │
│    базовой сантехники (унитазы, краны) │ │    бассейна без проекта                │
└────────────────────────────────────────┘ └────────────────────────────────────────┘

5.5. Структура расходов при продаже и налоги
Статья расходов	База расчета	Сумма при сделке €750 000	Примечание
Комиссия агентства	5% от цены сделки	€37 500	Стандартный договор AMI
НДС на комиссию (IVA)	23% от комиссии	€8 625	Законное требование в Португалии
Энергетический сертификат (CE)	Фиксированная стоимость инженера ADENE	€250 – €400	Обязателен для публикации объявления
Справки и выписки (Certidões)	Реестры Conservatória / Finanças	€50 – €100	Свежие выписки не старше 6 месяцев
Мелкий косметический финиш/клининг	Подрядчики	€3 000 – €6 000	Окупается ростом ликвидности
Чистый остаток до налогов (Net Before Tax)	—	~€697 000 – €700 000	Поступление продавцу до расчета прироста капитала

Налог на прирост капитала (Mais-Valias):

Зависит от резидентства продавца, года и стоимости первоначального приобретения (Valor de Aquisição), подтвержденных расходов на ремонт за последние 12 лет (Benfeitorias с фактурами NIF) и коэффициента инфляции (Coeficiente de Desvalorização da Moeda).

Для резидентов Португалии: 50% чистой прибыли прибавляется к общему доходу IRS и облагается по прогрессивной шкале (до 48% + солидарный налог), либо освобождается при реинвестировании в основное жилье (HPP).

Для нерезидентов: С учетом судебной практики ЕС и изменений в Orçamento do Estado, налогообложение нерезидентов приведено к правилам для резидентов (обложение 50% прибыли по прогрессивным ставкам).

6. Резюме для принятия решений (Decision Memo)
6.1. Ключевые ценовые ориентиры

Цена предложения (Start Asking Price): €795 000

Реалистичный диапазон закрытия сделки: €680 000 – €750 000

Расчетный минимум (Defensible Walk-Away Minimum): €540 000

6.2. Топ-5 наиболее релевантных рыночных аналогов

N250-1, Algueirão-Velho (Ref: ZMPT586227): Вилла на участке 3 100 м² за €765 000. Прямое подтверждение того, что аналогичный земельный объем в данном округе торгуется в районе €700k–€760k.   
OLX Portugal

Av. Bombeiros Voluntários, Mem Martins: Дом 516 м² на участке 870 м² за €890 000. Подтверждает предел цены для крупного здания (~500 м²) в центре поселка.

Casais de Mem Martins (ERPI Project): Участок 3 990 м² с утвержденным проектом за €850 000. Показывает потенциал коммерческого использования.

Bairro de São Carlos (Rua Vasco Santana): Вилла 266 м² на участке 490 м² за €650 000. Эталон локального спроса в непосредственном радиусе 150 метров от объекта.

Ouressa / Mem Martins (Gago Coutinho): Городской участок 2 700 м² за €600 000. Устанавливает базовую планку стоимости крупного участка без готового жилья.

6.3. Факторы первой величины, способные изменить оценку

[+] Регистрация 5 автономных фракций (Propriedade Horizontal): Увеличит совокупную стоимость реализации объекта до €850 000 – €950 000.

[–] Расхождение в Caderneta Predial (если легальная площадь < 200 м²): Снизит рыночную стоимость до €500 000 – €560 000 из-за невозможности покупателей привлечь банковскую ипотеку.

[–] Наличие сервитутов или ограничений PDM (охранные зоны линий передач, водотоков): Может заблокировать любое дополнительное использование земли.

6.4. Приоритетный чек-лист документов (Document Checklist)
[ ] 1. Caderneta Predial Urbana (Finanças) — не старше 3 месяцев. Проверить Área Bruta de Construção (ABC),
       Área Bruta Privativa (ABP) e Área de Implantação.
[ ] 2. Certidão Permanente de Registo Predial (Registo Predial Online via código de acesso). Проверить
       собственников, наличие ипотек, залогов, арестов и статус собственности (Total vs. Horizontal).
[ ] 3. Licença de Utilização / Alvará de Obras (Câmara Municipal de Sintra) или подтверждение освобождения
       (certidão de isenção de licença anterior a 1951, если применимо).
[ ] 4. Plantas Aprovadas pela Câmara Municipal de Sintra (Архитектурные планы). Сопоставить фактическую
       геометрию комнат с планами в архиве мэрии.
[ ] 5. Certificado Energético (CE), выданный сертифицированным экспертом ADENE (обязателен по закону до
       выхода в рекламу).
[ ] 6. Ficha Técnica da Habitação (FTH) — для объектов, построенных или реконструированных после марта 2004 г.
[ ] 7. Техническая сертификация инженерных сетей:
       - Ficha de Instalação Elétrica (DGEG / E-Redes);
       - Подтверждение подключения к муниципальным сетям водоснабжения и канализации (SMAS de Sintra).

6.5. 30-дневный операционный план подготовки к продаже

Дни 1–7: Юридический аудит и документация

Заказать электронную Certidão Permanente и свежую Caderneta Predial.

Поднять в архиве Câmara Municipal de Sintra исторический строительный файл (processo de obras) и поэтажные планы.

Пригласить аккредитованного инженера ADENE для энергетической оценки и выпуска Certificado Energético.

Дни 8–15: Техническое обследование и смета завершения

Провести выезд электрика с прибором для проверки контура заземления и целостности щитка; при необходимости получить технический отчет для DGEG.

Составить дефектную ведомость (snagging list) косметических работ: плинтусы, розетки, силикон в санузлах, подкраска сколов.

Нанять бригаду на 3 дня: генеральный покос травы, вырубка дикого кустарника, вывоз строительного мусора с участка 3000 м².

Дни 16–22: Выбор брокера и юридический мандат

Провести интервью с 3 ведущими агентствами района (с обязательной проверкой AMI), запросить их локальные отчеты CMA (Comparative Market Analysis).

Согласовать эксклюзивный договор с комиссией 5% + IVA, зафиксировав обязательства агентства по премиальному маркетингу и съемке.

Дни 23–27: Производство контента

Провести клининг готовых помещений.

Профессиональная интерьерная и экстерьерная фотосессия в ясный день.

Выполнить квадрокоптерную съемку участка, подъезда и панорамы в сторону Синтры с соблюдением требований ANAC.

Дни 28–30: Старт листинга

Запуск объявлений на Idealista (с промо-пакетом), Casa Sapo, Imovirtual и международных витринах по стартовой цене €795 000.

Фиксация входящего потока лидов и проведение первых квалифицированных показов.

7. Разделение типов информации и статус исследовательской сессии
7.1. Классификация статуса данных

Наблюдаемые факты (Observed Facts):

Локация Rua José Sampayo e Castro ([АДРЕС] Martins) верифицирована; улица является асфальтированным тупиком в жилой зоне Bairro de São Carlos.

Цены предложения на участки 2 500–3 500 м² в Algueirão-Mem Martins зафиксированы на уровне €600 000 – €765 000.   
Idealista

Сообщения владельца (Owner Reports):

Площадь участка 3 000 м²; здание восстановлено после 20 лет заброшенности; ранее проживали 5 пожилых людей; новые окна, благоустройство, интерьеры требуют косметики.

Рабочие допущения (Assumptions):

Площадь здания составляет порядка ~500 м² (не подтверждена официальным обмером или кадастром).

Несущие конструкции, кровля и гидроизоляция находятся в удовлетворительном техническом состоянии.

Неизвестные параметры (Unknowns):

Точная площадь по Caderneta Predial (ABC/ABP);

Наличие и дата выдачи Licença de Utilização;

Режим собственности (единый дом или горизонтальная собственность на 5 долей);

Наличие обременений PDM Sintra (зоны сервитутов, RAN, REN, AUGI);

Налоговый статус продавца (резидентство, база затрат).

Аналитические выводы (Inferences):

Снос здания под девелопмент финансово убыточен (резидуальная стоимость земли составляет всего ~€171 000 против стоимости объекта >€650 000).

Оптимальный рыночный сценарий — реализация как единой крупной резиденции/усадьбы либо продажа локальному арендному оператору.

7.2. Метаданные исследовательской сессии (Rail Status)

Rail Provider: Gemini Research Engine (Direct Browser / Web Search Grounding).

Status: Research Complete & Synthesized.

Search Execution Evidence: Выполнены прямые поисковые запросы на португальском языке к национальным базам и порталам: imoveis venda Mem Martins Sintra, "Rua Jose Sampayo e Castro" Sintra, Terreno com 3.100 m² em Algueirão, moradias Bairro de São Carlos, quinta Algueirão Mem Martins idealista.   
Idealista

Unique Sources Cited: 16 профильных листингов и источников (включая Idealista, Casa Sapo, Remax, ERA, CTT Códigos Postais, DGSI).




Thinking

Gemini is AI and can make mistakes, including about people. Your privacy and Gemini
Opens in a new window

Searching the web

## Ссылки со страницы (href, собраны рельсой)
https://www.idealista.pt/imovel/34863319/
https://www.idealista.pt/imovel/33988882/
https://casa.sapo.pt/comprar-moradias/sintra/algueirao-mem-martins/
https://www.idealista.pt/imovel/35389232/
https://www.idealista.pt/comprar-casas/algueirao-mem-martins/bairro-de-sao-carlos/com-moradias/
https://remax.pt/pt/comprar/outros---comercial/sintra/algueirao-mem-martins
https://www.idealista.pt/comprar-terrenos/sintra/algueirao-mem-martins/
https://www.era.pt/imovel/terreno-misto-sintra-mem-martins-386250079

---

**Claude:**

{"lang":"ru","topic":"Mem Martins, Rua José Sampayo e Castro 19: реалистичная цена и стратегия продажи","one_line":"Какова реалистичная цена продажи (asking, ожидаемая сделка, защитимый минимум) и лучшая стратегия продажи восстановленного здания ~500 м² на участке 3000 м² в пригороде Mem Martins (Sintra).","key_findings":["Адрес верифицирован как Rua José Sampayo e Castro, индекс 2725-354, фрегезия Algueirão-Mem Martins, Bairro de São Carlos; тупиковая улица. Это пригородный Mem Martins, а не премиальные Sintra/Colares/Beloura (там €1,5M–5M+), премиальные мультипликаторы переносить нельзя.","Площадь 500 м² - только рабочее допущение владельца, не подтверждена обмером или Caderneta Predial; от легальной площади (ABC/ABP) зависит всё. Пять исторических жилищ не доказывают пять юридических fracções, лицензию на использование или разрешение на ERPI.","Gemini-сценарии стоимости: худший (<200 м² по документам) €480–560k (вероятность 30%); рабочий (~300–350 м², единый дом) €650–750k (50%); оптимальный (500 м² узаконены, 5 fracções) €880k–1,05M (20%). Claude-ветка независимо: уверенность LOW, €850k лишь гипотеза при легальных 500 м² gross; нижняя граница и история цен не установлены, цена за землю не является минимумом.","Ориентиры Gemini: asking €795k (при подтверждении ≥350 м² и коммуникаций), реалистичная сделка €680–760k, быстрая продажа 30–90 дней €550–630k, нормальный срок 3–6 мес €680–740k, терпеливый 6–12 мес €780–840k, защитимый минимум ~€540k (не авторизованный резерв владельца). Это цены предложения, а не реализованные сделки; спред ask-vs-close оценён 8–18% без первичного источника.","Ключевые аналоги (asking): участок 3100 м² с домом ~220 м² на N250-1 Algueirão-Velho €765k; дом 516 м² на 870 м² (1993) Av. Bombeiros Voluntários €890k; вилла 266 м² на 490 м² Bairro de São Carlos (~150 м) €650k; участок 3990 м² с проектом ERPI (58 коек) €850k; городской участок 2700 м² (equipamento social) €600k. Потолок вилл в районе ~€700–900k.","Двойной счёт недопустим: 3000 м² × цена городской земли + дом по €/м² даёт фиктивные ~€1,85M. Снос под таунхаусы (6×160 м²) даёт остаточную стоимость земли всего ~€171k при расчёте Gemini, поэтому девелопмент невыгоден, ценность в восстановленном здании.","Мультиюнит (5 fracções) возможен только при законном оформлении Propriedade Horizontal: валовая аренда ~€54k/год, при 7% yield ~€770k за вычетом €60–80k на доделку и разделение сетей ≈ €690–710k. Оформление fracções могло бы дать €850–950k, но это условно.","Расходы при продаже: комиссия 5% + IVA 23% (эффективно 6,15%) ≈ €46k на €750k; чистыми до налога на прирост капитала ~€697–700k; доделка и сертификация €40–90k по оценке Gemini; налог на прирост капитала зависит от резидентства и базы приобретения (неизвестны).","Статус исследования: по состоянию на 23.10.2026 получены 2 из 4 вендоров (Claude, Gemini); ChatGPT и Mistral не получены, итоговая оценка не принята. Gemini-таблица содержит часть неточных или необъективных ссылок (в списке собраны лишь 8 прямых URL); Claude независимо проверил 4 листинга и поправил определения площади."],"recommendations":["Не публиковать asking и не ставить окончательную цену, пока не получены Caderneta Predial (ABC/ABP) и Certidão Permanente; сперва выяснить легальную площадь и количество fracções.","Заказать документы: Caderneta Predial, Certidão Permanente do Registo Predial, Licença de Utilização/планы в Câmara de Sintra, Certificado Energético (ADENE), электрический сертификат DGEG/E-Redes, подтверждение подключения к SMAS.","Продавать как восстановленную резиденцию с большой землёй, а не как девелоперский участок; ориентир asking около €795k только при подтверждении ≥350 м² и коммуникаций, иначе пересчитать по сценариям.","Эксклюзив с сетевым агентством 4–6 мес. с проверкой AMI на IMPIC, обязательная профессиональная фото-, видео- и дрон-съёмка (с проверкой ANAC/зоны авиабазы), листинг на Idealista, Imovirtual, Casa Sapo и международных порталах, материалы на PT и EN.","Тратить на косметику и сертификаты (электрика, покраска, уборка участка, вывоз мусора), не вкладываться в дорогую кухню, паркет, полный ландшафт или бассейн.","Ценовой тест: старт с asking, пересмотр по числу квалифицированных показов; быстрый сценарий €550–630k держать как запасной.","Дождаться оставшихся рельс (ChatGPT, Mistral) и перепроверить комп-таблицу Gemini по прямым URL, прежде чем принимать решение о цене."],"entities":{"people":["dev"],"companies":["Idealista","Imovirtual","Casa Sapo","Remax","ERA","Keller Williams","Century 21","Green-Acres","SennEdition","Kyero","Tranio","CTT"],"products_tools":["Caderneta Predial Urbana","Certidão Permanente de Registo Predial","Licença de Utilização","Certificado Energético (ADENE)","Ficha Técnica da Habitação","DGEG/E-Redes","IMPIC (AMI)","INE","ANAC","PDM Sintra","REN/RAN/AUGI","Propriedade Horizontal","SMAS de Sintra","Gemini Deep Research","Claude Research Max"]},"open_questions":["Какова легальная площадь (ABC/ABP) и действительная площадь здания: 500 м² неподтверждены.","Есть ли Licença de Utilização, сколько юридических fracções и какое назначение (в том числе ERPI) у здания.","Какова классификация участка по PDM Sintra, нет ли ограничений REN/RAN/AUGI и возможностей застройки.","Какие реальные цены закрытых сделок в районе (данные INE/регистра), а не только asking; верен ли заявленный спред 8–18%.","Достоверны ли аналоги и ссылки Gemini (много листингов без прямых URL) и корректны ли определения площади.","Налоговый статус продавца (резидентство, стоимость приобретения) для расчёта налога на прирост капитала.","Не получены отчёты ChatGPT и Mistral; нет резервной цены владельца, нужно ли ему срочно продавать."],"related_concepts":["оценка недвижимости методом сопоставимых объектов","цена предложения против цены сделки","остаточная стоимость земли (residual land value)","Propriedade Horizontal","легализация и лицензия на использование","PDM Sintra и REN/RAN","стратегия продажи и эксклюзивный мандат AMI","налог на прирост капитала в Португалии","ERPI (дома престарелых)","Deep Research кворум рельс"]}
