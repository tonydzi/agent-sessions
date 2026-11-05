---
session: s_66f15e4b
date: 2026-09-30
words: 1026
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_66f15e4b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-29-HUB-01-0839
REGISTRY TOPIC: bb (get-bb) как оркестратор: кто как использует, LLM поверх bb, интерфейсы (dr_reconcile 2026-09-29: на диске 2/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-29-HUB-01-0839\results)

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


===== VENDOR: report (DR26-09-29-HUB-01-0839.md) =====
---
id: DR26-09-29-HUB-01-0839
date: 2026-09-29 08:39:02
theme: bb (get-bb) как оркестратор: кто как использует, LLM поверх bb, интерфейсы
session_id: bb-interface-voice-7562
machine: HUB-01
targets: chatgpt,gemini,grok,glm,mistral
---

# Deep Research: как мир использует bb (get-bb, getbb.app) как оркестратор агентов, и какие интерфейсы к нему реально работают

## Контекст заказчика
У нас bb-app 0.41.0 уже работает на Linux-VPS (Hetzner, tailnet) как systemd-сервис, web UI доступен по tailnet на :8443. Латест 0.44.0. Флот: Windows-хаб с 2 GPU, Windows/Mac ноутбуки, Linux-VPS-анкер. Агенты на подписках: Claude Code (основной), Codex, Cursor, Grok CLI, Gemini CLI, GLM, Mistral. 100+ рутин в Windows Task Scheduler, межмашинный синк Syncthing, шина Telegram.

## Вопросы (по убыванию важности)
1. КТО И КАК реально использует bb (github.com/get-bb/bb) в проде/ежедневно: найди живые кейсы (блоги, X/Twitter, HN, Reddit, YouTube, GitHub discussions/issues, плагины сообщества). Что за паттерны: bb как ГЛАВНЫЙ оркестратор всего? Или LLM-агент ПОВЕРХ bb, который сам менеджирует остальные (manager thread, агент спавнит агентов в child threads, workflow plugin)?
2. Как люди подключают к bb НЕСКОЛЬКО разных агентов (Claude Code + Codex + Cursor + Grok + OpenCode + Hermes + ACP-агенты) и как делят между ними работу? Роутинг задач: кто планирует, кто исполняет, кто ревьюит?
3. Интерфейсы: web app, desktop (macOS/Linux AppImage), CLI, HTTP API, iOS app / mobile PWA (TestFlight), bb connect relay (yourhandle.getbb.app, до 20 серверов/20 машин). Что из этого люди реально используют для headless-сервера на VPS? Best practice: tailnet-only vs bb connect relay — плюсы/риски (API без аутентификации!).
4. Automations в bb (cron/one-shot) против внешнего планировщика (systemd timers, Task Scheduler): кто как решает конфликт «два планировщика»? Есть ли кейсы миграции существующего парка cron-рутин внутрь bb?
5. Ограничения и грабли 0.42–0.44: workflow plugin, dispatch queue, concurrency limit, split views, plugin safe mode — что из нового реально про мульти-агентную оркестрацию, что сырое (experimental_)?
6. Альтернативы для сравнения одним абзацем каждая: OpenClaw, Conductor, Vibe Kanban, omp, claude-squad и т.п. — есть ли у кого web-UI-поверх-CLI-агентов лучше, чем у bb, для нашего сценария (VPS + флот + свои подписки)?

## Формат ответа
Конкретика с URL и датами. Кейсы поимённо. Отдельным блоком: рекомендованная целевая схема для нашего флота (что оркестратор, где UI, как подключить 4-6 агентов) + риски.

---

**Claude:**

