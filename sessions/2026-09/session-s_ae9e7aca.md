---
session: s_ae9e7aca
date: 2026-09-25
words: 2322
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ae9e7aca` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-04-1604
REGISTRY TOPIC: идеальное CV 2026 — AI Compute / GPU Infrastructure — Enterprise Sales & BD [кластер compute]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 2/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-04-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-04-1604.md) =====
---
id: DR26-09-24-HUB-04-1604
date: 2026-09-24 16:04:48
theme: идеальное CV 2026 — AI Compute / GPU Infrastructure — Enterprise Sales & BD [кластер compute]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: none
targets: chatgpt,gemini,grok,glm,mistral
---

# Deep Research: идеальное CV 2026 — AI Compute / GPU Infrastructure — Enterprise Sales & BD

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — 6 архетипов компаний, где живут роли Enterprise Sales / BD / Account Executive по AI-компьюту и GPU-инфраструктуре:

1. **GPU-облака / neoclouds** — CoreWeave, Lambda, Crusoe, Nebius, Together AI, Voltage Park: продают GPU-capacity (обучение и инференс) AI-лабораториям и энтерпрайзу, роли AE / Enterprise Sales / Capacity Sales.
2. **Чип-вендоры и их энтерпрайз-каналы** — NVIDIA, AMD, Intel (партнёрские и прямые enterprise-продажи ускорителей, DGX/HGX-систем, сетевого стека).
3. **Гиперскейлеры, AI-инфраструктурные линии** — AWS (EC2 UltraClusters, Trainium), Google Cloud (TPU/GPU), Azure (ND-серии), Oracle OCI: роли AI Infrastructure Sales Specialist / GTM Specialist.
4. **OEM/ODM-серверостроители и дистрибуция** — Supermicro, Dell (AI Factory), HPE, Lenovo, плюс VAR/дистрибьюторы: классическая hardware-продажа стоек, кластеров и сопутствующего железа энтерпрайзу.
5. **Дата-центры и colocation под AI-нагрузку** — Equinix, Digital Realty, Vantage, Switch, новые AI-DC-девелоперы: продажа мощности (МВт), colocation и interconnect под GPU-кластеры.
6. **Инференс-платформы и compute-маркетплейсы** — Fireworks, Baseten, Modal, RunPod, Vast.ai, SF Compute: продажа инференс-мощности и брокеринг GPU-капасити, роли BD / Enterprise GTM.

## Текущее CV кандидата (полный текст)

```markdown
# [ИМЯ] [ФАМИЛИЯ] — AI Compute / GPU Infrastructure — Enterprise Sales & BD

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I sold compute hardware before I started buying it: 2006-2015 at one of Eastern Europe's largest IT distributors, moving chips, memory, GPUs and CPUs to B2B and enterprise buyers, ~$5M/month personally inside a department running $15M to $25M/month, with Southeast Europe as my territory. Today I sit on the other side of that same trade: I run a production multi-machine Claude fleet in public and consume compute every day, local GPU inference plus multi-vendor LLM spend, so I can talk to a buyer about capacity, procurement and cluster economics and still read the workload they intend to run on it. Eleven years as a hired operating executive (COO/CTO) in between, carrying revenue and delivery. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, enterprise sales, account executive, AI compute, GPU cloud, hardware sales, semiconductors, data center, infrastructure sales, capacity, technical account manager, solutions architect, distribution, channel, Southeast Europe, EMEA

## Experience

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

- Run a production multi-machine Claude fleet (6 machines) in public: consensus, persistent memory, CRM automation, 100+ autonomous routines, published evals and documented failure modes
- Day-to-day consumer of compute: local GPU inference for embeddings, reranking and transcription, plus multi-vendor LLM API spend routed across subscriptions by cost

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) at a startup incubator + software house in APAC since 2015 (11 years). Ran the commercial motion end to end: deal flow, enterprise advisory for subsidiaries of Foxconn and ANA Airlines, fundraising, and a distributed engineering org of 40+ developers across APAC as product owner.

- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents
- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation
- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines
- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched customer and investor base across the US, Japan, Korea, China, Australia and Europe
- Managed a distributed engineering org of 40+ developers across APAC as product owner

**Sales Director, compute hardware (Southeast Europe) / CRM-ERP Development Director (Microsoft Navision, Salesforce) — Merlion** (2006 – 2015)

