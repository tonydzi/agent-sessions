---
session: s_3407f7b4
date: 2026-09-11
words: 2675
turns: 14
tools: "Bash, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-11 · Scheduled run: registry-dispatcher-daily

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3407f7b4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="registry-dispatcher-daily" file="C:\Users\dev\.claude\scheduled-tasks\registry-dispatcher-daily\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

⚙️ РЕЛЬСА: SONNET (грунт). Эта рутина = механика, авторского голоса и суждения в ней нет.
Работай сам ТОЛЬКО если сессия уже на Sonnet. Если сессия стартовала на Opus/Fable — не жги
умный бак: передай ВСЮ содержательную работу субагенту через инструмент Agent с
`model: 'sonnet'` (промпт = шаги ниже целиком), а сам только прими его отчёт и заверши.
Детерминированные python-вызовы делай напрямую в любом случае — они 0 токенов.
Канон: CLAUDE.md §6.2 (маршрутизация), §6.3 (жечь оплаченные лимиты).

Ты диспетчер реестра задач на хабе HUB-01. Работа механическая, займёт несколько минут. Токенов трать минимум: ничего не исследуй, не читай волт, не строй дашборды.

ПОЧЕМУ ТЫ СУЩЕСТВУЕШЬ (приказ оператора 06.08.2026, дословно): «включай диспетчер, все ставь на автозапуск, у меня нет времени нажимать ЧИПЫ, 1 раз в сутки норм». До тебя будильник реестра каждое утро печатал список просроченных задач, и ноль из них сдвигалось: уведомление, которое никто не открывает, стоит ноль.

ЧТО ДЕЛАТЬ, по шагам:

0. СНАЧАЛА — очередь СЕССИЙ-ПОЧИНОК (канон §5.10, механизм из голосовой оператора hub:5164). Выполни:
   python C:\Users\dev\.claude\scripts\selfheal.py repairs --json
   Код 2 / пусто — пропусти шаг молча. Иначе на КАЖДЫЙ элемент массива положи СИД в очередь подъёма
   (см. поправку 08.09 в шаге 2 — create_scheduled_task из рутины ЗАПРЕЩЁН):
     --task-id = поле taskId · --description = поле title · --prompt-file = файл с полем seed
     ЦЕЛИКОМ, дословно (fireAt больше не нужен: очередь не расписание, разносить по времени нечего)
   Создал -> сразу отметь, иначе завтра поднимешь ту же сессию второй раз:
     python C:\Users\dev\.claude\scripts\selfheal.py repairs --commit <класс>
   Это НЕ обычные задачи реестра: у класса поломок набралось 3 датированные строки в
   00-System\Breakage-Journal.md, значит класс системный и чинится ОТДЕЛЬНОЙ сессией.
   Спрашивать оператора не надо ни на одном шаге — ночью нажать approve некому, в том и смысл.
   Если у элемента стоит "overdue": true — значит заявка ждала сессию больше суток: подними её
   ПЕРВОЙ и добавь строку в шину (шаг 4), что дверь молчала.

0.5. ДОСЕВ БУДИЛЬНИКОВ (одна команда, 0 токенов, идемпотентна). Гейт task_card_guard не
   пускает новые живые карточки без `review_after`, но скрипты-писатели и чужие узлы пишут
   мимо гейта. Досей дату каждой новой сироте (замер 21.08: до посева их было 80% реестра):
   python C:\Users\dev\.claude\scripts\task_wake_seed.py --apply
   «сирот к посеву: 0» — норма, молча дальше. Больше 20 за сутки — это уже не капля, а
   течь: добавь строку об этом в доклад шага 4 (кто-то плодит карточки мимо гейта).

1. Получи список:
   python C:\Users\dev\.claude\scripts\registry_dispatch.py --json
   Вернётся массив объектов {taskId, kind, why, card, title, priority, seed}. Пусто (код 2) — значит всё поднятое уже поднимали в последние 7 дней: молча закройся, ничего не делай, ничего не пиши.

