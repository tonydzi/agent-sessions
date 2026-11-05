---
session: s_00bc6451
date: 2026-09-09
words: 851
turns: 7
tools: "Glob, Grep, PowerShell, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-09 · На сольном у THP-17, на своем лутте HP-17, на Хьюльпаг-17. Я делал сенсер о том, что мы бу…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_00bc6451` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

На сольном у THP-17, на своем лутте HP-17, на Хьюльпаг-17. Я делал сенсер о том, что мы будем заметить продажным консалтингом и зарабатывать деньги на консалтинге. Вспомните все, что я делал на ноутсе за последнее время по продажам нашего консалтинга и так далее. И туда подумаем, кому мы это будем продавать. Сделал recall.

---

**Claude:**

Среда, вечер, 19:54, 9 сентября 2026.

🎙 Майк: идём верно — консалтинг как денежный трек мы уже трогали, сейчас подниму всё, что делалось на NODE-0X по этой теме, и тогда предметно решим «кому продавать». Начинаю RECALL.

---

> `Grep` -- {"pattern": "консалтинг|consulting|консалт", "path": "D:\\Vault\\Vault-Knowledge", "-i": true, "output_mode": "files_with_matches", "head_limit": 60}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\lead-with-own-stack-pays-in-audit.md"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\sourcing-by-symptom-not-title.md"}

---

**Claude:**

Память подтянул. Теперь смотрю сессии именно с ноута NODE-0X, где упоминается консалтинг.

---

> `PowerShell` -- {"command": "Get-ChildItem \"D:\\Vault\\Vault-Knowledge\\_session-md\\NODE-0X-NODE-0X\\*.md\" | Sort-Object LastWriteTime -Descending | Select-Object -First 25 Name,LastWriteTime", "description": "List recent NODE-0X session notes by date"}

---

> `Grep` -- {"pattern": "консалтинг|consulting", "path": "D:\\Vault\\Vault-Knowledge\\_session-md\\NODE-0X-NODE-0X", "-i": true, "output_mode": "content", "-C": 2, "head_limit": 120}

---

**Claude:**

Главная сессия нашлась. Читаю синтез из неё и проверяю решения в волте.

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_session-md\\NODE-0X-NODE-0X\\s_afa63177.md", "offset": 356, "limit": 120}

---

> `Grep` -- {"pattern": "консалтинг|consulting|productized|services", "path": "D:\\Vault\\Vault-Knowledge\\02-Decisions", "-i": true, "output_mode": "files_with_matches", "head_limit": 20}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\02-Decisions\\decision-ai-native-business-cc-codex.md"}

---

> `Grep` -- {"pattern": "консалтинг|consulting", "path": "D:\\Vault\\Vault-Knowledge\\10-Tasks", "-i": true, "output_mode": "files_with_matches", "head_limit": 15}

---

**Claude:**

Основа собрана. Добираю свежие куски: SKU-оффер и сентябрьские задачи.

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-05-sirenka-wedge-crypto-pitch.md"}

---

> `Grep` -- {"pattern": "consulting|консалтинг", "path": "D:\\Vault\\Vault-Knowledge\\_session-archive\\catalog-NODE-0X-NODE-0X.json", "-i": true, "output_mode": "content", "-C": 1, "head_limit": 40}

---

**Claude:**

Нашёл ключевую заметку «кому продавать» от 05.09. Читаю её.

---

