---
session: s_b5e40c0f
date: 2026-10-07
words: 976
turns: 6
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Проанализировать транскрипт разговора с ним

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b5e40c0f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Проанализировать транскрипт разговора с ним

И понять как стать таким же сейлз репрезентатив как и он

E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-07_15-18-40 (23).jpg

---

> `Bash` -- {"command": "ls -la \"/e/!CLAUDE-HUBPC-June26/downloads/photo_2026-10-07_15-18-40 (23).jpg\" 2>/dev/null || ls \"E:/!CLAUDE-HUBPC-June26/downloads/\" | grep \"15-18-40\"", "description": "Check the image file exists"}

---

**Claude:**

🚂 **План рельс:** картинку читаю САМ (зрение есть только у меня, аутсорс невозможен), разбор транскрипта и выводы — тоже сам (суждение + голос). Наружу уехало бы `web`/`code_read`, но тут их нет.

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-07_15-18-40 (23).jpg"}

---

**Claude:**

Это Mehdi. У нас уже есть его досье и транскрипт в репо — поднимаю (RECALL перед выводами).

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && wc -c docs/mehdi-tabdili-*.md && echo \"=== SAENA ===\" && cat docs/mehdi-tabdili-saena-2026-10-07.md", "description": "Read Mehdi dossier files"}

---

**Claude:**

Досье есть. Теперь сам транскрипт разговора — он в аддендуме.

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && cat docs/mehdi-tabdili-addendum-transcript-2026-10-07.md", "description": "Read Mehdi transcript addendum"}

---

> `Bash` -- {"command": "sed -n '40,400p' \"C:/Users/dev/AppData/Local/Temp/../../../..//Users/dev/.claude/projects/P---WORKDIR-HUB/s_b5e40c0f/tool-results/be4h3lmmt.txt\"", "description": "Read rest of addendum"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && sed -n '40,220p' docs/mehdi-tabdili-addendum-transcript-2026-10-07.md", "description": "Read addendum body"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && sed -n '220,400p' docs/mehdi-tabdili-addendum-transcript-2026-10-07.md", "description": "Read tail of addendum"}

---

**Claude:**

Вопрос уже разбирался пять раз (§7–§25). Делаю не шестой заход, а один свежий замер — цифры там протухали каждые 4 часа.

---

