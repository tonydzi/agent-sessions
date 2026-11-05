---
session: s_eb6cd0b1
date: 2026-10-11
words: 2860
turns: 3
tools: "Bash, ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-11 · Deep research with live web search and citations (URLs). Date: 2026-10-11. Topic: "swarms…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_eb6cd0b1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Deep research with live web search and citations (URLs). Date: 2026-10-11. Topic: "swarms of AI agents on ONE developer computer (and a small home fleet of 2-5 machines)": which tools exist RIGHT NOW for agent-to-agent coordination between coding agents (Claude Code, Codex CLI, Cursor, Gemini CLI, Grok Build, OpenCode, Hermes, OpenClaw, nanobot). Not drones, not robotics. Cover:
1) Message buses / inboxes for agents: file-based (events.jsonl, SQLite), MCP-based, NATS, Matrix/IM rooms, Telegram. Name repos, stars, last release, whether they do: atomic claim, lease with TTL, ACK, evidence-gated done, quorum/consensus rounds, tie-break, audit ledger, cross-machine delivery.
2) Orchestrators: [ИМЯ] [ИМЯ] ([ИМЯ]), Claude Code Agent Teams (built-in), Conductor, Claude Squad, LoopTroop, Paperclip, agent-mesh ([СКРЫТО]), AgentTeams (agentscope), Alook, Agent Relay, OpenAgentMesh, llm-bus, agent-bus ([СКРЫТО]), agentbus ([СКРЫТО]), agent-comm. For each: transport, roles model, vendor-neutral or Claude-only, local vs cloud, maturity.
3) Protocols: A2A, MCP, ACP (merged into A2A), ANP, OASF; what is actually used by local coding-agent tools in practice.
4) What most of these tools LACK (per community issues/blogs): cross-machine delivery over sync folders, human approval tiers, rule governance (canon), vendor-neutral consensus, cost accounting, "done = claim with evidence".
Output: structured markdown, tables, every claim with a URL, mark uncertain items. Length ~1500-2500 words.

---

**Claude:**

Начинаю с загрузки поисковых инструментов и RECALL по нашему волту: проверю, нет ли уже такого ресёрча.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports 2>/dev/null && timeout 90 python brain_ask.py \"agent swarm orchestrator [ИМЯ] [ИМЯ] agent teams message bus coordination\" 2>&1 | head -40", "description": "RECALL по волту по теме роя агентов", "timeout": 100000}

---

> `WebSearch` -- {"query": "[ИМЯ] [ИМЯ] [ИМЯ] [ИМЯ] multi-agent orchestrator github stars beads", "mode": "standard"}

---

> `WebSearch` -- {"query": "Claude Code agent teams mailbox shared task list docs experimental", "mode": "standard"}

---

> `WebSearch` -- {"query": "Conductor Claude Squad parallel coding agents git worktrees github", "mode": "standard"}

---

> `WebSearch` -- {"query": "Paperclip AI agent company orchestration github", "mode": "standard"}

---

> `WebSearch` -- {"query": "agent-mesh [СКРЫТО] github", "mode": "standard"}

---

> `WebSearch` -- {"query": "Agent Relay AI agents messaging Claude Codex github agent-relay", "mode": "standard"}

---

> `WebSearch` -- {"query": "A2A protocol Linux Foundation ACP merged adoption 2026 version", "mode": "standard"}

---

> `WebSearch` -- {"query": "MCP server inter-agent messaging between Claude Code and Codex sessions inbox claim lease", "mode": "standard"}

---

> `WebSearch` -- {"query": "LoopTroop AI coding agents orchestrator github", "mode": "standard"}

---

> `WebSearch` -- {"query": "agentscope AgentTeams multi-agent coding github", "mode": "standard"}

---

> `WebSearch` -- {"query": "OpenAgentMesh github agents", "mode": "standard"}

---

> `WebSearch` -- {"query": "[СКРЫТО] agent-bus github", "mode": "standard"}

