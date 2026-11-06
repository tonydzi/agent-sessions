---
session: s_5b9595bf
date: 2026-10-29
words: 1465
turns: 3
tools: "Bash, Grep, ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Нужно найти в Португалии или Европе газовый встраиваемый/накладной нагреватель для каменно…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5b9595bf` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

> `Grep` -- {"pattern": "(?i)fire ?pit|газов\\w* горелк|burner insert|столешниц\\w* .*огон", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "head_limit": 10}

---

> `WebSearch` -- {"query": "Planika Galio gas insert tabletop propane burner price Europe", "mode": "standard"}

---

> `WebSearch` -- {"query": "queimador gás embutir mesa fire pit propano Portugal", "mode": "standard"}

---

> `WebSearch` -- {"query": "gas fire pit burner insert rectangular 80x20 propane CE certified EU shop", "mode": "standard"}

---

> `WebSearch` -- {"query": "Gasfeuer Einbaubrenner Tisch Propan linear 80 cm CE Feuertisch Einsatz", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/forno-separate-built-in-burner-rectangle.html", "prompt": "Product name, dimensions (burner and cutout), price, gas type, power kW, regulator mbar, ignition, safety (thermocouple), glass windscreen options, delivery countries, other sizes available."}

---

> `WebFetch` -- {"url": "https://planikafires.com/outdoor-gas-fireplaces/galio-insert/", "prompt": "Dimensions of Galio Insert models (length, width, cutout, height), gas type LPG, consumption, power, cylinder recommendations, installation in tabletop requirements (ventilation, distance, materials like stone), glas

---

> `WebSearch` -- {"query": "Elementi burner insert gas fire table built-in kit glass windscreen LPG EU", "mode": "standard"}

---

> `WebSearch` -- {"query": "lareira a gás exterior queimador embutir mesa Portugal loja propano 30 mbar", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://cdn.adezz.com/production/ERP_handleidingen/Productmodellen/367/401/FORNO BRANN - DE.pdf", "prompt": "Extract: available burner sizes (rectangle/round/square), cutout dimensions, gas type and pressure (30/37/50 mbar), power kW, consumption g/h, installation requirements: ventilation 

---

> `WebFetch` -- {"url": "https://hooijer.com/wp-content/uploads/2024/01/Techcard_Galio_Insert_Manual.pdf", "prompt": "Extract dimensions (overall, cutout, depth), gas consumption, LPG pressure, glass dimensions, installation requirements (ventilation openings cm², table material, cylinder housing), weight."}

---

> `WebFetch` -- {"url": "https://www.iot-pool.com/en/products/lareira-a-gas-cocoon-move", "prompt": "Product, price, gas type, dimensions, Portugal seller details, other gas fire products sold (burners/inserts)."}

---

**Claude:**

Сайты отдали PDF в бинарном виде, читаю их напрямую.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_5b9595bf/tool-results/\" && for f in webfetch-1793314742929-pgk61p.pdf webfetch-1793314743638-dq5r6b.pdf; do echo \"=== $f\"; python -c \"\nimport sys\ntry:\n    import pypdf\n    r=pypdf.PdfRe

---

> `WebSearch` -- {"query": "Planika Galio distribuidor Portugal lareira gás exterior", "mode": "standard"}

---

> `WebSearch` -- {"query": "round built-in gas fire burner tabletop 40 cm LPG CE regulator glass windscreen Europe shop Adezz Forno round", "mode": "standard"}

---

> `WebSearch` -- {"query": "Happy Cocooning inbouwbrander gas rechthoek 80 cm glas propaan prijs", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/happy-cocooning-separate-built-in-burner-rectangle.html", "prompt": "Sizes (small/large) with outer dimensions and cutout, price, kW, gas pressure/regulator, ignition, thermocouple safety, glass screen accessory and price, delivery to Portugal/Europe and shipp

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/happy-cocooning-built-in-burner-round.html", "prompt": "Sizes with outer diameter and cutout, price each, kW, regulator mbar, ignition, thermocouple, glass screen accessory price, delivery countries."}

---

> `WebFetch` -- {"url": "https://www.firepit-online.com/forno-separate-built-in-burner-square.html", "prompt": "Does this shop deliver to Portugal? Shipping cost/time. Also any notes on ventilation of cylinder enclosure, thermocouple, ignition, cutout dimensions for FORNO burners."}

---

**Claude:**

Нашёл три подходящих газовых горелки, которые продают в Европе. Лучше всего подходит **FORNO Brann 80×20 см**: размер совпадает с вашим, цена около 270 €, стекло можно докупить. Из более дорогих есть **Planika Galio Insert 1000** (Польша): у неё уже есть стекло вокруг пламени, а фирма известная. Из круглых есть **Happy Cocooning** диаметром 39 или 48 см, от 195 €.

## Что купить

| | FORNO Brann | Planika Galio Insert Manual 1000 | Happy Cocooning Round |
|---|---|---|---|
| Форма, размер | прямоугольник **80×20×8 см** | прямоугольник 116×23 см, стекло высотой ~23 см | круг Ø39 см или Ø48 см |
| Цена | **269,95 €** (обычно 329,95) | **1 450 € без НДС** по прайсу 07.2026; версия с пультом 2 500 € | **195 €** (распродажа, обычно 349,95) |
| Мощность | 11,8 кВт | 11,8 кВт на баллонном газе | 6,5 или 12 кВт |
| Стекло | отдельно, Glasset 800×200 за +76,50 € | **уже в комплекте** (закалённое) | отдельно, +99,95 € |
| Что в коробке | шланг, редуктор 30 мбар, крышка, лавовые камни, электроподжиг | шланг 4 м, декоративные чёрные камни, регулировка высоты пламени | крышка, шланг 1 м, «дрова», лавовые камни, шаблон для выреза. **Редуктора нет** |
| Где купить | [firepit-online.com](https://www.firepit-online.com/forno-separate-built-in-burner-rectangle.html), срок поставки около 8 недель | [прайс Planika](https://planikafires.com/wp-content/uploads/2026/06/EN_EUR_Outdoor_Europe_Pricelist_07.2026.pdf), [mohd.it](https://shop.mohd.it/en/galio-outdoor-gas-fireplace.html) | [firepit-online.com](https://www.firepit-online.com/happy-cocooning-built-in-burner-round.html) |

Все три работают на газе из баллона, на биоэтанол они не рассчитаны. По FORNO и Galio я читал паспорта самих производителей.

Есть ещё вариант у той же марки Happy Cocooning: [прямоугольная горелка](https://www.firepit-online.com/happy-cocooning-separate-built-in-burner-rectangle.html) с большим стеклом. По поиску она стоит около 609 €, но размеры и цену на её странице я не подтвердил.

**🎙 Майк:** я бы взял FORNO и стекло к нему, вместе около 350 €. Galio стоит своих денег, только если стол дизайнерский и хочется пульт и приложение.

## Безопасность: что проверить до покупки и врезки

1. **Давление газа.** В Португалии баллонный пропан обычно подают под давлением 37 мбар (единица давления газа). Galio как раз рассчитана на 37 мбар. FORNO продают с редуктором на 30 мбар, это голландская норма. Поэтому у продавца нужно спросить, есть ли у горелки исполнение для Португалии. Редуктор берите тот, что указан в паспорте горелки, а не тот, что продаётся у баллона.
2. **Пропан, а не бутан.** В Португалии много бутана в оранжевых баллонах. Бутан на холоде почти не испаряется, и пламя зимним вечером будет слабым. Нужен пропан.
3. **Защита от погасания пламени** (термопара, по-английски FFD). Это датчик: если ветер задул огонь, он сам перекрывает газ. Без него горелку под столом не ставить. На страницах магазина у FORNO и Happy Cocooning этот датчик прямо не указан, нужно спросить продавца (тел. [ТЕЛЕФОН], [EMAIL]).
4. **Вентиляция под столом.** Баллонный газ тяжелее воздуха и при утечке скапливается внизу. Нельзя закрывать баллон в глухой короб. Нужен открытый низ или вентиляционные отверстия **у самого пола**, а лучше ещё и сверху. Горелки только для улицы или открытой террасы, не для помещения.
5. **Камень столешницы.**
   - Гранит, керамогранит и спечённый камень (Dekton) нормально переносят нагрев.
   - Кварцевый агломерат (Silestone и похожие) и тонкий мрамор от жара могут треснуть.
   - Горелку не кладите вплотную к камню: между краем выреза и металлом оставьте зазор в несколько миллиметров с жаростойкой прокладкой.
   - Стекло сильно нагревается, детям касаться нельзя.
6. **Расход газа.** По паспорту Galio на максимуме сжигает 0,93 кг газа в час. По моей прикидке, для 11,8 кВт выходит около 0,85 кг в час. Значит, баллона на 11 кг хватит примерно на 12–13 часов на полном огне, а на среднем пламени примерно вдвое дольше. Шланг должен проходить так, чтобы не касаться горячего дна горелки.
7. **Подключение газа** лучше доверить сертифицированному газовщику (*técnico de gás*). Если что-то случится, страховая спросит, кто подключал.

## Чего я не проверил

- В Португалии я не нашёл ни одного магазина, у которого такие горелки есть на складе. Все три варианта едут из Нидерландов, Польши или Италии.
- Доставку именно в Португалию надо уточнить у продавца: на сайте firepit-online.com Португалии в списке стран нет. Mohd.it отправляет по всему Евросоюзу.
- Не подтверждены размеры выреза и требования к вентиляции у FORNO: инструкция в открытом доступе описывает только готовый стол.
- Сессия Codex по этой же голосовой (тред `01a189ae…`) мне недоступна, её результат я не сверял.

**Следующий шаг:** если выбираете FORNO, я напишу продавцу. Спрошу про доставку в Португалию, датчик погасания пламени, давление 37 мбар и размеры выреза, и принесу ответ.

Sources:
- [FORNO Built-in Burner Rectangle](https://www.firepit-online.com/forno-separate-built-in-burner-rectangle.html)
- [Planika Galio Insert](https://planikafires.com/outdoor-gas-fireplaces/galio-insert/)
- [Прайс Planika EUR 07.2026](https://planikafires.com/wp-content/uploads/2026/06/EN_EUR_Outdoor_Europe_Pricelist_07.2026.pdf)
- [Паспорт Galio Insert Manual 1000](https://hooijer.com/wp-content/uploads/2024/01/Techcard_Galio_Insert_Manual.pdf)
- [Mohd: Galio](https://shop.mohd.it/en/galio-outdoor-gas-fireplace.html)
- [Happy Cocooning Built-in Burner Round](https://www.firepit-online.com/happy-cocooning-built-in-burner-round.html)
- [Happy Cocooning Built-in Burner Rectangle](https://www.firepit-online.com/happy-cocooning-separate-built-in-burner-rectangle.html)
- [Брошюра Adezz FORNO Brann](https://cdn.adezz.com/production/ERP_handleidingen/Productmodellen/367/401/FORNO%20BRANN%20-%20DE.pdf)
