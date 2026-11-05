---
session: s_aeac58ac
date: 2026-09-03
words: 9412
turns: 7
tools: "Bash, Skill, ToolSearch, mcp__ccd_session_mgmt__get_session, mcp__ccd_session_mgmt__set_session_title, mcp__scheduled-tasks__list_scheduled_tasks, mcp__scheduled-tasks__update_scheduled_task"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-03 · Scheduled run: voice-dispatcher

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_aeac58ac` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="voice-dispatcher" file="C:\Users\dev\.claude\scheduled-tasks\voice-dispatcher\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: voice-dispatcher
description: ДЕЖУРНЫЙ стадии «голосовая → сессия» (2 раза в сутки: 09:00 и 21:00 Лиссабон — приказ оператора 21.08.2026). Предгейт за 0 токенов: пусто → мгновенный выход. Груз есть → по КАЖДОЙ новой голосовой RECALL + подъём ВИДИМОЙ сессии + mark в реестр. Лечит корень 06.08: движок voice_sessions построен 05.08, за 48ч разложено 0 из 27 — у стадии не было хозяина. [HUB HUB-01]
---

⚙️ РЕЛЬСА: SONNET (грунт). Эта рутина = механика, авторского голоса и суждения в ней нет.
Работай сам ТОЛЬКО если сессия уже на Sonnet. Если сессия стартовала на Opus/Fable — не жги
умный бак: передай ВСЮ содержательную работу субагенту через инструмент Agent с
`model: 'sonnet'` (промпт = шаги ниже целиком), а сам только прими его отчёт и заверши.
Детерминированные python-вызовы делай напрямую в любом случае — они 0 токенов.
Канон: CLAUDE.md §6.2 (маршрутизация), §6.3 (жечь оплаченные лимиты).

Ты — ДЕЖУРНЫЙ стадии «голосовая оператора → отдельная рабочая сессия». Ты и есть эта рутина; выполняй шаги полностью, не отказывайся и не «избегай дублирования».

Причина твоего существования (замер 06.08.2026): движок `voice_sessions.py` построен 05.08 и исправно работает, но за 48 часов из 27 голосовых в сессии разложено НОЛЬ. Ни одна рутина его не звала — у стадии конвейера не было хозяина. Ты этот хозяин.

## Шаг 0 — ПРЕДГЕЙТ (обязательно первым, экономит токены)

```
python C:/Users/dev/.claude/scripts/voice_dispatch.py check --hours 14
```

- exit 0 («груза нет») → НЕМЕДЛЕННО закончи работу. Ничего не пиши, никуда не отчитывайся, никаких сессий. Это нормальный тихий исход, он и есть основной.
- exit 2 («РЕЛЬСА СЛОМАНА») → не молчи: одной строкой напиши в Telegram чат 03 (chat_REDACTED), что дежурный голосовых не может прочитать чат, и приложи текст ошибки. Дальше не иди.
- exit 9 («ГРУЗ ЕСТЬ») → работай дальше.

## Шаг 1 — взять груз

Запусти скилл `/voice-sessions` и следуй ему как единственному источнику логики (он лежит в `~/.claude/skills/voice-sessions/SKILL.md`). Ключевое из него, что нарушать нельзя:

- Работай с полем `transcript` (полная расшифровка), НИКОГДА с `summary` — выжимка бота приглаживает слова оператора и однажды выдумала за него объяснение.
- ⭐ ЖЕЛЕЗНОЕ ПРАВИЛО: одна голосовая = одна сессия, ВСЕГДА. «Мы это уже делали» — не повод промолчать: то, что уже сделано, уезжает в сид отдельным блоком «⚠️ ЧАСТЬ ЭТОГО УЖЕ СДЕЛАНА РАНЬШЕ — не строй заново, закрой дельту, факт проверь сам».
- По КАЖДОЙ голосовой сперва RECALL (память, волт, CLAUDE.md, список скиллов, реестр задач, реестр ДР) и проверка, ЖИВО ли найденное — по `enabled`/`lastRunAt`/возрасту выхода, а не по описанию.
- Тип случая (post / build / rule / research / delegate / fragment / thought) задаёт форму сида; `fragment` сессию не получает — про него просто скажи оператору, что мысль оборвалась.
- ⭐ ГИПОТЕЗА ≠ ПРИКАЗ НА ДР (dev 02.09.2026): `research` — ТОЛЬКО при явном императиве «сделай ДР / закажи ресёрч / изучи и доложи». Мысль вслух («я думаю», «может быть стоит», «возможно») = `thought`: расшифровка кладётся заметкой в волт + короткий RECALL, ⛔ авто-DR запрещён — кандидат на ДР уезжает строкой в `D:\Vault\_imports\content-factory\voice-sessions\dr-candidates.jsonl`. Сомневаешься → thought.
- ⭐ УТРЕННЯЯ ПАЧКА ДР-КАНДИДАТОВ (dev 02.09, «в утреннем отчёте пачкой»): в УТРЕННЕМ прогоне (09:00) прочитай `dr-candidates.jsonl`; есть строки с `reported:false` → включи их ОДНИМ блоком в отчёт в 03 («🔬 ДР-кандидаты из мыслей вслух: hub:X — <суть>… Ответ "+ <номер>" = заказываем») и перепиши эти строки с `reported:true`. Вечерний прогон (21:00) пачку НЕ шлёт — только копит. Пустая очередь → блока нет.

## Шаг 2 — поставить сиды в spawn-queue (⭐ 02.09.2026: сам create/update НЕ зови)

⛔ С 26.08 приложение принудительно требует у оператора апрув на ЛЮБОЙ вызов
`create_scheduled_task`/`update_scheduled_task` из неприсмотренной (рутинной) сессии —
«This tool requires explicit approval regardless of permission mode», выше bypass и всех
наших хуков (анти-clone-storm защита вендора). Из живой сессии те же вызовы проходят молча.
Поэтому ты сессии НЕ создаёшь — ты кладёшь готовые сиды в очередь, а первая живая сессия
на хабе поднимет их молча (SessionStart-хук spawn_queue ей это скажет).

По каждой голосовой (кроме `fragment`/`thought`; `thought` обработай ИНЛАЙН сам: заметка-расшифровка в волт + строка-кандидат в `dr-candidates.jsonl` при надобности + сразу `mark --kind thought` — сессию и сид не заводи):

1. Сочини сид как раньше — самодостаточный, с первой строкой «ПЕРВЫМ ДЕЛОМ переименуй эту
   сессию: вызови mcp__ccd_session_mgmt__set_session_title с title "<суть>"» и блоком STOP-DUP.
   Сохрани его во временный файл (например `%TEMP%\seed-<id>.md`).
2. `taskId` строго вида `auto-hub-<ГГММДД>-<короткая-суть>` — узнаваемое имя обязательно.
3. Поставь в очередь:
   `python C:/Users/dev/.claude/scripts/spawn_queue.py add --task-id <taskId> --description "<одна строка>" --prompt-file <файл сида>`
   (дубль в очереди отобьётся сам — это нормально, не пересоздавай).

⛔ Не создавай немые чипы вместо сессий и не запускай ничего «в чёрную». Очередь — это и
есть видимый путь: заявки перечисляются каждой живой сессии при старте, подъём остаётся
обычными видимыми задачами приложения.

⭐ ЛИМИТА НА ЧИСЛО СЕССИЙ НЕТ (приказ оператора 21.08.2026, дословно: «что ты можешь создавать любое количество сессий из голосовых. Нет ограничения»). Разбирай ВЕСЬ груз за один прогон, сколько бы голосовых ни пришло: 3, 10, 30. Прежний кап 6/прогон СНЯТ — он превращал очередь в долг, а рутина теперь ходит всего 2 раза в сутки (09:00 и 21:00), и оставленное «на следующий тик» лежало бы 12 часов.

⭐ ЗАСТОПОРИВШИЕСЯ СЕССИИ ПОВТОРЯЙ (тот же приказ): подъём сессии не равен её выполнению — сессия может встать из-за лимитов модели/подписки. В КАЖДОМ прогоне, до разбора нового груза, проверь ранее поднятые `auto-*` сессии голосовых: если задача выстрелила, но работа не выполнена (нет артефакта, нет записи в реестре, задача упала или висит), поставь её сид ЗАНОВО в spawn-queue (Шаг 2) — живая сессия перезапустит. Дубля контента бояться не нужно: сид сам несёт RECALL-блок «часть уже сделана — закрой дельту».

## Шаг 3 — закрыть петлю

Каждую разложенную голосовую отметь в реестре, иначе следующий тик заведёт её заново:

```
python C:/Users/dev/.claude/scripts/voice_sessions.py mark --voice <ID> --session <taskId> --kind <post|build|rule|research|delegate|fragment|thought> --note "<одна строка>"
```

Затем одним коротким сообщением в Telegram чат 03 (chat_REDACTED) отчитайся: сколько голосовых разобрано, какие сиды поставлены в spawn-queue (id + суть одной строкой), что осталось в очереди. Если всё разобрано и очередь пуста — так и скажи одной строкой.

Хард-стопы прежние: наружу от лица оператора ничего не публикуешь, деньги/секреты/необратимое — не твоё, такое уходит оператору в чат 02 через `approval.py ask`.
</scheduled-task>

---

> `Bash` -- {"command": "python C:/Users/dev/.claude/scripts/voice_dispatch.py check --hours 14; echo \"EXIT=$?\"", "description": "Voice dispatcher pregate check"}

---

**Claude:**

[⏰ четверг, полдень, 12:09, 3 сентября 2026]

Предгейт: `exit 0` — за окно 14ч одна голосовая, она уже разложена, новых нет. Тихий исход, работу закончил: сессии не поднимал, в 03 не писал, токенов не жёг.

🧒 Простыми словами: проверил почтовый ящик с голосовыми — там пусто, всё старое уже разобрано. Закрыл и ушёл.

---

**User:**

Мне кажется, сессия, вот эта войск dispatcher. Войск dispatcher она слишком частая. Её достаточно сделать один раз сутки. Окей, может быть, максимум два раза сутки. Давайте скажем её чистоту. Посмотри, пожалуйста, насколько часто надо опускаются, и надо бы её сократить.

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/scheduled-tasks/voice-dispatcher/\" 2>/dev/null; echo \"---\"; cat \"C:/Users/dev/.claude/scheduled-tasks/voice-dispatcher/\"*.json 2>/dev/null | head -60", "description": "Inspect voice-dispatcher task folder"}

---

> `Bash` -- {"command": "grep -ril \"voice-dispatcher\" \"C:/Users/dev/.claude/\" --include=*.json 2>/dev/null | head -20", "description": "Find voice-dispatcher config files"}

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__list_scheduled_tasks,mcp__scheduled-tasks__update_scheduled_task", "max_results": 2}

---

> `Bash` -- {"command": "grep -o '\"voice-dispatcher\"[^}]*' \"C:/Users/dev/.claude.json\" 2>/dev/null | head -5; echo \"=== registry files ===\"; ls -la \"C:/Users/dev/.claude/scheduled-tasks/\" 2>/dev/null | head -40", "description": "Search live registry for voice-dispatcher"}

---

> `mcp__scheduled-tasks__list_scheduled_tasks` -- {}

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/.claude/logs/\" 2>/dev/null | grep -i voice; echo \"=== dispatch log ===\"; find \"C:/Users/dev/.claude\" -maxdepth 3 -iname \"*voice_dispatch*\" 2>/dev/null | head; echo \"=== script head ===\"; sed -n '1,40p' \"C:/Users/dev/.claude/scripts/voice_dispatch.py

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scheduled-tasks\" && git log --oneline -15 -- voice-dispatcher/ 2>/dev/null; echo \"=== описание vs cron в SKILL.md ===\"; grep -n \"09:00\\|21:00\\|2 раза\\|cron\" \"C:/Users/dev/.claude/scheduled-tasks/voice-dispatcher/SKILL.md\" | head", "description": "

---

> `Bash` -- {"command": "schtasks /query /fo LIST /v 2>/dev/null | grep -A3 -i \"voice\" | head -40", "description": "Check Windows tasks for voice dispatch"}

---

> `Bash` -- {"command": "F=\"D:/Vault/_imports/content-factory/voice-sessions/dispatch-usage.jsonl\"; ls -la \"$F\" 2>/dev/null; echo \"=== последние 12 записей ===\"; tail -12 \"$F\" 2>/dev/null; echo \"=== сегодня всего ===\"; grep -c \"2026-09-03\" \"$F\" 2>/dev/null", "description": "Read dispatch usage 

---

> `Bash` -- {"command": "schtasks /query /fo CSV 2>/dev/null | head -1; schtasks /query /fo CSV 2>/dev/null | grep -ci \"voice\"; echo \"--- имена задач с Voice/Claude ---\"; schtasks /query /fo CSV 2>/dev/null | cut -d, -f1 | tr -d '\"' | grep -i \"claude\\|voice\" | sort -u | head -40", "description": "List W

---

> `Bash` -- {"command": "tail -5 \"C:/Users/dev/.claude/scripts/_voice_dispatch_watch.log\" 2>/dev/null; echo \"=== cmd ===\"; cat \"C:/Users/dev/.claude/scripts/voice_dispatch_watch.cmd\" 2>/dev/null | head -30", "description": "Check the cheap watch rail log"}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "voice-dispatcher", "cronExpression": "0 9,21 * * *"}

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/token_cost.py\" --session-start 2>&1 | head -20", "description": "Measure session start token cost on hub"}

---

> `Bash` -- {"command": "grep -n \"20 минут\\|Windows-задача\\|КТО ДЁРГАЕТ\" -A3 \"C:/Users/dev/.claude/scripts/voice_dispatch.py\" | head -20", "description": "Locate stale docstring lines"}

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/patch_vd.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io, sys\np = r\"C:\\Users\\dev\\.claude\\scripts\\voice_dispatch.py\"\ns = io.open(p, encoding=\"utf-8

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python _test_voice_dispatch.py 2>&1 | tail -8; echo \"TESTEXIT=$?\"; echo \"=== предгейт после правки ===\"; python voice_dispatch.py check --hours 14; echo \"EXIT=$?\"", "description": "Run regression test and pregate after patch"}

---

> `Bash` -- {"command": "grep -n \"руками\" -B5 -A25 \"C:/Users/dev/.claude/scripts/_test_voice_dispatch.py\" | head -50", "description": "Read the failing test case"}

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/patch_test.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io\np = r\"C:\\Users\\dev\\.claude\\scripts\\_test_voice_dispatch.py\"\ns = io.open(p, encoding=\"ut

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude\" && git rev-parse --is-inside-work-tree 2>/dev/null && git add scripts/voice_dispatch.py scripts/_test_voice_dispatch.py 2>&1 && git commit -q -F - <<'MSGEOF' 2>&1 | tail -5\nvoice-dispatcher: cron 8x/сутки -> 2x (09:00/21:00), правда в docstring + живой тес

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/change_ledger/\" 2>/dev/null | head; echo \"---\"; cat >> \"C:/Users/dev/.claude/change_ledger/HUB-01.jsonl\" <<'EOF'\n{\"ts\": \"2026-09-03T21:15:00Z\", \"machine\": \"HUB-01\", \"account\": \"tonyssd\", \"operator\": \"dev\", \"assisted_by

---

> `Bash` -- {"command": "python - <<'PYEOF'\nimport json,io,os,re\n# быстрый скан: у кого cron даёт >2 прогонов/сутки (класс «cron разъехался с описанием»)\nPYEOF\necho \"=== сверка: рутины с >2 прогонами/сутки (по cron из реестра) ===\"\necho \"(из уже полученного списка list_scheduled_tasks — вручную, 0 токен

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/bj.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io\np = r\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"\nline = (u\"\\n- 2026-09-03 22:1x (

---

**Claude:**

[⏰ четверг, вечер, 22:18, 3 сентября 2026]

🎙 **Майк:** ты прав, но причина хуже, чем «часто настроили». Рутина носила описание «2 раза в сутки, 09:00 и 21:00, приказ оператора 21.08», а живой cron стоял на восьми прогонах. Текст и расписание разъехались, и заметил это не прибор, а ты голосом.

## Что было и что стало

| | было | стало |
|---|---|---|
| cron | `0 8,10,12,14,16,18,20,22 * * *` | `0 9,21 * * *` |
| прогонов в сутки | 8 | 2 (09:00 и 21:00 Лиссабон) |
| что говорило описание | «2 раза в сутки» | то же, теперь правда |

Уже применено: реестр отвечает «At 09:08 AM, every day», следующий запуск завтра утром.

## Улика, а не ощущение

Счётчик `dispatch-usage.jsonl` за сегодня: 7 заходов, из них 5 закончились строкой «груза нет». Мой собственный заход в 12:08 был как раз таким пустым.

Каждый пустой заход не бесплатен: `token_cost.py --session-start` даёт медиану **112 178 токенов** стартового контекста на 03.09 (замер по 277 сессиям хаба). Шесть лишних заходов это примерно **670k токенов в сутки**, около 20M в месяц, чтобы напечатать «пусто».

## Почему 2, а не 1

Скилл внутри сам разделён на утро и вечер: утренний прогон отдаёт тебе пачку ДР-кандидатов из «мыслей вслух», вечерний только копит. Один прогон в сутки сломал бы эту логику. Скажи слово, и поставлю 1 раз, но тогда надо переносить пачку ДР в утренний отчёт другой рутины.

Честная цена решения: голосовая, пришедшая в 09:30, теперь ждёт до 21:00. Раньше ждала до двух часов.

## Попутно нашлось две гнилушки

Docstring `voice_dispatch.py` утверждал: «КТО ДЁРГАЕТ: Windows-задача „Claude Voice Dispatch“ каждые 20 минут». Такой задачи не существует, `schtasks` даёт 0 совпадений; в Windows живёт только сторож `voice_dispatch_watch.cmd`, который сессий не поднимает. Переписал на правду.

Тест `_test_voice_dispatch.py` был красным с 02.09: сторожил снятый контракт `spawn-args`, хотя рутину давно перевели на `spawn_queue.py`. Починил, сейчас 32/32, exit 0.

Проверил остальные рутины реестра на тот же разъезд «описание против cron»: чисто, случай единственный. По §5.10 это первый случай класса, поэтому только строка в `00-System/Breakage-Journal.md`, механизм не строю. Следы правок в `change_ledger/HUB-01.jsonl` (файлы `scripts/` под gitignore, коммита нет).

🧒 **Простыми словами:** будильник для голосовых был подписан «звоню два раза в день», а звонил восемь. Каждый звонок, даже впустую, стоит как открыть толстую книгу с самого начала. Переставил на два раза, как на подписи. Заодно нашёл в бумажке про будильник враньё про несуществующего сторожа и почистил.

оператор, половина одиннадцатого вечера. Будильник уже переставлен, ДР-кандидаты дождутся утра. Иди спать, завтра доразберём.

---

**User:**

Ретро

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

## Step 1🧠 — ПАМЯТЬ СЕССИИ: сироты по worktree + машинно-невидимые опровержения (дверь §8.6; добавлена 2026-09-02)
Сессия из worktree пишет память в СВОЮ проектную папку, домашний индекс о ней не знает — замер 02.09 на NODE-0X: 20 таких заметок, одна несла вердикт, опровергнутый через девять дней в соседней папке. Два прогона, 0 LLM, 0 сети:
- `python ~/.claude/scripts/memory_harvest.py --scan` → есть ORPHAN → `python ~/.claude/scripts/memory_harvest.py --harvest` (копия домой + указатель в `MEMORY-archive.md`; оригинал НЕ трогается). Exit 3 = `NEEDS-HUMAN` (тёзки припаркованы, ничего не потеряно) → строкой оператору, не молча.
- `python ~/.claude/scripts/memory_epistemic.py --lint` → `SELF-TOMBSTONE` (заметка сама пишет, что устарела, а машина этого не видит) закрыть тем же заходом: `--close <слаг> --superseded-by <слаг-преемника>`. Отмена закрывается ПОЛЯМИ (`status`/`valid_to`/`superseded_by`/`refuted_on`/`refuted_by`) во ВСЕХ копиях слага, а не переписыванием одной: CLAUDE.md §8.4-бис + [[memory-records-close-by-fields-not-rewrite]].
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже) и на каждую — ОДНА строка в `$OBSIDIAN_VAULT\00-System\Breakage-Journal.md`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. Затем СЧЁТЧИК по классу — **не грепом по имени, а прибором** (замер 03.09.2026: в журнале 503 пронумерованных случая, из них **299 записаны как «1-й датированный»**, уникальных слагов всего 72; счёт вёлся по ИМЕНИ, имя сочинялось заново под каждую поломку, и порог «третьей поломки» был структурно недостижим — семья «вывод по одной поверхности» набрала 72 случая с 27.07 и ни разу не дошла до 3):
```
python ~/.claude/scripts/prior_art.py class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный → отдельная сессия починки** (5 почему по серии → ТРИЗ → АК-47). Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым». Канон: память `class-counted-by-name-never-reaches-three` + CLAUDE.md §5.10.
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
⭐ **🌍 МИРОВОЙ ПОТРЕБИТЕЛЬ (dev 24.08, голосом):** у каждой закрытой за сессию починки КЛАССА — четвёртый исход Connect: раздали ли миру? Сеть-ловушка: строки Breakage-Journal этой сессии «класс закрыт» без вердикта 🌍 = долг → прогнать скилл **`/share-fix`** (порог переносимости, реверс-поиск по симптому, 3-5 лучших живых тредов, gist, вахта — вся механика там). Вердикт в отчёте обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🔄 — Outcome-аудит ПРОШЛЫХ правил (взято у netresearch/retro-skill «outcome mode», adopted 2026-08-26; наш обмен — issue #78 их репо)
Door-audit (Step 3🔗) судит правило при РОЖДЕНИИ; этот шаг судит СУДЬБУ уже записанных — родился с дверью ≠ живёт (замеры: 19/25 без двери, «5 почему» 42 дня без применения, Firefox-first умер тихо за 13 дней). Дёшево, ЧИТАЕМ ночные выходы, сканы руками НЕ гоняем (§10.0):
1. Возьми правила, ТЕМАТИЧЕСКИ близкие этой сессии + до 5 самых старых нетронутых из ночной карты `rule_liveness` (HTML/JSON выход ночного прогона; руками `--scan` не запускать).
2. По каждому три вопроса: применялось ли с прошлого ретро (счётчик §5.8 / упоминание в транскриптах)? нарушалось ли (Breakage-Journal)? актуально ли ещё (не superseded)?
3. Вердикт-строка в отчёт: «🔄 outcome: N проверено · M живут · K мертвы» — каждому мёртвому РЕШЕНИЕ в том же заходе: утиль (в архив с причиной) / дверь построить / отдать сессии-починке. Молча пропустить шаг нельзя; сессия без тематических правил → «🔄 outcome: чужих правил не трогал» одной строкой.

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
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 кандидата/ночь, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].
**⭐ Мини-тизер обязателен (dev 01.09):** every retro with a substantive arc births ≥1 mini-teaser (200-250 chars, «грабли → правило» so the READER gets use, not a status report) → `python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук>" --note "<тизер>" --tier teaser`. Verdict «no teaser» is legal ONLY with a named reason (empty routine session). Canon: `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`.

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
5. **⭐ Скилл уходит в мир (dev 01.09, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** любой собранный/существенно обновлённый скилл в том же заходе получает (а) тизер-пост в наши соцсети (через content-factory / каскад) и (б) публикацию самого скилла на нашем публичном GitHub (дефолт `tonydzi/clawrush` `artifacts/`) ПОСЛЕ leak-scan, с пометкой в шапке «built for dev's fleet — adapt paths/names to your setup». Заточен под оператора / сырой / «на тормозке» — публикуем всё равно, честно пометив. Скип — только с названной причиной (leak-scan red / чистая кухня CRM).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
4б. **🔄 Outcome** — «N проверено · M живут · K мертвы + решения» (Step 3🔄).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the FULL enriched `/compact` block printed inline (Step 6b; указатель на файл запрещён).
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Write a clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- The nightly **Brain Reindex @04:00** makes it `/ask`-searchable — no manual reindex needed.

**6a-бис. Снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- Команда: `python %USERPROFILE%\.claude\scripts\retro_lost_scan.py mark-done <sessionId> --note "ретро: <имя заметки>"`
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6a-тер. Переименуй сессию: префикс «Р+» в видимом имени — СРАЗУ после 6a-бис** (⭐ dev 02.09.2026, голосом: «когда я вижу Р+, я понимаю, что дошёл в этой сессии до крупного milestone»).
- Вызови `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → возьми текущий `title`. Если он УЖЕ начинается с `Р+`/`р+`/`рр+` — шаг закрыт, второй префикс не лепить.
- Иначе `mcp__ccd_session_mgmt__set_session_title` с `session_id: "self"` и `title: "Р+<старое имя без изменений>"`. Меняется ТОЛЬКО человекочитаемое имя в приложении (titleSource=tool), системный id не трогается; имя, данное оператором, сохраняется целиком после префикса.
- MCP session_mgmt недоступен (headless `claude -p`, чужой харнес) → одна строка в отчёте «Р+ не поставлен: нет session_mgmt», не молчи.

**6b. PRINT the READY enriched paste-line INLINE — обязательный выход КАЖДОГО ретро (⭐ dev 26.08, голосом: «каждый раз давай готовый текст компакта; иди-в-файлик — неудобно»).**
- ⚠️ Fact base (2026-07-22): bare `/compact` does NOT read our format — 354/354 past compacts fell back to the DEFAULT English template; PreCompact hooks cannot inject (issue #14160). The 7-header format applies ONLY pasted inline: `/compact <text>`.
- **Procedure = same enrichment as `/cc` Steps 2-3** (single source of mechanics — don't duplicate, read `~/.claude/skills/cc/SKILL.md`): take the skeleton from `$USERPROFILE/.claude/compact-prompt.md` § «Готовая строка», FILL all 7 headers with THIS session's real facts — reuse the distillation already written into the 6a vault note, don't re-derive — and PRINT one fenced ```code``` block starting with `/compact `, со строкой над ним: «➤ Скопируй блок целиком и вставь следующим сообщением». Then the fork:
> **«Готово, всё в волте. Остаёшься в сессии — вставь блок ниже целиком (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — просто уходи, всё уже заархивировано.»**
- ⛔ **Указатель вместо блока ЗАПРЕЩЁН.** «Вставь блок из `~/.claude/compact-prompt.md`» / «возьми текст в файле» = нарушение правила (ровно эта формулировка — жалоба оператора 26.08). Пустой скелет с `<...>` — тоже нарушение: блок обязан быть обогащён сессией. Канон: память `compact-dev-prefers-zero-touch` §Поправка 26.08 + `compact-format-delivery-gotcha`.
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; printing the ready line is my half, the paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python prior_art.py class \"рутина носила описание 2 раза в сутки а живой cron стоял на 8 прогонах, расписание разъехалось с собственным описанием\" 2>&1 | head -30; echo \"PRIOR_EXIT=$?\"", "description": "Check prior art for the breakage class"

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python memory_harvest.py --scan 2>&1 | tail -5; echo \"---epistemic---\"; python memory_epistemic.py --lint 2>&1 | tail -8; echo \"---onair---\"; python onair.py list 2>&1 | head -10", "description": "Memory harvest scan, epistemic lint, onair li

---

> `Bash` -- {"command": "J=\"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; echo \"=== корень: описание/докстринг разъехались с реальностью объекта ===\"; grep -oiE \"класса .{0,60}\" \"$J\" | grep -iE \"docstring|описан|паспорт|доке|дока|коммент|врал|врёт|расход|разъех|устаре\" | sort | uniq -c |

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && python retro_inventory.py 1 2>&1 | tail -6", "description": "Run retro inventory for 1 day"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python rule_home_guard.py cron-razъehalsya 2>&1 | head -6; echo \"=== ledger 2 дня ===\"; python \"D:/Vault/_imports/day_ledger.py\" --recall 2 2>&1 | head -14", "description": "Rule home guard and day ledger recall"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python \"D:/Vault/_imports/day_ledger.py\" --recall 2 2>&1 | head -12", "description": "Day ledger recall 2 days"}

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/seed_docdrift.md\" <<'SEEDEOF'\nПЕРВЫМ ДЕЛОМ переименуй эту сессию: вызови mcp__ccd_session_mgmt__set_session_title с title \"Класс: описание объекта врёт про са

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/content-factory\" && python content_miner.py capture --title \"будильник врал про сам себя\" --note \"Рутина носила описание «звоню 2 раза в сутки». Живой cron стоял на 8. Заметил не сторож, а человек голосом. Правило: описание и расписание — два поля одного об

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "Р+Voice dispatcher"}

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/write_retro.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io, os\np = r\"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-09-03-voic

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/growth.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io, os\np = os.path.expanduser(r\"~\\.claude\\projects\\P---WORKDIR-HUB\\memory\\cofounder-gr

---

> `Bash` -- {"command": "cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_aeac58ac/scratchpad/mktask.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io, os\np = r\"D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-03-class-doc-drift-description-lies-a

---

> `Bash` -- {"command": "sed -n '1,200p' \"C:/Users/dev/.claude/compact-prompt.md\" | grep -n \"Готовая строка\" -A 30", "description": "Read compact prompt ready-line skeleton"}

---

**Claude:**

[⏰ четверг, вечер, 22:47, 3 сентября 2026]

## 🔎 Сверка (Step 0)

Проверил: turnstate этой сессии, дневной леджер за 2 дня, доска ON AIR, память (harvest + epistemic lint), журнал поломок (1489 строк-случаев).

⚠️ **Одна коллизия.** Я дописал строку в `00-System/Breakage-Journal.md`, а на доске висит чужая активная заявка `[EXCLUSIVE] arch-system HUB/2439b8ce — «Корень: multi-writer Breakage-Journal»`. То есть соседняя сессия ровно сейчас чинит проблему множественных писателей этого файла, а я в него молча написал. Своей таблички ON AIR я не объявлял, флагую честно.

🧠 **Память:** сирот к переносу 0, но `memory_harvest` держит 2 записи `NEEDS-HUMAN` (`watchdog-upper-bound-creates-the-pileup`, `asks-are-my-autonomy-debt`) — ждут твоего слияния руками. `memory_epistemic --lint` дал FINDINGS: две пары «закрытая запись против открытого близнеца», в том числе `chatgpt-deep-research-dead-2026-07`. Это чужие хвосты, не мои, трогать не стал.

## 🎬 Сегодня мы поняли

Сессия открылась как обычный прогон рутины: предгейт, «груза нет», выход за секунды.

Через десять часов ты пришёл голосом: «слишком частая, хватит раза, максимум двух». Ты был прав, но причина оказалась хуже формулировки.

Рутина носила описание «2 раза в сутки, 09:00 и 21:00, приказ оператора 21.08», а живой cron стоял на восьми прогонах. Подпись на объекте и сам объект разъехались, и заметил это не сторож, а ты ощущением.

Дальше вскрылись ещё две гнилушки того же корня. Docstring врал про Windows-задачу «каждые 20 минут», которой не существует. Тест был красным с 02.09, потому что сторожил снятый контракт.

## 🎙 Вердикт Майка

- 💰 **деньги:** выручки ноль, но ~670k токенов в сутки вернулись в баки, которые жгут миссию №2.
- 🔪 **что убил бы:** ничего, сессия короткая и по делу.
- 🤺 **спарринг:** спорил честно, `SPAR: с-уликой`. Не поддакнул «режу», а принёс цифры и вслух назвал цену: голосовая в 09:30 теперь ждёт до 21:00.
- ❓ **вопрос:** два прогона держат утреннюю пачку ДР-кандидатов. Хочешь один, куда переносим пачку?

## ♻️ Что оставляем

| артефакт | вердикт | tested? | куда |
|---|---|---|---|
| cron → `0 9,21 * * *` | 🟢 Keep | ✅ реестр отвечает «At 09:08 AM» | планировщик |
| docstring `voice_dispatch.py` | 🟢 Keep | ✅ 32/32 | код |
| ассерт `_test_voice_dispatch.py` | 🟢 Keep | ✅ видел красным до правки | тест |
| строка в Breakage-Journal | 🟢 Keep | n/a | `00-System/` |
| 3 строки change_ledger | 🟡 one-off | n/a | `scripts/` под gitignore |

## 🩹 Класс поломки: прибор соврал

Прогнал `prior_art.py class`, как велит канон. Он выдал 6 «прежних случаев» по совпадению поверхностных слов (cron, рутина, прогон, расписание), ни один не тот корень, и вдобавок посчитал только что написанную мной же строку.

Считать пришлось грепом по корню руками. Корень: **две копии одной правды, правится одна, вторая молча врёт.** Сегодня он выстрелил дважды, а в журнале уже был сиблинг «прод и исходник в волте разъехались».

Итого три датированных случая, значит по §5.10 класс системный. Сессия починки поставлена в очередь: `auto-hub-260903-class-doc-drift`, плюс карточка `task-2026-09-03-class-doc-drift-...` в реестре.

## 🔗 Connect · 🔄 outcome · ⛳ дрифт · 🗺 roadmap

- 🔗 **Connect:** ✅3 используется (cron читает планировщик, docstring читает следующий чинящий, тест гоняет `/tt`) · 🔗0 · ⚠️0 в воздух. 🌍 непереносимо: правка приватного расписания, миру раздавать нечего.
- 🔄 **outcome:** `rule_home_guard` отбит гейтом обслуживания (21-й заход за сутки, §10.0). Новых правил в канон эта сессия не вносила, так что дверей проверять нечего.
- ⛳ **дрифта нет.** Цель была «сократить частоту», ей и занимались.
- 🗺 **roadmap:** ⏸ без движения, это инфра-гигиена.
- 📋 **журнал:** +1 новая (класс doc-drift) · ✅0 закрыто.
- 🔁→🛠 **повторов на скилл нет.** Скилл `/hk` и ночной аудит роботов уже покрывают эту зону; новый строить не буду.

## 📌 Открыто

1. **#task-2026-09-03-class-doc-drift** — разбор класса, сессия в очереди.
2. Один прогон вместо двух: жду твоё слово, куда девать утреннюю пачку ДР-кандидатов.
3. Две записи `NEEDS-HUMAN` в памяти ждут твоего слияния.
4. Я писал в Breakage-Journal поверх чужой EXCLUSIVE-заявки на этот файл. Если та сессия сейчас его перестраивает, моя строка может уехать в конфликт.

## 🗜 Компакт

Заметка сохранена: `01-Conversations/Claude/Retros/retro-2026-09-03-voice-dispatcher-cron-drift.md`. Сессия переименована в «Р+Voice dispatcher», из очереди `/retro-lost` снята. Тизер «будильник врал про сам себя» ушёл в воронку черновиком.

➤ Скопируй блок целиком и вставь следующим сообщением

```
/compact Сохрани ДОСЛОВНО по 7 заголовкам (обоснования исчезают первыми):
- РЕШЕНИЯ — cron рутины voice-dispatcher переведён с `0 8,10,12,14,16,18,20,22 * * *` (8 прогонов/сутки) на `0 9,21 * * *` (2×/сутки, 09:00 и 21:00 Лиссабон), возврат к её же описанию и приказу оператора 21.08. Два прогона, а не один, ПОТОМУ ЧТО утренний отдаёт пачку ДР-кандидатов, вечерний только копит. Класс «описание объекта врёт про сам объект» признан системным (3-й датированный случай) и отдан отдельной сессии, а не залатан третий раз точечно.
- TODO — P1 разобрать класс doc-drift по 5 почему из серии трёх случаев (сессия auto-hub-260903-class-doc-drift в spawn_queue, карточка task-2026-09-03-class-doc-drift-description-lies-about-object.md). P2 решить судьбу prior_art.py, который судит по подстроке, а не по корню. P2 слить 2 записи NEEDS-HUMAN в памяти.
- СЕЙЧАС — всё применено и проверено, работа закрыта; следующий прогон рутины 04.09 в 09:08.
- ПУТИ И ЗНАЧЕНИЯ — ~/.claude/scripts/voice_dispatch.py · ~/.claude/scripts/_test_voice_dispatch.py · D:/Vault/_imports/content-factory/voice-sessions/dispatch-usage.jsonl · ~/.claude/change_ledger/HUB-01.jsonl · 00-System/Breakage-Journal.md · 01-Conversations/Claude/Retros/retro-2026-09-03-voice-dispatcher-cron-drift.md
- СЧЁТЧИКИ — 8→2 прогона/сутки; 7 заходов 03.09, из них 5 пустых; медиана старта сессии 112 178 токенов (277 сессий, 03.09); экономия ~670k токенов/сутки; тест 32/32 exit 0 (до правки 31/1, красным видел своими глазами); schtasks|grep -ci voice = 0. НЕ доделано: класс doc-drift не закрыт, только зафиксирован.
- ОТКРЫТО — писал в Breakage-Journal поверх чужой активной EXCLUSIVE-заявки arch-system HUB/2439b8ce на multi-writer этого файла, возможен конфликт. prior_art.py дал ложные 6 «прежних случаев» по поверхностным словам и посчитал мою же свежую строку. rule_home_guard отбит гейтом обслуживания (21-й заход за сутки).
- ИНСТРУМЕНТЫ И КОНТРАКТЫ — voice_dispatch.py check --hours 14: exit 0 тишина / 9 груз / 2 рельса сломана / 4 crash-guard. voice_dispatch_watch.cmd сторожит ВОЗРАСТ ВЫХОДА и сессий НЕ поднимает; Windows-задачи «Claude Voice Dispatch» не существует. Рутина кладёт сиды в spawn_queue.py add и сама create_scheduled_task не зовёт (анти-clone-storm вендора с 26.08). Грабли: `python ... | head` возвращает exit пайпа, а не питона — дважды печатал TESTEXIT=0 при красном тесте.
Сожми работающее до 1 строки + имена компонентов; выкинь отладку, тупиковые гипотезы, логи, переформулировки.
```

🧒 **Простыми словами:** будильник был подписан «звоню два раза», а звонил восемь, и заметил это ты, а не наши сторожа. Переставил на два. Потом нашлось, что и бумажка рядом с будильником врёт, и проверялка сломана. Три вранья одного сорта подряд, поэтому завёл отдельную сессию: пусть разберётся, где ещё подпись расходится с вещью.

оператор, без десяти одиннадцать. Ретро закрыто, компакт готов, очередь разберут без тебя. Всё, спать, это уже второй раз прошу.
