---
session: s_b443e770
date: 2026-09-25
words: 2114
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b443e770` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-HUB-19-1604
REGISTRY TOPIC: идеальное CV 2026 — Startup Ecosystem / Accelerator & Incubator Programs [кластер startup-ecosystem]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги (dr_reconcile 2026-09-25: на диске 1/3 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-24-HUB-19-1604\results)

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


===== VENDOR: report (DR26-09-24-HUB-19-1604.md) =====
---
id: DR26-09-24-HUB-19-1604
date: 2026-09-24 16:04:50
theme: идеальное CV 2026 — Startup Ecosystem / Accelerator & Incubator Programs [кластер startup-ecosystem]: скрин ATS+рекрутёров 2026, скелет идеального CV, критика нашего, чек-лист сигналов опыта, красные флаги
session_id: ats-cv-ideal-24-09@HUB-01
machine: HUB-01
prior_art: DR26-09-14-ZB-14-2009
targets: chatgpt,gemini,grok
---

# Deep Research: идеальное CV 2026 — Startup Ecosystem / Accelerator & Incubator Programs

## Задача исследователю
Ты — исследователь рынка найма. Проведи веб-исследование (2025-2026, англоязычные источники: посты рекрутёров этой ниши, hiring-гайды компаний, разборы ATS) и ответь на 5 вопросов ниже. Не выдумывай фактов о кандидате; рекомендации «стоит указать X» — законны.

## Контекст кандидата
Наёмный руководитель (COO/CTO), программист Python и C++. ЗАПРЕЩЕНО в выводах называть его «founder/фаундер» или «не-кодером». Целевые работодатели — архетипы компаний, куда идут CV этого кластера:
1. Классические акселераторы и инкубаторы (Y Combinator, Techstars, 500 Global, Plug and Play, Alchemist) — роли Program Director / Managing Director / Partner, ведущие когорты и deal flow.
2. Startup-программы внутри AI-компаний и облачных провайдеров (OpenAI / Anthropic startup programs, AWS Activate, Google for Startups, NVIDIA Inception) — Head of Startup Ecosystem / Startup Partnerships.
3. Крипто-фонды и foundations с grants/ecosystem-подразделениями (Ethereum Foundation, Solana Foundation, Polygon, экосистемные арм-ы L1/L2) — Head of Grants / Ecosystem Lead.
4. Platform-команды венчурных фондов (VC platform / portfolio success / network teams в фондах уровня a16z, Sequoia scouts-программы, региональные фонды) — Head of Platform / Platform Director.
5. Корпоративные акселераторы и innovation-программы (CVC-арм-ы, corporate accelerators крупных корпораций, программы вроде тех, что делают Foxconn/ANA с подрядчиками) — Director of Open Innovation / Corporate Accelerator Lead.
6. Университетские и государственные экосистемные программы (Stanford-стиль venture studios, EU/EIC-акселераторы, национальные инновационные агентства) — Ecosystem / Program Director.

## Текущее CV кандидата (полный текст)
```
# [ИМЯ] [ФАМИЛИЯ] — Startup Ecosystem / Accelerator & Incubator Programs

https://tonydzi.github.io/ · github.com/tonydzi · [EMAIL] · WhatsApp [ТЕЛЕФОН] · calendly.com/paloaltolab/1-on-1 · Palo Alto, CA (Silicon Valley) – Sintra, PT / US O-1 · EU citizen (Poland)

## Summary
Ten years running a startup incubator hands-on: deal flow, cohorts, founder coaching, advisor matching, fundraising — the job a partner at 500 Startups or Plug and Play does, done daily at a boutique APAC incubator with rare depth in the Japanese and Korean startup communities. 10,000+ founder calls, 2,000+ institutional-investor calls, a syndicate of 250 VCs/angels, $35M fund under management. Equally at home with AI and crypto startups: today I run an AI-native research lab on a production multi-machine Claude fleet (6 machines), operated in public: consensus, CRM, persistent memory, 100+ automation routines; before that, a portfolio that was ~70% crypto. Looking to run or grow a startup program — accelerator, incubator, foundation grants/ecosystem arm, or a startups team inside an AI or crypto company. US O-1 visa (active) + EU citizen (Polish passport) — authorized to work in the US and anywhere in the EU immediately, no visa sponsorship required; open to relocation (SF Bay Area base network) or remote

