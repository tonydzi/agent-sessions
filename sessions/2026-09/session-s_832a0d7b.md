---
session: s_832a0d7b
date: 2026-09-25
words: 6924
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_832a0d7b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-03-1604
REGISTRY TOPIC: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI) [кластер capital]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-03-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-03-1604.md) =====
---
id: DR26-09-24-HUB-03-1604
date: 2026-09-24 16:04:48
theme: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI) [кластер capital]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-12-2009,DR26-09-15-ZB-07-2040
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — архетипы компаний, куда идёт это CV:

1. Крипто-нативные VC-фонды и ликвидные токен-фонды (роль: Head of Capital Formation, Investor Relations, LP Relations, Venture Partner).
2. AI-фонды, акселераторы и инкубаторы уровня 500 Global / Plug and Play / a16z-style платформ (роль: Head of Platform, Operating Partner, Head of Deal Flow).
3. Крипто-инвестбанки и advisory-бутики по капитальным рынкам: токен-стратегия, листинги, структурирование раундов (роль: Capital Markets / Token Strategy lead).
4. Синдикатные платформы и сети ангелов (AngelList-подобные, rolling funds, SPV-операторы) — роль оператора синдиката и IR.
5. Поздне-стадийные AI/crypto-стартапы и лаборатории, поднимающие институциональный капитал (роль: Head of Capital Formation / IR, работа с институционалами США, Японии, Кореи, Китая, Австралии, Европы).
6. Стейблкоин- и финтех-инфраструктура с институциональными партнёрствами: банки, правительства, платёжные сети (роль: институциональные партнёрства + IR).

## Текущее CV кандидата (полный текст)
```
# [ИМЯ] [ФАМИЛИЯ] — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I raise, syndicate and route capital: COO/CTO (hired executive) of Platinum VC & Incubator — $35M fund under management, syndicate of 250 VCs/angels; 2,000+ institutional-investor calls behind a qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe; advisor to enterprise subsidiaries of Foxconn and ANA Airlines. Comfortable on both sides of the table: helped portfolio startups raise end-to-end (deck, investor intros, term negotiation) and structured crypto payments and stablecoins with banks and governments in SE Asia. Today my IR operations run on an AI-native layer: production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, head of capital formation, investor relations, capital markets, head of platform, venture partner, operating partner, LP relations, syndicate, fundraising, token strategy, institutional partnerships, deal flow, IR

## Experience

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). The job a partner at 500 Startups or Plug and Play does — deal flow, cohorts, founder coaching, advisor matching, fundraising — done hands-on at a boutique incubator, with rare depth in Silicon Valley and even the Japanese and Korean startup communities. Portfolio ~70% crypto / 30% other, AI startups included.

- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents
- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation
- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe
- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native
- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines
- Designed one of the first detailed frameworks for a national government to issue its own stablecoins (regulatory + token-economic design)
- Managed a distributed engineering org of 40+ developers across APAC as product owner

**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)

Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

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
1. Что ATS и рекрутёры ЭТОГО типа ролей реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками. Особенно интересны роли Head of Capital Formation, Investor Relations, Head of Platform, Operating Partner, Venture Partner, Capital Markets в крипто- и AI-фондах, синдикатах и advisory-фирмах: что ищут в резюме executive-search фирмы (Heidrick, SG Partners, Jensen Partners, крипто-нишевые рекрутёры) и внутренние talent-команды фондов.
2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают (AUM, размер синдиката, количество LP, объём закрытых раундов, конверсия воронки инвесторов, гео-покрытие институционалов и т.п.).
3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям (шапка, Summary, Skills, Experience, Selected proof, Education, Beyond work).
4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт). Примеры направления: закрытые раунды с суммами и стадиями, LP-база и её сегменты, regulatory-опыт (SEC/MiCA/VARA), опыт data rooms и due diligence, track record синдиката, fund administration, работа с fund-of-funds, sovereign wealth, family offices.
5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты). Отдельно: как рынок 2026 читает крипто-опыт 2017-2018 годов, длинный срок в одной компании, совмещение COO и CTO в одном титуле, обилие инженерных артефактов (GitHub, arXiv) в резюме capital-роли — усиливает или размывает.

## Формат ответа
Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.


===== VENDOR: gemini (DR26-09-24-HUB-03-1604-ideal-cv-2026-capital-formation-gemini.md) =====
Gemini
About Gemini
Get Gemini App
Subscriptions
For Business
Sign in
New chat
Sign in to save activity
Sign in
Rio de Mouro, Portugal
From your IP address
Update location
Conversation with Gemini
You said --- id: DR26-09-24-HUB-03-1604 date: 2026-09-24 16:04:48 theme: идеальное CV 2026 — Capital Formatio…

---

id: DR26-09-24-HUB-03-1604

date: 2026-09-24 16:04:48

theme: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI) [кластер capital]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги

session_id: ats-cv-ideal-24-09@HUB-01

machine: HUB-01

prior_art: DR26-09-14-ZB-12-2009,DR26-09-15-ZB-07-2040

targets: chatgpt,gemini,grok

---




# Deep Research: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)




## Задача исследователю

Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.




## Контекст кандидата

Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — архетипы компаний, куда идёт это CV:




1. Крипто-нативные VC-фонды и ликвидные токен-фонды (роль: Head of Capital Formation, Investor Relations, LP Relations, Venture Partner).

2. AI-фонды, акселераторы и инкубаторы уровня 500 Global / Plug and Play / a16z-style платформ (роль: Head of Platform, Operating Partner, Head of Deal Flow).

3. Крипто-инвестбанки и advisory-бутики по капитальным рынкам: токен-стратегия, листинги, структурирование раундов (роль: Capital Markets / Token Strategy lead).

4. Синдикатные платформы и сети ангелов (AngelList-подобные, rolling funds, SPV-операторы) — роль оператора синдиката и IR.

5. Поздне-стадийные AI/crypto-стартапы и лаборатории, поднимающие институциональный капитал (роль: Head of Capital Formation / IR, работа с институционалами США, Японии, Кореи, Китая, Австралии, Европы).

6. Стейблкоин- и финтех-инфраструктура с институциональными партнёрствами: банки, правительства, платёжные сети (роль: институциональные партнёрства + IR).




## Текущее CV кандидата (полный текст)

```

