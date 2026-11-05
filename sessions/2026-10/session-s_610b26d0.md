---
session: s_610b26d0
date: 2026-10-26
words: 415
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_610b26d0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
1: Восстановление после обрыва сессии: где были, всё ли живо. Триггеры: «/1», «/!», «восстановись», «я вернулся», «где мы остановились».
3q: Алиас /QQQ = /continue. Триггеры: «/3q».
qqq: То же, что /continue: дожать задачу как кофаундер. Триггеры: «/QQQ». Голое QQQ = подтверждение, не команда.
a2a-cli: Делегировать задачу A2A-агенту через CLI a2a: карточка, отправка, статус. Триггеры: «/a2a-cli», «отдай агенту по A2A».
after-call: Разбор звонка: Plaud, Fireflies, Screenpipe, CRM, шаг. Триггеры: «/after-call», «разбери звонок», «что говорил лид». Текст = /fa.
agenda: День оператора: календарь и кто ждёт его лично. Триггеры: «/agenda», «что у меня сегодня», «повестка дня», «какие встречи сегодня».
ai-slop: Переписать робо-текст как живой занятой человек, резать 50-70%. Триггеры: «/ai-slop», «/slop», «очеловечь», «убери нейрослог».
alfa-search-recall-deepresearch: Альфа-протокол: RECALL + Deep Research до стратегической работы. Триггеры: «/alfa-search-recall-deepresearch», «альфа», «R+DR», «РДР».
alpha-credit: Кредит автору совета из комментов и тредов
...
s from my other machines
19: intake | запиши это как правило и разложи куда надо
20: five-whys | я уже третий раз говорю одно и то же, а вы опять забываете
21: intake | save this as a permanent rule
22: dr-teasers | собери за сегодня о чём я парился и сделай посты с просьбой о помощи
23: dr-teasers | весь день упирался в разные стены, может спросить у людей в сети
24: dr-teasers | draft ask posts from today's struggles
25: interview-debrief | собес закончился, разбери что было и напиши им письмо
=== END ===

---

**Claude:**

SERVICE
