---
session: s_d5f592d0
date: 2026-10-14
words: 753
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-14 · Base directory for this skill: C:\Users\dev\.claude\skills\find

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d5f592d0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

> `Bash` -- {"command": "cd /e/Obsidian/_imports/namesearch && PYTHONUTF8=1 python find_name.py Мерлион 2>&1 | head -80", "description": "Search names index for Merlion"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/whatsapp && python -c \"\nimport sqlite3;c=sqlite3.connect('wa_live.db')\nfor q in ['Мерлион','Merlion','мерлион']:\n  print(q, c.execute(\\\"SELECT name,n,first,last FROM chats WHERE name LIKE ?\\\",('%'+q+'%',)).fetchall())\n  print(c.execute(\\\"SELECT chat_na

---

> `Bash` -- {"command": "cd \"/e/Obsidian/Vault-Knowledge/07-People/Companies\" && head -30 merlion.md; echo ---; head -20 merlion-historical.md", "description": "Read main Merlion company notes"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py sig --model \"Opus 5.5\" 2>&1 | tail -1", "description": "Get fleet signature line"}

---

**Claude:**

В справочнике имён «Мерлион» нашёлся сразу, без опечаток и вариантов написания. Это 17 карточек компании и 7 контактов. В WhatsApp по словам «Мерлион», «мерлион» и «Merlion» нет ни чатов, ни сообщений.

**Компания**
| Заметка | Что это |
|---|---|
| `07-People\Companies\merlion.md` | Главная карточка «Мерлион» (alias Merlion), в ней **68 людей** |
| `merlion-historical.md` | Merlion (historical), в ней 1 человек |
| Филиалы | Москва (2 карточки: МЕРЛИОН МОСКВА и Мерлион Мск), СПБ, Новосибирск (2: Новосибирск и НСК), Екатеринбург, Красноярск (2: Красноярск и Крас), Иркутск (2: Иркутск и ирк), Самара, Ростов-на-Дону, СЭБ, Фин, «ранее МЕРЛИОН-ДВ» |
| `klient-merliona-dudinka-krasn-krai.md` | Клиент Мерлиона, Дудинка (Красноярский край) |

Люди из главной карточки (первые 10 из 68): Алексей Петрыкин и Иван Вячеславович Денисов (оба с пометкой «Айру», у второго «главный»), Александр Астапенко, Ксения Афанасьева, Анна Семенова, Мирослав Поточный (бытовая техника), Владимир Нечаев, Аня Борисенко (Восток, продажи), Александр Ищенко (директор, Красноярск), Сергей Васильков (директор филиала).

**Контакты** (папка `07-People\Contacts`): Евгений Мильман (директор, Самара), Екатерина Мерлион кадры, Мерлион Красноярск, Мерлион Екатеринбург, ОФИС Мерлион Ирк, общий контакт МЕРЛИОН МОСКВА. Пять из них есть и в контактах Apple.

Совпадает только с CRM-лидом Andrew Ayres (`leads\2023\andrew-ayres.md`), почему именно с ним, я не открывал. Остальное в выдаче (Merlin, Zerion, Berlin) просто похоже по написанию и к Мерлиону не относится.

Получилось 17 карточек на одну компанию: дубли филиалов («Мск» и «МОСКВА», «НСК» и «Новосибирск», «Крас» и «Красноярск», «ирк» и «Иркутск»). Склеить их можно скиллом `/dedup`. Это правка старых заметок, поэтому без твоего ОК трогать не буду.

🧒 **Простыми словами:** Мерлион есть в базе. Это большая компания, у нас в ней 68 знакомых и много филиалов по России. Некоторые филиалы записаны дважды под разными именами, как один человек в телефонной книге под двумя именами. В WhatsApp о Мерлионе переписки нет.

🏛H · Opus 5.5 · 15894
