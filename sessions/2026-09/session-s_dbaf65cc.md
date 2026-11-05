---
session: s_dbaf65cc
date: 2026-09-25
words: 2033
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_dbaf65cc` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-09-1604
REGISTRY TOPIC: идеальное CV 2026 — Forward-Deployed / AI Deployment Engineer (Solutions) [кластер fde]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-09-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-09-1604.md) =====
---
id: DR26-09-24-HUB-09-1604
date: 2026-09-24 16:04:49
theme: идеальное CV 2026 — Forward-Deployed / AI Deployment Engineer (Solutions) [кластер fde]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-20-2206,DR26-09-14-ZB-16-2205,DR26-09-14-ZB-11-2009
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — Forward-Deployed / AI Deployment Engineer (Solutions)

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — архетипы компаний, нанимающих Forward-Deployed / AI Deployment / Solutions Engineers:

1. Frontier-лаборатории с командами развёртывания у заказчика (Anthropic, OpenAI, Google DeepMind — роли Forward Deployed Engineer / Applied AI / Solutions Architect для enterprise-клиентов).
2. Компании палантировской модели «инженер живёт у клиента» (Palantir и её выпускники: гос- и defense-tech, data-платформы с FDE-культурой).
3. Applied-AI / агентные стартапы, продающие внедрение LLM-агентов в enterprise (Sierra, Decagon, Glean, Harvey-подобные вертикальные AI-компании — post-sales / deployment инженеры).
4. AI-инфраструктурные платформы и data/eval-компании с customer-facing инженерией (Scale AI, LangChain/LlamaIndex-экосистема, вендоры RAG/observability/evals).
5. Облачные провайдеры и их профессиональные сервисы по GenAI (AWS/Azure/GCP — GenAI Specialist SA, AI deployment consultants).
6. Регулируемые enterprise-заказчики, строящие внутренние AI-платформы (финтех, банки, страхование, здравоохранение), где ценят compliance-опыт и работу с регуляторами.

## Текущее CV кандидата (полный текст)
```markdown
# [ИМЯ] [ФАМИЛИЯ] — Forward-Deployed / AI Deployment Engineer (Solutions)

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
I deploy AI into messy real-world environments every day: I run a production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. I ship working agent systems end-to-end (MCP connectors, RAG over a 10-year knowledge base, CRM automation, evals) and can sit in front of a customer or a regulator: 15+ years operator/BD background, incl. structuring crypto payments and stablecoins with banks and governments in SE Asia — adversarial, compliance-heavy environments. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, forward deployed engineer, solutions engineer, AI deployment, LLM integration, MCP, RAG, agents, evals, Claude, customer-facing, post-sales

## Experience

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). The job a partner at 500 Startups or Plug and Play does — deal flow, cohorts, founder coaching, advisor matching, fundraising — done hands-on at a boutique incubator, with rare depth in Silicon Valley and even the Japanese and Korean startup communities. Portfolio ~70% crypto / 30% other, AI startups included.

- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents
- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched investor base across the US, Japan, Korea, China, Australia and Europe
- Wrote my own CRM to run it (roots: 5 years building ERP/CRM on Salesforce and Microsoft Navision at Merlion): social enrichment, parsing at scale, lead-to-call pipelines; up to 30 operators worked in it daily; today it is AI-native
- Ran cohorts end-to-end: recruited builders, coached founders, matched advisors; enterprise advisory for subsidiaries of Foxconn and ANA Airlines
- Shipped crypto-exchange infrastructure: cryptocurrency backends, market-maker engines, high-frequency trading systems; partnerships with hedge funds, market makers, brokers
- Designed one of the first detailed frameworks for a national government to issue its own stablecoins (regulatory + token-economic design)
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

> `Bash` -- {"command": "ls \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-24-HUB-09-1604\\results\" 2>&1", "description": "List DR result files on disk"}

---

**Claude:**

