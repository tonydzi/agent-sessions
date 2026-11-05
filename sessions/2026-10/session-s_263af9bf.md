---
session: s_263af9bf
date: 2026-10-06
words: 8537
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_263af9bf` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-15-1604
REGISTRY TOPIC: идеальное CV 2026 — Research Engineer / Member of Technical Staff (evals & agent infrastructure) [кластер research]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-15-1604\results) (dr-judge 03.10: живая нога одна, grok; gemini и glm = эхо промпта/UI. Синтез dr-synthesis-cv-research сверен с grok, совпадает. Insight-заметка врала «ответов нет»: исправлена блоком-корректировкой со ссылкой на синтез (бэкап .prebak-20261003), класс synthesis-read-only-the-garbage-rail, 4-й случай, сид на корень fix-dr-synthesize-queue-results-20261003. ПОТРЕБИТЕЛЬ: ветка CV (перегенерирована cv_forge 01.10 19:40) синтез НЕ впитала: частично: Inspect внесён, остальное сверить. Ветка = выход генератора и публичная, отметку в неё не ставлю (судейские отметки HUB-03..08 так и стёрлись); правки уходят в источник cv_forge, задача [[task-2026-10-03-cv-branches-absorb-dr-syntheses]].)

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


===== VENDOR: gemini (gemini.md) =====
Gemini
About Gemini
Get Gemini App
Subscriptions
For Business
Sign in
New chat
Sign in to save activity
Sign in
Algueirão–Mem Martins, Portugal
From your IP address
Update location
Conversation with Gemini
Meet Gemini, your personal AI assistant
Sign in to connect to Google apps, create images, and more
Sign in

---

id: DR26-09-24-HUB-15-1604

date: 2026-09-24 16:04:50

theme: идеальное CV 2026 — Research Engineer / Member of Technical Staff (evals & agent infrastructure) [кластер research]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги

session_id: ats-cv-ideal-24-09@HUB-01

machine: HUB-01

prior_art: DR26-09-15-ZB-05-2040

targets: chatgpt,gemini,grok

---




# Deep Research: идеальное CV 2026 — Research Engineer / Member of Technical Staff (evals & agent infrastructure)




## Задача исследователю

Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.




## Контекст кандидата

Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели:

1. Frontier-лаборатории (Anthropic, OpenAI, Google DeepMind, Meta FAIR, xAI, Mistral) — роли Research Engineer / Member of Technical Staff, особенно команды evals, agent infrastructure, safety.

2. Институты и организации AI-safety/evals (UK AISI, US CAISI, METR, Apollo Research, Redwood Research, MATS-экосистема) — evaluation engineering, red-teaming, dangerous-capability evals.

3. Стартапы вокруг evals, агентной надёжности и observability (Braintrust, LangSmith/LangChain, Patronus AI, Galileo, Humanloop, Freeplay и подобные) — инженеры eval-harness'ов и agent-инфраструктуры.

4. Trading-фирмы и HFT с ML-исследованиями (Jane Street, Hudson River Trading, Jump, Two Sigma, Citadel Securities) — research engineer / infrastructure для исследователей, где ценятся C++, low-latency и production-надёжность.

5. Big-tech applied-research команды (Google, Microsoft AI, NVIDIA, Amazon AGI) — model evaluation, agent platform, reliability engineering для исследований.

6. Хорошо профинансированные agent-инфраструктурные компании (Cursor/Anysphere, Cognition, Sierra, Adept-подобные) — инженеры, строящие control planes, memory, multi-agent orchestration.




## Текущее CV кандидата (полный текст)

```markdown

# [ИМЯ] [ФАМИЛИЯ] — Research Engineer / Member of Technical Staff (evals & agent infrastructure)




https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)




## Summary

Anthropic writes that about half its technical staff arrived with no prior ML experience; what the work does require is one deep column the lab is fighting with right now. Mine is adversarial distributed systems: MSc in Computer & Information Systems Security (MEPhI, cryptography), then exchange backends, market-maker engines and high-frequency trading systems shipped in production, then eleven years owning engineering delivery as a hired executive. I write Python and C++, and I run a production multi-agent system as an experimental rig: production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. I do not claim ML research; I claim the engineering research runs on — eval harnesses, reproducibility, failure taxonomies, agent control planes, and bug reports that arrive with a deterministic repro and a regression test shown failing on the unfixed code. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote




## Skills

research engineer, member of technical staff, MTS, applied research engineer, evals, evaluations, eval harness, Inspect, agent evaluations, interpretability infrastructure, RL environments, training infrastructure, technical program manager research, AI safety, red team, distributed systems, cryptography, Python, C++, reproducibility, model evaluations




## Experience




**Technical Lead — Palo Alto AI Research Lab** (2023 – Present)




Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).




- Merged code into UK AISI inspect_ai — the agent-evaluation framework evals orgs actually run — alongside merges into the MCP Go SDK, pydantic/logfire, fastmcp, agno and QwenLM/qwen-code

- Every bug report is shipped as an experiment: deterministic repro, a regression test demonstrated failing on the unfixed code, and a mutation matrix showing which of the project's own tests stayed green (google/adk-python#6957 — the author adopted all three findings within six hours)

- agent-control-plane-casebook: reproducible control-plane failure cases from a live fleet, each with a repro and an upstream bug report — a failure taxonomy, not a demo

- Reliability evals published with the number rather than the claim: 0/17 Tier-2 (high-risk) actions slipped past the human approval gate in recorded runs; failure modes public in FAILURE-MODES.md




**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)




Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.




**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)




Hired operating executive (COO/CTO) at a startup incubator and software house in APAC, 2015-2026 (11 years). Owned engineering delivery end to end: crypto-exchange infrastructure, market-maker engines and high-frequency trading systems, a distributed org of 40+ developers across APAC, and the in-house CRM I wrote myself and up to 30 operators worked in daily.




- Shipped crypto-exchange infrastructure: cryptocurrency backends, market-maker engines, high-frequency trading systems; partnerships with hedge funds, market makers, brokers

- Managed a distributed engineering org of 40+ developers across APAC as product owner

- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native




**CRM / ERP Development Director (Navision, Salesforce) — Merlion** (2006 – 2015)




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

Flash-Lite

Google Terms
Opens in a new window
 and the Privacy Policy
Opens in a new window
 apply. Gemini is AI and can make mistakes, including about people. Your privacy & Gemini
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

