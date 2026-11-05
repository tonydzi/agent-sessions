---
session: s_73a90ed4
date: 2026-10-28
words: 915
turns: 3
tools: "Bash, ToolSearch, Write, mcp__ccd_session_mgmt__get_usage, mcp__ccd_session_mgmt__set_session_title, mcp__scheduled-tasks__create_scheduled_task, mcp__scheduled-tasks__update_scheduled_task"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · Scheduled run: auto-hub-261028-competitor-mastra

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_73a90ed4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-261028-competitor-mastra" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-261028-competitor-mastra\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первым действием: mcp__ccd_session_mgmt__set_session_title(session_id="self", title="🎯 · 🧩🏗 Конкурент: Mastra · ДР + вклад").

Заказ оператора 28.10.2026 (дословно): «по поводу конкурентов, да, иди на их гитхабы, смотри, что они делают, и контрибьютим то, что у нас есть, и то, что как-то пересекается с тем, что они делают, и мы делаем. Плюс изучай их все тоже, делай на них DR-ы отдельными сессиями и на каждого из них... и думай, что у них тоже за это полезного».

Твой конкурент: Mastra — TypeScript-фреймворк агентов, Apache-2.0, Studio, трассировка, evals, MCP (Show HN 2026-01, ~28.5k★, github.com/mastra-ai/mastra). Лучшая основа, если мы когда-то строим свой UI флота.
Контекст: сессия H67518 (хаб HUB-01) нашла его в топ-5 конкурентов нашей связки (флот ~8 машин, Claude Code + Codex + Grok + Cursor, шина aibus, lease, роли, MCP-серверы telegram/whatsapp/codeindexer, evals). Отчёт-основание: D:\Vault\_originals\deep-research\DR26-10-27-HUB-04-1451-openflow-competitors-claudeai-extra-leg.md (раздел Top 5).

Шаги:
1. RECALL: brain_ask.py "Mastra agent framework" + grep памяти (gh search prs --author tonydzi repo:mastra-ai/mastra: не было ли наших PR).
2. ДР: dr_registry.py new, затем /dr-fanout (браузерные рельсы, кворум 4/6, дедуп до старта). Вопрос: что умеют, куда идут, где пересекаются с нами (MCP, evals, Windows, мультивендор), что взять нам, где мы сильнее.
3. GitHub: репо ≥1000★ → строго CLAUDE.md §4.7: только ПОЧИНКА по существующему issue (метки bug / good first issue / help wanted, Windows/MCP-грабли — наш опыт), фича только по явному приглашению, подпись только имя без ссылок на нашу работу, ≤2 наших открытых PR, gh_pr_discipline.py one-pr/sign-check/feature-gate, /issue-match до кода, /outbound-gate перед отправкой. Подписать CLA/DCO, если требуют — сами. Прочитай их CONTRIBUTING/AGENTS.md до правки.
4. Итог оператору в чат этой сессии: вердикт «что у них полезно нам» (≤10 строк), ссылки ДР-ног, PR/комменты с URL, applied/parked ДР, insight в 03-Insights. Подпись machine_stamp.py sig. Tier-2 → стоп и аск. Блок «🧒 Простыми словами».
</scheduled-task>

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🎯 · 🧩🏗 Конкурент: Mastra · ДР + вклад · H88589"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports; timeout 90 python brain_ask.py \"Mastra agent framework\" 2>&1 | head -40; echo \"---PRS\"; gh search prs --author tonydzi --repo mastra-ai/mastra --json url,title,state 2>&1 | head; echo \"---ISSUES\"; gh search issues --author tonydzi --repo mastra-ai/mastra -

---

**Claude:**

Пока RECALL идёт, смотрю репо Mastra и его открытые issue.

---