2. ⛔ ПОПРАВКА 08.09.2026 (канон CLAUDE.md §9.2, хук spawn-queue): из сессии, порождённой
   scheduled-task'ом, вызов mcp create_scheduled_task / update_scheduled_task ЗАПРЕЩЁН. Он открывает
   апрув-окно, нажать его в безлюдном прогоне некому, сессия виснет ПОСРЕДИ ХОДА и держит слот часами
   (замер: 93 из 101 блока апрува — именно эти вызовы; 02.09 три зависшие сессии остановили спавн на 6ч42м).
   Вместо подъёма — КЛАДИ СИД в очередь, по одному на элемент:
     python %USERPROFILE%/.claude/scripts/spawn_queue.py add --task-id <taskId> --description "<title>" --prompt-file <путь>
   Сид уже в очереди (список: spawn_queue.py list) — пропусти молча, дубль не клади.
   Сессии из очереди поднимает ЖИВАЯ сессия (человек за клавиатурой) — ей есть кому нажать.
   Спрашивать оператора не надо: ответ уже дан приказом 06.08, изменился только транспорт.

3. Все сессии созданы -> отметь их в леджере:
   python C:\Users\dev\.claude\scripts\registry_dispatch.py --commit
   Делай это СРАЗУ после последнего spawn_queue add, не откладывая на конец прогона. Замер
   11.08.2026: с 07 по 11.08 этот шаг не выполнился НИ РАЗУ (леджер стоял на 6 строках от 06.08),
   хотя сессии реально поднимались, и карточка repair-dead-scheduled-task уехала в очередь второй
   раз за сутки. С 11.08 дедуп подстрахован вторым, не-самоотчётным источником: скрипт сам смотрит,
   есть ли на диске каталог `~/.claude/scheduled-tasks/auto-hub-<дата>-<база>`. Подстраховка не
   отменяет шаг: без леджера нет счётчика «кого будили и когда».

3.5. СХЛОПНИ РОДНЮ (04.09.2026, режим /decide). Один дефект приезжает под 2-3 именами и
   жрёт 2-3 сессии — канон §5.10 велит считать и чинить по СЕМЬЕ, а не по имени. Выполни:
     python %USERPROFILE%/.claude/scripts/spawn_queue.py families
   Каждая строка с пометкой «СЛИТЬ» (в семье больше одного СЛИЯЕМОГО сида) -> слей:
     python %USERPROFILE%/.claude/scripts/spawn_queue.py merge <имя-семьи>
   Отказ «сливать нечего» — норма, иди дальше молча. Голосовые оператора и уже слитые сиды
   помечены 🔒 и не сливаются никогда (§9.2: голосовая = отдельная сессия ВСЕГДА) — это
   замок в коде, а не твоя вежливость, ломать его руками нельзя.
   Замер 04.09: 24 сида -> 17 подъёмов, пять ремонтных классов схлопнулись в две семьи.

4. Доложи ОДНОЙ строкой в шину:
   python C:\Users\dev\.claude\scripts\bus_send.py "диспетчер реестра: поднял N сессий (перечисли taskId через запятую)"

