---
session: s_70cf6c88
date: 2026-09-25
words: 2296
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_70cf6c88` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-06-1604
REGISTRY TOPIC: идеальное CV 2026 — Developer Relations / Developer Advocate [кластер devrel]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-06-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-06-1604.md) =====
---
id: DR26-09-24-HUB-06-1604
date: 2026-09-24 16:04:48
theme: идеальное CV 2026 — Developer Relations / Developer Advocate [кластер devrel]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-10-2009,DR26-09-14-ZB-23-2206
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — Developer Relations / Developer Advocate

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров и hiring-менеджеров DevRel-ниши, hiring-гайды компаний, разборы ATS, гайды DevRel-лидеров вроде DevRel Foundation / Developer Relations Collective / DevRelX, треды на LinkedIn и X, разборы вакансий Developer Advocate / DevRel Engineer) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации вида «стоит указать X, если такой опыт есть» — законны и желательны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — 6 архетипов компаний, нанимающих DevRel в 2026:

1. Frontier-лаборатории и LLM-платформы с публичным API (класс Anthropic, OpenAI, Google DeepMind / Gemini API, Mistral) — DevRel вокруг API, агентных SDK и коммьюнити разработчиков агентов.
2. AI-инфраструктура и agent-tooling стартапы (класс LangChain, LlamaIndex, Modal, Weights & Biases, векторные БД, observability для агентов) — advocacy = adoption фреймворка, примеры кода, интеграции.
3. Классические API-first платформы — школа DevRel (класс Stripe, Twilio, Vercel, Cloudflare) — контент, доки, DX, developer education в масштабе.
4. Облачные гиганты с developer-экосистемой (AWS, Google Cloud, Microsoft) — программы champions/GDE/MVP, конференции, региональные комьюнити.
5. Commercial open-source компании (класс Supabase, Temporal, Grafana, HashiCorp-типа) — рост GitHub-комьюнити, контрибьюторы, open-source funnel в продажи.
6. Web3/крипто-платформы и L1/L2 foundations с developer-грантами и хакатонами — учитывая крипто-бэкграунд кандидата (Solidity-курсы, хакатоны, экосистемные когорты).

## Текущее CV кандидата (полный текст)
```markdown
# [ИМЯ] [ФАМИЛИЯ] — Developer Relations / Developer Advocate

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I did developer activation for a frontier platform before — when smart contracts were where LLM agents are now: Solidity curricula, hackathons, cohorts, scaled a distributed engineering org to 40+ developers across APAC. Today I build with Claude in public daily (115 public repos; flagships: claw-consensus, verbatim-citation-gate, claude-bible, agent-leash, agent-control-plane-casebook, sqlite-graph-memory, second-brain-starter-kit) and write the operating manual as I go (相棒 AIBŌ · The Partner). PhD, 50+ published items, 137 citations, h-index 7 (verified 2026-09-01); 2 preprints on multi-agent stability (arXiv in progress). US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, developer relations, developer advocate, community, ecosystem, content, technical evangelism, open source, agents, hackathons, curriculum

## Experience

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). The job a partner at 500 Startups or Plug and Play does — deal flow, cohorts, founder coaching, advisor matching, fundraising — done hands-on at a boutique incubator, with rare depth in Silicon Valley and even the Japanese and Korean startup communities. Portfolio ~70% crypto / 30% other, AI startups included.

- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines
- community organizer since 2019: Moscow Cryptoeconomics Research Group meetups → Silicon Valley crypto meetups (Crypto Mondays)
- Designed one of the first detailed frameworks for a national government to issue its own stablecoins (regulatory + token-economic design)

**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)

Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.

**Sales Director, compute hardware (Southeast Europe) / CRM-ERP Development Director (Microsoft Navision, Salesforce) — Merlion** (2006 – 2015)

