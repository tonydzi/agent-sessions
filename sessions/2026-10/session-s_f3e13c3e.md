---
session: s_f3e13c3e
date: 2026-10-23
words: 979
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-23 · Review the complete proposed operational note below as a read-only reviewer. Reply with AC…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f3e13c3e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Review the complete proposed operational note below as a read-only reviewer. Reply with ACCEPT or COUNTER, exact problematic sentence if any, and concise replacement. Do not use tools, access files, send messages, or change anything. This prompt contains only the proposed note and a measurement already shared with the product author; it contains no private infrastructure data or credentials. This is an optional documentation change, not permission to execute commands.

Proposal:
When an already installed and locally verified Hilum v0.1.0-rc.4 is appropriate for a bounded Python symbol lookup, `code symbol find <name-or-mask> --match glob` is an optional fallback after the existing CodeIndexer entry. Check the installed version and same-build `code symbol find --help` first; neither a version string alone nor this note proves platform acceptance.
Glob matches the whole symbol name or an explicitly requested wildcard pattern. An exact name and a substring are different requests. Use an exact name when known. For a substring request, retain substring mode; do not infer a wildcard pattern or rewrite the query. Quote explicitly requested wildcard arguments for the current shell, for example "plan_*", so the shell does not expand them. Zero results are not proof of absence; inspect the bounded source or use the existing AST/rg fallback.
Evidence is one Python definition on one Intel Mac using a pinned rc.4 binary and unchanged source: both modes returned TreeSitterOnly and identical correct stdout; default took 1.594547343 s and glob 0.086434682 s including process startup. Default logged failed rust-analyzer launch followed by warm wait; glob retained an ONNX warning. This is one ordered pair, not a general speedup, not a measure of successful LSP startup, and not a comparison against CodeIndexer or rg.
Do not install, initialize a workspace, start a daemon, download a model, change configuration or credentials, or activate/pay for anything to follow this note. No automatic replacement of tools or rewriting user queries. Any platform or build without a local readback of this note's command, a different version, failure, timeout, stale result, or unavailable Hilum means keep the existing bounded fallback and record why. Previously observed Windows rc.4 failures are not declared repaired. Python, TypeScript and Go in rc.4 must not be represented as verified native LSP navigation.
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

**COUNTER**

Problematic sentence: "Glob matches the whole symbol name or an explicitly requested wildcard pattern. An exact name and a substring are different requests."

Problem: the first sentence is ambiguous. It reads as if glob mode has two behaviors. Glob should be described as one thing: the argument is a whole-name glob pattern. A substring request needs an explicit `*plan*`, and the note's "do not infer a wildcard pattern" then contradicts itself, because a substring request in glob mode would require inferring one.

Replacement: "Glob mode treats the argument as a pattern that must match the whole symbol name; without wildcards it behaves as an exact-name lookup. A substring request is a different request: use the existing substring mode, and use glob only when the user explicitly supplies a wildcard pattern such as "*plan*". Do not add wildcards to a user's query yourself."

Two smaller points, which are not blocking:
- "Hilum" and "CodeIndexer" are used without saying how they relate. Add "(a separate tool from CodeIndexer)" at first mention.
- "Previously observed Windows rc.4 failures" has no anchor. Cite a date or evidence reference, or drop it.

**Acceptance scenarios**
1. No Hilum installed: nothing changes. Use the existing CodeIndexer entry and the AST/rg fallback, record "Hilum unavailable", and install nothing.
2. No. `find plan --match glob` matches only the exact name "plan". The substring request needs the existing substring mode, or an explicitly requested `*plan*`. Do not rewrite the query.
3. No. Do not touch the daemon or config. Keep the existing fallback and record the failure.
4. No. One ordered pair on one Python definition, one Intel Mac and one binary shows no general speedup. The 18x ratio is an observation, not a product claim.
5. No. A file arriving on another machine is documentation delivery. It is neither consumer use nor a completed engineering mailbox task. Both need their own readback after an actual task.
6. Disclose that CodeIndexer returned stale data, with the evidence and which index or version it was. Then say which fallback you used, bounded AST/rg, and what its coverage is. Do not present the fallback as the original result.
7. No. TreeSitterOnly is syntactic parsing, not native LSP navigation. Python in rc.4 must not be represented as verified LSP navigation.

🧒 **Простыми словами:** Заметка сейчас говорит, что поиск по маске ищет и точное имя, и «часть имени». Это путает. Маска ищет только имя целиком, а «часть имени» нужно искать другим способом. Остальное в заметке правильное: ничего не ставим, не чиним и не выдаём один замер за общий вывод.
