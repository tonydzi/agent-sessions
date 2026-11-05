---
session: s_13aec556
date: 2026-09-25
words: 2215
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_13aec556` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-15-1604
REGISTRY TOPIC: идеальное CV 2026 — Research Engineer / Member of Technical Staff (evals & agent infrastructure) [кластер research]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-15-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-15-1604.md) =====
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

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Идеальное CV 2026 для Research Engineer / MTS (evals & agent infrastructure)",
 "one_line": "Бриф для внешних LLM (ChatGPT/Gemini/Grok) на исследование того, как ATS и рекрутёры фронтир-лабораторий и eval/agent-инфраструктурных компаний скринят CV в 2026 году, и как переработать CV кандидата под этот стандарт.",
 "key_findings": [
  "Файл содержит только постановку задачи (бриф + текущее CV кандидата) для трёх внешних LLM (chatgpt, gemini, grok) — фактические ответы вендоров на 5 вопросов в тексте отсутствуют",
  "Целевые работодатели разбиты на 6 кластеров: frontier-лаборатории (Anthropic, OpenAI, DeepMind, Meta FAIR, xAI, Mistral) роли Research Engineer/MTS в evals/agent infra/safety; AI-safety институты (UK AISI, US CAISI, METR, Apollo Research, Redwood Research, MATS); eval/observability-стартапы (Braintrust, LangSmith, Patronus AI, Galileo, Humanloop, Freeplay); HFT/trading-фирмы (Jane Street, HRT, Jump, Two Sigma, Citadel Securities); big-tech applied research (Google, Microsoft AI, NVIDIA, Amazon AGI); agent-инфраструктурные компании (Cursor/Anysphere, Cognition, Sierra)",
  "Жёсткое ограничение бренда кандидата: запрещено называть его 'founder/фаундер' или 'не-кодером' — позиционирование строго как наёмный руководитель (COO/CTO), программист Python и C++",
  "Текущее CV кандидата уже построено вокруг нарратива 'engineering research runs on' (eval harnesses, reproducibility, failure taxonomies, agent control planes) вместо claim'а ML-research опыта, с явными числовыми proof-точками: merge в UK AISI inspect_ai + 14 сторонних проектов, 52 issues с репродукциями, 0/17 Tier-2 действий прошли approval gate, 169k-подписчиков Telegram-канал, h-index 7 / 137 цитирований",
  "Структура CV: Summary → Skills → Experience (Palo Alto AI Research Lab 2023–present, Everex 2017–2018, Platinum COO/CTO 2015–present, Merlion Navision/Salesforce 2006–2015, CRM intern 2004–2006) → Selected proof → Education (PhD, MSc MEPhI security, BSc MEPhI) → Beyond work",
  "prior_art указан как DR26-09-15-ZB-05-2040 — более раннее исследование той же темы, к которому этот DR является продолжением/уточнением"
 ],
 "recommendations": [
  "Дождаться/найти фактические ответы вендоров (chatgpt/gemini/grok) на 5 вопросов — без них закрыть тему нельзя: в реестре текущий статус выправлен на основе того, что на диске найдена только 1/3 ног (vendor-ответов)",
  "После получения ответов свести их построчно против текущего CV: скелет секций, точный список 20-30 ключевых слов, чек-лист сигналов опыта, красные флаги — и внести правки в resume.json/cv_forge",
  "Сверить с prior_art DR26-09-15-ZB-05-2040 на предмет дублирующихся или уже отвеченных вопросов, чтобы не пересчитывать то, что уже известно"
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]"],
  "companies": ["Anthropic", "OpenAI", "Google DeepMind", "Meta FAIR", "xAI", "Mistral", "UK AISI", "US CAISI", "METR", "Apollo Research", "Redwood Research", "MATS", "Braintrust", "LangSmith", "LangChain", "Patronus AI", "Galileo", "Humanloop", "Freeplay", "Jane Street", "Hudson River Trading", "Jump", "Two Sigma", "Citadel Securities", "Google", "Microsoft AI", "NVIDIA", "Amazon AGI", "Cursor/Anysphere", "Cognition", "Sierra", "Adept", "Everex", "Platinum Software Development Company", "Platinum VC & Incubator", "Merlion"],
  "products_tools": ["inspect_ai", "MCP Go SDK", "pydantic/logfire", "fastmcp", "agno", "QwenLM/qwen-code", "google/adk-python", "claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "claude-bible", "agent-leash", "sqlite-graph-memory", "second-brain-starter-kit", "Salesforce", "Microsoft Navision"]
 },
 "open_questions": [
  "Что ATS и рекрутёры реально скринят в 2026 для этой роли: сигналы, ключевые слова, титулы (с источниками) — ответ вендоров отсутствует в тексте",
  "Скелет идеального CV: порядок секций, точный титул, список 20-30 ключевых фраз, решающие метрики/proof-артефакты — не получен",
  "Построчная критика приложенного CV против идеала — не получена",
  "Чек-лист 10-20 конкретных сигналов опыта, которые ожидаются в таких CV — не получен",
  "Красные флаги, вредящие CV этой роли (слова/форматы/акценты) — не получены"
 ],
 "related_concepts": ["dr_reconcile", "resume.json / cv_forge pipeline", "ATS screening 2026", "AI-safety evals hiring", "agent-infrastructure engineering roles"]
}
```
