---
session: s_be6d1831
date: 2026-10-28
words: 2044
turns: 2
tools: "ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · Алиса хочет поехать во Францию, в Париж, в Диснейленд. Нужно спланировать гипотетическую п…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_be6d1831` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Алиса хочет поехать во Францию, в Париж, в Диснейленд. Нужно спланировать гипотетическую поездку из Лиссабона на 3 дня / 2 ночи:

- Вылет из Лиссабона в Париж.
- 2 ночи в районе Диснейленда.
- На 3-й день в обед уехать обратно.
- Продумать трансфер/такси до Диснейленда и обратно.
- Посчитать, сколько стоит остановиться в Диснейленде на 2 ночи.
- Оценить, достаточно ли 2 ночей для поездки.
- Проверить, насколько Диснейленд интересен детям 6 и 9 лет: Алисе [ВОЗРАСТ], Артуру [ВОЗРАСТ].
- Оценить состояние парка и отелей: насколько всё новое, ухоженное, не «убитое».
- Сделать не просто предположение, а глубокое исследование с реальным планом поездки на 3 дня / 2 ночи.

Также нужно добавить альтернативы по Европе:
- тематические парки уровня Диснейленда;
- максимально свежие, новые, качественные;
- доступные из Лиссабона прямым/удобным перелётом до 4 часов.
__Перевела: GPT-5.5 + whisper__

• • • • •

Нужно сделать глубокое исследование и гипотетически спланировать поездку для семьи в Disneyland Paris:

Маршрут: Лиссабон → Париж/Disneyland → Лиссабон.  
Формат: 3 дня / 2 ночи.

Предварительная идея:
- утром прилететь из Лиссабона;
- добраться до Disneyland: такси / трансфер / другой удобный вариант;
- провести 2 ночи в Disneyland;
- на 3-й день уехать обратно примерно в обед.

Нужно выяснить:
- сколько стоит проживание в Disneyland на 2 ночи;
- какой бюджет всей поездки: перелеты, проживание, билеты в парк, трансфер, питание;
- достаточно ли 2 ночей для такой поездки;
- насколько Disneyland Paris интересен детям 6 и 9 лет: Алисе [ВОЗРАСТ], Артуру [ВОЗРАСТ];
- насколько парк свежий, качественный, не «убитый», актуальный по состоянию и впечатлениям;
- какие отели лучше выбрать рядом или внутри Disneyland;
- как оптимально построить программу на 3 дня / 2 ночи.

Также нужно добавить альтернативы по Европе:
- тематические парки уровня Disneyland;
- в радиусе до 4 часов перелета из Лиссабона;
- максимально новые, свежие, качественные;
- подходящие для детей 6 и 9 лет;
- с примерной стоимостью поездки.

Итогом нужно подготовить полноценный план поездки + сравнение альтернатив.
__Перевела: GPT-5.5 + 11labs__

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "Disneyland Paris 2026 World of Frozen Adventure Way Disney Adventure World opening review", "mode": "extended"}

---

> `WebSearch` -- {"query": "Disneyland Paris hotel 2 nights package price 2026 family 2 adults 2 children Disney Hotel New York Newport Bay Sequoia Lodge", "mode": "extended"}

---

> `WebSearch` -- {"query": "Lisbon to Paris Orly CDG flights TAP easyJet Transavia price family flight time; Magical Shuttle Disneyland Paris price 2026; taxi CDG to Disneyland Paris fixed fare", "mode": "extended"}

---

> `WebSearch` -- {"query": "best new theme parks Europe 2026 Europa-Park Rulantica PortAventura Ferrari Land Efteling Phantasialand new rides 2026 families", "mode": "extended"}

---

> `WebSearch` -- {"query": "Disneyland Paris hotels renovation status 2026 Sequoia Lodge Cheyenne Santa Fe Newport Bay Hotel New York Marvel which hotel best newest", "mode": "standard"}

---

> `WebSearch` -- {"query": "Europa-Park 2026 hotel Krønasår price per night family, Basel airport to Rust transfer; Rulantica; Lisbon Basel flight", "mode": "standard"}

---

> `WebSearch` -- {"query": "Disneyland Paris 2026 ticket price 2 day 2 park adult child dated; Disney Adventure World review crowds queues Raiponce Tangled Spin", "mode": "standard"}

---

**Claude:**

# Алиса и Артур в Disneyland Paris: 3 дня / 2 ночи из Лиссабона

