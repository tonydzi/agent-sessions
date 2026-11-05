---
session: s_30dd8e87
date: 2026-09-25
words: 2071
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_30dd8e87` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-11-1604
REGISTRY TOPIC: идеальное CV 2026 — Fund Platform / Portfolio Operations / Venture Partner (Crypto & AI Funds) [кластер fund]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 2/4 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-11-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-11-1604.md) =====
---
id: DR26-09-24-HUB-11-1604
date: 2026-09-24 16:04:49
theme: идеальное CV 2026 — Fund Platform / Portfolio Operations / Venture Partner (Crypto & AI Funds) [кластер fund]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-15-ZB-07-2040
targets: chatgpt,gemini,grok,glm
---

# Deep Research: идеальное CV 2026 — Fund Platform / Portfolio Operations / Venture Partner (Crypto & AI Funds)

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели: (1) крипто-нативные венчурные фонды и их platform/value-creation команды (типа Paradigm, a16z crypto, Pantera, Dragonfly); (2) хедж-фонды и liquid-фонды цифровых активов, где нужен middle office / fund operations с технической экспертизой; (3) AI-focused венчурные фонды, строящие portfolio-support и platform-функцию; (4) акселераторы, инкубаторы и venture-студии, нанимающие head of platform / head of ventures / operating partner; (5) фонд-администраторы и fund-ops платформы для крипто- и венчурных фондов (fund finance, treasury, отчётность LP); (6) family offices и fund-of-funds с аллокацией в crypto/AI, которым нужен технический due-diligence партнёр.

## Текущее CV кандидата (полный текст)
```
# [ИМЯ] [ФАМИЛИЯ] — Fund Platform / Portfolio Operations / Venture Partner (Crypto & AI Funds)

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I am the operator side of a fund, not the fundraising side: eleven years as a hired operating executive (COO/CTO) at an APAC incubator and software house that ran a $35M fund — portfolio companies coached, staffed and shipped, scaled a distributed engineering org to 40+ developers across APAC, an in-house CRM worked daily by up to 30 operators. Technical diligence is mine to do, not to outsource: PhD plus MSc in systems security, and a portfolio that was ~70% crypto infrastructure — exchanges, market-maker engines, HFT, DeFi. Today I run the same operating discipline AI-native: production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines, with published evals and failure modes. I run a finished product cycle: found the problem, built it, people use it. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, fund operations, portfolio operations, head of platform, value creation, venture partner, technical partner, operating partner, head of ventures, fund finance and operations, middle office, treasury, technical due diligence, crypto fund, digital assets, portfolio support, GP, LP

## Experience

**COO / CTO (hired executive), $35M fund platform — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) at a startup incubator, software house and $35M fund in APAC, 2015-2026 (11 years), reporting to Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). Ran the platform side of the portfolio: sourcing, diligence, cohorts, hiring for portfolio companies, engineering delivery and the CRM the whole firm worked in. Portfolio ~70% crypto infrastructure / 30% other, AI startups included.

- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation
- Portfolio support hands-on: coached founders through product and fundraising, recruited engineers into portfolio companies, matched advisors, ran cohorts end-to-end — the work a fund calls value creation
- Managed a distributed engineering org of 40+ developers across APAC as product owner
- Shipped crypto-exchange infrastructure: cryptocurrency backends, market-maker engines, high-frequency trading systems; partnerships with hedge funds, market makers, brokers
- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe
- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

- Operating controls written down and executed by machines: 100+ automation routines across six nodes, nightly unattended runs, human approval gates only on irreversible actions — the same discipline a fund needs in its middle office
- Every live part carries a usage counter; parts unused for 30 days are killed — operations measured, not assumed

**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)

Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.

**Sales Director, compute hardware (Southeast Europe) / CRM-ERP Development Director (Microsoft Navision, Salesforce) — Merlion** (2006 – 2015)

