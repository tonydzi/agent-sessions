---
session: s_f49bd018
date: 2026-10-21
words: 1643
turns: 5
tools: "Bash, Grep, Read, ToolSearch, WebFetch, WebSearch, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-21 · Проведи исследование про Рита Кафарова Все те митапы и конференции, что он организовал за…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f49bd018` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Проведи исследование про Рита Кафарова Все те митапы и конференции, что он организовал за последние 5 лет в Силиконовой долине Проведи глубокое исследование цен, которые он обычно брал за свои кампы и туры Проведи глубокое исследование Multiversity 1440 Это что-то типа базы отдыха, лагеря, кэмпа Такой а-ля гостиницы, где он проводит венты Изучи его сайт svc1440.com

---

**Claude:**

Начинаю с RECALL: ищу в волте и памяти, что мы уже знаем про Рита и svc1440. Параллельно загружаю веб-инструменты.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 5}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports 2>/dev/null && timeout 90 python brain_ask.py \"Рита Кафаров svc1440 Multiversity 1440\" 2>&1 | head -60", "description": "RECALL по волту через brain_ask", "timeout": 100000}

---

> `Grep` -- {"pattern": "Кафаров|Kafarov|svc1440|Multiversity|1440 Multiversity", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "-i": true, "head_limit": 30}

---

> `Grep` -- {"pattern": "Кафаров|Kafarov|svc1440|Multiversity", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "files_with_matches", "-i": true, "head_limit": 20}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\WhatsApp-wa2\\DM\\wa2-Rita-Gafarov--116420.md"}

---

> `WebFetch` -- {"url": "https://svc1440.com", "prompt": "Extract everything: who runs it, events, camps, tours, prices, dates, locations, team names, contacts, links to other pages. Be exhaustive."}

---

> `WebSearch` -- {"query": "1440 Multiversity Scotts Valley campus events retreat pricing", "mode": "standard"}

---

