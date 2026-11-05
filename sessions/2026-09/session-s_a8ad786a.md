---
session: s_a8ad786a
date: 2026-09-30
words: 31922
turns: 51
tools: "Bash, Edit, Grep, Monitor, Read, Skill, ToolSearch, Write, mcp__ccd_session_mgmt__get_session, mcp__ccd_session_mgmt__set_session_title, mcp__telegram__get_history"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a8ad786a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: bus:sm:auto-hub-260916-sm-T09.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
# auto-hub-260916-sm-T09 — Шаг 9: битемпоральные рёбра/факты в SQLite (valid_from/valid_to/observed_at/source_kind), close-don't-delete, human-edit-wins; temporal-gold с 4 до ≥ 30

Ты — сессия Claude Code на хабе HUB-01, автор `HUB-01·claude`, узел хаб. Первым делом `set_session_title "AUTO-hub-sm-T09 bitemporal-edges"`. Карточка задачи: `D:\Vault\Vault-Knowledge\10-Tasks\task-2026-09-16-sm-T09-bitemporal-edges.md` — открой, переведи state → wip, touched_at → сегодня; закрывай её же по факту.

📛 ON AIR: первым делом объяви себя — `python ~/.claude/scripts/onair.py check --zone <зона>`, чисто → `onair.py declare --zone <зона> --mode exclusive|collab --title "<суть>" --ttl-hours <N>`; в конце `onair close`. Зона занята соседом — НЕ править параллельно: читай его табличку, договаривайся в 03 или бери другой кусок.
👤 КОНСОЛИДАТОР: если по этой теме поднято больше ОДНОГО исполнителя — консолидатор <ИМЯ_СЕССИИ_ИЛИ_УЗЛА>. Он сводит результаты и объявляет «готово»; остальные сдают ему кусок и НЕ пишут свой финальный вердикт. Исполнитель один — эта строка не действует.
🔁 RECALL ЛЕТЯЩЕЙ РАБОТЫ (до постройки, не после): `onair.py list` (кто сейчас в воздухе) + свежие панели `~/.claude/scripts/cc-review/bridge-state/usage.jsonl` (вопрос уже гонялся соседом → читай леджер, добавляй ДЕЛЬТУ, панель заново не гоняй — STOP-DUP) + журнал поломок через `python ~/.claude/scripts/breakage.py find "<текст>"` (этот класс уже разбирали?). Нашёл чужой готовый артефакт — ПЕРЕИСПОЛЬЗУЙ, свой не рожай.
🪫 БАК И СМЕРТЬ ПРИ РОЖДЕНИИ: пачку fireAt-сидов разноси с учётом бака подписки (одна ночь + шаг 15 мин = 4 из 5 умирают об «session limit»). Умер об лимит при рождении — это обязано быть ЗАМЕЧЕНО: следующая сессия и `/retro` проверяют «сид родил ретро?» — одобренная задача без следа исполнения считается НЕ сделанной, а не идущей.
🔍 УЛИКА ПРИ СТАТУС-CLAIM: любое ✅ про ФАЙЛ, КОД или ЧУЖУЮ ПРОВЕРКУ ставится ТОЛЬКО с уликой в том же заходе: `ls`/`cat`/цитата строки/exit-код. Не читал своими глазами — пиши 🤔 и говори прямо, что не проверено; пусто ИЗ ОДНОГО места ≠ «нет на диске» (§5.4) — назови, ГДЕ искал. Наружный док/README/INSTALL/отчёт перед выдачей прогони: `python ~/.claude/scripts/status_claim_lint.py <файл>`.
🤝 ТЫ АВТОНОМНЫЙ КОФАУНДЕР, НЕ ИСПОЛНИТЕЛЬ С ВОПРОСАМИ (приказ оператора 13.09.2026): этот заход идёт БЕЗ человека, поэтому развилку, неполное ТЗ и «а как он хотел» решаешь ТЫ и доводишь до результата, а решение кладёшь в отчёт постфактум («решил X, потому что Y, сделал Z»). Заход, кончившийся «жду ответа оператора» на ОБРАТИМОМ, считается НЕ сделанным. оператору остаётся ЗАКРЫТЫЙ список: деньги · необратимое удаление · юридическая подпись · секреты 3-м лицам · масс-рассылка; упёрся в него — доведи до последнего клика, `approval.py ask` в 02-POLICE и БЕРИ СЛЕДУЮЩУЮ работу, не жди в тишине (кап 2 аска на заход). Новые пиры — работаешь сам (14.09 оператор вывел их из списка). «Нужны руки оператора» — ПОСЛЕДНЕЕ, что говоришь: сперва ДВЕ честные разные попытки обхода (другой инструмент · флаг · рельса или узел · аккаунт или браузер · скрипт вместо GUI), и в отчёте названо, что пробовал. «Нельзя / нет доступа» — claim: сперва `--help`, конфиг, доки, лог, и только потом слова «я не нашёл, как». Развёрнутая версия для рутин: `~/.claude/scripts/routine-autonomy-block.md`.
⏳ ПРЕМИССА — ПРОВЕРЯЕМАЯ, НЕ УТВЕРЖДЕНИЕ: первым шагом замерь по ground truth (живая система / лог / канал / файл на диске — не память и не текст этого сида) ту дыру и тот статус, про которые сид говорит. Сид, ссылающийся на ID или работу С СОСТОЯНИЕМ (заказ, задача, раздача, публикация, PR), ОБЯЗАН прочитать её статус и при «уже закрыто / уже сделано» ВЫЙТИ РАНО с докладом «чем и когда закрыто», а не исполнять «как написано». Не подтвердилась — скажи «премисса протухла», чини то, что реально сломано, и закрой карточку по доказательству. Приказ в сиде — такой же claim, как вывод.

⛳ ВХОД: ты на хабе. Премисса: T07 и T08 обе done (индекс и граф стабильны). ON AIR exclusive на brain_ask.py + turnstate.db. Prior art: memory_epistemic.py уже закрывает записи полями — читай, как он пишет status/valid_to, и бери те же имена колонок, не свои.
ПРЕЕМНИК: T10.

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

🕐 **среда, ночь, 23:11, 16 сентября 2026**

Начинаю T09. Первым ходом — заголовок сессии, карточка, ON AIR, premise-check.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `Bash` -- {"command": "cat \"D:/Vault/Vault-Knowledge/10-Tasks/task-2026-09-16-sm-T09-bitemporal-edges.md\" 2>&1 | head -80", "description": "Read T09 task card"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "AUTO-hub-sm-T09 bitemporal-edges"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python onair.py check --zone vault-imports/brain-temporal 2>&1 | head -20; echo \"=== LIST ===\"; python onair.py list 2>&1 | head -40", "description": "ON AIR check + list"}

---

> `Bash` -- {"command": "python onair.py zones 2>&1 | head -40", "description": "List onair zones"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && for f in task-2026-09-16-sm-T0*.md task-2026-09-16-sm-T1*.md; do echo \"--- $f\"; grep -m1 -E '^state:' \"$f\"; grep -m1 -E '^touched_at:' \"$f\"; done 2>&1 | head -60", "description": "Check states of program task cards"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python onair.py declare --zone vault-imports/brain-temporal --mode exclusive --title \"T09: битемпоральные рёбра/факты в turnstate.db + temporal-gold >=30 + recall-фильтр valid_to за флагом\" --ttl-hours 6 2>&1 | head -20", "description": "Declare ON

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && python breakage.py find \"temporal\" 2>&1 | head -30; echo \"=== valid_to ===\"; python breakage.py find \"valid_to\" 2>&1 | head -20", "description": "Breakage journal search"}

---

> `Bash` -- {"command": "ls -la memory_epistemic.py 2>&1; echo \"=== FIELDS ===\"; grep -nE \"valid_from|valid_to|observed_at|source_kind|superseded_by|refuted_on|refuted_by|status\" memory_epistemic.py 2>&1 | head -50", "description": "Read memory_epistemic prior art fields"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python -c \"\nimport sqlite3\ndb=sqlite3.connect('turnstate/turnstate.db')\nrows=db.execute(\\\"select name,type from sqlite_master where type in ('table','view') order by name\\\").fetchall()\nprint(len(rows),'objects')\nfor n,t in rows: print(t,n)\n\" 2>&1 |

---

> `Bash` -- {"command": "wc -l brain_ask.py && grep -nE \"^def |^class |os.environ.get|getenv\" brain_ask.py | head -80", "description": "brain_ask.py structure and env flags"}

---

> `Bash` -- {"command": "sed -n 214,372p brain_ask.py", "description": "Read brain_ask core retrieval"}

---

> `Bash` -- {"command": "ls -la brain_*.py 2>&1; echo \"=== main graph/keep usage ===\"; grep -nE \"keep|brain_graph|ppr|GHOPS|graph\" brain_ask.py | sed -n 1,60p", "description": "List brain modules, find keep/graph in main"}

---

> `Bash` -- {"command": "sed -n 372,452p brain_ask.py", "description": "Read main flags and _keep"}

---

> `Bash` -- {"command": "grep -nE \"^def |^class |^[A-Z_]+ =|sqlite|turnstate|enabled\\(\\)\" brain_graph.py | head -50", "description": "brain_graph structure"}

---

> `Bash` -- {"command": "grep -c . eval/gold-2026-09-16.jsonl; echo \"=== temporal qs ===\"; grep '\"cls\": *\"temporal\"' eval/gold-2026-09-16.jsonl 2>/dev/null | head -5; echo \"=== first line ===\"; head -1 eval/gold-2026-09-16.jsonl", "description": "Inspect gold file format"}

---

> `Bash` -- {"command": "grep -nE \"temporal|superseded|refuted\" brain_gold_eval.py | head -40", "description": "How gold builder makes temporal class"}

---

> `Bash` -- {"command": "sed -n 100,200p brain_gold_eval.py", "description": "Read gold builder"}

---

> `Bash` -- {"command": "grep -nE \"^CURATED|CURATED =\" -A8 brain_gold_eval.py | head -20; echo \"=== run/rest of eval invocation ===\"; sed -n 200,260p brain_gold_eval.py", "description": "CURATED folders + runner body"}

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -40\nimport re, pickle, pathlib, collections\nMETA = pathlib.Path('_brain_e5_meta.pkl')\nprint('meta exists', META.exists())\nimport glob\nprint([p for p in glob.glob('_brain*')][:20])\nPY", "description": "Locate index meta files"}

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -50\nimport pickle, pathlib, collections, re\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\nprint('chunks', len(meta))\nstems = {pathlib.Path(m['path']).stem.lower() for m in meta}\nprint('unique files', len(stems))\nfolders = collecti

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -50\nimport pickle, pathlib, collections\nBS = chr(92)\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\nprint('chunks', len(meta))\nstems = {pathlib.Path(m['path']).stem.lower() for m in meta}\nprint('unique files', len(stems))\nfolders 

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && ls -d 01-Rules 02-Protocols 2>&1; echo \"=== counts of temporal fields across vault ===\"; grep -rlE \"^superseded_by: *[^ ]\" --include=*.md . 2>/dev/null | wc -l; echo \"-- refuted_by:\"; grep -rlE \"^refuted_by: *[^ ]\" --include=*.md . 2>/dev/null |

---

> `Grep` -- {"pattern": "^superseded_by: *\\S", "path": "D:\\Vault\\Vault-Knowledge", "glob": "*.md", "output_mode": "count", "head_limit": 0}

---

> `Grep` -- {"pattern": "^(refuted_by|valid_to): *\\S", "path": "D:\\Vault\\Vault-Knowledge", "glob": "*.md", "output_mode": "files_with_matches", "head_limit": 0}

---

> `Bash` -- {"command": "ls -d /e/Obsidian/Vault-Knowledge/0*/ /e/Obsidian/Vault-Knowledge/1*/ /e/Obsidian/Vault-Knowledge/9*/ 2>&1; echo \"=== memory dir ===\"; ls /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/*.md | wc -l", "description": "Vault folders + memory file count"}

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge/01-Rules/ | head; echo \"count:\"; ls /e/Obsidian/Vault-Knowledge/01-Rules/*.md 2>/dev/null | wc -l; echo \"=== 02-Protocols ===\"; ls /e/Obsidian/Vault-Knowledge/02-Protocols/*.md 2>/dev/null | wc -l", "description": "Check 01-Rules content"}

---