One of the largest private IT distributors in Eastern Europe. Enterprise and B2B sales of computing hardware across Southeast Europe, and the ERP and CRM systems the sales floor ran on (Microsoft Navision and Salesforce, 5 years), where I learned that deal flow runs on CRM quality.

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
  "topic": "Идеальное CV 2026 для Fund Platform / Portfolio Operations / Venture Partner (Crypto & AI Funds)",
  "one_line": "Ресёрч-запрос (промпт для ChatGPT/Gemini/Grok/GLM) на то, что ATS и рекрутёры 2026 реально скринят для ролей fund platform/portfolio operations/venture partner в крипто- и AI-фондах, и как под это перестроить CV оператора.",
  "key_findings": [
    "Файл содержит только сам DR-промпт (задача, контекст кандидата, полный текст CV, 5 вопросов, формат ответа) — фактических ответов вендоров (ChatGPT/Gemini/Grok/GLM) в теле нет, несмотря на targets: chatgpt,gemini,grok,glm",
    "Целевые работодатели явно очерчены: (1) крипто-нативные VC и их platform-команды (Paradigm, a16z crypto, Pantera, Dragonfly), (2) хедж-фонды/liquid-фонды цифровых активов, (3) AI-фонды с portfolio-support функцией, (4) акселераторы/инкубаторы/venture-студии (head of platform/ventures), (5) фонд-администраторы/fund-ops платформы, (6) family offices и fund-of-funds",
    "Жёсткое ограничение на позиционирование кандидата: запрещено называть его 'founder/фаундер' или 'не-кодером' — везде наёмный руководитель (COO/CTO), программист Python и C++",
    "Текущее CV уже несёт целевой заголовок 'Fund Platform / Portfolio Operations / Venture Partner (Crypto & AI Funds)' и построено вокруг 11 лет COO/CTO при $35M фонде (APAC), портфель ~70% crypto-инфраструктуры, 40+ разработчиков, CRM на 30 операторов",
    "В CV заявлены количественные proof-точки: $35M under management, синдикат 250 VC/ангелов, 10,000+ founder calls и 2,000+ institutional-investor calls, 100+ automation routines на 6-машинном Claude-флоте, 0/17 Tier-2 действий проскочило approval gate, 115 публичных репо, 50+ публикаций/137 цитирований/h-index 7",
    "Prior art для этого исследования — DR26-09-15-ZB-07-2040 (предыдущий заход по той же теме CV/кластер fund)"
  ],
  "recommendations": [
    "Дождаться/найти фактические файлы ответов вендоров в results-папке ноги (D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-24-HUB-11-1604\\results) — в этой заметке зафиксирован только запрос, не выводы; dr_reconcile уже отметил расхождение 2/4 ног при статусе 'issued'",
    "При появлении ответов свести их в единый чек-лист по 5 вопросам (сигналы ATS/ключевые слова, скелет идеального CV, построчная критика текущего CV, чек-лист сигналов опыта, красные флаги) и применить через скилл /cv",
    "Проверить остальные 2 ноги DR (недостающие вендоры из targets) — кворум для этой темы не закрыт"
  ],
  "entities": {
    "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
    "companies": ["Paradigm", "a16z crypto", "Pantera", "Dragonfly", "Platinum Software Development Company / Platinum VC & Incubator", "Palo Alto AI Research Lab", "Everex", "Merlion", "Grand Corp", "Bloomberg", "Foxconn", "ANA Airlines"],
    "products_tools": ["ATS", "Salesforce", "Microsoft Navision", "claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "claude-bible", "agent-leash", "sqlite-graph-memory", "second-brain-starter-kit", "google/adk-python", "headroom"]
  },
  "open_questions": [
    "Фактические ответы ChatGPT/Gemini/Grok/GLM на 5 вопросов (сигналы ATS, скелет CV, критика, чек-лист, красные флаги) — отсутствуют в этом файле, нужно проверить results-папку",
    "Какие 2 из 4 ног реально долетели и что именно они ответили (dr_reconcile зафиксировал расхождение с реестром)",
    "Соответствует ли текущий текст CV (приведённый в промпте) финальной версии после этого DR, или CV уже правился по итогам"
  ],
  "related_concepts": ["cv-forge", "ats-screening-2026", "alpha-protocol-recall-plus-dr", "never-call-dev-a-founder", "job-search-no-mycroft-disclosure"]
}
```
