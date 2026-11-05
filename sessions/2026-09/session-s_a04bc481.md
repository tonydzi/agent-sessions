---
session: s_a04bc481
date: 2026-09-28
words: 642
turns: 1
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · Scheduled run: teach-podcast-queue

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a04bc481` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="teach-podcast-queue" file="C:\Users\dev\.claude\scheduled-tasks\teach-podcast-queue\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Ты ЕДИНСТВЕННЫЙ генератор учебных подкастов на флоте. Сессии оператора только КЛАДУТ заказы в очередь, генеришь их ты.

**Зачем ты есть (решение 28.09.2026, вопрос оператора голосом).** До тебя производителя не было: каждая сессия сама создавала блокноты и сама гоняла генерацию. Цена вылезла 26.09 за один вечер: две сессии на одной рельсе, ручная табличка ON AIR, риск двух исполнителей на одной очереди и сожжённых веером баков. Разделение простое: сессия думает и заказывает, ты исполняешь.

Границы: сессия (скилл `/teach-podcast`) пишет пакет, промпты RU и EN, создаёт блокнот, добавляет источники и делает `teach_backlog.py add`. Ты единственный зовёшь `teach_backlog.py run`. Карв-аут: эпизод под звонок сегодня или прямая просьба оператора «сгенери прямо сейчас» идёт из сессии напрямую мимо тебя, потому что FIFO не знает приоритетов и утопит срочное девятым в списке (грабля 21.09).

## Шаги

1. **Есть ли работа.** `python ~/.claude/scripts/_shared/teach_backlog.py status`. Строка «ждёт 0» → доклад одной строкой «очередь пуста» и выход. Ничего не поднимать, LLM не жечь.
2. **Не занята ли рельса.** Живой процесс `teach_backlog|notebooklm` в `Get-CimInstance Win32_Process` → выход со строкой «уже работает <pid>, не дублирую». Два исполнителя на одной очереди это тот самый веер, от которого предостерегает грабля 20.09.
3. **Табличка.** `python ~/.claude/scripts/onair.py declare --zone connectors --mode exclusive --title "teach-podcast-queue: ночная генерация N эпизодов"`. В конце прогона обязательно `onair close <id>`: истёкшая по TTL табличка это не закрытая табличка.
4. **Генерация.** `python ~/.claude/scripts/_shared/teach_backlog.py run --cooldown 45 --loop`. Порядок баков вшит (a2 → a → bb), ротация при лимите её работа, не твоя. Потолок ночи **12 эпизодов**; больше осталось, значит завтра, и это пишется в доклад числом.
5. **Проверка каждого свежего файла (§4.3-бис, второй заход другим методом).** Размер больше 1 МБ И длительность: `ffprobe -v error -show_entries format=duration -of csv=p=0 <файл>`. ⚠️ Заголовок `mvhd` у этих файлов пустой и врёт нулём, поэтому длительность только через ffprobe. Меньше 3 минут = брак: помечается в докладе, оператору как готовый не выдаётся.
6. **Учёт тем же прогоном.** В `D:\Vault\Vault-Knowledge\05-Resources\NotebookLM`: статус с длительностью в `_teach-curriculum.md`, строка в `_NotebookLM-Index.md`, проверить наличие строки в `_youtube-queue.md`. ⚠️ Колонка «Зачем» учебного плана уезжает в публичное описание YouTube (контракт 25.09): нет строки, у эпизода не будет блока заказа, а сочинять причину задним числом движку запрещено. Строки нет → пиши в доклад, чей это заказ, не выдумывай.
7. **Доклад в TG-03** через `bus_send.py`: сколько сгенерировано, сколько осталось в очереди, длительности, какие баки жгли, что забраковано.
8. **Два вердикта (§9.3-бис).** О скилле `/teach-podcast` и об ЭТОЙ своей инструкции: `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, каждый с причиной. Пустое «не надо» вердиктом не считается.

## Известные грабли, не переоткрывай
- **RU выходит втрое короче EN** при одинаковом `--length long`: замер 26.09 на серии recall дал RU 13-20 минут против EN 48-68 на тех же блокнотах. Класс `notebooklm-ru-episode-three-times-shorter-than-en`, 1-й датированный. Пока корень не найден, короткий русский эпизод это не брак рельсы, а известное поведение: в доклад числом.
- **Провал бывает ложным**: перед вердиктом «упал» сверь `notebooklm artifact list -n <id>`, сервер мог доделать, а поллер потерять (грабля 20.09).
- **Фоновая цепочка переживает TaskStop**: убивать процесс через `Get-CimInstance` + `Stop-Process -Force`, иначе через десять минут стартует вторая генерация.

Окно ночное, работай тихо. Tier-2 (деньги, апгрейд тарифа, необратимое удаление) = стоп и аск оператору, сама не решай.

Канон решения о разделении: память `podcast-routine-generates-session-only-orders`.

## Потребитель
оператор слушает в машине (память `dev-listens-to-teach-podcasts`: «ЗДОРОВО помогают»). Дальше по трубе очередь вычерпывает `/youtube-publish` на канал `@tonydzz`.
</scheduled-task>

---

> `Bash` -- {"command": "python ~/.claude/scripts/_shared/teach_backlog.py status 2>&1", "description": "Check teach-podcast backlog queue status"}
