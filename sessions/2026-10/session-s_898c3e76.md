---
session: s_898c3e76
date: 2026-10-01
words: 411
turns: 4
tools: "PowerShell, ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · изучи есть ли такой самодельный БАД когда орехи кедровые размалывают вместе с жесткой обол…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_898c3e76` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

изучи есть ли такой самодельный БАД когда орехи кедровые размалывают вместе с жесткой оболочко вокруг ореха?

---

**Claude:**

01:xx, вечер. Вопрос исследовательский: самодельный БАД из кедровых орехов, размолотых вместе с твёрдой скорлупой. Проверю в вебе, есть ли такая практика.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "кедровый орех размолотый вместе со скорлупой БАД мука польза"}

---

> `WebSearch` -- {"query": "pine nut shell ground whole supplement \"со скорлупой\" перемолоть кедровые орехи"}

---

**Claude:**

Есть след: традиция размалывать цельный орех со скорлупой существует. Добираю конкретику.

---

> `WebSearch` -- {"query": "\"кедровое молочко\" цельный орех \"со скорлупой\" толкут измельчают сибирский рецепт"}

---

> `WebSearch` -- {"query": "мука из цельного кедрового ореха со скорлупой купить продукт перемолотый"}

---

> `PowerShell` -- {"command": "Get-Date -Format \"HH:mm\"; [System.TimeZoneInfo]::Local.Id", "description": "Show current local time"}

---

**Claude:**

21:56. Да, такое существует, и это не выдумка. Нашёл два слоя.

**1. Традиционный сибирский рецепт (прямое попадание в твой вопрос).** Старожилы Байкальской Сибири веками делали «кедровое молочко» именно так: орех обжаривали и толкли целиком, ПРЯМО СО СКОРЛУПОЙ, потом заливали кипятком, а всплывшие скорлупки снимали с поверхности. То есть скорлупа участвует в помоле, но в итоге почти вся отфильтровывается водой. Это зафиксировано этнографами: [sibfolk.ru](https://sibfolk.ru/?p=2027), пересказ также у [oum.ru](https://www.oum.ru/yoga/pravilnoe-pitanie/kedrovoe-molochko/).

**2. Современные продукты.** Промышленность целый орех со скорлупой в один порошок обычно НЕ мелет, а разделяет на два товара: кедровая мука из жмыха ядра (например [sib-moskva.ru](https://www.sib-moskva.ru/kedrovaya-muka), [trawaoil.ru](https://trawaoil.ru/p/muka-iz-kedrovogo-oreha-bez-glyutena-61fbbd8a794ca42960920fa8)) и отдельно мука из скорлупы ([edlinhleb.ru](https://www.edlinhleb.ru/drugaya-muka/muka-iz-skorlupy-kedrovogo-oreha-200-g/)). Скорлупу народная медицина использует в отварах и настойках; томские учёные даже изучали углеводно-минеральный комплекс из скорлупы как компонент спортивного питания ([РИА Новости](https://ria.ru/20190604/id_b2f05554.html), [taiga-sibiri.ru](https://taiga-sibiri.ru/polza-skorlupy-kedrovogo-orekha/)).

**Важная оговорка.** Скорлупа кедрового ореха это в основном целлюлоза и лигнин, человек её не переваривает. Есть её как порошок в сухом виде смысла мало, а крупные твёрдые частицы опасны для зубов и ЖКТ. Поэтому традиция работает через воду (молочко, отвар, настойка): вытянуть растворимое, твёрдое выбросить.

🎙 Майк: если ты думаешь про это как про домашний БАД себе, рабочий вариант ровно один, старый сибирский: толочь со скорлупой, заливать горячей водой, скорлупки снимать. Сухой порошок «целый орех в кофемолку и ложкой в рот» никто всерьёз не практикует, и на то есть причина.

🧒 Простыми словами: да, в Сибири так делали сотни лет, но хитро. Орешки мяли вместе со скорлупками и заливали водой, как чай. Вода забирала всё полезное, а твёрдые скорлупки всплывали, и их выкидывали. Грызть или глотать саму скорлупу нельзя, она как деревяшка, живот её не умеет переваривать.

Sources: [sibfolk.ru](https://sibfolk.ru/?p=2027) · [oum.ru](https://www.oum.ru/yoga/pravilnoe-pitanie/kedrovoe-molochko/) · [РИА Новости](https://ria.ru/20190604/id_b2f05554.html) · [taiga-sibiri.ru](https://taiga-sibiri.ru/polza-skorlupy-kedrovogo-orekha/) · [edlinhleb.ru](https://www.edlinhleb.ru/drugaya-muka/muka-iz-skorlupy-kedrovogo-oreha-200-g/) · [sib-moskva.ru](https://www.sib-moskva.ru/kedrovaya-muka)

21:57.
