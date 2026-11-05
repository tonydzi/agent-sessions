---
session: s_a9d4129d
date: 2026-10-02
words: 347
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-02 · Scheduled run: referral-lane-build-20261001

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a9d4129d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="referral-lane-build-20261001" file="C:\Users\dev\.claude\scheduled-tasks\referral-lane-build-20261001\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Задача от оператора (голосом 01.10.2026, «+» на вариант 5 реферральной полосы; миссия = гигантский поток собеседований, канон: Библия reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna §Поправка 01.10, память [[mission-metric-100-interviews]]).

RECALL первым ходом (память + brain_ask «реферралы ИИ-лаборатории знакомые»).

Вход: очередь D:\Vault\Vault-Knowledge\04-Projects\Pipe-A-Batches\referral-lane-candidates-20261001.md (201 карточка 07-People, упоминающая ИИ-лабораторию). Упоминание НЕ значит «работает там» — это сырой детектор.

Работа порциями (слон, не один присест): за прогон взять 40 карточек сверху, по каждой прочитать карточку и вынести вердикт прямо в файл очереди: works-at (человек работает в лаборатории) / knows (связан с ней: инвестор, бывший, друг сотрудника) / noise (шум детектора). Отметить чекбокс и приписать вердикт.

По каждому works-at и сильному knows: черновик короткой тёплой просьбы о реферрале ОТ ПЕРВОГО ЛИЦА оператора (без Майкрофта — карв-аут найма 14.09; без слов «фаундер»/«не-кодер»; правда в цифрах; по-человечески, без ИИ-слопа, с якорем на реальное знакомство из карточки — контекст в ней). Черновики сложить в D:\Vault\Vault-Knowledge\04-Projects\Pipe-A-Batches\referral-drafts-20261001.md.

ОТПРАВКА: тёплые личные касания класса Class1/C — слать САМ по одному в день готовности, с самого частого канала диалога (§9.12); масс-рассылка запрещена, это НЕ веер: каждое сообщение уникально и опирается на реальное знакомство. Сомнение «холодный или тёплый» = не слать, оставить черновиком с пометкой.

Не разобрав все 201 за прогон — поставить себе продолжение (одноразовая задача на завтра, тот же промпт). Доклад: строка в TG-03 через bus_send.py «referral-lane: X судено, Y works-at, Z черновиков, N отправлено».
</scheduled-task>

---

**Claude:**

Начинаю прогон задачи `referral-lane-build-20261001`. Сначала RECALL и проверка входа.

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches/\" 2>&1 | head -40", "description": "List Pipe-A-Batches dir"}

---

> `Bash` -- {"command": "cd ~/.claude && ls memory/ 2>/dev/null | head -5; echo \"---\"; ls scripts/bus_send.py scripts/rail_plan.py 2>&1", "description": "Check scripts exist"}
