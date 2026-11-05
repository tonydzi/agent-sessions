---
session: s_d6f0bed6
date: 2026-10-20
words: 1145
turns: 4
tools: "Bash, Read, ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-20 · Рынок 2026: платное обучение и сообщества для power-юзеров Claude Code / Codex / AI-агенто…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d6f0bed6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Рынок 2026: платное обучение и сообщества для power-юзеров Claude Code / Codex / AI-агентов (клубы, коучинг, консалтинг).
1) Кто конкуренты (сообщества, курсы, коучи, агентства), цены, формат, размер аудитории.
2) Что реально покупают: B2C vs B2B, типичные чеки, воронка (бесплатный контент -> пилот -> клуб).
3) Каналы продвижения для RU и EN аудитории (Telegram, X, YouTube, GitHub), что работает с малым бюджетом.
4) Риски и провалы похожих клубов.
Дай факты со ссылками и датами, отметь, что не подтверждено.

---

**Claude:**

Сначала RECALL по волту (§0.3) и подключаю веб-поиск.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports 2>/dev/null && timeout 90 python brain_ask.py \"платное сообщество клуб Claude Code обучение консалтинг конкуренты цены\" 2>&1 | head -60", "description": "RECALL по волту: прошлые исследования клуба", "timeout": 100000}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude-AI\\conversations\\2026-08-28-platnye-telegram-kluby-rynok-konkurenciya-i-fandrayzing-v-si-1f0ed490.md", "limit": 120}

---

> `WebSearch` -- {"query": "Claude Code paid community course cohort price 2026", "mode": "extended"}

---

> `WebSearch` -- {"query": "Skool Claude Code community members monthly price AI agents", "mode": "standard"}

---

> `WebSearch` -- {"query": "курс Claude Code платный клуб Telegram цена 2026 обучение AI-агенты", "mode": "standard"}

---

**Claude:**

Первая волна дала цены Skool и курсов. Добираю B2B/консалтинг, каналы и провалы.

---

> `WebSearch` -- {"query": "Claude Code corporate training enterprise workshop price per seat AI agent consulting rates 2026", "mode": "extended"}

---

> `WebSearch` -- {"query": "Skool community churn AI course creators fail refund complaints 2026 hype AI education", "mode": "extended"}

---

> `WebSearch` -- {"query": "AI Builder Club Claude Code Skool free community funnel YouTube to paid conversion rate", "mode": "standard"}

---

> `WebSearch` -- {"query": "Telegram Stars paid channel subscriptions commission 2026 Tribute Telegram paid community fee", "mode": "standard"}

---

**Claude:**

# Рынок платного обучения и сообществ по Claude Code / Codex / AI-агентам, 2026

**Метод:** я искал сам, без панели чужих LLM. Это не полноценный ДР. RECALL по волту показал, что точного ресёрча по теме нет. Ближайшее — ДР от 28.08 про CatchClub (платформы для TG-клубов), он отвечает на другой вопрос. Почти все источники ниже — обзоры самих продавцов или партнёрские сайты. Цифры считай ориентирами.

## 1. Конкуренты, цены, аудитория

**Skool-сообщества (EN), ежемесячная подписка:**

