---
session: s_154e2276
date: 2026-08-24
words: 7508
turns: 19
tools: "Bash, Edit, Grep, PowerShell, Read, Skill, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-08-24 · изучи этот комп и скажи какую рабочую папку мне стоит выбирать при старте новой сессии

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_154e2276` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

изучи этот комп и скажи какую рабочую папку мне стоит выбирать при старте новой сессии

---

**Claude:**

[⏰ понедельник, утро, 08:30, 24 августа 2026]

Сейчас быстро осмотрю машину: какие папки-кандидаты есть, где живут прошлые сессии и память, и дам вердикт одной строкой.

---

> `PowerShell` -- {"command": "hostname; Get-PSDrive -PSProvider FileSystem | Select-Object Name,Used,Free,Root | Format-Table; ls \"C:\\Users\\dev\\.claude\\projects\" | Select-Object Name", "description": "Show hostname, drives, and Claude project folders"}

---

> `PowerShell` -- {"command": "ls \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\" | Select-Object Name -First 40", "description": "List contents of current working folder"}

---

> `PowerShell` -- {"command": "ls \"E:\\\" | Select-Object Name; \"---\"; $a=\"C:\\Users\\dev\\.claude\\projects\\C--Users-dev--CLAUDE-NODE-0X-May26\"; $b=\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\"; foreach($p in @($a,$b)){ $f=Get-ChildItem $p -Filter *.jsonl -ErrorAction SilentlyContinue;

---

> `PowerShell` -- {"command": "ls \"E:\\!CLAUDE-HUBPC-June26\" | Select-Object Name -First 30; \"---memory---\"; ls \"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\" -ErrorAction SilentlyContinue | Measure-Object | Select-Object Count", "description": "Inspect hub project folder and i

---

**Claude:**

Готово, картина ясная. Отвечаю.

**Вердикт: на этом компе (хаб HUB-01) новую сессию стартуй в папке `E:\!CLAUDE-HUBPC-June26`.**

Что я нашёл:

| Папка | Что это | Сессий | Последняя активность |
|---|---|---|---|
| `E:\!CLAUDE-HUBPC-June26` | **родной проект хаба** | 1920 | сегодня 07:45 |
| `C:\Users\dev\!CLAUDE-NODE-0X May26` | проект ноута NODE-0X, приехавший синком | 179 | сегодня 08:30 (это мы сейчас) |

Почему именно E:, а не текущая папка:

1. **Память живёт по имени папки.** Claude Code привязывает память и историю сессий к рабочей папке. У хаба почти вся память (1920 сессий, свой каталог memory) накоплена в `E:\!CLAUDE-HUBPC-June26`. Сидя в папке ноута, я вижу «чужую» память NODE-0X, а память хаба — только через костыльные ссылки (в MEMORY.md уже торчит такая ссылка через `../../P---WORKDIR-HUB/...` — это симптом, что сессия не в своём доме).
2. Текущая сессия — как раз пример дрейфа: хост HUB-01, а проект ноутбучный. Так теряется recall прошлых сессий хаба.
3. Папка `C:\Users\dev\!CLAUDE-NODE-0X May26` — легитимный дом только на самом ноуте NODE-0X. На хабе она нужна лишь как синкаемое хранилище (secrets, gmail-скрипты), не как рабочая директория.

Простое правило для всех машин: **рабочая папка = родная папка этой машины**, на хабе это `E:\!CLAUDE-HUBPC-June26`, на ноуте NODE-0X — `C:\Users\dev\!CLAUDE-NODE-0X May26`. Волт (`D:\Vault\...`) рабочей папкой не выбираем никогда — он подключается как дополнительная директория, иначе память сессий размажется по волту.

🎙 Майк: эта сессия уже сидит не в той папке — для разговора не страшно, но для стройки на хабе перезапустись из E:. Хочешь, добавлю в SessionStart-хук предупреждение «папка не родная для этой машины»?

🧒 Простыми словами: у каждого компа есть свой «домашний кабинет», где лежат все его дневники. Этот комп — большой десктоп, его кабинет на диске E:. Мы сейчас случайно сидим в кабинете ноутбука. Работать можно, но дневники не те. Новую сессию открывай в `E:\!CLAUDE-HUBPC-June26`.

---

**User:**

+ добавь хук и что нам это даст?

---

**Claude:**

[⏰ понедельник, утро, 08:36, 24 августа 2026]

Принял. Смотрю, как устроены реестр узлов и текущие SessionStart-хуки, чтобы встроиться в существующую рельсу, а не городить новую.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\fleet_nodes.json"}

---

> `PowerShell` -- {"command": "$s = Get-Content \"C:\\Users\\dev\\.claude\\settings.json\" -Raw | ConvertFrom-Json; $s.hooks.SessionStart | ConvertTo-Json -Depth 6", "description": "Show SessionStart hooks from settings.json"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\home_dirs.json", "content": "{\n  \"_meta\": {\n    \"purpose\": \"Native working directory ('home cabinet') per fleet node. Read by hooks/home_dir_guard.py at SessionStart: a session started outside its node's native workdir gets a one-line warning (memory/

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py", "content": "#!/usr/bin/env python3\n\"\"\"home_dir_guard.py — SessionStart hook: warn when a session starts outside this node's native workdir.\n\nWhy: Claude Code keys memory + session history to the working directory. A session\n

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.cmd", "content": "@echo off\nrem home_dir_guard.cmd — SessionStart wrapper for home_dir_guard.py (see its docstring).\npython \"%USERPROFILE%\\.claude\\hooks\\home_dir_guard.py\"\nexit /b 0\n"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_home_dir_guard.py", "content": "#!/usr/bin/env python3\n\"\"\"_test_home_dir_guard.py — tests for hooks/home_dir_guard.py::check (pure function, no I/O).\n\nRun: python ~/.claude/scripts/_test_home_dir_guard.py  (prints PASS/FAIL, exit 0/1).\n

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\_test_home_dir_guard.py\"; '{\"cwd\": \"C:\\\\Users\\\\dev\\\\!CLAUDE-NODE-0X May26\"}' | python \"C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py\"; \"--- native:\"; '{\"cwd\": \"E:\\\\!CLAUDE-HUBPC-June26\"}' | python \"C:\\Users\\dev

---

> `Grep` -- {"pattern": "session_resume_hook", "path": "C:\\Users\\dev\\.claude\\settings.json", "output_mode": "content", "-C": 6}

---

> `PowerShell` -- {"command": "'{\"cwd\": \"E:\\\\!CLAUDE-HUBPC-June26\"}' | python -c \"import sys,json; d=sys.stdin.read(); print(repr(d)); print(json.loads(d))\"", "description": "Check what stdin JSON looks like through PowerShell pipe"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py", "old_string": "        try:\n            payload = json.load(sys.stdin)\n        except Exception:\n            payload = {}", "new_string": "        try:\n            # lstrip BOM: a PowerShell pipe prepends 

---

> `PowerShell` -- {"command": "'{\"cwd\": \"E:/!CLAUDE-HUBPC-June26/docs\"}' | python \"C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py\"; \"--- native done (тишина = ок); foreign:\"; '{\"cwd\": \"C:/Users/dev/!CLAUDE-NODE-0X May26\"}' | python \"C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py\"; \"exit=$

---

**Claude:**

Работает правильно: родная папка — тишина, чужая — одна строка. Теперь регистрирую хук в settings.json.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\settings.json", "old_string": "            \"command\": \"\\\"C:\\\\Users\\\\dev\\\\.claude\\\\hooks\\\\session_resume_hook.cmd\\\"\",\n            \"timeout\": 15\n          }\n        ]\n      },", "new_string": "            \"comma

---

> `PowerShell` -- {"command": "python -c \"import json; d=json.load(open(r'C:\\Users\\dev\\.claude\\settings.json',encoding='utf-8-sig')); hs=[h['command'] for b in d['hooks']['SessionStart'] for h in b['hooks']]; print('JSON OK,', len(hs), 'SessionStart cmds'); print([c for c in hs if 'home_dir' in c])\"", "descri

---

**Claude:**

Коммичу с отпечатком автора (§4.9).

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude && git add home_dirs.json hooks/home_dir_guard.py hooks/home_dir_guard.cmd scripts/_test_home_dir_guard.py settings.json 2>&1 && git commit -m \"home-dir-guard: SessionStart warning when session cwd is not the node's native workdir\n\nRoot case 2026-08-24: hub 

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude && for d in hooks scripts; do echo \"== $d: $(git -C $d rev-parse --show-toplevel 2>/dev/null)\"; done; git rev-parse --show-toplevel; git check-ignore -v home_dirs.json settings.json 2>&1", "description": "Find which git repos cover hooks, scripts, and root fi

---

> `Bash` -- {"command": "sed -n 1,40p .gitignore && git ls-files | head -20", "description": "Inspect root repo gitignore whitelist and tracked files"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\.gitignore", "old_string": "!settings.json", "new_string": "!settings.json\n!home_dirs.json"}

---

> `Bash` -- {"command": "TRAILERS=\"Assisted-by: Claude Code / claude-fable-5\nMachine: HUB-01\nAccount: a2\nOperator: dev\" && git add .gitignore settings.json home_dirs.json && git commit -q -m \"home-dir-guard: register SessionStart hook + native-workdir registry\n\n$TRAILERS\" && echo ROOT-OK && cd

---

> `Bash` -- {"command": "python /c/Users/dev/.claude/scripts/bus_send.py --to NODE-0X-2023PAL --subject \"APPLY: home-dir-guard hook (регистрация в settings.json)\" --body \"Приехали синком: hooks/home_dir_guard.py + .cmd, ~/.claude/home_dirs.json, scripts/_test_home_dir_guard.py. ШАГ УСТАНОВКИ: добавь в свой

---

> `Bash` -- {"command": "python /c/Users/dev/.claude/scripts/bus_send.py --to NODE-0X-2023PAL \"TASK: APPLY home-dir-guard (регистрация SessionStart-хука). Приехали синком: hooks/home_dir_guard.py + home_dir_guard.cmd, ~/.claude/home_dirs.json, scripts/_test_home_dir_guard.py. ШАГ: добавь в свой ПЕР-МАШИННЫЙ 

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\C--Users-dev--CLAUDE-NODE-0X-May26\\memory\\native-workdir-per-node.md", "content": "---\nname: native-workdir-per-node\ndescription: У каждой машины родная рабочая папка (хаб = E:\\!CLAUDE-HUBPC-June26, NODE-0X = C:\\Users\\dev\\!CLAUDE-NODE-0X Ma

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\C--Users-dev--CLAUDE-NODE-0X-May26\\memory\\MEMORY.md", "old_string": "- [AppX-контейнер, а не замок файла](appx-container-deadlock-not-file-lock.md) — «file is in use» врёт; чинит перезагрузка / `ПОЧИНИТЬ CLAUDE.cmd`", "new_st

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\C--Users-dev--CLAUDE-NODE-0X-May26\\memory\\MEMORY.md", "old_string": "- [AppX-контейнер, а не замок файла](appx-container-deadlock-not-file-lock.md) — «file is in use» врёт; чинит перезагрузка / `ПОЧИНИТЬ CLAUDE.cmd`", "new_st

---

**Claude:**

[⏰ понедельник, утро, 08:36 → готово к 08:44, 24 августа 2026]

Сделано, проверено, закоммичено. Вердикт /tt: ✅ (7 юнит-кейсов PASS, живой прогон: чужая папка — предупреждение, родная — тишина, settings.json валиден, хук никогда не блокирует старт).

**Что построил:**
- Реестр родных папок [home_dirs.json](C:\Users\dev\.claude\home_dirs.json): хаб → `E:\!CLAUDE-HUBPC-June26`, NODE-0X → `C:\Users\dev\!CLAUDE-NODE-0X May26`. Новый узел = одна строка в этом файле.
- Сторож [home_dir_guard.py](C:\Users\dev\.claude\hooks\home_dir_guard.py) на SessionStart: молчит, когда всё ок (правило §5.5 — сторож не шумит на здоровом), а при чужой папке печатает одну строку «⚠️ ПАПКА НЕ РОДНАЯ… перезапустись из E:\…». Тест рядом, коммиты с отпечатком автора в трёх репо.
- По пути поймал и починил граблю: PowerShell-пайп подсовывает BOM в stdin, и JSON молча не парсился — сторож теперь BOM-устойчив (записал в [[deterministic-script-gotchas]]-класс).
- Раскатка: сами файлы доедут на все машины Syncthing-ом; регистрация хука пер-машинная, поэтому ноуту NODE-0X ушла посылка по шине (dual-send OK) с шагом установки и verify.
- Память: заметка `native-workdir-per-node` + строка в MEMORY.md.

**Что нам это даст:**
1. **Правильная память с первой секунды.** Сегодняшний случай — сессия на хабе 40 минут работала с памятью ноутбука и не знала о 1920 сессиях хаба. Теперь такая сессия узнаёт об этом первой строкой, а не случайно.
2. **Ошибка ловится в момент старта, а не в момент, когда «Claude что-то забыл».** Симптом «он не помнит, что мы решали» часто был именно этим классом, его теперь видно сразу.
3. **Ноль шума и ноль токенов.** На правильном старте хук не печатает ничего; это 0-LLM скрипт за миллисекунды.
4. **Класс закрыт, не случай:** правило работает для любого узла флота — добавление новой машины стоит одну строку в json.

🎙 Майк: эта сессия по-прежнему в чужой папке — доработаем в ней разговорное, но следующую рабочую на хабе открывай из `E:\!CLAUDE-HUBPC-June26`, и сторож сам подтвердит тишиной, что всё ок.

🧒 Простыми словами: мы повесили на дверь звоночек. Зашёл в свой кабинет — тихо. Зашёл по привычке в чужой — звоночек сразу говорит: «стоп, твои дневники не здесь, твой кабинет — вон та дверь». Больше не будет ситуаций, когда работаем полдня с чужими дневниками и удивляемся, почему ничего не помним.

---

**User:**

+ раскатай на остальные машины флота + ретро

---

**Claude:**

[⏰ понедельник, утро, 08:42, 24 августа 2026]

Принял: раскатка на весь флот по правильной рельсе (deploy_register с машинными apply/verify), потом ретро. Канарейка уже зелёная — хаб живёт с хуком, NODE-0X получил посылку. Сначала смотрю интерфейс deploy_register.

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\deploy_register.py\" --help 2>&1 | Select-Object -First 40", "description": "Show deploy_register.py usage"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\deploy_register.py", "limit": 80}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py", "content": "#!/usr/bin/env python3\n\"\"\"home_dir_guard_install.py — per-node installer/verifier for the home-dir-guard SessionStart hook.\n\nWhy: files (hooks/home_dir_guard.py|.cmd, home_dirs.json, the test) travel to 

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py\"; \"--- verify:\"; python \"C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py\" --verify; \"exit=$LASTEXITCODE\"", "description": "Run installer (should no-op on hub) and verify"}

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\deploy_register.py\" all home-dir-guard-2026-08-24 \"home-dir-guard: SessionStart-сторож чужой рабочей папки (регистрация хука в локальном settings.json)\" \"python ~/.claude/scripts/home_dir_guard_install.py\" \"python ~/.claude/scripts/home

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\deploy_register.py\" all home-dir-guard-2026-08-24 \"home-dir-guard: SessionStart-сторож чужой рабочей папки (регистрация хука в локальном settings.json)\" \"python3 ~/.claude/scripts/home_dir_guard_install.py\" \"python3 ~/.claude/scripts/ho

---

**Claude:**

Проверяю, что `python3` живёт и на Windows-узлах (иначе verify ляжет уже у них):

---

> `PowerShell` -- {"command": "python3 --version; python3 \"C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py\" --verify; \"exit=$LASTEXITCODE\"", "description": "Check python3 works on Windows hub"}

---

**Claude:**

Хаб свою посылку закрывает сам — прогоняю локальный sweep:

---

> `PowerShell` -- {"command": "ls \"C:\\Users\\dev\\.claude\\scripts\" -Filter \"deploy*\" | Select-Object Name", "description": "List deploy scripts"}

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\deploy_apply.py\" home-dir-guard-2026-08-24 2>&1 | Select-Object -First 15", "description": "Apply and close hub's own pending row"}

---

**Claude:**

Раскатка зарегистрирована и доказана на канарейке. Коммичу установщик и обновлённый реестр:

---

> `Bash` -- {"command": "TRAILERS=\"Assisted-by: Claude Code / claude-fable-5\nMachine: HUB-01\nAccount: a2\nOperator: dev\" && cd /c/Users/dev/.claude/scripts && git add home_dir_guard_install.py && git commit -q -m \"home_dir_guard_install: per-node apply/verify for the fleetwide deploy\n\n$TRAILER

---

**Claude:**

Раскатка готова. Теперь ретро — запускаю скилл.

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

**⏳ Measure the time-gap FIRST.** Check when this session's work actually happened (turnstate ledger / the digest's day-span) vs **now**. Old session → widen every lookup below to cover *"what changed SINCE"* — don't recall only the session's own window.

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
3. **Neighboring chats (lexical, 0 tok):** `/search <topic words>` (search_catalog.db, ~99k Telegram/FB/ChatGPT/Claude) — what did dev or another session **dictate elsewhere** about this topic?
4. **Vault meaning (RAG):** `/ask <topic>` (`$IMPORTS_ROOT/brain_ask.py`) — what does the Second Brain already hold / already decide on this?
5. **Memory + vault grep** for every rule/concept/decision this session touched — already captured? **superseded / changed** since?
6. **Peers & cross-machine:** `/inbox` + `_machine-bus` + consensus commits — "всё, о чём мы договорились" on the OTHER machines; did a peer already decide, or undo, this?
7. **Declined journal:** skill `/declined` — did we already reject something this session quietly re-did?

**Attribution guard:** the Step-1 inventory is machine-wide and WILL include other sessions' artifacts (skills/scripts/commits from the fleet). Treat anything NOT created in THIS conversation as **someone else's** — flag it, never claim or re-route it.

**Output of Step 0 — one tight «🔎 сверка» block up front** (checked + verdict):
- **checked:** what I actually looked at (N retros / chats / vault / peers).
- **✅ aligned** — this session's calls match the collaboration; or
- **⚠️ drift** — session did X but [[note/decision]] elsewhere says Y (superseded / contradicts / already undone) → flag for dev; or
- **🔗 to propagate** — session's durable work not yet in vault / peers / Bible → route it in Step 4.
If a parallel session already captured the durable item, **SKIP re-capturing** — just cross-link.

## Step 1 — Inventory (deterministic first; AK-47, ~free)
Ground the recap in facts, not memory alone — run the SHARED inventory script (same one the daily sweep uses, so the logic never drifts):
- `python "$IMPORTS_ROOT/retro_inventory.py" 1`  (arg = days; widen for a multi-day session)
- It prints `BUILT_ARTIFACTS <n>` and writes `$IMPORTS_ROOT/retro_candidates/digest-latest.md` — Read that digest: new/changed **skills**, **_imports scripts/sidecars**, **durable notes** (Protocols + Concepts), and recent **descriptive vault commits**.
- (⚠️ a concurrent Claude-Desktop fleet may interleave vault commits — its are descriptive; the terse `pre-intervention` ones are auto-backups.)
- **Cross-check** with what you (the agent) created/edited in THIS conversation: skills, scripts, vault notes, memory entries, `CLAUDE.md` edits, decisions made, rules captured, things flagged for dev.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже) и на каждую — ОДНА строка в `$OBSIDIAN_VAULT\00-System\Breakage-Journal.md`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. Затем СЧЁТЧИК по классу (`grep` по журналу, не по памяти): 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный → отдельная сессия починки** (5 почему по серии → ТРИЗ → АК-47). Механизм/робота на 1-2 случае НЕ строить.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · fail-closed гейты.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- Канон: Библия `reglament-mekhanizm-tolko-posle-tretey-polomki` + CLAUDE.md §5.10 + `reglament-pyat-pochemu-koren-po-serii-sessiy` §«Три инструмента»; проверка двери — `python ~/.claude/scripts/rule_home_guard.py mekhanizm-tolko-posle-tretey-polomki`.

## Step 2 — Summarize the arc ("сегодня мы поняли")
3–7 beats: starting idea → what got built → key realizations → what was decided. Honest, concise, his voice. This is the "Stan at the end of South Park" recap.

## Step 2🎙 — Вердикт кофаундера (Майк) — canon 2026-07-07, applied 2026-07-31
Right after the arc, Майк speaks as co-founder — 4 строки, без воды (canon `reglament-*` voice-through-line; восстановлен из потерянного сообщения шины, 23 дня в призраке; НЕ театр — работает ПОВЕРХ механики 28.07: если сессия дала стратегический выбор, мемо/адвокат-дьявола из [[cofounder-decision-artifact-gate]] главнее и уже сделаны):
- 💰 **деньги-линза** — что из сегодняшнего приближает выручку/оффер (цель №1/№2), одной строкой;
- 🔪 **что убил бы** — самая слабая трата времени сессии, которую завтра не повторяем;
- 🤺 **спарринг-аудит** — где я сегодня поддакнул вместо спора (провал роли §1.2) либо «спорил честно»;
- ❓ **вопрос** — один направляющий вопрос оператору на завтра.
Пустышку не писать: сессия чисто механическая без бизнес-среза → строка «🎙 Майк: бизнес-среза нет, чисто инфра» и дальше.

## Step 3 — Classify each artifact (Keep / Drop / Try) + tested? audit
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]). Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3📋 — Journal sync (реестр задач; dev's decree 2026-07-04)
Retro is the SAFETY NET of the task journal ([[task-journal-done-undone-linking]]): the in-session reflex («сформулировал → сразу в реестр») catches tasks at birth; retro catches what slipped. Two moves, both against the ONE journal ([[task-backlog-registry]] — **v2 markdown-first, SHIPPED 2026-07-07**):
- **Источник истины = markdown-заметки** `$OBSIDIAN_VAULT/10-Tasks/task-*.md` (шаблон `_Task-Template.md`, MOC `_Tasks-MOC.md`). Синкаются флоту, поэтому работают с ЛЮБОЙ машины без шины и без движка. Завести задачу = новый файл `task-ГГГГ-ММ-ДД-слаг.md`; закрыть = правка frontmatter (`state`/`status` + evidence). Схема строгая: неизвестный `state`/`prio` → `schema_errors` в аудите, а не тихий дефолт.
- **Витрину и аудит строит индексатор** `tasks_index.py` (markdown → `_Dashboards/Task-Backlog.html` + `10-Tasks/_audit/audit-latest.json`). Он крутится ночью на Маяке как ЕДИНСТВЕННЫЙ писатель — руками на хабе/ноуте его НЕ запускать (два писателя одного синкаемого дерива = sync-conflict).
- ⛔ Старый SQLite-движок task-registry (жил на ноуте NODE-0X) = **аварийный fallback, снят с вооружения**; на хабе его нет и не должно быть. Не зови его и не «восстанавливай» — v2 его заменил. (Имя намеренно без code-формата: backtick = «это надо запускать».)

Две операции ретро:
- **Сессия рождена из сида Task-Now?** (первое сообщение начинается «Продолжи задачу task-…» или «Реши СУДЬБУ задачи task-…») → обнови frontmatter ЭТОЙ задачи прямо сейчас: state/touched_at, при done — evidence+outcome; сид без обновлённого frontmatter = петля Task-Now разорвана (v4, dev 2026-08-20).
- **Closed this session** → mark `done` **with evidence** (the /tt proof, commit, counter) + link what it unblocked. Claimed-done without proof → flag, don't close.
- **Still open** (every «📌 Open item», seed prompt, deferred tail, «потом») → ensure it EXISTS in the registry with a link to where it was born + prio/type. Nothing from the open-items list may live only in the chat transcript.
Announce the delta in one line: «📋 журнал: +N новых · ✅M закрыто · без изменений K». Don't duplicate neighbor registries (DR-реестр, improvements-backlog, declined) — link, не копируй.

## Step 3🗺 — Roadmap checkpoint (dev's decree 2026-07-16: «в каждом ретро — как мы продвинулись по roadmap»)
Канон = `$OBSIDIAN_VAULT/04-Projects/ROADMAP.md` (живой публичный роадмап для фолловеров). Три движения, все против ЭТОГО файла:
- **Продвинулись** → отметить чекбоксы/статусы, веху уровня «фолловеру интересно» → строка в Ship log с датой.
- **Появилось новое направление в сессии** → добавить в NOW/NEXT/LATER (не дублируя детальные планы — ссылкой).
- **Ничего не двинулось** → честно сказать это в отчёте (тоже сигнал).
Announce одной строкой: «🗺 roadmap: ✅N продвинуто · ➕M добавлено · ⏸ без движения». Публичная проекция файла наружу — только через контент-гейт (Нора), ретро наружу не постит.

## Step 3🔗 — Connect check (построено → передано → ИСПОЛЬЗУЕТСЯ?) — dev 2026-07-04
Правило Connect ([[connect-rule-pipeline-ownership]]) на подведении итогов: для КАЖДОГО артефакта этой сессии довести цепочку до конца — **«собрали» это ещё НЕ финиш**. Финиш = построено → передано потребителю → **реально используется**. Три исхода на артефакт:
- ✅ **используется** — есть потребитель и он потребляет (скилл вызывают, рутина читает выход, поле CRM читают, дашборд открывают, данные доехали и применены). **Назвать потребителя** — иначе это не ✅.
- 🔗 **передано, потребления пока нет** — доехало, но никто ещё не читает/не применяет → на доску висячих, назначить потребителя/срок.
- ⚠️ **построено «в воздух»** — собрали и бросили, потребителя нет вовсе (dead-letter без consumer — как релинк-очередь: 29k сирот, 0 применено) → **ПОДСВЕТИТЬ оператору явно**: «построили X, но это никем не используется» → решить: подключить потребителя ИЛИ признать выброшенным.

Молчание ≠ используется. «Построили» без названного потребителя = недоделанный Connect, НЕ «done». Строкой: «🔗 Connect: ✅N используется · 🔗M передано-ждёт · ⚠️K в воздух».
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` = сейчас + 1-2 мин, разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro).

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].