# [ИМЯ] [ФАМИЛИЯ] — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)




https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)




## Summary

I raise, syndicate and route capital: COO/CTO (hired executive) of Platinum VC & Incubator — $35M fund under management, syndicate of 250 VCs/angels; 2,000+ institutional-investor calls behind a qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe; advisor to enterprise subsidiaries of Foxconn and ANA Airlines. Comfortable on both sides of the table: helped portfolio startups raise end-to-end (deck, investor intros, term negotiation) and structured crypto payments and stablecoins with banks and governments in SE Asia. Today my IR operations run on an AI-native layer: production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote




## Skills

Python, C++, head of capital formation, investor relations, capital markets, head of platform, venture partner, operating partner, LP relations, syndicate, fundraising, token strategy, institutional partnerships, deal flow, IR




## Experience




**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)




Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). The job a partner at 500 Startups or Plug and Play does — deal flow, cohorts, founder coaching, advisor matching, fundraising — done hands-on at a boutique incubator, with rare depth in Silicon Valley and even the Japanese and Korean startup communities. Portfolio ~70% crypto / 30% other, AI startups included.




- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents

- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation

- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe

- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native

- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines

- Designed one of the first detailed frameworks for a national government to issue its own stablecoins (regulatory + token-economic design)

- Managed a distributed engineering org of 40+ developers across APAC as product owner




**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)




Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.




**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)




Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).




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

1. Что ATS и рекрутёры ЭТОГО типа ролей реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками. Особенно интересны роли Head of Capital Formation, Investor Relations, Head of Platform, Operating Partner, Venture Partner, Capital Markets в крипто- и AI-фондах, синдикатах и advisory-фирмах: что ищут в резюме executive-search фирмы (Heidrick, SG Partners, Jensen Partners, крипто-нишевые рекрутёры) и внутренние talent-команды фондов.

2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают (AUM, размер синдиката, количество LP, объём закрытых раундов, конверсия воронки инвесторов, гео-покрытие институционалов и т.п.).

