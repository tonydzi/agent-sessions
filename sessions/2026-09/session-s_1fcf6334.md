---
session: s_1fcf6334
date: 2026-09-10
words: 3518
turns: 3
tools: "Bash, Skill, ToolSearch, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-10 · Scheduled run: share-fix-daily

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1fcf6334` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="share-fix-daily" file="C:\Users\dev\.claude\scheduled-tasks\share-fix-daily\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

---
name: share-fix-daily
description: 🌍 Ночной раздатчик: очередь share_fix_queue.jsonl → полный ритуал /share-fix (≤3 кандидата), отчёт в 03
---

Первым действием вызови mcp__ccd_session_mgmt__set_session_title с названием "AUTO-hub share-fix-daily 🌍 раздатчик очереди".
Прочитай и исполни блок STOP-DUP: $OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md (это единственный источник блока, тело сюда не копируется).

РОЛЬ: ночной раздатчик «починил — раздай миру» (канон: Библия reglament-pochinil-u-sebya-srazu-razday-miru + reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir, CLAUDE.md §4.7 и §9.4-бис).

ЗАДАЧА:
1. СНАЧАЛА замер, потом выборка — голый ноль запрещён: `python C:\Users\dev\.claude\scripts\share_fix_queue.py status` (печатает `pending=N invisible=M done=K всего=T`) и `python C:\Users\dev\.claude\scripts\share_fix_queue.py lint`. ЛЮБОЕ `invisible>0` = строки, которые ты физически не сможешь выбрать, потому что их писатель разошёлся с тобой в контракте — это НЕ пустая очередь, а потеря: прогони `python C:\Users\dev\.claude\scripts\share_fix_queue.py repair`, назови в отчёте, чей писатель сломан, и работай дальше. ПОЧЕМУ (замер 04.09.2026): рутина `casebook-drip-daily` писала строки без поля `status`, ты их не видел, они не попадали ни в один рапорт, и «очередь пуста» звучало честно при 2 потерянных кандидатах — ложный ноль, неотличимый от настоящего.
Затем открой $OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl и возьми до 3 строк со status:"pending" (старейшие первыми). ЧЕСТНО пусто (pending=0 И invisible=0) → одна строка в чат «очередь пуста, всего строк T» и штатное завершение, в 03 НЕ писать.
2. По каждому кандидату исполни ПОЛНЫЙ ритуал скилла /share-fix (вызови скилл share-fix и иди по его шагам): порог переносимости+чистоты → реверс-поиск gh search issues по дословным queries из строки (2-3 формулировки) → отбор 3-5 ЛУЧШИХ живых тредов (не бот-фермы, дедуп на tonydzi/Palo-Alto-AI-Research-Lab) → заточенный под каждый тред коммент (раскрытие Майкрофта первой строкой: "hi — Mycroft, dev's synthetic AI cofounder"; только доказанные цифры из поля numbers; совет без кода — законный исход) → pr_watch.py --add на каждый тред.
3. Гист/репо создавать только через /pack; если лечилка пересказывается словами — комментария достаточно, /pack не нужен.
4. После раздачи допиши в строку кандидата в очереди: status:"done", done:"<дата>", threads:[...]. Пусто по всем запросам → status:"dry", запросы названы в отчёте. Непереносимо → status:"skip" + причина.
5. Отчёт: одно сообщение в TG-чат 03 (chat_REDACTED) через bus_send.py (dual-send): "🌍 share-fix-daily: раздал N кандидатов → M тредов (ссылки) · dry K · skip L · очередь осталась X из T · невидимых было I (чей писатель)". Тот же текст — в чат сессии.

ГРАНИЦЫ: Tier-2 (юр/деньги/секреты/масс-действия) = стоп + аск через approval.py в 02. Правда в цифрах: раздаём только доказанное, гипотезы помечаем 🤔. Копипаста-веер запрещён — каждый коммент заточен. Больше 5 тредов на один класс не слать. Блок → state blocked + доклад в 03.

⭐⭐ ДОМЕН-ГЕЙТ (07.09) — ЛАЗЕРНЫЙ ФОКУС (приказ оператора 07.09.2026: «мусорные PR нам не нужны, нанимающий инженер должен за минуту понять: этот человек живёт в агентских рантаймах»).
Цели ТОЛЬКО из нашего круга: агентские фреймворки · LLM SDK · MCP · память для LLM · evals · observability для LLM.
Дверь: `python3 ~/.claude/scripts/github_targets.py --top 20` — по умолчанию отдаёт только domain=core; первыми идут ⭐ own_pain (репо, обо что споткнулись САМИ во флоте — правило первого приоритета), дальше остальной круг.
Репо не из выдачи → `--check owner/repo`: domain=off или «нет в списке» = НЕ ТРОГАТЬ, даже если issue красивая и хозяин живой. Исключение только по прямому слову оператора.
Правила и own_pain: `~/.claude/registry/github-universe/domain.json` (0 LLM; тест `_test_github_targets_domain.py`).
Метод (репро · красный тест · мутации · ревью объектом Review) не меняется — сужены только мишени.

<!-- ROUTINE-TOKEN-DISCIPLINE v1 · 08.09.2026 · приказ оператора: все рутины на всех узлах — режем шаги и мусор в контексте, не качество. Замер NODE-0X 06–08.09: 71% недельного бака = перечитывание ~180k контекста на каждом из 60–200 вызовов за прогон; после блока в 20 лейнах вес прогона −31% за первый день -->
🪙 ТОКЕН-ДИСЦИПЛИНА РУТИНЫ (стоимость прогона = контекст × число вызовов модели; качество результата НЕ режем):
1. РАЗВЕДКА ОДНИМ ВЫЗОВОМ: журнал, реестры, списки целей, `gh`/API-выборки — собери в ОДИН скрипт с `--jq`/`head`, не 10–15 команд. Потолок разведки — 5 вызовов.
2. НЕ ВЫВАЛИВАЙ: никогда `cat`/`Read` целого файла, треда или дампа в контекст — только нужные поля и строки (`--jq`, `sed -n`, `head -c 4000`). Большой объект читаешь ОДИН раз целиком в одном вызове, не по кусочкам.
3. ЦИКЛ ПРОВЕРОК = ОДИН СКРИПТ: репро/тесты/мутации — один `.py`/`.sh`, запуск один раз, итог ≤20 строк. Серия из 30–90 микро-вызовов в scratchpad ⛔ (замер s9 06.09: 95 из 132 команд).
4. ТЕКСТ ПИШЕШЬ ОДИН РАЗ через Write, правишь через Edit точечно; переписывать файл целиком ⛔.
5. ПОТОЛОК ПРОГОНА — 60 вызовов модели. На 50-м не закончил — закрывай заход честной строкой в журнал («сделано X, не успел Y, причина»), не тяни до 200.
6. МЫШЛЕНИЕ КОРОТКО: не пересказывай себе сид и правила; думай про предмет, не про регламент.
7. ГРУНТ — СУБАГЕНТУ НА SONNET, СУЖДЕНИЕ — У СЕБЯ: чтение больших диффов/логов, разведку, репро отдавай `Agent(model="sonnet")` с ТЗ «верни ≤40 строк выжимки»; сам читаешь выжимку и пишешь то, что уходит наружу под именем оператора.
8. ⛔ ОЖИДАНИЕ НЕ ЧЕРЕЗ МОДЕЛЬ (замер s7-fast 08.09: 87 из 138 команд = `sleep 1; echo idle`, каждый тик = вызов на 200k контекста, +39% веса прогона). Ждёшь сборку/тест/CI/синк — ОДИН Bash-вызов с блокирующим циклом внутри: `timeout 900 bash -c 'until <условие>; do sleep 20; done'` (Windows: `powershell -c "while(!(<условие>)){Start-Sleep 20}"`), либо run_in_background и ждёшь уведомления. Ручной цикл «sleep → посмотреть → ещё раз» ⛔. Дольше 15 минут — не жди: поставь на вахту (pr_watch / реестр) и закрой заход.
Проверка постфактум: `python3 ~/.claude/scripts/usage_audit.py` (0 LLM): вызовов на прогон ≤60, вес прогона ≤½ от базы 06–07.09.

<!-- RUNLOG-CONTRACT v1 · 09.09.2026 · приказ оператора (голосовая 09.09, хаб): каждая смена читает тетрадь предыдущих смен и оставляет свою. SKILL.md наследует ПРАВИЛА, RUNLOG наследует ИСТОРИЮ. -->
📓 ВАХТЕННЫЙ ЖУРНАЛ РУТИНЫ (память между прогонами):
ШАГ 0 — ПЕРВЫМ ДЕЛОМ, до любой работы: python C:\Users\dev\.claude\scripts\routine_runlog.py tail share-fix-daily
  Это записки последних 5 смен: что сделано, обо что споткнулись, что поменяли в этой инструкции, с чего начать. Не наступай на их грабли и не переделывай уже сделанное. Журнала нет — ты первая смена, работай по SKILL.md.
ФИНАЛ — ВСЕГДА, даже на пустом/тихом прогоне: python C:\Users\dev\.claude\scripts\routine_runlog.py add share-fix-daily "сделал: ...; споткнулся: ...; правил SKILL.md: да/нет+что; следующей смене: ..."
  3-6 строк, только сигнал (не пересказ). Починил что-то в SKILL.md — напиши об этом ЯВНО: следующая смена обязана узнать о починке из журнала, а не открыть её заново.
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python routine_runlog.py tail share-fix-daily 2>&1 | head -60; echo \"=== QUEUE STATUS ===\"; python share_fix_queue.py status 2>&1 | head -20; echo \"=== LINT ===\"; python share_fix_queue.py lint 2>&1 | head -30", "description": "Read runlog tail a

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "AUTO-hub share-fix-daily 🌍 раздатчик очереди"}

---

> `Bash` -- {"command": "sed -n '1,80p' \"$(cygpath 'D:\\Vault\\Vault-Knowledge\\08-Templates\\seed-stop-dup-block.md' 2>/dev/null || echo /e/Obsidian/Vault-Knowledge/08-Templates/seed-stop-dup-block.md)\" 2>&1 | head -60", "description": "Read STOP-DUP block"}

---

> `Bash` -- {"command": "python onair.py list 2>&1 | head -20; echo \"=== PENDING 3 ===\"; python -c \"\nimport json,io\np=r'D:\\Vault\\Vault-Knowledge\\_outreach\\share_fix_queue.jsonl'\nrows=[]\nfor i,l in enumerate(io.open(p,encoding='utf-8')):\n    l=l.strip()\n    if not l: continue\n    try: d=json.loa

---

> `Bash` -- {"command": "python github_targets.py --top 25 2>&1 | head -40", "description": "List allowed domain targets"}

---

> `Bash` -- {"command": "ls -la /c/Users/dev/.claude/registry/github-universe/ 2>&1 | head; echo \"=== check ===\"; python github_targets.py --check langchain-ai/langgraph 2>&1 | head -15; echo \"=== domain.json head ===\"; head -c 2500 /c/Users/dev/.claude/registry/github-universe/domain.json 2>&1", "descr

---

> `Bash` -- {"command": "gh auth status 2>&1 | head -5\nq(){ echo \"### $1\"; gh search issues \"$1\" --limit 12 --state open --json repository,title,url,updatedAt,commentsCount --jq '.[]|\"\\(.repository.nameWithOwner)|\\(.updatedAt[:10])|c\\(.commentsCount)|\\(.title[:80])|\\(.url)\"' 2>&1 | head -12; }\nq \"

---

> `Bash` -- {"command": "echo \"--- smoke test ---\"; gh search issues \"mcp server timeout\" --limit 5 --json repository,title,url --jq '.[]|\"\\(.repository.nameWithOwner)|\\(.title[:60])\"' 2>&1 | head -6; echo \"--- exit $? ---\"; echo \"--- fewer terms ---\"; gh search issues \"telethon updates stopped\" -

---

> `Bash` -- {"command": "q(){ echo \"### $1\"; gh search issues \"$1\" --limit 10 --state open --json repository,title,url,updatedAt,commentsCount --jq '.[]|\"\\(.repository.nameWithOwner)|\\(.updatedAt[:10])|c\\(.commentsCount)|\\(.title[:70])|\\(.url)\"' 2>&1 | head -10; }\nq \"worker silently stops processin

---

> `Bash` -- {"command": "q(){ echo \"### $*\"; gh search issues \"$1\" --limit 10 --state open --json repository,title,url,updatedAt,commentsCount --jq '.[]|\"\\(.repository.nameWithOwner)|\\(.updatedAt[:10])|c\\(.commentsCount)|\\(.title[:70])|\\(.url)\"' 2>&1 | head -10; }\nq \"mcp server dies silently\"\nq \

---

> `Bash` -- {"command": "q(){ echo \"### $1\"; gh search issues \"$1\" --limit 8 --state open --json repository,title,url,updatedAt,commentsCount --jq '.[]|\"\\(.repository.nameWithOwner)|\\(.updatedAt[:10])|c\\(.commentsCount)|\\(.title[:70])|\\(.url)\"' 2>&1 | head -8; }\nq \"orphan notes\"\nq \"backlinks mis

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/github_universe/ 2>&1 | head; echo \"=== README ===\"; head -c 1800 /c/Users/dev/.claude/scripts/github_universe/README.md 2>&1", "description": "Inspect github_universe collector"}

---

> `Bash` -- {"command": "grep -n \"add_argument\\|def \\|targets.json\\|sys.exit\" github_targets.py | head -40; echo \"--- size ---\"; wc -l github_targets.py", "description": "Inspect github_targets.py structure"}

---

> `Bash` -- {"command": "sed -n '40,110p' github_targets.py", "description": "Read domain_of implementation"}

---

> `Bash` -- {"command": "python -c \"\nimport json;d=json.load(open(r'C:\\Users\\dev\\.claude\\registry\\github-universe\\domain.json'))\nprint(len(d['own_pain']));[print(k,'::',v[:60]) for k,v in d['own_pain'].items() if k!='_doc']\nprint('REFUSE:',json.dumps(d.get('refuse') or d.get('refuse_list') or '',ens

---

> `Bash` -- {"command": "R=\"--repo anthropics/claude-code --repo anthropics/claude-agent-sdk-python --repo PrefectHQ/fastmcp --repo BerriAI/litellm --repo agno-agi/agno --repo langchain-ai/langgraph --repo google/adk-python --repo pydantic/pydantic-ai --repo evalstate/fast-agent --repo huggingface/smolagents -

---

> `Bash` -- {"command": "R=\"--repo anthropics/claude-code --repo anthropics/claude-agent-sdk-python --repo PrefectHQ/fastmcp --repo BerriAI/litellm --repo agno-agi/agno --repo langchain-ai/langgraph --repo google/adk-python --repo pydantic/pydantic-ai --repo evalstate/fast-agent --repo huggingface/smolagents -

---

> `Bash` -- {"command": "for u in BerriAI/litellm/34281 BerriAI/litellm/36896 BerriAI/litellm/40130 BerriAI/litellm/38535 anthropics/claude-code/75572 anthropics/claude-code/82416 anthropics/claude-code/88738; do o=${u%/*/*}; r=${u#*/}; n=${r#*/}; rr=${u%/*}; echo \"=== $rr#$n ===\"; gh issue view $n -R $rr --j

---

> `Skill` -- {"skill": "share-fix", "args": "candidate: telethon/OOM terminal-status class → 4 in-domain threads"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\share-fix

# /share-fix — 🌍 починил у себя → сразу раздай миру

**Канон:** Библия `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world` + CLAUDE.md §4.7. Логика оператора: в момент починки у нас в руках лучший поисковый ключ на свете — дословный симптом; никакой «робот-сканер всего GitHub» не сравнится с реверс-поиском того, кто только что дебажил. Поэтому раздача = ритуал в момент фикса, не фоновый сканер.

## Шаг 0-бис — источник кандидатов: очередь (dev 01.09)
Кроме «только что починил в руках», кандидаты приходят из очереди `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` — её наполняет `/retro` Step 4🌍 (судья), а раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 pending за прогон, полный ритуал ниже на каждого; после раздачи строка кандидата дополняется `status:done`+`threads`). Формат строки: `added·from·artifact·queries[дословные симптом-запросы]·numbers·status`.

⛔ **ТЕРМИНАЛЬНЫХ СТАТУСОВ ЧЕТЫРЕ, НЕ ОДИН** (08.09.2026, 3-й датированный случай `share-fix-selector-drift-task-vs-engine`): раздача закрывает строку не только как `done` — ⚪ пусто кладётся как `dry`, ⛔ непереносимо как `skip` (`VALID_STATUS` движка). Селектор «`status != done`» поэтому поднимает УЖЕ отработанные строки: замер 08.09 — 40 «не-done», из них 17 закрыты вердиктом, и первые три FIFO были ровно такими. Открытая строка = статус НЕ в {done, dry, skip} И без даты `done` (строка вовсе без поля `status`, как писал casebook-drip, тоже открытая — наивный `== pending` её теряет).

⛔ **ПРИПАРКОВАННУЮ СТРОКУ НЕ БЕРЁМ** (замер 07.09, 1-й датированный случай `ochered-ne-uvazhaet-pole-parkovki-revisit`): строка может нести `revisit: <дата>` — это парковка до урожая, а не обычный `pending`, и ни текст рутины, ни `share_fix_queue.py` её не отличают. Перед взятием кандидата: `revisit` в будущем ⇒ **пропустить, статус не трогать**, взять следующий FIFO. Иначе в мир уезжают недоказанные числа (07.09 так чуть не ушёл A/B с n=1 за сутки до урожая). Популяцию очереди читай прибором (`share_fix_queue.py status`), а не числом из текста задачи — оно стареет молча (класс `share-fix-selector-drift-task-vs-engine`, 2 случая).

## Шаг 0 — порог (2 булевых, оба ДА, иначе честный ⛔)
1. **Переносимость:** чужой человек может воспроизвести наш симптом БЕЗ наших внутренностей (наших скриптов, нашей инфры, наших аккаунтов)? Одноразовый глюк самоделки миру не нужен.
2. **Чистота:** в раздаваемом нет секретов/приватного/внутренних имён (аккаунты, задачи, пути с личным)? Скрипт для мира = НОВЫЙ чистый файл на английском, не внутренняя кнопка. Леак-скан глазами обязателен.

## Шаг 1 — реверс-поиск по ДОСЛОВНОМУ симптому (2 минуты)
```bash
gh search issues "<симптом дословно: код ошибки / статус / текст диалога>" --limit 30 --sort updated
```
Пробуй 2-3 формулировки (код ошибки `0x…`, статус `Modified, NeedsRemediation`, фраза из диалога). Пусто везде → вердикт ⚪ с названным запросом, конец.

⛔ **ГОЛОЕ ЧИСЛО В ЗАПРОСЕ = ЛОЖНЫЙ НОЛЬ** (замер 08.09.2026, 1-й датированный случай `gh-search-golye-chisla-chitayutsya-kak-nomer-issue`): `gh search issues "gemini cli valid license 3501"` возвращает issue **с номером 3501** из случайных репо (BusinessCentral, WordPress/Learn…), а не текстовый матч — выдача выглядит как честный поиск и читается как «фронт пуст». Так строка очереди 03.09 получила вердикт «пусто, 3 формулировки», а поиск ТОЧНОЙ ФРАЗОЙ `'"valid license of this product"'` в тот же вечер дал 4 живых треда, крупнейший на 45 комментов.
Правило: ищи **фразой в кавычках без чисел**, номер ошибки добавляй словами («error 3501» отдельным прогоном); длинная фраза из 6+ слов тоже отдаёт пусто — GitHub ANDит токены, дели на 1-3 ключевых слова + `--repo`.

⚠️ **ДОМЕН-ГЕЙТ: дверь может молчать.** `github_targets.py --top/--check` требует `~/.claude/registry/github-universe/targets.json`; на хабе 08.09 файла (и конвейера сборки) НЕТ — прибор выходит exit 2 на ЛЮБОЙ вызов. Гейт при этом не отменяется: применяй `registry/github-universe/domain.json` руками (own_pain → org вендора + `keyword_regex` → экосистема круга) и **назови в вердикте, что дверь была мертва**. Тихо считать «гейта нет» ⛔.

## Шаг 2 — отобрать 3-5 ЛУЧШИХ живых тредов (dev капсом: «ТРИ - ПЯТЬ, не 1-2»)
Критерии лучшего: живой (человеческая активность, не бот-бампы) · наш симптом там воспроизведён (не однословная коллизия) · есть кому помочь (страдальцы без решения). Дедуп: проверь, нет ли нас (tonydzi) уже в треде. Перекрёстно-связанные треды одного класса сверх 5 — НЕ слать: 7-й одинаковый коммент = веер. Ужимание до 1-2 «чтобы не отсвечивать» — нарушение §1.5 точно так же.

## Шаг 3 — раздать: каждый коммент ЗАТОЧЕН под тред

⭐ ЧЕМ ПОДАВАТЬ (замер 05.09): тред — PR и касание ПЕРВОЕ → только `gh pr review <N> -R <owner/repo> --comment --body-file <файл>`. `gh pr comment` не создаёт объект Review, работа не видна ни в графе вкладов, ни в фильтре `reviewed-by:tonydzi`, которым нас ищут (в чужих PR за 30 дн: 127 комментов против 7 ревью = 5.2% видимых). ⛔ ГРАНИЦА: у ISSUE ревью НЕ СУЩЕСТВУЕТ — там `gh issue comment`, и это большинство раздач; реплика в идущем PR-диалоге — тоже коммент. В вердикте называть, чем подано. Канон: Библия `reglament-v-chuzhom-pr-pishem-revyu-a-ne-kommentariy` + файл-константа `$OBSIDIAN_VAULT/08-Templates/github-review-not-comment.md`.

- ⭐ ПЕРЕД созданием gist/repo — прогони `/pack` (декрет 24.08: наружу выходит ПРОДУКТ, не сниппет: README по скелету, `--selftest`, дружелюбные комментарии, гейт публикации). Вердикт /pack «не дотянул» = сперва дотянуть, потом раздавать.
- Раскрытие Майкрофта первой строкой (§3.3), дальше — по существу ИХ улик: что у них в треде уже есть и как наша находка это дополняет/объясняет. Копипаста-веер ⛔.
- ⚠️ ТЕЛО КОММЕНТА БЕЗ BOM: файл под `-F body=@file` пиши только UTF-8 **без BOM** (python `open(...,encoding='utf-8')` / `Set-Content -Encoding utf8NoBOM`); PowerShell `Out-File`/`>` на этой машине ставит BOM по умолчанию, и `U+FEFF` уезжает ПЕРВЫМ символом публичного коммента — прямо перед раскрытием Майкрофта. Замер 01.09.2026: так ушли все 7 тредов ночной раздачи, чинено правкой постфактум. Перед постом: `head -c 3 <файл> | xxd` → `efbbbf` = стоп.
- Скрипт-лечилка → публичный gist (после Шага 0.2) → ссылка. Ссылку в уже отправленные комменты дописывай ПРАВКОЙ своих сообщений, не новыми постами: `gh api -X PATCH repos/<r>/issues/comments/<id> -F body=@file`.
- Кросс-вендор: тот же класс болезни у codex/gemini-cli — тоже дверь (прецедент openai/codex#35347).

## Шаг 4 — вахта + вердикт (молчание запрещено)
```bash
python "$USERPROFILE/.claude/scripts/pr_watch.py" --add <url каждого треда>
```
Вердикт в отчёт, один из трёх: **🟢 раздал** (ссылки) · **⚪ искал-пусто** (запрос назван) · **⛔ непереносимо/приватно** (причина). Треды дальше веду САМ (реглумент `reglament-github-kommunikaciya-vsegda-sam`), показ в утреннем отчёте из `pr_watch --digest`; ответ живого инженера → /pr-reply Шаг 5-бис (контент-воронка).

## Границы
- Юридическое (CLA/DCO), деньги, секреты, масс-действия = Tier-2 → пауза+спрос.
- Правда в цифрах: раздаём только доказанное нашим /tt; гипотезы помечаем 🤔 прямо в комменте.
- Скилл ничего не решает про НАШ контент-каскад — только GitHub-треды + gist.

⭐⭐ ДОМЕН-ГЕЙТ (07.09) — ЛАЗЕРНЫЙ ФОКУС (приказ оператора 07.09.2026: «мусорные PR нам не нужны, нанимающий инженер должен за минуту понять: этот человек живёт в агентских рантаймах»).
Цели ТОЛЬКО из нашего круга: агентские фреймворки · LLM SDK · MCP · память для LLM · evals · observability для LLM.
Дверь: `python3 ~/.claude/scripts/github_targets.py --top 20` — по умолчанию отдаёт только domain=core; первыми идут ⭐ own_pain (репо, обо что споткнулись САМИ во флоте — правило первого приоритета), дальше остальной круг.
Репо не из выдачи → `--check owner/repo`: domain=off или «нет в списке» = НЕ ТРОГАТЬ, даже если issue красивая и хозяин живой. Исключение только по прямому слову оператора.
Правила и own_pain: `~/.claude/registry/github-universe/domain.json` (0 LLM; тест `_test_github_targets_domain.py`).
Метод (репро · красный тест · мутации · ревью объектом Review) не меняется — сужены только мишени.


ARGUMENTS: candidate: telethon/OOM terminal-status class → 4 in-domain threads

---

> `Bash` -- {"command": "mkdir -p \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1fcf6334/scratchpad\" && python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, os\nd = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\4fa25333-84

---

> `Bash` -- {"command": "S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1fcf6334/scratchpad\"\ngh issue comment 34281 -R BerriAI/litellm --body-file \"$S/a_litellm_34281.md\" 2>&1 | tail -2\ngh issue comment 38535 -R BerriAI/litellm --body-file \"$S/b_litel

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts\nfor u in https://github.com/BerriAI/litellm/issues/34281 https://github.com/BerriAI/litellm/issues/38535 https://github.com/anthropics/claude-code/issues/82416 https://github.com/anthropics/claude-code/issues/88738; do python pr_watch.py --add \"$u\" 2

---

> `Bash` -- {"command": "python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io, json\np = r'D:\\Vault\\Vault-Knowledge\\_outreach\\share_fix_queue.jsonl'\nlines = io.open(p, encoding='utf-8').read().split('\\n')\nupd = {\n 45: dict(status=\"done\", done=\"2026-09-10\", threads=[\n   \"https://github.com/BerriA

---

> `Bash` -- {"command": "python - <<'PY'\n# -*- coding: utf-8 -*-\nimport io\np = r\"C:\\Users\\dev\\.claude\\scheduled-tasks\\share-fix-daily\\SKILL.md\"\ns = io.open(p, encoding='utf-8').read()\nanchor = \"Репо не из выдачи → `--check owner/repo`\"\nadd = (\"⚠️ ДВЕРЬ МЕРТВА НА ХАБЕ (замер 10.09.2026, смена 

---

> `Bash` -- {"command": "python routine_runlog.py add share-fix-daily \"сделал: раздал 1 кандидата (класс «терминальный статус без самовосстановления + OOM убивает детей, родитель зелёный») в 4 живых треда own_pain-репо: litellm#34281, litellm#38535, claude-code#82416, claude-code#88738; все 4 на вахте pr_watch

---

> `Bash` -- {"command": "python bus_send.py --to ALL --subject \"share-fix-daily 10.09\" --body \"🌍 share-fix-daily (хаб): раздал 1 кандидата → 4 треда · dry 1 · skip 2 · очередь осталась 19 из 85 · невидимых 0.\nКласс: терминальный статус без самовосстановления + cgroup-OOM убивает детей, родитель жив → движок

---

> `Bash` -- {"command": "python bus_send.py --to ALL \"🌍 share-fix-daily (хаб, 10.09): раздал 1 кандидата → 4 треда · dry 1 · skip 2 · очередь осталась 19 из 85 · невидимых 0.\nКласс: терминальный статус без самовосстановления + cgroup-OOM убивает детей, родитель жив → движок молчит зелёным (наш замер: 45 дней,

---

> `Bash` -- {"command": "date \"+%H:%M %Z\"; TZ=Europe/Lisbon date \"+Lisbon %H:%M\"", "description": "Check clock"}

---

**Claude:**

[⏰ четверг, ночь, 05:30, 10 сентября 2026]

# 🌍 share-fix-daily: раздал 4 треда, дверь домен-гейта оказалась мёртвой

**Замер до работы:** `pending=23 invisible=0 done=40 всего=85`, lint чистый — ложного нуля нет, чинить `repair` нечего. Журнала рутины не было: я первая смена, тетрадь завёл.

**Раздал (1 кандидат → 4 живых треда).** Класс: *терминальный статус без самовосстановления + cgroup-OOM убивает дочерние процессы, родитель жив → движок молчит зелёным*. Наши доказанные числа в комментах: 45 дней тишины (16.07–30.08), 31 воркер в одном терминальном статусе, реанимация 26 статусов + 2 перелогина, поток 4132 msg/8 мин.

| тред | почему он | чем подано |
|---|---|---|
| [litellm#34281](https://github.com/BerriAI/litellm/issues/34281) «Fail Gracefully for Health Checks», c10 живой | у них try/except — половина; вторая половина (вердикт обязан протухать и переспрашивать) — ровно наши грабли | `gh issue comment` |
| [litellm#38535](https://github.com/BerriAI/litellm/issues/38535) terminal `stop_reason` при 200 OK | сигнал успеха берётся с конверта, а не с работы — наш случай слоем ниже | `gh issue comment` |
| [claude-code#82416](https://github.com/anthropics/claude-code/issues/82416) LSP «alive, пустой ответ, не восстанавливается» | пусто ≠ ошибка; наш приём — канарейка, чей правильный ответ не может быть пустым | `gh issue comment` |
| [claude-code#88738](https://github.com/anthropics/claude-code/issues/88738) PreToolUse hook молча перестал стрелять | тишина не сигнал; предложил счётчик вызовов хука + громкое уведомление при отключении | `gh issue comment` |

Все четыре на вахте `pr_watch` (реестр 403 позиции), каждый коммент заточен под их улики, копипасты нет, раскрытие Майкрофта первой строкой, BOM проверен (`68692c` = «hi,»).

**Остальные строки закрыты вердиктом, не молчанием:** ⚪ `dry` — link-at-birth (в круге пусто по 4 запросам: orphan memories / memory entries links / generated notes / knowledge base backlinks); ⛔ `skip` ×2 — orphan-policy и flagship-index: живые треды есть, но только в PKM/note-app репо и github-мете, это вне лазерного круга. Очередь 23 → 19.

**Главная находка смены (⚠️ и она же чинилась).** Дверь домен-гейта на хабе мертва: `github_targets.py` требует `~/.claude/registry/github-universe/targets.json` — файла нет, и каталога-конвейера `~/.claude/scripts/github_universe/`, на который прибор ссылается в подсказке, тоже нет. Любой `--top`/`--check` = exit 2. Гейт я не отменял: применил `domain.json` руками — 18 own_pain-репо как сертифицированные цели, поиск сразу `gh search issues "<2-3 слова>" --repo <own_pain> …`. Абзац «⚠️ ДВЕРЬ МЕРТВА НА ХАБЕ» с этим обходом вписал в SKILL.md рутины (в скилле `/share-fix` эта грабля была с 08.09, в файле рутины — нет).

Вторая грабля, тоже записана: запросы из очереди дословно (6+ слов) дают **ложный ноль** — GitHub ANDит токены; работают 2-3 слова.

📝 **Вердикт о скилле (§9.3-бис):** правил файл рутины (дыра про мёртвую дверь), сам `/share-fix` править не надо — обе пережитые грабли там уже описаны, новых он мне не создал.

Отчёт ушёл dual-send: `syncthing:OK · tg-03:OK`.

🧒 **Простыми словами:** ночью я разношу по чужим проектам то, что мы сами недавно починили. Сегодня разнёс историю «программа умерла, а табло горит зелёным» в четыре чужих обсуждения, где люди мучаются тем же. По дороге выяснилось, что наш «список разрешённых адресов» на этом компьютере просто отсутствует — пришлось выбирать адреса вручную по правилам, а в инструкцию для следующей смены я вписал: не удивляйся, дверь сломана, вот обход.