---

> `WebSearch` -- {"query": "[СКРЫТО] agentbus github", "mode": "standard"}

---

> `WebSearch` -- {"query": "llm-bus github multi-agent message bus Claude Codex", "mode": "standard"}

---

> `WebSearch` -- {"query": "NATS JetStream coding agents Claude Code coordination message bus open source", "mode": "standard"}

---

> `WebSearch` -- {"query": "Matrix room coding agents Claude Code Codex bridge multi-agent chat open source", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://github.com/[ИМЯ]/mcp_agent_mail", "prompt": "Stars, last release/version and date, license, features: inbox, file reservations/leases with TTL, ack_required acknowledgments, storage (git+SQLite), cross-machine support, supported agents."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/gastown", "prompt": "Stars, latest release version and date, supported agents (Claude/Codex/others), architecture: mail, beads, roles (Mayor, Deacon, Witness, Refinery, Polecats), license, how work is claimed/merged."}

---

> `WebFetch` -- {"url": "https://code.claude.com/docs/en/agent-teams", "prompt": "Extract: how teammates communicate (mailbox), shared task list mechanics (claiming, file locking, dependencies), hooks (TeammateIdle, TaskCompleted), limitations list, version requirements, whether cross-machine or Claude-only, token 

---

> `WebSearch` -- {"query": "Alook agents coding multi-agent app mac orchestrate Claude Codex", "mode": "standard"}

---

> `WebSearch` -- {"query": "Claude Code agent teams limitations issues github no session resumption cross-machine token cost complaints", "mode": "standard"}

---

> `WebSearch` -- {"query": "Hermes agent OpenClaw nanobot multi-agent coordination messaging between agents A2A ACP support", "mode": "standard"}

---

> `WebSearch` -- {"query": "ANP Agent Network Protocol OASF Open Agent Schema Framework status 2026 adoption", "mode": "standard"}

---

> `WebSearch` -- {"query": "multi-agent coding \"evidence\" done verification gate agents claim completed false completion orchestrator problem blog 2026", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://code.claude.com/docs/en/cross-session-messaging", "prompt": "How cross-session messaging works: transport (sockets?), same machine only?, how receiving session treats messages, version requirements, limits, whether Claude-only."}

---

> `WebFetch` -- {"url": "https://github.com/AgentWorkforce/relay", "prompt": "Stars, latest release version/date, transport (broker, PTY, WebSocket?), supported CLIs, delivery guarantees (ack, retry, offline), cross-machine/cloud, license."}

---

> `WebFetch` -- {"url": "https://github.com/[СКРЫТО]/agent-bus", "prompt": "Stars, last release/commit, what it does, transport, supported agents, any claim/lease/ack features."}

---

> `WebFetch` -- {"url": "https://github.com/a2aproject/A2A", "prompt": "Stars, latest release version and date, governance (Linux Foundation), SDK languages."}

---

> `WebFetch` -- {"url": "https://nats.io/blog/coordinating-ai-agent-teams-on-nats/", "prompt": "Key claims: topologies, JetStream work queues, ack, presence, identity/sender spoofing prevention, cross-machine. Quote concisely."}

---

> `WebFetch` -- {"url": "https://github.com/smtg-ai/claude-squad", "prompt": "Stars, latest release version and date, license, supported agents, transport."}

---

**Claude:**

# Рой ИИ-агентов на одной машине и в домашнем флоте 2-5 узлов: срез на 2026-10-11

Это исследование без собственных проверок: данные из поиска и со страниц репозиториев, звёзды и версии на момент чтения. Метки: ✅ видел на первичной странице (репозиторий или официальные доки), 🟡 только вторичные источники, ❓ не нашёл или не подтверждено.

## Ключевые выводы

- Транспорты зрелые, дисциплина поверх них нет. Почти везде есть почтовый ящик, у части есть замок на файлы. Чтобы вместе были атомарный захват задачи, TTL, ACK и приёмка по доказательству, надо собирать самим.
- Кросс-машинная доставка есть у двух: у Anthropic через Remote Control (через их серверы) и у NATS-семейства. Доставки через папку синхронизации (Syncthing) в публичных инструментах я не нашёл ❓.
- Консенсус разных вендоров, уровни одобрения человеком, канон правил и учёт стоимости по рельсам: из того, что нашёл, всё это есть только в Paperclip (бюджеты и аудит), частично в [ИМЯ] [ИМЯ] (Refinery-гейты). Остальное ❓.
- Протоколы A2A и MCP живы, но локальные coding-агенты общаются в основном не через них, а через файлы, сокеты и MCP-сервера-почтовики.

## 1. Шины и почтовые ящики

| Проект | Транспорт | Звёзды / версия | Что из списка умеет | Источник |
|---|---|---|---|---|
| **Claude Code cross-session messaging** (встроенный) | Unix-сокет на сессию (named pipe на Windows); между машинами через серверы Anthropic и Remote Control | встроено, нужен v2.1.224+ ✅ | Доставка и 3 исхода (delivered, held, refused). Лимиты и защита от петель. Сообщение не может одобрить действие за человека. Offline-получатель получает после реконнекта. Захвата, lease и ACK-доказательств нет. Только Claude, только plain text. Между машинами нужен claude.ai-логин, не работает с API-ключом и Bedrock | [доки](https://code.claude.com/docs/en/cross-session-messaging) |
| **Claude Code Agent Teams** (встроенный) | JSON-файл на агента: `~/.claude/teams/{team}/inboxes/{agent}.json` | экспериментальная, нужен v2.1.32+ ✅ | Атомарный захват задачи через file locking ✅. Зависимости задач ✅. Хуки `TaskCompleted` и `TeammateIdle` с exit 2 дают гейт готовности ✅. TTL и lease нет. Одна команда на сессию, нет вложенных, не восстанавливается при `/resume` | [доки](https://code.claude.com/docs/en/agent-teams) |
| **mcp_agent_mail** ([ИМЯ]) | FastMCP по HTTP; Git для сообщений плюс SQLite FTS5 | 2.2k ✅; Python-версия помечена как «no longer maintained», её заменяет `mcp_agent_mail_rust` ✅; релиз и лицензию страница не показала | Inbox и outbox, `ack_required` плюс `acknowledge_message`, file reservations с `ttl_seconds` и `exclusive` (это lease, совещательный) ✅. Работает с Claude Code, Codex, Gemini CLI, Cursor и другими. Кросс-машинность: есть bearer и JWT-авторизация по HTTP, но многомашинный сценарий не описан ❓ | [GitHub](https://github.com/[ИМЯ]/mcp_agent_mail) |
| **Agent Relay** (AgentWorkforce/relay) | Брокер с каналами, DM, PTY-драйвер и SDK (TS, Python) | 872 ✅, Apache-2.0 ✅; версии в источниках расходятся (7.1.1 и 8.6.0) 🟡 | Заявлены durable delivery, offline catch-up, retries, receipts 🟡 (на странице репо не подтверждено). Работает с Claude, Codex, Gemini, OpenCode. Агенты на разных машинах через облако Agent Relay Cloud; self-host по запросу ✅ | [GitHub](https://github.com/AgentWorkforce/relay), [описание](https://www.everydev.ai/tools/agent-relay) |
| **LLM Bus** (llm-bus.com) | Streamable HTTP MCP, self-host под AGPL-3.0 или хостинг | ❓ только каталог | Бесшовные ID, advisory-локи на файлы, общий event log, presence, handoff-заметки, граф задач 🟡 | [mcp.so](https://mcp.so/servers/llm-bus) |
| **Agent Comms** (ExaDev) | TCP-меш на localhost, без файловой зависимости | ❓ | Комнаты, DM, presence, видимость между разными harness 🟡 | [glama](https://glama.ai/mcp/servers/ExaDev/agent-comms) |
| **[СКРЫТО]/agent-bus** | MCP через stdio, без демона, состояние в файлах | 0 звёзд, 7 коммитов ✅ | Поиск и чтение сессий, `ask_agent`, `handoff_session`, защита от рекурсии. Захвата, lease и ACK нет. Нужен macOS ✅ | [GitHub](https://github.com/[СКРЫТО]/agent-bus) |
| **mcp-comms** | Общая SQLite-база | ❓ | Директные сообщения, broadcast, обнаружение сессий; claim и lease не упомянуты 🟡 | [glama](https://glama.ai/mcp/servers/[СКРЫТО]/mcp-comms) |
| **InterAgentMail** | JSON на диске, только Codex | ❓ | Durable-ящики, авто-пробуждение; остаётся в очереди при офлайне получателя 🟡 | [glama](https://glama.ai/mcp/servers/cerberusgamelabs/cgl-interagentmail) |
| **nats-channel-mcp** ([СКРЫТО]) | NATS в MCP-канал Claude Code (v2.1.80+) | ❓ | JetStream-режим даёт durability, но авторы честно пишут, что сбой между получением и обработкой теряет сообщение 🟡 | [glama](https://glama.ai/mcp/servers/[СКРЫТО]/nats-channel-mcp) |
| **Synadia nats-channel** (плагин Claude Code) | NATS-микросервис, heartbeats, prompt и status | около 71 звезды 🟡 | Реализует Agent Protocol Synadia | [skillselion](https://skillselion.com/skills/synadia-ai/synadia-agents/agents/claude-code) |
| **Cotal на NATS** (пост на nats.io) | NATS и JetStream | ❓ | Work queue («ровно один экземпляр берёт работу»), presence в KV с TTL и heartbeats, JWT-проверка отправителя (запрет подделки), кластер из нескольких машин без изменений. Всё это заявления авторов, независимых замеров нет; семантика ACK в посте не описана ✅ | [nats.io](https://nats.io/blog/coordinating-ai-agent-teams-on-nats/) |
| **teamctl** | Состояние только на диске, path-based file leases | ❓ | Лизы на пути против merge-коллизий 🟡 | [поиск](https://www.mintlify.com/shanraisshan/claude-code-best-practice/workflows/agent-teams) |
| **josepavese/matrix** | Локальный демон; интерфейсы Telegram, HTTP, CLI | ❓ | Handoff между Claude, Gemini, OpenCode, ACP/A2A-агентами. К протоколу Matrix отношения не имеет 🟡 | [ecosyste.ms](https://awesome.ecosyste.ms/projects/github.com%2Fjosepavese%2Fmatrix) |
| **claude_codex_bridge** (SeemSeam) | Видимый CLI-воркспейс | около 3.4k 🟡 | Смешивает Codex, Claude, Gemini, Kimi, Qwen, Cursor, OpenCode и др. | [gittrend](https://gittrend.io/repo/SeemSeam/claude_codex_bridge) |

**Matrix/IM-комнаты:** готового моста «Matrix-комната ↔ coding-агенты» я не нашёл ❓ ([поиск](https://awesome.ecosyste.ms/projects/github.com%2Fjosepavese%2Fmatrix)). **Telegram:** есть как интерфейс человека (josepavese/matrix), как шины агент-агент не видел ❓. Чат-шины делаете вы сами.

## 2. Оркестраторы

| Инструмент | Транспорт | Роли | Вендор | Где | Зрелость |
|---|---|---|---|---|---|
| **[ИМЯ] [ИМЯ]** (gastownhall/gastown, раньше [СКРЫТО]) | mailbox, identities и handoffs; Beads (git-трекер задач); mail через хуки | Mayor, Deacon, Witness (на rig), Refinery (merge-очередь в стиле Bors), Polecats | Claude Code, Copilot, Codex, Gemini, Kiro, Cursor, Amp, OpenCode и др. ✅ | локально, tmux/worktrees | 18.3k звёзд, MIT ✅; версию страница не показала. Работа: `gt sling` → `gt done` → Refinery прогоняет verification gates ✅. Есть федерация Wasteland ✅. Это ближайший по духу аналог вашего «evidence-gated done» ✅ ([GitHub](https://github.com/[СКРЫТО]/gastown)). Beads отдельно, около 20k звёзд по вторичному источнику 🟡 ([пост](https://ascii.co.uk/news/article/news-20260102-190a5f9f/steve-yegge-releases-gas-town-multi-agent-orchestrator-for-c)) |
| **Claude Squad** (smtg-ai) | tmux и git worktrees | нет ролей, плоские сессии | Claude, Codex, Gemini, Aider, OpenCode, Amp ✅ | локально | 8.6k, AGPL-3.0 ✅; версию страница не показала. Агенты между собой не общаются ✅ ([GitHub](https://github.com/smtg-ai/claude-squad)) |
| **Conductor** (Melty Labs) | worktree на workspace | workspace как единица работы | Claude Code и Codex 🟡 | Mac-приложение | Бесплатно, свои подписки; диаграмма и PR-flow ([доки](https://www.conductor.build/docs/concepts/git-worktrees)). Не путать с conductor.com 🟡 |
| **Paperclip** (paperclipai/paperclip) | Node.js-сервер, встроенный Postgres, heartbeats | оргсхема, цели, роли как в компании | Claude Code, Codex, Gemini, любой агент с heartbeat 🟡 | self-hosted | Около 43k звёзд, MIT, март 2026 (вторичные источники; URL репо в источниках расходятся) 🟡. Бюджеты на агента, неизменяемый аудит-лог, апрувы ([обзор](https://abduzeedo.com/paperclip-open-source-ai-agent-orchestration-builders)) |
| **LoopTroop** | GUI, worktree на «bead» | LLM Council планирует и верифицирует (консенсус) | в основном OpenCode | локально | v0.3.1 (22.06.2026), ~40-60 звёзд, ранняя альфа, MIT; запускает OpenCode в режиме skip-permissions 🟡 ([HackerNoon](https://hackernoon.com/inside-looptroop-a-local-open-source-ai-orchestrator)) |
| **Claudete / Agentastic / Indigo** | окна с общим чатом | чат-комнаты (Claudete) | Claude, Codex, Grok, OpenCode 🟡 | Mac-приложения | зрелость ❓ ([список](https://www.everydev.ai/tools/claudete/llms.txt)) |
| **AgentBridge** (quilin-ai) | общий демон | пара Claude и Codex | Claude и Codex 🟡 | локально | MIT 🟡 ([alternativeto](https://alternativeto.net/software/agentbridge/about/)) |

**Не нашёл или не удалось отождествить** ❓:
- agent-mesh ([СКРЫТО]);
- OpenAgentMesh;
- agent-bus ([СКРЫТО]);
- agentbus ([СКРЫТО]), найдены только однофамильцы ([СКРЫТО], charlesnpx, roriau0422);
- AgentTeams (agentscope), нашёл лишь общий фреймворк AgentScope от Alibaba;
- Alook;
- «agent-comm» как точное имя.

Если эти имена из ваших ссылок, пришлите URL, добью.

**Hermes, OpenClaw, nanobot:**
- OpenClaw в источниках описан как ACP-переводчик (Agent Client Protocol, редакторский стандарт, не IBM-овский) со sub-agents как дочерними процессами 🟡 ([arXiv 2609.00006](https://arxiv.org/pdf/2609.00006)).
- Hermes: мульти-агентность через Profiles 🟡 ([сравнение](https://blog.kilo.ai/p/hermes-vs-openclaw-when-to-reach)).
- nanobot: только sub-agents, ACP или A2A не нашёл ❓.
- Источники противоречат друг другу по мульти-агентности OpenClaw 🟡.

## 3. Протоколы

| Протокол | Статус | Что реально используют локальные coding-агенты |
|---|---|---|
| **A2A** | v1.0 стабильная, март 2026 🟡 (в мае была сравнительная таблица с 0.3.x, версию надо сверить по репо). Репозиторий a2aproject/A2A: 26.1k звёзд, Apache-2.0, SDK на Python, Go, JS, Java, .NET, Rust ✅ ([GitHub](https://github.com/a2aproject/A2A)). Linux Foundation: 150+ организаций, апрель 2026 ✅ ([LF](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)). Переход в Agentic AI Foundation 17.08.2026: один источник, ❓ | Нужен для связи сервисов и облачных платформ. Среди локальных coding-инструментов явной поддержки у Claude Code, Codex, Cursor не нашёл ❓. Есть в демонах вроде josepavese/matrix 🟡 |
| **MCP** | Под Linux Foundation, вместе с A2A в AAIF 🟡 ([softwareseni](https://www.softwareseni.com/mcp-and-the-linux-foundation-what-vendor-neutral-governance-means-for-enterprise-protocol-risk)) | Де-факто основной «клей» между агентами: почти все почтовики выше (agent_mail, llm-bus, agent-bus, mcp-comms) это MCP-сервера |
| **ACP (IBM)** | Влит в A2A, август 2025; репозиторий в архиве ✅ ([tyk](https://tyk.io/learning-center/agent-protocols-a-complete-guide-to-mcp-a2a-and-acp/)) | Не использовать. Не путать с Zed Agent Client Protocol (редактор ↔ агент), он жив |
| **ANP** | «proposed», IETF-draft октября 2025 мог истечь 23.04.2026 ❓ ([arXiv](https://arxiv.org/pdf/2508.00007)) | Данных о внедрении нет ❓ |
| **OASF** (AGNTCY) | Схема описания возможностей агентов, ~288 звёзд 🟡 ([доки](https://docs.agntcy.org/pages/oasf.html)) | Данных о внедрении у coding-агентов нет ❓ |

Итог: на одной машине и в малом флоте работают файлы, сокеты, SQLite и MCP-серверы. Для вашей задачи A2A избыточен: он про открытые сети агентов, а не про 2-5 своих узлов.

## 4. Чего не хватает (по документации и блогам)

| Пробел | Что видно по источникам |
|---|---|
| **Доставка через синхронизируемую папку** | Встроенные почтовики Anthropic локальны или идут через их облако. Agent Teams пишут ящики в `~/.claude`, никаких гарантий для синхронизации между машинами в доках нет ❓. Публичных аналогов Syncthing-доставки не нашёл |
| **Атомарный захват плюс TTL плюс ACK вместе** | Teams: захват есть, TTL нет. agent_mail: TTL и ACK есть, захват задач не центральная идея. NATS: work-queue «один взял» и KV TTL есть, но это конструктор, не готовый инструмент. [ИМЯ] [ИМЯ]: через Beads, детали lease не подтверждены ❓ |
| **Готово = утверждение с уликой** | Встроено только как хуки (Teams `TaskCompleted`) и Refinery-гейты ([ИМЯ] [ИМЯ]). Рекомендация индустрии: независимый read-only верификатор, детерминированные доказательства (тесты, CI), аудит-след. Эмпирическая база тонкая: единичный кейс на arXiv 2605.17998, у гейта в нём 0.39% точности блокировок ([agentpatterns](https://agentpatterns.ai/multi-agent/verify-gated-completion-admission-control/), [amux](https://amux.io/guides/ai-agent-quality-gates/)) |
| **Уровни одобрения человеком** | Только через permission-режимы: Teams отдают prompts лидеру, plan approval лидер одобряет автоматически; inbound hold/refuse у cross-session; `isolatePeerMachines` ✅. Paperclip: апрувы и бюджеты 🟡. Общей модели «Tier» нет ❓ |
| **Канон правил (governance)** | Единый свод правил, который наследуют все вендоры, мне не встретился ❓. Ближе всего CLAUDE.md и подагентные определения, но «скилл без потребителя» и «правило без двери» нигде не упомянуты |
| **Консенсус разных вендоров и tie-break** | LoopTroop (Council) и «дебаты» в Teams. Кворум, раунды и tie-break между Claude, Codex, Grok как продукт не нашёл ❓ |
| **Учёт стоимости** | Teams: многократный рост токенов (оценка 7× для планирующих команд 🟡 из [guide](https://claudefa.st/blog/guide/agents/agent-teams-best-practices)); Paperclip: бюджеты на агента 🟡. Учёта «чей оплаченный бак жжём» и «процент недобора против плана» не видел ❓ |
| **Жалобы сообщества на Teams** | Теммейты не опрашивают inbox (tmux, macOS); зависшие «in progress»; лид сам кодит вместо координации; нет `/resume` ([claudeissues](https://claudeissues.com/version/v2.1.32), [pilot-shell](https://pilot-shell.com/blog/agent-teams-best-practices)). Часть могла быть исправлена позже, доки сами описывают fix v2.1.207 про битые записи |

## Что взять и где вы впереди

- **Брать готовое:** cross-session messaging и Agent Teams как «лёгкий» слой внутри Claude; NATS/JetStream, если понадобится честная кросс-машинная очередь с ACK; mcp_agent_mail (смотреть Rust-версию) как образец формата lease с TTL.
- **Идея в [ИМЯ] [ИМЯ]:** «polecat не пушит в main, Refinery проверяет гейтами». Это ближайший публичный аналог вашего «done = утверждение с уликой».
- **Вероятная ниша:** шина по синхронизируемой папке плюс кворум вендоров плюс Tier-одобрения плюс канон в одном виде. Сильное утверждение «такого нет» не доказано: я не обошёл GitHub-поиск полностью и не проверил офлайн-узлы, только то, что отдала веб-выдача.

## Не закрыто

- Версии и даты релизов большинства репозиториев (страницы не показывали Releases).
- Звёзды Paperclip, Beads и SeemSeam только из вторичных источников.
- Шесть названий из вашего списка не найдены.
- Нет проверки на исходниках: ACK и lease Agent Relay, семантика захвата в [ИМЯ] [ИМЯ].

Источники выше указаны ссылками в таблицах. Заметку в волт не клал, могу оформить по `/obsidian-ingest`.

🧒 Простыми словами: у агентов уже есть почтовые ящики и замки на файлы, как записки на холодильнике. Но чтобы записку взял ровно один, она не повисла вечно, а «сделано» подтверждалось тестом, а не словом, всё это надо клеить самим. Лучше всех про «проверку перед тем как сказать готово» думает [ИМЯ] [ИМЯ]. Передачу записок между разными компьютерами через общую папку никто публично не сделал, судя по моему поиску.

Sources:
- [Claude Code: Agent Teams](https://code.claude.com/docs/en/agent-teams)
- [Claude Code: Cross-session messaging](https://code.claude.com/docs/en/cross-session-messaging)
- [Gas Town](https://github.com/[СКРЫТО]/gastown)
- [Claude Squad](https://github.com/smtg-ai/claude-squad)
- [mcp_agent_mail](https://github.com/[ИМЯ]/mcp_agent_mail)
- [Agent Relay](https://github.com/AgentWorkforce/relay)
- [[СКРЫТО]/agent-bus](https://github.com/[СКРЫТО]/agent-bus)
- [A2A](https://github.com/a2aproject/A2A)
- [NATS: Coordinating AI agent teams](https://nats.io/blog/coordinating-ai-agent-teams-on-nats/)
- [Linux Foundation: A2A first year](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)
- [Tyk: MCP, A2A, ACP](https://tyk.io/learning-center/agent-protocols-a-complete-guide-to-mcp-a2a-and-acp/)
- [Verify-gated completion](https://agentpatterns.ai/multi-agent/verify-gated-completion-admission-control/)
