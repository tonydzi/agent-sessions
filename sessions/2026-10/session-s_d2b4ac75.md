---
session: s_d2b4ac75
date: 2026-10-06
words: 695
turns: 4
tools: "ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · We need them as potential ANGEL INVESTORS (small checks) and design partners for an open-s…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d2b4ac75` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

TASK: source a list of 15-20 real, named people who are CURRENT or FORMER CISOs / VP-Security / Head-of-Security / Deputy-CISO at a notable company, AND who write PUBLICLY about AI-agent security, autonomous-agent risk, MCP (Model Context Protocol) exposure, or agent/LLM vulnerabilities.

We need them as potential ANGEL INVESTORS (small checks) and design partners for an open-source control plane for heterogeneous AI agent fleets. So prefer people who either (a) are known to angel-invest / advise startups, or (b) are loud public writers on this exact pain.

HARD REQUIREMENTS for every row — a row without these is worthless to us:
1. Full name.
2. Security title + company (say clearly if FORMER and when).
3. EVIDENCE URL — a specific, real, working public page that shows BOTH that the person is who you say AND that this is genuinely their topic. Acceptable: their personal blog post, their Substack, a GitHub issue/repo they authored, a Hacker News comment thread, a conference talk page, a podcast episode page, a company engineering blog post under their byline, a Luma event where they speak. Deep link to the actual item, NOT a homepage.
4. DOOR — a concrete, usable way to reach them that is NOT LinkedIn: personal site contact page, public email, GitHub handle, X/Twitter handle, Substack (reply/DM), Hacker News username, Bluesky, Mastodon, their podcast/newsletter contact.
5. One line: what EXACTLY is their stated pain or public position about agents (quote or close paraphrase).

ABSOLUTE RULES:
- LinkedIn is BANNED as evidence or door. Do not output a single linkedin.com URL.
- DO NOT INVENT. If you are not confident a URL is real and live, write "UNVERIFIED" next to it instead of guessing. A short list of real people beats a long list of plausible fabrications. We will machine-check every URL and discard fabrications, and a fabricated row costs us more than a missing row.
- No generic famous-CISO names with no agent-security writing (e.g. do not pad with people who only talk about compliance).
- Diversity of door types is good (some GitHub-first, some Substack-first, some HN-first).

OUTPUT FORMAT: one block per person, plain text, fields labelled NAME / TITLE / EVIDENCE / DOOR / PAIN / ANGEL (yes-known-angel / advisor / unknown). Nothing else, no preamble.

---

**Claude:**

I'll research this using live web search to verify each person, title, and URL — fabricating any of this would be worse than a shorter list.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 5}

---

**Claude:**

I'll search for real candidates — security leaders (CISO/VP-Security/Head-of-Security) who publicly write about AI agent security, MCP, or LLM vulnerabilities — and verify each with live URLs.

---

> `WebSearch` -- {"query": "Diana Kelley CISO Protect AI blog LLM security agent"}

---

> `WebSearch` -- {"query": "Caleb Sima former CISO Robinhood AI agent security Cloud Security Alliance"}

---

> `WebSearch` -- {"query": "Chris Hughes CISO Aquia AI security blog substack"}

---

> `WebSearch` -- {"query": "Rick Doten CISO Centene AI security podcast agent"}

---

> `WebSearch` -- {"query": "Johann Rehberger embracethered MCP prompt injection AI agent security title"}

---

> `WebSearch` -- {"query": "\"Deputy CISO\" OR \"VP Security\" writes about \"MCP\" \"Model Context Protocol\" vulnerability blog"}

---

> `WebSearch` -- {"query": "Kayne McGladrey Field CISO AI agent security blog angel investor"}

---

> `WebSearch` -- {"query": "CISO angel investor AI agent security startup advisor 2026"}

---

> `WebSearch` -- {"query": "Diana Kelley CISO Protect AI LLM security"}

---

**Claude:**

I don't have web search permission enabled in this session, so I can't live-verify URLs — and the task explicitly bans inventing or guessing them. Rather than fabricate a list that would fail your machine-check, I need one of two things from you:

1. **Grant WebSearch/WebFetch permission** for this session (if your permission mode allows a prompt, try re-triggering it), or
2. **Let me delegate to an Agent** (subagent) that may have independent tool access — I can try that route now if you'd like.

Which do you want? I'd rather pause here than hand you a list where I can't stand behind the URLs — a fabricated row costs you more than a missing one, per your own requirement.