> `Bash` -- {"command": "cd \"/e/Obsidian/_imports/jobs-watch\" 2>/dev/null && ls -la jobs.db 2>/dev/null && (which sqlite3 || python -c \"import sqlite3; print('py ok')\" 2>&1 | head -2)", "description": "Check jobs.db and sqlite availability"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\" && python - <<'EOF'\nimport sqlite3\nc=sqlite3.connect(r\"D:\\Vault\\_imports\\jobs-watch\\jobs.db\")\nq=\"\"\"SELECT status, COUNT(*) FROM ats_jobs\nWHERE lower(company) LIKE '%anthropic%'\nAND (title LIKE '%Applied AI%' OR title LIKE '%Forward De

---

> `Bash` -- {"command": "date -u \"+%H:%M UTC\"; TZ=Europe/Lisbon date \"+%H:%M Лиссабон, %d.%m.%Y\"", "description": "Current time"}

---

**Claude:**

**23:31 Лиссабон, 07.10.2026**

🎙 **Майк:** Идём верно, но ты просишь шестой заход по вопросу, который разобран пять раз. Вместо повтора — докладываю, чем закрыто, и даю одну свежую улику. Вопрос к тебе в конце.

## Этот разбор уже сделан — 07.10, пять заходов

Скриншот на фото — это ровно тред, который уже лежит у нас в [docs/mehdi-tabdili-saena-2026-10-07.md](docs/mehdi-tabdili-saena-2026-10-07.md) (§7, все 7 сообщений с таймкодами). А транскрипт живой встречи разобран в [docs/mehdi-tabdili-addendum-transcript-2026-10-07.md](docs/mehdi-tabdili-addendum-transcript-2026-10-07.md) — Plaud `of_0eff444c`, 64 минуты, Claude Founder House SF.

**Главное, что нашли в транскрипте, и это переворачивает твой вопрос:**

Ты спросил «как стать b2b sales для Claude» **не у того человека**. Mehdi в записи про свою работу не сказал ни одного факта — его реплики это 62 секунды светской беседы (45:39–46:43), а в WhatsApp он вопрос просто конвертировал в звонок («let's discuss, we can work together»). Он не сейлз Claude, он владелец сервисной фирмы-внедренца.

**А ответ ты уже получил — в том же разговоре, от другого человека.** На 48:03 с тобой говорил сотрудник Anthropic из команды Applied AI, и он назвал профессию сам:

> «I'm part of our Applied AI team… broadly helping out with **kind of a technical sales role** — from high-level architecture design to lower level, like here's how to optimize your costing to save money, or here's the model you should be using.»

А на 60:08 он прямо ответил на твой вопрос: «Applied AI team is hiring right now… go check out the career page, pick whichever branch fits you, go for that one.»

## Как стать таким же — пять приёмов, снятых с записи

Это не приёмы продаж. Это инженерная консультация:

1. **Заходить снизу — с денег.** Сначала счёт и выбор модели, потом архитектура.
2. **Диагноз по поведению агента, не по бенчмарку.** «Sonnet ошибается в выборе инструмента → попробуй Opus», а не «Opus лучше».
3. **Горизонт вместо фичи.** Называть, что клиенту **перестанет** быть нужно через полгода.
4. **Главный товар — удаление чужого кода.** «Parts of that harness are less necessary now» — он забирает у клиента работу, а не добавляет.
5. **Честная граница знания вслух.** Он трижды сказал «не знаю», назвал себя biased и отказался одобрить чужой продукт. В этом жанре это сила.

И самое важное из разбора: **разрыв между тобой и им — не в знании.** На 31:30 ты ответил ему про фрактальную загрузку CLAUDE.md под класс задачи — это ровно предмет их работы. Не хватает трёх вещей: должности, права говорить «мы», и кейса с ЧУЖИМ платящим клиентом.

## Что нового — свежий замер только что (23:31, 08.10 по файлам)

Цифры в разборе протухали каждые 4 часа, поэтому пересчитал прямым SQL по `jobs.db`:

| | §25 (07.10 23:10) | сейчас |
|---|---|---|
| ролей Applied AI + FDE | 71 | **71** |
| подано | 22 | **22** |
| не подано (`new`) | 42 | **43** |
| заблокировано анкетой | 3 | **2** (error 1, homework 1) |

**29 не поданных ролей в США/ЕС**, из них в SF/NY/Seattle — 10 штук, включая шесть менеджерских (Financial Services, Healthcare, Commercial, Enterprise Tech Cyber, Megas) и Staff SWE Labs: Applied AI.

## Чего реально не хватает

Одна дыра, и она дорогая: **имя сотрудника Applied AI неизвестно** — в обеих расшифровках его почта побита по-разному (`andropay.com` / `drawpage.com`). Но он назвал вход дешевле реферала: он ведёт **office-hours Anthropic для стартапов** (47:04). Туда записываются не зная имени.

---

🧒 **Простыми словами:** Ты спросил у Мехди, как стать продавцом Claude. Мехди — не продавец Claude, он подрядчик, и он ничего не рассказал, а позвал на звонок. Зато на той же встрече с тобой говорил настоящий сотрудник Anthropic, и он прямо сказал: такая профессия называется Applied AI Architect, иди на сайт вакансий и подавайся. Мы уже подали 22 заявки, ещё 29 в Америке и Европе лежат неподанными.

**Вопрос к тебе, и он решает следующий ход:** добивать оставшиеся 29 ролей через `/apply` — или сначала искать имя того человека из Applied AI и записываться на его office-hours? Второе дешевле и даёт живой контакт, первое — объём. Я бы взял office-hours первым: один подготовленный разговор с инсайдером стоит больше двадцати анкет в тот же ящик.
