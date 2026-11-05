---
session: s_3923cc2b
date: 2026-10-23
words: 985
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-23 · Review the complete proposed operational note below as a read-only reviewer. Reply with AC…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3923cc2b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Review the complete proposed operational note below as a read-only reviewer. Reply with ACCEPT or COUNTER, exact problematic sentence if any, and concise replacement. Do not use tools, access files, send messages, or change anything. This prompt contains only the proposed note and a measurement already shared with the product author; it contains no private infrastructure data or credentials. This is an optional documentation change, not permission to execute commands.

Proposal:
When an already installed and locally verified Hilum v0.1.0-rc.4 is appropriate for a bounded Python symbol lookup, `code symbol find <name-or-mask> --match glob` is an optional fallback after the existing CodeIndexer entry. Check the installed version and same-build `code symbol find --help` first; neither a version string alone nor this note proves platform acceptance.
Glob matches the whole symbol name or an explicit wildcard pattern. An exact name and a substring are different requests. Use an exact name when known. For a substring request, choose an explicit pattern only if it preserves the user's intent, or retain substring mode. Quote wildcard arguments for the current shell, for example "plan_*", so the shell does not expand them. Zero results are not proof of absence; inspect the bounded source or use the existing AST/rg fallback.
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

**Problematic sentence:** "Glob matches the whole symbol name or an explicit wildcard pattern. An exact name and a substring are different requests."

Problem: it is correct, but the note never says what to do when the user's intent is a substring and the agent can't confirm that a wildcard preserves it. "Choose an explicit pattern only if it preserves the user's intent, or retain substring mode" leaves a loophole. `*plan*` is not equivalent to a substring search if the tool's glob treats `_` or `.` specially, is case-sensitive, or matches a different scope.

**Replacement:** "Glob matches the whole symbol name or an explicit wildcard pattern. An exact name and a substring are different requests. For a substring request, use `*plan*` only after a readback of the same build shows it returns the same set as substring mode on that input. Otherwise keep substring mode and do not rewrite the user's query."

Also minor: "Previously observed Windows rc.4 failures are not declared repaired" is fine. The evidence paragraph says "identical correct stdout" but does not name the source anchor or hash. This is acceptable for a one-pair measurement, because the note itself requires the anchor and hash in later task evidence.

**Acceptance scenarios**

1. No Hilum installed: nothing happens. Keep the existing CodeIndexer/AST/rg path, record "Hilum unavailable", and do not install it.
2. No. `find plan --match glob` matches only the exact name `plan`. A substring request needs `"*plan*"` (verified against substring mode) or substring mode itself.
3. No. Don't change the daemon, config or credentials. Keep the existing fallback, record the failure, and don't call it repaired.
4. No. One ordered pair (1.59 s vs 0.086 s, about 18x) on one Python definition, one Intel Mac and one binary shows no general speedup. It also includes warm-up and logging differences and has no CodeIndexer/rg baseline.
5. No. A file arriving is delivery, not use. Consumer use needs a natural task with the evidence fields recorded, and the observation message is not an engineering mailbox task.
6. Disclose that CodeIndexer returned stale data, with its source and age if known, and say that the fallback result is bounded. Don't present the fallback as a fresh full answer.
7. No. TreeSitterOnly is syntactic tree-sitter navigation, not native Python LSP. The note must not describe it as verified LSP navigation.

🧒 **Простыми словами:** Заметка почти хороша. Я бы поправил одно: «слово внутри имени» и «точное имя» ищутся по-разному. Звёздочки вокруг слова нельзя ставить на веру, их нужно сначала сверить с обычным режимом. Быстрее в 18 раз пока не доказано: мерили один раз на одном компьютере.
