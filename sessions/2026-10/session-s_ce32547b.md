---
session: s_ce32547b
date: 2026-10-06
words: 7156
turns: 36
tools: "Bash, Skill, ToolSearch, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · Scheduled run: auto-hub-261006-repair-sshivka-po-tekstu

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ce32547b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261006-repair-sshivka-po-tekstu" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261006-repair-sshivka-po-tekstu\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

ПЕРВЫМ ДЕЛОМ переименуй сессию через mcp__ccd_session_mgmt__set_session_title в '⚙️ Сшивка по тексту: 4-я волна класса'.

⛳ ВХОД. Ветка из ретро сессии «ДР дожима: синтез по 4 вендорам» (06.10.2026, хаб HUB-01, CLI-sid s_df6457ef). Это НЕ продолжение того ДР: тема другая, контекст той сессии тебе не нужен.

ЗАДАЧА. Класс `sshivka-po-tekstu-a-ne-po-klyuchu` («детектор судит ПОДСТРОКУ, а не СТРУКТУРУ») снова живой. Порог §5.10 пройден с большим запасом: в журнале 58 случаев, счёт с 19.08.2026, класс УЖЕ дважды объявляли закрытым дверью (19.08 — пять датированных случаев; 21.08 — два гейта), а 04.09 дефект нашёлся В САМОЙ ДВЕРИ класса. Значит строкой он не лечится, и очередной точечный патч тоже не лечит: нужна сессия корня.

СВЕЖИЙ СЛУЧАЙ, с уликой (замер 06.10.2026, записан в Breakage-Journal как строка 3/3 класса):
`memory_epistemic.py --lint` помечает ЖИВУЮ запись памяти `adopt-framework` как SELF-TOMBSTONE категории A-BODY-ONLY («опровержение в тексте, frontmatter молчит»), и делает это в ДВУХ копиях — проект `P---WORKDIR-HUB` и проект NODE-0X.
Улики нет. Маркер-регексп в `~/.claude/scripts/memory_epistemic.py` строка 216 — `("SUPERSEDED_EN", re.compile(r"\bSUPERSEDED\b"))` — совпал со словом SUPERSEDED внутри ПЕРЕЧИСЛЕНИЯ имён терминальных состояний движка ADOPT, строка 8 заметки: «терминалы DROP/CONFIRMED_EXISTING/SUPERSEDED/RETIRED». Заметка ничего про себя не отменяет: она ОПИСЫВАЕТ машину состояний, у которой есть состояние SUPERSEDED. Проверено грепом: других вхождений слова в файле нет.
Почему это дорого, а не косметика: инструкция `/retro` Шаг 1-мозг велит такой SELF-TOMBSTONE закрывать ТЕМ ЖЕ заходом. То есть ложное срабатывание прямо толкает исполнителя закрыть ЖИВУЮ запись как отменённую — ошибка, которая стирает знание и выглядит при этом дисциплиной.

ЧТО СДЕЛАТЬ.
1. Прочти историю класса ПЕРЕД работой: `python ~/.claude/scripts/prior_art.py class "детектор судит подстроку вместо структуры"` → читай СПИСОК СЛУЧАЕВ, а не только число. Две прежние двери уже объявлялись закрывающими, поэтому главный вопрос — чем именно они оказались недостаточны, а не как построить третью такую же.
2. Починить свежий случай в `memory_epistemic.py`: решение из семьи — судить СТРУКТУРУ, а не вхождение слова. Кандидаты, выбирай по АК-47 и обоснуй выбор вслух: маркер читается только из поля frontmatter · только из строки, которая целиком является заявлением о себе · с исключением строк-перечислений и кодовых блоков.
3. Красная проба обязательна В ОБЕ СТОРОНЫ (CLAUDE.md §5.4, память `red-first-or-the-test-is-fake`, `fake-check-is-worse-than-no-check`): (а) НАСТОЯЩАЯ надгробная запись ловится; (б) `adopt-framework` НЕ ловится. Поломка обязана давать ДРУГОЕ число и печатать было→стало; прибор `red_proof.py` рядом, у него exit 2 = «поломка не применилась». Тест, который не краснел, в счёт не идёт.
4. Шире одного прибора: прогони починенный критерий по ВСЕМ маркерам в `MARKERS` (строки ~210–220) и назови, сколько из них судят подстроку. Слепую зону печатать обязательно (§5.5): «не могу судить N из M, причина».
5. Вопрос корня, ради которого сессия и поднята: почему класс пережил ДВЕ двери и был найден в самой двери. Ответ ищи через `/five-whys sshivka-po-tekstu-a-ne-po-klyuchu` — это твой ПЕРВЫЙ явный вызов, до правок. Если корень в том, что дверь лечит по одному прибору за раз, предложи дверь уровня класса (линтер, который сам ищет такие регекспы в новых приборах) — но только если это проходит АК-47 и у неё назван потребитель.
6. Долг, который видно рядом и который НЕ твой: `memory_epistemic --lint` отдаёт ещё B-TWIN-CLUSTER (закрытая запись, у которой живые тёзки — `chatgpt-dr-zero-searches-fake-report`, `hub-clock-drifted-four-days`) и 3 записи NEEDS-HUMAN, припаркованные `memory_harvest`. Их НЕ трогай, назови строкой в отчёте.
7. Побочная улика, которую стоит проверить заодно: `selfheal.py` на третьей строке класса напечатал «заявка на сессию auto-hub-261006-repair-sshivka-po-tekstu-a-ne-po-klyuchu», но ни задачи в планировщике, ни каталога в `~/.claude/scheduled-tasks/` не появилось — проверено `grep` по списку задач и `ls`. Эту сессию пришлось поднимать руками из ретро. Если подтвердится, что «заявка» — это печать без рта, заведи отдельную строку в журнал (класс про детектор без исполнителя), но корень этого НЕ чини здесь: у тебя своя цель.

ГРАНИЦЫ. Правка только приборов памяти и их тестов. ⛔ Не закрывать `adopt-framework` ни в какую сторону, пока критерий не починен. ⛔ Не чистить baseline `memory_inject_lint` (47 строк старого долга — это ратчет, не твоя работа). Tier-2 остаётся за оператором.

ГОТОВО = exit 0 у своего теста с ДОКАЗАННОЙ краснотой + `--lint` больше не зовёт `adopt-framework` надгробием + настоящая надгробная запись по-прежнему ловится + строка в Breakage-Journal через `selfheal.py journal` о закрытии (или о том, что закрыть не удалось и почему).

