---
session: s_afe92b16
date: 2026-10-29
words: 5465
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_afe92b16` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-28-HUB-06
REGISTRY TOPIC: Оливковое масло в Португалии: антиоксиданты, качество, свежесть и реал

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


===== VENDOR: report (DR26-10-28-HUB-06-оливковое-масло-в-португалии-антиоксиданты-ка.md) =====
# Оливковое масло в Португалии: антиоксиданты, качество, свежесть и реальная покупка

**DR-ID: DR26-10-28-HUB-14-2011**  
**Дата проверки: 28 октября 2026, Europe/Lisbon.**

Главный вывод: рынок премиального EVOO в Португалии сейчас распадается на две очень разные категории. У большинства хороших португальских масел есть убедительные данные об урожае, сортах, холодной экстракции, DOP/organic и сенсорике, но **нет опубликованного COA конкретной текущей партии с полифенолами**. У нескольких греческих high-phenolic масел, наоборот, есть анализ конкретного урожая с олеоканталом, олеацеином и производными гидрокситирозола/тирозола, но они стоят на порядок дороже. Поэтому высокий рейтинг ниже не означает, что португальское масло «химически хуже»: это означает, что доказательная база по конкретной бутылке хуже.

Самое важное практическое обстоятельство на сегодня: урожай **2026/27 уже начался**, но подтверждённые COA нового урожая практически ещё не успели попасть в розницу. Например, свежий **Olival da Risca Primeur 2026/27** уже выставлен по €9,50/250 ml, произведён из оливок начала октября 2026, но продавец прямо указывает **pre-order и готовность к отправке только 9 ноября 2026**. Поэтому я не считаю его доступным сегодня и не подменяю им фактически продающийся урожай 2025/26. citeturn19view0

## Резюме и критерии отбора

Мой общий топ на 28 октября 2026:

| Место | Конкретная бутылка | Почему попала в топ |
|---|---|---|
| **Лучший overall по аналитике** | **Drop of Life Healthy Limited Reserve 500 ml** | Полный COA урожая Sep-2025: 2162 mg/kg анализируемых фенолов, 941 mg/kg производных hydroxytyrosol, 1221 mg/kg производных tyrosol, oleocanthal 234, oleacein 209; 43,25 mg квалифицируемых производных на 20 g. В наличии. citeturn22view0turn23view1 |
| **Максимальная измеренная концентрация** | **Sparta Medicinal Wild Olive Oil Limited White Label 250 ml** | 3057 mg/kg total phenolics и 2126 mg/kg oleocanthal, NMR, урожай Sep-2025; текущий продавец показывает Add to Cart. Но цена экстремальная. citeturn22view1 |
| **Лучший португальский premium/process** | **Olival da Risca Reserva da Família Organic 500 ml** | Урожай 2025/26, Demeter+organic, Cobrançosa/Galega/Verdeal, исключение кислорода на мельнице, фильтрация, стекло; €23,50. Полифенолы числом не опубликованы. citeturn20view0 |
| **Лучший value с явно указанным урожаем** | **Rosmaninho Gourmet Cobrançosa DOP 500 ml** | Урожай 2025/26, DOP Trás-os-Montes, monovarietal Cobrançosa, €13/500 ml, BBD 12/2027. Есть заявление о высоких полифенолах, но нет числа/COA. citeturn19view1 |
| **Сильный ранний португальский organic** | **Olmais Biológico 500 ml** | Урожай 2025/26, ранний сбор, 90% Cobrançosa, organic, холодная экстракция, €16; есть недатированные технические показатели качества, но нет текущего polyphenol COA. citeturn20view3turn19view3 |

Я использовал следующий порядок приоритета: **анализ конкретной партии/урожая и метод → свежесть → технология и защита от окисления → физико-химическое качество → упаковка → цена/value → награды/organic как вторичные признаки**. Organic, DOP, медаль или выраженная горечь сами по себе не являются измерением полифенолов.

Есть ещё одно важное ограничение: даже хороший COA от октября 2025 — это **снимок анализированного образца в момент анализа, а не гарантия концентрации в бутылке в октябре 2026**. Окисление, свет, тепло, кислород и длительность хранения уменьшают качество и содержание части фенольных соединений; IOC прямо рассматривает кислород, свет и тепло как основные факторы деградации масла. citeturn29view3turn28search15

## Сравнение кандидатов

Обозначения в таблице:

**COA** — лабораторный сертификат конкретного урожая/образца.  
**P** — producer/retailer claim или техкарта без доказанной привязки к текущей партии.  
**MAX** — нормативный максимум/«reference value», а **не измеренное значение** бутылки.  
**н/д** — релевантных опубликованных данных конкретной партии я не нашёл.  
Разные методы полифенолов **не сводятся в одну шкалу**; особенно нельзя механически сравнивать Folin, IOC-HPLC и NMR. IOC сам показывает, что даже две HPLC-процедуры могут систематически давать разные величины из-за экстракции, стандартов и response factors. citeturn29view2turn24search25

| Бренд / конкретное масло | Урожай, регион, сорта | Полифенолы и профиль | Классические показатели качества | Процесс, упаковка, вкус | Цена и доступность на 28.10.2026 |
|---|---|---|---|---|---|
| **Sparta Medicinal Wild Olive Oil Limited White Label, 250 ml** | Sep-2025; Laconia, Greece; organic wild olive | **3057 mg/kg total phenolics**, **oleocanthal 2126 mg/kg**, NMR, University of Crete, 30.09.2025. **Lab result quoted by seller**; полного qualifying hydroxytyrosol+derivatives sum в доступном описании нет, поэтому EU claim из одного total не вывожу. citeturn22view1 | FFA/PV/K232/K270/ΔK: н/д | Очень high-phenolic finishing oil; 250 ml | **€335**, то есть **€1340/L**; seller показывает Add to Cart и worldwide delivery. citeturn22view1 |
| **Drop of Life Healthy Limited Reserve, 500 ml** | Harvest Sep-2025; production 22.09.2025; Olympia variety; Greece | **COA:** total analyzed 2162; total tyrosol derivatives 1221; total hydroxytyrosol derivatives 941; free tyrosol 10; **oleocanthal 234; oleacein 209 mg/kg**. Analysis 10.10.2025, certificate C2526-00092 issued 27.11.2025. Seller identifies method as NMR/NKUA. **43,25 mg hydroxytyrosol, tyrosol or derivatives /20 g**. citeturn23view1turn22view0 | COA фенольный; FFA/PV/K не приведены | Organic, cold extraction; numbered gift package; robust green/bitter profile | **€255/500 ml = €510/L**, in stock, product page says free shipping and worldwide DHL/FedEx. citeturn22view0 |
| **Olival da Risca Reserva da Família Organic, 500 ml** | **2025/26**, Serpa; Cobrançosa, Galega Vulgar, Verdeal | Числовых polyphenol data текущего урожая: **н/д** | н/д | Organic + Demeter; собственная мельница; extraction with **oxidation exclusion**; **filtered**, стеклянная бутылка + коробка; medium green fruity. citeturn20view0 | **€23,50 = €47/L**, Add to Cart. LOA доставляет в Portugal Continental, бесплатно при заказе >€99. citeturn20view0 |
| **Rosmaninho Gourmet Cobrançosa DOP, 500 ml** | **2025/26**; Valpaços, DOP Trás-os-Montes; 100% Cobrançosa | Продавец говорит «alto nível de polifenóis», но **mg/kg, метод и COA отсутствуют** → P, не измерение. citeturn19view1 | Бренд Rosmaninho публикует около 0,2% acidity для линии, но это не идентифицированный COA этой бутылки/партии → P. citeturn12search5 | Быстрая доставка оливок на мельницу, холодная экстракция; medium green fruity | **€13/500 ml = €26/L**; Add to Cart; BBD **12/2027**; доставка Continental PT. citeturn19view1 |
| **Olmais Biológico, 500 ml** | **2025/26**, Vila Flor/Terra Quente; 90% Cobrançosa, 5% Verdeal, 5% Madural | Текущих mg/kg: **н/д** | Сторонний retailer публикует «lab test results»: FFA **0,2%**, peroxide **<15 mEq O₂/kg**, K232 **<2,00**, K268 **<0,20**, ΔK **<0,01**. **Дата/лот не указаны**, поэтому это P, не COA урожая 2025/26. citeturn19view3 | Organic, early harvest, cold extracted, **unfiltered**; чёрное стекло; интенсивный фруктовый, выраженная горечь/перечность. citeturn19view3turn20view3 | **€16/500 ml = €32/L**, Add to Cart на LOA. citeturn20view3 |
| **Acushla Limited Bio DOP, 500 ml** | Текущий harvest year не опубликован; Trás-os-Montes; organic/DOP | Текущих polyphenol mg/kg: **н/д** | Страница продукта: acidity **0,1%**, peroxide **5 mEq O₂/kg**. Нет даты анализа/COA → **P**, не считаю значениями текущего лота. citeturn20view2 | Centenary grove; medium fruity, slightly stronger bitter/pungent than classic; shelf-life claim 2 y after packing. citeturn20view2 | **€28/500 ml = €56/L**, Add to Cart; доставка PT Continental. citeturn20view2 |
| **Esporão Cobrançosa Extra Virgin, 500 ml** | **Campaign 2025**, harvest starts Oct; Alentejo/Reguengos; Cobrançosa | Текущих polyphenol mg/kg: н/д | **Acidity max 0,2%** — это спецификация, не измерение партии | Cold extraction max **24°C**, сразу filtered/packed; green banana/herbal profile, balanced bitter/pungent. citeturn2search1 | Exact Cobrançosa 500 ml был показан **28.10.2026 по €11,59 = €23,18/L**, available через El Corte Inglés. citeturn27search0 |
| **CARM Grande Escolha Bio, 500 ml** | Current harvest year на live shop не обозначен | Polyphenols текущего лота: н/д | Найденные техлисты в индексе относятся к старым годам; переносить на 2026 нельзя | Organic premium EVOO; live manufacturer shop | **€13,45 = €26,90/L** в магазине CARM. citeturn3search0turn3search5 |
| **Monterosa Premium Maçanilha, 500 ml** | Точный current harvest не указан | Polyphenols: н/д | FFA/PV/K текущей партии: н/д | Monovarietal premium line; текущая карточка продажи | **€23 = €46/L**; вариант Maçanilha показывался доступным, тогда как некоторые другие Monterosa были sold out. citeturn5search0turn20view2 |
| **Casa Relvas Azeite Virgem Extra, 500 ml — именно generic SKU** | Alentejo. PT retailer не публикует урожай/сорт; отдельная иностранная карточка generic label указывает Cobrançosa + Sikitita, но я не считаю это подтверждением конкретной PT партии | **н/д** по total phenols, HT/Tyr, oleocanthal/oleacein | **н/д для exact SKU** | 500 ml; exact Portuguese SKU ref/EAN **id_a6fb3093** | eWine показывает **12 шт. stock** на exact 500 ml SKU; публичная цена на странице не отображается. citeturn19view2turn5search2 |
| **Quinta de Lemos Galega, 500 ml** | Silgueiros/Viseu, Dão; Galega | Current-lot polyphenols: н/д | Производитель пишет, что его масла имеют очень низкую acidity в диапазоне **0,09–0,12%**, но это характеристика линейки, не current-batch COA конкретной Galega. citeturn27search4 | Cold mechanical extraction | Retailer показывает **€20,67/500 ml = €41,34/L**, Add to cart; год розлива может отличаться от изображения. citeturn27search1 |
| **Casa Anadia Private Collection / Galega Tributo, 500 ml** | «last olive campaign»; Private Collection Cobrançosa+Picual; Tributo = Galega | Polyphenols: н/д | Для некоторых линий публикуются **max** acidity 0,3%, PV≤20, K232≤2,50, K270≤0,22, ΔK≤0,01 — спецификации, **не lot measurements**. citeturn3search10 | Быстрая переработка; unfiltered; у Galega delicate bitter/pepper profile. citeturn3search6 | Pack 4×500 ml **€37,74** ≈ €9,44/bottle / €18,87/L, но проверенные страницы показывали **Notify Me / out of stock**. citeturn3search8turn3search12 |
| **Oliveira da Serra Lagar do Marmelo / O Lagar, 500 ml** | Current harvest на consumer page не опубликован | Current polyphenols: н/д | Current COA: н/д | Medium/intense green profile, banana peel/apple/grass, subtle bitter and medium pungency. citeturn11search0 | Price tracker показывал **€11,89/500 ml = €23,78/L**, но запись была ~39 дней старой, поэтому **не считаю цену live 28.10**. citeturn27search8 |
| **Gallo Reserva** | Current harvest/cultivar data не опубликованы на доступной consumer page | Current polyphenols: н/д | Current COA: н/д | Brand describes Reserva as intense, rich, persistent, with bitter/pungent/fruity profile; это сенсорика, не доказательство фенолов. citeturn11search1turn11search3 | Current exact Reserva price/lot не удалось верифицировать достаточно надёжно; массовые Gallo SKU широко доступны, но я не заменял Reserva другим SKU ради красивой цены |
| **Herdade dos Lagos EVOO** | Portugal; organic EVOO фигурирует в producer/B2B portfolio | По конкретной актуальной retail bottle: н/д | н/д | Consumer SKU с прозрачным current-lot dossier не найден | Подтвердить конкретную бутылку, цену и live delivery в Portugal Continental из проверяемого consumer checkout не удалось; поэтому исключён из рейтинга. citeturn12search15 |

**Витамин E и сквален:** для перечисленных **текущих 2025/26 retail-партий** я не нашёл надёжных lot-specific количественных данных, которые можно было бы честно поставить в сравнительную таблицу. В частности, фенольный COA Drop of Life не измеряет витамин E или сквален. Поэтому я не подставлял ни типовые значения EVOO, ни старые данные брендов.

Отдельно я проверил **PhenOLIV Organic** как high-phenolic benchmark. Его COA урожая October 2025 действительно очень сильный: 2011 mg/kg analyzed polyphenols, oleocanthal 180, oleacein 177, total tyrosol derivatives 1195, total hydroxytyrosol derivatives 816, free tyrosol 10 mg/kg; сертификат сообщает **40,22 mg hydroxytyrosol, tyrosol or derivatives на 20 g**. Но текущая розничная карточка у TheOlivest отмечена **Sold Out**, а Gourmet Groceries показывал bulk pack как pre-order, поэтому в список реально покупаемых пяти бутылок я его не включаю. citeturn23view0turn21search3

## Пять лучших бутылок с покупкой

**Drop of Life Healthy Limited Reserve 500 ml — мой лучший общий выбор при приоритете доказанной химии.**  
Главное преимущество — не просто огромная цифра «total polyphenols», а полный профиль конкретного урожая: oleocanthal 234, oleacein 209, tyrosol derivatives 1221, hydroxytyrosol derivatives 941 mg/kg и непосредственно рассчитанные лабораторией 43,25 mg qualifying compounds/20 g. Сертификат относится к образцу урожая September 2025; анализ 10 October 2025. Это наиболее содержательный COA среди доступных сегодня бутылок. citeturn23view1turn22view0

Цена — **€255/500 ml, €510/L**. Это чудовищно дорого как пищевое масло, но значительно рациональнее Sparta, если критерий — «сколько хорошо документированных фенолов я получаю за евро». Текущая карточка показывает **In stock (can be backordered)** и free shipping; продавец заявляет DHL/FedEx worldwide и Europe 1–2 days. citeturn22view0

Прямая покупка:  
`https://gourmetgroceries.com/product/drop-of-life-healthy-evoo-limited-edition-500ml/`

