---
session: s_41e878cc
date: 2026-09-27
words: 1840
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_41e878cc` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-26-HUB-01-2230
REGISTRY TOPIC: Jev (TypeSafe AI System One) — переносить ли решающие точки флота на типизированную decision-модель (dr_reconcile 2026-09-27: на диске 3/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-26-HUB-01-2230\results)

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


===== VENDOR: report (DR26-09-26-HUB-01-2230.md) =====
---
id: DR26-09-26-HUB-01-2230
date: 2026-09-26 22:30:05
theme: Jev (TypeSafe AI System One) — переносить ли решающие точки флота на типизированную decision-модель
session_id: hub-PaloAlto voice001 Jev 26.09
machine: HUB-01
targets: chatgpt,gemini,grok,glm,mistral
---

# DEEP RESEARCH: Jev (TypeSafe AI, "System One" decision model) — стоит ли переносить на него решающие точки агентного флота

## КОНТЕКСТ ЗАКАЗЧИКА (факты, не додумывать)
Заказчик — [ИМЯ] [ФАМИЛИЯ], Пало-Альто. У него флот из 5+ машин, на каждой круглосуточно работают
LLM-агенты (Claude Code как оркестратор + Codex/Grok/GLM/Gemini/Mistral как исполнители). Внутри
флота ДЕСЯТКИ «решающих точек», где сегодня решение принимает либо регулярка/эвристика, либо целая
LLM генерацией текста:
- маршрутизация голосовых заметок по адресам (живой исполнитель / правило в канон / сессия-стройка / карточка человека / контент-воронка);
- триаж входящих лидов по тирам (кому отвечать первым, кто шум);
- детектор «ИИ-слопа» в исходящем тексте (пройдёт/не пройдёт вкусовой гейт);
- гейт площадок (тизер ≤240 / средний / лонгрид — можно ли этот текст в этот канал);
- гейт отказа рельсы в Deep Research (рельса реально ответила или отказалась/не искала);
- подбор скилла под сообщение пользователя (сейчас — хук с ключевыми словами);
- классификация «этот PR/issue/тред стоит нашего касания или нет».
Объём: тысячи вызовов в сутки. Подписки на LLM уже оплачены (Claude Max $200, ChatGPT Pro $200,
SuperGrok $300, GLM $16, Gemini $20) + OpenRouter поштучно как фолбэк.

## ЧТО ИЗВЕСТНО НА 26.09.2026 (проверить и опровергнуть, если неверно)
- Jev — первая «System One»-модель компании TypeSafe AI; основатель Diogo Almeida, один из
  исследователей ChatGPT/InstructGPT. Модель НЕ генерирует свободный текст: она отвечает на
  заранее типизированные вопросы — Noul (вероятность 0..1), Choice (выбор из ≤255 опций с
  probabilities + confidence), Score (шкала 2-10 уровней).
- API: POST https://api.typesafe.ai/v1/systemone, Bearer-ключ, поля state + model + questions,
  ответ answers + usage{input_tokens, output_tokens}. Версия jev-1.13.0, контекст 32K, только текст.
- Цена: $0.042 за 1M входных токенов, выходные токены НЕ тарифицируются. Заявленная задержка
  70-500 мс (наблюдения до 81 мс).
- Доступ также через OpenRouter (POST /api/alpha/decisions, модель typesafe/jev-1.13),
  Cloudflare AI, AI/ML API, LiteLLM pass-through, Pydantic AI; есть Python и JS SDK (typesafe-sdk),
  есть drop-in agent-skill для Claude Code/Codex, есть awesome-jev и ~750 публичных кейсов.
- Компания привлекает >$1 млрд при оценке от $10 млрд (неделей ранее раунд по оценке $200 млн).

## ВОПРОСЫ, НА КОТОРЫЕ НУЖЕН ОТВЕТ С УЛИКАМИ
1. ЧТО ЭТО ТЕХНИЧЕСКИ. Как устроена System One модель: чем отличается от (а) классификатора на
   эмбеддингах + логрег, (б) LLM со structured outputs / constrained decoding, (в) cross-encoder
   реранкера, (г) маленькой локальной модели (ModernBERT, DeBERTa, Qwen-0.6B)? Есть ли статья,
   тех-репорт, карточка модели? Что именно означает «не генерирует токены ответа» на уровне
   архитектуры и почему выходные токены бесплатны?
2. КАЛИБРОВКА. Насколько probabilities и confidence реально калиброваны (ECE, Brier, reliability
   diagrams)? Кто мерил независимо? Где документированная «jaggedness» (у них есть страница
   model-jaggedness/jev-1.13) — какие задачи модель проваливает системно?
3. НЕЗАВИСИМЫЕ БЕНЧМАРКИ vs LLM. Реальные замеры качества/скорости/цены на задачах класса
   «спам», «категория комментария», «тональность», «интент-роутинг», «guardrails», «реранк RAG»:
   Jev против GPT-5-nano/mini, Claude Haiku, Gemini Flash-Lite, локального энкодера. Русский язык
   отдельно: есть ли деградация на не-английском?
4. ГДЕ ОНА ЛОМАЕТСЯ. Failure modes: длинный state (32K), много вопросов за раз, зависимые вопросы,
   вопросы, требующие рассуждения/цепочек, отрицания, сарказм, смешанные языки, домен-специфика,
   числа/даты. Что говорят практики, у которых Jev дала хуже, чем LLM?
5. ЭКСПЛУАТАЦИЯ. Rate limits (реальные, не документные), 429/529 частота, SLA/uptime, тайм-ауты,
   батчинг, параллельные вопросы, идемпотентность, версионирование модели (что происходит с
   калибровкой при смене jev-1.13 -> следующая), депрекейшн-политика.
6. ПРИВАТНОСТЬ И ЮРИДИКА. Data retention: логируются ли state и вопросы, используются ли для
   обучения, есть ли zero-retention/enterprise-режим, где физически обрабатываются данные, DPA,
   GDPR/EU. ВАЖНО: в state поедут тексты живых людей (личные переписки, лиды, транскрипты звонков).
   Что можно и что нельзя отправлять. Как это выглядит при доступе через OpenRouter/Cloudflare
   (кто ещё видит данные в этой цепочке)?
7. ВЕНДОР-РИСК. Стадия компании, раунды, кто инвесторы, команда, срок жизни early access, риск
   резкой смены цены после закрытия раунда ($10B оценка при цене $0.042/1M — где экономика?).
   План Б, если рельса умрёт или подорожает в 100 раз: чем заменить без переписывания.
8. ПАТТЕРНЫ ВНЕДРЕНИЯ. Разобрать их же паттерны (speculative fan-out, confidence-gated routing,
   composite scoring, intent routing, SDE cascade, guardrails, self-consistency) и сказать честно,
   какие из них дают выигрыш, а какие — маркетинг. Как правильно ставить порог по confidence и
   строить каскад «Jev решает дешёво -> при низкой уверенности эскалация в LLM».
9. ПРИМЕНИМО К НАШЕМУ ФЛОТУ. Из семи наших решающих точек (список выше) — какие ПЕРЕНОСИТЬ на Jev
   в первую очередь, какие НИКОГДА, и почему. Для каждой: типы вопросов (Noul/Choice/Score),
   что кладём в state, где ставим порог, чем меряем успех, сколько это стоит в месяц при
   ~5000 решений в сутки. Дай конкретные схемы вопросов, а не общие слова.
10. МЕТОДИКА ПРИЁМКИ. Как честно проверить Jev на НАШИХ данных: сколько размеченных примеров нужно
    на точку решения, как строить shadow-прогон, какие метрики (precision/recall на КАЖДОМ классе,
    не accuracy), как ловить дрейф, когда признать «хуже, чем было» и откатиться.
11. КОНКУРЕНТЫ И АЛЬТЕРНАТИВЫ. Кто ещё делает «decision layer» (System One, typed decisions):
    другие вендоры, open-source аналоги (в т.ч. упоминаемые открытые модели вроде Kev/SemIf),
    self-hosted вариант. Таблица: цена за 1M решений, задержка, качество, замкнутость на вендора.
12. ЭКОНОМИКА ПЕРЕХОДА. Точка окупаемости: у нас подписки УЖЕ оплачены (fixed cost), значит
    «дешевле, чем LLM» — не аргумент сам по себе. Где Jev даёт реальный выигрыш: задержка,
    детерминизм, отсутствие парсинга, калиброванная уверенность, экономия лимитов подписки на
    другую работу? Посчитай на числах.

## ФОРМАТ ОТВЕТА
- Вердикт первым абзацем: внедрять / внедрять точечно / не внедрять — и почему, в 5 строках.
- Дальше разделы по вопросам 1-12, каждый факт со ссылкой (URL + дата). Без ссылки = помечай 🤔 гипотеза.
- Отдельная таблица «наши 7 точек решения x внедрять да/нет x схема вопросов x риск».
- Отдельный блок «что проверить руками за 1 час, чтобы решение стало доказанным».
- В конце: что ты НЕ смог проверить и почему.
- Живой веб-поиск обязателен, укажи, какие источники читал. Русский язык ответа.

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Jev (TypeSafe AI System One) — переносить ли решающие точки флота на типизированную decision-модель",
 "one_line": "Deep-research оценивал, стоит ли переносить решающие точки агентного флота оператора (маршрутизация, триаж, слоп-гейт, гейт площадок и др.) на типизированную decision-модель Jev от TypeSafe AI вместо LLM-генерации или эвристик.",
 "key_findings": [
  "Jev (jev-1.13.0) — не текст-генератор, а модель, отвечающая на типизированные вопросы трёх форматов: Noul (вероятность 0..1), Choice (выбор из ≤255 опций с probabilities+confidence), Score (шкала 2-10 уровней); контекст 32K, только текст",
  "Цена $0.042 за 1M входных токенов, выходные токены не тарифицируются; заявленная задержка 70-500 мс (наблюдения до 81 мс)",
  "Доступ возможен через прямой API, OpenRouter, Cloudflare AI, AI/ML API, LiteLLM, Pydantic AI, есть Python/JS SDK и агент-скилл для Claude Code/Codex, ~750 публичных кейсов",
  "Компания TypeSafe AI привлекает раунд с оценкой >$1 млрд при базе от $10 млрд, всего неделей ранее был раунд с оценкой $200 млн — резкий скачок оценки при заявленной цене $0.042/1M токенов создаёт вопрос об экономике и вендор-риске",
  "Задание требовало проверки калибровки (ECE/Brier), независимых бенчмарков против GPT-5-nano/mini, Claude Haiku, Gemini Flash-Lite и локальных энкодеров, а также поведения на русском языке — заказчик отметил, что у TypeSafe AI есть собственная страница 'model-jaggedness/jev-1.13', документирующая системные провалы модели",
  "У оператора подписки на LLM уже оплачены как fixed cost (Claude Max $200, ChatGPT Pro $200, SuperGrok $300, GLM $16, Gemini $20 + OpenRouter фолбэк) — поэтому аргумент 'Jev дешевле LLM' сам по себе недостаточен, ценность нужно искать в задержке, детерминизме, калиброванной уверенности и экономии лимитов подписки на другую работу",
  "Семь решающих точек флота, для которых рассматривался перенос: маршрутизация голосовых заметок, триаж лидов по тирам, детектор ИИ-слопа, гейт площадок, гейт отказа рельсы в Deep Research, подбор скилла под сообщение, классификация GitHub PR/issue на стоящие внимания",
  "Заказ прямо требовал вердикт 'внедрять / внедрять точечно / не внедрять' с конкретными схемами вопросов (Noul/Choice/Score) и порогами confidence по каждой из семи точек, а также методику приёмки на реальных данных (shadow-прогон, precision/recall по классам, план отката)"
 ],
 "recommendations": [
  "Не принимать решение о переносе решающих точек на Jev без независимых бенчмарков (не только маркетинговых цифр вендора) на задачах, близких к реальным (спам, триаж, гейты) и отдельно на русском языке",
  "Перед внедрением проверить приватность: данные state (личные переписки, лиды, транскрипты звонков) не должны уходить без ясного data retention / zero-retention режима, особенно при доступе через OpenRouter/Cloudflare, где в цепочке появляются дополнительные посредники",
  "Заложить план Б на случай удорожания/смерти рельсы Jev (компания на ранней стадии, резкий рост оценки) — не переписывать архитектуру решающих точек так, чтобы они были жёстко привязаны к одному вендору",
  "Внедрять точечно и через shadow-прогон/dogfood на своих данных с метриками precision/recall по каждому классу, а не accuracy, прежде чем заменять существующие эвристики/LLM-точки",
  "Использовать каскадный паттерн 'confidence-gated routing': Jev решает дешёво, при низкой уверенности — эскалация в LLM, а не полная замена LLM на всех семи точках"
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]", "Diogo Almeida"],
  "companies": ["TypeSafe AI", "OpenRouter", "Cloudflare", "AI/ML API"],
  "products_tools": ["Jev (jev-1.13.0)", "System One", "typesafe-sdk", "LiteLLM", "Pydantic AI", "Claude Code", "Codex", "Grok", "GLM", "Gemini", "Mistral", "ModernBERT", "DeBERTa", "Qwen-0.6B"]
 },
 "open_questions": [
  "Реальная калибровка probabilities/confidence (ECE, Brier, reliability diagrams) — не проверена независимо в заказе, только запрошена",
  "Независимые бенчмарки Jev против GPT-5-nano/mini, Claude Haiku, Gemini Flash-Lite и локальных энкодеров, включая деградацию на русском языке",
  "Failure modes: длинный state, зависимые вопросы, отрицания, сарказм, смешанные языки, числа/даты — задокументированы ли конкретные случаи, где Jev хуже LLM",
  "Реальные rate limits, частота 429/529, SLA/uptime, политика депрекейшна и что происходит с калибровкой при смене версии модели",
  "Юридический статус данных: логируются ли state и вопросы, используются ли для обучения, есть ли enterprise zero-retention режим, где физически обрабатываются данные, DPA/GDPR",
  "Экономика вендора при оценке $10 млрд и цене $0.042/1M токенов — риск резкого повышения цены после закрытия раунда",
  "Конкуренты и open-source аналоги decision-layer (включая упомянутые Kev/SemIf) и self-hosted альтернативы — сравнительная таблица не была подтверждена в самом задании (это вопросы к ответу, не выводы)",
  "Сам текст ответа/синтеза vendor-секций с фактическими выводами по всем 12 вопросам не включён в предоставленный фрагмент — есть только постановка задачи (промпт), не сам DR-ответ"
 ],
 "related_concepts": ["model-routing-fable-smart", "burn-the-limits-utilization", "dr-max-thinking-and-wide-fanout", "ai-slop-gate", "platform-matrix-gate", "vendor-risk-assessment"]
}
```
