---
session: s_4935d357
date: 2026-10-23
words: 851
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-23 · Review the complete proposed operational note below as a read-only reviewer. Reply with AC…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4935d357` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Review the complete proposed operational note below as a read-only reviewer. Reply with ACCEPT or COUNTER, exact problematic sentence if any, and concise replacement. Do not use tools, access files, send messages, or change anything. This prompt contains only the proposed note and a measurement already shared with the product author; it contains no private infrastructure data or credentials. This is an optional documentation change, not permission to execute commands.

Proposal:
When an already installed and locally verified Hilum v0.1.0-rc.4 is appropriate for a bounded Python symbol lookup, `code symbol find <name-or-mask> --match glob` is an optional fallback after the existing CodeIndexer entry. Check the installed version and same-build `code symbol find --help` first; neither a version string alone nor this note proves platform acceptance.
Glob matches the whole symbol name or an explicit wildcard pattern. An exact name and a substring are different requests. Use an exact name when known. For a substring request, choose an explicit pattern only if it preserves the user's intent, or retain substring mode. Quote wildcard arguments for the current shell, for example "plan_*", so the shell does not expand them. Zero results are not proof of absence; inspect the bounded source or use the existing AST/rg fallback.
Evidence is one Python definition on one Intel Mac using a pinned rc.4 binary and unchanged source: both modes returned TreeSitterOnly and identical correct stdout; default took 1.594547343 s and glob 0.086434682 s including process startup. Default logged failed rust-analyzer launch followed by warm wait; glob retained an ONNX warning. This is one ordered pair, not a general speedup, not a measure of successful LSP startup, and not a comparison against CodeIndexer or rg.
Do not install, initialize a workspace, start a daemon, download a model, change configuration or credentials, or activate/pay for anything to follow this note. No automatic replacement of tools or rewriting user queries. Unsupported platform, different version, failure, timeout, stale result or unavailable Hilum means keep existing bounded fallback and record why. Previously observed Windows rc.4 failures are not declared repaired. Python, TypeScript and Go in rc.4 must not be represented as verified native LSP navigation.
Record each natural use in existing task evidence: actual version/platform, input semantics, command, source anchor/hash, correctness, elapsed time if measured, limitation. Use the existing usage mechanism only after an actual task; reading the note is not product use. Documentation deployment or an observation message is not an engineering mailbox task.
Rollback: stop selecting this optional mode; retain existing channels, tools and evidence. This does not renew or expand the separate mailbox experiment. Cross-machine installation and consumer use require separate readbacks.

Also answer these acceptance scenarios in one line each:
1. An agent has no Hilum installed. What happens?
2. User asks for names containing "plan" rather than exact name "plan". Is `find plan --match glob` equivalent?
3. An existing Windows rc.4 binary fails. Should it change daemon/config to satisfy the note?
4. Does one ordered pair establish 18x product speedup?
5. A file arrived on another machine. Does that prove consumer use or a completed engineering mailbox task?
6. CodeIndexer returned stale data. What must be disclosed before a bounded fallback?
7. A Python result says TreeSitterOnly. Is this native Python LSP navigation?

---

**Claude:**

**ACCEPT**, with one non-blocking edit.

**Problem sentence:** "Unsupported platform, different version, failure, timeout, stale result or unavailable Hilum means keep existing bounded fallback and record why."

"Unsupported platform" is undefined, and the note itself says it grants no platform acceptance. The only evidence is one Intel Mac, so a reader cannot tell which platforms count as supported.

**Replacement:** "Any platform or build without a local readback of this note's command, a different version, failure, timeout, stale result, or unavailable Hilum means keep the existing bounded fallback and record why."

The rest holds up. The 18x ratio is never claimed, the single ordered pair is labelled as such, and the Windows and LSP limits are stated.

**Acceptance scenarios**
1. Nothing happens: the agent keeps the existing CodeIndexer, AST or rg path, and does not install anything.
2. No. `find plan --match glob` matches only the exact name "plan", so a substring request needs an explicit pattern such as "*plan*" or the default substring mode.
3. No. The note forbids changing the daemon, config or credentials, so the agent keeps the fallback and records the failure.
4. No. One ordered pair on one machine (1.59 s vs 0.086 s) is not a general speedup, so cache or order effects cannot be excluded.
5. No. A file arriving on another machine proves neither real consumer use nor a completed engineering mailbox task.
6. Disclose that CodeIndexer returned stale data and what was stale (index age or coverage). Also disclose that the fallback is bounded in scope and may not be complete.
7. No. TreeSitterOnly means syntax-tree lookup only, and Python in rc.4 must not be presented as verified native LSP navigation.

🧒 Простыми словами: заметка почти верная. Надо только уточнить, что значит «неподдерживаемая платформа»: это любая машина, где команду не проверили сами. Одна быстрая проба не значит, что программа стала быстрее в 18 раз.