## Step 4★ — The «repeats → make a skill» reflex (milestone closeout)
This is the step dev asked for (2026-06-18): at a finished milestone, don't just *note* a repeating action — **offer to turn it into a skill**. It's the retro-time expression of the standing rule `evaluate-recurring-into-routine` (повторяющаяся задача → оцени «на рутину?»). Mirror of [[capture-rules-into-bible]] (that catches *rules*; this catches *tasks-to-automate*).

**Trigger (catch it, don't wait to be asked):** any action that **repeated ≥2–3×** this session/milestone, OR that we'll **clearly return to** later (a manual sequence I re-typed, a multi-step procedure, a recurring check).

**Procedure — 4 cheap moves:**
1. **RECALL first — don't duplicate.** Skim the available skills + memory `automation-inventory` for an existing skill/routine/hook that already covers it. If one exists, point dev to it instead of building a twin. **⛳ И тут же второй вопрос (dev hub:5090, 2026-08-04): скилл ЕСТЬ — не проапгрейдить ли его?** «Есть» ≠ «закрыто»: назови, чего ему не хватило ИМЕННО в этой сессии (шаг, который я делал руками поверх скилла / грабли, которых в нём нет / устаревшая строка) → правка в тот же заход, и это тоже строка в 🔁→🛠 (`built/proposed/declined`). Нечего добавить — скажи это словом, молчание = проверка не сработала. Дословный текст вопроса и формат ответа — единственный источник в `/skill-gap` §⛳ (там же — вход-конец рефлекса).
2. **⚠️ AK-47 guard — a skill is just a `SKILL.md`.** One markdown file with a procedure, NOT a server / DB / webhook / external service. (This is the exact trap the Codex milestone-retro report fell into — over-engineered for a SWE team; rejected 2026-06-18.) If the thing genuinely needs more than a markdown procedure, flag it **⚠️ УСЛОЖНЕНИЕ** and let dev decide.
3. **OFFER as ДО→ПОСЛЕ** (per `show-before-after`) — one compact block:
   > **ЧТО:** собрать `/<имя-скилла>` · **ДО:** как делаю руками сейчас (на реальном примере этой сессии) · **ПОСЛЕ:** одна команда `/<имя>` · **что сломается:** ничего (надстройка) · **делаем? да/нет**
4. **On dev's «+» → build it via `skill-creator`.** Pick the right home by SHAPE (per `operating-agreement` → «Where durable rules go»):
   - on-demand ritual I run when asked → **skill** (`skill-creator`).
   - «каждый раз автоматически когда X» → **hook** (skill `update-config`), not a skill.
   - time-based «каждый понедельник / каждое утро» → **scheduled task / routine** (skill `schedule`).
   - «рутина» ≠ обязательно 24/7-робот — часто правильное = простой полуавто + напоминание.
   - ⭐ **СПИСОЧНАЯ работа на N кусков (N велико) → КОНЕЧНАЯ рутина, «слон»** (dev 23.08, §4.5-бис).
     Признак: в сессии я перебирал однотипные элементы (видео / заметки / карточки / островá графа /
     ссылки), список не кончился, и он не кончится и в следующий раз; либо задача уже месяцами
     спотыкается об участие оператора, лимиты вендора или баны. Это НЕ задача и НЕ героическая сессия —
     это слон: `python ~/.claude/scripts/elephant.py new <slug> --title T --quota N --os-task <ЗадачаWindows>`,
     дальше рабочий скрипт на каждом прогоне делает `next` → работа → `mark` → `tick`.
     `tick` сам ловит конец (выключает OS-задачу + доклад в TG-03) и затык (5 пустых прогонов → `blocked`).
     ⛔ Журнал слона НИКОГДА не кладём в синкаемую папку — затрётся, и слон не кончится никогда.
     Живой пример: [[yt-watch-history-drip]]. Канон: [[finite-routines-eat-the-elephant]].
   Then route/link it normally (Step 4) and mention it in the final report (post-hoc, not for permission).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the ready `/compact` line (Step 6).
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Write a clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- The nightly **Brain Reindex @04:00** makes it `/ask`-searchable — no manual reindex needed.

**6a-бис. Снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- Команда: `python %USERPROFILE%\.claude\scripts\retro_lost_scan.py mark-done <sessionId> --note "ретро: <имя заметки>"`
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6b. Hand dev the ready paste-block** — ⚠️ CORRECTED 2026-07-22: bare `/compact` does NOT read `CLAUDE.md § Compact Instructions`. That earlier claim was FALSE — PreCompact hooks cannot inject instructions (only block; issue #14160 pending), and the evidence is 354/354 past compacts came out in the DEFAULT English template. Our 7-header format is applied ONLY when the block is pasted INLINE after the command: `/compact <text>`. So PRINT the fenced «Готовая строка» block from `$USERPROFILE/.claude/compact-prompt.md` and tell dev to PASTE it right after `/compact`. Then the fork:
> **«Готово, всё в волте. Хочешь остаться в задаче налегке — ВСТАВЬ блок ниже целиком после `/compact` (без него сжатие пойдёт по дефолтному английскому шаблону, не по нашему 7-заголовочному). Или новый чат — всё уже заархивировано, не зависит от нажатия.»**
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; the squeeze + paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

---

**Claude:**

Ретро. Сначала детерминированная часть: сверка, инвентарь, ON AIR, аудит раскатки.

---

> `Bash` -- {"command": "export IMPORTS_ROOT=\"D:/Vault/_imports\"; python \"$IMPORTS_ROOT/turnstate/turnstate_show.py\" 2>&1 | tail -25; echo \"=== RETROS:\"; ls \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/\" | tail -5; echo \"=== ONAIR:\"; python /c/Users/dev/.claude/scripts/onair.py lis

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; grep -ci \"BOM\" \"$J\"; grep -ci \"чуж.. папк\\|foreign.*cwd\\|не родн\" \"$J\"", "description": "Count prior journal cases for BOM and foreign-cwd classes"}

---

**Claude:**

BOM-класс уже имеет 2 строки — если мой случай тот же корень, это 3-й датированный → системный. Читаю строки:

---

> `Bash` -- {"command": "grep -i \"BOM\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"", "description": "Read prior BOM journal lines"}

---

> `Bash` -- {"command": "cat >> \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" << 'EOF'\n- 2026-08-24 ~08:35 (хаб HUB-01, сессия 6270af26) · **1-й случай класса «сессия открыта в ЧУЖОЙ рабочей папке → молча грузится чужая память»**: сессия хаба шла в ноутбучном проекте `!CLAUDE-NODE-0X May26`

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-home-dirs-selfreport.md", "content": "---\ntitle: \"home_dirs.json: дописать родные рабочие папки остальных узлов (Маяк, Mac-dev, Nora, Rita)\"\nstate: open\nprio: P2\ntype: infra\nowner: claude\nmachine: fleet\nborn: \"

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-home-dirs-selfreport.md", "content": "---\ntitle: \"home_dirs.json: дописать родные рабочие папки остальных узлов (Маяк, Mac-dev, Nora, Rita)\"\nstate: open\npriority: P2\nprio: P2\ntype: infra\nowner: claude\nmachine: f

---

> `Bash` -- {"command": "grep -n \"home-dirs\\|2026-08-24\" \"D:/Vault/Vault-Knowledge/10-Tasks/_Tasks-MOC.md\" | head -5; grep -n \"## \" \"D:/Vault/Vault-Knowledge/10-Tasks/_Tasks-MOC.md\" | head -10", "description": "Find where to wire the task into Tasks MOC"}

---

> `Bash` -- {"command": "python - << 'EOF'\np = r\"D:\\Vault\\Vault-Knowledge\\10-Tasks\\_Tasks-MOC.md\"\ns = open(p, encoding=\"utf-8\").read()\nanchor = \"- [[task-2026-08-24-codex-pilot-svod]] - свод Codex-пилота девочек, владелец хаб, 24.08\"\nline = \"\\n- [[task-2026-08-24-home-dirs-selfreport]] - допи

---

**Claude:**

Теперь заметка-ретро в волт и снятие сессии с очереди retro-lost:

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-08-24-home-dir-guard-native-workdir.md", "content": "---\ntitle: \"Retro: home-dir-guard — сторож родной рабочей папки узла\"\naliases: [\"Ретро: сторож чужой рабочей папки (24.08.2026)\"]\ndate: 2026-08-24\nt

---

> `Bash` -- {"command": "python - << 'EOF'\np = r\"D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-home-dirs-selfreport.md\"\ns = open(p, encoding=\"utf-8\").read()\nadd = \"\\n\\nРодился из [[retro-2026-08-24-home-dir-guard-native-workdir]].\\n\"\nif \"retro-2026-08-24-home-dir-guard\" not in s:\n    

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\compact-prompt.md"}

---

**Claude:**

[⏰ понедельник, утро, 08:42 → ретро закрыто к 08:56, 24 августа 2026]

Раскатка на флот сделана, ретро проведено и заархивировано.

**Раскатка (§7.3-бис):**
- Написан кросс-платформенный установщик [home_dir_guard_install.py](C:\Users\dev\.claude\scripts\home_dir_guard_install.py): apply идемпотентно регистрирует хук в локальном settings.json (с бэкапом и re-parse перед заменой), `--verify` читает факт (регистрация + тест). Гейт deploy_register поймал мою граблю «python вместо python3 умрёт на маках» — исправил.
- Манифест `home-dir-guard-2026-08-24` (tier 1) зарегистрирован на **все 6 узлов**; хаб-канарейка применил и доказал: `✅ applied (ДОКАЗАНО verify)`. Остальные 5 подберут своими inbox-рутинами (2×/сутки), табло — `fleet_fix_audit.py --by-fix home-dir-guard-2026-08-24`.
- Родные папки Мака, Маяка, Норы и Риты хабу неизвестны — заведена задача [task-2026-08-24-home-dirs-selfreport](D:\Vault\Vault-Knowledge\10-Tasks\task-2026-08-24-home-dirs-selfreport.md): установщик на каждом узле сам печатает подсказку, узел дописывает свою строку. До этого сторож там молчит (не ложнит).

---

**🎬 Сегодня мы поняли:** простой вопрос «какую папку выбирать» вскрыл системный дефект — память Claude Code привязана к рабочей папке, и сессия хаба молча жила с памятью ноутбука (179 сессий вместо родных 1920). За сессию: реестр родных папок + SessionStart-сторож (0 LLM, молчит когда здоров) + тест + раскатка на весь флот по deploy-рельсе.

**🎙 Майк:** 💰 напрямую денег не приносит, но чинит фундамент recall — а битый recall портил и лидов, и контекст; 🔪 убил бы мой первый ручной bus-parcel на NODE-0X — через 20 минут его накрыл штатный deploy-манифест, дубль; 🤺 спорил честно с гейтами (deploy-блок python→python3 принял по улике, не из вежливости); ❓ вопрос: на новых узлах флота папку-«кабинет» будем задавать при онбординге (строка в persona-kit?) — или пусть каждый self-report-ит как сейчас?

**♻️ Reuse:** 4 артефакта 🟢 Keep, все tested ✅ (хук+тест, реестр, установщик) — таблица в ноте-ретро.

**🩹 Поломки:** 2 строки в Breakage-Journal — «чужая папка = чужая память» (1-й случай, механизм построен тем же заходом) и BOM-в-stdin от PowerShell-пайпа (2-е касание семьи «PS-кодировка врёт прибору», порог 3 не достигнут, механизм не строю).

**🔗 Connect:** ✅1 используется (хук живёт в SessionStart хаба, DONE доказан) · 🔗5 передано-ждёт (узлы, законное ожидание inbox-рутин) · ⚠️0 в воздух. Правило `native-workdir-per-node`: дверь реальная и исполнимая (сам хук), след в always-loaded есть (rule_home_guard: инвариант ✅). Контрибьют-тест: ⛔ пока нет — боль нишевая (мульти-машинный флот с Syncthing), чужие треды не проверял; кандидат в `/release-slice` при случае.

**⛳ Дрифт:** цель = «выбрать папку → хук → раскатка» — дрифта нет. Параллельная сессия bca44929 дополнила реестр исключениями (worktrees, Temp) — сверено, конфликтов нет.

**📋 Журнал:** +1 новая (home-dirs-selfreport, P2) · закрытых нет (раскатка живёт в deploy-табло, не дублирую). **🗺 Roadmap:** ⏸ без движения — внутренняя инфра, фолловеру не веха. **🎬 Контент:** тизер захвачен в воронку черновиком (`cc:live-9a30e9`, «сессия в чужой папке = чужая память»).

**🗜 Compact handoff:** нота-ретро сохранена — [retro-2026-08-24-home-dir-guard-native-workdir](D:\Vault\Vault-Knowledge\01-Conversations\Claude\Retros\retro-2026-08-24-home-dir-guard-native-workdir.md), сессия снята с очереди retro-lost. Хочешь остаться в этом чате налегке — вставь блок ниже целиком сразу после `/compact` (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — тоже безопасно, всё уже в волте.

```text
При /compact сохрани ДОСЛОВНО по 7 заголовкам (обоснования исчезают первыми):
- РЕШЕНИЯ — что решили + ПОЧЕМУ (что отвергли; «делаем / НЕ делаем»)
- TODO — задачи с приоритетами
- СЕЙЧАС — что делаем прямо сейчас + следующий шаг (активная ошибка/состояние)
- ПУТИ И ЗНАЧЕНИЯ — файлы/скрипты/папки + точные значения (имена заметок/MOC, frontmatter, ID чатов/баз, БД, env, константы)
- СЧЁТЧИКИ — итоговые числа самопроверки + что НЕ доделано
- ОТКРЫТО — что сломалось/осталось/расходится (⚠ грабли, баги+симптомы)
- ИНСТРУМЕНТЫ И КОНТРАКТЫ — скрипты _imports/scheduled-tasks/MCP · версии · API/форматы
Сожми: что работает — 1 строка + компоненты по именам. Выкинь: отладку, тупики, логи, переформулировки.
```

🧒 Простыми словами: звоночек с двери мы сегодня повесили не только у себя, а разослали на все шесть компов семьи — каждый сам прикрутит его при ближайшей проверке почты, а четырём осталось лишь сказать, где их «родной кабинет». Потом сели и записали в дневник: что построили, что сломалось по пути, что оставляем навсегда. Ничего не потерялось — всё лежит в большой библиотеке.
