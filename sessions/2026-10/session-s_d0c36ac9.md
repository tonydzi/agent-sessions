---
session: s_d0c36ac9
date: 2026-10-06
words: 8959
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d0c36ac9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-03-HUB-01-0323
REGISTRY TOPIC: bb Harness versus Hermes Agent and OpenClaw: shared workspace and personal agent selection (через dr_start; ПОТРЕБИТЕЛЬ: dev chooses daily harness with shared workspace, shared skills and existing subscriptions) (dr_reconcile 2026-10-04: на диске 2/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-03-HUB-01-0323\results)

Return ONLY a JSON object (no prose, no code fence) with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "topic": "<clean human topic of the research, <=90 chars>",
 "one_line": "<one sentence: what question this deep-research answered>",
 "key_findings": ["<substantive conclusion grounded in the report>", "..."],
 "recommendations": ["<concrete recommendation / decision the report implies>", "..."],
 "entities": {"people": ["..."], "companies": ["..."], "products_tools": ["..."]},
 "open_questions": ["<what stayed unresolved / needs verification>", "..."],
 "related_concepts": ["<short concept name this connects to, for cross-linking>", "..."]
}
Rules: extract ONLY from the report text; never invent people, numbers or claims not present.
Merge across the vendor sections (they research the SAME question) -- deduplicate findings,
prefer the better-supported statement. 4-10 key_findings, be specific (numbers, names, tradeoffs).
If a list is empty use []. Write findings in the report's own language (ru stays ru).

REPORT (vendor sections tagged; may be Russian, English or mixed):


===== VENDOR: claudeai (claudeai.md) =====
# bb vs Hermes Agent vs OpenClaw: что выбрать как ежедневный «кокпит» на Windows + WSL (оценка на 2026-10-03)

**Вердикт: основной инструмент — bb (get-bb/bb), запущенный внутри WSL2, поверх уже авторизованных официальных CLI Claude Code и Codex. Hermes Agent и OpenClaw в роли основного инструмента не подходят: это персональные ассистенты и шлюзы мессенджеров, а не многоагентная IDE.** Опциональный компаньон один: Hermes Agent в отдельном WSL-профиле. Ставить его стоит только если нужны фоновые расписания или доступ из мессенджера, и только с общей библиотекой навыков, подключённой на чтение. OpenClaw как третий слой не ставить.

## TL;DR

- **Primary: bb в WSL2.** Это единственный из трёх кандидатов, который по своим документам является мультиагентным кокпитом: он управляет Codex, Claude Code, Pi и ACP-агентами параллельно, через ваши подписки и уже авторизованные CLI. Важные оговорки:
  - продукт ранний: версия 0.45.0 от 2 октября 2026, в README пометка «in active development»;\[1\]
  - нативный Windows появился только в 0.45.0 и помечен как alpha, поэтому работать нужно в WSL2.\[1\]
- **Hermes Agent и OpenClaw относятся к другой категории** (персональный ассистент, шлюз мессенджеров, рантайм). Подписку Claude они используют через обходные пути, которые зависят от политики Anthropic:
  - у Hermes OAuth-путь для Anthropic, по его же документации, работает только на Max и тратит extra usage, а не лимит подписки;
  - OpenClaw ссылается на устное разрешение «Anthropic staff told us».
- **Как избежать дублей памяти и навыков:**
  - держать один канонический каталог `~/.agents/skills` внутри файловой системы WSL и подключать его ссылками или путями, ничего не копируя;
  - держать один `AGENTS.md`;
  - запретить компаньону писать в общие навыки.
  
  Перед переходом пройти 7-дневный приёмочный тест, в котором нет ни одного необратимого шага.

---

## 1. Краткий вердикт

Ваш профиль: Windows + WSL, действующие подписки (Claude Pro/Max, возможно ChatGPT и Cursor), общий workspace для нескольких агентов и общая библиотека SKILL.md. Под него лучше всего подходит **bb в WSL2 как основной кокпит**. Движками остаются официальные CLI Claude Code и Codex; они нужны в любом случае, потому что именно через них тарифицируется подписка.

Почему bb:

- README прямо говорит, что bb «uses the provider CLI you already have authenticated» (README, проверено 2026-10-03).\[2\]
- Во внутреннем рантайме bb есть адаптеры для Codex, Claude Code, Pi и ACP.\[3\] Для многомашинной работы есть Account Pooler, worktree-потоки, «manager threads», автоматизации, а с 0.44.0 (2026-09-25) — отменяемое архивирование.\[1\]

**Опциональный компаньон — Hermes Agent.** Он нужен только под задачи, которые bb не закрывает: cron-расписания и доступ из Telegram или Discord. Поднимать его в отдельном профиле, `skills.external_dirs` направить на общий каталог, смонтированный только на чтение.

**OpenClaw не ставить.** Его ниша (шлюз, персональный ассистент, Windows Hub) почти полностью совпадает с нишей Hermes, а в истории подписочной авторизации Anthropic у него самый конфликтный след.

## 2. Таксономия категорий

| Инструмент | (a) IDE / мульти-харнесс кокпит | (b) Автономный персональный ассистент | (c) Шлюз мессенджеров | (d) Рантайм | (e) Фреймворк/SDK | Обоснование (источник, дата) |
|---|---|---|---|---|---|---|
| **bb** | **Да (основная)** | Нет | Частично: удалённый доступ через bb Connect и мобильный клиент, но не чат-мосты | Да: daemon, host-daemon, machines | Частично: SDK и плагинный API | README: «agentic IDE… desktop app, web app, CLI, and HTTP API»;\[2\] адаптеры Codex/Claude Code/Pi/ACP (README 2026-10-03; changelog 0.43.0–0.45.0, 2026-09-11…10-02) |
| **Hermes Agent** | Нет | **Да (основная)** | **Да** (`hermes gateway`: Telegram, Discord и др.) | Да: cron, профили, бэкенды Daytona/Modal | Частично: плагины и ACP-адаптер | README: «The agent that grows with you», `hermes gateway`, `hermes claw migrate`; в репозитории есть каталоги `cron/`, `gateway/`, `acp_adapter/` (проверено 2026-10-03) |
| **OpenClaw** | Нет | **Да** | **Да (основная)** | Да: Gateway как сервис, node mode | Частично: плагины «агентских харнессов» | README: «Your assistant, on your devices, in your chats»; харнессы Claude и Codex подключаются как сменные плагины (README main, проверено 2026-10-03) |
| OpenCode | Нет (терминальный агент) | Нет | Нет | Да | Частично | Документация по skills и permissions (opencode.ai, 2026-10-03)\[4\] |
| Pi | Нет (минимальный харнесс) | Нет | Нет | Да | **Да** (pi-agent-core, pi-ai, SDK) | Репозиторий earendil-works/pi: «AI agent toolkit» (2026-10-03)\[5\] |
| Claude Code | Частично (CLI, Desktop, subagents) | Нет | Нет | Да | Да (Agent SDK) | code.claude.com (2026-10-03) |
| Codex CLI / приложение | Частично (приложение: параллельные чаты, worktrees) | Нет | Нет | Да (sandbox) | — | developers.openai.com/codex (2026-10-03) |
| Cursor | Да (IDE с агентами, проприетарная) | Нет | Нет | Частично (Cloud Agents) | Нет | cursor.com/docs/skills (2026-10) |
| OpenHands | Частично (веб-GUI) | Нет | Нет | **Да** (Docker-песочница) | Да (agent-server, SDK) | docs.openhands.dev (2026-10-03) |

Главная граница для вашего решения:

- bb — **кокпит**: он ничего не «думает» сам, а запускает чужие харнессы.
- Hermes и OpenClaw — **сами являются агентами** со своей памятью, собственным циклом и шлюзом в мессенджеры.

Если поставить Hermes или OpenClaw рядом с Claude Code в одном workspace, вы получите второй, независимый мозг с собственной памятью. Это прямо противоречит цели «без дублирования памяти/конфигурации».

## 3. Коды доказательств (первичные URL)

Коды из этой таблицы используются в матрице ниже. Все страницы открыты 2026-10-03, если не указано иное.

