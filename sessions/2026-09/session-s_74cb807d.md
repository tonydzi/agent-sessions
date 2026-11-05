---
session: s_74cb807d
date: 2026-09-16
words: 6720
turns: 37
tools: "Bash, Edit, Read, ToolSearch, Write, mcp__ccd_session_mgmt__list_sessions, mcp__ccd_session_mgmt__set_session_title, mcp__telegram__get_history"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-16 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_74cb807d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: bus:sm:auto-hub-260916-sm-T08.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
# auto-hub-260916-sm-T08 — Шаг 8: entity-gate затянуть на gold, затем Personalized PageRank по wikilinks вместо 1-hop/40

Ты — сессия Claude Code на хабе HUB-01, автор `HUB-01·claude`, узел хаб. Первым делом `set_session_title "AUTO-hub-sm-T08 entity-gate-then-ppr"`. Карточка задачи: `D:\Vault\Vault-Knowledge\10-Tasks\task-2026-09-16-sm-T08-entity-gate-then-ppr.md` — открой, переведи state → wip, touched_at → сегодня; закрывай её же по факту.

📛 ON AIR: первым делом объяви себя — `python ~/.claude/scripts/onair.py check --zone <зона>`, чисто → `onair.py declare --zone <зона> --mode exclusive|collab --title "<суть>" --ttl-hours <N>`; в конце `onair close`. Зона занята соседом — НЕ править параллельно: читай его табличку, договаривайся в 03 или бери другой кусок.
👤 КОНСОЛИДАТОР: если по этой теме поднято больше ОДНОГО исполнителя — консолидатор <ИМЯ_СЕССИИ_ИЛИ_УЗЛА>. Он сводит результаты и объявляет «готово»; остальные сдают ему кусок и НЕ пишут свой финальный вердикт. Исполнитель один — эта строка не действует.
🔁 RECALL ЛЕТЯЩЕЙ РАБОТЫ (до постройки, не после): `onair.py list` (кто сейчас в воздухе) + свежие панели `~/.claude/scripts/cc-review/bridge-state/usage.jsonl` (вопрос уже гонялся соседом → читай леджер, добавляй ДЕЛЬТУ, панель заново не гоняй — STOP-DUP) + журнал поломок через `python ~/.claude/scripts/breakage.py find "<текст>"` (этот класс уже разбирали?). Нашёл чужой готовый артефакт — ПЕРЕИСПОЛЬЗУЙ, свой не рожай.
🪫 БАК И СМЕРТЬ ПРИ РОЖДЕНИИ: пачку fireAt-сидов разноси с учётом бака подписки (одна ночь + шаг 15 мин = 4 из 5 умирают об «session limit»). Умер об лимит при рождении — это обязано быть ЗАМЕЧЕНО: следующая сессия и `/retro` проверяют «сид родил ретро?» — одобренная задача без следа исполнения считается НЕ сделанной, а не идущей.
🔍 УЛИКА ПРИ СТАТУС-CLAIM: любое ✅ про ФАЙЛ, КОД или ЧУЖУЮ ПРОВЕРКУ ставится ТОЛЬКО с уликой в том же заходе: `ls`/`cat`/цитата строки/exit-код. Не читал своими глазами — пиши 🤔 и говори прямо, что не проверено; пусто ИЗ ОДНОГО места ≠ «нет на диске» (§5.4) — назови, ГДЕ искал. Наружный док/README/INSTALL/отчёт перед выдачей прогони: `python ~/.claude/scripts/status_claim_lint.py <файл>`.
🤝 ТЫ АВТОНОМНЫЙ КОФАУНДЕР, НЕ ИСПОЛНИТЕЛЬ С ВОПРОСАМИ (приказ оператора 13.09.2026): этот заход идёт БЕЗ человека, поэтому развилку, неполное ТЗ и «а как он хотел» решаешь ТЫ и доводишь до результата, а решение кладёшь в отчёт постфактум («решил X, потому что Y, сделал Z»). Заход, кончившийся «жду ответа оператора» на ОБРАТИМОМ, считается НЕ сделанным. оператору остаётся ЗАКРЫТЫЙ список: деньги · необратимое удаление · юридическая подпись · секреты 3-м лицам · масс-рассылка; упёрся в него — доведи до последнего клика, `approval.py ask` в 02-POLICE и БЕРИ СЛЕДУЮЩУЮ работу, не жди в тишине (кап 2 аска на заход). Новые пиры — работаешь сам (14.09 оператор вывел их из списка). «Нужны руки оператора» — ПОСЛЕДНЕЕ, что говоришь: сперва ДВЕ честные разные попытки обхода (другой инструмент · флаг · рельса или узел · аккаунт или браузер · скрипт вместо GUI), и в отчёте названо, что пробовал. «Нельзя / нет доступа» — claim: сперва `--help`, конфиг, доки, лог, и только потом слова «я не нашёл, как». Развёрнутая версия для рутин: `~/.claude/scripts/routine-autonomy-block.md`.
⏳ ПРЕМИССА — ПРОВЕРЯЕМАЯ, НЕ УТВЕРЖДЕНИЕ: первым шагом замерь по ground truth (живая система / лог / канал / файл на диске — не память и не текст этого сида) ту дыру и тот статус, про которые сид говорит. Сид, ссылающийся на ID или работу С СОСТОЯНИЕМ (заказ, задача, раздача, публикация, PR), ОБЯЗАН прочитать её статус и при «уже закрыто / уже сделано» ВЫЙТИ РАНО с докладом «чем и когда закрыто», а не исполнять «как написано». Не подтвердилась — скажи «премисса протухла», чини то, что реально сломано, и закрой карточку по доказательству. Приказ в сиде — такой же claim, как вывод.

⛳ ВХОД: ты на хабе. Премисса: T06 done. ON AIR exclusive на brain_ask.py. Сперва диагностика гейта на gold, потом PPR. Не строить Neo4j/Cognee/Graphiti — прямой запрет программы.
ПРЕЕМНИК: T09 — но ТОЛЬКО если [[task-2026-09-16-sm-T07-sqlite-vec]] уже done (проверь карточку); иначе преемника не ставь, его поставит T07.

