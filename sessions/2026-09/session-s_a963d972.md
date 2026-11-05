---
session: s_a963d972
date: 2026-09-04
words: 1055
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-04 · Scheduled run: task-hygiene-shadow

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a963d972` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="task-hygiene-shadow" file="C:\Users\dev\.claude\scheduled-tasks\task-hygiene-shadow\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: task-hygiene-shadow
description: Ночной счётчик гигиены реестра задач (режим понарошку, ничего не меняет)
---

⚙️ РЕЛЬСА: SONNET (грунт). Эта рутина = механика, авторского голоса и суждения в ней нет.
Работай сам ТОЛЬКО если сессия уже на Sonnet. Если сессия стартовала на Opus/Fable — не жги
умный бак: передай ВСЮ содержательную работу субагенту через инструмент Agent с
`model: 'sonnet'` (промпт = шаги ниже целиком), а сам только прими его отчёт и заверши.
Детерминированные python-вызовы делай напрямую в любом случае — они 0 токенов.
Канон: CLAUDE.md §6.2 (маршрутизация), §6.3 (жечь оплаченные лимиты).

TASK_HYGIENE_SHADOW_AUTORUN

ЦЕЛЬ: раз в сутки посчитать гигиену реестра задач и положить оператору короткую сводку. Режим ПОНАРОШКУ (shadow): НИЧЕГО не менять, ни одной карточки не трогать. Автономный прогон, вопросов не задавать.

⚠️ ПОЧЕМУ ПОНАРОШКУ. Приказ оператора 05.08.2026 («+++» на пакет «гейт + парковка + лимит P0»). Канон §5.7: новая альфа сперва идёт shadow с замером, решение о проде принимает оператор по цифрам за период. Руки (--apply) намеренно НЕ построены. Эта рутина НЕ имеет права закрывать, парковать или понижать задачи — только считать и рапортовать.

ШАГИ:
1. Прогнать движок (0 токенов LLM, детерминированно):
   C:\Users\dev\AppData\Local\Programs\Python\Python312\python.exe "%USERPROFILE%\.claude\scripts\task_hygiene.py"
   Он печатает строку счётчиков PARK=.. P0_OPEN=.. P0_OVER=.. P0_ROTTING=.. NO_ACC=.. SCRIPTED=.. AUDIT_AGE_H=..
   и пишет отчёт в $OBSIDIAN_VAULT\10-Tasks\_audit\hygiene-latest.md
2. Если движок вернул не 0 — не молчать: доложить оператору строку ошибки и на этом закончить.
3. Прочитать шапку отчёта (первые ~40 строк) — там таблица и предупреждение о возрасте аудита.
4. Отправить оператору в TG-папку «00 » 05 обработанные голосовые» (chat_id chat_REDACTED) ОДНО короткое сообщение (до 1200 символов):
   «🧹 Гигиена реестра (понарошку, ничего не изменено), <дата>
    A. припарковал бы: N
    B. P0: сейчас M при потолке 7 → сверх K; из них гниёт G — это и есть кандидаты на понижение
    C. открытых без критерия «сделано»: N (июльское легаси / августовские — сколько)
    Итого открытых: N. Отчёт: 10-Tasks\_audit\hygiene-latest.md»
   Рельса ТОЛЬКО такая (у рутин нет MCP из-за --strict-mcp-config):
     $env:TG_BUS_GROUP="chat_REDACTED"; & "C:\Users\dev\AppData\Local\Programs\Python\Python312\python.exe" "$env:USERPROFILE\.claude\scripts\tg_bus_send.py" --raw $msg
   ⚠️ В тексте НЕ должно быть двойных кавычек и квадратных скобок — PowerShell рвёт по ним аргумент, сообщение уедет кусками.
   ⚠️ ДОСТАВКА ДОКАЗЫВАЕТСЯ КОДОМ ВЫХОДА, а не глазами (корень-фикс 21.08): сразу после отправки прочитай `$LASTEXITCODE`.
     0 = доставлено (в выводе будет «BUS-SEND OK»); 3 = НЕ доставлено — текст припаркован в спуле, но оператор его СЕЙЧАС не увидит.
     Код 3 — это ПРОВАЛ рутины: повтори попытку ещё дважды с паузой 2 секунды (не 20-30: за замок дерутся несколько роботов,
     длинный шаг систематически проигрывает гонку), и если всё ещё 3 — закончи прогон ГРОМКО: напиши в лог
     «ОТЧЁТ НЕ ДОСТАВЛЕН (rc=3)» и заверши шаг ненулевым кодом. Молчаливое «ну и ладно» запрещено: 21.08 ровно так
     двадцать SKIP-ов подряд выглядели успехом.
5. Если цифры не изменились со вчерашнего дня ВООБЩЕ (те же PARK/P0/NO_ACC) — так и написать одной строкой «без движения», это тоже сигнал.

ОГРАНИЧЕНИЯ:
- Ничего наружу, только в папку chat_REDACTED.
- Не выдумывать: все цифры только из вывода движка и отчёта.
- Windows cp1252: кириллицу не печатать в stdout python — только в файлы и в Telegram.
- Закрывать/паркать/понижать задачи ЗАПРЕЩЕНО. Эта рутина читает и считает.

FINAL STEP (всегда, детерминированный heartbeat для крон-сторожа, 0 токенов):
  python "%USERPROFILE%\.claude\scripts\cron_heartbeat.py" task-hygiene-shadow
</scheduled-task>

---

**Claude:**

[⏰ пятница, 05:20, 4 сентября 2026]

Рутина `task-hygiene-shadow` — прогон в режиме понарошку.

---

> `Bash` -- {"command": "\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" \"$USERPROFILE/.claude/scripts/task_hygiene.py\"; echo \"EXIT=$?\"", "description": "Run task hygiene engine"}

---

> `Bash` -- {"command": "sed -n '1,45p' \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"", "description": "Read hygiene report header"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/\" 2>/dev/null | head -20; echo \"---HISTORY---\"; grep -rn \"PARK=\" \"$USERPROFILE/.claude/logs/\" 2>/dev/null | tail -5", "description": "List audit dir and look for history"}

---

> `Bash` -- {"command": "tail -4 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-runs.jsonl\"", "description": "Read last hygiene runs history"}

---

> `Bash` -- {"command": "grep -n \"^## \" \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"; echo \"---C---\"; awk '/^## C\\./,0' \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\" | head -12", "description": "Inspect report sections"}

---

> `Bash` -- {"command": "grep -n \"add_argument\" \"$USERPROFILE/.claude/scripts/tg_bus_send.py\" | head -20", "description": "Check tg_bus_send options"}

---

> `Bash` -- {"command": "sed -n '120,160p' \"$USERPROFILE/.claude/scripts/tg_bus_send.py\"", "description": "Read tg_bus_send main"}

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a963d972/scratchpad\"\nmkdir -p \"$SP\"\ncat > \"$SP/hyg_msg.txt\" <<'EOF'\n🧹 Гигиена реестра задач (понарошку, ничего не изменено), 04.09.2026\n\nA. припарковал бы: 86 (вчера 75, +11)

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a963d972/scratchpad\"\n\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" \"$SP/hyg_send.py\" \"$SP/hyg_msg.txt\"; echo \"RC=$?\"", "description": "Send hygiene repo

---

> `Bash` -- {"command": "\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" \"$USERPROFILE/.claude/scripts/cron_heartbeat.py\" task-hygiene-shadow; echo \"RC=$?\"", "description": "Cron heartbeat"}

---

**Claude:**

**Прогон `task-hygiene-shadow` закрыт ✅ — движок exit 0, отчёт доставлен (rc=0), heartbeat поставлен.**

Счётчики на 04.09 05:20 и дельта к вчера:

| Полоса | Сегодня | Вчера (03.09) | Δ |
|---|---|---|---|
| A — припарковал бы | 86 | 75 | **+11** |
| B — P0 сверх потолка 7 | 102 (P0 всего 109, гниёт 82) | 90 | **+12** |
| C — без критерия «сделано» | 232 | 217 | **+15** |
| Всего открытых | 624 | — | — |

Не «без движения»: все три полосы растут четвёртый день подряд (01.09 → 04.09: 65→86 · 77→102 · 196→232). Реестр наполняется быстрее, чем разгребается.

Главный источник течи по полосе C — **134 карточки вообще без метки узла-родителя** (гейт `task_card_guard` их не видел, значит писались мимо Write/Edit); дальше хаб 28 и NODE-0X 27.

Руками ничего не тронуто — по приказу 05.08 рутина только считает; `--apply` намеренно не построен, решение о проде за оператором по цифрам за период (§5.7).

🎙 Майк: цифры уже третьи сутки говорят одно — теневой замер сам по себе долг не уменьшает, он его только красиво нумерует. Урожай по этой тени пора собирать: либо даём уборщику руки на полосу A (парковка обратима, риск низкий), либо честно признаём, что реестр растёт как свалка. Вопрос один: разрешаешь построить `--apply` только для полосы A с логом и откатом?

🧒 Простыми словами: я как ночной сторож обошёл склад задач и пересчитал коробки. Их стало больше, чем вчера: 86 давно пылятся, 109 помечены «самое срочное» (а можно только 7), 232 вообще без записки «когда считать сделанным». Я ничего не переставлял — только посчитал и отправил тебе записку в телеграм.
