---
session: s_05a0ad6f
date: 2026-08-25
words: 999
turns: 3
tools: "Bash, PowerShell"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-08-25 · Scheduled run: task-hygiene-shadow

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_05a0ad6f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

**⏰ вторник, 25 августа 2026, 05:20**

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe\" \"$env:USERPROFILE\\.claude\\scripts\\task_hygiene.py\"; \"EXIT=$LASTEXITCODE\"", "description": "Run task hygiene engine"}

---

> `Bash` -- {"command": "head -c 4000 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\"", "description": "Read hygiene report header"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/\" | head -30; echo \"---C---\"; sed -n '/## C\\./,/^## /p' \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-latest.md\" | head -20", "description": "List audit dir and read section C"}

---

> `Bash` -- {"command": "tail -3 \"D:/Vault/Vault-Knowledge/10-Tasks/_audit/hygiene-runs.jsonl\"", "description": "Check previous hygiene runs for delta"}

---

> `PowerShell` -- {"command": "$msg = @'\n🧹 Гигиена реестра (понарошку, ничего не изменено), 25.08.2026\nA. припарковал бы: 18 (позавчера было 14)\nB. P0: сейчас 47 при потолке 7 → сверх 40; из них гниёт 20 — это и есть кандидаты на понижение\nC. открытых без критерия «сделано»: 137 (июльское легаси 50, августовские 

---

> `PowerShell` -- {"command": "& \"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe\" \"$env:USERPROFILE\\.claude\\scripts\\cron_heartbeat.py\" task-hygiene-shadow; \"RC=$LASTEXITCODE\"", "description": "Write cron heartbeat"}

---

**Claude:**

**⏰ вторник, 25 августа 2026, 05:21**

## 🧹 Гигиена реестра — прогон 25.08 (понарошку, ничего не тронуто)

| Полоса | Что | Сколько | Позавчера (23.08) |
|---|---|---|---|
| A | припарковал бы (гниёт, не P0) | **18** | 14 |
| B | P0 сверх потолка 7 | **40** (P0 всего 47, гниёт 20) | 43 |
| C | открытых без критерия «сделано» | **137** (июль 50 · август 87) | 136 |
| — | всего открытых | **411** | — |

Движение есть, «без движения» писать не надо: парковочная полоса +4, P0-перебор −3, полоса без критерия почти стоит (+1).

**Доставка доказана кодом:** движок rc=0, `tg_bus_send.py` rc=0 (`BUS-SEND OK` → −id_eee24e1c), heartbeat rc=0. Отчёт: [hygiene-latest.md](D:\Vault\Vault-Knowledge\10-Tasks\_audit\hygiene-latest.md)

**Что видно глазами в цифрах (не действие, наблюдение):**
- P0 растёт быстрее, чем чистится: 47 при потолке 7 — потолок фактически не работает как потолок.
- Полоса C течёт МИМО гейта `task_card_guard`: у 69 карточек из 137 вообще не помечен узел-родитель, значит писались не через Write/Edit-путь, где гейт стоит. Это корень, а не симптом.

Ничего не закрывал, не парковал, не понижал — по приказу 05.08 у этой рутины нет рук, решение о проде принимает оператор по цифрам за период.

🧒 **Простыми словами:** робот-уборщик ночью прошёл по списку задач и просто посчитал беспорядок, ничего не трогая. Задач-«срочных» 47 штук, а по правилам должно быть максимум 7. И у 137 задач не написано, как понять, что они сделаны — причём больше половины таких проскочили мимо сторожа, который должен был это ловить. Записку с цифрами я положил тебе в телеграм-папку, доставку проверил не глазами, а кодом.
