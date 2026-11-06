---
session: s_65d55cf0
date: 2026-10-29
words: 325
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_65d55cf0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
rd, а как ему поручить работу не знаю
15: delegate-agent-task | send this task to the remote agent via A2A protocol
16: after-call | разбери созвон который только что был, кто что сказал и что дальше делать
17: after-call | звонок закончился, запись где то в плауде, а я уже не помню о чем договорились
18: after-call | debrief my call that just ended
19: show-day-agenda | что у меня сегодня по встречам и кто меня ждет
20: show-day-agenda | утро, не понимаю с чего начать день и какие созвоны стоят
=== END ===

---

**Claude:**

SERVICE
