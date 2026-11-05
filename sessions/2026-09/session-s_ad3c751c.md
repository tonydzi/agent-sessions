---
session: s_ad3c751c
date: 2026-09-25
words: 2092
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ad3c751c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-20-1604
REGISTRY TOPIC: идеальное CV 2026 — AI Deployment Strategist [кластер strategist]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-20-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-20-1604.md) =====
---
id: DR26-09-24-HUB-20-1604
date: 2026-09-24 16:04:50
theme: идеальное CV 2026 — AI Deployment Strategist [кластер strategist]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-16-2205
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — AI Deployment Strategist

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — архетипы компаний, нанимающих на роли класса «AI Deployment Strategist / Enterprise AI Adoption Lead / Forward-Deployed AI Lead»:

1. Frontier-лаборатории и их прикладные/GTM-команды (Anthropic Applied AI, OpenAI Forward Deployed / Solutions, Google DeepMind applied) — роли «помоги enterprise-клиенту реально внедрить модель/агентов».
2. Forward-deployed вендоры enterprise-платформ (Palantir-стиль: FDE/Deployment Strategist как отдельная профессия; Scale AI, Sierra, Glean и подобные) — внедрение агентных систем у заказчика на месте.
3. AI-агент стартапы Series A-C, продающие в enterprise (агентные платформы, copilot-вендоры, MCP/tooling-компании) — первый deployment-стратег или head of AI adoption.
4. Консалтинг и системные интеграторы с AI-трансформационной практикой (McKinsey QuantumBlack, BCG X, Accenture, Deloitte AI) — лидер внедрения GenAI/агентов у клиентов.
5. In-house AI-трансформация крупных компаний (Fortune 500 «AI adoption office», Head of AI Enablement, Director of AI Transformation) — выбор кейсов, governance, change management, human-in-the-loop.
6. Enterprise-инфраструктура и cloud-провайдеры с AI-подразделениями (AWS/Azure/GCP AI specialist teams, NVIDIA enterprise AI) — customer-facing стратег по внедрению.

## Текущее CV кандидата (полный текст)

