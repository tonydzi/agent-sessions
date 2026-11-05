---
session: s_e52a173b
date: 2026-10-07
words: 965
turns: 2
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Проанализировать транскрипт разговора с ним

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_e52a173b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Проанализировать транскрипт разговора с ним

И понять как стать таким же сейлз репрезентатив как и он

E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-07_15-18-40 (22).jpg

---

> `Bash` -- {"command": "ls -la \"/e/!CLAUDE-HUBPC-June26/downloads/photo_2026-10-07_15-18-40 (22).jpg\" 2>/dev/null || ls \"E:/!CLAUDE-HUBPC-June26/downloads/\" | grep \"15-18-40\"", "description": "Check the image file exists"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-07_15-18-40 (22).jpg"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && wc -c docs/mehdi-tabdili-*.md && echo \"---\" && ls docs/ | grep -i mehdi", "description": "Find Mehdi transcript docs"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && cat docs/mehdi-tabdili-saena-2026-10-07.md", "description": "Read Mehdi profile doc"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && cat docs/mehdi-tabdili-addendum-transcript-2026-10-07.md", "description": "Read the transcript addendum"}

---

> `Bash` -- {"command": "sed -n '40,400p' \"C:/Users/dev/AppData/Local/Temp/../../../../Users/dev/.claude/projects/P---WORKDIR-HUB/s_e52a173b/tool-results/bjo06ndio.txt\" 2>/dev/null | head -250", "description": "Read rest of addendum"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && sed -n '40,250p' docs/mehdi-tabdili-addendum-transcript-2026-10-07.md", "description": "Read addendum body"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && sed -n '250,400p' docs/mehdi-tabdili-addendum-transcript-2026-10-07.md", "description": "Read tail of addendum"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts 2>/dev/null; python ~/.claude/scripts/rail_plan.py declare --self \"чтение локальных md+Plaud-транскрипта, SQL по jobs.db, синтез ответа оператору\" --outsource \"\" 2>&1 | tail -3", "description": "Declare rail plan"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch 2>/dev/null && ls jobs.db && python - <<'EOF'\nimport sqlite3\nc=sqlite3.connect(r\"D:\\Vault\\_imports\\jobs-watch\\jobs.db\")\nq=\"\"\"select status, count(*) from ats_jobs\nwhere company like '%Anthropic%' and (title like '%Applied AI%' or title 

---

> `Bash` -- {"command": "TZ=Europe/Lisbon date \"+%d.%m.%Y %H:%M Лиссабон\"", "description": "Current Lisbon time"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && cat >> docs/mehdi-tabdili-addendum-transcript-2026-10-07.md <<'EOF'\n\n---\n\n## 25. Поправка к §18 — свежий замер 07.10 23:10 (сессия H77064)\n\nСтрогий класс (компания Anthropic, title содержит «Applied AI» или «Forward Deployed»), прямой SQL по 

---

**Claude:**

**07.10.2026 23:10 Лиссабон**

🚂 Рельсы: всё сам (локальные файлы + SQL по `jobs.db`), наружу ничего — класс работы не выезжает.

## Сперва главное: этот разбор уже сделан, четырьмя заходами

Транскрипт встречи 06.10 (Plaud, 64 мин, Claude Founder House SF) найден и прочитан. Файлы:
- [mehdi-tabdili-saena-2026-10-07.md](docs/mehdi-tabdili-saena-2026-10-07.md) — кто такой Mehdi + разбор WhatsApp-треда с того самого скрина
- [mehdi-tabdili-addendum-transcript-2026-10-07.md](docs/mehdi-tabdili-addendum-transcript-2026-10-07.md) — транскрипт, 4 добора, поправки

Пятый заход вслепую делать не буду. Вот суть и одна свежая цифра.

## Вопрос задан не тому человеку

Mehdi в записи говорит **62 секунды** (45:39–46:43) и о своей работе — ни слова. Он не сейлз Claude, он владелец сервисной фирмы-внедренца Saena. На твой вопрос в WhatsApp он ответил «let's discuss, we can work together» — это не уклончивость, это его приём: рецепт у него товар, он меняет интерес на звонок.

**Но ответ на твой вопрос в той же записи есть — от сотрудника Anthropic** (46:43–60:51, имя в расшифровке побито). Ты сам его спросил на 60:00 «Are you like get support from Applied AI?» и получил прямо:

> «Applied AI team is hiring right now across a couple of different segments. Go check out the careers page, pick the one that's the best fit, and go for that one.»

## Профессия называется Applied AI Architect (и Forward Deployed Engineer)

Не «b2b sales for Claude» — такой профессии на рынке нет. Работа по его же словам: прийти к клиенту, сказать какую модель брать, как срезать счёт, и **что из его обвязки теперь можно выбросить**. Продаётся инженерное суждение.

Пять приёмов жанра, снятых с живого разговора (§23 аддендума):
1. Заходить **снизу**: сначала счёт и выбор модели, потом архитектура.
2. Диагноз через **наблюдаемую ошибку агента**, а не «Opus лучше».
3. Называть, что у собеседника **станет лишним** через полгода.
4. Главный товар — **удаление чужого кода**, а не добавление.
5. «Не знаю, и вот моя предвзятость» — вслух. Он трижды сказал «не знаю» и один раз отказался одобрить чужой продукт. В этом жанре это сила.

Пятый — самый неочевидный. И ровно в этом регистре ты уже говорил в той же записи (31:30, твой фрактал CLAUDE.md под задачу). Разрыв не в знании, а в трёх вещах: должность, право говорить «мы», кейс с **чужим платящим** клиентом.

## Свежий замер, 23:10 (цифры из аддендума за 4 часа протухли)

Строгий класс Applied AI + Forward Deployed в Anthropic: **71 роль, подано 22, не подано 42**, 3 заблокировано анкетой.

Из 42 не поданных на США/ЕС — 22: London 8 · Munich 5 · Paris 3 · NY/SF/Seattle 5 · Washington DC 1. Остальные 20 — APAC.

Три заблокированные (SF/NY) — самый дешёвый неиспользованный ресурс: там не «нет двери», а робот упёрся в домашку и ошибку анкеты.

## Что делать, от дешёвого к дорогому

1. **Добить 22 роли US/EU** через `/apply` — путь назван самим сотрудником Anthropic.
2. **Записаться на office-hours Anthropic для стартапов** — он ведёт их регулярно, это публичная программа, имя знать не нужно. Повторить тот же разговор подготовленным.
3. **Встреча с Mehdi 14.10** — не «научи меня», а переговоры о субподряде. Его оффер «we can work together» закрывает нашу единственную дыру: кейс с внешним платящим клиентом. Главный вопрос ему — сколько человек в команде (порог CPN — 10).
4. **Три цифры «до/после»** по стоимости запроса держать наготове — это их язык.

Один тактический урок из треда, который мы проиграли: он дал **инвайт**, а не ссылку. Ты кинул Calendly (просьба), он назавтра сам забронировал слот и написал «just sent an invite» (факт). Из визитки в календарь за 19,5 часов.

🧒 **Простыми словами:** Ты спросил у дяди с фотки «как стать таким продавцом». А дядя на самом деле не продавец — у него своя фирма, которая ставит Claude другим компаниям, и он ничего не рассказал, а позвал на звонок. Зато на той же встрече рядом сидел настоящий сотрудник Anthropic, и ты его тоже спросил — и он ответил прямо: «иди на сайт вакансий, выбери Applied AI, подавайся». Таких вакансий сейчас 42 свободных, 22 из них в Америке и Европе. Работа там — не уговаривать купить, а приходить и говорить: вот эту модель бери, вот здесь ты переплачиваешь, а вот этот твой код уже можно выкинуть. Ты так уже умеешь — не хватает только бумажки с должностью и одного живого клиента со стороны.

**07.10.2026 23:12 Лиссабон**
