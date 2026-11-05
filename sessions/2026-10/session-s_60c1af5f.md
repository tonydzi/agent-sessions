---
session: s_60c1af5f
date: 2026-10-04
words: 889
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-04 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_60c1af5f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-02-ZB-02-1136
REGISTRY TOPIC: Какая LLM лучше пишет короткие дерзкие X-посты (pain of the day, 200-280 зн): Grok vs GPT vs Claude vs Gemini и как это честно замерить (через dr_start; ПОТРЕБИТЕЛЬ: решение: какую рельсу ставить генератором/критиком EN-тизеров в /x-post и /social-daily (приказ dev 02.10.2026, голосом)) (dr_reconcile 2026-10-04: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-02-ZB-02-1136\results)

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


===== VENDOR: report (DR26-10-02-ZB-02-1136.md) =====
---
id: DR26-10-02-ZB-02-1136
date: 2026-10-02 11:36:43
theme: Какая LLM лучше пишет короткие дерзкие X-посты (pain of the day, 200-280 зн): Grok vs GPT vs Claude vs Gemini и как это честно замерить
session_id: NODE-0X-x-posts-20261002
machine: NODE-0X-2023PAL
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-02-ZB-02-1136 — Какая LLM лучше пишет короткие дерзкие X-посты (pain of the day, 200-280 зн): Grok vs GPT vs Claude vs Gemini и как это честно замерить

# Deep Research request: which LLM writes the best SHORT, punchy X (Twitter) posts in 2026?

Context. I run a small AI lab and post on X daily in English. The format I need is NOT longreads and NOT threads: single posts of 200-280 characters, "pain of the day" style: one concrete failure or frustration from real work, stated bluntly, first person, dry irony, no hashtags, no emoji bullets, no AI-sounding phrases (no "delve", "game-changer", no em dashes). Peer-to-peer engineer tone. The hypothesis I want tested: Grok writes the best tweets because xAI trained on X data. I do not want flattery, I want evidence.

Questions.
1. Published comparisons (2025-2026) of LLMs on short social copy: Grok 4/5, GPT-5.x, Claude 4.x/5, Gemini 2.5/3, DeepSeek, Qwen, Mistral, Llama. Blind tests, human-preference panels, creative-writing arenas (LMArena creative/writing categories, EQ-Bench creative writing, any "tweet" or "headline" specific evals). Cite sources with dates.
2. Is there any evidence that training on X data (Grok) translates into better SHORT post quality, or is it folklore? What do xAI, independent reviewers and heavy X users report?
3. Failure modes per model for short copy: which ones over-explain, which add hashtags/emoji by default, which produce "AI slop" markers, which keep character limits reliably.
4. Prompting recipes that measurably improve short punchy posts (few-shot with the author's own tweets, constraints on length, "write 10 pick 1", critique-then-rewrite, temperature, system prompts used by known tools like Typefully/Hypefury/Taplio AI).
5. How to run a fair in-house blind test: sample size, judges (human vs LLM-as-judge and its bias toward its own outputs), metrics beyond likes (replies, bookmarks, dwell), how many posts per model to reach a usable signal at a small account (<2k followers).
6. Final verdict table: model, strength for short punchy posts, weaknesses, recommended use (draft / critique / rewrite), confidence level.

Output. Structured report, English, with a one-paragraph BLUF at the top, a comparison table, and a ranked recommendation for a "pain of the day" post generator. Mark every claim as sourced or inferred. No marketing language.

---

> `Bash` -- {"command": "echo done"}

---

**Claude:**

```json
{
 "lang": "mixed",
 "topic": "Какая LLM лучше пишет короткие дерзкие X-посты (200-280 зн) и как это честно замерить",
 "one_line": "Запрос на deep-research, тестирующий гипотезу, что Grok пишет лучшие короткие твиты (т.к. xAI тренирует на X-данных), против GPT, Claude и Gemini, с требованием источников и честной методики блайнд-теста.",
 "key_findings": [],
 "recommendations": [],
 "entities": {
  "people": [],
  "companies": ["xAI", "OpenAI", "Anthropic", "Google", "DeepSeek", "Qwen", "Mistral", "Meta (Llama)"],
  "products_tools": ["Grok 4/5", "GPT-5.x", "Claude 4.x/5", "Gemini 2.5/3", "LMArena", "EQ-Bench", "Typefully", "Hypefury", "Taplio AI"]
 },
 "open_questions": [
  "Собранный документ содержит только исходный запрос (бриф) для deep research, а не фактические ответы/находки вендоров — сами выводы (сравнительная таблица, рейтинг, verdict) в теле отчёта отсутствуют и требуют дозагрузки результата",
  "Есть ли опубликованные блайнд-тесты/панели предпочтений людей по коротким соцпостам для Grok/GPT/Claude/Gemini с датами и источниками — не подтверждено в этом фрагменте",
  "Переводится ли тренировка Grok на X-данных в реально лучшее качество коротких постов, или это фольклор — не подтверждено в этом фрагменте",
  "Какие конкретные failure modes (over-explaining, авто-хэштеги/эмодзи, AI-slop маркеры, соблюдение лимита символов) характерны для каждой модели — не подтверждено в этом фрагменте",
  "Какие промпт-рецепты (few-shot на своих твитах, '10 вариантов — выбери 1', critique-then-rewrite, температура) измеримо улучшают короткие посты — не подтверждено в этом фрагменте",
  "Как just-in-house честно замерить на маленьком аккаунте (<2k подписчиков): размер выборки, судьи (люди vs LLM-as-judge с его bias), метрики кроме лайков — не подтверждено в этом фрагменте"
 ],
 "related_concepts": ["x-post", "social-daily", "model-routing", "ai-slop", "LLM-as-judge bias", "alpha-protocol-recall-plus-dr"]
}
```
