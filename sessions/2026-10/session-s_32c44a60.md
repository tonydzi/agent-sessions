---
session: s_32c44a60
date: 2026-10-30
words: 1269
turns: 3
tools: "ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-30 · Нужно найти в Португалии или Европе газовый встраиваемый/накладной нагреватель для каменно…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_32c44a60` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

> `WebSearch` -- {"query": "drop-in gas fire pit burner kit rectangular 20x60 cm table insert propane Europe CE", "mode": "extended"}

---

> `WebSearch` -- {"query": "queimador gás embutir mesa fogo exterior Portugal butano propano", "mode": "extended"}

---

> `WebSearch` -- {"query": "Planika Galio Gas insert table burner price Europe", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://planikafires.com/outdoor-gas-fireplaces/galio-insert/", "prompt": "Dimensions of Galio Insert manual and automatic variants (length, width, depth), power kW, gas types (LPG/propane/butane), cylinder use, glass screen option, installation into table/countertop, cutout requirements, v

---

> `WebSearch` -- {"query": "Gas Feuertisch Einbaubrenner Edelstahl rechteckig 60 cm Propan Einbau Tischplatte Brenner Set CE", "mode": "extended"}

---

> `WebSearch` -- {"query": "quemador gas empotrable mesa fuego exterior rectangular kit propano butano CE comprar", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://www.leroymerlin.es/productos/quemador-exterior-para-butano-propano-con-cristal-y-lenos-63-x-18-cm-88780301.html", "prompt": "Price, exact dimensions (outer, cutout, depth), kW, gas type, included items (glass, regulator, hose), ignition, safety thermocouple/flame failure device, CE,

---

> `WebFetch` -- {"url": "https://www.feuerkorb-shop.de/cosi-fires-einbaubrenner-straight.html", "prompt": "Price, exact dimensions, cutout size, kW, gas type, included items, ignition, flame failure safety (thermocouple), CE, glass screen option, shipping to Portugal/EU."}

---

> `WebFetch` -- {"url": "https://www.feuertisch-einbau.de/produkt/einbaubrenner-30x60-edelstahl-enjoyfires/", "prompt": "Price, exact dimensions, cutout size, kW, gas type, included items, ignition, flame failure safety, CE PIN, other sizes available (e.g. 20x80, 26x95), shipping to EU/Portugal."}

---

> `WebFetch` -- {"url": "https://www.feuertisch-einbau.de/product-categorie/einsatz-gasbrenner/", "prompt": "List all burners with dimensions, cutout, kW, price, shape (round/rect), glass options. Also shipping countries."}

---

> `WebSearch` -- {"query": "Nora Flames queimador exterior butano propano cristal Leroy Merlin Portugal", "mode": "standard"}

---

**Claude:**

Ищу варианты, уже нашёл три подходящих горелки. Сейчас проверяю цены и размеры.

---

> `WebFetch` -- {"url": "https://www.elcorteingles.es/bricor/A51939871-quemador-gas-rectangular-nora-630-x-180-lpg", "prompt": "Price, dimensions, cutout, kW, included glass, regulator, hose, flame failure safety, gas type, shipping."}

---

> `WebFetch` -- {"url": "https://www.feuertisch-einbau.de/produkt/einbaubrenner-26x95-edelstahl-easyfires-kopie/", "prompt": "Product name, exact dimensions, cutout, kW, price, gas, safety (thermocouple), glass option price."}

---

> `WebSearch` -- {"query": "Easyfires Einbaubrenner 26x76 Edelstahl Ausschnitt kW", "mode": "standard"}

---

> `WebSearch` -- {"query": "queimador embutir mesa lareira exterior gás propano inox loja Portugal comprar", "mode": "standard"}

---

**Claude:**

Нашёл, что купить: готовые горелки для врезки в столешницу есть, они продаются в Европе с доставкой в Португалию и стоят от 250 до 600 €. Это стальной лоток с пламенем над лавовыми камнями. Его вставляют в вырез в камне, и он держится на своём бортике. Баллон стоит под столом. Отдельно можно купить стеклянный экран вокруг пламени.

## Что подходит под 20×60 и 20×80

| Вариант | Размер | Мощность | Цена | Что важно |
|---|---|---|---|---|
| **Cosi Fires Straight** (Германия) | 60×22 см | 9 кВт, расход 565 г/ч | 249 € (было 349) | Точно ваш размер. Регулятор, камни и крышка в комплекте. Стекло 70×30 см за 119 €. ⚠️ Сейчас «скоро в наличии». Доставка в PT от 8,95 € |
| **Enjoyfires 30×60** (feuertisch-einbau.de) | 60×30 см, вырез 57×27 | 16 кВт | 304 € | Защита от утечки газа есть. Шланг 120 см, регулятор на 30 мбар. Стекло докупается |
| **Easyfires 26×76** (тот же магазин) | 26×76 см | не указана | 241 € | Ближе всего к 20×80. Стекло докупается |
| **Nora Flames 63×18** (Leroy Merlin ES, El Corte Inglés) | 63×18 см | не проверил | ~477–505 € | Стекло и декоративные поленья **уже в комплекте**. Сразу под баллоны бутан и пропан |
| **Planika Galio Insert** (Польша, премиум) | модульная «огненная линия» | 11,8 кВт на сжиженном газе | от 1 450 € без НДС | Дизайнерский вариант. Модули можно соединять в длинную линию |

**Круглые и квадратные варианты** (тот же магазин Easyfires): диаметр 30 см за 218 €, 40,5 см за 253 €, квадраты 30×30, 40×40, 50×50. У Nora Flames есть 40,5×40,5 со стеклом.

🎙 Майк: я бы взял **Enjoyfires 30×60 + стекло**. У Cosi размер идеальный, но его сейчас нет в наличии. У Enjoyfires подтверждена защита: если пламя погаснет, газ сам перекроется. На столе, где сидят люди, это главное. Хотите «поставил и работает» с уже готовым стеклом, тогда Nora Flames 63×18.

## Безопасность: что проверить до покупки

1. **Газ в Португалии.** Баллоны Galp и Rubis бывают пропан (давление 37 мбар) и бутан (28–30 мбар). У Enjoyfires регулятор на 30 мбар, то есть под бутан. Под пропан нужен регулятор на 37 мбар, его покупают отдельно за несколько евро. Скажите продавцу, какой у вас баллон.
2. **Маркировка CE с номером PIN** обязательна по регламенту ЕС о газовых приборах (2016/426). Без неё не берите.
3. **Защита от погасания пламени (термопара).** Если ветер задует огонь, газ сам перекроется. Это обязательно. Пьезоподжиг сам по себе газ не перекрывает.
4. **Вентиляция под столом.** Сжиженный газ тяжелее воздуха и собирается внизу. Если баллон стоит в закрытом коробе, нужны отверстия у самого пола и наверху. Ставить баллон прямо под горелкой нельзя, его лучше отодвинуть в сторону. Шланг ведите так, чтобы он не касался горячего дна лотка.
5. **Камень может треснуть от нагрева.** Гранит держит нормально. Мрамор и кварцевый агломерат (Silestone и похожие) могут лопнуть от перепада температур. Под бортик горелки положите термостойкую прокладку. Между стенками лотка и камнем оставьте 5–10 мм воздуха, у каждой модели есть свои размеры выреза. Вырез с закруглёнными углами делает камнерез.
6. **Только на улице или под открытым навесом.** Все эти горелки уличные, в помещении ими пользоваться нельзя.

## Что не проверено
- Страницы Leroy Merlin и El Corte Inglés закрыли доступ для моего инструмента. Цену Nora Flames я взял из поисковой выдачи, комплектацию и мощность не сверил.
- В португальских магазинах встраиваемых горелок я не нашёл, там продают только готовые столы с огнём (Cool-mania, Leroy Merlin PT). Поэтому покупать удобнее в Германии или Испании с доставкой.
- Мощность моделей Easyfires 26×76 и 25×50 в каталоге не указана.

**Следующий шаг:** скажите, какой камень у столешницы (гранит, мрамор или кварц) и какой баллон у вас будет. По этим данным подберу точный регулятор и размер выреза для камнереза.

Источники:
- [Cosi Fires Straight 60×22](https://www.feuerkorb-shop.de/cosi-fires-einbaubrenner-straight.html)
- [Enjoyfires 30×60](https://www.feuertisch-einbau.de/produkt/einbaubrenner-30x60-edelstahl-enjoyfires/)
- [Каталог Easyfires/Enjoyfires](https://www.feuertisch-einbau.de/product-categorie/einsatz-gasbrenner/)
- [Easyfires 26×182](https://www.feuertisch-einbau.de/produkt/einbaubrenner-26x95-edelstahl-easyfires-kopie/)
- [Nora Flames 63×18, Leroy Merlin ES](https://www.leroymerlin.es/productos/quemador-exterior-para-butano-propano-con-cristal-y-lenos-63-x-18-cm-88780301.html)
- [Nora Flames 630×180, El Corte Inglés](https://www.elcorteingles.es/bricor/A51939871-quemador-gas-rectangular-nora-630-x-180-lpg)
- [Planika Galio Insert](https://planikafires.com/outdoor-gas-fireplaces/galio-insert/)
- [Прайс Planika, 07.2026](https://planikafires.com/wp-content/uploads/2026/06/EN_EUR_Outdoor_Europe_Pricelist_07.2026.pdf)
- [Готовые столы с огнём, Cool-mania PT](https://www.cool-mania.pt/lar/mesa-de-fogueira-a-gas/fogueira-redonda-de-propano-mesa-de-lareira-a-gas-de-concreto-para-area-externa-106x40-cm-fenix-cinza)
