---
session: s_17db690e
date: 2026-10-08
words: 937
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-08 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_17db690e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-08-HUB-01-0421
REGISTRY TOPIC: MUSE / Instinct / Dots — архитектура, доступ из ЕС, программная дверь, вердикт по трём миссиям (dr_reconcile 2026-10-08: на диске 3/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-08-HUB-01-0421\results)

Return ONLY a JSON object (no prose, no code fence) with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "topic": "<clean human topic of the research, <=90 chars>",
 "one_line": "<one sentence: what question this deep-research answered>",
 "key_findings": ["<substantive conclusion grounded in the report>", "..."],
 "recommendations": ["<concrete recommendation / decision the report implies>", "..."],
 "entities": {"people": ["..."], "companies": ["..."], "products_tools": ["..."]},
 "open_questions": ["<what stayed unresolved / needs verification>", "..."],
 "related_concepts": ["<short concept name this connects to, for cross-linking>", "..."]
}
Rules: extract ONLY from the report text; never invent people, numbers or claims not present.
Merge across the vendor sections (they research the SAME question) -- deduplicate findings,
prefer the better-supported statement. 4-10 key_findings, be specific (numbers, names, tradeoffs).
If a list is empty use []. Write findings in the report's own language (ru stays ru).

REPORT (vendor sections tagged; may be Russian, English or mixed):


===== VENDOR: report (DR26-10-08-HUB-01-0421.md) =====
---
id: DR26-10-08-HUB-01-0421
date: 2026-10-08 04:21:11
theme: MUSE / Instinct / Dots — архитектура, доступ из ЕС, программная дверь, вердикт по трём миссиям
session_id: H70380
machine: HUB-01
targets: chatgpt,gemini,grok,glm,mistral
---

# Deep Research: MUSE / INSTINCT / DOTS — что это и как этим реально пользоваться

## Один вопрос исследования
Три продукта 2026 года — **Meta Muse** (запуск 08.09.2026), **Instinct** (Spear Street Technology, Noah Shinn, invite-only с августа 2026) и **OpenAI Dots** (DevDay, 29.09.2026) — называют «always-on ИИ-ассистентами». Нужен практический разбор: **чем именно они являются архитектурно, и что конкретно человек, живущий в Европе (Лиссабон/Португалия) и уже имеющий собственный агентный флот на Claude Code + MCP + рутины, может от них получить сегодня — и чего не может.**

## Контекст заказчика (чтобы ответ был применимым, а не обзорным)
- У заказчика уже работает собственная агентная инфраструктура: Claude Code на 5+ машинах, ~100 скиллов, MCP-коннекторы (Telegram, WhatsApp, Gmail, Calendar, Drive, Trello), ночные рутины, своя шина между машинами, CRM, векторный поиск по базе знаний.
- Три активные миссии: (1) трудоустройство в frontier ИИ-лабораторию, поток подач и собеседований; (2) привлечение инженеров-тестеров к своим OSS-инструментам; (3) фандрайзинг стартапа.
- География: ЕС (Португалия). Это важно: Muse — только США/Канада, Dots — не выкатился на EU/UK для Pro.
- Подписки: ChatGPT, Claude Max, Grok, Gemini, GLM, Mistral.

## Что обязательно закрыть (по каждому из трёх продуктов отдельно)
1. **Классификация без воды.** Это новая LLM? Обёртка-харнесс над существующей моделью? Продукт-ассистент? Назови модель под капотом (Muse Spark, GPT-6 Astra, что у Instinct) и скажи прямо: что здесь новое — модель или харнесс.
2. **Механика исполнения.** Чем именно действует агент: собственный облачный компьютер? браузер? телефонные звонки? коннекторы к приложениям? какой список коннекторов на деле (а не в пресс-релизе)? что происходит, когда коннектора нет.
3. **Цена и доступ на 08.10.2026.** Тарифы, что входит в базу, что сверху. Для Instinct — как реально получают инвайт (система «5 инвайтов на юзера», где просить). Для Dots — какой план ChatGPT нужен и в каких странах уже включили. Для Muse — статус EU.
4. **Доступ из ЕС.** Что работает законно: waitlist, веб-версия, WhatsApp-канал Muse, аккаунт с US-платёжкой. Что нарушает ToS (и чем именно рискует аккаунт). Был ли у кого-то бан за географию — дай реальные случаи, не гипотезы.
5. **Программная дверь.** Есть ли API, SDK, webhook, CLI, MCP-сервер у любого из трёх? Можно ли встроить их как «рельсу» в чужой агентный флот — или это закрытый consumer-продукт без двери? Если двери нет, скажи «двери нет» прямо.
6. **Где они объективно сильнее собственного флота на Claude Code + MCP.** Назови конкретные задачи, которые Muse/Instinct/Dots делают, а связка Claude Code + MCP не делает или делает плохо: телефонные звонки от имени пользователя, торг по счетам, заполнение чужих веб-форм без API, персистентность между сессиями, мобильный вход. И наоборот — где собственный флот сильнее.
7. **Риски передачи доступа.** Что эти продукты требуют: карта на файле до первого использования, OAuth к почте/календарю/банку, сохранённые credentials. Что известно про утечки, инциденты, политику хранения, обучение на данных пользователя. Что именно нельзя им отдавать.
8. **Коллизия имён.** Отдельно: arXiv-работа «MUSE: A Unified Agentic Harness for MLLMs» (arxiv.org/html/2606.03005v1) — это НЕ продукт Meta, а исследовательский харнесс. Стоит ли он чтения как инженерный материал: что в нём воспроизводимо (структурированный парсинг, детерминированная верификация, verifier-guided repair), есть ли код, какие заявленные прибавки на каких моделях.
9. **Четвёртый игрок.** В обзорах рядом упоминают «Wajo» — что это, кто делает, стоит ли считать его четвёртым в категории.
10. **Вердикт по трём миссиям заказчика.** Для каждой миссии: какой из трёх (или ни один) реально разгрузил бы работу, какую именно операцию он бы забрал, и что это стоит в деньгах и риске. Если ответ «ни один, собственный флот покрывает» — так и скажи, с обоснованием.

## Контракт вывода (обязателен)
- Для каждого факта о цене, географии и доступности — **дата и URL первоисточника** (блог вендора, страница тарифов, официальный пост). Пресс-пересказы допустимы только как второй слой и помечаются.
- Если факт не найден — пиши **NOT FOUND** явной строкой, не заполняй догадкой. Выдуманный URL хуже отсутствия ответа.
- Отдельная строка в конце: **«не могу судить N из M пунктов, причина»**.
- Таблица-сводка: продукт · вендор · модель под капотом · цена · гео · есть ли API · ключевой риск.
- В конце — **5 конкретных действий** для заказчика на следующую неделю, отсортированных по «дешевле и быстрее сначала».



REMINDER: output ONLY the JSON object, nothing else.

---

**Claude:**

You've hit your weekly limit · resets Oct 10, 4am (Europe/London)