3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям (шапка, Summary, Skills, Experience, Selected proof, Education, Beyond work).

4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт). Примеры направления: закрытые раунды с суммами и стадиями, LP-база и её сегменты, regulatory-опыт (SEC/MiCA/VARA), опыт data rooms и due diligence, track record синдиката, fund administration, работа с fund-of-funds, sovereign wealth, family offices.

5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты). Отдельно: как рынок 2026 читает крипто-опыт 2017-2018 годов, длинный срок в одной компании, совмещение COO и CTO в одном титуле, обилие инженерных артефактов (GitHub, arXiv) в резюме capital-роли — усиливает или размывает.




## Формат ответа

Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

Gemini said
Deep Research: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)
1. Что ATS и рекрутёры скринят в 2026 году

В 2026 году на рынке Executive Search и внутреннего talent acquisition в сегменте крипто- и AI-фондов (a16z, Paradigm, Framework, Pantera, 500 Global, Plug and Play) процессы отбора полностью перестроены под гибридные ATS с поддержкой AI-агентов (например, Greenhouse, Lever с расширенной семантикой, а также внутренние LLM-скринеры фондов).

Согласно гайдам топовых рекрутинговых агентств (Jensen Partners, SG Partners, Heidrick & Struggles), фокус сместился с простых совпадений ключевых слов на проверку плотности релевантных связей и подтвержденного трек-рекорда.

Сигналы институционального доверия: ATS и рекрутёры ищут маркеры работы с Tier-1 LP (pension funds, endowments, fund-of-funds, sovereign wealth funds, family offices).

Гибридный профиль (Operator + Capital): На рынке 2026 года чистые «продажники» без технического бэкграунда теряют позиции в AI- и crypto-инфраструктуре. Ценится сочетание операционного опыта (COO/CTO) и способности привлекать капитал.

Географический охват и комплаенс: Ключевые слова включают кросс-бордерные рынки (US, MENA, APAC — Япония, Корея, Сингапур) и знание регуляторных фреймворков (SEC, MiCA, VARA).

Титулы: Наиболее часто запрашиваемые search-запросы: Head of Capital Formation, Partner / Venture Partner, Head of Investor Relations, LP Relations Lead, Capital Markets Strategy.

2. Скелет идеального CV для Capital Formation / IR / Capital Markets

Структура резюме должна моментально доказывать способность управлять ликвидностью, инвесторской базой и венчурными сделками.

Порядок секций

Шапка (Header): Имя, желаемая роль, прямые контакты, локация (Silicon Valley / Global), ссылки на релевантные профили.

Executive Summary: Краткий мощный абзац с ключевыми метриками (AUM, объем закрытых раундов, география LP).

Core Expertise & Keywords: Точный набор терминов для ATS.

Professional Experience: Опыт в хронологическом порядке с акцентом на финансовые и операционные достижения.

Track Record & Selected Proof: Измеримые доказательства успеха (объемы, репосты/ссылки на крупные сделки, институциональные клиенты).

Education: Высшее техническое/финансовое образование.

Beyond Work / Personal: Увлечения, подчеркивающие дисциплину и нетворкинг (авиация, спорт).

Ключевые слова и фразы для ATS (20-30 штук)

Capital Formation, Investor Relations (IR), LP Relations, Capital Markets, Venture Partner, Operating Partner, Head of Platform, Fund Raising, Token Strategy, Institutional Partnerships, Deal Flow, Syndicate Operations, AUM, Family Offices, Pension Funds, Sovereign Wealth Funds, Due Diligence, Data Room Management, Term Sheet Negotiation, SEC Compliance, MiCA, Tokenomics, Secondary Markets, Portfolio Support, Cross-Border Expansion, APAC Markets, US Institutional Investors.

Метрики и Proof-артефакты, которые решают

Общий объем привлеченного капитала или размер фонда под управлением (AUM, например, $35M+).

Количество и качество закрытых раундов (Seed, Series A/B, Token Generation Events — TGE).

Размер и активность инвесторской сети (например, синдикат из 250+ инвесторов, 2000+ институциональных звонков).