## Skills
Python, C++, accelerator, incubator, startup program, ecosystem, cohort, demo day, founder coaching, deal flow, venture, grants, foundation, startup partnerships, AI startups, crypto startups

## Experience

**COO / CTO (hired executive) — Platinum Software Development Company / Platinum VC & Incubator** (2015 – Present)

Hired operating executive (COO/CTO) who ran a startup incubator + software house in APAC since 2015 (11 years), alongside Japanese partner Tetsuji Nagata (Grand Corp; 12 years at Bloomberg before that). Portfolio ~70% crypto / 30% other, AI startups included.

- Ran cohorts end-to-end: sourced and recruited founders, coached them through product and fundraising, matched advisors, ran demo-day-style investor introductions
- In fundraising since 2017: $35M fund under management, syndicate of 250 VCs/angels; helped portfolio startups raise end-to-end — deck, investor intros, term negotiation
- Built a deal-flow machine: 10,000+ founder calls and 2,000+ institutional-investor calls; qualified, enriched founder and investor bases across the US, Japan, Korea, China, Australia and Europe
- Superconnector as a system: founders, builders, engineers and investors matched daily — and every repeatable connector motion (enrichment, matching, follow-up) automated, first with a self-built CRM, today with AI agents
- Enterprise advisory for subsidiaries of Foxconn and ANA Airlines — the corporate side of startup partnerships: pilots, procurement, innovation programs

**Operating Lead — Palo Alto AI Research Lab** (2023 – Present)

Independent lab started in 2023 in Palo Alto, CA; grew a community of 500+ AI practitioners, including Stanford researchers and big-tech engineers. Production multi-machine Claude fleet run in public: claw-consensus (reproducible multi-machine agent consensus, offline demo, published evals, FAILURE-MODES.md), verbatim-citation-gate (zero-token gate + burden-of-proof judge that catches fabricated RAG citations, MIT), agent-control-plane-casebook (reproducible control-plane failures from the production fleet — each case ships a deterministic repro, a runnable red test and an upstream bug report), the operating manual written day by day (相棒 AIBŌ · The Partner).

- Community building and founder support are the same muscle as accelerator work: a 500+ member community of AI practitioners, including Stanford researchers and big-tech engineers

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
1. Что ATS и рекрутёры ЭТОГО типа ролей (accelerator/incubator program leadership, startup ecosystem, VC platform, grants/ecosystem у foundations) реально скринят в 2026: сигналы, ключевые слова, титулы. С источниками.
2. Скелет идеального CV для этой роли: порядок секций, идеальный титул, ТОЧНЫЙ список из 20-30 ключевых слов/фраз, какие метрики и proof-артефакты решают (например: число когорт, portfolio outcomes, follow-on funding rate, размер сети, NPS фаундеров).
3. Жёсткая критика приложенного CV против этого идеала: что убрать, что переставить, чего не хватает. Построчно по секциям.
4. Чек-лист «кандидат должен указать: …» — 10-20 конкретных сигналов опыта, которые в таких CV ждут (кандидат сам вспомнит, есть ли у него такой факт). Примеры класса сигналов: selection rate когорт, alumni-выходы, партнёрства с корпорациями, mentor-сеть, судейство демо-дней, LP-отношения.
5. Красные флаги: что в CV для этой роли ВРЕДИТ (слова, форматы, акценты).

## Формат ответа
Русский, markdown, секции по 5 вопросам, ключевые слова списком через запятую, источники ссылками в конце.

---

**Claude:**