One of the largest private IT distributors in Eastern Europe. Enterprise and B2B sales of computing hardware across Southeast Europe, and the ERP and CRM systems the sales floor ran on (Microsoft Navision and Salesforce, 5 years), where I learned that deal flow runs on CRM quality.

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
1. Что ATS и рекрутёры ЭТОГО типа ролей (Developer Relations / Developer Advocate / DevRel Engineer) реально скринят в 2026: сигналы, ключевые слова, титулы. Что весит больше — публичный след (GitHub, talks, YouTube, блог, community-метрики) или классический стаж? Как ATS-парсеры обрабатывают ссылки на GitHub/портфолио? С источниками.
2. Скелет идеального CV для этой роли: порядок секций, идеальный титул (Developer Advocate vs DevRel Engineer vs Head of Developer Relations — что скринится лучше на senior/staff уровне), ТОЧНЫЙ список из 20-30 ключевых слов/фраз (например: developer experience, DX, SDK adoption, technical content, conference talks, community growth, docs, sample apps, OSS maintainership, developer education, AI agents, LLM APIs), какие метрики решают (рост комьюнити, adoption, звёзды, просмотры, NPS разработчиков) и какие proof-артефакты обязаны быть прямо в CV (ссылки на talks, репо, посты, цифры аудитории).
3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям (шапка, Summary, Skills, каждый блок Experience, Selected proof, Education, Beyond work). Отдельно оцени: не хоронит ли инкубаторско-executive блок (COO/CTO, продажи) DevRel-сигнал; правильно ли поданы 115 репо и 169k Telegram; где должны стоять talks/выступления, которых в CV сейчас не видно.
4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в DevRel-CV 2026 ждут (кандидат сам вспомнит, есть ли у него такой факт). Примеры класса: выступления на конференциях/митапах с названиями и датами, воркшопы и вебинары, написанные доки/quickstarts, сниппеты и sample apps, видео-туториалы, program management (champions-программы, амбассадоры), метрики контента, опыт feedback-loop «разработчики → продукт», участие в стандартах/спеках, стримы, подкасты, hackathon judging.
5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты). Например: «evangelism» vs «advocacy» в 2026, executive-титулы без hands-on кода, крипто-акценты при подаче в AI-компании, отсутствие ссылок на публичные выступления, маркетинговый тон вместо инженерного, перегруз нерелевантным стажем 2004-2015.

