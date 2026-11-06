---
session: s_a87068f6
date: 2026-10-29
words: 418
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · Classify this Claude Code session as HUMAN or SERVICE by its CONTENT

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a87068f6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
1: Обрыв или крэш сессии: где были, всё ли живо. Триггеры: «/1», «/!», «восстановись», «я вернулся». НЕ /resume-last (вернуть старый чат в новый).
3: Консенсус машин без оператора. Триггеры: «/03», «003», «теперь вы сами», «договоритесь сами», «найдите консенсус».
3q: Алиас /QQQ = /continue. Триггеры: «/3q».
qqq: То же, что /continue: дожать задачу как кофаундер. Триггеры: «/QQQ». Голое QQQ = подтверждение, не команда.
a2a-cli: Делегировать задачу A2A-агенту через CLI a2a: карточка, отправка, статус. Триггеры: «/a2a-cli», «отдай агенту по A2A».
after-call: Разбор звонка: Plaud, Fireflies, CRM, шаг. Триггеры: «/after-call», «звонок закончился», «разбери звонок». НЕ /interview-debrief (интервью).
agenda: День оператора: календарь и кто ждёт его лично. Триггеры: «/agenda», «что у меня сегодня», «повестка дня», «какие встречи сегодня».
ai-slop: Робо-текст в живой, резать 50-70%; режим личка: ≤10 слов, без похвалы и хвастовства, чтобы ИИ не раскусили. Триггеры: «/ai-slop», «очеловечь текст», «убери нейрослог», «проверь личку на ИИ», «не раскусят ли». НЕ /mycroft-joke (добавить «я ИИ»).
alfa-search-recall-deepresearch: Новый продукт, стратегия: RECALL + Deep Research. Три
...
р под эту вакансию, сколько баллов наберу
15: interviewer-scorecard | не понимаю почему меня отсеивают на скрине, что они видят в моем cv под эту роль
16: interviewer-scorecard | score my CV against this job like a recruiter would
17: intro | познакомь Риту с Петей из стартапа, сделай им общий чат
18: intro | у меня есть инвестор и фаундер которым точно надо поговорить, сведи их
19: intro | make a warm intro between these two people
20: is-this-photo-real | проверь это фото настоящее или фейк
=== END ===

---

**Claude:**

SERVICE