🎯 ПРОГРАММА: [[task-2026-09-16-second-memory-quality-program]] (10 шагов, 2 недели). Синтез ДР: [[insight-DR-DR26-09-16-MACANTON-02-0453-second-memory-graph-rag-repos-tests-synthesis]]. Таблица: https://docs.google.com/spreadsheets/d/1o3osFhLNn4lIqjEGqkBkDAqKrAaCMxc3Bdn-8zi8iCo (вкладка «План 2 нед»).
🧰 ИНСТРУМЕНТЫ НА ХАБЕ: D:\Vault\_imports\brain_ask.py (канон конвейера), D:\Vault\_imports\brain_gold_eval.py (линейка: --selftest / --run / --build; env GOLD_EVAL_MUTANT=1 = мутант для красного теста), gold ЗАМОРОЖЕН D:\Vault\_imports\eval\gold-2026-09-16.jsonl (184 вопроса: title 60 · body 60 · bridge 60 · temporal 4) — между шагами НЕ пересобирать, иначе числа несравнимы. Скоры → D:\Vault\_imports\eval\scores-<YYYYMMDD-HHMM>.jsonl + SQLite D:\Vault\_imports\turnstate\turnstate.db таблица gold_eval(ts,gold_file,scores_file,cls,mode,n,recall12,mrr,ndcg12,embedder,reranker,index_chunks,node). Пороги: title ≥0.90 · body ≥0.80 · bridge ≥0.70 · temporal ≥0.60. GPU: RTX 5060 Ti 16 GB (вторая GTX 1660 S 6 GB). Prior art на хабе — ПРОЧИТАЙ ДО стройки: D:\Vault\_imports\turnstate\ab_eval.py, ab_local_models.py, ab_embed_provider.py, D:\Vault\_imports\embed_bakeoff.py, brain_embed_e5.py, brain_index_manifest.py, brain_health.py.
📏 ПРАВИЛО ПРОГРАММЫ (не обсуждается): любой шаг, меняющий конвейер или индекс, мержится ТОЛЬКО с прогоном линейки ДО и ПОСЛЕ на том же gold; регресс > 0.01 nDCG@12 на ЛЮБОМ классе = откат правки (git revert / вернуть файл), а в отчёте число и причина. «Улучшил» без двух таблиц = не сделано. Индекс e5 (_brain_e5.npy/_meta.pkl) НЕ перезаписывать — новые модели пишут в СВОИ файлы (_brain_<имя>.npy), переключение через env BRAIN_EMB_BACKEND.
🔐 ГРАНИЦЫ: ничего наружу (GitHub/посты) кроме шага 10; секреты не трогаем; чужие сессии на хабе не гасим; brain_ask.py правим только после `preflight_shared_edit.py` и ON AIR.
📣 ДОКЛАД (обязателен, «сделал → объяви»): (1) карточка задачи в 10-Tasks: state → done/blocked, evidence = обе таблицы линейки (цифры, не «стало лучше»), outcome; (2) строка в [[task-2026-09-16-second-memory-quality-program]] таблице «План» — состояние шага; (3) вкладка «План 2 нед» в Google-таблице через `python ~/.claude/scripts/sheets.py` (библиотека: set_range) — колонка «Состояние»; (4) одна строка в TG-03 через `python ~/.claude/scripts/bus_send.py NODE-0X "REPORT: <шаг> · <4 числа Recall@12 title/body/bridge/temporal> · <дельта nDCG> · <вердикт мерж/откат>"`; (5) /tt по собранному с красным тестом на мутанте; (6) вердикт о скилле и о собственной инструкции (§9.3-бис). Сессия кончилась «жду оператора» на обратимом = не сделана.
🔗 ЦЕПОЧКА ВОЛН: закончил (done ИЛИ blocked с причиной) → ПОДНИМИ преемника сам через рельсу 001 (видимая сессия на хабе, 0 LLM в тракте): в PowerShell `python C:\Users\dev\.claude\spawn_seeds\second-memory\fire_seed.py C:\Users\dev\.claude\spawn_seeds\second-memory\<ID>.md` (читает сид из файла и зовёт voice001_fire.py без шелл-кавычек; --dry-run для проверки) — exit 0 = сессия поднята, 7 = уже поднималась (дубль, это нормально), 3 = не вышло → фолбэк: `python C:\Users\dev\.claude\scripts\spawn_queue.py add --task-id <ID> --description "<заголовок>" --prompt-file C:\Users\dev\.claude\spawn_seeds\second-memory\<ID>.md` (очередь разгрузит живая сессия хаба) + строка в 03. ID преемников названы в конце этого сида (полный id = auto-hub-260916-sm-Txx). ⛔ В TG-группу 001 сессия НЕ пишет ничего (приказ 15.09).

⚠️ ГРАБЛИ ЛИНЕЙКИ (оплачено T01, 16.09): `brain_gold_eval.py` запускать ТОЛЬКО интерпретатором `PYTHON_EXE` из `~/.claude/machine.env`. Любой другой python (например `.brain-venv`) даёт **exit 0 за 1 секунду с пустым stdout**: `brain_ask.py` при импорте делает `os.execv`, а на Windows это не замена процесса, а детач — работа уходит невидимому ребёнку, scores появляются через 3 минуты, и прогон читается как «мгновенный успех». Успехом считать только вывод, содержащий строку «ЛИНЕЙКА второй памяти». Ночная рутина и её пороги: `~/.claude/scripts/brain_gold_eval_nightly.py` (`--check-only --dry-run` сравнит две последние строки `gold_eval`, ничего не гоняя).
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

---

**Claude:**

🕐 **среда, вечер, 22:08, 16 сентября 2026**

Начинаю T08. Первым делом — заголовок сессии, карточка, ON AIR и проверка премиссы (T06 done?).

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && ls -la task-2026-09-16-sm-T0*.md 2>&1", "description": "List T0x task cards"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "AUTO-hub-sm-T08 entity-gate-then-ppr"}

---

