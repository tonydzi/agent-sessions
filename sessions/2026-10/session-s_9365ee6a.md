---
session: s_9365ee6a
date: 2026-10-29
words: 325
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9365ee6a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Classify this Claude Code session as HUMAN or SERVICE by its CONTENT.
HUMAN = a real person (dev/colleague) actively typing: natural questions, instructions in their own words, back-and-forth, corrections. Title may look technical -- judge by whether a human is conversing.
SERVICE = automated/headless run with NO human conversing: first message is a skill loader ('Base directory for this skill: ...'), a scheduled routine that runs itself and reports (digest/sync/export), an inbox-robot/machine-bus handoff, or only templated prompts + tool results.
Answer with EXACTLY ONE WORD: SERVICE or HUMAN.

=== SESSION EXCERPT ===
### dev

You are an agent with the following skill shelf. Each line is `name: description`.
A user types a phrase. Decide which ONE skill you would invoke.
Answer ONLY with lines of the form `<n>: <skill-name> | <the phrase repeated>` (name exactly
as in the shelf, no slash). If no skill fits, answer `<n>: NONE | <the phrase repeated>`.
Repeating the phrase after `|` is mandatory: it keeps numbering aligned.

SHELF:
3q: 
qqq: 
adapt-post-to-channels: 
adopt-external-idea: 
after-call: 
ai-disclosure-joke: 
amplify-framing: 
analyze-job-compensation: 
answer-github-issues: 
apple-photos: 
apply-to-jobs: 
article-to-markdown: 
ask-any-llm: 
ask-vault: 
audit-approval-asks: 
audit-content: 
batch-overnight-work: 
book-lead-call: 
business-sparring: 
call-prep: 
challenge-beliefs: 
change-screen-resolution: 
check-mcp-connectors: 
check-memory-health: 
choose-browser: 
chrome-fix: 
claude-repair: 
claudeai-sync: 
clean-mac-processes: 
collect-fb-audience: 
connect-telegram: 
content-mine: 
contrib-watch: 
corpus-bench: 
create-desktop-plugin: 
create-session-chips: 
credit-advice-authors: 
crm-sync: 
cross-vendor-code-review: 
cursor-repair: 
decide-as-cofounder: 
delegate-agent-task: 
delegate-team-task: 
devrel-outreach: 
draft-help-requests: 
dual-agent-protocol: 
end-of-day: 
event-calendar-outreach: 
extract-main-chat-skills: 
extract-voice-tasks: 
fanout-deep-research: 
fb-message-commenters: 
fb-messenger: 
fb-reply: 
find-lodging: 
find-person-contacts: 
find-places-on-map: 
find-telegram-chat: 
find-the-original-image: 
find-unloaded-skills: 
finish-current-task: 
fi
...
3: lead-resolve | я говорил с каким-то фаундером на прошлой неделе, помню только что он из Израиля и про голосовых ботов
14: lead-resolve | figure out who that guy from the meetup was
15: llll | LLLL
16: llll | давай llll по этому вопросу
17: llll | llll
18: llm-onboard-test | подключи новую модель к нам и проверь экзаменом на что она годится
19: llm-onboard-test | поставили Gemini в Antigravity, а он тупит и не видит наших правил
20: llm-onboard-test | onboard and test this new LLM in our setup
=== END ===

---

**Claude:**

SERVICE