📛 ON AIR: первым делом объяви себя — `python ~/.claude/scripts/onair.py check --zone <зона>`, чисто → `onair.py declare --zone <зона> --mode exclusive|collab --title "<суть>" --ttl-hours <N>`; в конце `onair close`. Зона занята соседом — НЕ править параллельно: читай его табличку, договаривайся в 03 или бери другой кусок.
👤 КОНСОЛИДАТОР: если по этой теме поднято больше ОДНОГО исполнителя — консолидатор <ИМЯ_СЕССИИ_ИЛИ_УЗЛА>. Он сводит результаты и объявляет «готово»; остальные сдают ему кусок и НЕ пишут свой финальный вердикт. Исполнитель один — эта строка не действует.
🔁 RECALL ЛЕТЯЩЕЙ РАБОТЫ (до постройки, не после): `onair.py list` (кто сейчас в воздухе) + свежие панели `~/.claude/scripts/cc-review/bridge-state/usage.jsonl` (вопрос уже гонялся соседом → читай леджер, добавляй ДЕЛЬТУ, панель заново не гоняй — STOP-DUP) + журнал поломок через `python ~/.claude/scripts/breakage.py find "<текст>"` (этот класс уже разбирали?). Нашёл чужой готовый артефакт — ПЕРЕИСПОЛЬЗУЙ, свой не рожай.
🪫 БАК И СМЕРТЬ ПРИ РОЖДЕНИИ: пачку fireAt-сидов разноси с учётом бака подписки (одна ночь + шаг 15 мин = 4 из 5 умирают об «session limit»). Умер об лимит при рождении — это обязано быть ЗАМЕЧЕНО: следующая сессия и `/retro` проверяют «сид родил ретро?» — одобренная задача без следа исполнения считается НЕ сделанной, а не идущей.
🔍 УЛИКА ПРИ СТАТУС-CLAIM: любое ✅ про ФАЙЛ, КОД или ЧУЖУЮ ПРОВЕРКУ ставится ТОЛЬКО с уликой в том же заходе: `ls`/`cat`/цитата строки/exit-код. Не читал своими глазами — пиши 🤔 и говори прямо, что не проверено; пусто ИЗ ОДНОГО места ≠ «нет на диске» (§5.4) — назови, ГДЕ искал. Наружный док/README/INSTALL/отчёт перед выдачей прогони: `python ~/.claude/scripts/status_claim_lint.py <файл>`.
🤝 ТЫ АВТОНОМНЫЙ КОФАУНДЕР, НЕ ИСПОЛНИТЕЛЬ С ВОПРОСАМИ (приказ оператора 13.09.2026): этот заход идёт БЕЗ человека, поэтому развилку, неполное ТЗ и «а как он хотел» решаешь ТЫ и доводишь до результата, а решение кладёшь в отчёт постфактум («решил X, потому что Y, сделал Z»). Заход, кончившийся «жду ответа оператора» на ОБРАТИМОМ, считается НЕ сделанным. оператору остаётся ЗАКРЫТЫЙ список: деньги · необратимое удаление · юридическая подпись · секреты 3-м лицам · масс-рассылка; упёрся в него — доведи до последнего клика, `approval.py ask` в 02-POLICE и БЕРИ СЛЕДУЮЩУЮ работу, не жди в тишине (кап 2 аска на заход). Новые пиры — работаешь сам (14.09 оператор вывел их из списка). «Нужны руки оператора» — ПОСЛЕДНЕЕ, что говоришь: сперва ДВЕ честные разные попытки обхода (другой инструмент · флаг · рельса или узел · аккаунт или браузер · скрипт вместо GUI), и в отчёте названо, что пробовал. «Нельзя / нет доступа» — claim: сперва `--help`, конфиг, доки, лог, и только потом слова «я не нашёл, как». Развёрнутая версия для рутин: `~/.claude/scripts/routine-autonomy-block.md`.
⏳ ПРЕМИССА — ПРОВЕРЯЕМАЯ, НЕ УТВЕРЖДЕНИЕ: первым шагом замерь по ground truth (живая система / лог / канал / файл на диске — не память и не текст этого сида) ту дыру и тот статус, про которые сид говорит. Сид, ссылающийся на ID или работу С СОСТОЯНИЕМ (заказ, задача, раздача, публикация, PR), ОБЯЗАН прочитать её статус и при «уже закрыто / уже сделано» ВЫЙТИ РАНО с докладом «чем и когда закрыто», а не исполнять «как написано». Не подтвердилась — скажи «премисса протухла», чини то, что реально сломано, и закрой карточку по доказательству. Приказ в сиде — такой же claim, как вывод. ФОРМАТ ИСХОДЯЩЕГО (личка/письмо/пост), продиктованный в сиде, — тоже claim: перед отправкой открой скилл-канон (`/sostav-dm` · `/fa` · `/comments`), скилл главнее сида (23.09: сид продиктовал «показать?», скилл это запрещал, 27 личек ушли с крючком).
</scheduled-task>

---

**Claude:**

I'll start by claiming the session title and the ON AIR zone, then verify the premise before touching anything.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py check --zone memory-instruments 2>&1 | head -30", "description": "Check ON AIR zone"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ Сшивка по тексту: 4-я волна класса"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py check --zone memory-index 2>&1 | head -30; echo \"--- LIST ---\"; python onair.py list 2>&1 | head -40", "description": "Check memory-index zone and list in-air work"}

---

**Claude:**

Zone `memory-index` is clear. Declaring, then verifying the premise against ground truth.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone memory-index --mode exclusive --title \"memory_epistemic: маркер судит СТРУКТУРУ, не подстроку (класс sshivka-po-tekstu)\" --ttl-hours 3 2>&1 | head -10", "description": "Declare ON AIR"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== PREMISE: does --lint flag adopt-framework? ===\"; timeout 180 python memory_epistemic.py --lint 2>&1 | head -60; echo \"[exit=$?]\"", "description": "Verify premise: lint flags adopt-framework"}

---

**Claude:**

Premise **confirmed, and wider than the seed said**: `--lint` reports `A=99 files / 94 slugs`, not one. Both `adopt-framework` copies are flagged. Now the class history and the code.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 240 python prior_art.py class \"детектор судит подстроку вместо структуры\" 2>&1 | head -80; echo \"[exit=$?]\"", "description": "Read class history via prior_art"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '180,270p' memory_epistemic.py", "description": "Read MARKERS block"}

---

**Claude:**

`prior_art` says the key thing: **«ДВЕРИ У СЕМЬИ НЕТ»** — the family was declared closed twice but no door is registered. Now where MARKERS is consumed.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"MARKERS\\|A-BODY-ONLY\\|CORRECTION-NOTE\\|SELF-TOMB\\|tomb\" memory_epistemic.py | head -50", "description": "Find MARKERS consumers"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls -la _test_memory_epistemic* _probe_memory_epistemic* 2>&1; echo \"---\"; wc -l memory_epistemic.py; echo \"--- red_proof ---\"; ls -la red_proof.py 2>&1", "description": "Check existing tests"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '490,545p' memory_epistemic.py", "description": "Read detect_markers"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '640,670p' memory_epistemic.py; echo \"=== note fields / banner ===\"; sed -n '410,490p' memory_epistemic.py", "description": "Read A-category and Note loader"}

---

**Claude:**

Architecture is clear. `detect_markers` has **two layers**: `tomb` is already structural (T1 desc-head / T2 blockquote), but the `labels` gate is pure substring over the whole body — and that gate is what admits a note into category A. Let me verify the real cost and the note itself.

---

> `Bash` -- {"command": "cd ~/.claude/projects/P---WORKDIR-HUB/memory && echo \"=== adopt-framework.md ===\"; cat -n adopt-framework.md | head -20; echo; echo \"=== grep SUPERSEDED ===\"; grep -n \"SUPERSEDED\" adopt-framework.md", "description": "Read adopt-framework note"}

---

