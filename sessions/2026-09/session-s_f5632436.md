---
session: s_f5632436
date: 2026-09-27
words: 1828
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f5632436` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-26-MACANTON-01-1441
REGISTRY TOPIC: Все оплачиваемые двери в frontier AI research/security для сеньора по безопасности без ML-research: фелоушипы, FT-роли, гранты, конкурсы, компании из пяти направлений капитала — с датами интейков (через dr_start; ПОТРЕБИТЕЛЬ: решение оператора, куда ещё подаваться помимо Anthropic Fellows (его слова 25.09: «податься не только сюда, а на все альтернативные места»); календарь интейков на 12 месяцев) (dr_reconcile 2026-09-27: на диске 3/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-26-MACANTON-01-1441\results)

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


===== VENDOR: report (DR26-09-26-MACANTON-01-1441-glm.md) =====
GLM-5.3-Flash
Sign in
---
id: DR26-09-26-MACANTON-01-1441
date: 2026-09-26 14:41:26
theme: Все оплачиваемые двери в frontier AI research/security для сеньора по безопасности без ML-research: фелоушипы, FT-роли, гранты, конкурсы, компании из пяти направлений капитала — с датами интейков
session_id: unknown
machine: NODE-0X
targets: claudeai,gemini,chatgpt,glm,grok,mistral
---

# DR26-09-26-MACANTON-01-1441 — Все оплачиваемые двери в frontier AI research/security для сеньора по безопасности без ML-research: фелоушипы, FT-роли, гранты, конкурсы, компании из пяти направлений капитала — с датами интейков

# Deep Research request — every paid door into frontier AI research/security work for a senior security engineer with no ML-research record (Q4 2026 / 2027 intakes)

Run this as a full Deep Research / extended-research task. Open sources. Cite ONLY URLs you actually opened. Mark anything from an aggregator as UNVERIFIED. List the queries you ran. Finish with a verification pass over your own claims.

## Candidate (fixed facts — do not re-research, do not re-characterise)
[ИМЯ] [ФАМИЛИЯ]. Twenty years engineering plus hired operating-executive roles (COO/CTO — he is an employee, NOT an owner/founder; never use the word founder about him, never call him non-technical). MSc Computer & Information Systems Security (MEPhI, cryptography). Production work: crypto-exchange backends, market-maker engines, high-frequency trading systems; smart contracts at Everex 2017-18; audited and incubated many smart-contract teams — in smart contracts a defect costs money directly, so his security instincts come from a domain with immediate financial consequence. Python daily, C++ from exchange work. Runs a production multi-machine Claude agent fleet in public. Since Jul 2026: 45 merged pull requests into other people's repositories incl. UK AISI `inspect_ai` (#4769, strict-majority reducer for grader panels), MCP Go SDK, fastmcp, agno, qwen-code, marm-memory; 62 issues with reproductions; 21 third-party release-note credits; evidence page github.com/tonydzi/github-evidence. PhD in Education (Information Technologies); h-index 7, non-ML field. NO model-training, fine-tuning or RL experience, NO ML publications, NO CVEs or bug bounties yet. US O-1 active (petitioned by his own company; contracting through it is the standard arrangement), EU/Polish citizen, based Palo Alto CA, ready to relocate, ready for a paid work trial.

Already applied: Anthropic Fellows Program (Jan-2027 cohort, AI Security & Frontier Red Team stream) — do NOT re-research that program, it is covered.

## The question
**Enumerate EVERY other paid door into frontier AI research, safety, security or evaluation work that this profile can realistically enter in the next 12 months — and for each one give the intake mechanics, the deadline, and the honest odds.**

## Required coverage
1. **Fellowships, residencies and funded programmes** beyond Anthropic Fellows: MATS (all streams and the Residency), Constellation (Astra, Visiting Fellowship, Generator Residency, Incubator), Redwood Research, METR, Apollo Research, UK AI Security Institute (AISI) — including its own fellowships/secondments, EU AI Office, ARC Prize / Ndea, Open Philanthropy / Longview career-transition funding, LASR Labs, Pivotal Research, PIBBSS, GovAI, FAR AI, Timaeus, SPAR, AI Futures Project, Goodfire, Transluce, EleutherAI, AI2 / Ai2 Incubator, Cohere Labs (ex-For AI), Hugging Face fellows, Mistral programmes, Tokyo/Singapore/Seoul-based AI-safety programmes, and anything comparable you find that I have not named. For each: is the intake OPEN right now, when does it close, cohort size, stipend, location/work-authorisation requirement, whether a PhD or prior ML research is required, and the documented conversion-to-hire rate if any.
2. **Direct full-time doors that explicitly do NOT require ML research**: Research Engineer in evals/agents/safety-infrastructure, Member of Technical Staff (non-research track), Technical Program Manager (Research), Security Labs / Trusted Computing / Frontier Red Team engineering, AI security research at Apollo/METR/Redwood, and the same roles at second-tier-but-serious labs (Cohere, Mistral, AI2, EleutherAI, Goodfire, Transluce, Conjecture, Aligned AI). Give live posting URLs, the literal requirement lines, and salary bands where published.
3. **Doors that reward exactly his background**: smart-contract and exchange security. Who is hiring for AI × security-of-code, AI × smart-contract auditing, AI × exploit evaluation? Include Anthropic Frontier Red Team's own published agenda, OpenAI's security/trusted-computing roles, Google DeepMind security, plus security-first firms now building AI-agent evals (Trail of Bits, Zellic, Spearbit, Cantina, Code4rena, Immunefi, Sherlock) and any AI-native security startups funded in 2026. Explicitly: which of these treat "audited smart contracts where a bug costs money" as a credential rather than a detour?
4. **The money-follows path**: companies that raised in 2026 in the five destinations where the leading AI figures put personal money — (a) energy for data centres, (b) memory and compute rental, (c) world models and robotics, (d) star labs with no product, (e) AI-for-biology. For each destination name 5-10 funded companies with a 2026 round, and say which of them publish engineering roles that a security/infrastructure engineer could fill. Name the actual role titles they use.
5. **Grants and self-directed money**: research grants an independent person can win without institutional affiliation (Open Philanthropy, Survival and Flourishing Fund, Manifund, AI Safety Fund, Foresight, NSF SBIR-style, EU Horizon partner slots). Amounts, deadlines, whether an individual may apply.
6. **Competitions with cash and legible credentials**: ARC Prize 2026, AI cyber challenges (DARPA AIxCC successors), Kaggle/benchmark competitions in evals or security, CTFs with AI tracks, bug-bounty programmes run BY the labs themselves (Anthropic, OpenAI, Google) — what exactly do they pay for, and would a finding there count as a hiring credential?
7. **Named intake calendar.** Build one table of every dated intake in the next 12 months: programme/role, opens, closes, decision, start. Anything with a rolling intake say so explicitly.
8. **Where this profile is WASTING time.** Which of the above are closed in practice for him, and why — say it bluntly with the requirement line that excludes him.

## Output
- A single ranked table: door, type (fellowship / FT role / grant / competition), intake dates, what it demands, honest fit verdict for THIS profile (strong / plausible / closed), source URL.
- A section "what to do in the next 14 days" — only actions with a dated deadline attached.
- A section listing each claim that is UNVERIFIED or single-source.
- The exact queries you ran. 
 
Show full message
Deep Think
Max
Generated by AI. For reference only.
Tech Blog
Contact us
Terms of Service
and
Privacy Policy
Please complete security verification



Please drag the slider to complete the puzzle
CertifyId: iePUjMmdNm

---

**Claude:**

```json
{
  "lang": "mixed",
  "topic": "Оплачиваемые двери в frontier AI research/security для сеньора-безопасника без ML-research опыта",
  "one_line": "Deep-research запрос должен был перечислить все оплачиваемые фелоушипы/FT-роли/гранты/конкурсы (кроме уже поданного Anthropic Fellows) для профиля оператора с датами интейков на 12 месяцев, но представленная секция вендора GLM — это лишь эхо самого промпта-запроса.",
  "key_findings": [
    "Секция GLM не содержит результатов исследования — модель вернула только текст входного промпта и упёрлась в капчу ('Please complete security verification', слайдер-пазл), т.е. эта ветка (нога) не выполнена.",
    "dr_reconcile от 2026-09-27 подтверждает: на диске материализовалось только 3 из 6 заказанных ног, при этом реестр ошибочно показывал статус 'running' — статус выправлен постфактум.",
    "Сам запрос фиксирует профиль кандидата как неизменяемый факт: 20 лет инженерии + операционные C-level роли (COO/CTO, наёмный, не фаундер), MSc по крипто-безопасности (МИФИ), опыт бэкендов криптобирж/маркет-мейкеров/HFT, смарт-контракты в Everex 2017-18, PhD по образованию (не ML), h-index 7, без ML-публикаций/CVE/bug bounty, действующая O-1, готовность к релокации.",
    "С июля 2026 у кандидата 45 смёрженных PR в чужие репозитории (включая UK AISI inspect_ai #4769, MCP Go SDK, fastmcp, agno, qwen-code, marm-memory), 62 issue с репродукциями, 21 упоминание в release notes — это заявлено как основной актив вне ML-исследовательского трека.",
    "Anthropic Fellows Program (Jan-2027 cohort, AI Security & Frontier Red Team) уже подан и явно исключён из повторного исследования — цель была найти ВСЕ остальные двери.",
    "Запрошенное покрытие огромно и детально: MATS, Constellation (Astra/Visiting Fellowship/Generator/Incubator), Redwood Research, METR, Apollo Research, UK AISI, EU AI Office, ARC Prize/Ndea, Open Philanthropy/Longview, LASR Labs, Pivotal Research, PIBBSS, GovAI, FAR AI, Timaeus, SPAR, AI Futures Project, Goodfire, Transluce, EleutherAI, Ai2, Cohere Labs, HF fellows, Mistral, плюс FT-роли, security-фирмы (Trail of Bits, Zellic, Spearbit, Cantina, Code4rena, Immunefi, Sherlock), гранты и конкурсы (ARC Prize 2026, AIxCC-преемники, баг-баунти лабораторий) — ни по одному из этих направлений в представленном тексте ответа НЕТ фактических данных."
  ],
  "recommendations": [
    "Не использовать секцию GLM как источник фактов — она пуста по содержанию (капча заблокировала выполнение); синтез нужно строить на других 2 из 3 фактически выполненных ног (см. results-папку DR26-09-26-MACANTON-01-1441), их эта выдержка не содержит.",
    "Перед принятием решения оператора 'куда подаваться помимо Anthropic Fellows' — добрать недостающие 3 ноги (dr_latecomer_sweep / повторный dr-fanout), иначе итоговая таблица интейков будет неполной по вендорному покрытию.",
    "Зафиксировать инцидент 'GLM веб-капча блокирует автоматический DR' как класс поломки и проверить, не повторяется ли он на других DR-заказах через тот же рельс (glm)."
  ],
  "entities": {
    "people": ["[ИМЯ] [ФАМИЛИЯ]"],
    "companies": [
      "Anthropic", "MATS", "Constellation", "Redwood Research", "METR", "Apollo Research",
      "UK AI Security Institute (AISI)", "EU AI Office", "ARC Prize / Ndea", "Open Philanthropy",
      "Longview", "LASR Labs", "Pivotal Research", "PIBBSS", "GovAI", "FAR AI", "Timaeus", "SPAR",
      "AI Futures Project", "Goodfire", "Transluce", "EleutherAI", "AI2 / Ai2 Incubator",
      "Cohere Labs", "Hugging Face", "Mistral", "Trail of Bits", "Zellic", "Spearbit", "Cantina",
      "Code4rena", "Immunefi", "Sherlock", "OpenAI", "Google DeepMind", "Everex"
    ],
    "products_tools": ["inspect_ai", "MCP Go SDK", "fastmcp", "agno", "qwen-code", "marm-memory"]
  },
  "open_questions": [
    "Весь материальный вопрос (таблица дверей с датами интейков, дедлайнами, честными шансами) остаётся без ответа в этой вендорной секции — нужен доступ к результатам двух других фактически выполненных ног",
    "Не выяснено, почему GLM-рельса встретила CAPTCHA (защита от автоматизации на стороне сайта) и является ли это системным блокером для будущих DR через этот рельс",
    "Не проверено покрытие пп.2-8 запроса (FT-роли без ML, security-домены, money-follows компании 2026 года, гранты, конкурсы, календарь интейков, закрытые для профиля двери) — по факту GLM ничего из этого не исследовал"
  ],
  "related_concepts": ["dr-max-thinking-and-wide-fanout", "dr-sixth-rail-mistral", "alpha-protocol-recall-plus-dr", "anti-modesty-loud-by-default", "never-call-dev-a-founder"]
}
```