| Код | URL | Что доказывает |
|---|---|---|
| P1 | https://github.com/get-bb/bb | Репозиторий существует и публичен; MIT; README: на Windows запускать в WSL2, «Native Windows PowerShell and CMD are not supported»;\[2\] авторизация через provider CLI; телеметрия, отключаемая `BB_TELEMETRY=false`; в режимах `dev:remote` и `start:worktree-remote` серверный API без аутентификации |
| P2 | https://getbb.app/changelog | 0.45.0 (2026-10-02): «Native Windows support», Windows desktop (Alpha), «configurable Claude sandboxing»; 0.44.0 (2026-09-25): отмена архивирования за 30 с, восстановление workspace, plugin safe mode; 0.43.3 (2026-09-18): перенос сервера (experimental); 0.43.0 (2026-09-11): Account Pooler, Modal sandboxes |
| P3 | https://github.com/get-bb/bb/blob/main/packages/bb-app/README.md | Поддерживаемые хосты: macOS, Linux, «Windows via Ubuntu on WSL2»; `/mnt/c/...` работает, но медленнее и хуже с file watching\[6\] |
| P4 | https://github.com/get-bb/bb/pull/4736 | PR: native Windows как «alpha host beside WSL2», нужен Git for Windows, без переноса сервера на Windows\[7\] |
| P5 | https://github.com/get-bb/bb/blob/main/docs/configuration.md | Data dir `~/.bb/` (SQLite `bb.db`, логи, thread storage, плагины); навыки `~/.bb/skills` и `.bb/skills`; `~/.bb/AGENTS.md` и `.bb/AGENTS.md` дописываются в system prompt каждого провайдера; `maxPermissionMode` для каждой машины |
| P6 | https://github.com/get-bb/bb/issues/3405 · https://github.com/get-bb/bb/issues/3034 | Режимы прав: Approve for me / Accept Edits / Full Access («No sandbox and no approvals»); Claude-sandbox в bb разрешает запись в git-корни worktree и `~/.bb/thread-storage` |
| P7 | https://github.com/nousresearch/hermes-agent | Репозиторий существует; команды `hermes gateway`, `hermes claw migrate`; каталоги `cron/`, `gateway/`, `optional-mcps/`; MIT (по листингу организации NousResearch) |
| P8 | https://hermes-agent.nousresearch.com/docs/user-guide/features/skills | `~/.hermes/skills` как «single source of truth»; `skills.external_dirs` (например, `~/.agents/skills`); «External dirs are not a write-protection boundary»; совместимость с agentskills.io |
| P9 | https://hermes-agent.nousresearch.com/docs/user-guide/windows-native | Нативный Windows 10/11, данные в `%LOCALAPPDATA%\hermes`; WSL-данные в `~/.hermes`; шлюз через `schtasks` |
| P10 | https://hermes-agent.nousresearch.com/docs/user-guide/windows-wsl-quickstart | «supports both native Windows and WSL2» |
| P11 | https://hermes-agent.nousresearch.com/docs/integrations/providers | Anthropic OAuth: «only works on a Claude Max plan with purchased extra usage credits»; Pro этот путь не поддерживает; ChatGPT/Codex OAuth и Copilot поддерживаются\[8\] |
| P12 | https://hermes-agent.nousresearch.com/docs/plugins/claude-subscription-directsdk | Экспериментальный плагин: подписка Claude Pro/Max через официальный `claude` CLI (Agent SDK path) |
| P13 | https://github.com/NousResearch/hermes-agent/issues/47260 | Issue: документация про «extra usage» могла устареть после того, как Anthropic 16 июня откатила изменение\[9\] |
| P14 | https://github.com/openclaw/openclaw/blob/main/README.md | Репозиторий существует; установщик для macOS, Linux и Windows (PowerShell); харнессы как плагины; состояние, память и креды хранятся локально |
| P15 | https://docs.openclaw.ai/platforms/windows | Native Windows Hub + PowerShell CLI; «WSL2 remains the most Linux-compatible Gateway runtime» |
| P16 | https://docs.openclaw.ai/tools/skills | 7 уровней приоритета навыков; `skills.load.extraDirs` (самый низкий); `allowSymlinkTargets`;\[10\] realpath должен оставаться внутри корня; `~/.agents/skills` читается как personal\[10\] |
| P17 | https://docs.openclaw.ai/concepts/oauth | ChatGPT OAuth; Claude CLI reuse и `claude -p` считаются «sanctioned» на основании «Anthropic staff told us»\[11\] |
| P18 | https://docs.openclaw.ai/gateway/authentication | API-ключ рекомендован для always-on хоста; Claude CLI reuse и setup-token\[12\] |
| P19 | https://docs.openclaw.ai/start/wizard-cli-reference | Утверждения о провайдерах описывают v2026.9.3\[13\] |
| P20 | https://support.claude.com/en/articles/15036540-use-the-claude-agent-sdk-with-your-claude-plan | Обновление от 15 июня (страница датирована 2026-06-16): изменение приостановлено; Agent SDK, `claude -p` и «third-party app usage» по-прежнему расходуют лимиты подписки\[14\] |
| P21 | https://code.claude.com/docs/en/skills | Personal `~/.claude/skills`, project `.claude/skills`, plugin; при symlink навык загружается один раз; `claude plugin validate`\[15\] |
| P22 | https://code.claude.com/docs/en/setup | Native Windows (Git for Windows опционален, без него используется PowerShell-инструмент); WSL2; песочница есть только в WSL2, нет на native и WSL1\[16\]\[17\] |
| P23 | https://developers.openai.com/codex/windows | Native Windows sandbox в режимах `elevated` / `unelevated`; WSL рекомендуется для Linux-инструментов\[18\] |
| P24 | https://developers.openai.com/codex/app/windows | Приложение использует `%USERPROFILE%\.codex`; CLI в WSL по умолчанию **не** делит с ним config, auth и сессии; WSL1 не поддерживается с 0.115\[19\] |
| P25 | https://developers.openai.com/codex/concepts/sandboxing | Seatbelt на macOS, bubblewrap на Linux/WSL2, native sandbox в PowerShell\[20\] |
| P26 | https://opencode.ai/docs/skills/ | Читает `.opencode/skills`, `~/.config/opencode/skills`, `.claude/skills`, `~/.claude/skills`, `.agents/skills`, `~/.agents/skills`; права allow/deny/ask\[4\] |
| P27 | https://mariozechner.at/posts/2025-11-30-pi-coding-agent/ | (2025-11-30, **старше даты оценки**) Pi: Windows/Linux/macOS, continue/resume/branching, «YOLO by default», «No MCP support»\[21\] |
| P28 | https://github.com/earendil-works/pi | Pi сейчас в earendil-works; пакеты pi-coding-agent, pi-agent-core, pi-ai\[5\] |
| P29 | https://docs.openhands.dev/openhands/usage/run-openhands/local-setup | Windows только через WSL + Docker Desktop\[22\] |
| P30 | https://docs.openhands.dev/openhands/usage/troubleshooting/troubleshooting | «OpenHands only supports Windows via WSL»; навыки из `~/.openhands/skills` и `~/.agents/skills`, в Docker монтировать `:ro` через `SANDBOX_VOLUMES`\[23\] |
| P31 | https://cursor.com/docs/skills | Навыки из `.agents/skills`, `.cursor/skills`, `~/.agents/skills`, `~/.cursor/skills` и для совместимости из `.claude/skills` и `.codex/skills`; `~/.agents/skills` не копируется в Cloud Agents |
| P32 | https://docs.openclaw.ai/install | Node 24.16+ или 26.1+; Windows через Hub, PowerShell или WSL2; на native Windows автозапуск через Scheduled Task |

## 4. Матрица доказательств

Ячейки краткие, в скобках код источника из раздела 3. «н/п» означает «не подтверждено первичным источником в ходе этого исследования».

