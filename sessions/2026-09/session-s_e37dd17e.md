---
session: s_e37dd17e
date: 2026-09-24
words: 327
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · Scheduled run: robot-profile-scrub-nightly

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_e37dd17e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="robot-profile-scrub-nightly" file="C:\Users\dev\.claude\scheduled-tasks\robot-profile-scrub-nightly\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Ночная страховка против класса `robot-profile-holds-human-session` (замер 22.09.2026: робо-профили fbread/fbreply держали личный аккаунт оператора [EMAIL] у 6 вендоров, робот ходил на chatgpt.com Селениумом, провайдеры гасили сессию серверно и выбивали человеческий Chrome и Google-аккаунты).

Основная дверь — `guard()` в `firefox_selenium.make_driver`, он срабатывает перед КАЖДЫМ подъёмом робо-драйвера. Эта рутина — второй слой на случай, если робота подняли мимо него.

ШАГИ (всё детерминированно, 0 LLM, 0 сети):

1. `python ~/.claude/scripts/_shared/robot_profile_scrub.py --scrub`
   exit 0 = чисто · 1 = сняли чужое · 2 = профиль был занят живым Firefox.

2. Если exit 1 — это РЕЦИДИВ, и он важнее самой чистки: значит что-то залогинило робота обратно. Тогда:
   - назови, какие домены вернулись (их печатает сам прибор);
   - прогони `python ~/.claude/scripts/rail_sweep.py chatgpt` и `... google`, чтобы увидеть все поверхности;
   - добавь строку в журнал: `python ~/.claude/scripts/selfheal.py journal --class robot-profile-holds-human-session --what "<что вернулось и откуда>"`;
   - напиши оператору одну строку в чат 02.

3. Проверь бэкап кук Chrome: `python ~/.claude/scripts/_shared/chrome_login_shield.py`.
   Строка `backup ⛔` = элевированная задача `ai.paloalto.chrome-cookie-backup-admin` так и не поставлена (нужен один запуск от админа, команду печатает `chrome_login_shield.py --install-schedule-admin`). Напомни оператору про это НЕ чаще раза в неделю, иначе это alert-fatigue.

4. Прогони тест сторожа: `python ~/.claude/scripts/_shared/_test_robot_profile_scrub.py`. Красный тест = сторож сломан, это инцидент, доложи сразу.

5. Отчёт одной строкой в ночной housekeeping: «robot-profile-scrub: профилей N · снято M · рецидив да/нет · chrome-backup ок/нет».

Ничего не спрашивай у оператора: всё здесь обратимо (бэкап БД кладётся перед каждым удалением в ~/.claude/secrets/robot-profile-scrub/).
</scheduled-task>

---

**Claude:**

You've hit your weekly limit · resets Sep 27, 5am (Europe/London)