ГРАНИЦЫ. Сам ты задачи НЕ решаешь — только создаёшь сессии и коммитишь леджер. В карточки не пишешь.
Если скрипт упал или spawn_queue add вернул ошибку — не глотай молча: доложи по шине что
именно сломалось, с текстом ошибки, и НЕ коммить леджер (иначе задача будет считаться поднятой, не будучи
поднятой, и потеряется на неделю).
<!-- ROUTINE-TOKEN-DISCIPLINE v1 · 08.09.2026 · приказ оператора: все рутины на всех узлах — режем шаги и мусор в контексте, не качество. Замер NODE-0X 06–08.09: 71% недельного бака = перечитывание ~180k контекста на каждом из 60–200 вызовов за прогон; после блока в 20 лейнах вес прогона −31% за первый день -->
🪙 ТОКЕН-ДИСЦИПЛИНА РУТИНЫ (стоимость прогона = контекст × число вызовов модели; качество результата НЕ режем):
1. РАЗВЕДКА ОДНИМ ВЫЗОВОМ: журнал, реестры, списки целей, `gh`/API-выборки — собери в ОДИН скрипт с `--jq`/`head`, не 10–15 команд. Потолок разведки — 5 вызовов.
2. НЕ ВЫВАЛИВАЙ: никогда `cat`/`Read` целого файла, треда или дампа в контекст — только нужные поля и строки (`--jq`, `sed -n`, `head -c 4000`). Большой объект читаешь ОДИН раз целиком в одном вызове, не по кусочкам.
3. ЦИКЛ ПРОВЕРОК = ОДИН СКРИПТ: репро/тесты/мутации — один `.py`/`.sh`, запуск один раз, итог ≤20 строк. Серия из 30–90 микро-вызовов в scratchpad ⛔ (замер s9 06.09: 95 из 132 команд).
4. ТЕКСТ ПИШЕШЬ ОДИН РАЗ через Write, правишь через Edit точечно; переписывать файл целиком ⛔.
5. ПОТОЛОК ПРОГОНА — 60 вызовов модели. На 50-м не закончил — закрывай заход честной строкой в журнал («сделано X, не успел Y, причина»), не тяни до 200.
6. МЫШЛЕНИЕ КОРОТКО: не пересказывай себе сид и правила; думай про предмет, не про регламент.
7. ГРУНТ — СУБАГЕНТУ НА SONNET, СУЖДЕНИЕ — У СЕБЯ: чтение больших диффов/логов, разведку, репро отдавай `Agent(model="sonnet")` с ТЗ «верни ≤40 строк выжимки»; сам читаешь выжимку и пишешь то, что уходит наружу под именем оператора.
8. ⛔ ОЖИДАНИЕ НЕ ЧЕРЕЗ МОДЕЛЬ (замер s7-fast 08.09: 87 из 138 команд = `sleep 1; echo idle`, каждый тик = вызов на 200k контекста, +39% веса прогона). Ждёшь сборку/тест/CI/синк — ОДИН Bash-вызов с блокирующим циклом внутри: `timeout 900 bash -c 'until <условие>; do sleep 20; done'` (Windows: `powershell -c "while(!(<условие>)){Start-Sleep 20}"`), либо run_in_background и ждёшь уведомления. Ручной цикл «sleep → посмотреть → ещё раз» ⛔. Дольше 15 минут — не жди: поставь на вахту (pr_watch / реестр) и закрой заход.
Проверка постфактум: `python3 ~/.claude/scripts/usage_audit.py` (0 LLM): вызовов на прогон ≤60, вес прогона ≤½ от базы 06–07.09.

<!-- RUNLOG-CONTRACT v1 · 09.09.2026 · приказ оператора (голосовая 09.09, хаб): каждая смена читает тетрадь предыдущих смен и оставляет свою. SKILL.md наследует ПРАВИЛА, RUNLOG наследует ИСТОРИЮ. -->
📓 ВАХТЕННЫЙ ЖУРНАЛ РУТИНЫ (память между прогонами):
ШАГ 0 — ПЕРВЫМ ДЕЛОМ, до любой работы: python ~/.claude/scripts/routine_runlog.py tail registry-dispatcher-daily
  Это записки последних 5 смен: что сделано, обо что споткнулись, что поменяли в этой инструкции, с чего начать. Не наступай на их грабли и не переделывай уже сделанное. Журнала нет — ты первая смена, работай по SKILL.md.
ФИНАЛ — ВСЕГДА, даже на пустом/тихом прогоне: python ~/.claude/scripts/routine_runlog.py add registry-dispatcher-daily "сделал: ...; споткнулся: ...; правил SKILL.md: да/нет+что; следующей смене: ..."
  3-6 строк, только сигнал (не пересказ). Починил что-то в SKILL.md — напиши об этом ЯВНО: следующая смена обязана узнать о починке из журнала, а не открыть её заново.
</scheduled-task>

---

**Claude:**

[⏰ 05:17, 11 сентября 2026]

Рутина-диспетчер реестра. Начинаю с вахтенного журнала (шаг 0 контракта).

---

> `Bash` -- {"command": "python ~/.claude/scripts/routine_runlog.py tail registry-dispatcher-daily 2>&1 | head -60", "description": "Read routine runlog tail"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/selfheal.py repairs --json 2>&1 | head -80; echo \"EXIT=$?\"", "description": "Check repair-session queue"}

---

**Claude:**

Вахтенный журнал прочитан. Главное предупреждение прошлой смены: очередь подъёма распухла (хук сессии показывает 179 сидов). Это вынесу отдельно. Сначала механика.