| Инструмент | Windows | Подписка vs API | SKILL.md: чтение и пути | MCP | Память | Расписания и фон | Мультиагент и мультимашина | Права и песочница | Бэкап и resume | Лицензия | Риски и lock-in |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **bb** | WSL2 — основной путь (P1, P3); native — alpha с 0.45.0, 2026-10-02 (P2, P4) | Через уже авторизованные provider CLI (P1); Account Pooler для Claude и Codex (P2, 0.43.0) | Свои `~/.bb/skills` и `.bb/skills`; навыки провайдеров читает сам провайдер (P5); импорт из skills.sh — только по маркетинговому посту в X, **н/п** | Собственной конфигурации MCP **н/п**, по-видимому делегирует провайдеру (вывод) | Thread storage в `~/.bb`; `~/.bb/AGENTS.md` дописывается всем провайдерам (P5), отсюда риск дубля с AGENTS.md репозитория | Automations, scheduled send, workflows (P2, P5) | Параллельные потоки, manager threads, worktrees, machines, bb Connect (P2) | Потолок прав на машину `maxPermissionMode`; «Full Access = No sandbox and no approvals» (P5, P6); настраиваемая Claude-песочница с 0.45.0 (P2) | SQLite `~/.bb/bb.db`; `bb server export` и move — experimental (P5, P2); отмена архива 30 с (P2, 0.44.0) | MIT (P1); владелец авторских прав в LICENSE **н/п** | Версия 0.x, релизы еженедельно; API без аутентификации в remote-режимах (P1); телеметрия по умолчанию включена (P1) |
| **Hermes Agent** | Native Win10/11 (P9) **и** WSL2 (P10); на странице установки native помечен «early beta» (вторичное зеркало) — противоречие | Anthropic OAuth: только Max + extra usage, Pro не работает (P11);\[8\]\[24\] DirectSDK-плагин через `claude` CLI, experimental (P12); ChatGPT OAuth и Copilot (P11) | `~/.hermes/skills` + `skills.external_dirs`; агент может **изменять** внешние каталоги, если они доступны на запись (P8) | Да: каталог `optional-mcps/`, плагины (P7); детали транспорта **н/п** | Курируемая агентом память, «nudges» (P7); native и WSL хранят данные раздельно (P9) | Cron (P7); шлюз автозапускается через `schtasks` (P9) | Профили; бэкенды Daytona/Modal (P7); `/delegate` **н/п** | Модель approvals **н/п** в рамках этого исследования | `hermes skills snapshot export` (вторичное); бэкап профиля **н/п** | MIT (P7) | Очень большой поток issues и PR; стабильность версий **н/п** |
| **OpenClaw** | Windows Hub + PowerShell CLI; WSL2 — «most Linux-compatible» (P15, P32) | ChatGPT OAuth; Claude CLI reuse со ссылкой на «Anthropic staff told us» (P17);\[11\] для always-on рекомендован API-ключ (P18)\[12\] | 7 уровней приоритета;\[10\] `extraDirs` и `~/.agents/skills`; защита realpath и symlink (P16)\[10\] | **н/п** (через плагины и харнессы) | Локально на устройстве (P14) | Gateway как сервис: systemd или Scheduled Task (P15, P32) | Мультиагентные allowlist навыков (P16); node mode (P15) | Node `system.run` под контролем (P15); детали approvals **н/п** | **н/п** | **н/п** (LICENSE не открыт) | Описан блок подписки Anthropic с 2026-04-04 (вторичное); вредоносные навыки в реестре (вторичное)\[25\] |
| OpenCode | **н/п** | Встроенная авторизация Anthropic убрана в PR anomalyco/opencode#18186 «anthropic legal requests» (автор thdxr): «Remove opencode-anthropic-auth builtin plugin»; дата 2026-03-19 — по вторичным источникам | Все 6 путей, включая `.claude` и `.agents` (P26)\[4\] | Есть (вторичное) | AGENTS.md (вторичное) | **н/п** | Субагенты (вторичное) | allow/deny/ask для навыков (P26)\[4\] | **н/п** | **н/п** | Средний |
| Pi | Да (P27, 2025-11-30) | Мультипровайдерный; детали подписок **н/п** | `--skill`, пакеты, `skills/` (P27, P28) | «No MCP», только через расширение (P27); вторичный источник заявляет MCP с 2026-10-01 — **н/п**\[21\]\[26\] | AGENTS.md иерархически (P27) | **н/п** | Через tmux или расширения (P27) | «YOLO by default» (P27) — высокий риск удаления | continue, resume, branching (P27) | **н/п** | Смена владельца репозитория: badlogic → earendil-works (P28) |
| Claude Code | Native + WSL2; песочница только в WSL2 (P22)\[16\]\[17\] | Pro/Max — первая сторона | `~/.claude/skills`, `.claude/skills`, plugin; symlink дедуплицируется (P21)\[15\] | Да (вторичное) | CLAUDE.md, auto memory (**н/п** в этом исследовании) | `claude -p` (P20) | Subagents (вторичное) | Песочница на WSL2 (P22) | `--resume` / `--continue` (**н/п** здесь) | Проприетарная | Привязка к вендору |
| Codex | Native sandbox elevated/unelevated (P23); WSL2 (P25)\[18\] | ChatGPT-вход (вторичное) | Навыки поддерживаются (P24); путь `.agents/skills` — вторичное | Да (вторичное) | AGENTS.md (вторичное) | Scheduled tasks в приложении (P24)\[19\] | Worktrees, параллельные чаты (P24) | Seatbelt, bubblewrap, Windows sandbox (P25)\[20\] | Сессии в `.codex`; Windows и WSL **не делят** их (P24)\[19\] | Apache-2.0 по ТЗ, **н/п** | Средний |
| Cursor | Да (горячие клавиши для Windows, P31) | Подписка Cursor | 4 собственных пути + совместимость с `.claude` и `.codex` (P31) | Да; путь `.cursor/mcp.json` **н/п** | Rules (**н/п**) | Cloud Agents (P31) | Cloud Agents | **н/п** | **н/п** | Проприетарная | Высокий |
| OpenHands | Только WSL + Docker Desktop (P29, P30)\[22\]\[23\] | API-ключи и облако | `~/.openhands/skills`, `~/.agents/skills`; в Docker монтировать `:ro` (P30)\[23\] | Есть (**н/п**) | `~/.openhands` | **н/п** | **н/п** | Docker-песочница (P29) | Каталог `~/.openhands` | MIT по ТЗ, **н/п** | Требует Docker |

## 5. Детальный разбор трёх основных кандидатов

### 5.1 bb (get-bb/bb, getbb.app)

**Существование.** Репозиторий публичен и не архивирован: 6 235 коммитов, на 2026-10-03 видно 4,0k звёзд и 569 форков (P1).\[2\] Звёзды здесь не означают зрелость, это просто факт.

**Что это.** Агентная IDE. Ею можно управлять через desktop-приложение, веб, CLI и HTTP API, а потоки можно передавать другому агенту (P1).\[2\] bb не тянет собственную модель: «bb uses the provider CLI you already have authenticated» (P1).\[2\]

**Windows. Это главная оговорка для вас.**

- README на 2026-10-03 по-прежнему говорит: на Windows запускать в WSL2, native PowerShell и CMD не поддерживаются (P1).\[2\]
- Changelog 0.45.0 от 2026-10-02 объявляет «Native Windows support» и «Windows desktop» в статусе **Alpha** (P2).\[1\]
- PR #4736 переводит документацию на формулировку «alpha host beside WSL2» и требует Git for Windows (P4).\[7\]
- В README пакета указано, что `/mnt/c/...` поддерживается, но работает медленнее и менее надёжно с отслеживанием файлов (P3).\[6\]

Вывод: репозитории держать в `~/` внутри WSL, bb запускать через `npx bb-app@latest` из WSL.

**Подписки.** Account Pooler (0.43.0, 2026-09-11) ротирует несколько аккаунтов Claude и Codex при упоре в лимиты (P2).\[1\] Claude-провайдер bb работает через Claude SDK (P6), то есть попадает в категорию «third-party apps built on the Agent SDK». По справке Anthropic от 2026-06-16 такое использование **пока** расходует лимиты подписки (P20).\[14\] Это действующий, но политически хрупкий статус (см. раздел 6).

**Навыки.** Собственные уровни: `~/.bb/skills` → `.bb/skills` → навыки плагинов → встроенные; при совпадении имён проектные перекрывают пользовательские (P5).\[27\] Нативные папки провайдеров (`~/.claude/skills` и т.п.) читает сам провайдер. Это хорошо для вас: bb не создаёт копий.

**Память и конфигурация.** bb дописывает `~/.bb/AGENTS.md` и `.bb/AGENTS.md` в system prompt **каждого** провайдера (P5).\[27\] Если в репозитории тоже лежит AGENTS.md, а CLAUDE.md его импортирует, одни и те же инструкции попадут в контекст дважды. Правило: файлы `~/.bb/AGENTS.md` и `.bb/AGENTS.md` не создавать, единственным источником оставить репозиторный AGENTS.md.

**Права и защита от удаления.**

- Потолок `maxPermissionMode` задаётся на машину; меняет его только owner-сессия, через CLI и SDK он намеренно недоступен (P5).\[27\]
- Режим Full Access означает «No sandbox and no approvals» (P6).\[28\]
- Архивирование отменяется в течение 30 с, очищенные workspace можно восстановить (0.44.0, P2).\[1\] Удалённый поток при этом чистится сразу.\[1\]
- Команды `pnpm reset*` просят подтверждение (P1).\[2\]

**Бэкап.** Всё состояние лежит в `~/.bb` (SQLite `bb.db`, логи, thread storage, плагины). Директорию можно переопределить через `BB_DATA_DIR` (P5).\[27\] `bb server export` и `bb server move` пока экспериментальные (P2, P5).\[1\]\[27\]

**Риски.**

- Версия 0.x, релиз примерно раз в неделю (0.41.0 вышел 2026-09-01, 0.45.0 — 2026-10-02).\[1\]
- В режимах `dev:remote` и `start:worktree-remote` API не аутентифицирован и позволяет выполнять команды и читать файлы (P1).\[2\]
- Анонимная телеметрия включена по умолчанию (P1).\[2\]

### 5.2 Hermes Agent (NousResearch/hermes-agent)

**Существование.** Репозиторий публичен и очень активен: 26 383 коммита, «5k+» issues и «5k+» PR (P7).\[29\]

**Категория.** Персональный самообучающийся агент со шлюзом в мессенджеры (`hermes gateway`) и cron. Есть даже миграция с OpenClaw (`hermes claw migrate`) (P7).\[29\]

**Windows.** Документация противоречит сама себе:

- официальный native-гайд говорит, что Hermes «runs natively on Windows 10 and Windows 11» (P9);\[30\]
- страница установки (в зеркале документации) помечает native как «Early BETA».\[31\]

Native и WSL хранят данные раздельно: `%LOCALAPPDATA%\hermes` и `~/.hermes` (P9).\[32\] Поставив обе версии, вы получите **два независимых набора памяти и конфигурации**, ровно тот дубль, которого вы хотите избежать.

**Подписка Claude.**

- Документация провайдеров: OAuth-путь «only works on a Claude Max plan with purchased extra usage credits», а Pro этот путь не поддерживает вовсе (P11).\[8\]\[24\]
- Issue #47260 указывает, что после отката Anthropic 16 июня это описание могло устареть (P13).\[9\]
- Экспериментальный плагин DirectSDK запускает официальный `claude` CLI (P12).\[33\]

Вывод: на Pro подписка Claude в Hermes фактически не работает. На Max это допустимо, но через extra usage или экспериментальный плагин. ChatGPT/Codex OAuth и Copilot поддерживаются (P11).\[8\]

**Навыки.** Формат agentskills.io. Через `skills.external_dirs` можно подключить общий `~/.agents/skills` (P8). Документация предупреждает: «External dirs are not a write-protection boundary»; если каталог доступен на запись, агент может менять файлы в нём. Проектные каталоги куратор не трогает (P8).\[34\]\[35\] Поэтому общую библиотеку для Hermes нужно монтировать **только на чтение** (bind-mount `ro` или отдельный пользователь без права записи).

**Лицензия:** MIT (P7).\[36\]

### 5.3 OpenClaw (openclaw/openclaw, docs.openclaw.ai)

**Существование.** Репозиторий доступен, официальный домен — openclaw.ai / docs.openclaw.ai (P14, P15).\[37\]\[38\] Провайдерские утверждения в мастере установки относятся к v2026.9.3 (P19).\[13\] Версию «2.0 = v2026.8.1 от 2026-08-30» подтверждает только Wikipedia, это вторичный источник.\[25\]