> `Bash` -- {"command": "echo \"=== T08 ===\" && cat task-2026-09-16-sm-T08-entity-gate-then-ppr.md && echo \"=== T06 head ===\" && head -30 task-2026-09-16-sm-T06-title-h1-in-chunk.md && echo \"=== T07 head ===\" && head -20 task-2026-09-16-sm-T07-sqlite-vec.md", "description": "Read T08 card and T06/T07 state

---

> `Bash` -- {"command": "cd ~ && python ~/.claude/scripts/onair.py list 2>&1 | head -60; echo \"=== ZONES ===\"; python ~/.claude/scripts/onair.py zones 2>&1 | head -40", "description": "ON AIR list and zones"}

---

> `Bash` -- {"command": "cd ~ && python ~/.claude/scripts/onair.py check --zone vault-imports/brain-graph 2>&1 | tail -20", "description": "ON AIR check zone brain-graph"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && wc -l brain_ask.py && grep -n \"looks_like_entity\\|GHOPS\\|GMAX\\|wikilink\\|graph\" brain_ask.py | head -80", "description": "Grep graph internals in brain_ask.py"}

---

> `Bash` -- {"command": "cd ~ && python ~/.claude/scripts/onair.py declare --zone vault-imports/brain-graph --mode exclusive --title \"T08: entity-gate замер на gold + Personalized PageRank по wikilinks вместо 1-hop/40\" --ttl-hours 6 2>&1 | tail -10", "description": "Declare ON AIR exclusive"}

---

> `Bash` -- {"command": "sed -n '180,270p' brain_ask.py", "description": "Read brain_ask.py 180-270"}

---

> `Bash` -- {"command": "sed -n '180,275p' /e/Obsidian/_imports/brain_ask.py", "description": "Read brain_ask.py 180-275"}

---

> `Bash` -- {"command": "sed -n '400,480p' /e/Obsidian/_imports/brain_ask.py", "description": "Read graph expansion block"}

---

> `Bash` -- {"command": "cat ~/.claude/machine.env 2>/dev/null | head -20; echo \"=== gold eval ===\"; wc -l /e/Obsidian/_imports/brain_gold_eval.py; grep -n \"mode\\|graph\\|def \\|cls\" /e/Obsidian/_imports/brain_gold_eval.py | head -60", "description": "machine.env + gold eval structure"}

---

> `Bash` -- {"command": "sed -n '168,250p' /e/Obsidian/_imports/brain_gold_eval.py", "description": "Read gold eval run()"}

---

> `Bash` -- {"command": "ls -la /e/Obsidian/_imports/eval/ | tail -20", "description": "List eval dir"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && head -c 400 eval/_gold_eval_last.json; echo; echo \"--- row sample ---\"; head -1 eval/scores-20260916-2201.jsonl | python -c \"import sys,json; r=json.loads(sys.stdin.read()); print({k:(v if not isinstance(v,(dict,list)) else type(v).__name__) for k,v in r.it

---

> `Bash` -- {"command": "python - <<'PY'\nimport json, collections\nrows=[json.loads(l) for l in open('eval/scores-20260916-2201.jsonl',encoding='utf-8') if l.strip()]\nprint('rows', len(rows))\nEPS=1e-9\nagg=collections.defaultdict(lambda: collections.Counter())\ndsum=collections.defaultdict(float)\nfor r in r

---

> `Bash` -- {"command": "python - <<'PY'\nimport json, collections, statistics\nrows=[json.loads(l) for l in open('eval/scores-20260916-2201.jsonl',encoding='utf-8') if l.strip()]\nprint('%-9s %-7s %6s %6s %6s  %s' % ('cls','mode','recall','mrr','ndcg','cand_added(avg)'))\nfor c in ('title','body','bridge','tem

---

> `Bash` -- {"command": "ls -la _brain*.npy _brain*.pkl 2>/dev/null; grep -n \"EMB_PATH\\|META_PATH\\|def load_index\" brain_ask.py | head -20", "description": "Find index files"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport json, pickle\nfrom pathlib import Path\nmeta=pickle.load(open('_brain_e5_meta.pkl','rb'))\nif isinstance(meta,dict): meta=meta.get('meta',meta)\nprint('meta len', len(meta), 'sample keys', list(meta[0].keys()))\nstems={Path(m['path']).stem.lower() for m in meta}\

---

> `Bash` -- {"command": "grep -i \"PYTHON_EXE\" ~/.claude/machine.env", "description": "Get PYTHON_EXE"}

---

> `Bash` -- {"command": "cat > /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad/diag_bridge.py <<'PY'\n# -*- coding: utf-8 -*-\n\"\"\"Диагностика bridge-класса: где теряются gold-цели — в наборе кандидатов или в реранке.\"\"\"\nimport os, sys,

---

> `Bash` -- {"command": "python ~/.claude/scripts/workspace_write_lease.py status 2>&1 | head -40", "description": "Check workspace lease status"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\diag_bridge.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"T08-диагностика: где теряются bridge-цели — в наборе кандидатов или в реранке.\n\nПуть к _imports

---

> `Bash` -- {"command": "\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\" \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\diag_bridge.py\" 2>&1 | tail -15", "description": "Run bridge d

---

> `Bash` -- {"command": "ls -la /e/Obsidian/_imports/brain_lex.py && grep -n \"def \\|RRF\\|K_RRF\\|enabled\" /e/Obsidian/_imports/brain_lex.py | head -40", "description": "Inspect brain_lex RRF"}

---

> `Bash` -- {"command": "sed -n '305,355p' /e/Obsidian/_imports/brain_lex.py; echo \"=== enabled ===\"; sed -n '200,215p' /e/Obsidian/_imports/brain_lex.py", "description": "Read rrf_fuse and enabled"}

---

> `Bash` -- {"command": "sed -n '100,125p' /e/Obsidian/_imports/brain_lex.py; echo \"=== dedup ===\"; grep -n \"def dedup_best_per_file\" -A 20 /e/Obsidian/_imports/brain_ask.py; echo \"=== retrieve_candidates ===\"; grep -n \"def retrieve_candidates\" -A 25 /e/Obsidian/_imports/brain_ask.py", "description": "R

---

**Claude:**

Диагностика дала железный корень. Строю модуль.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Графовая полоса второй памяти: wikilink-граф волта, 1-hop расширение и Personalized PageRank.\n\n

---

> `Bash` -- {"command": "date -u +%H:%M; python ~/.claude/scripts/workspace_write_lease.py status 2>&1 | grep -i \"_imports\\b\\|_imports <-\" | head -5", "description": "Check lease expiry vs now"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "def _cache_path():\n    root = os.getenv('IMPORTS_ROOT') or str(Path(__file__).resolve().parent)\n    r

---

> `Bash` -- {"command": "SP=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\"\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nexport IMPORTS_ROOT='D:\\Vault\\_imports'\nexport B

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\t08_ruler.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"T08: линейка-дельта на замороженном gold — 4 режима вместо двух.\n\nПочему отдельный прогон, а не п

---

> `Bash` -- {"command": "SP=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\"\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nT08_LIMIT=12 \"$PY\" \"$SP\\\\t08_ruler.py\" 2>&1 | ta

---

**Claude:**

PPR на title сразу минусует — гейт, который сейчас бесполезен, получает настоящую работу. Гоню полную линейку.

---

> `Bash` -- {"command": "SP=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\"\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"$SP\\\\t08_ruler.py\" > \"$SP\\\\t08_full_ru

---

**Claude:**

Результат крупный: bridge +0.100, body +0.017, но title −0.076. Считаю, какой гейт это чинит — симуляцией по уже полученным скорам, без новых прогонов.

---

> `Bash` -- {"command": "SP=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad\"\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<PY\nimport json, collections\nrows=[json.loads(l) f

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nSP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nexport T08_SCORES=\"$SP\\\\t08-scores-20260916-2222.json

---

**Claude:**

Порог по длине разделил бы классы идеально — но это подгонка под конструкцию gold. Ищу честный механизм: сохраняю полные порядки один раз, дальше перебираю параметры офлайн без GPU.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\t08_dump.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"T08: один дорогой прогон -> полные порядки на диск, дальше вся сетка параметров офлайн.\n\nПочему та

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"$SP\\\\t08_dump.py\" > \"$SP\\\\t08_dump.log\"

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\t08_sweep.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"T08: офлайн-перебор способов слить порядок реранкера с Personalized PageRank.\n\nЧитает `t08-orders

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"$SP\\\\t08_sweep.py\" grid 2>&1 | tail -35", "

---

**Claude:**

Чистый победитель без гейта. Проверяю, не иголка ли это — соседняя сетка и сплит-валидация.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\t08_stability.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"T08: устойчив ли найденный вариант слияния или это подгонка под 184 вопроса.\n\nВыгодный вывод 

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"$SP\\\\t08_stability.py\" 2>&1 | tail -45", "d

---

**Claude:**

Все три проверки чистые: плато широкое, сплит выбрал те же параметры, пустой граф совпал до 1e-12. Проверяю взаимодействие с гейтом и цену по времени.

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"$SP\\\\t08_sweep.py\" gate 0.85 10 1.0 5 2>&1 

---

**Claude:**

Гейт только съедает выигрыш — PPR его не использует. Константы зафиксированы. Беру лизу на общий файл.

---

> `Bash` -- {"command": "date -u +%H:%M; python ~/.claude/scripts/workspace_write_lease.py status 2>&1 | grep -i \"_imports\" | head -6; echo \"=== preflight help ===\"; python ~/.claude/scripts/preflight_shared_edit.py --help 2>&1 | head -25", "description": "Check lease + preflight usage"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/preflight_shared_edit.py \"D:\\Vault\\_imports\\brain_ask.py\" 2>&1 | tail -20", "description": "Preflight shared edit on brain_ask.py"}

---

> `Bash` -- {"command": "sed -n '480,530p' /e/Obsidian/_imports/brain_ask.py", "description": "Read brain_ask rerank call site"}

---

> `Bash` -- {"command": "sed -n '530,600p' /e/Obsidian/_imports/brain_ask.py", "description": "Read brain_ask final ordering"}

---

**Claude:**

Правлю модуль под финальные константы, затем врезаю в бой и в линейку.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "# --- константы полосы (держим рядом: их читают и правят вместе) ---\nGHOPS, GMAX = 15, 40      # 1-hop

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "def fuse_with_rerank(ranked_stems, ppr_stems):\n    \"\"\"Слить порядок реранкера с порядком PPR по РАН

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "ФЛАГ: BRAIN_GRAPH_PPR=1. Дефолт — ВЫКЛ, пока обе таблицы линейки не показали, что не хуже\n(правило про

---

**Claude:**

Теперь тест — пишу его так, чтобы он краснел на сломанном коде.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\_test_brain_graph.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Регресс графовой полосы (шаг 8 программы «второй мозг»).\n\nKILL-LIST — что именно обязан п

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nexport PYTHONPATH='D:\\Vault\\_imports'\necho \"--- Ч

---

**Claude:**

Два провала — один настоящий баг ручки, один мой кривой тест. И заметил риск расхождения замера с реализацией — проверяю его числом.

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nexport T08_ORDERS=\"$SP\\\\t08-orders.jsonl\"\n\"$PY\" -

---

**Claude:**

Расхождение мизерное (body +0.027 → +0.023) — беру честный вариант: PPR только переставляет кандидатов.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "    if not ppr_stems:\n        return ranked_stems\n    head = PPR_HEAD if head is None else head\n    

---

> `Bash` -- {"command": "SP='/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad'\ngrep -n \"не видит\\.\" -A 14 \"$SP/brain_graph.py\" | head -20", "description": "Inspect docstring boundary"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "    там структура и добавляет то, чего текстовое сходство не видит.\n    \"\"\"\n    PPR ТОЛЬКО ПЕРЕСТА

---

**Claude:**

Чиню найденный тестом баг ручки GHOPS=0 и свой кривой case4.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\brain_graph.py", "old_string": "    added, in_order, seen_p, hop_from = [], set(base_order), set(), []\n    for i in base_order:\n     

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad\\_test_brain_graph.py", "old_string": "    on = bg.fuse_after_rerank(ranked, meta_lin, ['n3', 'n2'], topn=4, head=2)\n    chk('case4 пер

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nexport PYTHONPATH='D:\\Vault\\_imports'\necho \"--- Ч

---

**Claude:**

Тест зелёный и краснеет на всех трёх мутантах. Врезаю в бой и в линейку.

---

> `Bash` -- {"command": "SP='/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad'\nIM='/e/Obsidian/_imports'\ncp \"$IM/brain_ask.py\" \"$SP/brain_ask.py.bak-t08\"\ncp \"$IM/brain_gold_eval.py\" \"$SP/brain_gold_eval.py.bak-t08\"\ncp \"$SP/brain_g

---

**Claude:**

Теперь врезка в `brain_ask.py` — 1-hop переезжает на общий модуль, PPR встаёт за флагом.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_ask.py", "old_string": "    base_order = list(order); added = []\n    if (graph or ab) and order:\n        try:\n            GHOPS, GMAX = 15, 40            # expand from top-15 hits, add at most 40 neighbours\n            by_base = 

---

> `Bash` -- {"command": "SP='/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad'\ndiff \"$SP/brain_ask.py.bak-t08\" /e/Obsidian/_imports/brain_ask.py | head -60; echo \"=== lease ===\"; python ~/.claude/scripts/workspace_write_lease.py status 2>

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_ask.py", "old_string": "    def _best_per_file(scored):\n        return dedup_best_per_file(scored, meta, TOPN)", "new_string": "    def _best_per_file(scored):\n        # Дедуп по файлу берётся БЕЗ обрезки на TOPN, а порезка отдана 

---

**Claude:**

Теперь линейка — убираю её копию 1-hop и добавляю PPR.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "    def rerank(query, cand):\n        if ce is None or not cand:\n            sc = [float(sims[i]) for i in cand]\n            return ba.dedup_best_per_file(sorted(zip(cand, sc), key=lambda x: -x[1]), me

---

> `Bash` -- {"command": "SP='/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad'\ndiff \"$SP/brain_gold_eval.py.bak-t08\" /e/Obsidian/_imports/brain_gold_eval.py && echo \"ИДЕНТИЧНЫ — чужих правок нет\"", "description": "Verify gold_eval unchang

---

> `Read` -- {"file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "offset": 168, "limit": 75}

---

> `Read` -- {"file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "offset": 240, "limit": 45}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "    def rerank(query, cand):\n        if ce is None or not cand:\n            # sims=None — это режим переигрывания: порядок 1-й ступени уже лежит в файле\n            # кандидатов, поэтому «без судьи» =

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "    import brain_rerankers as brr\n    prof = beb.resolve(backend)", "new_string": "    import brain_rerankers as brr\n    import brain_graph as bg\n    prof = beb.resolve(backend)"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "        base = ba.retrieve_candidates(sims, meta, query=g['query'])\n        # 1-hop graph expansion — копия логики brain_ask (GHOPS файлов, ≤GMAX соседей)\n        added, in_order, seen_p, hop_from = []

---

**Claude:**

Теперь прокидываю PPR в оба пути прогона линейки.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "        rr0 = time.time()\n        res = {}\n        for mode, cand in (('vector', base), ('graph', base + added)):\n            ranked = [stem(i) for i, _ in rerank(g['query'], cand)]\n            res[m

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "            base, added, sims = _replay(frozen, k, g, meta)\n            rr0 = time.time()\n            res = {}\n            for mode, cand in (('vector', base), ('graph', base + added)):\n             

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\n\"$PY\" -m py_compile brain_ask.py brain_gold_eval.py brain_graph.py _test_brain_graph.py && echo \"COMPILE OK\"\necho \"--- selftest линейки ---\"\n\"$PY\" brain_g

---

**Claude:**

Прогоняю официальную линейку — сначала ДО (флаг снят), чтобы доказать, что рефакторинг воспроизводит baseline.

---

> `Bash` -- {"command": "PY='C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe'\nSP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\ncd /e/Obsidian/_imports\nunset BRAIN_GRAPH_PPR\n\"$(cygpath -u \"$PY\")\" 

---

> `Bash` -- {"command": "SP='/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_74cb807d/scratchpad'\ntail -25 \"$SP/t08_before.log\"", "description": "Read before-run log"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_gold_eval.py", "old_string": "        # T08: 1-hop больше не копия, а ТОТ ЖЕ вызов, что в бою (brain_graph.expand_1hop).\n        added = bg.expand_1hop(sims, meta, base, by_base)", "new_string": "        base = ba.retrieve_candidate

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" -m py_compile brain_gold_eval.py && echo \"COMPILE OK\"\nnvidia-smi --query-gpu=index,name,memory.used,memory.total --format=csv 2>&1 | head -5", "description": "Compile fix + check

---

> `Bash` -- {"command": "grep -n \"def pick_device\" -A 30 /e/Obsidian/_imports/brain_common.py | head -40", "description": "Read pick_device logic"}

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\nunset BRAIN_GRAPH_PPR\n\"$PY\" 

---

**Claude:**

ДО совпало с baseline T06 до третьего знака — рефакторинг чистый. Гоню ПОСЛЕ.

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\nexport BRAIN_GRAPH_PPR=1\n\"$PY

---

**Claude:**

Все классы выросли, body впервые взял порог ≥0.80. Правило программы даёт мерж — включаю дефолтом и распространяю на обычный recall тоже.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_ask.py", "old_string": "            added = brain_graph.expand_1hop(sims, meta, base_order, by_base, keep=_keep)\n            # Personalized PageRank: НЕ источник кандидатов (97% правильных ответов bridge-класса\n            # и так 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_graph.py", "old_string": "def enabled():\n    \"\"\"Полоса PPR включается флагом; дефолт до вердикта линейки — ВЫКЛ.\"\"\"\n    return str(os.getenv('BRAIN_GRAPH_PPR', '')).strip().lower() in ('1', 'on', 'yes', 'true')", "new_string"

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_graph.py", "old_string": "    # --- case 5: выключённый флаг невидим --------------------------------------\n    os.environ.pop('BRAIN_GRAPH_PPR', None)\n    if MUT == 'flag':\n        bg.enabled = lambda: True\n    meta_lin = 

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\n\"$PY\" -m py_compile brain_ask.py brain_graph.py _test_brain_graph.py && echo \"COMPILE OK\"\necho \"--- чистый ---\"; \"$PY\" _test_brain_graph.py; echo \"exit=$?

---

**Claude:**

Теперь проверяю бой вживую и цену полосы, плюс регрессы соседних полос.

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\necho \"=== brain_ask БЕЗ полосы (рубильник 0) ===\"\nBRAIN_GRAPH_PPR=0 timeout 300 \"$PY\" brain_ask.py \"правило трёх дней и бамп\" 2>&1 | grep -E \"^##|^\\s*$\" |

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\ntimeout 300 \"$PY\" brain_ask.py \"правило трёх дней и бамп\" 2>&1 | head -25; echo \"exit=$?\"", "description": "Raw brain_ask output", "timeout": 700000}

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\nBRAIN_GRAPH_PPR=0 timeout 300 \"$PY\" brain_ask.py \"правило трёх дней и бамп\" >/dev/null 2>&1\ncp _brain_answer_rr.txt /tmp/off.txt\ntimeout 300 \"$PY\" brain_ask

---

> `Bash` -- {"command": "echo \"=== diff off vs on ===\"; diff /tmp/off.txt /tmp/on.txt | head -40; echo \"--- размеры ---\"; wc -l /tmp/off.txt /tmp/on.txt; echo \"--- первые 30 строк ON ---\"; head -30 /tmp/on.txt", "description": "Diff live outputs"}

---

**Claude:**

Полоса работает в бою: голова цела, хвост переставлен. Но вижу дефект — один файл кэша на два разных индекса. Замеряю цену и чиню.

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\nls -la _brain_graph.pkl 2>/dev/null\n\"$PY\" - <<'PY'\nimport os, sys, time\nsys.path.insert(0, r'D:\\Vault\\_imports')\nos.environ.setdefault('BRAIN_EMB_BACKEND

---

**Claude:**

Замер убил кэш: сборка с диска 0.50 с, из кэша 0.53 с — он не окупается. Убираю по АК-47.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_graph.py", "old_string": "def _cache_path():\n    \"\"\"Файл кэша графа. BRAIN_GRAPH_CACHE переопределяет путь — это нужно тесту и\n    любому прогону, который не имеет права писать в общий каталог индекса.\"\"\"\n    direct = os.get

---

> `Bash` -- {"command": "grep -n \"cache\\|pickle\\|_CACHE\" brain_graph.py | head -20", "description": "Find remaining cache references"}

---

> `Read` -- {"file_path": "D:\\Vault\\_imports\\brain_graph.py", "offset": 250, "limit": 18}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_graph.py", "old_string": "    if fp:\n        _CACHE[fp] = g\n        if use_cache:\n            try:\n                with open(cp, 'wb') as f:\n                    pickle.dump({'fp': fp, 'stems': stems, 'idx': idx, 'indptr': indptr

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nsed -i 's/^import pickle$//' brain_graph.py\nsed -i 's/^_CACHE = {}               # fingerprint -> Graph (в пределах процесса)$/_CACHE = {}               # fingerprint -> Graph (кэш В ПАМЯТИ ПРОЦЕССА; дискового нет, см. build)/' brain_graph.py\nrm -f _brain_grap

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_graph.py", "old_string": "ДЕГРАДАЦИЯ (инвариант полосы): нет графа, нет рёбер, сломался кэш, упал PPR — полоса\nвозвращает ИСХОДНЫЙ порядок и пишет строку в stderr. Пустой граф обязан давать ровно\nvector-поведение, а не падение; это

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_graph.py", "old_string": "ФЛАГ: BRAIN_GRAPH_PPR=1. Дефолт — ВЫКЛ, пока обе таблицы линейки не показали, что не хуже\n(правило программы: новое поведение едет тенью).\n\"\"\"", "new_string": "ЦЕНА ПОЛОСЫ (замер на живом волте): сборка

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_graph.py", "old_string": "  7. кэш графа не протухает при смене индекса (укажет на чужие файлы)", "new_string": "  7. кэш графа В ПАМЯТИ не протухает при смене индекса (укажет на чужие файлы)"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\ngrep -n \"BRAIN_GRAPH_CACHE\\|use_cache\" _test_brain_graph.py", "description": "Find cache env usages in test"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nsed -i \"/os.environ\\['BRAIN_GRAPH_CACHE'\\]/d\" _test_brain_graph.py\nsed -i \"s/^    chk_true('case7 кэш переиспользован при том же индексе', g2.n_edges == g.n_edges)/    chk_true('case7 кэш памяти переиспользован при том же индексе', g2 is g)/\" _test_brain_

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nsed -i 's/  5. выключённый флаг меняет выдачу (полоса обязана быть байт-в-байт невидимой)/  5. рубильник BRAIN_GRAPH_PPR=0 не выключает полосу (обязана стать байт-в-байт невидимой)/' _test_brain_graph.py\nls _test_*.py | head -30", "description": "List neighbour

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nfor T in _test_brain_ask _test_brain_recall _test_brain_lex _test_brain_emb_backends _test_chunk_heading_path _test_ab_recall _test_brain_rerankers _test_brain_vec_

---

**Claude:**

Все девять соседних регрессов зелёные. Второй заход по §4.3-бис — перепрогон обеих таблиц на финальном коде.

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\necho \"### ПРОГОН 2: ПОСЛЕ (деф

---

**Claude:**

Числа воспроизвелись точно, хотя индекс за это время подрос. Третий заход — контроль отката рубильником.

---

> `Bash` -- {"command": "SP='C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_74cb807d\\scratchpad'\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ncd /e/Obsidian/_imports\necho \"### КОНТРОЛЬ: рубильник 

---

**Claude:**

Все три захода сошлись, откат доказан. Закрываю карточку и докладываю.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY'\nimport re, io, os\np = r'D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-16-sm-T08-entity-gate-then-ppr.md'\nt = io.open(p, 

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY'\nimport io\np = r'D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-16-sm-T08-entity-gate-then-ppr.md'\nt = io.open(p, encoding

---

> `Bash` -- {"command": "tail -8 /e/Obsidian/Vault-Knowledge/10-Tasks/task-2026-09-16-sm-T08-entity-gate-then-ppr.md", "description": "Check file paths rendered correctly"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks\nF=task-2026-09-16-sm-T08-entity-gate-then-ppr.md\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY'\nimport io\np = r'D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-16-sm-T08

---

**Claude:**

Карточка закрыта. Обновляю таблицу программы и Google-таблицу.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks\ngrep -n \"T08\\|Шаг 8\\|| 8 \" task-2026-09-16-second-memory-quality-program.md | head -10\necho \"=== шапка таблицы ===\"; grep -n \"^| *шаг\\|^| *#\\|^|---\" task-2026-09-16-second-memory-quality-program.md | head -5", "description": "Locate T0

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY'\nimport io, re\np = r'D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-16-second-memory-quality-program.md'\nt = io.open(p, en

---

> `Bash` -- {"command": "python ~/.claude/scripts/sheets.py --help 2>&1 | head -30", "description": "Sheets CLI usage"}

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY' 2>&1 | tail -30\nimport sys\nsys.path.insert(0, r'C:\\Users\\dev\\.claude\\scripts')\nimport sheets\nSID = '1o3osFhLNn4lIqjEGqkBkDAqKrAaCMxc3Bdn-8zi8iCo'\nrows = sheets.g

---

> `Bash` -- {"command": "grep -n \"^def \" /c/Users/dev/.claude/scripts/sheets.py | head -25", "description": "List sheets.py functions"}

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY' 2>&1 | tail -25\nimport sys\nsys.path.insert(0, r'C:\\Users\\dev\\.claude\\scripts')\nimport sheets\nSID = '1o3osFhLNn4lIqjEGqkBkDAqKrAaCMxc3Bdn-8zi8iCo'\nprint('вкладки:

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY' 2>&1 | tail -6\nimport sys\nsys.path.insert(0, r'C:\\Users\\dev\\.claude\\scripts')\nimport sheets\nSID = '1o3osFhLNn4lIqjEGqkBkDAqKrAaCMxc3Bdn-8zi8iCo'\nstate = (\"✅ СМЕ

---

> `Bash` -- {"command": "python ~/.claude/scripts/bus_send.py NODE-0X \"REPORT: T08 entity-gate+PPR · Recall@12 title 0.950 / body 0.850 / bridge 0.451 / temporal 1.000 · nDCG bridge +0.103, body +0.023, title +0.006, temporal 0.000 (ни один класс не просел) · вердикт МЕРЖ, полоса PPR включена дефолтом, р

---

> `ToolSearch` -- {"query": "select:mcp__telegram__get_history", "max_results": 3}

---

> `mcp__telegram__get_history` -- {"chat_id": chat_REDACTED, "limit": 3}

---

**Claude:**

Доклад в 03 доехал. Проверяю условие преемника — карточку T07.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks\ngrep -E \"^state:|^outcome:\" task-2026-09-16-sm-T07-sqlite-vec.md | cut -c1-300\necho \"---\"; grep -E \"^state:\" task-2026-09-16-sm-T09-bitemporal-edges.md\necho \"--- сид T09 ---\"; ls -la /c/Users/dev/.claude/spawn_seeds/second-memory/auto

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"C:\\Users\\dev\\.claude\\spawn_seeds\\second-memory\\fire_seed.py\" \"C:\\Users\\dev\\.claude\\spawn_seeds\\second-memory\\auto-hub-260916-sm-T09.md\" --dry-run 2>&1 | tail -1

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"C:\\Users\\dev\\.claude\\spawn_seeds\\second-memory\\fire_seed.py\" \"C:\\Users\\dev\\.claude\\spawn_seeds\\second-memory\\auto-hub-260916-sm-T09.md\" 2>&1 | tail -6; echo \"f

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__list_sessions", "max_results": 3}

---

> `mcp__ccd_session_mgmt__list_sessions` -- {"limit": 6}

---

**Claude:**

T09 поднята и работает. Закрываю хвосты: карта системы, раскатка на флот, журнал.

---

> `Bash` -- {"command": "grep -rn \"_imports\" /c/Users/dev/.stignore /c/Users/dev/.claude/fleet_nodes.json 2>/dev/null | head -5\necho \"--- есть ли _imports в синке (конфиг syncthing) ---\"\npython ~/.claude/scripts/deploy_register.py --help 2>&1 | head -12", "description": "Check if _imports syncs to fle

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PY' 2>&1 | head -20\nimport json, os\np = os.path.expanduser('~/.claude/fleet_nodes.json')\nd = json.load(open(p, encoding='utf-8'))\nnodes = d.get('nodes', d)\nfor k, v in (no

---

> `Bash` -- {"command": "ls -la /e/Obsidian/_imports/.stfolder /e/Obsidian/_imports/.stignore 2>&1 | head -5\necho \"--- волт ---\"; ls -d /e/Obsidian/Vault-Knowledge/.stfolder 2>&1\necho \"--- родитель ---\"; ls -d /e/Obsidian/.stfolder 2>&1", "description": "Check syncthing markers on _imports"}

---

> `Bash` -- {"command": "grep -nE \"brain_graph|brain_ask|\\*\\.py|^!|^\\(?\\*\" /e/Obsidian/_imports/.stignore | head -20", "description": "Check stignore rules for py files"}

---

> `Bash` -- {"command": "sed -n '1,60p' /c/Users/dev/.claude/scripts/deploy_register.py | grep -nE \"usage|apply|verify|tier|Пример|example\" | head -20", "description": "Read deploy_register usage details"}

---

> `Bash` -- {"command": "PY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"C:\\Users\\dev\\.claude\\scripts\\deploy_register.py\" all brain-graph-ppr-20260916 \"Второй мозг: графовая полоса PPR включена дефолтом (шаг 8 программы); brain_graph.py + прав

---

**Claude:**

Блок справедливый. Пишу read-only пробу вместо теста.

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\_probe_brain_graph_lane.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Проба графовой полосы второй памяти: жива ли она НА ЭТОМ узле. READ-ONLY.\n\nЗачем отдельная проба, а не регресс `_test_brain_graph.py`: verify-шаг посылки гоняется\nна КАЖДОМ узле флота, а

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" _probe_brain_graph_lane.py; echo \"exit=$?\"\necho \"--- красный контроль: проба должна ловить сломанную полосу ---\"\ncp brain_graph.py /tmp/bg.bak\n\"$PY\

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" _probe_brain_graph_lane.py; echo \"clean exit=$?\"\ncp brain_graph.py /tmp/bg.bak\npython - <<'PYX'\n# heredoc-escape-ok: патч без escape-последовательносте

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ndiff /tmp/bg.bak brain_graph.py && echo \"brain_graph восстановлен байт-в-байт\"\n\"$PY\" _test_brain_graph.py | tail -2\n\"$PY\" \"C:\\Users\\dev\\.claude\\scrip

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"C:\\Users\\dev\\.claude\\scripts\\deploy_register.py\" NODE-0X,NODE-0X-2023PAL brain-graph-ppr-20260916 \"Второй мозг: графовая полоса PPR включен

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nCMD='python3 ~/.claude/scripts/verify_probe.py run D:\\Vault\\_imports\\_probe_brain_graph_lane.py'\necho \"проверка verify_probe локально:\"; python3 ~/.claude/

---

> `Bash` -- {"command": "grep -n \"def _run\\|def main\\|subprocess\\|executable\\|'run'\" /c/Users/dev/.claude/scripts/verify_probe.py | head -20", "description": "Inspect verify_probe run implementation"}

---

> `Bash` -- {"command": "sed -n '260,280p' /c/Users/dev/.claude/scripts/verify_probe.py", "description": "Read cmd_run body"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\npython3 ~/.claude/scripts/verify_probe.py run python3 \"D:\\Vault\\_imports\\_probe_brain_graph_lane.py\"; echo \"exit=$?\"", "description": "Correct verify_probe invocation", "timeout": 300000}

---

**Claude:**

Проба ловит реальную грабли класса: `python3` на узле — другой интерпретатор без numpy. Чиню в корне.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_probe_brain_graph_lane.py", "old_string": "import os\nimport sys\nimport shutil\nimport tempfile\nfrom pathlib import Path\n\nsys.path.insert(0, str(Path(__file__).resolve().parent))\nFAILS = []", "new_string": "import os\nimport re\nimpo

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\necho \"--- через python3 (чужой интерпретатор) ---\"\npython3 ~/.claude/scripts/verify_probe.py run python3 \"D:\\Vault\\_imports\\_probe_brain_graph_lane.py\"; echo \"exit=$?\"\necho \"--- через PYTHON_EXE напрямую ---\"\nPY=\"$(cygpath -u 'C:\\Users\\dev\

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nSTEP='python3 ~/.claude/scripts/verify_probe.py run python3 D:\\Vault\\_imports\\_probe_brain_graph_lane.py'\n\"$PY\" \"C:\\Users\\dev\\.claude\\scripts\\deplo

---

**Claude:**

Дом проб — `~/.claude/scripts`, там уже живут `_probe_muzzle` и соседи. Переношу и делаю путь переносимым.

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/_probe_*.py 2>/dev/null | head -6", "description": "Confirm probes home"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\ngit -C /c/Users/dev/.claude rev-parse --is-inside-work-tree 2>/dev/null && echo \"claude-config = git\" || echo \"claude-config не git\"\nmv _probe_brain_graph_la

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_probe_brain_graph_lane.py", "old_string": "sys.path.insert(0, str(Path(__file__).resolve().parent))\nFAILS = []", "new_string": "FAILS = []\n\n\ndef _menv(key):\n    \"\"\"Значение из ~/.claude/machine.env — у каждого узла сво

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" - <<'PYX'\n# heredoc-escape-ok: правка ссылки на machine.env внутри функции reexec, без escape-последовательностей\nimport io\np = r'C:\\Users\\dev

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nSTEP='python3 ~/.claude/scripts/verify_probe.py run python3 ~/.claude/scripts/_probe_brain_graph_lane.py'\n\"$PY\" \"C:\\Users\\dev\\.claude\\scripts\\deploy_regi

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\nSTEP='python3 ~/.claude/scripts/verify_probe.py run python3 ~/.claude/scripts/_probe_brain_graph_lane.py'\n\"$PY\" \"C:\\Users\\dev\\.claude\\scripts\\deploy_regi

---

**Claude:**

Раскатка зарегистрирована. Закрываю оставшееся: журнал, карта системы, ON AIR.

---

> `Bash` -- {"command": "python ~/.claude/scripts/selfheal.py journal --class probe-run-by-wrong-python --what \"verify-шаг посылки зовётся python3, а python3 на узле = другая сборка без numpy (хаб 16.09: pythoncore-3.14 вместо Python312 конвейера) -> проба падает не потому что полоса сломана, и узел повис бы л

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"D:\\Vault\\_imports\\arch\\sys_scan.py\" 2>&1 | tail -8", "description": "Rescan system architecture map", "timeout": 900000}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports\nPY=\"$(cygpath -u 'C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\python.exe')\"\n\"$PY\" \"D:\\Vault\\_imports\\arch\\arch_status.py\" 2>&1 | head -18", "description": "Read arch status after scan", "timeout": 600000}

---

> `Bash` -- {"command": "git -C /e/Obsidian/_imports rev-parse --is-inside-work-tree 2>/dev/null && echo \"_imports = git\" || echo \"_imports НЕ git\"\necho \"--- claude-config status ---\"\ngit -C /c/Users/dev/.claude status --short 2>&1 | head -10", "description": "Check git state of both repos"}

---

> `Bash` -- {"command": "git -C /c/Users/dev/.claude log --oneline -3 2>&1 | head -5\necho \"--- есть ли проба в индексе ---\"\ngit -C /c/Users/dev/.claude log --oneline -1 -- scripts/_probe_brain_graph_lane.py 2>&1\necho \"--- _imports status ---\"\ngit -C /e/Obsidian/_imports status --short 2>&1 | head -1

---

> `Bash` -- {"command": "git -C /c/Users/dev/.claude ls-files --error-unmatch scripts/_probe_brain_graph_lane.py 2>&1 | head -2\necho \"--- ignore? ---\"; git -C /c/Users/dev/.claude check-ignore -v scripts/_probe_brain_graph_lane.py 2>&1 | head -2\necho \"--- _imports: brain_graph ---\"; git -C /e/Obsidian

---

> `Bash` -- {"command": "git -C /e/Obsidian/_imports log --oneline -3 -- brain_graph.py brain_ask.py 2>&1 | head -6\necho \"--- последний коммит целиком ---\"; git -C /e/Obsidian/_imports log -1 --format='%H%n%an <%ae>%n%s%n%b' 2>&1 | head -12\necho \"--- трекаются ли соседние пробы в claude-config ---\"; git -

---

**Claude:**

Важная проверка: проба зовётся посылкой — доедет ли она на те узлы.

---

> `Bash` -- {"command": "ls -d /c/Users/dev/.claude/.stfolder /c/Users/dev/.claude/scripts/.stfolder 2>&1 | head -3\necho \"--- stignore claude-config: игнорит ли scripts/_probe ---\"\ngrep -nE \"_probe|scripts|^\\*|\\.py\" /c/Users/dev/.claude/.stignore 2>/dev/null | head -12", "description": "Check clau

---

> `Bash` -- {"command": "grep -nE \"^!?/scripts\" /c/Users/dev/.claude/.stignore | head -20", "description": "Resolve scripts sync rules order"}

---

**Claude:**

Рельса пробы доказана: `.stignore`白listит `/scripts/**/*.py`. Закрываю ON AIR.

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close --zone vault-imports/brain-graph 2>&1 | tail -4\npython ~/.claude/scripts/onair.py list 2>&1 | head -6", "description": "Close ON AIR declaration"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close --help 2>&1 | head -12", "description": "Onair close usage"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close 2026-09-16T210854Z-HUB-01-f0316b45-vault-imports-brain-graph 2>&1 | tail -3\npython ~/.claude/scripts/onair.py list 2>&1 | head -5", "description": "Close my declaration by id"}

---

**Claude:**

🕐 **среда, ночь, 23:26, 16 сентября 2026**

## T08 закрыт: смержено и включено дефолтом

Первая правка программы, прошедшая порог. Шаги 3, 6 и 7 мержились выключенными — эта включена.

---

## Две таблицы линейки

Замороженный gold-2026-09-16, 184 вопроса, e5 + mmarco-mMiniLMv2, **nDCG@12**:

| класс | режим | ДО | ПОСЛЕ | дельта |
|---|---|---|---|---|
| title | vector | 0.921 | **0.927** | +0.006 |
| title | graph | 0.921 | **0.927** | +0.006 |
| body | vector | 0.611 | **0.640** | +0.029 |
| body | graph | 0.600 | **0.623** | +0.023 |
| bridge | vector | 0.160 | **0.223** | +0.063 |
| bridge | graph | 0.176 | **0.279** | **+0.103** |
| temporal | vector | 0.638 | 0.638 | +0.000 |
| temporal | graph | 0.638 | 0.638 | +0.000 |

**Recall@12:**

| класс | ДО | ПОСЛЕ | порог программы |
|---|---|---|---|
| title | 0.933 | **0.950** | ≥0.90 ✅ |
| body | 0.767 | **0.850** | ≥0.80 ✅ **впервые взят** |
| bridge | 0.251 | **0.451** | ≥0.70 ❌ ещё далеко |
| temporal | 1.000 | 1.000 | ≥0.60 ✅ |

Порог шага был «bridge ↑ ≥ 0.03 при body ↓ ≤ 0.01». Получилось bridge +0.103, а body не упал, а **вырос**. Ни один класс не просел.

---

## Гейт: затягивать оказалось нечего — он нулевой

Сид велел затянуть `looks_like_entity`. Замер на замороженных скорах сказал другое.

Гейт срабатывает **13 раз из 184**, и все 13 — на классе title, где 1-hop граф не меняет вообще ничего: dNDCG = 0.000 на всех 60 title-вопросах. То есть гейт выключает полосу ровно там, где она и так нейтральна. Его вклад в качество — **+0.000**.

А там, где граф реально вредит — 20 вопросов, из них body суммарно на −0.676 nDCG — гейт не сработал **ни разу**. Recall гейта 0/20, precision по спасённому ущербу 0/13.

Оценка 26.06 («1👍 / 5👎 на entity») делалась на шести ручных вопросах, не на замороженном наборе. Гейт я оставил на 1-hop как есть — он безвреден. Полоса PPR его **не использует**: с гейтом title +0.000, без него +0.006.

---

## Почему PPR встал ранжировщиком, а не источником кандидатов

Перед стройкой я померил, где именно теряются bridge-ответы. Из 307 gold-целей:

- **39%** уже лежат в dense-кандидатах
- **58%** добавляет 1-hop граф
- **3%** не находятся нигде

97% правильных ответов **уже в кандидатах**, а Recall@12 при этом 0.225. Значит теряет их не ретривер, а **реранкер**: cross-encoder судит «похож ли текст соседа на запрос», а связь bridge-класса структурная.

Наращивать hop'ы и GMAX было бы лечением симптома. Структуре нужен голос в **порядке**, а не в наборе.

Слияние — RRF поверх порядка реранкера, той же функцией `brain_lex.rrf_fuse`, что шаг 3 дал BM25. Первые 5 позиций реранкера защищены: голову cross-encoder знает лучше графа. Без защиты title падает на −0.076, с защитой растёт на +0.006.

---

## Решения, которые принял сам

- **numpy, не NetworkX.** 15 строк power iteration по CSR против новой зависимости в always-on рельсе recall.
- **Дисковый кэш графа построил и удалил.** Замер: сборка с нуля 0.50 с, подъём из pickle 0.53 с. Не окупался, но тащил файл, протухание и грабли «один кэш на две меты» (e5 и OpenAI).
- **Полоса работает и без `--graph`.** Линейка измерила обе воронки, обе в плюсе. Привязать полосу к флагу значило бы отдать плюс только тем, кто про флаг помнит.
- **Копию 1-hop из линейки удалил.** Она мерила свой пересказ конвейера, а не конвейер. Контрольный прогон после рефакторинга воспроизвёл baseline шага 6 до третьего знака.

---

## Как проверял, раз вывод выгодный

**Плато, а не иголка.** По всей сетке head 4…10, topm 5…60, alpha 0.15…0.85, вес 0.35…1.0 эффект положительный везде.

**Сплит-валидация.** Параметры выбирались на нечётных вопросах — вышли те же самые (alpha 0.85, topm 10, head 5), и на отложенных чётных дали bridge +0.111.

**Три захода линейки.** ДО → ПОСЛЕ → перепрогон на финальном коде: числа совпали.

**Откат доказан, а не заявлен.** `BRAIN_GRAPH_PPR=0` вернул baseline 0.921 / 0.600 / 0.176 / 0.638 точно.

**Тест краснел.** `_test_brain_graph.py`, 24 проверки, показан красным на трёх мутантах: `head` (3 провала), `flag` (1), `empty` (1). Девять соседних регрессов зелёные: brain_ask 61 PASS, brain_recall 18 ok, brain_lex, brain_emb_backends, chunk_heading_path, ab_recall, brain_rerankers, brain_vec_store, index_freshness.

---

## Честная граница

Класс bridge в gold построен **из исходящих wikilinks** заметки. Метод, ходящий по тем же ссылкам, там заведомо в выигрыше — это замер «умеет ли конвейер ходить по связям», а не «стал ли он умнее вообще». Ценность правки держится на body (+0.023…+0.029) и на том, что title и temporal не пострадали.

**Не проверено:** BGE-M3 (шаг 4) и другие реранкеры (шаг 5) — мерил только на паре e5 + mmarco. Temporal — 4 вопроса, улика пустая. На других узлах полоса не гонялась: посылка `brain-graph-ppr-20260916` ушла на NODE-0X и NODE-0X, их роботы прогонят пробу сами.

**Цена:** сборка графа 0.50 с один раз за процесс, PPR 2.6 мс на запрос. Граф волта — 7842 узла, 18308 рёбер, 78% файлов со ссылками.

---

## Два урока в журнал

**`probe-run-by-wrong-python`** — verify-шаг посылки зовётся как `python3`, а `python3` на хабе это pythoncore-3.14 без numpy. Проба падала бы не потому, что полоса сломана, и узел повис бы ложным отставшим. Вылечено re-exec на `PYTHON_EXE` из machine.env.

**`knob-cannot-turn-itself-off`** — `expand_1hop` проверял предел ПОСЛЕ добавления опоры, поэтому `ghops=0` давал одну опору вместо нуля. Ручка не умела выключать саму себя. Поймал собственный регресс, чинено проверкой до добавления.

---

## Файлы

- [brain_graph.py](D:/Vault/_imports/brain_graph.py) — новый модуль: граф волта, 1-hop, PPR, слияние
- [_test_brain_graph.py](D:/Vault/_imports/_test_brain_graph.py) — регресс, 24 проверки, kill-list в шапке
- [brain_ask.py](D:/Vault/_imports/brain_ask.py) — 1-hop переехал в модуль, PPR в `_best_per_file`
- [brain_gold_eval.py](D:/Vault/_imports/brain_gold_eval.py) — копия 1-hop удалена, PPR в обоих путях
- [_probe_brain_graph_lane.py](C:/Users/dev/.claude/scripts/_probe_brain_graph_lane.py) — read-only проба для флота

Доклады разосланы: карточка `task-2026-09-16-sm-T08` → done, строка в программе, ячейка G10 в Google-таблице, одна строка в TG-03 (`#e1d46efc`). ON AIR закрыт.

**Преемник поднят:** T07 оказался done, поэтому по условию сида запустил T09 — сессия «Битемпоральные рёбра в SQLite» работает.

---

## Вердикт о скилле и о собственной инструкции (§9.3-бис)

**Скилл:** ✅ не надо — ни одного скилла в этом заходе не применял, работал приборами программы напрямую.

**Собственная инструкция (сид):** 📝 обновлю не сейчас. Блок «ПРЕМИССА — ПРОВЕРЯЕМАЯ» отработал именно так, как задуман: приказ «затянуть гейт» оказался claim'ом, замер его опроверг, и заход пошёл по факту, а не по букве. Менять нечего. Единственное, что стоило бы добавить в шаблон сидов программы — строку «дорогой прогон делай один раз и сохраняй ПОЛНЫЕ порядки, сетку параметров перебирай офлайн»: это сэкономило здесь примерно час GPU. Но это оптимизация одного класса задач, а не дефект инструкции — вносить в общий шаблон по правилу третьей поломки рано, первый случай записан.

🧒 **Простыми словами:** твой второй мозг искал ответы только по смыслу слов. Я проверил и увидел смешную вещь: правильные заметки он **уже находил** — в 97 случаях из 100 они лежали в его корзинке, — но потом сам же выкидывал их из ответа, потому что судил «похоже ли написано», а связь между заметками не в словах, а в ссылках. Теперь ссылки получили право голоса: первые пять ответов трогать нельзя (тут он и так умный), а дальше заметки-соседи поднимаются вверх. Поиск по связям стал лучше почти в два раза, а остальное не испортилось — ни одна оценка не упала. И есть рубильник, чтобы выключить одним словом, если что-то пойдёт не так.
