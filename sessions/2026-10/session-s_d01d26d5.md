---
session: s_d01d26d5
date: 2026-10-26
words: 1168
turns: 5
tools: "Bash, Grep, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · Разработчик Warren93 выпустил Endo — open-source harness, который собирает агентов и модел…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d01d26d5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Изучить

Разработчик Warren93 выпустил Endo — open-source harness, который собирает агентов и модели в рабочие процессы. В демонстрации он собрал оркестрацию для симуляции президентских дебатов; проект вырос из требований к строгой детерминированности в трейдинге.

→ [https://github.com/longsurf-ai/endo](https://github.com/longsurf-ai/endo)

#automation

---

**Claude:**

Сначала RECALL и проверка сессии, параллельно с чтением репозитория.

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\voice001_collaboration.py\" describe --session-id s_d01d26d5 --wait-seconds 0 2>&1 | head -20", "description": "Classify session for 001 collaboration"}

---

> `Bash` -- {"command": "python \"D:\\Vault\\_imports\\brain_ask.py\" \"endo harness agents orchestration deterministic longsurf\" 2>&1 | head -40", "description": "RECALL in vault on Endo"}

---

> `Bash` -- {"command": "gh repo view longsurf-ai/endo --json name,description,stargazersCount,pushedAt,createdAt,licenseInfo,primaryLanguage,homepageUrl,repositoryTopics 2>&1; echo ---; gh api repos/longsurf-ai/endo/readme -H \"Accept: application/vnd.github.raw\" 2>&1 | head -200", "description": "Read Endo r

---

> `Bash` -- {"command": "gh repo view longsurf-ai/endo --json nameWithOwner,description,stargazerCount,forkCount,pushedAt,createdAt,licenseInfo,primaryLanguage,latestRelease 2>&1; echo ---; gh api repos/longsurf-ai/endo/contents/demo 2>&1 | head -30; echo ---; gh api \"repos/longsurf-ai/endo/git/trees/main?recu

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d01d26d5\\tasks\\bm9oq5pxn.output"}

---

> `Bash` -- {"command": "cd \"$TEMP\" && gh api repos/longsurf-ai/endo/contents/docs/architecture/workflow.md -H \"Accept: application/vnd.github.raw\" 2>&1 | head -90; echo =====; gh api repos/longsurf-ai/endo/contents/server/agent/command/commands/multi-turn-debate.ts -H \"Accept: application/vnd.github.raw\"

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py sig --model \"Sonnet 5.5\" 2>&1 | tail -1", "description": "Get fleet message signature"}

---

**Claude:**

Endo — это настольное приложение, которое запускает разные coding-агентов под вашими подписками и склеивает их в сценарии на TypeScript. Само приложение пока только под macOS на Apple Silicon.

Я прочитал README, `docs/architecture/workflow.md` и код команды `multi-turn-debate`. Ничего не запускал и не клонировал. Проверка в нашем волте (`brain_ask`) не уложилась в таймаут и ещё идёт в фоне. Поэтому сравнения «у нас это уже есть» ниже пока не подтверждены поиском.

**Что это такое**
- Автор Warren93, организация longsurf-ai. Репозиторий создан 14.10.2026, 100 звёзд, 6 форков, лицензия MIT, версия 0.1.2 от 16.10. Авторы сами пишут, что возможны поломки между версиями.
- Endo выросла из их же OpenChart, «торгового workspace с вашими агентами». Из того же репо видно, откуда у проекта тяга к детерминированности: команда делает ещё язык `tea` «для рынка».
- Endo не создаёт агентов. Она запускает Codex, Claude Code, Antigravity и Grok через их собственные CLI, под вашими логинами и без API-ключей. Диалог можно менять между агентами прямо в ходе, и каждый подхватывает полную историю.
- Сценарий — это файл `.workflow.ts`. В нём `agent()` зовёт любую модель, `parallel()` запускает несколько вызовов сразу, `phase()` их группирует, а `{sessionId}` продолжает прежний диалог дочернего агента.
- В комплекте готовые сценарии: `/best-of-n`, `/multi-turn-debate`, `/thesis-killer`, `/hypothesis-race`. Дебаты президентов из анонса — это, скорее всего, `multi-turn-debate` с другой темой; в самом коде я такой сценарий не нашёл.
- Есть расписания по cron или разово, «Dig In» (боковой диалог по выделенному куску ответа) и сохранение сессий на диске.

**Где «строгая детерминированность»**
- Поток управления лежит в обычном TypeScript, а не в промпте. Выходы агентов можно проверять схемой (`agent(input, {schema})`), и это работает без LLM-судьи.
- Другие правила: ESLint запрещает сценариям лишние импорты, динамическую загрузку и ввод-вывод, а запуск и трассировка идут через Effect.
- Сами модели недетерминированны. Детерминированы оркестрация и контракты вокруг них.

**Чего там нет**
- Это не песочница. Сценарий исполняется в основном процессе как доверенный код, и документ это прямо говорит.
- Продолжение диалога живёт только в рамках одного запуска. Возобновления после перезапуска процесса нет.

**Что это даёт нам**
- Идея «агенты как кирпичики поверх чужих платных подписок» совпадает с нашими правилами §6.3 и `llm_ask.py`. Новое для нас — оформить это как сценарии в коде с проверкой схемой.
- Для нас это готовый материал под `/corpus-bench` или рельсы `/llms` и `/continue`: взять шаблоны `best-of-n` и `thesis-killer` и сравнить с нашими.
- Живьём не попробовано: на Windows приложения нет. Из исходников оно собирается на Node 24, Bun 1.4.2 и Just, но запускать без вашего «+» не буду, это чужой код.

**Что дальше**
1. Дождаться `brain_ask` и свериться с волтом и памятью. Если в них пусто, записать заметку с оригиналом в `_originals` по §8.3.
2. По вашему «+» прогнать шаблоны `best-of-n` и `thesis-killer` против нашего веера (план рельс: чтение кода уходит на Codex).

🧒 **Простыми словами:** Endo — это пульт, на котором несколько ИИ-помощников (Claude, Codex, Grok и другие) работают по написанному вами сценарию, как актёры по сценарию. Сценарий — обычный код, поэтому порядок шагов всегда один и тот же, а творчество остаётся только внутри ответов самих помощников. Идея хорошая и похожа на то, что мы уже строим. Но проекту две недели, и пока это сырой софт под Mac.

🏛H · Sonnet 5.5 · 49122

---

**User:**

<task-notification>
<task-id>bm9oq5pxn</task-id>
<tool-use-id>toolu_015UxyZRgK4UJYYxJc6si73L</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_d01d26d5\tasks\bm9oq5pxn.output</output-file>
<status>completed</status>
<summary>Background command "RECALL in vault on Endo" completed (exit code 0)</summary>
</task-notification>

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d01d26d5\\tasks\\bm9oq5pxn.output"}

---

> `Grep` -- {"pattern": "Endo|Emdash|Orca|harness", "path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\insight-DR-DR26-10-11-HUB-01-0535-desktop-multi-harness-ade-windows-hub.md", "output_mode": "content", "-n": true, "head_limit": 25}

---

**Claude:**

RECALL закончился. В нём нашлось то, что меняет вывод: Endo не новая для нас категория, а ещё один кандидат в класс, который мы уже разбирали.

**Что было в волте**
- Заметка [insight-DR-DR26-10-11-HUB-01-0535](D:/Vault/Vault-Knowledge/03-Insights/insight-DR-DR26-10-11-HUB-01-0535-desktop-multi-harness-ade-windows-hub.md) от 11.10 разбирает «десктопное окно для нескольких harness на Windows-хабе». Решение там такое: канарейка Emdash, Orca нет, bb не трогаем. Endo в том разборе не упоминается, потому что репозиторий создан 14.10.
- Для Endo действует тот же фильтр, что для Orca и Emdash: сначала безопасность и обратимость, потом функции.
- Прямых совпадений по слову «endo» и по longsurf в волте нет. Остальное в выдаче про оркестрацию роя из старых заметок (2025) и к делу не относится.

**Что это значит для Endo**
- Сборка из README только под macOS на Apple Silicon. Под Windows-хаб она не подходит, годится как канарейка на NODE-0X. Возможность сборки из исходников на Windows (Node 24, Bun, Just) я не проверял.
- Отличие от Emdash и Orca в том, что у Endo есть слой сценариев в коде с проверкой схемой. Тот разбор такого слоя не оценивал. Это единственная причина смотреть на Endo отдельно.
- В том же разборе есть вывод, что harness важнее модели: разброс до 40 раз по токенам на одну решённую задачу (arXiv 2607.22585). Это довод за оркестрацию сценариями, но не за конкретно Endo.
- Не проверено: как Endo обращается с `~/.claude/settings.json` и `.credentials.json` (у Orca были красные флаги по перезаписи кредов), какие флаги обхода разрешений она ставит агентам, есть ли телеметрия. Пока этого нет, ставить её на машину с общими логинами нельзя.

**Предложение (ничего не делал, жду «+»)**
1. Вынести два вопроса в проверку чтением исходников, без установки: что Endo пишет в конфиги агентов и какие yolo-флаги ставит. Смотреть будет Codex (рельса `code_read`, план рельс: читаю сам только то, что уже прочитал).
2. Если чисто, поставить на NODE-0X в одноразовой папке, прогнать `best-of-n` и `thesis-killer`, записать вердикт в то же решение рядом с Emdash.
3. Заметку об Endo положить в волт с оригиналом README по §8.3 и связью с `decision-2026-10-11-ade-canary-emdash-not-orca`. Сделаю после вашего «+».

🧒 **Простыми словами:** Мы уже выбирали программу, где несколько ИИ-помощников сидят в одном окне, и Endo просто ещё один претендент. Отличие у неё в том, что порядок работы помощников записан кодом, а не просьбой на словах. Но пока она только для Mac, и я не знаю, не полезет ли она в чужие настройки. Сначала почитаю её исходники и только потом поставлю.

🏛H · Sonnet 5.5 · 49122