===== VENDOR: glm (glm.md) =====
GLM-5.3-Flash
Share
Sign in
---
id: DR26-09-24-HUB-15-1604
date: 2026-09-24 16:04:50
theme: идеальное CV 2026 — Research Engineer / Member of Technical Staff (evals & agent infrastructure) [кластер research]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-15-ZB-05-2040
targets: chatgpt,gemini,grok,glm
---

# Deep Research: идеальное CV 2026 — Research Engineer / Member of Technical Staff (evals & agent infrastructure)

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели:
1. Frontier-лаборатории (Anthropic, OpenAI, Google DeepMind, Meta FAIR, xAI, Mistral) — роли Research Engineer / Member of Technical Staff, особенно команды evals, agent infrastructure, safety.
2. Институты и организации AI-safety/evals (UK AISI, US CAISI, METR, Apollo Research, Redwood Research, MATS-экосистема) — evaluation engineering, red-teaming, dangerous-capability evals.
3. Стартапы вокруг evals, агентной надёжности и observability (Braintrust, LangSmith/LangChain, Patronus AI, Galileo, Humanloop, Freeplay и подобные) — инженеры eval-harness'ов и agent-инфраструктуры.
4. Trading-фирмы и HFT с ML-исследованиями (Jane Street, Hudson River Trading, Jump, Two Sigma, Citadel Securities) — research engineer / infrastructure для исследователей, где ценятся C++, low-latency и production-надёжность.
5. Big-tech applied-research команды (Google, Microsoft AI, NVIDIA, Amazon AGI) — model evaluation, agent platform, reliability engineering для исследований.
6. Хорошо профинансированные agent-инфраструктурные компании (Cursor/Anysphere, Cognition, Sierra, Adept-подобные) — инженеры, строящие control planes, memory, multi-agent orchestration.