{
 "lang": "ru",
 "topic": "bb (get-bb) как оркестратор мульти-агентного флота: паттерны использования и интерфейсы",
 "one_line": "Постановочный запрос deep-research (без вошедших в присланный текст ответов вендоров) о том, кто и как использует bb в проде как оркестратора агентов, как подключают несколько LLM-агентов и какие интерфейсы/альтернативы подходят для VPS-флота оператора.",
 "key_findings": [
  "Присланный текст содержит только запрос/промпт DR26-09-29-HUB-01-0839 (контекст + 6 вопросов), фактические ответы вендоров (chatgpt/gemini/grok/glm/mistral) в этом фрагменте отсутствуют — тело результатов лежит отдельно в _machine-bus/_dr/queue/.../results",
  "Текущее состояние флота-заказчика на момент запроса: bb-app 0.41.0 работает как systemd-сервис на Linux-VPS (Hetzner, tailnet), web UI на :8443, latest версия bb на тот момент — 0.44.0",
  "Флот состоит из Windows-хаба с 2 GPU, Windows/Mac ноутбуков и Linux-VPS-анкера; агенты работают на подписках: Claude Code (основной), Codex, Cursor, Grok CLI, Gemini CLI, GLM, Mistral",
  "На узлах уже стоит 100+ рутин в Windows Task Scheduler, межмашинный синк идёт через Syncthing, координация — через Telegram-шину",
  "Ключевые открытые вопросы касаются архитектурного выбора: bb как главный оркестратор vs LLM-агент поверх bb (manager thread/child threads/workflow plugin), маршрутизация задач между 4-6 агентами, tailnet-only vs bb connect relay (риск неаутентифицированного API), конфликт bb Automations vs внешний планировщик (systemd timers/Task Scheduler)",
  "Отдельно поставлен вопрос про грабли версий 0.42–0.44 (workflow plugin, dispatch queue, concurrency limit, split views, plugin safe mode) — что зрелое, а что experimental_",
  "Запрошено сравнение с альтернативами: OpenClaw, Conductor, Vibe Kanban, omp, claude-squad — по критерию web-UI-поверх-CLI-агентов для сценария VPS+флот+свои подписки"
 ],
 "recommendations": [
  "Прочитать фактическое тело результатов ДР по пути D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-09-29-HUB-01-0839\\results — в присланном фрагменте ответов нет, дистилляция на их основе невозможна без повторного запроса с полным телом",
  "После получения реальных ответов — свести в целевую схему для флота (что оркестратор, где UI, как подключить 4-6 агентов) и явно оценить риск bb connect relay (API без аутентификации) против tailnet-only варианта"
 ],
 "entities": {
  "people": [],
  "companies": ["Hetzner"],
  "products_tools": ["bb (get-bb, getbb.app)", "Claude Code", "Codex", "Cursor", "Grok CLI", "Gemini CLI", "GLM", "Mistral", "Syncthing", "Telegram", "Windows Task Scheduler", "tailnet", "OpenClaw", "Conductor", "Vibe Kanban", "omp", "claude-squad", "ACP"]
 },
 "open_questions": [
  "Кто и как реально использует bb в проде/ежедневно (живые кейсы из блогов, X/Twitter, HN, Reddit, YouTube, GitHub) — bb как главный оркестратор или LLM-агент поверх bb?",
  "Как люди подключают к bb несколько разных агентов одновременно и как делят между ними работу (планирование/исполнение/ревью)?",
  "Какие интерфейсы bb реально используются для headless-сервера на VPS (web app, desktop AppImage, CLI, HTTP API, iOS/PWA, bb connect relay) и что безопаснее — tailnet-only или relay?",
  "Как решается конфликт «два планировщика» (bb Automations vs systemd timers/Task Scheduler), есть ли кейсы миграции существующих cron-рутин внутрь bb?",
  "Что из нового в bb 0.42–0.44 (workflow plugin, dispatch queue, concurrency limit, split views, plugin safe mode) реально работает для мульти-агентной оркестрации, а что experimental_?",
  "Есть ли среди альтернатив (OpenClaw, Conductor, Vibe Kanban, omp, claude-squad) решение с лучшим web-UI-поверх-CLI-агентов для сценария VPS+флот+свои подписки?"
 ],
 "related_concepts": ["bb-orchestrator", "multi-agent-fleet-routing", "tailnet-vs-relay-security", "automation-scheduler-conflict", "cli-agent-web-ui-alternatives"]
}
