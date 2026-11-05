---
session: s_1444bb2d
date: 2026-09-25
words: 1906
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1444bb2d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-16-1604
REGISTRY TOPIC: идеальное CV 2026 — Technical Writer / AI Educator / Evals & Research-adjacent [кластер scholar]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-16-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-16-1604.md) =====
---
id: DR26-09-24-HUB-16-1604
date: 2026-09-24 16:04:50
theme: идеальное CV 2026 — Technical Writer / AI Educator / Evals & Research-adjacent [кластер scholar]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-23-2206
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — Technical Writer / AI Educator / Evals & Research-adjacent

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели: (1) frontier-лаборатории и их команды документации / developer relations / education (уровня Anthropic, OpenAI, Google DeepMind — роли Technical Writer, DevRel Engineer, AI Educator); (2) eval- и benchmark-компании (уровня Scale AI, Epoch AI, LMArena, METR — роли evals writer / research communicator); (3) AI-education платформы и курс-продюсеры (уровня DeepLearning.AI, Coursera, O'Reilly — авторы курсов и учебных программ по LLM/агентам); (4) институты AI-safety и государственные AI-институты (уровня UK AISI, NIST — technical writing и reproducible evals); (5) developer-tools компании с LLM-продуктом, где документация = продукт (уровня LangChain, Weights & Biases, Hugging Face); (6) технические издательства и research-adjacent контент-команды (technical author / research writer при исследовательских группах).

## Текущее CV кандидата (полный текст)
```
# [ИМЯ] [ФАМИЛИЯ] — Technical Writer / AI Educator / Evals & Research-adjacent

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
PhD + practitioner: 50+ published items, 137 citations, h-index 7 (verified 2026-09-01); 2 preprints on multi-agent stability (arXiv in progress). Designed and taught Solidity curricula; writing a book on human-AI collaboration (相棒 AIBŌ · The Partner) while running a production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines. I turn messy frontier practice into reproducible docs, evals and courses. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, technical writing, documentation, developer education, evals, curriculum, research engineer adjacent, publications, benchmarks

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
1. Что ATS и рекрутёры ЭТОГО типа ролей реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками.
2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают.
3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям.
4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт).
5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты).

## Формат ответа
ВАЖНО: не объявляй план и не пиши преамбулу вида «сначала я поищу источники» — первой строкой ответа сразу начинай секцию 1 готового отчёта.

Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

---

**Claude:**

{
  "lang": "ru",
  "topic": "Идеальное CV 2026 для Technical Writer / AI Educator / Evals-ролей во frontier-лабораториях",
  "one_line": "Задание трём внешним LLM (chatgpt/gemini/grok) разобрать, что ATS и рекрутёры реально скринят в CV для ролей Technical Writer/DevRel/AI Educator/evals-writer в 2026, и построчно раскритиковать приложенное CV кандидата против этого идеала.",
  "key_findings": [
    "Отчёт по факту содержит только задание исследователю (5 вопросов + полный текст CV кандидата) — фактические ответы вендоров (chatgpt/gemini/grok) в этом файле отсутствуют; dr_reconcile 2026-09-25 подтверждает: на диске лежит 1/3 ног, статус в реестре 'issued' выправлен по факту несоответствия",
    "Целевые работодатели заданы явно в 6 кластерах: frontier-лаборатории (Anthropic/OpenAI/DeepMind, роли Technical Writer/DevRel/AI Educator), eval-компании (Scale AI, Epoch AI, LMArena, METR), AI-education платформы (DeepLearning.AI, Coursera, O'Reilly), AI-safety институты (UK AISI, NIST), dev-tools с LLM-продуктом (LangChain, W&B, Hugging Face), технические издательства/research-adjacent контент-команды",
    "Жёсткое позиционирование: кандидат — наёмный руководитель (COO/CTO) и программист Python/C++; в выводах запрещено называть его 'founder/фаундер' или 'не-кодером'",
    "Текущее CV кандидата уже насыщено количественными proof-точками: 50+ публикаций, 137 цитирований, h-index 7 (verified 2026-09-01), 115 публичных репозиториев, 169k-подписчиков Telegram-канал, слияние правок в 14 сторонних инженерных проектов + 52 issue с репродукциями, 0/17 Tier-2 действий проскочивших human approval gate",
    "Структура CV: Summary → Skills → Experience (6 позиций от 2004 до наст. времени) → Selected proof → Education (PhD + MSc + BSc) → Beyond work (хобби/личное)",
    "US O-1 виза (активна) + гражданство ЕС (Польша) заявлены как готовность к немедленному найму без спонсорства визы"
  ],
  "recommendations": [],
  "entities": {
    "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
    "companies": ["Anthropic", "OpenAI", "Google DeepMind", "Scale AI", "Epoch AI", "LMArena", "METR", "DeepLearning.AI", "Coursera", "O'Reilly", "UK AISI", "NIST", "LangChain", "Weights & Biases", "Hugging Face", "Palo Alto AI Research Lab", "Platinum Software Development Company", "Platinum VC & Incubator", "Everex", "Merlion", "Grand Corp", "Foxconn", "ANA Airlines", "500 Startups", "Plug and Play"],
    "products_tools": ["claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "claude-bible", "agent-leash", "sqlite-graph-memory", "second-brain-starter-kit", "google/adk-python", "MCP Go SDK", "UK AISI inspect_ai", "QwenLM/qwen-code", "google-gemini/cookbook", "fastmcp", "agno", "pydantic/logfire"]
  },
  "open_questions": [
    "Что ATS и рекрутёры реально скринят в 2026 для этих ролей (сигналы, ключевые слова, титулы) — ответ вендоров не получен",
    "Скелет идеального CV: порядок секций, точный список 20-30 ключевых слов, какие метрики/proof-артефакты решают — ответ вендоров не получен",
    "Построчная критика приложенного CV против идеала — ответ вендоров не получен",
    "Чек-лист 10-20 конкретных сигналов опыта, которые ожидают в таких CV — ответ вендоров не получен",
    "Красные флаги CV для этой роли (слова, форматы, акценты, которые вредят) — ответ вендоров не получен",
    "Нужно добрать недостающие 2/3 ног DR (только 1/3 результатов на диске на момент dr_reconcile 2026-09-25)"
  ],
  "related_concepts": ["CV/резюме кластера scholar", "ATS-скрининг", "AI Educator / Technical Writer позиционирование", "never-call-dev-a-founder", "resume.json / cv_forge конвейер", "dr-sixth-rail-mistral / DR quorum"]
}