> `WebSearch` -- {"query": "Rita Gafarov Silicon Valley organizer camp tour 1440 neclub", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://svc1440.com/en", "prompt": "Find all pricing: ticket price, package tiers, what is included (lodging, meals), deposit, early-bird, payment terms, prices in USD. Also quote the exact text about last year's (May 2026) camp: attendance, speakers, dates. Be exhaustive and literal with n

---

> `WebFetch` -- {"url": "https://1440.neclub.org/2027", "prompt": "Find all pricing, tiers, what's included, dates, deposit, payment terms. Quote numbers literally."}

---

> `WebFetch` -- {"url": "https://sfih.us/45th-bootcamp-in-silicon-valley-an-insiders-look-at-key-events-and-outcomes/", "prompt": "Extract dates, venues in Silicon Valley, companies visited, speakers, program structure, number of participants, price if any."}

---

> `WebFetch` -- {"url": "https://sfih.us/silicon-valley-private-circle-an-event-in-a-church-and-a-hike-for-entrepreneurs/", "prompt": "Extract event date, venue, format, speakers, number of participants, price."}

---

> `WebSearch` -- {"query": "Silicon Valley bootcamp San Francisco Innovation Hub Гафаров стоимость участия бутcamp цена $", "mode": "extended"}

---

> `WebSearch` -- {"query": "Silicon Valley Camp 1440 Гафаров цена билета стоимость участия май 2026", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://svc1440.com/?lang=ru", "prompt": "Найди все цены, стоимость участия, пакеты, что входит, даты, FAQ, отзывы, цифры по прошлому кемпу (май 2026), список спикеров. Цитируй числа буквально."}

---

> `WebFetch` -- {"url": "http://sfih.us/index-page/", "prompt": "List all bootcamp editions, dates, programs, prices, links to other pages and articles. Exhaustive."}

---

> `WebFetch` -- {"url": "https://www.theamericanreporter.com/Rita-gafarov-and-his-san-francisco-innovation-hub-know-the-best-way-to-upgrade-your-company-in-silicon-valley/", "prompt": "Extract biography, company history, bootcamp format, prices, numbers, events, dates."}

---

> `WebSearch` -- {"query": "Рита Гафаров бутcamp Кремниевая долина стоимость участия тысяч долларов неделя", "mode": "extended"}

---

> `WebSearch` -- {"query": "SFIH San Francisco Innovation Hub bootcamp 2025 cohort Silicon Valley Gafarov 46th 47th 48th 49th 50th", "mode": "extended"}

---

> `WebFetch` -- {"url": "https://www.linkedin.com/in/malikone/", "prompt": "Extract experience, company, role, history, events."}

---

**Claude:**

Нашёл важный след: innovationcamp.us с бизнес-туром и ценой $6 500. Проверяю его, sfihub.com и посты 47-го и 48-го буткемпов.

---

> `WebFetch` -- {"url": "https://innovationcamp.us/business-tour-san-francisco", "prompt": "Extract all prices (per person, per tier), what is included/excluded, dates/schedule of tours, duration, hotel, group size, organizer name, cities, upcoming dates. Quote numbers literally. Also list links to other pages of t

---

> `WebFetch` -- {"url": "https://sfihub.com/", "prompt": "Extract all bootcamp info: dates, prices, formats, what's included, packages, application, past cohorts, numbers."}

---

> `WebFetch` -- {"url": "https://sfih.us/48th-bootcamp-in-silicon-valley-oscar-hartmann-top-companies-and-fresh-insights/", "prompt": "Extract dates, venues, companies visited, speakers, participants count, price."}

---

> `WebFetch` -- {"url": "https://sfih.us/the-47th-silicon-valley-bootcamp-meeting-with-entrepreneurs-and-all-for-good-reason/", "prompt": "Extract dates, venues, companies, speakers, participants count, price."}

---

> `WebFetch` -- {"url": "https://sfih.us/blog/", "prompt": "List all post titles with dates, especially bootcamp numbers (40th-51st), events, meetups, Private Circle, Grand Business Event, 1440 Multiversity, camps. Include URLs."}

---

> `WebFetch` -- {"url": "https://e-course.us/book-author/%D1%80%D1%83%D1%81%D0%BB%D0%B0%D0%BD-%D0%BC%D0%B0%D0%BB%D0%B8%D0%BA%D0%BE%D0%B2%D0%B8%D1%87-%D0%B3%D0%B0%D1%84%D0%B0%D1%80%D0%BE%D0%B2/", "prompt": "Extract the full biography of Rita Gafarov: career, companies, years, business tours, prices if any."}

---

> `WebFetch` -- {"url": "https://www.silicon-valley-book.site/", "prompt": "Extract author bio, book details, any mention of bootcamps, tours, prices, company names."}

---

> `WebFetch` -- {"url": "https://www.1440.org/llms.txt", "prompt": "Summarize 1440 Multiversity: location address, ownership, founding, capacity, lodging types and nightly rates, group/corporate event rental info, pricing, history."}

---

> `WebSearch` -- {"query": "1440 Multiversity Scotts Valley founded Scott Kriens campus history rooms lodging rates group buyout corporate retreat", "mode": "standard"}

---

> `WebSearch` -- {"query": "Silicon Valley Camp 1440 first camp May 2026 Wozniak Vaynerchuk Asprey Santa Cruz Gafarov participants price", "mode": "extended"}

---

**Claude:**

Последний добор: тарифы самой площадки 1440 и следы цен #maliktrip.

---

> `WebFetch` -- {"url": "https://1440.org/experience-1440/stay", "prompt": "Extract room types with nightly rates in USD, what's included in overnight stays, pod prices, group rates, minimums."}

---

> `WebSearch` -- {"query": "#maliktrip Рита Гафаров бизнес-тур США стоимость Malikspace тур в Кремниевую долину цена", "mode": "extended"}

---

> `WebSearch` -- {"query": "NEClub Neo Entrepreneurship Club membership price mastermind Silicon Valley Gafarov", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://maliktrip.malikspace.com/more/", "prompt": "Extract all prices, dates, program, group size, what's included, number of groups, hotel, years. Quote numbers literally."}

---

> `WebFetch` -- {"url": "https://www.forbes.ru/profile/359505-Rita-gafarov", "prompt": "Extract everything about Rita Gafarov: bio, companies, events, tours, prices, numbers."}

---

> `Write` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\research-gafarov-svc1440-2026-10-21.md", "content": "---\ntitle: \"Рита Гафаров (SFIH, NE Club, Silicon Valley Camp 1440): события, цены, 1440 Multiversity\"\ndate: 2026-10-21\ntype: research\nstatus: draft\ntags: [research, gafarov, svc1440, 144

---

**Claude:**

## Главное

**Фамилия Gafarov (Гафаров), не Kafarov.** оператор с ним уже переписывался в WhatsApp 10–11 октября. Рита сказал: «давай после 25-го спишемся».

**Публичных цен нет.** Вход на кэмп только через заявку и интервью. Единственная цена в моих источниках — его же ответ оператору 11.10: «Этот формат пока 40, ближе к новому году будет 50». Единицы он не назвал. Скорее всего это тысячи долларов, но это моя догадка, не факт.

## Кто он и что за структуры

- **Рита и Алина Гафаровы:** основатели San Francisco Innovation Hub (SFIH, офис в Los Gatos) и клуба NE Club.
- **Malikspace:** его более старая компания, организует образовательные события с 2010 года в 40 городах 8 стран.
- **Другие проекты:** MURS.AI, MalikCRM, книга 2021 года про культуру организаций Кремниевой долины.
- **#maliktrip:** деловые туры в США для русскоязычных предпринимателей, 26 групп, клуб 400+ человек.

## События в Долине

| Событие | Когда | Где | Масштаб |
|---|---|---|---|
| 45-й буткемп | октябрь 2024 | Stanford, Berkeley, Plug and Play, Google | ~180 человек на финале |
| Silicon Valley Private Circle | 20–21.10.2024 | Сан-Франциско (бывшая церковь) и Half Moon Bay | благотворительный аукцион на $10k+ |
| 47-й буткемп | завершён 8 марта, год на странице не указан | Stanford, Berkeley, Uber, Microsoft, Meta, Google | 40 участников |
| 48-й буткемп | 5–11 апреля, год на странице не указан | Stanford, Microsoft, Intel, Apple, Napa | не указано |
| **Silicon Valley Camp 1440, №1** | май 2026 | 1440 Multiversity | 150–200 человек |
| **Silicon Valley Camp 1440, №2** | 6–10 мая 2027 | 1440 Multiversity | лимит 150, осталось 47 мест |

- **Годы 47-го и 48-го:** поиск относит их к 2025 году, это не подтверждено.
- **Спикеры первого кэмпа (2026):** Wozniak, Gary Vaynerchuk, Dave Asprey, Scott Kriens, Arnnon Geshuri, Brandt Yan.
- **Спикеры 2027:** Huberman, Isaacson и ещё 60+.
- **Формат 2027:** 7 треков (AI, longevity, энергия, космос и робототехника, деньги будущего и другие) плюс программа для подростков. Вход заявлен «с капиталом от $5M». Регистрация закрывается в конце марта 2027.
- **Заявленные цифры:** 51 когорта с 2016 года и 1500+ выпускников. В статье августа 2023 было «700+», так что это маркетинговые числа, не проверенные.
- **Не нашёл:** 46-й и 49–51-й буткемпы, а также события 2021–2023 по отдельности.

## svc1440.com

Сайт лендинг в стиле «не конференция, а кэмп»: нет границы между сценой и залом. Цен нет, есть только кнопка «Apply now» и интервью. Контакт Алины: Telegram @alina868, WhatsApp [ТЕЛЕФОН]. Тот же контент лежит на 1440.neclub.org/2027. После кэмпа участники попадают в закрытый NE Club: ежемесячные мастермайнды, личные консультации, групповые поездки. Цену этого членства я не нашёл.

## Цены прошлых туров

Цен #maliktrip на его страницах нет. Формат: 11–12 дней, группа до 10 человек, из них 5 дней в Долине. Тарифы с innovationcamp.us ($4 900 / $5 500 / $6 500) принадлежат другому организатору, Flamb Media, и относятся к 2020 году. Ему я их не приписываю. Их можно брать только как ориентир рынка.

## 1440 Multiversity

Это не база отдыха, а некоммерческий центр обучения и велнеса.

- **Расположение:** Scotts Valley, а не Santa Cruz, как пишет Рита. 75 акров леса из секвой.
- **Основатели:** Scott и Joanie Kriens (Scott — сооснователь Juniper Networks). Открыт в мае 2017 года на месте бывшего Bethany University.
- **Объём:** 147 номеров, 40 000+ кв. футов под события, 30+ площадок.
- **Номера:** suites, premium balcony, deluxe, classic и pods (общая комната на 8 человек с общим санузлом).
- **Что входит в проживание:** питание три раза в день, фитнес-центр, инфинити-джакузи, тропы.
- **Тарифы:** на 1440.org их нет. По старым статьям: комната от $175 за ночь, дневной пасс около $95. Груп-заказы идут через запрос предложения (RFP).

Выходит так: Рита арендует площадку под свой кэмп, а сам продаёт в основном доступ к людям и закрытое сообщество.

## Что делать

Цену можно уточнить одной строкой у самого Рита. Он сам сказал писать после 25 октября, и оператор ему уже предлагал контакты инженеров из openai и anthropic для мини-встреч. Заметка сохранена в [research-gafarov-svc1440-2026-10-21.md](docs/research-gafarov-svc1440-2026-10-21.md).

В волт пока не разложено. Дистилляцию RECALL по этой теме можно сделать отдельным шагом.

## 🧒 Простыми словами

Рита возит предпринимателей в Кремниевую долину и сам снимает лесной «университет» 1440 под свой пятидневный лагерь. Сколько стоит лагерь, на сайте не написано: надо подать заявку и пройти собеседование. Он только сказал оператору «сорок, потом будет пятьдесят», и что это за деньги, нужно спросить у него самого.

Sources:
- [svc1440.com/en](https://svc1440.com/en)
- [1440.neclub.org/2027](https://1440.neclub.org/2027)
- [SFIH: 45th bootcamp](https://sfih.us/45th-bootcamp-in-silicon-valley-an-insiders-look-at-key-events-and-outcomes/)
- [SFIH: Private Circle](https://sfih.us/silicon-valley-private-circle-an-event-in-a-church-and-a-hike-for-entrepreneurs/)
- [SFIH: 47th bootcamp](https://sfih.us/the-47th-silicon-valley-bootcamp-meeting-with-entrepreneurs-and-all-for-good-reason/)
- [SFIH: 48th bootcamp](https://sfih.us/48th-bootcamp-in-silicon-valley-oscar-hartmann-top-companies-and-fresh-insights/)
- [The American Reporter](https://www.theamericanreporter.com/Rita-gafarov-and-his-san-francisco-innovation-hub-know-the-best-way-to-upgrade-your-company-in-silicon-valley/)
- [silicon-valley-book.site](https://www.silicon-valley-book.site/)
- [maliktrip.malikspace.com](https://maliktrip.malikspace.com/more/)
- [innovationcamp.us](https://innovationcamp.us/business-tour-san-francisco)
- [1440.org llms.txt](https://www.1440.org/llms.txt)
- [1440.org stay](https://1440.org/experience-1440/stay)
- [Press-Banner о 1440](https://pressbanner.com/multiversity-opens-to-locals/)