> `Bash` -- {"command": "grep -lE \"^(status|valid_to|superseded_by|refuted_by): *\\S\" /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/*.md 2>/dev/null | wc -l; echo \"-- with superseded_by nonempty:\"; grep -lE \"^superseded_by: *\\S\" /c/Users/dev/.claude/projects/P---WORKDIR-HUB

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -30\nimport pickle, pathlib, re, collections\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\npaths = {}\nfor m in meta:\n    p = pathlib.Path(m['path']); paths.setdefault(p.stem.lower(), str(p))\nWL = re.compile(r'\\[\\[([^\\]\\|#]+)')\

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -40\nimport pickle, pathlib, re, collections\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\npaths = {}\nfor m in meta:\n    p = pathlib.Path(m['path']); paths.setdefault(p.stem.lower(), str(p))\nWL = re.compile(r'\\[\\[([^\\]\\|#]+)')\

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -30\nimport pickle, pathlib, re, subprocess, json\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\nidx = {}\nfor m in meta:\n    p = pathlib.Path(m['path']); idx.setdefault(p.stem.lower(), str(p))\nWL = re.compile(r'\\[\\[([^\\]\\|#]+)')

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -35\nimport pickle, pathlib, re, os\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\nidx = {}\nfor m in meta:\n    p = pathlib.Path(m['path']); idx.setdefault(p.stem.lower(), str(p))\nWL = re.compile(r'\\[\\[([^\\]\\|#]+)')\nVAULT = r'E:

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -30\nimport pickle, pathlib, re, json, os\nmeta = pickle.loads(pathlib.Path('_brain_e5_meta.pkl').read_bytes())\nidx = {}\nfor m in meta:\n    p = pathlib.Path(m['path']); idx.setdefault(p.stem.lower(), str(p))\nclosed = []\nfor stem, p in idx.items():\n    t

---

> `Bash` -- {"command": "sed -n 505,545p brain_ask.py", "description": "Read brain_ask rerank block"}

---

> `Bash` -- {"command": "grep -E \"PYTHON_EXE\" /c/Users/dev/.claude/machine.env; echo \"=== eval CLI ===\"; sed -n '/^def cli\\|add_argument/,$p' brain_gold_eval.py | grep -E \"add_argument|def cli|def main\" | head -40", "description": "PYTHON_EXE + eval CLI args"}

---

> `Bash` -- {"command": "ls -la eval/ | head -30", "description": "List eval dir"}

---

> `Bash` -- {"command": "python - <<'PY' 2>&1 | tail -25\nimport sqlite3\ndb = sqlite3.connect('turnstate/turnstate.db')\ncols = [r[1] for r in db.execute(\"PRAGMA table_info(gold_eval)\")]\nprint(cols)\nrows = db.execute(\"select ts,cls,mode,n,recall12,mrr,ndcg12,embedder,reranker,index_chunks,scores_file from

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/preflight_shared_edit.py 2>&1; python /c/Users/dev/.claude/scripts/preflight_shared_edit.py --help 2>&1 | head -20", "description": "preflight tool help"}

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-Process python -ErrorAction SilentlyContinue | Select-Object Id,StartTime,CPU | Format-Table -AutoSize | Out-String -Width 120\" 2>&1 | head -20", "description": "Check running python processes"}

---

> `Bash` -- {"command": "grep -nE \"turnstate|_paths|VAULT|def db|sqlite3.connect|def enabled\" brain_lex.py | head -25; echo \"=== _paths ===\"; grep -nE \"^[A-Z_]+ *=\" _paths.py 2>/dev/null | head -20", "description": "Conventions: db path, enabled flag"}

---

> `Bash` -- {"command": "python -c \"\nimport sqlite3\ndb=sqlite3.connect('turnstate/turnstate.db')\nprint('journal_mode', db.execute('pragma journal_mode').fetchone())\nprint('size', __import__('os').path.getsize('turnstate/turnstate.db'))\n\"", "description": "Check turnstate journal mode"}

---

> `Bash` -- {"command": "grep -n \"VALID_STATUS\" /c/Users/dev/.claude/scripts/memory_epistemic.py | head -5; grep -n \"VALID_STATUS *=\" -A3 /c/Users/dev/.claude/scripts/memory_epistemic.py | head -8", "description": "memory_epistemic status vocabulary"}

---

**Claude:**

Премисса проверена — источник для temporal-gold из сида пуст. Пишу модуль.

---

> `Bash` -- {"command": "cat > brain_temporal.py <<'EOF'\n# -*- coding: utf-8 -*-\n\"\"\"Битемпоральный слой второй памяти: рёбра wikilink и факты заметок со ВРЕМЕНЕМ.\n\nШАГ 9 программы «второй мозг» (2026-09-16, хаб HUB-01). Единственное, что\nберётся у Graphiti, — МОДЕЛЬ ВРЕМЕНИ, не рантайм: у каждой 

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\brain_temporal.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Битемпоральный слой второй памяти: рёбра wikilink и факты заметок со ВРЕМЕНЕМ.\n\nШАГ 9 программы «второй мозг» (2026-09-16, хаб HUB-01). Единственное, что\nберётся у Graphiti, — МОДЕЛЬ ВРЕМЕ

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" brain_temporal.py selftest 2>&1 | tail -20", "description": "Run brain_temporal selftest"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def today():\n    return os.environ.get('BRAIN_TEMPORAL_TODAY') or datetime.date.today().isoformat()", "new_string": "def mutant():\n    \"\"\"МУТАНТ ДЛЯ КРАСНОГО ТЕСТА (правило «тест обязан краснеть на с

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    m = mode_ or mode()\n    if m == 'off' or not scored:\n        return scored", "new_string": "    m = mode_ or mode()\n    if m == 'off' or not scored or mutant() == 'order':\n        return scored"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def _conflict(con, kind, ref, human_value, disk_value, note):", "new_string": "def _close_edge(con, src, dst, rel, valid_from, day):\n    \"\"\"ЕДИНСТВЕННОЕ место, где ребро перестаёт быть живым (close-do

---

**Claude:**

Теперь провожу все закрытия через эти две двери:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        con.execute('UPDATE brain_edges SET valid_to=?, status=? WHERE src=? AND dst=? AND rel=? '\n                    'AND valid_from=?', (day, 'superseded', key[0], key[1], key[2], cur['valid_from']))\

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        elif (cur['value'] or '') != val:\n            con.execute('UPDATE brain_facts SET valid_to=?, status=? WHERE stem=? AND key=? '\n                        'AND valid_from=?', (day, 'superseded', ke

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        con.execute('UPDATE brain_facts SET valid_to=?, status=? WHERE stem=? AND key=? '\n                    'AND valid_from=?', (day, 'superseded', key[0], key[1], cur['valid_from']))\n        c['facts

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    for (vf,) in con.execute('SELECT valid_from FROM brain_facts WHERE stem=? AND key=? '\n                             'AND (valid_to IS NULL OR valid_to=\"\")', (stem, key)).fetchall():\n        if vf =

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "         source_kind TEXT NOT NULL DEFAULT 'machine',\n         evidence TEXT,\n         PRIMARY KEY(src, dst, rel, valid_from))\"\"\",", "new_string": "         source_kind TEXT NOT NULL DEFAULT 'machine

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "         source_kind TEXT NOT NULL DEFAULT 'machine',\n         evidence TEXT,\n         PRIMARY KEY(stem, key, valid_from))\"\"\",", "new_string": "         source_kind TEXT NOT NULL DEFAULT 'machine',\n

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def _live_edges(con):\n    out = {}\n    for src, dst, rel, vf, sk in con.execute(\n            'SELECT src,dst,rel,valid_from,source_kind FROM brain_edges '\n            'WHERE valid_to IS NULL OR valid_

---

> `Bash` -- {"command": "grep -n \"_close_edge(con\\|_close_fact(con\\|last_seen_at=? WHERE\" brain_temporal.py", "description": "Find call sites to update"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - <<'PY'\nimport io, re\np = 'brain_temporal.py'\ns = io.open(p, encoding='utf-8').read()\nsubs = [\n (\"\"\"            con.execute('UPDATE brain_edges SET last_seen_at=? WHERE src=? AND dst=? AND rel=? '

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "            con.execute('UPDATE brain_edges SET last_seen_at=? WHERE src=? AND dst=? AND rel=? '\n                        'AND valid_from=?', (now, key[0], key[1], key[2], cur['valid_from']))", "new_strin

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        _close_edge(con, key[0], key[1], key[2], cur['valid_from'], day)", "new_string": "        _close_edge(con, key[0], key[1], key[2], cur, day)"}

---

> `Edit` -- {"replace_all": true, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "_close_fact(con, key[0], key[1], cur['valid_from'], day)", "new_string": "_close_fact(con, key[0], key[1], cur, day)"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "            con.execute('UPDATE brain_facts SET last_seen_at=? WHERE stem=? AND key=? AND valid_from=?',\n                        (now, key[0], key[1], cur['valid_from']))", "new_string": "            con

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    for (vf,) in con.execute('SELECT valid_from FROM brain_facts WHERE stem=? AND key=? '\n                             'AND (valid_to IS NULL OR valid_to=\"\")', (stem, key)).fetchall():\n        # valid

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Регресс битемпорального слоя (шаг 9 программы «второй мозг», 2026-09-16).\n\nТесты гоняют ТОТ ЖЕ код, что работает в бою (brain_temporal.sync / set_fact /\napply_order / unclosed_versions), на

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -45; echo \"EXIT=$?\"", "description": "Run temporal regression test"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" -c \"\nimport sqlite3\nc=sqlite3.connect(':memory:')\nc.execute('create table t(k text, v text)')\nc.execute(\\\"insert into t values('status','superseded')\\\")\ntry:\n    print('DQS test:', c.execute('se

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\dbg_bt.py", "content": "# -*- coding: utf-8 -*-\nimport os, sys, tempfile, shutil\nfrom pathlib import Path\nsys.path.insert(0, r'D:\\Vault\\_imports')\ni

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/dbg_bt.py\" 2>&1 | tail -30", "description": "Debug sync behavior"}

---

**Claude:**

Тест поймал настоящий баг: в таблице есть колонки `status`/`value`/`valid_to`, поэтому SQL-литералы в двойных кавычках SQLite читает как ИМЕНА КОЛОНОК. Правлю все на одинарные:

---

> `Bash` -- {"command": "grep -n '\"' brain_temporal.py | grep -nE \"valid_to=\\\"\\\"|key=\\\"|rel IN|value IN|value<>\\\"\\\"|source_kind=\\\"|=\\\"human\\\"\" | head -30", "description": "Find double-quoted SQL literals"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\fix_quotes.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Одноразовый патч: SQL-литералы в двойных кавычках -> одинарные.\nПричина (замер 16.09, поймал _tes

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/fix_quotes.py\" 2>&1", "description": "Apply quote fix"}

---

**Claude:**

Патч сломал синтаксис (SQL-литералы попали внутрь одинарных python-строк). Чиню корректно:

---

> `Bash` -- {"command": "grep -n \"valid_to=''\\|key='status'\\|key='fm_valid_to'\\|value<>''\\|rel IN ('\\|source_kind='human'\" brain_temporal.py", "description": "Locate broken lines"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\fix_quotes2.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Починка после первого патча: SQL-литералы уехали внутрь ОДИНАРНЫХ python-строк.\nРешение без кавы

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/fix_quotes2.py\" 2>&1", "description": "Repair quotes properly"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" brain_temporal.py selftest 2>&1 | tail -4; echo \"--- test ---\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -30", "description": "Re-run selftest and regression test"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        chk('T1 sync: рёбра созданы', c1['edges_new'] >= 3, c1['edges_new'])", "new_string": "        # ровно два ребра: old-note -> side-note (wikilink в теле) и\n        # old-note -> new-note (re

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        hist = con.execute('SELECT value, valid_from, valid_to FROM brain_facts WHERE stem=\"new-note\" '\n                           'AND key=\"status\" ORDER BY valid_from').fetchall()", "new_stri

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        chk('T4 правка человека закрыла машинную строку, а не стёрла',\n            len(con.execute('SELECT 1 FROM brain_facts WHERE stem=\"side-note\" AND key=\"status\"'\n                         

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -12; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Re-run regression test"}

---

**Claude:**

Зелёный. Теперь красный тест на мутантах — доказательство, что тест не фальшивый:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== МУТАНТ delete (закрытие -> DELETE) ===\"\nBRAIN_TEMPORAL_MUTANT=delete \"$PY\" _test_brain_temporal.py 2>&1 | grep -E \"^FAIL|ИТОГ\"; echo \"EXIT=${PIPESTATUS[0]}\"\necho\necho \"=== МУТАНТ order (demot

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; time \"$PY\" brain_temporal.py sync 2>&1 | tail -5", "description": "First real sync into turnstate.db", "timeout": 600000}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" brain_temporal.py sync 2>&1 | tail -2; \"$PY\" brain_temporal.py status 2>&1 | tail -8", "description": "Idempotency + status"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" brain_temporal.py watch 2>&1 | tail -12; echo \"EXIT=${PIPESTATUS[0]}\"; echo; \"$PY\" brain_temporal.py gold 2>&1 | tail -3", "description": "Watchdog + build temporal gold"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - <<'PY' 2>&1 | head -40\nimport json, pathlib, collections\nrows=[json.loads(l) for l in pathlib.Path('eval/gold-temporal-2026-09-16.jsonl').read_text(encoding='utf-8').splitlines() if l.strip()]\nprint('

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/preflight_shared_edit.py brain_ask.py 2>&1 | head -25", "description": "Preflight before editing shared brain_ask.py"}

---

> `Bash` -- {"command": "ls -l --time-style=+%H:%M:%S brain_ask.py brain_rerankers.py brain_graph.py brain_gold_eval.py; sed -n 359,372p brain_ask.py", "description": "Check mtimes + view dedup function"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_ask.py", "old_string": "def dedup_best_per_file(scored, meta, topn=TOPN):\n    \"\"\"2-я ступень (фикс 04.08): дедуп по файлу ПОСЛЕ оценки — представителя файла выбирает\n    оценщик, а не косинус. `scored` = [(idx, score)], отсортир

---

> `Bash` -- {"command": "ls _test_brain*.py 2>&1; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; for t in _test_brain_recall.py _test_brain_ask.py; do [ -f \"$t\" ] && { echo \"=== $t\"; timeout 300 \"$PY\" \"$t\" 2>&1 | tail -6; echo \"exit=${PIPESTATUS[0]}\"; }; done", "description"

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; BRAIN_TEMPORAL=off timeout 1800 \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-09-16.jsonl --candidates eval/candidates-20260916-2200.jsonl 2>&1 | tail -30", "description": "Ruler BEFORE on frozen gold (te

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; export BRAIN_TEMPORAL=off; nohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-09-16.jsonl --freeze-candidates eval/candidates-t09-main.jsonl > /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB

---

> `Bash` -- {"command": "sleep 60; tail -5 /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_before_main.log", "description": "Check BEFORE run progress", "timeout": 120000}

---

> `ToolSearch` -- {"query": "select:Monitor", "max_results": 2}

---

> `Monitor` -- {"command": "tail -f \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_before_main.log\" | grep -E --line-buffered \"ЛИНЕЙКА|/184|Traceback|Error|RuntimeError|FAIL|scores-\"", "description": "BEFORE-прогон линейки на основном 

---

> `Bash` -- {"command": "grep -nE \"brain_|def main|ARTIFACTS|subprocess|run\\(\" /c/Users/dev/.claude/scripts/brain_gold_eval_nightly.py 2>&1 | head -30", "description": "Inspect nightly eval script"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/ | grep -iE \"housekeep|nightly\" | head -20", "description": "Find housekeeping scripts"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && cp task-2026-09-16-sm-T09-bitemporal-edges.md \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/T09-card.bak\" && sed -i 's/^state: open/state: wip/' task-2026-09-16-sm-T09-b

---

> `Bash` -- {"command": "sed -n '/ЛИНЕЙКА/,+30p' brain_gold_eval.py | head -45", "description": "See ruler report format"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && sed -n '/ЛИНЕЙКА/,+28p' brain_gold_eval.py | head -40", "description": "See ruler report format (correct cwd)"}

---

> `Bash` -- {"command": "until grep -q \"ЛИНЕЙКА второй памяти\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_before_main.log\" 2>/dev/null; do sleep 5; done; echo READY", "description": "Wait for BEFORE run to finish", "run_in_backg

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && grep -nE \"T0[5-9]|T1[0]|\\| *9 *\\||шаг 9\" task-2026-09-16-second-memory-quality-program.md | head -20", "description": "Program card plan table"}

---

> `Bash` -- {"command": "tail -22 \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_before_main.log\"", "description": "Check BEFORE run result"}

---

> `Bash` -- {"command": "head -c 700 eval/scores-20260916-2306.jsonl; echo; echo \"---keys---\"; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" -c \"\nimport json\nr=json.loads(open('eval/scores-20260916-2306.jsonl',encoding='utf-8').readline())\nprint(list(r.keys())); print(l

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" -c \"\nimport json\nr=json.loads(open('eval/scores-20260916-2306.jsonl',encoding='utf-8').readline())\nprint(list(r.keys())); print(list(r['res'].keys())); print(list(r['res'][

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "# ------------------------------------------------------------------ temporal gold", "new_string": "def version_dupes(scores_file, con=None, mode_key='vector', topn=12):\n    \"\"\"ВТОРОЙ критерий приёмки

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    ap.add_argument('cmd', choices=['sync', 'status', 'closed', 'set', 'watch', 'gold', 'selftest'])", "new_string": "    ap.add_argument('cmd', choices=['sync', 'status', 'closed', 'set', 'watch', 'gold'

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    if a.cmd == 'gold':", "new_string": "    if a.cmd == 'dupes':\n        if not a.scores:\n            print('dupes: нужен --scores <файл scores-*.jsonl>')\n            return 2\n        d, t, share, ex

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" brain_temporal.py selftest 2>&1 | tail -3 && \"$PY\" brain_temporal.py dupes --scores eval/scores-20260916-2306.jsonl 2>&1 | head -8", "description": "Test dupes metric on an old scores file"}

---

> `Bash` -- {"command": "tail -4 \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_before_main.log\"", "description": "BEFORE run progress"}

---

> `Bash` -- {"command": "until grep -q \"ЛИНЕЙКА второй памяти\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_before_main.log\" 2>/dev/null; do sleep 10; done; tail -18 \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB

---

**Claude:**

BEFORE снят. Запускаю AFTER (demote) по тем же замороженным кандидатам:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && export BRAIN_TEMPORAL=demote && nohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-09-16.jsonl --candidates eval/candidates-t09-main.jsonl > \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB

---

> `Bash` -- {"command": "until grep -qE \"ЛИНЕЙКА второй памяти|Traceback|RuntimeError\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/run_after_main.log\" 2>/dev/null; do sleep 10; done; tail -20 \"/c/Users/dev/AppData/Local/Temp/claud

---

> `Bash` -- {"command": "ls -l --time-style=+%H:%M:%S /e/Obsidian/_imports/_brain_e5.npy /e/Obsidian/_imports/_brain_e5_meta.pkl /e/Obsidian/_imports/_brain_e5_done.txt 2>&1; echo \"--- done.txt tail ---\"; tail -3 /e/Obsidian/_imports/_brain_e5_done.txt 2>&1; echo \"--- кто крутит: свежие процессы ---\"; power

---

**Claude:**

Индекс перестроился (24257 → 24261) прямо во время прогона. Снимаю СВОЙ снимок индекса, чтобы обе таблицы стояли на одном:

---

> `Bash` -- {"command": "cp _brain_e5.npy eval/snap-t09.npy && cp _brain_e5_meta.pkl eval/snap-t09_meta.pkl && ls -l --time-style=+%H:%M:%S eval/snap-t09*; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" -c \"\nimport pickle,numpy as np\nm=pickle.loads(open('eval/snap-t09_meta.

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nexport BRAIN_TEMPORAL=off\nnohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-

---

> `Bash` -- {"command": "until grep -qE \"ЛИНЕЙКА второй памяти|Traceback|RuntimeError\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/b2_main_off.log\" 2>/dev/null; do sleep 10; done; grep -vE \"Loading weights|it/s\" \"/c/Users/dev/Ap

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nexport BRAIN_TEMPORAL=demote\nnohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-20

---

> `Bash` -- {"command": "until grep -qE \"ЛИНЕЙКА второй памяти|Traceback|RuntimeError\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/b2_main_demote.log\" 2>/dev/null; do sleep 10; done; grep -vE \"Loading weights|it/s\" \"/c/Users/dev

---

**Claude:**

Числа AFTER подозрительно совпали с чужим replay-прогоном 23:06. Проверяю, не виноват ли сам режим переигрывания: гоняю off+replay и demote+fresh:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=off nohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-09-16.js

---

> `Bash` -- {"command": "until grep -qE \"ЛИНЕЙКА второй памяти|Traceback|RuntimeError|no-persist\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/b3_main_off_replay.log\" 2>/dev/null; do sleep 10; done; grep -vE \"Loading weights|it/s|/18

---

> `Bash` -- {"command": "sed -n '/def _load_frozen/,/^def run/p' brain_gold_eval.py | head -60", "description": "Read replay implementation"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=demote nohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-09-16

---

> `Bash` -- {"command": "until grep -qE \"ЛИНЕЙКА второй памяти|Traceback|RuntimeError\" \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/b4_main_demote_fresh.log\" 2>/dev/null; do sleep 10; done; grep -vE \"Loading weights|it/s|/184\" \"/c/

---

**Claude:**

Чистое сравнение fresh↔fresh получено. Теперь линейка на НОВОМ temporal-gold (53 вопроса), два прогона:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=off \"$PY\" brain_gold_eval.py --run --gold eval/gold-temporal-2026-09-16

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=demote \"$PY\" brain_gold_eval.py --run --gold eval/gold-temporal-2026-09

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"### MAIN gold, ДО (off, fresh) ###\"; \"$PY\" brain_temporal.py dupes --scores eval/scores-20260916-2342.jsonl 2>&1 | head -4\necho \"### MAIN gold, ПОСЛЕ (demote, fresh) ###\"; \"$PY\" brain_temporal.py du

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - <<'PY'\nimport json, pathlib\nclosed = set(open('eval/_closed.txt').read().split()) if pathlib.Path('eval/_closed.txt').exists() else None\nimport subprocess, sys\nsys.path.insert(0,'.')\nimport brain_te

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && for f in 02-Decisions/decision-config-portability-chezmoi-rejected.md 02-Decisions/decision-unified-multi-machine-platform.md 02-Decisions/decision-crm-cockpit-shrink-memo.md 02-Decisions/decision-crm-keep-cc-drop-decide.md; do echo \"=== $f\"; sed -n '

---

**Claude:**

Проверка premise окупилась: `supersedes` у НОВОЙ заметки часто указывает на ПУНКТ старой, а не на всю заметку — закрывать такие нельзя. Переделываю на строгий сигнал:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def version_families(con=None):\n    \"\"\"Семьи версий по живым рёбрам супернаследования: {новая: [старые, ...]}.\"\"\"\n    own = con is None\n    con = con or db(readonly=True)\n    fam = {}\n    try:\

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - <<'PY'\nimport sys; sys.path.insert(0,'.')\nimport brain_temporal as bt\ncon = bt.db(readonly=True)\ns = bt.version_families(con=con, strict=True); w = bt.version_families(con=con, strict=False)\nps = {(

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" - <<'PY'\nimport sys; sys.path.insert(0, r'D:\\Vault\\_imports')\nimport brain_temporal as bt\ncon = bt.db(readonly=True)\ns = bt.version_families(con=con, strict=True); w =

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/workspace_write_lease.py status 2>&1 | head -25", "description": "Check workspace lease status"}

---

**Claude:**

T05 (сессия 2ec4a020) взяла lease на `eval/` — мои записи туда ждут. Пока делаю всё, что вне неё:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\strict_check.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Сколько пар даёт СТРОГИЙ сигнал (superseded_by/refuted_by у старой заметки) против\nширокого (+ 

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/strict_check.py\" 2>&1 | head -30", "description": "Strict vs wide family counts"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    Пары `~timestamp` (копии конфликта синка) не версии и выбрасываются. Стемы в\n    списке gold уникальны — грабля nDCG>1 на дублях basename (журнал 16.09).\"\"\"\n    files = indexed_files(meta_path)\n

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def build_temporal_gold(meta_path=None, con=None, vault=None):", "new_string": "def build_temporal_gold(meta_path=None, con=None, vault=None, strict=True):"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "                rows.append({'cls': 'temporal', 'kind': kind, 'query': q, 'gold': [new],\n                             'lang': 'ru' if CYR_RX.search(q) else 'en', 'folder': folder,\n                      

---

**Claude:**

Теперь `watch` должен разделять красное и подсказки:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    if a.cmd == 'watch':\n        bad = unclosed_versions(con=db(a.db, readonly=True))\n        if not bad:\n            print('OK сторож версий: незакрытых старых версий нет')\n            return 0\n    

---

**Claude:**

Добавляю тест на это различение (сигнал старой заметки ≠ `supersedes` новой):

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        # ---- T8: gold строится из живых рёбер и не содержит дублей стемов", "new_string": "        # ---- T7b: `supersedes` у НОВОЙ заметки — НЕ закрытие старой (может быть про ПУНКТ)\n        not

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" _test_brain_temporal.py 2>&1 | tail -14", "description": "Re-run tests after strict change"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && for m in delete order; do echo \"=== мутант $m ===\"; BRAIN_TEMPORAL_MUTANT=$m \"$PY\" _test_brain_temporal.py 2>&1 | grep -cE \"^FAIL\"; done; echo \"--- lease status eval ---\"; \"$PY\" /c/Users/dev/.claude/

---

> `Bash` -- {"command": "date -u +\"UTC %H:%M:%S\"; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; echo \"### MAIN ДО (off) strict-families ###\" && \"$PY\" brain_temporal.py dupes --scores eval/scores-20260916-2342.jsonl 2>&1 | head -3 && echo \"### MAIN ПОСЛЕ (demote) strict ###\" &

---

**Claude:**

T05 держит `eval/` ещё ~26 минут. Строю строгий gold в scratchpad и снимаю числа без записи в `eval/`:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"; \"$PY\" brain_temporal.py gold --out \"$S/gold-temporal-strict.jsonl\" 2>&1 | tail -3; \

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=off \"$PY\" brain_gold_eval.py --run --gold \"$S/gold-temporal-strict.jso

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=demote \"$PY\" brain_gold_eval.py --run --gold \"$S/gold-temporal-strict.

---

**Claude:**

Все критерии приёмки закрыты. Обновляю карточку задачи:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/workspace_write_lease.py status 2>&1 | grep -ci \"imports.eval\"; date -u +\"UTC %H:%M\"; sed -n '28,50p' /e/Obsidian/Vault-Knowledge/10-Tasks/task-2026-09-16-sm-T09-bitempor

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\close_t09_card.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Закрыть карточку T09 по факту: state, чек-боксы приёмки, evidence, outcome.\nПишет ОДИН файл к

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/close_t09_card.py\" 2>&1 | tail -5", "description": "Apply card close"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/status_claim_lint.py /e/Obsidian/Vault-Knowledge/10-Tasks/task-2026-09-16-sm-T09-bitemporal-edges.md 2>&1 | tail -12; echo \"--- lease eval ---\"; \"$PY\" /c/Users/dev/.cla

---

**Claude:**

`eval/` освободился. Кладу строгий gold на место и снимаю обе таблицы с записью в SQLite:

---

> `Bash` -- {"command": "S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"; cp eval/gold-temporal-2026-09-16.jsonl \"$S/gold-temporal-wide-53q.jsonl.bak\" && cp \"$S/gold-temporal-strict.jsonl\" eval/gold-temporal-2026-09-16.jsonl && wc -

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\nBRAIN_TEMPORAL=off \"$PY\" brain_gold_eval.py --run --gold eval/gold-temporal-2026-09-16.jsonl --index-emb eval/snap-t09.npy --index-meta eval/snap-t09_meta.pkl 2>&1 | grep -E \"ЛИНЕЙКА|temporal |класс|scores\" | 

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\nBRAIN_TEMPORAL=demote \"$PY\" brain_gold_eval.py --run --gold eval/gold-temporal-2026-09-16.jsonl --index-emb eval/snap-t09.npy --index-meta eval/snap-t09_meta.pkl 2>&1 | grep -E \"ЛИНЕЙКА|temporal |класс|scores\"

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\show_rows.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Улика в SQLite: строки gold_eval, записанные прогонами T09 (только чтение).\"\"\"\nimport sqlite3\n

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/show_rows.py\" 2>&1 | grep -E \"temporal|всего|по temporal|title|body|bridge\" | head

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - <<'PY'\nimport sqlite3\ndb = sqlite3.connect(r'D:\\Vault\\_imports\\turnstate\\turnstate.db', timeout=30)\nfor r in db.execute(\"SELECT ts, gold_file, cls, mode, n, round(recall12,4), round(mrr,4), ro

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\add_sqlite_anchors.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Дописать в карточку T09 якоря улик в SQLite: какая строка gold_eval чей прогон.\"\"\"\nimp

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/add_sqlite_anchors.py\" 2>&1 | tail -2", "description": "Add SQLite evidence anchors 

---

**Claude:**

Теперь строка шага 9 в программной карточке:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\update_program_t09.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Строка шага 9 в программной карточке: состояние по факту прогонов T09.\"\"\"\nimport io\ni

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/update_program_t09.py\" 2>&1 | tail -3; grep -c \"МЕРЖ ЗА ФЛАГОМ, ДЕФОЛТ НЕ ПЕРЕКЛЮЧЁ

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/sheets.py --help 2>&1 | head -30", "description": "sheets.py help"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\sheet_t09.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Сначала ПРОЧИТАТЬ вкладку «План 2 нед», найти строку шага 9 и колонку «Состояние»,\nпотом записать.

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/sheet_t09.py\" 2>&1 | grep -v SyntaxWarning | head -18", "description": "Read the pla

---

> `Bash` -- {"command": "grep -nE \"^def [a-z_]+\\(\" /c/Users/dev/.claude/scripts/sheets.py | head -25", "description": "sheets.py public functions"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\sheet_t09.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Прочитать вкладку «План 2 нед» и показать строку шага 9 + шапку (перед записью).\"\"\"\nimport sys\

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/sheet_t09.py\" 2>&1 | grep -v \"SyntaxWarning\\|May26\" | head -16", "description": "

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\sheet_t09_write.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Записать «Состояние» шага 9 во вкладку «План 2 нед» (строка 11, колонка G).\nПеред записью св

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/sheet_t09_write.py\" 2>&1 | grep -v \"SyntaxWarning\\|May26\" | head -8", "descriptio

---

**Claude:**

Таблица обновлена. Строка в TG-03 и подъём преемника T10:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/bus_send.py NODE-0X \"REPORT: T09 битемпоральные рёбра · МЕРЖ ЗА ФЛАГОМ BRAIN_TEMPORAL=demote, дефолт off · Recall@12 на замороженном gold title 0.950 / body 0.850 / br

---

> `ToolSearch` -- {"query": "select:mcp__telegram__get_history", "max_results": 2}

---

> `mcp__telegram__get_history` -- {"chat_id": chat_REDACTED, "limit": 3}

---

**Claude:**

Отчёт в 03 доехал (id 1898817, полный текст; упал только бот-дубль по длине). Поднимаю преемника T10:

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/spawn_seeds/second-memory/ | head; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/spawn_seeds/second-memory/fire_seed.py /c/Users/dev/.claude/spawn_seeds/second-memory/auto-hub-260916-sm-T10.md --dry-r

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/spawn_seeds/second-memory/fire_seed.py /c/Users/dev/.claude/spawn_seeds/second-memory/auto-hub-260916-sm-T10.md 2>&1 | tail -5; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Fir

---

> `Bash` -- {"command": "grep -ln \"usage_log\\|_count(\\|counter\" brain_lex.py brain_graph.py brain_vec_store.py brain_rerankers.py brain_emb_backends.py 2>&1; echo \"--- shared helper? ---\"; ls /c/Users/dev/.claude/scripts/ | grep -iE \"^usage|counter\" | head", "description": "Do sibling brain modules ke

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/_counters/ | head -8; echo \"--- пример строки ---\"; f=$(ls /c/Users/dev/.claude/_counters/*.jsonl 2>/dev/null | head -1); echo \"$f\"; tail -2 \"$f\" 2>/dev/null; echo \"--- кто пишет ---\"; grep -rl \"_counters\" /c/Users/dev/.claude/scripts/*.py 2>/dev/

---

**Claude:**

Счётчик — дешёвый и по стандарту флота, добавляю:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def db(path=None, readonly=False):", "new_string": "COUNTER = Path(os.path.expanduser('~')) / '.claude' / '_counters' / 'brain_temporal.jsonl'\n\n\ndef count(event, outcome):\n    \"\"\"СЧЁТЧИК ИСПОЛЬЗОВА

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    con.commit()\n    if own:\n        con.close()\n    return c", "new_string": "    con.commit()\n    count('sync', 'files=%d edges_new=%d edges_closed=%d facts_new=%d facts_closed=%d human_kept=%d'\n  

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        live, dead = [], []\n        for i, sc in scored:\n            stem = Path(meta[i]['path']).stem.lower()\n            (dead if stem in cl else live).append((i, sc))\n        return live if m == 'd

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -3; \"$PY\" brain_temporal.py selftest 2>&1 | tail -2; \"$PY\" brain_temporal.py sync 2>&1 | tail -1; echo \"--- счётчик ---\"; tail -2 /c/Users/dev/.claude/_counters/

---

> `Skill` -- {"skill": "tt", "args": "brain_temporal.py + врезка в brain_ask.dedup_best_per_file (шаг T09): битемпоральные рёбра/факты, полоса demote за флагом, temporal-gold 41 вопрос"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\tt

# /tt — ворота качества сразу после сборки

> 🧒 **При докладе оператору:** заверши простым «Простыми словами» на его языке (его standing-правило [[eli5-always]]). Только в сообщении ЕМУ — не внутри артефактов.

Это **не ретро**. Ретро = упаковка всей сессии в конце. `/tt` = узкая проверка **одной вещи, которую мы только что собрали**, пока контекст горячий. Боль оператора (2026-06-25): «собрали, сказали „готово", пошли дальше — а оно сделано на 2/3». `/tt` ловит это ДО «готово».

**Когда:** сразу после сборки/правки **скилла · скрипта · рутины · хука · vault-пайплайна · заметки-механики** — всего, что должно ЧТО-ТО делать. Не для разговорных ответов и не для тривиальных правок текста.

**Граница vs соседи:** `/1` = жива ли СИСТЕМА после крэша; `/verify` (встроенный) = работает ли ПРИЛОЖЕНИЕ в браузере; `/tt` = работает ли **именно то, что мы только что собрали**.

---

## Шаг 0 — RECALL области (что вообще изменили)
Не по памяти — по фактам. Перечисли, что эта задача реально создала/тронула:
- свежие/изменённые файлы: `~/.claude/skills`, `~/.claude` (память/CLAUDE.md/хуки/scheduled-tasks), `$IMPORTS_ROOT`, волт-заметки;
- быстрый якорь: `python "$IMPORTS_ROOT/retro_inventory.py" 1` (тот же инвентарь, что у /retro) ИЛИ просто перечисли то, что правил в ЭТОЙ сессии.
- Возьми только то, что относится к ТЕКУЩЕЙ задаче (чужие fleet-правки игнор — это не наше, см. [[session-machine-tagging]]).
- **RECALL знаний по теме** (гейт, грабли 2026-07-04: чинили OAI-путь не глянув память — чуть не продублировали параллельную сессию): перед прогоном/фиксом подними, что УЖЕ известно — grep `memory\` + `/ask` (RAG) + греп волта по теме изменённого. Параллельная сессия могла уже сделать/задокументировать это ([[capture-rules-into-bible]] → RECALL-before-activity).
- ⭐ **А ЭТО УЖЕ НЕ ПОСТРОЕНО? — ПРИБОРОМ, ДО ПЕРВОЙ СТРОКИ КОДА** (замер 03.09.2026): память, RAG и волт свежий чужой скрипт НЕ видят — он лежит в `~/.claude/scripts` и всё. Сессия собрала `tg_voice_translate.py`, хотя рабочий `tg_translate_3chats.py` уже сутки лежал в той же папке, а рядом был и третий, `tg_translate.py`. RECALL был сделан «честно» и промахнулся, потому что не обошёл поверхность с кодом.
```
python ~/.claude/scripts/prior_art.py build <2-4 слова задачи>
```
Обходит scripts · _imports · skills · hooks · memory, печатает СКОЛЬКО поверхностей и файлов обошёл (пусто = замеренное пусто, а не «я посмотрел»). exit 0 = чисто, строй · **exit 3 = есть готовое: прочти найденное в разделах `scripts`/`_imports` ПРЕЖДЕ чем писать своё**. Русский запрос по английским именам ловится — внутри мост RU→EN. Контрфакт-проверка на реальном промахе: готовый движок вышел бы 5-м в топе своей поверхности. Канон: память `class-counted-by-name-never-reaches-three` (там же семьи дефектов и почему счёт по имени не работает).

- **⭐ Карта дверей [[three-tools-three-doors]]** (dev 09.08): АК-47 применяется на ОБОИХ концах — если спека НЕ прошла вопрос «слабейший починит молотком?» ДО стройки, это находка Шага 4, а не только брак приёмки. Чинится 3-й рецидив класса → сперва карта условий (`reglament-pyat-pochemu-koren-po-serii-sessiy`); очевидный фикс создаёт предъявленный вред → карточка противоречия (ТРИЗ), ⛔ до доказанной причины.

## Шаг 0-бис — СОБИРАЕШЬСЯ СКАЗАТЬ «НЕЛЬЗЯ»? СПРОСИ ИНСТРУМЕНТ

Срабатывает, если в вердикте вот-вот появится «невозможно», «нет такой ручки»,
«by design не поддерживается», «архитектурно нельзя» — или если ты готов
предложить оператору ручной шаг вместо автоматизации.

«Невозможно» — такой же claim, как вывод, и улика №1 не лог, а **собственный
интерфейс инструмента**. Пройди дешёвый круг снизу вверх, порядок не нарушать:

1. `<инструмент> --help` (и `-h`, и `help <подкоманда>`) — ПОЛНЫЙ список флагов,
   а не тот, что помнишь.
2. Подкоманды и их собственные `--help`.
3. Конфиг инструмента и переменные окружения.
4. Документация ТОЙ ЖЕ версии.
5. Только теперь логи, реверс бинаря, эксперимент.

Не прошёл круг — формулировка ровно одна: «я не нашёл, как это сделать».
Писать «этого не существует» без названного места поиска = вердикт максимум ⚠️.

⚠️ Ловушка, из-за которой правило родилось (10.09.2026, RC-факап): чем дороже
был путь к выводу, тем убедительнее он кажется. Сорок минут форензики по логам
приложения дали красивое доказанное «нельзя», а `claude --help` содержал
`--remote-control [name]` и закрывал задачу за пять секунд.
Дорогая улика НЕ отменяет обязанность пройти дешёвую.

Канон: `reglament-sprosi-instrument-pered-tem-kak-obyavit-nevozmozhnost`
+ память [[ask-the-tool-before-declaring-impossible]].

## Шаг 1 — ПРОГНАТЬ вживую (на реальных данных, не в теории)
Запусти собранное **по-настоящему** на настоящих данных оператора и покажи фактический вывод:
- скилл → выполни его процедуру руками здесь же;
- скрипт → запусти его (read-only/dry-run если есть побочки);
- рутина/хук → дёрни вручную или проверь, что он реально срабатывает (а не «должен бы»);
- заметка-правило → проверь, что ссылки/слаги резолвятся, frontmatter валиден.
«Теоретически работает» ≠ доказано. Нужен живой вывод.
- ⚠️ ТЕМ ЖЕ ИНТЕРПРЕТАТОРОМ/БИНАРЁМ, каким пойдёт у ПОТРЕБИТЕЛЯ (планировщик/рутина/другой узел), не «каким попало из PATH»: класс «PATH резолвит не тот питон/бинарь» кусался 11.08 (258 ложных падений регресса), 12.08 (две установки CC), 13.08 (gdocs_bridge: google-либы только у 3.12 из 5 питонов), 19.08 (brain_ask месяцами красный не тем питоном). Сомнение → напечатай `sys.executable`/`py -0p`/`which` и сверь с вызовом потребителя (Breakage-Journal, task-2026-08-13-python-path-class-repair).

## Шаг 2 — ПОЛОМАТЬ нарочно (negative + edge)
Попробуй сломать — реальные грабли этого дома:
- пустой / кривой ввод, отсутствует зависимость или ключ;
- грабли путей **C:/E:** ([[deterministic-script-gotchas]]) — ищет ли на правильном диске;
- машинно-специфичный хардкод: `grep -n "C:\\\\Users\\\\dev" <файл>` — путь с ЧУЖИМ юзером/машиной в общем движке обязан идти через `_paths.py`/machine.env (грабли 2026-07-04: хаб вшил `C:\Users\dev`, на ноуте путь мёртв → тихий fallback);
- v2.1 / 403 / устаревший конфиг — берётся ли факт из ЖИВОГО источника, не со стале-копии ([[recall-first-on-incident-and-live-source-truth]]);
- деградирует ли мягко (понятная ошибка), а не падает молча/тихо «делает вид»;
- ⭐⭐ **ЛЮБАЯ ПОЧИНКА, а не только сторож, закрывается ТЕСТОМ, ПОКАЗАННЫМ КРАСНЫМ** (CLAUDE.md §5.4 [[red-first-or-the-test-is-fake]]; дверь достроена 03.09.2026 — до этого шаг ниже требовал красноты только у СТОРОЖЕЙ/гейтов, а правило в каноне универсально, и обычный код закрывался «на глаз»). Порядок: сперва проверка на НЕчинёном коде и её падение ПОКАЗАНО (номер кейса + exit 1), потом починка, потом зелёный. Ломать — на КОПИИ в скретчпаде, живые файлы не портить; брейк-кейс остаётся в `_test_*.py`. Контр-кейс обязателен: хотя бы одна проверка, зелёная С САМОГО НАЧАЛА, иначе сетка красит всё подряд и ничего не доказывает. Нет предъявленного красного прогона → вердикт максимум ⚠️, «я посмотрел глазами» красным прогоном не является.
- ⭐⭐ **КРАСНОТУ ДОКАЗЫВАЕТ ПРИБОР, А НЕ ТВОЙ ГЛАЗОМЕР** (замер 04.09.2026, семья `neizvestnyy-flag-molcha-rabotaet` — 13 датированных случаев с 11.08): краснота трёх кейсов «проверялась» цепочкой `python test.py --flagA || python test.py --flagB`. Первый вызов шёл с ЧУЖИМ флагом, тест проглотил его молча (`"--red" in sys.argv` — членство, не разбор), отработал ЗЕЛЁНЫЙ набор, вернул 0, и `||` до правильного вызова не дошёл. Вывод «красный прогон показан» описывал команду, которая не запускалась.
  ```
  python ~/.claude/scripts/red_verify.py <test.py> --red-flag --against-broken-<чей>
  ```
  Три замера, ни один не пропускается: **канарейка строгости** (мусорный флаг обязан дать ≠0 — иначе скрипт глотает аргументы и его красный режим недоказуем в принципе), **зелёный 0**, **красный ≠0**. exit 0 доказано · 3 недоказуемо · 4 сам прибор не сошёлся на контрольном примере. ⛔ **Отказ запуститься (exit 2) краснотой НЕ является** — прибор ловил на этом сам себя на живом прогоне. Лечение недоказуемого теста — `_shared/strict_argv.py` (одна строка `strict(["--red"])` до любой работы; публичным артефактам — 6-строчная inline-копия, чтобы репо оставалось stdlib-only).
  ⭐ **У FAIL-CLOSED ГЕЙТА — МУТАЦИОННЫЙ ЗАМЕР, а не «тесты зелёные»** (замер 10.09.2026, процедура скилла `/red-first-review`): глуши по одной КАЖДУЮ его защиту и гоняй набор. Тест зелёный на мутанте = защиту можно удалить, и никто не заметит; именно она регрессирует молча. Живой результат на нашем leak-гейте касбука: **выжило 5 из 8** — сносились список имён людей, заимствованные паттерны, страховка по имени класса и САМ `control_sample`, все 14 тестов оставались зелёными. По ходу вскрылось, что заимствование паттернов у зрелого сканера было сломано молча (`getattr(rls,"PATTERNS",[])` при списке `FAIL` — тихий дефолт вернул пустоту, «мы берём зрелый сканер» было неправдой шесть дней). После кейсов-убийц: 8 из 8. Образец = `~/.claude/scripts/_mutate_casebook_gate.py`. ⚠️ Мутант обязан РЕАЛЬНО ломать защиту: `X = [] or [...]` возвращает НЕПУСТОЙ список, и два «выживших» оказались артефактом кривой мутации — проверяй саму мутацию, прежде чем верить её вердикту.
  ⚠️ И проверь, что краснеет КАЖДЫЙ кейс, а не файл целиком: красная ветка обязана ломать ОБЪЕКТ (подменить фильтр, движок, загрузчик), а не стирать провал теста (`if RED: missed = []`). Общий exit 1 от одного честного кейса маскирует соседей, которые не краснеют никогда — так 04.09 в одном файле два кейса из трёх молча проходили красный режим [[kill-list-makes-tests-checkable]].
- ⭐ артефакт = СТОРОЖ/гейт/пробник → ДВОЙНОЕ доказательство обязательно (dev «+++» 05.08, Библия `reglament-storozh-krasneet-na-slomannom-i-zhivyot-v-svoyom-kontekste`): (1) RED на заведомо сломанном показан, и брейк-кейс ОСТАЛСЯ в `--self-test`/`_test_*.py`; (2) прогон В КОНТЕКСТЕ проживания — из планировщика/cron (`schtasks /Run` / вызов crontab-строки) + чтение его ВЫХОДА (лог/артефакт), не из живой сессии. Замер 05.08: session_reaper 15 зелёных прогонов из Task Scheduler при живой аварии (MSIX-редирект). Нет любой половины → вердикт максимум ⚠️;
- ⭐ **чинил ВЫБОР/маршрутизацию (движок, вендор, модель, рельса, путь) → провокация обязана бить и ветку УМОЛЧАНИЯ, не только явную ошибку.** Вызови артефакт БЕЗ параметра выбора и докажи, что дефолт — тот, что заявлен (панель/None/явный отказ), а не тихий первый вендор. Замер 04→06.08: тест рельс secondop на 13 пунктов сторожил только явный `--engine`, ветка «движок не назван → молча codex» жила при зелёном тесте, нашёл оператор («почему только кодекс??»). У поломки выбора ВСЕГДА две двери: «назван неверно» и «не назван вообще» — закрыл одну, проверь вторую (паспорт `scripts/docs/secondop_rails.md`, проверки 8/8b/8c);
- ⭐ **РАЗНЫЕ РИТМЫ ПРОИЗВОДИТЕЛЯ И ПОТРЕБИТЕЛЯ → провоцируй ГЭП, а не «здесь и сейчас»** [[consumer-stamp-not-collector-stamp]]. Если сборщик бегает чаще потребителя (или наоборот), а потребитель читает «самый свежий» файл — подделай штамп/дату на длину пропуска и докажи, что окно РАСТЯНУЛОСЬ, а не осталось дефолтным; отдельно проверь недоставку (окно обязано копиться, а не пропадать) и потолок догона. Замер 30.08: сборщик ежедневный + судья раз в 2 суток = каждая вторая ночь клуба молча не доезжала до оператора, при этом ВСЕ приборы зелёные (каждый мерил свой шаг, а не сквозной путь данных); нашла панель Шага 2.5, живой прогон этот класс не ловит в принципе.
- ⭐ **ДЕТЕКТОР СУДИТ ПОДСТРОКУ, А НЕ СТРУКТУРУ** [[gate-must-judge-action-not-substring]] — прогон ОБЯЗАТЕЛЕН, если правка трогает гейт/сторож/фильтр/precheck/тест:
  `python3 ~/.claude/scripts/substr_lint.py <изменённые файлы>` (0 токенов, stdlib; exit 1 = находки).
  Шесть правил: R0 файл не разобрался → зелёный по нему ничего не значит (fail-closed) · R1 `"<короткое
  слово>" in <текст>` без границы · R2 regex-альтернатива голых слов без `\b` · R3 `grep` по выводу
  структурированного источника (JSON/YAML/py — слово может быть КЛЮЧОМ, а не значением) · R4 флагом
  `--md` — текстовое правило по заметке без отрезания YAML-шапки · **R5 вердикт по СЫРОЙ команде
  харнеса** (`tool_input["command"]` целиком уходит в матчер) → спроси `_shared/cmd_action.executed_text`:
  команда ЗАПУСКАЕТ сторожимое или лишь УПОМИНАЕТ его в данных. Находка = Шаг 4 (корень), либо
  ОСОЗНАННЫЙ глушитель `# substr-ok: <причина>` (голый маркер без причины не глушит).
  ⭐ **ПОПУЛЯЦИЯ, А НЕ АДРЕСАТ ИЗ РУК** (замер 03.09, разбор 22-го случая): у двери был ОДИН вызыватель —
  этот шаг по «изменённым файлам», счётчик показал 12 прогонов за 15 суток и только на хабе, поэтому
  10+ новых случаев родились в гейтах, которых никто в тот заход не правил. Правишь ЛЮБОЙ гейт/хук →
  добавь `python ~/.claude/scripts/substr_lint.py --roster` (живая перепись hook-файлов из settings.json
  + их `_shared`). Без рук это же сторожит ночная сетка: `_test_hook_roster_substr.py` (храповик —
  красный только на РОСТЕ долга, старый долг зафиксирован пер-узловой базовой линией).
  ⛔ **ПЕРЕПИСЬ — ТОЖЕ CLAIM, И ЕЁ ЧИСЛО НАДО ЧИТАТЬ** (замер 04.09, 23-й случай — дефект нашёлся
  В САМОЙ ДВЕРИ): `--roster` печатает «живых hook-файлов: N». Сверь N с `settings.json` глазами
  ОДИН раз. До 04.09 пути тянул regex по ВИДУ пути (требовал начала `C:\`, `$HOME/`, `%USERPROFILE%/`,
  `~/`), голый POSIX-абсолют `/Users/dev` не матчился: на NODE-0X из 39 команд попадали 3, перепись
  говорила «17» вместо 64, и вне неё были ровно рецидивисты класса — `blackbox_session_guard.py`
  (сломался дважды за утро 04.09), `maintenance_gate.py`, `false_no_guard.py`. Ночной храповик при
  этом был зелёным на базовой линии «1 находка» при реальном долге **43 находки в 16 гейтах (25%
  популяции)**. Урок общий: у сторожа с ПОПУЛЯЦИЕЙ доказывают не только вердикт, но и ПЕРЕПИСЬ —
  пустая или куцая популяция даёт зелёный, неотличимый от честного [[instrument-is-a-claim-too]].
  Замер 19.08: класс дал **5 датированных поломок за 8 дней** — 11.08 `"да"` внутри «со**зда**ём» увело
  приватную запись в `visibility: public` · 14.08 «является» внутри «появляется» · 18.08 «не **пост**авка»
  в ЗАГОЛОВКЕ сняла живой пост с публикации (SKIP не красный) · 19.08 `grep -E "dispatch|collect|deliver"`
  по JSON, где это КЛЮЧИ → 7 часовых тиков подряд будили LLM впустую. Шум двери замерен: **5.3% файлов
  на корпусе 1117** — это дверь, а не вечно красный сторож [[always-red-watchdog-teaches-ignoring-red]].
  ⛔ ГРАНИЦА (АК-47, не превращать каждый grep в парсер): структурный разбор обязателен там, где источник
  структурирован **И** вердикт что-то ГАСИТ (skip/block/publish/будить LLM); над плоским человеческим
  текстом, где ложный хит виден и дёшев, grep остаётся правильным решением. Тест: `_test_substr_lint.py`;
- ⭐ **СТАТУС-CLAIM БЕЗ УЛИКИ: ✅ рядом с именем файла** [[prichina-kak-claim]] — прогон ОБЯЗАТЕЛЕН,
  если в области Шага 0 есть НАРУЖНЫЙ док (README / INSTALL / отчёт / паспорт / пост) или черновик, писанный агентом:
  `python ~/.claude/scripts/status_claim_lint.py <файлы>` (0 токенов, stdlib; exit 2 = находки).
  Судит СТРУКТУРУ, не подстроку: ✅ в пределах 80 символов от имени файла → файл ищется на диске
  в НЕСКОЛЬКИХ корнях (§5.4 check-all-places), вердикт = «НЕ ПОДТВЕРЖДЁН + где искал», не «файла нет».
  Починка находки: приложи улику (`ls`/цитата) ЛИБО замени ✅ на 🤔 ЛИБО осознанный `status-claim-ok: <причина>`
  (голый маркер не глушит). Замер 29.08: класс дал **3 датированные поломки** (10.08 панель ревьюит
  непрочитанный файл · 13.08 панель судит вырожденный контекст · 14.08 draft-агент подал несуществующие
  `package_verify.py`/`quarantine_lite.py` как установленные ✅). Шум двери замерен: **3.5% файлов на корпусе 200**
  (было 1334 находки до структурного порога — это был бы вечно-красный сторож).
  Входная половина того же класса стоит сама: `secondop` EVIDENCE RULE + 5-я строка сид-блока 🔍 УЛИКА.
  Тест: `_test_status_claim_lint.py`;
- ⭐ **метрика-ДОЛЯ/отношение → сверь ЕДИНИЦЫ числителя и знаменателя** [[measurement-units-must-match]].
  Правка строит или трогает долю/процент/сравнение двух рельс записи? Выпиши, что физически
  означает ОДНА строка КАЖДОЙ рельсы. Разные единицы (событие хука vs подъём процесса vs
  сессия) → доля врёт молча. Замер 13.08: доля Firefox 9 дней сравнивала подъёмы драйвера
  с MCP-кликами (1.6% сырая vs 7.6% честная); ТРИ внешних ломателя не поймали — каждый
  смотрел свою рельсу порознь, сравнение единиц не проверял никто;
- ⭐ **фолбэк метрики: рапорт можно, ДЕЙСТВИЕ нельзя** [[fallback-metric-ok-to-report-never-to-act]].
  Найди в правке каждое место «честный измеритель молчит → беру соседний похуже» и посмотри,
  что стоит НИЖЕ по потоку: `print` — ок, `kill`/`send`/`write`/`commit` — дыра.
  Прогон: `grep -nE "or 0\b|except.*:\s*$|is None|not .*_map|fallback" <файл>` и глазами по хитам.
  Замер 04.08: обещание «судим только по дельте» жило в docstring и 54 зелёных тестах, а
  отменяла его ОДНА строка фолбэка на `ps %CPU` — нашёл внешний ломатель, не тесты.

## Шаг 2.5 — ВТОРОЕ МНЕНИЕ: ⭐ПАНЕЛЬ, все рельсы ОДНОВРЕМЕННО (приказ оператора 05.08.2026)

**Дефолт с 05.08 — одна команда, четыре пары глаз разом:**
```
python "%USERPROFILE%\.claude\scripts\cc-review\secondop.py" panel --ritual tt --task <id> --context "<что собрали + что проверили>"

⭐⭐ **ПАНЕЛЬ СУДИТ ПОЧИНКУ, А НЕ ИСХОДНУЮ ЗАДАЧУ** (замер 04.09.2026). Чинил корень — в `--context` кладёшь КОД ПОЧИНКИ и список «что я объявил закрытым», а в `--task` пишешь «сломай ЭТИ починки». Зелёная СВОЯ приёмка доказательством не является: 21 корень был зелёным локально и на сервере, после чего панель из 8 движков нашла в тех же починках **8 дефектов**, из них три назвали ≥2 движка независимо (маркер готовности удовлетворялся текстом прошлого отчёта · порог размера добивался сайдбарными ссылками · fail-closed гейт оказался fail-open по состоянию ПРЕДКА элемента). Сходимость ≥2 движков = чинить не думая; одиночное наблюдение = проверять уликой. И сетку, написанную НА находки панели, гони мутантами отдельно: её первая версия пропускала 4 из 8 мутантов, потому что смотрела на возвращаемый текст, а починки меняли время и сообщение ([[red-first-or-the-test-is-fake]], [[panel-broke-my-own-fix]]).

⭐ В `--context` кладём ПЕРВОИСТОЧНИК — живой код горячих участков (или файлы целиком), не свой пересказ; пересказ допустим лишь как навигация поверх. Замер 20-21.08: панель на пересказе — точность 25% (2 из 3 ложных находок выросли из формулировок пересказа), та же панель на живом коде — 10/10. Находки панели — гипотезы: каждую сверить с первоисточником, в отчёт обе колонки (принято/опровергнуто с уликой). Канон: Библия `reglament-proveryayushchemu-pervoistochnik-ne-pereskaz` + память [[panel-judges-my-spec-not-the-code]].
```
Codex, Grok и Gemini идут ПАРАЛЛЕЛЬНО (каждый своим процессом), а промпт браузерной ноги GLM ложится на диск ДО их старта — открывай вкладку `chat.z.ai`, пока headless крутятся, и добей вердикт через `log-ext --engine glm`. Код выхода `3` = независимого второго мнения нет (ответил один) → вердикт `/tt` максимум ⚠️. Порядок «сначала Codex, потом остальные» отменён: на практике он означал «только Codex» (замер 05.08: Grok $300/мес выбран на 12%). Паспорт: `scripts/docs/secondop_panel.md`.

Ниже — механика ОДИНОЧНЫХ рельс: она жива и нужна, когда панель избыточна (одна мелкая правка) или когда чинишь конкретного вендора.

### Одиночные рельсы (частный случай)
Своя проверка слепа к своим же слепым зонам — второй вендор ловит то, что мы не видим ([[test-after-build-skill]] + Decision Memo Phase 1.5). Поэтому ломает не только сессия, но и внешние глаза. Их ТРИ пары (dev 21.07; ⭐26.07 Grok переехал в CLI; ⭐27.07 добавлен Gemini): **Codex** (headless CLI, дефолт), **Grok** (⭐26.07 на хабе локальная CLI-рельса на подписке, headless — `secondop.py t3 --engine grok`; браузер grok.com = ФОЛБЭК, см. [[grok-second-reviewer-rail]]) и **Gemini** (headless без браузера, `gemini_review.py break`, см. [[gemini-third-reviewer-rail]]).

**Когда зову (узко, чтобы ритуал не раздуло):** в области Шага 0 есть изменённый **исполняемый** артефакт (скрипт · скилл · хук · рутина · пайплайн). Только заметки/тексты/frontmatter → пропускаю **осознанно**, логирую и пишу это в вердикт.

**Рельса 1 — Codex (дефолт, зову всегда первым):**
```
python "%USERPROFILE%\.claude\scripts\cc-review\secondop.py" t3 --ritual tt --task <id-задачи> --context "<что собрали + что уже проверили в шагах 1-2>"
```
Пир без Codex-логина → тот же вызов через `_shared\secondop_client.py` (брокер ответит по шине).

**Рельса 2 — Grok-ломатель (зову когда):** (а) Codex недоступен/quota-blocked — Grok спасает вердикт от ⚠️; (б) артефакт рискованный/safety-critical или Codex дал спорный COUNTER — гетеро-пара, зову ОБОИХ; (в) оператор сказал «спроси грока».
**Механика-дефолт (⭐26.07, хаб): локальный CLI headless** — `python ...\secondop.py t3 --engine grok --ritual tt --task <id> --context "..."` (лог и зеркало в чат 04 автоматические, ручной log-ext НЕ нужен). CLI мёртв/разлогинен (`secondop.py doctor` — ⚠️ не `grok doctor`: такой подкоманды у grok НЕТ, проверено 04.08, в `grok --help` 13 команд и doctor среди них нет; exit 0 = обе рельсы живы · 3 = вендор установлен и не отвечает ЛИБО рельс нет вовсе · 1 = канон обещает подкоманду, которой в движке нет) → **фолбэк-браузер** (Chrome-MCP, человеческий темп, как /dr-fanout; строго локальный браузер [[browser-work-on-peers-not-hub]]):
1. `python ...\secondop.py grok-prompt --task <id> --context "<что собрали + что проверили>"` → paste-ready промпт;
2. вставить в НОВЫЙ чат grok.com (обычная модель, Expert не трогать), дождаться ответа;
3. первая строка ответа = вердикт `ACCEPT`/`COUNTER`/`BLOCK`;
4. залогировать: `python ...\secondop.py log-ext --reviewer grok --task <id> --ritual tt --verdict "<1-я строка>" --note "<ссылка grok.com/c/… ПЕРВОЙ + суть находок>"`. Ссылка на чат в `--note` **обязательна и идёт первой** (note режется до 200 симв. — длинная преамбула съест ссылку, Grok COUNTER 21.07) — это доказательство, что вердикт реально от Grok, а не вписан рукой (Codex VERIFY 21.07); плюс ответ Grok целиком цитируется в вердикте /tt. Не распознан формат → вердикт НЕ засчитан (переспросить в формате или log-skip).

**Рельса 3 — Gemini-ломатель (⭐27.07, скилл `/gemini`; зову когда):** (а) Codex И Grok недоступны/выжгли квоту — Gemini спасает вердикт от ⚠️; (б) safety-critical артефакт или спорный COUNTER — зову третьим голосом; (в) оператор сказал «спроси джемини».
```
python "%USERPROFILE%\.claude\scripts\cc-review\gemini_review.py" break --task <id> --context "<что собрали + что проверили>"
```
Headless, без браузера (REST-рельса ~7-10 с; `--engine cli` = `@google/gemini-cli`). Вердикт первой строкой `ACCEPT`/`COUNTER`/`BLOCK` и **сам** пишется в `usage.jsonl` (`log-ext --reviewer gemini`) — ручной log-ext НЕ нужен. Рельса не ответила → скрипт сам пишет `log-skip` и выходит с кодом 3 (вердикт /tt тогда максимум ⚠️ PARTIAL). Ключ = бесплатный тир Google AI Studio (`secrets\gemini.env`), биллинга нет → превышение = 429, не счёт; ⚠️ OAuth-вход CLI для физлиц Google отключил — чинить бесполезно, живёт только API-ключ.

**Как читать ответ (всех трёх рельс):** `COUNTER`/`BLOCK`/сценарии поломки = **находка** → это Шаг 4 (корень → починить → перепрогнать), не «мнение к сведению». `ACCEPT` = согласие, находки нет. Достаточно ОДНОГО полученного внешнего вердикта; вторая пара глаз — по правилам рельсы 2.

**Рельса 4 — браузерная дверь ЛЮБОГО вендора (⭐31.07, правило оператора: отменяется дверь, а не вендор).** Кончилась квота / нет CLI / headless разлогинен → это закрылась ОДНА дверь; веб-морда вендора открыта всегда (подписки живые, Chrome залогинен на всех машинах [[one-chrome-account-all-machines]]):
1. `python ...\secondop.py web-prompt --engine <grok|gemini|chatgpt|claude|mistral|deepseek> --context "<что собрали + что проверили>"` → paste-ready промпт с контрактом вердикта;
2. вставить в НОВЫЙ чат на сайте вендора (строго локальный браузер), дождаться ответа;
3. залогировать `log-ext --reviewer <вендор>` со ссылкой на чат ПЕРВОЙ в `--note`.
Состояние дверей узла — факт, не догадка: `python ~/.claude/scripts/llm_rails.py --verify` (❌ = двери нет совсем; ⚠️/✅ = дверь есть). Цена ошибки замерена 31.07: Grok был залогинен в браузере и уже дал вердикт, а сессия записала «нужен login = руки оператора» — смотрели на закрытую дверь рядом с открытой ([[browser-door-when-cli-dead]]).

**Скип — только явный, никогда молчаливый** (COUNTER Codex 17.07): причины **«квота» и «нет CLI» больше НЕ принимаются** — сперва рельса 4; log-skip законен, только когда закрыты ВСЕ двери (включая браузерную — например, узел headless без браузера И шина-брокер молчит) / нет исполняемых артефактов →
```
python ... secondop.py log-skip --ritual tt --task <id> --reason "<все двери закрыты: перечисли какие|нет исполняемых артефактов>"
```
и вердикт Шага 5 **не может быть ✅** по этой причине: максимум **⚠️ PARTIAL «второе мнение не получено»**. Пропущенный звонок ≠ зелёный тест. Исключение: артефакт неисполняемый — тогда скип нейтрален, ✅ возможен.

**Наблюдаемость:** каждый вызов/скип пишется в `bridge-state/usage.jsonl` (attempted · ok · skipped · finding); суточный дайджест — `secondop.py digest --post` → чат 03. Ноль вызовов за сутки = сигнал «ритуал не работает», а не тишина.

## Шаг 3 — СЛОЙ ВИДИМОСТИ (видно ли, что сработало?)
Самый частый тихий баг — не в ядре, а в том, что **результат не видно** ([[verify-existing-before-proposing]]):
- **Готовый гейт первым:** если у проверяемого есть СВОЙ детерминированный гейт/тест (`memory_guard.py`, `/arch`, `sync_check`, `_test_*.py`) — запусти ЕГО и бери ЕГО вердикт; не пере-выводи логику самодельным awk/grep — дубль гейта со временем разъезжается с оригиналом и даёт ложные/расходящиеся тревоги (грабли 2026-06-27/07-04: raw-awk и `memory_guard.py` мерили длину строк по-разному).
- есть ли счётчик/лог/строка-доказательство, что оно отработало?
- «LastResult=N без логов» = неотладимо → это ❌ по видимости, даже если ядро вроде ок. (Так поймали пустой TurnState и ложный RED синка.)
- ⭐ **ПРИЧИНА ОБЯЗАНА БЫТЬ ПРИЧИНОЙ ТОГО, ЧТО ДЕРЖИТ** (замер 14.08.2026, `hold-with-reason-ok-is-a-lying-indicator`). У прибора с НЕСКОЛЬКИМИ условиями возьми красную строку и спроси: «по ней человек знает, что чинить?». Красный флаг с зелёным хвостом (`[HOLD] файл.md — ok`) = прибор ВРЁТ: он считал два условия, а напечатал причину не того. Так 47 из 106 постов копилки стояли молча, 21 из них 8 суток. Держат оба условия — печатать оба. Это ❌ по видимости, даже если ядро право.

## Шаг 3.1 — ⭐ ГЕЙТ МАСШТАБА: цена растёт с ОБЪЁМОМ или с ИЗМЕНЕНИЯМИ? (03.09.2026)
Собрал/правил прибор, который что-то ОБХОДИТ (треды, файлы, репо, чаты, строки БД) — задай ему один вопрос: **с чем растёт цена прогона?**
- Растёт с ЧИСЛОМ ИЗМЕНЕНИЙ — ок, поток изменений примерно постоянен.
- Растёт с ОБЪЁМОМ — **дата смерти уже назначена**, прибор сломается ровно от нашего успеха. Лечение = кэш вердикта по дешёвому признаку изменения, который отдаёт сам источник (`updated_at`, ETag, хэш, mtime): неизменившийся объект обязан стоить НОЛЬ запросов. Поднять потолок ≠ починить (это перенос смерти на месяц).
- Есть потолок/лимит/`--max-*` — три обязательных проверки: (1) прибор ПЕЧАТАЕТ, что посчитал не всё («осмотрено N из M»), а не отдаёт голое число ([[instrument-is-a-claim-too]]); (2) рез идёт ПОСЛЕ сортировки, иначе под нож уходит хвост списка — а там обычно лежит добор-заплатка, закрывающая дыру покрытия; (3) у кэша названа ГРАНИЦА ТОЧНОСТИ (что признак изменения НЕ ловит) и принудительное протухание по возрасту.
- Замер, из которого правило: `github_reply_meter` умер дважды от одного корня — 29.08 по таймауту (громко), 03.09 потолком с молчаливой потерей 14 тредов из 214 (тихо). Кэш по `updated_at`: покрытие 200/214 → 217/217, API 433 → 110. Канон: [[instrument-cost-must-scale-with-change]].
- Пропустил гейт на приборе-обходчике → вердикт максимум ⚠️.

## Шаг 3.2 — ПУБЛИЧНАЯ ВИДИМОСТЬ: смотри с чужой стороны провода (01.08.2026)
Если изменённый артефакт **публичный** (профиль, README, страница, репо, пакет, пост) — зелёный тест на нашей стороне ещё НЕ значит, что снаружи это видно. Проверка обязана быть **анонимной**: свой токен/кука/логин показывают тебе твою же приватную картину, и ты объявишь «готово» ровно там, где сломано.
- Правило: **опубликовано ≠ видно.** Пока анонимный запрос не увидел артефакт — он не зашипен, а лежит.
- Инструмент (GitHub-аккаунт лабы и его Pages): `python3 ~/.claude/scripts/public_surface_audit.py --html` → exit 1 при красном, дашборд `_Dashboards/Public-Surface.html`, паспорт `00-System/Public-Surface-Passport.md`. Ночная рутина сигналит только на СМЕНУ картины.
- Для чего у аудитора нет строки — проверь руками одним `curl` без токенов на конкретную строку из артефакта (не на код 200: 200 с пустым телом — самый частый тихий сбой).
- Цена пропуска замерена: profile README двух сессий (S0 31.07 + S1 01.08) был невидим, потому что GitHub требует отдельного клика «Share to Profile» и молчит, когда он не нажат ([[github-profile-readme-share-to-profile]]).

## Шаг 3.3 — ⭐ ЖИВОЙ ЛИ ОБЪЕКТ, В КОТОРЫЙ МЫ ПИШЕМ? (03.09.2026)
Артефакт пишет в **профиль / аккаунт / базу / ветку / слот / канал**, выбранные по КОНФИГУ (`default=`, `current`, `active`, `[Install*]`, «первый в списке») → один дешёвый замер ДО вердикта: чем доказано, что этим объектом ПОЛЬЗУЮТСЯ? Конфиг называет НАМЕРЕНИЕ установщика, диск показывает ФАКТ — свежесть `prefs.js`/`cookies`/`logins`/mtime/счётчика.
- ⛔ Признак живости НЕ должен включать файл, который пишет сам проверяемый инструмент: после залива мёртвый объект выглядит самым свежим, и прибор врёт ровно там, где его зовут.
- Расхождение конфига и факта печатается ВСЛУХ (`WARN: конфиг указывает на X (активность …), живой — Y (активность …)`), а не глушится.
- Замер, из-за которого шаг появился: `chrome2firefox` залил 19978 адресов, 59646 визитов и 6817 закладок в профиль Firefox из `profiles.ini` и напечатал зелёные счётчики; живой профиль оператора в `profiles.ini` не значился вовсе, а у выбранного последняя активность была за три недели ДО миграции. Поймал не тест, а человек, который пошёл проверять свои пароли.
- Не доказал живость → вердикт максимум ⚠️. Канон: память [[live-object-is-picked-by-use-not-by-config]], [[instrument-is-a-claim-too]].

## Шаг 3.3-полу — ⭐ СКОРИНГ СУДИТ ОБЪЕКТ ИЛИ МЕШОК СЛОВ? (04.09.2026)
Артефакт **фильтрует / скорит / ранжирует / отбирает** из РАЗНОРОДНОГО потока (лента, канал, инбокс, выдача поиска, чужой борд) → два вопроса ДО вердикта, оба с цифрой:
- **Чем доказано, что это объект нужного ТИПА?** У вакансии есть ДОЛЖНОСТЬ; буллет, проза и рекламная простыня должностью не являются. Отвод только по ПОЗИТИВНО опознанному признаку («это фрагмент»), а не по «не нашёл каноническую форму» — иначе выпадают живые разговорные посты и дайджесты списком.
- **Признак взят из ПРЕДМЕТА или из текста вокруг него?** Роль и тема считаются по должности; тело даёт уменьшенный вес, но не ноль (иначе теряется не-AI роль в AI-компании).
- ⛔ **Каждое слово словаря — claim, и его надо посчитать на живых данных**: сколько верных срабатываний против ложных. Голое «Partner» дало 82 срабатывания и НИ ОДНОГО верного.
- Замер, из-за которого шаг появился: фильтр вакансий `jobs_tg.py` принимал за вакансию обрывки разрезанных постов, резюме соискателей (96 в базе), рекламу самого канала и скам с торговлей SSN — последний брал 8-11 баллов, потому что нёс и EU, и US, и remote. Брак: 13 строк из 60, 5 из 12 верхних. Прибор не падал ни разу, счётчики были зелёные.
- Не опознал тип и не посчитал словарь → вердикт максимум ⚠️. Канон: память [[score-the-object-not-the-bag-of-words]], [[instrument-is-a-claim-too]].

## Шаг 3.3-бис — ⭐ КЛЮЧ, ПО КОТОРОМУ СШИВАЮТ: он вообще заполнен? (03.09.2026)
Артефакт опирается на **join key / поле идемпотентности / ключ дедупа / ключ «уже сделано»** (`slug`, `external_id`, `msg_id`, `hash`, `story_id`) → ОДИН дешёвый замер ДО вердикта: какая ДОЛЯ записей этот ключ реально несёт? Считать `count(*) WHERE key = '' OR key IS NULL`, а не проверять, что поле есть в схеме.
- ⛔ Пустой у большинства ключ = гейт, который открыт ВСЕГДА и молчит: проверка честно возвращает False на каждой записи, ни один прибор не краснеет, счётчики печатают числа, и по ним принимают решения.
- Ключ читает один код, а заполняет другой → назови обоих поимённо. Читатель есть, писателя нет — это и есть поломка, а не «фича не сработала».
- Второй провод обязан быть НЕЗАВИСИМ от первого: статус в базе и файл на диске врут по-разному. У детектора расхождения обязан быть исполнитель (`--heal`), иначе долг только печатается ([[detector-without-executor]]).
- Замер, из-за которого шаг появился: в контент-воронке `slug` пуст у 2248 записей из 2276 (98.8%) и у 100% сидов в статусе `new`. Один пустой ключ дал три следствия — идемпотентность выбора не срабатывала ни разу, обратная связь черновик→воронка рвалась молча (2 живых долга), а публикация не пришивалась к сиду: леджер 173 `posted` (137 с 20.08) против `published: 2` в воронке.
- Не посчитал заполненность ключа → вердикт максимум ⚠️. Канон: память [[empty-join-key-is-an-always-open-gate]], [[instrument-is-a-claim-too]].

## Шаг 3.3-тер — ⭐ ПРОМЕЖУТОЧНОЕ СОСТОЯНИЕ: кто вернёт элемент, если держатель умрёт? (04.09.2026)
Артефакт переводит элемент в **промежуточную корзину** (`taking` / `in-progress` / `claimed` / `lease` / `processing` / статус «взято в работу») → три вопроса ДО вердикта, все три дешёвые:
- **(1) Кто возвращает?** Есть ли жатва/reaper, которая по TTL вернёт элемент в очередь, если держатель умер между «взял» и «отметил». Атомарный захват защищает от ДУБЛЯ и ничего не говорит про ПОТЕРЮ — это разные беды, и вторая молчит.
- **(2) От какого события мерится возраст удержания?** `os.replace`/`mv`/`UPDATE` часто сохраняют старую метку, и возраст выходит «сколько лежит в очереди», а не «сколько держат». Сторож на такой метке сожмёт свежий захват старого элемента в первую же секунду.
- **(3) Видит ли счётчик здоровья промежуточную корзину?** Если «сколько ждёт» считает только `pending`, потерянные элементы делают очередь короче, чем она есть, и здоровье выглядит зелёным.
- Замер, из-за которого шаг появился (04.09, `spawn_queue.py`): `take` уносил сид в `taking/` атомарно и правильно, возврата не было — 03.09 два сида восстанавливали руками, 04.09 третий висел 11 часов и не считался никем; возраст при этом мерился от `add`, а не от `take`.
- Исполнителя вешай на УЖЕ СУЩЕСТВУЮЩУЮ дверь ([[detector-without-executor]]): здесь жатву вшили в хук самой очереди (96 срабатываний за двое суток), новой рутины не завели.
- Нет ответа хотя бы на один из трёх вопросов → вердикт максимум ⚠️. Канон: память [[atomic-take-without-reaper-loses-work]].

## Шаг 3.3-кватер — ⭐ СКЛЕЙКА ЛЮДЕЙ: чем доказано, что это ОДИН человек? (04.09.2026)
Артефакт **связывает запись с человеком** (импорт контактов, обогащение CRM, дедуп карточек, «дописать ссылку в существующую карточку») → назови КЛЮЧ каждой связи ДО вердикта.
- **В файл пишется только сильный ключ** — телефон или handle. Совпадение по ИМЕНИ или ПОЧТЕ в файл не идёт никогда: оно уходит в корзину «требует глаз» и ждёт человека. Молча выбросить = потерять подсказку, молча записать = отравить карточку.
- **Сильный ключ на входе не делает сильной всю цепочку.** Замер 03.09: телефон верно находил контакт в мосте `apple-contacts`, а ложной была следующая связь «контакт → заметка волта» со своим tier. Проверяй tier у КАЖДОГО звена, а не только у первого.
- **Ошибка склейки выглядит как успех**: лог рапортует «дописано ссылок 143», карточка выглядит обогащённой. Поэтому нужен красный кейс «слабый tier → ссылки нет», а не глазами по логу.
- Ключ-индекс строй по нормализованной форме рядом с маркером (`+`, `phone:`, `тел`), а не «любое число 9-15 цифр»: 637 коллизий last10 и склеенные даты `2026 09 03` в роли номеров, победитель по порядку `os.walk`. При коллизии не выигрывает НИКТО.
- Замер, из-за которого шаг появился: мост на 75% построен по имени (T4-name 957 из 1275), и слабый tier вписал 4 ЧУЖИЕ переписки в боевые карточки лидов — Azam Shaghaghi в `amir-sultan-malik-awan.md`, Manizha Ash дважды в `alex-ge-pengfei-ge.md`, Нора Лебедева в `apefan-2.md`.
- **Прогон гейта** (эталонная сетка склейки, 0 LLM — красный кейс «слабый tier → ссылки нет» уже внутри):
  ```bash
  python D:\Vault\_imports\whatsapp\_test_wa_ingest.py
  ```
  Свой импортёр людей — скопируй оттуда секцию «ИДЕНТИЧНОСТЬ» под свой мост и покажи её КРАСНОЙ на сломанной копии.
- Не назвал ключ каждой связи → вердикт максимум ⚠️. Канон: память [[identity-merge-only-on-strong-key]], [[crm-lead-full-provenance]].

## Шаг 3.3-квинт — ⭐ КОРПУС В ВОЛТЕ: чем его НАЙДУТ, и доказано ли это запросом? (04.09.2026)
Артефакт кладёт в волт **пачку заметок** (импорт переписки, выгрузка, корпус) → назови ДВЕРЬ поиска и покажи ЖИВОЙ хит.
- Строка в логе про реиндекс — claim про прибор, не про результат ([[instrument-is-a-claim-too]]). Реиндекс мог отработать ДО рождения заметок, не покрыть их по scope или собрать базу, у которой нет потребителя.
- Доказательство = запрос по редкому слову из конкретной новой заметки и её путь в выдаче. Замер 03.09: 454 заметки и 148 696 сообщений лежали в волте, в векторном индексе WhatsApp-чанков **ноль**, FTS знал 35 старых путей. После пересборки каталога запрос «Dearden» вернул `wa-Timothy-Dearden--461055.md`, путей стало 492.
- Есть быстрый SQL/FTS слой поверх корпуса → назови его вслух в `/find` и `/ask`, иначе LLM будет читать markdown вместо бесплатного запроса (§6.1).
- Дверь не названа или названа без живого хита → вердикт максимум ⚠️. Канон: память [[corpus-needs-a-named-search-door]].

## Шаг 3.3-секст — ⭐ СШИВКА С ЧУЖИМ ОБЪЕКТОМ: ключ СТРУКТУРНЫЙ или текстовый? (04.09.2026)
Прибор связывает НАШУ запись с ЧУЖИМ объектом (письмо, страница, карточка, тред) → четыре вопроса, каждый обязателен:
- **Ключ структурный?** Домен адреса, id в URL, отдельное поле — да. «Имя компании встречается в строке письма» — нет: текст несёт ещё и транспорт (`[EMAIL]`), и матч цепляется за него. Замер 04.09: в реестре лежала строка `company='ashby'` (мусор писателя), её алиас совпадал в служебном адресе КАЖДОГО письма Ashby и забрал 16 чужих подтверждений — mem0, dust, Cursor получили вердикт «заявка не ушла», а 61/61 тестов были зелёными.
- **Матч однозначен?** «Первый по порядку словаря» = случайный владелец, то есть тихая кража В ПЛЮС. Побеждает самый длинный/специфичный ключ, ничья → None. Молчание честнее выдуманного хозяина.
- **Приговор по ТЕЛУ или по заголовку?** Заголовок (тема письма, title страницы) — свободный текст чужого вендора, бесконечное множество: латать его регекспами = чинить симптом, дыра откроется на следующем шаблоне (замер: латали 03.09, открылась 04.09). Тело — шаблонный язык, конечное множество идиом; пополнять его законно.
- **Какой канал прибор НЕ смотрит?** Назови вслух. Часть объектов приходит другой дорогой (мы подавались письмом, а не формой) — для них у прибора обязан быть ОТДЕЛЬНЫЙ вердикт, а не молчаливое «не найдено». Смешать со «доказано» = соврать в цифрах; выдать за «пропало» = послать человека делать необратимый дубль.
- Хоть один вопрос без ответа → вердикт максимум ⚠️. Канон: память [[match-entity-by-structural-key]], [[instrument-is-a-claim-too]].

## Шаг 3.4 — ⭐ РАТЧЕТ: escape-авария в коде (03.09.2026)

```
python ~/.claude/scripts/_test_no_control_bytes.py
```

Правил код патчем, внутри которого есть обратный слэш (windows-путь, `\n`, `\b`, `\d` в регулярке)? Прогони это ПЕРЕД вердиктом. `exit 1` = где-то в коде лежит управляющий байт.

**Почему отдельный шаг, а не «и так увижу».** 03.09 класс сработал шесть раз за один день, и один случай был дорогим и невидимым: в `deploy_deadwood.py` литерал `r"\bmd5"` стал `r"<0x08>md5"`, и живая проверка «verify прибит к md5» не срабатывала **никогда**. Голый `grep` печатает такую строку как `r"md5"` — терминал съедает backspace, глазами дефект не виден вообще. Нашёлся только побайтовым сканом.

**Лечение на будущее:** патч с обратными слэшами пишем **файлом** (Write → `python файл.py`), а не python-в-heredoc: escape ломается на границе слоёв. Канон: память [[patch-code-via-file-not-heredoc]].

## Шаг 3.45 — ⭐ ВЛАДЕЛЕЦ ОБЪЕКТА: не заводи второго убийцу (04.09.2026)

```
python ~/.claude/scripts/robot_owner_lint.py
```

Собрал робота, который **трогает объект** — гасит процессы, перезапускает приложение, чистит папку, правит общий файл? Прогони это перед вердиктом. `exit 1` = появился робот, которого нет в `~/.claude/robot_owners.json`.

**Правило:** у объекта один АВТОМАТИЧЕСКИЙ владелец. Владелец есть — расширяй его, а не заводи своего. Свой всё же нужен (ручной инструмент, патруль) — впиши в реестр с ролью и с тем, чем он ограничен, и **уважай рельсы владельца**.

**Почему отдельный шаг.** Класс с тремя датированными случаями: 26.07 два сторожа дрались на восстановлении пакета; 31.08 двенадцать чинилок на одно приложение довели до приказа «выключить всё», и невиновный жнец простоял трое суток (138 зависших процессов); 03.09 патруль закрыл ровно те процессы, что жнец пощадил осознанно. Пять «почему» дали корень не в роботах: **владельца негде было посмотреть, поэтому своего написать дешевле, чем найти чужого.** Замер 04.09: 13 скриптов способны убить процесс Claude.

Канон: память [[one-object-one-owner-robot]], реестр `~/.claude/robot_owners.json`.

## Шаг 3.5 — ТЕСТ + ДОК гейт (§5.8, dev 28.07 «и ВСЕГДА это делать теперь»)
Каждая живая деталь в области Шага 0 обязана выйти из /tt с тестом И доком — иначе вердикт максимум ⚠️:
- **НОВАЯ деталь** (скрипт/скилл/рутина/хук): тест и док-паспорт рождаются **в этом же заходе**, ждать «докажи, что приживётся» ⛔. Паспорт — для слабейшего починщика ([[repairability-first-how-we-build]]): что делает · вход/выход · кто дёргает · что ломается · как понять · как починить.
- ⭐ **РУТИНА → СТРОКА В РЕЕСТРЕ** (dev 02.09, голосом): собрал/изменил повторяющийся процесс (задача планировщика · cron · hook · вахта · ручная повторёнка) → покажи его строку в мега-списке рутин: обнови снимок узла `python %USERPROFILE%\.claude\scripts\fleet_routines_collect.py` и найди рутину в `_machine-bus\_fleet-routines\routines-<NODE>.json` (Маяк ежечасно сводит снимки в Google-книгу «Флот — живой стол»). Повторёнка ВНЕ планировщика сама не доедет — занеси в книгу руками. Нет строки → ⚠️. Канон `reglament-lyubaya-povtoryayushchayasya-rabota-zhivyot-v-reestre-rutin` + [[routine-must-live-in-registry]].
- ⭐ **РУТИНА → НАЗОВИ СВОЙ ВЫХОД** (класс `silent-green-watchdog` / семья `instrument-vrjot-zelyonym`, 46 датированных случаев, починка 04.09): рутина рождается с рапортом «зелено» и БЕЗ единого свидетеля результата — «задача выстрелила» ≠ «работа приземлилась». Прогон: `python %USERPROFILE%\.claude\scripts\_shared\green_gap.py` (0 LLM, свой контрольный пример, exit 0/1/3/4). Новая рутина обязана дать ОДНО из двух: строку в `ARTIFACTS` (`scripts\_shared\output_freshness.py` — ГДЕ приземляется её работа) **либо** строку с ПРИЧИНОЙ в `~/.claude/green_gap_exempt.json` (выхода нет осознанно). Молчание = зелёный, который никто не проверял → вердикт максимум ⚠️. Ратчет: старый долг назван числом и молчит, кричит только НОВОЕ. Замер 04.09 (хаб): 243 наших включённых задачи против 41 строки реестра = выход заявлен у 17%.
- ⭐ **ВЫХОД В СИНКАЕМОЙ ПАПКЕ → НАЗОВИ ЕГО КЛАСС** (класс `shared-writers`, починка 14.09): выход рутины/скрипта лёг в синкаемое (волт · `_machine-bus` · `~/.claude` · `_imports`) → он ОБЯЗАН иметь строку в `D:\Vault\_imports\sync\derived_writers.json`, ровно в одном из трёх классов: `per_node` (данные пер-узловые — имя получает суффикс узла, конфликт физически невозможен) · `writers` (данные общие — ОДИН назначенный владелец, и раннер у него ДОКАЗАН, иначе меняем громкую поломку на тихую заморозку) · `idempotent_verified` (тело рендера НЕ зависит от часов — **только с именем теста**, который это доказывает). Прогон: `python D:\Vault\_imports\sync\derived_writers.py --check` и `--audit`. Нет строки → вердикт максимум ⚠️. ⚠️ Класс определяется по ВОПРОСУ «данные тут про ЭТОТ узел или про весь флот?», а не по тому, где лежит файл: ошибка в эту сторону стоила слепоты — один писатель у пер-узлового файла = ослепли на пяти узлах. Замер 14.09: 8 путей кровоточили 10 суток, самый громкий (`ACTIVE_NOW.md`) — 43 копии с 6 узлов, потому что класс `idempotent` был объявлен БЕЗ теста и оказался ложью. Канон: `derived_writers.json` §_refuted + [[watchdog-must-verify-the-item]].
- ⭐ **ПУТЬ В КОНФИГЕ ОБЯЗАН СУЩЕСТВОВАТЬ** (класс `config-path-points-nowhere`, замер 06.09.2026): трогал реестр аккаунтов/профилей (`_imports/chatgpt/accounts.json`, `~/.claude/browser-profiles/accounts.json`) → прогони `python3 ~/.claude/scripts/accounts_paths_lint.py` (0 LLM, 0 сети; exit 0 чисто · 1 красное · 3 нет данных · 4 крэш). Повод: `ff_profile` у `bb`/`au04` указывал на `autoff-bb`/`autoff-au04`, которых не было НИ НА ОДНОМ узле — лестница жатвы токена не могла отработать в принципе и **не сказала ни слова** (рельса печатала честный SKIP «нет bearer», а ПРИЧИНУ не назвал никто). Линт судит и **связку двух реестров**, но ТОЛЬКО у аккаунта, чей `runner` = этот узел: браузерный реестр машинно-локален (`browser-profiles/` в `~/.claude/.gitignore` + под `*` в `.stignore` — ни git, ни Syncthing его не возят), поэтому у чужого аккаунта два поля описывают РАЗНЫЕ машины и сравнивать их нельзя (у a2 верны ОБА: `fbread` на хабе, `autoff` на NODE-0X). Такое не молчит и не желтит — идёт строкой «НЕ СВЕРЯЛОСЬ» + `meta[join_not_compared]`. ⚠️ Имя узла с доменным хвостом (`<узел>.local`, FQDN в Docker/CI) резолвится срезом хвоста: без него СВОЙ сломанный аккаунт выходил ЗЕЛЁНЫМ (замер 07.09: `rc=0`, `GREY` вместо `RED`). Красное = чинится здесь; не прогнал после правки реестра → вердикт максимум ⚠️. Тест: `_test_accounts_paths_lint.py` (5 мутаций, все показаны красными 07.09).
- ⭐ **ДОКА ЖИВЁТ В КОДЕ** (dev 07.08 голосом, СУПЕР ВАЖНО): у Python-детали док = **docstring в самом файле** (назначение · вход/выход · кто дёргает · рельса · `updated: ГГГГ-ММ-ДД`), один источник — отдельный md-пересказ того же самого ⛔; тест назван в docstring, деталь названа в тесте (код·тест·дока = единый узел). Docstring отсутствует или без updated-даты → ⚠️. Канон `reglament-dokumentaciya-po-chastyam-i-vnutri-koda`.
- **ИЗМЕНЁННАЯ/ПОЧИНЕННАЯ деталь**: поведение поменялось → док обновляется **той же сессией** (док, который врёт, дороже отсутствующего); класс пойманного бага получает тест/гейт, чтобы не вернулся ([[fix-root-cause-not-symptoms]] forever-fix).
- **«Тест есть» ≠ «тест гоняют»** ([[test-exists-vs-grid-runs-it]]): тест без расписания/сетки и видимой даты прогона ≤30 дн считается несуществующим (§5.8 правило 2). Подключи в регресс-сетку или назови причину.
- ⭐ **СЧЁТЧИК ИСПОЛЬЗОВАНИЯ** (§5.8 третий атрибут, dev 04.08: «на весь функционал вешаем счётчики — кто и насколько успешно использует»): деталь считает свои вызовы строкой JSONL `ts·node·actor·event·outcome` рядом с собой (эталоны: `usage.jsonl` secondop, `_spawn_slot_guard.log`, `_chip_guard.log` — тот же паттерн, НЕ новая инфраструктура). Гейт считает ALLOW/BLOCK, скилл — старт, рутина — исход тика (не факт запуска). Флотовой механизм → лог читаем с хаба, иначе «кто пользуется» снова слепое пятно (замер 04.08: session-control-pack — применение видно 5/6, использование только локально). Нет счётчика → ⚠️. Канон `reglament-schyotchik-ispolzovaniya-na-ves-funkcional`.
  ⭐ **И ТЕСТ В НЕГО НЕ ПИШЕТ** (замер 04.09.2026): путь счётчика обязан переопределяться флагом `--counter`/env, а регресс-сетка обязана его переопределять — иначе метрика «живое или утиль» врёт. Замер: в `whatsapp_pipeline.jsonl` 67% строк написал тест, использование было завышено **в 7 раз**, и почти не используемая деталь выглядела живой. Кейс приёмки: снять размер боевого JSONL в начале теста и сверить в конце («боевой счётчик тестом НЕ тронут»). Эталон: `D:\Vault\_imports\whatsapp\_test_wa_ingest.py` (подстановка в общей `run()`). Счётчик без флага → ⚠️. Память [[counter-is-production-tests-must-not-write-it]].
- ⭐ **KILL-LIST: тест обязан сказать, что именно он ловит** (замер 11.08, [[kill-list-makes-tests-checkable]]). В докстроке теста — блок `МУТАЦИИ, КОТОРЫЕ ЭТОТ ТЕСТ ОБЯЗАН УБИТЬ`: одна строка = конкретная правка исходника → ИМЯ падающего от неё кейса. Ревьюер применяет каждую строку к **КОПИИ** детали (живую не мутируй: сторож стреляет каждые 5-20 минут) и смотрит, покраснел ли НАЗВАННЫЙ кейс. Строка не сработала = ЛОЖНАЯ заявка, и это хуже отсутствующей: по ней деталь считается защищённой. Добавь сверх списка СВОЮ мутацию — обе фикции 11.08 (кейс из одних отрицательных проверок; снятая защита, которую тест не заметил) всплыли именно на ней. Пустая мутация (добавил переменную) ничего не доказывает — сверь, что подстановка изменила поведение. Пишет тест внешняя подписка (§6.3, `secondop.py implement`), kill-list требуй прямо в спеке + «честный пробел лучше зелёного вранья».
- **Доказательство**: строка детали в карте покрытия — `python ~/.claude/scripts/coverage_map.py` (тест ✅ · док ✅ · ссылки); нет карты на узле → перечисли тест и док явными путями в вердикте. ⚠️ Карта считает покрытым только `_test_<имя детали>.py`: тест, названный по сценарию (`_test_cron_watchdog_absent.py`), в зачёт не идёт → покрытие ЗАНИЖЕНО, проверь глазами перед выводом «тестов нет».
- ⭐ **РЕЛЬСА ХРАНЕНИЯ — НАЗОВИ ОКНО ВОССТАНОВЛЕНИЯ** (dev 21.08 «почини корень»): деталь, которую зовём бэкапом / зеркалом / репликой / синком / снапшотом, выходит из /tt с ✅ только если (1) названо ОКНО — сколько времени есть на откат, и (2) показан ПРОГОН, где удаление на источнике НЕ уничтожило вторую копию. Способы ровно три: датированный карантин · версия/снимок · отказ прохода по порогу из ЗАМЕРА (медиана + наблюдённый максимум по истории прогонов, не из головы). Реплика без окна — вторая мишень, а не страховка. Отчёт обязан нести ЧИСЛО удалённого/отложенного И В ХОРОШИЕ ДНИ ТОЖЕ (цифры, которой нет в отчёте, для наблюдателя не существует), красное едет на живую рельсу, а не в файл рядом со скриптом. Нет окна или нет прогона → максимум ⚠️. Замер 21.08: зеркало E→F каждую ночь переносило в «запасную копию» все удаления суток и рапортовало успех, потому что «удалено N extras» лежит внутри кодов возврата 0-7. Канон `reglament-strahovka-ne-povtoryaet-razrushenie` + [[insurance-must-not-replay-destruction]].
- ⭐ **CLI-ДЕТАЛЬ ОБЯЗАНА ОТВЕЧАТЬ НА `--help` И БИТЬ ПО НЕИЗВЕСТНОМУ ФЛАГУ** (гейт при рождении, замер 03.09.2026): тронул/собрал скрипт, который читает аргументы → `python ~/.claude/scripts/help_flag_lint.py --check <путь>`. exit 0 = чисто ЛИБО дыра заморожена в baseline (**старый долг правку НЕ блокирует**) · **exit 1 = НОВАЯ дыра класса `unparsed-flag-silently-runs-work` → чинить В ЭТОМ ЖЕ заходе**, иначе вердикт максимум ⚠️ (лечение линт печатает сам, 3 строки в начало `main()`). Почему гейт ЗДЕСЬ, а не только в ночной сетке: ratchet краснеет НОЧЬЮ и только ОТЧЁТОМ, а отчёт ничего не держит — за 11 дней после baseline 23.08 во флот въехало **55 новых дыр, ВСЕ в файлах, тронутых после baseline** (старых 0), и класс дал 8 датированных случаев уже ПОСЛЕ объявления «закрыт» (`pr_watch.py --help` = 7.5 мин живого тика по GitHub; `output_freshness.py --help` отправил пост в живой чат 03 в 01:41). ⚠️ **exit 2 = «НЕ ПРОВЕРЕН», и это НЕ «чисто»**: файл вне корней линта (`scripts/`, `imports/`) он не сканирует — гони гейт на детали, живущей в корнях, либо задай `HELP_FLAG_LINT_ROOT`. Тест: `_test_help_flag_lint.py` секция G (мутации: вырезать ветку → G1/G3/G4/G5; гейт, который не краснеет → G2; убрать проверку корней → G6 ловит ложное зелёное).
- ⭐ **ОТПЕЧАТОК АВТОРА ВНЕ GIT — ЧЕРЕЗ ЕДИНСТВЕННУЮ ДВЕРЬ** (§5.11; дыра вскрыта замером 15.09.2026): тронул деталь → проверь, доедет ли провенанс. `git ls-files --error-unmatch <файл>` отвечает «не знает git» (на NODE-0X `~/.claude/.gitignore` держит `*`, поэтому `scripts/` и `skills/` под git НЕ ходят) → идёт вне-git ветка §5.11: подпись с датой ВНУТРЬ артефакта + строка РОВНО через `python ~/.claude/scripts/change_ledger.py add --actor … --tool … --target … --summary …`. ⛔ Самодельный писатель запрещён: `open(<леджер>,'a')` руками и имя узла из `socket.gethostname()` вместо `COMPUTERNAME` — это класс `ledger-writer-bypasses-the-one-door`, ТРИ датированных случая (04.09 · 10.09 · 15.09), и 10.09 он стоил УНИЧТОЖЕННОГО файла журнала на case-insensitive FS (два написания одного узла = один инод). Доказательство: `python ~/.claude/scripts/change_ledger.py lint` — назови долю канона ЧИСЛОМ (замер NODE-0X 15.09: всего 234, канон 5, вне канона 227 — дверь обходили 97%). Строки нет либо писал мимо двери → вердикт максимум ⚠️. Канон `reglament-otpechatok-avtora-na-kazhdom-izmenenii-koda` + [[edit-authorship-signature]]; корневой гейт — `task-2026-09-15-ledger-writer-bypasses-the-one-door`.
- **УБЕРИ ВЕРСТАК** (§5.8 правило 1): каждый созданный по пути инструмент проштампуй — постоянный (тест+док) / одноразовый (`_scratch\`, авто-снос 30 дн) / в корзину. Не проштамповал = не закрыл.

## Шаг 3.6 — BACKPRESSURE: цикл без внешнего давления не допускается (альфа 17.08.2026)
Если проверяемая деталь **работает без человека в цикле** (рутина, cron, `/loop`, Ralph-луп, `claude -p`
в баш-цикле, самоперезапускающийся агент, автоулучшатель) — она обязана **назвать своё внешнее
давление**. Не назвала → вердикт максимум ⚠️, в прод не идёт.

Откуда правило: Julia [ФАМИЛИЯ], приём **backpressure** — внешнее давление, которое удерживает
зацикленного агента от того, чтобы «слететь с катушек». Агент в цикле **будет** придумывать себе
всё новые улучшения; без давления он уходит в космос и жжёт бак. Источник — доклад Крестникова
(Сбер/GigaChain) 17.08.2026, [[insight-2026-08-17-harness-i-ralph-loop-krestnikov]]. ⚠️ Приём чужой,
у нас на своих задачах ещё не замерен — это 🤔 гипотеза, но цена ошибки односторонняя: без давления
теряем бак и данные, с давлением теряем только пару строк кода.

**Не новая инфраструктура:** у нас давление УЖЕ есть, просто у него не было имени и не было двери,
которая спрашивает. Годные виды давления (нужен хотя бы один, лучше два):
1. **Детерминированный судья** — `_test_*.py` / готовый гейт (`regress_run.py`, `memory_guard.py`,
   `/arch`), который цикл обязан пройти на каждой итерации. Судья не живёт внутри того, что судит (§5.5).
2. **Потолок итераций / времени** — жёсткий кап и авто-kill ([[shadow-first-mvp-pattern]] time-box).
   «Бесконечный» цикл без капа = ❌, а не ⚠️.
3. **Бюджетный тормоз** — лимит токенов/вызовов, при упоре цикл встаёт САМ, а не после счёта оператору.
4. **Kill-switch** — файл-флаг/`paused`, который останавливает цикл без правки кода.
5. **Порог «не хуже»** — метрика упала → откат итерации (это и есть keep/rollback п.6 альфы).

**Проверка на приёмке (не на слово):** взять названное давление и **сломать нарочно** —
одна итерация обязана быть отбита. Не проверил прогоном = давления нет (§5.8 «проверка без
прогона = нет проверки»).

⛔ Давлением НЕ являются: «промпт просит быть аккуратным», «я посмотрю утром», «модель умная»,
ревью человеком постфактум. Давление должно быть машинным и срабатывать БЕЗ человека —
иначе человек снова оказался в середине конвейера (§4.1 [[human-is-the-bottleneck]]).

## Шаг 3.7 — ⭐ РАЗДАЙ НА ФЛОТ: ноу-хау без раздачи = пользы нет (dev 05.08, капсом «ДАВАТЬ ПОЛЬЗУ»)
Собрал полезное — оно обязано доехать до КАЖДОГО узла-потребителя, иначе вердикт максимум ⚠️.
Правило §7.3-бис существовало и молчало: 05.08 два новых скилла и патч движка пролежали три часа
никому не раздаными, потому что ни одна дверь не спрашивала «а флот?». Теперь спрашивает эта.
1. **Назови круг потребителей ДО раздачи.** Кому не нужно — явная строка `NOTFORME` с причиной
   (чужая ОС, нет железа), а не молчание.
2. **Проверь РЕЛЬС, а не надежду.** «Синк довезёт» — claim, требующий улики: у каждой шары свой
   список пиров. Спроси факт у самого Syncthing:
   `python3 -c "..."` → `rest/db/file?folder=<шара>&file=<путь>` (файл в индексе = едет).
   Замер 05.08: `claude-skills` = 6 узлов, `claude-home` (там же `scripts/*.py`) = 5 — **Маяка нет**,
   и скилл приехал бы туда без движка, который зовёт. Дверь без замка хуже отсутствия двери.
3. **Рельс не достаёт → payload-посылка** (`_deploy/payloads/<id>/` + `install.py` + `CHECKSUMS.txt`) —
   единственный канал, провабельно доходящий до всех; затем `deploy_register.py all <id> ... --verdict PASS --tier 1`
   с МАШИННЫМИ apply/verify (verify читает ФАКТ: маркер/хэш/значение, не намерение).
   `--verdict` обязателен (гейт 02.09): в шину едет только PASS этого /tt; WARN/FAIL = отказ,
   осознанный обход `--force-unsafe "причина"` (причина уезжает в запись посылки).
4. **Закрой свой узел сам** (`deploy_apply.py <id>`) и назови поимённо, кто ещё не применил.
   ⛔ Тишина узла ≠ применено: выключенный, отставший и исправный молчат одинаково.
5. ⭐ **КАНАРЕЙКА СНАЧАЛА, ПОТОМ ОСТАЛЬНЫЕ** (dev 06.08, [[canary-before-fleet-rollout]]):
   раздача ОПАСНОГО класса (канон · хук · шина · синк · сторож · авторизация · автозапуск ·
   системная настройка) идёт ступенями — **1 узел-канарейка** → verify читает ФАКТ (+ один живой
   прогон, если тронута рельса) → **узел ДРУГОГО типа/ОС** → остальные потребители. Откат назван
   ДО раскатки; узлам без того же механизма — `NOTFORME`. Безобидное (заметка · док · тест ·
   строка в скилл) едет сразу всем. Сомнение → считаем опасным. Опасный класс, уехавший на всех
   разом без зелёной канарейки, — вердикт максимум ⚠️: повезло ≠ проверено.
Табло: `python ~/.claude/scripts/fleet_fix_audit.py --html`. Канон: CLAUDE.md §7.3-бис,
[[fleet-parity-board]], [[improvement-rollout-all-peers]], [[sync-can-silently-downgrade-a-part]].

## 🛠 ВЕРДИКТ О СКИЛЛЕ, КОТОРЫМ ПОЛЬЗОВАЛИСЬ (dev 07.09, голосом — обязателен, молчание = нарушение)
Применил в этой работе скилл — вынеси вердикт об ЕГО обновлении. Одной строкой, с причиной в обе стороны:
`🔧 обновляю /X — <что споткнулось>` (чинить В ТОМ ЖЕ заходе) · `📝 обновлю не сейчас — <причина>, строка легла в <адрес>` · `✅ /X обновлять не надо — <почему именно: прошло без заминки / заминка разовая и внешняя / правка дороже боли>`.

⭐ **ВЕРДИКТОВ ДВА, НЕ ОДИН** (dev 13.09, голосом). Второй вердикт: **собственная инструкция того, кто сейчас работал** (рутина `scheduled-tasks/<имя>/SKILL.md`, сид, хук): «не стоит ли переписать мою инструкцию на будущее, чтобы она была качественнее?». Та же тройка `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, всегда с причиной. ⚠️ Замер 13.09: рутина `devto-publish-rhythm` починила СВОЙ файл и смолчала про скилл `/comments`, где висел ПРОТИВОПОЛОЖНЫЙ гейт, правило исполнилось наполовину, и спрашивать пришлось оператору. Канон живёт в СКИЛЛЕ, рутина держит только специфику прогона: разошлись, значит правду в скилл, а из рутины указатель. Канон: [[routine-judges-its-own-instruction-too]], CLAUDE.md §9.3-бис.
Пустое «не надо» вердиктом не является. ⛔ Не путать с `/skill-gap` (тот про скилл, которого НЕТ) и не право раздувать: АК-47 в силе — правка снимает ПЕРЕЖИТУЮ боль, не гипотетическую.
Канон: Библия `reglament-polzuemsya-skillom-srazu-sudim-nado-li-ego-obnovit` · CLAUDE.md §9.3-бис · [[skill-used-judge-if-it-needs-update]].

## Шаг 4 — КОРЕНЬ → починить → перепрогнать
⭐ СНАЧАЛА ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (dev 09-10.08, CLAUDE.md §5.10): поломка объекта ВНЕ области этой задачи → НЕ чинить, а строка в журнал ТОЛЬКО дверью `python ~/.claude/scripts/selfheal.py journal --class <класс> --what "..." --conditions "..." --parts "..." --guess "..."` — рукописная строка в Breakage-Journal.md НЕВИДИМА счётчику (journal_rows считает только |-таблицу; замер 21.08: 27 рукописных строк browser-rail-down не подняли ни одной починки); дверь сама считает счёт и сама заводит сессию починки на 3-й датированной строке; чинится класс только на 3-й датированной строке, отдельной сессией. Карв-ауты «сразу»: сам собранный артефакт этой задачи · KEEP-ядро · потеря данных · безопасность · деньги. ⭐ ИМЯ КЛАССА = ПРЕДМЕТ РЕМОНТА, НЕ КАНАЛ (CLAUDE.md §5.10, 02.09): не бери в `--class` симптом сторожа, код возврата или «красную строку» — проверь фразой «починю — класс закроется НАВСЕГДА?». «Нет, завтра приедет другой предмет» = это очередь под видом дефекта, дроби по предмету (`<цель>-<тег>`). Замер: 32 разных робота сидели в одном `dead-scheduled-task`, счёт не опускался ниже порога и две настоящие починки его не закрыли [[breakage-class-is-a-defect-not-a-channel]].
Любой провал шагов 1-3 (= артефакт ЭТОЙ задачи) → копай в КОРЕНЬ ([[fix-root-cause-not-symptoms]]), не лепи заплатку на симптом, почини КЛАСС → вернись на Шаг 1 и перепрогони, пока чисто. Safety-critical (локи/синк/auth/scheduler/идемпотентность) → «прочитай прежде чем чинить» + мини-тест ([[verify-existing-before-proposing]]).

## Шаг 4.5 — РАЗРЫВ СЕССИИ: считаем сигналы (ТЕНЬ с 2026-07-28, оператор «+»)
Нашёл баг на шагах 1-3 и он не чинится с ходу — прежде чем зарываться, посчитай 4 сигнала и **залогируй**:
```
python ~/.claude/scripts/split_rule.py log --what "<что чиним>" --attempts <провалившихся попыток> \
   --files <файлов в корне> --repro-min <минут на воспроизведение> --context-pct <% контекста> \
   [--shared] --decision stay|split --minutes <итого> --note "<комментарий>"
```
Правило (пока ТЕНЬ, решение всё равно твоё): выносить в отдельную сессию, если сработал ЛЮБОЙ сигнал —
**A** ≥2 провалившихся попытки · **B** корень >2 файлов или задета смежная система (шина/канон/планировщик/auth) ·
**C** воспроизведение >10 мин · **D** контекст съеден ≥70%.
Выносишь — сид-промпт обязателен (что делали · чего достигли · что уже отвергнуто и почему · критерий приёмки ·
не-цели), задача в `10-Tasks`, артефакт помечается ⚠️, а не ✅. Тень без записей = правило НЕ проверено;
сводка `split_rule.py summary --days 14`, критерии флипа в `00-System/Split-Rule-Shadow.md`.

## Шаг 4.9 — ⭐⭐ ВТОРОЙ ЗАХОД: «готово» — такой же CLAIM, как причина (dev 13.09.2026, две голосовые подряд)
Дословно: «когда ты сделал тесты, всё проверил и думаешь, что всё работает — сделай тест ещё раз. Часто бывает: ты говоришь, что всё работает, а на самом деле нихера не работает. И когда я спрашиваю „а ты точно всё починил?" — оказывается „ой, нет, что-то не сделал"».

⚠️ ЗАМЕР АРХИВА 15.08→14.09.2026 (3613 транскриптов): **57 реплик-сомнений оператора в 36 сессиях, 21 из них — сразу после моего claim'а готовности**. Самая частая форма — голое «проверь ещё раз» и «ТЫ УВЕРЕН???????????». Класс датирован многократно, механизм по §5.10 законен.

Шаги 1-3 зелёные — это ПЕРВЫЙ заход. Слово «готово» произносится только после ВТОРОГО, и второй обязан отличаться от первого, иначе он повторяет ту же слепоту:

1. **От ТРЕБОВАНИЯ, а не от кода.** Выпиши списком, что просили (по словам оператора/сида, не по своему пересказу), и против КАЖДОГО пункта поставь улику: живой вывод, счётчик, строку файла. Пункт без улики = не сделан, даже если помнишь, что делал его. Именно тут ловится «сделано на 2/3».
2. **ДРУГИМ методом.** Повтор той же команды вторым заходом НЕ является. Смени угол: прочитай изменённое место С ДИСКА вместо памяти о правке · спроси ПОТРЕБИТЕЛЯ вместо производителя · посчитай прибором то, что первый раз смотрел глазами · глянь артефакт с чужой стороны провода.
3. **Ровно те места, что чинил.** Не общее здоровье системы: изменение реально на диске? доехало до потребителя? СТАРОЕ поведение исчезло (а не соседствует с новым)?
4. **Свой ПРИБОР — тоже объект второго захода.** Первый замер этого самого правила дал 475 «случаев»; второй заход по прибору показал, что в выборку попали системные вставки харнеса, и честное число — 57. Зелёный счётчик, посчитавший не то, хуже отсутствия счётчика.
5. **Назови, чего НЕ проверял.** Строка «проверено: … · НЕ проверено: … (почему)» обязательна. Честное «эту половину не трогал» — нормальный результат; умолчание — ложное «готово».
6. **Критичное → ТРЕТИЙ заход, чужими глазами** (деньги · необратимое · раскатка на флот · исходящее третьим лицам · публикация · секреты · правка канона): панель Шага 2.5, другой узел или другой инструмент.

⛔ Пока Шаг 4.9 не пройден, запрещены слова «всё работает» · «готово» · «починил» · «✅». Максимум — «первый прогон зелёный, иду на перепроверку». Вердикт ✅ без предъявленного второго захода = максимум ⚠️.
Канон: CLAUDE.md §4.3-бис · Библия `reglament-gotovo-dokazyvaetsya-vtorym-zahodom` · [[done-is-a-claim-recheck-twice]]; блок для рутин — `~/.claude/scripts/routine-recheck-block.md` (раскатка `routine_discipline_apply.py --block=recheck`).

## Шаг 5 — ВЕРДИКТ с доказательством
Короткая таблица: **что проверено · как (живой вывод) · ✅/⚠️/❌**. Затем одна итоговая строка:
- ✅ **PASS** — прогнал, ломал, видно — работает. ТОЛЬКО это = «готово».
- ⚠️ **PARTIAL** — работает, но есть жёлтый флаг (назови его + что осталось).
- ❌ **FAIL** — не работает / не видно → корень + что чиню.
Доказательство (вывод/счётчик/скрин) обязательно — без него «✅» не считается.
⭐ **Второй заход (Шаг 4.9) предъявлен строкой** «перепроверил так-то, нашёл/не нашёл то-то» — иначе вердикт максимум ⚠️, каким бы зелёным ни был первый прогон.

**🪞 Гейт льстящего вывода (до того, как назвать вердикт).** Вывод, к которому пришёл, — ВЫГОДЕН ли он мне? (закрывает работу · объясняет неудачу не нашей виной · ставит нас впереди · разрешает не делать неприятное · подтверждает то, во что уже верили).

Да → усилить проверку, а не ослабить: ОДНА НЕЗАВИСИМАЯ улика сверх той, что уже есть.
Прибор: `python ~/.claude/scripts/self_serving_gate.py --check "<вывод>"` (`--ru` печатает чек-лист).

**Потолки вердикта (жёлтый максимум, даже если всё остальное зелёное):** явный скип второго мнения
(Шаг 2.5) · нет теста/дока/счётчика (Шаг 3.5) · **автономный цикл без названного и проверенного
backpressure (Шаг 3.6)** · не раздано на флот (Шаг 3.7). Автономный цикл БЕЗ потолка итераций —
не ⚠️, а ❌: это единственный случай, когда отсутствие давления валит вердикт сразу.

**🌍 Мировой потребитель (декрет оператора 24.08.2026):** вердикт ✅ на починке КЛАССА (чужой может воспроизвести симптом без наших внутренностей) → в ТОМ ЖЕ заходе прогнать скилл **`/share-fix`** (реверс-поиск по дословному симптому → 3-5 лучших живых тредов → gist → вахта pr_watch). Вердикт обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина; молчание запрещено. Механика целиком в `/share-fix` — тут только вызов и вердикт. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.

**📋 Журнал задач (декрет оператора 2026-07-04):** вердикт ✅ = момент закрытия в реестре задач ([[task-journal-done-undone-linking]]): если проверенная вещь числится в реестре — отметь `done` с ЭТИМ доказательством + линк, что она разблокировала; ❌/⚠️ = задача остаётся open (хвост «дочинить X» — в реестр сразу). С машины без движка — `bus_send.py` TASK/DONE. Одна строка в докладе: «📋 журнал: #id → done (доказательство: …)».

---

## Связка с /retro (аудит, не дубль)
`/tt` тестирует на каждой задаче (горячо). `/retro` в конце сессии лишь **АУДИТит** строку «протестировано? ✅/❌» по каждому артефакту и, если ❌ — флагает и предлагает прогнать `/tt` сейчас. Ретро само проверку НЕ делает (поздно/холодно). Не дублируем: каждый уровень ссылается вниз (AK-47).

## Границы / не-дубль
- markdown-only тонкий оркестратор; НЕ сервер/БД/вебхук (если правда нужен > markdown — флаг ⚠️ УСЛОЖНЕНИЕ, решает оператор).
- read-only/dry-run где есть побочки; запись в волт — бэкап-первым ([[vault-backup-rule]]).
- Если сессия ничего не собрала — скажи прямо «тестировать нечего», без церемонии.


ARGUMENTS: brain_temporal.py + врезка в brain_ask.dedup_best_per_file (шаг T09): битемпоральные рёбра/факты, полоса demote за флагом, temporal-gold 41 вопрос

---

**Claude:**

Прохожу оставшиеся ворота скилла (prior art, линты, провенанс, панель):

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== prior_art ===\"; \"$PY\" /c/Users/dev/.claude/scripts/prior_art.py build битемпоральные рёбра valid_to 2>&1 | tail -12; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Prior art check"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== help_flag_lint ===\"; \"$PY\" /c/Users/dev/.claude/scripts/help_flag_lint.py --check D:/Vault/_imports/brain_temporal.py 2>&1 | tail -6; echo \"EXIT=${PIPESTATUS[0]}\"\necho \"=== substr_lint ===\"

---

> `Bash` -- {"command": "sed -n '405,415p' brain_temporal.py", "description": "Look at the substr_lint finding"}

---

> `Edit` -- {"replace_all": true, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    if not fresh and 'v' in _CLOSED_CACHE:\n        return _CLOSED_CACHE['v']", "new_string": "    if not fresh and 'stems' in _CLOSED_CACHE:   # substr-ok: членство в СЛОВАРЕ, не подстрока\n        return

---

> `Bash` -- {"command": "grep -n \"_CLOSED_CACHE\\[\" brain_temporal.py", "description": "Find other cache key uses"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        _CLOSED_CACHE['v'] = out", "new_string": "        _CLOSED_CACHE['stems'] = out"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\n\"$PY\" /c/Users/dev/.claude/scripts/substr_lint.py D:/Vault/_imports/brain_temporal.py D:/Vault/_imports/brain_ask.py 2>&1 | tail -3; echo \"SUBSTR_EXIT=${PIPESTATUS[0]}\"\n\"$PY\" _test_brain_temporal.py

---

> `Bash` -- {"command": "git status --porcelain brain_temporal.py _test_brain_temporal.py brain_ask.py 2>&1 | head; echo \"--- last commits ---\"; git log --oneline -3 2>&1 | head -5; echo \"--- trailer sample ---\"; git log -1 --format=\"%B\" 2>&1 | tail -8", "description": "Git state of _imports"}

---

> `Bash` -- {"command": "git add brain_temporal.py && git commit -q -F - <<'MSG'\nT09: битемпоральные рёбра и факты второй памяти (brain_temporal)\n\nПолоса ранжирования по времени за флагом BRAIN_TEMPORAL (off|demote|drop),\nclose-don-t-delete и human-edit-wins в turnstate.db, сторож версий, сборка\ntemporal-g

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\ncat brain_temporal.py > \"$S/panel_ctx.txt\"; echo \"=== ВРЕЗКА В brain_ask.dedup_best_p

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== derived_writers: наш счётчик в синкаемой ~/.claude ===\"; \"$PY\" /e/Obsidian/_imports/sync/derived_writers.py --check 2>&1 | tail -6; echo \"EXIT=${PIPESTATUS[0]}\"\necho; echo \"=== есть ли _counters 

---

> `Bash` -- {"command": "head -40 /e/Obsidian/_imports/sync/derived_writers.json", "description": "Registry format"}

---

**Claude:**

Счётчик кладу в синкаемую папку одним именем на все узлы — это тот самый класс `shared-writers`. Делаю имя пер-узловым и регистрирую:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "COUNTER = Path(os.path.expanduser('~')) / '.claude' / '_counters' / 'brain_temporal.jsonl'", "new_string": "def _node():\n    return os.environ.get('COMPUTERNAME') or os.environ.get('HOSTNAME') or 'unknow

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        row = {'ts': now_utc(), 'node': os.environ.get('COMPUTERNAME') or 'unknown',\n               'actor': 'robot-or-session', 'event': event, 'outcome': outcome}", "new_string": "        row = {'ts': 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\sync\\derived_writers.json", "old_string": "    \"_session-archive/run.log\",\n    \"scripts/_shared/_last_run.json\"\n  ],", "new_string": "    \"_session-archive/run.log\",\n    \"scripts/_shared/_last_run.json\",\n    \"_counters/brain_

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\nrm -f /c/Users/dev/.claude/_counters/brain_temporal.jsonl\n\"$PY\" /e/Obsidian/_imports/sync/derived_writers.py --check 2>&1 | tail -3; echo \"EXIT=${PIPESTATUS[0]}\"\n\"$PY\" brain_temporal.py sync 2>&1 | tail 

---

> `Bash` -- {"command": "tail -30 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/panel.log\" 2>&1", "description": "Check panel progress"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/cc-review/secondop.py --help 2>&1 | grep -iE \"context|file|panel|engine\" | head -20", "description": "secondop args for context file"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\run_panel.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Запустить панель второго мнения по T09, положив в контекст ЖИВОЙ КОД горячих участков\n(а не переск

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"; nohup \"$PY\" \"$S/run_panel.py\" > \"$S/panel2.log\" 2>&1 & echo \"pid $!\"", "descript

---

> `Bash` -- {"command": "until grep -qE \"rc = |Traceback\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/panel2.log\" 2>/dev/null; do sleep 15; done; head -60 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/a09aed

---

**Claude:**

Панель (3/3) нашла настоящие дефекты, три из них назвали ≥2 движка. Чиню:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def now_utc():\n    return datetime.datetime.now(datetime.timezone.utc).strftime('%Y-%m-%dT%H:%M:%SZ')", "new_string": "def now_utc():\n    \"\"\"Отметка НАБЛЮДЕНИЯ с МИКРОСЕКУНДАМИ. Секундной точности ма

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    out = set()\n    try:\n        out = {r[0] for r in con.execute(\n            \"SELECT DISTINCT stem FROM brain_facts WHERE (valid_to IS NULL OR length(valid_to)=0) AND (\"\n            \"(key='status

---

**Claude:**

Теперь инвалидация кэша (её назвали все три движка):

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "_CLOSED_CACHE = {}", "new_string": "_CLOSED_CACHE = {}\n\n\ndef cache_clear():\n    \"\"\"Сбросить кэш закрытых стемов. Зовётся ЛЮБОЙ записью (sync, set_fact): иначе\n    долгоживущий процесс (ask_server,

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    con.commit()\n    count('sync', 'files=%d edges_new=%d edges_closed=%d facts_new=%d facts_closed=%d human_kept=%d'", "new_string": "    con.commit()\n    cache_clear()\n    count('sync', 'files=%d edg

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    con.execute('INSERT INTO brain_facts(stem,key,value,valid_from,valid_to,observed_at,'\n                'last_seen_at,status,source_kind,evidence) VALUES(?,?,?,?,NULL,?,?,?,?,?)',\n                (ste

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "def set_fact(stem, key, value, actor='human', con=None, evidence=''):", "new_string": "def set_fact(stem, key, value, actor='human', con=None, evidence='', _norm=True):"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    own = con is None\n    con = con or db()\n    ensure_schema(con)\n    now, day = now_utc(), today()\n    for vf, oa in con.execute('SELECT valid_from, observed_at FROM brain_facts WHERE stem=? '", "ne

---

**Claude:**

Счётчик — честная метка, и снимаю рассинхрон флага во врезке:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        if dead and not _CLOSED_CACHE.get('counted'):\n            # один раз на процесс: полоса реально ПОДВИНУЛА выдачу, а не просто была включена\n            _CLOSED_CACHE['counted'] = True\n         

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_ask.py", "old_string": "    seen, out = set(), []\n    for i, sc in scored:\n        p = meta[i]['path']\n        if p in seen: continue\n        seen.add(p); out.append((i, sc))\n        if len(out) >= topn and os.environ.get('BRAIN

---

**Claude:**

Добавляю тесты на все находки панели (T9–T12) и мутант для красноты:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        con.close()\n    finally:\n        os.environ.pop('BRAIN_TEMPORAL_TODAY', None)", "new_string": "        # ---- T9: две записи в ОДНУ секунду не оставляют факт без живой версии\n        # (п

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -18", "description": "Run tests with panel-driven cases"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - <<'PYEOF'\nimport io\nP = r'D:\\Vault\\_imports\\brain_temporal.py'\ns = io.open(P, encoding='utf-8').read()\nsubs = [\n (\"\"\"    return datetime.datetime.now(datetime.timezone.utc).strftime('%Y-%m-

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    второго мнения 17.09 (Grok #1 и Gemini #5 независимо), закрыто тестом T9.\"\"\"\n    return datetime.datetime.now(datetime.timezone.utc).strftime('%Y-%m-%dT%H:%M:%S.%fZ')", "new_string": "    второго 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "    движка панели 17.09 независимо — единственная находка, которую назвали ВСЕ.\"\"\"\n    _CLOSED_CACHE.clear()", "new_string": "    движка панели 17.09 независимо — единственная находка, которую назвали

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "        out = {r[0] for r in con.execute(\n            \"SELECT DISTINCT lower(stem) FROM brain_facts \"\n            \"WHERE (valid_to IS NULL OR length(valid_to)=0) AND (\"", "new_string": "        out 

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== чистый ===\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -2\nfor m in second cache case delete order; do printf \"=== мутант %-7s: \" \"$m\"; BRAIN_TEMPORAL_MUTANT=$m \"$PY\" _test_brain_temporal.py 2>

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        bt.set_fact('MiXeD-Case', 'status', 'superseded', actor='human', con=con)\n        cl11 = bt.closed_stems(con=con, fresh=True)\n        chk('T11 регистр не ломает closed_stems', 'mixed-case'

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== чистый ===\"; \"$PY\" _test_brain_temporal.py 2>&1 | grep -cE \"^OK\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -2\nfor m in second cache case delete order; do printf \"%-7s: FAIL=\" \"$m\"; BRAIN_TE

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; for t in _test_brain_ask.py _test_brain_recall.py _test_brain_graph.py _test_brain_lex.py; do printf \"%-24s \" \"$t\"; timeout 600 \"$PY\" \"$t\" 2>&1 | grep -E \"ИТОГ|ok,|PASS|FAIL\" | tail -1; done", "descripti

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" _test_brain_graph.py 2>&1 | tail -3", "description": "brain_graph suite result", "timeout": 600000}

---

**Claude:**

Все соседние полосы целы. Контрольный перепрогон линейки ПОСЛЕ починок панели (второй заход другим составом кода):

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad\"\nBRAIN_TEMPORAL=demote nohup \"$PY\" brain_gold_eval.py --run --gold eval/gold-2026-09-16

---

> `Bash` -- {"command": "until grep -qE \"ЛИНЕЙКА второй памяти|Traceback|RuntimeError\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/b5_recheck_demote.log\" 2>/dev/null; do sleep 15; done; grep -vE \"Loading weights|it/s|/184\" \"C:/Use

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" brain_temporal.py dupes --scores eval/scores-20260917-0019.jsonl 2>&1 | head -2; \"$PY\" brain_temporal.py watch 2>&1 | tail -4; echo \"WATCH_EXIT=${PIPESTATUS[0]}\"", "description": "Dupes on recheck scor

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\add_panel_round.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Дописать в карточку T09 раунд панели второго мнения и контрольный перепрогон.\"\"\"\nimport i

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/add_panel_round.py\" 2>&1 | tail -2; \"$PY\" /c/Users/dev/.claude/scripts/status_cl

---

> `Bash` -- {"command": "git add brain_temporal.py _test_brain_temporal.py brain_ask.py sync/derived_writers.json && git commit -q -F - <<'MSG'\nT09: починки по находкам панели второго мнения + тесты T9-T12\n\nobserved_at с микросекундами (факт не остаётся без живой версии при двух записях\nв одну секунду), cac

---

> `Bash` -- {"command": "git add brain_temporal.py _test_brain_temporal.py brain_ask.py && git commit -q -F - <<'MSG'\nT09: починки по находкам панели второго мнения + тесты T9-T12\n\nobserved_at с микросекундами (факт не остаётся без живой версии при двух записях\nв одну секунду), cache_clear() из sync/set_fac

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/change_ledger.py add --actor \"claude\" --operator \"dev\" --session \"AUTO-hub-sm-T09\" --tool \"Claude Code / claude-opus-5\" --target \"D:/Vault/_imports/sync/derived

---

**Claude:**

Закрываю ON AIR и сверяю последний штрих — карту покрытия детали:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/coverage_map.py 2>&1 | grep -iE \"brain_temporal|ИТОГ|покрыт\" | head -6", "description": "Coverage map for the new detail"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" onair.py close --zone vault-imports/brain-temporal 2>&1 | tail -3; \"$PY\" onair.py list 2>&1 | head -5", "description": "Close ON AIR declaration"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" onair.py close 2>&1 | tail -3; \"$PY\" onair.py list 2>&1 | head -4", "description": "Close own ON AIR"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" onair.py close 2026-09-16T221203Z-HUB-01-a09aedcd-vault-imports-brain-temporal 2>&1 | tail -2; \"$PY\" onair.py list 2>&1 | head -4", "description": "Close ON AIR by id"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/coverage_map.py 2>&1 | tail -8", "description": "coverage_map output"}

---

> `Bash` -- {"command": "grep -n \"brain_temporal\" /e/Obsidian/Vault-Knowledge/00-System/Coverage-Map.md 2>&1 | head -4; echo \"--- явные пути (страховка) ---\"; ls -l --time-style=+%H:%M D:/Vault/_imports/brain_temporal.py D:/Vault/_imports/_test_brain_temporal.py | awk '{print $6, $7}'; head -3 E:/Obsi

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "ВАЖНО: звать ТОЛЬКО интерпретатором PYTHON_EXE из ~/.claude/machine.env (грабля T01:\nbrain_ask при импорте делает os.execv, чужой python даёт мгновенный exit 0 и пустоту).\n\"\"\"", "new_string": "ВАЖНО:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" _test_brain_temporal.py 2>&1 | tail -2; \"$PY\" brain_temporal.py status 2>&1 | tail -6; git add brain_temporal.py && git commit -q -m \"T09: паспорт детали в docstring (кто дёргает, рельса, тест, счётчик,

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" _test_brain_temporal.py 2>&1 | tail -2 && \"$PY\" brain_temporal.py status 2>&1 | tail -6 && git add brain_temporal.py && git commit -q -m \"T09: паспорт детали в docstring (кт

---

**Claude:**

Два вердикта о скиллах (§9.3-бис) — первый чиню сразу, боль была пережита в этом заходе:

---

> `Bash` -- {"command": "grep -n \"help_flag_lint.py --check\" /c/Users/dev/.claude/skills/tt/SKILL.md | head -3; grep -n \"context CONTEXT\\|--context \\\"\" /c/Users/dev/.claude/skills/tt/SKILL.md | head -3", "description": "Locate the stale lines in the /tt skill"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\tt\\SKILL.md", "old_string": "тронул/собрал скрипт, который читает аргументы → `python ~/.claude/scripts/help_flag_lint.py --check <путь>`.", "new_string": "тронул/собрал скрипт, который читает аргументы → `python ~/.claude/scri

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\tt\\SKILL.md", "old_string": "⭐ В `--context` кладём ПЕРВОИСТОЧНИК — живой код горячих участков (или файлы целиком), не свой пересказ;", "new_string": "⚠️ ЛИМИТ КОМАНДНОЙ СТРОКИ (замер 17.09, T09): `--context` уезжает АРГУМЕНТОМ

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/change_ledger.py add --actor \"claude\" --operator \"dev\" --session \"AUTO-hub-sm-T09\" --tool \"Claude Code / claude-opus-5\" --target \"C:/Users/dev/.claude/skills/tt/

---

> `Bash` -- {"command": "date -u +\"UTC %H:%M\"; TZ=Europe/Lisbon date +\"Лиссабон: %A, %H:%M, %d.%m.%Y\"", "description": "Clock for the timestamp"}

---

**Claude:**

🕐 **четверг, ночь, 00:25, 17 сентября 2026**

# T09 — битемпоральные рёбра: сделано, вердикт МЕРЖ ЗА ФЛАГОМ

## Премисса сида протухла наполовину, и это пришлось замерить первым делом

Сид велел набрать temporal-gold «из `superseded_by`/`refuted_by` в 01-Rules и памяти». Замер по диску:

* `D:\Vault\Vault-Knowledge\01-Rules\` существует и содержит **0** md-файлов;
* в памяти (955 файлов) `superseded_by` встречается **0** раз, хоть одно эпистемическое поле есть у **4** файлов;
* ни один из этих двух источников вообще **не в индексе** (0 чанков), то есть gold оттуда мерил бы дыру индекса, а не recall.

Решил сам (обратимое, кофаундерский блок): набрал набор по **всему индексу** (7844 файла, 165 из них несут `superseded_by`). T07 и T08 обе `done`, это в премиссе подтвердилось.

## Две таблицы линейки

Оба плеча свежие, на **своём снимке индекса** `eval/snap-t09.npy` (24 261 чанк). Снимок понадобился потому, что боевой индекс за ночь двигался трижды: 24 239 → 24 253 → 24 257 → 24 261 (инкрементальный реиндекс в 23:38 прошёл прямо во время первого прогона).

**Замороженный gold-2026-09-16, 184 вопроса, режим vector:**

| класс | n | ДО (`off`) R@12 / nDCG@12 | ПОСЛЕ (`demote`) R@12 / nDCG@12 | Δ nDCG |
|---|---|---|---|---|
| title | 60 | 0.950 / 0.927 | 0.950 / **0.915** | **−0.012** ⛔ выше порога 0.01 |
| body | 60 | 0.850 / 0.640 | 0.850 / 0.634 | −0.006 |
| bridge | 60 | 0.338 / 0.223 | 0.338 / 0.223 | 0.000 |
| temporal (старый, n=4) | 4 | 1.000 / 0.638 | 1.000 / **0.875** | **+0.237** |
| ru / en | 147 / 37 | 0.687 / 0.847 | 0.687 / 0.847 | ru −0.003, en +0.011 |

**Recall@12 не сдвинулся ни на одном классе.** Ранжирование вниз меняет МЕСТО ответа, а не факт его попадания в дюжину, и это ровно та разница между `demote` и `drop`, из-за которой `drop` нельзя ставить дефолтом.

**Новый temporal-gold, 41 вопрос** (22 по заголовку + 19 по первому абзацу, 22 ребра; файл `eval/gold-temporal-2026-09-16.jsonl`, основной gold не тронут):

| | R@12 | MRR | nDCG@12 |
|---|---|---|---|
| ДО (`off`) vector / graph | 0.805 / 0.854 | 0.486 / 0.500 | 0.575 / 0.598 |
| ПОСЛЕ (`demote`) vector / graph | 0.805 / 0.854 | **0.658 / 0.682** | **0.705 / 0.736** |
| Δ | 0 | +0.172 | **+0.130 / +0.138** |

Порог класса (R@12 ≥ 0.60) пройден: 0.805. `drop` на этом наборе даёт те же числа, что `demote`, то есть выбрасывать закрытые незачем.

**Дубли версий одной сущности в top-12** (второй критерий приёмки, прибор `brain_temporal.py dupes`): **14 из 184 = 7.61% → 9 из 184 = 4.89%**, порог 5% пройден.

## Вердикт и почему дефолт не переключён

✅ **МЕРЖ ЗА ФЛАГОМ `BRAIN_TEMPORAL=off|demote|drop`, дефолт `off`.**

Единственный класс за порогом отката: title, −0.012. Это не баг полосы, а свойство данных. У **трёх** вопросов замороженного gold правильный ответ сам закрыт:

* `title-009` и `body-006` → `decision-config-memory-github-remote-2026-06-28`, `status: superseded`;
* `bridge-021` → `insight-dr-...-hf-hiring-lever`, `valid_to: 2026-09-04`.

Жёсткий фильтр `valid_to IS NULL` из ТЗ обнулил бы эти три вопроса по построению, поэтому отсев запрещён, а вопрос «найди заметку с таким заголовком» законно хочет старую заметку. Вывод: временная полоса это режим для вопросов «что верно СЕЙЧАС», а не глобальный дефолт. Живой пример на `title-009`: до полосы на первом месте стояла закрытая заметка, после полосы первой стала её замена.

## Что построено

`D:\Vault\_imports\brain_temporal.py`: `sync` (диск → БД), `status`, `closed`, `set`, `watch`, `gold`, `dupes`, `selftest`. В `turnstate.db` сейчас **69 796 живых рёбер**, **1867 живых фактов**, таблица конфликтов. Колонки взяты у `memory_epistemic.py` буква в букву (`status/valid_from/valid_to/superseded_by/refuted_on/refuted_by`) плюс `observed_at` (когда МЫ увидели) и `source_kind` (machine|human). `observed_at` входит в первичный ключ, иначе правка в тот же день затирала бы только что закрытую строку и close-don't-delete держался бы на словах.

Врезка в конвейер одна: `brain_ask.dedup_best_per_file`. Её зовёт и бой, и линейка, поэтому мерился конвейер, а не его пересказ. Порядок: дедуп → время → обрезка topn.

`_test_brain_temporal.py`: **47 проверок**, T1…T12.

## Красный тест

Мутанты живут в самом модуле, чтобы доказательство воспроизводилось:

| мутант | что ломает | FAIL |
|---|---|---|
| `delete` | закрытие превращается в DELETE | 8 |
| `order` | demote не двигает закрытые | 3 |
| `second` | `observed_at` обратно в секунды | 3 |
| `cache` | кэш закрытых не сбрасывается | 2 |
| `case` | стем из базы без `lower()` | 1 |

Чистый прогон: ALL PASS, exit 0. Соседние полосы после правки `brain_ask`: `_test_brain_ask` 61 PASS, `_test_brain_recall` 18 ok, `_test_brain_graph` 24/0, `_test_brain_lex` PASS.

## Вторая находка в данных, из-за которой я спорил с ТЗ

`supersedes` у НОВОЙ заметки это **не** закрытие старой. В волте это поле сплошь про ПУНКТ:

> `decision-config-portability-chezmoi-rejected.supersedes` = «clause «chezmoi = ЦЕЛЬ» в `[[decision-unified-multi-machine-platform]]` §Решение п.2»

а сама platform-заметка `status: accepted` и жива. Широкий проход давал 30 пар, 53 вопроса и «8 незакрытых версий», и если бы я пошёл их закрывать, я записал бы в волт ложь. Строгий сигнал (объявление у самой старой заметки) даёт 22 пары, 41 вопрос и **1** честный красный случай: `task-2026-07-28-onboard-dima-petya-starter-kit` → `task-2026-08-19-first-external-install-proof`. Семь clause-подсказок сторож печатает отдельным списком и красным не считает.

## Панель второго мнения нашла 5 дефектов в моей же починке

3 из 3 headless-рельс ответили за 107 с на живом коде горячих участков.

| находка | кто назвал | чем закрыто |
|---|---|---|
| кэш закрытых не сбрасывается при записи | **все трое** | `cache_clear()` из `sync`/`set_fact`, тест T10, мутант `cache` |
| две записи в одну секунду: старую закрыли, новую отбил `INSERT OR IGNORE`, факт без живой версии | Grok + Gemini | микросекунды в `observed_at`, тест T9, мутант `second` |
| стем в базе не в нижнем регистре, закрытая заметка не опускается никогда | Codex + Gemini | `lower(stem)` плюс нормализация в `set_fact`, тест T11, мутант `case` |
| две правды о режиме (env во врезке против `mode()` в полосе): `drop` возвращал меньше дюжины | Grok + Gemini | режим считается один раз одной переменной, тест T12 |
| счётчик пишет один раз на процесс, занижает использование | Gemini | оставлено осознанно, но занижение названо в самой строке: `scope=first-hit-per-process` |
| конкурентные `sync` могут положить две живые версии | Codex + Grok | не чинил, назвал пределом |

После починок линейка перепрогнана и воспроизвела таблицу ПОСЛЕ до третьего знака (`scores-20260917-0019.jsonl`), дубли независимо пересчитаны на новом файле: снова 4.89%.

## Находка про ПРИБОР, важная для T05

Режим переигрывания линейки (`--candidates`) даёт **не те** числа, что свежий прогон на том же индексе и том же gold:

* off + fresh: title 0.950, body 0.850, bridge 0.338
* off + replay: title 0.933, body 0.767, bridge 0.225

Моя первая версия таблицы ПОСЛЕ была снята в replay и выглядела катастрофой (body −0.100, bridge −0.113). Контрольный прогон off+replay показал, что виноват режим, а не полоса. T05 сравнивает реранкеры именно в replay: его A/B внутренне честен (оба плеча в одном режиме), но абсолютные числа с baseline сравнивать нельзя. Класс `replay-mode-not-equal-fresh`, случай 1, в 03 предупредил.

Мелочь оттуда же: `scores-*` называются с точностью до минуты, два прогона в одну минуту затирают друг другу ranked-списки (числа выживают в `gold_eval`).

## Честные пределы

* Полоса меряется на **23 закрытых заметках** из 7846, сигнал редкий; +0.130 nDCG на 41 вопросе это ещё не статистика.
* `sync` **не** поставлен в ночную рутину осознанно: пока флаг выключен, устаревать нечему. Включение дефолта обязано идти пакетом с «`sync` перед ночной линейкой».
* Не проверено: два писателя в БД одновременно; закрытие фактов при удалении файла целиком (стем уходит из scope); полоса на другом узле (раздачи не было, дефолт off, раздавать нечего); `drop` на основном gold.
* Грабля, которую поймал мой же тест: в `brain_facts` есть колонки `status`/`value`/`valid_to`, поэтому SQL вида `key="status"` SQLite читает как сравнение **двух колонок** и молча отдаёт пусто. Все литералы переведены на одинарные кавычки и `length()`.

## Доклад развезён

Карточка `task-2026-09-16-sm-T09-bitemporal-edges` → `done`, 136 строк с обеими таблицами и якорями строк `gold_eval`. Строка 9 в программной карточке обновлена. Google-таблица, вкладка «План 2 нед», колонка «Состояние» (было `⚪`). Строка в TG-03 доехала (id 1898817, полный текст; упал только бот-дубль по длине). Коммиты с трейлерами: `9590f951`, `8fd66f2c`, `d6c8fa10`, провенанс-линт 0 нарушений. Счётчик зарегистрирован как `per_node` в `derived_writers.json` плюс строка в change_ledger. ON AIR закрыт. Преемник **T10 поднят** (сессия `48a2c10b`, уже держит свою зону `vault-imports/eval-module`).

## Вердикты о скиллах (§9.3-бис)

🔧 **обновил `/tt` в этом же заходе**, две пережитые боли: у `help_flag_lint.py` нет флага `--check` (линт сам отбил его как неизвестный аргумент, живые флаги `--json|--list|--accept|--prune`), и у `secondop panel --context` есть лимит командной строки Windows (43 КБ упали с `Argument list too long`, влезло 13.6 КБ горячих функций). Обе правки в скилле, строка в леджере.

📝 **свою инструкцию (сид T09) не переписываю**, причина: сиды на эту программу больше не рождаются, T10 последний, а урок про протухшую премиссу лёг туда, где его прочтут, то есть в программную карточку строкой про 01-Rules и память.

---

🧒 **Простыми словами:** заметки в твоём волте умеют говорить «меня заменили на другую». Раньше поиск этого не читал и мог показать старое правило рядом с новым. Теперь у каждой связи и у каждого такого признака есть два времени: когда это было правдой в жизни и когда мы это увидели, а старое не стирается, а закрывается датой. Плюс появился рубильник: включишь, и закрытые заметки уезжают в конец выдачи. На вопросах «что тут теперь правда» стало заметно лучше, а на вопросе «найди заметку с таким заголовком» чуть хуже, потому что там как раз хотят старую. Поэтому рубильник поставлен, но по умолчанию выключен, и это твоё решение когда включать. Ещё я попросил три чужих ИИ поломать мою же работу, они нашли пять дыр, я их закрыл и перемерил: числа те же. И набор проверочных вопросов про время вырос с 4 до 41, потому что на четырёх ничего доказать нельзя.

---

**User:**

Stop hook feedback:
СТОП: ты выносишь вердикт о СПОСОБНОСТИ движка, не обойдя все его копии.
  фрагмент: …**обновил `/tt` в этом же заходе**, две пережитые боли: у `help_flag_lint.py` нет флага `--check` (линт сам отбил его как неизвестный аргумент, жив…

Класс замерен 04.08: «у approval_clock нет команды place» объявлено по ДВОЙНИКУ
из _scratch (30 962 б), пока канон-движок с place (46 106 б) лежал в _imports.
Цена: ложный вывод «канон врёт» ушёл оператору и в два артефакта.

Сделай ДО вывода:
    python ~/.claude/scripts/copy_sweep.py <имя-движка>
Он обойдёт ВСЕ корни (включая _scratch и бэкапы), покажет копии с размерами
и назовёт, если они разные. Вердикт «команды нет» законен только по КАНОН-копии.
Если про конкретный файл и ты его сам открыл — назови ПУТЬ в вердикте:
«в <путь> команды X нет» (per-копия), а не «движок не умеет» (про весь мир).

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/copy_sweep.py help_flag_lint 2>&1 | head -20", "description": "Copy sweep for help_flag_lint"}

---

**Claude:**

Хук прав: копии разные. Проверяю, есть ли `--check` в БОЛЬШЕЙ версии, прежде чем судить:

---

> `Bash` -- {"command": "for f in \"/c/Users/dev/.claude/scripts/help_flag_lint.py\" \"/c/Users/dev/.claude/scripts/help_flag_lint.sync-conflict-20260915-214318-4YSJ7MU.py\" \"/e/Obsidian/Vault-Knowledge/_machine-bus/_transit/scripts-from-NODE-0X-2023PAL/help_flag_lint.py\"; do echo \"=== $f\"; grep -oE '\"

---

**Claude:**

`--check` ЕСТЬ, но в другой копии. Разбираюсь, какая канон, прежде чем что-то утверждать:

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude && git log --oneline -6 -- scripts/help_flag_lint.py 2>&1 | head -8; echo \"=== diff размеров по коммитам ===\"; git log --format=\"%h %ad\" --date=short -3 -- scripts/help_flag_lint.py 2>&1 | head; echo \"=== что делает --check в большой копии ===\"; grep -n -

---

**Claude:**

Разобрался: `--check` это фича от 03.09 под шаг 3.5 `/tt`, и **канон это большая копия**. На хабе работает августовская версия, потому что sync-конфликт 15.09 не разрешили. Мой вердикт был про копию, не про движок — откатываю правку скилла и чиню настоящую поломку:

---

> `Bash` -- {"command": "grep -nE \"^# updated|updated:|ВЕРСИЯ\" /c/Users/dev/.claude/scripts/help_flag_lint.py /c/Users/dev/.claude/scripts/help_flag_lint.sync-conflict-20260915-214318-4YSJ7MU.py 2>/dev/null | head -6; echo \"=== секция G в тесте ===\"; grep -c \"check\" /c/Users/dev/.claude/scripts/_tes

---

> `Bash` -- {"command": "ls -l /c/Users/dev/.claude/scripts/_test_help_flag_lint.py 2>&1 | head -2; grep -nE \"def t_g|--check\" /c/Users/dev/.claude/scripts/_test_help_flag_lint.py 2>/dev/null | head -8", "description": "Does the local test require --check"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; grep -c \"check\" /c/Users/dev/.claude/scripts/_test_help_flag_lint.py; grep -n \"check\" /c/Users/dev/.claude/scripts/_test_help_flag_lint.py | head -6; echo \"=== прогон теста на ТЕКУЩЕЙ копии ===\"; \"$PY\"

---

> `Bash` -- {"command": "ls -l /e/Obsidian/Vault-Knowledge/_machine-bus/_transit/scripts-from-NODE-0X-2023PAL/_test_help_flag_lint.py 2>&1 | head -2; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; cd /c/Users/dev/.claude/scripts && cp help_flag_lint.py help_flag_lint.py.bak-pre-T09-

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; cd /c/Users/dev/.claude/scripts\necho \"=== старый тест на НОВОМ движке (baseline был PASS 29 / FAIL 1) ===\"; \"$PY\" _test_help_flag_lint.py 2>&1 | tail -3\ncp _test_help_flag_lint.py _test_help_flag_lint.py.b

---

> `Bash` -- {"command": "mv help_flag_lint.sync-conflict-20260915-214318-4YSJ7MU.py help_flag_lint.py.resolved-into-canon-20260917 && ls -l help_flag_lint* | awk '{print $5, $6, $7, $9}'; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" copy_sweep.py help_flag_lint 2>&1 | grep -

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\tt\\SKILL.md", "old_string": "тронул/собрал скрипт, который читает аргументы → `python ~/.claude/scripts/help_flag_lint.py --list` и найди в выводе свой файл (⚠️ 17.09: флага `--check` у линта НЕТ — сам линт отбивает его как неи

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\n\"$PY\" /c/Users/dev/.claude/scripts/selfheal.py journal --class sync-conflict-left-node-on-stale-copy --what \"sync-конфликт 15.09 откатил help_flag_lint.py на хабе к августовской копии (23393 б, без --check), 

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/prior_art.py class \"синк-конфликт оставил узел на старой копии кода\" 2>&1 | tail -14", "description": "Family count for the class (§5.10)"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/selfheal.py journal --help 2>&1 | head -18", "description": "selfheal journal flags (rename/merge?)"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/selfheal.py journal --class sync-resolves-conflict-to-older-version --what \"2-й датированный случай СЕМЬИ (1-й: 16.09 ретро-рутина, тот же инцидент синка 15.09 21:43): на ха

---

> `Bash` -- {"command": "grep -rln \"sync-conflict-left-node-on-stale-copy\" /e/Obsidian/Vault-Knowledge/00-System/ 2>/dev/null | head -3; grep -n \"sync-conflict-left-node-on-stale-copy\" /e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md 2>/dev/null | head -2 | cut -c1-160", "description": "Find my jou

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/breakage.py count --class sync-resolves-conflict-to-older-version 2>&1 | tail -3; \"$PY\" /c/Users/dev/.claude/scripts/breakage.py count --class sync-conflict-left-node-on-

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/change_ledger.py add --actor \"claude\" --operator \"dev\" --session \"AUTO-hub-sm-T09\" --tool \"Claude Code / claude-opus-5\" --target \"C:/Users/dev/.claude/skills/tt/

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_a8ad786a\\scratchpad\\add_correction.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Поправка в карточку T09: вердикт о скилле был про отставшую копию, а не про движок.\"\"\"\nimp

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_a8ad786a/scratchpad/add_correction.py\" 2>&1 | tail -2; \"$PY\" /c/Users/dev/.claude/scripts/status_cla

---

**Claude:**

🕐 **четверг, ночь, 00:40, 17 сентября 2026**

# Поправка к моему же вердикту (её поймал стоп-хук, и он был прав)

Я написал «у `help_flag_lint.py` нет флага `--check`, скилл `/tt` врёт» и успел снять `--check` из шага 3.5. Это был вердикт о способности движка, вынесенный по одной копии.

`copy_sweep.py help_flag_lint` показал **15 копий с РАЗНЫМ содержимым**:

* канон с `--check`: 28 683 б, md5 `f121378d`;
* августовская без него: 23 393 б, md5 `28c0ee39`, и именно она лежала рабочей в `~/.claude/scripts/`.

Дальше картина собралась по фактам диска, а не по догадке. Фичу `--check` дописали **на этом же хабе 03.09** под шаг 3.5 `/tt`: рядом так и лежал её собственный бэкап `help_flag_lint.py.bak-precheck-20260903`. Потом **sync-конфликт 15.09 в 21:43 сделал рабочей августовскую копию**, а каноническую положил рядом файлом `*.sync-conflict-*`, и конфликт никто не разрешил. Узел ослеп на свой же гейт, а скилл для оператора хаба выглядел врущим.

## Что сделано вместо ложной правки

* Правка скилла **откачена**: шаг 3.5 снова требует `--check`, плюс туда дописан диагноз (проверить `copy_sweep`, сверить 28 683 против 23 393) и лечение.
* Каноническая копия поставлена рабочей, старая рядом как `bak-pre-T09-20260917`, конфликтный файл переименован в `help_flag_lint.py.resolved-into-canon-20260917` (ничего не удалял).
* Парный `_test_help_flag_lint.py` из `_transit` поставлен: **PASS 35 · FAIL 1**. Старый тест на новом движке: **PASS 29 · FAIL 1**, то есть ровно прежний baseline, регресса нет. Упавший в обоих случаях `D1 «новых дыр во флоте нет»` был красным и до моей правки, это старый долг флота.
* Гейт прогнан по назначению: `--check D:/Vault/_imports/brain_temporal.py` → **exit 0**, дыры класса `unparsed-flag-silently-runs-work` в моей детали нет. Так шаг 3.5 закрыт честно, а не «пропущен, потому что инструмент не понял флаг».
* Класс записан дверью `selfheal.py journal`, поправка в change_ledger, блок с разбором дописан в карточку T09.

## Честный хвост, который я не заметаю

Счёт семьи разъехался по именам. Тот же инцидент синка 15.09 уже лежит в журнале как `sync-resolves-conflict-to-older-version` (запись ретро-рутины 16.09), моя строка встала как `sync-conflict-left-node-on-stale-copy`, и дверь дедупа слить их не дала, а прямая правка `Breakage-Journal.md` запрещена хуком (правильно запрещена). Фактически это два датированных случая одной семьи под двумя именами: механизма по §5.10 не положено (нужен третий случай), но слияние имён это работа того самого третьего захода. Ровно та грабля, про которую память `class-counted-by-name-never-reaches-three`.

Вердикт по самой задаче T09 не меняется: **МЕРЖ ЗА ФЛАГОМ, дефолт `off`**, числа те же, они перепроверены дважды.

🧒 **Простыми словами:** я сказал «инструмент не умеет такую команду, значит инструкция врёт». Сторож меня остановил и правильно: таких файлов на компьютере пятнадцать штук, и они разные. Оказалось, команда есть, просто нашему компьютеру две недели назад синхронизация подсунула старую версию файла вместо новой, а новую положила рядом и никому не сказала. Я вернул новую на место, проверил тестами (35 из 36, последний был красным и до меня), а свою поспешную правку инструкции отменил, чтобы неправда не уехала на все компьютеры.

---

**User:**

<task-notification>
<task-id>bxolzh1ix</task-id>
<tool-use-id>toolu_01JYY3ngJursJWK1WQ4trnh2</tool-use-id>
<status>stopped</status>
<summary>No completion record was found for this background shell command from the previous session. It may have been stopped (via the UI, Monitor timeout, or agent teardown — these leave no transcript marker), or it may have been running when the previous Claude Code process exited. Check the output file for partial results before assuming it completed.</summary>
</task-notification>

---

**User:**

ретро

---

> `Skill` -- {"skill": "retro", "args": "сессия T09 битемпоральные рёбра, хаб HUB-01"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

**⏳ Measure the time-gap FIRST.** Check when this session's work actually happened (turnstate ledger / the digest's day-span) vs **now**. Old session → widen every lookup below to cover *"what changed SINCE"* — don't recall only the session's own window.

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2а. **Робот уже сделал ретро этой сессии? (0 tok):** `ls ~/.claude/logs/retro_lost_done/ | grep <sessionId>` — маркер есть → ночной `retro-lost` уже разобрал сессию (заметка `Retros/retro-lost-<дата>-<узел>-*.md`, единица с твоим sid). Тогда твоё ретро = ДЕЛЬТА поверх неё (живая сверка «что изменилось с тех пор» + компакт), с перекрёстной ссылкой, а не второй полный разбор. Замер 15.09.2026: сессия 07–08.09 получила лайт-ретро робота утром 15.09, живое ретро вечером чуть не переписало всё заново.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
2в. **Рутина бежала или нет — только СЧЁТЧИК ПРОГОНОВ, НЕ наличие файлов (0 tok):**
   `python ~/.claude/scripts/routine_cost_audit.py --days <N>` -> колонка «прог.».
   Выход рутины пишется НЕ каждый прогон (у `pipe-a-inbox-watch` отчёт рождается только в дни
   с живыми письмами), поэтому «файла за 11.09 нет» не значит «11.09 не работала». Замер 15.09:
   объявил оператору 4 пропуска подряд, счётчик показал 8 прогонов за 9 дней — вывод был ложный
   и уже озвучен. Семья класса «судим по побочному следу вместо счётчика самой работы» насчитывает
   6 прежних случаев (ближайший 20.08: опись судила mtime заявленного stdout вместо факта работы),
   так что механизм тут не нужен — нужен ПОРЯДОК: счётчик первым, файлы вторыми.
   Канон: [[instrument-is-a-claim-too]], CLAUDE.md §5.4.
3. **Neighboring chats (lexical, 0 tok):** `/search <topic words>` (search_catalog.db, ~99k Telegram/FB/ChatGPT/Claude) — what did dev or another session **dictate elsewhere** about this topic?
4. **Vault meaning (RAG):** `/ask <topic>` (`$IMPORTS_ROOT/brain_ask.py`) — what does the Second Brain already hold / already decide on this?
5. **Memory + vault grep** for every rule/concept/decision this session touched — already captured? **superseded / changed** since?
6. **Peers & cross-machine:** `/inbox` + `_machine-bus` + consensus commits — "всё, о чём мы договорились" on the OTHER machines; did a peer already decide, or undo, this?
7. **Declined journal:** skill `/declined` — did we already reject something this session quietly re-did?

**Attribution guard:** the Step-1 inventory is machine-wide and WILL include other sessions' artifacts (skills/scripts/commits from the fleet). Treat anything NOT created in THIS conversation as **someone else's** — flag it, never claim or re-route it.

**Output of Step 0 — one tight «🔎 сверка» block up front** (checked + verdict):
- **checked:** what I actually looked at (N retros / chats / vault / peers).
- **✅ aligned** — this session's calls match the collaboration; or
- **⚠️ drift** — session did X but [[note/decision]] elsewhere says Y (superseded / contradicts / already undone) → flag for dev; or
- **🔗 to propagate** — session's durable work not yet in vault / peers / Bible → route it in Step 4.
If a parallel session already captured the durable item, **SKIP re-capturing** — just cross-link.

## Step 1 — Inventory (deterministic first; AK-47, ~free)
Ground the recap in facts, not memory alone — run the SHARED inventory script (same one the daily sweep uses, so the logic never drifts):
- `python "$IMPORTS_ROOT/retro_inventory.py" 1`  (arg = days; widen for a multi-day session)
- It prints `BUILT_ARTIFACTS <n>` and writes `$IMPORTS_ROOT/retro_candidates/digest-latest.md` — Read that digest: new/changed **skills**, **_imports scripts/sidecars**, **durable notes** (Protocols + Concepts), and recent **descriptive vault commits**.
- (⚠️ a concurrent Claude-Desktop fleet may interleave vault commits — its are descriptive; the terse `pre-intervention` ones are auto-backups.)
- **Cross-check** with what you (the agent) created/edited in THIS conversation: skills, scripts, vault notes, memory entries, `CLAUDE.md` edits, decisions made, rules captured, things flagged for dev.

## Step 1🧠 — ПАМЯТЬ СЕССИИ: сироты по worktree + машинно-невидимые опровержения (дверь §8.6; добавлена 2026-09-02)
Сессия из worktree пишет память в СВОЮ проектную папку, домашний индекс о ней не знает — замер 02.09 на NODE-0X: 20 таких заметок, одна несла вердикт, опровергнутый через девять дней в соседней папке. Два прогона, 0 LLM, 0 сети:
- `python ~/.claude/scripts/memory_harvest.py --scan` → есть ORPHAN → `python ~/.claude/scripts/memory_harvest.py --harvest` (копия домой + указатель в `MEMORY-archive.md`; оригинал НЕ трогается). Exit 3 = `NEEDS-HUMAN` (тёзки припаркованы, ничего не потеряно) → строкой оператору, не молча.
- ⚠️ **Прибор даёт ложное «чисто» (замер 10.09.2026, NODE-0X):** `--scan` напечатал «0 missing pointer(s) to repair», а указатель на свежую заметку (`zenodo-publish-rail`, дописан 07.09) из `MEMORY.md` за ночь исчез — сироту он не увидел, потому что сверяет не ту пару папок. Поэтому ПОМИМО прогона сверь руками указатели на заметки, которые ЭТА сессия и пара прошлых записали: `grep -c "<слаг>" <проектная-папка>/memory/MEMORY.md` → 0 = дописать строку тем же заходом. Класс = `memory-index-line-lost-overnight`, 4 датированных случая, корень чинится отдельной сессией.
- `python ~/.claude/scripts/memory_inject_lint.py --scan` → анти-инъекция и секрет-паттерны memory-стора (порт bb plugins/memory, 05.09.2026): exit 1 = НОВАЯ находка против baseline — разобрать тем же заходом (чужая закладка? секрет в памяти → в secrets-стор); старый долг молчит ратчетом. Это ЕДИНСТВЕННАЯ дверь линта ([[rule-needs-a-door-quota]]).
- `python ~/.claude/scripts/memory_epistemic.py --lint` → `SELF-TOMBSTONE` (заметка сама пишет, что устарела, а машина этого не видит) закрыть тем же заходом: `--close <слаг> --superseded-by <слаг-преемника>`. Отмена закрывается ПОЛЯМИ (`status`/`valid_to`/`superseded_by`/`refuted_on`/`refuted_by`) во ВСЕХ копиях слага, а не переписыванием одной: CLAUDE.md §8.4-бис + [[memory-records-close-by-fields-not-rewrite]].
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже). Для каждой поломки **СНАЧАЛА**, до выбора имени класса и до записи, найди смысловую семью:
```
python "$HOME/.claude/scripts/prior_art.py" class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ ошибка и НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Если напечатана `СЕМЬЯ <slug>`, используй именно её как `<класс>`. Если показаны прежние строки без известной семьи, бери имя предмета ремонта/нарушенного инварианта из самой ранней строки, не новый синоним. При `exit 0`, когда прежней строки нет, назови класс по текущему предмету ремонта/нарушенному инварианту и запиши как 1-й датированный случай; канал, код возврата, текст алерта и симптом классом не являются.

ТОЛЬКО ПОСЛЕ этого запиши ОДНУ строку через дверь `python "$HOME/.claude/scripts/selfheal.py" journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Счёт бери из фактического ответа `selfheal.py`: дедуп означает, что новой строки нет.

Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный**. Внутри `/retro` причинную цепочку НЕ строй: используй ровно одну отдельную ВИДИМУЮ repair-сессию, чей первый явный вызов — `/five-whys <класс>` в Claude или `$five-whys <класс>` в Codex, с датированными строками серии. Если `selfheal.py` уже поставил её в очередь, вторую не создавай. Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым».
- ⚠️ **Завёл новую семью — обязательна КРАСНАЯ проба в том же заходе** (замер 21.09.2026, NODE-0X, ошибся дважды подряд): широкие ключи (`argv`, `206`, `тело промпта`) намели 77 чужих случаев и прибор объявил «порог §5.10 пройден»; вторая редакция утащила соседнюю семью «передали ПУТЬ вместо тела» — то же лицо, другой корень. Проверка обязана идти в ОБЕ стороны: чужой симптом НЕ ловится (`grep -c` = 0) И свой ловится. Ложно раздутый счётчик хуже отсутствующего: он заказывает сессию починки, которой не нужно быть. Канон: память `class-counted-by-name-never-reaches-three` + CLAUDE.md §5.10.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · соврал сам прибор · fail-closed гейты. Для KEEP-ядра, потери данных, безопасности, денег и совравшего прибора та же отдельная видимая `/five-whys`/`$five-whys`-сессия запускается немедленно; анализ внутри `/retro` не вести.
- ⚠️ **Дедуп двери отбивает УТОЧНЕНИЕ к своему же классу** (замер 10.09.2026, NODE-0X, дважды за один
  заход): `selfheal.py journal` отвечает «СТРОКА НЕ ЗАПИСАНА (дедуп: этот класс уже журналился
  недавно). Поправку к своей строке правь в журнале явно» — а прямая правка `Breakage-Journal.md`
  ЗАПРЕЩЕНА хуком `breakage_write_guard` (см. абзац выше). Инструкция сама себе противоречит.
  Пока корень не починен, обход: уточнение 2-го случая (условия, свежие цифры, порог третьего)
  кладётся в **задачу реестра** класса и в **ретро-заметку**, а в отчёте пишется честно
  «дедуп отбил, уточнение легло в <адрес>». ⛔ Молча проглотить отбой нельзя — иначе
  уточнение условий теряется, и следующая сессия снова считает случай первым.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- Канон: Библия `reglament-mekhanizm-tolko-posle-tretey-polomki` + CLAUDE.md §5.10 + `reglament-pyat-pochemu-koren-po-serii-sessiy` §«Три инструмента»; проверка двери — `python ~/.claude/scripts/rule_home_guard.py mekhanizm-tolko-posle-tretey-polomki`.

## Step 2 — Summarize the arc ("сегодня мы поняли")
3–7 beats: starting idea → what got built → key realizations → what was decided. Honest, concise, his voice. This is the "Stan at the end of South Park" recap.

## Step 2🎙 — Вердикт кофаундера (Майк) — canon 2026-07-07, applied 2026-07-31
Right after the arc, Майк speaks as co-founder — 4 строки, без воды (canon `reglament-*` voice-through-line; восстановлен из потерянного сообщения шины, 23 дня в призраке; НЕ театр — работает ПОВЕРХ механики 28.07: если сессия дала стратегический выбор, мемо/адвокат-дьявола из [[cofounder-decision-artifact-gate]] главнее и уже сделаны):
- 💰 **деньги-линза** — что из сегодняшнего приближает выручку/оффер (цель №1/№2), одной строкой;
- 🔪 **что убил бы** — самая слабая трата времени сессии, которую завтра не повторяем;
- 🤺 **спарринг-аудит** — где я сегодня поддакнул вместо спора (провал роли §1.2) либо «спорил честно»;
- ❓ **вопрос** — один направляющий вопрос оператору на завтра.
Пустышку не писать: сессия чисто механическая без бизнес-среза → строка «🎙 Майк: бизнес-среза нет, чисто инфра» и дальше.

## Step 3 — Classify each artifact (Keep / Drop / Try) + tested? audit
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]).
⭐⭐ **И ВТОРАЯ КОЛОНКА — перепроверено? ✅/❌** (dev 13.09.2026, CLAUDE.md §4.3-бис): «протестировано» и «перепроверено вторым, ДРУГИМ заходом» — разные вещи, и ложное «готово» живёт именно в зазоре между ними. Артефакт, у которого первый прогон зелёный, а второго захода не было, ретро помечает ⚠️, а НЕ ✅, и предлагает прогнать Шаг 4.9 скилла `/tt` сейчас. Замер архива 15.08→14.09: 21 раз за месяц оператор спрашивал «ты точно починил?» сразу после моего «готово». Канон: [[done-is-a-claim-recheck-twice]]. Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3📋 — Journal sync (реестр задач; dev's decree 2026-07-04)
Retro is the SAFETY NET of the task journal ([[task-journal-done-undone-linking]]): the in-session reflex («сформулировал → сразу в реестр») catches tasks at birth; retro catches what slipped. Two moves, both against the ONE journal ([[task-backlog-registry]] — **v2 markdown-first, SHIPPED 2026-07-07**):
- **Источник истины = markdown-заметки** `$OBSIDIAN_VAULT/10-Tasks/task-*.md` (шаблон `_Task-Template.md`, MOC `_Tasks-MOC.md`). Синкаются флоту, поэтому работают с ЛЮБОЙ машины без шины и без движка. Завести задачу = новый файл `task-ГГГГ-ММ-ДД-слаг.md`; закрыть = правка frontmatter (`state`/`status` + evidence). Схема строгая: неизвестный `state`/`prio` → `schema_errors` в аудите, а не тихий дефолт.
- **Витрину и аудит строит индексатор** `tasks_index.py` (markdown → `_Dashboards/Task-Backlog.html` + `10-Tasks/_audit/audit-latest.json`). Он крутится ночью на Маяке как ЕДИНСТВЕННЫЙ писатель — руками на хабе/ноуте его НЕ запускать (два писателя одного синкаемого дерива = sync-conflict).
- ⛔ Старый SQLite-движок task-registry (жил на ноуте NODE-0X) = **аварийный fallback, снят с вооружения**; на хабе его нет и не должно быть. Не зови его и не «восстанавливай» — v2 его заменил. (Имя намеренно без code-формата: backtick = «это надо запускать».)

Две операции ретро:
- **Сессия рождена из сида Task-Now?** (первое сообщение начинается «Продолжи задачу task-…» или «Реши СУДЬБУ задачи task-…») → обнови frontmatter ЭТОЙ задачи прямо сейчас: state/touched_at, при done — evidence+outcome; сид без обновлённого frontmatter = петля Task-Now разорвана (v4, dev 2026-08-20).
- **Closed this session** → mark `done` **with evidence** (the /tt proof, commit, counter) + link what it unblocked. Claimed-done without proof → flag, don't close.
- **Still open** (every «📌 Open item», seed prompt, deferred tail, «потом») → ensure it EXISTS in the registry with a link to where it was born + prio/type. Nothing from the open-items list may live only in the chat transcript.
- ⏱ **РАЗРЕЗ ОЖИДАНИЯ (добавлено 07.09 после того, как этот шаг сам породил долг):** у каждого открытого пункта вида «ждём замера / ещё копим / не проверено» спроси — **какая его часть НЕ требует времени?** Почти всегда внутри склеены два вопроса: УСТРОЙСТВО («работает ли конструкция») проверяется детерминированным прибором за минуты, СПРОС («пользуемся ли мы этим») действительно требует недель. Часть про устройство закрывается **в этом же заходе**, а не переносится в реестр. Замер, из-за которого пункт появился: ретро 06.09 записало «гипотеза ДР не проверена, урожай 08.09» — на деле 5 ног гипотезы закрылись прибором за пару минут 07.09, а ждать надо было только спроса. Обязательные подпорки при таком закрытии: **красный контроль** (зелёная нога пустая, пока не показано, что прибор видит поломку) и **независимая линза чужим кодом**, если вывод тебе выгоден. Канон: память [[architecture-proves-in-minutes-demand-needs-weeks]], CLAUDE.md §5.4.
Announce the delta in one line: «📋 журнал: +N новых · ✅M закрыто · без изменений K». Don't duplicate neighbor registries (DR-реестр, improvements-backlog, declined) — link, не копируй.

## Step 3🗺 — Roadmap checkpoint (dev's decree 2026-07-16: «в каждом ретро — как мы продвинулись по roadmap»)
Канон = `$OBSIDIAN_VAULT/04-Projects/ROADMAP.md` (живой публичный роадмап для фолловеров). Три движения, все против ЭТОГО файла:
- **Продвинулись** → отметить чекбоксы/статусы, веху уровня «фолловеру интересно» → строка в Ship log с датой.
- **Появилось новое направление в сессии** → добавить в NOW/NEXT/LATER (не дублируя детальные планы — ссылкой).
- **Ничего не двинулось** → честно сказать это в отчёте (тоже сигнал).
Announce одной строкой: «🗺 roadmap: ✅N продвинуто · ➕M добавлено · ⏸ без движения». Публичная проекция файла наружу — только через контент-гейт (Нора), ретро наружу не постит.

## Step 3🔗 — Connect check (построено → передано → ИСПОЛЬЗУЕТСЯ?) — dev 2026-07-04
Правило Connect ([[connect-rule-pipeline-ownership]]) на подведении итогов: для КАЖДОГО артефакта этой сессии довести цепочку до конца — **«собрали» это ещё НЕ финиш**. Финиш = построено → передано потребителю → **реально используется**. Три исхода на артефакт:
- ✅ **используется** — есть потребитель и он потребляет (скилл вызывают, рутина читает выход, поле CRM читают, дашборд открывают, данные доехали и применены). **Назвать потребителя** — иначе это не ✅.
- 🔗 **передано, потребления пока нет** — доехало, но никто ещё не читает/не применяет → на доску висячих, назначить потребителя/срок.
- ⚠️ **построено «в воздух»** — собрали и бросили, потребителя нет вовсе (dead-letter без consumer — как релинк-очередь: 29k сирот, 0 применено) → **ПОДСВЕТИТЬ оператору явно**: «построили X, но это никем не используется» → решить: подключить потребителя ИЛИ признать выброшенным.

Молчание ≠ используется. «Построили» без названного потребителя = недоделанный Connect, НЕ «done». Строкой: «🔗 Connect: ✅N используется · 🔗M передано-ждёт · ⚠️K в воздух».
⭐ **🌍 МИРОВОЙ ПОТРЕБИТЕЛЬ (dev 24.08, голосом):** у каждой закрытой за сессию починки КЛАССА — четвёртый исход Connect: раздали ли миру? Сеть-ловушка: строки Breakage-Journal этой сессии «класс закрыт» без вердикта 🌍 = долг → прогнать скилл **`/share-fix`** (порог переносимости, реверс-поиск по симптому, 3-5 лучших живых тредов, gist, вахта — вся механика там). Вердикт в отчёте обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
⚠️ **Грабля 10.09 (NODE-0X):** `fleet_fix_audit.py` стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — второй заход за день отбивается. Уже гоняли сегодня → бери вывод ночной карты / `deploy_check.py`, `--force` только с названной оператору причиной. Отбитый гейтом аудит НЕ повод молчать: проверь `PENDING-<узел>` и скажи честно, что доказана РЕГИСТРАЦИЯ, а не применение.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🚂 — РЕЛЬСЫ: честный процент по чужим LLM + причины недобора (dev 21.09.2026, голосом)
Дословно: «я использовал такие-то LLM на какое-то количество процентов, а не использовал по каким-то причинам. То есть ты ещё называешь честные причины, почему ты не использовал. Забыл ты или какие-то другие причины. И сразу пытаешься поправить этот скилл».

Почему шаг живёт тут, а не в §6.3: правило «выгребай лимиты» стоит с 04.08, дверь `llm_ask.py` построена 06.08 — и всё равно замер 21.09 дал grok 0 вызовов на узле за 7 дней при $300/мес. Корень назвал оператор сам: **забыл**. Забывание невидимо, пока обещание не машиночитаемо.

Один прогон, 0 токенов:
`python ~/.claude/scripts/rail_plan.py verdict --session <id>` → таблица «обещано / вызовов факт / вердикт».
- **exit 0** — у каждой обещанной рельсы есть либо вызовы, либо названная причина.
- **Прибора на узле НЕТ** (`rail_plan.py: No such file`) — это НЕ повод пропустить шаг молча.
  Проверь очередь посылок (`deploy_check.py`): не применённая `rail-plan-*` применяется тут же
  (§7.5). Применить нельзя (чужая живая табличка ON AIR на зоне `fleet-code`, замер 21.09) →
  ⛔ НЕ форсить, а написать в отчёт строкой: «🚂 прибора нет, посылка <id> заблокирована
  ON AIR <узел>/<id>, применю после закрытия». Сессия СТАРШЕ самого правила (работа шла до
  21.09) → так и сказать: плана не было, потому что правила ещё не существовало, выдумывать
  задним числом проценты запрещено (§5.4 правда в цифрах).
- **exit 1 «ПЛАНА НЕТ»** — сессия не объявила рельсы на старте. Это и есть нарушение; объявить сейчас (`rail_plan.py declare`) и сказать в отчёте честно, что план родился на ретро, а не на старте.
- **exit 1 «НЕДОБОР без причины»** — добери причины: `--reason <рельса>=<код>:<текст>`, коды `forgot · rail-dead · class-mismatch · too-small · tier2 · no-work · **own-subagent**`.
- ⭐ **`rail-dead` РУКАМИ БОЛЬШЕ НЕ ПИШЕМ, если рельсу реально звали** (правка 30.09.2026): прибор сам ставит «rail-dead (авто): N попыт., рельса упала», когда в леджере есть ПОПЫТКА. Колонка «попыток мимо» в таблице — это и есть улика. Строка «авто» = долг ПОЧИНКИ РЕЛЬСЫ (логин, квота), а не долг дисциплины: заводи задачу на рельсу, а не причину в вердикт. ГРАНИЦА: прибор доказывает попытку, а не диагноз — 401 и 429 для него одинаковы, текст ошибки вендора ищи в stderr прогона («рельса <имя> мимо: …»).
- ⭐ **Грунт сделал СУБАГЕНТ (Agent model=sonnet/opus) — это код `own-subagent`, а НЕ `forgot` и НЕ `class-mismatch`** (правка 30.09.2026). Субагент жжёт НАШ бак Anthropic, внешней рельсой не является и прибором не считается СОЗНАТЕЛЬНО; объявить его в `declare --outsource` теперь нельзя (exit 2). Замер 28–29.09: два прогона подряд весь грунт отдали субагентам, прибор напечатал ноль и заставил выдумать причину — `own-subagent` существует, чтобы подмена чужой оплаченной подписки своим баком **считалась по леджеру**, а не пряталась под «too-small».
- **Узловой срез** (что вообще этот компьютер обещал и сжёг за окно, все сессии сразу): `rail_plan.py verdict --all-sessions --days <N>`. По умолчанию сверка ПОСЕССИОННАЯ — иначе возвращается класс «вердикт судит чужой план» (8 датированных случаев 21–28.09).
- **`No such file` — прибора на узле НЕТ** (замер 21.09, NODE-0X: посылка `rail-plan-20260921` лежала непринятой, и шаг судить было нечем). Это НЕ повод пропустить шаг молча: (1) посмотреть очередь посылок `python ~/.claude/scripts/deploy_check.py` и применить её тем же заходом; (2) применение отбито правами/классификатором → строка в отчёт «🚂 сверка невозможна: прибора нет, посылка <id> не применена» + пункт в TODO. Отсутствие прибора называется вслух, а не превращается в «рельсы не жгли».

⭐ **«forgot» обязывает ПРАВИТЬ ДВЕРЬ в том же заходе**, а не объяснять. Это прямой приказ оператора («сразу пытаешься поправить этот скилл, чтобы в будущем так не ошибаться») и он смыкается с 🛠 «вердиктом о скилле» ниже: причина `forgot` = скилл/рутина пропустили рельсу, значит правится вызывающий, а не только этот файл.

⛔ Запрещено закрывать шаг словами «мало пользовались другими LLM» без цифр: доля считается прибором, а не на глаз (§5.4 «правда в цифрах»). ⛔ Не смешивать два числа: `rail_plan.py` считает **ВЫЗОВЫ наших рельс**, а процент выборки бака вендора живёт в `subscription_utilization.py report` — это разные величины разного происхождения.
Строкой в отчёт: «🚂 рельсы: жгли <рельса=N…> · недобор <рельса:код> · правка двери: да/нет».
Канон: [[rail-plan-declared-then-verified]], [[burn-the-limits-utilization]], [[other-llm-rails-were-review-only]].

## Step 3🔄 — Outcome-аудит ПРОШЛЫХ правил (взято у netresearch/retro-skill «outcome mode», adopted 2026-08-26; наш обмен — issue #78 их репо)
Door-audit (Step 3🔗) судит правило при РОЖДЕНИИ; этот шаг судит СУДЬБУ уже записанных — родился с дверью ≠ живёт (замеры: 19/25 без двери, «5 почему» 42 дня без применения, Firefox-first умер тихо за 13 дней). Дёшево, ЧИТАЕМ ночные выходы, сканы руками НЕ гоняем (§10.0):
1. Возьми правила, ТЕМАТИЧЕСКИ близкие этой сессии + до 5 самых старых нетронутых из ночной карты `rule_liveness` (HTML/JSON выход ночного прогона; руками `--scan` не запускать).
2. По каждому три вопроса: применялось ли с прошлого ретро (счётчик §5.8 / упоминание в транскриптах)? нарушалось ли (Breakage-Journal)? актуально ли ещё (не superseded)?
3. Вердикт-строка в отчёт: «🔄 outcome: N проверено · M живут · K мертвы» — каждому мёртвому РЕШЕНИЕ в том же заходе: утиль (в архив с причиной) / дверь построить / отдать сессии-починке. Молча пропустить шаг нельзя; сессия без тематических правил → «🔄 outcome: чужих правил не трогал» одной строкой.

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` — ТОЛЬКО из двери `python ~/.claude/scripts/_shared/fireat_now.py --in 15`, руками время не писать: класс из 6 случаев 11.08-09.09, часы шелла врали до 11 ч; разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro). ⚠️ Грабля 10.09 (NODE-0X): этот прибор ТОЖЕ стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — на 5-м заходе за сутки он отбивается, и «доказать счётчиком» становится нечем. Тот же класс, что каветат про `fleet_fix_audit.py` в Step 3🔗. Отбило → либо `--force` с названной оператору причиной, либо честная строка в отчёте «дверь проверена глазами, счётчик отбит суточным гейтом» — молча пропускать проверку нельзя.

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 кандидата/ночь, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.
**⭐ HN-кандидат (dev «+++» 10.09):** тот же проход задаёт ВТОРОЙ вопрос ровно один раз на артефакт — «это годится в Hacker News?». Годится ТОЛЬКО жанр «мы померили и показываем цифры» (post-mortem · замер · разбор поломки) и ТОЛЬКО как самостоятельная публичная страница с данными, не пост из ежедневного девлога. Да → строка в `$OBSIDIAN_VAULT/_outreach/hn_candidates.jsonl` (added·from·artifact·title·url·numbers·genre·status:ready|needs-page·blocked_by). Нет → молча, вердикт не нужен. ⛔ Потолок лейна: **своя ссылка на HN не чаще 1 раза в 2 недели** (ежедневный поток туда = профиль спамера, теневой бан накрывает аккаунт И домен); регулярное присутствие = комментарии в ЧУЖИХ тредах 1-3/нед. ⛔ Подача идёт ТОЛЬКО с хаба, ТОЛЬКО после «+» оператора и ОК Норы, ноль организованного голосования. Пока нет входа в HN на хабе — очередь копится, наружу не уходит ничего.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].
**⭐ Мини-тизер обязателен (dev 01.09):** every retro with a substantive arc births ≥1 mini-teaser (200-250 chars, «грабли → правило» so the READER gets use, not a status report) → `python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук>" --note "<тизер>" --tier teaser`. Verdict «no teaser» is legal ONLY with a named reason (empty routine session). Canon: `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`.

## 🛠 ВЕРДИКТ О СКИЛЛЕ, КОТОРЫМ ПОЛЬЗОВАЛИСЬ (dev 07.09, голосом — обязателен, молчание = нарушение)
Применил в этой работе скилл — вынеси вердикт об ЕГО обновлении. Одной строкой, с причиной в обе стороны:
`🔧 обновляю /X — <что споткнулось>` (чинить В ТОМ ЖЕ заходе) · `📝 обновлю не сейчас — <причина>, строка легла в <адрес>` · `✅ /X обновлять не надо — <почему именно: прошло без заминки / заминка разовая и внешняя / правка дороже боли>`.

⭐ **ВЕРДИКТОВ ДВА, НЕ ОДИН** (dev 13.09, голосом). Второй вердикт: **собственная инструкция того, кто сейчас работал** (рутина `scheduled-tasks/<имя>/SKILL.md`, сид, хук): «не стоит ли переписать мою инструкцию на будущее, чтобы она была качественнее?». Та же тройка `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, всегда с причиной. ⚠️ Замер 13.09: рутина `devto-publish-rhythm` починила СВОЙ файл и смолчала про скилл `/comments`, где висел ПРОТИВОПОЛОЖНЫЙ гейт, правило исполнилось наполовину, и спрашивать пришлось оператору. Канон живёт в СКИЛЛЕ, рутина держит только специфику прогона: разошлись, значит правду в скилл, а из рутины указатель. Канон: [[routine-judges-its-own-instruction-too]], CLAUDE.md §9.3-бис.
Пустое «не надо» вердиктом не является. ⛔ Не путать с `/skill-gap` (тот про скилл, которого НЕТ) и не право раздувать: АК-47 в силе — правка снимает ПЕРЕЖИТУЮ боль, не гипотетическую.
Канон: Библия `reglament-polzuemsya-skillom-srazu-sudim-nado-li-ego-obnovit` · CLAUDE.md §9.3-бис · [[skill-used-judge-if-it-needs-update]].

## Step 4★ — The «repeats → make a skill» reflex (milestone closeout)
This is the step dev asked for (2026-06-18): at a finished milestone, don't just *note* a repeating action — **offer to turn it into a skill**. It's the retro-time expression of the standing rule `evaluate-recurring-into-routine` (повторяющаяся задача → оцени «на рутину?»). Mirror of [[capture-rules-into-bible]] (that catches *rules*; this catches *tasks-to-automate*).

**Trigger (catch it, don't wait to be asked):** any action that **repeated ≥2–3×** this session/milestone, OR that we'll **clearly return to** later (a manual sequence I re-typed, a multi-step procedure, a recurring check).

**Procedure — 4 cheap moves:**
1. **RECALL first — don't duplicate.** Skim the available skills + memory `automation-inventory` for an existing skill/routine/hook that already covers it. If one exists, point dev to it instead of building a twin. **⛳ И тут же второй вопрос (dev hub:5090, 2026-08-04): скилл ЕСТЬ — не проапгрейдить ли его?** «Есть» ≠ «закрыто»: назови, чего ему не хватило ИМЕННО в этой сессии (шаг, который я делал руками поверх скилла / грабли, которых в нём нет / устаревшая строка) → правка в тот же заход, и это тоже строка в 🔁→🛠 (`built/proposed/declined`). Нечего добавить — скажи это словом, молчание = проверка не сработала. Дословный текст вопроса и формат ответа — единственный источник в `/skill-gap` §⛳ (там же — вход-конец рефлекса).
2. **⚠️ AK-47 guard — a skill is just a `SKILL.md`.** One markdown file with a procedure, NOT a server / DB / webhook / external service. (This is the exact trap the Codex milestone-retro report fell into — over-engineered for a SWE team; rejected 2026-06-18.) If the thing genuinely needs more than a markdown procedure, flag it **⚠️ УСЛОЖНЕНИЕ** and let dev decide.
3. **OFFER as ДО→ПОСЛЕ** (per `show-before-after`) — one compact block:
   > **ЧТО:** собрать `/<имя-скилла>` · **ДО:** как делаю руками сейчас (на реальном примере этой сессии) · **ПОСЛЕ:** одна команда `/<имя>` · **что сломается:** ничего (надстройка) · **делаем? да/нет**
4. **On dev's «+» → build it via `skill-creator`.** Pick the right home by SHAPE (per `operating-agreement` → «Where durable rules go»):
   - on-demand ritual I run when asked → **skill** (`skill-creator`).
   - «каждый раз автоматически когда X» → **hook** (skill `update-config`), not a skill.
   - time-based «каждый понедельник / каждое утро» → **scheduled task / routine** (skill `schedule`).
   - «рутина» ≠ обязательно 24/7-робот — часто правильное = простой полуавто + напоминание.
   - ⭐ **СПИСОЧНАЯ работа на N кусков (N велико) → КОНЕЧНАЯ рутина, «слон»** (dev 23.08, §4.5-бис).
     Признак: в сессии я перебирал однотипные элементы (видео / заметки / карточки / островá графа /
     ссылки), список не кончился, и он не кончится и в следующий раз; либо задача уже месяцами
     спотыкается об участие оператора, лимиты вендора или баны. Это НЕ задача и НЕ героическая сессия —
     это слон: `python ~/.claude/scripts/elephant.py new <slug> --title T --quota N --os-task <ЗадачаWindows>`,
     дальше рабочий скрипт на каждом прогоне делает `next` → работа → `mark` → `tick`.
     `tick` сам ловит конец (выключает OS-задачу + доклад в TG-03) и затык (5 пустых прогонов → `blocked`).
     ⛔ Журнал слона НИКОГДА не кладём в синкаемую папку — затрётся, и слон не кончится никогда.
     Живой пример: [[yt-watch-history-drip]]. Канон: [[finite-routines-eat-the-elephant]].
   Then route/link it normally (Step 4) and mention it in the final report (post-hoc, not for permission).
5. **⭐ Скилл уходит в мир (dev 01.09, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** любой собранный/существенно обновлённый скилл в том же заходе получает (а) тизер-пост в наши соцсети (через content-factory / каскад) и (б) публикацию самого скилла на нашем публичном GitHub (дефолт `tonydzi/clawrush` `artifacts/`) ПОСЛЕ leak-scan, с пометкой в шапке «built for dev's fleet — adapt paths/names to your setup». Заточен под оператора / сырой / «на тормозке» — публикуем всё равно, честно пометив. Скип — только с названной причиной (leak-scan red / чистая кухня CRM).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
4б. **🔄 Outcome** — «N проверено · M живут · K мертвы + решения» (Step 3🔄).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the FULL enriched `/compact` block printed inline (Step 6b; указатель на файл запрещён).
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Reserve the final Latin filename first, acquire exact leases for that note and `01-Conversations/Claude/_Claude-Sessions-MOC.md`, and add the MOC wikilink **before the note's first write**. The no-orphan guard rejects a new note that has no incoming link; if the MOC lease is busy, wait for its owner instead of creating an orphan or overriding the lease. Then write the clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **Formal review status is a scoped receipt, not prose.** Every independent-review claim in the note MUST be one exact line: `REVIEW[<artifact-id>]: verdict=<VERIFY|ACCEPT|BLOCK|REQUEST_CHANGES>; scope=<what exact bytes/state the verdict covers>; source=<thread:<uuid>|file:<absolute-path>>; reviewer=<name>`. A partial GREEN/RED run never upgrades the formal verdict; a rollback-only VERIFY stays rollback-only and cannot verify the proposal.
  ⚠️ Три грабли формата, каждая стоила прогона линта (замер 26.09.2026): (1) `scope` — максимум **200 символов**, два sha256 туда уже не влезают, оставляй один и слово «только»; (2) **точка с запятой внутри `scope` рвёт разбор** (поле читается как `[^;]+`) — внутри только запятые; (3) `source=file:<path>` обязан лежать в корнях, которые линт обходит (`~/.claude`, волт, `_imports`, папка дока, cwd) — вывод из `Temp\claude\…\tasks\` не засчитывается, копируй улику к остальным квитанциям. Плюс проза: слова «независимый ревьюер» рядом с «accept/pass/verify» в обычном абзаце тоже требуют receipt, поэтому в тексте пиши «Codex смотрит дифф», а вердикты держи только в receipt-строках. (4) **путь в `source=file:` пиши через ПРЯМЫЕ слэши** (`D:/Vault/...`): обратный слэш съедается любым генератором строки (в Python `\R`/`\0` стали управляющими символами и линт дважды отбил receipt с «битым» путём — замер 27.09.2026).
- **Door before archive/mark-done:** immediately after drafting the note, run `python -B "$HOME/.claude/scripts/status_claim_lint.py" "<absolute-retro-note>"`. `rc=0` is required before MOC/log/`mark-done`; `rc=2` means correct the claims and rerun. Do not archive or claim verification while this door is red.
- ⚠️ **Хук `orphan_check_hook` отобьёт запись: новое ретро рождается сиротой.** Дом входящей ссылки один и он известен: `01-Conversations/Claude/_Claude-Sessions-MOC.md`, секция «Свежие ретро» (плюс на ретро ссылаются `DayLedgers/day-ledger-*.md` и `00-System/Breakage-Journal.md`). Впиши строку `- [[retro-...]] · <в чём суть>` ТУДА первой записью батча, до создания note; после появления note проверь, что ссылка ровно одна.
  ⚠️ Грабля замера 14.09.2026: искать дом грепом по всему волту НЕ надо, `grep -rl` по `D:\Vault\Vault-Knowledge` уходит в таймаут 120с. На таймауте я объявил «ретро не линкует никто» и вписал этот вывод сюда как факт; фоновый прогон досчитался и вывод ОПРОВЕРГ. Ровно [[prichina-kak-claim]]: незавершённый поиск даёт «я не нашёл», а не «этого нет».
  Вторая ссылка из содержательного дома (реглумент/концепт/решение, к которому ретро относится) полезна и закрывает заодно Step 4, но обязательной является ссылка из MOC.
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- Nightly Brain Reindex does NOT make this note `/ask`-searchable. `01-Conversations` is evidence, and `brain_embed_update.py` skips it. Copy the recallable facts into an essence note (`02-Decisions` or `10-Tasks`) in the same retro. The chat catalog indexes the retro file only on its own rebuild, not on the 15-minute brain tick. Proof 2026-09-25: a phrase that lives only in the retro = 0 chunks, the same facts in the decision memo = 1 chunk in `_brain_lex_e5.db`.

**6a-бис. Взять и снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- До работы выбери абсолютный путь `<absolute-receipt.json>` вне репозитория и захвати сессию: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" take <sessionId> --holder "<taskId>" --json --receipt-out "<absolute-receipt.json>"`.
- `rc=0` доверяй только когда durable receipt exists и JSON содержит непустые `question_id`, `session_id`, `logical_file_id`, `holder` и `epoch` как positive integer. Receipt сохрани до подтверждённого DONE: он нужен для replay после crash. При отсутствующем/битом receipt остановись; DONE не ставь.
- После записи ретро передай значения **дословно из receipt**: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" mark-done "<receipt.session_id>" --question-id "<receipt.question_id>" --logical-file-id "<receipt.logical_file_id>" --holder "<receipt.holder>" --epoch "<receipt.epoch>" --note "<retro-note>"`. Do not recompute identity по пути или sessionId. Wrong/missing identity обязана завершиться fail-closed без DONE/release; точный replay идемпотентен.
  ⚠️ `"$HOME/..."` буквально работает и в Windows PowerShell 5.1, и в Git Bash. `~` после `python` в PowerShell 5.1 остаётся буквальным путём, а `%USERPROFILE%` раскрывает только CMD.
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6a-тер. Переименуй сессию: маркер «Р» в видимом имени — СРАЗУ после 6a-бис** (⭐ dev 02.09.2026, голосом: «когда я вижу этот маркер, я понимаю, что дошёл в этой сессии до крупного milestone»; ⭐ **поправка dev 15.09.2026, голосом: маркер теперь просто `Р`, БЕЗ плюсика** — «дописываем не Р с плюсиком, а просто Р»).
- Вызови `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → возьми текущий `title`. Если в нём УЖЕ стоит маркер ретро — `Р ` (новый) ЛИБО legacy `Р+`/`р+`/`рр+` — шаг закрыт, второй маркер не лепить и legacy НЕ переписывать (старые имена оставляем как есть, чинить историю нечем и незачем).
- Иначе `mcp__ccd_session_mgmt__set_session_title` с `session_id: "self"` и `title: "<иконка> Р <старое имя без изменений>"` — маркер `Р` + ПРОБЕЛ, после иконки группы (иконка первой, см. 6a-кватер), без иконки — просто `"Р <старое имя>"`. Меняется ТОЛЬКО человекочитаемое имя в приложении (titleSource=tool), системный id не трогается; имя, данное оператором, сохраняется целиком после маркера.
- ⚠️ Пробел после `Р` обязателен: он и есть граница маркера. `Р` без пробела слипается с русским словом («Ретро», «Работа») и читатели (жнец, таблица сессий) такую сессию маркером не считают.
- MCP session_mgmt недоступен (headless `claude -p`, чужой харнес) → одна строка в отчёте «маркер Р не поставлен: нет session_mgmt», не молчи.

**6a-кватер. Проверь ИКОНКУ группы в заголовке — сразу после маркера Р** (⭐ dev 07.09.2026 «кладёшь её в нужную группу»; ⭐ dev 10.09.2026, голосом: «мало пикселей на экране, нужна иконка», и «переименовывать НА СТАРТЕ»).
- Иконка ставится НЕ здесь, а на СТАРТЕ сессии (скилл `/session-groups`). Ретро только ПЕРЕПРОВЕРЯЕТ: тема сессии за день могла уехать в другую группу.
- `get_session self` уже вызван в 6a-тер. Заголовок начинается с иконки из алфавита? 💰 $$$ (деньги/оффер/витрины/статьи наружу) · 🧠 2мозг (волт/RAG/память/клон) · ✍️ content (посты/соцсети/Майкрофт) · 🎯 Лиды-CRM · ⚙️ Инфра (скрипты/флот/синк/канон/браузеры) · 🔬 ДРы · 🏠 личное · 📥 SINK (инбокс/шина/посылки) · ❓ не понял.
- Иконки нет ЛИБО она уже не про эту сессию → `set_session_title self` в форму `<иконка> Р <имя>`. Веха ретро `Р ` живёт ПОСЛЕ иконки (legacy `Р+` в старых именах не переписываем). Гадать запрещено: тема не читается — ставь ❓, оператор разнесёт сам.
- Строка в отчёт: «иконка: <какая>, флаг ccd_sidebar OFF». Молчать нельзя.
- Рычаг настоящего переноса = MCP `ccd_sidebar.move_sessions`, появляется только когда приложение его отдаёт: проверка `python ~/.claude/scripts/claude_desktop_gate_probe.py` (exit 0 = флаг id_0bae24da ON) → тогда переноси по-настоящему, а иконка больше не нужна. Замер 07-10.09: флага в выдаче фич нет, issue anthropics/claude-code#92621.
- ⛔ Правка `claude_desktop_config.json` руками НЕ рельса: приложение файл живьём не перечитывает и перепишет из памяти (замер 07.09).
- Канон: память `session-group-at-retro`; движок и алфавит — скилл `/session-groups`; публичная копия github.com/tonydzi/claude-session-icons.

**6b. PRINT the READY enriched paste-line INLINE — обязательный выход КАЖДОГО ретро (⭐ dev 26.08, голосом: «каждый раз давай готовый текст компакта; иди-в-файлик — неудобно»).**
- ⚠️ Fact base (2026-07-22): bare `/compact` does NOT read our format — 354/354 past compacts fell back to the DEFAULT English template; PreCompact hooks cannot inject (issue #14160). The 7-header format applies ONLY pasted inline: `/compact <text>`.
- **Procedure = same enrichment as `/cc` Steps 2-3** (single source of mechanics — don't duplicate, read `~/.claude/skills/cc/SKILL.md`): take the skeleton from `$USERPROFILE/.claude/compact-prompt.md` § «Готовая строка», FILL all 7 headers with THIS session's real facts — reuse the distillation already written into the 6a vault note, don't re-derive — and PRINT one fenced ```code``` block starting with `/compact `, со строкой над ним: «➤ Скопируй блок целиком и вставь следующим сообщением». Then the fork:
> **«Готово, всё в волте. Остаёшься в сессии — вставь блок ниже целиком (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — просто уходи, всё уже заархивировано.»**
- ⛔ **Указатель вместо блока ЗАПРЕЩЁН.** «Вставь блок из `~/.claude/compact-prompt.md`» / «возьми текст в файле» = нарушение правила (ровно эта формулировка — жалоба оператора 26.08). Пустой скелет с `<...>` — тоже нарушение: блок обязан быть обогащён сессией. Канон: память `compact-dev-prefers-zero-touch` §Поправка 26.08 + `compact-format-delivery-gotcha`.
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; printing the ready line is my half, the paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

## ⭐ Полнота списка потребителей (dev 10.09.2026)

Первый найденный потребитель почти никогда не единственный — он просто лежал на поверхности. Поиск закончен не когда кто-то найден, а когда **две оси подряд дали ноль новых имён**; внутренний потребитель (узел флота, робот, наш же скилл с костылём) ищется ПЕРВЫМ. Девять осей перебора и обязательный вердикт с числом («осей N/9 · адресов M · насыщение да/нет») — `/consumer-hunt` §Шаг 1-бис. ⚠️ Исчерпывающим обязан быть ПОИСК, адресация идёт по правилам двери: найденный адрес не выбрасывается, а получает статус и дату (🟢 постучались · ⏸ глухая очередь по замеру · 🪦 непереносимо). Канон: `reglament-vypustil-funkcional-naydi-potrebiteley-i-pridi-k-nim` §Поправка 10.09 + [[consumers-are-a-set-not-the-first-one]].


ARGUMENTS: сессия T09 битемпоральные рёбра, хаб HUB-01

---

**Claude:**

Запускаю ретро. Сначала сверка и инвентарь:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" turnstate/turnstate_show.py 2>&1 | tail -25", "description": "Turnstate spine of this session"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/logs/retro_lost_done/ 2>/dev/null | grep -i a09aedcd | head -3; echo \"(пусто = робот ретро не делал)\"; ls -t /e/Obsidian/Vault-Knowledge/01-Conversations/Claude/Retros/ 2>/dev/null | head -6", "description": "Robot retro marker + recent retros"}

---

**Claude:**

Стоп: часы и маркер говорят, что прошло время. Проверяю ground truth:

---

> `Bash` -- {"command": "date -u +\"UTC сейчас: %Y-%m-%d %H:%M\"; echo \"--- маркер робота ---\"; ls -l --time-style=+%Y-%m-%d_%H:%M /c/Users/dev/.claude/logs/retro_lost_done/s_a8ad786a* 2>&1 | head -3; cat /c/Users/dev/.claude/logs/retro_lost_done/a09aedcd-7945-4410-8e9c-480c6675b

---

**Claude:**

Разрыв 13 дней: работа шла в ночь 16→17.09, сейчас **30.09 19:54**. И ночная догонялка уже разбирала эту сессию 20.09 — значит моё ретро это ДЕЛЬТА, а не второй полный разбор. Сверяю живое:

---

> `Bash` -- {"command": "sed -n '1,60p' /e/Obsidian/Vault-Knowledge/01-Conversations/Claude/Retros/retro-lost-2026-09-20-hub-desyatka-33-sessii.md 2>&1 | head -50", "description": "Read the robot's retro note"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== файлы живы? ===\"; ls -l --time-style=+%m-%d_%H:%M brain_temporal.py _test_brain_temporal.py eval/gold-temporal-2026-09-16.jsonl 2>&1 | awk '{print $5, $6, $7}'\necho \"=== вр

---

**Claude:**

Ночная догонялка нашла настоящий дефект в моём тесте, он живой и сегодня. Чиню (карв-аут «артефакт этой же сессии»):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && sed -n '/T1: первый sync/,/e_after1 = /p' _test_brain_temporal.py | head -14; echo \"=== где ставится TODAY впервые ===\"; grep -n \"BRAIN_TEMPORAL_TODAY\" _test_brain_temporal.py | head -5", "description": "Find the calendar-dependent fixture"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        # ---- T1: первый sync создаёт рёбра и факты\n        c1 = bt.sync(con=con, files=files)", "new_string": "        # ЧАСЫ ФИКСИРУЮТСЯ С ПЕРВОГО ЖЕ ПРОГОНА (починка 30.09: нашла ночная догонял

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        hist = con.execute('SELECT value, valid_from, valid_to FROM brain_facts WHERE stem=? '\n                           'AND key=? ORDER BY valid_from', ('new-note', 'status')).fetchall()", "new_

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" _test_brain_temporal.py 2>&1 | tail -3; echo \"=== мутанты (краснота не потерялась?) ===\"; for m in second cache case delete order; do printf \"%-7s FAIL=\" \"$m\"; BRAIN_TEMP

---

**Claude:**

Тест починен, мутанты по-прежнему красные. Дальше дельта-сверка за 13 дней:

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && grep -m1 -E \"^state:\" task-2026-09-16-sm-T10-share-eval-module.md; grep -m1 -E \"^state:\" task-2026-09-16-sm-T09-bitemporal-edges.md; echo \"=== флаг где-то включён? ===\"; grep -rn \"BRAIN_TEMPORAL\" /c/Users/dev/.claude/settings*.json /c

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\nfor c in sync-resolves-conflict-to-older-version sync-conflict-left-node-on-stale-copy replay-mode-not-equal-fresh scores-filename-minute-collision sqlite-double-quoted-literal-is-a-column; do printf \"%-46s \" \"

---

> `Bash` -- {"command": "C=\"/c/Users/dev/.claude/_counters/brain_temporal-HUB-01.jsonl\"; echo \"всего строк: $(wc -l < $C)\"; echo \"--- по размеру прогона (files=N) ---\"; grep -oE '\"outcome\": \"files=[0-9]+' \"$C\" | sed 's/.*files=//' | sort -n | uniq -c | sort -rn | head -8; echo \"--- event=ap

---

**Claude:**

Счётчик врёт: из 987 строк **986 написали мои же тесты**, боевых прогонов ровно 1. Это класс `counter-is-production-tests-must-not-write-it`. Чиню:

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\brain_temporal.py", "old_string": "COUNTER = (Path(os.path.expanduser('~')) / '.claude' / '_counters'\n           / ('brain_temporal-%s.jsonl' % _node()))", "new_string": "COUNTER = Path(os.environ.get('BRAIN_TEMPORAL_COUNTER')\n          

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "    tmp = Path(tempfile.mkdtemp(prefix='bt-test-'))\n    try:", "new_string": "    tmp = Path(tempfile.mkdtemp(prefix='bt-test-'))\n    # СЧЁТЧИК ТЕСТА — СВОЙ. Боевой файл трогать нельзя: он и есть 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\_test_brain_temporal.py", "old_string": "        con.close()\n    finally:\n        os.environ.pop('BRAIN_TEMPORAL', None)\n        os.environ.pop('BRAIN_TEMPORAL_TODAY', None)", "new_string": "        # ---- T13: боевой счётчик тестом НЕ 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\nC=\"/c/Users/dev/.claude/_counters/brain_temporal-HUB-01.jsonl\"; BEFORE=$(wc -l < \"$C\")\n\"$PY\" _test_brain_temporal.py 2>&1 | tail -3\nAFTER=$(wc -l < \"$C\"); echo \"строк

---

> `Bash` -- {"command": "C=\"/c/Users/dev/.claude/_counters/brain_temporal-HUB-01.jsonl\"; mv \"$C\" \"${C%.jsonl}.polluted-by-tests-thru-20260930.jsonl\" && cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" brain_temporal.py sync 2>&1 | tail

---

**Claude:**

Живая улика дельты: индекс вырос 7846 → **23 084** файла, sync закрыл **3 реальных ребра** (close-don't-delete впервые сработал в бою). Теперь журнал поломок:

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\nfor q in \"режим переигрывания линейки даёт не те числа что свежий прогон\" \"счётчик использования пишут тесты и метрика завышена\" \"SQL литерал в двойных кавычках читается как имя колонки\"; do echo \"=== $q\";

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/breakage.py find \"тесты пишут в боевой\" 2>&1 | grep -oE \"класс[а]? [a-z-]{8,}|\\| [a-z-]{12,} \\|\" | sort -u | head -8", "description": "Exact family slug for test-pollut

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/breakage.py find \"боевой лог\" 2>&1 | head -6 | cut -c1-200; echo \"---\"; \"$PY\" /c/Users/dev/.claude/scripts/breakage.py count --class counter-is-production-tests-must-

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=/c/Users/dev/.claude/scripts\n\"$PY\" $S/selfheal.py journal --class counter-is-production-tests-must-not-write-it --what \"счётчик brain_temporal: 986 из 987 строк за 13 дней написала регресс-сетка (фикстуры 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== rail_plan verdict ===\"; \"$PY\" /c/Users/dev/.claude/scripts/rail_plan.py verdict --session s_a8ad786a 2>&1 | tail -8; echo \"EXIT=${PIPESTATUS[0]

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; S=/c/Users/dev/.claude/scripts\necho \"=== memory_harvest ===\"; \"$PY\" $S/memory_harvest.py --scan 2>&1 | tail -3\necho \"=== memory_inject_lint ===\"; \"$PY\" $S/memory_inject_lint.py --scan 2>&1 | tail -3\ne

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/memory_epistemic.py --lint 2>&1 | grep -E \"TOMBSTONE|findings|FINDINGS|\\[.*\\]\" | head -10", "description": "What exactly memory_epistemic found"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\" && \"$PY\" retro_inventory.py 1 2>&1 | tail -12", "description": "Deterministic inventory"}

---

> `Bash` -- {"command": "M=/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory; for f in dr-never-through-codex-cli gemini-geoblocked-on-austrian-ip; do echo \"=== $f\"; grep -nE \"^status|^valid_to|^superseded_by|устарел|опроверг|уже не|ОТМЕН|более не\" \"$M/$f.md\" 2>/dev/null | head -4; done"

---

> `Bash` -- {"command": "find /c/Users/dev/.claude/projects -name \"dr-never-through-codex-cli.md\" -o -name \"gemini-geoblocked-on-austrian-ip.md\" 2>/dev/null | head -4", "description": "Locate the tombstone notes"}

---

> `Bash` -- {"command": "head -20 \"/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/dr-never-through-codex-cli.md\" 2>&1 | cut -c1-190", "description": "Read tombstone content"}

---

**Claude:**

Находки памяти разобраны: обе не мои и закрытию не подлежат (первая помечена автором как намеренная «ПОКА-клауза», вторая в проекте NODE-0X). Пишу заметку ретро — сперва ссылка в MOC, чтобы не родить сироту:

---

> `Bash` -- {"command": "grep -n \"Свежие ретро\" -A 4 /e/Obsidian/Vault-Knowledge/01-Conversations/Claude/_Claude-Sessions-MOC.md 2>&1 | head -8", "description": "Find MOC section for fresh retros"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\_Claude-Sessions-MOC.md", "old_string": "## Свежие ретро\n- [[retro-2026-09-30-sm-t05-reranker-delta]] · T05 второй памяти: оба реранкера отвергнуты числом, а главным оказался контроль «судьи нет вообще»; д

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\_Claude-Sessions-MOC.md", "offset": 866, "limit": 10}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\_Claude-Sessions-MOC.md", "old_string": "## Свежие ретро\n- [[retro-2026-09-30-sm-t05-reranker-delta]] · T05 второй памяти: оба реранкера отвергнуты числом, а главным оказался контроль «судьи нет вообще»; д

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-09-30-sm-t09-bitemporal-delta.md", "content": "---\ntitle: \"T09 битемпоральные рёбра — дельта 13 дней спустя\"\naliases: [\"ретро T09 битемпоральная полоса\", \"retro T09 bitemporal delta\"]\ndate: 2026-09-30

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" -B /c/Users/dev/.claude/scripts/status_claim_lint.py \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-09-30-sm-t09-bitemporal-delta.md\" 2>&1 | tail -3; echo \"rc=${PIPESTATUS[0]}\

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git add brain_temporal.py _test_brain_temporal.py && git commit -q -F - <<'MSG'\nT09 ретро-дельта: тест перестал краснеть по календарю, счётчик отделён от тестов\n\n1) Часы теста фиксируются с первого прогона + сортировка по (valid_from, observed_at):\n   с 19

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🧠 Р AUTO-hub-sm-T09 bitemporal-edges"}

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== retro_lost: сессия уже снята роботом? ===\"; \"$PY\" /c/Users/dev/.claude/scripts/retro_lost_scan.py status s_a8ad786a 2>&1 | tail -4 || true\necho \"=== тизер в воронку ===\

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" /c/Users/dev/.claude/scripts/retro_lost_scan.py list 2>&1 | grep -i a09aedcd | head -2; echo \"(пусто в очереди = сессия уже закрыта маркером 20.09)\"; echo \"=== roadmap: есть ли строка про вторую памят

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/10-Tasks && for f in task-2026-09-16-sm-T*.md; do printf \"%-18s \" \"$(echo $f | grep -oE 'T[0-9]+')\"; grep -m1 -E \"^state:\" \"$f\"; done", "description": "All program steps state"}

---

> `Bash` -- {"command": "grep -nE \"^## |^### \" /e/Obsidian/Vault-Knowledge/04-Projects/ROADMAP.md | head -12; echo \"--- последние строки Ship log ---\"; grep -n \"2026-09-2\\|2026-09-3\" /e/Obsidian/Vault-Knowledge/04-Projects/ROADMAP.md | tail -4 | cut -c1-150", "description": "ROADMAP structure + latest sh

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\04-Projects\\ROADMAP.md", "offset": 299, "limit": 4}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\04-Projects\\ROADMAP.md", "old_string": "- 2026-09-29 — онбординг флота стал ссылкой: в second-brain-starter-kit доехали ONBOARDING-WINDOWS", "new_string": "- 2026-09-30 — программа качества второй памяти закрыта: все 10 шагов (лине

---

> `Bash` -- {"command": "PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== дверь правила: полоса времени ===\"; \"$PY\" /c/Users/dev/.claude/scripts/rule_home_guard.py bitemporal-recall-demote-not-drop 2>&1 | tail -4\necho \"=== очередь раздачи share-fix ===\"; tail -2 /e/Ob

---

**Claude:**

Дверь правила красная — закрываю (память + указатель в always-loaded):

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\bitemporal-demote-not-drop.md", "content": "---\nname: bitemporal-demote-not-drop\ndescription: Закрытые заметки в recall ОПУСКАЕМ вниз, а не отсеиваем — у части gold правильный ответ сам закрыт; ручка BRAIN_TE

---

> `Bash` -- {"command": "M=/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/MEMORY.md; grep -c \"bitemporal-demote-not-drop\" \"$M\"; tail -3 \"$M\" | cut -c1-120", "description": "Check MEMORY.md tail before appending"}

---

> `Bash` -- {"command": "M=/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/MEMORY.md; printf '%s\\n' '- [Время в recall: опускаем, не отсеиваем](bitemporal-demote-not-drop.md) — ⭐30.09 у 3 вопросов gold правильный ответ сам закрыт; BRAIN_TEMPORAL=demote, дефолт off, цена названа' >> \"$M\"; 

---

> `Bash` -- {"command": "Q=/e/Obsidian/Vault-Knowledge/_outreach/share_fix_queue.jsonl; PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"; \"$PY\" - \"$Q\" <<'PYEOF'\nimport io, json, sys\nrow = {\n  \"added\": \"2026-09-30\",\n  \"from\": \"retro-2026-09-30-sm-t09-bitemporal-delta\",\n  

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PY=\"C:/Users/dev/AppData/Local/Programs/Python/Python312/python.exe\"\necho \"=== финальная проверка: тесты + мутанты + боевой счётчик ===\"\nC=\"/c/Users/dev/.claude/_counters/brain_temporal-HUB-01.jsonl\"; B=$(wc -l < \"$C\")\n\"$PY\" _test_brain

---

> `Bash` -- {"command": "sed -n '/Готовая строка/,/^##/p' /c/Users/dev/.claude/compact-prompt.md 2>/dev/null | head -30", "description": "Canonical compact block skeleton"}

---

**Claude:**

🕐 **четверг, вечер, 20:10, 30 сентября 2026**

# Ретро: T09 битемпоральные рёбра — дельта 13 дней спустя

## 🔎 Сверка (Step 0)

**Проверено:** turnstate-хребет, каталог ретро, маркер `retro_lost_done`, состояния всех 10 карточек программы, журнал поломок (5 классов), три сканера памяти, rail_plan, ON AIR, живая БД и диск.

⚠️ **Первое, что вскрыла сверка: разрыв 13 дней.** Работа шла в ночь 16→17.09, а ретро я делаю **30.09**. И ночная догонялка `retro-lost` уже разобрала эту сессию **20.09** ([[retro-lost-2026-09-20-hub-desyatka-33-sessii]], вердикт «Keep, артефакты на диске, 3 из 4 тестов зелёные, четвёртый календарный ложный RED»). Поэтому это ретро — **дельта**, а не второй полный разбор.

## 🎬 Сегодня мы поняли

**Полоса времени жива и ведёт себя ровно так, как обещала.** Файлы целы, врезка в конвейер на месте, дефолт `off` держится (флага нет ни в `settings*.json`, ни в `machine.env`). T10 закрыт, вся программа из 10 шагов `done`.

**Close-don't-delete впервые сработал в бою, а не в тестах.** Индекс под слоем вырос за 13 дней с 7 846 до **23 084** файлов; сегодняшний `sync` добавил 14 128 рёбер и **закрыл 3** — три wikilink исчезли из заметок и получили `valid_to` вместо удаления. Живых рёбер теперь 83 921.

**Ночная догонялка оказалась права про мой тест, и я это подтвердил живым прогоном.** `_test_brain_temporal.py` краснел **по календарю**: первый `sync` шёл с реальной датой, а следующие версии писались захардкоженными `2026-09-17…22`. Пока календарь стоял до 18.09, порядок `ORDER BY valid_from` случайно совпадал с ожиданием; с 19.09 тест краснел каждый день, а продукт был цел.

**Мой счётчик использования врал в 987 раз, и нашёл это тоже ретро, а не сессия сборки.** В боевом файле накопилось 987 строк, из них боевой прогон **ровно один** (`files=7846`), остальные 986 — мои же тестовые фикстуры (`files=3` 584 шт, `files=6` 216, `files=5` 73) плюс 113 событий `apply`. Я выполнил правило «повесь счётчик» и не выполнил правило «изолируй тест от боевого лога» — метрика «живое или утиль» показывала бы активную деталь там, где в бою был один вызов.

**Обе поломки починены в этом же заходе** (карв-аут «артефакт этой же сессии»): часы теста фиксируются с первого прогона и сортировка идёт по обеим осям; путь счётчика стал параметром `BRAIN_TEMPORAL_COUNTER`, добавлен кейс приёмки T13, загрязнённый файл выведен как `*.polluted-by-tests-thru-20260930.jsonl`, чистый счёт начат. Доказано: боевой счётчик после прогона сетки **987 → 987, разница 0**; тестов теперь **49**, все зелёные, мутанты по-прежнему красные (`second` 3 · `cache` 2 · `case` 1 · `delete` 8 · `order` 3).

## 🎙 Вердикт Майка

💰 **деньги-линза:** прямой выручки ноль, но закрытая программа из 10 шагов — это готовый публичный материал жанра «мы померили и показали цифры», самый конвертящий у нас на GitHub и HN. Половина шагов кончилась откатом, и именно это честная история, которую другие не пишут.

🔪 **что убил бы:** гонку за числами на чужом движущемся индексе. Полчаса ночью ушло на таблицы, которые пришлось выбросить, потому что сосед переиндексировал волт под руками. Снимок индекса надо делать ПЕРВЫМ действием, а не после второго сюрприза.

🤺 **спарринг-аудит:** спорил честно и дважды выиграл спор с ТЗ (пустой источник gold; `supersedes` как «пункт», а не «заметка»), но один раз поддался своему же выводу и чуть не записал в канон ложь про несуществующий флаг — остановил сторож, не я.

❓ **вопрос:** включаем полосу времени по умолчанию, зная цену (temporal +0.130 против title −0.012), или она остаётся режимом «что верно сейчас» под флагом?

## ♻️ Keep / Drop / Try

| артефакт | вердикт | тест | перепроверено | куда |
|---|---|---|---|---|
| `brain_temporal.py` | 🟢 Keep | ✅ 49 проверок, 5 мутантов | ✅ повторный прогон линейки после починок панели, числа сошлись | `_imports`, паспорт в docstring |
| врезка в `brain_ask.dedup_best_per_file` | 🟢 Keep | ✅ соседние сетки 61/18/24/PASS | ✅ | за флагом, дефолт off |
| `eval/gold-temporal-2026-09-16.jsonl` (41 вопрос) | 🟢 Keep | ✅ оба плеча | ✅ | `_imports/eval` |
| `_test_brain_temporal.py` | 🟢 Keep | ✅ | ✅ починен сегодня дважды | `_imports` |
| метрика `dupes` | 🟢 Keep | ✅ на двух scores-файлах | ✅ 4.89% воспроизведено | подкоманда модуля |
| снимок индекса `eval/snap-t09.*` | 🟡 one-off | — | — | приём «свой снимок, когда сосед двигает индекс» стоит помнить |

## 🩹 Журнал поломок

Дозаписал три класса, которые в сессии были названы, но дверь не прошли: `eval-replay-mode-not-equal-fresh` (1/3), `sqlite-double-quoted-literal-is-a-column` (1/3), `counter-is-production-tests-must-not-write-it` (**2/3**, семья давно системная — легаси-строки 20.08 и 04.09). Плюс `sync-resolves-conflict-to-older-version` = 2, и честный хвост: мой дубль под именем `sync-conflict-left-node-on-stale-copy` слить дверью не дали, счёт семьи разъехался по именам.

## 🧠 Память · 🔗 Connect · 🚂 Рельсы

**🧠 память:** сирот моей сессии нет (найденные — чужие, припаркованы), анти-инъекция чисто (новых 0), два `SELF-TOMBSTONE` разобраны и **закрытию не подлежат**: первый автор сам пометил как намеренную «ПОКА-клаузу», второй живёт в проекте NODE-0X.

**🔗 Connect:** ✅ используется — 1 (слой зовут линейка и боевой `brain_ask`, доказано сегодняшним sync с тремя закрытиями) · 🔗 передано-ждёт — 1 (полоса `demote` ждёт решения о дефолте) · ⚠️ в воздух — 0. 🌍 мир: раздачи нет, слой завязан на наши колонки; в очередь `/share-fix` ушёл переносимый класс про счётчик, загрязнённый тестами.

**🔄 outcome:** правило «отсев запрещён, ранжирование вниз разрешено» было записано только в карточку — дверь краснела. Закрыто: память `bitemporal-demote-not-drop` + строка в `MEMORY.md`, повторная проверка даёт ✅ «след в always-loaded слое есть».

**🚂 рельсы:** `rail_plan.py verdict` → **exit 0, сверка закрыта** (codex/gemini/grok/glm/mistral жгли). Честно: плана на старте не было, потому что правило §6.3-бис родилось 21.09, а сессия шла 16-17.09 — задним числом проценты не выдумываю. Фактический аутсорс суждения был: панель `secondop` (codex + grok + gemini), 3 из 3 ответили и нашли 5 дефектов в моей же починке.

**⛳ дрифт:** цель = шаг 9. Унесло в две чужие темы (замер replay-режима линейки, sync-конфликт `help_flag_lint`) — обе закрыты по дороге, сессий не плодил.

**🗺 roadmap:** ➕1 — в Ship log добавлена веха «программа качества второй памяти закрыта: все 10 шагов вынесли вердикт числом, половина кончилась откатом или мержем за флагом».

**🎬 контент:** тизер в воронке — `cc:live-f49982` «Счётчик показал 987 использований. Настоящих был один».

## 🛠 Вердикты о скиллах

🔧 **обновил `/tt` (в прошлом заходе, сегодня подтверждаю правку):** шаг 3.5 теперь объясняет, что ответ «не понял аргумент `--check`» означает отставшую копию движка, а не отсутствие фичи, и даёт лечение через `copy_sweep`.

✅ **`/retro` обновлять не надо:** шаги 0 (разрыв времени), 2а (маркер робота) и 1🩹 (счёт по семье) сработали ровно по написанному и вытащили обе поломки; заминок не было.

📝 **своя инструкция (сид T09) — не сейчас:** сиды программы больше не рождаются, все 10 шагов закрыты; урок про протухшую премиссу уже лежит в программной карточке.

## 📌 Открытое

- Дефолт полосы времени: решение за тобой, цена названа числом.
- При включении — `sync` в ночную рутину перед линейкой (одним пакетом).
- Гонка двух писателей в БД и закрытие фактов по удалённым файлам — не проверено.
- Два имени у одного класса sync-конфликта: слияние на третьем случае.

## 🗜 Компакт

Заметка: `01-Conversations/Claude/Retros/retro-2026-09-30-sm-t09-bitemporal-delta.md` (линт чист, ссылка из MOC стоит).

➤ Скопируй блок целиком и вставь следующим сообщением

```
/compact Сохрани ДОСЛОВНО по 7 заголовкам (обоснования исчезают первыми):
- РЕШЕНИЯ — полоса времени второй памяти мержится ЗА ФЛАГОМ BRAIN_TEMPORAL=off|demote|drop, дефолт off: title nDCG -0.012 выше порога отката 0.01, и это свойство данных (у 3 вопросов замороженного gold правильный ответ сам закрыт), а не дефект. Жёсткий отсев valid_to IS NULL ЗАПРЕЩЁН, разрешено только ранжирование вниз. `supersedes` у НОВОЙ заметки не является закрытием старой (в волте это поле про ПУНКТ) — temporal-gold строится только по объявлению самой старой заметки. Данные в turnstate.db, а не в своём файле, потому что строки source_kind=human невосстановимы. Отвергнуто: drop по умолчанию, gold из 01-Rules и памяти (оба источника пусты и не в индексе), закрытие 8 «незакрытых версий» (7 из них живы законно).
- TODO — P1 решить про дефолт полосы (оператор); P1 при включении поставить brain_temporal.py sync в ночную рутину ПЕРЕД линейкой; P2 слить два имени класса sync-конфликта на третьем случае; P2 закрывать brain_facts по удалённым файлам; P2 разобраться, почему replay-режим линейки даёт не те числа, что свежий прогон.
- СЕЙЧАС — ретро T09 закрыто, обе всплывшие поломки починены (календарный тест, счётчик загрязнён тестами), всё закоммичено. Активной работы нет.
- ПУТИ И ЗНАЧЕНИЯ — D:\Vault\_imports\brain_temporal.py · _test_brain_temporal.py · brain_ask.py (dedup_best_per_file) · eval/gold-temporal-2026-09-16.jsonl · turnstate/turnstate.db (brain_edges, brain_facts, brain_temporal_conflicts) · ~/.claude/_counters/brain_temporal-HUB-01.jsonl (+ .polluted-by-tests-thru-20260930) · ручки BRAIN_TEMPORAL, BRAIN_TEMPORAL_COUNTER, BRAIN_TEMPORAL_TODAY, BRAIN_TEMPORAL_MUTANT · карточка 10-Tasks/task-2026-09-16-sm-T09-bitemporal-edges.md · ретро 01-Conversations/Claude/Retros/retro-2026-09-30-sm-t09-bitemporal-delta.md
- СЧЁТЧИКИ — temporal-gold 41 вопрос (было 4) · R@12 0.805 · nDCG 0.575→0.705 · дубли версий в top-12 7.61%→4.89% · title 0.927→0.915 · body 0.640→0.634 · bridge 0.223→0.223 · тестов 49 зелёных · мутантов 5 красных (3/2/1/8/3) · рёбер 83 921 (закрыто 3) · фактов 1963 · индекс 7846→23 084 файла · счётчик врал 987:1 · НЕ доделано: дефолт не включён, ночного sync нет.
- ОТКРЫТО — гонка двух писателей в БД не проверена; brain_facts по удалённому файлу не закрываются; класс eval-replay-mode-not-equal-fresh назван, но корень внутри _replay НЕ найден (гипотеза); счёт семьи sync-конфликта разъехался по двум именам, дедуп двери слить не даёт.
- ИНСТРУМЕНТЫ И КОНТРАКТЫ — brain_temporal.py <sync|status|closed|set|watch|gold|dupes|selftest> · brain_gold_eval.py --run --gold <файл> [--index-emb/--index-meta снимок] [--candidates замороженные] · звать ТОЛЬКО PYTHON_EXE из ~/.claude/machine.env (иначе os.execv даёт мгновенный exit 0 и пустоту) · счётчик изолируется env BRAIN_TEMPORAL_COUNTER · мутанты для красного теста BRAIN_TEMPORAL_MUTANT=second|cache|case|delete|order.
Сожми работающее до 1 строки + имена компонентов; выкинь отладку, тупиковые гипотезы, логи, переформулировки.
```

Готово, всё в волте. Остаёшься в сессии — вставь блок целиком (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — просто уходи, всё уже заархивировано.

🧒 **Простыми словами:** две недели назад я научил твою память понимать время: заметки теперь не стираются, а «закрываются» датой, и поиск может опускать устаревшие вниз. Сегодня я вернулся посмотреть, живо ли оно. Живо: за это время оно впервые само закрыло три устаревшие связи, а не удалило их. Но нашлись две мои оплошности. Первая: проверочный тест краснел просто потому, что наступило другое число — как будильник, который звонит от того, что месяц сменился. Вторая хуже: я повесил счётчик «сколько раз этим пользовались», он показал 987 раз, а на деле по-настоящему им пользовались **один** раз — остальные 986 накрутили мои же тесты. Обе починил, всё перепроверил. Включать новую способность по умолчанию я не стал: она помогает вопросам «что сейчас правда» и чуть мешает вопросам «найди заметку по названию», поэтому выключатель есть, а решение за тобой.
