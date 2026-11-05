---
session: s_27760a7b
date: 2026-09-08
words: 1651
turns: 3
tools: "PowerShell, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-08 · Scheduled run: hanging-tasks-digest

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_27760a7b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="hanging-tasks-digest" file="C:\Users\dev\.claude\scheduled-tasks\hanging-tasks-digest\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: hanging-tasks-digest
description: Ежедневно (05:52 Лиссабон) — сводка ВИСЯЧИХ задач оператору в TG-папку. Источник истины = реестр 10-Tasks; голосовая очередь показывается ТОЛЬКО как «новое, не разобрано». [HUB HUB-01; account tonyssd]
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
</scheduled-task>

---

**Claude:**

Вторник, 13:17.

Запускаю рутину сводки висячих задач. Сборщик детерминированный (0 токенов LLM), делаю напрямую.

---

> `PowerShell` -- {"command": "$H = \"$env:USERPROFILE\\.claude\\scripts\\hanging_tasks\"; $T = \"$env:TEMP\\ht\"; if (-not (Test-Path $T)) { New-Item -ItemType Directory -Force $T | Out-Null }; Get-ChildItem $H -ErrorAction SilentlyContinue | Select-Object Name, Length, LastWriteTime", "description": "List hanging_t

---

> `PowerShell` -- {"command": "$H = \"$env:USERPROFILE\\.claude\\scripts\\hanging_tasks\"; python \"$H\\_test_build_msg.py\"; \"EXIT=$LASTEXITCODE\"", "description": "Run build_msg test grid"}

---

> `PowerShell` -- {"command": "$H = \"$env:USERPROFILE\\.claude\\scripts\\hanging_tasks\"; $T = \"$env:TEMP\\ht\"; python \"$H\\scan_tasks.py\" > \"$T\\scan.json\"; \"scan_exit=$LASTEXITCODE size=$((Get-Item \"$T\\scan.json\").Length)\"", "description": "Scan task registry to JSON"}

---

> `PowerShell` -- {"command": "$T = \"$env:TEMP\\ht\"; python D:/Vault/_imports/content-factory/voice_task_promote.py pending --json > \"$T\\voice.json\"; \"voice_exit=$LASTEXITCODE size=$((Get-Item \"$T\\voice.json\" -ErrorAction SilentlyContinue).Length)\"; python \"$env:USERPROFILE\\.claude\\scripts\\ask_debt.p

---

> `PowerShell` -- {"command": "$a = \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/audit-latest.json\"; if (Test-Path $a) { $f = Get-Item $a; \"audit age_h=\" + [math]::Round(((Get-Date) - $f.LastWriteTime).TotalHours,1) + \" size=\" + $f.Length } else { \"audit MISSING\" }", "description": "Check audit file freshness

---

> `PowerShell` -- {"command": "$H = \"$env:USERPROFILE\\.claude\\scripts\\hanging_tasks\"; $T = \"$env:TEMP\\ht\"; python \"$H\\build_msg.py\" --scan \"$T\\scan.json\" --voice \"$T\\voice.json\" --audit D:/Vault/Vault-Knowledge/10-Tasks/_audit/audit-latest.json --askdebt \"$T\\askdebt.txt\" --out \"$T\\msg.txt\"; 

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\ht\\msg.txt"}

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe\" -m pip show telethon 2>&1 | Select-String -Pattern \"^(Name|Version|Location)\"", "description": "Verify telethon in Python312"}

---

> `PowerShell` -- {"command": "$env:TG_BUS_GROUP=\"chat_REDACTED\"; $msg = Get-Content \"$env:TEMP\\ht\\msg.txt\" -Raw -Encoding UTF8; & \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe\" \"$env:USERPROFILE\\.claude\\scripts\\tg_bus_send.py\" --raw $msg; \"SEND_EXIT=$LASTEXITCODE\"", "descrip

---

> `PowerShell` -- {"command": "python \"$env:USERPROFILE\\.claude\\scripts\\cron_heartbeat.py\" hanging-tasks-digest; \"HB_EXIT=$LASTEXITCODE\"", "description": "Deterministic cron heartbeat"}

---

**Claude:**

**Сводка отправлена** в TG-папку `chat_REDACTED` (`BUS-SEND OK`, 3220 знаков, одно сообщение).

## Счётчики прогона

| блок | число |
|---|---|
| Реестр `10-Tasks`, открытых | **747** (open 649 · wip 69 · blocked 29) |
| P0 | 186 (в сводке перечислено 12, потолок объявлен) |
| P1 | 323 (перечислено 6, потолок объявлен) |
| someday | 232 |
| ждут критерия (inbox) | 9 |
| Без критерия «сделано» | 324 |
| Гниёт без хода | 271 |
| Схема сломана | 4 · нечитаемых 0 |
| Голосовая очередь (инбокс) | 473 «не разобрано», из них 358 старше 30 дней; за 7 дн — 9 новых |
| 🙋 Долг асков за 7 дн | 33, протухло 33 (**100%**), ложных 0 |

**Рельса:** механика целиком детерминированная — `scan_tasks.py` → `voice_task_promote.py` → `ask_debt.py` → `build_msg.py`, 0 токенов LLM на сборку. Сетка `_test_build_msg.py` прогнана до доверия: **GREEN 13/13**. Аудит индексатора свежий (8.8ч, порог 36ч). Отправка — Telethon-рельсой через Python312 (telethon 1.44.0), без MCP.

**Что бросается в глаза** (рапорт, не действие — закрывать задачи рутина права не имеет):
- 🚩 **асков протухло 100% из 33.** По памяти `asks-are-my-autonomy-debt` это не «оператор занят», а «спрашивал там, где надо было решать самому». Тридцать три из тридцати трёх — это не хвост, это система.
- Самый старый P0 гниёт **18 дней**, самый старый P1 — **63 дня** (судьба vault git: 1734 D / 505 M / 491 ??).
- Одиннадцать из двенадцати верхних P0 — однотипные «класс X стал системным, нужна отдельная сессия починки», все висят 17 дней. Сессии-починки заводятся, но не поднимаются: в очереди спавна 83 сида.

🧒 Простыми словами: я сходил в твой список дел, пересчитал всё по-честному и положил тебе в телеграм короткую бумажку. Дел много — 747 незакрытых. Ещё нашёл смешное и грустное: за неделю я 33 раза спросил у тебя разрешения, и все 33 вопроса протухли без ответа. Значит, я слишком часто дёргаю тебя вместо того, чтобы решать сам.