> `Glob` -- {"pattern": "**/*whom-to-sell*", "path": "D:\\Vault\\Vault-Knowledge"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\2026-09-05-whom-to-sell-ai-automation-now.md"}

---

**Claude:**

Среда, вечер, 19:54, 9 сентября 2026.

RECALL сделан: поднял память, решения в волте и сессии с NODE-0X. Хорошая новость — вопрос «кому продавать» мы уже почти решили, причём совсем недавно. Вот вся картина.

## Что делалось на NODE-0X по продаже консалтинга

**18.06 — Decision Memo «AI-native бизнес на CC+Codex»** ([decision-ai-native-business-cc-codex.md](D:\Vault\Vault-Knowledge\02-Decisions\decision-ai-native-business-cc-codex.md)). Главные выводы: продавать не часы, а фикс-пакеты. Лестница: диагностика $10–25K → спринт $25–60K → ретейнер $5–15K/мес. Стартовая SKU оформлена отдельным one-pager'ом: «AI-Native Readiness Diagnostic». Инвариант «защищай Денис-часы» (он единственный ревьюер). Revenue-модель на 5 месяцев: реалистичный центр ~$200–250K кумулятивно.

**Кофаундер-сессии (июль–август):** «один оффер за 72ч, продать тёплой сети из CRM, не тратить лучшие контакты на пустые интро». Плюс дорожка быстрого кэша: крипто GTM/BD-ретейнер $5–15K/мес и done-for-you AI-автоматизация $2–5K/проект.

**13.08 — DR по SMB-консалтингу** (идея Артура Арсенова, 3/6 рельс — кворум не добран, помнить при ставках): первыми брать бухгалтерские/налоговые фирмы 8–50 человек (маржа 56%, и они сами — канал к своим SMB-клиентам), потом HVAC/сантехники, потом дантисты. Лестница: бесплатный fit-call → аудит $3.5K → один workflow $12–18K → $3–5K/мес.

**05.09 — синтез «Кому продавать AI-автоматизацию сейчас»** ([заметка](D:\Vault\Vault-Knowledge\03-Insights\2026-09-05-whom-to-sell-ai-automation-now.md)) + открытая задача [task-2026-09-05-sirenka-wedge-crypto-pitch.md](D:\Vault\Vault-Knowledge\10-Tasks\task-2026-09-05-sirenka-wedge-crypto-pitch.md). Это самый свежий и самый конкретный ответ.

## Кому продаём — ответ уже есть, три круга

**Круг 1 (самый горячий, наша родная база): crypto/web3-организации из нашей CRM.** База 18 381 лидов почти целиком telegram-native — ровно тот сегмент, где «второй мозг для организации» (Сиренка-клин: архив сообщений + CRM-слой + drip) — наш родной лёд, а не красный океан Glean/Dust. Уже названы первые кандидаты T4_hot из США: Jenna Peterson (OpenDeFi, COO), Mehow (MatterFi, CEO), FJ Paul (Stable Finance), Horvat O'Grady (CPA, Cryptedge — одновременно клиент и канал-партнёр).

**Круг 2 (руками Артура): SMB с улицы.** В нашей CRM целевых SMB-вертикалей ~ноль (замер 05.09), поэтому покупателей добываем с улицы, а из базы берём канал-партнёров (CPA: Zach Gordon, O'Grady, Greg Tomaselli). Открытый вопрос с 05.09 висит до сих пор: Артур так и не подтвердил, берёт ли он воронку как охотник.

**Круг 3 (тёплая Долина): Readiness Diagnostic $10–20K.** Фаундеры/VP Eng/COO из тёплой сети — по принципу из памяти: искать по симптому и достижимости, а не по титулу; человек, публично кричащий «мои агенты разбежались», уже сам себя квалифицировал. И помнить правило: лид со своим стеком платит аудитом/находками, а не покупкой установки.

## Что НЕ сделано (вот где затык, а не в «кому»)

Задача Сиренка-клина открыта с 05.09, review_after — 12.09 (через 3 дня), и ни один из трёх acceptance-пунктов не закрыт: нет оффера-одностраничника, нет 3–5 первых касаний, нет ни одного ответа лида в CRM. Ответ Артуру ушёл 05.09 — реакции нет, фоллоуап не делался.

🎙 Майк: идём верно — но мы четвёртый раз за лето «думаем, кому продавать», а первых касаний по уже названным четырём живым людям так и нет. Мой ход как кофаундера: не заказывать новый ресёрч, а в следующем заходе написать одностраничник Сиренка-клина с ценовой лестницей и сделать первые 3–5 касаний по T4-списку через /triage + safe_send (исходящее лидам — как раз работа хаба). Скажи «+» — и я стартую именно это; если хочешь сначала глазами — соберу оффер и покажу до→после перед отправкой.

🧒 Простыми словами: мы уже трижды хорошо подумали и записали, кому продавать. Ответ: сначала — крипто-командам из нашей же записной книжки (им продаём «второй мозг»), параллельно — бухгалтерам в Америке через Артура, и дорогой аудит — тёплым знакомым из Долины. Думать больше не надо — надо постучаться к четырём конкретным людям, которых мы выбрали ещё 5 сентября, но так и не написали им.
