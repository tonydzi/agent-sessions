---
session: s_515e710c
date: 2026-10-26
words: 406
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_515e710c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
-daily | запости сегодняшние посты в фейсбук тредс и инсту
20: social-daily | за вчера ни итог ни факап дня так и не вышли в соцсети
21: social-daily | run today's social autoposting
22: sostav-comments | набросай мне ответы на интересные посты в составе из ночной подборки
23: sostav-comments | разбираю шортлист клуба, а сам писать комменты в треды лень
24: sostav-comments | draft replies to fresh Sostav club threads
25: sostav-dm | напиши в личку ребятам из состава, которые просили про ии и crm
=== END ===

---

**Claude:**

SERVICE
