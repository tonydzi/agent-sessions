---
session: s_a3a37f96
date: 2026-08-31
words: 1003
turns: 3
tools: "Bash, PowerShell"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-08-31 · Scheduled run: task-hygiene-shadow

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a3a37f96` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

[⏰ понедельник, утро, 05:20, 31 августа 2026]

Запускаю движок гигиены.

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe\" \"$env:USERPROFILE\\.claude\\scripts\\task_hygiene.py\"; \"EXIT=$LASTEXITCODE\"", "description": "Run task hygiene engine"}

---

> `Bash` -- {"command": "sed -n '1,45p' \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"", "description": "Read hygiene report header"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/\" | head -30; echo \"---C---\"; grep -n \"^## C\" -A 8 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\" | head -20", "description": "List audit dir and read section C"}

---

> `Bash` -- {"command": "tail -4 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-runs.jsonl\"", "description": "Read hygiene run history"}

---

> `Bash` -- {"command": "sed -n '135,165p' \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"", "description": "Read section C detail"}

---

> `PowerShell` -- {"command": "$msg = @'\n🧹 Гигиена реестра (понарошку, ничего не изменено), 31.08.2026\nA. припарковал бы: 62\nB. P0: сейчас 73 при потолке 7 → сверх 66; из них гниёт 50 — это и есть кандидаты на понижение\nC. открытых без критерия «сделано»: 182 (июльское легаси 49 / августовские 133)\nИтого открыты

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe\" \"$env:USERPROFILE\\.claude\\scripts\\cron_heartbeat.py\" task-hygiene-shadow; \"RC=$LASTEXITCODE\"", "description": "Write cron heartbeat"}

---

**Claude:**

[⏰ понедельник, утро, 05:22, 31 августа 2026]

Рутина отработала. Ничего не менял — только посчитал и доложил.

| Полоса | Что | Сегодня | Вчера | Δ |
|---|---|---|---|---|
| A | припарковал бы (гниёт, не P0) | **62** | 57 | +5 |
| B | P0 сверх потолка 7 | **66** (P0 всего 73, гниёт 50) | 58 | +8 |
| C | открытых без критерия «сделано» | **182** (июль 49 / август 133) | 173 | +9 |
| — | всего открытых в реестре | 518 | — | — |

Движок: exit 0. Доставка в TG-папку «00 » 05 обработанные голосовые» подтверждена кодом выхода (`BUS-SEND OK`, rc=0). Heartbeat поставлен.

Что видно поверх цифр (это уже моё суждение, не вывод движка):
- Четвёртые сутки подряд растут **все три** полосы. С 26.08 неделя: A 25→62, B 48→66, C 147→182. Реестр не просто не убирается — он пополняется быстрее, чем закрывается.
- Полоса C (182 карточки без критерия «сделано») течёт **мимо гейта** `task_card_guard`: гейт ловит запись через Write/Edit, а 99 из 182 карточек даже не помечены узлом-родителем. То есть их пишет что-то, что мимо гейта проходит.

Отчёт целиком: [hygiene-latest.md](D:\Vault\Vault-Knowledge\10-Tasks\_audit\hygiene-latest.md)

🧒 Простыми словами: я как уборщик, которому запретили трогать вещи — только пересчитать и сказать вслух. Пересчитал: в комнате 518 несделанных дел, из них 66 помечены «срочно-срочно» сверх нормы (норма — семь), а 182 записаны так, что непонятно, когда их считать сделанными. И куча растёт четвёртый день подряд. Руки мне давать или нет — решаешь ты.