**Коротко:** ехать стоит, и сейчас удачное время. Весной 2026 года (29.03) открылась полностью переделанная вторая часть курорта, Disney Adventure World, и в ней World of Frozen. Для детей 6 и 9 лет это попадание. Двух ночей хватает на главное, но день будет плотный; третья ночь сделала бы поездку заметно спокойнее. Семья из 4 человек уложится примерно в 2 300-3 500 € в зависимости от отеля.

## 1. Насколько свежий парк

| Часть курорта | Состояние |
|---|---|
| **Disney Adventure World** (бывшая Walt Disney Studios) | Новое с 29.03.2026: World of Frozen с замком Эльзы на горе высотой 36 м, аттракцион Frozen Ever After, робот-Олаф в натуральный размер, встреча с Анной и Эльзой. Ещё новая аллея Adventure Way с озером, ночным шоу и каруселью «Рапунцель» (Raiponce Tangled Spin). Плюс Avengers Campus (2022) и Worlds of Pixar |
| **Disneyland Park** (главный, с замком) | Большая реставрация прошла к 25-летию в 2017-2019 годах (замок, Big Thunder, Phantom Manor). Состояние хорошее, не «убитое» |
| **Слабое место** | Adventure World остаётся меньшим из двух парков. На Frozen очереди огромные: в день открытия стояли сначала на вход в зону, потом на сам аттракцион |

## 2. Что понравится детям

- **Алисе (6):** Frozen целиком, Peter Pan's Flight, Dumbo, «it's a small world», Рапунцель, Ratatouille, Pirates of the Caribbean, встречи с принцессами. Для неё это сказка в чистом виде.
- **Артуру (9):** Big Thunder Mountain (рост от 102 см), Star Wars Hyperspace Mountain (120 см), Spider-Man W.E.B. Adventure, Avengers Flight Force (120 см), Crush's Coaster (107 см). Indiana Jones требует 140 см, туда он может не пройти.
- ⚠️ **Рост:** если в Алисе меньше 120 см, на Hyperspace и Avengers её не пустят. Перед поездкой измерьте обоих.

**Вердикт:** 6 и 9 лет почти идеальный возраст для Disney. Младшая верит в сказку, старшему хватает горок.

## 3. Отели: какой брать

