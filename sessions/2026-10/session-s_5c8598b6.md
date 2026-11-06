---
session: s_5c8598b6
date: 2026-10-29
words: 402
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5c8598b6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
3q: Алиас /QQQ = /continue. Триггеры: «/3q».
qqq: То же, что /continue: дожать задачу как кофаундер. Триггеры: «/QQQ». Голое QQQ = подтверждение, не команда.
adapt-post-to-channels: Разложить пост по тирам: тизер, FB, лонгрид. Триггеры: «/adapt-post-to-channels», «/adapt», «собери эпизод», «разложи пост по площадкам».
adopt-external-idea: Внедрить внешнюю идею тестом или обоснованно отбросить. Триггеры: «/adopt», «внедри альфу», «протестируй идею».
after-call: Разбор звонка: Plaud, Fireflies, CRM, шаг. Триггеры: «/after-call», «звонок закончился», «разбери звонок». НЕ /interview-debrief (интервью).
ai-disclosure-joke: Первая строка «я ИИ» с юмором в исходящем от Майкрофта. Триггеры: «/ai-disclosure-joke», «начало от ИИ звучит сухо», «шутка Майкрофта». НЕ /ai-slop.
amplify-framing: Усилить рамку артефакта, не трогая цифр; сам перед исходящим наружу. Триггеры: «/amplify-framing», «приукрась», «продай это», «усиль рамку».
analyze-job-compensation: Вилка рынка и оценка оффера по jobs.db, цель $200K+. Триггеры: «/analyze-job-compensation», «сколько платят за роль», «конкурентен ли оффер».
answer-github-issues: Ответить нашим опытом в живых чужих тредах GitHub. Триг
...
t | get me the telegram group id and link by its name
15: ройдальше | рой глубже, не останавливайся на этом
16: ройдальше | ты вроде нашёл что-то, но ощущение что это не всё, там ещё есть что копать
17: ройдальше | dig deeper, keep going
18: five-whys | эта штука ломается уже третий раз, разбери почему по-настоящему
19: five-whys | опять тот же сбой что на прошлой неделе и до этого, латаем а оно возвращается
20: check-mcp-connectors | глянь какие коннекторы у нас сейчас живые, а какие отвалились
=== END ===

---

**Claude:**

SERVICE