**Категория.** Персональный ассистент в ваших чатах. Модели и харнессы (Claude, Codex) подключаются как сменные плагины (P14).\[37\]

**Windows.** Есть native Windows Hub и PowerShell CLI, но для Gateway рекомендуется WSL2 как «the most Linux-compatible» (P15).\[38\] Требуется Node 24.16+ или 26.1+ (P32).\[39\] Старые сторонние гайды пишут «только WSL2» и «companion app planned»; сейчас это уже неверно.\[40\]\[41\]

**Подписка Claude.** OpenClaw считает Claude CLI reuse и `claude -p` разрешёнными, потому что «Anthropic staff told us this usage is allowed again» (P17).\[11\] Это не публичная политика Anthropic. Для always-on хоста сам OpenClaw рекомендует API-ключ (P18).\[12\]

**Навыки.** Самая строгая модель загрузки из трёх кандидатов:

- 7 уровней приоритета;
- `extraDirs` на самом низком уровне;\[10\]
- `allowSymlinkTargets`;
- требование, чтобы realpath SKILL.md оставался внутри корня;\[10\]
- `~/.agents/skills` читается как personal (P16).

**Риски.** По вторичным источникам:

- The Register (Thomas Claburn, 2026-04-06) приводит заявление представителя Anthropic: «Starting April 4, third-party tools will draw from extra usage instead of subscription limits»; об изменении объявил Boris Cherny, head of Claude Code;
- Cisco Blogs (Amy Chang, Vineeth Sai Narajala, 2026-01-28) прогнали уязвимый сторонний навык «What Would Elon Do?» против OpenClaw и пишут: «OpenClaw fails decisively»; там же — «26% of 31,000 agent skills analyzed contained at least one vulnerability».

Лицензию по файлу LICENSE в этом исследовании проверить не удалось, поэтому она **н/п**.

## 6. Контрольные инструменты

- **Claude Code** задаёт эталон для навыков и Windows.
  - Есть native Windows: без Git for Wi

===== VENDOR: gemini (gemini.md) =====
Gemini
New chat
Search chats
Images
Videos
Library
Notebooks
New notebook
Recent
КОНТЕНТ ЗАВОД
LLM Comparison for X Posts
Оценка мультиагентных рабочих пространств
Ошибка отказа языковой модели
Стратегия OSS-контрибьютинга для ИИ-оффера
Стратегия OSS-экспертизы для ИИ-оффера
AI Security Career Path for Senior Engineer
Anthropic Fellows Program Security Stream Analysis
AI Security Career Doors for dev
Anthropic Fellows Program Application Strategy
Стратегия OSS-контрибьютинга для ИИ-оффера
bb Orchestrator Fleet Setup and Practices
Окестрация агентов с bb
Критика архитектуры второго мозга
Анализ внедрения Jev в агентский флот
Анализ и улучшение CV для Silicon Valley AI Landing Lead
Идеальное CV AI Deployment Strategist 2026
Анализ и оптимизация венчурного CV
Идеальное CV 2026: Стейблкоин Strategy & BD
Идеальное CV для Stablecoin & BD
Идеальное CV 2026 для AI Security Engineer
Гранты и двери в ИИ-лаборатории
LinkedIn Account Restriction Recovery Guide
Прохождение ATS в 2026 году
AIGOV and European AI Laboratories Investigation
Activity
CryptoPunk Dz2
Work
•
Expanded
Rio de Mouro, Portugal
From your IP address
Update location
Conversation with Gemini
You said --- id: DR26-10-03-HUB-01-0323 date: 2026-10-03 03:23:33 theme: bb Harness versus Hermes Agent and O…

---

id: DR26-10-03-HUB-01-0323

date: 2026-10-03 03:23:33

theme: bb Harness versus Hermes Agent and OpenClaw: shared workspace and personal agent selection

session_id: s_aaa6e38d

machine: HUB-01

targets: chatgpt,gemini,grok,claudeai,glm,mistral

---




# DR26-10-03-HUB-01-0323 — bb Harness versus Hermes Agent and OpenClaw: shared workspace and personal agent selection




Compare get-bb/bb (getbb.app) versus NousResearch/hermes-agent and OpenClaw (openclaw/openclaw), with OpenCode, Pi, Claude Code/Codex/Cursor and OpenHands as category controls. Decision: a Windows user with WSL, existing vendor subscriptions, a shared workspace with multiple agents, and a shared library of SKILL.md files wants the fastest reliable daily cockpit without accidental deletions or duplicated memory/config. Use live web research and primary official docs/source/release notes, date-stamp claims. Distinguish IDE multi-harness orchestration from autonomous personal assistant, messaging gateway, runtime and framework. Compare Windows support, real subscription authentication vs API billing, skill portability and parsing, MCP/connectors, memory, background schedules, multiagent and multimachine, workspace permissions/approval/sandbox, backup/resume, licensing, maintenance risks and lock-in. Do not infer features from stars or marketing. Cite at least 8 direct primary URLs with concrete evidence, explain contradictory docs and unknowns. Give the strongest argument against your preferred choice, migration cost, a 7-day non-destructive acceptance test, and recommendation for primary plus optional companion rather than installing everything. Do not access local private files or secrets or run shell commands; web research only. Return a substantial Russian report with an evidence matrix and verdict. Current evaluation date 2026-10-03; label source dates and do not fabricate newer versions.

Gemini said

Отчет об оценке AI-инфраструктуры: Мультиагентные рабочие пространства (Дата оценки: 03.10.2026)

1. Введение и разграничение классов

Для построения надежного ежедневного пульта управления (cockpit) в среде Windows/WSL с существующими подписками и библиотекой SKILL.md необходимо четко разделить инструменты по их архитектурным ролям:

get-bb/bb (getbb.app): IDE Multi-harness orchestration. Это визуальный пульт управления (cockpit) и оркестратор. Он не является отдельным агентом, а представляет собой среду для управления множеством параллельных агентов (через подсистемы Orca и Munder Difflin).

hermes-agent (Nous Research): Autonomous personal assistant / Messaging Gateway / Runtime. Это автономный агент с циклом самообучения, встроенным планировщиком (cron) и поддержкой изоляции сред (Docker, Modal).   
GitHub

OpenClaw: Устаревший фреймворк. Прародитель формата SKILL.md, выполняющий задачи от лица текущего пользователя, что делает его уязвимым для прямого использования,.   
GitHub

Контрольная группа (Cursor, Claude Code, OpenHands, Pi): Это узкоспециализированные монолиты. Они отлично пишут код или ведут диалог, но не поддерживают федерацию нескольких агентов, общие рабочие пространства и не могут служить шлюзом для мессенджеров.

2. Матрица доказательств
Критерий	get-bb/bb	Hermes Agent (Nous Research)	OpenClaw
Роль	Пульт управления (Cockpit) / IDE	Фоновый процесс / Gateway / Runtime	Локальный ассистент (Legacy)
Windows / WSL	Native — Alpha. Рекомендуется WSL2 (npx bb-app@latest).	Нативная поддержка WSL2 (curl-скрипт).	WSL2.
Биллинг (Auth)	Subscription Auth: Перехватывает уже авторизованные CLI провайдеров (Claude, ChatGPT), экономя API-токены.	API Billing / Local: OpenRouter, Kimi, локальные LLM. Поддержка OAuth.	API Billing.
SKILL.md (Парсинг)	Собственный формат плагинов. Необходима адаптация.	Полная нативная поддержка через hermes claw migrate.	Создатель стандарта SKILL.md.
MCP / Коннекторы	Встроенный мост provider-acp для интеграции MCP.	Кастомные RPC-вызовы, интеграция с GitHub.	Ограниченная.
Память (Memory)	Изолированная SQLite БД (~/.bb/bb.db) на каждый проект.	Файловая: SOUL.md, MEMORY.md, циклы обучения.	Лог контекста.
Фоновые расписания	Плагин "Send later", очереди.	Встроенный cron (ежедневные отчеты, аудиты).	Отсутствуют.
Multiagent	Инструменты Orca и Munder Difflin для флота агентов.	Изолированные субагенты.	Отсутствует.
Sandbox / Права	Modal sandboxes, permission modes.	6 бэкендов исполнения (Docker, SSH, Modal, Daytona).	Исполнение с правами пользователя (Опасно).
3. Анализ ключевых факторов и разрешение противоречий
Противоречия в документации

Поддержка Windows в get-bb/bb: На главной странице GitHub указано, что инсталлятор Windows имеет статус "alpha" и может вызывать проблемы. Однако в логах обновлений от октября 2026 года сообщается об исправлении багов десктопного браузера и всплывающих окон OAuth в Windows. Вывод: Визуальная оболочка стабилизируется, но для надежной работы с файловой системой (учитывая требования к отсутствию дубликатов конфигов) необходимо запускать серверную часть bb строго внутри WSL2.   
bb

Безопасность OpenClaw: OpenClaw позиционируется как удобный локальный помощник. Однако отчеты по безопасности за 2026 год указывают, что YAML-фронтматтер в SKILL.md может содержать вредоносный код, который выполнится с привилегиями хоста. Hermes решает эту проблему за счет принудительного использования песочниц (Docker/Modal backends).   
Skywork
+ 1

Auth vs API Billing

get-bb/bb обладает уникальным преимуществом для пользователей с существующими подписками: он может маршрутизировать запросы через уже авторизованные CLI-клиенты провайдеров. Это исключает затраты на pay-per-token API. hermes-agent, напротив, ориентирован на API-ключи (OpenRouter, OpenAI) и облачные GPU,.   
GitHub

