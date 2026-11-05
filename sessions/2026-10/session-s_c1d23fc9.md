---
session: s_c1d23fc9
date: 2026-10-05
words: 633
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-05 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c1d23fc9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-03-HUB-01-0323
REGISTRY TOPIC: bb Harness versus Hermes Agent and OpenClaw: shared workspace and personal agent selection (через dr_start; ПОТРЕБИТЕЛЬ: dev chooses daily harness with shared workspace, shared skills and existing subscriptions) (dr_reconcile 2026-10-04: на диске 2/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-03-HUB-01-0323\results)

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


===== VENDOR: report (DR26-10-03-HUB-01-0323.md) =====
---
id: DR26-10-03-HUB-01-0323
date: 2026-10-03 03:23:33
theme: bb Harness versus Hermes Agent and OpenClaw: shared workspace and personal agent selection
session_id: s_aaa6e38d
machine: HUB-01
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-03-HUB-01-0323 — bb Harness versus Hermes Agent and OpenClaw: shared workspace and personal agent selection

Compare get-bb/bb (getbb.app) versus NousResearch/hermes-agent and OpenClaw (openclaw/openclaw), with OpenCode, Pi, Claude Code/Codex/Cursor and OpenHands as category controls. Decision: a Windows user with WSL, existing vendor subscriptions, a shared workspace with multiple agents, and a shared library of SKILL.md files wants the fastest reliable daily cockpit without accidental deletions or duplicated memory/config. Use live web research and primary official docs/source/release notes, date-stamp claims. Distinguish IDE multi-harness orchestration from autonomous personal assistant, messaging gateway, runtime and framework. Compare Windows support, real subscription authentication vs API billing, skill portability and parsing, MCP/connectors, memory, background schedules, multiagent and multimachine, workspace permissions/approval/sandbox, backup/resume, licensing, maintenance risks and lock-in. Do not infer features from stars or marketing. Cite at least 8 direct primary URLs with concrete evidence, explain contradictory docs and unknowns. Give the strongest argument against your preferred choice, migration cost, a 7-day non-destructive acceptance test, and recommendation for primary plus optional companion rather than installing everything. Do not access local private files or secrets or run shell commands; web research only. Return a substantial Russian report with an evidence matrix and verdict. Current evaluation date 2026-10-03; label source dates and do not fabricate newer versions.

---

**Claude:**

```json
{
  "lang": "mixed",
  "topic": "bb Harness vs Hermes Agent vs OpenClaw: выбор ежедневного харнесса с общим workspace и скиллами",
  "one_line": "Какой харнесс (get-bb/bb, Hermes Agent, OpenClaw — с OpenCode, Pi, Claude Code/Codex/Cursor, OpenHands как контроль) лучше всего подходит Windows-пользователю с WSL, существующими подписками, общим workspace нескольких агентов и общей библиотекой SKILL.md.",
  "key_findings": [],
  "recommendations": [],
  "entities": {
    "people": [],
    "companies": ["NousResearch"],
    "products_tools": ["bb (getbb.app)", "Hermes Agent", "OpenClaw", "OpenCode", "Pi", "Claude Code", "Codex", "Cursor", "OpenHands"]
  },
  "open_questions": [
    "В доступном тексте ДР присутствует только бриф/промпт задания (theme, targets, критерии сравнения), а не сами ответы вендоров — сравнительная evidence-матрица и вердикт не сохранились в этой секции отчёта",
    "По dr_reconcile на диске обнаружено только 2 из 6 ног (chatgpt, gemini, grok, claudeai, glm, mistral) — выводы по Windows-поддержке, реальной аутентификации подписки vs API-биллинга, портируемости скиллов, MCP/коннекторам, памяти, фоновым расписаниям, мультиагентности, правам/approval/sandbox, бэкапу/resume, лицензированию и lock-in не подтверждены текстом",
    "Не найден контраргумент против предпочтённого выбора, стоимость миграции и 7-дневный неразрушающий acceptance-тест, которые требовались по заданию"
  ],
  "related_concepts": [
    "coding-agent-harness-comparison",
    "shared-workspace-multi-agent",
    "skill-md-portability",
    "subscription-vs-api-billing",
    "mcp-connectors"
  ]
}
```