**Sparta Medicinal Wild Olive Oil Limited White Label Organic 250 ml — максимум измеренной концентрации.**  
Seller приводит **3057 mg/kg total phenolics** и **2126 mg/kg oleocanthal**, NMR, University of Crete, 30 September 2025; harvest September 2025. Это количественно выше Drop of Life и особенно экстремально по oleocanthal. Но доступный мне источник не даёт полного hydroxytyrosol+tyrosol derivatives sum, поэтому я **не превращаю 3057 mg/kg total в заключение по EU 432/2012**. citeturn22view1

Цена — **€335/250 ml = €1340/L**. То есть цена за литр примерно в 2,6 раза выше Drop of Life, а total-NMR фенолы выше примерно в 1,4 раза. Поэтому для человека, которому нужна не абсолютная максимизация oleocanthal, а разумный antioxidant/value, Drop of Life логичнее.

Страница, на которую сам продавец направляет для актуальной Limited medicinal wild EVOO:  
`https://gourmetgroceries.com/product/sparta-limited-edition-medicinal-organic-wild-evoo-250ml/`

Текущий каталог продавца показывает White Label **Add to Cart за €335** и worldwide delivery. citeturn22view1

**Olival da Risca Reserva da Família Organic 500 ml — мой лучший португальский premium сегодня.**  
Здесь нет polyphenol COA, поэтому химически я не ставлю его в один ряд с двумя маслами выше. Зато очень хороша совокупность факторов, реально влияющих на сохранность масла: явно обозначенный **урожай 2025/26**, собственные organic+biodynamic olives, Demeter, технологическое **исключение кислорода** при производстве, фильтрация перед отправкой, стеклянная бутылка и сорта Cobrançosa/Galega Vulgar/Verdeal. citeturn20view0