---

> `Bash` -- {"command": "cd ~ && echo \"=== WAKE SEED ===\" && python ~/.claude/scripts/task_wake_seed.py --apply 2>&1 | tail -5\necho \"=== SPAWN QUEUE COUNT ===\"\npython ~/.claude/scripts/spawn_queue.py list 2>&1 | wc -l\necho \"=== REGISTRY DISPATCH ===\"\npython ~/.claude/scripts/registry_dispatch.py --jso

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_3407f7b4/scratchpad\"\nmkdir -p \"$SP\"\npython ~/.claude/scripts/registry_dispatch.py --json > \"$SP/rd.json\" 2>\"$SP/rd.err\"; echo \"EXIT=$?\"\nhead -3 \"$SP/rd.err\"\npython -c \"

---

> `Bash` -- {"command": "python ~/.claude/scripts/spawn_queue.py list 2>&1 | head -8\necho \"--- grep existing ---\"\npython ~/.claude/scripts/spawn_queue.py list 2>&1 | grep -c \"auto-hub-2609\"\nfor t in auto-hub-260910-repair-apply-ne-dostavlyaet auto-hub-260910-repair-open-w-usekaet-zhivoy-fayl-do-dokazanno

---

**Claude:**

Дубликатов нет. Кладу 6 сидов одним проходом.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_3407f7b4/scratchpad\"\ncat > \"$SP/place.py\" <<'PYEOF'\nimport json, os, subprocess, sys\nSP = sys.argv[1]\nHOME = os.path.expanduser(\"~\")\nSQ = os.path.join(HOME, \".claude\", \"sc

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_3407f7b4\\scratchpad\\place.py", "content": "\"\"\"Диспетчер реестра: кладёт сиды из registry_dispatch --json в spawn_queue.\n\nОдин проход = один вызов модели (токен-дисциплина р

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_3407f7b4/scratchpad\"\npython \"$SP/place.py\" \"$SP\"", "description": "Place seeds into spawn queue"}

---

> `Bash` -- {"command": "for c in apply-ne-dostavlyaet open-w-usekaet-zhivoy-fayl-do-dokazannoy-zapisi detektor-dolga-sudit-podmnozhestvo-vselennoy-tredov memory-index-line-lost-overnight run-env-path-or-command-missing; do\n  echo \"--- $c\"\n  python ~/.claude/scripts/selfheal.py repairs --commit \"$c\" 2>&1 

---

**Claude:**

Стоп. `--commit` напечатал ДРУГИЕ taskId, чем те 6, что я реально положил. Проверяю леджер — это похоже на рецидив класса «commit пересчитывает вместо записи».

---

> `Bash` -- {"command": "L=$(ls -t ~/.claude/*dispatch* ~/.claude/**/*dispatch* 2>/dev/null | head -5); echo \"candidates: $L\"\npython - <<'PY'\nimport os,glob\nh=os.path.expanduser('~/.claude')\nhits=[]\nfor root,dirs,files in os.walk(h):\n    if any(s in root for s in ('node_modules','.git')): continue\n    

---

> `Bash` -- {"command": "tail -8 ~/.claude/_registry_dispatch.jsonl | python -c \"\nimport sys,json\nfor ln in sys.stdin:\n    ln=ln.strip()\n    if not ln: continue\n    try: d=json.loads(ln)\n    except: print('RAW',ln[:160]); continue\n    print(d.get('ts','?'), '|', d.get('taskId','?'), '|', str(d.get('card

---

**Claude:**

Класс рецидивировал: леджер записал 6 задач, из которых реально положена в очередь ОДНА. Чиню немедленно — сперва спрашиваю инструмент.

---

> `Bash` -- {"command": "python ~/.claude/scripts/registry_dispatch.py --help 2>&1 | head -40", "description": "Check registry_dispatch flags"}

---

**Claude:**

Инструмент не умеет адресно; леджер правлю сам (атомарно, с бэкапом), это единственная ложная запись.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_3407f7b4\\scratchpad\\fix_ledger.py", "content": "\"\"\"Убрать из _registry_dispatch.jsonl ЛОЖНЫЕ записи прогона 2026-09-11.\n\nПовод: registry_dispatch.py --commit пересчитал спи

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_3407f7b4/scratchpad\"\npython \"$SP/fix_ledger.py\"\necho \"=== tail after ===\"\ntail -3 ~/.claude/_registry_dispatch.jsonl | python -c \"\nimport sys,json\nfor ln in sys.stdin:\n    

---

**Claude:**

Леджер соответствует факту. Записываю поломку в журнал класса (§5.10).

---

> `Bash` -- {"command": "python ~/.claude/scripts/selfheal.py journal --help 2>&1 | head -20", "description": "Check selfheal journal flags"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/prior_art.py class \"коммит леджера пересчитывает набор кандидатов заново вместо записи выданного набора, в леджер уезжают не те задачи\" 2>&1 | head -25", "description": "Check class family by description"}

---

> `Bash` -- {"command": "grep -c \"commit-recomputes-instead-of-recording\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" 2>&1\ngrep -n \"commit-recomputes-instead-of-recording\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" 2>&1 | head -6 | cut -c1-220", "description": "Count pr

---

> `Bash` -- {"command": "python ~/.claude/scripts/breakage.py count --class commit-recomputes-instead-of-recording 2>&1 | head -10", "description": "Count class occurrences via the door"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/selfheal.py journal --class commit-recomputes-instead-of-recording \\\n --what \"registry_dispatch.py --commit пересчитал набор кандидатов заново вместо записи набора, выданного --json: --json отдал 6 свежих ремонтных классов (260910/260911), в леджер уехали 6 Д

---

**Claude:**

Класс стал системным (4/3). Проверяю, появилась ли заявка на сессию починки, и схлопываю родню.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_3407f7b4/scratchpad\"\npython ~/.claude/scripts/selfheal.py repairs --json 2>/dev/null > \"$SP/sh2.json\"\npython -c \"\nimport json\nd=json.load(open(r'$SP/sh2.json',encoding='utf-8')

---

> `Bash` -- {"command": "python ~/.claude/scripts/selfheal.py repairs 2>&1 | tail -3; echo \"EXIT=$?\"\necho \"=== FAMILIES ===\"\npython ~/.claude/scripts/spawn_queue.py families 2>&1 | tail -40", "description": "Check repairs plain output and spawn queue families"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/spawn_queue.py families 2>&1 | grep -i \"слить\" | head -20\necho \"--- header ---\"\npython ~/.claude/scripts/spawn_queue.py families 2>&1 | head -15", "description": "Find mergeable families"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/spawn_queue.py families 2>&1 | grep \"слияемых\" | grep -v \"слияемых 0\" | head -20; echo \"RC_of_grep=$?\"", "description": "Find families with mergeable seeds"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/spawn_queue.py merge vyvod-po-odnoy-poverhnosti 2>&1 | tail -8\necho \"=== after ===\"\npython ~/.claude/scripts/spawn_queue.py families 2>&1 | head -1", "description": "Merge the flagged family"}

---

**Claude:**

Докладываю в шину.

---

> `Bash` -- {"command": "python ~/.claude/scripts/bus_send.py \"диспетчер реестра 11.09: положил 6 сидов (auto-hub-260910-repair-apply-ne-dostavlyaet, -open-w-usekaet-zhivoy-fayl-do-dokazannoy, -detektor-dolga-sudit-podmnozhestvo-vsele, -memory-index-line-lost-overnight, auto-hub-260911-repair-run-env-path-or-c

---

**Claude:**

Проверяю, нет ли уже открытого аска по этой же теме, прежде чем поднимать оператору.

---

> `Bash` -- {"command": "ls ~/.claude/scripts/approval.py >/dev/null 2>&1 && python ~/.claude/scripts/approval.py list 2>&1 | tail -15 || echo \"no approval.py\"", "description": "List pending asks"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/approval.py pending 2>&1 | tail -20", "description": "Check open asks and cap"}

---

**Claude:**

Новый аск не создаю — по этой теме уже висит открытый `#9f63a519` (рельсы подъёма сессий выключены с 31.08, это и есть корень нерасчищенной очереди). Проверяю, пора ли его пере-пинговать штатной дверью.

---

> `Bash` -- {"command": "python ~/.claude/scripts/approval.py due 2>&1 | head -40", "description": "Check asks due for re-ping"}

---

**Claude:**

Аск не дублирую: открытый `#9f63a519` спрашивает ровно это (рельсы подъёма сессий выключены с 31.08), а движок пере-пинг по нему сегодня не назначил. Пишу вахтенный журнал.

---

> `Bash` -- {"command": "python ~/.claude/scripts/routine_runlog.py add registry-dispatcher-daily \"сделал: 6 сидов в spawn_queue (5 ремонтных классов из selfheal + scheduled-tasks-mcp-haba из реестра), все 5 классов --commit ОК; досев будильников 1 сирота; слита семья vyvod-po-odnoy-poverhnosti (2 сида -> fam-

---

**Claude:**

[⏰ 05:26, 11 сентября 2026]

## Диспетчер реестра: прогон 11.09 закрыт

**Положено 6 сидов** в очередь подъёма (`spawn_queue`), дублей не было:

| taskId | класс |
|---|---|
| `auto-hub-260910-repair-apply-ne-dostavlyaet` | 3-я поломка |
| `auto-hub-260910-repair-open-w-usekaet-zhivoy-fayl-do-dokazannoy` | 10-я |
| `auto-hub-260910-repair-detektor-dolga-sudit-podmnozhestvo-vsele` | 3-я (ушёл в семью) |
| `auto-hub-260910-repair-memory-index-line-lost-overnight` | 4-я |
| `auto-hub-260911-repair-run-env-path-or-command-missing` | 3-я |
| `auto-hub-260911-repair-scheduled-tasks-mcp-haba-smotri` | из реестра |

Пять классов отмечены в `selfheal --commit`, досев будильников дал 1 сироту, семья `vyvod-po-odnoy-poverhnosti` слита (2 сида в один подъём). Доклад в шину ушёл dual-send, обе рельсы ОК.

## Поломка, которую прогон поймал на себе

`registry_dispatch.py --commit` **не записывает набор, который выдал `--json`, а пересчитывает кандидатов заново в момент записи.** `--json` отдал 6 свежих карточек, в леджер уехали 6 других `taskId` по карточкам от 22.08, и реально поднята из них была одна.

Спусковой крючок, доказанный, это сам порядок шагов инструкции: шаг 0 (`selfheal repairs --commit`) выбивает карточки из кандидатов между двумя вызовами, и подтягиваются следующие по приоритету. Без проверки пять задач считались бы поднятыми не будучи поднятыми и выпали бы из видимости на неделю, ровно то, что инструкция запрещает своим последним абзацем.

Ущерб вычищен в том же заходе: пять ложных строк убраны из леджера атомарно, бэкап `~/.claude/_registry_dispatch.jsonl.bak-20260911-false-commit`, правдивая строка оставлена. Класс `commit-recomputes-instead-of-recording` записан дверью `selfheal journal` и стал 4/3, то есть системным. Сам forever-fix в скрипте я не делал: §Границы диспетчера это прямо запрещают, это работа сессии починки.

**Вердикт о скилле (§9.3-бис): ✅ не надо править.** Порядок шагов оказался крючком, но менять инструкцию значит спрятать симптом; чинить надо скрипт, а отмечать поднятое всё равно обязательно до конца прогона.

## Что требует твоего решения, но нового вопроса я не задавал

Очередь подъёма: **184 сида, 132 подъёма после слияния, старшим больше недели.** Диспетчер кладёт исправно, поднимать некому.

Корень уже лежит у тебя открытым вопросом `#9f63a519` (три рельсы подъёма сессий выключены с 31.08), он висит 6.8 суток. Пятый аск про то же я создавать не стал: кап 4 из 5, дубль сжёг бы последний слот, а движок пере-пинг по нему сегодня не назначил.

🧒 **Простыми словами:** каждое утро я складываю в коробку записки «вот это надо починить». Сегодня коробка чуть не соврала: она пометила пять записок как «отдано в работу», хотя отдана была одна. Я это заметил, лишние пометки стёр и записал в тетрадь поломок, чтобы отдельный мастер починил саму коробку. Но главная беда другая: записок в коробке уже 184, а разбирать их никто не приходит, потому что три «будильника» выключены с 31 августа и ждут твоего «+».

[⏰ 05:26, 11 сентября 2026]
