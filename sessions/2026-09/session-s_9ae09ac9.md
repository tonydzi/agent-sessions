---
session: s_9ae09ac9
date: 2026-09-12
words: 1584
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-12 · Scheduled run: hanging-tasks-digest

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9ae09ac9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="hanging-tasks-digest" file="C:\Users\dev\.claude\scheduled-tasks\hanging-tasks-digest\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: hanging-tasks-digest
description: Ежедневно (05:52 Лиссабон) — сводка ВИСЯЧИХ задач оператору в TG-папку. Источник истины = реестр 10-Tasks; голосовая очередь показывается ТОЛЬКО как «новое, не разобрано». [HUB HUB-01; account tonyssd]
model: sonnet
---

⚙️ РЕЛЬСА: SONNET (грунт). Эта рутина = механика, авторского голоса и суждения в ней нет.
Работай сам ТОЛЬКО если сессия уже на Sonnet. Если сессия стартовала на Opus/Fable — не жги
умный бак: передай ВСЮ содержательную работу субагенту через инструмент Agent с
`model: 'sonnet'` (промпт = шаги ниже целиком), а сам только прими его отчёт и заверши.
Детерминированные python-вызовы делай напрямую в любом случае — они 0 токенов.
Канон: CLAUDE.md §6.2 (маршрутизация), §6.3 (жечь оплаченные лимиты).

HANGING_TASKS_DIGEST_AUTORUN

ЦЕЛЬ: раз в день класть оператору в его TG-папку сводку ВИСЯЧИХ задач, чтобы ничего не терялось. Автономный прогон — действуй сам. Наружу ничего.

⚠️ КОРЕНЬ, КОТОРЫЙ ЗАКРЫТ 27.07.2026 — ЧИТАЙ ДО ПЕРВОГО ШАГА.
Раньше эта рутина читала `triage/tasks.md` и рапортовала её как «висячие задачи». Это породило ВТОРОЙ бэклог: очередь голосового триажа — append-only файл без поля состояния, из неё физически нечем было закрыть задачу, и ни одна из 299 карточек реестра `10-Tasks` на неё не ссылалась (0 совпадений по `hub:NNNN`). Итог за месяц: 73 «висячих» в очереди против 137 в реестре, при этом 26 из 73 были давно сделаны, 3 дублировали живые карточки. Очередь = ИНБОКС, не реестр. Единственный источник истины по задаче — карточка `10-Tasks/task-*.md`. Не вернуть старое поведение: сводка по очереди без реестра = отчёт о том, чего нет.

ПУТИ/КОНТЕКСТ:
- 🔴 Источник истины: `D:\Vault\Vault-Knowledge\10-Tasks\task-*.md` (frontmatter `state:` = inbox|open|wip|blocked|done|dropped|someday|archived, `priority:` P0..P3, `owner:`). Готовый аудит ночного индексатора (пишет Маяк): `10-Tasks\_audit\audit-latest.json`, витрина `_Dashboards\Task-Backlog.html`.
- 🟡 Инбокс голосовых: `D:\Vault\_imports\content-factory\triage\tasks.md` — только как «новое, ещё не разобрано». Разбор = `python D:\Vault\_imports\content-factory\voice_task_promote.py pending|promote --src hub:NNNN|promote-live|verify`.
- Выход (глаза оператора): TG-группа «00 » 05 обработанные голосовые» chat_id chat_REDACTED, account "tonyssd", без parse_mode.
- ⚠️ КОРЕНЬ ЗАКРЫТ 03.08.2026 — 2 дня подряд (02.08, 03.08) рутина считала цифры, но НЕ могла отправить: `claude_run.py` инжектит `--strict-mcp-config` в headless-прогон (нет Telegram MCP), а инструкция ниже не называла MCP-НЕЗАВИСИМУЮ рельсу — агент разводил руками и оставлял текст в логе. Рабочий рецепт (проверен вживую 03.08, `BUSSEND OK`): отправляй через `tg_bus_send.py --raw "<текст>"` с `TG_BUS_GROUP=chat_REDACTED` (переопределяет дефолтный чат 03), БЕЗ MCP вообще — тот же Telethon-рельс, что `bus_ping.py`/`tg_bus_read.py` (сессия @TonySsd из `D:\Vault\_imports\dialogs\.env`). ⚠️ интерпретатор важен: дефолтный `python`/`python3` на хабе — pythoncore-3.14 БЕЗ telethon; используй `C:\Users\dev\AppData\Local\Programs\Python\Python312\python.exe` (telethon 1.44.0 стоит там) — проверь `pip show telethon`, если путь съехал. Пример (PowerShell): `$env:TG_BUS_GROUP="chat_REDACTED"; & "C:\Users\dev\AppData\Local\Programs\Python\Python312\python.exe" "%USERPROFILE%\.claude\scripts\tg_bus_send.py" --raw $msg`. Вывод `BUS-SEND OK -> ...` = доставлено; `BUS-SEND FAIL: No module named 'telethon'` = взят не тот python — переключись.

