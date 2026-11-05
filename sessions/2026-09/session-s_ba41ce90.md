---
session: s_ba41ce90
date: 2026-09-05
words: 32657
turns: 79
tools: "AskUserQuestion, Bash, Edit, Glob, Grep, PowerShell, Read, Skill, ToolSearch, WebSearch, Write, mcp__ccd_session_mgmt__get_session"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-05 · На этом компьютере, на этом компьютере мекать аномалии. Мы постоянно вылогиниваете Chrome…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ba41ce90` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

На этом компьютере, на этом компьютере мекать аномалии. Мы постоянно вылогиниваете Chrome. Я только что недавно сходил в Facebook вчера или позавчера. И снова мне недавно надо заходить. Посмотри, в чем проблема, поищи какие-нибудь корни, потому что это просто ужасно. Постоянно мне приходит заново залогиниваться в вообще в клоды, в Facebook, абсолютно во все. То, что такой-то треш какой-то происходит.

---

**Claude:**

[⏰ воскресенье, день, 13:05, 30 августа 2026]

Using superpowers:systematic-debugging to investigate — это баг-расследование, а не правка.

---

> `Skill` -- {"skill": "superpowers:systematic-debugging", "args": "Chrome на хабе HUB-01 постоянно вылогинивает из всех сайтов (Facebook, claude.ai и т.д.) — найти корень"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\plugins\cache\superpowers-marketplace\superpowers\6.2.0\skills\systematic-debugging

# Systematic Debugging

## Overview

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

**Violating the letter of this process is violating the spirit of debugging.**

## The Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

If you haven't completed Phase 1, you cannot propose fixes.

## When to Use

Use for ANY technical issue:
- Test failures
- Bugs in production
- Unexpected behavior
- Performance problems
- Build failures
- Integration issues

**Use this ESPECIALLY when:**
- Under time pressure (emergencies make guessing tempting)
- "Just one quick fix" seems obvious
- You've already tried multiple fixes
- Previous fix didn't work
- You don't fully understand the issue

**Don't skip when:**
- Issue seems simple (simple bugs have root causes too)
- You're in a hurry (rushing guarantees rework)
- Manager wants it fixed NOW (systematic is faster than thrashing)

## The Four Phases

You MUST complete each phase before proceeding to the next.

### Phase 1: Root Cause Investigation

**BEFORE attempting ANY fix:**

1. **Read Error Messages Carefully**
   - Don't skip past errors or warnings
   - They often contain the exact solution
   - Read stack traces completely
   - Note line numbers, file paths, error codes

2. **Reproduce Consistently**
   - Can you trigger it reliably?
   - What are the exact steps?
   - Does it happen every time?
   - If not reproducible → gather more data, don't guess

3. **Check Recent Changes**
   - What changed that could cause this?
   - Git diff, recent commits
   - New dependencies, config changes
   - Environmental differences

4. **Gather Evidence in Multi-Component Systems**

   **WHEN system has multiple components (CI → build → signing, API → service → database):**

   **BEFORE proposing fixes, add diagnostic instrumentation:**
   ```
   For EACH component boundary:
     - Log what data enters component
     - Log what data exits component
     - Verify environment/config propagation
     - Check state at each layer

   Run once to gather evidence showing WHERE it breaks
   THEN analyze evidence to identify failing component
   THEN investigate that specific component
   ```

   **Example (multi-layer system):**
   ```bash
   # Layer 1: Workflow
   echo "=== Secrets available in workflow: ==="
   echo "IDENTITY: ${IDENTITY:+SET}${IDENTITY:-UNSET}"

   # Layer 2: Build script
   echo "=== Env vars in build script: ==="
   env | grep IDENTITY || echo "IDENTITY not in environment"

   # Layer 3: Signing script
   echo "=== Keychain state: ==="
   security list-keychains
   security find-identity -v

   # Layer 4: Actual signing
   codesign --sign "$IDENTITY" --verbose=4 "$APP"
   ```

   **This reveals:** Which layer fails (secrets → workflow ✓, workflow → build ✗)

5. **Trace Data Flow**

   **WHEN error is deep in call stack:**

   See `root-cause-tracing.md` in this directory for the complete backward tracing technique.

   **Quick version:**
   - Where does bad value originate?
   - What called this with bad value?
   - Keep tracing up until you find the source
   - Fix at source, not at symptom

### Phase 2: Pattern Analysis

**Find the pattern before fixing:**

1. **Find Working Examples**
   - Locate similar working code in same codebase
   - What works that's similar to what's broken?

2. **Compare Against References**
   - If implementing pattern, read reference implementation COMPLETELY
   - Don't skim - read every line
   - Understand the pattern fully before applying

3. **Identify Differences**
   - What's different between working and broken?
   - List every difference, however small
   - Don't assume "that can't matter"

4. **Understand Dependencies**
   - What other components does this need?
   - What settings, config, environment?
   - What assumptions does it make?

### Phase 3: Hypothesis and Testing

**Scientific method:**

1. **Form Single Hypothesis**
   - State clearly: "I think X is the root cause because Y"
   - Write it down
   - Be specific, not vague

2. **Test Minimally**
   - Make the SMALLEST possible change to test hypothesis
   - One variable at a time
   - Don't fix multiple things at once

3. **Verify Before Continuing**
   - Did it work? Yes → Phase 4
   - Didn't work? Form NEW hypothesis
   - DON'T add more fixes on top

4. **When You Don't Know**
   - Say "I don't understand X"
   - Don't pretend to know
   - Ask for help
   - Research more

### Phase 4: Implementation

**Fix the root cause, not the symptom:**

1. **Create Failing Test Case**
   - Simplest possible reproduction
   - Automated test if possible
   - One-off test script if no framework
   - MUST have before fixing
   - Use the `superpowers:test-driven-development` skill for writing proper failing tests

2. **Implement Single Fix**
   - Address the root cause identified
   - ONE change at a time
   - No "while I'm here" improvements
   - No bundled refactoring

3. **Verify Fix**
   - Test passes now?
   - No other tests broken?
   - Issue actually resolved?
   - Use the `superpowers:verification-before-completion` skill before claiming success

4. **If Fix Doesn't Work**
   - STOP
   - Count: How many fixes have you tried?
   - If < 3: Return to Phase 1, re-analyze with new information
   - **If ≥ 3: STOP and question the architecture (step 5 below)**
   - DON'T attempt Fix #4 without architectural discussion

5. **If 3+ Fixes Failed: Question Architecture**

   **Pattern indicating architectural problem:**
   - Each fix reveals new shared state/coupling/problem in different place
   - Fixes require "massive refactoring" to implement
   - Each fix creates new symptoms elsewhere

   **STOP and question fundamentals:**
   - Is this pattern fundamentally sound?
   - Are we "sticking with it through sheer inertia"?
   - Should we refactor architecture vs. continue fixing symptoms?

   **Discuss with your human partner before attempting more fixes**

   This is NOT a failed hypothesis - this is a wrong architecture.

## Red Flags - STOP and Follow Process

If you catch yourself thinking:
- "Quick fix for now, investigate later"
- "Just try changing X and see if it works"
- "Add multiple changes, run tests"
- "Skip the test, I'll manually verify"
- "It's probably X, let me fix that"
- "I don't fully understand but this might work"
- "Pattern says X but I'll adapt it differently"
- "Here are the main problems: [lists fixes without investigation]"
- Proposing solutions before tracing data flow
- **"One more fix attempt" (when already tried 2+)**
- **Each fix reveals new problem in different place**

**ALL of these mean: STOP. Return to Phase 1.**

**If 3+ fixes failed:** Question the architecture (see Phase 4.5)

## your human partner's Signals You're Doing It Wrong

**Watch for these redirections:**
- "Is that not happening?" - You assumed without verifying
- "Will it show us...?" - You should have added evidence gathering
- "Stop guessing" - You're proposing fixes without understanding
- "Ultra-think this" - Question fundamentals, not just symptoms
- "We're stuck?" (frustrated) - Your approach isn't working

**When you see these:** STOP. Return to Phase 1.

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Issue is simple, don't need process" | Simple issues have root causes too. Process is fast for simple bugs. |
| "Emergency, no time for process" | Systematic debugging is FASTER than guess-and-check thrashing. |
| "Just try this first, then investigate" | First fix sets the pattern. Do it right from the start. |
| "I'll write test after confirming fix works" | Untested fixes don't stick. Test first proves it. |
| "Multiple fixes at once saves time" | Can't isolate what worked. Causes new bugs. |
| "Reference too long, I'll adapt the pattern" | Partial understanding guarantees bugs. Read it completely. |
| "I see the problem, let me fix it" | Seeing symptoms ≠ understanding root cause. |
| "One more fix attempt" (after 2+ failures) | 3+ failures = architectural problem. Question pattern, don't fix again. |

## Quick Reference

| Phase | Key Activities | Success Criteria |
|-------|---------------|------------------|
| **1. Root Cause** | Read errors, reproduce, check changes, gather evidence | Understand WHAT and WHY |
| **2. Pattern** | Find working examples, compare | Identify differences |
| **3. Hypothesis** | Form theory, test minimally | Confirmed or new hypothesis |
| **4. Implementation** | Create test, fix, verify | Bug resolved, tests pass |

## When Process Reveals "No Root Cause"

If systematic investigation reveals issue is truly environmental, timing-dependent, or external:

1. You've completed the process
2. Document what you investigated
3. Implement appropriate handling (retry, timeout, error message)
4. Add monitoring/logging for future investigation

**But:** 95% of "no root cause" cases are incomplete investigation.

## Supporting Techniques

These techniques are part of systematic debugging and available in this directory:

- **`root-cause-tracing.md`** - Trace bugs backward through call stack to find original trigger
- **`defense-in-depth.md`** - Add validation at multiple layers after finding root cause
- **`condition-based-waiting.md`** - Replace arbitrary timeouts with condition polling


ARGUMENTS: Chrome на хабе HUB-01 постоянно вылогинивает из всех сайтов (Facebook, claude.ai и т.д.) — найти корень

---

> `PowerShell` -- {"command": "$ud = \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\"; Get-ChildItem $ud -Directory | Where-Object {$_.Name -match 'Default|Profile'} | Select-Object Name, LastWriteTime; Write-Output \"---LocalState---\"; (Get-Item \"$ud\\Local State\").LastWriteTime", "description": "L

---

> `Grep` -- {"pattern": "taskkill.*chrome|kill.*chrome|Stop-Process.*chrome|remote-debugging-port|user-data-dir", "path": "C:\\Users\\dev\\.claude\\scripts", "output_mode": "content", "-i": true, "head_limit": 60}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\fix-chrome-bridge.ps1"}

---

> `PowerShell` -- {"command": "$prefs = Get-Content \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Preferences\" -Raw | ConvertFrom-Json; Write-Output \"exit_type: $($prefs.profile.exit_type)\"; Write-Output \"exited_cleanly: $($prefs.profile.exited_cleanly)\"; $prefs.profile.content_settings

---

> `PowerShell` -- {"command": "$c = Get-Item \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\Cookies\"; Write-Output \"Cookies DB: created $($c.CreationTime) modified $($c.LastWriteTime) size $($c.Length)\"; Write-Output \"---scheduled tasks mentioning chrome/bridge---\"; Get-Schedule

---

> `Grep` -- {"pattern": "fix-chrome-bridge", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches", "head_limit": 30}

---

> `PowerShell` -- {"command": "$ls = Get-Item \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Local State\"; Write-Output \"Local State: created $($ls.CreationTime) modified $($ls.LastWriteTime)\"; $j = Get-Content $ls.FullName -Raw | ConvertFrom-Json; $st = $j.user_experience_metrics.stability; Write-

---

> `Grep` -- {"pattern": "taskkill.*chrome|Stop-Process.*chrome|kill.*chrome\\.exe", "path": "D:\\Vault\\_imports", "output_mode": "content", "-i": true, "head_limit": 30}

---

> `Grep` -- {"pattern": "вылогин|разлогин|relogin|logged out|logout|перелогин", "path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "output_mode": "content", "-i": true}

---

> `Grep` -- {"pattern": "вылогин|разлогин|перелогин|relogin|куки слет|cookie.*(слет|lost|wipe)", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "content", "-i": true, "head_limit": 40}

---

> `PowerShell` -- {"command": "Write-Output \"=== System restarts/shutdowns last 14 days ===\"; Get-WinEvent -FilterHashtable @{LogName='System'; Id=41,1074,6008; StartTime=(Get-Date).AddDays(-14)} -ErrorAction SilentlyContinue | Select-Object TimeCreated, Id, @{n='Info';e={($_.Message -split \"`n\")[0]}} | Format-Ta

---

