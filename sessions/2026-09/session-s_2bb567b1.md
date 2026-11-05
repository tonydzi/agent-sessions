---
session: s_2bb567b1
date: 2026-09-23
words: 1067
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2bb567b1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-22-ZB-01-1143
REGISTRY TOPIC: Рынок AI-compute провайдеров (GPU cloud / neocloud) как работодателей: карта компаний + карта ролей под профиль COO/CTO с продуктовым циклом (через dr_start; ПОТРЕБИТЕЛЬ: Куда оператору подаваться на работу в секторе GPU/AI-инфраструктуры и на какие роли) (dr_reconcile 2026-09-23: на диске 2/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-22-ZB-01-1143\results)

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


===== VENDOR: report (DR26-09-22-ZB-01-1143.md) =====
---
id: DR26-09-22-ZB-01-1143
date: 2026-09-22 11:43:11
theme: Рынок AI-compute провайдеров (GPU cloud / neocloud) как работодателей: карта компаний + карта ролей под профиль COO/CTO с продуктовым циклом
session_id: unknown
machine: NODE-0X-2023PAL
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-09-22-ZB-01-1143 — Рынок AI-compute провайдеров (GPU cloud / neocloud) как работодателей: карта компаний + карта ролей под профиль COO/CTO с продуктовым циклом

# Deep Research: рынок AI-compute провайдеров (GPU cloud / neocloud) как РАБОТОДАТЕЛЕЙ

## Кто спрашивает и зачем
[ИМЯ] [ФАМИЛИЯ] — наёмный руководитель уровня COO/CTO, программист (Python, C++), живёт в Пало-Альто, гражданин ЕС + активная O-1 США, готов к релокации. Ищет работу. У него законченный продуктовый цикл за плечами (строил продукты от идеи до выручки) и глубокий операционный опыт. Уже проходил интервью в Lambda Labs на Senior Solution Engineer (сентябрь 2026).

Ему нужно решение: **в какие конкретно компании этого сектора подаваться и на какие роли**.

## Тезис, который надо проверить или опровергнуть
Гипотеза оператора: компании типа Lambda Labs сейчас сверхприбыльны и НЕ ищут клиентов — они выбирают, с кем работать, потому что есть острый дефицит GPU, памяти и вычислительных мощностей. Это продлится ещё несколько лет. Значит, это «излишне богатый» сектор, и туда стоит целиться как соискателю.

Проверь этот тезис фактами. Особенно: правда ли, что у них нет проблемы со спросом, и на сколько лет хватит окна.

## Половина 1 — КАРТА КОМПАНИЙ
1. Полный ландшафт: кто зарабатывает на продаже/аренде GPU-мощностей, compute для обучения моделей, inference и ML-инфраструктуры. Разложи по слоям: гиперскейлеры · «неооблака» (CoreWeave, Lambda, Crusoe, Nebius, Together, Fluidstack, Nscale, IREN, Applied Digital) · inference/serving-платформы (Modal, Baseten, Replicate, fal, RunPod, Anyscale, Fireworks, Deepinfra) · производители чипов со своим облаком (Cerebras, Groq, SambaNova, Tenstorrent) · брокеры и споты (SFCompute, Prime Intellect, Vast.ai) · европейские и азиатские игроки.
2. По каждому значимому: выручка и её рост, кто главные клиенты, какая доля выручки на одном-двух заказчиках (концентрационный риск), стадия (частная / IPO / подана заявка), последний раунд и оценка, численность, где офисы, нанимают ли сейчас и на что.
3. Отдельно: у кого реально «очередь клиентов», а у кого выручка законтрактована с одним гигантом (Microsoft, OpenAI, Nvidia) — это принципиально разные работодатели по риску.
4. Кто из них опасен как работодатель: долговая нагрузка под закупку железа, зависимость от одного контракта, признаки замедления.

## Половина 2 — КАРТА РОЛЕЙ (приоритет)
5. Какие роли в этом секторе реально открыты и чего в них дефицит. Эмпирическое наблюдение из базы вакансий: доминирует **Forward Deployed Engineer** (Modal, Baseten, Nebius, RunPod, Together — у всех), плюс Solutions/Applied AI Engineer, Developer Relations, Product Manager по инфраструктуре, Business Development. Подтверди или опровергни, что FDE — главная точка входа.
6. Что на самом деле требуют в FDE / Solutions Engineer / Applied AI Engineer в этом секторе: обязателен ли глубокий ML-бэкграунд и тренировка моделей, или достаточно сильного инженерного и клиентского профиля. Это ключевой вопрос: у оператора нет ML-research бэкграунда, но есть продукт, операции и код.
7. Куда в этих компаниях берут людей с профилем COO/CTO и законченным продуктовым циклом: Head of FDE, Head of Solutions, VP Operations, Chief of Staff, GM направления, Head of Platform. Есть ли такие вакансии и какая планка.
8. Вилки компенсаций по ролям и уровням, с источниками.
9. Спонсорство виз и отношение к релокации: кто берёт из Европы, кто требует присутствия в Bay Area / NY. У оператора O-1 США активна и паспорт ЕС — где это преимущество.
10. Как в этот сектор реально заходят: через кого, какие каналы, что работает в аутриче, что смотрят в резюме.

## Что нужно на выходе
- Ранжированный шорт-лист 10–15 компаний под ЕГО профиль, с причиной по каждой и с указанием конкретной роли-входа.
- Карта ролей: название роли → что требуют → берут ли туда не-ML людей → его шанс честно.
- Вердикт по гипотезе: окно открыто или уже закрывается, и на сколько.
- Что делать на этой неделе: 3–5 конкретных шагов.

## Требования к ответу
Цифры только с источниками и датами. Где данных нет — скажи «не нашёл», не выдумывай. Отдельно отметь то, что изменилось за последние 3 месяца. Пиши по делу, без воды.



REMINDER: output ONLY the JSON object, nothing else.

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Рынок GPU cloud/neocloud провайдеров как работодателей для профиля COO/CTO",
 "one_line": "Файл содержит только исходный запрос Deep Research (карта компаний-neocloud + карта ролей под профиль COO/CTO), но не фактические результаты ни от одного из вендоров (chatgpt, gemini, grok, claudeai, glm, mistral).",
 "key_findings": [],
 "recommendations": [],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]"],
  "companies": ["Lambda Labs", "CoreWeave", "Crusoe", "Nebius", "Together", "Fluidstack", "Nscale", "IREN", "Applied Digital", "Modal", "Baseten", "Replicate", "fal", "RunPod", "Anyscale", "Fireworks", "Deepinfra", "Cerebras", "Groq", "SambaNova", "Tenstorrent", "SFCompute", "Prime Intellect", "Vast.ai", "Microsoft", "OpenAI", "Nvidia"],
  "products_tools": []
 },
 "open_questions": [
  "Не найдено фактического содержимого отчёта — только текст исходного промпта; неизвестно, был ли Deep Research реально выполнен вендорами",
  "Гипотеза оператора о сверхприбыльности и дефиците спроса в секторе GPU cloud (Lambda Labs и аналоги) не проверена фактами",
  "Ранжированный шорт-лист 10–15 компаний под профиль оператора не сформирован",
  "Карта ролей (FDE/Solutions Engineer/Applied AI Engineer — требования, берут ли не-ML людей) не построена",
  "Вилки компенсаций, визовая политика и каналы захода в сектор не исследованы"
 ],
 "related_concepts": ["job-search-gpu-compute-sector", "forward-deployed-engineer-role", "neocloud-market-map", "hub-job-search", "cofounder-growth-log"]
}
```