⚠️ КОРЕНЬ, КОТОРЫЙ ЗАКРЫТ 04.09.2026 — СБОРЩИК ЖИВЁТ НА ДИСКЕ, НЕ В ГОЛОВЕ СЕССИИ.
До 04.09 шаги 1-4 каждая сессия писала с нуля: ~100 строк питона на Opus каждую ночь
и заново те же дефекты. Замер 04.09: в отправленную сводку уехало «схема
сломана в 3» вместо 14 (взял из своего скана, а не из аудита) + сырой python-список
в поле blocked_by. Теперь сборка = два постоянных скрипта, 0 LLM, под тестом.
Сессия СВОЙ сборщик БОЛЬШЕ НЕ ПИШЕТ — только гонит готовые (шаг 1а) и шлёт.
Дом: `~/.claude/scripts/hanging_tasks/` — `scan_tasks.py` (реестр → JSON),
`build_msg.py` (JSON + голосовая + аудит + ask_debt → msg.txt), сетка `_test_build_msg.py`
(13 проверок, показана КРАСНОЙ на 3 сломах 04.09). В сборщике НИ ОДНОЙ захардкоженной
цифры: нет источника → явная строка «нет данных», битый скан → exit 1 (не пустая сводка).
Потолки списков (12 P0 / 6 P1 / 5 wip) ОБЯЗАНЫ объявляться в тексте — при 109 P0
и 298 P1 полный список = ~30к знаков = 8 сообщений = та самая свалка, которую рутина запрещает.

