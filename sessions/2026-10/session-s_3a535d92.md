---
session: s_3a535d92
date: 2026-10-02
words: 4893
turns: 52
tools: "Bash, Edit, PowerShell, ToolSearch, Write, get_page_text, mcp__Claude_Browser__browser_batch, mcp__Claude_Browser__computer, mcp__Claude_Browser__get_page_text, mcp__Claude_Browser__preview_start, mcp__Claude_Browser__read_page, mcp__telegram__send_message"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-02 · Scheduled run: intern-fellows-lane-20261002

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3a535d92` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="intern-fellows-lane-20261002" file="C:\Users\dev\.claude\scheduled-tasks\intern-fellows-lane-20261002\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Задача от оператора (01.10.2026, голосом: «Интерн-феллоус полоса... согласен полностью, это роли с низкой конкуренцией... пункт 3 максимально копаю в этом направлении, отдельная сессия»). Канон: Библия reglament-vnutr-ii-laboratorii §Поправка 01.10 (интерншип в лабе = легитимная нога в двери), [[mission-metric-100-interviews]].

RECALL первым ходом. Рабочая папка: D:\Vault\_imports\jobs-watch\.

В jobs.db уже лежит урожай (замер 01.10): 46 intern-ролей + 26 fellows/residency с кластером lab-door (Cohere SWE Intern Winter 2027, Perplexity Search ML Internship, Together AI Research Intern ×7, Anthropic Fellows ×3, Mistral Applied Scientist Internship, Extropic/Normal Computing Residents, 1X AI Residency, Chai Discovery Internship).

Работа:
1. Выбрать из базы ВСЕ intern/fellows/residency роли лабораторий: SELECT по cluster='lab-door' + регулярка \bintern(ship)?\b|fellow|residen по title. Отранжировать: fellows/residency первыми (конверсия в штат), потом research/engineering intern, потом остальное.
2. По каждой проверить eligibility ЧЕСТНО по тексту вакансии (многие intern-роли требуют текущего enrollment — такие пометить enrollment-gate и НЕ подавать, это ворота анкеты, не наша трусость; Fellows/Residency обычно без него).
3. На проходящие — подать через обычный конвейер (/apply механика, answers_canon, CV-ветка research или product). В мотивационных полях: оператор идёт учиться и строить внутри, 15+ лет инженерии, PhD; слово «overqualified» не вносим, не оправдываемся.
4. Доска DeepMind/Meta: проверить их intern/residency страницы руками (lab_hand.py add).
5. Доклад: TG-03 через bus_send.py «intern-lane: X ролей, Y подано, Z enrollment-gate».

Правила: правда в цифрах (возраст/опыт не трогаем, он не студент и это ок — канон 01.10), «фаундер»/«не-кодер» запрещены, оффер = Tier-2. Не доделал — продолжение завтра. /tt перед «готово».
</scheduled-task>

---

**Claude:**

Начинаю. Сперва RECALL и разведка базы.

**🚂 План рельс (§6.3-бис):** сам как Claude — SQL по `jobs.db`, eligibility-разбор текстов вакансий, подача через конвейер `/apply`, доклад в шину. На чужой бак — ничего не планирую: задача про наши приборы и наши анкеты, LLM-суждение тут не нужно (`no-work` по чужим рельсам, назову на ретро).

---

> `PowerShell` -- {"command": "Get-Date -Format \"yyyy-MM-dd HH:mm:ss zzz\"; Write-Output \"--- UTC ---\"; (Get-Date).ToUniversalTime().ToString(\"yyyy-MM-dd HH:mm:ss\")", "description": "Get current local and UTC time"}

---

> `PowerShell` -- {"command": "Get-ChildItem \"D:\\Vault\\_imports\\jobs-watch\\\" | Select-Object Name, Length, LastWriteTime | Sort-Object Name | Format-Table -AutoSize", "description": "List jobs-watch directory"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor r in c.execute(\\\"select name from sqlite_master where type='table' order by name\\\"):\n    print(r[0])\n\"", "description": "List tables in jobs.db"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/ | grep -iE \"apply|intern|fellow|lab|job|mission|cv\" ", "description": "Recall memory files about jobs/apply"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/ && for f in get-inside-the-lab-at-any-position.md mission-metric-100-interviews.md apply-canon-answers-yourself.md apply-never-ask-just-send.md apply-proof-of-delivery.md pipe-a-apply-elephant.md; do echo \"=== $f =

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor t in ['jobs','ats_jobs']:\n    print('===',t)\n    for r in c.execute(f'PRAGMA table_info({t})'):\n        print(r[1], r[2])\n    print('count', c.execute(f'select count(*) from {t}').f

---

**Claude:**

Контекст поднят. Теперь замер по базе.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, re\nc=sqlite3.connect('jobs.db')\nc.row_factory=sqlite3.Row\nrx=re.compile(r'\\b(intern|internship|interns|fellow|fellowship|fellows|residen|resident|residency)\\b', re.I)\nrows=[dict(r) for r in c.execute(\\\"select * 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, re\nfrom collections import Counter\nc=sqlite3.connect('jobs.db'); c.row_factory=sqlite3.Row\nrx=re.compile(r'\\b(intern|internship|interns|fellow|fellowship|fellows|residen|resident|residency)\\b', re.I)\nrows=[dict(r)

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python -c \"\nimport sqlite3, re, json\nc=sqlite3.connect('jobs.db'); c.row_factory=sqlite3.Row\nrx=re.compile(r'\\b(intern|internship|interns|fellow|fellowship|fellows|residen|resident|residency)\\b', re.I)\nrows=[dict(r) for r in c.execute(\\\"sel

---

**Claude:**

Выборка готова: 72 роли. Теперь честная проверка eligibility по тексту вакансий — смотрю, есть ли готовый фетчер в конвейере.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -nE \"def (fetch|_get|http|ashby|greenhouse)|posting-api|boards-api|descriptionPlain\" jobs_discover.py | head -40; echo \"=== resolve_door ===\"; grep -nE \"def |posting-api|boards-api\" resolve_door.py | head -30; echo \"=== selenium_apply ==

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '430,470p' jobs_discover.py; echo \"=== selenium_apply rest ===\"; ls selenium_apply/ | grep -v \"^_test\" ", "description": "Read fetch() and list apply engine files"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -nE \"INTERN_OK_RX|STUDENT_ONLY_RX|LAB_JUNK_RX\" jobs_discover.py | head; echo \"---\"; python - <<'EOF'\nimport re,io\nsrc=open('jobs_discover.py',encoding='utf-8').read()\nfor name in ['INTERN_OK_RX','STUDENT_ONLY_RX','LAB_JUNK_RX']:\n    i=s

---

**Claude:**

Регулярка `STUDENT_ONLY_RX` ловит «2027 Summer», но не «Summer 2027» — проверю это отдельно. Сперва строю прибор eligibility по тексту вакансий.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'EOF'\nimport urllib.request, json\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/131.0 Safari/537.36\"\ndef g(u, acc=\"application/json\"):\n    r=urllib.request.Request(u, headers={\"User-Agent\":UA,\"Accept\"

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cat > intern_gate.py <<'PYEOF'\n# -*- coding: utf-8 -*-\n\"\"\"intern_gate.py -- ЧЕСТНЫЙ eligibility-гейт для интерн/феллоус/residency полосы лабораторий.\n\nЗАЧЕМ. Канон 01.10 (Библия `reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna`

---

**Claude:**

Heredoc споткнулся на кавычках в регулярках — пишу файл напрямую.

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"intern_gate.py -- ЧЕСТНЫЙ eligibility-гейт для intern/fellows/residency полосы лабораторий.\n\nЗАЧЕМ. Канон 01.10 (Библия `reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna`\n§

---

**Claude:**

Теперь red-first тест с kill-list.

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\jobs-watch\\_test_intern_gate.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"_test_intern_gate.py -- сторож eligibility-гейта intern/fellows полосы.\n\nKILL-LIST (что обязано краснеть, если прибор испортят) -- фразы взяты из РЕАЛЬНЫХ\nтекстов вакансий, добытых

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python _test_intern_gate.py 2>&1 | tail -30; echo \"EXIT=$?\"", "description": "Run intern_gate test"}

---

**Claude:**

Зелёный. Теперь доказываю, что он КРАСНЕЕТ на сломанном коде (§5.4).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cp intern_gate.py /tmp/ig.ok.py && python - <<'EOF'\nimport re\np='intern_gate.py'\ns=open(p,encoding='utf-8').read()\n# поломка 1: убрать правило currently-enrolled\ns=s.replace('(\"currently-enrolled\", r\"currently\\\\s+enrolled\"),','')\n# полом

---

**Claude:**

Red-first доказан (7 провалов, exit 1). Гоняю прибор по живой полосе.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && timeout 900 python intern_gate.py --include-skipped --json _scratch/intern_gate_1002.json 2>&1 | tail -120", "description": "Run eligibility gate on full lane"}

---

**Claude:**

100% покрытие, 0 слепых. Теперь ВТОРОЙ заход другим методом по вердиктам «open» — выгодный вывод требует усиленной проверки (§5.4).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'EOF'\nimport json, re, sys\nsys.path.insert(0,'.')\nimport intern_gate as ig\nrows=json.load(open('_scratch/intern_gate_1002.json',encoding='utf-8'))\nop=[r for r in rows if r['verdict']=='open']\nWORDS=re.compile(r\"\\b(student|students

---

**Claude:**

Второй заход нашёл 4 дыры в моей регулярке. Сперва разберу спорный Scale HFC (гиг-мельница или нет).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'EOF'\nimport sys; sys.path.insert(0,'.')\nimport intern_gate as ig\nfor u,label in [(\"https://job-boards.greenhouse.io/scaleai/jobs/id_5a48f42d\",\"Scale SWE Fellow US\"),\n                (\"https://jobs.ashbyhq.com/physicalintelligence

---

**Claude:**

Два важных вывода второго захода:

**Scale AI «Human Frontier Collective Fellowship» = гиг-мельница в бейдже феллоушипа.** Дословно из вакансии: `"This is a fully remote, 1099 independent contractor opportunity"`, `"flexible 10–40 hour weeks"`, `"Project pay rates vary across platforms"`, работа = создание датасетов для «partnered AI labs and platforms». Канон отсекает вендорский бейдж и гиг-мельницу — слово «Fellows» в заголовке было прокси, а суть противоположна. 13 строк Scale HFC выбывают.

Плюс моя регулярка пропускала «Progress towards a degree», «Graduating in Fall 2026», и наоборот ворочала там, где стоит «Nice to have / Preferred». Чиню на два яруса — hard/soft.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "old_string": "ENROLL_PATTERNS = [\n    (\"currently-enrolled\", r\"currently\\s+enrolled\"),", "new_string": "ENROLL_PATTERNS = [\n    (\"currently-enrolled\", r\"currently\\s+enrolled\"),\n    (\"progress-tow

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "old_string": "ENROLL_RX = [(name, re.compile(rx, re.I)) for name, rx in ENROLL_PATTERNS]\n\n_ashby_cache = {}", "new_string": "ENROLL_RX = [(name, re.compile(rx, re.I)) for name, rx in ENROLL_PATTERNS]\n\n# СМ

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "old_string": "def enrollment_verdict(text):\n    \"\"\"-> {'verdict': 'open'|'enrollment-gate'|'no-text', 'hits': [{'rule','quote'}]}.\"\"\"\n    if not (text or \"\").strip():\n        return {\"verdict\": \"

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYX'\nimport io\np='intern_gate.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('''    counts = {\"open\": 0, \"enrollment-gate\": 0, \"no-text\": 0}''',\n            '''    counts = {\"open\": 0, \"enrollment-gate\": 0, \"gig-not

---

**Claude:**

Обновляю сторож под двухъярусную логику.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\_test_intern_gate.py", "old_string": "print()\nif FAILS:", "new_string": "# --- L13..L15: СМЯГЧИТЕЛИ. Та же фраза в рамке \"nice to have\" ворот не делает. --------\nprint(\"L13-L15 пожелание про диплом НЕ ворота (иначе теряем 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python _test_intern_gate.py 2>&1 | grep -E \"FAIL|КРАСНО|ЗЕЛЕНО|^L1[3-9]|^L2[01]|^L16\" ; echo \"EXIT=${PIPESTATUS[0]}\"", "description": "Run updated test"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && cp intern_gate.py /tmp/ig2.ok.py && python - <<'PYX'\nimport io\np='intern_gate.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace('strength = \"soft\" if SOFTENER_RX.search(window) else \"hard\"','strength = \"hard\"')  # смягчителей нет\ns=s.r

---

**Claude:**

Red-first подтверждён и для новых правил (10 провалов). Прогоняю исправленный гейт по полосе.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && timeout 900 python intern_gate.py --include-skipped --json _scratch/intern_gate_1002.json 2>&1 | grep -E \"^(OK|GATE|GIG|BLIND)|^всего|^не могу|^json\" | head -90", "description": "Re-run gate with fixed logic"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "old_string": "    print(\"\\nвсего %d | open %d | enrollment-gate %d | no-text %d\"\n          % (n, counts[\"open\"], counts[\"enrollment-gate\"], counts[\"no-text\"]))", "new_string": "    print(\"\\nвсего %

---

**Claude:**

38 ролей проходят. Смотрю конвейер подачи и не бегает ли уже волна.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && head -60 run_slice.py; echo \"=== select_wave ===\"; head -40 select_wave.py", "description": "Read run_slice and select_wave headers"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && echo \"=== run_1002_LIVE.out tail ===\"; tail -25 run_1002_LIVE.out 2>/dev/null; echo \"=== run_night_2026-10-02.out tail ===\"; tail -20 run_night_2026-10-02.out 2>/dev/null; echo \"=== recent applied in db ===\"; cd .. && python -c 

---

**Claude:**

Селектор волн режет intern-заголовки (`BAD_TITLE`) — это пре-01.10 фильтр. Чиню класс, а не случай: вердикт гейта поедет в базу, селектор станет его читать.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && grep -n \"BAD_TITLE\" select_wave.py | head; echo \"---\"; python - <<'PYX'\nimport io,re\ns=io.open('select_wave.py',encoding='utf-8').read()\ni=s.find('BAD_TITLE')\nprint(s[i:i+900])\nPYX", "description": "Read BAD_TITLE filter in s

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -nE \"COLS|expected|column|PRAGMA table_info\" jobs_db_guard.py | head -20; echo \"=== running procs ===\"; powershell -NoProfile -Command \"Get-Process python,chrome,chromedriver -ErrorAction SilentlyContinue | Group-Object ProcessName | Selec

---

**Claude:**

34 chrome + 29 python живых, база менялась 11 минут назад — проверяю, не бежит ли волна прямо сейчас.

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-CimInstance Win32_Process -Filter \\\"Name='python.exe'\\\" | Select-Object ProcessId, CreationDate, @{n='cmd';e={\\$_.CommandLine.Substring(0,[Math]::Min(160,\\$_.CommandLine.Length))}} | Sort-Object CreationDate -Descending | Format-List\" 2>&1 | h

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && ls -lt runs/ | head -8; echo \"=== newest .out ===\"; ls -lt *.out 2>/dev/null | head -4", "description": "Check newest run artifacts"}

---

**Claude:**

Полоса свободна (последняя волна финишировала 19:45). Смотрю точку фильтра в селекторе.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && sed -n '85,100p;205,245p' select_wave.py", "description": "Read select_wave filter block"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && python - <<'PYX'\nimport io\ns=io.open('select_wave.py',encoding='utf-8').read()\nfor k in ['BAD_LOC','US_HINT']:\n    i=s.find(k+' =')\n    print('>>>',k); print(s[i:i+420].split('\\n\\n')[0]); print()\nPYX\ncd .. && python -c \"\nim

---

**Claude:**

Anthropic Fellows — главная цель полосы, и в тексте стоит отдельная ссылка на подачу. Читаю её целиком.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYX'\nimport sys, json, re, urllib.request, html\nsys.path.insert(0,'.')\nimport intern_gate as ig\nd=json.loads(ig._get(\"https://boards-api.greenhouse.io/v1/boards/anthropic/jobs/id_2e26dffe\"))\nraw=html.unescape(d.get(\"content\",\"\"

---

> `Bash` -- {"command": "cat \"/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/dev-eu-polish-passport.md\"; echo \"=== relocation ===\"; cat \"/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/relocation-is-on-the-table.md\" 2>/dev/null | head -20", "description": "Read w

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && python - <<'PYX'\nimport urllib.request\nUA=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/131.0 Safari/537.36\"\nclass NoRedir(urllib.request.HTTPRedirectHandler):\n    def redirect_request(self,req,fp,code,msg,hdrs,newurl):\

---

**Claude:**

Право на работу сверено: O-1 США активна → US-роли проходят; Париж проходит по польскому паспорту; UK/Канада без спонсорства. Anthropic Fellows подаётся через отдельную Airtable-форму, не через Greenhouse — это отдельная дверь.

Теперь вшиваю вердикт гейта в базу, чтобы селектор и ночная рутина его видели.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "old_string": "    ap.add_argument(\"--limit\", type=int, default=0)\n    a = ap.parse_args(argv)", "new_string": "    ap.add_argument(\"--limit\", type=int, default=0)\n    ap.add_argument(\"--write-db\", acti

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\intern_gate.py", "old_string": "    if a.out_json:\n        with open(a.out_json, \"w\", encoding=\"utf-8\") as f:\n            json.dump(res, f, ensure_ascii=False, indent=1)\n        print(\"json -> \" + a.out_json)\n    retu

---

**Claude:**

Теперь карв-аут в селекторе волн: intern-заголовок выживает только если это лаборатория и гейт сказал `open`.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "            or BAD_TITLE.search(r[\"title\"] or \"\")", "new_string": "            or (BAD_TITLE.search(r[\"title\"] or \"\") and not intern_lane_ok(r))"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "BAD_TITLE = re.compile(", "new_string": "# КАРВ-АУТ ПОЛОСЫ ЛАБОРАТОРИЙ (канон 01.10, Библия\n# `reglament-vnutr-ii-laboratorii-lyuboy-cenoy-poziciya-ne-vazhna` §Поправка 01.10,\n#

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "    rows = c.execute(\n        f\"SELECT url, company, ats, title, location, tier, cluster, score, {pay_sql} AS pay \"\n        \"FROM ats_jobs WHERE status='new' AND ats IN ('ash

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && timeout 900 python intern_gate.py --include-skipped --write-db --json _scratch/intern_gate_1002.json 2>&1 | tail -4; echo \"=== elig в базе ===\"; python -c \"\nimport sqlite3; c=sqlite3.connect('jobs.db')\nfor r in c.execute(\\\"select elig, count(

---

**Claude:**

Селектор пропатчен. Добавляю ему флаг на эту полосу и проверяю выборку.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && grep -n \"def pick\\|def main\\|add_argument\\|pick(\" select_wave.py | head -25", "description": "Find select_wave signature and args"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && sed -n '155,180p;274,320p' select_wave.py", "description": "Read select function signature and main"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && grep -n \"^def build\" select_wave.py; sed -n \"$(grep -n '^def build' select_wave.py | cut -d: -f1),+14p\" select_wave.py", "description": "Read build() signature"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && python - <<'PYX'\nimport io\np='select_wave.py'; s=io.open(p,encoding='utf-8').read()\ns=s.replace(\"\"\"def build(n=58, min_score=8, quota=None, exclude_urls=None, ats=None, money=False,\n          min_pay=B.MIN_PAY, excluded=None, v

---

**Claude:**

Python в этой папке вдруг падает на старте — проверяю, не затенён ли stdlib локальным файлом.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && ls | grep -iE \"^(encodings|codecs|io|abc|site|types|os)\\.py$|^encodings$\"; echo \"---retry---\"; python -c \"print('ok')\" 2>&1 | tail -3; echo \"--- from parent ---\"; cd .. && python -c \"print('ok parent')\" 2>&1 | tail -2", "de

---

> `PowerShell` -- {"command": "$lib=\"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\\Lib\"; Test-Path \"$lib\\encodings\\__init__.py\"; (Get-ChildItem \"$lib\\encodings\" -ErrorAction SilentlyContinue | Measure-Object).Count; Write-Output \"--- python312.zip? ---\"; Test-Path \"C:\\Users\\dev\\AppDa

---

**Claude:**

Python 3.12 stdlib исчезает прямо сейчас (`Lib\encodings` пуст). Это живой инцидент — диагностирую.

---

> `PowerShell` -- {"command": "$root=\"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\"\nWrite-Output \"=== root items ===\"; (Get-ChildItem $root -ErrorAction SilentlyContinue).Name -join \", \"\nWrite-Output \"=== Lib count ===\"; (Get-ChildItem \"$root\\Lib\" -ErrorAction SilentlyContinue | Measure-

---

**Claude:**

Подтверждено: `Lib` у Python 3.12 опустел (остался только `site-packages`), исчезли `Scripts`, `libs`, `include`; метка папки 20:12:18 — ровно в середине моей работы. Рядом живёт новый `pythoncore-3.14-64` с менеджером установки Python. Проверяю, что осталось рабочим.

---

> `PowerShell` -- {"command": "$p314=\"C:\\Users\\dev\\AppData\\Local\\Python\\pythoncore-3.14-64\\python.exe\"\nWrite-Output \"=== 3.14 exists ===\"; Test-Path $p314\nif (Test-Path $p314) { & $p314 -c \"import sys; print(sys.version)\" 2>&1 | Select-Object -First 2\n  Write-Output \"=== selenium in 3.14? ===\"; & 

---

**Claude:**

Теперь и `pythoncore-3.14-64\python.exe` не находится, хотя 10 минут назад процесс из него работал. Что-то активно сносит Python на хабе. Это серьёзнее моей полосы — собираю улики.

---

> `PowerShell` -- {"command": "Write-Output \"=== disk ===\"; Get-PSDrive C,E | Select-Object Name,@{n='FreeGB';e={[math]::Round($_.Free/1GB,1)}},@{n='UsedGB';e={[math]::Round($_.Used/1GB,1)}} | Format-Table -AutoSize\nWrite-Output \"=== AppData\\Local\\Programs ===\"; (Get-ChildItem \"C:\\Users\\dev\\AppData\\Loca

---

**Claude:**

`AppData\Local\Python` опустел полностью, а в Python312 выжили ровно папки с нативными бинарниками (`DLLs`, пакеты с `.pyd`) — исчезли именно `.py`-файлы. Срочно проверяю, цел ли волт и наши скрипты.

---

> `PowerShell` -- {"command": "Write-Output \"=== jobs-watch .py count ===\"; (Get-ChildItem \"D:\\Vault\\_imports\\jobs-watch\\*.py\" -ErrorAction SilentlyContinue | Measure-Object).Count\nWrite-Output \"=== intern_gate.py ===\"; Get-Item \"D:\\Vault\\_imports\\jobs-watch\\intern_gate.py\" -ErrorAction Silentl

---

**Claude:**

Волт, скрипты и jobs.db целы — повреждение локализовано в установке Python. Ищу виновника.

---

> `PowerShell` -- {"command": "Write-Output \"=== Defender detections (last 24h) ===\"\ntry { Get-MpThreatDetection -ErrorAction Stop | Where-Object {$_.InitialDetectionTime -gt (Get-Date).AddHours(-24)} | Select-Object InitialDetectionTime,ThreatID,@{n='res';e={$_.Resources -join ';'}} | Format-Table -AutoSize -Wrap

---

> `PowerShell` -- {"command": "Get-ScheduledTask | ForEach-Object { $i = $_ | Get-ScheduledTaskInfo -ErrorAction SilentlyContinue; if ($i.LastRunTime -gt (Get-Date).AddMinutes(-25)) { [pscustomobject]@{Name=$_.TaskName; Last=$i.LastRunTime; Result=$i.LastTaskResult} } } | Sort-Object Last -Descending | Select-Object 

---

**Claude:**

Инцидент: Python 3.12 на хабе уничтожен (stdlib вырезан, выжили только нативные бинарники), из-за этого сыпятся все python-рутины — `inbox-robot`, `Hub-Priority-Shepherd`, `SecondOp Broker`, `Pulse`, `fleet-key-grant`, доорбелл дают Result=1. Виновник пока НЕ установлен: Defender за 24ч ничего не ловил, MSI-событий нет. Ищу путь ремонта без скачивания.

---

> `PowerShell` -- {"command": "Write-Output \"=== локальные установщики python ===\"\nGet-ChildItem \"C:\\Users\\dev\\Downloads\",\"E:\\downloads\",\"C:\\Users\\dev\\AppData\\Local\\Temp\" -Filter \"python*\" -File -ErrorAction SilentlyContinue | Select-Object FullName,Length,LastWriteTime | Format-Table -AutoSiz

---

> `PowerShell` -- {"command": "Write-Output \"=== pyvenv.cfg базы ===\"\n@(\"E:\\!CLAUDE-HUBPC-June26\\_scratch\\venv312\\pyvenv.cfg\",\"D:\\Vault\\_imports\\.venv-diar\\pyvenv.cfg\",\"D:\\Vault\\_imports\\dialogs\\.venv-archive\\pyvenv.cfg\",\"D:\\Vault\\_imports\\goblin-corpus\\train\\venv\\pyvenv.cfg

---

**Claude:**

Волт цел, повреждение не расползается за пределы Python. Проверяю, закончилось ли удаление, и есть ли дверь к Windows-пиру для восстановления stdlib.

---

> `PowerShell` -- {"command": "$root=\"C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312\"\nWrite-Output \"=== стабильность (повтор замера) ===\"\n\"DLLs:   \" + (Get-ChildItem \"$root\\DLLs\" -ErrorAction SilentlyContinue | Measure-Object).Count\n\"Lib:    \" + (Get-ChildItem \"$root\\Lib\" -ErrorAction 

---

**Claude:**

Удаление остановилось (замер не меняется с 20:12:18). NODE-0X жив по tailnet. Проверяю дверь и наличие там того же Python.

---

> `Bash` -- {"command": "timeout 40 ssh -o BatchMode=yes -o StrictHostKeyChecking=no -o ConnectTimeout=15 dev@10.0.0.0 \"cmd /c \\\"dir /b \\\\\\\"C:\\\\Users\\\\dev\\\\AppData\\\\Local\\\\Programs\\\\Python\\\\Python312\\\\\\\" && \\\\\\\"C:\\\\Users\\\\dev\\\\AppData\\\\Local\\\\Programs\\\\Python\

---

> `Bash` -- {"command": "grep -rhoE \"ssh [-A-Za-z0-9@._ ]{0,40}(100\\.70\\.118\\.68|NODE-0X[a-z0-9-]*)\" /c/Users/dev/.claude/skills/ /c/Users/dev/.claude/scripts/ 2>/dev/null | sort -u | head -10; echo \"=== ssh users in configs ===\"; grep -rhoE \"(User|user)[\\\"': ]+[A-Za-z0-9_.-]+\" /c/Users/dev/.ssh/

---

> `Bash` -- {"command": "sed -n '1,60p' /c/Users/dev/.ssh/config 2>/dev/null | tr -d '\\r'", "description": "Read ssh config for fleet hosts"}

---

**Claude:**

NODE-0X в ssh-конфиге стоит с логином-заглушкой `User _` — живой двери туда нет. Ищу любой другой Python на дисках, прежде чем звать оператора.

---

> `PowerShell` -- {"command": "$found = @()\nforeach ($r in @(\"C:\\Users\\dev\\AppData\\Local\",\"C:\\Users\\dev\\AppData\\Roaming\",\"C:\\Program Files\",\"C:\\Program Files (x86)\",\"C:\\mcp\",\"C:\\ProgramData\",\"D:\\Vault\\_imports\",\"E:\\!CLAUDE-HUBPC-June26\")) {\n  if (Test-Path $r) {\n    $foun

---

**Claude:**

Локально Python не восстановить: целого stdlib нигде нет, дверь к Windows-пиру мертва, точки восстановления под Access denied. Ремонт требует скачивания установщика — это Tier-2, зову оператора. Сперва доклад по рельсе, пока TG-MCP жив (он поднят до поломки).

---

> `Bash` -- {"command": "grep -rhoE \"\\\"?(chat_)?0?3[^\\\"]{0,20}\\\"?\\s*[:=]\\s*-?[0-9]{9,14}\" /c/Users/dev/.claude/*.json 2>/dev/null | head -10; echo \"=== tg chats config ===\"; ls /c/Users/dev/.claude/ | grep -iE \"tg|telegram|chat\" | head; echo \"=== grep 03 chat id ===\"; grep -rhoiE \"(03[- _]?

---

> `Bash` -- {"command": "cat /c/Users/dev/.claude/tg_bus.json 2>/dev/null | head -50", "description": "Read tg_bus.json for chat ids"}

---

**Claude:**

TG-03 = `chat_REDACTED`, аккаунт `platinumvc1`. Шлю инцидент по рельсе.

---

> `ToolSearch` -- {"query": "select:mcp__telegram__send_message,mcp__telegram__list_accounts", "max_results": 2}

---

> `mcp__telegram__send_message` -- {"account": "platinumvc1", "chat_id": chat_REDACTED, "message": "🔴 ИНЦИДЕНТ ХАБ HUB-01 · Python 3.12 УНИЧТОЖЕН · 02.10 20:12\n\nЧТО: установка Python 3.12.10 (C:\\Users\\dev\\AppData\\Local\\Programs\\Python\\Python312) потеряла весь stdlib. Lib содержит ровно 1 элемент (site-packages), папки 

---

**Claude:**

Инцидент на рельсе. Полоса подач через selenium мертва вместе с Python — но главная дверь полосы (Anthropic Fellows) идёт через Airtable, которую конвейер всё равно не умел. Её делаю браузером. Поднимаю факты для анкеты.

---

> `Bash` -- {"command": "cat \"/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/dev-cv-lives-on-github.md\" 2>/dev/null; echo \"=== hub-job-search ===\"; head -30 \"/c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/hub-job-search.md\" 2>/dev/null", "description": "Read CV 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && grep -nE \"^\\s*(NAME|EMAIL|PHONE|LINKEDIN|GITHUB|WEBSITE|LOCATION|CV_|RESUME)\" answers_canon.py | head -25; echo \"=== cv attachment ===\"; head -25 CV_ATTACHMENT.md", "description": "Read canonical answers and CV attachment path"}

---

> `Bash` -- {"command": "ls -lt \"/e/Obsidian/_imports/jobs-watch/selenium_apply/runs/cv-cache/\" 2>/dev/null | head -15; echo \"=== PDFs ===\"; find \"/e/Obsidian/_imports/jobs-watch/selenium_apply/runs/cv-cache/\" -name \"*.pdf\" 2>/dev/null | head -20", "description": "Check for cached CV PDFs"}

---

> `Bash` -- {"command": "ls \"/e/Obsidian/_imports/jobs-watch/selenium_apply/runs/cv-cache/\" | grep \"\\.pdf$\" | sed -E 's/^[ИМЯ]-[ФАМИЛИЯ]-CV-(.*)-[0-9a-f]{16}\\.pdf$/\\1/' | sort -u", "description": "List distinct CV cluster variants"}

---

**Claude:**

`Research-Engineer-MTS-Evals` — точное попадание под Fellows. Открываю дверь Anthropic Fellows в браузере.

---

> `Bash` -- {"command": "ls -t \"/e/Obsidian/_imports/jobs-watch/selenium_apply/runs/cv-cache/\" | grep \"Research-Engineer-MTS-Evals.*pdf\" | head -3; echo \"--- newest full path ---\"; ls -t /e/Obsidian/_imports/jobs-watch/selenium_apply/runs/cv-cache/[ИМЯ]-[ФАМИЛИЯ]-CV-Research-Engineer-MTS-Evals-*.pdf | 

---

> `mcp__Claude_Browser__preview_start` -- {"url": "https://airtable.com/appCHLjgoTUCJMLct/pagUhpiBE5KxoU3lX/form"}

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 4000}

---

**Claude:**

Форма одна на все три стрима — значит это ОДНА заявка, а не три. Но вижу жёсткий человеческий барьер. Читаю остаток.

---

> `mcp__Claude_Browser__get_page_text` -- {"max_chars": 3000}

---

> `mcp__Claude_Browser__read_page` -- {"filter": "interactive", "max_chars": 6000}

---

**Claude:**

Форма одна на три стрима, и в ней жёсткий барьер: **три обязательные референции с именами и почтами**, причём Anthropic пишет, что свяжется с ними без предупреждения. Выдумывать людей или отдавать чужие контакты без их согласия я не буду — это единственное, что тут реально требует слова оператора.

Проверяю, чем смогу записать подачи без Python.

---

> `Bash` -- {"command": "which sqlite3 2>/dev/null; ls /c/Users/dev/.claude/scripts/*.exe 2>/dev/null | head -3; find /c/Users/dev/AppData/Local /c/Program* -maxdepth 4 -name \"sqlite3.exe\" 2>/dev/null | head -3; echo \"--- node? ---\"; which node; node -e \"console.log('node ok')\" 2>&1 | head -2", "descr

---

**Claude:**

Node.js жив — это замена Python для записи в базу. Проверяю и winget (если есть, ремонт будет одной строкой).

---

> `Bash` -- {"command": "ls /c/Users/dev/AppData/Local/Microsoft/WindowsApps/ 2>/dev/null | grep -iE \"winget|python\" | head; echo \"--- winget direct ---\"; /c/Users/dev/AppData/Local/Microsoft/WindowsApps/winget.exe --version 2>&1 | head -2; echo \"--- node sqlite ---\"; node -e \"const {DatabaseSync}=re

---

**Claude:**

`node:sqlite` работает — записывать подачи смогу. Беру ранжированный список проходных ролей.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && node -e \"\nconst fs=require('fs');\nconst rows=JSON.parse(fs.readFileSync('_scratch/intern_gate_1002.json','utf8')).filter(r=>r.verdict==='open');\nlet i=0;\nfor (const r of rows) console.log(String(++i).padStart(2)+'. ['+r.tier+'] '+r.company+' | 

---

**Claude:**

Начинаю подачи браузером. Первая — Perplexity Research Fellowship.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "resize_window", "input": {"preset": "desktop", "width": 1400, "height": 1000}}, {"name": "navigate", "input": {"url": "https://jobs.ashbyhq.com/perplexity/s_7b4d0217/application"}}, {"name": "read_page", "input": {"filter": "interactive", "max_chars":

---

> `mcp__Claude_Browser__computer` -- {"action": "screenshot"}

---

**Claude:**

Браузерная панель не отображается — это слепая сессия планировщика ([[blind-session-tasks-cannot-see-windows]]): нет скриншотов, дерево страницы 0x0, кликать и печатать нечем. Значит подать заявки сегодня нельзя двумя независимыми причинами: мёртвый Python и слепая сессия. Чтение страниц работает — делаю пункт 4 задачи (доски DeepMind/Meta).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '1,40p' lab_hand.py; echo \"=== lab_hand.json shape ===\"; node -e \"\nconst d=JSON.parse(require('fs').readFileSync('lab_hand.json','utf8'));\nconsole.log('top keys:', Object.keys(d));\nconst k=Object.keys(d).filter(x=>x!=='_meta')[0];\ncons

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -nE \"JUNK_RX|INTERN_OK|STUDENT_ONLY\" jobs_discover.py lab_hand.py | head -20; echo \"=== JUNK_RX def ===\"; node -e \"\nconst s=require('fs').readFileSync('jobs_discover.py','utf8');\nconst i=s.indexOf('JUNK_RX =');\nconsole.log(s.slice(i, i+

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '395,430p' jobs_discover.py; echo \"=== как lab_hand скорит ===\"; grep -nE \"score_title|door_cluster\" lab_hand.py", "description": "Read score_title and lab_hand usage"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '145,160p' lab_hand.py", "description": "Read lab_hand scoring branch"}

---

**Claude:**

`classify` падает в `door_cluster`, где карв-аут 01.10 живёт — значит ручная полоса интернов пропускает (докстринг `lab_hand.py` про «JUNK_RX режет стажировки» устарел). Проверяю имена компаний и иду на доски.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && node -e \"\nconst s=require('fs').readFileSync('jobs_discover.py','utf8');\nconst i=s.indexOf('LAB_DOOR_CO = frozenset');\nconst blk=s.slice(i, s.indexOf('})', i));\nfor (const n of ['DeepMind','Meta','Google']) {\n  const re=new RegExp('\\\"[^\\\"]

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && node -e \"\nconst s=require('fs').readFileSync('jobs_discover.py','utf8');\nconst i=s.indexOf('LAB_DOOR_CO = frozenset');\nconst blk=s.slice(i, s.indexOf('})', i));\nconst names=[...blk.matchAll(/\\\"([^\\\"]+)\\\"/g)].map(m=>m[1]).filter(x=>x.lengt

---

**Claude:**

Доски DeepMind и Meta — читаю браузером.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.google.com/about/careers/applications/jobs/results?company=DeepMind&q=intern"}}, {"name": "get_page_text", "input": {"max_chars": 3500}}]}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && grep -nE \"GCAREERS|results\\?|google.com/about\" lab_hand.py | head -8", "description": "Read lab_hand GCAREERS URL"}

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.google.com/about/careers/applications/jobs/results?company=DeepMind"}}, {"name": "get_page_text", "input": {"max_chars": 2500}}, {"name": "navigate", "input": {"url": "https://www.google.com/about/careers/applications/jobs/results?q=stu

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.google.com/about/careers/applications/jobs/results?company=DeepMind&employment_type=INTERN"}}, {"name": "get_page_text", "input": {"max_chars": 1800}}, {"name": "navigate", "input": {"url": "https://deepmind.google/about/careers/"}}, {"

---

**Claude:**

DeepMind: intern/residency ролей на доске сейчас НЕТ (это «не нашёл», не «не существует» — программа Student Researcher сезонная). Проверяю Meta.

---

> `mcp__Claude_Browser__browser_batch` -- {"actions": [{"name": "navigate", "input": {"url": "https://www.metacareers.com/jobs?q=AI%20Residency"}}, {"name": "get_page_text", "input": {"max_chars": 3000}}]}

---

**Claude:**

Meta: список приезжает GraphQL'ом за cookie-баннером, в слепой сессии без кликов не перечислить — состояние с 27.09 не изменилось. Дописываю селектору флаг на эту полосу, чтобы она шла отдельной волной, а не тонула в денежной сортировке.

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "          min_pay=B.MIN_PAY, excluded=None, verbose=False):\n    \"\"\"Ворклист волны. ats -- набор рельс (--ats); money -- только зарплата >= min_pay или\n    vip/target; exclude

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "        if (\n            r[\"url\"] in exclude_urls", "new_string": "        if intern_lane and not intern_lane_ok(r):\n            continue\n        if (\n            r[\"url\"]

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "                    help=\"ручная квота мест по рельсам: greenhouse=70,ashby=0,lever=3 (иначе из данных)\")\n    args = ap.parse_args()", "new_string": "                    help=\

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\selenium_apply\\select_wave.py", "old_string": "                ats=ats, money=args.money, min_pay=args.min_pay, excluded=excluded, verbose=True)", "new_string": "                ats=ats, money=args.money, min_pay=args.min_pay,

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\lab_hand.py", "old_string": "Полоса НЕ обходит правила: стажировки и new grad режет jobs_discover.JUNK_RX, гиг-мельницу", "new_string": "Полоса НЕ обходит правила: new grad и student-only режет STUDENT_ONLY_RX, гиг-мельницу"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\lab_hand.py", "old_string": "(AI Tutor, аннотатор, rater) режет LAB_JUNK_RX, деньги старше ноги в двери, кластер без своей", "new_string": "(AI Tutor, аннотатор, rater) режет LAB_JUNK_RX, деньги старше ноги в двери, кластер без

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch && sed -n '24,38p' lab_hand.py", "description": "Verify lab_hand docstring region"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\jobs-watch\\lab_hand.py", "old_string": "CV-ветки. ПОПРАВКА 02.10.2026: строка «стажировки режет JUNK_RX» устарела — после канона\n01.10 intern/residency/fellowship в ЛАБОРАТОРИИ законны, и classify() это уже умеет, потому\nчто score_title

---

**Claude:**

Теперь артефакт в волт — полоса с уликами плюс готовый пакет ответов для Anthropic Fellows.

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge/ | head -20; echo \"=== 04-Projects sample ===\"; ls /e/Obsidian/Vault-Knowledge/04-Projects/ 2>/dev/null | head -8", "description": "Check vault structure"}

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\04-Projects\\Intern-Fellows-Lane-2026-10-02.md", "content": "---\ntitle: \"Полоса intern/fellows/residency лабораторий — замер и шорт-лист 02.10.2026\"\ndate_established: 2026-10-02\nnode_type: project\nstatus: active\nauthor: Claude (claude-opus-5) · A-

---

**Claude:**

Добавляю входящую ссылку (без сирот, §8.3) и пишу память.

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge/90_MOCs/ 2>/dev/null | head -20; echo \"=== mission2 / jobs files ===\"; ls /e/Obsidian/Vault-Knowledge/04-Projects/ | grep -iE \"mission|job|pipe\" | head", "description": "Find a MOC to link from"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/04-Projects && tail -6 job-search-diary-roadmap.md; echo \"===APPEND===\"; cat >> job-search-diary-roadmap.md <<'EOF'\n\n- 2026-10-02 · [[Intern-Fellows-Lane-2026-10-02]] — полоса intern/fellows/residency лабораторий\n  измерена: 76 ролей, 38 проходных, 24

---

**Claude:**

Теперь память: две записи — находка про гиг-мельницу и инцидент с Python.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\gig-mill-judged-by-body-not-title.md", "content": "---\nname: gig-mill-judged-by-body-not-title\ndescription: \"Гиг-мельница в полосе лабораторий судится ТЕЛОМ вакансии (1099-контрактор, почасовая гибкость), а 

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\hub-python312-stdlib-destroyed-20261002.md", "content": "---\nname: hub-python312-stdlib-destroyed-20261002\ndescription: \"02.10.2026 20:12 на хабе HUB-01 уничтожен stdlib Python 3.12.10 — исчезли все .

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && cat >> MEMORY.md <<'EOF'\n- [Хаб: уничтожен stdlib Python 3.12](hub-python312-stdlib-destroyed-20261002.md) — ⭐02.10 20:12 исчезли все .py, выжили нативные; все python-рутины красные; причина НЕ установлена; замен

---

**Claude:**

Финальный доклад по полосе в TG-03.

---

> `mcp__telegram__send_message` -- {"account": "platinumvc1", "chat_id": chat_REDACTED, "message": "📊 intern-lane: 76 ролей · 0 подано · 24 enrollment-gate · 14 гиг-мельница · покрытие прибора 100%\n\nЧЕСТНОЕ ЧИСЛО ПОДАЧ = 0. Две независимые причины, обе названы: (1) на хабе в 20:12 уничтожен Python 3.12 → конвейер selenium мёртв (инцид

---

**Claude:**

Финальная сверка правок чтением (прогнать нечем — Python мёртв).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports/jobs-watch/selenium_apply && echo \"=== intern_lane_ok ===\"; sed -n \"$(grep -n 'LAB_LANE_RX = ' select_wave.py | cut -d: -f1),+14p\" select_wave.py; echo; echo \"=== точка фильтра ===\"; grep -n \"intern_lane\" select_wave.py; echo; echo \"=== elig в SELECT ===

---

> `Bash` -- {"command": "date \"+%d.%m.%Y %H:%M\"", "description": "Current time for report"}

---

**Claude:**

**02.10.2026 20:29 WEST · рутина intern-fellows-lane-20261002 · хаб HUB-01**

## Итог: полоса измерена и разблокирована, подач ноль — причины названы

**Замер.** 2072 строки `lab-door` → 72 по заголовку → добрал 4 из других кластеров со статусом `skip` (их резал пре-01.10 фильтр) → минус ложные срабатывания → **полоса 76 ролей**. Проверено по ПОЛНОМУ тексту вакансий из публичных API площадок: **38 проходят · 24 ворота enrollment · 14 гиг-мельница · 0 строк, по которым прибор слеп (покрытие 100%)**.

**Главная находка — я почти подал 14 заявок на мельницу.** Scale AI держит 14 вакансий «<Домен> Fellow — Human Frontier Collective». Заголовок говорит «Fellow», а тело — `"fully remote, 1099 independent contractor"`, `"flexible 10–40 hour weeks"`, `"project pay rates vary across platforms"`, работа = датасеты для «partnered AI labs». Штата нет, внутренней доски нет. Канон отсекал мельницу по слову в заголовке и прямо разрешал «Fellows Program» — прокси сломался, потому что название программы пишет тот, кого мы фильтруем. Теперь судим телом.

**Цель №1 полосы — Anthropic Fellows**: одна анкета на все три стрима, настоящая дверь — Airtable (`bit.ly/afpsafety`), а не Greenhouse; 4 месяца фултайма, $3 850/нед + компьют ~$15K/мес, Berkeley по O-1. Пакет ответов собран целиком.

### ⛔ Нужны твои руки — ровно одно
**Три референции для Anthropic Fellows:** имя + email + кто он + что делали вместе. Anthropic пишет, что свяжется с ними **без предупреждения**, с ответом в течение недели. Чужие контакты третьей стороне без согласия этих людей я не отдаю, и выбирать поручителей — твоё решение. Это единственное, что держит заявку.

### Чего я НЕ сделал
**Подач 0.** Две независимые причины, обе наступили во время работы:
1. **В 20:12 на хабе уничтожен Python 3.12** — исчез весь stdlib (`Lib` = 1 элемент), выжили только нативные бинарники. Конвейер selenium мёртв, вместе с ним красные `inbox-robot`, `Hub-Priority-Shepherd`, `SecondOp Broker`, `Pulse`, доорбелл. Причину я **не установил** — Defender за 24ч чист, MSI-событий нет. Обходы перебрал: другого Python на машине нет, дверь к NODE-0X мертва (`User _` в конфиге), точки восстановления под Access denied. Ремонт = переустановка, это Tier-2 → команда отправлена в 03, ждёт «+».
2. **Сессия слепая** — панель браузера не отображается, скриншот отбит, дерево страницы 0x0. Заполнять твои анкеты, не видя результата, я не стал: у полосы уже есть урок про девять затёртых подач.

Ещё не сделано: правка `select_wave.py` **не прогнана тестом** (Python умер раньше) — перед первой ночной волной обязателен `_test_select_money.py`; счётчик использования у нового прибора не поставлен; Meta не перечислить в слепой сессии; у DeepMind intern-ролей сегодня **нет ни одной** (это «не нашёл», программа сезонная).

### Что теперь работает
Прибор `intern_gate.py` с паспортом внутри файла и сторожем — **красный показан дважды** (7 провалов на сломанном базовом коде, 10 на отключённых новых правилах). Вердикты лежат в базе (`ats_jobs.elig`), и снят настоящий тормоз: `BAD_TITLE` в селекторе рубил любой заголовок со словом intern, из-за чего полоса давала 38 проходных ролей и **0 подач** — расхождение канона 01.10 и кода жило сутки.

Волт: [Intern-Fellows-Lane-2026-10-02.md](D:\Vault\Vault-Knowledge\04-Projects\Intern-Fellows-Lane-2026-10-02.md). Память: две записи + индекс. Доклады в TG-03: два.

**🔧 Вердикт по скиллу (§9.3-бис): `/apply` обновить** — в нём нет шага «полоса лабораторий», и без `intern_gate` подача на intern-роль либо не доедет, либо уедет на мельницу.

🧒 **Простыми словами:** я нашёл 76 стажировок и феллоушипов в ИИ-лабораториях и прочитал каждое объявление целиком. 24 оказались только для студентов — туда тебя робот анкеты не пустит по году выпуска. 14 выглядели как почётная программа, а на деле подработка по часам — чуть не подался. Остаются 38 хороших, и самая важная — Anthropic, где одна анкета идёт сразу на три команды. Отправить её не смог: у формы требуют трёх живых людей, которые за тебя поручатся, а чужие телефоны без спроса я не даю — назови трёх. И прямо посреди работы на хабе сломался Python, которым подаются заявки; починить его сам не могу, нужно твоё «да» на переустановку.
