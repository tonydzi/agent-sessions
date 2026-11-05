---
session: s_c85cbe7c
date: 2026-09-25
words: 2175
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c85cbe7c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-13-1604
REGISTRY TOPIC: идеальное CV 2026 — Institutional Onboarding / Ecosystem BD (Hyperliquid & Perp-DEX Ecosystems) [кластер hyperliquid]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-13-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-13-1604.md) =====
---
id: DR26-09-24-HUB-13-1604
date: 2026-09-24 16:04:49
theme: идеальное CV 2026 — Institutional Onboarding / Ecosystem BD (Hyperliquid & Perp-DEX Ecosystems) [кластер hyperliquid]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-21-2206
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — Institutional Onboarding / Ecosystem BD (Hyperliquid & Perp-DEX Ecosystems)

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели: (1) core-команды и foundation'ы perp-DEX и деривативных L1 (Hyperliquid, dYdX, Vertex, Drift, Aevo и аналоги) — роли ecosystem BD / institutional partnerships; (2) HIP-3-деплойеры и команды capital-backed markets, строящие новые рынки поверх Hyperliquid; (3) маркет-мейкеры и proprietary trading фирмы с крипто-десками (Wintermute, GSR, Amber, Flow Traders класс) — роли institutional coverage / counterparty onboarding; (4) прайм-брокеры, кастодианы и credit-дески, заводящие институционалов в DeFi/перпы (FalconX, Hidden Road, Copper класс); (5) вольт-протоколы и builder-code приложения экосистемы Hyperliquid (frontends, структурные продукты на vaults), которым нужен человек на институциональный капитал и листинги; (6) ecosystem-фонды и growth-подразделения L1/L2, финансирующие ликвидность и онбординг маркет-мейкеров.