Цена **€23,50/500 ml = €47/L**. LOA прямо обслуживает Portugal Continental и даёт бесплатную доставку при заказе свыше €99. citeturn20view0

Прямая покупка:  
`https://en.loa.pt/product-page/azeite-ve-olival-da-risca-reserva-de-fam%C3%ADlia`

Есть ещё более свежий **Primeur 2026/27**, собранный в начале октября 2026, но на 28 октября он только pre-order с отправкой 9 ноября; поэтому я его намеренно не называю сегодняшним победителем. citeturn19view0

**Rosmaninho Gourmet Cobrançosa DOP 500 ml — лучший practical value.**  
За **€13** получаем точный harvest **2025/26**, monovarietal Cobrançosa, DOP Trás-os-Montes, BBD 12/2027 и прямой португальский checkout. Продавец говорит о высоком содержании полифенолов, но без mg/kg и метода это остаётся маркетингово-техническим утверждением, а не аналитическим доказательством. citeturn19view1

Тем не менее €26/L при явном урожае и хорошей traceability — сильнее, чем многие более дорогие premium bottles, у которых даже год урожая не указан.

Прямая покупка:  
`https://www.loa.pt/product-page/azeite-ve-rosmaninho-gourmet-cobran%C3%A7osa`

**Olmais Biológico 500 ml — лучший выбор для любителя раннего, мощного португальского профиля.**  
LOA сейчас указывает **harvest 2025/26**, €16/500 ml. Масло organic, cold extracted, unfiltered, с 90% Cobrançosa + 5% Verdeal + 5% Madural. Другая актуальная карточка бренда описывает ранний сбор и приводит FFA 0,2%, peroxide <15, K232<2,00, K268<0,20 и ΔK<0,01, но поскольку дата лабораторных результатов не дана, я **не приписываю эти цифры текущему урожаю 2025/26**. citeturn20view3turn19view3