> `PowerShell` -- {"command": "Write-Output \"=== chrome.exe app crashes/hangs last 14d ===\"; Get-WinEvent -FilterHashtable @{LogName='Application'; Id=1000,1002; StartTime=(Get-Date).AddDays(-14)} -ErrorAction SilentlyContinue | Where-Object {$_.Message -match 'chrome'} | Select-Object TimeCreated, Id | Format-Tabl

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\claudeai-sync-needs-a2-account.md"}

---

> `PowerShell` -- {"command": "$p = Get-Process chrome | Sort-Object StartTime | Select-Object -First 1; Write-Output \"Oldest chrome.exe start: $($p.StartTime)\"; Write-Output \"chrome count: $((Get-Process chrome).Count)\"; Write-Output \"=== profiles in Local State ===\"; $j = Get-Content \"C:\\Users\\dev\\AppDa

---

> `PowerShell` -- {"command": "$src=\"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\Cookies\"; $dst=\"$env:LOCALAPPDATA\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\cookies_copy.db\"; New-Item -ItemType Directory -Force (Split-Path $ds

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\cookie_audit.py", "content": "import sqlite3, datetime, sys\n\ndef chrome_ts(t):\n    if not t:\n        return '-'\n    return (datetime.datetime(1601, 1, 1

---

> `PowerShell` -- {"command": "$sp=\"$env:LOCALAPPDATA\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\"; esentutl /y \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\Cookies\" /d \"$sp\\cookies_copy.db\" /vss | Select-Object -Last 2; pytho

---

> `PowerShell` -- {"command": "$sp=\"$env:LOCALAPPDATA\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\"; Get-Item \"$sp\\cookies_copy.db\" | Select-Object Length, LastWriteTime; esentutl /y \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\

---

> `Glob` -- {"pattern": "10-Tasks/**/task-2026-08-10-browser-rail-down*", "path": "D:\\Vault\\Vault-Knowledge"}

---

> `Grep` -- {"pattern": "restarting Chrome|relaunch|Chrome relaunched|CloseMainWindow|перезапуск Chrome|рестарт Chrome", "path": "C:\\Users\\dev\\.claude\\scripts\\_logs", "output_mode": "content", "-i": true, "head_limit": 20}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-10-browser-rail-down-forever-fix.md"}

---

> `PowerShell` -- {"command": "(Get-WinEvent -FilterHashtable @{LogName='System'; Id=1074; StartTime=(Get-Date).AddDays(-5)} | Select-Object -First 1).Message; Write-Output \"===\"; python -c \"\nimport sqlite3\ncon = sqlite3.connect(r'C:\\Users\\dev\\.claude\\scripts\\fb_guard.db')\nprint(con.execute('select name 

---

> `Grep` -- {"pattern": "checkpoint|разлогин|вылогин|Facebook.*(вход|логин)|FB.*(разлог|логин)", "path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "output_mode": "content", "-i": true, "head_limit": 15}

---

**Claude:**

Рестарт 27.08 инициировал наш же робот («Claude: repair MSIX package limbo»). Читаю строки журнала поломок про разлогины.

---

> `PowerShell` -- {"command": "$f=\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"; $lines = Get-Content $f -Encoding UTF8; foreach($n in 41,65,122,378,631,634,637,869,1019,1124,1193,1347,1513,1612,1617,1637){ $t=$lines[$n-1]; if($t.Length -gt 260){$t=$t.Substring(0,260)+'…'}; Write-Output \"[$n] $t\

---

> `PowerShell` -- {"command": "$f=\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"; $lines = Get-Content $f -Encoding UTF8; Write-Output \"=== [122] ===\"; $lines[121]; Write-Output \"=== [631] ===\"; $lines[630]; Write-Output \"=== [1193] ===\"; $lines[1192]; Write-Output \"=== [1347] ===\"; $lines[

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "limit": 40}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "old_string": "## Строки (append-only, новые сверху)\n\n- 2026-08-30 02:5x", "new_string": "## Строки (append-only, новые сверху)\n\n- 2026-08-30 13:2x (HUB-01, живая сессия по жалобе оператора «

---

**Claude:**

Теперь чиню мелочь с уликой: fix-chrome-bridge.ps1 добивает Chrome через 4 секунды, а куки коммитятся батчем ~30с.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\fix-chrome-bridge.ps1", "old_string": "# graceful close, then hard kill leftovers (Chrome lingers in background)\n$chrome | ForEach-Object { $_.CloseMainWindow() | Out-Null }\nStart-Sleep 4\nGet-Process chrome -ErrorAction Sile

---

> `PowerShell` -- {"command": "cd C:\\Users\\dev\\.claude; git add scripts/fix-chrome-bridge.ps1; git commit -m @'\nfix-chrome-bridge: wait up to 45s for graceful Chrome exit before hard kill\n\nChrome commits cookies in ~30s batches; the old 4s kill was a crash exit\nthat could eat fresh login cookies (part of the

---

**Claude:**

scripts/ в ~/.claude вне git (игнорится) — тогда по §5.11 подпись идёт в change_ledger.

---

> `PowerShell` -- {"command": "$led=\"C:\\Users\\dev\\.claude\\change_ledger\\HUB-01.jsonl\"; New-Item -ItemType Directory -Force (Split-Path $led) | Out-Null; $rec = @{ts=(Get-Date).ToUniversalTime().ToString('yyyy-MM-ddTHH:mm:ssZ'); file='scripts/fix-chrome-bridge.ps1'; change='wait up to 45s for graceful 

---

**Claude:**

[⏰ воскресенье, день, 13:13, 30 августа 2026]

🎙 Майк: корень нашёл, и он неприятный: главный «вылогиниватель» из claude.ai - это мы сами, наши же ночные роботы. С Facebook хуже: там нас выкидывает сервер Meta за автоматизацию с твоего аккаунта. Один вопрос тебе в конце.

## Что происходит: три причины, все с датированными уликами

**1. claude.ai: война человека с роботом за один браузер (корень доказан, уже починено этой ночью).**
Ночная рутина claudeai-sync до вчерашнего дня «лечила» себя прямо в твоём живом Chrome: делала logout на claude.ai и входила под рабочий аккаунт a2 по magic-link. Ты входишь под своим аккаунтом (bb) - робот ночью тебя вылогинивает - утром ты снова у логин-стены. Это повторилось минимум трижды (14.08, 20.08, 27.08, всё в журнале поломок). В журнале висел открытый вопрос «кто перещёлкивает Chrome обратно на bb» - ответ: ты сам, и это нормально, аккаунт твой. Ночью 30.08 параллельная сессия увела робота в отдельный профиль `_chrome_profile_a2`, твой Chrome он больше не трогает. **Если после сегодняшнего дня claude.ai снова разлогинит - скажи, значит корень не только этот.**

**2. Facebook: сессию убивает сервер Meta, не Chrome.**
Улики: 19.08 FB требовал «подтверди личность» (чекпойнт), 23.08 и 25.08 - логин-стена, куки `c_user` нет. Решающий факт добавила твоя жалоба: ты входил в FB 28-29.08, сегодня снова выкинуло, при этом Chrome непрерывно работает с 28.08 18:30 и машина не перезагружалась с 27.08. То есть куки не «потерялись» - Meta погасила сессию со своей стороны, прожила она сутки-двое. Наиболее вероятная причина: риск-движок Meta реагирует на ежедневную автоматизацию с твоего аккаунта (fb-reply, fb-likes до 40 ответов и 60 лайков в день) плюс входы с нескольких машин.

**3. Отягчитель: Chrome на хабе регулярно умирает «грязно».**
Хаб перезагружали 10 раз за 14 дней (в основном руками через AnyDesk, один раз наш робот 27.08 в 6:29 командой shutdown для починки MSIX). Chrome при этом помечен как «Crashed», а куки он пишет на диск порциями раз в ~30 секунд - свежий логин перед ребутом может просто не доехать до диска. Плюс наш скрипт рестарта Chrome добивал его через 4 секунды после закрытия - это я уже починил (теперь ждёт до 45с), подпись правки в change_ledger.

## Что сделано этой сессией
- Разбор записан строкой в Breakage-Journal (закрыт открытый вопрос строки 27.08).
- [fix-chrome-bridge.ps1](C:\Users\dev\.claude\scripts\fix-chrome-bridge.ps1) больше не убивает Chrome раньше сброса куков.

## Что требует твоего решения (это не чинится браузером)
У FB нет запасной безлюдной рельсы (токен пуст с 11.07), и каждый разлогин Meta = снова твои руки. Варианты: (а) сбавить темп fb-автоматизации, чтобы риск-движок успокоился; (б) поднять токен-рельсу Graph API, чтобы роботы не жили в твоей браузерной сессии; (в) оставить как есть и принять перелогин раз в 1-2 дня как цену. Я за (б)+(а) вместе. Что выбираешь?

🧒 Простыми словами: у тебя один браузер, а живут в нём двое - ты и роботы. Робот ночью выходил из твоего Клода, чтобы войти под своим аккаунтом, поэтому утром тебя «выкидывало». Это уже починили: роботу дали отдельный браузер. А Фейсбук выгоняет тебя сам, со своей стороны: ему не нравится, что с твоего аккаунта кто-то слишком ровно и много лайкает. Пока роботы работают из-под тебя, Фейсбук будет выгонять снова и снова.

[⏰ воскресенье, день, 13:14, 30 августа 2026]

---

**User:**

Stop hook feedback:
СТОП: ты объявляешь недоступность, не обойдя ВСЕ поверхности.
  фрагмент: …трогает. **Если после сегодняшнего дня claude.ai снова разлогинит - скажи, значит корень не только этот.*…
(последний обход: x, 1586 мин назад — не тот вендор или устарел)

Класс замерен трижды за трое суток (29-31.07): вывод «Google мёртв» делался по ОДНОМУ
профилю, пока живая сессия лежала в Chrome на другом аккаунте. Каждый повтор = ложный
аск оператору + день не той работы.

Сделай ДО вывода:
    python3 ~/.claude/scripts/rail_sweep.py claude_ai
Он перечислит ВСЕ места (профили рельсы · системный Firefox · профили Chrome · Chrome-MCP)
и назовёт те, что с диска не читаются — их проверяют ЖИВОЙ вкладкой, а не файлом.
Вывод «доступа нет» законен, только когда пусты ВСЕ поверхности из списка.
Если место одно и ты это знаешь — так и напиши: «в профиле X сессии нет» (per-профиль),
а не «X недоступен» (про весь мир).

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\rail_sweep.py claude_ai 2>&1 | Select-Object -First 60", "description": "Sweep all claude.ai auth surfaces before concluding", "timeout": 180000}

---

**Claude:**

[⏰ воскресенье, день, 13:16, 30 августа 2026]

Принял поправку сторожа: прогнал обход всех поверхностей `rail_sweep.py claude_ai`. Уточняю формулировку, чтобы она была про-профильной, а не «про весь мир»:

- Поверхностей с claude.ai на этой машине три: системный Firefox (профиль 646yqiss, куки есть), Firefox-профиль fbread (куки есть) и Chrome с MCP-расширением (с диска не читается, живость только вкладкой).
- Мой вывод про «войну за аккаунт» касается ровно ОДНОЙ поверхности: профиля **Chrome Default** на хабе, где живёшь ты и где до 30.08 ночной робот делал logout и вход под a2. Firefox-профили этой войной не задеты, там свои сессии (по прошлым замерам обе под bbplatinum).
- «Если снова разлогинит» читай так: если после 30.08 тебя снова выкинет из claude.ai **именно в Chrome Default**, значит в этом профиле есть ещё один переключатель, кроме уже уведённого робота, и я вернусь копать по строке журнала.

Остальное из моего разбора (Meta-серверные разлогины FB, грязные смерти Chrome при ребутах) этой поправкой не меняется.

🧒 Простыми словами: я уточнил адрес поломки. Не «Клод выкидывает вообще», а «выкидывало в одном конкретном браузерном профиле, где робот жил вместе с тобой». Из этого профиля робота уже выселили.

[⏰ воскресенье, день, 13:16, 30 августа 2026]

---

**User:**

(б) поднять токен-рельсу Graph API, чтобы роботы не жили в твоей браузерной сессии!! Написано у меня ещё и куча других вещей вылогиливается. Ага. Так. что-то делать. Может быть, на, может, можно пишет правила Библи, что ты всегда работаешь на веб-прям, напишем правила Библию. Хочешь два делать, два делать отдельной сессии? Всегда работаем через лицо, всегда работаем через лису, всегда работаем через Firefox. Firefox всегда. А Chrome используем как запасный вариант. Твои раскатанные слоты уже создал балла. Чинить это. Вообще. Да, экстати, пункт первый. С этого компьютера тоже отправил Библию. Мы же делали уже это правило. Я всегда работаю через аккаунт Биби Платину. Клод на этом компьютере всегда запустится, включён за работу через Биби Платин. Всегда запиши я, пожалуйста, без зарубин на носу. Пожалуйста, сделай так, чини корни. Чни все корни, чини все корни.  O

---

**Claude:**

[⏰ воскресенье, день, 13:19, 30 августа 2026]

Принято: (б) токен-рельса Graph API, правило «Firefox всегда, Chrome запасной», правило «Клод на этом компе всегда под bbplatinum», починка корней в отдельных сессиях через слоты. Сначала RECALL: проверяю, что из этих правил уже записано, чтобы не плодить дубли.

---

> `Grep` -- {"pattern": "bbplatinum|ББ Платинум|bb-платин", "path": "D:\\Vault\\Vault-Knowledge\\05-Reglaments", "output_mode": "files_with_matches", "-i": true, "head_limit": 15}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\session_slot.py status 2>&1 | Select-Object -First 30", "description": "Show reusable session slot pool"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\session_slot.py --list 2>&1 | Select-Object -First 25", "description": "List reusable session slots"}

---

> `Grep` -- {"pattern": "bbplatinum.*(всегда|правило|hub|хаб)|хаб.*bbplatinum|этом компьютере.*bb", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "-i": true, "head_limit": 10}

---

> `Glob` -- {"pattern": "**/reglament-firefox-po-maksimumu*", "path": "D:\\Vault\\Vault-Knowledge"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-firefox-po-maksimumu-i-zamer.md", "limit": 60}

---

> `PowerShell` -- {"command": "Get-Content \"D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-firefox-po-maksimumu-i-zamer.md\" -Encoding UTF8 | Select-Object -Last 25", "description": "Read tail of firefox reglament for amendment format"}

---

> `PowerShell` -- {"command": "$f=\"D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-firefox-po-maksimumu-i-zamer.md\"; $add = @'\n\n## §Поправка 30.08.2026 — четвёртое подтверждение приказа + новый мотив: разделение личностей\n\nДословно (dev 30.08, голосом, в разборе «Chrome постоянно вылогинивае

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-hab-brauzernye-lichnosti-bb-i-roboty.md", "content": "---\ntitle: \"Регламент: браузерные личности хаба — оператор всегда под bbplatinum, роботы НЕ живут в его браузере\"\naliases: [\"браузерные личности хаба\", \"bb всегд

---

**Claude:**

Теперь память + строка в MEMORY.md INBOX.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\hub-browser-identities-bb-and-robots.md", "content": "---\nname: hub-browser-identities-bb-and-robots\ndescription: \"STANDING (dev 30.08 голосом): человеческий Chrome хаба = bbplatinum ВСЕГДА; роботы не дела

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\n- _(пусто — разнесено 29.08: 7 спиц дословно в хабы §3 — leads · tg-rails · te

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\n- _(пусто — разнесено 29.08: 7 спиц дословно в хабы §3 — leads · tg-rails · te

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\n- _(пусто — разнесено 29.08: 7 спиц дословно в хабы §3 — leads · tg-rails · te

---

**Claude:**

Поднимаю двух починщиков через переиспользование слотов (§9.2).

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\session_slot.py --claim \"fb-graph-token-rail\" 2>&1 | Select-Object -First 15; Write-Output \"===\"; python C:\\Users\\dev\\.claude\\scripts\\session_slot.py --claim \"robots-out-of-human-browser\" 2>&1 | Select-Object -First 15", "descripti

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__update_scheduled_task,mcp__scheduled-tasks__list_scheduled_tasks", "max_results": 2}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "auto-hub-260825-fleet-debt-drain", "description": "FB Graph API токен-рельса: роботы вон из браузерной сессии оператора (приказ 30.08)", "fireAt": "2026-08-30T13:40:00+01:00", "prompt": "Первым действием вызови mcp__ccd_session__set_session_title с заголовком «FB Graph API токен-рельса (при

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "auto-hub-260824-dr-runner-hiring", "description": "Роботы вон из браузера человека: миграция рутин в свои профили + карта разлогинов (приказ 30.08)", "fireAt": "2026-08-30T13:55:00+01:00", "prompt": "Первым действием вызови mcp__ccd_session__set_session_title с заголовком «Роботы вон из 

---

**Claude:**

Read-back (урок класса seed-premise/readback от сегодняшней утренней сессии): проверяю фактом, что приказы легли в слоты.

---

> `PowerShell` -- {"command": "foreach($t in 'auto-hub-260825-fleet-debt-drain','auto-hub-260824-dr-runner-hiring'){ $p=\"C:\\Users\\dev\\.claude\\scheduled-tasks\\$t\\SKILL.md\"; if(Test-Path $p){ $c=Get-Content $p -Raw -Encoding UTF8; $m1=$c -match 'set_session_title'; $m2=$c -match 'seed-stop-dup-block'; $m3=$c 

---

> `PowerShell` -- {"command": "Select-String -Path \"C:\\Users\\dev\\.claude\\scheduled-tasks\\auto-hub-260825-fleet-debt-drain\\SKILL.md\" -Pattern 'FB Graph API' -Encoding UTF8 | Select-Object -First 1; Select-String -Path \"C:\\Users\\dev\\.claude\\scheduled-tasks\\auto-hub-260824-dr-runner-hiring\\SKILL.md\" 

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\rule_home_guard.py reglament-hab-brauzernye-lichnosti-bb-i-roboty 2>&1 | Select-Object -First 15", "description": "Check rule homes and door coverage for new reglament"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "- [Личности браузеров хаба](hub-browser-identities-bb-and-robots.md) — ⭐30.08 Chrome человека=bb всегда, роботы не перелогинивают; FB токен-рельса ОК", "new_stri

---

> `Grep` -- {"pattern": "ШАГ 0|Шаг 0", "path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "output_mode": "content", "head_limit": 5}

---

> `Grep` -- {"pattern": "logout|чужой орг|аккаунт", "path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "output_mode": "content", "-n": true, "head_limit": 10}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "offset": 10, "limit": 30}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "old_string": "### 0. ГВАРД АККАУНТА + САМОЛЕЧЕНИЕ ВХОДА (не пропускать)\n`GET /api/organizations` → chat-org (caps содержит `chat`) обязан быть `s_be15d406` (a2).\nЕсли там чу

---

> `Grep` -- {"pattern": "claude\\.ai/logout", "path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "output_mode": "content", "-n": true}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "offset": 36, "limit": 35}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "limit": 36}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "old_string": "ШАГ 0 — ГВАРД АККАУНТА (КРИТИЧНО, не пропускать):\n1. Claude-in-Chrome: list_connected_browsers. Если ни одного браузера → НЕ делай вывод «нового нет». Пинг в Telegram чат 

---

> `PowerShell` -- {"command": "$led=\"C:\\Users\\dev\\.claude\\change_ledger\\HUB-01.jsonl\"; foreach($f in @('skills/claudeai-sync/SKILL.md','scheduled-tasks/claudeai-sync-daily/SKILL.md')){ $rec=@{ts=(Get-Date).ToUniversalTime().ToString('yyyy-MM-ddTHH:mm:ssZ'); file=$f; change='ШАГ 0 переписан по reglamen

---

> `PowerShell` -- {"command": "$led=\"C:\\Users\\dev\\.claude\\change_ledger\\HUB-01.jsonl\"; foreach($f in @('skills/claudeai-sync/SKILL.md','scheduled-tasks/claudeai-sync-daily/SKILL.md')){ $rec=@{ts=(Get-Date).ToUniversalTime().ToString('yyyy-MM-ddTHH:mm:ssZ'); file=$f; change='ШАГ 0 переписан по reglamen

---

**Claude:**

[⏰ воскресенье, день, 13:33, 30 августа 2026]

🎙 Майк: всё принял и уже поднял. Одна честная оговорка про Graph API ниже - прочитай её, она важная: API не умеет всё, что умеет браузер.

## Токен-рельса Graph API: как и когда

**Когда: уже.** Сессия-строитель «FB Graph API токен-рельса (приказ 30.08)» стартует сегодня в **13:40** (переиспользованный слот, видна в списке сессий). Вторая, «Роботы вон из браузера человека», стартует в **13:55**.

**Как (план сессии):**
1. Сначала честная карта по свежей документации Meta: что реально переносимо на токен. Оговорка: с 2018 года Graph API почти не управляет ЛИЧНЫМ профилем - постить на твою личную стену, лайкать и отвечать от твоего лица через API нельзя, это Meta закрыла всем. На токен уезжает: чтение, работа со Страницами (посты, комменты, лайки от имени Страницы), Messenger. Что не уедет - сессия предъявит списком с вариантами (вести с Страницы / снизить темп / принять перелогин), решишь ты.
2. Получение long-lived токена (60 дней) + бессрочных page-токенов, хранение в secrets store, сторож протухания, который кричит ЗА 7 дней до смерти токена, а не после.
3. Один шаг потребует твоих рук: первичная выдача токена = твой вход в developers.facebook.com. Сессия подготовит точный клик-путь и поднимет аск в 02 POLICE - пароль я не ввожу по канону.

## Правила записаны (без зарубок на носу)

- **«Клод на этом компе всегда под bbplatinum»**: новый регламент в Библии `reglament-hab-brauzernye-lichnosti-bb-i-roboty` + память + строка в MEMORY.md. Проверка домов правила прошла (guard зелёный).
- **«Firefox всегда, Chrome запасной»**: это правило уже жило в Библии с 04.08 (твой же приказ, трижды повторённый). Дубль не плодил - дописал туда Поправку 30.08 с новым мотивом: разделение личностей человек/робот.

## И главный улов по ходу: корень добит прямо сейчас

Проверяя двери правила, нашёл, что ночная рутина и скилл claudeai-sync **до сих пор несли инструкцию «сделай logout в живом Chrome»** - ту самую, что тебя вылогинивала. Вычистил оба файла: теперь роботу прямо запрещено трогать твой браузер, вход a2 только через выделенный профиль. Подписи правок в change_ledger.

Подсказка от планировщика: если будешь у компа в 13:40, нажми у задачи «Run now» - тогда разрешения на браузер/коннекторы запомнятся на задаче и будущие прогоны не встанут на апрувах.

🧒 Простыми словами: роботам выдали собственные ключи от собственных квартир, а из твоей квартиры их выселили и правило об этом повесили на стену. Для Фейсбука строим роботам служебный вход через API, но у этого входа есть ограничение: от твоего личного имени Фейсбук пускает только живого человека - что с этим делать, сессия принесёт тебе варианты.

[⏰ воскресенье, день, 13:34, 30 августа 2026]

---

**User:**

Я проверил бы, чтобы на чем флоте это работало, и потом сделал бы ретро. Короче. Отдельно все сидела на ग्राх API. Отдельно все сидела на graph API, не подключайся. Так, окей. Да, и все, все по максимуму, что может провести, перевести на graph API. Переводим и работаем. Да, я задаю где вопрос Facebook com. Делать девяносто шесть минут. Проверь еще, какие рутины и какие скилы несли в себе инструкции, сделала галд в аккаунту браузере. Посмотри, везде на всех машинах переучена этом компьютерной хабе. Что такое ереси больше никогда не было? Такой е

---

**Claude:**

[⏰ воскресенье, день, 14:41, 30 августа 2026]

Принял: (1) максимум на Graph API переводим и работаем, (2) свип по ВСЕМ машинам: какие ещё рутины и скиллы несут инструкцию «сделай logout в живом браузере», чтобы ереси не осталось нигде, (3) потом проверка на флоте и ретро. Начинаю со свипа на хабе.

---

> `Grep` -- {"pattern": "navigate.*logout|logout['\"`]?\\)|сделай logout|выйди из аккаунта|claude\\.ai/logout|/logout", "path": "C:\\Users\\dev\\.claude", "output_mode": "content", "-i": true, "-n": true, "glob": "**/*.{md,py,ps1,cmd,sh,json}", "head_limit": 40}

---

> `Grep` -- {"pattern": "navigate.*logout|claude\\.ai/logout|сделай logout|выйди из аккаунта", "path": "D:\\Vault\\_imports", "output_mode": "content", "-i": true, "-n": true, "glob": "**/*.{md,py,ps1,cmd,sh}", "head_limit": 30}

---

> `Grep` -- {"pattern": "claude\\.ai/logout", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "content", "-n": true, "head_limit": 15}

---

> `Grep` -- {"pattern": "claude\\.ai/logout", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "content", "-n": true, "head_limit": 15}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\claudeai-sync-needs-a2-account.md", "old_string": "**2026-07-30 — РАБОЧИЙ ВХОД БЕЗ РУК оператора (сделан, проверен, синк поехал).** Правильная лестница, когда a2 недоступен:", "new_string": "

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py --help 2>&1 | Select-Object -First 20", "description": "Check bus_send usage"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK [для КАЖДОГО узла, вкл. NODE-0X/NODE-0X/NODE-0X/Нора/Рита/Маяк]: СВИП ЕРЕСИ LOGOUT (приказ оператора 30.08, канон в волте reglament-hab-brauzernye-lichnosti-bb-i-roboty). Контекст: на хабе найден и добит корень 'Chrome п

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK: свип ереси logout на КАЖДОМ узле (NODE-0X, NODE-0X, NODE-0X, Нора, Рита, Маяк). Приказ оператора 30.08, канон в волте reglament-hab-brauzernye-lichnosti-bb-i-roboty. Контекст: на хабе найден и добит корень 'Chrome посто

---

**Claude:**

[⏰ воскресенье, день, 14:42, 30 августа 2026]

🎙 Майк: свип сделан, ересь на хабе выжжена, флоту разослан приказ выжечь у себя. Одну фразу из твоей голосовой я не разобрал - переспрошу внизу.

## Свип «кто ещё несёт инструкцию logout в живом браузере»

**Хаб (этот комп): чисто.** Живых инструкций `claude.ai/logout` осталось ноль. Сегодня выжжено три места: скилл `/claudeai-sync` (ШАГ 0 переписан), ночной рунбук `claudeai-sync-daily` (старый путь (а)-(д) удалён физически, не только «отменён поправкой»), и памятка-справка, где лестница 30.07 с logout лежала как «рабочий рецепт» - теперь она помечена запретом. Остались только упоминания в архивах транскриптов и истории браузера - это история, не инструкции. Кстати, история браузера дала ещё одну улику: заходы на `claude.ai/logout` ровно в 01:28 - время ночной рутины. Война задокументирована и там.

**Флот: приказ разослан по обеим рельсам** (шина + TG-03, доставка подтверждена). Каждый узел обязан: прогнать тот же grep у себя, переписать найденное по канону, отдельно ноуты - у них живёт fallback-копия ночной рутины 04:40 со старым ШАГом 0. Формат ответа: ACK + «чисто / найдено N, переписано» в 03. Проверю ответы по ритму синка; кто отмолчится - будет поимённо в парити-долге.

## Что уже сделали сессии-починщики (пока мы говорили)

Вторая сессия («Роботы вон из браузера») отработала в 14:1x: из живого Chrome уехали claudeai-sync (в выделенный профиль) и chatgpt-token-guard (в системный Firefox). В живом Chrome по канону остаются 11 скиллов (весь fb-лейн, x-лейн, luma) - в каждый вставлена строка «читаем и действуем, логины не трогаем». Замер показал масштаб: 4703 захода Chrome против 47 у Firefox за 14 дней, пики ночью - это роботы. Ровно этот перекос и будет резать Graph API-сессия: **всё, что переносимо на API - переводим и работаем**, твой приказ у неё в сиде.

Ретро сделаю в конце этой сессии, когда соберём ответы флота - как ты и сказал: сначала проверка, что работает везде, потом ретро.

**Переспрос одной фразы:** «я задаю вопрос facebook com, делать девяносто шесть минут» - не разобрал. Если это про developers.facebook.com: твоих рук там понадобится минут десять, сессия-строитель подготовит точный клик-путь и пришлёт аск в 02, когда всё будет готово к твоему одному входу. Если имел в виду другое - скажи голосом ещё раз, одной фразой.

🧒 Простыми словами: я прошёлся с металлоискателем по всем инструкциям роботов на этом компе - мин «выйди из аккаунта хозяина» больше нет. Остальным компьютерам разослал приказ пройтись с тем же металлоискателем у себя и отчитаться. А роботы тем временем уже переезжают из твоего браузера: кто в свой отдельный, кто на служебный API-вход.

[⏰ воскресенье, день, 14:44, 30 августа 2026]

---

**User:**

This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.

Summary:
1. Primary Request and Intent:
   dev (RU, voice-transcribed messages) on hub HUB-01:
   - Msg 1: "Chrome постоянно вылогинивает" — he keeps getting logged out of everything (Facebook re-login needed again after logging in 28-29.08, claude.ai, everything). Investigate and find the roots.
   - Msg 2 (after my diagnosis offering options): chose **(б) build FB Graph API token rail** so robots leave his browser session ("!!"); noted "куча других вещей вылогинивается"; ordered two rules recorded ("без зарубок на носу"): (R1) "Всегда работаем через Firefox. Firefox всегда. Chrome — запасной вариант" (Bible), (R2) "Я всегда работаю через аккаунт ББ Платинум. Клод на этом компьютере всегда залогинен/работает через bbplatinum"; repairs in separate sessions via reusable slots; "чини все корни".
   - Mid-turn: "(б) поднять токен-рельсу Graph API КАК И КОГДА СДЕЛАЕМ?"
   - Msg 3: verify fixes work fleet-wide, then do retro; move everything possible to Graph API ("всё по максимуму, что можно перевести на Graph API — переводим и работаем"); explicitly: "Проверь ещё, какие рутины и какие скиллы несли в себе инструкции сделать logout в аккаунте браузера. Посмотри везде на всех машинах, не только на этом компьютере-хабе. Чтобы такой ереси больше никогда не было." (Contains an unclear garbled fragment about developers.facebook.com / "96 минут" — not yet clarified.)

2. Key Technical Concepts:
   - Chrome cookie persistence: flushed in ~30s batches; kill/hard-close = crash exit (`exit_type: Crashed`), fresh login cookies lost (measured 19.08, documented in agent_chrome.sh).
   - "War for the browser": nightly claudeai-sync robot did `claude.ai/logout` → magic-link a2 login in dev's LIVE Chrome Default; dev (bb account) re-logged in daily → mutual logout war (3 dated cases 14.08/20.08/27.08; corroborated by Browser-History showing claude.ai/logout at 01:28 = routine slot).
   - Meta server-side session invalidation: FB checkpoint 19.08, login.php 23/25.08; session after manual login died ≤1-2 days with NO Chrome restart in between (oldest chrome.exe alive since 28.08 18:30, no reboot since 27.08) → client-side loss excluded, Meta risk engine reacting to fb-reply/fb-likes automation.
   - Graph API limits: personal-profile posting/liking/replying via API dead since 2018 (publish_actions removed); only reading, Pages, Messenger portable to tokens.
   - Dedicated robot browser profiles: `_chrome_profile_a2` + railc_login_a2.py + pull_rail_c.py --profile=a2 (rail C, headed Chromium, no Firefox cookie injection); magic-link fetched by Gmail MCP connector; "Continue with Google" popup invisible to extension (⛔); cookie-consent banner must be "Reject All"; a2 profile TTL can be <70 min.
   - Session slot reuse (§9.2): session_slot.py --claim → update_scheduled_task with new prompt/fireAt; seeds must start with set_session_title + carry stop-dup block pointer ($OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md); read-back verification of written prompts (seed-premise/readback class lesson from same morning).
   - Rule intake (§8.6): homes = Bible reglament + memory + MEMORY.md (≤150 char lines, memory_write_gate enforces) + skill door; rule_home_guard.py verification; CLAUDE.md edits left to nightly optimizer (§10.0).
   - Provenance (§4.9/§5.11): ~/.claude/scripts is gitignored → signatures go to ~/.claude/change_ledger/HUB-01.jsonl (JSON lines with ts/file/change/assisted_by/machine/account/operator).
   - bus_send.py dual-send (TG-03 + _machine-bus); messages must start "TASK:" with colon or inbox robots ignore them.
   - dead_claim_guard stop hook: availability claims require rail_sweep.py sweep of ALL surfaces; conclusions must be per-profile, not global.
   - maintenance_gate.py: maintenance scripts 1x/day, bypass with --force + stated reason.
   - Reply style rules: RU timestamp line at start AND end; 🎙 Майк micro-block; 🧒 ELI5 block; NO em/en dashes (use hyphens/words).

3. Files and Code Sections:
   - `C:\Users\dev\AppData\Local\Google\Chrome\User Data\Default\Preferences` (read): `exit_type: Crashed`; browser.clear_data had cookies:true/time_period:4 (saved dialog state, not clear-on-exit); no clear-on-exit content settings.
   - `C:\Users\dev\.claude\scripts\fix-chrome-bridge.ps1` (edited): replaced `Start-Sleep 4` before hard kill with:
     ```powershell
     # Chrome flushes cookies to disk in ~30s batches (замер 19.08, agent_chrome.sh) —
     # killing early = crash exit, свежие логин-куки теряются. Ждём до 45с, добиваем только тогда.
     $chrome | ForEach-Object { $_.CloseMainWindow() | Out-Null }
     $deadline = (Get-Date).AddSeconds(45)
     while ((Get-Process chrome -ErrorAction SilentlyContinue) -and ((Get-Date) -lt $deadline)) { Start-Sleep 3 }
     Get-Process chrome -ErrorAction SilentlyContinue | Stop-Process -Force -ErrorAction SilentlyContinue
     ```
   - `D:\Vault\Vault-Knowledge\00-System\Breakage-Journal.md` (edited): inserted dated line 2026-08-30 13:2x under "## Строки (append-only, новые сверху)" — combined analysis of both classes, closes 27.08 open question ("кто перекидывает на bb" = dev himself), records FB server-side kill proof, aggravator (daily reboots, dirty Chrome deaths), notes fix-chrome-bridge patched. (Note: never write this file via open('w') — prior 0-byte truncation incident.)
   - `D:\Vault\Vault-Knowledge\10-Tasks\task-2026-08-10-browser-rail-down-forever-fix.md` (read): P0 card with full browser-rail-down series, five facades, 5-why, browser_rail_watch.py, FB_USER_TOKEN empty since 11.07 (ask #c1b678cb).
   - `C:\Users\dev\.claude\projects\...\memory\claudeai-sync-needs-a2-account.md` (read + edited): key history; edit added before the 2026-07-30 ladder: "⛔⛔ ПОПРАВКА 30.08 (приказ оператора): лестница ниже ЗАПРЕЩЕНА в ЖИВОМ браузере человека — logout/смена аккаунта только в выделенном робо-профиле (`railc_login_a2.py` + `_chrome_profile_a2`); канон `reglament-hab-brauzernye-lichnosti-bb-i-roboty`..."
   - `D:\Vault\Vault-Knowledge\05-Resources\Protocols\reglament-hab-brauzernye-lichnosti-bb-i-roboty.md` (created): new Bible reglament — human Chrome Default hub = bbplatinum always; robots never logout/switch/inject in human browsers; a2 only in dedicated profiles; fleet-wide principle; doors = claudeai-sync-daily runbook, pull_rail_c guard, browser_rail_watch.py.
   - `D:\Vault\Vault-Knowledge\05-Resources\Protocols\reglament-firefox-po-maksimumu-i-zamer.md` (appended): §Поправка 30.08.2026 — 4th confirmation of Firefox-first, new motive = identity separation, link to sister reglament.
   - `C:\Users\dev\.claude\projects\...\memory\hub-browser-identities-bb-and-robots.md` (created; later extended on disk by the spawned audit session with 30.08 14:1x audit results: 2 routines moved out, 11 skills remain in live Chrome by canon with "логины НЕ трогаем" lines, chrome 4703 vs firefox 47 visits/14d).
   - `C:\Users\dev\.claude\projects\...\memory\MEMORY.md` (edited): INBOX line "- [Личности браузеров хаба](hub-browser-identities-bb-and-robots.md) — ⭐30.08 bb всегда; канон reglament-hab-brauzernye-lichnosti-bb-i-roboty" (≤150 chars after two gate rejections).
   - `C:\Users\dev\.claude\skills\claudeai-sync\SKILL.md` (edited): ШАГ 0 rewritten — live-Chrome logout forbidden, rail C/dedicated profile only.
   - `C:\Users\dev\.claude\scheduled-tasks\claudeai-sync-daily\SKILL.md` (edited): old ШАГ 0 (а)-(д) logout path DELETED, replaced with prohibition + pointer to header's ПОПРАВКА 30.08 rail-C procedure. (Later also touched by the audit session — description updated.)
   - `C:\Users\dev\.claude\change_ledger\HUB-01.jsonl` (appended 3 records): fix-chrome-bridge patch + both SKILL.md ШАГ 0 rewrites, each with assisted_by='Claude Code / claude-fable-5', machine='HUB-01', account='bb', operator='robot:hub-live-session'.
   - Scheduled tasks updated via mcp__scheduled-tasks__update_scheduled_task: `auto-hub-260825-fleet-debt-drain` → FB Graph API token-rail seed (fireAt 13:40); `auto-hub-260824-dr-runner-hiring` → robots-out-of-human-browser seed (fireAt 13:55). Read-back verified (set_session_title marker, stop-dup pointer, new descriptions present).
   - Scratchpad: cookie_audit.py (unused — Cookies DB copy failed).

4. Errors and fixes:
   - Cookies DB locked by Chrome; Copy-Item failed; esentutl /vss failed (0x80070005, needs admin) → pivoted to alternate discriminators (process start times, event log, journal evidence) instead of forcing admin/UAC.
   - Inline python -c quoting broke in PowerShell → wrote script file to scratchpad instead.
   - git commit in ~/.claude failed: scripts/ is gitignored → recorded provenance in change_ledger per §5.11.
   - Stop hook dead_claim_guard blocked my reply for an availability-style claim without sweeping all surfaces → ran rail_sweep.py claude_ai (3 surfaces) and issued per-profile clarification (war conclusion applies to Chrome Default only).
   - memory_write_gate blocked MEMORY.md line twice (196 then 158 chars > 150) → shortened to fit.
   - session_slot.py "status" arg invalid → used --list.
   - rule_home_guard blocked by maintenance_gate (2nd run/day) → re-ran with --force (stated reason: rule intake verification).
   - rule_home_guard initially red (no MEMORY.md/CLAUDE.md trace) → added reglament slug into MEMORY.md pointer line → green (CLAUDE.md left to nightly optimizer per §10.0).
   - bus_send.py refused broadcast: "TASK [..." without colon = robot-invisible → resent as "TASK: свип ереси logout..." → DUAL-SEND OK.
   - Found that scheduled-tasks/claudeai-sync-daily/SKILL.md still carried the old (а)-(д) logout recipe verbatim below the 30.08 header amendment (conflicting instructions) → excised it.

5. Problem Solving:
   Root-caused "Chrome logs me out of everything": (1) claude.ai = robot/human account war in shared Chrome Default (robot's nightly logout→a2 self-heal; fixed 30.08 night via dedicated profile; live instruction remnants purged by me from both claudeai-sync SKILL.md files); the 27.08 open question "who flips to bb" answered: dev himself. (2) Facebook = Meta server-side invalidation (risk engine vs automation on his personal account) — proven by session dying ≤1-2 days with no Chrome restart. (3) Aggravator = near-daily hub reboots + hard Chrome kills losing cookie batches (fix-chrome-bridge patched to 45s wait). Recorded rules in all homes, spawned two repair sessions, executed logout-heresy sweep on hub (clean except historical/quarantined), broadcast fleet-wide sweep task via dual-send bus (#logout-heresy-sweep).

6. All user messages:
   - Msg 1 (voice): "На этом компьютере... Мы постоянно вылогиниваете Chrome. Я только что недавно сходил в Facebook вчера или позавчера. И снова мне недавно надо заходить. Посмотри, в чем проблема, поищи какие-нибудь корни... Постоянно мне приходит заново залогиниваться в вообще в клоды, в Facebook, абсолютно во все."
   - Msg 2 (voice): "(б) поднять токен-рельсу Graph API, чтобы роботы не жили в твоей браузерной сессии!! Написано у меня ещё и куча других вещей вылогинивается... можно пишет правила Библи... Всегда работаем через лису, всегда работаем через Firefox. Firefox всегда. А Chrome используем как запасный вариант. Твои раскатанные слоты уже создал... Чинить это... пункт первый... Мы же делали уже это правило. Я всегда работаю через аккаунт Биби Платину. Клод на этом компьютере всегда запустится, включён за работу через Биби Платин. Всегда запиши я, пожалуйста, без зарубин на носу. Пожалуйста, сделай так, чини корни. Чни все корни, чини все корни."
   - Msg 3 (mid-turn): "Так,(б) поднять токен-рельсу Graph API КАК И КОГДА СДЕЛАЕМ?"
   - Msg 4 (voice): "Я проверил бы, чтобы на чем флоте это работало, и потом сделал бы ретро. Короче. Отдельно все сидела на graph API, не подключайся. Так, окей. Да, и все, все по максимуму, что может провести, перевести на graph API. Переводим и работаем. Да, я задаю где вопрос Facebook com. Делать девяносто шесть минут. Проверь еще, какие рутины и какие скилы несли в себе инструкции, сделала галд в аккаунту браузере. Посмотри, везде на всех машинах переучена этом компьютерной хабе. Что такое ереси больше никогда не было?"
   - Also a Stop-hook feedback block (system-injected, not dev) requiring rail_sweep before availability claims.

7. Pending Tasks:
   - Compose final reply to dev for Msg 4 (sweep results, fleet broadcast sent, Graph API "по максимуму" note, retro plan). Address the garbled "developers.facebook.com / 96 минут" fragment honestly (unclear, invite correction).
   - Fleet verification: collect ACKs/reports from peers on #logout-heresy-sweep (TG-03 / bus); ensure laptops' claudeai-sync-daily 04:40 fallback copies get rewritten.
   - "Всё по максимуму на Graph API" mandate: ensure the 13:40 FB-token session's scope covers maximal migration (its seed already orders the capability map + migration; dev reinforced maximalism after seed was written — may need scope top-up via SendMessage or in-card note).
   - Retro (/retro) after fleet verification — dev explicitly ordered this sequence.
   - Watch spawned sessions: FB Graph API token rail (fired 13:40) and robots-out-of-browser audit (fired 13:55, already produced its 14:1x audit; its remaining items: reboot-mitigation proposal to dev, Breakage-Journal line, /tt + retro).
   - FB personal-wall остаток: options list (Page vs tempo vs accept relogin) to be presented by the token session; dev's decision.

8. Current Work:
   Executing Msg 4's logout-heresy sweep: (a) hub grep of ~/.claude and _imports for `claude.ai/logout` / logout instructions — clean (only _scratch sync-conflict copies of dr-fanout skill and historical archives); (b) vault grep — only session transcripts + Browser-History (corroborating evidence: logout at 01:28 routine time, involuntary logout); (c) amended memory claudeai-sync-needs-a2-account.md with ⛔⛔ ПОПРАВКА 30.08 so the 30.07 logout ladder can't be read as a live recipe; (d) broadcast fleet sweep task via bus_send.py — first attempt refused (TASK without colon), second attempt succeeded: "DUAL-SEND -> syncthing:OK(broadcast) tg-03:OK", tag #logout-heresy-sweep, instructing every node to grep its ~/.claude, rewrite live logout instructions per reglament-hab-brauzernye-lichnosti-bb-i-roboty, fix laptop claudeai-sync-daily 04:40 fallback, and ACK+report to 03. The final text reply to dev was NOT yet written when the summary request arrived.

9. Optional Next Step:
   Write the final reply to dev (RU, timestamp at start/end, Майк + ELI5 blocks, no long dashes) reporting: hub sweep verdict ("живых инструкций logout на хабе не осталось; память-справка помечена запретом"), fleet broadcast sent and awaiting per-node ACKs in 03, Browser-History corroboration (01:28 logouts), confirmation that "всё по максимуму на Graph API" is inside the 13:40 session's mandate, retro planned after fleet verification per his order ("Я проверил бы, чтобы на всём флоте это работало, и потом сделал бы ретро"), and one clarifying line about the garbled "developers.facebook.com / 96 минут" fragment. Then, per his fleet-verification order, follow up later on #logout-heresy-sweep ACKs before running /retro.

If you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: C:\Users\dev\.claude\projects\P---WORKDIR-HUB\s_ba41ce90.jsonl
Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.

---

**User:**

<local-command-caveat>Caveat: The messages below were generated by the user while running local commands. DO NOT respond to these messages or otherwise consider them in your response unless the user explicitly asks you to.</local-command-caveat>

---

**User:**

<command-name>/compact</command-name>
            <command-message>compact</command-message>
            <command-args></command-args>

---

**User:**

<local-command-stdout>Compacted PreCompact [python "C:\Users\dev\.claude\hooks\compact_guard_pre.py"] completed successfully</local-command-stdout>

---

**User:**

Да, я про developers.facebook.com -  куда мне нажимать чтобы сделать токен?

---

**Claude:**

[⏰ воскресенье, день, 15:35, 30 августа 2026]

Сейчас дам точный клик-путь. Сначала гляну, что уже подготовила сессия-строитель токен-рельсы (она стартовала в 13:40) - чтобы не дать тебе устаревшую инструкцию.

---

> `Grep` -- {"pattern": "graph|FB_USER_TOKEN|developers\\.facebook", "path": "C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets", "output_mode": "files_with_matches", "-i": true}

---

> `Glob` -- {"pattern": "*fb*token*", "path": "D:\\Vault\\_imports"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env"}

---

> `Glob` -- {"pattern": "10-Tasks/*fb-graph*", "path": "D:\\Vault\\Vault-Knowledge"}

---

> `Bash` -- {"command": "ls -lt \"C:\\Users\\dev\\.claude\\scripts\" | head -15; echo ---; ls -lt \"D:\\Vault\\Vault-Knowledge\\10-Tasks\" | head -8", "description": "List recently modified scripts and task cards"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-07-11-fb-graph-token-enable.md"}

---

**Claude:**

Нашёл заготовку: приложение «dev Metrics Reader» было начато 11.07, но FB тогда запросил повторный пароль, и на этом всё встало. Всё остальное (скрипты, обменник токена, ночной сборщик) готово и ждёт ровно трёх значений. Вот твой клик-путь.

🎙 Майк: твоих рук тут минут на 7-10, дальше всё моё. Пароль вводишь только ты - мне его трогать запрещено.

## Куда нажимать на developers.facebook.com

**Шаг 1. Проверить/создать приложение (~3 мин)**
1. В своём Chrome открой **developers.facebook.com/apps** (ты уже залогинен в FB как оператор - этого хватит).
2. Если в списке уже есть **«dev Metrics Reader»** - открой его и переходи к шагу 2.
3. Если списка нет или пусто: зелёная кнопка **«Create App»** → на вопрос про use case выбери **«Other»** → тип **«None»** (или «Business», если None не предложат) → имя приложения: **dev Metrics Reader** → **Create app** → тут FB попросит **твой пароль** - введи. Это тот самый шаг, где всё застряло 11 июля.

**Шаг 2. Взять App ID и App Secret (~1 мин)**
1. В левом меню приложения: **Settings → Basic**.
2. Сверху две строки: **App ID** (видно сразу) и **App Secret** → кнопка **Show** (снова спросит пароль) → скопируй оба.

**Шаг 3. Сгенерировать токен (~3 мин)**
1. Открой **developers.facebook.com/tools/explorer** (Graph API Explorer).
2. Справа в выпадашке **Meta App** выбери **dev Metrics Reader**.
3. Ниже **User or Page** = **User Token**.
4. **Add a permission** → найди и добавь **user_posts**.
5. Кнопка **Generate Access Token** → выскочит окно FB «разрешить доступ» → **Continue/OK**.
6. Скопируй длинную строку токена из поля Access Token.

**Шаг 4. Отдай мне три строки** - прямо сюда в чат: App ID, App Secret, токен. Дальше сам: обменяю короткий токен на длинный (~60 дней), положу в `secrets\fb_graph.env`, прогоню `fb_posts_poll.py check` до AUTH OK и запущу залив метрик. Токен будет протухать раз в ~60 дней - поставлю сторожа, который заранее попросит тебя об одном таком же клике.

⚠️ Честная граница, чтобы не ждать чуда: этот токен даёт **чтение** твоей стены (посты, реакции, комменты - оживают метрики, книга, fb-watch). **Постить на личный профиль через API нельзя никому с 2018 года** - это ограничение Facebook, не наше. Постинг через API возможен только на Страницу; эту развилку разберём отдельно после того, как чтение поедет.

🧒 Простыми словами: FB выдаёт роботам служебный ключик от твоей стены, но только чтобы читать, не писать. Ключик выдают в специальном кабинете для разработчиков, и пароль там можешь ввести только ты. Ты нажмёшь шесть кнопок, скопируешь три строчки, а я из них сделаю рабочий ключ на два месяца и всё подключу.

[⏰ воскресенье, день, 15:37, 30 августа 2026]

---

**User:**

что выбираем!?

---

**Claude:**

[⏰ воскресенье, день, 16:13, 30 августа 2026]

Выбирай **Consumer** (нижний) → Next.

Причина: нужное нам разрешение `user_posts` (чтение твоей личной стены) относится к consumer-разрешениям Facebook Login. Business - это про Страницы, рекламу и WhatsApp, для чтения личного профиля он не нужен, а тип потом поменять нельзя.

Дальше на экране Details: имя **dev Metrics Reader**, контактный email оставь как есть → **Create app** → введёшь пароль.

[⏰ воскресенье, день, 16:14, 30 августа 2026]

---

**User:**

создал, вот тебе App ID и Secret Слушай, я залогинен сейчас в, в Лизе, Firefox. Открой мой экран, посмотри сам и возьми сам, пожалуйста, я по аудиии секрет. Это скин скриншот, нам виден. А этот синэп ID виден. Ад ID виден. Но секреты нигде не вижу, девизель. Подожди, возьми сам, пожалуйста, был браузер открыт. Браузер
App ID:
ired actions
Docs
Tools
Support
Search input

Facebook
Searchable selector for all apps

dev Metrics Reader

App ID:
App Mode: Development
Live
App type:Consumer

---

**Claude:**

[⏰ воскресенье, день, 16:18, 30 августа 2026]

Понял, App ID вижу: **1655895462767856**. Иду сам в твой браузер за секретом.

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers,mcp__claude-in-chrome__select_browser,mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__computer,mcp__claude-in-chrome__read_page,mcp__claude-in-chrome__javascript_tool,mcp__claude-in-chrome

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

> `AskUserQuestion` -- {"questions": [{"question": "К какому браузеру подключиться, чтобы забрать App Secret с developers.facebook.com?", "header": "Браузер", "multiSelect": false, "options": [{"label": "Browser 1, этот ПК (Recommended)", "description": "Windows, локальный - хаб HUB-01, где открыт твой developers.f

---

> `mcp__claude-in-chrome__select_browser` -- {"deviceId": "s_0ebdfa43"}

---

> `mcp__claude-in-chrome__tabs_context_mcp` -- {"createIfEmpty": true}

---

> `mcp__claude-in-chrome__navigate` -- {"tabId": id_230bc47f, "url": "https://developers.facebook.com/apps/1655895462767856/settings/basic/"}

---

> `mcp__claude-in-chrome__get_page_text` -- {"tabId": id_230bc47f}

---

> `ToolSearch` -- {"query": "+computer-use request_access screenshot click", "max_results": 8}

---

> `ToolSearch` -- {"query": "screen desktop control mouse keyboard window", "max_results": 10}

---

> `ToolSearch` -- {"query": "request_access clipboard access", "max_results": 5}

---

**Claude:**

Стоп, честный отчёт: до твоего Firefox я отсюда физически не достаю. Проверил обе руки: расширение Claude живёт только в Chrome (подключился - Chrome на хабе в FB не залогинен, кидает на логин), а инструмент управления экраном к этой сессии не подключён. Врать «сейчас возьму» не буду.

🎙 Майк: ты в одном клике от финиша, быстрее твоих 30 секунд тут ни одна моя рельса не сработает.

Сделай в своём Firefox, где открыт кабинет:

1. Слева в меню: **App settings → Basic**.
2. Вторая строка сверху: **App Secret** → кнопка **Show** (может снова спросить пароль - ты его только что вводил, скорее всего пропустит).
3. Скопируй секрет и кинь сюда в чат.

И сразу же, чтобы два раза не вставать, **токен** (это шаг 3 из моей инструкции выше):

4. Открой **developers.facebook.com/tools/explorer** → справа выпадашка Meta App = **dev Metrics Reader** → User Token → **Add a permission** → `user_posts` → **Generate Access Token** → в попапе Continue → скопируй длинную строку токена и тоже кинь сюда.

Как только пришлёшь секрет и токен - дальше всё сам: обменяю на 60-дневный, положу в store, прогоню проверку до AUTH OK.

🧒 Простыми словами: у меня есть руки только в Chrome, а твоя дверь открыта в Firefox. Ключик из этой двери можешь вынести только ты - две строчки скопировать. Дальше опять работаю я.

[⏰ воскресенье, день, 16:21, 30 августа 2026]

---

**User:**

1655895462767856 
a8e0c76ebe760a316951dd20f3bb5616 Ну, кстати, ты же как-то с, типа, с Firefox работаешь. Ты можешь делать, могут, могут делать скриншот, ты мог бы взять, захватить моё управление экраном и открыть Firefox, нажать кнопочки и получить доступ. Для чего? Вот тебе, что ты просил.

---

**Claude:**

[⏰ воскресенье, день, 16:52, 30 августа 2026]

Принял, кладу в store. Про захват экрана - сейчас ещё раз проверю, подключён ли этот инструмент к текущей сессии.

---

> `ToolSearch` -- {"query": "select:mcp__computer-use__request_access,mcp__computer-use__screenshot,mcp__computer-use__computer", "max_results": 5}

---

> `Bash` -- {"command": "cat > \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env\" << 'EOF'\n# Facebook Graph API (dev-mode app \"dev Metrics Reader\") - READ-ONLY metrics личной стены\n# Потребитель: C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py (check | posts | metrics)\n# Как получить: d

---

**Claude:**

Секрет и App ID легли в store (`secrets\fb_graph.env`), это забрал.

Про захват экрана - двойной честный ответ:
1. **Технически**: инструмент экрана к этой сессии не подключён (проверил дважды - его тут просто нет в наборе). Это моя рельса на будущее, починю отдельно.
2. **По делу - и это важнее**: даже с руками на экране я бы НЕ жал кнопки в твоём живом Facebook. Мы сегодня весь день чиним ровно то, что Meta серверно убивает твою сессию за запах автоматизации. Робот, кликающий OAuth-диалог в твоём личном FB - это снова тот же грех. Кнопку разрешения в твоём FB должна нажать твоя рука.

Остались ровно **4 клика** в твоём Firefox:

1. Открой **developers.facebook.com/tools/explorer**
2. Справа: **Meta App** = dev Metrics Reader · ниже **User Token**
3. **Add a permission** → вбей `user_posts` → выбери
4. **Generate Access Token** → в попапе Continue → скопируй длинную строку и кинь сюда

Дальше без тебя: обменяю на 60-дневный, добью env, прогоню `fb_posts_poll.py check` до AUTH OK и залью метрики.

🧒 Простыми словами: два ключика из трёх уже у меня в сейфе. Остался последний - разрешение «можно читать стену». Его Facebook выдаёт только по клику живого хозяина, и это нам на руку: меньше запаха робота - дольше живёт твой вход.

[⏰ воскресенье, день, 16:54, 30 августа 2026]

---

**User:**

правильно или НЕТ?

---

**Claude:**

[⏰ воскресенье, день, 17:10, 30 августа 2026]

**Правильно, всё на месте**: приложение dev Metrics Reader ✓, разрешение `user_posts` добавлено ✓ (плюс `public_profile` - это норм, оно всегда там).

Осталось: жми синюю кнопку **Generate Access Token** → в выскочившем окне Facebook нажми **Continue** (или «Продолжить как оператор») → после этого верхнее поле **Access Token** заполнится длинной строкой → нажми иконку копирования справа от поля и кинь строку сюда.

[⏰ воскресенье, день, 17:10, 30 августа 2026]

---

**User:**

Может быть, мы сделаем больше permission для нашего токена? Давай побольше сделаем, чтобы меньше это я спрашивал в будущем.

---

**Claude:**

[⏰ воскресенье, день, 17:14, 30 августа 2026]

Дельно. В dev-режиме твоё приложение может выдать себе почти любые разрешения без проверки Meta - они работают для тебя-владельца. Добавь через **Add a Permission** вот этот набор (каждое ищи по имени и выбирай):

**Твой профиль (чтение):**
- `user_posts` - уже есть
- `user_photos`
- `user_videos`
- `user_likes`
- `user_events`

**Страницы - задел на будущий API-постинг (главная ценность):**
- `pages_show_list`
- `pages_read_engagement`
- `pages_read_user_content`
- `pages_manage_posts`
- `pages_manage_engagement`
- `pages_manage_metadata`
- `pages_messaging`
- `read_insights`

**Instagram (если когда-нибудь привяжем к Странице):**
- `instagram_basic`
- `instagram_content_publish`
- `instagram_manage_insights`

Чего в списке НЕТ и не ищи: постинг в личный профиль и в группы - Meta их удалила из API совсем, разрешений таких больше не существует. И `user_friends` не бери - список друзей API всё равно отдаёт пустым, только лишний запах.

Добавил все → **Generate Access Token** → Continue в попапе (там будет длинный список галочек - жми ОК на всё) → скопируй токен и кинь сюда.

🧒 Простыми словами: мы просим у Facebook связку ключей сразу от всех дверей, которые вообще открываются, чтобы потом не ходить к тебе за каждой дверью отдельно. Двери «постить на личную стену» у Facebook нет ни за какие ключи, а вот от Страниц - полный комплект берём.

[⏰ воскресенье, день, 17:15, 30 августа 2026]

---

**User:**

EAAXiBzTX7PABSc9bY2clIDHx837jO3SZAk5MOEdoA3qMA1Ndi302AVtyMnXDVnYfoooodyW6HLyuT3MGlaYJk1ZBszETpQasIz3cwmGWB5XJfyiwX8tGo0R9uB8DmxKNqmKazg3Y27F1e7eMqcFZAOTt4FWYMdj46KeSTVTNZC20YE8z8iZBeXwzvcIM270ZAyZA6TNBSPyKBxXPiMorXZBirTojRKWJXkSZC7o3arnZCfurZCN3ZC2smHWxZAPPWwCJNfko0FZChWZAQHKzZAZBaTRJuYzTLKz3X2kl74S87O6SQTH1fV3L3ZAw7Wvw4rMjoKcwd4BRTxx36ojVvJX52a

---

**Claude:**

[⏰ воскресенье, день, 17:16, 30 августа 2026]

Токен получил. Меняю на 60-дневный и проверяю, что он реально открывает.

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\" && cat > fb_exchange.py << 'EOF'\nimport json, urllib.request, urllib.parse\nAPP_ID=\"1655895462767856\"\nAPP_SECRET=\"REDACTED"

---

> `Bash` -- {"command": "TOK=$(cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\fb_long_token.txt\")\ncat > \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env\" << EOF\n# Facebook Graph API (dev-mode app \"dev Metr

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py\" check 2>&1 | tail -5", "description": "Verify FB Graph rail auth"}

---

> `Bash` -- {"command": "ls -la \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\"; grep -o \"^FB_APP_ID=.*\" \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\"; grep -c \"FB_USER_TOKEN=EAA\" \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\" || true", "description": "Inspect which creds file the poller u

---

> `Bash` -- {"command": "a=$(grep \"^FB_USER_TOKEN=\" \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\" | cut -c15-40); b=$(grep \"^FB_USER_TOKEN=\" \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env\" | cut -c15-40); echo \"claude-secrets: $a\"; echo \"NODE-0X-secrets:   $b\"; grep -l \"2026-08-30\"

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py\" metrics 2>&1 | tail -8", "description": "Pull real wall posts metrics via Graph API", "timeout": 120000}

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\" && cat > fb_probe.py << 'EOF'\nimport json, urllib.request\nTOK=open(\"fb_long_token.txt\").read().strip()\ndef get(path):\n    url=f\"https://graph.face

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\" && cat > fb_probe2.py << 'EOF'\nimport json, urllib.request\nTOK=open(\"fb_long_token.txt\").read().strip()\nq=\"me?fields=posts.limit(3){id,created_time

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\" && cat > fb_exchange2.py << 'EOF'\nimport json, urllib.request\nAPP_ID=\"1655895462767856\"; APP_SECRET=\"REDACTED"\nSHORT=\"EAA

---

> `Bash` -- {"command": "TOK=$(cat \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\fb_long_token2.txt\")\nfor f in \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env\" \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\

---

> `Grep` -- {"pattern": "me/posts|me/feed|posts\\?|def fetch|GRAPH|graph\\.facebook", "path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "output_mode": "content", "-n": true}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "offset": 100, "limit": 100}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "offset": 40, "limit": 60}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "old_string": "def cmd_check():", "new_string": "def _me_posts(requests, tok, fields, limit, timeout=60):\n    \"\"\"Список постов стены через field-expansion: me?fields=posts.limit(N){...}.\n    Прямые /me/p

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "old_string": "    try:\n        r = requests.get(GRAPH + \"/me/posts\", params={\n            \"fields\": \"id,message,permalink_url,created_time\",\n            \"limit\": limit, \"access_token\": tok}, tim

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "old_string": "        me = requests.get(GRAPH + \"/me\", params={\"fields\": \"id,name\", \"access_token\": tok},\n                          timeout=30)\n        r = requests.get(GRAPH + \"/me/posts\", param

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py\" check 2>&1 | tail -2 && python \"C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py\" metrics 2>&1 | head -30", "description": "Re-run check and metrics after patch", "timeout": 120000}

---

**Claude:**

Метрики поехали, но комменты приходят пустыми при счётчике 4 - проверяю, отдаёт ли их отдельный эндпоинт.

---

> `Bash` -- {"command": "cd \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\" && cat > fb_probe3.py << 'EOF'\nimport json, urllib.request\nTOK=open(\"fb_long_token2.txt\").read().strip()\npid=\"28812850911655795_28810615281879358\"

---

> `Bash` -- {"command": "grep -n \"ingest-fb-graph\" \"D:\\Vault\\_imports\\pub_metrics.py\" 2>/dev/null | head -3 || grep -rn \"ingest-fb-graph\" \"C:\\Users\\dev\\.claude\\scripts\" --include=\"*.py\" -l | head -3", "description": "Locate pub_metrics ingest engine"}

---

> `Grep` -- {"pattern": "ingest-fb-graph|ingest_fb_graph", "path": "D:\\Vault\\_imports", "output_mode": "files_with_matches", "head_limit": 5}

---

> `Grep` -- {"pattern": "ingest-fb-graph|ingest_fb_graph", "path": "C:\\Users\\dev\\.claude\\scripts", "output_mode": "files_with_matches", "head_limit": 5}

---

> `Bash` -- {"command": "grep -n -A5 \"ingest-fb-graph\" \"D:\\Vault\\_imports\\content-factory\\registry\\pub_metrics.py\" | head -20", "description": "See ingest-fb-graph CLI contract"}

---

> `Bash` -- {"command": "S=\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\"\npython \"C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py\" metrics --limit 50 --out \"$S\\fb_metrics.json\" 2>&1 | tail -1\npython \"D:\\Vault\\_

---

> `Bash` -- {"command": "head -30 \"C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py\" | grep -E '\"\"\"|^#|def ' | head -12; echo ---; grep -n \"fb\" \"C:\\Users\\dev\\.claude\\scripts\\collect_pub_metrics.cmd\" 2>/dev/null | head -5", "description": "Check parallel session's fb_token_rail and nightly FB

---

> `Bash` -- {"command": "sed -n 3,40p \"C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py\"; echo ===; ls \"C:\\Users\\dev\\.claude\\scripts\" | grep -i \"collect_pub\\|pub_metrics\" ", "description": "Read fb_token_rail docstring and find nightly collector"}

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py\" status 2>&1 | tail -6", "description": "Check token rail status and marker"}

---

> `Bash` -- {"command": "grep -c \"FB_RAIL_ENABLED_AT\" \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\" || python \"C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py\" install --field FB_RAIL_ENABLED_AT --value 2026-08-30 2>&1 | tail -2", "description": "Ensure rail-enabled marker present"}

---

> `Bash` -- {"command": "echo \"2026-08-30\" | python \"C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py\" install --field FB_RAIL_ENABLED_AT 2>&1 | tail -3; python \"C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py\" status 2>&1 | tail -2", "description": "Install rail-enabled marker via stdin"}

---

> `Bash` -- {"command": "for f in \"C:\\Users\\dev\\.claude\\secrets\\fb_graph.env\" \"E:\\!CLAUDE-HUBPC-June26\\secrets\\fb_graph.env\" \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env\" \"C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\secrets\\fb_graph.env\"; do echo \"$f: $(grep '^FB_USER_TOKEN=' \"$f

---

**Claude:**

Все 4 копии store держат один токен, сторож видит рельсу OK (59 дней). Прогоняю тест рельсы и оформляю паспорта.

---

> `Bash` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\_test_fb_token_rail.py\" 2>&1 | tail -4", "description": "Run token rail regression test", "timeout": 120000}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py", "old_string": "\"\"\"fb_posts_poll.py - read dev's own recent FB posts via Graph API /me/posts (READ-ONLY).", "new_string": "\"\"\"fb_posts_poll.py - read dev's own recent FB posts via Graph API (READ-ONL

---

> `Bash` -- {"command": "python - << 'EOF'\nimport json, datetime\nrec = {\n \"ts\": datetime.datetime.now().isoformat(timespec=\"seconds\"),\n \"file\": r\"C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py\",\n \"change\": \"posts/metrics переведены с /me/posts на field-expansion me?fields=posts{...} (хелпе

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-07-11-fb-graph-token-enable.md", "old_string": "state: someday", "new_string": "state: done"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-07-11-fb-graph-token-enable.md", "old_string": "## Outcome", "new_string": "## Outcome\n2026-08-30 17:3x — ЗАКРЫТА, рельса живая насквозь. оператор создал app «dev Metrics Reader» (Consumer, ID 1655895462767856), 

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\fb-personal-profile-api-limits.md"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\fb-personal-profile-api-limits.md", "old_string": "- ✅ **Чтение своей стены** — `user_posts`, `GET /me/posts` отдаёт id · message · created_time · permalink_url. App Review не нужен, если 

---

> `Bash` -- {"command": "rg -l \"ingest-fb-graph|fb_posts_poll\" \"D:\\Vault\\_imports\\content-factory\" --glob \"*.cmd\" --glob \"*.py\" 2>/dev/null | head -5; ls \"D:\\Vault\\_imports\\content-factory\\registry\" | grep -i collect", "description": "Find nightly metrics collector FB step"}

---

> `Bash` -- {"command": "grep -n -B2 -A4 \"fb_posts_poll\" \"D:\\Vault\\_imports\\content-factory\\registry\\collect_pub_metrics.cmd\"", "description": "Verify FB step in nightly collector"}

---

**Claude:**

[⏰ воскресенье, день, 17:36, 30 августа 2026]

🎙 Майк: рельса, которая 50 дней лежала в чертежах, сегодня поехала насквозь - от твоих шести кликов до 50 постов с метриками в реестре. Вопрос тебе один, на подумать: заводим ли когда-нибудь Страницу FB - только она откроет API-постинг.

## ✅ FB Graph API - живая, от ключей до метрик

**Что проехало сегодня:**
- Приложение «dev Metrics Reader» создано, App ID + Secret + токен в store (все 4 копии `fb_graph.env` одинаковые).
- Второй токен, который ты перегенерировал - принят: в нём **весь пользовательский набор** (посты, фото, видео, лайки, ивенты, локации, друзья...). Живёт до **29 октября**, сторож `oauth_probe` закричит за 14 дней до смерти - тогда с тебя снова один клик Generate.
- По пути поймал и починил граблю: Facebook закрыл старый эндпоинт чтения стены для профилей в professional-режиме («New Pages Experience Is Not Supported»). Нашёл рабочий обход через расширение полей, зашил в читалку [fb_posts_poll.py](C:\Users\dev\.claude\scripts\fb_posts_poll.py) классом, а не заплаткой.
- **Первый залив сделан: 50 постов, 50 снапшотов метрик** (реакции, шеры, счётчики комментов) в реестр публикаций. Ночной сборщик уже содержит FB-шаг - дальше метрики будут капать сами, 0 токенов LLM, браузер не нужен.
- Тест рельсы GREEN, паспорт правки в change_ledger, карточка задачи от 11 июля закрыта.

**Две честные границы платформы** (не наши недоделки):
1. Тексты чужих комментов API не отдаёт - только их количество. Приватность Meta: видны комменты лишь тех, кто сам авторизовал приложение.
2. Постинг/комменты/лайки/Messenger от личного профиля через API невозможны с 2018 года. Эти роботы остаются браузерными - но теперь они в твоём браузере только **читают и жмут**, а не логинятся-разлогиниваются. Единственный путь увести и их с браузера - завести Страницу: там API умеет всё, и токен бессрочный.

🧒 Простыми словами: раньше робот ходил читать твою стену через твой браузер, и Facebook злился и выкидывал тебя. Теперь у робота свой служебный пропуск на два месяца - он ходит через чёрный ход для программ, твой браузер не трогает. Сегодня он этим пропуском уже принёс 50 твоих постов со всеми лайками. А писать на твою личную стену через чёрный ход Facebook не разрешает никому - для этого нужна «Страница», это отдельный разговор.

[⏰ воскресенье, день, 17:37, 30 августа 2026]

---

**User:**

На этом компьютере, на этом компьютере мекать аномалии. Мы постоянно вылогиниваете Chrome. Я только что недавно сходил в Facebook вчера или позавчера. И снова мне недавно надо заходить. Посмотри, в чем проблема, поищи какие-нибудь корни, потому что это просто ужасно. Постоянно мне приходит заново залогиниваться в вообще в клоды, в Facebook, абсолютно во все. То, что такой-то треш какой-то происходит.

---

**Claude:**

[⏰ воскресенье, день, 13:05, 30 августа 2026]

Using superpowers:systematic-debugging to investigate — это баг-расследование, а не правка.

---

> `Skill` -- {"skill": "superpowers:systematic-debugging", "args": "Chrome на хабе HUB-01 постоянно вылогинивает из всех сайтов (Facebook, claude.ai и т.д.) — найти корень"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\plugins\cache\superpowers-marketplace\superpowers\6.2.0\skills\systematic-debugging

# Systematic Debugging

## Overview

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

**Violating the letter of this process is violating the spirit of debugging.**

## The Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

If you haven't completed Phase 1, you cannot propose fixes.

## When to Use

Use for ANY technical issue:
- Test failures
- Bugs in production
- Unexpected behavior
- Performance problems
- Build failures
- Integration issues

**Use this ESPECIALLY when:**
- Under time pressure (emergencies make guessing tempting)
- "Just one quick fix" seems obvious
- You've already tried multiple fixes
- Previous fix didn't work
- You don't fully understand the issue

**Don't skip when:**
- Issue seems simple (simple bugs have root causes too)
- You're in a hurry (rushing guarantees rework)
- Manager wants it fixed NOW (systematic is faster than thrashing)

## The Four Phases

You MUST complete each phase before proceeding to the next.

### Phase 1: Root Cause Investigation

**BEFORE attempting ANY fix:**

1. **Read Error Messages Carefully**
   - Don't skip past errors or warnings
   - They often contain the exact solution
   - Read stack traces completely
   - Note line numbers, file paths, error codes

2. **Reproduce Consistently**
   - Can you trigger it reliably?
   - What are the exact steps?
   - Does it happen every time?
   - If not reproducible → gather more data, don't guess

3. **Check Recent Changes**
   - What changed that could cause this?
   - Git diff, recent commits
   - New dependencies, config changes
   - Environmental differences

4. **Gather Evidence in Multi-Component Systems**

   **WHEN system has multiple components (CI → build → signing, API → service → database):**

   **BEFORE proposing fixes, add diagnostic instrumentation:**
   ```
   For EACH component boundary:
     - Log what data enters component
     - Log what data exits component
     - Verify environment/config propagation
     - Check state at each layer

   Run once to gather evidence showing WHERE it breaks
   THEN analyze evidence to identify failing component
   THEN investigate that specific component
   ```

   **Example (multi-layer system):**
   ```bash
   # Layer 1: Workflow
   echo "=== Secrets available in workflow: ==="
   echo "IDENTITY: ${IDENTITY:+SET}${IDENTITY:-UNSET}"

   # Layer 2: Build script
   echo "=== Env vars in build script: ==="
   env | grep IDENTITY || echo "IDENTITY not in environment"

   # Layer 3: Signing script
   echo "=== Keychain state: ==="
   security list-keychains
   security find-identity -v

   # Layer 4: Actual signing
   codesign --sign "$IDENTITY" --verbose=4 "$APP"
   ```

   **This reveals:** Which layer fails (secrets → workflow ✓, workflow → build ✗)

5. **Trace Data Flow**

   **WHEN error is deep in call stack:**

   See `root-cause-tracing.md` in this directory for the complete backward tracing technique.

   **Quick version:**
   - Where does bad value originate?
   - What called this with bad value?
   - Keep tracing up until you find the source
   - Fix at source, not at symptom

### Phase 2: Pattern Analysis

**Find the pattern before fixing:**

1. **Find Working Examples**
   - Locate similar working code in same codebase
   - What works that's similar to what's broken?

2. **Compare Against References**
   - If implementing pattern, read reference implementation COMPLETELY
   - Don't skim - read every line
   - Understand the pattern fully before applying

3. **Identify Differences**
   - What's different between working and broken?
   - List every difference, however small
   - Don't assume "that can't matter"

4. **Understand Dependencies**
   - What other components does this need?
   - What settings, config, environment?
   - What assumptions does it make?

### Phase 3: Hypothesis and Testing

**Scientific method:**

1. **Form Single Hypothesis**
   - State clearly: "I think X is the root cause because Y"
   - Write it down
   - Be specific, not vague

2. **Test Minimally**
   - Make the SMALLEST possible change to test hypothesis
   - One variable at a time
   - Don't fix multiple things at once

3. **Verify Before Continuing**
   - Did it work? Yes → Phase 4
   - Didn't work? Form NEW hypothesis
   - DON'T add more fixes on top

4. **When You Don't Know**
   - Say "I don't understand X"
   - Don't pretend to know
   - Ask for help
   - Research more

### Phase 4: Implementation

**Fix the root cause, not the symptom:**

1. **Create Failing Test Case**
   - Simplest possible reproduction
   - Automated test if possible
   - One-off test script if no framework
   - MUST have before fixing
   - Use the `superpowers:test-driven-development` skill for writing proper failing tests

2. **Implement Single Fix**
   - Address the root cause identified
   - ONE change at a time
   - No "while I'm here" improvements
   - No bundled refactoring

3. **Verify Fix**
   - Test passes now?
   - No other tests broken?
   - Issue actually resolved?
   - Use the `superpowers:verification-before-completion` skill before claiming success

4. **If Fix Doesn't Work**
   - STOP
   - Count: How many fixes have you tried?
   - If < 3: Return to Phase 1, re-analyze with new information
   - **If ≥ 3: STOP and question the architecture (step 5 below)**
   - DON'T attempt Fix #4 without architectural discussion

5. **If 3+ Fixes Failed: Question Architecture**

   **Pattern indicating architectural problem:**
   - Each fix reveals new shared state/coupling/problem in different place
   - Fixes require "massive refactoring" to implement
   - Each fix creates new symptoms elsewhere

   **STOP and question fundamentals:**
   - Is this pattern fundamentally sound?
   - Are we "sticking with it through sheer inertia"?
   - Should we refactor architecture vs. continue fixing symptoms?

   **Discuss with your human partner before attempting more fixes**

   This is NOT a failed hypothesis - this is a wrong architecture.

## Red Flags - STOP and Follow Process

If you catch yourself thinking:
- "Quick fix for now, investigate later"
- "Just try changing X and see if it works"
- "Add multiple changes, run tests"
- "Skip the test, I'll manually verify"
- "It's probably X, let me fix that"
- "I don't fully understand but this might work"
- "Pattern says X but I'll adapt it differently"
- "Here are the main problems: [lists fixes without investigation]"
- Proposing solutions before tracing data flow
- **"One more fix attempt" (when already tried 2+)**
- **Each fix reveals new problem in different place**

**ALL of these mean: STOP. Return to Phase 1.**

**If 3+ fixes failed:** Question the architecture (see Phase 4.5)

## your human partner's Signals You're Doing It Wrong

**Watch for these redirections:**
- "Is that not happening?" - You assumed without verifying
- "Will it show us...?" - You should have added evidence gathering
- "Stop guessing" - You're proposing fixes without understanding
- "Ultra-think this" - Question fundamentals, not just symptoms
- "We're stuck?" (frustrated) - Your approach isn't working

**When you see these:** STOP. Return to Phase 1.

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Issue is simple, don't need process" | Simple issues have root causes too. Process is fast for simple bugs. |
| "Emergency, no time for process" | Systematic debugging is FASTER than guess-and-check thrashing. |
| "Just try this first, then investigate" | First fix sets the pattern. Do it right from the start. |
| "I'll write test after confirming fix works" | Untested fixes don't stick. Test first proves it. |
| "Multiple fixes at once saves time" | Can't isolate what worked. Causes new bugs. |
| "Reference too long, I'll adapt the pattern" | Partial understanding guarantees bugs. Read it completely. |
| "I see the problem, let me fix it" | Seeing symptoms ≠ understanding root cause. |
| "One more fix attempt" (after 2+ failures) | 3+ failures = architectural problem. Question pattern, don't fix again. |

## Quick Reference

| Phase | Key Activities | Success Criteria |
|-------|---------------|------------------|
| **1. Root Cause** | Read errors, reproduce, check changes, gather evidence | Understand WHAT and WHY |
| **2. Pattern** | Find working examples, compare | Identify differences |
| **3. Hypothesis** | Form theory, test minimally | Confirmed or new hypothesis |
| **4. Implementation** | Create test, fix, verify | Bug resolved, tests pass |

## When Process Reveals "No Root Cause"

If systematic investigation reveals issue is truly environmental, timing-dependent, or external:

1. You've completed the process
2. Document what you investigated
3. Implement appropriate handling (retry, timeout, error message)
4. Add monitoring/logging for future investigation

**But:** 95% of "no root cause" cases are incomplete investigation.

## Supporting Techniques

These techniques are part of systematic debugging and available in this directory:

- **`root-cause-tracing.md`** - Trace bugs backward through call stack to find original trigger
- **`defense-in-depth.md`** - Add validation at multiple layers after finding root cause
- **`condition-based-waiting.md`** - Replace arbitrary timeouts with condition polling


ARGUMENTS: Chrome на хабе HUB-01 постоянно вылогинивает из всех сайтов (Facebook, claude.ai и т.д.) — найти корень

---

> `PowerShell` -- {"command": "$ud = \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\"; Get-ChildItem $ud -Directory | Where-Object {$_.Name -match 'Default|Profile'} | Select-Object Name, LastWriteTime; Write-Output \"---LocalState---\"; (Get-Item \"$ud\\Local State\").LastWriteTime", "description": "L

---

> `Grep` -- {"pattern": "taskkill.*chrome|kill.*chrome|Stop-Process.*chrome|remote-debugging-port|user-data-dir", "path": "C:\\Users\\dev\\.claude\\scripts", "output_mode": "content", "-i": true, "head_limit": 60}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\fix-chrome-bridge.ps1"}

---

> `PowerShell` -- {"command": "$prefs = Get-Content \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Preferences\" -Raw | ConvertFrom-Json; Write-Output \"exit_type: $($prefs.profile.exit_type)\"; Write-Output \"exited_cleanly: $($prefs.profile.exited_cleanly)\"; $prefs.profile.content_settings

---

> `PowerShell` -- {"command": "$c = Get-Item \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\Cookies\"; Write-Output \"Cookies DB: created $($c.CreationTime) modified $($c.LastWriteTime) size $($c.Length)\"; Write-Output \"---scheduled tasks mentioning chrome/bridge---\"; Get-Schedule

---

> `Grep` -- {"pattern": "fix-chrome-bridge", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches", "head_limit": 30}

---

> `PowerShell` -- {"command": "$ls = Get-Item \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Local State\"; Write-Output \"Local State: created $($ls.CreationTime) modified $($ls.LastWriteTime)\"; $j = Get-Content $ls.FullName -Raw | ConvertFrom-Json; $st = $j.user_experience_metrics.stability; Write-

---

> `Grep` -- {"pattern": "taskkill.*chrome|Stop-Process.*chrome|kill.*chrome\\.exe", "path": "D:\\Vault\\_imports", "output_mode": "content", "-i": true, "head_limit": 30}

---

> `Grep` -- {"pattern": "вылогин|разлогин|relogin|logged out|logout|перелогин", "path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "output_mode": "content", "-i": true}

---

> `Grep` -- {"pattern": "вылогин|разлогин|перелогин|relogin|куки слет|cookie.*(слет|lost|wipe)", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "content", "-i": true, "head_limit": 40}

---

> `PowerShell` -- {"command": "Write-Output \"=== System restarts/shutdowns last 14 days ===\"; Get-WinEvent -FilterHashtable @{LogName='System'; Id=41,1074,6008; StartTime=(Get-Date).AddDays(-14)} -ErrorAction SilentlyContinue | Select-Object TimeCreated, Id, @{n='Info';e={($_.Message -split \"`n\")[0]}} | Format-Ta

---

> `PowerShell` -- {"command": "Write-Output \"=== chrome.exe app crashes/hangs last 14d ===\"; Get-WinEvent -FilterHashtable @{LogName='Application'; Id=1000,1002; StartTime=(Get-Date).AddDays(-14)} -ErrorAction SilentlyContinue | Where-Object {$_.Message -match 'chrome'} | Select-Object TimeCreated, Id | Format-Tabl

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\claudeai-sync-needs-a2-account.md"}

---

> `PowerShell` -- {"command": "$p = Get-Process chrome | Sort-Object StartTime | Select-Object -First 1; Write-Output \"Oldest chrome.exe start: $($p.StartTime)\"; Write-Output \"chrome count: $((Get-Process chrome).Count)\"; Write-Output \"=== profiles in Local State ===\"; $j = Get-Content \"C:\\Users\\dev\\AppDa

---

> `PowerShell` -- {"command": "$src=\"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\Cookies\"; $dst=\"$env:LOCALAPPDATA\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\cookies_copy.db\"; New-Item -ItemType Directory -Force (Split-Path $ds

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\cookie_audit.py", "content": "import sqlite3, datetime, sys\n\ndef chrome_ts(t):\n    if not t:\n        return '-'\n    return (datetime.datetime(1601, 1, 1

---

> `PowerShell` -- {"command": "$sp=\"$env:LOCALAPPDATA\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\"; esentutl /y \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\Cookies\" /d \"$sp\\cookies_copy.db\" /vss | Select-Object -Last 2; pytho

---

> `PowerShell` -- {"command": "$sp=\"$env:LOCALAPPDATA\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\"; Get-Item \"$sp\\cookies_copy.db\" | Select-Object Length, LastWriteTime; esentutl /y \"C:\\Users\\dev\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Network\\

---

> `Glob` -- {"pattern": "10-Tasks/**/task-2026-08-10-browser-rail-down*", "path": "D:\\Vault\\Vault-Knowledge"}

---

> `Grep` -- {"pattern": "restarting Chrome|relaunch|Chrome relaunched|CloseMainWindow|перезапуск Chrome|рестарт Chrome", "path": "C:\\Users\\dev\\.claude\\scripts\\_logs", "output_mode": "content", "-i": true, "head_limit": 20}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-10-browser-rail-down-forever-fix.md"}

---

> `PowerShell` -- {"command": "(Get-WinEvent -FilterHashtable @{LogName='System'; Id=1074; StartTime=(Get-Date).AddDays(-5)} | Select-Object -First 1).Message; Write-Output \"===\"; python -c \"\nimport sqlite3\ncon = sqlite3.connect(r'C:\\Users\\dev\\.claude\\scripts\\fb_guard.db')\nprint(con.execute('select name 

---

> `Grep` -- {"pattern": "checkpoint|разлогин|вылогин|Facebook.*(вход|логин)|FB.*(разлог|логин)", "path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "output_mode": "content", "-i": true, "head_limit": 15}

---

**Claude:**

Рестарт 27.08 инициировал наш же робот («Claude: repair MSIX package limbo»). Читаю строки журнала поломок про разлогины.

---

> `PowerShell` -- {"command": "$f=\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"; $lines = Get-Content $f -Encoding UTF8; foreach($n in 41,65,122,378,631,634,637,869,1019,1124,1193,1347,1513,1612,1617,1637){ $t=$lines[$n-1]; if($t.Length -gt 260){$t=$t.Substring(0,260)+'…'}; Write-Output \"[$n] $t\

---

> `PowerShell` -- {"command": "$f=\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"; $lines = Get-Content $f -Encoding UTF8; Write-Output \"=== [122] ===\"; $lines[121]; Write-Output \"=== [631] ===\"; $lines[630]; Write-Output \"=== [1193] ===\"; $lines[1192]; Write-Output \"=== [1347] ===\"; $lines[

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "limit": 40}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "old_string": "## Строки (append-only, новые сверху)\n\n- 2026-08-30 02:5x", "new_string": "## Строки (append-only, новые сверху)\n\n- 2026-08-30 13:2x (HUB-01, живая сессия по жалобе оператора «

---

**Claude:**

Теперь чиню мелочь с уликой: fix-chrome-bridge.ps1 добивает Chrome через 4 секунды, а куки коммитятся батчем ~30с.

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\fix-chrome-bridge.ps1", "old_string": "# graceful close, then hard kill leftovers (Chrome lingers in background)\n$chrome | ForEach-Object { $_.CloseMainWindow() | Out-Null }\nStart-Sleep 4\nGet-Process chrome -ErrorAction Sile

---

> `PowerShell` -- {"command": "cd C:\\Users\\dev\\.claude; git add scripts/fix-chrome-bridge.ps1; git commit -m @'\nfix-chrome-bridge: wait up to 45s for graceful Chrome exit before hard kill\n\nChrome commits cookies in ~30s batches; the old 4s kill was a crash exit\nthat could eat fresh login cookies (part of the

---

**Claude:**

scripts/ в ~/.claude вне git (игнорится) — тогда по §5.11 подпись идёт в change_ledger.

---

> `PowerShell` -- {"command": "$led=\"C:\\Users\\dev\\.claude\\change_ledger\\HUB-01.jsonl\"; New-Item -ItemType Directory -Force (Split-Path $led) | Out-Null; $rec = @{ts=(Get-Date).ToUniversalTime().ToString('yyyy-MM-ddTHH:mm:ssZ'); file='scripts/fix-chrome-bridge.ps1'; change='wait up to 45s for graceful 

---

**Claude:**

[⏰ воскресенье, день, 13:13, 30 августа 2026]

🎙 Майк: корень нашёл, и он неприятный: главный «вылогиниватель» из claude.ai - это мы сами, наши же ночные роботы. С Facebook хуже: там нас выкидывает сервер Meta за автоматизацию с твоего аккаунта. Один вопрос тебе в конце.

## Что происходит: три причины, все с датированными уликами

**1. claude.ai: война человека с роботом за один браузер (корень доказан, уже починено этой ночью).**
Ночная рутина claudeai-sync до вчерашнего дня «лечила» себя прямо в твоём живом Chrome: делала logout на claude.ai и входила под рабочий аккаунт a2 по magic-link. Ты входишь под своим аккаунтом (bb) - робот ночью тебя вылогинивает - утром ты снова у логин-стены. Это повторилось минимум трижды (14.08, 20.08, 27.08, всё в журнале поломок). В журнале висел открытый вопрос «кто перещёлкивает Chrome обратно на bb» - ответ: ты сам, и это нормально, аккаунт твой. Ночью 30.08 параллельная сессия увела робота в отдельный профиль `_chrome_profile_a2`, твой Chrome он больше не трогает. **Если после сегодняшнего дня claude.ai снова разлогинит - скажи, значит корень не только этот.**

**2. Facebook: сессию убивает сервер Meta, не Chrome.**
Улики: 19.08 FB требовал «подтверди личность» (чекпойнт), 23.08 и 25.08 - логин-стена, куки `c_user` нет. Решающий факт добавила твоя жалоба: ты входил в FB 28-29.08, сегодня снова выкинуло, при этом Chrome непрерывно работает с 28.08 18:30 и машина не перезагружалась с 27.08. То есть куки не «потерялись» - Meta погасила сессию со своей стороны, прожила она сутки-двое. Наиболее вероятная причина: риск-движок Meta реагирует на ежедневную автоматизацию с твоего аккаунта (fb-reply, fb-likes до 40 ответов и 60 лайков в день) плюс входы с нескольких машин.

**3. Отягчитель: Chrome на хабе регулярно умирает «грязно».**
Хаб перезагружали 10 раз за 14 дней (в основном руками через AnyDesk, один раз наш робот 27.08 в 6:29 командой shutdown для починки MSIX). Chrome при этом помечен как «Crashed», а куки он пишет на диск порциями раз в ~30 секунд - свежий логин перед ребутом может просто не доехать до диска. Плюс наш скрипт рестарта Chrome добивал его через 4 секунды после закрытия - это я уже починил (теперь ждёт до 45с), подпись правки в change_ledger.

## Что сделано этой сессией
- Разбор записан строкой в Breakage-Journal (закрыт открытый вопрос строки 27.08).
- [fix-chrome-bridge.ps1](C:\Users\dev\.claude\scripts\fix-chrome-bridge.ps1) больше не убивает Chrome раньше сброса куков.

## Что требует твоего решения (это не чинится браузером)
У FB нет запасной безлюдной рельсы (токен пуст с 11.07), и каждый разлогин Meta = снова твои руки. Варианты: (а) сбавить темп fb-автоматизации, чтобы риск-движок успокоился; (б) поднять токен-рельсу Graph API, чтобы роботы не жили в твоей браузерной сессии; (в) оставить как есть и принять перелогин раз в 1-2 дня как цену. Я за (б)+(а) вместе. Что выбираешь?

🧒 Простыми словами: у тебя один браузер, а живут в нём двое - ты и роботы. Робот ночью выходил из твоего Клода, чтобы войти под своим аккаунтом, поэтому утром тебя «выкидывало». Это уже починили: роботу дали отдельный браузер. А Фейсбук выгоняет тебя сам, со своей стороны: ему не нравится, что с твоего аккаунта кто-то слишком ровно и много лайкает. Пока роботы работают из-под тебя, Фейсбук будет выгонять снова и снова.

[⏰ воскресенье, день, 13:14, 30 августа 2026]

---

**User:**

Stop hook feedback:
СТОП: ты объявляешь недоступность, не обойдя ВСЕ поверхности.
  фрагмент: …трогает. **Если после сегодняшнего дня claude.ai снова разлогинит - скажи, значит корень не только этот.*…
(последний обход: x, 1586 мин назад — не тот вендор или устарел)

Класс замерен трижды за трое суток (29-31.07): вывод «Google мёртв» делался по ОДНОМУ
профилю, пока живая сессия лежала в Chrome на другом аккаунте. Каждый повтор = ложный
аск оператору + день не той работы.

Сделай ДО вывода:
    python3 ~/.claude/scripts/rail_sweep.py claude_ai
Он перечислит ВСЕ места (профили рельсы · системный Firefox · профили Chrome · Chrome-MCP)
и назовёт те, что с диска не читаются — их проверяют ЖИВОЙ вкладкой, а не файлом.
Вывод «доступа нет» законен, только когда пусты ВСЕ поверхности из списка.
Если место одно и ты это знаешь — так и напиши: «в профиле X сессии нет» (per-профиль),
а не «X недоступен» (про весь мир).

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\rail_sweep.py claude_ai 2>&1 | Select-Object -First 60", "description": "Sweep all claude.ai auth surfaces before concluding", "timeout": 180000}

---

**Claude:**

[⏰ воскресенье, день, 13:16, 30 августа 2026]

Принял поправку сторожа: прогнал обход всех поверхностей `rail_sweep.py claude_ai`. Уточняю формулировку, чтобы она была про-профильной, а не «про весь мир»:

- Поверхностей с claude.ai на этой машине три: системный Firefox (профиль 646yqiss, куки есть), Firefox-профиль fbread (куки есть) и Chrome с MCP-расширением (с диска не читается, живость только вкладкой).
- Мой вывод про «войну за аккаунт» касается ровно ОДНОЙ поверхности: профиля **Chrome Default** на хабе, где живёшь ты и где до 30.08 ночной робот делал logout и вход под a2. Firefox-профили этой войной не задеты, там свои сессии (по прошлым замерам обе под bbplatinum).
- «Если снова разлогинит» читай так: если после 30.08 тебя снова выкинет из claude.ai **именно в Chrome Default**, значит в этом профиле есть ещё один переключатель, кроме уже уведённого робота, и я вернусь копать по строке журнала.

Остальное из моего разбора (Meta-серверные разлогины FB, грязные смерти Chrome при ребутах) этой поправкой не меняется.

🧒 Простыми словами: я уточнил адрес поломки. Не «Клод выкидывает вообще», а «выкидывало в одном конкретном браузерном профиле, где робот жил вместе с тобой». Из этого профиля робота уже выселили.

[⏰ воскресенье, день, 13:16, 30 августа 2026]

---

**User:**

(б) поднять токен-рельсу Graph API, чтобы роботы не жили в твоей браузерной сессии!! Написано у меня ещё и куча других вещей вылогиливается. Ага. Так. что-то делать. Может быть, на, может, можно пишет правила Библи, что ты всегда работаешь на веб-прям, напишем правила Библию. Хочешь два делать, два делать отдельной сессии? Всегда работаем через лицо, всегда работаем через лису, всегда работаем через Firefox. Firefox всегда. А Chrome используем как запасный вариант. Твои раскатанные слоты уже создал балла. Чинить это. Вообще. Да, экстати, пункт первый. С этого компьютера тоже отправил Библию. Мы же делали уже это правило. Я всегда работаю через аккаунт Биби Платину. Клод на этом компьютере всегда запустится, включён за работу через Биби Платин. Всегда запиши я, пожалуйста, без зарубин на носу. Пожалуйста, сделай так, чини корни. Чни все корни, чини все корни.  O

---

**Claude:**

[⏰ воскресенье, день, 13:19, 30 августа 2026]

Принято: (б) токен-рельса Graph API, правило «Firefox всегда, Chrome запасной», правило «Клод на этом компе всегда под bbplatinum», починка корней в отдельных сессиях через слоты. Сначала RECALL: проверяю, что из этих правил уже записано, чтобы не плодить дубли.

---

> `Grep` -- {"pattern": "bbplatinum|ББ Платинум|bb-платин", "path": "D:\\Vault\\Vault-Knowledge\\05-Reglaments", "output_mode": "files_with_matches", "-i": true, "head_limit": 15}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\session_slot.py status 2>&1 | Select-Object -First 30", "description": "Show reusable session slot pool"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\session_slot.py --list 2>&1 | Select-Object -First 25", "description": "List reusable session slots"}

---

> `Grep` -- {"pattern": "bbplatinum.*(всегда|правило|hub|хаб)|хаб.*bbplatinum|этом компьютере.*bb", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "-i": true, "head_limit": 10}

---

> `Glob` -- {"pattern": "**/reglament-firefox-po-maksimumu*", "path": "D:\\Vault\\Vault-Knowledge"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-firefox-po-maksimumu-i-zamer.md", "limit": 60}

---

> `PowerShell` -- {"command": "Get-Content \"D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-firefox-po-maksimumu-i-zamer.md\" -Encoding UTF8 | Select-Object -Last 25", "description": "Read tail of firefox reglament for amendment format"}

---

> `PowerShell` -- {"command": "$f=\"D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-firefox-po-maksimumu-i-zamer.md\"; $add = @'\n\n## §Поправка 30.08.2026 — четвёртое подтверждение приказа + новый мотив: разделение личностей\n\nДословно (dev 30.08, голосом, в разборе «Chrome постоянно вылогинивае

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\05-Resources\\Protocols\\reglament-hab-brauzernye-lichnosti-bb-i-roboty.md", "content": "---\ntitle: \"Регламент: браузерные личности хаба — оператор всегда под bbplatinum, роботы НЕ живут в его браузере\"\naliases: [\"браузерные личности хаба\", \"bb всегд

---

**Claude:**

Теперь память + строка в MEMORY.md INBOX.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\hub-browser-identities-bb-and-robots.md", "content": "---\nname: hub-browser-identities-bb-and-robots\ndescription: \"STANDING (dev 30.08 голосом): человеческий Chrome хаба = bbplatinum ВСЕГДА; роботы не дела

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\n- _(пусто — разнесено 29.08: 7 спиц дословно в хабы §3 — leads · tg-rails · te

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\n- _(пусто — разнесено 29.08: 7 спиц дословно в хабы §3 — leads · tg-rails · te

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)\n- _(пусто — разнесено 29.08: 7 спиц дословно в хабы §3 — leads · tg-rails · te

---

**Claude:**

Поднимаю двух починщиков через переиспользование слотов (§9.2).

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\session_slot.py --claim \"fb-graph-token-rail\" 2>&1 | Select-Object -First 15; Write-Output \"===\"; python C:\\Users\\dev\\.claude\\scripts\\session_slot.py --claim \"robots-out-of-human-browser\" 2>&1 | Select-Object -First 15", "descripti

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__update_scheduled_task,mcp__scheduled-tasks__list_scheduled_tasks", "max_results": 2}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "auto-hub-260825-fleet-debt-drain", "description": "FB Graph API токен-рельса: роботы вон из браузерной сессии оператора (приказ 30.08)", "fireAt": "2026-08-30T13:40:00+01:00", "prompt": "Первым действием вызови mcp__ccd_session__set_session_title с заголовком «FB Graph API токен-рельса (при

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "auto-hub-260824-dr-runner-hiring", "description": "Роботы вон из браузера человека: миграция рутин в свои профили + карта разлогинов (приказ 30.08)", "fireAt": "2026-08-30T13:55:00+01:00", "prompt": "Первым действием вызови mcp__ccd_session__set_session_title с заголовком «Роботы вон из 

---

**Claude:**

Read-back (урок класса seed-premise/readback от сегодняшней утренней сессии): проверяю фактом, что приказы легли в слоты.

---

> `PowerShell` -- {"command": "foreach($t in 'auto-hub-260825-fleet-debt-drain','auto-hub-260824-dr-runner-hiring'){ $p=\"C:\\Users\\dev\\.claude\\scheduled-tasks\\$t\\SKILL.md\"; if(Test-Path $p){ $c=Get-Content $p -Raw -Encoding UTF8; $m1=$c -match 'set_session_title'; $m2=$c -match 'seed-stop-dup-block'; $m3=$c 

---

> `PowerShell` -- {"command": "Select-String -Path \"C:\\Users\\dev\\.claude\\scheduled-tasks\\auto-hub-260825-fleet-debt-drain\\SKILL.md\" -Pattern 'FB Graph API' -Encoding UTF8 | Select-Object -First 1; Select-String -Path \"C:\\Users\\dev\\.claude\\scheduled-tasks\\auto-hub-260824-dr-runner-hiring\\SKILL.md\" 

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\rule_home_guard.py reglament-hab-brauzernye-lichnosti-bb-i-roboty 2>&1 | Select-Object -First 15", "description": "Check rule homes and door coverage for new reglament"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "- [Личности браузеров хаба](hub-browser-identities-bb-and-robots.md) — ⭐30.08 Chrome человека=bb всегда, роботы не перелогинивают; FB токен-рельса ОК", "new_stri

---

> `Grep` -- {"pattern": "ШАГ 0|Шаг 0", "path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "output_mode": "content", "head_limit": 5}

---

> `Grep` -- {"pattern": "logout|чужой орг|аккаунт", "path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "output_mode": "content", "-n": true, "head_limit": 10}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "offset": 10, "limit": 30}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\claudeai-sync\\SKILL.md", "old_string": "### 0. ГВАРД АККАУНТА + САМОЛЕЧЕНИЕ ВХОДА (не пропускать)\n`GET /api/organizations` → chat-org (caps содержит `chat`) обязан быть `s_be15d406` (a2).\nЕсли там чу

---

> `Grep` -- {"pattern": "claude\\.ai/logout", "path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "output_mode": "content", "-n": true}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "offset": 36, "limit": 35}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "limit": 36}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scheduled-tasks\\claudeai-sync-daily\\SKILL.md", "old_string": "ШАГ 0 — ГВАРД АККАУНТА (КРИТИЧНО, не пропускать):\n1. Claude-in-Chrome: list_connected_browsers. Если ни одного браузера → НЕ делай вывод «нового нет». Пинг в Telegram чат 

---

> `PowerShell` -- {"command": "$led=\"C:\\Users\\dev\\.claude\\change_ledger\\HUB-01.jsonl\"; foreach($f in @('skills/claudeai-sync/SKILL.md','scheduled-tasks/claudeai-sync-daily/SKILL.md')){ $rec=@{ts=(Get-Date).ToUniversalTime().ToString('yyyy-MM-ddTHH:mm:ssZ'); file=$f; change='ШАГ 0 переписан по reglamen

---

> `PowerShell` -- {"command": "$led=\"C:\\Users\\dev\\.claude\\change_ledger\\HUB-01.jsonl\"; foreach($f in @('skills/claudeai-sync/SKILL.md','scheduled-tasks/claudeai-sync-daily/SKILL.md')){ $rec=@{ts=(Get-Date).ToUniversalTime().ToString('yyyy-MM-ddTHH:mm:ssZ'); file=$f; change='ШАГ 0 переписан по reglamen

---

**Claude:**

[⏰ воскресенье, день, 13:33, 30 августа 2026]

🎙 Майк: всё принял и уже поднял. Одна честная оговорка про Graph API ниже - прочитай её, она важная: API не умеет всё, что умеет браузер.

## Токен-рельса Graph API: как и когда

**Когда: уже.** Сессия-строитель «FB Graph API токен-рельса (приказ 30.08)» стартует сегодня в **13:40** (переиспользованный слот, видна в списке сессий). Вторая, «Роботы вон из браузера человека», стартует в **13:55**.

**Как (план сессии):**
1. Сначала честная карта по свежей документации Meta: что реально переносимо на токен. Оговорка: с 2018 года Graph API почти не управляет ЛИЧНЫМ профилем - постить на твою личную стену, лайкать и отвечать от твоего лица через API нельзя, это Meta закрыла всем. На токен уезжает: чтение, работа со Страницами (посты, комменты, лайки от имени Страницы), Messenger. Что не уедет - сессия предъявит списком с вариантами (вести с Страницы / снизить темп / принять перелогин), решишь ты.
2. Получение long-lived токена (60 дней) + бессрочных page-токенов, хранение в secrets store, сторож протухания, который кричит ЗА 7 дней до смерти токена, а не после.
3. Один шаг потребует твоих рук: первичная выдача токена = твой вход в developers.facebook.com. Сессия подготовит точный клик-путь и поднимет аск в 02 POLICE - пароль я не ввожу по канону.

## Правила записаны (без зарубок на носу)

- **«Клод на этом компе всегда под bbplatinum»**: новый регламент в Библии `reglament-hab-brauzernye-lichnosti-bb-i-roboty` + память + строка в MEMORY.md. Проверка домов правила прошла (guard зелёный).
- **«Firefox всегда, Chrome запасной»**: это правило уже жило в Библии с 04.08 (твой же приказ, трижды повторённый). Дубль не плодил - дописал туда Поправку 30.08 с новым мотивом: разделение личностей человек/робот.

## И главный улов по ходу: корень добит прямо сейчас

Проверяя двери правила, нашёл, что ночная рутина и скилл claudeai-sync **до сих пор несли инструкцию «сделай logout в живом Chrome»** - ту самую, что тебя вылогинивала. Вычистил оба файла: теперь роботу прямо запрещено трогать твой браузер, вход a2 только через выделенный профиль. Подписи правок в change_ledger.

Подсказка от планировщика: если будешь у компа в 13:40, нажми у задачи «Run now» - тогда разрешения на браузер/коннекторы запомнятся на задаче и будущие прогоны не встанут на апрувах.

🧒 Простыми словами: роботам выдали собственные ключи от собственных квартир, а из твоей квартиры их выселили и правило об этом повесили на стену. Для Фейсбука строим роботам служебный вход через API, но у этого входа есть ограничение: от твоего личного имени Фейсбук пускает только живого человека - что с этим делать, сессия принесёт тебе варианты.

[⏰ воскресенье, день, 13:34, 30 августа 2026]

---

**User:**

Я проверил бы, чтобы на чем флоте это работало, и потом сделал бы ретро. Короче. Отдельно все сидела на ग्राх API. Отдельно все сидела на graph API, не подключайся. Так, окей. Да, и все, все по максимуму, что может провести, перевести на graph API. Переводим и работаем. Да, я задаю где вопрос Facebook com. Делать девяносто шесть минут. Проверь еще, какие рутины и какие скилы несли в себе инструкции, сделала галд в аккаунту браузере. Посмотри, везде на всех машинах переучена этом компьютерной хабе. Что такое ереси больше никогда не было? Такой е

---

**Claude:**

[⏰ воскресенье, день, 14:41, 30 августа 2026]

Принял: (1) максимум на Graph API переводим и работаем, (2) свип по ВСЕМ машинам: какие ещё рутины и скиллы несут инструкцию «сделай logout в живом браузере», чтобы ереси не осталось нигде, (3) потом проверка на флоте и ретро. Начинаю со свипа на хабе.

---

> `Grep` -- {"pattern": "navigate.*logout|logout['\"`]?\\)|сделай logout|выйди из аккаунта|claude\\.ai/logout|/logout", "path": "C:\\Users\\dev\\.claude", "output_mode": "content", "-i": true, "-n": true, "glob": "**/*.{md,py,ps1,cmd,sh,json}", "head_limit": 40}

---

> `Grep` -- {"pattern": "navigate.*logout|claude\\.ai/logout|сделай logout|выйди из аккаунта", "path": "D:\\Vault\\_imports", "output_mode": "content", "-i": true, "-n": true, "glob": "**/*.{md,py,ps1,cmd,sh}", "head_limit": 30}

---

> `Grep` -- {"pattern": "claude\\.ai/logout", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "content", "-n": true, "head_limit": 15}

---

> `Grep` -- {"pattern": "claude\\.ai/logout", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "output_mode": "content", "-n": true, "head_limit": 15}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\claudeai-sync-needs-a2-account.md", "old_string": "**2026-07-30 — РАБОЧИЙ ВХОД БЕЗ РУК оператора (сделан, проверен, синк поехал).** Правильная лестница, когда a2 недоступен:", "new_string": "

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py --help 2>&1 | Select-Object -First 20", "description": "Check bus_send usage"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK [для КАЖДОГО узла, вкл. NODE-0X/NODE-0X/NODE-0X/Нора/Рита/Маяк]: СВИП ЕРЕСИ LOGOUT (приказ оператора 30.08, канон в волте reglament-hab-brauzernye-lichnosti-bb-i-roboty). Контекст: на хабе найден и добит корень 'Chrome п

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK: свип ереси logout на КАЖДОМ узле (NODE-0X, NODE-0X, NODE-0X, Нора, Рита, Маяк). Приказ оператора 30.08, канон в волте reglament-hab-brauzernye-lichnosti-bb-i-roboty. Контекст: на хабе найден и добит корень 'Chrome посто

---

**User:**

This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.

Summary:
1. Primary Request and Intent:
   dev (RU, voice messages, hub HUB-01) — continuation of "Chrome постоянно вылогинивает из всего" root-fix session. Current thread: build the FB Graph API token rail (his chosen option "(б)"), with dev doing the manual developers.facebook.com steps guided by me:
   - "Да, я про developers.facebook.com - куда мне нажимать чтобы сделать токен?"
   - Screenshot Q: Business vs Consumer app type — "что выбираем!?"
   - Created app; gave App ID + App Secret; repeatedly asked me to capture his screen / drive Firefox myself ("возьми сам, пожалуйста... захватить моё управление экраном и открыть Firefox, нажать кнопочки").
   - Graph Explorer screenshot: "правильно или НЕТ?"
   - "Может быть, мы сделаем больше permission для нашего токена? Давай побольше сделаем, чтобы меньше это я спрашивал в будущем."
   - Sent short-lived token #1, then mid-turn a regenerated token #2 with extended permissions ("вот новый").
   Standing orders still active from earlier in session: verify fixes fleet-wide then run retro; move "всё по максимуму" to Graph API; ensure no routine/skill anywhere on the fleet ever carries browser-logout instructions again.

2. Key Technical Concepts:
   - FB Graph API dev-mode app (Consumer type, no App Review for app admin): app "dev Metrics Reader", ID 1655895462767856.
   - Token ladder: short-lived Explorer token → long-lived (~60d) via GET graph.facebook.com/v21.0/oauth/access_token?grant_type=fb_exchange_token&client_id=..&client_secret=..&fb_exchange_token=..
   - ⚠️ KEY GOTCHA (measured 30.08): profiles in Meta professional mode get 400/code 200/subcode 2069030 "New Pages Experience Is Not Supported" on direct GET /me/posts and /me/feed; workaround = field expansion `me?fields=posts.limit(N){...}` which returns the same posts AND metrics (reactions/comments summaries, shares).
   - Platform limits (memory fb-personal-profile-api-limits): personal-profile posting/commenting/liking/Messenger via API impossible since 2018 (publish_actions removed) — only reading migrates; API posting only to a Page (dev has none). Comment TEXTS from other users not returned (privacy; only counts) — user token sees only comments of users who authorized the app.
   - Token scopes v2 (granted): email, manage_fundraisers, public_profile, user_age_range, user_birthday, user_events, user_friends, user_gender, user_hometown, user_likes, user_link, user_location, user_photos, user_posts, user_videos. No pages_* (Explorer didn't attach them to Consumer app; needed only when a Page exists).
   - fb_token_rail.py (built by parallel 13:40 session): exchange/install/status/pages/where; FB_RAIL_ENABLED_AT marker distinguishes DORMANT vs INCOMPLETE; watchdog oauth_probe.py EXPIRY_STORES alarms 14 days before expiry; test _test_fb_token_rail.py.
   - Secrets store copies (4, all must hold same token): C:\Users\dev\.claude\secrets\fb_graph.env, E:\!CLAUDE-HUBPC-June26\secrets\fb_graph.env, C:\Users\dev\!CLAUDE-NODE-0X May26\secrets\fb_graph.env, C:\Users\dev\!CLAUDE-NODE-0X May26\secrets\fb_graph.env. fb_posts_poll SECRET_DIRS order: $CLAUDE_SECRETS → ~/.claude/secrets → E:\!CLAUDE... → NODE-0X.
   - claude-in-chrome extension = Chrome only; hub Chrome NOT logged into FB (redirects to login); dev's FB session lives in Firefox; computer-use screen MCP NOT attached to this session (verified twice via ToolSearch).
   - Security/behavioral rules in force: never type dev's passwords; never click OAuth/logins in dev's live FB browser (Meta risk engine kills sessions over automation — the class we're escaping); robots never logout/switch accounts in human browsers (reglament-hab-brauzernye-lichnosti-bb-i-roboty); secrets stay in store, never in vault/always-loaded/public.
   - Reply style: RU, timestamp line at start AND end ([⏰ ...]), 🎙 Майк micro-block, 🧒 ELI5 block, NO em/en dashes.
   - Provenance: ~/.claude/scripts is gitignored → signatures go to ~/.claude/change_ledger/HUB-01.jsonl (ts/file/change/assisted_by='Claude Code / claude-fable-5'/machine='HUB-01'/account='bb'/operator='robot:hub-live-session').

3. Files and Code Sections:
   - C:\Users\dev\!CLAUDE-NODE-0X May26\secrets\fb_graph.env AND C:\Users\dev\.claude\secrets\fb_graph.env (rewritten): header comments + FB_APP_ID=1655895462767856, FB_APP_SECRET=REDACTED, FB_USER_TOKEN=<long-lived v2>, note "Скоупы 30.08 v2: полный user_* ... pages_* нет"; FB_RAIL_ENABLED_AT=2026-08-30 added via fb_token_rail install (which wrote E:\ and C:\Users\dev copies too). All 4 copies verified identical (token prefix EAAXiBzTX7PABSUb8cESR).
   - C:\Users\dev\.claude\scripts\fb_posts_poll.py (patched — the main code change):
     - Module docstring now: "30.08.2026: прямой /me/posts закрыт для профиля в professional-режиме (200/2069030), все чтения идут через field-expansion me?fields=posts.limit(N){...} - см. _me_posts()."
     - New helper inserted before cmd_check():
       ```python
       def _me_posts(requests, tok, fields, limit, timeout=60):
           """Список постов стены через field-expansion: me?fields=posts.limit(N){...}.
           Прямые /me/posts и /me/feed для профилей в новом professional-режиме Meta
           отбивает кодом 200/2069030 "New Pages Experience Is Not Supported"
           (замер 30.08.2026); расширение полей отдаёт те же посты и метрики.
           Возвращает (resp, posts_list|None): при не-200 posts_list=None."""
           r = requests.get(GRAPH + "/me", params={
               "fields": "posts.limit(%d){%s}" % (limit, fields),
               "access_token": tok}, timeout=timeout)
           if r.status_code != 200:
               return r, None
           return r, (r.json().get("posts") or {}).get("data", [])
       ```
     - cmd_posts: replaced direct /me/posts call with `r, data = _me_posts(requests, tok, "id,message,permalink_url,created_time", limit, timeout=30)`; error check `if data is None`; loop `for it in data:`.
     - cmd_metrics: same swap with fields "id,message,permalink_url,created_time,shares,reactions.summary(true).limit(0),comments.summary(true).limit(100){id,from,message,created_time}"; error check `if me.status_code != 200 or data is None`.
     - GRAPH = "https://graph.facebook.com/v26.0" (was already bumped by parallel session).
   - C:\Users\dev\.claude\scripts\fb_token_rail.py (read, built by parallel 13:40 session — do not duplicate): commands exchange|install|status|pages|where; install takes value via STDIN (no --value flag); status output: "fb-token: OK -- expires 2026-10-29 (59д); scopes=...".
   - C:\Users\dev\AppData\...\scratchpad\: fb_exchange.py, fb_exchange2.py (token exchanges via urllib), fb_probe.py/fb_probe2.py/fb_probe3.py (endpoint probes), fb_long_token.txt, fb_long_token2.txt (live token v2 — sensitive), fb_metrics.json (consumed+deleted by ingest? passed via --in).
   - D:\Vault\Vault-Knowledge\10-Tasks\task-2026-07-11-fb-graph-token-enable.md (edited): state: someday → done; Outcome filled: app created by dev, long-lived token to 2026-10-29, full user_* scopes, 2069030 workaround, ingest 50 posts/50 snapshots, comments-text platform limit.
   - C:\Users\dev\.claude\projects\P---WORKDIR-HUB\memory\fb-personal-profile-api-limits.md (edited): added 2069030 gotcha + workaround pointer (fb_posts_poll.py::_me_posts), comments-texts limitation, "30.08 17:3x рельса ЖИВАЯ" status line.
   - C:\Users\dev\.claude\change_ledger\HUB-01.jsonl (appended): provenance record for the fb_posts_poll.py patch.
   - D:\Vault\_imports\content-factory\registry\pub_metrics.py + collect_pub_metrics.cmd (read): ingest-fb-graph --in fb_metrics.json; nightly .cmd already runs `fb_posts_poll.py metrics --limit 25 --out fb_metrics.json` then ingest, graceful without token — no edit needed.
   - Pre-compaction artifacts still relevant: reglament-hab-brauzernye-lichnosti-bb-i-roboty.md (vault Protocols), hub-browser-identities-bb-and-robots.md (memory), claudeai-sync-needs-a2-account.md (memory with ⛔⛔ ПОПРАВКА 30.08), both claudeai-sync SKILL.md files (logout paths excised).

4. Errors and fixes:
   - Cannot reach dev's Firefox: claude-in-chrome connected only to Chrome (chrome://newtab; FB not logged in → login redirect); computer-use MCP absent from session (ToolSearch found nothing, twice). Fix: honest hand-back to dev for the password/secret/token clicks, with explicit reasoning that automating his live FB would retrigger Meta's risk engine. dev accepted and did the clicks.
   - fb_posts_poll.py metrics → 400 {"code":200,"error_subcode":2069030,"error_user_title":"New Pages Experience Is Not Supported"}: root-caused via probes (both /me/posts and /me/feed blocked; me?fields=posts{...} works) → patched with _me_posts() helper (class fix, both commands).
   - Token #1 had only user_posts+public_profile (dev generated before adding extended perms) → dev regenerated; token #2 exchanged and installed everywhere.
   - Comments arrays empty despite counts → determined platform privacy limitation (probe on post 28812850911655795_28810615281879358: data:[] summary total_count:4), not a bug; documented, not "fixed".
   - fb_token_rail.py install --field ... --value → "ERROR: no value on stdin (or --token)" → value must be piped via stdin: `echo "2026-08-30" | fb_token_rail.py install --field FB_RAIL_ENABLED_AT`.
   - FB_RAIL_ENABLED_AT marker missing after my manual env writes (would confuse the DORMANT/INCOMPLETE watchdog logic) → installed marker, status stays OK.
   - AskUserQuestion browser choice: dev answered free-form "firefox открыт на хабе этом ПК" rather than picking an option — interpreted correctly (his session is Firefox; Browser 1 turned out to be Chrome).

5. Problem Solving:
   FB Graph API token rail brought fully alive in one sitting: app created (Consumer, dev mode) → App ID/Secret in store → short token exchanged to long-lived (expires 2026-10-29, 59d) with full user_* scope set → professional-mode endpoint block worked around via field expansion → fb_posts_poll.py check=AUTH OK, metrics returns live posts with reactions/shares/comment counts → pub_metrics ingest = 50 posts / 50 snapshots → nightly collector step already wired → expiry watchdog armed (oauth_probe EXPIRY_STORES, 14-day alarm; FB_RAIL_ENABLED_AT marker set) → regression test _test_fb_token_rail.py GREEN → provenance ledger + task card done + memory updated. This closes task-2026-07-11-fb-graph-token-enable (stalled 50 days). Earlier in session: logout-war root fix, rules recorded, hub sweep clean, fleet sweep broadcast (#logout-heresy-sweep).

6. All user messages (post-compaction):
   - "Да, я про developers.facebook.com - куда мне нажимать чтобы сделать токен?" (after /compact local command)
   - [Screenshot of Create an app: Business vs Consumer] "что выбираем!?"
   - [Screenshot of created app dashboard] "создал, вот тебе App ID и Secret Слушай, я залогинен сейчас в, в Лизе, Firefox. Открой мой экран, посмотри сам и возьми сам, пожалуйста... секреты нигде не вижу... возьми сам, пожалуйста, был браузер открыт." (garbled voice; App ID visible, secret not yet)
   - AskUserQuestion answer: "firefox открыт на хабе этом ПК"
   - [Screenshot of Settings→Basic with App secret revealed] "1655895462767856 a8e0c76ebe760a316951dd20f3bb5616 Ну, кстати, ты же как-то с, типа, с Firefox работаешь... ты мог бы взять, захватить моё управление экраном и открыть Firefox, нажать кнопочки и получить доступ. Для чего? Вот тебе, что ты просил."
   - [Screenshot of Graph Explorer configured] "правильно или НЕТ?"
   - "Может быть, мы сделаем больше permission для нашего токена? Давай побольше сделаем, чтобы меньше это я спрашивал в будущем."
   - [Screenshot + token #1 pasted] "EAAXiBzTX7PABSc9bY2clIDHx837jO3SZAk5MOEdoA3qMA1Ndi302AVty..." (full short-lived token)
   - Mid-turn: "EAAXiBzTX7PABSW0dZCGPwgH6agsBabQNl14AixpYs7g5GCcu6tNCKrs...ZDZD вот новый" (token #2 with extended perms)
   Security-relevant constraints in force (from canon/earlier): I never enter dev's passwords; secrets only in secrets store (never vault/always-loaded/public/outbound); no robot logins/logouts/OAuth clicks in dev's live browsers; Meta = ban-sensitive.

7. Pending Tasks:
   - Write the final report to dev on the completed FB Graph rail (the immediate open item — report not yet delivered).
   - Fleet verification of #logout-heresy-sweep: collect per-node ACKs/reports in TG-03; chase silent nodes; laptops must fix their claudeai-sync-daily 04:40 fallback copies.
   - Run /retro after fleet verification (dev's ordered sequence: "Я проверил бы, чтобы на всём флоте это работало, и потом сделал бы ретро").
   - FB остаток "всё по максимуму на Graph API": reading is migrated; posting/comments/likes/Messenger of personal profile cannot migrate (platform limit) — the Page-creation option (page tokens are permanent, pages_manage_posts etc.) remains an open decision for dev; pages_* scopes would need a token regen once a Page exists.
   - Token expiry 2026-10-29: watchdog will alarm at ≤14 days; renewal = dev's one Generate-click + `fb_token_rail.py exchange`.

8. Current Work:
   Finishing the FB token rail closure. Last actions: verified nightly collector FB step exists (grep of D:\Vault\_imports\content-factory\registry\collect_pub_metrics.cmd showed lines 5-10: `python C:\Users\dev\.claude\scripts\fb_posts_poll.py metrics --limit 25 --out fb_metrics.json` + `pub_metrics.py ingest-fb-graph --in fb_metrics.json`, graceful without token). All verification is green: `fb_token_rail.py status` = "fb-token: OK -- expires 2026-10-29 (59д)" with full scope list; `_test_fb_token_rail.py` = "GREEN: все кейсы прошли"; ingest = "fb-graph: новых постов 50 · снапшотов 50 · новых комментов 0". Task card set to done, memory updated, change_ledger written. The ONLY thing not yet done is the final chat report to dev (RU, [⏰...] timestamp at start and end, 🎙 Майк block, 🧒 ELI5 block, no em/en dashes).

9. Optional Next Step:
   Write the final reply to dev reporting the rail is fully alive: token v2 (полный user_* набор) exchanged to long-lived until 2026-10-29 and installed in all 4 store copies; the 2069030 "New Pages Experience" block found and worked around in fb_posts_poll.py (все чтения через me?fields=posts{...}); live proof (his real posts with reactions/shares, e.g. today's post 12:26 with 7 reactions/4 comments/1 share); first ingest 50 posts/50 snapshots; nightly collector will now feed metrics automatically; watchdog armed 14 days before expiry (one Generate-click from him then); honest limits: чужие тексты комментов API не отдаёт (только счётчики), постинг/комменты/лайки/Messenger личного профиля остаются браузерными навсегда — вариант Страницы за ним; напомнить, что fleet-ACK check + /retro идут следующими по его приказу ("Я проверил бы, чтобы на всём флоте это работало, и потом сделал бы ретро").

If you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: C:\Users\dev\.claude\projects\P---WORKDIR-HUB\s_ba41ce90.jsonl
Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.

---

**User:**

<local-command-caveat>Caveat: The messages below were generated by the user while running local commands. DO NOT respond to these messages or otherwise consider them in your response unless the user explicitly asks you to.</local-command-caveat>

---

**User:**

<command-name>/compact</command-name>
            <command-message>compact</command-message>
            <command-args></command-args>

---

**User:**

<local-command-stdout>Compacted PreCompact [python "C:\Users\dev\.claude\hooks\compact_guard_pre.py"] completed successfully</local-command-stdout>

---

**User:**

давай заведём Страницу и переведём постинг на API

---

**Claude:**

[⏰ воскресенье, день, 17:26, 30 августа 2026]

Отлично, это единственный путь увести постинг с браузера. Сначала гляну, что уже умеет наша рельса про Страницы, потом дам тебе клик-путь.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py"}

---

> `AskUserQuestion` -- {"questions": [{"question": "Как назвать Страницу FB? С неё роботы будут постить через API (посты уходят на Страницу, не на твою личную стену - это важно).", "header": "Имя Страницы", "multiSelect": false, "options": [{"label": "[ИМЯ] [ФАМИЛИЯ] (Recommended)", "description": "Личный бренд - совпад

---

**Claude:**

[⏰ воскресенье, день, 17:29, 30 августа 2026]

🎙 Майк: TonyDzi - хорошо, совпадает с рабочим @tonydzi в TG, единый бренд. Одно важное «но» держи в голове: посты Страницы НЕ попадают на твою личную стену, где живут твои друзья - Страница набирает свою аудиторию с нуля. Личная стена остаётся браузерной навсегда, это граница Meta.

Твои клики, всё в твоём Firefox (5 минут, два захода):

**Заход 1 - создать Страницу:**
1. Открой `facebook.com/pages/create`
2. Имя: **TonyDzi** · Категория: набери **Entrepreneur** (или Digital creator) · жми **Create Page**
3. Био и фото можно пропустить, это потом.

**Заход 2 - новый токен с правами на Страницу:**
4. Открой `developers.facebook.com/tools/explorer` (то же приложение **dev Metrics Reader**)
5. В Permissions добавь: **pages_show_list, pages_read_engagement, pages_read_user_content, pages_manage_posts, pages_manage_engagement** (набирай в поиске по одному)
6. Жми **Generate Access Token** → в попапе FB выбери Страницу **TonyDzi** → разреши всё
7. Скопируй токен и кинь его мне сюда.

Дальше всё сам: обменяю на long-lived, вытащу **бессрочный** page-токен (у Страниц токен не протухает - даже 60-дневное продление уйдёт в прошлое для постинга), положу в store, соберу постилку и сделаю тестовый пост на TonyDzi с живым доказательством.

🧒 Простыми словами: ты заводишь витрину с вывеской TonyDzi и даёшь роботу ключ от неё. Ключ от витрины вечный и официальный - Facebook сам его выдал, банить за него не будет. Робот сможет вешать посты на витрину без браузера. А вот к твоей личной стене ключей Facebook не делает ни для кого - туда по-прежнему только руками или через твой браузер.

[⏰ воскресенье, день, 17:29, 30 августа 2026]

---

**User:**

Смотри, я знаю, что если я не ошибаюсь, я могу собственно страничку проапгрейдить до бизнес-странички. Мне кажется, будет лучше. То есть я можем не называть отдельную бизнес-страницу, можем сделать мой профиль до бизнес-страницы, и тогда я сохраню своих подписчиков и так далее. Как ты на это смотришь? Мне кажется, так проще.

---

**Claude:**

[⏰ воскресенье, вечер, 18:09, 30 августа 2026]

Хорошая мысль, но тут есть подвох, который мы сегодня уже замерили живьём. Дай секунду, сверю с актуальной докой Meta, чтобы не гадать по памяти.

---

> `ToolSearch` -- {"query": "select:WebSearch", "max_results": 1}

---

> `WebSearch` -- {"query": "Facebook convert personal profile to business Page 2026 discontinued professional mode API posting"}

---

**Claude:**

[⏰ воскресенье, вечер, 18:11, 30 августа 2026]

🎙 Майк: идея красивая, но этой двери у Meta больше нет - и вот тебе улика с нашего же сегодняшнего замера: твой профиль **уже** в professional-режиме, и именно поэтому API отбивал нам чтение стены ошибкой «New Pages Experience Is Not Supported». То есть апгрейд, о котором ты говоришь, у тебя давно включён - а постинг через API он не открыл и не откроет.

Разбираю по фактам:

1. **Кнопки «превратить профиль в Страницу» больше не существует.** Meta убрала прямую конвертацию; сейчас есть только два разных инструмента: professional mode (остаёшься профилем) и создание отдельной Страницы. [Meta Help](https://www.facebook.com/business/help/1608528132896450) это прямо разводит: «Professional mode does not turn a profile into a Page».
2. **Professional mode = всё ещё профиль в глазах API.** Постинг закрыт для любых профилей с 2018 года, режим не важен. Мы это сегодня проверили живьём: `POST /me/feed` с твоим токеном отвечает «You can't perform this operation on this endpoint».
3. **Подписчики никуда не мигрируют** ни при каком варианте: инструмент переноса аудитории профиль→Страница умер вместе с конвертацией.

Так что развилка реальная только одна, и она та же, что час назад:
- **Личная стена с твоими подписчиками** - постим как раньше, браузером (теперь аккуратным: роботы больше не трогают логины, война за сессию закончена).
- **Страница TonyDzi** - единственное место, куда Facebook пускает API-постинг. Она добавляется в каскад как ещё одно зеркало: тот же пост уходит и на стену (браузер), и на Страницу (API, без рисков бана).

Мой вердикт: заводим TonyDzi по плану из прошлого сообщения (7 кликов), теряем ноль подписчиков, получаем официальную API-трубу. Переубеди меня, если видишь что-то, чего я не вижу - но дока и живой замер оба на этой стороне.

🧒 Простыми словами: ты думал, что личную страничку можно «повысить до магазина» и все друзья перейдут с ней. Раньше так было можно, теперь Facebook эту кнопку убрал совсем. Твоя страничка и так уже в «профессиональном режиме» - мы сегодня в это упёрлись носом - но роботу писать на неё всё равно нельзя. Магазин придётся открыть отдельно, зато друзья никуда не денутся.

Sources: [Meta Business Help: professional mode vs Page](https://www.facebook.com/business/help/1608528132896450) · [Meta Help: pro mode](https://www.facebook.com/help/2978174759158711) · [Multilogin: professional mode 2026](https://multilogin.com/blog/mobile/what-is-facebook-professional-mode/)

[⏰ воскресенье, вечер, 18:12, 30 августа 2026]

---

**User:**

тесты и ретро

---

**Claude:**

You've hit your session limit · resets 2am (Europe/London)

---

**User:**

Try again

---

**Claude:**

[⏰ суббота, ночь, 02:01, 5 сентября 2026]

Принял: сперва прогоняю /tt по собранному (FB Graph рельса), потом /retro. Кстати, уже 2 часа ночи - после тестов и ретро гони себя спать, работа никуда не денется.

---

> `Skill` -- {"skill": "tt", "args": "FB Graph API рельса: fb_token_rail.py + fb_posts_poll.py (обход 2069030) + ingest"}

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


ARGUMENTS: FB Graph API рельса: fb_token_rail.py + fb_posts_poll.py (обход 2069030) + ingest

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py status; python C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py check", "description": "FB token status + auth check"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\_test_fb_token_rail.py", "description": "Run FB rail regression test"}

---

> `PowerShell` -- {"command": "$reg = \"D:\\Vault\\_imports\\content-factory\\registry\"; Get-ChildItem $reg\\fb_metrics.json | Select-Object Name,LastWriteTime; Get-ChildItem $reg\\*.db | Select-Object Name,LastWriteTime", "description": "Check fb_metrics.json and registry DB freshness"}

---

> `PowerShell` -- {"command": "Get-Content \"D:\\Vault\\_imports\\content-factory\\registry\\collect_pub_metrics.cmd\"; python -c \"import sqlite3; c=sqlite3.connect(r'D:\\Vault\\_imports\\content-factory\\registry\\pubmetrics.db'); [print(r) for r in c.execute(\\\"select name from sqlite_master where type='tab

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\fb_db_probe.py", "content": "import sqlite3\nc = sqlite3.connect(r\"D:\\Vault\\_imports\\content-factory\\registry\\pubmetrics.db\")\ntabs = [r[0] for r i

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\fb_db_probe.py\"", "description": "Probe pubmetrics.db for FB snapshot freshness"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\fb_db_probe2.py", "content": "import sqlite3\nc = sqlite3.connect(r\"D:\\Vault\\_imports\\content-factory\\registry\\pubmetrics.db\")\nprint(\"pub cols:\"

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_ba41ce90\\scratchpad\\fb_db_probe2.py\"", "description": "Verify FB rows in daily snapshots"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\help_flag_lint.py --check C:\\Users\\dev\\.claude\\scripts\\fb_token_rail.py; echo \"rc=$LASTEXITCODE\"; python C:\\Users\\dev\\.claude\\scripts\\help_flag_lint.py --check C:\\Users\\dev\\.claude\\scripts\\fb_posts_poll.py; echo \"rc=$LAS

---

> `PowerShell` -- {"command": "$log=\"C:\\Users\\dev\\.claude\\scripts\\cc-review\\bridge-state\\usage.jsonl\"; if (Test-Path $log) { Select-String -Path $log -Pattern \"fb\" | Select-Object -Last 6 | ForEach-Object { $_.Line.Substring(0, [Math]::Min(240, $_.Line.Length)) } } else { echo \"no usage.jsonl at $log\" 

---

**Claude:**

Улики второго мнения есть: панель 30.08 (5 находок, все починены - живут брейк-кейсами в секции 5 теста) плюс свежая панель 04.09 по задаче `fb-rail-and-freshness-roots` - 6 движков (codex/grok/gemini × 2 рельсы), все отработали. Повторно жечь панель на неизменённом коде не буду (§10.0).

## Вердикт /tt - FB Graph рельса

| Что проверено | Как (живой вывод) | Итог |
|---|---|---|
| Токен жив | `status`: OK, до 2026-10-29 (54д), полный user_* набор | ✅ |
| Авторизация | `check`: AUTH OK, [ИМЯ] [ФАМИЛИЯ], id 28812850...795 | ✅ |
| Регресс-тест | `_test_fb_token_rail.py`: GREEN, все кейсы (вкл. 5 находок панели 30.08 как брейк-кейсы) | ✅ |
| Сквозной путь 6 суток | pubmetrics.db: `fb_wall` по 25 снапшотов КАЖДУЮ ночь 31.08-04.09, свежайший 04.09 03:43 с живыми лайками/шерами | ✅ |
| Обход 2069030 | работает в проде: метрики едут через `me?fields=posts{...}` | ✅ |
| CLI-гейт флагов | fb_token_rail чисто; fb_posts_poll - дыра старая, заморожена в baseline (не наш долг) | ✅ |
| Второе мнение | панель 30.08 + панель 04.09 (6 движков, usage.jsonl) | ✅ |
| Сторож | oauth_probe EXPIRY_STORES, крик за 14 дней; маркер FB_RAIL_ENABLED_AT стоит | ✅ |
| Тест+док+счётчик | docstring с updated в обоих файлах; `_fb_token_rail_usage.jsonl` пишет исходы | ✅ |
| Флот | NOTFORME для пиров: FB-работа по канону с хаба (§7.2 IP-sensitive), секреты и скрипты доезжают синком | ✅ |

**Итог: ✅ PASS.** Гейт льстящего вывода: вывод «всё зелёное» мне выгоден → независимая улика сверх моих прогонов есть - 5 ночей автономной работы трубы, которые породила не эта сессия, плюс чужая панель 04.09. 🌍 share-fix: обход 2069030 уже был кандидатом на раздачу - проверю в ретро, ушёл ли он в share_fix_queue. 📋 Журнал: карточка task-2026-07-11 закрыта 30.08 с этим же доказательством.

Теперь ретро:

---

> `Skill` -- {"skill": "retro"}

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
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
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
- `python ~/.claude/scripts/memory_epistemic.py --lint` → `SELF-TOMBSTONE` (заметка сама пишет, что устарела, а машина этого не видит) закрыть тем же заходом: `--close <слаг> --superseded-by <слаг-преемника>`. Отмена закрывается ПОЛЯМИ (`status`/`valid_to`/`superseded_by`/`refuted_on`/`refuted_by`) во ВСЕХ копиях слага, а не переписыванием одной: CLAUDE.md §8.4-бис + [[memory-records-close-by-fields-not-rewrite]].
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже) и на каждую — ОДНА строка ЧЕРЕЗ ДВЕРЬ `python ~/.claude/scripts/selfheal.py journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Затем СЧЁТЧИК по классу — **не грепом по имени, а прибором** (замер 03.09.2026: в журнале 503 пронумерованных случая, из них **299 записаны как «1-й датированный»**, уникальных слагов всего 72; счёт вёлся по ИМЕНИ, имя сочинялось заново под каждую поломку, и порог «третьей поломки» был структурно недостижим — семья «вывод по одной поверхности» набрала 72 случая с 27.07 и ни разу не дошла до 3):
```
python ~/.claude/scripts/prior_art.py class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный → отдельная сессия починки** (5 почему по серии → ТРИЗ → АК-47). Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым». Канон: память `class-counted-by-name-never-reaches-three` + CLAUDE.md §5.10.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · fail-closed гейты.
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
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]). Then classify:
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
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

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
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` = сейчас + 1-2 мин, разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro).

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 кандидата/ночь, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].
**⭐ Мини-тизер обязателен (dev 01.09):** every retro with a substantive arc births ≥1 mini-teaser (200-250 chars, «грабли → правило» so the READER gets use, not a status report) → `python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук>" --note "<тизер>" --tier teaser`. Verdict «no teaser» is legal ONLY with a named reason (empty routine session). Canon: `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`.

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
Write a clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- The nightly **Brain Reindex @04:00** makes it `/ask`-searchable — no manual reindex needed.

**6a-бис. Снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- Команда: `python %USERPROFILE%\.claude\scripts\retro_lost_scan.py mark-done <sessionId> --note "ретро: <имя заметки>"`
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6a-тер. Переименуй сессию: префикс «Р+» в видимом имени — СРАЗУ после 6a-бис** (⭐ dev 02.09.2026, голосом: «когда я вижу Р+, я понимаю, что дошёл в этой сессии до крупного milestone»).
- Вызови `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → возьми текущий `title`. Если он УЖЕ начинается с `Р+`/`р+`/`рр+` — шаг закрыт, второй префикс не лепить.
- Иначе `mcp__ccd_session_mgmt__set_session_title` с `session_id: "self"` и `title: "Р+<старое имя без изменений>"`. Меняется ТОЛЬКО человекочитаемое имя в приложении (titleSource=tool), системный id не трогается; имя, данное оператором, сохраняется целиком после префикса.
- MCP session_mgmt недоступен (headless `claude -p`, чужой харнес) → одна строка в отчёте «Р+ не поставлен: нет session_mgmt», не молчи.

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

---

> `PowerShell` -- {"command": "Get-ChildItem \"D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\" | Where-Object { $_.LastWriteTime -gt \"2026-08-30\" } | Where-Object { $_.Name -match \"fb|graph|logout|chrome|browser\" } | Select-Object Name,LastWriteTime", "description": "Related retros since 30.08"}

---

> `PowerShell` -- {"command": "Select-String -Path \"D:\\Vault\\Vault-Knowledge\\_outreach\\share_fix_queue.jsonl\" -Pattern \"2069030|fb\" | ForEach-Object { $_.Line.Substring(0,[Math]::Min(200,$_.Line.Length)) }; echo \"---tasks---\"; Get-ChildItem \"D:\\Vault\\Vault-Knowledge\\10-Tasks\" -Filter \"*fb*\" | S

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-08-30-fb-graph-token-rail.md", "limit": 60}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\prior_art.py class \"Meta professional-mode профиль отбивает прямые эндпоинты чтения стены, обход через field-expansion\"", "description": "Check breakage family for 2069030 class"}

---

> `PowerShell` -- {"command": "python D:\\Vault\\_imports\\content-factory\\content_miner.py capture --title \"Facebook сам закрыл нам дверь, которую сам же выдал\" --note \"Дал роботу официальный ключ читать мою стену через API - а API ответил 'New Pages Experience Is Not Supported'. Профиль в professional-режиме

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\selfheal.py journal --class fb-api-endpoint-blocked-professional-mode --what \"GET /me/posts и /me/feed для профиля в professional-режиме Meta отбиваются 400/code 200/subcode 2069030 'New Pages Experience Is Not Supported' при валидном токене с

---

> `PowerShell` -- {"command": "Add-Content -Encoding utf8 \"D:\\Vault\\Vault-Knowledge\\_outreach\\share_fix_queue.jsonl\" '{\"added\": \"2026-09-05\", \"from\": \"retro hub dc7f8c3a fb-graph-rail\", \"artifact\": \"workaround for Graph API error subcode 2069030 New Pages Experience Is Not Supported on /me/posts /

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-05-fb-page-tonydzi-api-posting.md", "content": "---\nid: task-2026-09-05-fb-page-tonydzi-api-posting\ntitle: \"FB Страница TonyDzi: создать + pages_* токен → перевести постинг на API\"\nstate: open\ntype: infra\npriority: P1\nowner

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-05-fb-page-tonydzi-api-posting.md", "content": "---\nid: task-2026-09-05-fb-page-tonydzi-api-posting\ntitle: \"FB Страница TonyDzi: создать + pages_* токен → перевести постинг на API\"\nstate: open\ntype: infra\npriority: P1\nowner

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-07-11-fb-graph-token-enable.md", "old_string": "Ограничение платформы: тексты чужих комментов API не отдаёт (только счётчики) — комментинг/постинг личного профиля остаётся браузерным навсегда ([[fb-personal-profi

---

**Claude:**

Теперь заметка-ретро в волт (дельта моей сессии, с кросс-линком на ретро строителя):

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-09-05-fb-graph-rail-live-enable-tonydzi.md", "content": "---\ntitle: \"Retro: FB Graph рельса оживлена насквозь + решение TonyDzi (живая сессия хаба)\"\naliases: [\"Ретро 05.09.2026 — FB Graph рельса живьём + 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-09-05-fb-page-tonydzi-api-posting.md", "old_string": "related: [\"[[task-2026-07-11-fb-graph-token-enable]]\", \"fb_token_rail.py (команда pages готова)\", \"память fb-personal-profile-api-limits\"]", "new_string

---

**Claude:**

Снимаю сессию с очереди догонялки и ставлю Р+ в имя:

---

> `PowerShell` -- {"command": "python $env:USERPROFILE\\.claude\\scripts\\retro_lost_scan.py mark-done s_ba41ce90 --note \"ретро: retro-2026-09-05-fb-graph-rail-live-enable-tonydzi.md\"", "description": "Mark session retro done for retro-lost scanner"}

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "Р+!!!FB!!! Постоянные разлогинивания браузера"}

---

**Claude:**

[⏰ суббота, ночь, 02:09, 5 сентября 2026]

## 🎬 Сегодня мы поняли (ретро сессии 30.08 → /tt 05.09)

1. Рельса FB Graph прожила **5 ночей без единого человека**: по 25 снапшотов метрик каждую ночь 31.08-04.09 - это и есть настоящее доказательство, а не «в день сборки работало».
2. Грабля 2069030 (professional-режим закрывает прямое чтение стены) починена классом и уже поставлена в очередь раздачи миру - симптом гуглится, страдальцы есть.
3. «Апгрейд профиля до бизнес-страницы» - миф: Meta убрала конвертацию, постинг личного профиля закрыт навсегда. Единственная дверь - отдельная Страница **TonyDzi** (имя ты выбрал 30.08).

🎙 Майк: 💰 лейн FB - главная дверь к твоей аудитории, чтение уже без браузера и без риска бана. 🔪 убил бы: 6 дней карточка TonyDzi не существовала - решение было принято голосом и чуть не утонуло в транскрипте, теперь она в реестре. 🤺 спорил честно: твою идею с апгрейдом профиля опроверг докой и живым замером, не поддакнул. ❓ вопрос: 7 кликов на TonyDzi сделаешь на выходных? Без них постинг так и живёт в браузере.

**/tt: ✅ PASS** (таблица выше). **Ретро закрыто:** заметка в волте, 🩹 строка 2069030 в журнал через дверь, 🌍 обход в share_fix_queue, 🎬 тизер в воронку, 📋 +1 карточка [[task-2026-09-05-fb-page-tonydzi-api-posting]] (ждёт твоих 7 кликов, ревью 12.09), догонялка отмечена, сессия переименована в Р+. ⛳ дрифта нет. Флот: NOTFORME для пиров (FB - хаб).

➤ Скопируй блок целиком и вставь следующим сообщением (если остаёшься в сессии; уходишь - всё уже в волте):

```
/compact Сожми по 7 заголовкам (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ), русским языком, факты не выдумывать.
РЕШЕНИЯ: FB-постинг через API = только Страница TonyDzi (dev 30.08); конвертация профиль→Страница у Meta не существует, professional mode ≠ Page (опровергнуто докой+замером); чтение FB навсегда через field-expansion me?fields=posts{...} (обход 2069030), прямые /me/posts не чинить.
TODO: TonyDzi - 7 кликов оператора (facebook.com/pages/create + Graph Explorer с pages_show_list/read_engagement/read_user_content/manage_posts/manage_engagement) → мне токен → exchange → fb_token_rail.py pages → FB_PAGE_TOKEN/FB_PAGE_ID в store (патч FIELDS) → fb_page_post.py + тестовый пост + /tt; карточка task-2026-09-05-fb-page-tonydzi-api-posting (review 12.09). Продление user-токена 29.10: сторож oauth_probe крикнет за 14д, 1 клик Generate + exchange.
СЕЙЧАС: /tt ✅ PASS и ретро закрыты 05.09 02:0x (заметка retro-2026-09-05-fb-graph-rail-live-enable-tonydzi.md, retro_lost mark-done, сессия Р+).
ПУТИ И ЗНАЧЕНИЯ: fb_graph.env в 4 копиях store (канон C:\Users\dev\.claude\secrets); app dev Metrics Reader 1655895462767856; токен long-lived до 2026-10-29, полный user_*, pages_* НЕТ; fb_token_rail.py (exchange|install|status|pages|where, значения через stdin), fb_posts_poll.py::_me_posts, _test_fb_token_rail.py GREEN.
СЧЁТЧИКИ: ingest 30.08 = 50 постов/50 снапшотов; ночной collect_pub_metrics = 25 снапшотов fb_wall каждую ночь 31.08-04.09 без пропусков (pubmetrics.db); токену осталось 54д.
ОТКРЫТО: тексты чужих комментов API не отдаёт (только счётчики, приватность Meta) - fb-reply остаётся браузерным; share_fix_queue строка 2069030 pending (раздаст share-fix-daily); подписчики профиля на Страницу не мигрируют.
ИНСТРУМЕНТЫ И КОНТРАКТЫ: fb_token_rail install --field X значение по stdin; статусы OK/EXPIRING/DEAD/DORMANT/INCOMPLETE (маркер FB_RAIL_ENABLED_AT); page-токен из long-lived user = бессрочный; FB-работа только с хаба (§7.2).
```

🧒 Простыми словами: мы устроили built-вещи экзамен. Робот-почтальон, которого собрали неделю назад, все пять ночей сам приносил цифры с твоей стены - экзамен сдан на пятёрку. Урок про обход запертой двери Facebook мы записали в дневник и поставили в очередь «рассказать другим людям в интернете, у кого та же беда». Осталась одна недоделка, и она за тобой: семь кликов, чтобы открыть витрину TonyDzi - тогда робот сможет ещё и вешать посты, а не только читать. А теперь - спать, третий час ночи!

[⏰ суббота, ночь, 02:10, 5 сентября 2026]