> `Bash` -- {"command": "gh repo view mastra-ai/mastra --json stargazerCount,licenseInfo,pushedAt,description 2>&1; echo ---; for L in \"bug\" \"good first issue\" \"help wanted\"; do echo \"== $L\"; gh issue list -R mastra-ai/mastra --label \"$L\" --state open --limit 30 --json number,title,comments,updatedAt,

---

> `Bash` -- {"command": "for Q in \"windows in:title\" \"win32\" \"MCP in:title\" \"path windows\"; do echo \"== $Q\"; gh issue list -R mastra-ai/mastra --state open --search \"$Q\" --limit 20 --json number,title,comments,updatedAt,labels,author --jq '.[] | \"\\(.number)\\t\\(.comments|length)\\t\\(.updatedAt[:

---

> `Bash` -- {"command": "gh issue view 27301 -R mastra-ai/mastra --comments 2>&1 | head -80; echo ======; gh pr list -R mastra-ai/mastra --state all --search \"27301\" --json number,title,state,author 2>&1", "timeout": 60000}

---

> `Bash` -- {"command": "gh api repos/mastra-ai/mastra/contents/CONTRIBUTING.md --jq .content 2>/dev/null | base64 -d | head -120", "timeout": 60000}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_73a90ed4/tasks/b3smp12s0.output\" | head -60; node -v; pnpm -v; git --version"}

---

> `Bash` -- {"command": "grep -n -i -B2 -A4 mastra \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/agent-memory-class-is-our-hiring-lane.md\" | head -30; echo ---; python ~/.claude/scripts/dr_registry.py --help 2>&1 | head -30; echo ---; python ~/.claude/scripts/dr_registry.py list 2>&1 | 

---

> `Bash` -- {"command": "f=$(ls ~/.claude/skills/dr-fanout/SKILL.md); wc -c $f; grep -n -E \"dr_start|dr_registry.py new|^## |^### \" $f | head -60"}

---

> `Bash` -- {"command": "sed -n 10,70p ~/.claude/skills/dr-fanout/SKILL.md"}

---

> `Bash` -- {"command": "ls $HOME/.claude/scripts/dr_start.py /e/Obsidian/_imports/dr_start.py 2>&1; python /e/Obsidian/_imports/dr_start.py --help 2>&1 | head -40 || python ~/.claude/scripts/dr_start.py --help 2>&1 | head -40"}

---

> `Bash` -- {"command": "ls $HOME/.claude/scripts/dr_start.py /e/Obsidian/_imports/dr_start.py 2>&1; python /e/Obsidian/_imports/dr_start.py --help 2>&1 | head -50  # pipe-rc-ok: help only"}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_73a90ed4\\scratchpad\\dr-mastra-prompt.md", "content": "# Deep Research: Mastra (mastra-ai/mastra) as a competitor and reference for a multi-vendor agent fleet\n\nUse your stronge

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python dr_start.py \"Mastra (mastra-ai/mastra): что умеют, куда идут, пересечение с флотом (MCP, evals, Windows, мультивендор), что взять, где мы сильнее, основа UI флота\" --for \"решение: что берём у Mastra в стек флота + основа ли Mastra Studio для UI флота

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__create_scheduled_task", "max_results": 1}

---

> `Bash` -- {"command": "date -u +%Y-%m-%dT%H:%M:%SZ; date +%Y-%m-%dT%H:%M:%S%z"}

---

> `mcp__scheduled-tasks__create_scheduled_task` -- {"taskId": "auto-hub-261028-dr-runner-mastra", "title": "🔬 · 🧩🏗 ДР-ноги Mastra DR26-10-28-HUB-13-1920", "description": "AUTO-HUB-261028-dr-runner: браузерные ноги ДР DR26-10-28-HUB-13-1920 (Mastra)", "fireAt": "2026-10-28T19:23:00+00:00", "notifyOnCompletion": true, "prompt": "Первым действием: mcp_

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_usage", "max_results": 1}

---

> `mcp__ccd_session_mgmt__get_usage` -- {}

---

**Claude:**

Бюджет в порядке (5ч окно 1%, неделя 40%). Повторяю постановку сессии-исполнителя ДР.

---

> `mcp__scheduled-tasks__create_scheduled_task` -- {"taskId": "auto-hub-261028-dr-runner-mastra", "title": "🔬 · 🧩🏗 ДР-ноги Mastra DR26-10-28-HUB-13-1920", "description": "AUTO-HUB-261028-dr-runner: браузерные ноги ДР DR26-10-28-HUB-13-1920 (Mastra)", "fireAt": "2026-10-28T19:25:00+00:00", "notifyOnCompletion": true, "prompt": "Первым действием: mcp_

---

> `Bash` -- {"command": "python ~/.claude/scripts/_shared/fireat_now.py --in 3; head -12 ~/.claude/scheduled-tasks/auto-hub-261028-critic-loop-gauntlet-from-openflow/SKILL.md"}

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__update_scheduled_task", "max_results": 1}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "auto-hub-261028-critic-loop-gauntlet-from-openflow", "title": "🔬 · 🧩🏗 ДР-ноги Mastra DR26-10-28-HUB-13-1920", "description": "Браузерные ноги ДР DR26-10-28-HUB-13-1920 (Mastra) для H88589", "fireAt": "2026-10-28T19:36:16Z", "notifyOnCompletion": true, "prompt": "ПЕРВЫМ ДЕЛОМ переименуй э