```markdown
# [ИМЯ] [ФАМИЛИЯ] — AI Deployment Strategist

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I decide *what* to deploy, *where agents actually pay off*, and *how to prove it* — then run the deployment myself. Daily driver: a production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines — with published evals and failure modes. An operator-engineer, hands-on in Python, who translates a real business (fund, incubator, CRM-driven outreach) into working agent systems end-to-end, and can sit in front of a customer or a regulator: 15+ years running BD and delivery in high-stakes environments, incl. structuring crypto payments and stablecoins with banks and governments in SE Asia — adversarial, compliance-heavy environments. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, AI deployment strategist, enterprise AI adoption, agents, deployment strategy, MCP, RAG, evals, human-in-the-loop, governance, change management, customer-facing, Claude

## Experience

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

- Deployment surface run daily: MCP connectors, RAG over a 10-year knowledge base, CRM automation, cross-machine message bus, human-approval gates for risky actions
- Deployment strategy artifacts published as I go: what to automate first, where humans must stay in the loop, how to measure adoption vs. theater

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). The job a partner at 500 Startups or Plug and Play does — deal flow, cohorts, founder coaching, advisor matching, fundraising — done hands-on at a boutique incubator, with rare depth in Silicon Valley and even the Japanese and Korean startup communities. Portfolio ~70% crypto / 30% other, AI startups included.

- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents
- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native
- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines
- Managed a distributed engineering org of 40+ developers across APAC as product owner

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
1. Что ATS и рекрутёры ЭТОГО типа ролей реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками.
2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают.
3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям.
4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт).
5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты).

## Формат ответа
Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Идеальное CV 2026 для роли AI Deployment Strategist / Forward-Deployed AI Lead",
 "one_line": "Задание трём внешним LLM (chatgpt, gemini, grok) — оценить текущее CV оператора против того, что реально скринят ATS и рекрутёры в 2026 для ролей класса AI Deployment Strategist / Enterprise AI Adoption Lead, и дать скелет, критику, чек-лист сигналов и красные флаги.",
 "key_findings": [
  "Целевые работодатели определены как 6 архетипов: frontier-лаборатории (Anthropic Applied AI, OpenAI Forward Deployed, DeepMind applied), forward-deployed enterprise-вендоры (Palantir-стиль, Scale AI, Sierra, Glean), AI-агент стартапы Series A-C, консалтинг/системные интеграторы (McKinsey QuantumBlack, BCG X, Accenture, Deloitte AI), in-house AI-трансформация Fortune 500, cloud/AI-инфраструктура (AWS/Azure/GCP, NVIDIA).",
  "Жёсткое ограничение на позиционирование: кандидату запрещено называть себя 'founder/фаундер' — только 'наёмный руководитель (COO/CTO)'; запрещено называть 'не-кодером' — указывается программист Python/C++.",
  "Текущее CV построено вокруг двух параллельных ролей: 'Operating Lead — Palo Alto AI Research Lab' (2023–наст.время, публичный multi-machine Claude fleet на 6 машинах, 500+ community) и 'COO/CTO — Platinum Software Development Company/Incubator' (2015–наст.время, APAC-инкубатор, портфель ~70% крипто/30% прочее).",
  "Proof-секция CV опирается на измеримые артефакты: 115 публичных репо, вклады в 14 сторонних инженерных проектов + 52 issue-репорта с воспроизведением, 50+ публикаций/137 цитирований/h-index 7, eval 0/17 Tier-2-действий проскочивших approval-gate, аудитория 169k Telegram-подписчиков.",
  "Прежний опыт кандидата включает Chief Engineer Lending & Risk Management в Everex (Сингапур, 2017–2018, смарт-контракты и работа с банками/госорганами SE Asia по крипто-платежам/стейблкоинам) и 9 лет в Merlion (продажи hardware + разработка ERP/CRM на Navision/Salesforce).",
  "DR ссылается на предыдущий deep-research по той же теме (prior_art: DR26-09-14-ZB-16-2205), то есть это уже вторая итерация исследования по CV-позиционированию.",
  "Сам текст отчёта содержит только постановку задачи для трёх LLM (5 вопросов: скрин ATS/рекрутёров, скелет идеального CV с 20-30 ключевыми словами, построчная критика текущего CV, чек-лист сигналов опыта, красные флаги) и полный текст CV-кандидата — фактические ответы/выводы vendors в предоставленном тексте отсутствуют."
 ],
 "recommendations": [
  "Дождаться/затребовать фактические ответы chatgpt/gemini/grok на 5 вопросов — в текущем виде нога DR содержит только промпт и CV, а не результаты исследования.",
  "При следующей правке CV жёстко соблюдать запрет на 'founder' и 'не-кодер' — эти формулировки закреплены как обязательные для всех будущих версий CV и позиционирования."
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
  "companies": ["Anthropic", "OpenAI", "Google DeepMind", "Palantir", "Scale AI", "Sierra", "Glean", "McKinsey QuantumBlack", "BCG X", "Accenture", "Deloitte AI", "AWS", "Azure", "GCP", "NVIDIA", "Everex", "Merlion", "Platinum Software Development Company", "Platinum VC & Incubator", "Foxconn", "ANA Airlines", "Grand Corp", "Palo Alto AI Research Lab"],
  "products_tools": ["Claude", "MCP", "RAG", "claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "sqlite-graph-memory", "second-brain-starter-kit", "claude-bible", "agent-leash", "headroom", "google/adk-python", "Salesforce", "Microsoft Navision"]
 },
 "open_questions": [
  "Каковы фактические ответы chatgpt/gemini/grok на 5 вопросов (скрин ATS 2026, скелет CV, построчная критика, чек-лист сигналов, красные флаги) — в тексте ноги отсутствуют, только постановка задачи.",
  "dr_reconcile 2026-09-25 отметил расхождение реестра: на диске найдена только 1/3 ожидаемых 'ног' исследования при статусе 'issued' — не ясно, довезены ли остальные 2/3 ответов вендоров и где они лежат."
 ],
 "related_concepts": ["AI Deployment Strategist positioning", "ATS keyword screening 2026", "resume-cv-pipeline", "cv-forge", "prior_art DR26-09-14-ZB-16-2205"]
}
```
