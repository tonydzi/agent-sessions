---
session: s_09cf66dc
date: 2026-09-23
words: 1491
turns: 4
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_09cf66dc` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

---

**Claude:**

```json
{
  "lang": "ru",
  "topic": "Карта GPU-cloud/neocloud компаний и ролей под профиль COO/CTO оператора",
  "one_line": "Бриф Deep Research ставит вопрос, в какие компании GPU-compute/neocloud сектора и на какие роли подаваться оператору (COO/CTO без ML-research бэкграунда), но доступный текст содержит только запрос-промпт, без сведённых ответов вендоров.",
  "key_findings": [
    "Гипотеза оператора, требующая проверки в отчёте: neocloud-провайдеры (пример — Lambda Labs) сейчас сверхприбыльны из-за острого дефицита GPU/памяти/мощностей и сами выбирают клиентов, а не ищут их; окно, по гипотезе, продержится ещё несколько лет — это НЕ подтверждённый вывод, а тезис на верификацию",
    "оператор уже проходил интервью в Lambda Labs на позицию Senior Solution Engineer (сентябрь 2026)",
    "Эмпирическое наблюдение из его базы вакансий (заявлено в запросе, не результат исследования): в секторе доминирует роль Forward Deployed Engineer — открыта одновременно у Modal, Baseten, Nebius, RunPod, Together",
    "Ключевая неопределённость профиля: у оператора нет ML-research бэкграунда и опыта тренировки моделей, но есть завершённый продуктовый цикл, операционный опыт и код (Python, C++)",
    "У оператора активна виза O-1 США и есть паспорт ЕС — заявлено как потенциальное преимущество при найме/релокации, требующее проверки по компаниям",
    "Landscape сектора структурирован по слоям: гиперскейлеры · neoclouds (CoreWeave, Lambda, Crusoe, Nebius, Together, Fluidstack, Nscale, IREN, Applied Digital) · inference/serving-платформы (Modal, Baseten, Replicate, fal, RunPod, Anyscale, Fireworks, Deepinfra) · чипмейкеры со своим облаком (Cerebras, Groq, SambaNova, Tenstorrent) · брокеры/споты (SFCompute, Prime Intellect, Vast.ai)"
  ],
  "recommendations": [],
  "entities": {
    "people": ["[ИМЯ] [ФАМИЛИЯ]"],
    "companies": ["Lambda Labs", "CoreWeave", "Crusoe", "Nebius", "Together", "Fluidstack", "Nscale", "IREN", "Applied Digital", "Modal", "Baseten", "Replicate", "fal", "RunPod", "Anyscale", "Fireworks", "Deepinfra", "Cerebras", "Groq", "SambaNova", "Tenstorrent", "SFCompute", "Prime Intellect", "Vast.ai", "Microsoft", "OpenAI", "Nvidia"],
    "products_tools": []
  },
  "open_questions": [
    "Подтверждена ли гипотеза о сверхприбыльности и дефиците спроса у GPU-cloud провайдеров, и на сколько лет хватит этого окна",
    "У каких компаний выручка диверсифицирована (реальная очередь клиентов), а у каких сконцентрирована на 1-2 заказчиках (Microsoft/OpenAI/Nvidia) — критично для оценки риска работодателя",
    "Финансовое состояние по каждой компании: выручка и рост, стадия (частная/IPO), последний раунд и оценка, численность, офисы, текущий найм",
    "Кто из провайдеров рискован как работодатель из-за долговой нагрузки на железо или зависимости от одного контракта",
    "Действительно ли Forward Deployed Engineer — главная точка входа в сектор, и что по факту требуют в FDE/Solutions/Applied AI Engineer ролях (обязателен ли ML-бэкграунд)",
    "Куда берут людей с профилем COO/CTO и продуктовым циклом (Head of FDE, Head of Solutions, VP Operations, Chief of Staff, GM, Head of Platform) и какая там планка",
    "Вилки компенсаций по ролям и уровням в секторе, с источниками",
    "Политика спонсорства виз и релокации по компаниям — где O-1 + паспорт ЕС дают реальное преимущество",
    "Через какие каналы реально заходят в сектор (аутрич, резюме, нетворк)",
    "Итоговый ранжированный шорт-лист 10-15 компаний с ролью-входом по каждой — не получен в этом фрагменте отчёта"
  ],
  "related_concepts": ["job-search-gpu-compute", "neocloud-market", "forward-deployed-engineer", "coo-cto-profile-no-ml-background", "lambda-labs-interview", "o1-visa-eu-passport-advantage"]
}
```

---

**User:**

Stop hook feedback:
СТОП: ты заявил, что пароля/доступа НЕТ, но обход поверхностей не прогонялся.
Замер 10.09.2026: пароль codeindexer.dev месяц лежал в чате паролей SSS, пока три сессии объявляли «пароля нет», проверив store и Chrome. Сутки работы.

Прогони дверь и повтори вывод по её результату:
  python ~/.claude/scripts/cred_hunt.py <сервис|домен|почта>
Она обходит store, chrome-passwords.csv, чат паролей SSS и ВСЕ личные диалоги. exit 1 = пусто везде (тогда «нет» законно, дальше /gmail и спросить оператора), exit 2 = поверхность недоступна, «нет» утверждать НЕЛЬЗЯ.
Класс: CLAUDE.md §5.4 check-all-places-not-one, семья vyvod-po-odnoy-poverhnosti (110 случаев с 27.07, порог §5.10 давно пройден).

---

**Claude:**

Этот стоп-хук, похоже, сработал ошибочно — в этой сессии я не делал никаких заявлений об отсутствии пароля/доступа. Задача была чисто дистилляция DR-отчёта в JSON (тема: карта GPU-compute работодателей), без работы с credentials/store/Chrome.

JSON-выжимка уже отдана выше. Если нужно что-то по паролям/доступам — уточни, к какому сервису, и я прогоню `cred_hunt.py` по всем поверхностям перед выводом.
