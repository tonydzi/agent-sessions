---
session: s_31b22b30
date: 2026-09-03
words: 1008
turns: 3
tools: "Bash, PowerShell"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-03 · Scheduled run: task-hygiene-shadow

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_31b22b30` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

четверг, утро, 05:19

---

> `Bash` -- {"command": "\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" \"$USERPROFILE/.claude/scripts/task_hygiene.py\"; echo \"RC=$?\"", "description": "Run task hygiene engine"}

---

> `Bash` -- {"command": "head -c 3000 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"", "description": "Read hygiene report header"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/\" | head -30; echo \"---\"; grep -rn \"PARK=\" \"$USERPROFILE/.claude/scripts/task_hygiene.py\" | head -5", "description": "List audit dir and check engine history"}

---

> `Bash` -- {"command": "tail -3 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-runs.jsonl\"", "description": "Read last runs history"}

---

> `Bash` -- {"command": "grep -n \"^## \" \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"; echo \"---\"; sed -n '/^## C\\./,/^## /p' \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\" | head -12", "description": "Inspect report sections"}

---

> `Bash` -- {"command": "grep -n \"add_argument\" \"$USERPROFILE/.claude/scripts/tg_bus_send.py\" | head -20", "description": "Check tg_bus_send arguments"}

---

> `PowerShell` -- {"command": "$msg = @'\n🧹 Гигиена реестра (понарошку, ничего не изменено), 03.09.2026\n\nA. припарковал бы: 75 (вчера 69)\nB. P0: сейчас 97 при потолке 7 → сверх 90; из них гниёт 75 — это и есть кандидаты на понижение\nC. открытых без критерия «сделано»: 217 (вчера 210); течёт мимо гейта: без метки 

---

> `Bash` -- {"command": "\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" \"$USERPROFILE/.claude/scripts/cron_heartbeat.py\" task-hygiene-shadow; echo \"RC=$?\"", "description": "Write cron heartbeat"}

---

**Claude:**

Прогон рутины `task-hygiene-shadow` за 03.09.2026 закончен. Ничего не менял — режим понарошку.

**Счётчики движка** (`task_hygiene.py`, rc=0):
`PARK=75 P0_OPEN=97 P0_OVER=90 P0_ROTTING=75 NO_ACC=217 SCRIPTED=0 AUDIT_AGE_H=0.8`

| Полоса | Что | Сегодня | Вчера (02.09) | Δ |
|---|---|---|---|---|
| A | припарковал бы (гниёт, не P0) | 75 | 69 | +6 |
| B | P0 сверх потолка 7 | 90 (P0=97, гниёт 75) | 86 | +4 |
| C | открытых без критерия «сделано» | 217 | 210 | +7 |
| — | всего открытых | 589 | — | — |

**Сигнал, а не просто цифры:** все три полосы растут третий день подряд (01.09 → 65/77/196, 02.09 → 69/86/210, 03.09 → 75/90/217). «Без движения» не было ни разу — реестр набирает долг быстрее, чем разгребается.

Течь по полосе C идёт мимо гейта `task_card_guard`: 127 карточек **без метки узла-родителя**, дальше NODE-0X 27, хаб 23, NODE-0X-NODE-0X 12. Рождённых скриптом — 0, значит пишут живые сессии, а не роботы.

Доставка доказана кодом: `LASTEXITCODE=0`, в выводе `BUS-SEND OK`. Сообщение ушло в папку `chat_REDACTED`. Heartbeat для крон-сторожа проставлен.

Отчёт целиком: [hygiene-latest.md](D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md)

🧒 Простыми словами: раз в сутки я пересчитываю, сколько задач у нас пылится, и просто говорю цифры — трогать их мне нельзя. Сегодня опять больше, чем вчера, и так третий день. Куча в 589 задач растёт сама, никто её не разбирает. Руки этому уборщику ты пока не давал — он умеет только считать и жаловаться.
