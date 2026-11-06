---
session: s_5fd21c7d
date: 2026-10-30
words: 1170
turns: 2
tools: "ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-30 · Нужно найти в Португалии или Европе газовый встраиваемый/накладной нагреватель для каменно…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5fd21c7d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Нужно найти в Португалии или Европе газовый встраиваемый/накладной нагреватель для каменной столешницы большого стола.

Идея: врезать или поставить поверх каменной столешницы конструкцию с открытым пламенем, чтобы были видны языки огня. Под столом будет небольшой газовый баллон, шланг пройдет через отверстие в столешнице.

Параметры:
- Газовый, не биоэтанол/спирт/жидкое топливо.
- Открытое пламя, возможно с защитным стеклом вокруг.
- Формат: прямоугольный примерно 20×60 или 20×80 см, можно больше/меньше.
- Также можно рассмотреть круглые варианты.
- Нужен вариант для установки в каменную столешницу или поверх нее.

Важно: жидкостные/спиртовые варианты не подходят — дорого и неудобно постоянно доливать.
__Перевела: GPT-5.5 + whisper__

• • • • •

Нужно провести глубокое исследование и найти, что купить в Португалии или Европе для встраивания газового нагревателя/горелки в каменную столешницу большого стола.

Задача: встроить или установить поверх каменной столешницы газовую fire pit / газовую горелку, чтобы было видно открытое пламя. Под столом планируется небольшой газовый баллон, подключение через отверстие под газовый шланг.

Что нужно искать:
- именно газовый вариант, не биоэтанол/спирт/жидкое топливо;
- встраиваемая или накладная конструкция для стола;
- прямоугольная или круглая форма;
- ориентировочные размеры: 20×60 см, 20×80 см или похожие, можно больше/меньше;
- пламя может быть открытым или со стеклянным защитным экраном;
- покупка в Португалии или с доставкой по Европе.

Важно учитывать безопасность: совместимость с газовыми баллонами, тип газа, редуктор, вентиляция под столом, защита каменной столешницы от нагрева, возможность установки в мебель/столешницу.
__Перевела: GPT-5.5 + 11labs__
(ВОСКРЕШЕНИЕ ПОСЛЕ ЛИМИТА: дверь Claude не подняла эту голосовую вовремя -- дверь Claude: UIA-SUBMIT-FAIL; Codex взял тред s_4b1b99f8, итог не сверен)

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "Planika Fire Line Gas table insert propane drop-in burner Europe price", "mode": "standard"}

---

> `WebSearch` -- {"query": "gas fire pit burner insert for table rectangular 80x20 propane EU CE kit buy", "mode": "standard"}

---