Из-за того, что это unfiltered oil урожая прошлого сезона, лично я сейчас не покупал бы его ящиком: взял бы одну 500-ml бутылку и использовал достаточно быстро.

Прямая покупка:  
`https://www.loa.pt/product-page/azeite-ve-olmais-biol%C3%B3gico-500ml`

Все цены LOA выше указаны без предположения о стоимости доставки одной бутылки; магазин прямо обещает бесплатную доставку в Portugal Continental только при заказе **>€99**. citeturn19view1turn20view0

## Casa Relvas: отдельная проверка нужной бутылки

Здесь особенно важно не смешивать три разных продукта.

Искомая бутылка — **Casa Relvas Azeite Virgem Extra 500 ml**, generic Casa Relvas EVOO. В португальском eWine находится именно такой текущий SKU:

**EAN/ref: id_a6fb3093**  
**Marca: CASA RELVAS**  
**Região: ALENTEJO**  
**Volume: 0,500 L**  
**Stock на момент проверки: 12 unidades.** citeturn19view2

Прямая карточка:  
`https://ewine.pt/product/azeite-casa-relvasl-gf-500ml-un`

Публичная страница eWine **не показывает цену**, поэтому я не буду выдумывать её или брать цену другого Casa Relvas. Отдельная иностранная карточка именно generic **Casa Relvas Azeite Virgem Extra** описывает бутылки 500 ml из Alentejo и указывает Cobrançosa + Sikitita; однако без matching lot/EAN я рассматриваю сорта только как вторичное retailer claim, а не как подтверждённый состав сегодняшних 12 бутылок eWine. citeturn5search2

Что удалось подтвердить для exact generic Casa Relvas:

| Параметр | Что известно |
|---|---|
| Total polyphenols | **не опубликованы** |
| Метод / дата polyphenol assay | **нет** |
| Hydroxytyrosol/tyrosol derivatives | **нет данных** |
| Oleocanthal / oleacein | **нет данных** |
| Vitamin E / squalene | **нет current-lot данных** |
| Free acidity | **нет достоверного exact-SKU current value** |
| Peroxide / K232 / K270 / ΔK | **нет exact-SKU current values** |
| Current harvest year | **не опубликован** |
| Portugal availability | **да, 12×500 ml на проверенной PT странице** |
| Цена | **публично не показана** |

Поэтому с точки зрения задачи «максимум доказанных антиоксидантов» Casa Relvas сегодня **не попадает в топ**. Это не означает плохое масло; это означает слабую публичную аналитическую прозрачность.

Почему нельзя подставлять данные **Segredos de São Miguel Grande Escolha**: актуальная техническая карта Casa Relvas для этого **другого продукта** явно говорит **harvest 2025–2026**, сорта **Arbequina + Arbosana**, acidity **0,4%**, peroxide **20 max**, K232 **2,50 max**, K270 **0,22 max**. И внизу технического листа прямо стоит пометка, что это **«valores de referência»**. То есть даже внутри Segredos эти числа — reference/spec limits, а не COA партии; и тем более они не относятся к generic Casa Relvas 500 ml. citeturn23view2

