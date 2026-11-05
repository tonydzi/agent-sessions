---
session: s_0c244bd7
date: 2026-09-14
words: 3149
turns: 15
tools: "Bash, Edit, PowerShell, ToolSearch, Write, mcp__ccd_session_mgmt__set_session_title, mcp__telegram__get_history, mcp__whatsapp2__get_my_profile, mcp__whatsapp__list_messages, mcp__whatsapp__search_contacts, mcp__whatsapp__send_message"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-14 · Scheduled run: auto-hub-260903-debt-voice-whisper-translate

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0c244bd7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260903-debt-voice-whisper-translate" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260903-debt-voice-whisper-translate\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Класс `wa-write-rail-lock-war` / `wa-mcp-instance-storm`. 14.09.2026 — **пятый датированный случай**, и он УЖЕ в Breakage-Journal с замером. Починка по этому же taskId прогонялась 10.09.2026 и класс НЕ закрыла.

СНАЧАЛА прочитай ~/.claude/scripts/routine-autonomy-block.md (ROUTINE-COFOUNDER-AUTONOMY) и $OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md.

## ⚠️ ГИПОТЕЗА «два брокера делят соединение» ОПРОВЕРГНУТА ЗАМЕРОМ — не гоняйся за ней
Я так думал в 13:13 и ошибся. `prior_art.py` вытащил из журнала шесть прежних строк, и настоящий корень назван числами:
- 14.09: «5-й датированный: send_message read-only, **147 висящих stdio-инстансов whatsapp-mcp** (старший 5452 мин = 3.8 суток)».
- 11.09: «~45 параллельных экземпляров whatsapp-mcp (**пара main+wa2 на КАЖДУЮ сессию Claude**), write достаётся первому».
- 11.09: «45 stale node-процессов от старых робот-сессий держали лок коннекта по очереди».
- 10.09: «134 legacy stdio whatsapp-mcp, снял 132» — то есть прошлый «ремонт» был УБОРКОЙ ПРОЦЕССОВ, а не починкой корня. Через четыре дня их снова 147.

Корень: **каждая сессия Claude поднимает свою пару stdio-инстансов коннектора, и они не умирают вместе с сессией**. Лок достаётся случайному старому процессу, живая сессия получает read-only. Убийство процессов лечит симптом на день-два.

## Что сделать
1. Пройди круг §5.5 «спроси инструмент»: `--help` коннектора, его конфиг и env, доки ТОЙ ЖЕ версии — есть ли штатный режим одного общего сервера (shared/http-транспорт вместо stdio-на-сессию), есть ли TTL/идле-таймаут у инстанса.
2. Взвесь и назови цену каждого: **один долгоживущий брокер + все сессии к нему** (убирает сам источник размножения) · **reaper по возрасту процесса** (дешевле, но это опять уборка) · **передача владения локом с TTL**. АК-47: выбери то, что оператор починит сам.
3. Тест обязан покраснеть на сломанном коде: сценарий «подняты два инстанса, живая сессия шлёт» → без фикса read-only, с фиксом уходит.
4. Раскатка по флоту §7.3-бис: инстансы плодит КАЖДЫЙ узел, значит починка бессмысленна на одном. Канарейка → verify читает факт → остальные.

## Долг, который закрывается этой починкой
Отправить [ИМЯ] в WhatsApp **[ТЕЛЕФОН]** дубль первого шага онбординга (текст — последнее сообщение в TG-группе chat_REDACTED). Это реальный непоставленный дубль 14.09, не тест.

Отчёт в TG-03: корень, красный тест, кто раскатан, ушёл ли дубль [ИМЯ]. Если снова получится только уборка процессов — скажи это прямо словом «уборка, не починка», и класс останется открытым.
</scheduled-task>

---

**Claude:**

**13:45**

Начинаю починку класса `wa-write-rail-lock-war` / `wa-mcp-instance-storm`. Сначала читаю обязательные блоки и проверяю замер.

---

> `Bash` -- {"command": "cat ~/.claude/scripts/routine-autonomy-block.md 2>/dev/null; echo \"=== SEED-STOP-DUP ===\"; cat \"D:/Vault/Vault-Knowledge/08-Templates/seed-stop-dup-block.md\" 2>/dev/null", "description": "Read autonomy block and stop-dup block"}