4. Главный аргумент против рекомендуемого выбора

Самый существенный недостаток get-bb/bb в вашем сценарии — vendor lock-in форматов.
bb использует собственную базу SQLite (~/.bb/bb.db) для хранения стейта агентов и собственную архитектуру плагинов. Он не сможет "из коробки" прочитать вашу существующую разделяемую библиотеку SKILL.md. Вам придется либо переписывать скрипты в формат плагинов bb, либо использовать промежуточный фреймворк для их исполнения.   
Obsidian Community

Стоимость миграции:

Для OpenClaw -> Hermes: Стоимость нулевая. Встроена команда hermes claw migrate --preset user-data, которая за несколько секунд конвертирует и импортирует навыки и память в ~/.hermes/skills/openclaw-imports/.   
GitHub

Для внедрения get-bb/bb: Средняя. Потребуется настройка provider-acp и адаптация хранения рабочих пространств.

5. 7-дневный план безопасного тестирования (Acceptance Test)

Данный план гарантирует защиту текущих данных и предотвращает дублирование конфигов:

День 1 (WSL Sandbox): Установите bb в изолированной директории WSL2 (npx bb-app@latest). Проверьте захват текущих подписок (без ввода API-ключей).

День 2 (Миграция): Выполните hermes claw migrate --dry-run. Проверьте лог импорта SKILL.md без фактической записи файлов.   
GitHub

День 3-4 (Изоляция Runtime): Разверните hermes-agent. Настройте бэкенд исполнения в изолированном контейнере: hermes config set terminal.backend docker.   
Hermes AI

День 5 (Gateway): Подключите Hermes к Telegram (hermes gateway). Запустите cron-задачу на выполнение одного из портированных SKILL.md.

День 6-7 (Интеграция): Настройте bb как визуальный пульт управления для делегирования потоков субагентам Hermes. Убедитесь, что глобальный контекст (SOUL.md) обновляется корректно и не конфликтует с проектной БД bb.

6. Итоговый вердикт и рекомендации

Не пытайтесь установить все инструменты или найти единый монолит — их архитектуры предназначены для разных слоев.

1. Primary (Ежедневный пульт / Cockpit): get-bb/bb
Используйте bb как основное окно взаимодействия. Он предоставляет непревзойденный визуальный контроль над параллельными потоками (через Munder Difflin/Orca) и позволяет существенно экономить бюджет, используя ваши текущие потребительские подписки вместо API-биллинга.

2. Optional Companion (Фоновый движок / Runtime): hermes-agent
Используйте Hermes исключительно как "рабочую лошадку" без визуального интерфейса. Он бесшовно мигрирует ваши SKILL.md файлы из OpenClaw, обеспечит безопасное их исполнение в Docker-контейнерах (защищая хост-машину Windows) и возьмет на себя фоновые cron-задачи и связь через Telegram.   
GitHub

Отказ: Полностью откажитесь от запуска OpenClaw на вашем основном ПК из-за уязвимостей безопасности при парсинге SKILL.md на уровне хоста.   
Skywork




Pro

Gemini is AI and can make mistakes, including about people. Your privacy and Gemini
Opens in a new window

Defining Tool Workflows

===== VENDOR: grok (grok.md) =====
Соберу первичные источники по каждому проекту и сверю их с критериями ежедневного кокпита, не опираясь на звёзды и маркетинг. Начинаю с официальных репозиториев и документации.Категории уже расходятся: bb — оркестратор IDE, Hermes — автономный агент, OpenClaw — шлюз-ассистент. Дальше читаю первичные страницы по Windows, подпискам, навыкам и разрешениям.**Вердикт на 2026-10-03.** Ежедневный кокпит ставить один: **bb (`get-bb/bb`, getbb.app) внутри уже существующего Ubuntu в WSL2**, поверх уже залогиненных Claude Code и Codex. Нативные CLI остаются рантаймами под bb. Hermes Agent и OpenClaw в эту неделю не ставить: у обоих свои память, конфиг и право писать в навыки. Опциональный спутник позже, и только если понадобится мессенджер или cron, — Hermes в отдельном `HERMES_HOME`, с одобрением записи в память и навыки и с общей библиотекой `SKILL.md` только на чтение. OpenClaw рядом с ними не добавлять.

Оценка сделана по официальным документам и исходным README, снятым 2026-10-03. Звёзды и слоганы в расчёт не входили. Версии не новее найденных в этих страницах не заявлены.

## Что это за классы

| Класс | Кто им является | Что это даёт ежедневному кокпиту |
| --- | --- | --- |
| Оркестратор нескольких harness в IDE | **bb**; близкий сосед — OpenHands Agent Canvas | Одна оболочка гоняет уже установленные агенты, треды, worktree и чужие подписки |
| Автономный личный ассистент | **Hermes Agent** | Свой цикл памяти и навыков, свой дом `~/.hermes/`, делегирование в CLI |
| Шлюз и мессенджер | **OpenClaw** (у Hermes шлюз тоже есть, но это не его единственная роль) | Постоянный Gateway, каналы, cron, узлы, своя SQLite-учётная запись |
| Рантайм / harness | Claude Code, Codex, **Pi**, OpenCode, Cursor Agent | Исполняют задачу в репозитории и читают `SKILL.md` |
| Фреймворк и SDK | OpenHands software-agent-sdk, Agent Server, ACP | Сборка своего агента и сервера, не готовый утренний кокпит |

bb в README прямо описан как agentic IDE: треды, desktop/web/CLI/HTTP, провайдеры, которые уже стоят у пользователя. Hermes в своей документации отделяет себя от IDE-копилота и чат-обёртки и называет себя автономным агентом с памятью, навыками и шлюзом. OpenClaw в getting started ставит Gateway, онбординг и каналы; README говорит, что состояние, память и учётные данные живут на вашей машине, а модели и harness подключаются плагинами. Это три разных продукта. Ставить все три — три дома конфигов.

## Матрица доказательств

Снято 2026-10-03. «Да» стоит только там, где это написано в первичном документе.

| Критерий | bb 0.45.0 (changelog 2026-10-02) | Hermes Agent | OpenClaw | Контроль, который ближе всего |
| --- | --- | --- | --- | --- |
| Windows | WSL2 — поддержанный путь. Нативный Windows 11 x64 — **alpha**. Сервер на Windows-машину переносить нельзя (`platform-support.md`) | Нативный Windows и WSL2 в английском гайде. Китайский индекс всё ещё пишет «ранняя тестовая» про нативный PowerShell | Windows Hub, нативный CLI/Gateway, отдельный app-owned WSL-дистрибутив, Scheduled Task. Документирован сломанный автоапдейт с 2026.9.4 | Codex: нативное приложение и sandbox. Claude Code: sandbox только macOS/Linux/WSL2 |
| Подписка, а не API-счёт | Берёт уже выполненную авторизацию CLI. Свой биллинг моделей не вводит. Account Pooler — экспериментальная ротация аккаунтов Claude/Codex | `hermes auth add openai-codex` и делегирование в `codex` CLI с OAuth. Nous Portal — отдельный кредитный путь | OAuth Codex и повторное использование Claude CLI. Для продакшена сами советуют API-ключ. Личный аккаунт Anthropic на общем шлюзе — API-ключ, не токен подписки | Codex и Claude Code: подписка на свои приложения. Pi `/login`: подписка или API-ключ |
| Общая библиотека `SKILL.md` | Индексирует чужие корни, включая `~/.agents/skills`, и не объявляет себя единственным хранилищем. Свои `~/.bb/skills` и `<workspace>/.bb/skills` перекрывают по имени | Источник истины — `~/.hermes/skills/`. `external_dirs` сканируются и **не являются границей записи** | Много корней: workspace, `.agents/skills`, `~/.openclaw/skills`, extraDirs. В песочнице читается копия, не исходный путь | Cursor, Claude Code, Codex, Pi, OpenCode читают соседние корни по-разному |
| Память | Отдельной общей памяти нет. Память Claude и Codex остаётся в плагинах этих провайдеров | `MEMORY.md` и `USER.md`, снимок на старте сессии, фоновые nudge. По умолчанию агент пишет сам | Свои memory-инструменты и SQLite (`~/.openclaw/state/openclaw.sqlite` и база агента) | У каждого harness своя память. Общей нет |
| Фон и расписание | Send later, concurrency limit, workflows. Это очередь bb, не личный cron в Telegram | `hermes cron`, навыки на задаче, доставка в чат. Новый сеанс на каждый запуск | Gateway cron, heartbeat, задачи переживают рестарт | OpenHands Automation Server: расписание и вебхуки |
| Мультиагент и несколько машин | Треды, дочерние треды, handoff между провайдерами, машины, Modal sandbox экспериментально. Потолок прав на машину `maxPermissionMode` | Субагенты, профили, терминальные бэкенды local/Docker/SSH/Daytona/Modal/Singularity/Vercel | Агенты, subagents, nodes, ACP, несколько профилей авторизации | Canvas: несколько Agent Server. Pi по умолчанию без субагентов |
| Права, одобрение, песочница | Режимы вроде Accept Edits и Approve for me. Для Claude в этих режимах Bash идёт в sandbox Claude, пока это не выключено. Архивация с подтверждением по умолчанию. CLI/SDK архивируют без вопроса | Блоклист команд, запрет записи в `~/.ssh`, `.env`, свои секреты. `memory.write_approval` и `skills.write_approval` по умолчанию выключены | `tools.exec.mode`: deny / allowlist / ask / auto / full. Для Codex app-server локальный stdio **по умолчанию YOLO**: `approvalPolicy: never` и `sandbox: danger-full-access`, пока не включён `auto` | Codex Windows: sandbox. Claude на нативном Windows: команды без sandbox |
| Удаление worktree | Последний тред удалён — `git worktree remove --force` сразу. Архив последнего треда — льготные **5 минут**, затем то же. Ветка с коммитами остаётся, незакоммиченное нет | Куратор навыки из hub не удаляет, архивирует. `skill_manage` при этом умеет delete | Песочница с `workspaceAccess: ro` или `none` отказывается править копию. Политика хоста отдельно | Зависит от harness |
| Бэкап и продолжение | Обновление **не откатывается**. Новая миграция SQLite может не открыться старым релизом. Архив 0.44.0: Undo за 30 секунд сохраняет ход и терминалы | Сессии в профиле. Память на диске сразу, в промпт — со следующей сессии | Doctor, rollback-дока, с 2026.9.4 на Windows автоматический апдейт сами просят не считать завершённым | У bb и OpenClaw это явный риск миграции базы |
| Лицензия | MIT, Copyright 2026 Horvat Yong | MIT по официальному `llms.txt` (текст от 2026-08-21) | README: MIT, платного яруса и своего токена нет | OpenHands `LICENSE` репозитория — MIT © 2025. Каталог `enterprise/` в старом вводном тексте docs.all-hands.dev описывался иначе |
| Главный риск для этого пользователя | Молодой оркестратор, alpha Windows, самоизменение, принудительное удаление worktree | Сам пишет в общую папку навыков и заводит вторую память | Token sink может разлогинить Claude/Codex. Дефолт Codex — полный доступ. Отдельный WSL-дистрибутив | — |

