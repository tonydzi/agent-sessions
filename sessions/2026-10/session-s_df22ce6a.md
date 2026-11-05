---
session: s_df22ce6a
date: 2026-10-14
words: 753
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-14 · Base directory for this skill: C:\Users\dev\.claude\skills\find

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_df22ce6a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<command-message>find</command-message>
<command-name>/find</command-name>
<command-args>Мерлион</command-args>

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\find

# /find — умный поиск имени/компании по написанию

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap.

Детерминированный, 0 токенов — **НЕ RAG**. Эмбеддинги не понимают каракули (`dbrnjh`, опечатки, раскладку); это ловит отдельный код по фонетическим отпечаткам + нечёткому сравнению. Для поиска по СМЫСЛУ — это `/ask`, не сюда.

## Когда сюда
«найди Виктора» · «все Викторы» · «найди компанию Мерлион» · «кто такой <имя>» · `dbrnjh`/опечатки/транслит — любое имя ЧЕЛОВЕКА, лида, контакта или КОМПАНИИ в любом написании.

## Запуск (ВСЕГДА `PYTHONUTF8=1` — иначе cp1252 краш на виндовой консоли)
`PYTHONUTF8=1 python "$IMPORTS_ROOT/namesearch/find_name.py" <имя> [--html] [--all]`
- по умолчанию: лиды + люди + компании + Apple-контакты (заметки волта скрыты)
- `--all` — добавить заголовки заметок всего волта
- `--html` — визуальный дашборд в `_Dashboards\Name-Search-*.html` (оператор работает глазами — предлагай его для длинных списков)

Имя в кириллице даёт чистый запрос (виктор → ровно `Reiter`); раскладочный/опечаточный запрос — расширяется автоматически.

## Сперва спроси WhatsApp-базу, если ищешь по ПЕРЕПИСКЕ
`namesearch` знает имена и карточки, но НЕ знает текста WhatsApp: 148 978 сообщений живут в
`D:\Vault\_imports\whatsapp\wa_live.db` (SQLite+FTS5, 0 токенов), и в волт едет только хвост
транскрипта -- «не нашёл в заметках» там не значит «не было».
- по человеку: `SELECT name,n,n_mine,first,last FROM chats WHERE name LIKE '%<имя>%'`
- по телефону: `SELECT name,handle,wa_phone FROM people WHERE wa_phone LIKE '%<хвост>'` (leads.db)
- по словам: `SELECT chat_name,sender,text FROM messages_fts WHERE messages_fts MATCH '<слово>' LIMIT 20`
Витрины: [[_WhatsApp-People-Index]] (люди) · [[_WhatsApp-Chats-Index]] (все чаты, включая ниже порога).

## Смежное
- `expand_query.py <слово> [--grep] [--line]` — развернуть слово во все написания для grep по волту или для скармливания в `/ask` (RAG-хук).
- Индекс `names.db` пересобирается недельной задачей (и вручную `name_index.py --vault`). Если после большого импорта чего-то не хватает — упомяни, что нужна пересборка; сам не запускай без спроса.

## Ответ
- Дай список/таблицу (display · тип · файл-ссылка); для длинного — `--html` дашборд.
- Компания всплывает первой по запросу фирмы + связанные люди.
- Если 0 хитов — скажи прямо, предложи проверить написание или пересобрать индекс; не угадывай.
- Коротко; закончи 🧒-рекапом.

## Не путать
- `/ask` = по смыслу (RAG, эмбеддинги). `/find` = по написанию (детерминированный отпечаток). Канон-память [[smart-name-search]].


ARGUMENTS: Мерлион

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python namesearch/find_name.py Мерлион 2>&1 | head -60; echo \"exit=$?\"", "description": "Search name index for Мерлион"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && set -o pipefail && PYTHONUTF8=1 python namesearch/find_name.py Мерлион 2>&1 | head -80; echo \"exit=$?\"", "description": "Search name index for Мерлион"}

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/07-People/Companies\" && head -30 merlion.md; echo ---; head -15 merlion-historical.md", "description": "Peek at main Merlion company notes"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py sig --model \"Opus 5.5\"", "description": "Get fleet signature line"}

---

**Claude:**

🔎 **«Мерлион»**: по точному совпадению нашлось 17 карточек компании и 7 контактов. В индексе 247 похожих имён (поиск выполнен через `find_name.py`, exit 0).

**Компания: главная карточка и её филиалы**
| Карточка | Файл |
|---|---|
| **Мерлион** (основная, 68 человек) | `07-People/Companies/merlion.md` |
| Merlion (historical), 1 человек | `merlion-historical.md` |
| Москва (2 записи) | `merlion-moskva.md`, `merlion-msk.md` |
| Новосибирск (2) | `merlion-novosibirsk.md`, `merlion-nsk.md` |
| Иркутск (2) | `merlion-irkutsk.md`, `merlion-irk.md` |
| Красноярск (2) | `merlion-krasnoyarsk.md`, `merlion-kras.md` |
| Екатеринбург, Самара, СПБ, Ростов-на-Дону, СЭБ, Фин, ранее МЕРЛИОН-ДВ | по одной карточке |

**Люди с «Мерлион» в имени или подписи**
| Кто | Файл |
|---|---|
| Евгений Мильман, директор Мерлион Самара | `07-People/Contacts/Евгений Мильман.md` |
| Екатерина, Мерлион кадры | `Екатерина Мерлион кадры.md` + Apple |
| Офис Мерлион Ирк | `ОФИС Мерлион Ирк.md` + Apple |
| Мерлион Красноярск / Екатеринбург / Москва (общие номера) | `07-People/Contacts/` + Apple |
| Andrew Ayres (лид 2023) | `Platinum-CRM/leads/2023/andrew-ayres.md` |

В основной карточке перечислены 68 сотрудников, например Иван Денисов («Айру, главный»), Александр Ищенко (директор Красноярска), Сергей Васильков (директор филиала) и Аня Борисенко (Восток, продажи).

Похожие имена (Merlin, Merlin Labs, Zerion) к Мерлиону не относятся. Исключение: «Клиент Мерлиона Дудинка».

⚠️ Есть дубли филиалов: Мск и Москва, НСК и Новосибирск, Ирк и Иркутск, Крас и Красноярск. Похоже, одна и та же компания записана под двумя названиями. Если скажешь, склею их через `/dedup`. Склейка меняет старые заметки, поэтому без твоего «да» не делаю (§8.8).

🧒 **Простыми словами:** «Мерлион» у нас записан как большая компания с филиалами по всей России. В главной карточке 68 человек, и ещё несколько отдельных контактов, например директор в Самаре и отдел кадров. Некоторые города записаны дважды под разными названиями, как одна книга на двух полках.

🏛H · Opus 5.5 · 38470
