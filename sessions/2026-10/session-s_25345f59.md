---
session: s_25345f59
date: 2026-10-28
words: 1654
turns: 8
tools: "Agent, Bash, Grep, ToolSearch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · Scheduled run: auto-hub-261028-pinned-eval-corpus

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_25345f59` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261028-pinned-eval-corpus" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261028-pinned-eval-corpus\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первым действием: mcp__ccd_session_mgmt__set_session_title(session_id="self", title="⚙️ · 📏🧪 Эталонный набор задач флота на одной модели").

Заказ оператора 28.10.2026 (дословно): «Закрепленный набор задач для замеров на одной модели, верно... давай это делать, поднимай на это сессии». Соседняя сессия auto-hub-261028-critic-loop-gauntlet-from-openflow делает три других механизма (лимиты раундов, critic-must-execute, чекпоинты) — её зону не трогай.

Цель: фиксированный набор из ~5-6 типовых задач нашего флота (координация через шину, lease, ревью diff, DR-сбор, починка теста и т.п.), который прогоняется каждый релиз на ОДНОЙ закреплённой дешёвой модели, чтобы изменения меряли нашу логику (шина, lease, протокол ролей), а не модели. Сравнение двух прогонов: статус, вердикт, время, стоимость, раунды; порог регрессии «больше 10% или одной единицы».
Образец: OpenFlow, локально E:\!CLAUDE-HUBPC-June26\_oss\openflow\packages\flow\evals\ (README.md, score.ts) и src/graph/corpus.ts, FLOW.md раздел «The eval corpus». Ключевые принципы оттуда: скрипт НЕ гоняет модели сам (иначе мерит себя), он читает логи прогонов; одна закреплённая модель на всё; бесплатная половина = тест формы, платная = человек/сессия запускает.

Правила: RECALL первым — у нас могут уже быть близкие вещи (/corpus-bench, практика H79753 «парный замер», practice_adoption_report.py, _test_*.py); проверь и строй поверх, а не рядом. АК-47, без нового фреймворка. Тень первой (§5.7, дата урожая в 00-System/Shadow-First-Queue.md). Паспорт + счётчик (§5.8), назови вызывателя (/retro, /tt, /corpus-bench?) и подключи. Тест обязан покраснеть. Коммит с трейлерами §5.11. onair.py declare.
Итог оператору в чат этой сессии: что построено, улики (команды с выводом и exit-кодом), первый базовый прогон, что дальше. Подпись machine_stamp.py sig. Блок «🧒 Простыми словами».
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ · 📏🧪 Эталонный набор задач флота на одной модели"}

---

> `Bash` -- {"command": "cd ~/.claude; ls skills/corpus-bench/ 2>/dev/null; head -60 skills/corpus-bench/SKILL.md 2>/dev/null; ls scripts | grep -iE \"corpus|bench|practice_adoption|paired|eval\" ; ls \"/e/!CLAUDE-HUBPC-June26/_oss/openflow/packages/flow/evals/\"", "description": "Recall existing bench too

---

> `Bash` -- {"command": "cd ~/.claude/scripts; head -80 micro_bench.py; ls micro_bench_tasks micro_bench_profiles; wc -l micro_bench.py _test_micro_bench.py; grep -rl micro_bench ../skills/*/SKILL.md 2>/dev/null | head", "description": "Inspect existing micro_bench tool"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\"; sed -n 1,200p _oss/openflow/packages/flow/evals/README.md | head -120; echo ----; git show --stat 131b671 | head -20", "description": "Read OpenFlow evals README and replay commit"}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\"; sed -n 1,60p docs/collab-roles-replay-2026-10-25.md; echo ----; ls ~/.claude/scripts | grep -iE \"critic_loop|aibus_lite|workspace_write_lease|voice001_replay|replay\"; grep -n \"def \\|jsonl\\|receipt\" ~/.claude/scripts/critic_loop.py | head -40", 

---

> `Bash` -- {"command": "cd ~/.claude/scripts; sed -n 1,70p critic_loop.py; sed -n 126,200p critic_loop.py; ls state/critic_loop/runs 2>/dev/null | head; ls ~/.claude/state/critic_loop/runs 2>/dev/null | head", "description": "Read critic_loop run format"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; cat ~/.claude/state/critic_loop/runs/H45914-live.json; echo; tail -2 ~/.claude/state/critic_loop/receipts.jsonl; grep -n \"def review\\|def cmd_review\\|verdict\\|DB\\b\\|sqlite\\|\\.jsonl\" aibus_lite.py | head -30", "description": "Inspect a real run file and aib

---

> `Bash` -- {"command": "cat ~/.claude/scripts/critic_loop_prices.json; ls ~/.claude/scripts/red_proof.py; grep -n \"Corpus\\|corpus\\|eval\" \"/e/Obsidian/Vault-Knowledge/00-System/Shadow-First-Queue.md\" | head -5; tail -15 \"/e/Obsidian/Vault-Knowledge/00-System/Shadow-First-Queue.md\"", "description": "Chec

---

> `Bash` -- {"command": "cd ~/.claude/scripts; sed -n 100,125p critic_loop.py; python ~/.claude/scripts/onair.py declare --help 2>&1 | head -15", "description": "Check load_prices and onair usage"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone fleet-code/eval-corpus --mode exclusive --title \"fleet_eval_corpus.py: закреплённый набор задач флота на одной модели\" --summary \"новый файл + тест + прайс eval; critic_loop.py не трогаю (читаю его runs/receipts)\" --ttl-hours 4 --agen

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\fleet_eval_corpus.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"fleet_eval_corpus.py -- закреплённый набор задач флота, одна модель, сравнение релизов.\n\nMachine: HUB-01 (Хаб) · Agent: Claude Code (Opus 5.5) · Opera

---

> `Bash` -- {"command": "cd ~/.claude/scripts; for f in aibus_lite.py bus_send.py dr_registry.py workspace_write_lease.py critic_loop.py; do ls $f 2>/dev/null || echo \"MISSING $f\"; done; find ~/.claude -maxdepth 3 -name aibus_lite.py 2>/dev/null | head -3; python -c \"\nimport sys; sys.path.insert(0,'.'); imp

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_25345f59/tasks/b0goqmaqm.output\"; cd ~/.claude/scripts && python -c \"\nimport sys; sys.path.insert(0,'.'); import fleet_eval_corpus as m\nfor c in m.CASES: print(c['id'], m.task_sha

---

> `Grep` -- {"pattern": "aibus_lite", "path": "E:\\!CLAUDE-HUBPC-June26\\docs\\agent-protocol.md", "output_mode": "content", "head_limit": 4}

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\"; ls scripts/aibus_lite.py tools/aibus_lite.py 2>/dev/null; git ls-files | grep aibus_lite | head", "description": "Locate aibus_lite.py"}

---

**Claude:**

Нашёл `aibus_lite.py` в корне проекта, а не в scripts. Правлю поиск деталей и вставляю настоящие хэши.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'EOF'\np='fleet_eval_corpus.py'; s=open(p,encoding='utf-8').read()\nold_new={'\"a8b2c2bba1b6\"':'\"852267b94494\"','\"7f8a2b6dd84f\"':'\"2f9c12f9f7f6\"','\"54a74ab6c76f\"':'\"ad987cfd060e\"',\n'\"f6b49e4b2bb9\"':'\"252eadec117f\"','\"5e4b1d78b2a0\"':'\

---

**Claude:**

Форма зелёная. Теперь тест, который обязан покраснеть.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_fleet_eval_corpus.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"_test_fleet_eval_corpus.py -- тест fleet_eval_corpus.py, 0 LLM, временные каталоги.\n\nMachine: HUB-01 (Хаб) · Agent: Claude Code (Opus 5.5) · Ope

---

> `Bash` -- {"command": "cd \"/e/!CLAUDE-HUBPC-June26\"; python ~/.claude/scripts/_test_fleet_eval_corpus.py; echo \"exit=$?\"; python ~/.claude/scripts/red_proof.py --help 2>&1 | head -20", "description": "Run test and show red_proof usage"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'EOF'\np='_test_fleet_eval_corpus.py'; s=open(p,encoding='utf-8').read()\na='''    check(\"shape живого набора чист\", m.shape(prices=prices, dirs=[HERE, os.getcwd(), os.path.dirname(HERE)]) == []\n          or all(\"деталь\" in e for e in m.shape(pric

---

**Claude:**

Тест зелёный, 5 из 5 мутаций его красят. Делаю первый настоящий базовый прогон кейса `test-repair` на Haiku 4.5.

---

> `Bash` -- {"command": "D=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_25345f59/scratchpad/eval-test-repair\"; mkdir -p \"$D\"; cd \"$D\"\ncat > calc.py <<'EOF'\ndef mean(xs):\n    \"\"\"Среднее списка; пустой список = 0.0.\"\"\"\n    return sum(xs) / (len

---

> `Agent` -- {"description": "Haiku author fixes red test", "model": "haiku", "run_in_background": false, "prompt": "You are the implementer in a fixed eval task. Work only inside this folder: C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_25345f59/scratchpad/ev

---

> `Bash` -- {"command": "D=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_25345f59/scratchpad/eval-test-repair\"\nexport CRITIC_LOOP_PRICES=~/.claude/scripts/fleet_eval_prices.json\ncd \"$D\"; git diff --no-index /dev/null test_calc.py >/dev/null; grep -n \"r

---

**Claude:**

Базовый прогон записан. Осталось: строка в очереди теней, подключение к `/corpus-bench` и `/tt`, коммит.

---

> `Bash` -- {"command": "cd ~/.claude; git rev-parse --show-toplevel 2>&1 | head -1; git status --short scripts/fleet_eval_corpus.py 2>&1 | head; grep -n \"^## \\|^### \" skills/tt/SKILL.md | head -30; python scripts/machine_stamp.py line --agent \"Claude Code (Opus 5.5)\"", "description": "Check git home and t

---

> `Bash` -- {"command": "cd ~/.claude && git check-ignore -v scripts/fleet_eval_corpus.py; git ls-files scripts/critic_loop.py skills/tt/SKILL.md skills/corpus-bench/SKILL.md; git log -1 --format=%h -- scripts/critic_loop.py", "description": "Check git tracking of target files"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && git status --short fleet_eval_corpus.py _test_fleet_eval_corpus.py fleet_eval_prices.json critic_loop.py; git log -1 --format='%h %s' -- critic_loop.py; cd ~/.claude/skills 2>/dev/null && git rev-parse --show-toplevel 2>&1|head -1", "description": "Check scripts 

---

**Claude:**

Подключаю вызывателей: раздел в `/tt` (после шага 3.6) и в `/corpus-bench`.

---

> `Bash` -- {"command": "cd ~/.claude/skills && cp tt/SKILL.md \"tt/SKILL.md.bak-evalcorpus-20261028\" && cp corpus-bench/SKILL.md \"corpus-bench/SKILL.md.bak-evalcorpus-20261028\" && python - <<'EOF'\nblk_tt = '''## Шаг 3.65 — ⭐ ЛОГИКА ФЛОТА НЕ ПРОСЕЛА? Закреплённый набор на одной модели (dev 28.10.2026)\n\n

---

**Claude:**

Строка в очередь теней (с бэкапом) и коммиты.

---

> `Bash` -- {"command": "Q=\"/e/Obsidian/Vault-Knowledge/00-System/Shadow-First-Queue.md\"; cp \"$Q\" \"/e/!CLAUDE-HUBPC-June26/_app-backups/Shadow-First-Queue-H64d0-evalcorpus-20261028.before.md\"\ncat >> \"$Q\" <<'EOF'\n- 🌑 fleet-eval-corpus (сессия auto-hub-261028-pinned-eval-corpus, старт **2026-10-28*

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close --help 2>&1 | head -5; python ~/.claude/scripts/onair.py close 2026-10-28T164722Z-HUB-01-64d0a7cb-fleet-code-eval-corpus 2>&1 | tail -1; tail -3 ~/.claude/logs/fleet_eval_corpus_usage.jsonl; python ~/.claude/scripts/machine_stamp.py sig --m

---

**Claude:**

Я собрал набор из шести закреплённых задач флота на одной модели и записал первый базовый прогон. Пока он покрывает **1 кейс из 6**, остальные пять ещё не прогонялись.

**Как устроено.** Прибор: [fleet_eval_corpus.py](C:/Users/dev/.claude/scripts/fleet_eval_corpus.py), сделан по образцу OpenFlow evals.
- Шесть задач: передача задачи по шине, спор двух исполнителей за один файл (lease), ревью diff, сбор ответов для DR, починка красного теста, петля автор/критик. Текст каждой задачи заморожен хэшем: если его поправить, прибор видит дрейф и проверка формы падает.
- Модель одна на весь набор: `claude-haiku-4-5`. Прогон на любой другой модели прибор отказывается записывать.
- Модели он сам не запускает, а читает логи соседнего `critic_loop.py`: раунды, деньги, время, квитанцию критика. Файл `critic_loop.py` я не трогал.
- `shape` бесплатно проверяет форму набора. `record` записывает прогон, `compare` сравнивает два прогона и печатает регрессии первыми.
- Статус и вердикт считаются регрессией при любом ухудшении. Деньги, время и раунды считаются регрессией, только если выросли больше чем на 10% или на одну единицу, смотря что больше.

**Что уже работает, с выводом команд:**
- `shape` → `SHAPE: OK (6 кейсов, 0 проблем, модель claude-haiku-4-5)`, exit=0.
- Тест `_test_fleet_eval_corpus.py` → `PASS: 0 провалов`, exit=0.
- `red_proof.py`: все 5 поломок (порог, закрепление модели, пропавший кейс, порядок статуса, дрейф текста) дали `КРАСНОЕ ДОКАЗАНО`.
- Настоящий прогон соседа на claude-plan и codex прибор отверг: `ОТКАЗ: … набор закреплён на claude-haiku-4-5`, exit=2.

**Первый базовый прогон (`base-2026-10-28`), кейс test-repair.** Субагент на Haiku 4.5 починил `calc.py`, критик запустил тест через `critic_loop.py exec` и получил квитанцию rc=0. Запись: `test-repair: done · pass · $0.087406 · 58.6 c · 1 раундов`. Сравнение базы с самой собой даёт 0 регрессий, exit=0.

Две оговорки к этим цифрам:
- 58.6 с включают и мою подготовку: сам субагент работал 38 с.
- Харнес отдал только общий счёт токенов (87 406), без деления на вход и выход. Поэтому стоимость посчитана грубо, по цене Haiku как API. Это мерка для сравнения прогонов, а не реальный счёт: работа шла по подписке.

**Куда подключено:**
- `/tt`, новый шаг 3.65: после правки шины, lease или ролей запускать `shape`, после релиза запускать `compare`.
- `/corpus-bench`: добавлен раздел о том, чем этот прибор отличается от `micro_bench`.
- Счётчик использования пишется в `~/.claude/logs/fleet_eval_corpus_usage.jsonl`.
- Тень до 11.11, строка в `00-System/Shadow-First-Queue.md`, перед правкой снят бэкап.
- Коммиты: scripts `64852d3`, skills `55e0cb7`, с трейлерами. Табличка onair открыта и закрыта.
- План рельс я не объявил: вся работа сделана мной, плюс один субагент Haiku.

**Что дальше:**
1. Прогнать на Haiku остальные пять кейсов и записать их в ту же базу. Lease и шину можно мерить в отдельной временной папке.
2. После первого релиза логики флота запустить `compare base-2026-10-28 <тег>`.
3. К 11.11 решить, становится ли `compare` блокирующей проверкой в `/tt`.

🏛H · Opus 5.5 · 47975

🧒 **Простыми словами:** мы завели одинаковую контрольную работу для нашей системы. Каждый раз её решает один и тот же «ученик», Haiku. Если оценка стала хуже, значит, мы испортили школу, а не ученика. Пока проверен один предмет из шести, и по нему пятёрка.