То же касается **Art.Terra** — ещё одной отдельной линейки Casa Relvas. В её sheet указаны harvest 2025–2026, Koroneiki+Cobrançosa, acidity 0,2%, peroxide max 20, K232 max 2,50, K270 max 0,22, также с пометкой reference values. Эти данные также нельзя переносить на нужную вам generic bottle. citeturn23view3

**Итог по Casa Relvas:** я бы считал его нормальным кандидатом для вкусовой покупки при хорошей цене, но **не покупкой, обоснованной антиоксидантами**, пока exact SKU не публикует harvest date + lot-specific phenolic analysis. Главное достоинство сейчас — реальная доступность 500 ml в Portugal; главный недостаток — почти нулевая прозрачность по нужным вам биохимическим параметрам. citeturn19view2

## Нормативы и почему цифры полифенолов нельзя смешивать

Для **extra virgin olive oil** действующий IOC Trade Standard Rev.22/2026 устанавливает верхний предел free acidity **0,80%**, peroxide value **20 mEq active O₂/kg**, K270 **0,22**, ΔK **0,01** и, где применяется, K232 **2,50**. Это **границы категории**, а не доказательство exceptional quality: значение «≤20 peroxide» в техкарте означает лишь обещание соответствовать максимуму, а не фактические 20 или фактические 5. citeturn25view0turn29view0turn29view1

Именно поэтому я не трактую Casa Relvas «PV 20 max» или Casa Anadia «K232 ≤2,50» как результаты лаборатории. Настоящее измерение должно содержать хотя бы идентификацию образца/партии, дату анализа и фактическое полученное значение.

С полифенолами ситуация ещё сложнее. Действующая разрешённая формулировка EU Regulation 432/2012 относится к утверждению, что **olive-oil polyphenols contribute to protection of blood lipids from oxidative stress**, и допускается для масла, содержащего не менее **5 mg hydroxytyrosol and its derivatives — включая, например, oleuropein complex и tyrosol — на 20 g масла**. citeturn24search15turn24search7

Математически 5 mg/20 g соответствует 250 mg/kg. Но критически важна вторая половина определения: это должны быть **правильно определённые hydroxytyrosol/tyrosol-related compounds**, а не любые вещества, которые какой-то Folin assay назвал «total polyphenols». Поэтому:

**«Total polyphenols = 250 mg/kg» ≠ автоматически EU health claim.**

Для Drop of Life ситуация сильнее: сам COA не просто сообщает total = 2162 mg/kg, а отдельно даёт **total tyrosol derivatives 1221 + total hydroxytyrosol derivatives 941 mg/kg** и непосредственно сообщает **43,25 mg/20 g** соответствующих производных. Это примерно в **8,65 раза** выше порога 5 mg/20 g на момент анализа. citeturn23view1

У Sparta есть phenomenal total-NMR 3057 mg/kg и oleocanthal 2126 mg/kg, но доступная retail documentation не даёт мне такого же полного qualifying sum; поэтому я сознательно не пишу «12× EU threshold» из одной цифры total. citeturn22view1

IOC в документе о методах определения фенолов отдельно подчёркивает, что разные способы экстракции и количественного анализа дают различающиеся результаты; один из методов может недооценивать flavonoids и ligustrosides, а более новый SPE/HPLC-DAD использует response factors для отдельных соединений и позволяет определять individual phenols, включая oleocanthal/oleacein. citeturn29view2 Систематическое сравнение Folin-Ciocalteu, IOC method и специфических LC/MS/HPLC подходов также показывает, что это аналитически разные способы измерения, а не взаимозаменяемые «термометры полифенолов». citeturn24search25

Именно поэтому в этом отчёте я не ранжировал условные «600 mg/kg Folin» выше или ниже «500 mg/kg NMR» как будто методы одинаковы.

## Что реально доказано для здоровья, как хранить и готовить

Наиболее аккуратное утверждение о пользе — то, которое разрешено самой EU: достаточное количество соответствующих olive-oil polyphenols помогает **защищать липиды крови от окислительного стресса**. Это не утверждение о лечении атеросклероза, воспалительных заболеваний, деменции или рака. citeturn24search7

Классический EUROLIVE randomized crossover trial включал 200 здоровых мужчин и сравнивал масла с различным содержанием фенолов. Авторы обнаружили, что фенольная часть масла давала дополнительные эффекты на показатели окислительного повреждения липидов и липопротеинов по сравнению с объяснением только мононенасыщенным жиром. Это хорошо согласуется с легальным EU claim, но не превращает high-phenolic EVOO в лекарство. citeturn28search0turn28search8

Более поздний метаанализ контролируемых исследований high-phenol против low-phenol olive oil сообщил благоприятные изменения некоторых маркеров, включая ox-LDL и MDA, но эффекты неодинаковы по всем исходам и не являются доказательством клинического лечения заболеваний. citeturn28search24

Практически это означает: ради здоровья гораздо важнее регулярно использовать качественный EVOO вместо менее благоприятных жиров в адекватном рационе, чем охотиться за рекордным oleocanthal за €1340/L. High-phenolic COA полезен, когда цель именно **стандартизировать фенольную экспозицию**, но соотношение цена/доказательность быстро становится плохим после уровня Drop/Risca.

Для хранения IOC рекомендует минимизировать три главных врага — **oxygen, light и heat**. Масло должно оставаться плотно закрытым, в прохладном тёмном месте, вдали от духовки/плиты и солнечного света. IOC отдельно отмечает, что скорость окисления зависит от исходного качества, технологии, упаковки и условий хранения. citeturn29view3

Поэтому для домашнего использования я предпочитаю:

- непрозрачную/тёмную бутылку или металлическую упаковку вместо прозрачного стекла;
- 250–500 ml для дорогого high-phenolic масла, если оно расходуется медленно;
- не держать дорогую бутылку открытой месяцами ради «экономии»;
- не использовать открытый декоративный pourer постоянно;
- не хранить рядом с плитой.

Нагревать EVOO **можно**; проблема «никогда не готовить на EVOO» слишком примитивна. Но нагрев действительно изменяет фенольный профиль и уменьшает часть антиоксидантов. Исследования domestic cooking показывают заметную деградацию ряда фенольных соединений с температурой и временем. citeturn28search22turn28search6 Из этого следует практический, а не медицинский вывод: **масло за €255–335 с лабораторно измеренным oleocanthal рациональнее употреблять сырым/как finishing oil**, а для тушения, sauté и обычного приготовления использовать хорошее, но гораздо более дешёвое EVOO вроде Rosmaninho, Esporão или CARM. Платить за 2000–3000 mg/kg NMR, а затем специально уничтожать часть этих соединений длительным нагревом — экономически бессмысленно.

## Что я бы купил лично и где остаются пробелы

Для ежедневной кухни в Португалии мой выбор сейчас — **Rosmaninho Gourmet Cobrançosa DOP 500 ml за €13**. Причина не в недоказанном обещании «high polyphenols», а в сочетании конкретного урожая 2025/26, DOP, mono-Cobrançosa, прямой доступности и цены €26/L. Это лучший risk-adjusted value из исследованного набора. citeturn19view1

Для более дорогой португальской бутылки я бы взял **Olival da Risca Reserva da Família 500 ml**. Исключение кислорода при производстве, фильтрация, organic/Demeter и явный урожай дают мне больше оснований доверять сохранности, чем многочисленные награды без COA. citeturn20view0

Если задача сформулирована именно как **«хочу измеряемую фенольную экспозицию, а бюджет вторичен»**, я бы взял **Drop of Life 500 ml**, а не Sparta. Drop менее экстремален по абсолютной концентрации, но имеет существенно более полный COA, explicit hydroxytyrosol/tyrosol derivative data, oleocanthal+oleacein и значительно менее безумную цену на литр. citeturn23view1turn22view0

**Sparta** я бы покупал только для специфической цели — максимизировать именно аналитически измеренный oleocanthal/total NMR вне зависимости от цены. При **€1340/L** это уже скорее аналитический luxury/N=1-продукт, чем рациональная food purchase. citeturn22view1

**Esporão Cobrançosa** — потенциально лучший mainstream-premium value: current price около **€11,59/500 ml**, explicit 2025 campaign, cold extraction ≤24°C, immediate filtration/packaging. Он не вошёл в главную пятёрку исключительно из-за отсутствия current-lot phenolic assay и менее чистой цепочки «official current bottle → direct specialist checkout», а не из-за признаков плохого качества. citeturn2search1turn27search0

**Acushla Limited** очень достойно выглядит по заявленным acidity 0,1% и peroxide 5, но без даты анализа и harvest year €56/L трудно оправдать относительно Risca/Rosmaninho, если цель — доказательность, а не бренд/сенсорика. citeturn20view2

**Casa Relvas generic 500 ml** я бы покупал только по вкусу/цене, не ради заявленной «антиоксидантности»: exact SKU есть в наличии, но current harvest, phenol COA и даже фактическая acidity конкретной партии публично отсутствуют. И данные Segredos de São Miguel Grande Escolha к нему применять нельзя. citeturn19view2turn23view2

Самый большой пробел всего португальского premium-сегмента — не качество масел, а **аналитическая прозрачность**. У производителей часто великолепно описаны terroir, DOP, cold extraction, awards и acidity, но практически отсутствуют downloadable lot COA с date/sample ID, IOC-HPLC или валидированным individual-phenol assay. Для пользователя, который действительно выбирает по hydroxytyrosol derivatives / oleocanthal, это принципиальная разница.

И ещё один temporal caveat: на **28 октября 2026** покупать большие запасы high-phenolic урожая Sep–Oct 2025 уже не оптимально. По мере выхода настоящего урожая 2026/27 приоритет должен быстро перейти к бутылкам с harvest Oct/Nov-2026 и новым COA, а не к прошлогодним рекордным цифрам. Это особенно видно на Risca Primeur: новый урожай уже произведён, но 28 октября ещё не отгружается. citeturn19view0turn29view3

## Источниковая база

