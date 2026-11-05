---
session: s_96dfa95f
date: 2026-10-28
words: 1154
turns: 3
tools: "Bash, ToolSearch, mcp__ccd_session_mgmt__set_session_title, mcp__scheduled-tasks__create_scheduled_task, mcp__scheduled-tasks__update_scheduled_task"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · Scheduled run: auto-hub-261028-competitor-agentdock

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_96dfa95f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261028-competitor-agentdock" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261028-competitor-agentdock\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первым действием: mcp__ccd_session_mgmt__set_session_title(session_id="self", title="🎯 · 🧩📋 Конкурент: AgentDock · ДР + вклад").

Заказ оператора 28.10.2026 (дословно): «по поводу конкурентов, да, иди на их гитхабы, смотри, что они делают, и контрибьютим то, что у нас есть, и то, что как-то пересекается с тем, что они делают, и мы делаем. Плюс изучай их все тоже, делай на них DR-ы отдельными сессиями и на каждого из них... и думай, что у них тоже за это полезного».

Твой конкурент: AgentDock — новичок 2026: «self-hosted control plane for Claude Code agents… with a board, designs, budgets, approvals and Telegram, across your repos and machines» (PR #366, смержен 2026-10-15). По смыслу ближе всех к нашей связке шина + lease + Telegram. Найди репо (точное имя/владельца), лицензию, звёзды, мейнтейнеров.
Контекст: сессия H67518 (хаб HUB-01) нашла его в топ-5 конкурентов нашей связки (флот ~8 машин, Claude Code + Codex + Grok + Cursor, шина aibus + Telegram workroom, workspace_write_lease, роли, approval.py/QQQ аски, бюджеты plan_budget). Отчёт-основание: D:\Vault\_originals\deep-research\DR26-10-27-HUB-04-1451-openflow-competitors-claudeai-extra-leg.md (раздел Top 5).

Шаги:
1. RECALL: brain_ask.py "AgentDock control plane Claude Code" + grep памяти.
2. ДР: dr_registry.py new, затем /dr-fanout (браузерные рельсы, кворум 4/6, дедуп до старта). Вопрос: что умеют, куда идут, где пересекаются с нами (Telegram-аски, бюджеты, approvals, multi-machine), что взять, где мы сильнее (мультивендорность Codex/Grok/Cursor).
3. GitHub: ищи, где наш опыт даёт ПОЧИНКУ (Windows, Telegram-грабли, multi-machine, lease). Правила CLAUDE.md §4.7: починка по существующему issue, фича только по приглашению мейнтейнера; <1000★ и не корпоративный → можно ссылку github.com/tonydzi (gh_pr_discipline.py sign-check решает); ≤2 наших открытых PR; one-pr/feature-gate, /outbound-gate. Маленький живой репо = шанс стать своим через ревью чужих PR (§4.7, ревью = баг/риск с file:line). Нет двери — честно.
4. Итог оператору в чат этой сессии: вердикт «что у них полезно нам» (≤10 строк), ссылки ДР-ног, PR/комменты с URL, applied/parked ДР, insight в 03-Insights. Подпись machine_stamp.py sig. Tier-2 → стоп и аск. Блок «🧒 Простыми словами».
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title,WebFetch,WebSearch", "max_results": 3}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🎯 · 🧩📋 Конкурент: AgentDock · ДР + вклад"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && timeout 90 python brain_ask.py \"AgentDock control plane Claude Code\" 2>&1 | head -40; grep -ril \"agentdock\" /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/ 2>/dev/null | head; grep -n -i -A3 \"agentdock\" \"/e/Obsidian/_originals/deep-

---

> `Bash` -- {"command": "gh repo view VeselyBegma/AgentDock --json name,description,stargazerCount,forkCount,licenseInfo,pushedAt,createdAt,isArchived,owner,homepageUrl,primaryLanguage 2>&1; gh api repos/VeselyBegma/AgentDock/contributors --jq '.[]|\"\\(.login) \\(.contributions)\"' 2>&1|head; gh issue list -R 

---

> `Bash` -- {"command": "cd /tmp; for i in 259 260 261 262; do gh issue view $i -R VeselyBegma/AgentDock --json title,body,comments --jq '\"=== \\(.title)\\n\\(.body[:700])\\n--c: \\([.comments[]|.author.login+\": \"+.body[:300]]|join(\" | \"))\"'; done; gh pr diff 1054 -R VeselyBegma/AgentDock 2>&1 | grep -n -

---

> `Bash` -- {"command": "gh pr diff 1054 -R VeselyBegma/AgentDock > /c/Users/dev/AppData/Local/Temp/pr1054.diff; grep -n \"^+++ \" /c/Users/dev/AppData/Local/Temp/pr1054.diff; grep -n -E \"kill\\(|detached|SIGKILL|SIGTERM|-pid|win\" /c/Users/dev/AppData/Local/Temp/pr1054.diff | head -40; gh pr view 1054 -

---

> `Bash` -- {"command": "sed -n 944,1004p /c/Users/dev/AppData/Local/Temp/pr1054.diff; gh api repos/VeselyBegma/AgentDock/contents/README.md --jq .content | base64 -d | grep -n -i -E \"windows|macos|linux|tmux|wsl\" | head", "description": "Read exec.ts change and platform notes"}

---

> `Bash` -- {"command": "sed -n 729,760p /c/Users/dev/AppData/Local/Temp/pr1054.diff; sed -n 1593,1666p /c/Users/dev/AppData/Local/Temp/pr1054.diff | head -75; gh pr view 1054 -R VeselyBegma/AgentDock --json headRefOid,comments --jq '.headRefOid, (.comments[]|.author.login+\": \"+.body[:400])'", "descriptio

---

> `Bash` -- {"command": "which bun wsl 2>&1; bun --version 2>&1; ssh -o ConnectTimeout=5 -o BatchMode=yes root@fleet-anchor \"which bun; uname -a\" 2>&1 | head -3; grep -o '\"[A-Za-z0-9_-]*\": *{[^}]*\"host\"[^}]*}' ~/.claude/fleet_nodes.json 2>/dev/null | head -3", "description": "Look for a Bun runtime to rep

---

> `Bash` -- {"command": "timeout 60 wsl -e bash -lc \"which bun node npm npx; ls ~/.bun/bin 2>/dev/null\" 2>&1 | head", "description": "Check WSL for bun or node"}

---

> `Bash` -- {"command": "mkdir -p /c/Users/dev/AppData/Local/Temp/claude/bunrepro && cd /c/Users/dev/AppData/Local/Temp/claude/bunrepro && cat > repro.ts <<'EOF'\n// Mirrors createExec in PR #1054: Bun.spawn + proc.kill('SIGKILL') on abort,\n// then await stdout/stderr text and exited. Child is a shell that

---

> `Bash` -- {"command": "cd /c/Users/dev/AppData/Local/Temp/claude/bunrepro && cat > fix.ts <<'EOF'\nconst run = async (label: string, spawnOpts: any, kill: (p: any) => void) => {\n  const t0 = Date.now();\n  const proc = Bun.spawn(['/bin/sh', '-c', 'sleep 30; echo done'], { stdout: 'pipe', stderr: 'pipe', ..

---

> `Bash` -- {"command": "gh api \"repos/VeselyBegma/Nautelle/contents/apps/runner/src/detect/exec.ts?ref=217a975a72e25a7222725ab25a5d21d62a4c86a5\" --jq .content | base64 -d | grep -n -E \"Bun.spawn|proc.kill|new Response\\(proc.stdout|killSignal\" ; gh api \"repos/VeselyBegma/Nautelle/contents/apps/runner/src/

---

> `Bash` -- {"command": "python ~/.claude/scripts/gh_pr_discipline.py sign-check VeselyBegma/Nautelle 2>&1 | tail -5; python ~/.claude/scripts/gh_pr_discipline.py silence VeselyBegma/Nautelle 2>&1 | tail -4; python ~/.claude/scripts/machine_stamp.py sig --model \"Opus 5.5\" 2>&1", "description": "Run signature 

---

> `Bash` -- {"command": "cat > /c/Users/dev/AppData/Local/Temp/claude/bunrepro/review.md <<'EOF'\nMycroft here, a synthetic AI co-founder working with dev. I review process trees for a living, so naturally I came looking for orphans.\n\n**Risk: the abort kills the direct child only, and the call can still h

---

> `Bash` -- {"command": "ls ~/.claude/skills/dr-fanout/; grep -n -i -E \"^#|python .*\\.py\" ~/.claude/skills/dr-fanout/SKILL.md | head -40; python ~/.claude/scripts/dr_registry.py --help 2>&1 | head -15", "description": "Read dr-fanout skill entry points"}

---

**Claude:**

Ревью опубликовано. Теперь регистрирую ДР и ищу в скилле dr-fanout запуск одной командой.

---

> `Bash` -- {"command": "sed -n 10,70p ~/.claude/skills/dr-fanout/SKILL.md", "description": "Read dr-fanout current canary section"}

---

> `Bash` -- {"command": "ls ~/.claude/scripts/dr_start.py /e/Obsidian/_imports/dr_start.py 2>&1; python ~/.claude/scripts/dr_start.py --help 2>&1 | head -30 || python /e/Obsidian/_imports/dr_start.py --help 2>&1 | head -30; python /e/Obsidian/_imports/dr_registry.py list 2>&1 | grep -i -E \"agentdock|nautelle\"

---

> `Bash` -- {"command": "set -o pipefail; ls ~/.claude/scripts/dr_start.py /e/Obsidian/_imports/dr_start.py 2>&1; python /e/Obsidian/_imports/dr_start.py --help 2>&1 | head -30; python /e/Obsidian/_imports/dr_registry.py list 2>&1 | grep -i -E \"agentdock|nautelle\" | head", "description": "Check dr_start usage

---

> `Bash` -- {"command": "cat > /c/Users/dev/AppData/Local/Temp/claude/bunrepro/dr_prompt.md <<'EOF'\nDeep Research: Nautelle (formerly AgentDock), github.com/VeselyBegma/Nautelle, homepage nautelle.luna-realm.com. MIT, TypeScript/Bun, created 2026-10-07, solo maintainer, ~2700 commits, 1 star as of 2026-10-28

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__create_scheduled_task", "max_results": 1}

---

> `Bash` -- {"command": "date -u +%Y-%m-%dT%H:%M:%SZ; date -u -d '+3 min' +%Y-%m-%dT%H:%M:%S+00:00", "description": "Get current UTC time for fireAt"}

---

**Claude:**

ДР DR26-10-28-HUB-12-1807 заведён, ставлю видимую сессию-исполнитель для браузерных ног.

---

> `mcp__scheduled-tasks__create_scheduled_task` -- {"taskId": "auto-hub-261028-dr-runner-nautelle", "title": "🔬 · 🧩📋 ДР Nautelle/AgentDock · DR26-10-28-HUB-12-1807", "description": "AUTO-HUB-261028-dr-runner: браузерный веер ДР DR26-10-28-HUB-12-1807 (Nautelle/AgentDock)", "fireAt": "2026-10-28T18:10:33+00:00", "notifyOnCompletion": true, "prompt": 

---

> `Bash` -- {"command": "python ~/.claude/scripts/_shared/fireat_now.py --in 3; head -12 ~/.claude/scheduled-tasks/intern-fellows-lane-20261002/SKILL.md", "description": "Get fireAt from door and inspect slot frontmatter"}

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__update_scheduled_task", "max_results": 1}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "intern-fellows-lane-20261002", "title": "🔬 · 🧩📋 ДР Nautelle/AgentDock · DR26-10-28-HUB-12-1807", "description": "ДР-исполнитель: браузерный веер DR26-10-28-HUB-12-1807 (конкурент Nautelle/AgentDock)", "fireAt": "2026-10-28T18:22:54Z", "notifyOnCompletion": true, "prompt": "ПЕРВЫМ ДЕЛОМ п

---

> `Bash` -- {"command": "sed -i 's/^model: claude-sonnet-5-5$/model: claude-opus-5-5/' ~/.claude/scheduled-tasks/intern-fellows-lane-20261002/SKILL.md; head -5 ~/.claude/scheduled-tasks/intern-fellows-lane-20261002/SKILL.md", "description": "Set slot model to Opus for DR orchestration"}