```json
{
 "lang": "ru",
 "topic": "Идеальное CV 2026 для ролей Startup Ecosystem / Accelerator & Incubator Programs",
 "one_line": "ДР должен был выяснить, что ATS и рекрутёры реально скринят в 2026 для ролей уровня Program Director/Head of Ecosystem/Platform (акселераторы, VC platform, foundation grants, corporate innovation) и как перестроить CV оператора под этот идеал — но по факту на диске оказалась только 1/3 запрошенных ног (chatgpt/gemini/grok), остальные ответы отсутствуют.",
 "key_findings": [
  "Файл содержит только постановку задачи (промпт + текущее CV кандидата) для трёх LLM (chatgpt, gemini, grok) — фактических ответов исследователей в теле документа нет",
  "dr_reconcile 2026-09-25 зафиксировал расхождение: в реестре статус стоял 'issued', на диске присутствует лишь 1/3 ног — статус выправлен по факту, ДР фактически не закрыт",
  "Целевые архитипы работодателей для CV этого кластера заданы явно: классические акселераторы/инкубаторы (YC, Techstars, 500 Global, Plug and Play, Alchemist), startup-программы AI/облачных компаний (OpenAI/Anthropic, AWS Activate, Google for Startups, NVIDIA Inception), крипто-фонды/foundations (Ethereum Foundation, Solana Foundation, Polygon), platform-команды VC (a16z, Sequoia), корпоративные акселераторы (CVC, Foxconn/ANA-подрядчики), университетские/госпрограммы (Stanford venture studios, EU/EIC)",
  "Жёсткое ограничение на позиционирование кандидата: запрещено называть его 'founder/фаундер' или 'не-кодером' — он наёмный COO/CTO, программист Python и C++",
  "Текущее CV кандидата уже содержит количественные proof-точки: 10 000+ звонков с фаундерами, 2000+ звонков с институциональными инвесторами, синдикат 250 VC/ангелов, $35M под управлением, 500+ участников AI-лаборатории, 169k подписчиков TG-канала, 115 публичных репозиториев, h-index 7, 137 цитирований",
  "В CV уже заявлена мультидоменность (AI + крипто ~70% портфеля) и enterprise-advisory для дочерних структур Foxconn и ANA Airlines как пример 'corporate side of startup partnerships'"
 ],
 "recommendations": [
  "Дособрать оставшиеся 2/3 ног DR (минимум ещё gemini/grok или повторно chatgpt) прежде чем делать выводы по 5 вопросам — сейчас нет материала для скелета CV, критики и чек-листа сигналов",
  "После получения полных ответов — сверить формулировки со списком ключевых слов/титулов для ролей Program Director / Head of Startup Ecosystem / Platform Director, не выдумывая их самостоятельно",
  "Зафиксировать в реестре DR корректный статус (не 'issued') до тех пор, пока все 3 ноги не лягут на диск, чтобы избежать повторного false-positive при следующей сверке"
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]", "Tetsuji Nagata"],
  "companies": ["Platinum Software Development Company / Platinum VC & Incubator", "Everex", "Merlion", "Foxconn", "ANA Airlines", "Y Combinator", "Techstars", "500 Global", "Plug and Play", "Alchemist", "OpenAI", "Anthropic", "AWS Activate", "Google for Startups", "NVIDIA Inception", "Ethereum Foundation", "Solana Foundation", "Polygon", "a16z", "Sequoia"],
  "products_tools": ["claw-consensus", "verbatim-citation-gate", "agent-control-plane-casebook", "claude-bible", "agent-leash", "sqlite-graph-memory", "second-brain-starter-kit", "headroom"]
 },
 "open_questions": [
  "Что ATS и рекрутёры этих ролей реально скринят в 2026 (сигналы, ключевые слова, титулы) — не отвечено, ответы вендоров отсутствуют на диске",
  "Скелет идеального CV: порядок секций, точный список 20-30 ключевых слов, какие метрики/proof решают — не отвечено",
  "Построчная критика текущего CV против идеала — не отвечено",
  "Чек-лист «кандидат должен указать» (10-20 сигналов опыта) — не отвечено",
  "Красные флаги для CV этого типа роли — не отвечено",
  "Почему в реестре стоял статус 'issued' при 1/3 ног на диске — механизм рассинхронизации не выяснен"
 ],
 "related_concepts": ["idealnoe-cv-2026", "ats-screening-2026", "startup-ecosystem-roles", "cv-cluster-accelerator-incubator", "dr-quorum-and-reconcile"]
}
```