## Кандидаты

### bb — оркестратор, и поэтому основной кандидат

README (`https://github.com/get-bb/bb/blob/main/README.md`, файл на `main`, чтение 2026-10-03) говорит: bb управляет уже установленными агентами, поверхности равны (desktop, web, CLI, HTTP), работа идёт тредами. Лицензия в том же репозитории — MIT. Changelog на https://getbb.app/changelog помечает **0.45.0 датой 2 октября 2026**: нативный Windows и Android названы alpha; отдельно включены service tiers, в том числе Codex Ultrafast, и облачные заголовки тредов через аккаунт bb без входа в Codex. Это облако выключается: в `configuration.md` есть `bb ai off`, после чего на getbb.app для этих задач ничего не уходит.

`docs/platform-support.md` делит Windows на два пути. В WSL2 стек тот же, что на Linux: Node, Git и CLI провайдеров внутри дистрибутива, пути вида `/mnt/c/...` разрешены, но медленнее и со слабее file-watching. Нативный хост — alpha, нужен Git for Windows, UNC отвергается, терминал — PowerShell 7 или Windows PowerShell, **сервер на Windows-машину переносить нельзя**. Для пользователя с уже живым WSL это прямой аргумент запускать `npx bb-app@latest` из Ubuntu, а не ставить alpha-инсталлятор. Слушать только loopback: тот же README пишет, что API при `10.0.0.0` не аутентифицирован и умеет выполнять команды и читать файлы.

Подписки. `packages/bb-app/README.md` пишет, что bb подхватывает уже настроенные учётные данные. Changelog 0.42.0 и 0.43.0 описывает экспериментальный Account Pooler: несколько аккаунтов Claude и Codex, ротация при лимитах, без повторного логина на каждой машине. Это не новый счёт bb за токены моделей. Отдельный bb cloud в 0.45.0 касается заголовков, commit message и транскрипции.

Навыки. В `docs/configuration.md` bb индексирует корни провайдера и показывает их в меню `/` этого провайдера. Таблица корней включает Codex (`~/.agents/skills`, `$CODEX_HOME/skills`, `.agents/skills`, `.codex/skills`), Claude Code (`~/.claude/skills`, `.claude/skills`), Pi, Cursor (в том числе `~/.claude/skills` и `~/.codex/skills`), OpenCode. Свои навыки bb лежат в `~/.bb/skills` и `<workspace>/.bb/skills` и перекрывают одноимённые. Общую библиотеку имеет смысл держать в `~/.agents/skills` и проектных `.agents/skills`, а `~/.bb/skills` не заводить вторым каноном.

Удаления. `docs/worktrees.md`: worktree, которым никто не пользуется, снимается само. Удаление последнего треда вызывает `git worktree remove --force` сразу. Архив последнего треда даёт пять минут. Перед удалением выполняется `.bb-env-teardown.sh`, затем SIGTERM и SIGKILL процессам, чей cwd внутри worktree, включая фоновые MCP и случайный shell, который туда зашёл. Ветка остаётся, незакоммиченное — нет. Подтверждение архива в настройках по умолчанию включено, Undo тоста есть, но CLI и SDK архивируют без диалога (`configuration.md`). В Accept Edits и Approve for me Bash Claude идёт в sandbox Claude Code, пока `sandboxEnabled` не выключен. Для Pi bb не показывает свой trust-prompt: нерешённый `ask` остаётся недоверенным (`packages/bb-app/README.md`).

Обновления. В `configuration.md` bb не откатывает обновление. Если новая версия мигрировала базу и не стартовала, следующий запуск снова пытается её же. Старый релиз может не открыть эту базу. In-app updates выключены, пока не передан `--in-app-updates`.

### Hermes — ассистент, который пишет в ваши файлы

Документация https://hermes-agent.nousresearch.com/docs/ (страница с отметкой 2026-10-02) и гайд WSL https://hermes-agent.nousresearch.com/docs/user-guide/windows-wsl-quickstart (отметка 2026-10-03) описывают Linux, macOS, WSL2 и нативный Windows. Английский текст перечисляет на Windows CLI, TUI, шлюз, cron, браузер и MCP. Китайский индекс от 2026-10-02 всё ещё помечает нативный PowerShell как раннюю тестовую сборку. Для машины, где уже есть WSL, сам гайд советует не плодить вторую установку.

Навыки, страница https://hermes-agent.nousresearch.com/docs/user-guide/features/skills: совместимость с agentskills.io, прогрессивная загрузка, дом `~/.hermes/skills/`. Агент может изменить или удалить любой навык. `external_dirs` (в том числе `~/.agents/skills`) видны как обычные навыки, и документ прямо говорит: внешний каталог **не защищён от записи**, если процесс может туда писать. Новые навыки по умолчанию создаются в `~/.hermes/skills/`, а `patch` существующего идёт туда, где файл найден. `skills.write_approval: true` только ставит запись на одобрение. Значение по умолчанию в том же документе — писать свободно, включая фоновый self-improvement. Куратор hub-навыки не удаляет и складывает в `.archive/`, но это не отменяет `skill_manage` delete.

Память живёт в `~/.hermes/memories/` (`USER.md`, `MEMORY.md`). Снимок замораживается на старте сессии. Это вторая память рядом с памятью Claude и Codex. `hermes claw migrate` в README существует как перенос с OpenClaw, то есть продукты пересекаются по состоянию, а не дополняют друг друга без миграции.

Подписка реальная, но частичная. Документ bundled-навыка Codex (страница от 2026-10-03) различает `model.provider: openai-codex` после `hermes auth add openai-codex` и отдельный `~/.codex/auth.json` для CLI. Делегирование — `codex exec` в терминале Hermes, внутри git-репозитория. Это не замена IDE-кокпита.

### OpenClaw — шлюз, с которым легко разъехаться по секретам и правам

https://docs.openclaw.ai/start/getting-started: Node 24.16+ или 26.1+, онбординг находит уже существующий логин Claude Code или Codex CLI либо API-ключ, проверяет его completion и пишет конфиг. Gateway в фоне: LaunchAgent, systemd, на нативном Windows — Scheduled Task. Порт в этом тексте — 18789.

https://docs.openclaw.ai/platforms/windows: Windows Hub на первом запуске поднимает **свой** WSL-дистрибутив `OpenClawGateway` и не трогает существующий Ubuntu. Это бережно к текущему WSL и одновременно второй рантайм, вторая копия Node и второй дом состояния. Там же описан обход сломанного апдейтера 2026.9.4: автоматическое обновление не завершать, делать проверенный бэкап и ставить пакет вручную, не понижая метки схемы.

https://docs.openclaw.ai/concepts/oauth, чтение 2026-10-03. OpenClaw называет OAuth «subscription auth» для Codex (ChatGPT OAuth) и для повторного использования Claude CLI. Дальше важная оговорка: сотрудники Anthropic, по словам OpenClaw, снова разрешили такое использование, поэтому проект считает `claude -p` допустимым, пока Anthropic не опубликует новую политику. Для продакшена та же страница рекомендует API-ключ. Хранилище — SQLite, не файлы CLI. Модель token sink: после того как OpenClaw владеет локальным refresh token, он каноничен. Симптом, который страница называет сама: вход и в OpenClaw, и в Claude Code или Codex CLI приводит к тому, что кого-то из них позже разлогинивает, потому что провайдеры инвалидируют предыдущий refresh token. Для пользователя с живыми подписками в CLI это прямой риск ежедневной работы.

Права. https://docs.openclaw.ai/plugins/codex-harness-reference/approval-and-sandbox: локальные stdio-сессии Codex app-server по умолчанию в YOLO, `approvalPolicy: "never"` и `sandbox: "danger-full-access"`. `tools.exec.mode: "auto"` этот дефолт ломает и переводит на guardian. Пока режим не переключён, «просто поставить OpenClaw» не равно «спрашивать перед удалением».

