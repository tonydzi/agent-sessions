---
session: s_d9fb7fec
date: 2026-10-29
words: 359
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d9fb7fec` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
1: 
3: 
3q: 
qqq: 
a2a-cli: 
after-call: 
agenda: 
ai-slop: 
alfa-search-recall-deepresearch: 
alpha-credit: 
alpha-judge: 
apple-photos: 
apply: 
arch: 
ask: 
ask-any: 
ask-debt: 
audit-content: 
bible: 
booking: 
brain: 
brain-onboard: 
bus: 
call-prep: 
canon-revision: 
cc: 
ccgui-plugin-creator: 
chat: 
chat-search: 
chat001: 
chip: 
chrome-fix: 
claude-repair: 
claudeai-sync: 
codex-mirror: 
codex-review: 
cofounder: 
comments: 
community-alpha: 
comp-analysis: 
content-mine: 
continue: 
contrib-watch: 
corpus-bench: 
crm-sync: 
cursor-repair: 
cv: 
cv-outreach: 
dash: 
decide-as-cofounder: 
deflate: 
defuddle: 
devrel-wave: 
display-mode: 
dr-fanout: 
dr-teasers: 
elephant: 
end-of-day: 
episode: 
fa: 
faaa-sync: 
fake-it: 
fb-audience: 
fb-dm: 
fb-messenger: 
fb-reply: 
find: 
find-person: 
find-the-original-image: 
fireflies-sync: 
firefox: 
five-hard: 
five-whys: 
fleet: 
follower-onboard: 
fundraise: 
gemini: 
geo: 
gh-discussions: 
github-growth: 
gmail: 
gonka-fundraise: 
granola-sync: 
handle-objection: 
handoff: 
hdd-storage-cleaning: 
hk: 
hubrun: 
hyper-research: 
inbox: 
intake: 
intention: 
interview-debrief: 
interview-prep: 
interviewer-sco
...

14: brain-onboard | у знакомой куча всего в мессенджерах и почте, хочет такой же волт как у меня но свой
15: brain-onboard | set up a personal second brain for my friend
16: brain | проверь жив ли поиск по волту и не протух ли индекс
17: brain | автоподсказки из памяти перестали появляться, кажется что-то с поиском легло
18: brain | is my second brain search healthy?
19: bus | напиши ноутбуку и хабу чтобы обновили скрипт
20: bus | хаб молчит уже полдня, хочу глянуть что машины писали друг другу
=== END ===

---

**Claude:**

SERVICE
