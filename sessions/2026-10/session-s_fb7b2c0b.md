---
session: s_fb7b2c0b
date: 2026-10-11
words: 2491
turns: 3
tools: "Agent, Bash, Edit, SendUserFile, ToolSearch, WebFetch, WebSearch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-11 · ВОСКРЕШЕНИЕ ПОСЛЕ ЛИМИТА: сессия edfcace3 умерла первым ответом на лимите подписки (10.10…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fb7b2c0b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

ВОСКРЕШЕНИЕ ПОСЛЕ ЛИМИТА: сессия edfcace3 умерла первым ответом на лимите подписки (10.10 15:25 UTC) и не сделала ничего. Это та же задача, поднятая заново ОДИН раз.

Нужно провести глубокое исследование, какие уже есть сейчас тулзы для раев, для раев этих агентов, то есть, и какие я могу сейчас сам использовать. У нас тоже есть типа агенты, где друг другу колбаливы, да? И мы друг другу координировать все, что-то делать. Вообще нужно провести исследование, какие существуют вообще раи и какие тулзы. существуют ли их друг другу на жирном действии. Но не рыки какие-нибудь военные, а дроны. А вот чисто вот так, у тебя на компьютере рой агентов, и тебе нужно его найти. Это очень всё банально и тупо и просто. Нужно мне найти, в общем, как всё это можно организовать прямо на компьютере. В общем, красивое, хорошее, на самом деле, глубокое исследование. узнать, кто как организовывает взаимодействие райов друг с другом. И, значит, как мы организовываем взаимодействие райов и агентов друг с другом, и посмотреть, сколько вообще то, что мы сделали, отличается от того, что сделано на рынке.

---

**Claude:**

Понял: поднимаю ДР заново один раз. Порядок: заголовок сессии и план рельс, RECALL (что мы уже знаем и построили), номер в реестре ДР, затем рыночная карта инструментов для роёв агентов на одной машине и сравнение с нашим стеком. Отчёт лягу в `docs/` и в чат.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title,WebSearch,WebFetch", "max_results": 3}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python rail_plan.py declare --self \"RECALL волта/памяти, синтез и сравнение рынка с нашим стеком (machine_bus, aibus_lite, claw-consensus, llm-pact, peer_help), отчёт в docs + волт\" --outsource \"web:gemini,dr_orchestrate:codex,second_opinion:codex\" 2>&1 | tai

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🔬 H18428 ДР: рои агентов на одном ПК, рынок vs наш стек"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_registry.py new --help 2>&1 | head -20; echo ---; python D:/Vault/_imports/brain_ask.py \"рой агентов координация агент-агент инструменты на одном компьютере multi-agent swarm orchestration\" 2>&1 | head -60", "description": "Check DR registry CLI an

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && grep -rli \"multi-agent\\|рой агентов\\|agent swarm\\|swarm\" --include=*.md . 2>/dev/null | grep -v _originals | head -40; echo ---MEM---; grep -rli \"swarm\\|рой\\|multi-agent\\|a2a\\|agent-to-agent\" \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB

---