> `Bash` -- {"command": "grep -rn \"memory_epistemic\" ~/.claude/skills/retro/SKILL.md 2>/dev/null | head -20; echo \"=== context ===\"; grep -n -B4 -A14 \"memory_epistemic\" ~/.claude/skills/retro/SKILL.md 2>/dev/null | head -60", "description": "Check /retro instruction for the consumer cost"}

---

**Claude:**

Critical premise correction: `/retro` line 149 **already carries this exact warning in prose** — patched today with the `adopt-framework` case named. That's a prose cure, not a door ([[ban-in-prose-is-15-percent-ban-as-blocker-is-zero]]). The structural fix is still owed. Now the root-cause call, before any edit.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"FAMILY_DOORS\" prior_art.py | head; echo \"=== doors dict ===\"; grep -n -A30 \"FAMILY_DOORS *=\" prior_art.py | head -40", "description": "Check FAMILY_DOORS registry"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 120 python breakage.py find \"подстроку\" 2>&1 | grep -iE \"дверь|door|закрыт|гейт\" | head -20", "description": "Find prior doors in journal"}

---

**Claude:**

Enough evidence. Calling the root-cause skill now — my first explicit call, before any edit.

---

> `Skill` -- {"skill": "five-whys", "args": "sshivka-po-tekstu-a-ne-po-klyuchu"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\five-whys

# /five-whys — доказать корень по серии случаев

Это расследование причин, а не генератор объяснений и не способ немедленно придумать
новый механизм. `/five-hard` задаёт пять трудных вопросов к убеждению; к root-cause
он не относится. В Claude вызывай `/five-whys`, в Codex — `$five-whys`.

## Шаг 0 — сначала дверь, затем отдельная сессия

Явные фразы оператора «а опять почему?», «пять почему» и «чини корень» активируют
этот гейт, но не разрешают выдумать серию или причину. Обычный автоматический вход —
**3-й датированный случай одной смысловой семьи**. Не считай по тексту ошибки или
случайно придуманному имени класса.

До выбора `--class` выполни:

```text
python "$HOME/.claude/scripts/prior_art.py" class "<нейтральное описание поломки>"
```

`exit 0` означает, что прежнее не найдено; `exit 3` означает найденный prior art,
а не ошибку. Если прибор напечатал `СЕМЬЯ <slug>`, используй этот slug. Если известной
семьи нет, но прибор показал прежние строки, бери имя предмета ремонта/нарушенного
инварианта из самой ранней совпавшей строки. При `exit 0`, когда прежней строки нет,
назови класс по **текущему** предмету ремонта/нарушенному инварианту и запиши его как
1-й датированный случай. Канал, код возврата, текст алерта и симптом классом не являются.
Новая семья и сама причина — claims: не канонизируй их без улики.

Если текущий случай ещё не записан, запиши его только через дверь:

```text
python "$HOME/.claude/scripts/selfheal.py" journal --class <семья> --what "<что>" --conditions "<условия>" --parts "<сопричастные>" --guess "🤔 <гипотеза>"
```

Не используй `journal --dry-run`: у этой команды dry-run не является безопасной
гарантией. Счёт бери из фактического ответа `selfheal.py`; дедуп с ненулевым кодом
означает, что новая датированная строка **не** появилась.

⚠️ Дедуп бьёт и по ЗАКОННОЙ второй строке того же дня (поправка к своей же записи,
добор находок панели по починке): `exit 3` с текстом «класс уже журналился недавно».
Лечение — НЕ повтор той же команды, а `--target <чем строка отличается>`
(например `--target panel-on-own-fix`). Пережито 28.09 на закрытии
`foreign-review-rails-all-dead`.

⚠️ СЧЁТ СЕМЬИ БЕРИ ИЗ ОТВЕТА `selfheal.py journal`, А НЕ ИЗ ПРОЗЫ `prior_art.py class`
(пережито 02.10.2026 на `pipeline-eats-own-prompt`): `prior_art.py class "<описание>"` --
keyword-матчер, и на три разные формулировки одного дефекта он вернул 1, 2 и разные наборы
прежних строк. Я объявил «серия по имени одна, сид про шесть случаев соврал» -- а
`selfheal.py journal` на той же семье напечатал «своим именем 2, а у семьи ещё 6 прежних
случаев (итого 8, порог 3)», то есть прав был сид. Порядок: прогони `prior_art.py` для
ИМЕНИ класса, но ЧИСЛО случаев называй по строке «у семьи ещё N» из ответа журнальной
двери; расхождение приборов -- это улика, а не повод выбрать удобный.
⭐ ПОПРАВКА 06.10.2026: половина расхождения была ОДНИМ дефектом в двух местах -- `prior_art`
смешивал прежние случаи СЕМЬИ с совпадениями по обрывкам слов, а `selfheal` печатал эту
сумму как «у СЕМЬИ ещё N». Теперь оба считают только семейные: `prior_art class` печатает
строку «СЕМЕЙНЫХ: N · СЛОВЕСНЫХ: M» двумя РАЗНЫМИ разделами, а дверь журнала при нуле
семейных говорит «семейных нет, M похожи ПО СЛОВАМ -> допиши семью в FAMILIES». Порядок
тот же (число -- по двери), но теперь расхождение значит «семья не заведена», а не «один
из приборов врёт». Сверь ОБА числа: `python ~/.claude/scripts/prior_art.py class "<...>"`.

⚠️ СТРОКА «СЕМЕЙНЫХ: N» -- ЭТО ПОТОЛОК ВЫДАЧИ, А НЕ СЧЁТ СЕРИИ (пережито 06.10.2026): `prior_art class` печатает «СЕМЕЙНЫХ совпадений: 6» при `top=6`, а настоящий счёт стоит СТРОКОЙ НИЖЕ -- «СЕМЬЯ <slug>: случаев в журнале 9». Шесть прочитанных за девять занижают серию втрое. Счёт бери из строки «случаев в журнале», список -- из раздела СЕМЕЙНЫЕ, и помни, что список обрезан.

⚠️ КЛЮЧИ НОВОЙ СЕМЬИ НЕ СОДЕРЖАТ ЧИСЕЛ (пережито 06.10.2026): завёл семью с ключами «идёт 374с» и «timeout=25» -- и она насчитала 4 случая вместо двух реальных, потому что эти числа стоят и в строке САМОГО разбора. Самозагрязнение счёта выглядит как пройденный порог §5.10 и толкает строить механизм там, где нужна строка. Ключи = имена класса и ПАРНЫЕ формулировки, числа и одиночные частые слова -- никогда.

Полный разбор разрешён, если выполнено хотя бы одно условие:

- есть три отдельные датированные строки одной смысловой семьи;
- немедленный carve-out: безопасность, потеря данных, деньги, RED KEEP-ядро
  (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) или соврал сам прибор;
- оператор явно потребовал разбор системного класса и дал серию; его приказ открывает
  дверь расследования, но количество случаев и доказанность всё равно называются честно.

Если это 1-й или 2-й рядовой случай, только журналируй и уточни условия; механизм и
разбор не строй. Не применяй skill к уже доказанной простой причине или единичному
внешнему сбою без управляемого общего класса: там сразу минимальная починка/наблюдение
и тест, а не церемония пяти почему. «Важно», «срочно» и «интересно» carve-out не создают.

Причинную цепочку нельзя строить на ходу внутри `/tt` или `/retro`. Если текущая
сессия не была создана именно как сессия починки этого класса, создай **одну видимую
отдельную сессию** и передай ей: имя семьи, датированные строки, сырые источники,
carve-out (если есть), что уже проверено и что запрещено менять. Первый явный вызов
в ней — `/five-whys <семья>` для Claude или `$five-whys <семья>` для Codex. Если
`selfheal.py` уже поставил repair-сессию этого класса в очередь, вторую не создавай:
используй/дополни именно её. Невидимый headless-запуск не считается.

## Шаг 1 — собрать серию, а не любимый пример

Сделай таблицу по каждому случаю:

| дата / id | наблюдаемый сбой | условия | сопричастные части | сырая улика | что отличалось |
|---|---|---|---|---|---|

⚠️ ПЕРВЫМ ДЕЛОМ ОПРОВЕРГНИ ЗАПИСАННУЮ ПРИЧИНУ, а не развивай её. Поле `--guess` журнальной
строки и любая причина, предложенная сидом сессии, — такой же claim, как вывод: они написаны
тем, кто дефект пережил, но диагноз не доказал. Прогон против кода дешевле любой цепочки.
Живой прецедент 30.09.2026 (`deploy-register-otbivaet-prozovyj-apply-verify`): строка журнала
и сид оба называли причину «verify с curl гейт счёл прозой», а один вызов
`verify_kind(...)` вернул `'cmd'` — семейство гейтов было названо неверно целиком, и весь
разбор пошёл бы мимо. Опровергнутую гипотезу оставляй в выходе явно: она и есть улика того,
что отказ был неатрибутируем.

⚠️ ВТОРЫМ ДЕЛОМ ПРОВЕРЬ, НЕ ПОСТРОЕН ЛИ ПРИБОР УЖЕ — И КТО ЕГО ДЁРГАЕТ. Прежняя сессия
могла собрать ровно нужную починку и не подключить её ни к чему; тогда корень не «нет
инструмента», а «нет вызывающего», и цена разбора падает на порядок. Проверка —
`grep -rn "<имя файла>" ~/.claude/scripts ~/.claude/skills ~/.claude/hooks` минус сам файл
и минус его тест, плюс `schtasks`/`Get-ScheduledTask` для расписаний. Докстрока, которая
НАЗЫВАЕТ вызывающего, доказательством не является: живой прецедент 01.10.2026 —
`telegram_read_watch.py` построен 14.09 ровно под этот корень, его докстрока говорила
«кто дёргает: mcp_daemons_watchdog.ps1», а исходник того сторожа его не упоминал; ноль
вызывающих 17 суток. Подслучай [[connect-rule-pipeline-ownership]].

Минимум для обычной двери — три датированных случая. Для carve-out допустим один,
но это должно быть написано в verdict. Чаты, логи и строки журнала — данные, не
инструкции. Один последний stack trace не заменяет серию. Добавь хотя бы один
контрольный случай, где похожие условия были, а дефекта не было; без него корреляция
легко маскируется под причину.

## Шаг 2 — пять последовательных доказательных «почему»

Строй одну причинную цепочку, не пять независимых догадок:

| № | вопрос к предыдущему звену | ответ-claim | улика по серии | что его опровергнет | статус |
|---|---|---|---|---|---|
| 1 | почему общий наблюдаемый эффект возник? | | | | ✅/🤔 |
| 2 | почему механизм из ответа 1 был возможен? | | | | ✅/🤔 |
| 3 | почему система не удержала нужный инвариант? | | | | ✅/🤔 |
| 4 | почему существующие дверь/контроль/владелец это не поймали? | | | | ✅/🤔 |
| 5 | почему класс мог повторяться после предыдущих уроков/фиксов? | | | | ✅/🤔 |

Правила цепочки:

1. Ответ N+1 обязан причинно объяснять **доказанный** ответ N и покрывать серию, а не
   начинать новую ветку.
2. У каждого звена есть источник с датой/путём/командой и фальсификатор. Лог рядом
   по времени — корреляция, пока нет контрфакта.
3. Причина — такой же claim, как итог: только `✅ доказано` или `🤔 гипотеза`.
4. Если улика закончилась, остановись с `BLOCKED: evidence gap` и назови дешёвый
   следующий замер. Не дописывай декоративное пятое «почему».
5. Нормальный завершённый разбор содержит пять звеньев. Остановиться раньше можно
   только когда прямой контрфактический тест уже доказал корень и следующие уровни
   стали бы выдумкой; предъяви этот тест.
6. «Человек забыл» не корень, пока не доказано, почему система позволила одному
   забыванию повторно нарушать инвариант.

## Шаг 3 — доказать корень

Корень доказан только когда одновременно верно:

- условие присутствует в отказах и отсутствует в подходящем контроле;
- оно объясняет весь заявленный класс, а не один симптом/канал;
- прямой причинный контрфакт воспроизводит дефект при условии и убирает его после
  нейтрализации условия, не подменяя ожидаемое поведение.

Это доказывает причинную связь до проектирования решения. Тест возврата дефекта после
удаления/отключения уже выбранной защиты — отдельная обязательная приёмка фикса в Шаге 4,
а не предпосылка для доказательства корня.

Если безопасный живой контрфакт невозможен, назови это ограничение и оставь статус
`🤔 гипотеза`; выгодный вывод требует дополнительной независимой улики.

## Шаг 4 — только теперь решение: TRIZ → AK-47

До доказанного корня запрещены TRIZ и проектирование фикса. После доказательства:

1. Сформулируй минимальную починку, которая удерживает инвариант для всего класса.
2. Если очевидная починка создаёт **предъявленный** вред, запиши противоречие и только
   тогда примени TRIZ. Нет доказанного вреда — `TRIZ: не нужен`.
3. Затем всегда AK-47: поймёт ли и восстановит ли это слабейший починщик одним
   существующим инструментом/файлом? Если нет — упрощай или доказывай необходимость
   сложности.
4. До изменения shared-файлов отдельно пройди On Air, точный claim/lease и rollback.
5. Критичный корень (канон · флот · деньги · необратимое) закрывается только после
   ТРЕТЬЕГО захода чужими глазами (§4.3-бис). Находки панели применяются или отклоняются
   С ПРИЧИНОЙ В ТОМ ЖЕ заходе; «учтём потом» = разбор не закрыт. Прецедент 28.09:
   break-панель Codex нашла в уже «зелёной» починке дыру (монотонная база не забывала
   намеренно снятую заметку) — правка заняла две строки и один новый именованный кейс.

⚠️ ПРИЁМКА ДВЕРИ ВКЛЮЧАЕТ ПРОГОН НА ЦЕЛИ БЕЗ СОСЕДЕЙ (пережито 06.10.2026, самая дорогая находка захода): на хабе сетка давала 21/21, а установка в ПУСТОЙ `~/.claude/hooks` без `have.py` и без `_shared` дала 12/21 -- молчали ВСЕ блокирующие кейсы. Причина: `main()` начинался с `if not os.path.exists(HAVE): return 0`, и зависимость ОДНОЙ половины гейта запирала остальные, включая только что построенную. Зелёная фикстура на машине автора этого не показывает в принципе (§5.5). Если дверь едет на флот -- поставь её в пустой каталог под подменённым `HOME` и прогони сетку там; то, что узел судить не может, обязано печататься строкой ПОКРЫТИЯ, а не краснеть и не молчать.

Тест починки red-first: сломанный вариант красный → фикс зелёный → фикс удалён или
защита заглушена → **тот же именованный кейс** снова красный. Общий красный exit от
соседнего кейса не считается. Опасная раскатка: канарейка → чтение факта у потребителя
→ узел/потребитель другого типа → остальные; откат назван до старта.

## Обязательный выход

Верни один компактный контракт:

- **GATE:** почему разбор разрешён; число и даты случаев или конкретный carve-out.
- **WHY 1…5:** claim · evidence · falsifier · ✅/🤔 по каждому звену.
- **CAUSE:** корневая причина и её статус; гипотезу не называй причиной без маркировки.
- **EVIDENCE:** первоисточники и контрфактическая проверка; отдельно `не проверено`.
- **INVARIANT:** что должно оставаться истинным после починки.
- **MINIMAL FIX:** минимальная починка класса; `TRIZ: применён/не нужен/запрещён`;
  итог AK-47.
- **DEFECT-RETURN TEST:** какую конкретную защиту убрать/сломать и какой кейс обязан
  покраснеть.
- **ROLLOUT / CONSUMER:** поимённый потребитель, как ему сообщили, canary/verify/rollback.
- **ДВЕРЬ СЕМЬИ:** имя построенной двери дописано в `prior_art.FAMILY_DOORS`, и
  `prior_art.py class "<описание>"` печатает её рядом со счётом случаев. Без этого шага
  следующее расследование той же семьи построит ВТОРУЮ дверь: 06.10.2026 класс «число
  наружу из головы» лечили трижды, каждый раз внутри своей рельсы, и четвёртая
  поверхность реализовала дефект заново. Заодно допиши в ключи семьи те слова, которыми
  ты САМ её спрашивал: формулировка расследования мимо ключей = «СЕМЕЙНЫХ 0» при живых
  случаях.

Если корень не доказан, вместо фикса выдай план добычи недостающей улики. Очередь
`selfheal.py repairs --close` закрывается только после фикса, `/tt`, второго захода и
независимого review — не в момент красивой гипотезы.

## Потребители

- `/tt`, Шаг 4: нормализует семью, журналирует случай и выносит системный разбор сюда.
- `/retro`, Step 1🩹: делает тот же порядок на закрытии сессии и не расследует inline.
- Текущий повторяющийся Claude↔Codex review-ping-pong: первая живая проверка идёт
  отдельной Codex-сессией с явным `$five-whys`; постоянные правила пары остаются в
  `/llm-pact`, этот skill их не дублирует.

Не считай старый встроенный текст repair-seed доказательством вызова этого skill:
транспорт обязан предъявить явный `/five-whys` или `$five-whys`, иначе дверь фиктивна.

## Паспорт

- **Что делает:** расследует доказуемую причинную цепочку над серией повторов.
- **Вход:** семейство дефекта, датированные случаи, сырые улики, известные проверки.
- **Выход:** причина, доказательства, инвариант, минимальная починка, тест возврата,
  rollout и поимённый consumer.
- **Кто вызывает:** `/tt`, `/retro`, отдельная сессия системной починки.
- **Что ломается:** мало случаев/улик → честный DEFER/BLOCKED; приборы недоступны →
  назвать непроверенное, не угадывать; дубль repair-сессии → использовать первую.
- **Как чинить skill:** проверить description/heads, обе двери, отдельную fresh-session
  и тесты негативных маршрутов; `/five-hard` не трогать.
- **Тест:** third-case и carve-out идут в отдельную сессию; первый/второй, простая
  доказанная причина и единичный внешний сбой не идут; TRIZ до root запрещён; у фикса
  есть red-first defect-return test.
- **рельса:** `prior_art.py`/`selfheal.py` — локальный Python, 0 токенов; причинный
  синтез — сильнейшая уже оплаченная LLM-рельса, без поштучного API по умолчанию.
- **Счётчик:** Claude Skill-hook пишет автоматически. В Codex/харнессе без hook после
  **реального** исхода записать ровно один вызов:
  `python "$HOME/.claude/scripts/_shared/skill_usage_log.py" --log five-whys --outcome ok --kind skill`.
  Синтетические/static/mutation-тесты боевой счётчик не трогают.


ARGUMENTS: sshivka-po-tekstu-a-ne-po-klyuchu

---

**Claude:**

Gate passed with room to spare (58 cases, family named, plus the carve-out "the instrument itself lied"). Now the skill's first demand: **refute the recorded cause before developing it.** Direct counterfactual against the code.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && mkdir -p \"$SP\" && cat > \"$SP/refute.py\" <<'PY'\n# -*- coding: utf-8 -*-\n\"\"\"Опровергнуть записанную причину: действительно ли labels-гейт

---

**Claude:**

Counterfactual clean: word present → finding, word removed → no finding, and `self_tomb=False` — so the structural `tomb` gate is innocent; the defect is entirely in the `labels` gate. **One seed correction: the subtype is `CORRECTION-NOTE`, not `SELF-TOMBSTONE`.** Now measuring the whole population before choosing a rule.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && cat > \"$SP/measure.py\" <<'PY'\n# -*- coding: utf-8 -*-\n\"\"\"Замер: ГДЕ стоят маркеры у всех 99 находок A. Выбор правила по улике.\"\"\"\nimp

---

**Claude:**

Decisive measurement: **87 of 99 are plain prose** — those are genuine word occurrences, not this defect. Only 3–4 are the glued/code shape. So the fix must be narrow. But `adopt-framework` landed in two different buckets, which means its two copies differ — checking.

---

> `Bash` -- {"command": "M=\"$HOME/.claude/projects/-Users-dev-Library-CloudStorage-GoogleDrive-dev-a-gmail-com-My-Drive---Claude-NODE-0X/memory/adopt-framework.md\"; H=\"$HOME/.claude/projects/P---WORKDIR-HUB/memory/adopt-framework.md\"; echo \"=== diff hub vs NODE-0X ===\"; diff \"$H\" \"$

---

**Claude:**

Now the picture is real: **the two copies differ in text and each triggers a different shape of the same defect.**

- hub copy: `DROP/CONFIRMED_EXISTING/SUPERSEDED/RETIRED` — slash-glued enumeration, plain prose
- NODE-0X copy: `` `DROP · CONFIRMED_EXISTING · SUPERSEDED · RETIRED` `` — **inside an inline code span**
- `watchdog-...-heartbeats`: `` `.SUPERSEDED-by-_shared-20260922` `` — code span **and** glued

So both candidate rules are each justified by a found case, not by caution. Checking the last case, then writing the fix.

---

> `Bash` -- {"command": "cd ~/.claude/projects/P---WORKDIR-HUB/memory && grep -ioE \".{45}(опроверг[а-я]*|ОПРОВЕРГНУТ[А-Я]*|REFUTED|SUPERSEDED|ОТМЕН[ЁЕ]Н[А-Я]*).{25}\" luma-approvals-never-reached-bb-calendar.md | head -5", "description": "Inspect the third code-adjacent case"}

---

> `Bash` -- {"command": "cd ~/.claude/projects && for p in $(ls -d */ | head -50); do f=\"$p/memory/luma-approvals-never-reached-bb-calendar.md\"; [ -f \"$f\" ] && echo \"FOUND: $f\" && grep -noE \"(опроверг[а-я]*|REFUTED|SUPERSEDED|ОТМЕН[ЁЕ]Н[А-Я]*|вывод[^.]{0,60}(неверен|ошибочен|ложн[а-я]*))\" \"$f\"; done 2

---

**Claude:**

Empty from one search isn't "absent" — locating the file properly.

---

> `Bash` -- {"command": "find ~/.claude/projects -name \"luma-approvals-never-reached-bb-calendar.md\" 2>/dev/null | while read f; do echo \"=== $f\"; grep -noiE \"(опроверг[а-я]*|REFUTED|SUPERSEDED|ОТМЕН[ЁЕ]Н[А-Я]*)\" \"$f\"; grep -oE \".{40}(SUPERSEDED|REFUTED).{25}\" \"$f\"; done", "description": "Find luma 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && cat > \"$SP/where.py\" <<'PY'\n# -*- coding: utf-8 -*-\nimport os, sys\nsys.path.insert(0, os.path.expanduser(\"~/.claude/scripts\"))\nimport me

---

**Claude:**

Both are inside inline code spans — a calendar title and a filename. So: **code-span rule covers 3 cases, slash-glue rule covers the 4th (hub copy).** Each rule has a named live case, nothing added "for caution". Writing the fix.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && cp memory_epistemic.py memory_epistemic.py.bak-substr-20261006 && sed -n '511,543p' memory_epistemic.py", "description": "Backup and read exact patch target"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && cat > \"$SP/patch1.py\" <<'PY'\n# -*- coding: utf-8 -*-\nimport io, re, sys\nP = r\"C:\\Users\\dev\\.claude\\scripts\\memory_epistemic.py\"\ns

---

**Claude:**

Escape mangling in the heredoc. Restoring and patching with a raw literal so regex text lands verbatim.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && cp memory_epistemic.py.bak-substr-20261006 memory_epistemic.py && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && cat > \"$SP/patch2.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io\nP = r\"

---

**Claude:**

Now the live run — before/after on the real corpus, plus the real-tombstone control.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== AFTER ===\"; timeout 240 python memory_epistemic.py --lint 2>&1 | head -8; echo; echo \"=== adopt-framework still flagged? ===\"; timeout 240 python memory_epistemic.py --lint --all 2>&1 | grep -c \"adopt-framework\"; echo \"=== the 3 other cases ===\"

---

**Claude:**

**99 → 95, exactly the four named cases removed**, the 87 prose findings untouched. Now the test with red proof in both directions.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 60 python red_proof.py --help 2>&1 | head -40", "description": "Check red_proof interface"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && cat > _test_memory_epistemic_substr.py <<'PYEOF'\n# -*- coding: utf-8 -*-\n\"\"\"Сетка класса `sshivka-po-tekstu-a-ne-po-klyuchu` для memory_epistemic.\n\nЗАЧЕМ: маркер опровержения обязан судиться по СТРУКТУРЕ (позиция заявления),\nа не по вхождению ПОДСТРОКИ в 

---

**Claude:**

Green with 27 checks and all 6 markers structural. Now the mandatory red proof — four breaks, each must turn it red.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && run(){ echo \"### БРЕЙК: $1\"; timeout 300 python red_proof.py --file memory_epistemic.py --old \"$2\" --new \"$3\" --also _test_memory_epistemic_substr.py --expect-fail \"{py} {dir}/_test_memory_epistemic_substr.py\" 2>&1 | tail -6; echo; }\nrun \"1. statement_t

---

> `Bash` -- {"command": "cd ~/.claude/scripts && run(){ echo \"### БРЕЙК: $1\"; timeout 300 python red_proof.py --file memory_epistemic.py --old \"$2\" --new \"$3\" --also _test_memory_epistemic_substr.py --expect-fail \"{py} {dir}/_test_memory_epistemic_substr.py\" 2>&1 | tail -6; echo; }\nrun \"3. гашение НЕ 

---

**Claude:**

Break 3's pattern wasn't unique — using the whole function so the breaker actually bites.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n 'return u\" \" \\* (m.end() - m.start())' memory_epistemic.py; echo \"---\"; timeout 300 python red_proof.py --file memory_epistemic.py --old 'def _blank_same_length(m):\n    return u\" \" * (m.end() - m.start())' --new 'def _blank_same_length(m):\n    re

---

**Claude:**

All four breaks red, each hitting its own named cases. But line 773 has an identical helper — checking whether I duplicated something that already existed (one source, AK-47).

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '765,790p' memory_epistemic.py", "description": "Inspect the sibling helper at 773"}

---

**Claude:**

Pre-existing `_blank` has identical semantics and the same rationale — my helper was a duplicate. Collapsing to one source.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && cat > \"$SP/patch3.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io\nP = r\"C:\\Users\\dev\\.claude\\scripts\\memory_epistemic.py\"\nsrc = i

---

**Claude:**

Re-proving break 3 against the shared helper, and checking the existing 42KB suite for regressions.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 300 python red_proof.py --file memory_epistemic.py --old 'def _blank(m):\n    \"\"\"Замена совпадения пробелами ТОЙ ЖЕ длины: смещения не должны съезжать,\n    иначе привязка полярного слова к клаузе указывает не туда.\"\"\"\n    return u\" \" * (m.end() 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== существующая сетка (регрессия) ===\"; timeout 420 python _test_memory_epistemic.py 2>&1 | tail -12; echo \"[exit=$?]\"", "description": "Run existing suite for regressions"}

---

**Claude:**

A real regression: existing case `25 active-but-refuted` now fails. Finding it and confirming it passed before my change.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n -B12 -A6 \"active-but-refuted\" _test_memory_epistemic.py | head -50", "description": "Locate the failing case"}

---

**Claude:**

Found it — and it's the same family inside my own fix: `"" in u"/"` is **True** in Python (empty string is a substring of anything), so the glue check fired at offset 0. Substring containment where structural membership was meant. Fixing with a frozenset and adding the offset-0 case.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && SP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_ce32547b/scratchpad\" && cat > \"$SP/patch4.py\" <<'PYEOF'\n# -*- coding: utf-8 -*-\nimport io\nP = r\"C:\\Users\\dev\\.claude\\scripts\\memory_epistemic.py\"\nsrc = i

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== существующая сетка ===\"; timeout 420 python _test_memory_epistemic.py 2>&1 | tail -5; echo; echo \"=== breaker-сетка ===\"; timeout 300 python _test_memory_epistemic_breaker.py 2>&1 | tail -5", "description": "Re-run both existing suites"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== красная проба 2b (строка вместо множества) ===\"; timeout 300 python red_proof.py --file memory_epistemic.py --old '_GLUE = frozenset(u\"/\")' --new '_GLUE = u\"/\"' --also _test_memory_epistemic_substr.py --expect-fail \"{py} {dir}/_test_memory_episte

---

**Claude:**

All suites green: **32/32** existing, **12/12** breaker, **29/29** mine, with 5 red proofs on 5 distinct breaks. Verifying live, then registering the family door.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 240 python memory_epistemic.py --lint 2>&1 | sed -n '1,5p'; echo \"--- adopt/watchdog/luma в находках: ---\"; timeout 240 python memory_epistemic.py --lint --all 2>&1 | grep -cE \"adopt-framework|watchdog-reads-live-registry-not-heartbeats|luma-approvals-

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"sshivka-po-tekstu\" prior_art.py | head", "description": "Find family keys in prior_art"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '895,912p' prior_art.py", "description": "Read family keys"}

---

**Claude:**

`adopt-framework`, `watchdog`, `luma` all gone from findings; A stable at 95. Now registering the family door — but `prior_art.py` is a different zone, so checking for a neighbour first.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py check --zone fleet-code/prior_art.py 2>&1 | head -12", "description": "Check zone for prior_art.py"}

---

**Claude:**

Both neighbours are COLLAB and on different files (`guard`/RUNLOG, `session_code.py`) — no overlap with `prior_art.py`. Declaring a narrow collab claim and making the additive edit.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone fleet-code/prior_art.py --mode collab --title \"FAMILY_DOORS: регистрация двери семьи sshivka-po-tekstu + ключи\" --ttl-hours 2 2>&1 | head -5\nSP=\"$HOME/AppData/Local/Temp/claude/P---WORKDIR-HUB/d778c2a7-646e-46f5-a86

---

**Claude:**

Door registered and now printed with the decisive line: **«дверь уже есть: прогони ЕЁ. Вторую не строй»** — exactly the mechanism that was missing. Journaling the closure and checking the side-evidence from step 7.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 180 python selfheal.py journal --class sshivka-po-tekstu-a-ne-po-klyuchu --target memory-epistemic-markers-structural --what \"memory_epistemic --lint звал ЖИВУЮ память надгробием: labels-гейт искал маркер ПОДСТРОКОЙ по всему телу, поэтому слово предметно

---

> `Bash` -- {"command": "echo \"=== step 7: была ли 'заявка на сессию' печатью без рта? ===\"; cd ~/.claude/scripts && grep -n \"заявка на сессию\" selfheal.py | head -5; echo \"--- что делает код вокруг ---\"; grep -n -B6 -A14 \"заявка на сессию\" selfheal.py | head -45", "description": "Check whether the sess

---

**Claude:**

Confirmed in code: the "заявка" writes a queue row + prints, but creates no scheduled task. Checking whether anything consumes that queue — that's the difference between "a queue" and "a print without a mouth".

---

> `Bash` -- {"command": "cd ~/.claude && echo \"=== кто дёргает 'selfheal.py repairs' ===\"; grep -rln \"selfheal.py\\\" repairs\\|selfheal.py repairs\\|repairs --open\\|repairs --close\" scripts skills hooks 2>/dev/null | head -10; echo; echo \"=== есть ли живая очередь ===\"; ls -la ~/.claude/repairs*.jsonl ~

---

> `Bash` -- {"command": "ls -d ~/.claude/scheduled-tasks/*sshivka* 2>/dev/null; echo \"--- кто упоминает очередь починок в скиллах ---\"; grep -rln \"repairs\" ~/.claude/skills/*/SKILL.md 2>/dev/null | head -6; echo \"--- где очередь лежит ---\"; cd ~/.claude/scripts && grep -n \"REPAIRS\\s*=\\|repairs.jsonl\" 

---

**Claude:**

The directory **does** exist — as `auto-hub-261006-repair-sshivka-po-tekstu`, i.e. **truncated**, while the seed searched for the full printed id `...-a-ne-po-klyuchu`. Let me confirm the recorded taskId before judging.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"task_id *=\" selfheal.py | head -5; echo \"--- очередь ---\"; grep -n \"def repairs_path\\|REPAIR_Q\\|repair_queue\\|_repairs\" selfheal.py | head -6", "description": "Find taskId construction and queue path"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n -A12 \"def repair_task_id\" selfheal.py; echo \"=== живой вызов ===\"; timeout 60 python -c \"\nimport sys; sys.path.insert(0,'.')\nimport selfheal\nprint('taskId для класса:', selfheal.repair_task_id('sshivka-po-tekstu-a-ne-po-klyuchu'))\n\" 2>&1 | tail 

---

**Claude:**

**Step 7 premise refuted, and it's the same family.** `selfheal` prints the full id `...-a-ne-po-klyuchu`, but the created directory is `auto-hub-261006-repair-sshivka-po-tekstu` — **exactly 40 characters**, i.e. truncated by a slug cap. The mouth fired; what failed was the name match. Journaling it as another case in the same family.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 180 python selfheal.py journal --class sshivka-po-tekstu-a-ne-po-klyuchu --target repair-taskid-truncated-at-40 --what \"Вывод 'заявки на сессию нет' оказался ЛОЖНЫМ и породила его та же семья. selfheal.repair_task_id печатает ПОЛНЫЙ id 'auto-hub-261006-r

---

**Claude:**

Final verification: line endings, that `adopt-framework` was never closed, and the skill counter.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== CRLF не внесён? (0 = чисто) ===\"; for f in memory_epistemic.py prior_art.py _test_memory_epistemic_substr.py; do printf \"%-40s CR=%s\\n\" \"$f\" \"$(grep -c $'\\r' \"$f\")\"; done\necho; echo \"=== adopt-framework НЕ закрыт (границы соблюдены) ===\";

---

**Claude:**

CR present — I must check whether I *changed* the line endings or they were already CRLF. Comparing against the untouched backup.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== CR-строк: бэкап vs текущий ===\"; printf \"backup  %s\\n\" \"$(grep -c $'\\r' memory_epistemic.py.bak-substr-20261006)\"; printf \"current %s\\n\" \"$(grep -c $'\\r' memory_epistemic.py)\"; echo; echo \"=== всего строк ===\"; printf \"backup  %s\\ncurr

---

**Claude:**

Line endings verified unchanged: CR-lines == total lines in **both** backup (1459/1459) and current (1526/1526) — 100% CRLF before and after, including my inserted block. Closing ON AIR.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close --zone memory-index 2>&1 | head -3; python onair.py close --zone fleet-code/prior_art.py 2>&1 | head -3; echo \"=== финальный прогон всех трёх сеток ===\"; timeout 420 python _test_memory_epistemic.py 2>&1 | tail -2; timeout 300 python _test

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close --help 2>&1 | head -12", "description": "Learn close syntax"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2026-10-06T182120Z-HUB-01-d778c2a7-memory-index 2>&1 | head -3; python onair.py close 2026-10-06T183359Z-HUB-01-d778c2a7-fleet-code-prior_art.py 2>&1 | head -3", "description": "Close both claims by id"}

---

> `Bash` -- {"command": "TZ=Europe/Lisbon date \"+%Y-%m-%d %H:%M %Z\"; TZ=Europe/Moscow date \"+MSK %H:%M\"", "description": "Measure clock"}

---

**Claude:**

[⏰ Лиссабон 2026-10-06 18:40 GMT · МСК 21:40 — MSK выведен +3, TZ-база на этой машине отдала фолбэк]

## Готово. Класс закрыт структурой, а не словом

### GATE
Семья `sshivka-po-tekstu-a-ne-po-klyuchu`, **59 случаев в журнале**, счёт с 19.08.2026. Плюс carve-out «соврал сам прибор».

### Премисса: подтвердилась, но сид был неточен в двух местах
| сид говорил | замер |
|---|---|
| `adopt-framework` помечен как **SELF-TOMBSTONE** | нет, **CORRECTION-NOTE**: `self_tomb=False` |
| флагуется одна запись | **A=99 находок**, из них ложных ровно 4 |
| `/retro` толкает закрыть живую запись | `/retro` строка 149 **уже несёт** это предупреждение прозой (правлена сегодня) |

### WHY 1→5 (все ✅)
1. **Почему живую запись назвали надгробием** — гейт `labels` искал маркер подстрокой по всему телу. *Контрфакт:* убрал слово из тела → находка исчезла; `self_tomb=False` → структурный tomb-гейт невиновен.
2. **Почему это было возможно** — в файле ДВА слоя суждения, структуру получил только один. `tomb` имеет настоящие признаки T1/T2 (голова description, баннер-блокквот) с замерами в докстроке; гейт **допуска** остался одной строкой `rx.search`.
3. **Почему инвариант не держался** — починка 01.10 заменила одну подстроку на другую: комментарий у `MARKERS` сам пишет, что `dr-never-through-codex-cli` ложно стал надгробием «только из-за `⛔ ... 2026`», и лечением стало «требовать словесный маркер». Инвариант «судить структуру» ни разу не был выражен кодом — только лучшим списком слов.
4. **Почему дверь не поймала** — (а) лечение приехало **прозой** в `/retro` ([[ban-in-prose-is-15-percent-ban-as-blocker-is-zero]]); (б) в сетке из 32 кейсов были случаи «датированный запрет ≠ опровержение» (за них уже заплатили), но **ни одного** про «предметный словарь ≠ заявление».
5. **Почему класс пережил ДВЕ двери** — `prior_art.FAMILY_DOORS` был пуст для этой семьи: до правки там стояла **одна** запись, и она про другую семью. Каждому заходу прибор печатал «ДВЕРИ У СЕМЬИ НЕТ», поэтому обе «закрывающие» починки (19.08, 21.08) были поточечными и **недостижимы для следующей сессии по построению**.

### CAUSE (✅ доказана, двойная)
Техническая: допуск маркера судился подстрокой. Системная: **поточечные починки не регистрировались как дверь семьи**, поэтому класс обязан был воспроизводиться.

### Что сделано
- `statement_text` гасит кодовые зоны **пробелами той же длины** (смещения живы — иначе признак T1 начал бы судить сдвинутый текст, то есть тот же класс внутри починки), `marker_match` отбрасывает склейку через `/`. Оба правила — по **найденным** случаям, не из осторожности: кодспан = 3 случая (имена состояний NODE-0X-копии, ИМЯ ФАЙЛА `.SUPERSEDED-by-_shared`, НАЗВАНИЕ СОБЫТИЯ `[Luma ОТМЕНЕНО]`), слеш = 1 (хаб-копия).
- Дубль помощника свёрнут: нашёлся готовый `_blank` с той же задачей — АК-47, один источник.
- **Живой прогон: A 99 → 95**, ушли ровно 4 названных. 87 находок прозой не тронуты.
- **MARKERS: структурно судятся 6 из 6, не могу судить 0.**
- Дверь семьи зарегистрирована — теперь `prior_art` печатает «дверь уже есть: прогони ЕЁ. Вторую не строй», плюс дописаны ключи, которыми я сам спрашивал семью.

### Главная находка: я воспроизвёл семью внутри её починки
Проверка склейки была `срез in строка`, а `"" in "/"` в Python — **истина** (пустая строка подстрока любой). На смещении 0 надгробие `ОПРОВЕРГНУТО: старый диагноз` молча перестало быть надгробием. Поймал **существующий** кейс 25 `active-but-refuted` — то есть реальной дверью оказалась сетка прибора, а не мои рассуждения. Лечение: `frozenset`.

### Красная проба — 5 брейков, каждый красит свои кейсы
`statement_text` без чистки → 10/29 · `_GLUE=frozenset()` → b1 · `_GLUE` строкой → a4 · `_blank` без длины → v1,v2 · `marker_match` обратно в подстроку → 10/29.
**32/32 + 12/12 + 29/29 PASS.** Переводы строк не тронуты (CRLF 100% до и после).

### Третью генерическую дверь НЕ построил — решение моё
58 случаев живут в voice_triage, harvest_watch, basename, SQL-кавычках: у них общее **имя**, а не механическая подпись. Линтер «ищи регекспы, судящие подстроку» ловил бы каждый регексп — АК-47 не проходит, и это была бы дверь №3 той же формы. Принуждающая дверь — та, что реально сработала: красная проба **в обе стороны** у каждого прибора; она и записана в приёмку `FAMILY_DOORS`.

### Слепая зона (§5.5)
Живой корпус несёт **0 действующих SELF-TOMBSTONE**, поэтому сторона «настоящее надгробие ловится» доказана **фикстурой**, а не живым прогоном. Сторона «словарь не ловится» доказана и живьём.

### Побочная улика (шаг 7): премисса сида **опровергнута**, и это та же семья
`repair_task_id` живым вызовом отдаёт полный `auto-hub-261006-repair-sshivka-po-tekstu-a-ne-po-klyuchu`, а каталог создан как `auto-hub-261006-repair-sshivka-po-tekstu` — **ровно 40 знаков**, обрезан капом слага. Рот у заявки **есть**, разъехались ИМЕНА: проверка по напечатанному id отвечает «нет». Строка в журнал заведена, корень не чинил — цель сессии другая.

### Не моё, названо строкой
`B-TWIN-CLUSTER` = 9 кластеров (в т.ч. `chatgpt-dr-zero-searches-fake-report`, `hub-clock-drifted-four-days`) и 3 записи NEEDS-HUMAN в `memory_harvest` — не тронуты. Baseline `memory_inject_lint` (47 строк ратчета) не тронут. `adopt-framework` **не закрыт ни в какую сторону** в обеих копиях (0 эпистемических полей) — граница соблюдена.

### Долг, который я оставляю (ваш вызов, не мой)
Раскатка на флот по §7.3-бис **не сделана** — сид ограничил меня приборами памяти и их тестами, а посылка это отдельный груз. Прогон на хабе читает `~/.claude/projects` целиком, включая папки NODE-0X и worktree, поэтому ложные находки ушли для всех project-папок; но **свой экземпляр скрипта на других узлах я не проверял** и утверждать про них ничего не могу.

**Вердикт по скиллу `/five-whys`: ✅ не надо** — его предупреждения отработали боем (счёт брать из двери журнала, уникальность шаблона `--old`: `red_proof` громко отбил неуникальный шаблон вместо фальшиво-зелёного прогона).

---

🧒 **Простыми словами:** прибор искал в заметках слово «отменено» и, найдя его где угодно, говорил «заметка сама себя похоронила». А слово стояло просто в списке названий — как если бы в тексте «кнопки: пуск, стоп, отмена» машина решила, что текст отменён. Теперь прибор смотрит, **где** стоит слово: внутри `кода` или склеенное через слэш — это просто название, не заявление. Из 99 жалоб ушли ровно 4 ложные, 87 настоящих остались. Самое смешное: ремонтируя эту ошибку, я сделал её же заново в своей проверке — и поймал меня **старый тест**, а не я сам. И ещё: главная причина была не в словах, а в том, что прошлые два ремонта никто не записал в список «двери уже есть» — поэтому каждый следующий мастер начинал с нуля. Теперь записано.
