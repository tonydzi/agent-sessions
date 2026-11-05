---
session: s_9a027b88
date: 2026-10-28
words: 1390
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9a027b88` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-27-ZB-01-1315
REGISTRY TOPIC: Снять харнес-ограничения AI-агента легально и в облаке: модели без лишнего over-refusal, капча HITL/продукты, платёжные рельсы агентов (дельта 2025-2026 к DR26-08-02-ZB-02-2305) (через dr_start; ПОТРЕБИТЕЛЬ: оператор/Майкрофт: выбор облачных моделей + капча-рельсы + платёжные рельсы для флота на 90 дней) (dr_reconcile 2026-10-28: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-27-ZB-01-1315\results)

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


===== VENDOR: report (DR26-10-27-ZB-01-1315.md) =====
---
id: DR26-10-27-ZB-01-1315
date: 2026-10-27 13:15:36
theme: Снять харнес-ограничения AI-агента легально и в облаке: модели без лишнего over-refusal, капча HITL/продукты, платёжные рельсы агентов (дельта 2025-2026 к DR26-08-02-ZB-02-2305)
session_id: unknown
machine: NODE-0X-2023PAL
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-27-ZB-01-1315 — Снять харнес-ограничения AI-агента легально и в облаке: модели без лишнего over-refusal, капча HITL/продукты, платёжные рельсы агентов (дельта 2025-2026 к DR26-08-02-ZB-02-2305)

# Deep Research: снять харнес-ограничения у AI-агента ЛЕГАЛЬНО и в облаке (модели / капча / платежи)

CONTEXT. We run a fleet of autonomous AI agents for our own accounts and our own business. We want to remove self-imposed harness friction and move fast, but WITHOUT defeating other sites' protections and WITHOUT giving a bot unattended free rein over a payment card. Survey publicly-sold or open-source PRODUCTS and official rails. Describe capabilities, pricing, cloud-integration surface, and legal/ToS risk. Do NOT write step-by-step instructions for defeating any specific website's bot-protection. Answer in English.

SCOPE NOTE (avoid re-researching what we already know): bounded-budget agent spending via Stripe Issuing / Ramp / Deel and "policy engine outside the LLM" are already settled for us — do NOT re-litigate whether agents can have budgets. We want the 2025-2026 DELTA and concrete product specifics below.

Search the web extensively and cite ONLY URLs you actually opened. Give 15-25 primary sources, each claim with a short quote and exact URL. Prefer official docs, pricing pages, changelogs, GitHub repos dated 2025-2026. End with a "proof of work" list of queries run and pages read.

## Q1 — MODELS with less restrictive alignment, runnable IN THE CLOUD (not on our own hardware)
- Which models are known for low over-refusal on legitimate business writing / negotiation / outreach (e.g. Venice Uncensored / Dolphin-Mistral, Nous Hermes 3/4, others)? Give concrete model IDs available on OpenRouter / Together / Fireworks / Hugging Face Inference as of 2025-2026.
- For each: hosting provider(s), exact per-token price, context window, and any published refusal-rate benchmark (name the benchmark and who ran it — flag vendor-self-reported numbers).
- Cloud run options compared: OpenRouter vs Together vs Fireworks vs DeepInfra vs Hugging Face — fees, rate limits, data-retention/privacy policy, and whether they log/train on prompts.
- RISK: do less-aligned models measurably degrade on prompt-injection resistance and jailbreak-robustness? Cite any benchmark. This matters because our agents touch the web and (separately) payment rails.
- Legal/ToS: any provider terms that forbid "uncensored" use or specific content; export-control or sanctions notes for Chinese-origin models (GLM, Qwen, DeepSeek, Kimi) used via cloud.

## Q2 — CAPTCHA: legitimate handling and human-in-the-loop products (2025-2026)
- Human-in-the-loop (HITL) agent frameworks that PAUSE on a challenge and hand off to a human: Anchor Browser, Browserbase, Steel, LangGraph interrupt, Cloudflare Agents, Mastra — capabilities, pricing, how the pause/resume + live-view works, cloud API surface.
- Which agent-browser products advertise "solves CAPTCHA" and what is the LEGAL / ToS status of using them on third-party sites (reCAPTCHA/hCaptcha/Turnstile terms, CFAA/anti-bot case law 2024-2026)? Describe the risk landscape, not how-to.
- Official no-CAPTCHA paths: which common services expose an official API that removes the need to drive a UI at all (so no CAPTCHA arises)? General principle + concrete examples.

## Q3 — AGENT PAYMENTS: official rails, the 2025-2026 delta
- Visa Intelligent Commerce, Mastercard Agent Pay / Agent Pay for Machines, Google Agent Payments Protocol (AP2), OpenAI/Stripe Agentic Commerce / Order Intents: what each does, launch status, how a developer integrates from the cloud, what tokens/mandates/passkeys they use, and how the HUMAN approves (per-transaction, spend caps).
- Virtual-card APIs with hard per-transaction limits and single-merchant lock: Stripe Issuing, Privacy.com (exact API: single-use card, spend_limit, merchant lock, sandbox), Lithic, Ramp — pricing, approval requirements, which allow programmatic issuance.
- Pattern for "agent builds the cart → human confirms with one tap → card minted for exactly that amount": which products support it natively, and the fraud/prompt-injection safeguards.

DELIVERABLE: a comparison the reader can act on — for each of the three areas, a shortlist with price, cloud-integration surface, legal/ToS risk, and a one-line recommendation. Show disagreements between sources rather than averaging them.

---

**Claude:**

{"lang":"mixed","topic":"Агенты: облачные модели без over-refusal, капча HITL, платёжные рельсы (дельта 2025-2026)","one_line":"Какие облачные модели с мягким выравниванием, HITL-продукты для капчи и официальные платёжные рельсы агентов (дельта 2025-2026 к DR26-08-02-ZB-02-2305) можно легально использовать флоту на 90 дней.","key_findings":["ВНИМАНИЕ: в файле только исследовательское ТЗ (промпт), результатов и находок вендоров в нём нет. По реестру на диске 1 из 6 ног, и она содержит лишь постановку вопроса. Выводов по существу из этого текста извлечь нельзя, чтобы не выдумывать.","Зафиксированная рамка: флот автономных агентов работает на собственных аккаунтах и бизнесе. Цель: убрать самонакладываемое трение харнеса, не обходя чужую защиту сайтов и не давая боту неподконтрольный доступ к платёжной карте.","Из объёма исключено как уже решённое: бюджеты агентов через Stripe Issuing / Ramp / Deel и policy engine вне LLM. Нужна только дельта 2025-2026 и конкретика по продуктам.","Q1 в ТЗ: модели с низким over-refusal (названы Venice Uncensored / Dolphin-Mistral, Nous Hermes 3/4) на OpenRouter, Together, Fireworks, DeepInfra, Hugging Face. По каждой нужны ID, провайдер, цена за токен, контекст, бенчмарк отказов (с пометкой самоотчётных цифр), политика логов и обучения на промптах, устойчивость к prompt-injection и jailbreak, ограничения ToS и санкций/экспорта для GLM, Qwen, DeepSeek, Kimi.","Q2 в ТЗ: HITL-фреймворки с паузой на капче и передачей человеку (Anchor Browser, Browserbase, Steel, LangGraph interrupt, Cloudflare Agents, Mastra), продукты «решает капчу» и их правовой статус (reCAPTCHA/hCaptcha/Turnstile, CFAA/anti-bot прецеденты 2024-2026), официальные API, после которых капча не возникает. Инструкций по обходу защиты конкретных сайтов ТЗ запрещает.","Q3 в ТЗ: Visa Intelligent Commerce, Mastercard Agent Pay (и для машин), Google AP2, OpenAI/Stripe Agentic Commerce / Order Intents, виртуальные карты с жёсткими лимитами (Stripe Issuing, Privacy.com, Lithic, Ramp), паттерн «агент собирает корзину, человек подтверждает одним тапом, карта выпускается на точную сумму».","Требования к результату: 15-25 первичных источников с цитатой и точным URL, только реально открытые страницы; по каждой из трёх областей шорт-лист с ценой, облачной поверхностью интеграции, правовым риском и однострочной рекомендацией; расхождения между источниками показывать, а не усреднять; в конце список выполненных запросов и прочитанных страниц."],"recommendations":["Перезапустить или добрать недостающие 5 из 6 ног ДР (chatgpt, gemini, grok, claudeai, glm, mistral): на диске только постановка без ответов.","До применения выводов в флоте дождаться реального отчёта: сейчас по моделям, капче и платежам рекомендовать нечего, всё без улики.","При следующем прогоне держать в промпте запрет на пошаговый обход защит и требование цитат с URL, как в этом ТЗ."],"entities":{"people":[],"companies":["Venice","Nous Research","OpenRouter","Together","Fireworks","DeepInfra","Hugging Face","Anchor Browser","Browserbase","Steel","Cloudflare","Mastra","LangGraph","Visa","Mastercard","Google","OpenAI","Stripe","Privacy.com","Lithic","Ramp","Deel","Qwen","DeepSeek","Kimi","GLM"],"products_tools":["Venice Uncensored","Dolphin-Mistral","Nous Hermes 3/4","Visa Intelligent Commerce","Mastercard Agent Pay","Agent Pay for Machines","Google AP2 (Agent Payments Protocol)","OpenAI/Stripe Agentic Commerce","Order Intents","Stripe Issuing","Privacy.com API","reCAPTCHA","hCaptcha","Cloudflare Turnstile","LangGraph interrupt","Cloudflare Agents"]},"open_questions":["Какие конкретно модели, цены, контексты и бенчмарки отказов выдадут внешние вендоры: в файле ответов нет.","Измеримо ли ухудшается устойчивость к prompt-injection и jailbreak у менее выровненных моделей (бенчмарк не получен).","Правовой статус продуктов «решает капчу» на чужих сайтах (CFAA/ToS 2024-2026): не исследован.","Статус запуска и способ интеграции из облака для Visa/Mastercard/AP2/Agentic Commerce и точный API Privacy.com: не получены.","Какие 5 из 6 ног не отработали и почему (реестр выправлен по факту dr_reconcile 2026-10-28)."],"related_concepts":["over-refusal и менее выровненные модели","prompt-injection resistance","captcha human-in-the-loop","агентные платежи и virtual cards","policy engine вне LLM","DR26-08-02-ZB-02-2305","dr-fanout кворум 4/6","облачные рельсы моделей OpenRouter/Together"]}