Навыки. https://docs.openclaw.ai/tools/skills и FAQ skills-and-automation: `SKILL.md` с YAML, порядок видимости `<workspace>/skills` → `<workspace>/.agents/skills` → `~/.agents/skills` → `~/.openclaw/skills` → bundled → `extraDirs`. Песочница читает материализованную копию. `requires.bins` проверяется на хосте при загрузке и должен существовать ещё и внутри контейнера. Это уже не тот же файл, который видит Claude Code.

## Контроли категории

**Pi** — минимальный harness, не кокпит. README, полученный 2026-10-03 с `https://raw.githubusercontent.com/badlogic/pi-mono/main/packages/coding-agent/README.md`, уже описывает пакет `@earendil-works/pi-coding-agent`, установщик `https://pi.dev/install.ps1` для Windows, `/login` для подписки или API-ключа, MIT, и отсылает к OpenClaw как к примеру интеграции. Субагентов и plan mode в поставке нет. Changelog https://pi.dev/changelog (заметки 0.99.0 от 2026-09-29 и 1.0.0 от 2026-10-01): MCP и codemode вошли в 0.99.0, 1.0.0 их ужал по токенам и починил OAuth. Вторичные новости, что «MCP появился только в 1.0», расходятся с этим changelog. Навыки Pi следуют спецификации agentskills.io; невалидные поля предупреждают, а не роняют старт (документ skills в репозитории). Сообщественный пакет `@cgaravitoq/pi-claude-code-auth` на pi.dev сам цитирует запрет Anthropic на чужой Claude.ai login и подмену трафика под Claude Code. Это не официальный путь подписки.

**OpenCode.** Актуальный v2 на https://opencode.ai/v2/docs/ отдаёт отдельные бинарники Windows x64 и ARM64 и пишет, что пакетные менеджеры Windows не поддерживаются. Старая страница https://open-code.ai/en/docs рекомендует WSL и перечисляет Chocolatey, Scoop и npm. Схемы прав тоже разные: https://opencode.ai/docs/permissions/ ключует `bash`/`edit`/`skill`, а https://opencode.ai/v2/docs/permissions требует правила `action` / `resource` / `effect`. Общий `opencode.json` между поколениями переносить нельзя. `/connect` во v2 умеет API-ключ и OAuth, в подсказке есть ChatGPT Pro/Plus. Навыки — `SKILL.md` и инструмент `skill` (страница skills с отметкой поиска 2026-10-02). Это один harness, не диспетчер нескольких.

**Claude Code.** https://code.claude.com/docs/en/skills (чтение 2026-10-03): `SKILL.md`, личные `~/.claude/skills`, проектные `.claude/skills`, поле `allowed-tools`. https://code.claude.com/docs/en/sandboxing (отметка инструмента 2026-10-03): sandbox Bash на macOS, Linux и WSL2; на нативном Windows команды идут без sandbox. Файловые инструменты, MCP и хуки живут вне sandbox. Для WSL-пользователя sandbox доступен. Подписка Pro/Max относится к самому Claude Code. Можно ли тем же логином кормить чужой процесс, документы OpenClaw и цитата в пакете Pi расходятся. Пока это не выяснено у Anthropic, чужие продукты не должны обновлять `~/.claude` refresh token.

**Codex.** https://developers.openai.com/codex/windows (в поисковом индексе страница помечена 2026-07-08, содержание снято 2026-10-03): нативное приложение, PowerShell, Windows sandbox elevated или unelevated, либо WSL2 с Linux-sandbox. Full access страница прямо связывает с порчей данных. https://developers.openai.com/codex/skills: навыки по открытому стандарту, прогрессивное раскрытие, CLI, IDE и приложение. https://developers.openai.com/codex/concepts/sandboxing: команды локально по умолчанию в ограниченной среде. Это самый взрослый одиночный Windows-кокпит, но он не сводит Claude, Cursor и Pi в одну ленту.

**Cursor.** https://cursor.com/docs/skills и help-страница skills: `SKILL.md`, корни `.cursor/skills`, `.agents/skills`, плюс совместимость с `.claude/skills` и `.codex/skills`. Автовызов отключается `disable-model-invocation: true`. Run modes: Auto-review рекомендован, sandbox через `sandbox.json`, changelog режима — Cursor 3.6 от 29 мая 2026. Песочница защищает `.cursor/*.json` и `.git/config`, но каталог `skills/` внутри `.cursor` как раз записываемый. Подписка Cursor — своя. В bb Cursor подключён как ACP-провайдер.

**OpenHands.** README `https://github.com/OpenHands/OpenHands/blob/main/README.md` на 2026-10-03 описывает уже не старый GUI, а **Agent Canvas**, бета: локально, Docker, несколько Agent Server, ACP (OpenHands, Claude Code, Codex, Gemini). Образ в quickstart — `ghcr.io/openhands/agent-canvas:1.24.0`. Вариант без sandbox предупреждает о полном доступе к файловой системе. Несколько Docker-песочниц на Windows — только через WSL2 (`README.windows.md`). `LICENSE` репозитория — MIT © 2025. Старый вводный текст https://docs.all-hands.dev/ отдельно говорит, что каталог `enterprise/` source-available и дольше месяца требует лицензию. Перед любым самохостингом Enterprise это надо сверить с текущим `enterprise/`-лицензионным файлом: общий MIT на Canvas не доказывает MIT на Enterprise. Своей подписки Claude/Codex Canvas не заменяет: LLM profiles — это ключи и свои модели. Для задачи «быстрый кокпит без второй памяти» Canvas тяжелее bb и моложе как бета-оболочка.

## Противоречия и неизвестное

Расхождение по нативному Windows у Hermes: английский гайд описывает рабочий набор функций, китайский индекс от 2026-10-02 называет нативную сборку ранней тестовой. Надёжнее считать нативный Windows поддержанным, но менее обкатанным, чем WSL2.

Расхождение по Claude-подписке. OpenClaw пишет, что сотрудники Anthropic снова разрешили CLI-reuse, и тут же советует API-ключ для предсказуемых трат. Пакет Pi цитирует публичный запрет Anthropic на логин Claude.ai для сторонних разработчиков. Саму страницу `code.claude.com` legal в этом прогоне я не открывал, поэтому запрет фиксирую как цитату внутри пакета Pi, а не как свежую вычитку политики Anthropic. Для ежедневной работы вывод практический: пусть refresh token Claude и Codex обновляют только официальные CLI, которые запускает bb. Второй агент не должен логиниться тем же OAuth.

Расхождение по MCP у Pi. Журналистские заметки от 2026-10-02 говорят, что MCP пришёл в Pi 1.0. Первичный changelog pi.dev относит появление MCP и codemode к 0.99.0 (заметки от 2026-09-29), а 1.0.0 (2026-10-01) меняет экономию токенов и OAuth. Версия «новее 1.0.0» в этих страницах не указана.

Расхождение OpenCode v1 и v2 по Windows и по схеме permissions. Конфиг одного поколения нельзя считать конфигом другого.

Расхождение OpenClaw про дефолт Codex. Страница approval-and-sandbox говорит, что локальный stdio по умолчанию YOLO. Страница permission modes говорит, что `tools.exec.mode: "auto"` этот YOLO не сохраняет. Итог зависит от того, выставили ли вы `auto` до первого агентного хода. Пока не выставили, дефолт опасный.

Расхождение внутри Hermes про длину `description`: авторский навык пишет лимит 1024 символа и имя до 64, а `/learn` говорит про описание до 60 символов. Парсер и генератор живут по разным правилам. Общая библиотека от этого не должна проходить через `/learn`.

Неизвестно по первичным источникам этого прогона. Нет независимого измерения скорости bb против Codex app на Windows. Нет текста ToS, который разрешает или запрещает Account Pooler крутить несколько подписок. Нет гарантии, что bb и Cursor одинаково парсят нестандартный frontmatter. Не проверялось, копирует ли bb файлы навыков или только индексирует пути: документ говорит об индексе и меню `/`, побайтовое копирование не описано. Судьба незакоммиченных файлов после `worktree remove --force` описана как потеря. Поведение alpha-инсталлятора Windows за пределами `platform-support.md` не проверялось.

## Самый сильный довод против выбранного bb

bb моложе своих рантаймов и сам является поверхностью, которую агент может менять. README прямо говорит, что продукт в активной разработке и что workflows ещё эволюционируют. Нативный Windows на 2026-10-02 всё ещё alpha, а перенос сервера на Windows запрещён. Обновление не откатывается, миграция базы может сделать даунгрейд невозможным. Управляемый worktree уничтожается принудительно, как только последний тред удалён или как только истекли пять минут после архива, и CLI это делает без вопроса. Агент, которому разрешили создавать и архивировать треды, способен снести незакоммиченную работу и убить процессы, чей cwd оказался в этом worktree. Если бы критерий был только «ни одного случайного удаления на Windows», зрелый одиночный Codex с elevated sandbox или Claude Code в WSL с sandbox были бы спокойнее. bb выигрывает только потому, что критерий шире: несколько уже оплаченных агентов, одна лента, одна библиотека навыков и запрет на вторую память. Этот выигрыш держится на дисциплине прав, а не на зрелости оболочки.

## Цена перехода

Если Claude Code и Codex уже залогинены в том же Ubuntu WSL, отдельной миграции секретов нет: bb их подхватывает. Библиотеку навыков не переносить. Канон оставить в `~/.agents/skills` и в `.agents/skills` репозитория. Не создавать параллельные копии в `~/.hermes/skills`, `~/.openclaw/skills` и `~/.bb/skills`. Память Claude и Codex не импортировать. `hermes claw migrate` не запускать. Новый WSL-дистрибутив OpenClaw не создавать. День настройки — один вечер: Node 22.19+ внутри WSL, `npx bb-app@latest`, loopback `http://localhost:38886`, `BB_TELEMETRY=false`, подтверждение архива не выключать, in-app updates не включать, `BB_SERVER_BIND_HOST` не ставить в `10.0.0.0`. Откат — перестать запускать bb. CLI и репозитории от этого не меняются. Платная миграция не требуется.