---

> `Bash` -- {"command": "cat ~/.claude/scripts/routine-autonomy-block.md 2>/dev/null | head -60", "description": "Read routine autonomy block"}

---

> `Bash` -- {"command": "cd ~ && python -c \"\nimport json,os\np=os.path.expanduser('~/.claude.json')\nd=json.load(open(p,encoding='utf-8'))\nms=d.get('mcpServers',{})\nfor k,v in ms.items():\n    if 'whats' in k.lower(): print(k, json.dumps(v,ensure_ascii=False))\n\" 2>&1 | head -20", "description": "Read what

---

> `Bash` -- {"command": "node \"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\\index.js\" --help 2>&1 | head -60", "description": "whatsapp-mcp --help"}

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\" && cat package.json 2>&1 | head -40 && echo \"=== DIST ===\" && ls dist/ 2>&1 | head -40", "description": "Inspect whatsapp-mcp package"}

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\" && echo \"=== index.js (arg parsing / main) ===\" && grep -n \"argv\\|process.env.WHATSAPP_MCP_URL\\|connect-proxy\\|http-server\\|--http\\|--serve\\|--connect\" index.js | head -40", "description

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\" && sed -n '1,200p' index.js", "description": "Read index.js main"}

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\" && sed -n '200,260p' index.js && echo \"=== connect-proxy.js ===\" && cat connect-proxy.js", "description": "Read rest of index.js and connect-proxy.js"}

---

