---
session: s_29fb3757
date: 2026-10-12
words: 4276
turns: 4
tools: "Bash, Edit, Grep, PowerShell, Read, Skill, ToolSearch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-12 · Scheduled run: auto-hub-261005-prior-art-verdict-family-vs-words

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_29fb3757` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261005-prior-art-verdict-family-vs-words" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261005-prior-art-verdict-family-vs-words\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

ПЕРВЫМ ДЕЛОМ переименуй эту сессию: вызови mcp__ccd_session_mgmt__set_session_title с session_id "self" и title "⚙️ Починка: whisper садится на слабую GPU". Затем:

/five-whys whisper-on-weak-gpu

Machine: HUB-01 (Хаб) · Agent: Claude · Operator: dev · 2026-10-12. Рождена из ретро сессии H15325 (факт-чек видео + подкаст).

Outcome: класс «ML-задача на хабе садится на слабую GTX 1660 вместо RTX 5060 Ti» закрыт ДВЕРЬЮ, а не памятью.

Контекст (датированная серия, семья заведена в ~/.claude/scripts/prior_art.py FAMILIES['whisper-on-weak-gpu'], бэкап prior_art.py.bak-whisper-gpu-family-20261012):
- 08.10 whisper-lands-on-weak-gpu-by-default: whisper_best сел на GTX 1660 (GPU0, занята, FP16 без тензорных ядер).
- 09.10 cuda-visible-devices-without-pci-order: NODE-0X на хабе, CUDA_VISIBLE_DEVICES=1 без CUDA_DEVICE_ORDER=PCI_BUS_ID выбрал GTX 1660.
- 12.10 (H15325): самописный scratchpad fw_transcribe.py с CUDA_VISIBLE_DEVICES=1 без PCI_BUS_ID сел на 1660 (100% загрузки), 5060 Ti простаивала. Корень доказан: в D:/Vault/_imports/whisper_best.py уже есть _pin_best_gpu (строка ~84), а сессия написала двойника, не сделав RECALL.
Факт: в порядке CUDA (FASTEST_FIRST по умолчанию) и в порядке nvidia-smi (PCI_BUS_ID) индексы GPU на хабе не совпадают.

Scope: пять почему по трём случаям, затем одна дешёвая дверь (АК-47). Кандидаты: (а) whisper_best.py как единственный вход, экспортирующий pin_best_gpu() для любых ML-скриптов; (б) хук PreToolUse на Bash, который при `CUDA_VISIBLE_DEVICES=` без `CUDA_DEVICE_ORDER=PCI_BUS_ID` печатает предупреждение и указатель на whisper_best; (в) переменная CUDA_DEVICE_ORDER=PCI_BUS_ID в профиле пользователя хаба. Выбери простейшее, докажи красной пробой (дверь краснеет на сломанной команде и молчит на правильной).

Попутно второй дефект для той же сессии (одна строка в журнал, без стройки): гейт spawn_slot_guard 12.10 сначала отбил create с именем «repair-…» требованием «создай со своим именем, слот НЕ бери», а после переименования отбил тот же create требованием «возьми прогретый слот». Две ветки одного хука противоречат друг другу; запиши selfheal.py journal --class spawn-slot-guard-contradicts-itself.

Deliverable: дверь + тест, строка selfheal.py journal --amend с доказанной причиной, раскатка по §0.13 на узлы с двумя GPU (если такие есть по fleet_nodes.json).
DoD: красный тест показан, дверь стоит, потребитель назван (какие скрипты и скиллы зовут whisper), доклад в чат сессии с до и после.
Ограничения: ничего не удалять; правку общего файла начинать с бэкапа; Tier-2 нет.
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `Skill` -- {"skill": "five-whys", "args": "whisper-on-weak-gpu"}

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

⚠️ ДВЕРЬ ЖУРНАЛА ТОЖЕ ОБРЕЗАЛА СЧЁТ (починено 06.10.2026). Правило выше «число -- по двери
`selfheal.py journal`» стояло на том, что дверь считает всю семью. На семье
`vneshnyaya-zapis-o-registracii-protuhla` она печатала «ещё 6 прежних (итого 7)» при
СЕМНАДЦАТИ строках, потому что брала ДЛИНУ списка `split_class_hits` с потолком
`top=6`. Теперь дверь зовёт его с `top=None`, и оба прибора сходятся. Если всё же
расходятся -- бери БОЛЬШЕЕ и сверь его со строкой «СЕМЬЯ <slug>: случаев в
журнале N»: заниженный счёт хоронит системный класс молча, а на границе порога
потолок умеет его и подделать.

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


ARGUMENTS: whisper-on-weak-gpu

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ H45073 Починка: whisper садится на слабую GPU"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"ML-задача на хабе садится на слабую GTX 1660 вместо RTX 5060 Ti, whisper CUDA_VISIBLE_DEVICES без PCI_BUS_ID\" 2>&1 | head -40; echo ---; nvidia-smi -L; echo ---; nvidia-smi --query-gpu=index,pci.bus_id,name --format=csv; echo; echo \"

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && sed -n 70,125p whisper_best.py; echo ---CONSUMERS; grep -rln \"whisper_best\" ~/.claude/scripts ~/.claude/skills ~/.claude/hooks /e/Obsidian/_imports 2>/dev/null | head -30; echo ---CF; python - <<'E'\nimport os,subprocess\ncode=\"import torch;print([(i,torch.

---

> `Read` -- {"file_path": "D:\\Vault\\_imports\\whisper_best.py", "offset": 60, "limit": 70}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_29fb3757\\tasks\\bndxi195i.output"}

---

> `Bash` -- {"command": "cd ~/.claude; ls hooks | head -60; echo ---; grep -n \"PreToolUse\" -A30 settings.json | head -70", "description": "List hooks and PreToolUse registration"}

---

> `Grep` -- {"pattern": "CUDA_VISIBLE_DEVICES", "path": "C:\\Users\\dev\\.claude\\scripts", "output_mode": "content", "glob": "*.py", "head_limit": 40}

---

> `Bash` -- {"command": "cd ~/.claude/hooks; cat av_spawn_guard.cmd; echo ----; sed -n 1,80p av_spawn_guard.py; echo ----; ls _test_av_spawn_guard.py && sed -n 1,40p _test_av_spawn_guard.py", "description": "Read model hook and its test"}

---

> `PowerShell` -- {"command": "foreach($s in 'User','Machine'){ \"$s CVD=\" + [Environment]::GetEnvironmentVariable('CUDA_VISIBLE_DEVICES',$s) + \" CDO=\" + [Environment]::GetEnvironmentVariable('CUDA_DEVICE_ORDER',$s) }; Get-Content \"$env:USERPROFILE\\.claude\\scripts\\_shared\\asr_local.py\" | Select-Object -Skip 

---

> `Grep` -- {"pattern": "CUDA_VISIBLE_DEVICES|CUDA_DEVICE_ORDER", "path": "D:\\Vault\\_imports", "output_mode": "content", "glob": "*.{py,ps1,cmd,bat}", "head_limit": 50}

---

> `Bash` -- {"command": "cd ~/.claude/hooks; sed -n 80,400p av_spawn_guard.py | grep -n \"def main\" -A40 | head -70; grep -n '\"Write\\|Edit|' ~/.claude/settings.json | head; ls ~/.claude/hooks | grep -i \"mcp_lazy_gate\\|_test_mcp\" ", "description": "See hook main() payload handling and Write matchers"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\cuda_order_guard.py", "content": "\"\"\"\nPreToolUse hook (Bash|PowerShell|Write|Edit|MultiEdit): ДВЕРЬ семьи whisper-on-weak-gpu.\n\nПАСПОРТ\n  Что делает: блокирует (exit 2) команду или файл, которые ЗАДАЮТ индекс GPU через\n    переменную CUDA_VISI

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\cuda_order_guard.cmd", "content": "@echo off\nREM PreToolUse hook: GPU index without CUDA_DEVICE_ORDER=PCI_BUS_ID -> block (family whisper-on-weak-gpu).\nREM Machine-portable: %USERPROFILE% resolves per machine. Python reports to stderr, exit 2 = bloc

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\_test_cuda_order_guard.py", "content": "\"\"\"Тест cuda_order_guard: обязан краснеть на трёх реальных случаях серии whisper-on-weak-gpu\nи молчать на правильных формах. Строки собраны через N, чтобы сам тест не пугал хук.\nRun: python ~/.claude/hooks/

---

> `Bash` -- {"command": "cd ~/.claude/hooks && python _test_cuda_order_guard.py; echo exit=$?", "description": "Run the guard test"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\hooks\\cuda_order_guard.py", "old_string": "_ASSIGN = re.compile(\n    r\"\"\"(?:[\"']?\"\"\" + _NAME + r\"\"\"[\"']?\\s*(?:\\]\\s*)?(?:=|,)\\s*)(?P<v>[^\\s;&|)\\n]*)\"\"\")", "new_string": "_ASSIGN = re.compile(\n    r\"\"\"(?:[\"']?\"

---

> `Bash` -- {"command": "cd ~/.claude/hooks && python _test_cuda_order_guard.py | grep -v ^PASS; echo exit=$?; echo; echo \"=== RED PROOF: ломаю защиту (убираю проверку PCI_BUS_ID) на копии ===\"; sed 's/return not (_ORDER.search(text) or _ORDER.search(context or \"\"))/return True/' cuda_order_guard.py > /tmp/

---

> `Bash` -- {"command": "cd ~/.claude/hooks && set -o pipefail; python _test_cuda_order_guard.py > /tmp/t_ok.txt; echo real_exit=$?; grep -v ^PASS /tmp/t_ok.txt; mkdir -p /tmp/cog_broken; sed 's/return not (_ORDER.search(text) or _ORDER.search(context or \"\"))/return True/' cuda_order_guard.py > /tmp/cog_broke

---

> `Bash` -- {"command": "cd ~/.claude/hooks && set -o pipefail; sed 's/        return True\\n    return False//; s/^def _assigns_index(text: str) -> bool:/def _assigns_index(text: str) -> bool:\\n    return False/' cuda_order_guard.py > /tmp/cog_broken/cuda_order_guard.py; (cd /tmp/cog_broken; python _test_cuda

---

> `Bash` -- {"command": "cd ~/.claude && cat > /tmp/reg.py <<'E'\nimport json\np=r\"C:\\Users\\dev\\.claude\\settings.json\"\ns=json.load(open(p,encoding=\"utf-8\"))\npre=s[\"hooks\"][\"PreToolUse\"]\nassert not any(\"cuda_order_guard\" in json.dumps(x) for x in pre)\ncmd=\"\\\"C:\\\\Users\\\\dev\\\\.claude

---

**Claude:**

Регистрирую хук в settings.json (бэкап уже снят). Патч пишу файлом, как требует гард.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_29fb3757\\scratchpad\\reg_cuda_guard.py", "content": "import json, os\np = os.path.expanduser(r\"~\\.claude\\settings.json\")\ns = json.load(open(p, encoding=\"utf-8\"))\npre = s[

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_29fb3757/scratchpad/reg_cuda_guard.py\"; ls ~/.claude/settings.json.bak-cuda-order-guard-20261012", "description": "Run registration script"}

---

> `Bash` -- {"command": "CUDA_VISIBLE_DEVICES=1 python -c \"print('live probe')\"", "description": "Live probe: hook must block this"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_29fb3757/tasks/bndxi195i.output\" | sed -n '/CONSUMERS/,$p' | head -50; cd ~/.claude/scripts; grep -n \"whisper-on-weak-gpu\" prior_art.py | head; grep -n \"FAMILY_DOORS\" prior_art.p

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_29fb3757\\scratchpad\\cf_cuda_order.py", "content": "\"\"\"Контрфакт семьи whisper-on-weak-gpu: какую карту видит cuda:0 при разных env.\nУсловие: CUDA_VISIBLE_DEVICES=1 с порядко

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_29fb3757/scratchpad\" && timeout 110 python cf_cuda_order.py", "description": "Run GPU order counterfactual", "timeout": 115000}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_29fb3757/scratchpad\"; for v in .venv-diar .venv-sep; do P=\"/e/Obsidian/_imports/$v/Scripts/python.exe\"; echo \"== $v\"; timeout 60 \"$P\" -c \"import torch;print(torch.__version__, 

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_29fb3757/scratchpad\"; sed -i 's#\\[sys.executable, \"-c\", CODE\\]#[r\"D:\\\\Vault\\\\_imports\\\\.venv-diar\\\\Scripts\\\\python.exe\", \"-c\", CODE]#' cf_cuda_order.py; timeout 1

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_29fb3757\\scratchpad\\cf_cuda_order.py", "old_string": "[r\"E:Obsidian_imports.venv-diarScriptspython.exe\", \"-c\", CODE]", "new_string": "[\"D:/Vault/_i

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_29fb3757/scratchpad\"; timeout 115 python cf_cuda_order.py", "description": "Rerun counterfactual with fixed venv path", "timeout": 120000}

---

> `Grep` -- {"pattern": ".", "path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_29fb3757\\tasks\\bndxi195i.output", "output_mode": "content", "offset": 56, "head_limit": 45}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; sed -n 240,256p prior_art.py; sed -n 1255,1262p prior_art.py; python selfheal.py journal --help 2>&1 | head -30", "description": "View family keys, FAMILY_DOORS head, journal help"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; cp prior_art.py prior_art.py.bak-cuda-order-door-20261012; awk 'NR>=1255 && /^}/ {print NR; exit}' prior_art.py; sed -n 1262,1285p prior_art.py", "description": "Backup prior_art and view FAMILY_DOORS entry format"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; sed -n 1400,1408p prior_art.py", "description": "See end of FAMILY_DOORS"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\prior_art.py", "old_string": "        \"и дала рост 58 -> 156.\",\n}", "new_string": "        \"и дала рост 58 -> 156.\",\n    # Зарегистрирована 12.10.2026 (/five-whys, хаб, H45073). КОРЕНЬ (✅ контрфакт в venv-diar,\n    # cud

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\prior_art.py", "old_string": "        'сел на GTX 1660', 'выбрал GTX 1660', 'RTX 5060 Ti простаива',\n    ],", "new_string": "        'сел на GTX 1660', 'выбрал GTX 1660', 'RTX 5060 Ti простаива',\n        'без PCI_BUS_ID', 'на

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python prior_art.py class \"ML-задача на хабе села на слабую GPU без PCI_BUS_ID вместо RTX 5060 Ti\" > /tmp/pa.txt; echo exit=$?; grep -n \"СЕМЕЙНЫХ\\|СЕМЬЯ\\|ДВЕРЬ\\|cuda_order\" /tmp/pa.txt | head; python selfheal.py journal --help 2>&1 | head -5; python selfheal

---

> `Bash` -- {"command": "cd ~/.claude/scripts; grep -n \"amend\" selfheal.py | head -15", "description": "Find amend syntax in selfheal"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python selfheal.py journal --amend --class whisper-on-weak-gpu --target root-proven-door-built --what \"[ПОПРАВКА] 12.10 H45073 /five-whys: причина ДОКАЗАНА контрфактом (venv-diar, cuda:0 при индексе 1: без CUDA_DEVICE_ORDER = GTX 1660 SUPER, с PCI_BUS_ID = RTX 506

---

> `Bash` -- {"command": "cd ~/.claude/scripts; grep -c \"spawn-guards-contradict-on-slot-reuse\" ~/.claude/../../../Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md 2>/dev/null || grep -rc \"spawn-guards-contradict-on-slot-reuse\" /e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md; grep -n \"spawn-

---

> `Bash` -- {"command": "cd ~/.claude/scripts; python breakage.py count --class spawn-guards-contradict-on-slot-reuse; python breakage.py count --class spawn-slot-guard-contradicts-itself", "description": "Count sibling spawn-guard classes"}

---

> `Grep` -- {"pattern": "whisper_best", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches", "glob": "{scripts,skills,hooks}/**/*.{py,md,ps1,cmd}", "head_limit": 25}

---

**Claude:**

Корень найден и доказан, дверь построена и стоит на хабе, но на остальные узлы я её не раскатывал.

## ⚙️ Починка семьи `whisper-on-weak-gpu` (12.10, сессия H45073)

**GATE.** В журнале три датированных случая одной семьи: 08.10, 09.10 и 12.10. Счёт взят из строки `prior_art.py`: «СЕМЬЯ whisper-on-weak-gpu: случаев в журнале 3».

**Почему так, пять звеньев:**

| № | Звено | Статус |
|---|---|---|
| 1 | ML-задача села на GTX 1660 SUPER, а RTX 5060 Ti простаивала | ✅ nvidia-smi, 100% загрузки на 1660 |
| 2 | Скрипт задал `CUDA_VISIBLE_DEVICES=1` по индексам nvidia-smi | ✅ три случая |
| 3 | CUDA по умолчанию нумерует карты FASTEST_FIRST, а nvidia-smi по PCI-шине, поэтому индекс 1 означает разные карты | ✅ контрфакт ниже |
| 4 | Ничто не проверяло запись индекса: `_pin_best_gpu` в `whisper_best.py` есть, но звать его никого не заставляло | ✅ |
| 5 | Каждая новая сессия писала пин заново, а RECALL не находил готовый | ✅ 12.10 написан двойник `fw_transcribe.py` |

**Контрфакт.** Я запустил один и тот же код в `.venv-diar` (torch 2.11, видит обе карты) и смотрел, что такое `cuda:0`:

| Условие | Карта |
|---|---|
| индекс 1, без `CUDA_DEVICE_ORDER` | GTX 1660 SUPER |
| индекс 1, с `PCI_BUS_ID` | RTX 5060 Ti |
| индекс 0, без порядка | RTX 5060 Ti |
| индекс 0, с `PCI_BUS_ID` | GTX 1660 SUPER |

Системный Python CUDA-torch не имеет, поэтому первая попытка дала «none» на всех четырёх.

**Дверь.** Выбран вариант (б), хук `cuda_order_guard.py`. Он срабатывает на `Bash`, `PowerShell`, `Write`, `Edit` и `MultiEdit` и блокирует (exit 2) запись индекса GPU без `PCI_BUS_ID`. Вариант (а) не закрыл бы самописный скрипт, а (в) не поймал бы случай в момент написания. Хук зарегистрирован в `settings.json`, бэкап: `settings.json.bak-cuda-order-guard-20261012`. Бэкап `prior_art.py` тоже снят.

**Доказательства:**
- `_test_cuda_order_guard.py` даёт «всё зелёное» (exit 0).
- Мутант «порядок не проверяется» даёт 4 FAIL.
- Мутант «индекс не ищется» даёт 8 FAIL.
- Живая проба: команда `CUDA_VISIBLE_DEVICES=1 python …` в этой же сессии была заблокирована хуком.
- Семья заведена: `prior_art.py class` печатает счёт 3 и «ДВЕРЬ СЕМЬИ».
- В ключи семьи добавил парные формулировки, без чисел.

**Потребители `whisper_best`:** `asr_local.py`, `voice001_watch.py`, `voice001_transcribe_chat.py`, `wake_listener.py`, `asr_bench.py`, `tg_translate_3chats.py`, `tg_voice_translate.py`, скиллы `voice-sessions` и `voice001-peer`.

**Журнал:**
- Поправка по `whisper-on-weak-gpu` с доказанной причиной записана с флагом `--amend`.
- `spawn-slot-guard-contradicts-itself` записан отдельной строкой. Рядом есть класс `spawn-guards-contradict-on-slot-reuse` тоже с одной строкой, так что на третьем случае их стоит объединить и заводить ремонт.

**Не сделано, по §0.13:**
- Раскатки на флот нет. По `fleet_nodes.json` две карты заявлены только у хаба, а число GPU у остальных узлов я не проверял.
- Хук лежит в `~/.claude/hooks`, и пока не понятно, едет ли он на другие узлы сам.
- `deploy_register.py` я не запускал.
- Чужими глазами (панель) дверь не проверяли. Критичной она не считается, но по §4.3-бис это ещё не закрыто.
- Скрипты, уже содержащие индекс без `PCI_BUS_ID`, не искал. Хук ловит только новые записи.

**Первый обход в scratchpad.** Проверка в `scratchpad/cf_cuda_order.py` изначально шла через системный Python и показала «none». Ничего не удалялось.

🧒 **Простыми словами:** В компьютере две видеокарты, и два списка нумеруют их в разном порядке. Скрипты брали номер из одного списка, а работали по другому, поэтому садились на слабую карту. Я поставил сторожа: он не даёт записать номер карты, пока не указан и порядок нумерации. Проверил, что сторож краснеет на плохом и молчит на хорошем. Одно осталось: убедиться, что такой же сторож нужен остальным компьютерам.