```json
{
 "lang": "mixed",
 "topic": "Идеальное CV 2026 для Forward-Deployed / AI Deployment Engineer (Solutions)",
 "one_line": "Задание внешним LLM (chatgpt/gemini/grok) — по CV оператора и архетипам работодателей (Anthropic/OpenAI/Palantir/Sierra/Scale AI/облачные GenAI SA) определить, что ATS и рекрутёры в 2026 скринят для роли Forward-Deployed/AI Deployment Engineer, дать скелет идеального CV, построчную критику и красные флаги; тело ответов вендоров в этом документе отсутствует — на диске найдена только часть результатов (1/3), реестр был помечен 'issued' без подтверждения.",
 "key_findings": [
 "Файл содержит только постановку задачи (5 вопросов + полный текст CV кандидата + список из 6 архетипов целевых работодателей) — фактические ответы chatgpt/gemini/grok по существу вопросов в теле отчёта не приведены",
 "dr_reconcile 2026-09-25 обнаружил рассинхрон: на диске лежит только 1 из 3 ожидаемых 'ног' (вендорских ответов), при этом реестр ошибочно показывал статус 'issued' (как будто все получены) — статус исправлен вручную по факту",
 "Целевые архетипы работодателей для этой роли явно заданы: frontier-лаборатории (Anthropic/OpenAI/DeepMind FDE), Palantir-модель, applied-AI/agentic стартапы (Sierra, Decagon, Glean, Harvey), AI-инфраструктура (Scale AI, LangChain/LlamaIndex), облачные GenAI Specialist SA (AWS/Azure/GCP), регулируемый enterprise (финтех/банки/здравоохранение)",
 "Кандидату жёстко запрещено называться 'founder/фаундер' или 'не-кодером' в любых выводах ресёрча — позиционирование зафиксировано как COO/CTO наёмный руководитель, программист Python/C++",
 "Текущее CV кандидата уже структурировано под роль (Summary → Skills → Experience → Selected proof → Education → Beyond work) с явными proof-артефактами: 115 публичных репозиториев, OSS-вклады в 14 проектов, 169k-подписчиков TG-канал, US O-1 + EU-паспорт, измеренные evals агентного флота (0/17 Tier-2 действий проскочили гейт)"
 ],
 "recommendations": [
 "Перед использованием заметки — добрать недостающие ноги ресёрча (2 из 3 вендоров) через `/dr-fanout` или ручной relaunch на chatgpt/gemini/grok по тому же промпту, иначе выводы по вопросам 1-5 не из чего делать",
 "После получения полных ответов — прогнать сверку реестра `dr_reconcile`, чтобы статус 'issued' отражал реальное количество результатов на диске, а не предполагаемое",
 "Использовать уже собранный в этом файле список из 6 архетипов работодателей как готовый чек-лист таргетинга при рассылке CV, не дожидаясь остальных ног"
 ],
 "entities": {
 "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
 "companies": ["Anthropic", "OpenAI", "Google DeepMind", "Palantir", "Sierra", "Decagon", "Glean", "Harvey", "Scale AI", "LangChain", "LlamaIndex", "AWS", "Azure", "GCP", "Everex", "Merlion", "Foxconn", "ANA Airlines", "Platinum Software Development Company", "Platinum VC & Incubator", "Palo Alto AI Research Lab"],
 "products_tools": ["MCP", "RAG", "claw-consensus", "verbatim-citation-gate", "claude-bible", "agent-leash", "agent-control-plane-casebook", "sqlite-graph-memory", "second-brain-starter-kit", "headroom"]
 },
 "open_questions": [
 "Каковы фактические ответы chatgpt/gemini/grok на 5 вопросов (скрин ATS/рекрутёров, скелет идеального CV, критика текущего CV, чек-лист сигналов, красные флаги) — в доступном тексте отсутствуют",
 "Почему реестр показывал 'issued' при 1/3 ног на диске — сбой процесса сбора результатов или преждевременная отметка статуса",
 "Нужно ли перезаказывать недостающие 2 ноги под тем же DR-ID или заводить новый номер"
 ],
 "related_concepts": ["cv-forge", "apply-pipeline", "fde-cluster-cv", "dr-quorum-registry", "job-search-no-mycroft-disclosure", "never-call-dev-a-founder"]
}
```