ШАГИ:
1а. СБОРКА ОДНИМ БЛОКОМ (предпочтительный путь, 0 токенов; шаги 1-2 он закрывает).
⚠️ Пути СПЕЦИАЛЬНО через forward-slash: обратные слеши в этом файле уже четыре раза
молча съедались как escape-последовательности (\v \a \b \1). Не «исправляй» их назад.
```
set H=%USERPROFILE%/.claude/scripts/hanging_tasks
set T=%TEMP%/ht
mkdir "%T%" 2>nul
python "%H%/scan_tasks.py" > "%T%/scan.json"
python D:/Vault/_imports/content-factory/voice_task_promote.py pending --json > "%T%/voice.json"
python "%USERPROFILE%/.claude/scripts/ask_debt.py" --days 7 --no-snapshot > "%T%/askdebt.txt"
python "%H%/build_msg.py" --scan "%T%/scan.json" --voice "%T%/voice.json" ^
  --audit D:/Vault/Vault-Knowledge/10-Tasks/_audit/audit-latest.json ^
  --askdebt "%T%/askdebt.txt" --out "%T%/msg.txt"
```
Затем прочитать `%T%/msg.txt` глазами (§3.6) и отправить по рецепту из шага 4.
Скрипт упал / не найден → сказать это вслух и уйти на ручные шаги 1-4 ниже, не молчать.
Сетка перед доверием: python "%H%/_test_build_msg.py"  (ждём GREEN).
1. РЕЕСТР: собери из `10-Tasks\task-*.md` незакрытые (state ∈ open|wip|blocked; inbox считай отдельной строкой «ждут критерия»). Дешёвым способом: `_audit\audit-latest.json`, если свежий (≤36ч), иначе прочитай frontmatter напрямую (0 токенов, без LLM).
2. ИНБОКС: `voice_task_promote.py pending --json` → сколько голосовых задач ещё не разобрано.
3. Ничего нигде → одна строка «📋 Висячих задач нет ✅» и выход.
4. Иначе отправь ОДНИМ сообщением (>4000 симв. — разбей), в таком порядке:
   «📋 Задачи на <дата>
   🔴 P0 (N): по строке — заголовок + владелец
   🟡 P1 (N): по строке
   ⏳ wip/blocked (N): заголовок + чем блокирована
   📥 новое из голосовых, не разобрано (N): заголовок + hub:id
   Итого открытых в реестре: N · someday: N · ждут критерия (inbox): N»
   P2/P3 не перечислять поимённо — только счётчиком (иначе сводка снова станет свалкой).
4б. ДОЛГ АВТОНОМНОСТИ (одна строка, 0 токенов LLM, добавлено 06.08.2026): прогони `python "%USERPROFILE%\.claude\scripts\ask_debt.py" --days 7 --no-snapshot` и возьми ТОЛЬКО шапку → строка вида «🙋 асков за 7 дн: N · протухло M (X%) · ложных 🚩K». Смысл: протухший аск = не «оператор занят», а «я спросил там, где не следовало» (память `asks-are-my-autonomy-debt`); 🚩 = формулировка «+ = да, займись», где ответ описывает работу самого робота. Скрипт READ-ONLY по `approvals.db`. Не печатать таблицы целиком — сводка не должна стать свалкой; детали смотрит человек командой `/ask-debt`. Скрипт не найден / упал → строка «🙋 замер долга не сработал (<причина>)», не молчание.
5. ЛОГ: счётчики по каждому блоку + факт отправки.

ОГРАНИЧЕНИЯ:
- Ничего наружу; только в папку chat_REDACTED.
- Приватность: чужие имена/@, суммы, лиды/CRM — обобщай.
- Windows cp1252: кириллицу НЕ печатать в stdout python — только в файлы/Telegram.
- Не выдумывай — только из файлов. Пусто из ОДНОГО источника ≠ «задач нет»: проверь оба.
- Закрывать задачи эта рутина НЕ имеет права — только читает и рапортует.

FINAL STEP (always run, deterministic heartbeat for the cron-watchdog, 0 tokens): run `python "%USERPROFILE%\.claude\scripts\cron_heartbeat.py" hanging-tasks-digest`

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
ШАГ 0 — ПЕРВЫМ ДЕЛОМ, до любой работы: python ~/.claude/scripts/routine_runlog.py tail hanging-tasks-digest
  Это записки последних 5 смен: что сделано, обо что споткнулись, что поменяли в этой инструкции, с чего начать. Не наступай на их грабли и не переделывай уже сделанное. Журнала нет — ты первая смена, работай по SKILL.md.
ФИНАЛ — ВСЕГДА, даже на пустом/тихом прогоне: python ~/.claude/scripts/routine_runlog.py add hanging-tasks-digest "сделал: ...; споткнулся: ...; правил SKILL.md: да/нет+что; следующей смене: ..."
  3-6 строк, только сигнал (не пересказ). Починил что-то в SKILL.md — напиши об этом ЯВНО: следующая смена обязана узнать о починке из журнала, а не открыть её заново.
</scheduled-task>

---

**Claude:**

You've hit your weekly limit · resets 5am (Europe/London)