> `WebSearch` -- {"query": "queimador gás embutir mesa fogo lareira exterior propano Portugal", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://planikafires.com/wp-content/uploads/2026/06/EN_EUR_Outdoor_Europe_Pricelist_07.2026.pdf", "prompt": "List all gas burner inserts suitable for building into a table (drop-in, fire pit insert, Fire Line, Galio, etc.): model name, dimensions, gas type (LPG/NG), ignition (manual/automat

---

> `WebSearch` -- {"query": "Happy Cocooning gasbrander inbouw rechthoek tafel propaan CE prijs", "mode": "standard"}

---

> `WebSearch` -- {"query": "Enjoyfires inbouwbrander gas tafel 80 cm propaan", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/cosi-fires-built-in-burner-rectangular-straight.html", "prompt": "Give price, outer dimensions, cutout dimensions, gas type, pressure, kW, ignition, flame failure device, what's included (regulator, hose, lid, glass), CE, shipping to Portugal/EU."}

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/happy-cocooning-separate-built-in-burner-rectangle.html", "prompt": "Give price, outer dimensions, cutout dimensions, gas type, pressure, kW, ignition, flame failure device, what's included, CE, shipping to Portugal/EU. Also mention the Large version if refere

---

> `WebFetch` -- {"url": "https://firepit-online.com/fire-pit-tables/built-in-burners.html", "prompt": "List all built-in gas burners on this page with name, size, price. Note shipping countries."}

---

> `WebSearch` -- {"query": "FORNO built-in burner rectangle 80 x 20 propane", "mode": "standard"}

---

> `WebSearch` -- {"query": "Planika Galio Insert gas fire pit automatic LPG price EUR glass table", "mode": "standard"}

---

> `WebSearch` -- {"query": "gofire superset inbouwbrander rechthoek 75 x 25 prijs glas", "mode": "standard"}

---

> `WebSearch` -- {"query": "queimador encastrar mesa fogo gás Cosi OR \"Happy Cocooning\" Portugal loja", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/forno-separate-built-in-burner-rectangle.html", "prompt": "Price, dimensions, cutout size, kW, gas category/pressure, ignition, thermocouple/flame failure, included items, glass option, delivery time, shipping to Portugal."}

---

**Claude:**

Нашёл три уровня цены. Лучшее попадание в ваш размер: готовая горелка ровно 80×20 см под пропан примерно за 270 €. Её врезают в столешницу, стеклянный экран докупается отдельно. В португальских магазинах таких горелок я не нашёл. Покупать проще в нидерландском магазине Firepit-online, он доставляет по Европе. Доставку именно в Португалию на сайте я не проверял.

## Что купить

| Вариант | Размер | Мощность | Цена | Стекло |
|---|---|---|---|---|
| **FORNO Built-in Burner Rectangle «Brann»** ⭐ | 80×20×8 см | 11,8 кВт | **269,95 €** | экран 80×20 за 76,50 € |
| **Cosi Fires Built-in-burner Straight** (сталь или чёрный) | 60×22×16 см | 9 кВт, расход до 565 г/ч | **249 €** | набор стекла 119 € |
| **GoFire Superset** (у Happy Cocooning/Cosi есть похожие) | 75×25 см | нет данных | цена не найдена | экран уже в комплекте |
| **Planika Galio Insert Automatic** (премиум, Польша) | 1000 / 2000 мм | нет данных | **2500 € / 3800 €** | со стеклом около 4000 € |
| Круглые: Happy Cocooning Built-in Round | Ø39 или Ø48 см | нет данных | **195 € / 249 €** | опция |

- **FORNO 80×20.** В комплекте лавовые камни, крышка, шланг и редуктор на 30 мбар с отметкой CE, поджиг кнопкой. Есть минус: срок поставки сейчас около 8 недель.
- **Cosi 60×22.** Самый ходовой вариант для врезки в стол, комплект почти такой же. Статус на сайте «скоро в наличии».
- **Planika.** Это дизайнерский уровень: автоматика и длинное узкое пламя.

**Что я бы взял:** FORNO 80×20 со стеклом, вместе примерно 350 € плюс доставка. Если 8 недель ждать долго, то Cosi 60×22 со стеклом, около 370 €.

Дешёвые горелки VEVOR (eur.vevor.com) я бы не брал. Они сделаны под американские нормы, и европейская газовая сертификация CE (стандарт 2016/426) у них не подтверждена.

## Безопасность: что проверить до покупки

1. **Газ только пропан, не бутан.** Бутан на холоде плохо испаряется, вечером на улице пламя будет садиться. В Португалии синие и оранжевые баллоны Galp/Repsol бывают обоих типов, нужен пропановый. Баллона на 11 кг хватит примерно на 20 часов при 565 г/ч.
2. **Давление и редуктор.** Горелки из Нидерландов рассчитаны на 30 мбар, а португальский пропан часто идёт на 37 мбар. Сначала смотрите табличку на горелке (категория вроде I3B/P(30)). Потом ставьте редуктор, который подходит и горелке, и португальскому вентилю баллона. Голландский редуктор к португальскому баллону может не прикрутиться. Подключение лучше доверить местному газовщику.
3. **Вентиляция под столом.** Пропан тяжелее воздуха и при утечке скапливается внизу, как вода в яме. Шкаф для баллона должен быть открыт снизу или иметь отверстия у пола. Глухой ящик не годится.
4. **Камень.** Гранит и натуральный камень выдерживают жар, но от резкого перепада температуры могут треснуть. Горелка должна стоять на своём фланце с воздушным зазором, по монтажной схеме производителя. Искусственный кварцевый камень (Silestone и похожие) рядом с огнём лучше не использовать. Отверстие под горелку режет каменщик водяной пилой по чертежу из инструкции.
5. **Защита от погасшего пламени.** Если ветер задул огонь, газ продолжит идти. Защиту (термопару) я подтвердил только у Planika. Для FORNO и Cosi уточните её наличие у продавца до покупки, и стекло всё равно ставьте: оно помогает и от этого.
6. **Только улица** или открытая терраса. Шланг ведите подальше от горелки, и раз в сезон проверяйте соединения мыльной водой.

**Следующий шаг:** напишите, какой формат берём. Могу проверить у Firepit-online доставку в Португалию, наличие защиты от погасшего пламени и подобрать португальский редуктор.

Источники:
- [FORNO Built-in Burner Rectangle 80×20](https://www.firepit-online.com/forno-separate-built-in-burner-rectangle.html)
- [Все встраиваемые горелки Firepit-online](https://firepit-online.com/fire-pit-tables/built-in-burners.html)
- [Cosi Fires Built-in-burner Straight](https://www.firepit-online.com/cosi-fires-built-in-burner-rectangular-straight.html)
- [Happy Cocooning Built-in Round](https://www.firepit-online.com/happy-cocooning-built-in-burner-round.html)
- [GoFire Superset 75×25 (Marktplaats)](https://www.marktplaats.nl/v/tuin-en-terras/terrasverwarmers/a1440177456-gofire-superset-inbouwbrander-rechthoek-75-x-25-cm)
- [Planika Galio Insert](https://planikafires.com/outdoor-gas-fireplaces/galio-insert/) и [прайс Planika Outdoor EUR 07.2026](https://planikafires.com/wp-content/uploads/2026/06/EN_EUR_Outdoor_Europe_Pricelist_07.2026.pdf)
- [VEVOR EU горелка](https://eur.vevor.com/fire-pit-burner-c_12235/vevor-6-x-18-inch-drop-in-fire-pit-pan-rectangular-stainless-steel-fire-pit-burner-natural-propane-gas-fire-pan-h-burner-90-000-btu-for-indoor-or-outdoor-use-p_010380467555)
