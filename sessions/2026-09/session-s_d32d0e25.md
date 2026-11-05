---
session: s_d32d0e25
date: 2026-09-05
words: 14614
turns: 26
tools: "Bash, Edit, Grep, Skill, ToolSearch, Write, mcp__97420a88-50ae-4ab1-99f6-f5ec547aebd8__search_threads, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-05 · Scheduled run: auto-hub-260901-cv-rebuild-contacts

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d32d0e25` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260901-cv-rebuild-contacts" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260901-cv-rebuild-contacts\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

ПЕРВЫМ ДЕЙСТВИЕМ вызови set_session_title("Починка класса: сессия a2 протухает молча").

📌 ОБЯЗАТЕЛЬНО: прочитай и исполни блок STOP-DUP из
$OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md (ON AIR · консолидатор · RECALL летящей
работы · бак) — дословно, до начала любой стройки.

ЗАЧЕМ ТЫ ПОДНЯТА (класс системный, §5.10 — 4 датированных случая):
Выделенный профиль `D:\Vault\_imports\claude-ai\_chrome_profile_a2` теряет сессию
claude.ai (аккаунт [EMAIL]) и это каждый раз ломает ночную рутину
`claudeai-sync-daily` на шаге 0 (гвард `pull_rail_c.py --plan --profile=a2` → exit 2,
403 account_session_invalid). Случаи: 01.09 01:26 · 02.09 (дважды) · 03.09 01:26.
Строки в D:\Vault\Vault-Knowledge\00-System\Breakage-Journal.md — грепни
"_chrome_profile_a2", там улики целиком, начни с них, не с нуля.

ЧТО УЖЕ ДОКАЗАНО (не переоткрывай):
- Рельса C здорова: Cloudflare проходится, /api/organizations = 200 при живой сессии.
- Чинилка автономна и РАБОТАЕТ: railc_login_a2.py --wait=420 в фоне + magic-link из
  Gmail-коннектора a2 в $SCRATCH/magic_link.txt. Прогон 03.09 01:30-01:40 — GUARD OK,
  руки оператора не нужны. Провал 02.09 02:5x был capability-gap (у той сессии не было
  Gmail-коннектора), а НЕ сломанной рельсой.
- Живой Chrome оператора (профиль Default) НЕ ТРОГАТЬ ни при каких условиях
  (канон reglament-hab-brauzernye-lichnosti-bb-i-roboty).

ЧТО НЕ ДОКАЗАНО — это и есть работа:
Почему сессия умирает. Замер 02.09: жива в ~01:30, мертва в ~02:5x ⇒ ≈1.5 часа, а не сутки,
значит формулировка «короткий TTL» 🤔 не подтверждена. Конкурирующая гипотеза: сессию гасит
что-то ещё (второй Chromium на том же профиле, параллельный вход, чистка профиля).
Мерить нечем: возраст и исход входа никуда не пишутся.

ЗАДАЧА (АК-47, самое простое, что чинит КЛАСС):
1. Дешёвый 0-LLM журнал состояния входа (ts · исход гварда · org · возраст последнего
   успешного входа) — чтобы TTL стал ЗАМЕРОМ, а не гипотезой. Пишущий = pull_rail_c.py и
   railc_login_a2.py; журнал НЕ в синкаемой папке (грабли §4.5-бис).
2. Сторож живёт ВНЕ того, что сторожит (§5.5): проверяет ВОЗРАСТ ВЫХОДА (свежесть бандла в
   raw\), молчит когда ок, орёт именем больного и лечением в TG-03 когда нет.
3. Проверить конкурирующую гипотезу: не открывает ли кто-то второй Chromium на
   _chrome_profile_a2 (pull_rail_c + railc_login + ручные прогоны).
4. Если замер покажет TTL < суток — предложить упреждающий перелогин ПЕРЕД пулом,
   а не после красного гварда.

ПРИЁМКА: /tt с красным прогоном на сломанном коде (тест обязан краснеть, §5.4), вердикт
только ✅/⚠️/❌ с доказательством; починка класса → /share-fix (🌍 мировой потребитель).
Границы: Tier-2 = стоп + аск в 02; пароли не вводить (только magic-link); публичное — гейт.
</scheduled-task>

---

**Claude:**

I'll start by setting the session title as instructed.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "Починка класса: сессия a2 протухает молча"}

---

> `Bash` -- {"command": "cat \"D:/Vault/Vault-Knowledge/08-Templates/seed-stop-dup-block.md\"", "description": "Read STOP-DUP block"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py list 2>&1 | head -40; echo \"=== ZONES ===\"; python onair.py zones 2>&1 | head -40", "description": "ON AIR list and zones"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone vault-imports/claudeai-rail-c --mode exclusive --title \"Класс: сессия a2 протухает молча (журнал+сторож TTL)\" --ttl-hours 3 2>&1 | tail -5", "description": "ON AIR declare"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/00-System\" && grep -n \"_chrome_profile_a2\" Breakage-Journal.md | head -30", "description": "Grep breakage journal for the class"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && ls -la | head -40; echo \"=== SIZES ===\"; wc -l pull_rail_c.py railc_login_a2.py 2>&1", "description": "List claude-ai import dir"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && cat pull_rail_c.py", "description": "Read pull_rail_c.py"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && cat railc_login_a2.py", "description": "Read railc_login_a2.py"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai/_chrome_profile_a2\" && ls -la | head -30; echo \"=== Network ===\"; ls -la Default/Network/ 2>/dev/null | head; echo \"=== lock files ===\"; ls -la Singleton* 2>/dev/null; ls -la Default/*.lock 2>/dev/null", "description": "Inspect a2 chrome profile 

---

> `Bash` -- {"command": "cd \"$(cygpath -u \"$TEMP\" 2>/dev/null || echo /tmp)\" 2>/dev/null; SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\"; mkdir -p \"$SC\"; cp \"D:/Vault/_imports/claude-ai/_chrome_profile_a2/Default/Network/Coo

---

> `Bash` -- {"command": "python - <<'PY'\nimport sqlite3, datetime\np = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\ck_a2.sqlite\"\ncon = sqlite3.connect(p)\ndef t(us):\n    if not us: return \"-\"\n    try: return (datetime.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && tail -60 daily_sync.log", "description": "Tail daily sync log"}

---

> `Bash` -- {"command": "for f in \"C:/Users/dev/.claude/.stignore\" \"D:/Vault/.stignore\" \"D:/Vault/_imports/.stignore\" \"D:/Vault/Vault-Knowledge/.stignore\"; do echo \"=== $f ===\"; cat \"$f\" 2>/dev/null | head -30; done", "description": "Check stignore files"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/.stignore\" | grep -v '^//' | sed -n '1,120p'", "description": "Full stignore rules for .claude"}

---

> `Bash` -- {"command": "ls -d ~/.claude/*/ 2>/dev/null | head -40; echo \"=== logs ===\"; ls ~/.claude/logs 2>/dev/null | head -20", "description": "List .claude subdirs"}

---

> `Bash` -- {"command": "grep -rln \"_chrome_profile_a2\\|railc_login_a2\\|profile=a2\" ~/.claude/scripts ~/.claude/skills ~/.claude/hooks ~/.claude/scheduled-tasks \"D:/Vault/_imports\" 2>/dev/null | grep -v __pycache__ | head -30", "description": "Find all users of the a2 profile"}

---

> `Grep` -- {"pattern": "_chrome_profile_a2|railc_login_a2|--profile=a2", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches", "head_limit": 40}

---

> `Grep` -- {"pattern": "_chrome_profile_a2|railc_login_a2|profile=a2", "path": "D:\\Vault\\_imports\\claude-ai", "output_mode": "files_with_matches", "head_limit": 30}

---

> `Bash` -- {"command": "ls ~/.claude/skills/claudeai-sync/ 2>/dev/null; grep -n \"profile=a2\\|railc_login\\|_chrome_profile\" ~/.claude/skills/claudeai-sync/SKILL.md 2>/dev/null | head -20", "description": "Check claudeai-sync skill"}

---

> `Bash` -- {"command": "sed -n '1,80p' ~/.claude/skills/claudeai-sync/SKILL.md", "description": "Read claudeai-sync skill head"}

---

> `Bash` -- {"command": "P=\"D:/Vault/_imports/claude-ai/_chrome_profile_a2\"; python - <<'PY'\nimport json\np=r\"D:\\Vault\\_imports\\claude-ai\\_chrome_profile_a2\\Default\\Preferences\"\nd=json.load(open(p,encoding=\"utf-8\"))\nprof=d.get(\"profile\",{})\nprint(\"exit_type:\", prof.get(\"exit_type\"), 

---

> `Bash` -- {"command": "ls ~/.claude/scripts/ | grep -i \"gmail\\|mail\" | head -20; echo \"=== tasks near 02 ===\"; ls ~/.claude/scheduled-tasks/ | head -50", "description": "Look for gmail scripts and scheduled tasks"}

---

> `Bash` -- {"command": "grep -rl \"claudeai\" ~/.claude/scheduled-tasks/*/SKILL.md 2>/dev/null | head; echo \"=== live task list ===\"; powershell -NoProfile -Command \"Get-ScheduledTask | Where-Object {\\$_.TaskName -like '*laude*'} | ForEach-Object { \\$i=\\$_ | Get-ScheduledTaskInfo; '{0,-45} {1,-9} {2}' -f

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"schtasks /query /fo csv /v\" 2>&1 | python -c \"\nimport sys,csv,io\nrows=list(csv.reader(io.StringIO(sys.stdin.read())))\nhdr=None\nfor r in rows:\n    if not r: continue\n    if r[0]=='HostName' or (hdr is None and 'TaskName' in r):\n        hdr=r; con

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"schtasks /query /fo csv /v\" 2>&1 | python -c \"\nimport sys,csv,io\nrows=list(csv.reader(io.StringIO(sys.stdin.read())))\nhdr=None\nfor r in rows:\n    if not r: continue\n    if r[0]=='HostName' or (hdr is None and 'TaskName' in r):\n        hdr=r; con

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && cat _test_railc_a2_profile.py", "description": "Read a2 profile test"}

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"schtasks /query /tn 'ClaudeAI Sync Nightly' /xml\" 2>&1 | head -60", "description": "Inspect ClaudeAI Sync Nightly task"}

---

> `Bash` -- {"command": "cat ~/.claude/scripts/claudeai_sync_nightly.cmd", "description": "Read nightly cmd"}

---

> `Bash` -- {"command": "P=\"D:/Vault/_imports/claude-ai/_chrome_profile_a2\"; echo \"=== Default/LOG ===\"; cat \"$P/Default/LOG\" 2>/dev/null | tail -20; echo \"=== chrome_debug/LOG in root ===\"; ls \"$P\"/*.log \"$P\"/LOG* 2>/dev/null; echo \"=== Local State os_crypt ===\"; python - <<'PY'\nimport json,h

---

> `Bash` -- {"command": "cat ~/.claude/projects/P---WORKDIR-HUB/memory/patch-code-via-file-not-heredoc.md 2>/dev/null; echo \"=== gmail memory ===\"; cat ~/.claude/projects/P---WORKDIR-HUB/memory/claudeai-sync-needs-a2-account.md 2>/dev/null", "description": "Read relevant memories"}

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\claude-ai\\railc_journal.py", "content": "# -*- coding: utf-8 -*-\nr\"\"\"railc_journal.py -- дешёвый 0-LLM журнал состояния входа a2 в claude.ai.\n\nЗАЧЕМ (класс `browser-rail-down`, подкласс «сессия a2 протухает молча», 5 датированных\nслучаев 01.09-03.09): к

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python -c \"import ast,sys; ast.parse(open('railc_journal.py',encoding='utf-8').read()); print('AST OK')\" && python railc_journal.py snapshot", "description": "Syntax check + first snapshot"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\claude-ai\\pull_rail_c.py", "old_string": "import sqlite3, shutil, os, tempfile, json, sys, time\nfrom pathlib import Path\nfrom playwright.sync_api import sync_playwright", "new_string": "import sqlite3, shutil, os, tempfile, json, sys, t

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\_imports\\claude-ai\\pull_rail_c.py", "old_string": "    page = ctx.pages[0] if ctx.pages else ctx.new_page()\n    page.set_default_timeout(60000)\n    page.goto(\"https://claude.ai/recents\", wait_until=\"domcontentloaded\")", "new_string": "    _j

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && grep -n \"ctx.close(); sys.exit\\|ctx.close()$\" pull_rail_c.py", "description": "Find exit points"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && sed -n '138,156p' pull_rail_c.py; echo \"---178,184---\"; sed -n '176,184p' pull_rail_c.py; echo \"---228,234---\"; sed -n '226,234p' pull_rail_c.py", "description": "Show exit contexts"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python - <<'PY'\nfrom pathlib import Path\np = Path(\"pull_rail_c.py\")\ns = p.read_text(encoding=\"utf-8\")\nreps = [\n ('        print(\"ORGS FAILED:\", orgs); ctx.close(); sys.exit(2)',\n  '        print(\"ORGS FAILED:\", orgs)\\n        _fin(

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python - <<'PY'\nfrom pathlib import Path\np = Path(\"pull_rail_c.py\"); s = p.read_text(encoding=\"utf-8\")\nold = 'ACCOUNT GUARD: refuses to pull an org that is not signed in; a2 org = a673590f-...\\nupdated: 2026-08-30 (added --profile=a2: own

---

**Claude:**

Now wiring the login script:

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python - <<'PY'\nfrom pathlib import Path\np = Path(\"railc_login_a2.py\"); s = p.read_text(encoding=\"utf-8\")\n\nold_imp = 'import os, sys, re, time, json\\nfrom pathlib import Path\\nfrom playwright.sync_api import sync_playwright\\n'\nnew_imp

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && SCRATCH=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" python railc_login_a2.py --wait=600 2>&1 | tail -40", "description": "Start a2 magic-link relogin in background", "r

---

> `ToolSearch` -- {"query": "select:mcp__s_8e110270__search_threads,mcp__s_8e110270__get_thread", "max_results": 3}

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:anthropic.com newer_than:1d", "pageSize": 5}

---

> `Bash` -- {"command": "tail -5 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/b2ms78rs1.output\" 2>/dev/null", "description": "Check login progress"}

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:anthropic.com newer_than:1h", "pageSize": 5}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python - <<'PY'\nfrom pathlib import Path\np = Path(\"railc_journal.py\"); s = p.read_text(encoding=\"utf-8\")\nold = 'def snapshot(profile=\"a2\"):\\n    prof = profile_dir(profile)'\nnew = ('def snapshot(profile=\"a2\", prof_dir=None):\\n'\n   

---

> `mcp__s_8e110270__search_threads` -- {"query": "from:anthropic.com newer_than:1h", "pageSize": 5}

---

**Claude:**

You've hit your session limit · resets 11:30am (Europe/London)

---

**User:**

<task-notification>
<task-id>b2ms78rs1</task-id>
<tool-use-id>toolu_01Mz6q3oq9avdTGpcrxxWk8U</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_d32d0e25\tasks\b2ms78rs1.output</output-file>
<status>completed</status>
<summary>Background command "Start a2 magic-link relogin in background" completed (exit code 0)</summary>
</task-notification>

---

**Claude:**

You've hit your session limit · resets 11:30am (Europe/London)

---

**User:**

<task-notification>
<task-id>bp29i4yqh</task-id>
<tool-use-id>toolu_01MNL49LydLceozv2VeVPfv1</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_d32d0e25\tasks\bp29i4yqh.output</output-file>
<status>completed</status>
<summary>Background command "Find all users of the a2 profile" completed (exit code 0)</summary>
</task-notification>

---

**Claude:**

You've hit your session limit · resets 11:30am (Europe/London)

---

**User:**

Continue from where you left off.

---

**Claude:**

No response requested.

---

**User:**

продолжи

---

**Claude:**

You've hit your session limit · resets 2am (Europe/London)

---

**User:**

Продолжи

---

**Claude:**

You've hit your session limit · resets 2am (Europe/London)

---

**User:**

Try again

---

**Claude:**

[⏰ суббота, ночь, 02:00, 5 сентября 2026]

Продолжаю. Прошло ~1.5 суток с обрыва — сперва проверяю премиссу по факту, а не по своему старому плану: часть работы, судя по файлу на диске, уже уехала вперёд без меня.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && ls -la railc_*.py _test_railc*.py 2>&1; echo \"=== watchdog? ===\"; ls -la ~/.claude/scripts/railc_a2_watchdog.py 2>&1; echo \"=== journal ===\"; ls -la ~/.claude/logs/railc_a2_session.jsonl 2>&1; wc -l ~/.claude/logs/railc_a2_session.jsonl 2>&1"

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python railc_journal.py status 2>&1 | head -30", "description": "Journal status"}

---

> `Bash` -- {"command": "cd ~/.claude/logs && python - <<'PY'\nimport json\nrows=[json.loads(l) for l in open(\"railc_a2_session.jsonl\",encoding=\"utf-8\") if l.strip()]\nfor r in rows:\n    print(\"%s %-6s %-5s %-26s ck=%-5s all=%-5s exit=%-8s osc=%s %s\" % (\n        r.get(\"ts_local\",\"\")[:19], r.get(\"ev

---

> `Bash` -- {"command": "tail -25 ~/.claude/scripts/_claudeai_sync_nightly.log 2>&1; echo \"=== raw bundles (a2) ===\"; ls -la \"D:/Vault/_imports/claude-ai/raw\" | grep -v bbplatinum | tail -6", "description": "Check tonight's nightly run and bundle freshness"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py check --zone vault-imports/claudeai-rail-c 2>&1 | tail -3 && python onair.py declare --zone vault-imports/claudeai-rail-c --mode exclusive --title \"Класс a2-сессия: сторож возраста выхода + вердикт\" --ttl-hours 3 2>&1 | tail -2", "description": 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py list 2>&1 | grep -i \"claudeai-rail-c\\|vault-imports\" | head -5", "description": "Verify my declaration registered"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && SCRATCH=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" timeout 180 python pull_rail_c.py --plan --profile=a2 2>&1 | tail -20", "description": "Live guard probe: did the se

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"claudeai\" _shared/output_freshness.py | head -10; echo \"=== bus_send usage ===\"; sed -n '1,40p' bus_send.py | head -45", "description": "Check ARTIFACTS registry and bus_send API"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/brkmj1dz7.output\"", "description": "Read guard probe result"}

---

> `Bash` -- {"command": "ls -la \"D:/Vault/_imports/claude-ai/raw/claude-ai-export-2026-09-05.json\" 2>&1; echo \"=== journal tail ===\"; cd \"D:/Vault/_imports/claude-ai\" && python railc_journal.py status 2>&1 | head -12; echo \"=== nightly log tail ===\"; tail -6 daily_sync.log", "description": "Check 

---

> `Bash` -- {"command": "cd ~/.claude/logs && python - <<'PY'\nimport json\nrows=[json.loads(l) for l in open(\"railc_a2_session.jsonl\",encoding=\"utf-8\") if l.strip()]\nfor r in rows[-6:]:\n    print(\"%s pid=%-6s %-6s %-5s %-10s mode=%-7s note=%s\" % (\n        r.get(\"ts_local\",\"\")[:19], r.get(\"pid\"),

---

**Claude:**

Сессия a2 **жива прямо сейчас** — гвард зелёный через 16 ч после входа. Это опровергает «TTL полтора часа». Теперь строю недостающий кусок — сторожа.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "content": "# -*- coding: utf-8 -*-\nr\"\"\"railc_a2_watchdog.py -- сторож рельсы claude.ai/a2. Живёт ВНЕ того, что сторожит.\n\nЗАЧЕМ (класс `browser-rail-down`, подкласс «сессия a2 протухает молча», 7+ датированных\nслучаев 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "def main():\n    if \"--self-test\" in sys.argv:\n        return self_test()", "new_string": "# Опечатка во флаге не имеет права молча пройти как «обычный прогон»: сторож с\n# непонятым арг

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python -c \"import ast; ast.parse(open('railc_a2_watchdog.py',encoding='utf-8').read()); print('AST OK')\" && echo \"=== self-test ===\" && python railc_a2_watchdog.py --self-test; echo \"exit=$?\"; echo \"=== unknown flag ===\"; python railc_a2_watchdog.py --non

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_railc_a2_watchdog.py", "content": "# -*- coding: utf-8 -*-\nr\"\"\"_test_railc_a2_watchdog.py -- регрессия сторожа рельсы claude.ai/a2.\n\nЗАЧЕМ: сторож ловит четыре РАЗНЫХ вида смерти рельсы, и три из них выглядят как успех\n(зелёный лог при 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python _test_railc_a2_watchdog.py; echo \"exit=$?\"", "description": "Run the regression test green"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\red_verify_watchdog.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Красная проверка сторожа: ломаем КОПИЮ по kill-list и требуем, чтобы тест покраснел.\n\nЖ

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python red_verify_watchdog.py 2>&1 | tail -20", "description": "Red-first proof on a broken copy"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python red_verify_watchdog.py 2>&1 | grep -E \"^(КОНТРОЛЬ|  ok|  FAIL|  \\?\\?|ИТОГ)\"", "description": "Show which break survived"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_railc_a2_watchdog.py", "old_string": "        probs, _ = m.diagnose(jp, raw)\n        check(any(p[\"id\"] == \"no-output\" for p in probs),\n              \"бандл bbplatinum НЕ считается выходом рельсы a2\")", "new_string

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python red_verify_watchdog.py 2>&1 | grep -E \"^(КОНТРОЛЬ|  ok   слом|  FAIL|  \\?\\?|ИТОГ)\"", "description": "Re-run red verify after test fix"}

---

> `Bash` -- {"command": "date \"+%Y-%m-%d %H:%M:%S %Z\"; python -c \"\nimport datetime,zoneinfo\nprint('Lisbon:', datetime.datetime.now(zoneinfo.ZoneInfo('Europe/Lisbon')).strftime('%Y-%m-%d %H:%M'))\"", "description": "Current time"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.cmd", "content": "@echo off\nREM ============================================================================\nREM Сторож рельсы claude.ai/a2 (класс browser-rail-down, подкласс «сессия a2\nREM протухает молча»). Судит НОЧЬ: MCP-рут

---

> `Bash` -- {"command": "cd ~/.claude/scripts && powershell -NoProfile -Command \"schtasks /create /tn 'Claude RailC A2 Watchdog' /tr '\\\"C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.cmd\\\"' /sc daily /st 05:45 /ru 'HUB-01\\dev' /np /rl LIMITED /f\" 2>&1 | tail -3", "description": "Register 

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python - <<'PY'\nimport subprocess, re, pathlib\nxml = subprocess.run([\"powershell\",\"-NoProfile\",\"-Command\",\"schtasks /query /tn 'ClaudeAI Sync Nightly'

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\make_watchdog_task.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Регистрирует OS-задачу сторожа рельсы a2, копируя S4U-принципала у соседней\nрабочей задач

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python make_watchdog_task.py; echo \"exit=$?\"", "description": "Register watchdog task from XML"}

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"schtasks /create /tn 'Claude RailC A2 Watchdog' /tr '\\\"C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.cmd\\\"' /sc daily /st 05:45 /f\" 2>&1 | tail -3; echo \"---\"; powershell -NoProfile -Command \"schtasks /query /tn 'Claude RailC A2 Watchdog'

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"schtasks /run /tn 'Claude RailC A2 Watchdog'\" 2>&1 | tail -2; sleep 8; echo \"=== лог ===\"; tail -6 ~/.claude/logs/_railc_a2_watchdog.log 2>&1", "description": "Fire the task once and read its log"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && sed -n '385,425p' output_freshness.py", "description": "Inspect ARTIFACTS entry format"}

---

> `Bash` -- {"command": "ls -la ~/.claude/scripts/_shared/output_freshness.py; echo \"=== ARTIFACTS_COMMON first entry shape ===\"; sed -n '425,470p' ~/.claude/scripts/_shared/output_freshness.py", "description": "Check file recency and common entry shape"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "    problems, facts = diagnose(journal, raw_dir, max_b, max_j)\n\n    if \"--json\" in sys.argv:", "new_string": "    problems, facts = diagnose(journal, raw_dir, max_b, max_j)\n\n    # СОС

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "def should_alert(problems, now=None):", "new_string": "def touch_state(problems, facts, now=None):\n    \"\"\"Отметка «я отработал» на КАЖДОМ прогоне -- в т.ч. когда всё зелено и мы молчим.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "    fresh = (key != prev_key) or (now - prev_ts) / 3600.0 >= REALERT_AFTER_H\n    save_state({\"key\": key, \"ts\": now if fresh else prev_ts, \"problems\": [p[\"id\"] for p in problems]})\

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python -c \"import ast; ast.parse(open('railc_a2_watchdog.py',encoding='utf-8').read()); print('AST OK')\" && rm -f ~/.claude/logs/railc_a2_watchdog.state.json && python railc_a2_watchdog.py --verbose; echo \"exit=$?\"; echo \"=== state ===\"; cat ~/.claude/logs/

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\register_artifact.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Регистрирует ВЫХОД сторожа рельсы a2 в ARTIFACTS_COMMON (§5.5: новая рутина обязана\nназват

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python register_artifact.py && cd ~/.claude/scripts && python _shared/output_freshness.py 2>&1 | grep -i \"railc\\|claudeai\" | head -5; echo \"exit=$?\"", "de

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && grep -n \"verdict_persisted\" *.py | head; echo \"=== _fin in login ===\"; sed -n '53,72p' railc_login_a2.py", "description": "Is the false-ok verdict wired in?"}

---

**Claude:**

Сторож готов и зарегистрирован. Прогоняю ворота качества — до этого «готово» не говорю.

---

> `Skill` -- {"skill": "tt", "args": "сторож рельсы claude.ai/a2: railc_a2_watchdog.py + журнал входа railc_journal.py"}

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
- ⭐ **ДОКА ЖИВЁТ В КОДЕ** (dev 07.08 голосом, СУПЕР ВАЖНО): у Python-детали док = **docstring в самом файле** (назначение · вход/выход · кто дёргает · рельса · `updated: ГГГГ-ММ-ДД`), один источник — отдельный md-пересказ того же самого ⛔; тест назван в docstring, деталь названа в тесте (код·тест·дока = единый узел). Docstring отсутствует или без updated-даты → ⚠️. Канон `reglament-dokumentaciya-po-chastyam-i-vnutri-koda`.
- **ИЗМЕНЁННАЯ/ПОЧИНЕННАЯ деталь**: поведение поменялось → док обновляется **той же сессией** (док, который врёт, дороже отсутствующего); класс пойманного бага получает тест/гейт, чтобы не вернулся ([[fix-root-cause-not-symptoms]] forever-fix).
- **«Тест есть» ≠ «тест гоняют»** ([[test-exists-vs-grid-runs-it]]): тест без расписания/сетки и видимой даты прогона ≤30 дн считается несуществующим (§5.8 правило 2). Подключи в регресс-сетку или назови причину.
- ⭐ **СЧЁТЧИК ИСПОЛЬЗОВАНИЯ** (§5.8 третий атрибут, dev 04.08: «на весь функционал вешаем счётчики — кто и насколько успешно использует»): деталь считает свои вызовы строкой JSONL `ts·node·actor·event·outcome` рядом с собой (эталоны: `usage.jsonl` secondop, `_spawn_slot_guard.log`, `_chip_guard.log` — тот же паттерн, НЕ новая инфраструктура). Гейт считает ALLOW/BLOCK, скилл — старт, рутина — исход тика (не факт запуска). Флотовой механизм → лог читаем с хаба, иначе «кто пользуется» снова слепое пятно (замер 04.08: session-control-pack — применение видно 5/6, использование только локально). Нет счётчика → ⚠️. Канон `reglament-schyotchik-ispolzovaniya-na-ves-funkcional`.
  ⭐ **И ТЕСТ В НЕГО НЕ ПИШЕТ** (замер 04.09.2026): путь счётчика обязан переопределяться флагом `--counter`/env, а регресс-сетка обязана его переопределять — иначе метрика «живое или утиль» врёт. Замер: в `whatsapp_pipeline.jsonl` 67% строк написал тест, использование было завышено **в 7 раз**, и почти не используемая деталь выглядела живой. Кейс приёмки: снять размер боевого JSONL в начале теста и сверить в конце («боевой счётчик тестом НЕ тронут»). Эталон: `D:\Vault\_imports\whatsapp\_test_wa_ingest.py` (подстановка в общей `run()`). Счётчик без флага → ⚠️. Память [[counter-is-production-tests-must-not-write-it]].
- ⭐ **KILL-LIST: тест обязан сказать, что именно он ловит** (замер 11.08, [[kill-list-makes-tests-checkable]]). В докстроке теста — блок `МУТАЦИИ, КОТОРЫЕ ЭТОТ ТЕСТ ОБЯЗАН УБИТЬ`: одна строка = конкретная правка исходника → ИМЯ падающего от неё кейса. Ревьюер применяет каждую строку к **КОПИИ** детали (живую не мутируй: сторож стреляет каждые 5-20 минут) и смотрит, покраснел ли НАЗВАННЫЙ кейс. Строка не сработала = ЛОЖНАЯ заявка, и это хуже отсутствующей: по ней деталь считается защищённой. Добавь сверх списка СВОЮ мутацию — обе фикции 11.08 (кейс из одних отрицательных проверок; снятая защита, которую тест не заметил) всплыли именно на ней. Пустая мутация (добавил переменную) ничего не доказывает — сверь, что подстановка изменила поведение. Пишет тест внешняя подписка (§6.3, `secondop.py implement`), kill-list требуй прямо в спеке + «честный пробел лучше зелёного вранья».
- **Доказательство**: строка детали в карте покрытия — `python ~/.claude/scripts/coverage_map.py` (тест ✅ · док ✅ · ссылки); нет карты на узле → перечисли тест и док явными путями в вердикте. ⚠️ Карта считает покрытым только `_test_<имя детали>.py`: тест, названный по сценарию (`_test_cron_watchdog_absent.py`), в зачёт не идёт → покрытие ЗАНИЖЕНО, проверь глазами перед выводом «тестов нет».
- ⭐ **РЕЛЬСА ХРАНЕНИЯ — НАЗОВИ ОКНО ВОССТАНОВЛЕНИЯ** (dev 21.08 «почини корень»): деталь, которую зовём бэкапом / зеркалом / репликой / синком / снапшотом, выходит из /tt с ✅ только если (1) названо ОКНО — сколько времени есть на откат, и (2) показан ПРОГОН, где удаление на источнике НЕ уничтожило вторую копию. Способы ровно три: датированный карантин · версия/снимок · отказ прохода по порогу из ЗАМЕРА (медиана + наблюдённый максимум по истории прогонов, не из головы). Реплика без окна — вторая мишень, а не страховка. Отчёт обязан нести ЧИСЛО удалённого/отложенного И В ХОРОШИЕ ДНИ ТОЖЕ (цифры, которой нет в отчёте, для наблюдателя не существует), красное едет на живую рельсу, а не в файл рядом со скриптом. Нет окна или нет прогона → максимум ⚠️. Замер 21.08: зеркало E→F каждую ночь переносило в «запасную копию» все удаления суток и рапортовало успех, потому что «удалено N extras» лежит внутри кодов возврата 0-7. Канон `reglament-strahovka-ne-povtoryaet-razrushenie` + [[insurance-must-not-replay-destruction]].
- ⭐ **CLI-ДЕТАЛЬ ОБЯЗАНА ОТВЕЧАТЬ НА `--help` И БИТЬ ПО НЕИЗВЕСТНОМУ ФЛАГУ** (гейт при рождении, замер 03.09.2026): тронул/собрал скрипт, который читает аргументы → `python ~/.claude/scripts/help_flag_lint.py --check <путь>`. exit 0 = чисто ЛИБО дыра заморожена в baseline (**старый долг правку НЕ блокирует**) · **exit 1 = НОВАЯ дыра класса `unparsed-flag-silently-runs-work` → чинить В ЭТОМ ЖЕ заходе**, иначе вердикт максимум ⚠️ (лечение линт печатает сам, 3 строки в начало `main()`). Почему гейт ЗДЕСЬ, а не только в ночной сетке: ratchet краснеет НОЧЬЮ и только ОТЧЁТОМ, а отчёт ничего не держит — за 11 дней после baseline 23.08 во флот въехало **55 новых дыр, ВСЕ в файлах, тронутых после baseline** (старых 0), и класс дал 8 датированных случаев уже ПОСЛЕ объявления «закрыт» (`pr_watch.py --help` = 7.5 мин живого тика по GitHub; `output_freshness.py --help` отправил пост в живой чат 03 в 01:41). ⚠️ **exit 2 = «НЕ ПРОВЕРЕН», и это НЕ «чисто»**: файл вне корней линта (`scripts/`, `imports/`) он не сканирует — гони гейт на детали, живущей в корнях, либо задай `HELP_FLAG_LINT_ROOT`. Тест: `_test_help_flag_lint.py` секция G (мутации: вырезать ветку → G1/G3/G4/G5; гейт, который не краснеет → G2; убрать проверку корней → G6 ловит ложное зелёное).
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

## Шаг 5 — ВЕРДИКТ с доказательством
Короткая таблица: **что проверено · как (живой вывод) · ✅/⚠️/❌**. Затем одна итоговая строка:
- ✅ **PASS** — прогнал, ломал, видно — работает. ТОЛЬКО это = «готово».
- ⚠️ **PARTIAL** — работает, но есть жёлтый флаг (назови его + что осталось).
- ❌ **FAIL** — не работает / не видно → корень + что чиню.
Доказательство (вывод/счётчик/скрин) обязательно — без него «✅» не считается.

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


ARGUMENTS: сторож рельсы claude.ai/a2: railc_a2_watchdog.py + журнал входа railc_journal.py

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== prior_art ===\"; python prior_art.py build watchdog claude.ai session 2>&1 | tail -8; echo \"exit=$?\"", "description": "Шаг 0: prior art check"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== help_flag_lint ===\"; python help_flag_lint.py --check railc_a2_watchdog.py 2>&1 | tail -4; echo \"rc=$?\"; echo; echo \"=== substr_lint ===\"; python substr_lint.py railc_a2_watchdog.py _test_railc_a2_watchdog.py 2>&1 | tail -6; echo \"rc=$?\"; echo; 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== green_gap ===\"; python _shared/green_gap.py 2>&1 | tail -8; echo \"rc=$?\"; echo; echo \"=== red_verify (прибор доказывает красноту) ===\"; python red_verify.py _test_railc_a2_watchdog.py --red-flag 2>&1 | tail -10; echo \"rc=$?\"", "description": "gr

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python red_verify.py --help 2>&1 | head -30", "description": "red_verify usage"}

---

> `Bash` -- {"command": "ls ~/.claude/scripts/_shared/strict_argv.py 2>&1 && sed -n '1,25p' ~/.claude/scripts/_shared/strict_argv.py", "description": "Check strict_argv helper"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_red_mode.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Переносит kill-list из одноразового скретчпад-скрипта В САМ ТЕСТ (--red).\n\nКанон: брейк-кейс о

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python add_red_mode.py && cd ~/.claude/scripts && python _test_railc_a2_watchdog.py 2>&1 | tail -3; echo \"green rc=$?\"", "description": "Embed red mode into 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python _test_railc_a2_watchdog.py --red 2>&1 | tail -12; echo \"red rc=$?\"", "description": "Run embedded red mode"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python red_verify.py _test_railc_a2_watchdog.py --red-flag --red 2>&1 | tail -12; echo \"rc=$?\"", "description": "red_verify on the test"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_red_counter.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Доводит красный режим до контракта red_verify.py: нужен СЧЁТЧИК проверок\n('N/M passed') в об

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && python fix_red_counter.py && cd ~/.claude/scripts && python red_verify.py _test_railc_a2_watchdog.py --red-flag --red 2>&1 | tail -6", "description": "Fix coun

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "def touch_state(problems, facts, now=None):", "new_string": "def count_use(outcome, problems, counter=None):\n    \"\"\"СЧЁТЧИК ИСПОЛЬЗОВАНИЯ (§5.8): ts·node·actor·event·outcome одной строк

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\" && cat > wire_counter.py <<'PYEOF'\nimport pathlib, ast\nP = pathlib.Path.home() / \".claude\" / \"scripts\" / \"railc_a2_watchdog.py\"\ns = P.read_text(encoding=

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\wire_counter.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Вешает счётчик использования на тик сторожа (§5.8) и объявляет флаг --counter,\nчтобы тест мог п

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/wire_counter.py\" && python ~/.claude/scripts/railc_a2_watchdog.py --verbose && echo \"--- счётчик ---\" && tail -2 ~/.claude/logs/railc_a2_watchdog.jsonl", "de

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python cc-review/secondop.py panel --ritual tt --task railc-a2-watchdog --context \"Собрал сторожа рельсы claude.ai/a2: ~/.claude/scripts/railc_a2_watchdog.py (0 LLM, 0 сети, stdlib) + регрессию _test_railc_a2_watchdog.py. Контекст класса: ночной пулл claude.ai а

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python fleet_routines_collect.py 2>&1 | tail -5; echo \"---\"; grep -o \"Claude RailC A2 Watchdog\" \"D:/Vault/Vault-Knowledge/_machine-bus/_fleet-routines/routines-HUB-01.json\" 2>/dev/null | head -2", "description": "Шаг 3.5: рутина в реестр флота"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_counter_check.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Добавляет в регрессию кейс «боевой счётчик тестом НЕ тронут» (§5.8, замер 04.09:\n67% строк

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_counter_check.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -8", "description": "Add counter isolation check and re-run test"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python red_verify.py _test_railc_a2_watchdog.py --red-flag --red 2>&1 | tail -4", "description": "Re-prove redness after adding cases"}

---

> `Bash` -- {"command": "tail -45 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bm6cw4kk4.output\"", "description": "Read panel verdicts"}

---

> `Bash` -- {"command": "grep -n \"вердикт первой строкой\\|^\\*\\*\\|^###\\|^- \\*\\*\\|COUNTER\\|ACCEPT\\|BLOCK\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bm6cw4kk4.output\" | head -40", "description": "Extract panel findings"}

---

> `Bash` -- {"command": "sed -n '1,80p' \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bm6cw4kk4.output\"", "description": "Read panel head"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\panel_with_code.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Перезапуск панели с ПЕРВОИСТОЧНИКОМ вместо пересказа.\n\nПервый прогон 05.09 02:2x получил пе

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/panel_with_code.py\" 2>&1 | tail -5", "description": "Re-run panel with live code", "run_in_background": true}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review/bridge-state && ls -t | head -5; python - <<'PY'\nimport json, pathlib\np = pathlib.Path.home()/\".claude\"/\"scripts\"/\"cc-review\"/\"bridge-state\"/\"usage.jsonl\"\nrows=[json.loads(l) for l in p.read_text(encoding=\"utf-8\").splitlines() if l.strip()]\

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review/bridge-state && python -c \"\nimport json,pathlib\np=pathlib.Path('railc-a2-watchdog.json')\nd=json.loads(p.read_text(encoding='utf-8'))\nprint(type(d), list(d)[:10] if isinstance(d,dict) else len(d))\nimport sys\ntxt=json.dumps(d,ensure_ascii=False,indent

---

> `Bash` -- {"command": "cd ~/.claude/scripts && timeout 180 python coverage_map.py 2>&1 | grep -i \"railc\" | head -5; echo \"rc=$?\"", "description": "Coverage map for new parts"}

---

> `Bash` -- {"command": "F=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/panel_code_out.txt\"; wc -l \"$F\"; grep -n \"ПАНЕЛЬ:\\|вердикт первой строкой\\|^ACCEPT\\|^COUNTER\\|^BLOCK\\|^VERIFY\" \"$F\" | head -20", "description": "Panel-wi

---

> `Bash` -- {"command": "sed -n '1,56p' \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/panel_code_out.txt\"", "description": "Read full panel-with-code output"}

---

**Claude:**

Панель на живом коде нашла три настоящих дефекта (два назвали независимо два движка). Чиню.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_panel_findings.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Чинит три находки панели 05.09 (две назвали независимо ДВА движка -> чиню не думая).\n\n1.

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/fix_panel_findings.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -4 && python ~/.claude/scripts/railc_a2_watchdog.py --self-test", "de

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_panel_cases.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Запирает три находки панели 05.09 регрессией + мутациями kill-list.\n\nБез этого починка живё

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_panel_cases.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -12", "description": "Add panel regression cases"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_indent.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Чинит отступ, съехавший при вставке блока кейсов панели (заголовок печати стоял на\n4 пробелах, а 

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/fix_indent.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -14", "description": "Fix indent and run test"}

---

> `Bash` -- {"command": "sed -n '195,212p' ~/.claude/scripts/_test_railc_a2_watchdog.py | cat -A | sed 's/\\$$//' | head -20", "description": "Inspect the broken region"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python -c \"\nimport ast\ns=open('_test_railc_a2_watchdog.py',encoding='utf-8').read()\ntry:\n    ast.parse(s)\n    print('AST OK')\nexcept SyntaxError as e:\n    print('ERR line', e.lineno, ':', e.msg)\n    lines=s.splitlines()\n    for i in range(max(0,e.lineno

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_indent2.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Возвращает строке 235 её родные 8 пробелов.\n\nКорень обеих сегодняшних опечаток один: якорь заме

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/fix_indent2.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -16", "description": "Fix indent and run full test"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python red_verify.py _test_railc_a2_watchdog.py --red-flag --red 2>&1 | tail -3; echo \"--- по-мутационно ---\"; python _test_railc_a2_watchdog.py --red-each 2>&1 | tail -13", "description": "Re-prove redness incl. new panel mutations"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_killlist.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Чинит две ложные заявки kill-list, найденные прогоном --red-each.\n\n1. Мутация «детектор ложног

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/fix_killlist.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -3 && echo \"=== --red-each ===\" && python ~/.claude/scripts/_test_railc_a

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_docstring.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Приводит паспорт теста в соответствие с тем, что он реально делает и чем доказан.\n\nСтрока «ДО

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/fix_docstring.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -2; echo \"=== время ===\"; date \"+%H:%M:%S\"; echo \"=== журнал: что был

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python selfheal.py journal --help 2>&1 | head -25", "description": "selfheal journal interface"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python prior_art.py class \"сессия a2 в выделенном профиле протухает молча, вход отчитывается ok а куки не ложатся на диск\" 2>&1 | head -20; echo \"rc=$?\"", "description": "Count the class by family, not by name"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python selfheal.py journal --class \"railc-a2-session-not-persisted\" --what \"ПОЧИНКА КЛАССА: сессия a2 в _chrome_profile_a2 «протухала молча». Два прибора: (1) railc_journal.py -- 0-LLM журнал входа в ~/.claude/logs/railc_a2_session.jsonl (ВНЕ синка), пишет PRE

---

> `Bash` -- {"command": "J=~/.claude/logs/railc_a2_session.jsonl; N0=$(wc -l < \"$J\"); for i in $(seq 1 60); do sleep 30; N=$(wc -l < \"$J\"); if [ \"$N\" -gt \"$N0\" ]; then echo \"НОВЫЕ СТРОКИ ЖУРНАЛА: было $N0, стало $N\"; break; fi; done; echo \"=== итог ===\"; date \"+%H:%M:%S\"; tail -6 \"$J\" | python -

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_node_scope.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Узловая область сторожа: на узле, где рельсы a2 нет, он обязан МОЛЧАТЬ, а не орать.\n\nФайл ст

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_node_scope.py\" && python ~/.claude/scripts/railc_a2_watchdog.py --verbose && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -3", "descript

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_scope_case.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Запирает узловую область: на чужом узле сторож молчит, на своём -- судит.\"\"\"\nimport ast\ni

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_scope_case.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -6", "description": "Add node-scope case and run"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python _test_railc_a2_watchdog.py --red-each 2>&1 | tail -5; echo \"=== прибор ===\"; python red_verify.py _test_railc_a2_watchdog.py --red-flag --red 2>&1 | tail -3", "description": "Final red proof"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bp4yk0589.output\" 2>/dev/null | tail -12; echo \"---время---\"; date \"+%H:%M:%S\"", "description": "Check nightly-run watcher progress"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\update_wd_doc.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Догоняет паспорт сторожа до фактического поведения (после починок панели и узловой\nобласти). Д

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/update_wd_doc.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -2 && python ~/.claude/scripts/help_flag_lint.py --check ~/.claude/scripts

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bp4yk0589.output\" 2>/dev/null | tail -10; echo \"--- сейчас ---\"; date \"+%H:%M:%S\"", "description": "Check for the 02:50 nightly result"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && for t in _test_pull_rail_c.py _test_railc_a2_profile.py _test_railc_false_ok.py; do echo \"=== $t ===\"; timeout 120 python \"$t\" 2>&1 | tail -3; echo \"rc=$?\"; done", "description": "Run the rail's own regression tests"}

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\claude-ai\\_test_railc_journal.py", "content": "# -*- coding: utf-8 -*-\nr\"\"\"_test_railc_journal.py -- регрессия журнала входа рельсы claude.ai/a2.\n\nЗАЧЕМ: журнал -- ЕДИНСТВЕННЫЙ прибор, превративший «сессия a2 протухает» из спора двух\nгипотез в замер. Ес

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python _test_railc_journal.py 2>&1 | tail -22", "description": "Run the new journal regression"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python _test_railc_journal.py --red 2>&1 | tail -9; echo \"=== прибор ===\"; python ~/.claude/scripts/red_verify.py _test_railc_journal.py --red-flag --red 2>&1 | tail -3", "description": "Red-prove the journal test"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\journal_red_all.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Тот же контракт красноты, что у сторожа: --red = все мутации разом В ЭТОМ ЖЕ процессе\n(чтобы

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/journal_red_all.py\" && cd \"D:/Vault/_imports/claude-ai\" && python ~/.claude/scripts/red_verify.py _test_railc_journal.py --red-flag --red 2>&1 | tail -3 &

---

> `Bash` -- {"command": "date \"+%H:%M:%S\"; cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bp4yk0589.output\" 2>/dev/null | tail -12", "description": "Check watcher / time"}

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge/10-Tasks/\" | grep -i \"browser-rail\\|a2-session\\|railc\" | head -10", "description": "Find related task cards"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/10-Tasks\" && head -25 task-2026-08-10-browser-rail-down-forever-fix.md", "description": "Read the P0 task card"}

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\"; mkdir -p \"$SC/fakerail/raw\" \"$SC/fakerail/_chrome_profile_a2\"; python - <<'PY'\nimport json, pathlib, datetime, os\nsc = pathlib.Path(r\"C:\\Users\\dev\\Ap

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "                \"what\": \"вход отчитался ok, но на диске 0 claude.ai-кук (%s) -- сессия НЕ переживёт процесс, \"\n                        \"следующий пулл получит 403\" % last_post.get(\"

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad\"; python ~/.claude/scripts/railc_a2_watchdog.py --raw=\"$SC/fakerail/raw\" --journal=\"$SC/fakerail/j.jsonl\" --counter=\"$SC/fakerail/c.jsonl\" --dry-run 2>&1 | s

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\touch_task_card.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Дописывает улику в карточку P0 browser-rail-down. Карточка остаётся OPEN: закрыт\nподкласс «с

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/touch_task_card.py\" && python -c \"\nimport yaml,sys\np=r'D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-10-browser-rail-down-forever-fix.md'\ns=open(p,

---

> `Bash` -- {"command": "date \"+%H:%M:%S\"; echo \"--- watcher ---\"; cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bp4yk0589.output\" 2>/dev/null | tail -12", "description": "Check time and watcher"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python self_serving_gate.py --check \"Гипотеза «короткий TTL сессии a2» опровергнута замером: сессия прожила 16ч через три процесса. Настоящий дефект -- ложное ok при пустой банке кук.\" 2>&1 | tail -12", "description": "Self-serving conclusion gate"}

---

**Claude:**

[⏰ суббота, ночь, 02:39, 5 сентября 2026]

🎙 **Майк:** главный результат не сторож, а **опровержение**. Мы полторы недели чинили «короткий TTL» — его нет. Сессия жива 16 часов подряд. Ломается другое: логин **врёт, что вошёл**, когда куки не долетели до диска.

**Что доказано замером (а не рассуждением)**

| Проверка | Как | Итог |
|---|---|---|
| Жива ли сессия сейчас | живой гвард `pull_rail_c --plan --profile=a2` | ✅ 200, орг a2, 418 чатов, кук на диске 17 |
| «TTL полтора часа» | журнал: вход 04.09 09:38 → гвард 05.09 02:01 | ❌ **опровергнуто**, 16 ч через 3 разных процесса |
| Настоящий дефект | журнал 04.09 02:55:42 | ✅ `outcome=ok` при **0 кук**, 403 через 14 секунд |
| Второй Chromium гасит сессию? | 3 процесса на профиле за 70 с (02:00–02:02) | ❌ не подтвердилось, все три зелёные |

Сессию наследует **диск**, а не память браузера. Поэтому «логин прошёл» и «сессия есть» — два разных факта, и раньше мы мерили только первый.

**Что построено**

`railc_journal.py` — журнал входа в `~/.claude/logs/` (вне синка, грабли §4.5-бис). Пишет на каждый запуск: исход гварда, сколько claude.ai-кук **на диске**, `exit_type` браузера, отпечаток ключа шифрования, возраст последнего успешного входа. Это он и превратил спор в замер.

`railc_a2_watchdog.py` — сторож **вне** рельсы (§5.5), OS-задача 05:45, 0 LLM и 0 сети. Ловит четыре разные смерти: протухший выход, молчащий писатель, ложное ok, свежее падение. Молчит на зелёном, при красном шлёт в 03 имя больного и готовую команду лечения.

**Панель второго мнения нашла три настоящих дефекта в моей же починке**, два назвали Codex и Grok независимо: `posts[-1]` брал последнюю строку **файла**, а не последнюю **по времени** (свежий 403 прятался за дописанным старым ok); анти-спам штамповался **до** отправки, поэтому упавший `bus_send` глушил тревогу на 12 часов ровно тогда, когда сломана рельса доклада; `ck_claude == 0` не ловил строковый `"0"`. Все три починены и заперты регрессией.

**Краснота доказана прибором, не глазомером:** `red_verify.py` → канарейка строгая, зелёный 25/25, красный 15/25; по-мутационно 11 из 11 сломов убивают сетку. Первый прогон показал 2 ложные заявки в kill-list (протухший якорь и неизолированный случай) — обе починены.

⚠️ **Честные границы.** Задачу Планировщика удалось завести только `Interactive-only`: S4U требует elevation, `schtasks` вернул Access denied. На всегда-включённом хабе она сработает, на разлогиненном узле — нет. И 16 часов жизни измерены на профиле, **пересозданном 04.09 в интерактивном контексте**; переживёт ли куки безлюдный S4U-прогон 02:50 — ещё не доказано. Этот прогон стартует через 11 минут, сторож его запишет, доложу результатом.

Дашборд не строю: фактов для решения мало и они укладываются в таблицу выше (§2.4, причина названа).

🧒 **Простыми словами:** мы думали, что ключ от двери быстро ржавеет. Оказалось, ключ хороший и держится сутки. Беда в другом: иногда робот радостно кричит «я вошёл!», а ключ в этот момент выпал из кармана и до полки не доехал. Теперь у нас есть тетрадка, куда робот записывает, лежит ли ключ на полке, и сторож, который утром смотрит в тетрадку и будит нас, если ключа нет.

И отдельно: **половина третьего ночи**. Иди спать, я тут сам доработаю и положу результат в отчёт — прогон в 02:50 никуда не денется, а ты завтра нужен живым.

---

**User:**

<task-notification>
<task-id>bp4yk0589</task-id>
<tool-use-id>toolu_011QdK3YJsk1WmKyr8Qeumy9</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_d32d0e25\tasks\bp4yk0589.output</output-file>
<status>completed</status>
<summary>Background command "Wait for the 02:50 nightly run and report" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/tasks/bp4yk0589.output\"", "description": "Read the 02:50 experiment result"}

---

> `Bash` -- {"command": "date \"+%H:%M:%S\"; echo \"=== задача ===\"; powershell -NoProfile -Command \"schtasks /query /tn 'ClaudeAI Sync Nightly' /fo list /v\" 2>&1 | grep -iE \"Last Run Time|Last Result|Status|Next Run\"; echo \"=== хвост лога ===\"; tail -6 ~/.claude/scripts/_claudeai_sync_nightly.log", "des

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_ctx_field.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Добавляет в журнал поле `ctx` -- в КАКОМ контексте шёл прогон.\n\nЗачем именно это поле. Ночь 0

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_ctx_field.py\" && cd \"D:/Vault/_imports/claude-ai\" && python _test_railc_journal.py 2>&1 | tail -2 && python _test_railc_false_ok.py 2>&1 | tail -2 && 

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"\\$p=Get-Process -Id \\$PID; 'powershell SessionId: ' + \\$p.SessionId; 'explorer SessionId: ' + ((Get-Process explorer -ErrorAction SilentlyContinue | Select-Object -First 1).SessionId); 'SESSIONNAME env: [' + \\$env:SESSIONNAME + ']'\" 2>&1 | tail -5; 

---

**Claude:**

Мой же прибор чуть не соврал: `SESSIONNAME` пуст, но процесс идёт в **сессии 1**, а не в нулевой. Чиню детектор, пока он не отравил журнал.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\fix_ctx_detector.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Чинит детектор контекста, пойманный на вранье через 4 минуты после рождения.\n\nПервая верси

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/fix_ctx_detector.py\" && cd \"D:/Vault/_imports/claude-ai\" && python -c \"\nimport sys; sys.path.insert(0,'.')\nimport railc_journal as m\nprint('ctx =', m.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_ctx_case.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Запирает починенный детектор контекста красным кейсом.\n\nДефект жил четыре минуты, но он образц

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_ctx_case.py\" && cd \"D:/Vault/_imports/claude-ai\" && python _test_railc_journal.py 2>&1 | tail -8 && echo \"=== по-мутационно ===\" && python _test_rai

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/claude-ai\" && python ~/.claude/scripts/red_verify.py _test_railc_journal.py --red-flag --red 2>&1 | tail -3; echo \"=== боевой прогон гварда: ctx попадёт в журнал ===\"; SCRATCH=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/58cf8618-f

---

> `Bash` -- {"command": "cd ~/.claude/logs && tail -2 railc_a2_session.jsonl | python -c \"\nimport sys, json\nfor l in sys.stdin:\n    r = json.loads(l)\n    print('%s %-5s %-4s ctx=%-11s winsess=%-4s ck=%-4s %s' % (r.get('ts_local','')[:19], r.get('event'), r.get('phase'), r.get('ctx'), r.get('winsession'), r

---

**Claude:**

Сторож напечатал **отрицательный возраст журнала** — это ложь прибора, разбираюсь.

---

> `Bash` -- {"command": "cd ~/.claude/logs && python -c \"\nimport json, time\nfrom datetime import datetime, timezone\nrows=[json.loads(l) for l in open('railc_a2_session.jsonl',encoding='utf-8') if l.strip()]\nlast=rows[-1]\nprint('ts_utc  :', last['ts_utc'])\nprint('ts_local:', last['ts_local'])\nt=datetime.

---

> `Bash` -- {"command": "python ~/.claude/scripts/railc_a2_watchdog.py --json 2>&1 | python -c \"\nimport sys, json\nd=json.load(sys.stdin)\nf=d['facts']\nprint('journal_age_h:', f.get('journal_age_h'))\nprint('last_line    :', f.get('last_line'))\nprint('bundle       :', f.get('bundle'))\nprint('problems     :

---

**Claude:**

Нашёл: не расчёт, а **сама печатная строка** — `0.0 or -1` даёт `-1` (нулевой возраст ложно-отрицателен). Прибор врал в собственном статусе.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\railc_a2_watchdog.py", "old_string": "            b = facts.get(\"bundle\")\n            print(\"🟢 railc-a2 здорова: выход %s (%.1fч), журнал %s строк (%.1fч), последний исход %s\" % (\n                b[\"name\"] if b else \"-

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\add_zero_age_case.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Запирает «ложно-отрицательный ноль» в статусной строке сторожа.\n\nЗамер 05.09 03:05: на по

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/add_zero_age_case.py\" && python ~/.claude/scripts/_test_railc_a2_watchdog.py 2>&1 | tail -3 && echo \"=== мутации ===\" && python ~/.claude/scripts/_test_railc

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== red_verify (сторож) ===\"; python red_verify.py _test_railc_a2_watchdog.py --red-flag --red 2>&1 | tail -2; echo \"=== red_verify (журнал) ===\"; cd \"D:/Vault/_imports/claude-ai\" && python ~/.claude/scripts/red_verify.py _test_railc_journal.py --r

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_d32d0e25\\scratchpad\\journal_help_gate.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Закрывает дыру класса unparsed-flag-silently-runs-work в CLI журнала.\n\nОпечатка во флаге 

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_d32d0e25/scratchpad/journal_help_gate.py\" && cd \"D:/Vault/_imports/claude-ai\" && echo \"--- help ---\" && python railc_journal.py --help 2>&1 | head -2 && echo \"--- мусорный

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python substr_lint.py railc_a2_watchdog.py _test_railc_a2_watchdog.py \"D:/Vault/_imports/claude-ai/railc_journal.py\" \"D:/Vault/_imports/claude-ai/_test_railc_journal.py\" 2>&1 | tail -3; echo \"=== _test_no_control_bytes ===\"; python _test_no_control_by

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close --zone vault-imports/claudeai-rail-c 2>&1 | tail -2; echo \"=== рутина в реестре ===\"; python fleet_routines_collect.py 2>&1 | tail -1; echo \"=== выход рутины ===\"; python _shared/output_freshness.py 2>&1 | grep -i railc", "description": 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close --zone vault-imports/claudeai-rail-c 2>&1 | tail -2; echo \"=== рутина в реестре флота ===\"; python fleet_routines_collect.py 2>&1 | tail -1", "description": "Close ON AIR and refresh routine registry"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py list 2>&1 | grep -i \"claudeai-rail-c\"; python onair.py close 2>&1 | tail -2", "description": "Close my ON AIR declaration"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ID=$(python onair.py list --json 2>/dev/null | python -c \"\nimport sys,json\ntry:\n    d=json.load(sys.stdin)\nexcept Exception:\n    sys.exit(1)\nrows=d if isinstance(d,list) else d.get('claims') or d.get('active') or []\nfor r in rows:\n    if 'claudeai-rail-c

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -o '2026-09-05T[0-9T]*Z-HUB-01-58cf8618[a-z0-9-]*' \"D:/Vault/Vault-Knowledge/_onair/ACTIVE_NOW.md\" 2>/dev/null | head -3; ls \"D:/Vault/Vault-Knowledge/_onair/\" 2>/dev/null | grep -i \"58cf8618\" | head -3", "description": "Locate the claim i

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close --help 2>&1 | head -8; echo \"---\"; grep -rl \"claudeai-rail-c\" \"D:/Vault/Vault-Knowledge/_onair/\" 2>/dev/null | head -3", "description": "Inspect close usage and claim storage"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2026-09-05T095239Z-HUB-01-58cf8618-vault-imports-claudeai-rail-c 2>&1 | tail -2; echo \"---\"; python onair.py list 2>&1 | grep -ci \"claudeai-rail-c\"", "description": "Close the declaration by its id"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -nE \"^(STORE|DB|BOARD|ROOT)\\s*=|_onair|onair.*\\.json|\\.db\" onair.py 2>/dev/null | head -8", "description": "Find onair storage path"}

---

> `Bash` -- {"command": "ls \"D:/Vault/Vault-Knowledge/_machine-bus/_onair/active/\" 2>/dev/null | grep -i \"58cf8618\" | head -3", "description": "Find my claim file"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close \"HUB-01__58cf8618__vault-imports-claudeai-rail-c__2026-09-05T010129Z\" 2>&1 | tail -2; python onair.py list 2>&1 | grep -ci \"claudeai-rail-c\"", "description": "Close the ON AIR claim"}

---

> `Bash` -- {"command": "python -c \"\nimport json\np=r'D:\\Vault\\Vault-Knowledge\\_machine-bus\\_onair\\active\\HUB-01__58cf8618__vault-imports-claudeai-rail-c__2026-09-05T010129Z.json'\nd=json.load(open(p,encoding='utf-8'))\nprint({k:d[k] for k in list(d)[:12]})\"", "description": "Read claim json 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close \"2026-09-05T010129Z-HUB-01-58cf8618-vault-imports-claudeai-rail-c\" 2>&1 | tail -2; python onair.py list 2>&1 | grep -ci \"claudeai-rail-c\"", "description": "Close claim by real id"}

---

> `Bash` -- {"command": "date \"+%H:%M\"; echo \"--- итоговое состояние рельсы ---\"; python ~/.claude/scripts/railc_a2_watchdog.py --verbose; echo \"--- задача планировщика ---\"; powershell -NoProfile -Command \"schtasks /query /tn 'Claude RailC A2 Watchdog' /fo list\" 2>&1 | grep -E \"TaskName|Next Run|Statu

---

**Claude:**

[⏰ суббота, ночь, 03:10, 5 сентября 2026]

🎙 **Майк:** ночной эксперимент не состоялся, и это тоже результат. Задача 02:50 увидела свежий бандл от 02:01 и **пропустила пулл целиком** — браузер не поднимался, значит вопрос «губит ли безлюдный контекст банку кук» так и не проверен. Ставить опыт насильно не стал: S4U-задачу без прав администратора не завести, а гонять Chromium на боевом профиле ради опыта — это и есть тот риск, который мы изучаем.

Вместо опыта сделал так, чтобы ответ **выпал из обычной работы**: каждая строка журнала теперь несёт контекст прогона. Первый же настоящий ночной пулл покажет пару «безлюдная сессия + сколько кук легло» рядом с уже известной парой «живая сессия + 17 кук», и гипотезы разведутся сами.

**Ловил себя за руку дважды, оба раза прибор врал зелёным.** Детектор контекста сначала судил по переменной `SESSIONNAME`: пусто значит безлюдный. Замер тут же показал, что это неправда — в этом самом процессе переменная пуста, а Windows-сессия равна 1, ровно как у проводника. Переписал на настоящий идентификатор сессии процесса, число пишу в журнал уликой. Второй случай: статусная строка сторожа напечатала «журнал 26 строк (**-1.0ч**)» на здоровой рельсе, потому что свежий журнал даёт возраст 0.0, а в питоне `0.0 or -1` возвращает минус единицу. Расчёт был верен, врала печать. Оба дефекта заперты красными кейсами.

**Вердикт `/tt`**

| Что | Как проверено | Итог |
|---|---|---|
| Журнал входа | 18 проверок, 6 мутаций, `red_verify` | ✅ зелёный 18/18, красный 11/18 |
| Сторож | 26 проверок, 12 мутаций, `red_verify` | ✅ зелёный 26/26, красный 15/26 |
| Сторож вживую | подделал протухший выход и ложное ok | ✅ два диагноза с именем и лечением |
| Задача в Планировщике | `schtasks /run`, чтение лога | ✅ отработала, следующая 05:45 |
| Рельса сейчас | живой гвард | ✅ 200, орг a2, 418 чатов, 17 кук |
| Второе мнение | панель на живом коде | ✅ 3 находки, все починены |
| Тесты рельсы | 4 файла | ✅ все зелёные |
| **Корень класса** | эксперимент 02:50 не состоялся | ⚠️ **не доказан** |

**Итог: ⚠️ PARTIAL.** Приборы готовы и доказаны, рельса жива, слепое пятно закрыто. Но корень «почему в некоторых прогонах куки не доезжают до диска» остаётся гипотезой, и выдавать это за закрытый класс я не буду.

Флоту не раздаю: рельса живёт только на хабе, профиль машинно-локален. Сторож приедет на пиры вместе с папкой скриптов и там **молчит по маркеру узла** — иначе каждый пир орал бы «нет журнала» каждую ночь. Раздачу миру (`/share-fix`) откладываю по названной причине: раздают починку с доказанным корнем, а у нас пока доказан только диагноз.

⚠️ Одна честная слабость: задачу сторожа удалось завести только `Interactive-only`, потому что `schtasks` отказал в правах на S4U. На всегда-включённом хабе она сработает, на разлогиненном узле — нет. Это записано в её паспорте, не спрятано.

🧒 **Простыми словами:** ночью робот должен был сходить за новыми чатами и заодно показать нам, теряется ли ключ в темноте. Но он увидел, что чаты уже принесли час назад, и никуда не пошёл. Опыт не получился. Тогда я приделал к тетрадке новую графу: «кто ходил — дневной человек или ночной робот». Теперь в следующий раз ответ запишется сам, без всяких опытов. А ещё я дважды поймал свои же приборы на вранье и починил их, потому что прибор, который врёт зелёным, хуже сломанного.

Сейчас **десять минут четвёртого**. Всё зафиксировано, сторож встанет в 05:45 сам и без тебя. Иди спать, пожалуйста.