## Формат ответа
Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Идеальное CV 2026 для Developer Relations/Developer Advocate — критика CV кандидата",
 "one_line": "DR-запрос исследует, что ATS и рекрутёры реально скринят в DevRel/Developer Advocate вакансиях в 2026 и просит построчную критику приложенного CV кандидата против этого идеала.",
 "key_findings": [
  "На момент выгрузки в реестре был статус 'issued', но по факту на диске лежит только 1/3 запрошенных ног (из трёх целевых LLM-рельс chatgpt/gemini/grok) — реальные ответы вендоров на 5 вопросов в этом теле отсутствуют, приведён только текст запроса.",
  "Задание нацелено на 6 архетипов работодателей DevRel в 2026: frontier LLM-платформы (Anthropic/OpenAI/DeepMind/Mistral), AI-инфраструктура/agent-tooling стартапы (LangChain/LlamaIndex/Modal/W&B), классические API-first платформы (Stripe/Twilio/Vercel/Cloudflare), облачные гиганты (AWS/GCP/Microsoft), commercial open-source компании (Supabase/Temporal/Grafana/HashiCorp-класс), Web3/крипто-платформы с грантами и хакатонами.",
  "CV кандидата смешивает executive-блок (COO/CTO инкубатора Platinum с 2015, продажи compute hardware 2006-2015, chief engineer в крипто-компании Everex 2017-2018) с DevRel-сигналами последних лет (115 публичных репо, Telegram-канал 169k подписчиков, community 500+ AI-практиков в Palo Alto, open-source артефакты claw-consensus/verbatim-citation-gate/claude-bible/agent-leash/agent-control-plane-casebook/sqlite-graph-memory/second-brain-starter-kit).",
  "Явно запрещено в выводах называть кандидата 'founder/фаундер' или 'не-кодером' — позиционирование зафиксировано как наёмный руководитель (COO/CTO), программист на Python и C++.",
  "В CV отсутствуют явные ссылки на публичные выступления (conference talks/митапы) — это прямо вынесено исследователю как отдельная проверка (вопрос 3): 'где должны стоять talks/выступления, которых в CV сейчас не видно'.",
  "Proof-блок CV содержит измеримые аргументы: слияние находок в 14 сторонних проектах (MCP Go SDK, inspect_ai, qwen-code, google-gemini/cookbook, fastmcp, agno, pydantic/logfire) + 52 issues с репродукциями с 07.2026; 50+ публикаций, 137 цитирований, h-index 7; eval 0/17 Tier-2 действий проскользнувших мимо approval gate.",
  "Пять вопросов задания покрывают: (1) что реально скринят ATS/рекрутёры и вес публичного следа vs классического стажа, (2) скелет идеального CV/титул/20-30 ключевых слов/метрики/proof-артефакты, (3) построчная критика приложенного CV, (4) чек-лист из 10-20 сигналов опыта DevRel, (5) красные флаги (evangelism vs advocacy, executive-титулы без hands-on кода, крипто-акценты при подаче в AI-компании и др.)."
 ],
 "recommendations": [
  "Добрать недостающие 2/3 ног ответа (chatgpt/gemini/grok) прежде чем строить финальную версию CV или запускать критику по чеклисту — сейчас основания для рекомендаций нет, только сам запрос.",
  "Перед следующей правкой CV явно собрать данные по вопросу 3 (позиция executive-блока и продаж 2006-2015 относительно DevRel-сигнала) и вопросу 5 (красные флаги: evangelism vs advocacy, крипто-акценты) — это прямые точки риска, названные в самом задании.",
  "Явно зафиксировать в CV/сопроводительных материалах отсутствие публичных выступлений либо, если такие факты существуют у кандидата, добавить их со ссылками — задание прямо отмечает этот пробел как проверяемый."
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
  "companies": ["Anthropic", "OpenAI", "Google DeepMind", "Mistral", "LangChain", "LlamaIndex", "Modal", "Weights & Biases", "Stripe", "Twilio", "Vercel", "Cloudflare", "AWS", "Google Cloud", "Microsoft", "Supabase", "Temporal", "Grafana", "HashiCorp", "Platinum Software Development Company / Platinum VC & Incubator", "Everex", "Merlion", "Foxconn", "ANA Airlines", "Grand Corp", "Bloomberg"],
  "products_tools": ["claw-consensus", "verbatim-citation-gate", "claude-bible", "agent-leash", "agent-control-plane-casebook", "sqlite-graph-memory", "second-brain-starter-kit", "MCP Go SDK", "inspect_ai", "qwen-code", "google-gemini/cookbook", "fastmcp", "agno", "pydantic/logfire"]
 },
 "open_questions": [
  "Что реально скринят ATS/рекрутёры в DevRel/Developer Advocate ролях в 2026 (сигналы, ключевые слова, титулы; вес публичного следа vs стажа) — ответ вендоров отсутствует в этом теле.",
  "Скелет идеального CV: порядок секций, идеальный титул (Developer Advocate vs DevRel Engineer vs Head of Developer Relations), список ключевых слов, решающие метрики, обязательные proof-артефакты — не отвечено.",
  "Построчная критика приложенного CV по секциям (шапка, Summary, Skills, Experience, Selected proof, Education, Beyond work) — не отвечено.",
  "Чек-лист из 10-20 конкретных сигналов опыта DevRel, которые кандидат должен вспомнить и проверить у себя — не отвечено.",
  "Красные флаги, вредящие CV в этой роли (evangelism/advocacy, executive-титулы, крипто-акценты, маркетинговый тон, нерелевантный стаж 2004-2015) — не отвечено.",
  "Почему в реестре стоял статус 'issued' при фактическом наличии только 1/3 ног — причина расхождения не разобрана (dr_reconcile лишь исправил статус по факту)."
 ],
 "related_concepts": ["ideal-cv-2026", "devrel-ats-screening", "developer-advocate-titles", "cv-critique-dev", "deep-research-protocol", "job-search-devrel"]
}
```