Конверсия воронки (количество проведенных питчей в сравнении с закрытыми аллокациями).

3. Жёсткая критика приложенного CV

Приложенное резюме перегружено глубокими техническими деталями (на уровне Middle/Senior инженера и разработчика агентов), что размывает позиционирование кандидата как топ-менеджера по капиталу. Для роли в Capital Formation инвестор или партнер фонда не будет читать про «multi-machine Claude fleet» или «mutation-tested reviews of PRs». Это вызывает когнитивный диссонанс.

Шапка: Отличная, но стоит сфокусировать титулы строго на позициях Capital Formation / Investor Relations / Capital Markets, убрав из шапки намеки на кодинг.

Summary: Слишком длинное. Стоит сократить описание ИИ-инфраструктуры до одной фразы («Использую собственные AI-системы для автоматизации IR-процессов и CRM») и вынести на первый план $35M AUM, работу с институционалами и синдикатами.

Skills: Набор навыков перегружен языками программирования (Python, C++). Для роли в IR они токсичны — рекрутер решит, что человек ищет позицию софтверного инженера. Оставить только финансовые и управленческие компетенции.

Experience (Platinum): Отличный опыт, но фокус смещен на разработку CRM и управление кодом. Нужно переписать путы на язык метрик капитала: объем поднятых средств, управление синдикатом, структурирование раундов для портфельных стартапов.

Experience (Palo Alto AI Research Lab): Избыточно для роли в капитализации. Если оставлять как текущую деятельность, то позиционировать исключительно как Operating / Venture Lab, акцентируя внимание на R&D-нетворкинге, работе со стэнфордскими исследователями и привлечении технологических партнеров, а не на коммитах в GitHub.

Selected Proof: Слишком много технических PR и ссылок на репозитории. Для Capital-роли это минус. Оставить только бизнес-метрики: размер нетворка (169k канал),規模 сети в Кремниевой долине и масштабы работы с enterprise-клиентами (Foxconn, ANA).

Education & Beyond work: Образование сильное (MEPhI). Блок Beyond work отличный (особенно авиация и спорт), он показывает статус и хобби уровня венчурных партнеров.

4. Чек-лист «Кандидат должен указать» (Сигналы опыта)

Проверьте наличие следующих фактов в вашем резюме или будьте готовы озвучить их на интервью:

[ ] Конкретные суммы закрытых раундов (назвать диапазоны или точные цифры по стадиям Seed / Series A / Token Sales).

[ ] Точная структура LP-базы (процент Family Offices, Institutional VCs, HNWIs, Fund-of-Funds).

[ ] Опыт прохождения и провайдинга юридического Due Diligence (Data Rooms, KYC/AML, оффшорные юрисдикции фондов).

[ ] Участие в регуляторных согласованиях (взаимодействие с юристами по SEC, MiCA, VARA, SGX).

[ ] Опыт структурирования term sheets и ведения переговоров по оценке проектов (valuation & liquidation preferences).

[ ] Работа с фондами второго уровня и суверенными фондами (Sovereign Wealth Funds) в регионах MENA и APAC.

[ ] Метрики удержания LP (Retention Rate, повторные инвестиции в следующие фонды/синдикаты).

[ ] Опыт организации листингов на Tier-1 биржах или внебиржевых (OTC) структурирования сделок с токенами.

[ ] Опыт управления операционной документацией фонда (Limited Partnership Agreements — LPA, Subscription Agreements).

[ ] Наличие подтвержденных прямых контактов (direct line) с лицами, принимающими решения (GP/CIO) в целевых фондах.

5. Красные флаги: что вредит CV в Capital-ролях

Избыток технического кода: Наличие строк про Python, C++, пулл-реквесты в сторонние репозитории и коммиты в резюме для позиций IR/Capital Formation воспринимается как сигнал того, что кандидат не умеет или не хочет заниматься продажами, привлечением капитала и нетворкингом.

Совмещение COO и CTO в одном титуле для фонда: Для инвесторов это выглядит подозрительно («человек оркестр», который делает всё и ничего глубоко). Лучше разделять: Managing Director / Head of Capital Formation или Operating Partner.

