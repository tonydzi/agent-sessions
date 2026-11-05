---
session: s_4bfde5c5
date: 2026-10-06
words: 4748
turns: 52
tools: "Bash, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · В ночную волну подач Трубы А проходят student-only вакансии, на которые оператор ([ВОЗРАСТ…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4bfde5c5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

В ночную волну подач Трубы А проходят student-only вакансии, на которые оператор ([ВОЗРАСТ], не студент) не может податься: анкета отбивает по году выпуска / статусу студента. Это тратит попытки и флагает компанию на сутки.

ЗАМЕР (06.10.2026, хаб HUB-01, боевая база D:\Vault\_imports\jobs-watch\jobs.db):
отбор `python -c "import pipe_a_night as P; P.select(sqlite3.connect('jobs.db'),150)"` вернул 129 строк, среди них пять student-only:
- Harvey, «Software Engineering Intern (Summer 2027)»
- Glean, «Software Engineer, Intern (Summer 2027)»
- Together AI, «Research Intern, Frontier Agents (Summer 2027)»
- Together AI, «Research Intern, Frontier Agents (Winter 2027)»
- Xaira Therapeutics, «AI Scientist Intern, Computational Protein Design»

Проверено, что это НЕ полоса одноклассников: при пустом `pipe_a_night.PEER_DOOR_CO` все пять остаются в волне, то есть приходят из ЛАБОРАТОРНОЙ полосы.

ПОЧЕМУ ТАК ПОЛУЧАЕТСЯ (гипотеза, требует подтверждения чтением кода, не словами):
- `pipe_a_night.BAD_LAB` намеренно НЕ режет токен `intern` у строк кластера 'lab-door' — это право из приказа оператора 01.10 «в лаборатории интерншип это легитимная нога в двери»;
- но тот же приказ отсекал student-only программы: в `jobs_discover.door_cluster` для этого есть `STUDENT_ONLY_RX` (new grad / campus / graduate / summer analyst). Шаблон «Summer 2027» / «Winter 2027» в формулировке «Research Intern, Frontier Agents (Summer 2027)» под него, судя по всему, не попадает;
- возможна и вторая дверь: колонка `elig` в ats_jobs и `selenium_apply/select_wave.py` (`intern_lane_ok`, условие `elig='open'`) — проверить, заполняется ли `elig` для этих строк вообще.

ЗАДАЧА:
1. Найти ТОЧНОЕ место, где student-only роль проходит, и доказать логом/выборкой, а не рассуждением (какая именно регулярка не совпала, на каком тайтле).
2. Починить корень, а не случай: правило должно резать класс «сезон+год» (Summer/Winter/Fall/Spring 20NN) и «Intern» в связке с годом выпуска, при этом НЕ задев легитимные для нас residency / fellowship / MTS-интерншип без студенческого гейта (право 01.10 на лаборатории).
3. Сторож с доказанной краснотой: прибор `python ~/.claude/scripts/red_proof.py`. ВАЖНО: при проверке в temp вези соседей через --also, включая D:\Vault\_imports\cv_forge.py, и СНАЧАЛА убедись, что целая копия в temp ЗЕЛЁНАЯ — иначе получишь ложное «КРАСНОЕ ДОКАЗАНО» (эта грабля наступлена 06.10: три ложных доказательства подряд из-за отсутствующего cv_forge).
4. Утверждение теста обязано называть ЧИСЛО, которое меняет поломка (сколько student-only строк в волне: было 5, стало 0), а не факт прохождения.
5. Проверить, не тянет ли та же дыра в batch_daily (у него условие-близнец: `WHERE status='new' AND (cluster='lab-door' OR title NOT LIKE '%intern%')` в jobs_discover около строки 716).

Файлы: D:\Vault\_imports\jobs-watch\pipe_a_night.py, jobs_discover.py (JUNK_RX, INTERN_OK_RX, STUDENT_ONLY_RX, door_cluster), selenium_apply/select_wave.py, тесты _test_pipe_a_night.py и _test_jobs_discover.py.

⚠️ КООРДИНАЦИЯ: 06.10 над этими файлами работали ДВЕ сессии параллельно (полоса одноклассников PEER_DOOR_CO и сортировка лабораторной полосы lab_order). Перед правкой сверься с `git log --oneline -10` в D:\Vault\_imports и объяви зону через onair.py, иначе затрёшь чужое.

---

**Claude:**

I'll start by coordinating (checking what other sessions did) and reading the actual code.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git log --oneline -10 2>&1; echo \"=== STATUS ===\"; git status --short 2>&1 | head -40", "description": "Check recent commits and status in _imports"}

---

