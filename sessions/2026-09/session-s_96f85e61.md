---
session: s_96f85e61
date: 2026-09-04
words: 728
turns: 8
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-04 · Scheduled run: git-s7-fast

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_96f85e61` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="git-s7-fast" file="C:\Users\dev\.claude\scheduled-tasks\git-s7-fast\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: git-s7-fast
description: GIT-25 рутина: быстрый лейн мержей в маленьких/средних репо (<2k⭐), PR только под живой issue
---

Ты — ежедневная рутина GIT-S7-FAST программы GIT-25 (быстрый лейн мержей; рождён 20.08.2026 разрезом git-s7-deep-lane на fast/vendor по приказу оператора: «те, которые работают эффективно — чтобы работали ещё эффективнее»). Замер 10–19.08: ВСЕ 5 мержей окна пришли из маленьких/средних репо (go-sdk, diri×2, Konnect, book-to-skill) — это твоя территория. Большие вендоры — НЕ твоя работа, для них есть git-s7-vendor.

⭐ УЗЕЛ: ты работаешь на ХАБЕ `HUB-01` (Windows, Europe/Lisbon). Рутина перенесена сюда с `NODE-0X` 22.08.2026 приказом оператора «перенеси эту рутину на ХАБ немедленно» — причина класса: ноут не always-on, а хаб держит длинные внешние треды (CLAUDE.md §7.1, §7.12). На NODE-0X задача погашена в тот же заход; двух копий быть не должно — увидел живой git-s7-fast на другом узле, скажи об этом строкой в журнал.

ЦЕЛЬ И МЕТРИКА: мержи. Быстрый темп, маленькие/средние репо (< 2000 звёзд, живой мейнтейнер: коммиты за последние 30 дней). Прочитай журнал `D:\Vault\Vault-Knowledge\10-Tasks\git25-journal.md` (что уже сделано, есть ли ответы, кому НЕ стучаться повторно) и мастер-файл `D:\Vault\Vault-Knowledge\10-Tasks\task-2026-07-31-github-25-routines-program.md`.

⭐ ПРИБОР «У КОГО МЯЧ» — ГОТОВЫЙ, НЕ ИЗОБРЕТАЙ СВОЙ (урок 21.08, повтор 22.08): очередь ответов печатает
`python C:\Users\dev\.claude\scripts\pr_watch.py --digest` — блок «🔴 МЯЧ У НАС», правило трёх дней, 🪦-могилы,
реестр `_outreach/outbound_github.json`. Свой перебор `gh search prs` = дубль центрального сторожа (7 рутин зовут его).
Открыл наш PR/issue и его нет в реестре → `pr_watch.py --add <url>` В ТОМ ЖЕ ЗАХОДЕ, иначе мяч по нему невидим.

Задача на заход (по приоритету):
1. ОТВЕТЫ — если мейнтейнер/кто-то ответил на наше — реагировать сегодня же, быстро и по существу (прерывание №1).
2. Живые просьбы мейнтейнера (help-wanted / good-first-issue / его комменты «надо бы») → focused PR ≤100 строк с тестами и описанием-репортом.
3. Issues-исследование: воспроизведение чужого бага у себя + root cause + предложение фикса.
За заход — 1-2 качественных действия, не больше.

⭐ ПРАВИЛО ИЗ ВЛИТОГО git-s23 (влит 20.08.2026, причина: 0 мержей за месяц у холодной волны): PR ТОЛЬКО под живой issue / живую просьбу мейнтейнера (issue-matched). Холодные PR веером ⛔ — холодный PR в глухую очередь не работает [[cold-pr-into-silent-queue]]; замер 26.07: отклик получает только issue-matched PR. Проверка входа: `python C:\Users\dev\.claude\scripts\issue_match.py <owner/repo>` (если скрипт есть) либо руками найти живой issue — нет живого issue → PR не шлём, делаем ревью/issue-коммент.

В конце — строка в журнал `git25-journal.md`, формат канона (по строкам судит `github_routines_registry.py`): **Строка:** дата · GIT-S7-FAST · репо · действие · ответ/мерж (с URL артефактов). В строке называй узел (`узел HUB-01`), как это делали заходы с NODE-0X.

Стоп-правила: накрутка ⛔ · leak-scan диффов и тел PR (FAIL=0) · CLA/contributor agreement → стоп и аск в 02, автономно не подписывать · себя не ревьюим · бампы в закрытые/молчащие треды ⛔ (их мяч + тишина >3д = 🪦) · раскрытие «I am an AI agent (Claude)» первой строкой тела PR + Assisted-by: Claude (Anthropic) в коммитах (не Co-authored-by, DR-701) · верстак (клоны/venv) в скретчпаде сессии, не в волте · Tier-2 не трогаем · наружу ничего кроме GitHub-коммуникации (§4.7 — она без гейтов).

Перед любым действием от лица оператора рутина обязана сначала загрузить Библию через скилл bible и действовать по ней.
Рутина безлюдная: работай в bypass-permissions / auto-режиме, не жди кликов-одобрений от оператора — истинные блоки (Tier-2, CLA) решаются аском в 02, а не ожиданием у терминала.
</scheduled-task>

---

**Claude:**

You've hit your weekly limit · resets Sep 6, 5am (Europe/London)

---

**User:**

Продолжи

---

**Claude:**

You've hit your weekly limit · resets Sep 6, 5am (Europe/London)

---

**User:**

Continue from where you left off.

---

**Claude:**

No response requested.

---

**User:**

Try again

---

**Claude:**

**пятница, вечер, 22:16, 4 сентября 2026**

Начинаю прогон GIT-S7-FAST. Первым делом — прибор «у кого мяч» и журнал.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && tail -n 60 git25-journal.md 2>/dev/null || echo \"NO JOURNAL\"", "description": "Читаю хвост журнала GIT-25"}

---

> `Bash` -- {"command": "cd ~ && python \"C:\\Users\\dev\\.claude\\scripts\\pr_watch.py\" --digest 2>&1 | head -n 80", "description": "Прибор: у кого мяч по нашим PR/issue"}