> `Agent` -- {"description": "Inventory our agent-coordination stack", "subagent_type": "Explore", "prompt": "Inventory what dev's fleet has ALREADY BUILT for agent-to-agent / multi-session / multi-machine coordination on a computer. Thoroughness: very thorough. Read-only.\n\nLook at (paths): C:/Users/dev/.c

---

> `WebSearch` -- {"query": "multi-agent orchestration frameworks 2026 comparison local swarm of coding agents on one machine", "mode": "extended"}

---

> `WebSearch` -- {"query": "agent-to-agent protocols 2026 A2A MCP ACP ANP agent communication protocol comparison", "mode": "extended"}

---

> `WebSearch` -- {"query": "Claude Code agent teams subagents Codex multi-agent tmux orchestrator tools 2026 (claude-squad, agent-relay, ccswarm, paperclip, gastown)", "mode": "extended"}

---

> `WebSearch` -- {"query": "local multi-agent runtime desktop \"agent mesh\" \"agent bus\" open source 2026 nanobot openclaw agents coordinating each other", "mode": "extended"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_registry.py new \"Рои агентов на одном ПК: инструменты и рельсы координации агент-агент на рынке vs наш стек\" --tool inhouse 2>&1 | tail -3", "description": "Register DR number in registry"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && for f in \"02-Decisions/_Inbox/2026-09-22--agenty-v-odnoy-papke-loki-mira-i-gde-my-vperedi.md\" \"02-Decisions/_Inbox/2026-09-15--patterny-mezhagentnoy-koordinacii-v-prode-chto-rabotaet-i-lomaetsya.md\" \"03-Insights/insight-coddy-1-3-swarm-fleet-ve

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python llm_ask.py --help 2>&1 | head -40; ls ~/.claude/llm_routing.json && python -c \"import json;d=json.load(open(r'C:/Users/dev/.claude/llm_routing.json'));print({k:v for k,v in d.items() if k in ('web','dr_orchestrate','second_opinion')} if isinstance(d,dic

---

> `WebSearch` -- {"query": "\"agent-mesh\" [СКРЫТО] OR \"LoopTroop\" OR \"Alook\" agents shared rooms inboxes OR \"Agent Relay\" coding agents messaging local 2026", "mode": "extended"}

---

> `WebSearch` -- {"query": "Gas Town [ИМЯ] [ИМЯ] Claude Code orchestrator \"Paperclip\" agent company orchestrator 2026 multi-agent coordination mail beads", "mode": "extended"}

---

> `WebSearch` -- {"query": "file-based message bus for AI agents between machines Syncthing OR Telegram OR NATS \"agent bus\" lease claim ACK consensus 2026 github", "mode": "extended"}

---

> `WebSearch` -- {"query": "Claude Code agent teams vs Codex multi-agent vs Cursor background agents vs Gemini CLI swarm 2026 built-in multi-agent features comparison", "mode": "extended"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_fb7b2c0b/tool-results\" && grep -n \"^## \\|^### \\|впереди\\|велосипед\\|Вердикт\\|вердикт\" bcgrljiun.txt | head -60; echo ======; sed -n '/Где мы впереди/,/^=== /p' bcgrljiun.txt | head -60"

---

> `Bash` -- {"command": "mkdir -p \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad\" && cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad/dr_prompt.md\" <<'EOF'\nDee

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/awesome-agent-orchestrators", "prompt": "List every orchestrator/tool named in this list with its one-line description and category grouping. Keep names exact. Note which are local/desktop, which are cloud, which are vendor-neutral."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/agent-bus", "prompt": "Summarize: transport (files? server?), core primitives (claim, lease, TTL, ACK, evidence gate, audit, dispute freeze, merge gate, inbox, topology), supported agents/vendors, cross-machine support, stars/last update if visible, license."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/llm-bus", "prompt": "Summarize: transport (MCP? HTTP?), primitives (atomic claims, ledger, leases, presence, handoffs, tasks), supported agents, local vs hosted, cross-machine, stars/last update, license."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/agentbus", "prompt": "Summarize: transport, verbs (inbox, send, claim, lock, ask/answer, fact, watch), supported vendors (Claude Code, Codex, Cursor), cross-machine support, maturity signals (stars, last commit), license."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/agent-mesh", "prompt": "Summarize: architecture (process fleets, A2A messaging, receipts, quorum councils, provider-neutral advisory routing), supported providers, transport, local vs networked, human approval features, maturity (stars, releases), license."}

---

> `WebFetch` -- {"url": "https://github.com/alookai/alook", "prompt": "Summarize: what it is (rooms for people and agents), supported local agents, transport/hosting (cloud service vs self-host), identities/inboxes, pricing if any, maturity, license."}

---

> `WebFetch` -- {"url": "https://github.com/agentscope-ai/AgentTeams", "prompt": "Summarize: architecture (Matrix rooms, Manager/Worker, Controller API), supported runtimes (OpenClaw, QwenPaw, Hermes), human-in-the-loop features, local vs server, maturity (version, stars), license."}

---

> `WebFetch` -- {"url": "https://code.claude.com/docs/en/agent-teams", "prompt": "Summarize Claude Code Agent Teams: how teammates are spawned, shared task list, messaging between teammates, tmux requirement, single-machine limitation, experimental flag, limitations listed."}

---

> `WebFetch` -- {"url": "https://paddo.dev/blog/gastown-two-kinds-of-multi-agent/", "prompt": "Summarize the \"two kinds of multi-agent\" distinction and how Gas Town's mail/beads/hooks coordination works, plus any criticism of cost or reliability."}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_fb7b2c0b/tool-results\" && sed -n '34,115p' bcgrljiun.txt | cut -c1-600; echo; echo \"=== CODDY SWARM VERDICT\"; sed -n '233,300p' bcgrljiun.txt | cut -c1-500", "description": "Read prior note 

---

> `Bash` -- {"command": "gh search repos \"agent-bus\" --sort stars --limit 8 --json fullName,stargazersCount,description,updatedAt 2>&1 | head -40; echo ---; gh search repos \"coordination coding agents message bus claude code codex\" --sort stars --limit 10 --json fullName,stargazersCount,description,updatedA

---

> `WebFetch` -- {"url": "https://code.claude.com/docs/en/cross-session-messaging", "prompt": "Summarize cross-session messaging in Claude Code: how sessions discover each other, transport, same-machine only or cross-machine, trust model of incoming messages, limitations."}

---

> `WebFetch` -- {"url": "https://github.com/openagentmesh/openagentmesh", "prompt": "Summarize: transport (NATS?), contracts/discovery, local vs prod, supported agent frameworks, maturity (stars, release), license, whether it targets coding CLIs like Claude Code/Codex."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/AgentMesh", "prompt": "Summarize: what it coordinates (independent coding agents), transport, primitives (locks, tasks, messages, memory), vendors supported, maturity, license."}

---

> `WebFetch` -- {"url": "https://developers.openai.com/codex/multi-agent", "prompt": "Summarize Codex CLI built-in multi-agent / subagent features: how agents are spawned, whether they communicate with each other, single-machine, config flags, limitations."}

---

> `WebFetch` -- {"url": "https://github.com/EvoMap/awesome-agent-swarm", "prompt": "List the categories and the most notable swarm frameworks/protocols with one-line descriptions, especially anything about agent-to-agent communication, consensus, and local/desktop operation."}

---

> `Bash` -- {"command": "for r in alookai/alook agentscope-ai/AgentTeams [СКРЫТО]/agent-mesh [СКРЫТО]/agentbus [СКРЫТО]/llm-bus gastownhall/gastown gastownhall/beads [СКРЫТО]/AgentMesh [СКРЫТО]/agent-comm openagentmesh/openagentmesh smtg-ai/claude-squad [СКРЫТО]/foremerge [СКРЫТО]/agent-bus hcom-ai

---

> `WebFetch` -- {"url": "https://learn.chatgpt.com/docs/agent-configuration/subagents", "prompt": "Summarize Codex CLI subagents / multi-agent: how spawned, whether subagents communicate with each other or only report back, single machine only, config, limitations."}

---

> `Bash` -- {"command": "gh search repos \"hcom agents message spawn terminals\" --limit 3 --json fullName,stargazersCount,description 2>/dev/null | head -20; gh search repos paperclip agents heartbeats tickets --limit 3 --json fullName,stargazersCount,description 2>/dev/null | head -20; gh search repos \"agent

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad/dr_web_rail.md\"; ls -la \"$f\" 2>&1; wc -c \"$f\"; head -c 600 \"$f\"; echo; echo \"--- err:\"; tail -5 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls -la machine_bus.py aibus_lite.py bus_send.py peer_help.py onair.py workspace_write_lease.py spawn_queue.py approval.py 2>&1 | awk '{print $5, $6, $7, $9}'; echo \"--- fleet nodes:\"; python -c \"import json;d=json.load(open(r'C:/Users/dev/.claude/fleet_nodes

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && ls public-repos/ _oss/ 2>/dev/null | head -60; echo \"--- claw-consensus:\"; find . -maxdepth 3 -iname \"*claw-consensus*\" -o -maxdepth 3 -iname \"JOIN.md\" 2>/dev/null | grep -v node_modules | head; grep -rn \"^version\\|\\\"version\\\"\" public-

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && for d in public-repos/claude-consensus _scratch/rwai-rollout/claw-consensus; do echo \"=== $d\"; (cd \"$d\" && git log -1 --format='%h %ad %s' --date=short 2>/dev/null; git remote -v 2>/dev/null | head -1; ls | head -20; grep -m3 -i \"version\" pyp

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '1,60p' aibus_lite.py | grep -v \"^$\" | head -50; echo \"=== peer_help passport\"; sed -n '1,40p' peer_help.py | grep -v \"^$\" | head -30", "description": "Read passports of aibus_lite and peer_help"}

---

> `Write` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md", "content": "# ДР: рои агентов на одном компьютере. Рынок инструментов координации агент↔агент и сравнение с нашим стеком\n\n> DR26-10-11-HUB-03-0732 · 2026-10-11 · сессия H18428 · воскрешение после лимита (

---

> `Edit` -- {"replace_all": false, "file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md", "old_string": "<!-- INVENTORY -->", "new_string": "Инвентарь снят субагентом read-only на хабе 11.10 (даты = mtime файла или последняя запись в логе). Флот: 8 узлов в `fleet_nodes.json

---

> `Edit` -- {"replace_all": false, "file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md", "old_string": "3. **Шина не MCP.** Все новые шины отдают агенту инструменты через MCP, у нас CLI-скрипты и SessionStart-хук. Для Codex/Cursor это лишний шаг.", "new_string": "3. **Шина

---

> `Edit` -- {"replace_all": false, "file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md", "old_string": "| 5 | **Коннект с рынком** (§4.7): issue/PR в agentbus и agent-mesh с нашим «ACK как долг» и «consensus без сервера», ссылка на claw-consensus; agent-mesh просит quorum 

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_registry.py update --help 2>&1 | head -15; echo ---; python rail_plan.py verdict --help 2>&1 | head -15; echo ---; python machine_stamp.py lint \"E:/!CLAUDE-HUBPC-June26/docs/dr-agent-swarms-on-one-pc-2026-10-11.md\" 2>&1 | tail -3; echo ---; ls \"

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && git remote -v | head -2; git status --short docs/dr-agent-swarms-on-one-pc-2026-10-11.md; wc -w docs/dr-agent-swarms-on-one-pc-2026-10-11.md", "description": "Check git remote and report size"}

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/03-Insights/insight-DR-DR26-10-11-HUB-03-0732-roi-agentov-na-odnom-pk-rynok-vs-nash-stek.md\" <<'EOF'\n---\ntitle: \"Insight (DR): рои агентов на одном ПК. Рынок координации агент↔агент vs наш стек claw-consensus\"\ntype: insight\nstage: distilled\nso

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && git add docs/dr-agent-swarms-on-one-pc-2026-10-11.md && git -c commit.gpgsign=false commit -q -m \"docs: ДР DR26-10-11-HUB-03-0732 рои агентов на одном ПК: 4 слоя рынка (вендоры/оркестраторы/шины/протоколы), 28 деталей нашего стека, матрица 15 свой

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\agent-swarm-market-vs-our-stack-2026-10.md", "content": "---\nname: agent-swarm-market-vs-our-stack-2026-10\ndescription: ДР 11.10.2026 по роям агентов на одном ПК: четыре слоя рынка, где наш claw-consensus уни

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad/dr_web_rail.md\"; wc -c \"$f\"; head -c 400 \"$f\"; echo; tail -3 \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/31991e9e-9539-484f-9fff-7bb

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad/dr_web_rail.md\"; grep -n \"^#\\|^|\" \"$f\" | cut -c1-220 | head -90; echo \"--- not in my report:\"; for t in Cyclops hcom AgentBridge Concord Paseo \"ai-maestro\"

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad/dr_web_rail.md\"; sed -n '6,12p;19,20p;76,100p' \"$f\" | cut -c1-700", "description": "Read second-pass key findings, gaps, and recommendations"}

---

> `Edit` -- {"replace_all": false, "file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md", "old_string": "### 2.4 Протоколы", "new_string": "### 2.3-бис Второй проход рельсы (`llm_ask --class web`, упала на `rail=claude`, 23 KB)\n\nНе независимый вендор (тот же Claude), поэт

---

> `Edit` -- {"replace_all": false, "file_path": "E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md", "old_string": "| 2 | **Intent+scope в lease** по образцу foremerge: `workspace_write_lease acquire <путь> --intent \"symbol:X=extend\"` | 1 вечер | флаг необязателен | Codex-implemente

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && cp \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_fb7b2c0b/scratchpad/dr_web_rail.md\" docs/dr-prompts/dr-agent-swarms-2026-10-11-rail-claude-pass2.md 2>/dev/null || (mkdir -p docs/dr-prompts && 

---

> `SendUserFile` -- {"files": ["E:\\!CLAUDE-HUBPC-June26\\docs\\dr-agent-swarms-on-one-pc-2026-10-11.md"], "caption": "ДР DR26-10-11-HUB-03-0732: рои агентов на одном ПК, рынок vs наш стек (2145 слов, 30 источников)", "status": "normal", "display": "render"}

---

**Claude:**

🕰 11.10.2026, 06:41 Лиссабон

ДР сделан и закрыт: отчёт [dr-agent-swarms-on-one-pc-2026-10-11.md](docs/dr-agent-swarms-on-one-pc-2026-10-11.md) (2 коммита b1e9f93, def16df), заметка в волте `03-Insights/insight-DR-DR26-10-11-HUB-03-0732-…`, реестр ДР `synthesized`, память записана.

**Ответ на вопрос «насколько наше отличается от рынка»**

Рынок за год разошёлся на четыре слоя, и ни один из них не закрывает нашу клетку целиком:

- **Вендоры** (Claude Code Agent Teams + cross-session messaging через сокет, Codex subagents, Cursor background): рой = один вендор, одна машина или их облако. Горизонтали Claude↔Codex↔Cursor никто не даёт.
- **Оркестраторы одной машины**: Gas Town 18k⭐ + Beads 28k⭐ (Claude-only, $100 в час на пике, ломал main), Paperclip 100k⭐ (сервер с Postgres, бюджеты и аудит), Claude Squad 8.6k⭐ (только изоляция worktree), LoopTroop (совет моделей на планировании). Каталог awesome-agent-orchestrators насчитывает около 80 кокпитов и 40 «роёв»: кокпитов перебор, протокола между разнородными агентами единицы.
- **Шины для разнородных агентов**, наш класс, родился летом 2026: agentbus 0⭐ (append-only jsonl в git, самый близкий к нам по идее), llm-bus 9⭐, agent-mesh 1⭐ (quorum councils, но локально), mcp_agent_mail 2.2k⭐ (ACK + lease с TTL, лучший прайор-арт нашего ACK-долга), Alook 1.3k⭐ и Agent Relay 872⭐ (облако), AgentTeams 5.7k⭐ (Matrix + k8s), OpenAgentMesh (NATS). Шесть из десяти моложе 60 дней.
- **Протоколы**: A2A (ACP в него влит), MCP, ANP. По факту локальные кодинг-агенты общаются файлами, SQLite и MCP-почтовиками, не A2A. У нас A2A-карточка на входе есть, в классе это редкость.

**Где мы одни.** Разнородные агенты + несколько машин + без сервера (Syncthing + TG) + тиры одобрения оператора + leader/follower канон + межмашинный консенсус с тай-брейком + учёт стоимости по рельсам. Статья arXiv 2606.31498 «Governance Gaps» называет ровно эти дыры у MCP/A2A/ACP. Второй проход рельсы (упала на claude, не независимый вендор) пришёл к тому же.

**Где мы велосипед, честно.** Нет кокпита «все сессии всех вендоров на всех машинах» (рынок богат: cmux 27k⭐). Lease у нас на файл, а не на смысл: foremerge 538⭐ ловит «один заменяет PaymentService, другой расширяет», мы нет. Шина не MCP, для Codex/Cursor лишний шаг. Межмашинный claim только у peer_help.

**Дыры нашего стека по прибору** (субагент, read-only, 28 деталей): NATS-рельса мертва (selftest 06.10), доска aibus_lite пустая (0 локов, ночник спит с 30.09), консенсус-лог Маяка молчит с 03.08, claw-consensus v0.4.0 без тега, две локальные копии на v0.2.1/v0.3.1.

**Что брать сейчас** (таблица §5 отчёта, 6 строк): cross-session messaging как третью рельсу внутри узла (0 инфраструктуры), intent+scope в lease по foremerge, MCP-обёртку над шиной, issue/PR в agentbus и agent-mesh с нашим «ACK как долг» и «consensus без сервера», гигиену витрины. Не брать: серверные шины ради 8 узлов, облачные комнаты для шины флота, Gas Town целиком.

**Не проверено:** gemini дала 429 на трёх моделях, независимого веб-мнения нет; звёзды и даты сняты `gh api`, описания инструментов по README (claim авторов); `[СКРЫТО]/agent-bus` 404.

🎙 Майк: прайор-арт подорожал, не убил: mcp_agent_mail с 2.2k звёзд делает наш ACK+lease, но на одной машине и без канона. Наш свободный угол «папка-синк + кворум вендоров + тиры + канон» в выдаче пустой. Следующий ход не стройка, а §4.7: прийти в agentbus и agent-mesh с готовым кодом.

🧒 Простыми словами: все на рынке строят либо «много одинаковых рабочих у одного станка» (Gas Town), либо «почтовый ящик для роботов на одном компьютере». А мы построили почту между разными роботами на разных компьютерах без центрального сервера, с правилом «кто решает» и «готово только с доказательством». Такого в магазине нет, у нас оно есть, но пара наших лампочек перегорела (NATS, Маяк), и витрину надо подкрасить.