| Источник | Что использовано |
|---|---|
| **EUR-Lex, Regulation EU 432/2012, consolidated 2025** citeturn24search15turn24search7 | Точный критерий 5 mg hydroxytyrosol+derivatives/20 g и разрешённый health claim |
| **International Olive Council — Standards, Methods and Guides** citeturn25view0 | Актуальность Trade Standard Rev.22/2026 и методов |
| **IOC Trade Standard Rev.22/2026** citeturn29view0turn29view1 | EVOO: acidity, peroxide, K270, K232, ΔK и органолептические критерии |
| **IOC COI/T.20/Doc.29 Rev.2** citeturn29view2 | Почему методы определения фенолов могут давать разные результаты; HPLC-DAD/SPE |
| **IOC Consumer Storage Guidelines** citeturn29view3 | Кислород, свет, тепло и хранение |
| **Olmo-García et al., comparison of phenolic methods** citeturn24search25 | Folin/IOC/LC-based методы не эквивалентны |
| **Covas et al., Ann Intern Med, EUROLIVE RCT** citeturn28search0turn28search8 | Human RCT по high- vs low-phenol olive oil |
| **2023 meta-analysis of olive-oil phenols** citeturn28search24 | Ox-LDL/MDA и границы доказательности |
| **Ramírez-Anaya et al., cooking study** citeturn28search22turn28search6 | Изменение фенольного профиля EVOO при нагреве |
| **World Olive Center for Health — Drop of Life COA C2526-00092** citeturn23view1 | Полный индивидуальный phenolic profile урожая 2025 |
| **Gourmet Groceries — Drop of Life current SKU** citeturn22view0 | €255, stock, shipment, harvest, retail status |
| **Gourmet Groceries — high-phenolic bundle / Sparta data** citeturn22view1 | Sparta 3057 mg/kg, oleocanthal 2126, NMR/date, current price/status |
| **World Olive Center for Health — PhenOLIV COA C2526-00142** citeturn23view0 | 2011 mg/kg и полный derivative profile benchmark |
| **LOA — Olival da Risca Reserva da Família** citeturn20view0 | Harvest 2025/26, сорта, Demeter, oxidation exclusion, €23,50 |
| **LOA — Olival da Risca Primeur** citeturn19view0 | Harvest 2026/27, Oct-2026, preorder/ship 9 Nov |
| **LOA — Rosmaninho Gourmet Cobrançosa** citeturn19view1 | Harvest 2025/26, DOP, BBD, €13 |
| **LOA — Olmais Biológico** citeturn20view3 | Harvest 2025/26, varietal proportions, price |
| **Loja Portuguez — Olmais technical data** citeturn19view3 | Early harvest, packaging, undated FFA/PV/K values |
| **LOA — Acushla Limited Bio DOP** citeturn20view2 | Current SKU, price, acidity/PV claims |
| **Esporão official — Cobrançosa EVOO** citeturn2search1 | Campaign 2025, extraction temperature, filtration, max acidity |
| **CARM official shop** citeturn3search0turn3search5 | Current 500-ml prices |
| **Casa Relvas exact PT SKU — eWine** citeturn19view2 | Generic Casa Relvas 500 ml, EAN, Alentejo, stock |
| **Casa Relvas official — Segredos de São Miguel sheet** citeturn23view2 | Доказательство, что это отдельный product и показатели reference/max |
| **Casa Relvas official — Art.Terra sheet** citeturn23view3 | Вторая отдельная линейка; нельзя переносить данные на generic SKU |
| **Quinta de Lemos official / current retailer** citeturn27search4turn27search1 | Acidity claim линейки и текущая Galega 500-ml price |

**Итоговый выбор на 28.10.2026:** для максимальной аналитической доказательности — **Drop of Life Limited**; для абсолютного рекорда по измеренным NMR-фенолам — **Sparta White Label**; из португальских — **Risca Grande Reserva da Família**; по value — **Rosmaninho Gourmet Cobrançosa**; для мощного organic/early-harvest профиля — **Olmais Biológico**. **Casa Relvas Azeite Virgem Extra 500 ml** подтверждён как реально имеющийся PT SKU, но из-за отсутствия harvest-specific COA его нельзя честно ставить рядом с лидерами по антиоксидантной доказательности.

---

**Claude:**