> `PowerShell` -- {"command": "$procs = Get-CimInstance Win32_Process -Filter \"Name='node.exe'\" | Where-Object { $_.CommandLine -like '*whatsapp-mcp*' }\n\"TOTAL whatsapp-mcp node procs: $($procs.Count)\"\n$g = $procs | Group-Object { if ($_.CommandLine -like '*--connect*') {'connect-proxy'} elseif ($_.CommandLine 

---

> `PowerShell` -- {"command": "$procs = Get-CimInstance Win32_Process -Filter \"Name='node.exe'\" | Where-Object { $_.CommandLine -like '*whatsapp-mcp*' -and $_.CommandLine -notlike '*--connect*' -and $_.CommandLine -notlike '*--http*' }\nforeach ($p in $procs) {\n  \"=== pid=$($p.ProcessId) ppid=$($p.ParentProcessId

---

> `Bash` -- {"command": "grep -rl \"whatsapp-mcp\" \"C:/Users/dev/.claude/\" \"E:/!CLAUDE-HUBPC-June26/\" \"C:/Users/dev/.claude.json\" 2>/dev/null --include=\"*.json\" --include=\"*.mcp.json\" | head -30", "description": "Find all configs referencing whatsapp-mcp"}

---

> `PowerShell` -- {"command": "$cands = @(\n \"$env:USERPROFILE\\.claude.json\",\n \"$env:USERPROFILE\\.claude\\settings.json\",\n \"$env:USERPROFILE\\.claude\\settings.local.json\",\n \"$env:USERPROFILE\\.claude\\.mcp.json\",\n \"$env:USERPROFILE\\.claude\\mcp.json\",\n \"E:\\!CLAUDE-HUBPC-June26\\.mcp.json\",\

---

> `Bash` -- {"command": "python -c \"\nimport json,os,datetime\np=os.path.expanduser('~/.claude.json')\nprint('mtime:', datetime.datetime.fromtimestamp(os.path.getmtime(p)))\nd=json.load(open(p,encoding='utf-8'))\nprint('--- TOP-LEVEL mcpServers whatsapp ---')\nfor k,v in d.get('mcpServers',{}).items():\n    if

---

> `PowerShell` -- {"command": "Get-ChildItem \"$env:USERPROFILE\\.claude\\scripts\" -Filter \"*wa*\" -File -ErrorAction SilentlyContinue | Select-Object -ExpandProperty Name\n\"--- broker-ish ---\"\nGet-ChildItem \"$env:USERPROFILE\\.claude\\scripts\" -Recurse -Include \"*.py\",\"*.cmd\",\"*.ps1\" -ErrorAction Silent

---

> `PowerShell` -- {"command": "Get-Content \"$env:USERPROFILE\\.claude\\scripts\\wa_broker.py\" -TotalCount 120", "description": "Read wa_broker.py head"}

---

> `PowerShell` -- {"command": "$roots = @(\"D:\\Vault\\Vault-Knowledge\",\"D:\\Vault\\_imports\",\"C:\\Users\\dev\\.claude\",\"C:\\Users\\dev\",\"E:\\!CLAUDE-HUBPC-June26\")\nforeach ($r in $roots) {\n  Get-ChildItem $r -Filter \".mcp.json\" -File -ErrorAction SilentlyContinue | ForEach-Object { \"FOUN

---

> `PowerShell` -- {"command": "python \"$env:USERPROFILE\\.claude\\scripts\\wa_broker.py\" --status 2>&1 | Select-Object -First 60", "description": "Run wa_broker status"}

---

> `PowerShell` -- {"command": "Get-Content \"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\\lock.js\"", "description": "Read lock.js"}

---

> `PowerShell` -- {"command": "python -c \"\nimport psutil,sys\nfor pid in (78204,189180,107584):\n    try:\n        p=psutil.Process(pid)\n        e=p.environ()\n        keys={k:v for k,v in e.items() if 'WHATSAPP' in k.upper() or k.upper()=='XDG_DATA_HOME' or k.upper()=='MCP_API_KEY'}\n        print(pid, 'created',

---

**Claude:**

Корень найден и доказан замером. Теперь — долг [ИМЯ], параллельно с починкой. Беру текст из TG-группы.

---

> `ToolSearch` -- {"query": "select:mcp__telegram__get_history,mcp__telegram__list_accounts", "max_results": 5}

---

> `mcp__telegram__get_history` -- {"chat_id": chat_REDACTED, "limit": 6}

---

> `ToolSearch` -- {"query": "select:mcp__whatsapp__search_contacts,mcp__whatsapp__send_message,mcp__whatsapp2__search_contacts,mcp__whatsapp2__send_message,mcp__whatsapp__list_messages,mcp__whatsapp2__list_messages", "max_results": 8}

---

> `mcp__whatsapp__search_contacts` -- {"query": "id_83204a1d"}

---

> `mcp__whatsapp__send_message` -- {"jid": "[EMAIL]", "text": "[ИМЯ], привет. Это Майкрофт — напарник оператора, тот самый ИИ, который знает про его работу примерно всё. Дублирую сюда то же, что написал в телеграм-комнату, чтобы точно не потерялось.\n\nЧто мы делаем. За несколько дней развернём тебе то же самое, что с

---

> `mcp__whatsapp__list_messages` -- {"jid": "[EMAIL]", "limit": 3}

---

**Claude:**

Долг закрыт (доказано: сообщение в сторе, 12:51 UTC). Теперь корень.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ WA lock-war корень (5-й случай)"}

---

> `PowerShell` -- {"command": "$pkg=\"C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\"\n\"--- patches dir ---\"; Get-ChildItem \"$pkg\\patches\" -ErrorAction SilentlyContinue | Select-Object -ExpandProperty Name\n\"--- existing vendor-patch scripts of ours ---\"\nGet-ChildItem \"$env:US

---

> `PowerShell` -- {"command": "python \"$env:USERPROFILE\\.claude\\scripts\\workspace_write_lease.py\" status 2>&1 | Select-Object -First 30", "description": "Check workspace lease status"}

---

**Claude:**

Пишу починку. Сначала патчер вендора в scratchpad.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\wa_vendor_patch.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"wa_vendor_patch.py -- close the class `wa-write-rail-lock-war` / `wa-

---

> `Bash` -- {"command": "SCR=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\"\nSB=\"$SCR/sandbox-pkg\"\nrm -rf \"$SB\"; mkdir -p \"$SB/dist\"\ncp \"/c/Users/dev/AppData/Roaming/npm/node_modules/[СКРЫТО]/dist/\"*.js \"$SB/dis

---

**Claude:**

Поймал ложно-зелёное в собственном патчере: маркеры в строке импортов обманывали `--verify`. Чиню.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\wa_vendor_patch.py", "old_string": "# `path` and `net` are not imported by the vendor's index.js.\nIMPORT_ANCHOR = 'import fs from \"fs

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\wa_vendor_patch.py", "old_string": "def verify(pkg):\n    \"\"\"[] when every guard is in place, otherwise the names of the missing one

---

> `Bash` -- {"command": "SCR=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\"\nSB=\"$SCR/sandbox-pkg\"\nrm -rf \"$SB\"; mkdir -p \"$SB/dist\"\ncp \"/c/Users/dev/AppData/Roaming/npm/node_modules/[СКРЫТО]/dist/\"*.js \"$SB/dis

---

**Claude:**

Патчер работает. Теперь красный тест — обе поломки воспроизводим на **неисправленном** коде.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"_test_wa_vendor_patch.py -- regression for the class `wa-write-

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "def sandbox(patched):\n    \"\"\"A private copy of dist/, optionally patched. Never touches t

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "    root, index_js = sandbox(patched)\n    results = []\n    try:\n        for name, fn in TE

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && timeout 400 python _test_wa_vendor_patch.py 2>&1 | tail -30", "description": "Run red-then-green regression", "timeout": 420000}

---

**Claude:**

T1 не позеленел — проверяю, врёт ли `process.kill(ppid,0)` на Windows (зомби-PID при открытом хэндле).

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && python - <<'PY'\nimport subprocess, sys, os, time\n# victim: a short-lived python; the test process keeps its Popen handle open (zombie PID case)\nv = subproce

---

**Claude:**

`kill(0)` не врёт. Значит виснет сам `shutdown()`. Ловлю stderr сироты.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "    r, w = os.pipe()  # `w` stays open in THIS process: the sibling that keeps stdin alive\n 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "        if died_at is None:\n            _kill(child)\n            return False, (\n         

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && timeout 200 python -c \"\nimport _test_wa_vendor_patch as T, tempfile, shutil\nroot, idx = T.sandbox(patched=True)\nh = tempfile.mkdtemp(prefix='wadata-')\ntry

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && timeout 120 python -c \"\nimport _test_wa_vendor_patch as T, tempfile, shutil, subprocess, os, time, sys\nroot, idx = T.sandbox(patched=True)\nh = tempfile.mkd

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "    errlog = os.path.join(data_home, \"orphan.err\")\n    os.makedirs(data_home, exist_ok=Tru

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "    finally:\n        os.close(w)\n        _kill(parent.pid, tree=True)", "new_string": "    

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && timeout 200 python -c \"\nimport _test_wa_vendor_patch as T, tempfile, shutil\nroot, idx = T.sandbox(patched=True)\nh = tempfile.mkdtemp(prefix='wadata-')\ntry

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && timeout 180 python -c \"\nimport _test_wa_vendor_patch as T, tempfile, shutil, subprocess, sys, os, time, psutil\nroot, idx = T.sandbox(patched=True)\nh = temp

---

**Claude:**

Найдено: `os.kill(pid, 0)` на Windows **убивает** процесс (Python вызывает `TerminateProcess`) — мой тест сам стрелял в подопытного. Чиню детектор жизни.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\_test_wa_vendor_patch.py", "old_string": "def _alive(pid):\n    try:\n        os.kill(pid, 0)\n        return True\n    except OSError:

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\" && sed -i 's/^import tempfile$/import tempfile\\nimport psutil/' _test_wa_vendor_patch.py && grep -n \"^import psutil\" _test_wa_vendor_patch.py && timeout 500 py

---

**Claude:**

Оба теста красные на вендоре как есть, зелёные после патча. Ставлю на живую систему.

---

> `Bash` -- {"command": "SCR=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\"\nDST=\"/c/Users/dev/.claude/scripts\"\ncp \"$SCR/wa_vendor_patch.py\" \"$DST/wa_vendor_patch.py\" && echo \"installed wa_vendor_patch.py\"\ncp \"$SCR/_test_wa_

---

> `Bash` -- {"command": "DST=\"/c/Users/dev/.claude/scripts\"\npython \"$DST/wa_vendor_patch.py\" --apply; echo \"exit=$?\"\necho \"--- node syntax check on live files ---\"\nnode --check \"/c/Users/dev/AppData/Roaming/npm/node_modules/[СКРЫТО]/dist/index.js\" && echo \"index.js OK\"\nnode --ch

---

> `PowerShell` -- {"command": "Get-Content \"$env:USERPROFILE\\.claude\\scripts\\mcp_whatsapp_http.cmd\"\n\"--- scheduled tasks mentioning whatsapp/wa ---\"\nGet-ScheduledTask -ErrorAction SilentlyContinue | Where-Object { $_.TaskName -match 'wa|whats' } | Select-Object TaskName,State | Format-Table -AutoSize\n\"--- 

---

> `PowerShell` -- {"command": "\"--- kill legacy stdio owners (they hold both locks) ---\"\nforeach ($pid in 78204,189180) { $r = taskkill /PID $pid /F 2>&1; \"  $pid -> $r\" }\n\"--- restart brokers so they load the patched code ---\"\nforeach ($t in \"Claude WA Broker Owner (main)\",\"Claude WA Broker Owner (wa2)\"

---

> `PowerShell` -- {"command": "foreach ($p in 78204,189180) { $r = (taskkill /PID $p /F 2>&1) -join ' '; \"  $p -> $r\" }\nStart-Sleep -Seconds 8\n\"--- descriptors ---\"\nforeach ($f in \"$env:USERPROFILE\\.local\\share\\whatsapp-mcp\\store\\.broker.json\",\"$env:USERPROFILE\\.local\\share\\wa-wa2\\whatsapp-mcp\\sto

---

> `PowerShell` -- {"command": "\"--- listeners ---\"\nGet-NetTCPConnection -State Listen -LocalPort 8791,8792 -ErrorAction SilentlyContinue | ForEach-Object { \"  port=$($_.LocalPort) pid=$($_.OwningProcess)\" }\n\"--- all whatsapp-mcp procs now ---\"\nGet-CimInstance Win32_Process -Filter \"Name='node.exe'\" | Where

---

> `PowerShell` -- {"command": "python -c \"\nimport psutil\nfor p in psutil.process_iter(['pid','name','cmdline','create_time']):\n    try:\n        cl=' '.join(p.info['cmdline'] or [])\n    except Exception: continue\n    if 'whatsapp-mcp' in cl:\n        print(p.info['pid'], p.info['name'], '|', cl.replace(r'C:\\Us

---

> `PowerShell` -- {"command": "Get-Process node -ErrorAction SilentlyContinue | Select-Object Id,StartTime | Sort-Object StartTime | Format-Table -AutoSize\n\"--- cim retry ---\"\n$r = Get-CimInstance Win32_Process -Filter \"Name='node.exe'\"\n\"node procs seen by CIM: $($r.Count)\"\n$r | Where-Object { $_.CommandLin

---

> `PowerShell` -- {"command": "$out = (taskkill /PID 114644 /F 2>&1) -join ' '; \"kill 114644 -> $out\"\nStart-Sleep -Seconds 3\nStart-ScheduledTask -TaskName \"Claude WA Broker Owner (wa2)\"\nStart-Sleep -Seconds 12\n$d2 = \"$env:USERPROFILE\\.local\\share\\wa-wa2\\whatsapp-mcp\\store\\.broker.json\"\nif (Test-Path 

---

> `PowerShell` -- {"command": "\"attempt 1: purpose-built door\"\npython \"$env:USERPROFILE\\.claude\\scripts\\wa_broker.py\" --stop --account wa2 2>&1 | Select-Object -First 5\nStart-Sleep -Seconds 3\n$still = (Get-NetTCPConnection -State Listen -LocalPort 8792 -ErrorAction SilentlyContinue | Select-Object -First 1)

---

> `PowerShell` -- {"command": "Start-ScheduledTask -TaskName \"Claude WA Broker Owner (wa2)\"\nStart-Sleep -Seconds 15\n$d2 = \"$env:USERPROFILE\\.local\\share\\wa-wa2\\whatsapp-mcp\\store\\.broker.json\"\nif (Test-Path $d2) { \"wa2 descriptor: $(Get-Content $d2 -Raw)\" } else { \"wa2 descriptor: MISSING\" }\npython 

---

> `PowerShell` -- {"command": "\"attempt 3: Stop-Process\"\ntry { Stop-Process -Id 114644 -Force -ErrorAction Stop; \"  stopped\" } catch { \"  ERR: $($_.Exception.Message)\" }\nStart-Sleep -Seconds 2\n\"exists in tasklist? \"\n(tasklist /FI \"PID eq 114644\" /NH 2>&1) -join ' '\n\"8792 listener:\"\nGet-NetTCPConnect

---

> `mcp__whatsapp2__get_my_profile` -- {}

---

> `PowerShell` -- {"command": "$f=\"$env:USERPROFILE\\.claude\\scripts\\wa_broker.py\"\n$lines = Get-Content $f\n$start = ($lines | Select-String -Pattern \"^def watch\\(\\):\" | Select-Object -First 1).LineNumber\n$lines[($start-1)..($start+40)] | ForEach-Object { $_ }", "description": "Read wa_broker watch()"}

---

**Claude:**

Вешаю дверь: сторож теперь проверяет, не снёс ли npm-update патч.

---

> `Bash` -- {"command": "python - <<'PY'\nimport io, os, re\np = os.path.expanduser(r\"~/.claude/scripts/wa_broker.py\")\ns = io.open(p, encoding=\"utf-8\").read()\n\nif \"_vendor_guards_missing\" in s:\n    print(\"already wired\"); raise SystemExit(0)\n\nhelper = '''\ndef _vendor_guards_missing():\n    \"\"\"

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_0c244bd7\\scratchpad\\wire_watch.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"One-shot: teach wa_broker.py --watch to notice that npm update wiped the v

---

> `Bash` -- {"command": "SCR=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_0c244bd7/scratchpad\"\ncp \"/c/Users/dev/.claude/scripts/wa_broker.py\" \"$SCR/wa_broker.py.bak-prepatchcheck\" && echo \"backup made\"\npython \"$SCR/wire_watch.py\"\npython -c \"i

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_wa_broker_patchcheck.py", "content": "#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"_test_wa_broker_patchcheck.py -- сторож `wa_broker.py --watch` обязан КРАСНЕТЬ, когда\nnpm update снёс патчи вендора (wa_vendor_patch.py).\n\nЗачем: к

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts && timeout 180 python _test_wa_broker_patchcheck.py 2>&1 | tail -12", "description": "Run watchdog patch-check regression", "timeout": 200000}

---

**Claude:**

Канарейка (хаб) зелёная. Раскатываю на флот.

---

> `Bash` -- {"command": "python deploy_register.py --help 2>&1 | head -40", "description": "Check deploy_register CLI"}

---

> `Bash` -- {"command": "python fleet_nodes.py 2>&1 | head -20 || python -c \"\nimport json,os\np=os.path.expanduser('~/.claude/fleet_nodes.json')\nd=json.load(open(p,encoding='utf-8'))\nnodes = d.get('nodes', d)\nfor k,v in (nodes.items() if isinstance(nodes,dict) else [(n.get('name'),n) for n in nodes]):\n   

---

> `Bash` -- {"command": "python - \"$PWD\" <<'EOF'\nimport io, os, sys\np = os.path.join(sys.argv[1], \"wa_vendor_patch.py\")\ns = io.open(p, encoding=\"utf-8\").read()\nif \"not a consumer\" in s:\n    print(\"already handled\"); raise SystemExit(0)\nold = \"    pkg = os.path.expanduser(a.pkg)\\n\"\nnew = (\" 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\wa_vendor_patch.py", "old_string": "    pkg = os.path.expanduser(a.pkg)\n\n    if a.verify:", "new_string": "    pkg = os.path.expanduser(a.pkg)\n\n    # Не каждый узел флота держит whatsapp-mcp. Отсутствие вендора -- НЕ поломк

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts\npython wa_vendor_patch.py --verify --pkg \"/c/nonexistent-pkg\"; echo \"non-consumer exit=$?\"\npython wa_vendor_patch.py --verify; echo \"live exit=$?\"\ncp wa_vendor_patch.py \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/765

---

**Claude:**

Тест должен работать и на уже пропатченной машине — беру заводские файлы из `.waorig`.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_wa_vendor_patch.py", "old_string": "    if patched:\n        wa_vendor_patch.apply(pkg)\n        missing = wa_vendor_patch.verify(pkg)\n        if missing:\n            raise AssertionError(\"sandbox patch incomplete: %s\

---

> `Bash` -- {"command": "timeout 500 python _test_wa_vendor_patch.py 2>&1 | tail -10", "description": "Re-run full red-green on patched machine", "timeout": 540000}

---

> `Bash` -- {"command": "python deploy_register.py all wa-vendor-lockwar-guards-20260914 \"WhatsApp: три защиты внутри вендора против войны локов и шторма инстансов (5-й случай класса)\" \"python ~/.claude/scripts/wa_vendor_patch.py --apply\" \"python ~/.claude/scripts/wa_vendor_patch.py --verify\" --verdict PA

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts\nDEPLOY_ALLOW_WINDOWS_CMD=1 python deploy_register.py HUB-01,NODE-0X-2023PAL,NODE-0X wa-vendor-lockwar-guards-win-20260914 \"WhatsApp: три защиты внутри вендора против войны локов и шторма инстансов (5-й случай класса)\" \"python %USERPRO

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts\nDEPLOY_ALLOW_POSIX_CMD=1 python deploy_register.py FLEET-ANCHOR,NODE-0X,NODE-0X wa-vendor-lockwar-guards-posix-20260914 \"WhatsApp: три защиты внутри вендора против войны локов и шторма инстансов (5-й случай класса)\" \"python3 ~/.claude/

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/scripts\npython selfheal.py journal --class wa-write-rail-lock-war --what \"5-й случай ЗАКРЫТ починкой корня, а не уборкой. Корень измерен в коде вендора [СКРЫТО] 2.4.0, три дефекта: (D1) ветка --http зовёт initWhatsApp() НЕ трогая acquireWhatsAppL

---

> `Bash` -- {"command": "ls -la \"/e/Obsidian/Vault-Knowledge/00-System/\" 2>/dev/null | grep -i breakage\npython selfheal.py journal --class wa-write-rail-lock-war-root-closed --what \"ЗАКРЫТИЕ класса wa-write-rail-lock-war (5-й случай, 14.09): чинили КОРЕНЬ в вендоре, не процессы. Три дефекта @sjawhar/whatsap

---

> `Bash` -- {"command": "tail -c 1200 \"/e/Obsidian/Vault-Knowledge/00-System/Breakage-Journal.md\"", "description": "Inspect journal tail format"}

---

> `Bash` -- {"command": "python routine_runlog.py add --routine auto-hub-260903-debt-voice-whisper-translate --what \"Класс wa-write-rail-lock-war закрыт ПОЧИНКОЙ КОРНЯ в вендоре (не уборкой процессов). Найдено 3 дефекта [СКРЫТО] 2.4.0: D1 ветка --http зовёт initWhatsApp БЕЗ acquireWhatsAppLock (дв

---

> `Bash` -- {"command": "python bus_send.py \"🔧 WA lock-war: ПОЧИНКА КОРНЯ, не уборка (5-й случай класса закрыт)\n\nКОРЕНЬ измерен в коде вендора [СКРЫТО] 2.4.0, три дефекта, все проверяемы:\nD1 — ветка --http зовёт initWhatsApp() НЕ трогая acquireWhatsAppLock: брокер и legacy-инстанс держат ДВА со

---

**Claude:**

**13:45 → конец смены** (точную метку конца не ставлю: гейт call-budget разрешает только закрывающие вызовы, часы дёрнуть нечем).

## Это починка, а не уборка

Слово «уборка» произносить не пришлось. Корень найден **в коде вендора**, а не в списке процессов — и все три дефекта проверяемы построчно.

**D1.** `dist/index.js`, ветка `--http`: брокер зовёт `initWhatsApp()`, **ни разу не тронув** `acquireWhatsAppLock()`. Тот самый замок, который уважает stdio-ветка, назначенный владелец игнорирует. Отсюда два живых сокета Baileys на один аккаунт, WhatsApp выбивает одного, и проигравший отвечает `send_message` из SQLite только на чтение.

**D2.** Сторож сирот в `index.js` и `connect-proxy.js` читает `/proc/self/stat`, а в `catch` возвращает `process.ppid`, который Node **кэширует при старте**. На Windows сравнение `currentPpid !== originalPpid` не может стать истинным никогда — сторож вечный no-op. Вот откуда 134 инстанса 10.09 и 147 сегодня.

**D3.** Приложение Claude кэширует определение MCP-сервера **при своём запуске**. `psutil` показал решающее: у обоих legacy-pid нет ни `WHATSAPP_MCP_URL`, ни `MCP_API_KEY` — вообще пустой env, тогда как у брокера они есть. Значит `~/.claude.json` был флипнут на `--connect` уже давно, но сессии до сих пор рождаются в до-брокерной форме. Поэтому уборка 10.09 и продержалась ровно четыре дня.

## Что построено

[wa_vendor_patch.py](../../../Users/dev/.claude/scripts/wa_vendor_patch.py) — идемпотентный патчер с `--verify` / `--revert` и бэкапами `.waorig`. Одной фразой: **рядом живёт брокер — любой инстанс молча становится его прокси, брокер держит замок, а сирота умирает сам.** Цена трёх вариантов взвешена: рипер по возрасту — снова уборка, отвергнут; передача владения с TTL — протокол, которого у вендора нет и который оператор не отладит; выбран третий — вендор уже несёт нужную форму (`--http` + `--connect`), ей не хватало замка, дискавери и смерти сироты.

## Красный показан мутацией

[_test_wa_vendor_patch.py](../../../Users/dev/.claude/scripts/_test_wa_vendor_patch.py) гоняет сценарии сперва на **заводском** вендоре, поднятом из `.waorig`:

```
RED  T1 orphan dies   orphan 183376 STILL ALIVE 30s after its parent died
RED  T2 auto-proxy    broker published no .broker.json
GREEN T1 orphan dies  orphan exited after parent death
GREEN T2 auto-proxy   plain instance attached as proxy
```

T2 поднимает брокер, потом plain-инстанс с **вычищенным env** — ровно та форма, что измерена на legacy-pid сегодня. Отдельно [_test_wa_broker_patchcheck.py](../../../Users/dev/.claude/scripts/_test_wa_broker_patchcheck.py) краснеет, когда `npm update` сносит патч: сторож `wa_broker.py --watch` теперь проверяет защиты, а не только открытый порт.

По дороге поймал два ложно-зелёных у себя: маркер в строке импортов обманывал мой же `--verify`, а `os.kill(pid, 0)` на Windows не опрашивает, а **вызывает `TerminateProcess`** — тест расстреливал подопытного и потом вечно считал его живым.

## Раскатка и долг

Посылки `wa-vendor-lockwar-guards-win-20260914` (хаб, NODE-0X, Нора) и `-posix-20260914` (Маяк, оба Mac). Хаб = канарейка: applied+verified, legacy-инстансов 0, дескриптор main опубликован.

**Дубль [ИМЯ] ушёл** — WhatsApp [ТЕЛЕФОН], шаг 1 онбординга, `3EB012E04528304A80099C`, подтверждён чтением стора.

## Хвосты, которые не закрыл

Строка закрытия класса не легла в Breakage-Journal — дедуп `selfheal.py` отбил, класс журналился утром. Брокер wa2 (pid 114644) живёт в сессии 0: три разные попытки снять (`taskkill /F`, `wa_broker.py --stop`, `Stop-Process`) дали Access denied — нужен UAC; патч он подхватит при следующем старте своей задачи, рельса wa2 при этом жива. Заметку в волт не завёл — упёрся в потолок вызовов.

🧒 **Простыми словами:** у нас есть один «телефонист», через которого все сессии пишут в WhatsApp. Раньше он хватал трубку, не глядя, занята ли линия — и когда другая программа тоже хватала ту же трубку, сообщения переставали уходить, но никто об этом не говорил. Ещё старые программки не умирали, когда их хозяин уходил, и их накопилось полторы сотни. Теперь: телефонист сначала берёт замок, вешает рядом записку «я тут, звоните мне», все остальные читают записку и просто передают ему свои слова, а брошенная программка сама выключается за пять секунд. И я это не на словах проверил — сперва сломал обратно и показал, что тесты краснеют.
