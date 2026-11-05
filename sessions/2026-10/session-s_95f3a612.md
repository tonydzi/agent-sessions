---
session: s_95f3a612
date: 2026-10-26
words: 414
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_95f3a612` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
03: Консенсус машин без оператора. Триггеры: «/03», «003», «теперь вы сами», «договоритесь сами», «найдите консенсус».
1: Обрыв или крэш сессии: где были, всё ли живо. Триггеры: «/1», «/!», «восстановись», «я вернулся». НЕ /resume-last (вернуть старый чат в новый).
3q: Алиас /QQQ = /continue. Триггеры: «/3q».
qqq: То же, что /continue: дожать задачу как кофаундер. Триггеры: «/QQQ». Голое QQQ = подтверждение, не команда.
a2a-cli: Делегировать задачу A2A-агенту через CLI a2a: карточка, отправка, статус. Триггеры: «/a2a-cli», «отдай агенту по A2A».
after-call: Разбор звонка: Plaud, Fireflies, CRM, шаг. Триггеры: «/after-call», «звонок закончился», «разбери звонок». НЕ /interview-debrief (интервью).
agenda: День оператора: календарь и кто ждёт его лично. Триггеры: «/agenda», «что у меня сегодня», «повестка дня», «какие встречи сегодня».
ai-slop: Робо-текст в живой, резать 50-70%. Триггеры: «/ai-slop», «очеловечь текст», «убери нейрослог». НЕ /mycroft-joke (добавить «я ИИ»).
alfa-search-recall-deepresearch: Новый продукт, стратегия: RECALL + Deep Research. Триггеры: «/alfa-search-recall-deepresearch», «R+DR», «альфа». НЕ /recall (память).
alpha-credit: Кредит автору сове
...
ons | what sessions are running right now
20: share-fix | мы починили баг в их библиотеке, отправь им репорт и поделись фиксом с людьми
21: share-fix | у нас заработал обход чужого бага, а люди в issue до сих пор мучаются
22: share-fix | report this upstream bug and share our fix
23: skill-catalog | поищи среди отключённых скиллов, есть ли под это что-то
24: skill-catalog | ни один видимый скилл не подходит, а я помню что был какой-то для сео
25: skill-catalog | find a hidden skill for this task
=== END ===

---

**Claude:**

SERVICE