| Сообщество | Цена | Аудитория | Источник |
|---|---|---|---|
| Chase AI+ | $98/мес или $58/мес за год | больше 1000 участников | [обзор](https://aifunnelinsider.com/chase-ai-skool-review/) |
| Agentic Academy (Simon Scrapes) | $37/мес, анонс роста до $87 | 1300+ | [обзор](https://aifunnelinsider.com/agentic-academy-review-2026/) |
| Claude Club (Samin Yasar) | $97/мес, анонс роста до $120 | 304+ | [обзор](https://aifunnelinsider.com/claude-club-skool-review-2026/) |
| Claude AI Community | $49/мес (founding price) | 598 | [Skool](https://www.skool.com/ai-leaders-1796) |
| Claude Codex Mastery | $9/мес навсегда | не указано | [Skool](https://www.skool.com/yar-ai-automation-school-9911/about) |
| AI Automation Society Plus | около $99/мес | не проверял | [сводка](https://www.aibuilderclub.com/blog/best-claude-code-courses-2026) |
| AItomation Academy | около $69/мес (founder rate) | не указано | [обзор](https://www.aitomationacademy.com/blog/best-claude-courses) |

**Когорты и курсы:**
- AI Hero, живая когорта на 2 недели: $795 ([сводка](https://fast.io/resources/claude-code-course-guide/)).
- Code with Mosh: $249 за 9 часов ([сводка](https://fast.io/resources/claude-code-course-guide/)).
- Udemy: $15-25 по скидке ([сводка](https://fast.io/resources/claude-code-course-guide/)).
- Официальные курсы Anthropic бесплатные, включая курс для опытных разработчиков ([kod.ru, 28.07.2026](https://kod.ru/anthropic-besplatnyj-kurs-claude-code)). Это потолок для платной базы: платить надо за то, чего в бесплатном курсе нет.

**RU-рынок:**
- Курс «ИИ-бот на Claude Code и n8n»: 9 900 ₽ по акции на 16.09.2026 ([toolfox](https://toolfox.ru/courses/c/claude-code-skillbox)).
- Курс на Stepik, цена не видна ([Stepik](https://stepik.org/course/280316)).
- Форум Infostart: упоминается курс за 20 000 ₽ ([Infostart](https://forum.infostart.ru/forum9/topic342308/message3283468/)).
- **Не подтверждено:** я не нашёл ни одного платного Telegram-клуба именно по Claude Code с публичной ценой и размером. Он может существовать закрыто. Нужен отдельный поиск по самим TG-каналам.

## 2. Что покупают

**B2B-корпоративное обучение (там чеки выше всего):**
- Команда: $4 500-12 500 за воркшоп или серию, от $30 000 за внедрение. Публичные когорты: $1 000-2 000 за место. Индивидуальный коучинг: $200-400 за час ([Arcforma](https://arcforma.ai/blog/how-much-does-claude-training-cost-2026)).
- Claude Workshop: $1 000 за человека в день, минимум 8 человек ([claudeworkshop.com](https://www.claudeworkshop.com/training)).
- Syntalith: от €1 200 в день на группу до 15 человек ([Syntalith](https://syntalith.ai/en/blog/claude-training-for-companies-2026)).
- Workshops.de: 5 утренних сессий за €1 679 ([Workshops.de](https://workshops.de/en/courses/software-engineering-claude-code)).
- Сингапур: S$397 с человека за день, от 10 человек ([Keith Teo](https://keithteo.ai/blog/best-claude-code-workshops-singapore-2026/)).
- Это цены на сайтах самих продавцов. Реальные сделки неизвестны.

**B2C:** подписка $9-100 в месяц, разово $15-800. Чем дешевле чек, тем больше людей, но обслуживать приходится больше народа за те же деньги.

**Воронка.** Рабочая схема из публичных примеров:
1. YouTube.
2. Бесплатная Skool-группа с челленджем.
3. Платный клуб.

Примеры: [Leon van Zyl](https://www.skool.com/leonvanzyl/about) (бесплатная AI Builder Hub, платный Agentic Labs), [Luke](https://www.skool.com/ai-automation-hub-5735/welcome-post-free-skool-community). Luke прямо пишет, что бесплатные группы быстро затихают, поэтому он открыл платную. **Конверсию я не нашёл нигде.** Ни по клубам, ни по пилотам. Это закрытые данные, их надо спрашивать у авторов лично.

**Что нашёл про пилот.** Таких данных открыто нет. Из рынка видно только, что B2B-предложения продают воркшопом на день или серией с фиксированной ценой.

## 3. Каналы (малый бюджет)

- **EN:** YouTube — главный источник входа. Skool-клубы почти все привязаны к YouTube-каналу автора ([подборка авторов](https://thesearchsherpa.com/best-youtube-creators-claude-code-2026/)). X и GitHub как каналы продаж я не проверял: данных нет.
- **RU:** Telegram как канал и как место оплаты. Платные подписки в TG идут через Stars (по неподтверждённым данным, 30% Telegram, плюс 30% Apple/Google при покупке Stars на мобильном) или через Tribute (10% или 20%, источники противоречат). Это [Telegram](https://telegram.org/blog/superchannels-star-reactions-subscriptions/be?setln=en), [ExitBid](https://exitbid.io/blog/telegram-bot-monetization-2026), [Habr](https://habr.com/ru/articles/1033346/). **Проверь ставки на официальных страницах до расчёта юнит-экономики.**
- **Не подтверждено:** какой канал даёт самый дешёвый платящий клик в RU. Данных нет, нужен эксперимент.

## 4. Риски и провалы

- **Возвраты.** Решает админ клуба, Skool не вмешивается. Есть жалобы в BBB: человек просит вернуть деньги, админ молчит ([BBB](https://www.bbb.org/us/ca/el-segundo/profile/online-shopping/skool-1216-1000037014/complaints)). Контент за «уровнями» вызывает претензии ([Trustpilot](https://www.trustpilot.com/review/www.skool.com)).
- **Тонкий контент.** Типичная жалоба: переупакованные бесплатные туториалы за деньги ([ранжирование](https://aiprofitboardroom.com/blog/best-ai-community-on-skool/)). Это особенно опасно, раз у Anthropic курсы бесплатные.
- **Тактика «цена вырастет на N участников».** Рецензенты называют её искусственной срочностью ([AI Builders review](https://aifunnelinsider.com/ai-builders-skool-review-2026/)).
- **Платформенная зависимость от Telegram.** Tribute потребовал от издания «Волна» убрать публикации ([Новая газета Europe, 17.09.2025](https://novayagazeta.eu/articles/2025/09/17/servis-donatov-v-telegram-potreboval-ot-emigrantskogo-izdaniia-volna-udalit-publikatsii-s-lgbt-flagami-i-svastikoi-news)). Комиссии и правила меняются без согласования.
- **Устаревание.** Инструменты меняются быстрее программ. Это мой вывод, а не источник.
- **Не нашёл:** статистику оттока (churn), закрытия клубов, число авторов, ушедших в минус. Публично такого нет. Данные только у владельцев.

## Что не подтверждено и как закрыть

1. Конверсия бесплатный → клуб → пилот: спросить 3-5 авторов напрямую.
2. Платные RU Telegram-клубы по Claude Code: отдельный поиск по самим каналам.
3. Ставки Tribute и Stars: официальные страницы.
4. Реальные B2B-сделки: заявленные цены не равны закрытым.

🧒 **Простыми словами:** я нашёл, что делают другие и сколько просят. Клубы стоят от 9 до 100 долларов в месяц. Корпоративные занятия стоят от тысячи долларов за человека в день. Хуже всего у меня с данными о том, сколько людей реально платит и сколько уходит. Их знают только владельцы клубов, у них стоит спросить напрямую. Ещё бесплатные курсы Anthropic ставят планку: платить стоит только за то, чего там нет.

Sources:
- [fast.io: 7 Best Claude Code Courses](https://fast.io/resources/claude-code-course-guide/)
- [AItomation Academy](https://www.aitomationacademy.com/blog/best-claude-courses)
- [aifunnelinsider: Chase AI+](https://aifunnelinsider.com/chase-ai-skool-review/)
- [Arcforma: Claude training cost](https://arcforma.ai/blog/how-much-does-claude-training-cost-2026)
- [Claude Workshop](https://www.claudeworkshop.com/training)
- [Telegram blog](https://telegram.org/blog/superchannels-star-reactions-subscriptions/be?setln=en)
- [BBB: Skool](https://www.bbb.org/us/ca/el-segundo/profile/online-shopping/skool-1216-1000037014/complaints)