> `Bash` -- {"command": "ls -la /e/Obsidian/_imports/jobs-watch/pipe_a_night.py /e/Obsidian/_imports/jobs-watch/jobs_discover.py /e/Obsidian/_imports/jobs-watch/_test_pipe_a_night.py /e/Obsidian/_imports/jobs-watch/_test_jobs_discover.py /e/Obsidian/_imports/jobs-watch/selenium_apply/select_wave.py 2>&1", "desc

---

**Claude:**

Uncommitted changes exist in `jobs_discover.py` — another session is mid-work there. Let me check the diff and declare my zone.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git diff --stat jobs-watch/jobs_discover.py jobs-watch/_test_jobs_discover.py 2>&1; echo \"=== DIFF HEAD ===\"; git diff jobs-watch/jobs_discover.py 2>&1 | head -80", "description": "Inspect uncommitted diff in jobs_discover"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"STUDENT_ONLY_RX\\|INTERN_OK_RX\\|JUNK_RX\\|def door_cluster\\|BAD_LAB\" jobs_discover.py 2>&1 | head -40", "description": "Locate the regex definitions"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '410,470p' jobs_discover.py", "description": "Read door_cluster"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '515,560p' jobs_discover.py", "description": "Read JUNK_RX / INTERN_OK_RX / STUDENT_ONLY_RX"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py zones 2>&1 | head -30", "description": "List onair zones"}

---

**Claude:**

Key miss already visible: `STUDENT_ONLY_RX` has `(20\d\d)\s+(summer|winter|spring)` — **year first**. The live titles are `(Summer 2027)` — **season first**. Let me prove it on real data before touching anything.

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone vault-imports/jobs-watch-student-gate --mode exclusive --what \"student-only роли в волне Трубы А: корень STUDENT_ONLY_RX (сезон+год)\" 2>&1 | head -20", "description": "Declare onair zone"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport re, sys\nsys.path.insert(0,'.')\nimport jobs_discover as J\ntitles = [\n 'Software Engineering Intern (Summer 2027)',\n 'Software Engineer, Intern (Summer 2027)',\n 'Research Intern, Frontier Agents (Summer 2027)',\n 'Research I

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone vault-imports/jobs-watch-student-gate --mode exclusive --title \"student-only в волне Трубы А: корень STUDENT_ONLY_RX (сезон+год)\" --summary \"правка STUDENT_ONLY_RX/JUNK_RX в jobs_discover.py + сторож; НЕ трогаю PEER_DOOR_CO и lab_order

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, sys\nsys.path.insert(0,'.')\nimport pipe_a_night as P\ncon = sqlite3.connect('jobs.db')\nrows = P.select(con, 150)\nprint('ВСЕГО В ВОЛНЕ:', len(rows))\nprint('тип строки:', type(rows[0]).__name__)\ntry:\n    print('ключ

---

**Claude:**

129 rows reproduced. Intersecting claims are Plaud work — different subtree. Now the exact student-only rows:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, sys, re\nsys.path.insert(0,'.')\nimport pipe_a_night as P, jobs_discover as J\ncon = sqlite3.connect('jobs.db')\nrows = P.select(con, 150)\nSEASON = re.compile(r'\\b(summer|winter|spring|fall|autumn)\\b', re.I)\nYEAR   

---

**Claude:**

Measurement reproduced exactly: **5 student-only + 1 legitimate open door** (`Scale AI / COLM 2026 - General Interest`, score 14 — note it carries a year `2026`, so a naive "any year" rule would kill it). Now the `elig` column and Xaira's real eligibility:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3\ncon = sqlite3.connect('jobs.db')\ncur = con.cursor()\ncur.execute(\\\"SELECT name FROM sqlite_master WHERE type='table'\\\")\nprint('таблицы:', [r[0] for r in cur.fetchall()])\ncur.execute('PRAGMA table_info(ats_jobs)')

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"intern_lane_ok\\|elig\" selenium_apply/select_wave.py 2>&1 | head -30", "description": "Check select_wave intern_lane_ok"}

---

**Claude:**

There IS a second door: `intern_gate.py` writes `elig` from job text, and `select_wave.intern_lane_ok` is fail-closed. Let me check `elig` for our 5 rows and whether `pipe_a_night` consults it at all:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3\ncon = sqlite3.connect('jobs.db'); con.row_factory=sqlite3.Row\nfor t in ['Software Engineering Intern (Summer 2027)','Software Engineer, Intern (Summer 2027)','Research Intern, Frontier Agents (Summer 2027)','Research I

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"elig\\|BAD_LAB\\|intern\" pipe_a_night.py 2>&1 | head -40", "description": "Check pipe_a_night for elig and BAD_LAB"}

---

**Claude:**

`intern_gate.py` **already judged 4 of 5 correctly** as `enrollment-gate` — the verdict was sitting in the DB and `pipe_a_night` never asked for it. That's a sharper root than a regex miss. Let me verify the duplicate-title ambiguity, the residency/fellowship population, and the batch_daily twin.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, sys\nsys.path.insert(0,'.')\nimport pipe_a_night as P\ncon = sqlite3.connect('jobs.db'); con.row_factory=sqlite3.Row\nprint('=== строки с этим тайтлом (дубль компаний?) ===')\nfor r in con.execute(\\\"SELECT company,tit

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, sys, re\nsys.path.insert(0,'.')\nimport jobs_discover as J\ncon = sqlite3.connect('jobs.db'); con.row_factory=sqlite3.Row\nRES = re.compile(r'\\b(residen(t|cy)|fellow(s|ship)?)\\b', re.I)\nprint('=== residency/fellowshi

---

**Claude:**

Decisive counterexample found: `Together AI, Systems Research Engineer Intern - GPU Programming (Summer 2027)` carries **`elig='open'`** — a legitimate lab internship with no student gate, and it has "Summer 2027" in the title. And every residency/fellowship (Anthropic Fellows, Perplexity, Extropic, 1X) already carries `elig='open'`.

So tightening the title regex on "season+year" — the hypothesis in the task — would **destroy a legitimate open lane**. Let me confirm the dead token and read the remaining doors.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, re\ncon = sqlite3.connect('jobs.db'); con.row_factory=sqlite3.Row\nYEARFIRST = re.compile(r'\\b20\\d\\d\\s+(summer|winter|spring|fall|autumn)\\b', re.I)\nSEASONFIRST = re.compile(r'\\b(summer|winter|spring|fall|autumn)\

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '700,735p' jobs_discover.py; echo \"=== intern_gate exists? ===\"; ls -la intern_gate.py 2>&1; echo \"=== how is it scheduled? ===\"; grep -rn \"intern_gate\" --include=*.py --include=*.md --include=*.cmd . 2>/dev/null | grep -v \"_test_\" | 

---

**Claude:**

Confirmed: the broken token catches **1** title, misses **44**. And `intern_gate.py` is **not scheduled anywhere** — purely manual, which is why 22105 rows have empty `elig`. Let me read `pipe_a_night.select()` and find the batch_daily twin.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"cluster='lab-door' OR title NOT LIKE\\|lab-door' OR title\\|status='new' AND (cluster\" jobs_discover.py 2>&1", "description": "Find batch_daily twin condition"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '96,175p' pipe_a_night.py", "description": "Read pipe_a_night select"}

---

**Claude:**

Now I have the exact spot. Let me read the remaining pieces: `KEYS`/`BAD_LAB` in pipe_a_night, the batch_daily twin at line 807, and how `select_wave` guards the missing column.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '60,95p' pipe_a_night.py; echo \"=== KEYS ===\"; grep -n \"^KEYS\\|^N_DEFAULT\\|^LAB_SHARE\\|^PER_COMPANY\" pipe_a_night.py", "description": "Read BAD_LAB and KEYS"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '795,830p' jobs_discover.py; echo \"=== select_wave guard ===\"; sed -n '236,250p' selenium_apply/select_wave.py", "description": "Read batch_daily twin and select_wave guard"}

---

**Claude:**

Full picture established. Let me measure the layer-1 title holes precisely before writing code.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, sys, re\nsys.path.insert(0,'.')\nimport jobs_discover as J\ncon = sqlite3.connect('jobs.db'); con.row_factory=sqlite3.Row\nSEASONFIRST = re.compile(r'\\b(summer|winter|spring|fall|autumn)\\s+20\\d\\d\\b', re.I)\nINTERN 

---

**Claude:**

Three genuine layer-1 leaks confirmed with live clusters — `Applied AI Engineer Co-op – Spring 2027` rides as **fde/8**, above the pack threshold. Now let me check the import wiring and write the fix.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"^LAB_DOOR\\s*=\\|^GIG_RX\\|^import\\|^from\\|jobs_discover\" pipe_a_night.py | head -20; echo \"=== jobs_discover LAB_DOOR ===\"; grep -n \"^LAB_DOOR\" jobs_discover.py", "description": "Check imports and LAB_DOOR constant"}

---

**Claude:**

Writing the fix. Layer 1 — title gates in `jobs_discover.py`:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYEOF'\nimport io, re\np = 'jobs_discover.py'\ns = io.open(p, encoding='utf-8').read()\n\nold_junk = '''JUNK_RX = re.compile(r\"\\\\bintern(ship)?\\\\b|\\\\bgraduate\\\\b|\\\\bcampus\\\\b|new grad|\"\n                     r\"\\\\bapprent

---

**Claude:**

Escaping got mangled through the heredoc. Let me write the patcher as a real file with raw strings.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch1.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч 1: title-ворота + intern_eligible в jobs_discover.py\"\"\"

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cp jobs_discover.py /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/jobs_discover.py.bak && python /c/Users/dev/AppData/Local/Temp/claude

---

**Claude:**

Layer 1 applied. Verifying it cuts the right things and preserves the open lane:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sys; sys.path.insert(0,'.')\nimport jobs_discover as J\ncases = [\n ('Applied AI Engineer Co-op - Spring 2027 (January Start)', None, 'ДОЛЖЕН срезаться (был fde/8)'),\n ('Network Planning Sales Engineer Associate (Winter 2027)',

---

**Claude:**

Layer 1 verified on all 10 cases. Now layer 2 — the elig gate. Let me see the existing import block:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '46,62p' pipe_a_night.py", "description": "Read pipe_a_night import block"}

---

**Claude:**

Now layer 2 — the eligibility gate in both selectors:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch2.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч 2: ворота eligibility в pipe_a_night.select() и jobs_disco

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cp pipe_a_night.py /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/pipe_a_night.py.bak && python /c/Users/dev/AppData/Local/Temp/claude/E

---

**Claude:**

Now the blind-zone report line and the `batch()` twin. Let me see where `select()` ends:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '185,250p' pipe_a_night.py", "description": "Read end of select()"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch3.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч 3: строка слепой зоны в pipe_a_night.select() + ворота в j

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/patch3.py 2>&1", "description": "Apply patch 3"}

---

**Claude:**

Now the measurement that matters — the number the fix changes:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, sys, re\nsys.path.insert(0,'.')\nimport pipe_a_night as P, jobs_discover as J\ncon = sqlite3.connect('jobs.db')\nrows = P.select(con, 150)\nprint()\nprint('ВОЛНА ПОСЛЕ ПОЧИНКИ:', len(rows), 'строк')\nINTERN = re.compile

---

**Claude:**

**5 → 0**, wave still 129 rows (freed slots refilled by legitimate roles), open door preserved, 28 intern rows cut with a loud blind-zone line. Now the guard. Let me match the existing test style:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '1,60p' _test_pipe_a_night.py", "description": "Read test file header and fixtures"}

---

**Claude:**

The test fixture has **no `elig` column** — so it exercises the fail-closed path. Let me run the existing suites to see what my change does to them:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && echo \"=== _test_pipe_a_night.py ===\" && python _test_pipe_a_night.py 2>&1 | tail -30; echo \"EXIT=$?\"", "description": "Run pipe_a_night test suite"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"u4\\|u18\" _test_pipe_a_night.py 2>&1 | head -20", "description": "Check assertions referencing intern rows"}

---

**Claude:**

Three failures, all one cause: lab interns with **no verdict** are now cut. The old fixture has no `elig` column at all, so those assertions encoded an unmodelled dimension. 

Fail-closed is the right call — it's the policy already documented in `select_wave.py:100` ("непроверенный интерншип не едет"), so I'm propagating an existing decision, not inventing one. But I must preserve dev's 01.10 right where a verdict says open. Let me model `elig` in the fixture and add the guard:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch4.py", "content": "#!/usr/bin/env python3\n\"\"\"Патч 4: колонка elig в фикстуре _test_pipe_a_night.py + блок S 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && tail -5 _test_pipe_a_night.py; echo \"--- applying ---\"; cp _test_pipe_a_night.py /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/_test_pi

---

**Claude:**

The file ends with `sys.exit` — appending after it would mean block S never runs. Let me insert before the final verdict instead:

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad && python - <<'PYEOF'\nimport io\np='patch4.py'\ns=io.open(p,encoding='utf-8').read()\n# блок S не должен нести свой итог/exit

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/patch4.py 2>&1 && echo \"--- RUN ---\" && python _test_pipe_a_night.py 2>&1 | grep -

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad && sed -n '155,165p' patch4.py", "description": "View broken tail of patch4"}

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad && python - <<'PYEOF'\nimport io\np='patch4.py'\nlines=io.open(p,encoding='utf-8').read().split('\\n')\n# найти индекс строки 

---

**Claude:**

Escaping layers are fighting me. Let me write a clean patcher with a single-line anchor:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch4b.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Патч 4b: колонка elig в фикстуре _tes

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/patch4b.py 2>&1 && echo \"--- RUN ---\" && python _test_pipe_a_night.py 2>&1 | grep 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python _test_pipe_a_night.py; echo \"EXIT=$?\"", "description": "Run test showing full output"}

---

**Claude:**

All original N1–N11 pass. Other inline INSERTs still use 11 positional values. Let me find and fix them:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"INSERT INTO ats_jobs\" _test_pipe_a_night.py", "description": "Find all inserts in test file"}

---

**Claude:**

Lines 107/124/126/128 insert 11 values into the now-12-column table. Let me name the columns explicitly (more robust than positional):

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYEOF'\nimport io\np='_test_pipe_a_night.py'\nlines=io.open(p,encoding='utf-8').read().split('\\n')\nCOLS=\"(url,company,title,ats,cluster,location,score,tier,status,applied,comp_min)\"\nn=0\nfor i in (106,123,125,127):   # 0-based = стр

---

**Claude:**

S9 fails — let me see what the gate actually printed:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sys, os, sqlite3, tempfile\nsys.path.insert(0,'.')\nimport pipe_a_night as P\nsdb = os.path.join(tempfile.mkdtemp(), 'jobs.db')\ncs = sqlite3.connect(sdb)\ncs.execute('CREATE TABLE ats_jobs (url TEXT PRIMARY KEY, company TEXT, t

---

**Claude:**

Real defect caught: `enrollment-gate=5` when only 4 rows have that verdict — the counter double-counts, because `take()` runs per lane and Glean sits in **both** the lab and peer lanes. A lying instrument is worse than none. Fixing:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYEOF'\nimport io\np='pipe_a_night.py'\ns=io.open(p,encoding='utf-8').read()\n\nold = '''    gate_cut = {\"enrollment-gate\": 0, \"gig-not-inside\": 0, \"no-verdict\": 0, \"other\": 0}'''\nnew = '''    gate_cut = {\"enrollment-gate\": 0,

---

**Claude:**

All 32 green. Now the `jobs_discover` side — let me run its suite and add the title-layer + batch block:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python _test_jobs_discover.py 2>&1 | tail -20; echo \"EXIT=$?\"; echo \"=== tail of file ===\"; tail -8 _test_jobs_discover.py", "description": "Run jobs_discover suite"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch5.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Патч 5: блок E в _test_jobs_discover.p

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cp _test_jobs_discover.py /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/_test_jobs_discover.py.bak && python /c/Users/dev/AppData/Local

---

**Claude:**

Both suites green. Now the red proof — with neighbors carried and the intact temp copy verified green first:

---

> `Bash` -- {"command": "python ~/.claude/scripts/red_proof.py --help 2>&1 | head -40", "description": "Read red_proof usage"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && ls *.py | tr '\\n' ' '; echo; echo \"=== что импортируют тесты ===\"; grep -hn \"^import \\|^from \\|^    import \\|    from \" _test_pipe_a_night.py _test_jobs_discover.py | grep -v \"^.*:import \\(os\\|sys\\|re\\|json\\|datetime\\|sqlite3\\|tempfi

---

**Claude:**

Noting a **Syncthing conflict copy** `jobs_discover.sync-conflict-20261006-155440-JR2M6T4.py` — I'll check it before committing. First, the red proof. Control run of the intact copy in temp:

---

> `Bash` -- {"command": "ls -la /e/Obsidian/_imports/cv_forge.py 2>&1; echo \"=== контрольный прогон ЦЕЛОЙ копии в temp ===\"\nT=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/ctl\nrm -rf \"$T\"; mkdir

---

**Claude:**

Exactly the trap the task warned about — the intact copy is **not green** in temp (missing `jobs_tg`, which silently emptied `PEER_DOOR_CO`). Carrying all neighbors:

---

> `Bash` -- {"command": "T=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/ctl\nrm -rf \"$T\"; mkdir -p \"$T\"\ncd /e/Obsidian/_imports/jobs-watch\nfor f in *.py; do case \"$f\" in *sync-conflict*) ;; *

---

**Claude:**

Control copy is **green** in temp. Now `red_proof.py` with the full neighbor set:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch\nALSO=\"\"\nfor f in *.py *.json; do case \"$f\" in *sync-conflict*|jobs_discover.py) ;; *) ALSO=\"$ALSO --also $f\" ;; esac; done\nALSO=\"$ALSO --also /e/Obsidian/_imports/cv_forge.py\"\necho \"соседей: $(echo $ALSO | grep -o ' --also' | wc -l)\"\npyt

---

**Claude:**

Red proven. Now let me show the **numbers** each breakage changes, in the verified-green control dir:

---

> `Bash` -- {"command": "T=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/ctl\ncd \"$T\"\nrun() {  # $1 = имя полома\n  echo \"=== ПОЛОМКА: $1 ===\"\n  python _test_pipe_a_night.py 2>&1 | grep -E \"^\\

---

**Claude:**

Numbers move (1→6, 1→2). Now the title layer, the border guard, and the counter:

---

> `Bash` -- {"command": "T=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/ctl\ncd \"$T\"\nrunE() { python _test_jobs_discover.py 2>&1 | grep -E \"E1 |E2 |E3 |E4 \" | sed 's/^/   /'; }\nrunS() { python 

---

**Claude:**

Breakages 3–5 silently **did not apply** (escape mangling again) — the tests only looked green. That's precisely the fake-check trap. Let me use `red_proof.py` with file-based patterns, which refuses when the breakage doesn't match:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\mk_snips.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Пишет пары old/new для red_proof.py 

---

> `Bash` -- {"command": "S=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad\npython \"$S/mk_snips.py\"\ncd /e/Obsidian/_imports/jobs-watch\nALSO=\"\"\nfor f in *.py *.json; do case \"$f\" in *sync-confli

---

**Claude:**

All three red-proven (red_proof verifies the replacement matched exactly once). Let me confirm *which* assertion each breakage kills — especially b5, the "tempting improvement":

---

> `Bash` -- {"command": "S=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad\nT=$S/ctl\ncd \"$T\"\nfor b in b3 b4 b5; do\n  python - \"$S/$b.old\" \"$S/$b.new\" <<'PY'\nimport io,sys\nold=io.open(sys.argv

---

**Claude:**

Each breakage kills exactly its own assertion with the number named (3→2, 6→1), and **b5 — the tempting "improvement" — kills the border guard E4**. Now let me check I didn't break neighbours. Running the whole suite:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && pass=0; fail=0; failed=\"\"\nfor t in _test_*.py; do\n  out=$(timeout 180 python \"$t\" 2>&1); rc=$?\n  if [ $rc -eq 0 ]; then pass=$((pass+1)); else fail=$((fail+1)); failed=\"$failed $t(rc=$rc)\"; fi\ndone\necho \"ЗЕЛЁНЫХ: $pass   КРАСНЫХ: $fail\"

---

**Claude:**

Two reds — let me determine whether they're mine or pre-existing:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && echo \"=== careers_feed ===\"; python _test_careers_feed.py 2>&1 | grep -E \"FAIL|Error|error\" | head -5; echo \"=== jobs_comp ===\"; python _test_jobs_comp.py 2>&1 | grep -E \"FAIL|Error|error\" | head -5", "description": "Inspect the two red test

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git stash list | head -3; echo \"=== являются ли они моими? прогон на HEAD-версии jobs_discover ===\"\nT=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchp

---

**Claude:**

Both were already red before my changes. But `_test_jobs_comp` touches `batch()`, which I edited — let me confirm the failures are identical, not merely both red:

---

> `Bash` -- {"command": "S=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad\ncd \"$S/pre\" && python _test_jobs_comp.py 2>&1 | grep -E \"^(OK|FAIL)\" | sort > \"$S/comp_before.txt\"\ncd /e/Obsidian/_impo

---

**Claude:**

Both reds are byte-identical before and after — pre-existing, from the other session's in-flight `careers_leg` work. 

Now the Syncthing conflict copy I spotted:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && ls -la jobs_discover.sync-conflict*.py; echo \"=== чем конфликтная копия отличается от того, что было ДО моих правок (HEAD+uncommitted) ===\"\ndiff <(cat /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB

---

**Claude:**

The conflict copy is **my own** intermediate state — Syncthing raced my write at 15:47, not another session. Let me confirm it's a strict subset before clearing it:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && C=jobs_discover.sync-conflict-20261006-155440-JR2M6T4.py\necho \"в конфликтной копии:\"\nfor t in \"def intern_eligible\" \"_SEASON_YEAR\" \"ворота eligibility срезали\" \"_elig = \\\"elig\\\"\"; do\n  printf \"   %-34s %s\\n\" \"$t\" \"$(grep -c \"

---

**Claude:**

**Important catch — the relationship is reversed.** The conflict copy holds my `batch()` gate; the **live file lost it** — Syncthing overwrote my patch3 edit. And my tests didn't notice, because E6/E7 exercise the predicate rather than `batch()` itself. Let me check the full extent of the loss:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && C=jobs_discover.sync-conflict-20261006-155440-JR2M6T4.py\necho \"=== есть в ЖИВОМ, но нет в конфликте (некомментарные) ===\"\ndiff \"$C\" jobs_discover.py | grep '^>' | grep -v '^> *#' | grep -v '^> *$' | head -10\necho \"(таких строк: $(diff \"$C\"

---

**Claude:**

Confirmed: the live file lost exactly the `batch()` gate and nothing else. Re-applying it:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/patch3.py 2>&1 | tail -3\necho \"=== сверка с конфликтной копией ===\"\ndiff jobs_di

---

**Claude:**

patch3 aborted on its already-applied pipe_a_night half. Applying just the `batch()` half:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch3b.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Патч 3b: ТОЛЬКО ворота eligibility в 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad/patch3b.py && echo \"=== сверка с конфликтной копией ===\" && (diff jobs_discover.sy

---

**Claude:**

Converged. Now I must close the hole that let this loss go unnoticed — E6/E7 test the *predicate*, not `batch()` itself. Let me add an end-to-end guard:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -n \"^DB\\s*=\\|^def batch\\|^def ensure_schema\" jobs_discover.py | head; echo \"=== CV_FILE ключи ===\"; python -c \"\nimport sys; sys.path.insert(0,'.')\nimport jobs_discover as D\nprint('DB =', D.DB)\nprint('CV_FILE keys:', list(D.CV_FILE)[

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_4bfde5c5\\scratchpad\\patch6.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"Патч 6: E8 -- СКВОЗНОЙ прогон jobs_dis

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && head -20 _test_jobs_discover.py | grep -n \"^import\\|^from\"; echo \"--- apply ---\"; python /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchp

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad && python - <<'PYEOF'\nimport io\np='patch6.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace(\"    anchor = 'import sys\

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad && grep -n \"anchor = \" patch6.py; echo \"--- в тесте: ---\"; sed -n '1,6p' /e/Obsidian/_imports/jobs-watch/_test_jobs_discov

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad && sed -i \"68s/.*/    anchor = 'import sys, os' + chr(10)/\" patch6.py && sed -n '68p' patch6.py\ncd /e/Obsidian/_imports/job

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python _test_jobs_discover.py 2>&1 | tail -12", "description": "See E8 result"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -i '3a import sqlite3' _test_jobs_discover.py && sed -n '1,10p' _test_jobs_discover.py && echo \"--- RUN ---\" && python _test_jobs_discover.py 2>&1 | tail -6; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Add sqlite3 import and run"}

---

**Claude:**

E8 green. Now red-prove it — it must catch exactly the loss Syncthing caused:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYEOF'\nimport io\np='_test_jobs_discover.py'\ns=io.open(p,encoding='utf-8').read()\ns=s.replace(\"import contextlib\\nimport io\\nimport os\\nsys.path.insert\",\"import contextlib\\nimport io\\nsys.path.insert\",1)\nio.open(p,'w',encodi

---

**Claude:**

Red proven for the batch gate too. Let me finalize and then do the retro.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && pass=0; fail=0; failed=\"\"\nfor t in _test_*.py; do out=$(timeout 180 python \"$t\" 2>&1); rc=$?\n  if [ $rc -eq 0 ]; then pass=$((pass+1)); else fail=$((fail+1)); failed=\"$failed $t\"; fi; done\necho \"ИТОГОВЫЙ ПРОГОН: зелёных $pass, красных $fai

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && S=/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_4bfde5c5/scratchpad\nmv jobs_discover.sync-conflict-20261006-155440-JR2M6T4.py \"$S/\" && echo \"конфликтная 

---

**Claude:**

Only my 4 files are staged; the other session's work stays untouched. Committing with provenance trailers:

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git log -1 --format='%B' 63ea11ec | tail -8", "description": "Check trailer format of recent commit"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git commit -q -F - <<'MSG' && git log --oneline -1\nТруба А: student-only стажировки не едут в волну -- спрашиваем elig, а не тайтл\n\nЗАМЕР (боевая jobs.db, отбор на 150): в волне 129 строк ехали ПЯТЬ student-only\nстажировок -- Harvey, Glean, Together AI x2 

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close --zone vault-imports/jobs-watch-student-gate 2>&1 | tail -3; echo \"=== интерншип-гейт в расписании? ===\"; python ~/.claude/scripts/selfheal.py journal --class jobs-watch-student-only-gate --what \"ворота eligibility не спрашивались двумя ночными

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py list 2>&1 | grep -i \"student-gate\" ; python ~/.claude/scripts/onair.py close --help 2>&1 | head -8", "description": "Find correct close syntax"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close 2026-10-06T143931Z-HUB-01-c96f6010-vault-imports-jobs-watch-student-gate 2>&1 | tail -3", "description": "Close onair claim by id"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\assertion-on-a-part-does-not-guard-its-call-site.md", "content": "---\nname: assertion-on-a-part-does-not-guard-its-call-site\ndescription: Тест, зовущий предикат напрямую, зелёный даже когда вызов предиката вы

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\season-year-is-not-a-student-signal.md", "content": "---\nname: season-year-is-not-a-student-signal\ndescription: «Summer 2027» в тайтле не признак студенческой программы; eligibility живёт в тексте вакансии (к

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && python - <<'PYEOF'\nimport io\np='MEMORY.md'\ns=io.open(p,encoding='utf-8').read()\nanchor='## 📥 INBOX'\ni=s.index(anchor); j=s.index('\\n', s.index('\\n', i)+1)\nnew = (\"\\n- [«Summer 2027» не признак студента](

---

**Claude:**

Line count looks lower than the 255 reported at session start — let me verify I didn't truncate it:

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && ls -la MEMORY.md && echo \"строк: $(wc -l < MEMORY.md)  байт: $(wc -c < MEMORY.md)\" && echo \"=== разделы на месте? ===\" && grep -c \"^## \" MEMORY.md && grep \"^## \" MEMORY.md && echo \"=== мои 2 строки ===\" 

---

> `Bash` -- {"command": "date \"+%H:%M %d.%m.%Y\"; cd /e/Obsidian/_imports && git show --stat --format=\"\" HEAD", "description": "Time and final diffstat"}

---

**Claude:**

*16:06 06.10.2026*

## Ретро сессии — student-only в волне Трубы А

### Что просили и что вышло
**5 → 0** student-only стажировок в волне, волна осталась 129 строк, открытая дверь `Scale AI / COLM 2026` на месте. Коммит `38273af7`.

### Главное: гипотеза в задаче была неверной, и это хорошо, что проверил
Задача предполагала корень в `STUDENT_ONLY_RX` (сезон+год). Регулярка действительно сломана — токен стоял только в порядке «2027 Summer», а доски пишут «(Summer 2027)»; в базе год-первым **1** тайтл, сезон-первым **44**.

Но чинить надо было **не это**. Живая база дала контрпример: `Together AI / Systems Research Engineer Intern - GPU Programming (Summer 2027)` имеет `elig='open'` — тот же сезон и год, но без студенческого гейта. Доработай я регулярку, как просили, — молча убил бы открытую лабораторную дверь, то есть ровно то, что оператор разрешил 01.10.

**Настоящий корень:** вердикт уже лежал в базе. `intern_gate.py` прочитал текст вакансий и поставил `enrollment-gate` четырём из пяти. Политика «едет только `elig=open`» была реализована **правильно в одной двери из трёх** (`select_wave.intern_lane_ok`), а два ночных селектора её просто не спрашивали. Знакомый класс: лечение лежит в одной двери, новый прогонщик за ним не пришёл.

### Инцидент внутри сессии (Keep — урок дороже самой починки)
Гонка Syncthing в 15:47 **откатила живой файл** к версии без ворот в `batch()`. Мои тесты E6/E7 остались **зелёными** — они зовут предикат напрямую, а не `batch()`. Нашёл глазами, по имени `.sync-conflict`-файла, а не прибором. Добавил сквозной E8, который дёргает настоящую `batch()` и считает число (2 из 5; без ворот — 5), красное доказано.

Побочно поймал **врущий счётчик**: `enrollment-gate=5` при четырёх строках — полосы пересекаются (Glean и в лабораториях, и в одноклассниках), счёт шёл по проходу, а не по ссылке.

### Доказательства
- 18 новых утверждений, каждое называет **число**, которое меняет поломка (S1 считает волну дважды в одном прогоне: 6 → 1).
- Красное доказано `red_proof.py` на **7** поломках. Целая копия в temp предварительно проверена **зелёной** — и это было не формальностью: первый контрольный прогон упал на отсутствующих соседях (`jobs_tg`), что молча обнулило `PEER_DOOR_CO`. Везу 106 соседей, включая `cv_forge.py`.
- Отдельно поймал три **ложных «красных доказательства»**: поломка не применялась из-за съеденных экранов, а тест выглядел «устойчивым». Поэтому финальные проверки — только через `red_proof.py`, который требует ровно одного совпадения.

### Что НЕ сделано (явно)
- **`intern_gate.py` нигде не стоит в расписании.** Пустых `elig` — 22105 против 76 отсуженных. Поэтому fail-closed сейчас режет и неизвестно-открытые стажировки: в волне это `no-verdict=7`. Ворота об этом **кричат строкой**, но лечится прогоном гейта, а не ослаблением фильтра. Это главный открытый долг.
- `select_wave.intern_lane_ok` намеренно не трогал: у него другая семантика (override для `BAD_TITLE`), подмена предиката там — регрессия.
- `_test_careers_feed` и `_test_jobs_comp` красные, но были красными **до** моих правок байт-в-байт (чужая незакоммиченная работа по `careers_leg`). Проверил диффом выводов, не на глаз.
- Расхождение: на старте сессии система сообщила про MEMORY.md «255 строк, 53.2KB», на диске — 137 строк, 21KB. Все 6 разделов целы, мои 2 строки добавлены. Причину расхождения не выяснял.

### 🧒 Простыми словами
Робот ночью рассылал заявки на работу и среди них слал **студенческие стажировки** — а тебе [ВОЗРАСТ], анкета таких сразу выкидывает, и попытка сгорает зря.

Я сначала хотел, как просили, ловить их по названию — там написано «Summer 2027». Но проверил по настоящей базе и увидел: у одной хорошей вакансии в лаборатории **точно такое же название**, а студентов она не требует. То есть по названию судить нельзя — выкинул бы хорошее вместе с плохим.

Оказалось, правильный ответ уже лежал рядом: другой робот заранее **прочитал текст** каждой вакансии и честно пометил, где нужен студент. Просто никто его не спрашивал. Теперь спрашивают — и плохих стало **ноль**, а хорошие остались.

Ещё по дороге случилась неприятность: синхронизация между компьютерами **откатила кусок моей починки назад**, а проверки этого не заметили — они щупали деталь, а не то место, где её включают. Починил и добавил проверку, которая теперь это ловит.