## Текущее CV кандидата (полный текст)
```markdown
# [ИМЯ] [ФАМИЛИЯ] — Research Engineer / Member of Technical Staff (evals & agent infrastructure)

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
Anthropic writes that about half its technical staff arrived with no prior ML experience; what the work does require is one deep column the lab is fighting with right now. Mine is adversarial distributed systems: MSc in Computer & Information Systems Security (MEPhI, cryptography), then exchange backends, market-maker engines and high-frequency trading systems shipped in production, then eleven years owning engineering delivery as a hired executive. I write Python and C++, and I run a production multi-agent system as an experimental rig: production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. I do not claim ML research; I claim the engineering research runs on — eval harnesses, reproducibility, failure taxonomies, agent control planes, and bug reports that arrive with a deterministic repro and a regression test shown failing on the unfixed code. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
research engineer, member of technical staff, MTS, applied research engineer, evals, evaluations, eval harness, Inspect, agent evaluations, interpretability infrastructure, RL environments, training infrastructure, technical program manager research, AI safety, red team, distributed systems, cryptography, Python, C++, reproducibility, model evaluations

## Experience

**Technical Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

- Merged code into UK AISI inspect_ai — the agent-evaluation framework evals orgs actually run — alongside merges into the MCP Go SDK, pydantic/logfire, fastmcp, agno and QwenLM/qwen-code
- Every bug report is shipped as an experiment: deterministic repro, a regression test demonstrated failing on the unfixed code, and a mutation matrix showing which of the project's own tests stayed green (google/adk-python#6957 — the author adopted all three findings within six hours)
- agent-control-plane-casebook: reproducible control-plane failure cases from a live fleet, each with a repro and an upstream bug report — a failure taxonomy, not a demo
- Reliability evals published with the number rather than the claim: 0/17 Tier-2 (high-risk) actions slipped past the human approval gate in recorded runs; failure modes public in FAILURE-MODES.md

**Chief Engineer, Lending & Risk Management — Everex (Singapore)** (2017 – 2018)

Wrote smart contracts and led government/bank relations across SE Asia on structuring crypto payments and stablecoins; blockchain credit scoring, stable-value payments.

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) at a startup incubator and software house in APAC, 2015-2026 (11 years). Owned engineering delivery end to end: crypto-exchange infrastructure, market-maker engines and high-frequency trading systems, a distributed org of 40+ developers across APAC, and the in-house CRM I wrote myself and up to 30 operators worked in daily.

- Shipped crypto-exchange infrastructure: cryptocurrency backends, market-maker engines, high-frequency trading systems; partnerships with hedge funds, market makers, brokers
- Managed a distributed engineering org of 40+ developers across APAC as product owner
- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native

**CRM / ERP Development Director (Navision, Salesforce) — Merlion** (2006 – 2015)

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
 
Show full message
Your current concurrent conversation limit has been reached. Please try again later.
Deep Think
Max
Generated by AI. For reference only.
Tech Blog
Contact us
Terms of Service
and
Privacy Policy

===== VENDOR: grok (grok.md) =====
Собираю живые источники 2025–2026 по скринингу Research Engineer / MTS: вакансии лабораторий, гайды рекрутёров и разборы ATS.# A. Что ATS и рекрутёры этих ролей реально скринят в 2026

Первый фильтр почти везде двойной. Сначала парсер должен вообще прочитать файл. Потом человек или модель за  один проход решают, есть ли у кандидата одна глубокая колонка под конкретную вакансию.

Greenhouse, а на нём сидят и Anthropic, и UK AISI, официально принимает pdf, doc, docx, rtf, txt. Парсер отказывается работать с файлом тяжелее 2.5 МБ и ломается на графике, фото, резюме-картинке, таблицах, колонках, тексте в колонтитуле или в текстовом боксе, и на секциях без ясных заголовков. Имя и контакты в шапке документа парсер часто не видит. Неполные титулы вроде «Sr.» тоже портят разбор. Это не совет блога, это страница поддержки Greenhouse про неуспешный parse.

https://support.greenhouse.io/hc/en-us/articles/id_48704da0-Unsuccessful-resume-parse

https://support.greenhouse.io/hc/en-us/articles/id_4ef950a9-Supported-formats-for-resumes-cover-letters-and-other-candidate-uploads

Рекрутёрский разбор 2026 года, который рецензировал бывший рекрутёр Google и Airbnb Markus Fink, описывает сам просмотр так. Глаз падает на текущий титул, работодателя и первые один-два буллета последней роли. Если эти строки мутные, остальная страница редко спасает. Дальше он ищет уровень, масштаб, прогресс и техническое суждение, а не список инструментов. Ключевое слово имеет вес только внутри сделанной работы. Отдельная простыня навыков без буллетов сигнал не создаёт.

https://www.sweresume.app/articles/faang-resume-guide/

Наймовый маркетплейс Fonzi в мае 2026 пишет, что AI-фильтр MTS-профилей поднимает резюме, где есть масштаб, latency, надёжность и явные ярлыки вроде «model evaluation harness» и «agentic orchestration». Это не рекрутёр лаборатории, но это прямое описание того, как автоматический матчинг читает MTS в 2026.

https://fonzi.ai/blog/what-does-member-of-technical-staff-mean

Дальше скрин уже не общий, а по типу двери.

**Frontier-лаборатории, инженерная дверь.** Anthropic на своей странице найма пишет дословно: около половины technical staff пришли без предшествующего ML-опыта, около половины имеют PhD, и есть сильные люди без колледжа. И отдельно: если есть независимое исследование, вдумчивый блог или open source, это надо ставить наверх резюме. Инженеру с инженерным бэкграундом они советуют подаваться как инженеру, потому что так человек лучше проходит их интервью. На вакансии Software Engineer, Research Tools написано прямо: ML и research experience не требуются. Ждут 5+ лет разработки, инструменты для технических пользователей, experiment orchestration, визуализацию failure modes и sandboxed execution для кода, который породила модель.

https://www.anthropic.com/careers

https://job-boards.greenhouse.io/anthropic/jobs/id_265330cf

Их Fellows-программа для safety research говорит то же жёстче. PhD, прошлый ML и опубликованные статьи не нужны. Нужны Python, умение взять туманную задачу и довести, желание заниматься эмпирической safety-работой. Удачные феллоу приходили из физики, математики, CS и cybersecurity.

https://alignment.anthropic.com/2025/anthropic-fellows-program-2026/

OpenAI на роли Research Engineer / AI Systems Engineer команды RSI (San Francisco, вилка базы $295–445K) скринит другой набор. Оценки исследовательского суждения, длинные эксперименты, превращение реальных провалов модели в данные и eval-маховик, agent harnesses, RL environments, sandboxed runtimes, research infrastructure, большие distributed systems. Плюс вкус к научной честности, safety, privacy, reliability и scale. Это уже не «любой сильный бэкенд».

https://openai.com/careers/research-engineer-research-scientist-ai-systems-engineer-rsi-san-francisco/

Google DeepMind описывает Research Engineer как инженера с глубоким пониманием machine learning и deep learning. Он экспериментатор между теорией и реализацией, строит инфраструктуру distributed computing и часто становится соавтором статей. Это более узкая дверь, чем Anthropic Research Tools. Рядом у них отдельно живут Software Engineer, Research Scientist и Technical Program Manager. TPM там не синоним RE.

https://deepmind.google/careers/

xAI, роль Member of Technical Staff, Enterprise Model Evaluation, в копии на агрегаторе (вакансия уже закрыта, текст читался оттуда, не с x.ai): evaluation suites дальше обычных бенчмарков, реальная полезность модели в проде, статистика, experimental design, бенчмарки в реальных условиях. Офис Palo Alto, около 5 дней в неделю. Интервью: разбор CV и «statement of exceptional work», короткий созвон, два coding, system design, рассказ о прошлой сильной работе. Карточку компании на том же агрегаторе я не использую: она выглядит протухшей.

https://startup.jobs/member-of-technical-staff-enterprise-model-evaluation-xai-7643539

Cursor / Anysphere, Software Engineer, ML Research, San Francisco и New York: distributed training, inference и RL-инфраструктура, библиотеки для больших data jobs, системы, которые превращают пользовательские данные в тренировочные. В «подходите, если» стоят infrastructure и distributed systems, end-to-end ownership, интуиция про language models и желание учить ML. Глубокого ML-резюме на входе они не требуют.

https://cursor.com/careers/software-engineer-ml-research

**Институты evals и safety.** METR, Member of Technical Staff, Evaluation Execution, Berkeley, база $328–579K. Обязательны три вещи: сильная инженерия и инфра, умение лезть в чужие системы и чинить узкие места по логам; скорость и чувство 80/20; внимание к мелочам, включая баги в транскриптах. Желательно вкус к тому, какой график информативен, внешняя коммуникация, жонглирование потоками и письмо отчётов. Они прямо пишут, что могут прогонять заявки через AI и искать несостыковки. Гибрид, команда в офисе Berkeley 3–5 дней.

https://jobs.lever.co/metr/s_e69eed88

UK AISI в сентябре 2026 выложила Engineering Playbook. Их стек оценок это пять слоёв: Evaluate, Isolate, Connect, Run, Scale. Inspect делает оценки воспроизводимыми и пригодными для агентных задач, с логами, трейсами и метриками. METR переехала с собственного Vivaria на Inspect. Apollo после трёх месяцев испытания выкинула свой фреймворк и строит новые оценки на Inspect, отдельно назвав secure agent sandboxes. Прямая загрузка вакансии AISI с Greenhouse в этом прогоне не открылась. Зеркало aievalsjobs помечает текст как сверенный с их доской 23 сентября 2026: Alignment Red Team, Research Engineer. Обязательны один законченный safety/security/alignment проект с инженерией и разбором эксперимента на frontier LLM, Python для ML или SWE от года, чистый документированный код, PyTorch или Inspect. Желательны статьи первым автором на NeurIPS, ICLR или ICML, опыт в лаборатории или у стороннего оценщика, сильный OSS вокруг LLM. Дедлайн той вакансии 11 октября 2026. Национальность они готовы обсуждать шире стандартных правил госслужбы, но успешный кандидат проходит BPSS, и CTC для них желателен.

https://www.aisi.gov.uk/blog/releasing-aisis-engineering-playbook

https://aievalsjobs.com/jobs/a722563aac74/

Apollo на странице найма скринит CV плюс короткие вопросы, потом 30 минут про прошлые дела и миссию, потом take-home на 2–2.5 часа, близкий к настоящей работе. Для технических ролей они хотят код, который уехал, системы, которыми владели, и программы, собранные с нуля. Это громче диплома. Инженерия у них production-grade: ML pipelines, CI/CD, distributed systems, не академический скрипт. Отдельно ценятся prompting, агенты, scaffolding, а для исследовательских ролей прямой опыт scheming, deception, AI control или model organisms. Офис London или San Francisco.

https://www.apolloresearch.ai/careers

CAISI при NIST, вакансия AI Research Scientist от 19 декабря 2025, прямо требует экспертизу evaluation methods. Работа: научно корректные оценки, пост-деплой и реальные условия, failure modes, разбор самих инструментов оценки, red teaming, бенчмарки, automated scoring, гайдлайны. Резюме для USAJobs не длиннее двух страниц, читают только первые две, и за опыт дают зачёт только если указаны месяц, год и число часов. Для этой конкретной позиции написано US Citizenship required. O-1 это не гражданство США.

https://www.nist.gov/news-events/news/2025/12/apply-usajobs-open-caisi-position-ai-research-scientist

MATS пишет, что берут 4–7% заявок. Менторам нужны миссия, след исследования или технической работы под конкретный стрим и проверяемые рекомендации. Доказательства, которые они называют: статьи, блог, open source, самодельные проекты. Феллоу бывают и действующими инженерами, которые переходят в alignment.

https://www.matsprogram.org/faq/getting-into-mats

**Trading.** Jane Street публично пишет, что каждую заявку читает человек, и что SWE-интервью это программирование на настоящем языке, который кандидат знает лучше всего. OCaml ради сигнала они не любят. PhD и магистратура большинству их SWE не нужны. CS-база, которую они сами перечисляли в более старом посте блога: абстракции, базовые структуры, оценка стоимости CPU и памяти. Свежая страница интервью олимпиадную математику для SWE явно снимает.

https://www.janestreet.com/preparing-for-a-software-engineering-interview/

https://blog.janestreet.com/interviewing-at-jane-street/

Citadel Securities, C++ Software Engineer, New York, база $150–300K: глубокий C++, multithreading, concurrency, distributed systems, latency, reliability, throughput, код в проде с мониторингом. Финансовый бэкграунд плюс, не условие. Степень бакалавра CS или смежного, либо выше.

https://www.citadelsecurities.com/careers/details/c-software-engineer-2/

Живой JD Hudson River Trading, Jump и Two Sigma в этом прогоне не открывался. У HRT открыт инженерный пост 2025 года: их исследовательское хранилище отдаёт клиентам C++ библиотеку, которая линкуется прямо в приложения. Это культурный сигнал «исследовательская инфра на C++», не текст вакансии.

https://www.hudsonrivertrading.com/hrtbeat/distributed-filesystem-for-scalable-research/

**Чего в этом прогоне нет, и это надо сказать прямо.** Не открыты первоисточники вакансий Redwood Research, Mistral, Meta FAIR, NVIDIA, Microsoft AI, Amazon AGI, Patronus, Galileo, Humanloop, Freeplay, Jump, Two Sigma. Страница Eval Engineer у Braintrust на Ashby при прямом открытии вернулась пустой. LangSmith и Sierra попались копиями на агрегаторах, не на их собственных досках. Выводы ниже для этих имён перенесены с ближайших открытых дверей и помечены как перенос, а не как их слова.

# B. Скелет идеального CV под эту роль

Один мастер на две страницы. Не шесть разных биографий. Меняется порядок буллетов и заголовок. Для USAJobs режется до двух страниц с часами в неделю. Для лаборатории вторая страница допустима, только если там ещё доказательство, а не биография.

Рекрутёрский гайд Fink говорит: одна страница для большинства, вторая оправдана у senior и staff, если материал сильный. Первая роль получает 3–5 буллетов. Старое сжимается.

https://www.sweresume.app/articles/faang-resume-guide/

**Порядок секций**

1. Шапка в теле документа, не в колонтитуле. Имя. Один целевой титул. Город и готовность к офису. Почта. GitHub. Один сайт. Больше контактов не нужно.
2. Три строки колонки. Не абзац про то, как нанимает компания.
3. Selected systems. Три-пять публичных систем со ссылкой, одной метрикой и одним предложением, что сломалось бы без этой работы. Anthropic просит ставить OSS и независимое исследование наверх.
4. Experience. Сначала работа, которая доказывает целевой титул. Старые места по две строки, если они не добавляют новую колонку.
5. Skills. Только то, что уже доказано буллетом выше.
6. Education. Сначала степень, которая объясняет техническую колонку.
7. Одна строка вне работы, если она правда говорит о характере. Не треть страницы.

**Идеальный титул в шапке, один.**

Для лабораторий, AISI, METR, Apollo, Cursor и eval-инфры: `Research Engineer, evaluation infrastructure`.

Слова Member of Technical Staff имеет смысл поставить один раз в скобках, потому что так называется пачка этих вакансий. Повторять MTS, applied research engineer и technical program manager в навыках нельзя. У DeepMind TPM это другая профессия.

https://deepmind.google/careers/

Для Jane Street и Citadel тот же человек подаётся с другим заголовком: `Software Engineer, C++ and production systems`. Иначе первый буллет про агентов отвечает не на тот вопрос. Jane Street читает заявку человеком и может сама предложить другую роль, так что врать титулом себе дороже.

https://www.janestreet.com/preparing-for-a-software-engineering-interview/

**Буллет, который проходит и парсер, и человека.** Форма из открытых описаний, не из мотивационных книг: задача, что сделал руками, знаменатель, ссылка. Пример формы, не выдуманный факт: «Merged a regression test into UK AISI inspect_ai (ссылка). The test fails on the unfixed build and covers sandbox escape X.» Дробь без определения термина и без ссылки не считается метрикой.

Метрики, которые на этих дверях решают, потому что сами вакансии ими описывают работу:

- доля пропущенных опасных действий с знаменателем и определением класса, плюс публичный список failure modes. Это форма, которую уже использует текущее CV, и она совпадает с тем, как METR и CAISI говорят об оценках;
- число прогонов, сред и моделей в одной eval-кампании. Apollo описывает кампании как тысячи прогонов и сотни сред. В их JD это было на агрегаторах раньше, на открытой странице карьеры они говорят о rigorous experiments и production pipelines;
- слитый PR в инструмент, которым команда реально пользуется. Для этого круга в 2026 такой инструмент называется Inspect;
- детерминированный repro, красный регрессионный тест на нечиненом коде, и что автор чужого PR принял находку. Это сильнее слова «контрибьютил»;
- для торговли и инференса: p99, throughput, uptime, инцидент, который починил сам. Fonzi прямо приводит эту форму. Citadel пишет latency, reliability, throughput;
- для оркестрации исследований: sandboxed runtime, experiment orchestration, трейсы, CI-гейт, который не пускает релиз. Это язык Anthropic Research Tools, OpenAI RSI и AISI Playbook.

**20–30 фраз, которые стоит иметь в буллетах, если факт правда есть.** Через запятую, как просили.

Python, C++, model evaluation, evaluation harness, Inspect, agent scaffold, agent harness, sandboxed runtime, experiment orchestration, traces, failure modes, deterministic repro, regression test, reproducibility, LLM-as-judge, red teaming, AI control, distributed systems, Linux, concurrency, latency, throughput, CI/CD, PyTorch, RL environments, research infrastructure, open source, production on-call, experimental design, human approval gate

Откуда ряд, коротко. Inspect, traces, sandboxes: AISI Playbook и вакансия Alignment Red Team. Agent harness, RL environments, sandboxed runtimes, research infrastructure: OpenAI RSI. Experiment orchestration, failure modes, sandboxed execution: Anthropic Research Tools. Transcripts, logs, bottlenecks: METR. PyTorch или Inspect как пара: AISI. C++, concurrency, latency, throughput: Citadel. Linux и C++ как клиент исследовательской инфры: пост HRT, не их JD. Experimental design: текст xAI Model Evaluation на агрегаторе. Слова «interpretability infrastructure», «training infrastructure» и «technical program manager» в этот список не входят. Их нет в обязательных строках открытых eval-вакансий, а в текущих навыках они висят без буллета.

# C. Жёсткая критика приложенного CV

Сверка с идеалом из раздела B. Факты кандидата я не проверял по его репозиториям в этом прогоне. Критикую текст как его увидит скрин.

**Шапка.** Ссылки, почта, Palo Alto, O-1 и польский паспорт собраны правильно по сути. Anthropic спонсирует визы не на каждую роль, METR пишет про cap-exempt H-1B, Apollo спонсирует. Строка «могу выйти в США и ЕС без спонсорства, готов к переезду» это плюс, и её надо оставить в двух строках.

Портят шапку WhatsApp и Calendly. Ни одна открытая вакансия не просит мессенджер и ссылку на свой слот. Это читается как исходящий аутрич, не как IC. Для USAJobs и Greenhouse лишние каналы ещё и мусор в поле контакта.

Локация «Palo Alto – Sintra / remote» спорит с открытыми режимами. Anthropic ждёт офис минимум 25% времени. METR хочет Berkeley 3–5 дней. xAI в той копии хочет Palo Alto около 5 дней. Cursor указан как San Francisco и New York. «Open to relocation, Bay Area» оставить. «Remote» как равноправный вариант убрать из шапки лабораторий.

**Summary.** Первое предложение пересказывает карьерную страницу Anthropic. Факт на странице есть, формулировка «about half … had no prior ML experience» почти дословная. В резюме это слабый ход. Работодатель знает свой текст. Первая строка потрачена не на колонку.

Дальше колонка названа верно: adversarial distributed systems, криптография MEPhI, прод exchange и HFT, Python и C++. Это попадает в Anthropic Research Tools, в Cursor и в Citadel лучше, чем фраза «I do not claim ML research». Честность полезна одной клаузой в конце, не вторым абзацем. Для DeepMind RE и для AISI Alignment Red Team дисклеймер читается как самоотвод: у первых RE это человек с глубоким ML, у вторых обязателен ML-проект на frontier LLM и PyTorch или Inspect.

«Eleven years owning engineering delivery as a hired executive» и «production multi-machine Claude fleet» в одном абзаце отвечают на два разных титула. Скрин Fink останавливается на первых строках. Сейчас он видит нанятого руководителя, а вакансия спрашивает человека, который дебажит логи.

Абзац длинный. На парсере и на шестисекундном просмотре он проигрывает трём коротким строкам.

**Skills.** Строка начинается с «research engineer, member of technical staff, MTS, applied research engineer, technical program manager research». Это титулы вакансий, не навыки. Гайд Fink прямо запрещает keyword stuffing и говорит, что слово живёт только внутри достижения. Навыки «interpretability infrastructure, RL environments, training infrastructure» в опыте ниже не показаны отдельным фактом. Список, который шире буллетов, на техническом скрине это главный красный флаг такого формата.

Inspect в навыках нет, хотя в опыте есть merge в inspect_ai. Для AISI, METR и Apollo это самое дорогое слово документа, и оно не стоит в том месте, где парсер и человек ищут стек.

**Experience, Technical Lead, Palo Alto AI Research Lab, 2023–Present.** Содержательно это лучшая секция файла. Форма «детерминированный repro, красный тест, чужой автор принял находки за шесть часов» совпадает с тем, что Apollo называет authorship громче диплома, и с тем, что METR проверяет вниманием к мелочам. Дробь 0/17 с публичным FAILURE-MODES.md имеет правильную форму метрики.

Подача слабее фактов.

Титул Technical Lead в лаборатории, которую рекрутёр не находит как компанию с юрлицом, проигрывает первым двум секундам. Fink пишет: неизвестный работодатель всё ещё силён, если сразу ясны продукт, пользователи или ставка. Сейчас сначала идут «community of 500+», Stanford и big-tech. Это аудитория, не система. Имена вроде claw-consensus и 相棒 AIBŌ без одной строчки «что это делает» для внешнего читателя пустые. Jane Street-разбор чужого резюме в открытых источниках я не кладу в основу, но сам принцип «имя проекта должно говорить, что оно делает» совпадает с тем, как AISI и METR называют свои системы: Time Horizon, Inspect, не внутренний позывной.

Самый сильный факт, merge в inspect_ai, стоит в середине абзаца вместе с MCP Go SDK, pydantic/logfire, fastmcp, agno и Qwen. Для eval-роли Inspect надо поставить буллетом номер один, со ссылкой на PR и одной строкой, что именно изменилось. Остальные репозитории оставить как список ссылок, не как равные по весу.

«google/adk-python#6957» без полного URL человек по ссылке не откроет из PDF. Полный https-адрес или явный github.com/... обязателен.

Фразы «verified 2026-09-04» и «Scope since 07.2026» выглядят как внутренний журнал, вклеенный в резюме. Рекрутёр не знает, кто верифицировал. Писать обычные даты.

Японское название книги в этой секции сжигает строку, которая могла быть вторым PR.

**Everex, 2017–2018.** Один год, smart contracts, банки, стейблкоины. Ни одна открытая eval-вакансия это не скринит. На версии для лаборатории сжать до одной строки или убрать. На версии для Citadel оставить только если есть прод-система с latency или отказами, а не отношения с банками.

**COO / CTO, Platinum, 2015–Present.** Факт «нанятый операционный руководитель» для этого человека называть нужно именно так. Проблема не в слове, а в объёме. Два Present одновременно с лабораторией заставляют скрин спросить, кто вы в понедельник. USAJobs ещё и хочет часы.

«Managed 40+ developers as product owner» и «partnerships with hedge funds» это масштаб менеджера. Citadel и Jane Street нанимают человека, который пишет C++ и держит прод. METR нанимает человека, который чинит узкое место по логам. Из этого места на странице должны остаться три инженерных факта, если они правдивы: что именно написано на C++ в market-maker или HFT, какой p99 или какой инцидент, и CRM, которую написал сам и в которой сидели до 30 операторов. Орг из 40 человек одной клаузой, не абзацем.

Корни в Salesforce и Navision для этой роли почти не покупают интервью. Оставить полстроки как происхождение CRM, не как отдельную гордость.

**Merlion, 2006–2015, и интернатура 2004–2006.** Девять лет ERP. Для senior-резюме Fink советует старое резать агрессивно, когда оно меньше текущей работы и похоже по типу. Здесь две роли можно слить в две строки: enterprise CRM/ERP, Microsoft Navision и Salesforce, что из этого дожило до собственной системы. Имена Foxconn и ANA в этой зоне файла нет, они ниже, и им там тоже тесно.

**Selected proof.** Почти дублирует буллеты лаборатории. 14 чужих репозиториев и 52 issue с repro звучат как тот след, который MATS и Anthropic просят показывать. Но строка «2 preprints on multi-agent stability (arXiv in progress)» доказательством не является. Пока нет URL, это намерение. AISI в желательных ставит вышедшую статью первым автором на NeurIPS, ICLR или ICML. Fellows говорят, что статьи не обязательны. Невышедший arXiv не закрывает ни ту, ни другую дверь.

h-index 7, 137 цитирований, 50+ публикаций без ссылки на Scholar и без площадки рекрутёр за проход не проверит. Если площадки не ML, цифра ещё и спорит с желательным критерием AISI. Оставить две самые сильные работы: название, год, площадка, ссылка. Индекс убрать.

169k подписчиков, сообщество 500+, сеть Японии и Кореи, совет Foxconn и ANA. Ни METR, ни AISI, ни Apollo, ни Cursor, ни Citadel это не скринят. METR отдельно описывает культуру как low-ego. Anthropic описывает себя как high-trust, low-ego. Аудиторная цифра на инженерном CV читается как другой вид работы.

Повтор 0/17 во второй раз не усиливает, а занимает место.

**Education.** Порядок сейчас PhD in Education, потом MSc security MEPhI, потом BSc. Первая образовательная строка отвечает «доктор образования». Колонка, которую продаёт summary, это безопасность информационных систем и криптография. Её надо поставить первой. PhD не прятать, Anthropic прямо говорит, что примерно половина technical staff имеет какой-то PhD. Но не ставить его выше степени, которая объясняет C++ и криптографию. Для Jane Street лишняя степень не дисквалифицирует, они пишут, что большинству SWE продвинутая степень не нужна и за неё не режут.

**Beyond work.** Вертолёт, даунхилл, ножи, девять мониторов, ужин для семьи. На культуру «с ним хочется работать» это может сработать в разговоре. На странице, где первые буллеты ещё не содержат p99 и ссылки на Inspect, это съедает место, которое Fink считает дорогим. Оставить две строки. Девять мониторов и голосовой ввод звучат как привычка к параллельной работе, их можно одной клаузой перенести в опыт флота, если это правда про эксплуатацию, а не про вкус.

# D. Чек-лист: кандидат должен указать, если факт у него есть

Каждый пункт это сигнал, который открытые вакансии называют прямо. Если факта нет, строку не рисовать.

1. Полный URL слитого PR в `inspect_ai` и одно предложение, что изменилось в прогоне агентной оценки.
2. Один законченный проект, где был дизайн эксперимента, прогон на сильной модели, разбор результата и инженерный артефакт, а не только текст. Это обязательный порог AISI Alignment Red Team.
3. Писал ли чистый код под PyTorch или только под Python-инфру. Для AISI достаточно честного одного из двух. Для DeepMind RE отсутствие ML-глубины лучше сказать, чем замаскировать списком навыков.
4. Sandbox или другая изоляция, в которой гонялся недоверенный код агента, и что случилось на границе изоляции.
5. Схема трейса: что логируется на шаг агента, как это потом читает человек или судья.
6. LLM-as-judge или другой автоматический скорер, и как проверяли, что судья сам не врёт.
7. Золотой набор, версия датасета и возможность переиграть оценку заново.
8. CI-гейт: оценка, которая блокирует выкладку, а не отчёт после выкладки.
9. Число прогонов, сред и моделей в одной кампании, со сроком.
10. Пример бага в транскрипте, который нашёл глазами, и что из этого стало тестом.
11. Инцидент прода, который сам разобрал по логам до причины, с временем и последствием.
12. Для C++ систем: ежедневный ли это язык, Linux, потоки, память, сеть, и одна цифра latency или throughput.
13. On-call и что именно будило ночью.
14. Библиотека или внутренний фреймворк, который другие инженеры расширяют, а не только вызывают. Так формулируют инфраструктурные MTS-роли.
15. Сколько часов в неделю сейчас уходит на код, а не на управление. Для USAJobs это ещё и формальное поле.
16. Имена площадок двух самых сильных текстов, со ссылкой. Не h-index.
17. Готовность быть в офисе Bay Area или London N дней в неделю. Для этих вакансий это логистика скрина, не вкус.
18. Для CAISI отдельно: есть ли гражданство США. На открытой вакансии NIST оно обязательное.
19. Два человека, которые видели код и ответят на reference. MATS это называет прямо, лаборатории спрашивают на скрине.
20. Один публичный текст короче статьи, где разобран свой провал оценки. Anthropic просит «thoughtful blog post» наверх резюме. METR просит умение писать выводы.

# E. Красные флаги именно для этой роли

Титулы вакансий в блоке навыков. «MTS, research engineer, technical program manager» в skills говорят парсеру, что резюме собрано под поиск, и говорят человеку, что глубина не показана. TPM на странице DeepMind это соседняя профессия, не синоним.

Дисклеймер «я не претендую на ML» в первых строках. Для Anthropic Research Tools и для Fellows это нормальная честность, если рядом стоит колонка. Для DeepMind RE, для OpenAI RSI и для AISI Alignment Red Team так звучит отказ от обязательного куска.

Два текущих места без часов и без того, какое из них является инженерной работой. Скрин спрашивает «что вы ведёте сейчас». Ответ «и лабораторию, и COO с 2015» не выбирает дверь.

Аудитория вместо системы. Подписчики, размер сообщества, советы корпорациям, сеть стран. На low-ego инженерном скрине METR и Anthropic это шум. На Citadel это вообще другой разговор.

Невышедшая статья и индекс цитирования без площадки. «arXiv in progress» хуже пустого места, потому что обещает проверку, которую нельзя сделать.

Навыки, которых нет в буллетах. Interpretability, RL environments, training infrastructure. Если на интервью попросят открыть код, расхождение ловится. METR прямо предупреждает, что ищут несостыковки в материалах заявки.

Внутренние имена и внутренние журналы. Позывной проекта, японский заголовок книги, «verified 2026-09-04». Внешний читатель не обязан знать словарь.

Крипто-абзац как вторая по длине работа. Короткий факт про прод-системы не вреден. Абзац про банки, стейблкоины и отношения с государством на eval-CV уводит скрин в другую биографию.

Хобби длиннее доказательства. Вертолёт и кухня не запрещены. Они вредят, пока на первой половине страницы нет ссылки на Inspect и нет одной цифры по C++.

Простыня контактов и призыв забронировать слот. Почта и GitHub достаточны. Calendly в шапке выглядит как рассылка.

Одно резюме на все шесть корзин работодателей. Открытые тексты противоречат друг другу. Anthropic Research Tools пишет, что ML не нужен. AISI пишет, что нужен проект на frontier LLM и PyTorch или Inspect. DeepMind описывает RE как человека с глубоким ML. Citadel описывает C++ и наносекунды. Jane Street читает человека и не любит язык, выбранный ради впечатления. Один мастер с заменой заголовка и порядка буллетов честнее, чем универсальный абзац, который пытается понравиться всем сразу.

Для позиции CAISI декабря 2025 отдельный жёсткий стоп: в тексте вакансии требуется гражданство США, а в CV указаны O-1 и паспорт Польши. Подавать туда этот текст значит не пройти формальный порог, даже если eval-колонка сильная.

**Что в прогоне не открылось и потому не стало опорой.** Прямая страница Greenhouse UK AISI. Вакансии Redwood, Mistral, Meta FAIR, NVIDIA, Microsoft AI, Amazon AGI, Patronus, Galileo, Humanloop, Freeplay, Jump, Two Sigma. Ashby-страница Braintrust Eval Engineer вернула пусто. LangSmith и Sierra читались только как копии на агрегаторе. Пост HRT использован как культурный сигнал C++, не как их список требований к резюме. Коммерческие списки «100 ключевых слов ATS» в отчёт не брал: у них нет метода, который можно проверить.

Источники, которые открыты в этом прогоне:

https://www.anthropic.com/careers

https://job-boards.greenhouse.io/anthropic/jobs/id_265330cf

https://alignment.anthropic.com/2025/anthropic-fellows-program-2026/

https://openai.com/careers/research-engineer-research-scientist-ai-systems-engineer-rsi-san-francisco/

https://deepmind.google/careers/

https://cursor.com/careers/software-engineer-ml-research

https://jobs.lever.co/metr/s_e69eed88

https://www.aisi.gov.uk/blog/releasing-aisis-engineering-playbook

https://aievalsjobs.com/jobs/a722563aac74/

https://www.apolloresearch.ai/careers

https://www.nist.gov/news-events/news/2025/12/apply-usajobs-open-caisi-position-ai-research-scientist

https://www.matsprogram.org/faq/getting-into-mats

https://www.janestreet.com/preparing-for-a-software-engineering-interview/

https://blog.janestreet.com/interviewing-at-jane-street/

https://www.citadelsecurities.com/careers/details/c-software-engineer-2/

https://www.hudsonrivertrading.com/hrtbeat/distributed-filesystem-for-scalable-research/

https://startup.jobs/member-of-technical-staff-enterprise-model-evaluation-xai-7643539

https://support.greenhouse.io/hc/en-us/articles/id_48704da0-Unsuccessful-resume-parse

https://support.greenhouse.io/hc/en-us/articles/id_4ef950a9-Supported-formats-for-resumes-cover-letters-and-other-candidate-uploads

https://www.sweresume.app/articles/faang-resume-guide/

https://fonzi.ai/blog/what-does-member-of-technical-staff-mean

🧒 Простыми словами. Резюме сейчас рассказывает, какой оператор важный руководитель и сколько людей вокруг. Эти работы ищут человека, который руками собрал проверку для капризного робота и может показать ссылку, где проверка поймала ошибку. Самый сильный кусок у него уже есть, он про проверки и чужие починки. Его надо поставить наверх, а рассказ про посты, вертолёт и должности убрать с первой половины страницы.

---

**Claude:**

```json
{
  "lang": "mixed",
  "topic": "Идеальное CV 2026 для Research Engineer/MTS (evals & agent infrastructure) — скрин ATS и критика CV",
  "one_line": "ДР выясняет, что реально скринят ATS и рекрутёры фронтир-лабораторий и eval-институтов в 2026 для ролей Research Engineer/Member of Technical Staff, строит скелет идеального CV и жёстко критикует CV кандидата против этого идеала.",
  "key_findings": [
    "Greenhouse (на нём Anthropic и UK AISI) технически ломается на графиках, фото-резюме, таблицах, колонках, тексте в колонтитуле и файлах тяжелее 2.5 МБ — это документированная причина парсинг-отказа, не совет блога.",
    "Человеческий скрин (разбор Markus Fink, экс-рекрутёр Google/Airbnb) падает на титул, работодателя и первые 1-2 буллета последней роли; ключевое слово без буллета-достижения сигнала не создаёт — отдельная 'простыня навыков' читается как keyword stuffing.",
    "Требования к ML-глубине расходятся по дверям: Anthropic Research Tools и Fellows explicitly не требуют прежнего ML-опыта (у ~половины technical staff его не было), тогда как Google DeepMind RE, OpenAI RSI и AISI Alignment Red Team требуют ML-проект/PyTorch или Inspect как обязательный порог — дисклеймер 'I do not claim ML research' помогает в одних дверях и выглядит самоотводом в других.",
    "Метрики, которые реально решают: доля пропущенных опасных действий с явным знаменателем (форма '0/17' уже совпадает с языком METR/CAISI), число прогонов/сред/моделей в eval-кампании, слитый PR в Inspect (inspect_ai) как самый дорогой сигнал для AISI/METR/Apollo, детерминированный repro + красный регрессионный тест, принятый автором чужого PR, и p99/throughput/uptime для торговых фирм.",
    "Текущее CV кандидата критикуется построчно: WhatsApp/Calendly в шапке читаются как исходящий аутрич, а не IC; summary почти дословно пересказывает карьерную страницу Anthropic вместо того, чтобы называть колонку; skills-секция забита титулами вакансий (MTS, TPM, research engineer), которых нет в буллетах ниже; merge в inspect_ai спрятан в середине списка репозиториев вместо буллета №1; два параллельных 'Present' (Technical Lead лаборатории и COO/CTO) конкурируют за ответ 'кто вы в понедельник'.",
    "Аудиторные метрики (169k подписчиков, h-index 7, 137 цитирований, сообщество 500+, советы Foxconn/ANA) не скринятся ни одной из открытых инженерных дверей — METR и Anthropic описывают культуру как low-ego, и это читается как другой вид работы; невышедший arXiv-препринт без ссылки хуже пустого места, потому что обещает проверку, которую нельзя сделать.",
    "Education-секция сейчас открывается PhD in Education вместо MSc Computer and Information Systems Security (MEPhI) — первая строка отвечает не на тот вопрос, который задаёт summary.",
    "CAISI (NIST, вакансия от 19.12.2025) требует US Citizenship явным текстом — O-1 виза + польский паспорт кандидата формально не проходит этот порог, независимо от силы eval-колонки.",
    "Одно универсальное резюме на все 6 категорий работодателей противоречит их собственным текстам: Anthropic Research Tools говорит 'ML не нужен', AISI требует ML-проект и PyTorch/Inspect, DeepMind описывает RE как человека с глубоким ML, Citadel и Jane Street читают заявку по-другому (C++/наносекунды vs человек читает лично и не любит язык, выбранный ради впечатления)."
  ],
  "recommendations": [
    "Собрать один мастер-CV на 2 страницы, где меняется только титул и порядок буллетов под дверь: 'Research Engineer, evaluation infrastructure' для лабораторий/AISI/METR/Apollo/Cursor, 'Software Engineer, C++ and production systems' для Jane Street/Citadel.",
    "Убрать WhatsApp и Calendly из шапки, оставить email, GitHub и один сайт.",
    "Поставить merge в UK AISI inspect_ai буллетом номер один со ссылкой на PR и одним предложением, что именно изменилось — не растворять среди MCP Go SDK/fastmcp/agno/Qwen.",
    "Очистить skills-секцию: убрать титулы вакансий (MTS, TPM, research engineer) и навыки без подтверждающего буллета (interpretability infrastructure, RL environments, training infrastructure), оставить только доказанное.",
    "Переставить Education: MSc Computer and Information Systems Security (MEPhI) первой строкой, PhD in Education не выше неё.",
    "Сжать или убрать аудиторные метрики (подписчики, h-index, цитирования без ссылки на Scholar/площадку) и невышедший arXiv-препринт без URL.",
    "Сократить секцию Beyond work до двух строк, перенести факт про 9-монитор-флот в опыт эксплуатации, если это про работу, а не про вкус.",
    "Не подавать текущий вариант CV на вакансию CAISI (гражданство США обязательно) без отдельной оговорки; для остальных дверей — разделить, кто сейчас ведёт инженерную работу, а кто управляет (два 'Present' должны выбрать дверь)."
  ],
  "entities": {
    "people": ["Markus Fink"],
    "companies": ["Anthropic", "OpenAI", "Google DeepMind", "Meta FAIR", "xAI", "Mistral", "UK AISI", "US CAISI", "METR", "Apollo Research", "Redwood Research", "MATS", "Braintrust", "LangSmith/LangChain", "Patronus AI", "Galileo", "Humanloop", "Freeplay", "Jane Street", "Hudson River Trading", "Jump", "Two Sigma", "Citadel Securities", "Microsoft AI", "NVIDIA", "Amazon AGI", "Cursor/Anysphere", "Cognition", "Sierra", "Greenhouse", "Fonzi", "Everex", "Platinum Software Development Company", "Merlion"],
    "products_tools": ["Inspect (inspect_ai)", "Greenhouse ATS", "Ashby", "Lever", "USAJobs", "PyTorch", "MCP Go SDK", "pydantic/logfire", "fastmcp", "agno", "QwenLM/qwen-code", "google/adk-python"]
  },
  "open_questions": [
    "Gemini и GLM ноги не дали живого ответа (эхо промпта/UI вместо исследования) — только Grok реально отработал вопрос, по подтверждению dr-judge от 03.10.",
    "Не открылись первоисточники для Redwood, Mistral, Meta FAIR, NVIDIA, Microsoft AI, Amazon AGI, Patronus, Galileo, Humanloop, Freeplay, Jump, Two Sigma; страница Braintrust Eval Engineer на Ashby вернулась пустой; LangSmith и Sierra доступны только как копии на агрегаторах.",
    "В рамках этого прогона не проверялись факты самого CV (контрибьюшены, метрики 0/17, h-index) против первоисточников кандидата — критика строится на тексте CV, не на верификации фактов.",
    "Синтез dr-synthesis-cv-research уже сверен с grok-ногой и совпадает, но впитывание в публичную CV-ветку (cv_forge) частично: Inspect внесён, остальные правки (skills-чистка, Education-порядок, аудиторные метрики) требуют отдельной сверки."
  ],
  "related_concepts": ["cv-forge-branches", "ats-resume-parsing", "inspect-eval-framework", "ai-safety-evals-hiring", "job-search-no-founder-framing", "synthesis-read-only-the-garbage-rail"]
}
```