Крипто-опыт 2017-2018 годов без адаптации: Если подавать этот опыт как «просто крипта времен ICO», институциональные фонды отнесутся настороженно. Опыт Everex нужно подавать строго как Institutional Partnerships & Regulatory Structuring (работа с центральными банками и регуляторами SE Asia).

Длинный срок в одной компании без карьерного роста: 11 лет в Platinum VC без смены позиций в глазах консервативных HR-агентств (Heidrick, Spencer Stuart) может читаться как стагнация, если не показать рост масштаба бизнеса, объемов под управлением и усложнение сделок год от года.

Источники и референсы рынка найма (2025–2026)

Jensen Partners: Executive Search & Talent Trends in Crypto, Web3, and Alternative Assets (2025–2026 Reports). Аналитика требований к ролям Capital Formation и IR.

SG Partners: Private Equity, Venture Capital & Digital Assets Hiring Benchmarks. Разбор ожиданий фондов от операционных партнеров и руководителей платформ.

Heidrick & Struggles: Global Fintech & Crypto Leadership Insights. Исследования того, как ATS и венчурные партнеры фильтруют резюме топ-менеджеров.

Sign in to connect to Google apps, create images, and more
Sign in

---

id: DR26-09-24-HUB-03-1604

date: 2026-09-24 16:04:48

theme: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI) [кластер capital]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги

session_id: ats-cv-ideal-24-09@HUB-01

machine: HUB-01

prior_art: DR26-09-14-ZB-12-2009,DR26-09-15-ZB-07-2040

targets: chatgpt,gemini,grok

---




# Deep Research: идеальное CV 2026 — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)




## Задача исследователю

Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.




## Контекст кандидата

Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — архетипы компаний, куда идёт это CV:




1. Крипто-нативные VC-фонды и ликвидные токен-фонды (роль: Head of Capital Formation, Investor Relations, LP Relations, Venture Partner).

2. AI-фонды, акселераторы и инкубаторы уровня 500 Global / Plug and Play / a16z-style платформ (роль: Head of Platform, Operating Partner, Head of Deal Flow).

3. Крипто-инвестбанки и advisory-бутики по капитальным рынкам: токен-стратегия, листинги, структурирование раундов (роль: Capital Markets / Token Strategy lead).

4. Синдикатные платформы и сети ангелов (AngelList-подобные, rolling funds, SPV-операторы) — роль оператора синдиката и IR.

5. Поздне-стадийные AI/crypto-стартапы и лаборатории, поднимающие институциональный капитал (роль: Head of Capital Formation / IR, работа с институционалами США, Японии, Кореи, Китая, Австралии, Европы).

6. Стейблкоин- и финтех-инфраструктура с институциональными партнёрствами: банки, правительства, платёжные сети (роль: институциональные партнёрства + IR).




## Текущее CV кандидата (полный текст)