One of the largest private IT distributors in Eastern Europe. Sold compute hardware to B2B and enterprise buyers: semiconductors and chips, memory, GPUs, CPUs and the rest of the computing stack, with Southeast Europe as my sales territory. In parallel built the ERP and CRM systems the sales floor ran on (Microsoft Navision and Salesforce, 5 years), where I learned that deal flow runs on CRM quality.

- Carried Southeast Europe as sales territory for compute hardware: chips and semiconductors, memory, GPUs, CPUs and adjacent computing equipment, sold B2B and enterprise to customers procuring compute capacity and hardware infrastructure
- Personal turnover ~$5M per month; the department I sold in ran $15M to $25M per month
- Sold on a deliberately competitive floor: departments competed against each other for the same enterprise accounts
- Then built the ERP and CRM that floor ran on (Microsoft Navision, Salesforce, 5 years), roots of the CRM I later wrote from scratch at Platinum

**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)

Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.

**CRM Developer Intern — CRM/ERP consulting (Salesforce ecosystem)** (2004 – 2006)

First professional years: CRM systems development in the Salesforce/ERP ecosystem.

## Selected proof
- Evidence-first OSS reliability work in the AI-agent ecosystem: mutation-tested reviews of other people's PRs and bug reports carrying a deterministic repro plus a regression test shown failing on the unfixed code. google/adk-python#6957 — author adopted all three review findings in 6h («genuinely one of the most useful reviews I've gotten on this PR»); #6887 fixed upstream from our report; credited in headroom v2.0.8 release notes. Scope since 07.2026 (verified 2026-09-04): merged into 14 third-party engineering projects (MCP Go SDK, UK AISI inspect_ai, QwenLM/qwen-code, google-gemini/cookbook, fastmcp, agno, pydantic/logfire) + 52 issues with reproductions
- 115 public repos; flagships: claw-consensus, verbatim-citation-gate, claude-bible, agent-leash, agent-control-plane-casebook, sqlite-graph-memory, second-brain-starter-kit
- 50+ published items, 137 citations, h-index 7 (verified 2026-09-01); 2 preprints on multi-agent stability (arXiv in progress)
- Measured agent-fleet reliability evals published (07.2026): 0/17 Tier-2 (high-risk) actions slipped past the human approval gate in recorded runs; failure modes documented in public (FAILURE-MODES.md)
- Audience & network: 169k-subscriber Telegram channel (@PaloAltoAi) + 500+ AI-practitioner community in Palo Alto, the heart of Silicon Valley; Silicon Valley network built on the ground plus a decade of Japan/Korea startup-community depth; enterprise advisory for Foxconn and ANA Airlines subsidiaries

## Education

- PhD in Education (Information Technologies), Paris College of International Education
- MSc, Computer and Information Systems Security, National Research Nuclear University MEPhI
- BSc, Computer and Information Sciences, National Research Nuclear University MEPhI

## Beyond work