## Текущее CV кандидата (полный текст)
```
# [ИМЯ] [ФАМИЛИЯ] — Institutional Onboarding / Ecosystem BD (Hyperliquid & Perp-DEX Ecosystems)

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I bring institutional capital and market-maker flow into trading ecosystems — and I ship on the platform myself. Owner-level relationships with market makers, hedge funds, brokers and exchanges built over a decade of servicing them; shipped crypto-exchange infrastructure hands-on (cryptocurrency backends, market-maker engines, high-frequency trading systems) and consulted startups building exchanges and perpetuals venues. Fluent in how a perp-DEX ecosystem actually monetizes: deployer economics (HIP-3-style capital-backed markets), builder-code distribution, vault/LP capital, prime-broker onboarding, KYC/KYB bilateral credit. On top of that — an AI-native operator layer: a production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines — with published evals, so risk dashboards, monitoring and CRM-driven origination come built-in. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## What I do for an ecosystem team (90-day shape)
- Institutional onboarding pipeline: qualified conversations with funds, custodians, market makers and credit desks — tracked weekly in CRM, measured by meetings held and capital onboarded, not by reach
- Liquidity & listings orchestration: match market makers and OTC desks to new markets/vaults; a decade of matchmaking founders ↔ investors ↔ liquidity, 10,000+ founder calls and 2,000+ institutional-investor calls behind it
- Capital formation for deployer/staking/credit products: fund raised and syndicated since 2017 ($35M fund under management, syndicate of 250 VCs/angels)
- Agent-driven ops on the platform: monitoring, risk dashboards, origination automation — built with my own fleet, documented in public

## Skills
Python, C++, institutional onboarding, ecosystem BD, perpetuals, perp DEX, Hyperliquid, HIP-3, builder codes, vaults, market making, prime brokerage, liquidity, listings, capital formation, staking, credit desks, KYC/KYB, crypto, AI agents

## Experience

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). Portfolio focus: exchange/trading infrastructure (~70% crypto), with rare depth in Silicon Valley and even the Japanese and Korean startup communities.

- Shipped crypto-exchange infrastructure: cryptocurrency backends, market-maker engines, high-frequency trading systems; partnerships with hedge funds, market makers, brokers
- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents
- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation
- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe
- Wrote my own CRM to run it: social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native
- Designed one of the first detailed frameworks for a national government to issue its own stablecoins (regulatory + token-economic design); built my own stablecoin project (QDAO, 2019)
- Managed a distributed engineering org of 40+ developers across APAC as product owner

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

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
  "topic": "Идеальное CV 2026 для Institutional Onboarding / Ecosystem BD в perp-DEX экосистемах (Hyperliquid и аналоги)",
  "one_line": "ДР должен был выяснить, что ATS и рекрутёры реально скринят в 2026 для ролей institutional onboarding/ecosystem BD в perp-DEX экосистемах, дать скелет идеального CV и построчную критику текущего CV оператора — но в переданном тексте присутствует только постановка задачи и полный текст текущего CV, без фактических ответов вендоров на 5 вопросов.",
  "key_findings": [
    "В доступном материале нет ответов chatgpt/gemini/grok на 5 вопросов ДР — присутствует только промпт-задание и приложенное CV; согласно системной пометке dr_reconcile, на диске обнаружена только 1 из 3 ожидаемых 'ног' (ответов вендоров), реестр 'issued' исправлен на фактический статус",
    "Целевые работодатели заданы в 6 категорий: core-команды/foundation'ы perp-DEX и деривативных L1 (Hyperliquid, dYdX, Vertex, Drift, Aevo) на ролях ecosystem BD/institutional partnerships; HIP-3-деплойеры; маркет-мейкеры и proprietary trading фирмы (Wintermute/GSR/Amber/Flow Traders класс); прайм-брокеры/кастодианы/кредитные дески (FalconX/Hidden Road/Copper класс); vault-протоколы и builder-code приложения Hyperliquid; ecosystem-фонды и growth-подразделения L1/L2",
    "Жёсткое ограничение позиционирования: кандидата запрещено называть 'founder/фаундер' или 'не-кодером' — он наёмный руководитель (COO/CTO), программист Python и C++",
    "Текущее CV построено вокруг тезиса 'привожу институциональный капитал и market-maker flow в трейдинг-экосистемы и сам шиплю на платформе' — с акцентом на deployer economics (HIP-3), builder-code distribution, vault/LP капитал, prime-broker onboarding, KYC/KYB bilateral credit",
    "В CV заявлен AI-native operator layer как дифференциатор: продакшн-флот Claude на 6 машинах, публичные evals, consensus/CRM/автоматизации, что подаётся как встроенные risk dashboards и CRM-driven origination",
    "Proof-секция CV опирается на верифицируемые OSS-артефакты (google/adk-python PR-ревью, 14 сторонних проектов, 52 issue с репродукциями, 115 публичных репозиториев, 50+ публикаций/137 цитирований/h-index 7, измеренные fleet-reliability evals 0/17 Tier-2 нарушений) и на нетворк-метрики (169k Telegram-канал, 500+ community в Palo Alto)",
    "prior_art у этого ДР — DR26-09-14-ZB-21-2206, то есть тема идеального CV для этого кластера уже исследовалась ранее и это повторный/уточняющий заход"
  ],
  "recommendations": [
    "Долить недостающие 2 из 3 ног (ответы chatgpt/gemini/grok на 5 вопросов) прежде чем строить финальные выводы по скелету CV и построчную критику — на руках сейчас нет фактического анализа ATS-сигналов, ключевых слов, красных флагов",
    "После получения полного комплекта ответов свериться с prior_art DR26-09-14-ZB-21-2206 на предмет дублирования/расхождений по тому же кластеру Hyperliquid",
    "Не использовать текущий текст как источник готовых рекомендаций по CV — он содержит только задание и объект анализа (CV), а не результат"
  ],
  "entities": {
    "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
    "companies": ["Hyperliquid", "dYdX", "Vertex", "Drift", "Aevo", "Wintermute", "GSR", "Amber", "Flow Traders", "FalconX", "Hidden Road", "Copper", "Platinum Software Development Company", "Platinum VC & Incubator", "Grand Corp", "Bloomberg", "Everex", "Merlion", "Palo Alto AI Research Lab", "Foxconn", "ANA Airlines"],
    "products_tools": ["HIP-3", "claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "claude-bible", "agent-leash", "sqlite-graph-memory", "second-brain-starter-kit", "google/adk-python", "QDAO"]
  },
  "open_questions": [
    "Фактические ответы chatgpt/gemini/grok на все 5 вопросов (ATS-сигналы, скелет идеального CV с ключевыми словами, построчная критика текущего CV, чек-лист сигналов опыта, красные флаги) — отсутствуют в переданном материале, статус ДР на диске неполный (1/3 ног)",
    "Нужно ли перезаказывать недостающие ноги или дособрать их у прежних вендоров",
    "Как соотносится этот ДР с prior_art DR26-09-14-ZB-21-2206 — что нового добавляет этот заход"
  ],
  "related_concepts": ["cv-forge", "ats-screening", "hyperliquid-ecosystem-bd", "institutional-onboarding-positioning", "perp-dex-employer-map", "dr-registry-reconcile"]
}
```