| Отель | Состояние | Ориентир на 2 ночи с билетами на 3 дня, семья 2+2 | Мнение |
|---|---|---|---|
| [Disneyland Hotel](https://www.google.com/maps/search/?api=1&query=Disneyland+Hotel+Paris) | Полностью переделан, открылся в начале 2024 | от ~4 000 € | Роскошь, у входа в парк |
| [Disney Hotel New York: The Art of Marvel](https://www.google.com/maps/search/?api=1&query=Disney+Hotel+New+York+The+Art+of+Marvel) | Переделан в 2021 | ~2 000-3 000 € | ⭐ Лучшее «новое» за разумные деньги, Артуру зайдёт Marvel |
| [Disney Newport Bay Club](https://www.google.com/maps/search/?api=1&query=Disney+Newport+Bay+Club) | Ремонт 2016, бассейн | ~1 500-2 200 € | Хорошая середина, бассейн для детей |
| [Disney Hotel Cheyenne](https://www.google.com/maps/search/?api=1&query=Disney+Hotel+Cheyenne) / [Santa Fe](https://www.google.com/maps/search/?api=1&query=Disney+Hotel+Santa+Fe) | Обновлены в стиле Toy Story и «Тачек» | ~900-1 300 € | Бюджетно и весело, до парка 15-20 минут пешком или автобусом |
| [Sequoia Lodge](https://www.google.com/maps/search/?api=1&query=Disney+Sequoia+Lodge) | ⛔ Полная реконструкция с января 2026, примерно до 2028 | | Не брать: идут стройработы |

**Моя рекомендация:** Hotel New York Art of Marvel. Он свежий, от него 10 минут пешком до парков, а в отелях Disney дают Extra Magic Time, ранний вход в парк до общей толпы. Это главный способ пройти Frozen без многочасовой очереди. Если нужно сэкономить, берите Newport Bay.

## 4. Перелёт и трансфер

- **Перелёт:** Лиссабон → Париж, около 2 ч 30 мин в воздухе. Летают TAP, Air France, Transavia, easyJet. Ориентир 80-180 € на человека в одну сторону. Учтите, что у Парижа время на час вперёд.
- **Лучший вариант: прилёт в CDG.** Прямо из аэропорта идёт поезд TGV до станции Marne-la-Vallée Chessy, около 10 минут. Станция стоит у ворот парка.
- **Такси с фиксированной ценой:** из CDG примерно 75-95 € (минивэн до 110 €), в дороге 45-60 минут. Это самый простой вариант с детьми и багажом. Если брать билеты на Orly, такси самое разумное решение, потому что прямого поезда оттуда нет.
- **Magical Shuttle** (автобус из CDG и Orly): 24 € взрослый и 11 € ребёнок за поездку, то есть около 70 € на семью в одну сторону. С 19.10.2026 наличные не принимают.

## 5. План по дням

**День 1: прилёт**
- Утренний рейс, например в 06:00-07:00 из Лиссабона, с прилётом около 10:00 по Парижу.
- Такси или TGV, в отеле оставляете багаж и около 12:30 входите в **Disneyland Park**.
- Порядок: Peter Pan, Big Thunder, Pirates, Phantom Manor. Вечером ночное шоу у замка.

**День 2: Frozen**
- Ранний вход в **Adventure World** через Extra Magic Time. Первым делом Frozen Ever After, потом встреча с Анной и Эльзой.
- Дальше Ratatouille, Crush's Coaster, Рапунцель, Spider-Man и Avengers.
- После обеда отдых в отеле или бассейне (дети 6 лет устанут). Вечером ночное шоу на Adventure Bay.

**День 3: отъезд**
- С раннего входа до примерно 12:30 в Disneyland Park: повторить любимое или успеть пропущенное (Hyperspace Mountain, Dumbo, small world).
- Около 13:00 такси, рейс в 15:30-16:30 из CDG. В Лиссабоне будете вечером.

**Хватит ли двух ночей:** ⚠️ впритык. Реально выходит около двух полных парковых дней на два парка. Главное успеете, если сделать три вещи: жить в отеле Disney ради раннего входа, на одну-две очереди купить **Premier Access** (платный проход без очереди, ориентир 15-30 € за человека на аттракцион) и не ехать в пик (каникулы, Пасха, июль-август). Три ночи были бы заметно спокойнее для шестилетки.

## 6. Бюджет на семью 2+2 (вне пика)

| Статья | Эконом | Комфорт | Мой выбор (Marvel) |
|---|---|---|---|
| Перелёты туда и обратно с багажом | 450 | 600 | 600 |
| Отель на 2 ночи и билеты на 3 дня | 1 000 (Cheyenne) | 1 800 (Newport) | 2 400 |
| Трансферы туда и обратно | 140 | 180 | 180 |
| Еда, 2,5 дня | 250 | 350 | 400 |
| Premier Access и сувениры | 100 | 200 | 300 |
| **Итого, €** | **~1 950** | **~3 100** | **~3 900** |

Обоим детям меньше 12 лет, так что билеты у них детские. Отдельный билет на 2 дня и 2 парка стоит от 132 € (ребёнок) до 224 € (взрослый в пик). ⚠️ Все цифры ориентиры из открытых источников; живые цены на конкретные даты я не проверял.

**Сезон:** с начала ноября до начала января в парке рождественский сезон, это красиво, но холодно (+3…+8 °C). Самое удачное окно по погоде и очередям: апрель-июнь вне каникул или сентябрь.

## 7. Альтернативы в Европе (до 4 часов полёта)

| Парк | Дорога из Лиссабона | Почему | Для 6 и 9 лет | Ориентир на 3 дня / 2 ночи, семья |
|---|---|---|---|---|
| ⭐ [Europa-Park + Rulantica](https://www.google.com/maps/search/?api=1&query=Europa-Park+Rust) (Германия) | Перелёт до Базеля 2 ч 40 мин (easyJet) + машина около 1 ч 10 мин | В сентябре 2026 в 11-й раз назван лучшим парком мира (Golden Ticket Awards). Отель Krønasår открылся в 2019, при парке аквапарк Rulantica | Отлично: горки на любой возраст, очередей меньше, чем у Disney | ~2 200-3 200 € |
| [PortAventura + Ferrari Land](https://www.google.com/maps/search/?api=1&query=PortAventura+World) (Испания) | Перелёт до Барселоны около 1 ч 50 мин + около 1 ч 15 мин дороги | Новинки 2026: Coral Bay в аквапарке, Makamanu Jungle. Тепло, есть зона Sesame Street | Хорошо, Артуру особенно | ~1 600-2 500 € |
| [Efteling](https://www.google.com/maps/search/?api=1&query=Efteling) (Нидерланды) | Перелёт до Амстердама или Эйндховена около 2 ч 45 мин + около 1 ч | Сказочный лес, в 2026 детская башня свободного падения Hooghmoed | Идеально для Алисы, Артуру немного по-детски | ~1 800-2 600 € |
| [Phantasialand](https://www.google.com/maps/search/?api=1&query=Phantasialand) (Германия, у Кёльна) | Перелёт около 3 ч | Лучшая тематизация в Европе | Скорее для 10+, у шестилетки многое отсечёт ростом | ~2 000-2 800 € |

**Вывод:** для Алисы с её Эльзой Disney Paris вне конкуренции, и сейчас он свежее, чем был последние 30 лет. Если сама мечта «про Disney» не главное, лучший парк по качеству и цене за впечатления Europa-Park.

🎙 Майк: правильный ход Disney на 2 ночи с отелем Marvel, ранним входом и поездкой не в каникулы. Без раннего входа Frozen съест полдня в очереди. Главный вопрос к тебе один: какие даты? От них зависит цена в полтора-два раза.

Могу собрать это в страницу со ссылками, чтобы переслать семье, и проверить живые цены, когда будут даты.

Sources:
- [Disney: World of Frozen и Adventure World, 29.03.2026](https://thewaltdisneycompany.com/news/disneyland-paris-adventure-world-opening/)
- [Disneyland Paris News: Adventure World](https://news.disneylandparis.com/en/on-march-29-2026-world-of-frozen-along-with-many-new-experiences-will-open-within-disney-adventure-world-the-reimagined-second-park-at-disneyland-paris/)
- [Riding the Magic: очереди в день открытия](https://ridingthemagic.uk/news/disney-adventure-world-opening-day-world-of-frozen-steals-the-show)
- [Disney Tourist Blog: Adventure World по-прежнему слабее](https://www.disneytouristblog.com/still-disneys-weakest-park-new-improved-adventure-world-adds-ride-entertainment-in-2026-2027/)
- [DLP Tips: Raiponce Tangled Spin](https://dlptips.com/things-to-do/walt-disney-studios-rides/raiponce-tangled-spin-disneyland-paris-guide-tips/)
- [WDWMagic: реконструкция Sequoia Lodge](https://wdwmagic.com/wdwmagic-plus/disneyland-paris-resort/news/14apr2025-disney-sequoia-lodge-at-disneyland-paris-set-for-major-renovation-starting-in-2026.htm)
- [Disney Tourist Blog: Sequoia до 2028](https://disneytouristblog.com/should-you-avoid-one-of-our-favorite-disney-hotels-until-2028/)
- [Julie Ears: цены 2026](https://julieears.com/en/prices/disneyland-paris-cost/)
- [Family Deal Finder: цены для семьи 2026](https://familydealfinder.co.uk/blog/how-much-does-disneyland-paris-cost-2026)
- [The Better Vacation: билет на 2 дня](https://thebettervacation.com/disneyland-paris-two-day-ticket)
- [Mickey from the UK: Magical Shuttle без наличных](https://mickeyfromthe.uk/news/disneyland-paris-magical-shuttle-stops-accepting-cash-on-board)
- [Mickey Cabs: такси CDG → Disney](https://www.mickeycabs.com/en/blog/how-much-is-a-taxi-from-cdg-to-disneyland-paris)
- [Momondo: Лиссабон → Париж](https://www.momondo.com/flights/lisbon/paris)
- [Wanderlust Chloe: Europa-Park, Golden Ticket 2026](https://www.wanderlustchloe.com/european-theme-parks/)
- [TourSpain: новинки PortAventura 2026](https://www.tourspain.es/en/b2b/theme-parks-news-experiences-2026/)
- [Themeparks-EU: новинки 2026](https://www.themeparks-eu.com/news/most-anticipated-new-attractions-at-theme-parks-in-europe-2026-preview)
- [Europa-Park: цены Rulantica](https://www.europapark.de/en/rulantica/prices-opening-hours)
- [Suntransfers: Базель → Rust](https://www.suntransfers.com/basel-airport-to-europa-park-rust)

🧒 **Простыми словами:** Диснейленд у Парижа недавно сделал целую новую страну «Холодного сердца», с замком Эльзы на горе. Алисе там будет как в мультике, Артуру хватит горок. Два дня хватит, если жить прямо в отеле Диснея: тогда вас пускают в парк раньше всех, пока нет очередей. Вся поездка на четверых стоит примерно как хороший ноутбук, от 2 до 4 тысяч евро. Если хочется просто лучший парк аттракционов, а не именно Дисней, есть немецкий Europa-Park.