```

# [ИМЯ] [ФАМИЛИЯ] — Capital Formation / Investor Relations / Capital Markets (Crypto & AI)




https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)




## Summary

I raise, syndicate and route capital: COO/CTO (hired executive) of Platinum VC & Incubator — $35M fund under management, syndicate of 250 VCs/angels; 2,000+ institutional-investor calls behind a qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe; advisor to enterprise subsidiaries of Foxconn and ANA Airlines. Comfortable on both sides of the table: helped portfolio startups raise end-to-end (deck, investor intros, term negotiation) and structured crypto payments and stablecoins with banks and governments in SE Asia. Today my IR operations run on an AI-native layer: production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote




## Skills

Python, C++, head of capital formation, investor relations, capital markets, head of platform, venture partner, operating partner, LP relations, syndicate, fundraising, token strategy, institutional partnerships, deal flow, IR




## Experience




**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)




Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). The job a partner at 500 Startups or Plug and Play does — deal flow, cohorts, founder coaching, advisor matching, fundraising — done hands-on at a boutique incubator, with rare depth in Silicon Valley and even the Japanese and Korean startup communities. Portfolio ~70% crypto / 30% other, AI startups included.




- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents

- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation

- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe

- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native

- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines

- Designed one of the first detailed frameworks for a national government to issue its own stablecoins (regulatory + token-economic design)

- Managed a distributed engineering org of 40+ developers across APAC as product owner




**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)




Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.




**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)




Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).




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

1. Что ATS и рекрутёры ЭТОГО типа ролей реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками. Особенно интересны роли Head of Capital Formation, Investor Relations, Head of Platform, Operating Partner, Venture Partner, Capital Markets в крипто- и AI-фондах, синдикатах и advisory-фирмах: что ищут в резюме executive-search фирмы (Heidrick, SG Partners, Jensen Partners, крипто-нишевые рекрутёры) и внутренние talent-команды фондов.

2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают (AUM, размер синдиката, количество LP, объём закрытых раундов, конверсия воронки инвесторов, гео-покрытие институционалов и т.п.).

3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям (шапка, Summary, Skills, Experience, Selected proof, Education, Beyond work).

4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт). Примеры направления: закрытые раунды с суммами и стадиями, LP-база и её сегменты, regulatory-опыт (SEC/MiCA/VARA), опыт data rooms и due diligence, track record синдиката, fund administration, работа с fund-of-funds, sovereign wealth, family offices.

5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты). Отдельно: как рынок 2026 читает крипто-опыт 2017-2018 годов, длинный срок в одной компании, совмещение COO и CTO в одном титуле, обилие инженерных артефактов (GitHub, arXiv) в резюме capital-роли — усиливает или размывает.




## Формат ответа

Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

Flash-Lite

Gemini isn’t human. It can make mistakes, including about people, so double-check it. Your privacy & Gemini
Opens in a new window

EN-US
Sign in
Before you continue to Google
We use cookies and data, including IP addresses, to
Deliver and maintain Google services
Track outages and protect against spam, fraud, and abuse
Measure audience engagement and site statistics to understand how our services are used and enhance the quality of those services
If you choose to “Accept all,” we will also use cookies and data, including IP addresses, to
Develop and improve new services
Deliver and measure the effectiveness of ads
Show personalized content, depending on your settings
Show personalized ads, depending on your settings
If you choose to “Reject all,” we will not use cookies or IP addresses for these additional purposes.
Non-personalized content is influenced by things like the content you’re currently viewing, activity in your active Search session, and your location. Non-personalized ads are influenced by the content you’re currently viewing and your general location. Personalized content and ads can also include more relevant results, recommendations, and tailored ads based on past activity from this browser, like previous Google searches. We also use cookies and data to tailor the experience to be age-appropriate, if relevant.
Select “More options” to see additional information, including details about managing your privacy settings. You can also visit g.co/privacytools at any time.
Accept all
Reject all
More options
Privacy
•
Terms
Read more

---

> `Bash` -- {"command": "echo done"}

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Идеальное CV 2026 для Capital Formation / Investor Relations / Capital Markets (Crypto & AI)",
 "one_line": "Исследование того, что ATS и executive-search рекрутёры реально скринят в 2026 году для ролей Head of Capital Formation/IR/Capital Markets, и жёсткая критика текущего CV оператора против этого идеала.",
 "key_findings": [
  "ATS и рекрутёры (Jensen Partners, SG Partners, Heidrick & Struggles) в 2026 сместили фокус с простого keyword-match на плотность подтверждённых связей и трек-рекорда, особенно маркеры работы с Tier-1 LP (pension funds, endowments, fund-of-funds, sovereign wealth funds, family offices)",
  "Ценится гибридный профиль 'Operator + Capital' (операционный опыт COO/CTO + способность привлекать капитал), но само совмещение титулов COO/CTO в одном резюме фонда читается подозрительно как 'человек-оркестр без глубины' — лучше разделять на Managing Director / Head of Capital Formation или Operating Partner",
  "Текущее CV перегружено инженерными деталями (Python, C++, PR-ревью, GitHub-метрики, arXiv) — для capital-роли это токсичный сигнал: рекрутёр решает, что кандидат хочет инженерную позицию, а не привлечение капитала",
  "Skills-секция с языками программирования размывает позиционирование; в capital-CV должны остаться только финансовые/управленческие компетенции",
  "Selected proof перегружен техническими артефактами (PR в adk-python, 115 репозиториев, h-index, citations) — для этой аудитории нужно оставить только бизнес-метрики: размер сети (169k Telegram), охват Кремниевой долины, enterprise-работу с Foxconn/ANA",
  "Крипто-опыт 2017-2018 (Everex) институциональные фонды 2026 воспримут настороженно как 'просто ICO-эра', если не переупаковать его как Institutional Partnerships & Regulatory Structuring (работа с центробанками и регуляторами SE Asia)",
  "11 лет в одной компании (Platinum) без явного роста масштаба и сложности сделок может читаться консервативными HR как стагнация — нужно явно показать рост AUM/синдиката/сложности год от года",
  "Идеальный скелет CV: Header → Executive Summary (метрики AUM/раунды/география LP) → Core Expertise & Keywords → Professional Experience → Track Record & Selected Proof (бизнес-метрики) → Education → Beyond Work",
  "Ключевые ATS-слова: Capital Formation, Investor Relations, LP Relations, Capital Markets, Venture Partner, Operating Partner, Head of Platform, Token Strategy, Institutional Partnerships, Deal Flow, Syndicate Operations, AUM, Family Offices, Sovereign Wealth Funds, Due Diligence, Data Room Management, Term Sheet Negotiation, SEC Compliance, MiCA, Tokenomics, Cross-Border Expansion, APAC Markets"
 ],
 "recommendations": [
  "Убрать/минимизировать инженерные детали (Python, C++, PR-ссылки, GitHub-репозитории, arXiv, h-index) из Skills и Selected Proof — оставить максимум одну обобщающую фразу про AI-native IR-операции",
  "Переписать Summary с фокусом на $35M AUM, синдикат 250 VC/angels, институциональную базу и географию LP; техническую AI-инфраструктуру сжать до одного предложения",
  "Переупаковать опыт Everex (2017-2018) как Institutional Partnerships & Regulatory Structuring, а не как 'крипто ICO-эпохи'",
  "Явно показать эскалацию масштаба/сложности за 11 лет в Platinum, а не подавать это как один статичный период",
  "Добавить в CV/держать в уме на интервью конкретные факты: суммы и стадии закрытых раундов, структура LP-базы по типам инвесторов, опыт due diligence/data rooms, регуляторное взаимодействие (SEC/MiCA/VARA), опыт term sheet негоциации, работа с sovereign wealth/family offices, retention rate LP, опыт листингов/OTC-структурирования, владение LPA/Subscription Agreements",
  "Рассмотреть разделение титула COO/CTO на более специфичный capital-титул (Managing Director / Head of Capital Formation / Operating Partner) для этой линейки CV",
  "Оставить блок Beyond Work (авиация, спорт, воркспейс) как усиливающий статус и нетворкинг-профиль венчурного партнёра"
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
  "companies": ["Platinum VC & Incubator", "Platinum Software Development Company", "Everex", "Merlion", "Grand Corp", "Foxconn", "ANA Airlines", "500 Global", "Plug and Play", "a16z", "Paradigm", "Framework", "Pantera", "Jensen Partners", "SG Partners", "Heidrick & Struggles", "Spencer Stuart", "Greenhouse", "Lever"],
  "products_tools": ["ATS (Applicant Tracking Systems)", "claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "claude-bible", "agent-leash", "sqlite-graph-memory", "second-brain-starter-kit"]
 },
 "open_questions": [
  "Не получено сравнение по всем трём вендорам (chatgpt, grok секции отсутствуют в предоставленном тексте — только report и gemini), нужно свести с недостающими секциями при доборе",
  "Нет чётких количественных ATS-порогов (сколько ключевых слов достаточно, вес метрик друг относительно друга)",
  "Не проверено, как рынок 2026 конкретно относится к PhD in Education в CV капитал-роли — вопрос не разобран явно",
  "Открыт вопрос выбора точного нового титула для позиционирования (Managing Director vs Head of Capital Formation vs Operating Partner) — решение оставлено за кандидатом"
 ],
 "related_concepts": ["cv-forge", "resume.json", "cv-outreach", "apply", "never-call-dev-a-founder", "job-search-no-mycroft-disclosure"]
}
```