{"lang":"ru","topic":"Оливковое масло в Португалии: полифенолы, качество, свежесть и покупка (октябрь 2026)","one_line":"Какое оливковое масло extra virgin в Португалии на 28.10.2026 лучше всего по доказанным антиоксидантам, свежести и цене, и что реально можно купить.","key_findings":["Рынок премиального EVOO делится на две категории. У греческих high-phenolic масел есть COA конкретного урожая (олеокантал, олеацеин, производные гидрокситирозола и тирозола), но они на порядок дороже. У большинства португальских масел есть данные об урожае, сортах, DOP/organic и сенсорике, но нет опубликованного COA с полифенолами для текущей партии. Низкий рейтинг португальских масел значит слабую доказательную базу по бутылке, а не худшую химию.","Drop of Life Healthy Limited Reserve 500 ml (Греция, урожай Sep-2025) лучший по аналитике. Всего 2162 мг/кг фенолов, производные гидрокситирозола 941, производные тирозола 1221, олеокантал 234, олеацеин 209 мг/кг. 43,25 мг производных на 20 г при пороге EU 5 мг (примерно в 8,65 раза выше). Цена €255 за 500 ml (€510/л), в наличии.","Sparta Medicinal Wild Olive Oil 250 ml даёт максимум измеренного: 3057 мг/кг total phenolics и 2126 мг/кг олеокантала (NMR, Univ. of Crete, 30.09.2025). Цена €335 за 250 ml (€1340/л), то есть в 2,6 раза дороже за литр Drop of Life при фенолах выше примерно в 1,4 раза. Полной суммы производных гидрокситирозола и тирозола нет, поэтому соответствие EU-claim из одной цифры не выводится.","Лучшие португальские: Olival da Risca Reserva da Família Organic 500 ml (€23,50; урожай 2025/26, Demeter, исключение кислорода, фильтрация), Rosmaninho Gourmet Cobrançosa DOP 500 ml (€13, урожай 2025/26, BBD 12/2027, лучший value, €26/л), Olmais Biológico 500 ml (€16, ранний сбор, 90% Cobrançosa, нефильтрованное). Полифенолы числом у всех не опубликованы, утверждения о высоком содержании остаются маркетингом.","Casa Relvas Azeite Virgem Extra 500 ml (EAN id_a6fb3093) есть в PT eWine, 12 шт., цена не показана. Урожай, COA на фенолы и фактические кислотность и перекись не опубликованы, поэтому по антиоксидантам в топ не попадает. Данные Segredos de São Miguel (Arbequina+Arbosana, acidity 0,4%) и Art.Terra переносить на него нельзя. Это reference/max-значения техкарт, а не измерения партии.","Нормативные максимумы (IOC Rev.22/2026: acidity 0,8%, peroxide ≤20, K270 0,22, ΔK 0,01, K232 2,50) и «max»-цифры в техкартах не измерения партии. Claim EU 432/2012 требует ≥5 мг гидрокситирозола и производных на 20 г (250 мг/кг), считая правильные соединения, а не любой Folin total. Методы Folin, IOC-HPLC и NMR не сводятся в одну шкалу.","Доказанная польза ограничена разрешённым EU-claim (защита липидов крови от окислительного стресса). Подтверждают EUROLIVE RCT (200 мужчин) и метаанализ по ox-LDL и MDA, лечебного эффекта нет. Важнее регулярно использовать качественное EVOO, чем гнаться за рекордным олеоканталом за €1340/л.","Хранение: главные враги масла кислород, свет и тепло (IOC). Нужны тёмная бутылка или металл, небольшой объём для дорогого масла, подальше от плиты. Нагрев снижает часть фенолов, поэтому дорогое high-phenolic масло лучше сырым (finishing), а для готовки брать дешёвое EVOO вроде Rosmaninho, Esporão или CARM.","Свежесть: урожай 2026/27 начался (Olival da Risca Primeur 2026/27, €9,50 за 250 ml, предзаказ, отправка 9.11.2026), но COA нового урожая в рознице ещё нет. Крупные запасы масла урожая Sep–Oct 2025 покупать уже не оптимально, COA — снимок образца, а не гарантия содержания в бутылке через год.","Esporão Cobrançosa 500 ml (кампания 2025, холодная экстракция ≤24°C) около €11,59 (€23,18/л), потенциально лучший mainstream-value, но без COA на фенолы. PhenOLIV Organic (COA Oct-2025: 2011 мг/кг, олеокантал 180, олеацеин 177, 40,22 мг/20 г) распродан или предзаказ, в топ не вошёл. Для витамина E и сквалена надёжных данных по партиям нет."],"recommendations":["Для максимальной доказанной химии при вторичном бюджете брать Drop of Life Limited Reserve 500 ml. Sparta покупать только для цели максимизировать именно измеренный олеокантал независимо от цены.","Для ежедневной кухни в Португалии брать Rosmaninho Gourmet Cobrançosa DOP 500 ml (€13). Из португальских premium выбрать Olival da Risca Reserva da Família 500 ml (€23,50).","Для мощного органик early-harvest профиля взять одну бутылку Olmais Biológico и использовать быстро. Ящиком не покупать из-за нефильтрованности и урожая прошлого сезона.","Дорогие high-phenolic масла (Drop of Life, Sparta) употреблять сырыми, а для тушения и жарки использовать недорогое хорошее EVOO.","Покупать по прозрачным данным: просить у производителя lot COA с датой анализа, ID образца и методом (IOC-HPLC или валидированный individual-phenol assay). Не принимать «max»-цифры техкарты и общие заявления о высоких полифенолах за измерения.","Casa Relvas generic 500 ml покупать только по вкусу и цене, не ради антиоксидантов.","Следить за урожаем 2026/27 (Risca Primeur с 9.11.2026) и переходить на бутылки с harvest Oct/Nov-2026 и новым COA. Малые объёмы хранить в тёмном прохладном месте."],"entities":{"people":[],"companies":["Drop of Life","Sparta","Olival da Risca","Rosmaninho","Olmais","Acushla","Esporão","CARM","Monterosa","Casa Relvas","Quinta de Lemos","Casa Anadia","Oliveira da Serra","Gallo","Herdade dos Lagos","PhenOLIV","LOA","Gourmet Groceries","eWine","TheOlivest","Loja Portuguez","International Olive Council","World Olive Center for Health","University of Crete","El Corte Inglés"],"products_tools":["Drop of Life Healthy Limited Reserve","Sparta Medicinal Wild Olive Oil Limited White Label","Olival da Risca Reserva da Família Organic","Olival da Risca Primeur 2026/27","Rosmaninho Gourmet Cobrançosa DOP","Olmais Biológico","Acushla Limited Bio DOP","Esporão Cobrançosa","CARM Grande Escolha Bio","Casa Relvas Azeite Virgem Extra","Segredos de São Miguel Grande Escolha","Art.Terra","PhenOLIV Organic","EU Regulation 432/2012","IOC Trade Standard Rev.22/2026","EUROLIVE RCT"]},"open_questions":["Нет опубликованных lot-specific COA на полифенолы у португальских масел (Risca, Rosmaninho, Olmais, Esporão и др.). Можно запросить у производителей или заказать независимый анализ.","Не подтверждено, что показатели Drop of Life и Sparta сохраняются в бутылке через год после анализа (COA октября 2025). Для Sparta нет суммы производных гидрокситирозола и тирозола для проверки EU-claim.","Нет надёжных данных по витамину E и сквалену для текущих партий.","Неизвестны цена, урожай и сорта конкретной бутылки Casa Relvas 500 ml на eWine. Состав Cobrançosa+Sikitita подтверждён только иностранной карточкой.","Herdade dos Lagos и Gallo Reserva не подтверждены по цене, партии и доставке. Цена Oliveira da Serra устарела примерно на 39 дней, Casa Anadia показан как out of stock.","Когда появятся COA и розничная доступность урожая 2026/27, включая Risca Primeur после 9.11.2026."],"related_concepts":["полифенолы оливкового масла (олеокантал, олеацеин, гидрокситирозол)","EU Regulation 432/2012 health claim","COA и lot-specific анализ","сравнимость методов Folin, HPLC и NMR","свежесть и хранение масла (кислород, свет, тепло)","IOC стандарты качества EVOO","покупка продуктов в Португалии","нагрев и деградация фенолов"]}
