---
session: s_f85329eb
date: 2026-10-26
words: 1744
turns: 7
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · Давай изучим из гитхаб и подумаем что законтрибютить??

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f85329eb` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Давай изучим из гитхаб и подумаем что законтрибютить??

**В опенсорсе нашли способ почти вдвое увеличить вычислительную мощность RTX 3090**

Проект gpu-unlock за пару дней набрал уже более 5 тысяч звезд на GitHub: https://github.com/Zagitta/gpu-unlock. 

Разбираемся. 

У видеокарт GeForce 30-й серии (к ним относятся RTX 3080, 3090, 3090 Ti и тд) тензорные ядра умеют перемножать матрицы в FP16 и BF16 с накоплением результата в FP32. Именно через эту операцию обучают и запускают нейросети. Однако, поскольку это игровые GPU, Nvidia специально программно ограничила скорость этой операции на них вдвое. Классическая сегментация рынка, хочешь делать ML – плати за ML-видеокарту, а не за игровую. 

Ограничение сделано как делитель скорости выдачи инструкций, и его значение лежит в регистрах, в которые обычно писать нельзя. То есть обойти эту штуку напрямую невозможно. Но автор этой репы нашел, как это сломать. 

Автор взял технику, которую раньше придумали для разблокировки аналогичных ограничений майнинговых карт CMP 170HX, и оформил ее как модуль ядра Linux. Он срабатывает при загрузке, до старта драйвера NVIDIA, прописывает полную скорость и только потом отдает карту стоковому драйверу. Главное, что модуль работает именно до драйвера, поэтому не нужно патчить драйвер при каждом обновлении и/или перепрошивать BIOS.

Цифры из репозитория для 3090 Ti (GEMM 8192, 450 Вт):
BF16 87,5 → 157,4 TFLOPS
FP16 87,5 → 118,4 TFLOPS
TF32 42,6 → 82,6 TFLOPS

На реальных задачах прирост немножко скромнее, но он есть. Префилл LLM ускоряется примерно на 14–36%. Результаты вычислений при этом побитово совпадают с прежними.

Оригинальный репозиторий только для Linux, но уже есть сторонние порты для Windows, [вот например](https://huggingface.co/TOTORONG/AD103_win_unlocker). 

Инструкция по установке есть в репо. Повышаем пенсионный возраст своей 3090  😎

E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-26_06-31-56.jpg

---

**Claude:**

Смотрю репо и картинку параллельно.

---

> `Bash` -- {"command": "cd /tmp 2>/dev/null; gh repo view Zagitta/gpu-unlock --json description,stargazerCount,pushedAt,licenseInfo,primaryLanguage,issues,url 2>&1 | head -40; echo ---; gh api repos/Zagitta/gpu-unlock/contents --jq '.[].name' 2>&1 | head -50", "description": "Fetch repo metadata and file list"

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-26_06-31-56.jpg"}

---

> `Bash` -- {"command": "gh issue list -R Zagitta/gpu-unlock --state all --limit 50 2>&1 | head -60; echo ---PRS; gh pr list -R Zagitta/gpu-unlock --state all --limit 30 2>&1 | head -40", "description": "List issues and PRs of the repo"}

---

> `Bash` -- {"command": "cd \"$TEMP\" 2>/dev/null || cd /tmp; gh issue list -R Zagitta/gpu-unlock --state open --limit 200 --json number,title,labels,comments,createdAt 2>&1 | python -c \"\nimport json,sys\nd=json.load(sys.stdin)\nfor i in d:\n    t=i['title']\n    if t.startswith('Compatibility report') : cont

---

> `Bash` -- {"command": "gh api repos/Zagitta/gpu-unlock/readme --jq .content | base64 -d | head -150; echo; gh api repos/Zagitta/gpu-unlock/contents/CONTRIBUTING.md --jq .name 2>&1 | head -2", "description": "Read the repo README"}

---

> `Bash` -- {"command": "cd \"$TEMP\" 2>/dev/null || cd /tmp; gh pr list -R Zagitta/gpu-unlock --state open --limit 100 --json number,title,body,author,createdAt | python -c \"\nimport json,sys,re\nd=json.load(sys.stdin)\ncov={}\nfor p in d:\n    refs=set(re.findall(r'#(\\d+)',p['title']+' '+(p['body'] or '')))

---

> `Bash` -- {"command": "cd \"$TEMP\" 2>/dev/null || cd /tmp; for n in 135 137 124 45 44 43 138; do echo \"=== #$n\"; gh issue view $n -R Zagitta/gpu-unlock --json title,body,comments --jq '.title, (.body[0:1500]), ([.comments[]|\"> \"+.body[0:500]]|join(\"\\n\"))' 2>&1 | head -45; done", "description": "Read c

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; nvidia-smi --query-gpu=name,pci.device_id,driver_version --format=csv 2>&1 | head; echo ---; cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/unrunnable-repo-is-still-auditable.md\" | head -30; echo ---; grep -ril \"gpu-unloc

---

> `Bash` -- {"command": "cd \"$TEMP\" 2>/dev/null || cd /tmp; gh issue list -R Zagitta/gpu-unlock --state all --limit 300 --json number,title,body > issues.json; python - <<'E'\nimport json,re,collections\nd=json.load(open('issues.json',encoding='utf-8'))\nres=collections.Counter(); noup=[]; probe=[]\nfor i in 

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python ~/.claude/scripts/rail_plan.py declare --self \"триаж репо через gh, сборка рекомендации\" --outsource \"code_read:codex,second_opinion:codex\" 2>&1 | tail -3; python ~/.claude/scripts/machine_stamp.py sig --model \"Sonnet 5.5\" 2>&1 | tail -1

---

**Claude:**

Разобрал репо и его очередь через `gh`; код ядра пока не читал. Ниже вывод и рекомендация, ничего не менял и никуда не писал.

## Что за репо
`Zagitta/gpu-unlock` — 7,6 тыс. звёзд, ~125 issue, 28 открытых PR, обновляется каждый час. Мейнтейнер закрывает дубли в день подачи: #161, #90 и #41 закрыты как повторы чужих PR. Главный риск здесь не качество, а то, что тебя опередят.

## Ограничение у нас
На хабе стоят GTX 1660 SUPER (Turing) и RTX 5060 Ti (Blackwell). Карты семейства GA10x нет ни одной, поэтому отчёт о совместимости или замер разблокировки сделать нельзя. Я проверил только хаб; остальные узлы флота (ноуты, Mac) не смотрел. Остаётся работа без железа: код, пакеты, документация. Тесты в репо идут на заглушках, WSL Ubuntu на хабе есть, `gcc` и `make` в Windows нет.

## Кандидаты (по убыванию ценности)

| # | Что | Почему | Риск |
|---|---|---|---|
| 1 | **Issue #43**: после неудачной разблокировки при выходе из сна карта остаётся в «грязном» состоянии (память удержана, маски DMA не восстановлены), а на следующий сон модуль пробует её снова | Реальный дефект, воспроизводится на их же заглушках без железа. PR на него нет | Сложный код ядра, а проверить на карте нечем. Автор issue может подать PR сам |
| 2 | **Issue #44**: пакет для Arch не ставит конфиг `dracut`, поэтому на Arch с dracut модуль не грузится до драйвера NVIDIA | Правка маленькая, воспроизводится без железа, зеркалит уже принятый PR #26 для Debian | Три issue (#42, #43, #44) написаны одним автором, и он, скорее всего, подаст PR сам |
| 3 | **Класс «разблокировка прошла, ускорения нет»** (#111, #124, #149) | В #135 найдена вероятная причина: драйвер 595 пересбрасывает регистры, помогает `NVreg_GpuInitOnProbe=1` (+56% BF16 на ноуте). Это раздел «Troubleshooting» в README | Доказательство одно, на одном ноуте. Включать опцию по умолчанию нельзя, только описать |
| 4 | Таблица «Tested cards» в README правится руками в 6 открытых PR одновременно (#162, #140, #129, #109, #105, #89) | Корень проблемы виден: форма отчёта структурная, таблицу можно собирать скриптом | Это новая фича. По нашему правилу в чужое репо ≥1000★ непрошеные фичи не шлём, только предлагаем issue-ом |

Не берём: порт на Windows (делают сторонние), Ada/AD10x (там уже PR #24), добавление ID карт (4 PR спорят, нужно железо), Turing и Blackwell (доказательств нет).

## Рекомендация
Один PR: **#43**, через второе мнение Codex по коду до отправки. Параллельно оставить в #135 комментарий с разбором: сколько отчётов «без ускорения» совпадает с этой причиной. Пункт 4 предложить issue-ом мейнтейнеру, а не PR. Всё это работает на видимость нашей линии «чиним по существующему issue», а не «шлём фичу».

Перед стартом по канону нужны три проверки: `gh_pr_discipline.py feature-gate` (тип изменения), `/outbound-gate` (нет ли дубля, не опередили ли за ночь) и прогон тестов в WSL. Подпись в PR только именем, без ссылок: репо больше 1000 звёзд.

Какой путь берём: #43 с полной проверкой в WSL, или сначала быстрая победа на #44?

🧒 **Простыми словами:** Это популярная заплатка, которая заставляет видеокарты 30-й серии считать быстрее. У нас такой карты нет, поэтому пробовать её на железе мы не можем. Зато в коде нашлись настоящие дырки, которые никто ещё не чинит. Самая стоящая: после сна компьютера сломанная карта остаётся в плохом состоянии. Чинить такое можно без самой карты, на тестовых заглушках.

🏛H · Sonnet 5.5 · 28918

---

**User:**

Stop hook feedback:
001-пара: эта задача ушла и тебе, и Codex (session s_2947263e). Ты ещё не написал напарнику. До ответа оператору, один раз: (1) прочитай его сообщения по точной теме: python -X utf8 ~/.claude/scripts/tg_bus_read.py --workroom --all --peek --recipient Claude и оставь только строки с [voice001:chat_REDACTED:x2e99a45e002b94]; (2) отправь ОДИН конверт [Claude→Codex][voice001:chat_REDACTED:x2e99a45e002b94][VERIFY|COUNTER|PROPOSE] с session_id=s_f85329eb peer_session_id=s_2947263e, где сверяешь свой вывод с его (цитируй его msg_id) или даёшь свой план; python -X utf8 ~/.claude/scripts/tg_bus_send.py --workroom --raw "<конверт>"; (3) впиши в ответ оператору строку «напарник: согласен / расходимся в … / молчит (NO_QUORUM)». Это блок один раз, второй Stop пройдёт.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python -X utf8 ~/.claude/scripts/tg_bus_read.py --workroom --all --peek --recipient Claude 2>&1 | grep -F \"x2e99a45e002b94\" | tail -10", "description": "Read partner messages on this topic"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python -X utf8 ~/.claude/scripts/tg_bus_read.py --workroom --all --peek --recipient Claude 2>&1 | grep -F -A40 \"voice001:chat_REDACTED:x2e99a45e002b94\" | head -120", "description": "Read Codex's full messages on this topic"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python -X utf8 ~/.claude/scripts/tg_bus_read.py --workroom --all --peek 2>&1 | grep -F -B2 -A30 \"x2e99a45e002b94\" | head -100", "description": "Re-read workroom without recipient filter"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python -X utf8 ~/.claude/scripts/tg_bus_send.py --workroom --raw \"[Claude→Codex][voice001:chat_REDACTED:x2e99a45e002b94][PROPOSE round 2/3] session_id=s_f85329eb peer_session_id=s_2947263e. Твои тела

---

**Claude:**

Конверт ушёл напарнику (msg_id 1991384).

напарник: молчит (NO_QUORUM). Его два письма (PROPOSE r1, VERIFY r2) я вижу в ленте, но тела не открылись ни с фильтром, ни без. Сверить свой вывод с его я не смог, msg_id его писем не цитирую.

Мой вывод прежний: один PR на issue #43, запасной вариант #44, по #135 только комментарий. Перед отправкой нужны `feature-gate`, `/outbound-gate` и прогон тестов в WSL.

🧒 **Простыми словами:** Я написал напарнику-Codex, что выбрал. Его ответ в чате вижу, но прочитать не смог, поэтому «согласен» сказать не могу. Решение прежнее: чиним баг с «сном» (#43), остальное потом.

🏛H · Sonnet 5.5 · 28918

---

**User:**

<task-notification>
<summary>Stop hook feedback</summary>
</task-notification>

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; python -X utf8 ~/.claude/scripts/tg_bus_read.py --workroom --all --peek --recipient Claude 2>&1 | grep -F -A40 \"x2e99a45e002b94\" | head -150", "description": "Read Codex's replies on this topic"}

---

**Claude:**

Codex закрыл обмен как NO_QUORUM (письмо [1991383]): он не успел увидеть мой конверт в своё 120-секундное окно. Дальше по шине писать не нужно.

**напарник: расходимся в выборе.** Его письма [1991374] и [1991383] теперь прочитались.

| | Codex | Я |
|---|---|---|
| Главное | Общий раннер замеров с офлайн-сравнением: один и тот же GPU, явный FP32-аккумулятор, контроли, питание и частоты, отказ от несовместимых базовых замеров | Исправление issue #43, запасной вариант #44 |
| Второе | Многокарточность в уже открытый PR #116 (диагностика SM) | Комментарий в #135 |

**Где сходимся:** без правок кода, без установки на GPU и без публичных постов до твоего решения. Независимой проверки друг друга нет, консенсус не заявляю.

**Мой довод против его главного пункта:** раннер замеров это новая фича, а по нашему канону непрошеную фичу в репо больше 1000 звёзд не шлём, только по issue мейнтейнера. Пользу идеи он показал верно: #107 и #137 действительно требуют замера энергии и устойчивости. Поэтому вариант Codex я бы сначала предложил мейнтейнеру issue-ом и PR не открывал. Остальное в моей рекомендации выше без изменений.

Решение за тобой:
1. #43, исправление с тестами в WSL.
2. Issue-предложение про раннер замеров.
3. Оба: PR на #43 и отдельный issue.

🧒 **Простыми словами:** Мы с Codex выбрали разное. Он предлагает линейку, чтобы мерить скорость карт одинаково, а я предлагаю чинить баг со сном. Чужой проект не любит непрошеные новинки, поэтому мой вариант безопаснее, а его идею лучше сначала предложить хозяевам.

🏛H · Sonnet 5.5 · 28918
