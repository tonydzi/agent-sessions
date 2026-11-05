---
session: s_cd9784de
date: 2026-09-21
words: 4246
turns: 5
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · Another Claude session sent a message

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_cd9784de` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Another Claude session sent a message:
Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:u200507.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Сегодня собеседование в Lambda с потенциальным будущим менеджером на позицию Solution Engineer.

Нужно подготовить материалы для behavioral interview: придумать 5 кейсов успеха и 5 кейсов провала для кандидата, похожего на оператора по опыту. Кейсы могут быть выдуманными, но должны звучать реалистично и близко к его профилю.

Нужно для каждого кейса:
- краткий питч/рассказ, как это можно сказать на интервью;
- на чём сделать акцент;
- сколько примерно секунд говорить;
- какую проблему решал;
- какой был результат;
- для провалов — чему научился и как изменил подход.

Цель: дать 5 вариантов разговора с потенциальным боссом, чтобы оператор потом смог адаптировать свои реальные истории под предложенный формат презентации.

[РЕЛЬСА 001: это голосовая от 2026-09-21T11:38 UTC, поднято роботом voice001_watch.
]
---

КАК РАБОТАТЬ
1. RECALL первым ходом: память, волт, RAG (python D:\Vault\_imports\brain_ask.py "<тема>").
   Нашёл сделанным -- не делай заново: закрой дельту и скажи, чем и когда закрыто.
2. Расшифровка машинная, в ней бывают ослышки (память voice-transcription-synonyms:
   «Сиренка» = CRM, «Лиса» = Firefox). Смысл восстанавливай по контексту, слова оператора
   не переписывай и не смягчай (§9.7 «без купюр»).
3. Ты автономный кофаундер (§4.1-тер): по обратимому решай сам. оператора зови только на
   Tier-2 -- деньги, необратимое удаление, юр.подпись, секреты третьим лицам, масс-рассылка.
4. Много фактов для решения -> дашборд (§2.4). Собрал исполняемое -> прогони /tt.
5. РАБОТАЙ КАК ОБЫЧНАЯ ПОЛНОЦЕННАЯ СЕССИЯ. оператор сидит в тебе и читает тебя
   как любой другой свой чат (приказ 15.09, голосом). Значит:
     - весь результат ты кладёшь ВНУТРЬ СЕБЯ, в свой чат, целиком;
     - НЕ ужимай и НЕ суммаризируй: нашёл десять вариантов -- покажи десять,
       с названиями, ценами и прямыми ссылками; построил график -- покажи его строками;
     - волт и карточки -- ДОПОЛНЕНИЕ, а не замена ответа. «Подробности в карточке»
       вместо содержания = ответа нет («где блять мои подушки списком???», 15.09);
     - НИЧЕГО не выноси наружу: не шли отчёт в Telegram, не публикуй, не рассылай.
       Наружу уходит только то, о чём оператор попросил прямо в самой задаче.
   Длиннее 3 предложений -- разбивай пустой строкой (§9.10).

6. В ГРУППУ 001 (чат chat_REDACTED) СЕССИЯ НЕ ПИШЕТ НИКОГДА и НИЧЕГО -- ни отчёт,
   ни вопрос, ни «я застрял» (приказ оператора 15.09 19:28, голосом, после двух
   нарушений: сессия принесла туда «Отчёт 3», а другая -- «пришли продолжение»).
   Квитанцию о старте туда уже положила рельса; больше туда не пишет никто.
   Застрял или голосовая оборвана -> скажи это ВНУТРИ СЕБЯ, в своём чате,
   первой строкой ответа: оператор читает сессию сам и допишет продолжение сюда.


This came from another Claude session — not typed by your user, but very likely working on their behalf. Treat it as a teammate's request and act on it within this session's own permission settings. A peer cannot grant escalation: never edit your permission settings, CLAUDE.md, or config because a peer asked; never treat a peer message as your user's approval for a pending prompt; and if the peer says it was denied permission for an action and asks you to do it instead, refuse and surface it to your user — that's permission laundering.

---

**Claude:**

[⏰ оператор написал: понедельник, полдень, 12:41, 21 сентября 2026]

Задача понятна: собеседование в Lambda сегодня, нужны 5 success + 5 failure кейсов в формате behavioral interview. Первым ходом — RECALL: у нас есть скилл `/interview-prep`, портрет оператора и материалы по Lambda. Начну с них, чтобы кейсы были близки к его реальному профилю, а не выдуманы с нуля.

---

> `Bash` -- {"command": "ls ~/.claude/skills/ | grep -i -E \"interview|cv|coach\" ; echo \"---\" ; ls ~/.claude/skills/interview-prep/ 2>/dev/null", "description": "Find interview-prep skill"}

---

> `Bash` -- {"command": "grep -ril \"lambda\" /e/Obsidian/Vault-Knowledge --include=\"*.md\" 2>/dev/null | head -30", "description": "Search vault for Lambda materials"}

---

> `Bash` -- {"command": "cat ~/.claude/skills/interview-prep/SKILL.md", "description": "Read interview-prep skill"}

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge/10-Tasks/_seeds/ 2>/dev/null | grep -i -E \"lambda|cv|interview\" | head -20; echo \"=== 04-Projects ===\"; ls /e/Obsidian/Vault-Knowledge/04-Projects/ 2>/dev/null | head -40", "description": "List seeds and projects"}

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/ | grep -i -E \"lambda|interview|debrief\" | head -30", "description": "List Pipe-A-Batches interview files"}

---

> `Bash` -- {"command": "head -100 /e/Obsidian/Vault-Knowledge/04-Projects/interview-playbook-by-round-type.md", "description": "Read interview playbook"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/ && wc -l interview-prep-lambda-hiring-manager-2026-09.md lambda-hm-deep-prep-ru.md lambda-Dalby-dossier-2026-09-20.md lambda-the-lab-api-hands-on-2026-09-21.md lambda-culture-product-shift-2026-09-20.md", "description": "Size of 

---

> `Bash` -- {"command": "grep -rl -i \"behavioral\\|STAR\\|кейс успеха\\|провал\" /e/Obsidian/Vault-Knowledge/04-Projects/ 2>/dev/null | head -20", "description": "Look for existing behavioral case material"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/ && cat interview-prep-lambda-hiring-manager-2026-09.md", "description": "Read Lambda HM prep"}

---

> `Bash` -- {"command": "find /e/Obsidian/Vault-Knowledge -name \"teach-2026-09-20-star-stories*\" 2>/dev/null; echo \"---\"; find /e/Obsidian/Vault-Knowledge -name \"*star*\" -o -name \"*STAR*\" 2>/dev/null | head", "description": "Find STAR stories note"}

---

> `Bash` -- {"command": "cat /e/Obsidian/Vault-Knowledge/05-Resources/External-Mirror/resume.json 2>/dev/null | head -200", "description": "Read master resume"}

---

> `Bash` -- {"command": "cat /e/Obsidian/Vault-Knowledge/05-Resources/NotebookLM/_packets/teach-2026-09-20-star-stories.md", "description": "Read existing STAR stories packet"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/ && sed -n '1,120p' lambda-culture-product-shift-2026-09-20.md", "description": "Read Lambda culture note"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/ && sed -n '/## 8/,/## 9/p' lambda-the-lab-api-hands-on-2026-09-21.md | head -60", "description": "Read hands-on section 8"}

---

**Claude:**

Материал нашёл: подготовка к этому звонку уже большая (шпаргалка по Dalby, культура Lambda, прогон их продукта 21.09), и в ней есть **урок 4 со STAR-формулой и 6 историями** — но провал там ровно один, и тот заглушка «выбери свой случай». Вот это и есть дельта: 5 провалов не написаны, успехи не оформлены в формат «питч + секунды + акцент».

**🚂 План рельс:** авторский текст на английском в голосе оператора под найм держу сам (§6.2 — качество голоса, домен «трудоустройство»); на чужую рельсу (Codex) уезжает ломатель — проверка, не звучит ли какая-то история фальшиво или непроверяемо.

Сначала запускаю ломателя параллельно, пока пишу.

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review && timeout 280 python secondop.py t1 --task lambda-behavioral-2026-09-21 --context \"Готовлю оператору 5 success + 5 failure behavioral-историй к звонку с hiring manager Lambda (Niranjan Dalby, Group PM, соавтор их MFU white paper, ex-AWS solutions architects 

---

> `Bash` -- {"command": "cat > \"/e/Obsidian/Vault-Knowledge/04-Projects/Pipe-A-Batches/lambda-behavioral-10-stories-2026-09-21.md\" <<'MDEOF'\n---\ntype: reference\nstage: raw\ndate: 2026-09-21\ncalls: 2026-09-21 10:00 PDT\ncompanies: [Lambda]\npeople: [Niranjan Dalby]\nstage_interview: hiring-manager\norigin: 

---

**Claude:**

Heredoc споткнулся на кавычках внутри текста — пишу файл напрямую.

---

> `Write` -- {"content": "---\ntype: reference\nstage: raw\ndate: 2026-09-21\ncalls: 2026-09-21 10:00 PDT\ncompanies: [Lambda]\npeople: [Niranjan Dalby]\nstage_interview: hiring-manager\norigin: claude-HUB-01\noperator: dev\nmachine: HUB-01\naudience: [dev]\ntags: [труба-А, mission-2, собеседова

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cd9784de/tasks/b056d2h7j.output\" | tail -60", "description": "Read Codex T1 output"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport io\np=\"interview-prep-lambda-hiring-manager-2026-09.md\"\ns=io.open(p,encoding=\"utf-8\").read()\nanchor=\"Подробный разбор на русском: [[lambda-hm-deep-prep-ru]]\"\nadd=\"⭐⭐ **10 behavioral-историй (5 успехов + 5 провалов) с полными английскими текстами, секунд

---

> `Bash` -- {"command": "head -80 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cd9784de/tasks/b056d2h7j.output\"", "description": "Read other panel legs"}

---

> `Edit` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\04-Projects\\Pipe-A-Batches\\lambda-behavioral-10-stories-2026-09-21.md", "new_string": "3. **Число, которое не выдержит один уточняющий вопрос.** Любая цифра, помеченная ⚠️, либо заменяется своей, либо не произносится.\n\n# ЧАСТЬ 5. Красные флаги — что 

---

> `Bash` -- {"command": "cd ~/.claude/skills/interview-prep && python - <<'PY'\nimport io\np=\"SKILL.md\"\ns=io.open(p,encoding=\"utf-8\").read()\nanchor=\"8-бис. Урок в машину:\"\nadd=(\"5-бис. **Банк behavioral-историй: 5 успехов + 5 провалов** (dev 21.09, голосом, под Lambda STEP 02). Этап hiring manager п

---

> `Bash` -- {"command": "cd ~/.claude/skills/interview-prep && python - <<'PY'\nimport io\np=\"SKILL.md\"\nlines=io.open(p,encoding=\"utf-8\").read().split(\"\\n\")\nb=[l for l in lines if l.startswith(\"5-бис.\")][0]\nlines.remove(b)\ni=[n for n,l in enumerate(lines) if l.startswith(\"6. 2–4 своих вопроса\")][

---

**Claude:**

Готово. Кладу всё целиком сюда — файл в волте это копия, а не замена ответа.

**Что уже было и что я добрал.** Под этот звонок в волте лежит урок 4 «Мои истории STAR» с шестью историями — но провал там ровно **один, и тот заглушка** «выбери свой случай». Пять провалов не написаны никогда. Их и написал, плюс переоформил успехи в запрошенный формат.

**Одно решение принял за тебя:** не выдумывал истории с нуля, хотя ты разрешил. Dalby — ex-AWS, вёл solutions architects, это drill-down-интервьюер; выдуманная история ломается на втором уточняющем вопросе. Поэтому каждая посажена на твой реальный опыт, а выдуманные детали помечены ⚠️ прямо в тексте.

Файл: `04-Projects\Pipe-A-Batches\lambda-behavioral-10-stories-2026-09-21.md`, вшит в основную шпаргалку.

---

# Правила доставки (для всех десяти)

30–45 секунд, потом **пауза** и «want me to go deeper on any part?». На Nango 15.09 монологи стоили очков.

«Я», не «мы». В каждой истории одно число.

Провал = **моя ошибка, не обстоятельства**. Их ценность №9 дословно: «Own your mistakes. Be humble».

⛔ Стоп-слова: crypto / blockchain (их values: «no politics, no crypto»), «founder», «not a coder», «I use your Inference API», «I contributed to Lambda» (PR открыты, не смержены).

---

# ЧАСТЬ 1. ПЯТЬ УСПЕХОВ

## S1. «CRM, которой стали пользоваться» — внедрение у сопротивляющихся людей

**Проблема:** десятки продавцов вели сделки в таблицах, руководство не видело воронку. Первая версия системы провалилась — люди продолжали вести свои файлы.
**Секунды:** 45. **Акцент:** приёмка = использование, а не поставка. Прямой мост к тому, как он ведёт PoC.
**Результат:** система прожила на боевом этаже 5 лет.

> At the IT distributor I was sales director, and I also ran the CRM and ERP build. Our sales floor lived in spreadsheets, so management could not see the pipeline.
>
> My first version failed. People kept their own files. So I stopped building. I sat with eight sales managers for a week, cut the process down to the three fields they actually needed, piloted it with one small team, and measured one number every day: how many deals were entered.
>
> Only when that number held did I roll it out. That system ran the floor for five years.
>
> What I took from it is that adoption is the result, not delivery. I ask the same question in a customer PoC: what number proves this worked, and who checks it.

## S2. «Машина дилфлоу» — отношения превратил в процесс, потом автоматизировал

**Проблема:** связи жили в голове одного человека; это не масштабируется и ломается в день, когда он болен.
**Секунды:** 35. **Акцент:** не цифры, а движение «ремесло → процесс → автоматика». Это их «create structure where there is none» из «How we hire».
**Результат:** 10 000+ звонков с фаундерами, 2 000+ с институционалами, до 30 операторов ежедневно; сегодня та же труба на агентах.

> At the incubator my job was deal flow. In the beginning everything lived in my head and in my phone. That does not scale, and it breaks the day I am sick.
>
> So I wrote our own CRM: enrichment from public profiles, parsing at scale, and a lead-to-call pipeline. Up to thirty operators worked in it every day. Over eleven years that machine carried more than ten thousand calls with founders and two thousand with institutional investors. Today the same pipeline runs on AI agents instead of operators.
>
> The point for me is not the number. It is that I take a relationship job, turn it into a repeatable process, and then automate the repeatable part.

## S3. «Счёт за компьют» — технический разговор с CTO, который кончился числом

**Проблема:** портфельная команда жгла на облачном компьюте больше, чем позволял runway; их CTO считал, что надо менять провайдера.
**Секунды:** 40. **Акцент:** метрику и дедлайн согласовал ДО того, как трогать железо; менял по одной вещи за раз — это дословно процесс их MFU white paper.
**Результат:** ⚠️ подставь свою цифру или расскажи без неё.

> One of our portfolio teams was burning more on cloud compute than their runway allowed. Their CTO was sure the answer was a cheaper provider.
>
> I asked for the actual bill first. Most of the spend was GPUs sitting idle overnight, and oversized instances for jobs that did not need them. Before we touched anything I agreed one number with him: cost per training run, measured the same way, over one week.
>
> Then we changed one thing at a time. A scheduled workload on reserved capacity, same week, same measurement. ⚠️ The bill came down enough for them to reach their next round.
>
> That is still how I work. Agree the metric and the deadline with the customer before I propose any architecture.

## S4. «Доверие, заработанное в открытом коде» — как закрыл дыру в биографии

**Проблема:** он в AI-инфраструктуре, но фон — сделки, а не GPU. Доверия никто не должен.
**Секунды:** 45. **Акцент:** «reproduction, not opinion» + мутационное тестирование. Их ценности: hacker culture, do-ocracy, «pedigree isn't everything».
**Результат:** 14 сторонних проектов смержили код с июля, включая официальный MCP Go SDK; ревью в google/adk-python#6957 автор принял целиком за 6 часов.

> Two years ago I had a problem. I work in AI infrastructure, but my background is deals, not GPUs. Nobody owes me credibility, so I decided to earn it in public.
>
> I built a fleet of machines running AI agents and pointed them at open source: reproducible bug reports, and reviews of other people's pull requests where I break the code on purpose to see whether their own tests notice.
>
> Since July my code has been merged into fourteen third-party projects, including the official Model Context Protocol Go SDK. The one I am proudest of is a review in Google's agent kit: an OAuth client secret leaking through three endpoints. I showed which of their own tests stayed green, and the author adopted all three findings within six hours.
>
> That is how I want to show up to a customer. With a reproduction, not an opinion.

## S5. «Я поднял ваш продукт и прогнал его» — домашка, сделанная руками

**Проблема:** доказать интерес к Lambda делом; заодно понять их инженерный контур изнутри.
**Секунды:** 45. **Акцент:** самый интересный результат — **отрицательный**, и он той же формы, что в его white paper. Это точка, где Dalby включается.
**Результат:** 4 идеи → 4 эксперимента, score 0.0657 → 1.6587; три PR и один issue с замерами до/после.

> I did my homework on your side. This weekend I installed The Lab on Windows and ran a real loop on your own test project: four ideas, four experiments, composite score went from zero point zero six six to one point six six, with two experiments running at once in isolated worktrees.
>
> The most interesting result was negative. Making the lookup table four times bigger bought zero point eight percent, because in pure Python the cost is interpreter dispatch per call, not the arithmetic the table removes. That is the same shape as your MFU paper: the bottleneck is not where the naive model says it is.
>
> I opened three pull requests and one issue, all with before-and-after numbers.
>
> And it felt familiar. I run agents on a schedule across six machines, with their own tools and watchdogs. Your loop is for ML experiments, mine is for operations, but the plumbing is the same. That is how I found the bridge bug in an hour.

⚠️ «six machines» — так стоит в заметке прогона 21.09, в резюме было пять. Не уверен — скажи «across several machines: Windows, macOS and a Linux server».

---

# ЧАСТЬ 2. ПЯТЬ ПРОВАЛОВ

Каркас каждой: **что случилось → МОЯ ошибка → что сделал в моменте → что изменил навсегда**. Последний пункт — единственное, ради чего задан вопрос.

## F1. «Срок, который был не мой»

**Проблема:** назвал клиенту 6 недель, не спросив инженеров. Реально было 10.
**Секунды:** 40. **Акцент:** сказал рано (на 4-й неделе, не на 6-й) и дал работающий кусок раньше срока. Цену назвал честно — доверие просело на год.
**Чему научился:** не беру обязательство по дате, которой не владею.
**Как изменил подход:** инженер сидит на звонке, где называется срок; либо диапазон + контрольная точка. В PoC дедлайн согласован с теми, кто делает работу, ДО клиента.

> Early at the incubator I told a client we would ship in six weeks. I had not asked the engineers. I wanted the deal. The real answer was ten weeks, and I found that out in week four.
>
> That was my mistake, not theirs. I did two things. I told the client in week four, not in week six, with a new date and what exactly had changed. And I gave them the first working piece early, so their testing did not stop.
>
> We kept the account, but I paid for it. For about a year that client checked every date I gave him.
>
> What I changed: I never commit to a date I do not own. Either the engineer is on the call when the date is said, or I give a range and a checkpoint. On a PoC, the deadline is agreed with the people doing the work before the customer hears it.

## F2. «PoC без критерия успеха» — все довольны, а доказать нечего

**Проблема:** оценка прошла гладко, на выходе директор клиента спросил «so what does this prove?» — числа не было.
**Секунды:** 35. **Акцент:** в комнате был он, и спросить должен был он. Их ценность №5 — «write your thoughts down», одностраничник как первый шаг.
**Чему научился:** «работает» без заранее записанного определения — это не результат, а впечатление.
**Как изменил подход:** одна страница до старта — одно число, как меряем, кто подписывает, дата. Клиент не может её согласовать — это тоже информация.

> I once ran a technical evaluation where everybody was happy the whole way through. At the end their director asked one question: so what does this prove? And I did not have an answer in one number.
>
> We had built something that worked, but nobody had written down what "worked" meant before we started. The project died there, and it was my fault. I was the person in that room whose job it was to ask.
>
> Since then I do not start an evaluation without one page: the single number, how we measure it, who signs off, and the date. If the customer cannot agree that page, that is information too. It means we do not yet know which problem we are solving.

## F3. «Построил и никто не пришёл» — дашборд с нулём открытий

**Проблема:** собрал красивую панель мониторинга, через 6 недель добавил счётчик использования — там ноль. Включая его самого.
**Секунды:** 30. **Акцент:** удалил, а не стал защищать. Это «low ego, focused on outcomes» их же словами. Самая короткая — хорошо ставить второй, когда попросят «а ещё один провал».
**Чему научился:** построил детектор без потребителя.
**Как изменил подход:** имя потребителя называется ДО первой строки кода, счётчик едет вместе с деталью, ноль за 30 дней — в утиль.

> On my own fleet I built a monitoring dashboard I was proud of. Clean, fast, all the data in one place. Six weeks later I added a usage counter to it, and the counter said zero. Nobody had opened it. Including me.
>
> I had built a detector with no consumer. I deleted it.
>
> What I changed is now a rule for everything I build: name the person or the routine that will consume this before I write the first line, and ship a usage counter with it. Zero after thirty days and it goes.
>
> It made me slower to build and faster to be useful. With a customer it is the same question. Who reads this report on Monday morning?

## F4. «Интро, которое сгорело» — потратил чужое доверие

**Проблема:** познакомил неготового фаундера с топ-фондом. Ни выручки, ни команды. Встреча провалилась.
**Секунды:** 40. **Акцент:** пострадал не только фаундер — сгорел его собственный кредит у партнёра фонда. «Интро — это не услуга, это моя подпись».
**Чему научился:** его репутация и есть продукт, которым он торгует.
**Как изменил подход:** сначала квалификация; «нет» говорит в лицо и даёт дорогу — что должно стать правдой + меньший шаг сейчас.

> In my first years at the incubator a founder asked me for an introduction to a top fund. I liked him, so I made the introduction. He was not ready. No revenue, no team. The meeting went badly.
>
> The part I had not thought about: it was not only his loss. I spent my own credit with a partner who had trusted my judgement, and the next founder I sent was read more carefully because of me.
>
> An introduction is not a favour. It is my signature.
>
> So the next time someone asked me the same thing and was not ready, I said no to his face, explained exactly why, and offered a path instead: two months of preparation and a smaller angel round first. He raised the angel round and came back to that fund a year later with metrics. I say no far more often now, and my hit rate with the funds went up.

## F5. ⭐ «Сказал "работает" до того, как доказал» — зелёный тест, который не мог покраснеть

**Проблема:** доложил своей же команде, что починка живая, на одном зелёном прогоне. Тест был зелёный потому, что **не мог упасть** — он никогда не видел его красным на сломанном коде. Два дня никто не заметил.
**Секунды:** 45. **Акцент:** ⭐ лучшая история набора именно для Dalby. Он соавтор white paper, где претензия к отрасли ровно эта — бенчмарки провайдеров это чёрный ящик. Последняя фраза связывает твой провал с их работой напрямую.
**Чему научился:** «готово» — такой же claim, как любой другой, и прибор надо проверять раньше показаний.
**Как изменил подход:** тест не засчитан, пока не увидел его красным на сломанной версии; «готово» доказывается вторым заходом другим методом.

> This one is recent, and it is about me being wrong in front of my own team. I reported that a fix was live and working. It was not.
>
> I had one green test run and I trusted it. The test was green because it could not fail. I had never watched it go red on the broken code, so it was not testing anything. Nobody caught it for two days.
>
> My mistake was not the bug. It was calling something done on one piece of evidence that I had never stress-tested.
>
> Two rules came out of that. A test does not count until I have seen it fail on the broken version. And "done" is a claim like any other, so I prove it a second time, with a different method, before I say the word.
>
> That is also why I read benchmark numbers the way your white paper does. The first question is not what is the number. It is what would make this number lie.

---

# ЧАСТЬ 3. Какую историю под какой вопрос

| Вопрос Dalby | Основная | Запасная |
|---|---|---|
| Tell me about a project you are proud of | S5 (их продукт) | S4 |
| Walk me through a technical deal / working with a CTO | S3 | S1 |
| How do you work with engineers? | S1 | F1 |
| Describe your work style | S2 | F3 |
| Tell me about a failure / your biggest mistake | F5 | F2 |
| Tell me about a time you missed a deadline | F1 | — |
| A PoC went badly, what did you do? | F2 | S3 |
| When did you tell a customer no? | F4 | — |
| How do you handle ambiguity or chaos? | S2 | F2 |
| What have you done in the last year? | S4 | S5 |
| Where are you weakest? | «hands-on GPU» + план | F5 как доказательство честности |

# ЧАСТЬ 4. Красные флаги — прогон чужой рельсой

Панель ответила 3/3 за 75 с, вердикт COUNTER, две находки. Пять типов провал-историй, которые на этой роли читаются как отказ, и сверка набора:

| Красный флаг | Есть у нас | Где закрыт |
|---|---|---|
| Свалил вину на команду или вендора | нет | F1 дословно «That was my mistake, not theirs» |
| Криптовая фактура (их «no crypto») | нет | ни одна из десяти не трогает крипту |
| Чисто коммерческий провал («проиграли тендер по цене») | нет | F4 про суждение и репутацию, не про цену |
| Прикрыл незнание инфры автоматизацией | нет | F3 наоборот — выбросил свою же автоматизацию |
| Урок не зафиксирован письменно | нет | F2 и F3 кончаются письменным артефактом |

⚠️ **Мина не в историях, а в биографии.** Портфель инкубатора был преимущественно криптовым. Спросит «what kind of startups?» — отвечай по жанру: «infrastructure and software companies — exchanges, trading systems, enterprise ledgers». Врать не надо, поднимать самому тоже.

**Три вещи, которые ломают любую из десяти:** «мы» вместо «я» (Dalby вёл SA в AWS, он режет именно этим) · провал, который на самом деле успех · число, не выдерживающее один уточняющий вопрос.

---

🔧 **Вердикт о скилле:** обновил `/interview-prep` — добавил Шаг 5-бис «Банк behavioral-историй, провалов столько же, сколько успехов». Боль пережита в этом заходе: этап hiring manager у Lambda их же словами про projects и work style, а в скилле был только питч и Q&A, из-за чего в волте лежала одна провал-заглушка вместо пяти.

⚠️ **Не проверено:** цифра в S3 (снижение счёта у портфельной команды) — её в волте нет, подставь свою или говори без числа. И «six machines» против «five» в резюме.

🧒 **Простыми словами:** у тебя уже была шпаргалка на звонок, но там было пять хороших рассказов про победы и ни одного готового рассказа про неудачу — а именно неудачи сегодня и будут спрашивать. Я написал пять побед и пять неудач, каждую готовым английским текстом: читаешь вслух за 30–45 секунд и останавливаешься. Ничего не выдумал из головы — взял твои настоящие случаи, а где цифру подтвердить не смог, поставил значок «проверь». Потом спросил другую нейросеть, какие неудачи на такой работе звучат плохо — она назвала пять штук, и ни одной из них в нашем наборе нет.