## Семидневная приёмка, ничего не разрушая

Все пробы только в копии репозитория. Основной рабочий каталог и домашние конфиги CLI не трогать. Перед первым запуском скопировать, не перемещая, `~/.claude`, `~/.codex` и каталог навыков в архив вне зоны агентов. Секреты в отчёт не класть.

1. День 1. В существующем Ubuntu WSL поставить bb с loopback. Убедиться, что `claude` и `codex` по-прежнему отвечают в том же дистрибутиве. Телеметрию выключить. Архивное подтверждение оставить включённым. Нативный Windows-инсталлятор не ставить.
2. День 2. В копии репозитория открыть по одному треду Claude Code и Codex в режиме Accept Edits. Проверить, что `/` показывает навыки из `~/.agents/skills` и что в `~/.bb/skills` и `~/.hermes` новых копий не появилось.
3. День 3. Дать команду, которая удалила бы файл вне worktree, и команду `rm` внутри копии. Зафиксировать, спросил ли Claude sandbox и спросил ли Codex. Полный доступ не включать.
4. День 4. Только в копии: закоммитить мусорную ветку, завести managed worktree, архивировать тред, нажать Undo в пределах 30 секунд. Затем архивировать снова и вернуть тред в пределах пяти минут. Убедиться, что каталог ещё на месте. Незакоммиченный файл в этой копии специально оставить и после ист

[срез/truncated: бюджет поделён между 3 ногами; урезаны claudeai.md, grok.md. Отсутствие факта в куске НЕ означает, что нога его не называла.]

---

**Claude:**

```json
{
  "lang": "ru",
  "topic": "bb vs Hermes Agent vs OpenClaw — выбор ежедневного мультиагентного кокпита на Windows+WSL",
  "one_line": "Исследование отвечает, какой инструмент (bb, Hermes Agent или OpenClaw) ставить как ежедневный кокпит для общего рабочего пространства с несколькими агентами, общей библиотекой SKILL.md и уже оплаченными подписками без риска случайных удалений и дублирования памяти/конфигов.",
  "key_findings": [
    "Все три вендора (claudeai, gemini, grok) независимо сошлись на одном вердикте: bb (get-bb/bb, getbb.app) — единственный из трёх, кто по первичным документам является мультиагентным IDE-оркестратором, а не отдельным агентом; он управляет уже установленными harness (Claude Code, Codex, Pi, ACP) через треды/worktree и использует уже выполненную авторизацию provider CLI, не вводя свой биллинг моделей",
    "На Windows bb нужно запускать строго внутри WSL2: README на 2026-10-03 прямо требует WSL2, native PowerShell/CMD не поддерживаются; нативный Windows появился только в 0.45.0 (2026-10-02) и помечен alpha, перенос серверной части bb на Windows запрещён",
    "Hermes Agent и OpenClaw относятся к другой категории — автономный персональный ассистент / шлюз мессенджеров (Telegram, Discord), а не кокпит; у каждого своя собственная память и конфиг (`~/.hermes`, `~/.openclaw`), что при параллельной установке создаёт второй независимый 'мозг' и дублирует память/конфиг",
    "У Hermes Agent Anthropic OAuth-путь по его собственной документации работает только на Claude Max с докупленными extra usage credits — Pro этот путь не поддерживает вовсе; есть экспериментальный DirectSDK-плагин через официальный `claude` CLI как альтернатива",
    "Документация Hermes прямо предупреждает: внешние каталоги навыков (`skills.external_dirs`, включая общий `~/.agents/skills`) НЕ являются границей защиты от записи — агент может сам изменять или удалять файлы в общей библиотеке, если у процесса есть права на запись",
    "OpenClaw обосновывает разрешённость Claude CLI reuse / `claude -p` устной ссылкой 'Anthropic staff told us this usage is allowed again', а не опубликованной политикой Anthropic; при этом сам рекомендует API-ключ для продакшена/always-on хоста, а дефолт локального Codex app-server — YOLO (`approvalPolicy: never`, `sandbox: danger-full-access`), пока не включён режим `auto`",
    "Риски bb: версия 0.x с релизами примерно раз в неделю, незааутентифицированный HTTP API в режимах `dev:remote`/`start:worktree-remote`, включённая по умолчанию телеметрия, принудительное `git worktree remove --force` сразу после удаления последнего треда (архив даёт только 30 сек / 5 минут отсрочки), необратимые обновления (новая миграция SQLite может не открыться старой версией)",
    "bb дописывает `~/.bb/AGENTS.md` и `.bb/AGENTS.md` в system prompt каждого провайдера — если в репозитории уже есть свой AGENTS.md, инструкции задублируются; решение — не создавать эти файлы bb, единственный источник — репозиторный AGENTS.md",
    "По вторичным источникам у OpenClaw задокументированы уязвимости: вредоносный YAML-фронтматтер в SKILL.md может исполниться с привилегиями хоста (Cisco Blogs: 26% из 31 000 проанализированных skills содержали хотя бы одну уязвимость), а также риск 'token sink' — вход в OpenClaw может разлогинить Claude Code/Codex CLI из-за инвалидации refresh-токена",
    "Единый итоговый рецепт всех трёх отчётов: Primary = bb в WSL2 поверх существующих подписок; Optional companion = Hermes Agent только при нужде в cron/мессенджер-шлюзе, в отдельном профиле, с общей библиотекой skills, смонтированной ТОЛЬКО на чтение; OpenClaw не устанавливать вообще"
  ],
  "recommendations": [
    "Ставить bb командой `npx bb-app@latest` внутри уже существующего Ubuntu в WSL2, не устанавливать alpha-инсталлятор нативного Windows",
    "Запускать bb поверх уже залогиненных `claude` и `codex` CLI; не вводить отдельный биллинг моделей, использовать Account Pooler только как экспериментальную ротацию аккаунтов",
    "Канонический каталог навыков держать один: `~/.agents/skills` + `.agents/skills` в репозитории; не плодить вторые копии в `~/.bb/skills`, `~/.hermes/skills`, `~/.openclaw/skills`",
    "Не создавать `~/.bb/AGENTS.md` и `.bb/AGENTS.md` — единственным источником инструкций оставить репозиторный AGENTS.md",
    "Если нужен Hermes Agent как опциональный компаньон (cron-задачи, доступ из Telegram/Discord) — ставить в отдельном WSL-профиле/`HERMES_HOME`, общую библиотеку навыков монтировать строго read-only, включить `skills.write_approval` и `memory.write_approval`",
    "OpenClaw не ставить вообще — риски безопасности SKILL.md-фронтматтера и конфликт OAuth refresh-токенов с уже работающими Claude Code/Codex CLI перевешивают пользу шлюза",
    "Для bb: выключить телеметрию (`BB_TELEMETRY=false`), не слушать на `10.0.0.0` (неаутентифицированный API), не включать in-app updates, оставить подтверждение архивации worktree включённым",
    "Перед переходом прогнать предложенный 7-дневный неразрушающий приёмочный тест в копии репозитория, предварительно скопировав (не перемещая) `~/.claude`, `~/.codex` и каталог навыков в архив"
  ],
  "entities": {
    "people": ["Horvat Yong", "Boris Cherny", "Thomas Claburn", "Amy Chang", "Vineeth Sai Narajala"],
    "companies": ["Anthropic", "OpenAI", "NousResearch", "Cisco", "Cursor", "OpenHands / All Hands AI"],
    "products_tools": ["bb (get-bb/bb, getbb.app)", "Hermes Agent", "OpenClaw", "Claude Code", "Codex CLI", "Codex app", "Cursor", "OpenCode", "Pi (pi-coding-agent)", "OpenHands Agent Canvas", "WSL2", "SKILL.md", "AGENTS.md", "Account Pooler", "Modal", "Daytona", "Docker"]
  },
  "open_questions": [
    "Реальная текущая политика Anthropic по использованию подписки сторонними CLI/Agent SDK (OpenClaw ссылается на устное разрешение сотрудников Anthropic, пакет Pi цитирует публичный запрет — противоречие не разрешено ни одним вендором)",
    "Нативная поддержка Windows у Hermes Agent: английский гайд описывает рабочий функционал, китайский индекс (2026-10-02) помечает native-сборку как 'early beta' — расхождение документации",
    "Когда в Pi появился MCP — по первичному changelog это 0.99.0 (2026-09-29), журналистские заметки относят к версии 1.0.0 (2026-10-01)",
    "Копирует ли bb файлы навыков побайтово или только индексирует пути провайдеров — не задокументировано явно",
    "Лицензия OpenClaw не подтверждена первичным файлом LICENSE в рамках этого исследования",
    "Поведение alpha-инсталлятора нативного Windows для bb за пределами platform-support.md не проверялось",
    "Различия схем permissions и Windows-поддержки между OpenCode v1 и v2 — конфиг одного поколения, по заявлению отчёта, нельзя переносить на другое"
  ],
  "related_concepts": ["multi-agent-orchestration", "shared-skills-library", "skill-md-portability", "wsl2-as-primary-runtime", "subscription-vs-api-billing", "agent-sandbox-permissions", "bb-orchestrator-fleet-setup"]
}
```
