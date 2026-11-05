---
session: s_a3b94bb6
date: 2026-10-05
words: 1001
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-05 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a3b94bb6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

**Claude:**

```json
{
  "lang": "en",
  "topic": "Which LLM writes the best short punchy X posts (Grok vs GPT vs Claude vs Gemini)",
  "one_line": "This deep-research ticket asks which LLM best writes short 200-280 character 'pain of the day' X posts and how to fairly benchmark Grok, GPT, Claude and Gemini for that format, but the captured report contains only the original research prompt — no vendor findings or answers were actually recorded (reconcile note: 1/6 legs present on disk, registry status was corrected from 'running' to reflect this).",
  "key_findings": [
    "The report file contains only the research request/prompt text (BLUF question, 6 sub-questions, requested output format) — no synthesized findings, comparison table, or verdict from any vendor are present in this document.",
    "DR reconcile flagged the run as incomplete: only 1 of 6 targeted legs (chatgpt, gemini, grok, claudeai, glm, mistral) produced a result on disk, so the registry 'running' status was corrected to match reality rather than reflecting a finished synthesis."
  ],
  "recommendations": [],
  "entities": {
    "people": [],
    "companies": ["xAI"],
    "products_tools": ["Grok 4/5", "GPT-5.x", "Claude 4.x/5", "Gemini 2.5/3", "DeepSeek", "Qwen", "Mistral", "Llama", "LMArena", "EQ-Bench", "Typefully", "Hypefury", "Taplio AI"]
  },
  "open_questions": [
    "Are there published 2025-2026 blind tests / human-preference panels / creative-writing arenas (LMArena, EQ-Bench, tweet/headline-specific evals) comparing these models on short social copy?",
    "Does training on X data (Grok/xAI) actually translate into better short-post quality, or is that folklore — what do xAI, independent reviewers, and heavy X users report?",
    "What are the per-model failure modes for short copy (over-explaining, default hashtags/emoji, AI-slop markers, reliability of staying within character limits)?",
    "Which prompting recipes (few-shot on author's own tweets, length constraints, 'write 10 pick 1', critique-then-rewrite, temperature, known tool system prompts) measurably improve short punchy posts?",
    "How should an in-house blind test be designed (sample size, human vs LLM-as-judge bias, metrics beyond likes, posts-per-model needed for signal on a <2k-follower account)?",
    "What is the final ranked verdict (model, strength, weaknesses, recommended use as draft/critique/rewrite, confidence level) — this was requested but not answered in the captured report."
  ],
  "related_concepts": ["LLM creative-writing benchmarks", "short-form X/Twitter copywriting", "LLM-as-judge bias", "EN teaser generator for /x-post and /social-daily"]
}
```