- **Aviation**: Licenced helicopter pilot, ~200 flight hours; Student pilot on fixed-wing, working toward the licence; Long-term goal: a small plane for the family, and a round-the-world flight in it
- **Endurance and mountain biking**: Half-marathons; Mountain biking (downhill, jumps) on an analogue bike by choice: a workout should stay a workout; Surfing, windsurfing, kitesurfing, tennis
- **Sharp tools, clean workspace**: Perfectionist about the instrument: kitchen knives, keyboard, mouse, spotless glass; A 5-machine, 9-monitor workspace I administer myself, so work runs in parallel instead of context-switching inside one box; Ten years of orchestrating many tasks at once; voice-first input over typing
- **Cooking for the family**: Cook dinner for the household on weekends
```

## Пять вопросов
1. Что ATS и рекрутёры ЭТОГО типа ролей (Enterprise Sales / AE / BD в AI compute, GPU cloud, дата-центрах, чип-вендорах) реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками.
2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают (quota attainment, ARR, размер сделок, циклы, named accounts, знание GPU-стека и экономики кластеров).
3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям.
4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт). Примеры направления: % выполнения квоты по годам, крупнейшая закрытая сделка, знакомство с процессом procurement GPU-капасити, опыт переговоров о take-or-pay / committed-use контрактах, знание NVIDIA-стека (DGX, InfiniBand, NVLink), опыт продажи через каналы/дистрибуцию, CRM-дисциплина (Salesforce), вертикали покупателей.
5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты).

## Формат ответа
Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Идеальное CV 2026 для Enterprise Sales/BD в AI Compute и GPU-инфраструктуре",
 "one_line": "ДР должен был ответить на 5 вопросов о скрининге ATS/рекрутёров, скелете идеального CV, критике текущего CV оператора, чек-листе сигналов опыта и красных флагах для ролей Enterprise Sales/AE/BD в AI compute, GPU cloud, чип-вендорах, гиперскейлерах, OEM/дистрибуции, дата-центрах и инференс-платформах — но в переданном тексте присутствует только ТЗ-промпт и текущее CV кандидата, синтезированных ответов вендоров (chatgpt/gemini/grok/glm/mistral) в этой секции нет.",
 "key_findings": [
  "Реестр DR26-09-24-HUB-04-1604 при сверке 2026-09-25 показал только 2 из 5 ног собранными на диске, при этом статус в реестре ошибочно стоял 'issued' — выправлен по факту; полный синтез по 5 вопросам недоступен из переданного текста",
  "Задача нацелена на 6 архетипов работодателей: GPU-облака/neoclouds (CoreWeave, Lambda, Crusoe, Nebius, Together AI, Voltage Park), чип-вендоры (NVIDIA, AMD, Intel), гиперскейлеры (AWS, Google Cloud, Azure, Oracle OCI), OEM/ODM и дистрибуция (Supermicro, Dell AI Factory, HPE, Lenovo), дата-центры/colocation (Equinix, Digital Realty, Vantage, Switch) и инференс-маркетплейсы (Fireworks, Baseten, Modal, RunPod, Vast.ai, SF Compute)",
  "Жёсткое ограничение ТЗ: в выводах запрещено называть кандидата 'founder/фаундер' или 'не-кодером' — позиционирование только как наёмный COO/CTO и программист Python/C++",
  "Текущее CV кандидата уже содержит компьют-специфичный бэкграунд: 2006-2015 продажа compute-hardware (чипы, память, GPU, CPU) B2B/enterprise в Юго-Восточной Европе, личный оборот ~$5M/мес при обороте отдела $15-25M/мес, плюс 11 лет COO/CTO и текущая роль оператора публичного multi-machine Claude-флота как 'потребителя compute' (локальный GPU-инференс, мульти-вендорный LLM-spend)",
  "Ни ответы на 5 вопросов (сигналы ATS/рекрутёров, скелет идеального CV с 20-30 ключевыми словами, построчная критика приложенного CV, чек-лист 10-20 сигналов опыта, список красных флагов), ни источники в переданном фрагменте не приведены — секция начинается и заканчивается заданием исследователю"
 ],
 "recommendations": [
  "Добрать недостающие 3 из 5 ног ДР из results-директории (D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-24-HUB-04-1604\\results) до финальной дистилляции, иначе заметка фиксирует только постановку задачи, а не выводы",
  "При повторном прогоне явно включать в тело заметки синтезированные ответы вендоров по всем 5 вопросам, а не только session-файл с промптом",
  "Держать в позиционировании CV жёсткие рамки ТЗ (COO/CTO, не founder; программист, не 'не-кодер') при любой последующей правке резюме под эту нишу"
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]"],
  "companies": ["CoreWeave", "Lambda", "Crusoe", "Nebius", "Together AI", "Voltage Park", "NVIDIA", "AMD", "Intel", "AWS", "Google Cloud", "Azure", "Oracle OCI", "Supermicro", "Dell", "HPE", "Lenovo", "Equinix", "Digital Realty", "Vantage", "Switch", "Fireworks", "Baseten", "Modal", "RunPod", "Vast.ai", "SF Compute", "Merlion", "Everex", "Platinum Software Development Company"],
  "products_tools": ["ATS", "Salesforce", "Microsoft Navision", "DGX", "HGX", "InfiniBand", "NVLink", "Trainium", "TPU"]
 },
 "open_questions": [
  "Что ATS и рекрутёры этих ролей реально скринят в 2026 (сигналы, ключевые слова, титулы) — не отвечено в переданном тексте",
  "Каков скелет идеального CV: порядок секций, титул, точный список 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают (quota attainment, ARR, размер сделок, циклы, named accounts) — не отвечено",
  "Построчная критика приложенного CV против идеала: что убрать, что переставить, чего не хватает — не отвечено",
  "Чек-лист 10-20 конкретных сигналов опыта, которые ожидаются в таких CV — не отвечено",
  "Какие красные флаги (слова, форматы, акценты) вредят CV для этой роли — не отвечено",
  "Где физически лежат ответы 2 собранных ног и почему 3 ноги отсутствуют на диске при статусе 'issued'"
 ],
 "related_concepts": ["ats-cv-ideal-24-09", "cv-forge", "enterprise-sales-ai-compute", "dr-quorum-and-latecomer-sweep"]
}
```
