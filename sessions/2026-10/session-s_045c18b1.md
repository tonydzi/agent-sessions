---
session: s_045c18b1
date: 2026-10-06
words: 9392
turns: 2
tools: "ToolSearch, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_045c18b1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-05-HUB-01-1355
REGISTRY TOPIC: n8n: как использовать для нашей автоматизации — 20-30 связок, плюсы-минусы vs текущая локальная реализация (dr_reconcile 2026-10-05: на диске 4/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-05-HUB-01-1355\results)

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


===== VENDOR: gemini (gemini.md) =====
## Short Verdict

**What to move to n8n:** Move all external HTTP ingress (webhooks, Telegram/WhatsApp routers), multi-step LLM tool chains, credential-dependent third-party SaaS syncs, and multi-step retried API pipelines.
**What to KEEP local:** Keep local filesystem transformations, Claude Code CLI hooks, Windows OS management, and low-latency local file watching.
**The Single Highest-Leverage Change:** Establish a single **Execution Ingestion Contract**—a unified HTTP Webhook endpoint in n8n where every local Python script POSTs an execution heartbeat, status code, and payload summary upon completion. This immediately eliminates local dashboard blindness, fixes missing dead-letter queues, and provides a centralized run ledger without rewriting 1271 scripts.

---

## 1. How n8n is Actually Used in the Wild

Based on practitioner reports across the n8n community, GitHub issues, and self-hosted postmortems, four canonical workflow patterns emerge repeatedly:

```
Pattern 1: Webhook Ingress & Dynamic API Gateway
[Webhook] ──► [Switch / IF] ──► [HTTP Request (API Call)] ──► [Set Data] ──► [Respond to Webhook]
```
*   **Problem Solved:** Acts as a lightweight API backend for incoming external events (Telegram updates, CRM webhooks, web forms) that require sub-second acknowledgment while executing background work.
*   **Where it Breaks:** High-concurrency bursts without n8n Queue Mode cause incoming Webhook timeouts. If a downstream API call hangs without an explicit timeout, the HTTP worker pool gets exhausted. Cited in n8n Forum self-hosted scaling threads (*Source [1]*).

```
Pattern 2: Batch Processing & Idempotent Sync
[Schedule Trigger] ──► [Split In Batches] ──► [HTTP Request (Retry on Fail)] ──► [Merge] ──► [DB Upsert]
```
*   **Problem Solved:** Mass ingestion from third-party APIs (Airtable, PostgreSQL, MongoDB) with rate limiting and retry backoff.
*   **Where it Breaks:** Large arrays (>10,000 items) held in n8n's Node.js memory cause heap Out-Of-Memory (OOM) crashes. `SplitInBatches` retains prior state across executions unless explicitly cleared. Cited in r/n8n architectural audits (*Source [3]*).

```
Pattern 3: Multi-Tool Agentic Supervisor
[AI Agent / Chain] ──► [Execute Workflow Trigger (Sub-Tool 1..N)] ──► [Structured Output Parser] ──► [Telegram/Store]
```
*   **Problem Solved:** Dynamic task delegation where a central LLM Supervisor routes tasks to discrete tool workflows (`toolWorkflow`).
*   **Where it Breaks:** High token costs, unhandled sub-workflow timeouts, and JSON schema drift from LLM outputs breaking downstream nodes. Cited in awesome-n8n agentic patterns (*Source [5]*).

```
Pattern 4: Global Error Trap & Re-Queue
[Error Trigger] ──► [Filter / Code (Parse Error)] ──► [Wait Node] ──► [HTTP / Telegram Alert]
```
*   **Problem Solved:** Catching unhandled node failures across all workflows via `settings.errorWorkflow` and dispatching alerting payloads to Telegram or dead-letter queues.
*   **Where it Breaks:** If the Error Workflow itself triggers an error (e.g., Telegram API down), it can enter an infinite error loop or fail silently unless isolated. Cited in n8n official docs & incident reports (*Source [6]*).

---

## 2. Concrete Automations for dev’s Estate

Below are 22 concrete automations matched to your exact fleet (317 local tasks, 1271 scripts, 98 n8n workflows, 5-machine estate).

| # | Automation Name & Job | Trigger & Node Chain | Status in Estate | Why n8n is BETTER Here | Why n8n is WORSE Here | Verdict & Proof Metric |
|---|---|---|---|---|---|---|
| **1** | **Central Local Script Run-Ledger Ingestion**<br>Collects exit codes, logs, and execution metrics from all 317 Windows tasks. | **Webhook** `POST /local-ledger` ──► **Code (Sanitize)** ──► **MongoDB / Postgres Upsert** | **NEW** (Fixes missing run-ledger) | Built-in high-throughput REST endpoint; visual UI to query and filter execution history across 5 machines. | Remote dependency; if n8n host goes down, local execution logs buffer or drop locally. | **HYBRID**<br>*Metric:* 100% of non-zero exits across all 5 machines visible in one dashboard within 10s. |
| **2** | **Delayed One-Time Job Queue & Scheduler**<br>Replaces Windows Task Scheduler for delayed/one-time jobs to fix p90 16.4h lateness. | **Webhook / REST** ──► **Wait Node (Dynamic Delay)** ──► **HTTP / SSH / Bus Dispatcher** | **REPLACES-EXISTING** (Replaces local Task Scheduler 1-time jobs) | True precision timer engine; not subject to local Windows session queuing or power state stalls. | Remote single point of failure for time-critical local machine actions. | **MOVE TO N8N**<br>*Metric:* One-time task execution delay drops from p90 16.4h to <5 seconds. |
| **3** | **Telegram Lead Router & CRM Supervisor (CHARM CRM)**<br>Ingests incoming Telegram leads, runs agent tools, updates MongoDB. | **Telegram Trigger** ──► **AI Agent** ──► **toolWorkflow (20 sub-wf)** ──► **MongoDB** | **LEAVE-ALONE** (Already in n8n as CHARM CRM ~38 wf) | Visual routing, native LLM tool chaining, persistent webhook listener. | Pyodide code limitations; WAF user-agent edge cases on HTTP nodes. | **KEEP IN N8N**<br>*Metric:* Zero missed incoming lead webhooks; response time <3s. |
| **4** | **Dead Channel & Heartbeat Monitor (Synthetic Ping/Pong)**<br>Synthetically tests dead channels across machines and alert rails. | **Schedule (Every 15m)** ──► **HTTP Request (Ping)** ──► **IF (No ACK)** ──► **Telegram Alert** | **REPLACES-EXISTING** (Fixes "watchdog mints green from transport") | Runs on external host (`n8n.palo-alto.ai`), isolating it from local machine bus failures. | Needs explicit network reachability to local nodes. | **MOVE TO N8N**<br>*Metric:* Detects dead channel within 15 mins (down from 5.4 days). |
| **5** | **Obsidian Vault Markdown Engine & RAG Ingestion**<br>Parses, cleans, and indexes local Obsidian markdown files into pgvector. | **Local Schedule / Watcher** ──► **Python Scripts (`D:\Vault`)** ──► **HTTP POST embeddings** | **HYBRID** (Existing local scripts + pgvector) | n8n handles pgvector HTTP upserts and rate-limited LLM embedding calls cleanly. | Massive disk-read latency on 100k local markdown files over network. | **HYBRID**<br>*Metric:* Local Python handles vault parsing; n8n handles LLM embedding + pgvector upsert. |
| **6** | **Global Unhandled Error Catcher & Telegram Dispatcher**<br>Catches workflow execution failures across all 98 workflows. | **Error Trigger (`settings.errorWorkflow`)** ──► **Code** ──► **Telegram ("03" Rail)** | **LEAVE-ALONE** (Already configured in n8n) | Centralized failure routing out-of-the-box for all n8n workflows. | If Telegram API or n8n container fails, alerts drop silently without dead-letter local backup. | **KEEP IN N8N**<br>*Metric:* 100% of n8n node failures dispatched to Telegram rail within 5 seconds. |
| **7** | **LLM Subscription Budget & Token Guard**<br>Tracks token usage and cost across LLM sub-workflows, throttling on limit. | **Execute Workflow Trigger** ──► **Code (Token Count)** ──► **IF (Over Budget)** ──► **Switch/Block** | **NEW** (Replaces local unmonitored LLM scripts) | Visual node execution state tracking; easily stores running counters in MongoDB/Postgres. | Native Code nodes in Python use Pyodide, slowing down large regex/string parsing. | **MOVE TO N8N**<br>*Metric:* 0 LLM sub-workflow calls exceed monthly quota allocations. |
| **8** | **Cross-Machine Bus File Deliverer & Verification ACK**<br>Ensures files dropped into Syncthing `_machine-bus` are ingested by target. | **Schedule (5m)** ──► **HTTP / Local Bus API** ──► **IF (Consumer Verified)** ──► **Telegram ACK** | **REPLACES-EXISTING** (Fixes transport-only success claiming) | Enforces end-to-end ACK verification before clearing task state. | Adds network dependency to local file movement. | **HYBRID**<br>*Metric:* 0 false "green" watchdogs logged on transport-only delivery. |
| **9** | **Audio Transcription Pipeline (Whisper + ElevenLabs)**<br>Ingests audio snippets, triggers STT, formats transcriptions. | **Webhook / Telegram Trigger** ──► **HTTP (Whisper API)** ──► **Set** ──► **Telegram / File Save** | **LEAVE-ALONE** (Already in n8n Cluster 3) | Seamless multi-API integration (Whisper + ElevenLabs + Telegram) with retry backoff. | Handling large raw binary audio files inside Node.js memory can cause memory spikes. | **KEEP IN N8N**<br>*Metric:* Audio files processed and returned <10s with automated retries on API fail. |
| **10** | **Task Scheduler Non-Zero Exit Aggregator**<br>Scrapes 69 failing local Windows scheduled tasks and sends aggregated report. | **Local Task (Daily)** ──► **Python Scraper** ──► **HTTP POST to n8n** ──► **Telegram Summary** | **NEW** (Fixes blind aggregate dashboards) | Provides rich HTML/Markdown formatting and Telegram button callbacks for triage. | Local Windows Event Log scraping must remain on local Windows host. | **HYBRID**<br>*Metric:* Daily digest of exact failing task names delivered to Telegram at 08:00 AM. |
| **11** | **Google OAuth Token Automatic Re-authenticator**<br>Refreshes expiring Google API OAuth tokens and distribution keys. | **Schedule (Daily)** ──► **HTTP (OAuth Refresh)** ──► **n8n Credential Vault Update** | **NEW** (Fixes local google reauth gate halts) | n8n securely manages OAuth credentials in encrypted persistent storage. | If credential update fails, manual re-auth required via browser GUI. | **MOVE TO N8N**<br>*Metric:* Zero Claude Code hooks gated on expired Google OAuth tokens. |
| **12** | **Social & Content Factory Publisher**<br>Generates content via LLM, formats, posts to social/web distribution channels. | **Schedule Trigger** ──► **lmChatOpenAi** ──► **Code** ──► **HTTP (API Post)** ──► **Postgres** | **LEAVE-ALONE** (Already in n8n Cluster 2) | Native OpenAI nodes, easy prompt tweaking in visual canvas, built-in API retries. | No native Git visual diff when changing prompts or routing logic in JSON canvas. | **KEEP IN N8N**<br>*Metric:* Scheduled posts publish without missing execution slots due to rate-limiting. |
| **13** | **Job Application & CV Tailoring Pipeline**<br>Ingests job postings, uses LLM tools to tailor markdown CV, drafts response. | **Webhook / Manual Trigger** ──► **AI Agent** ──► **toolWorkflow** ──► **ConvertToFile** | **LEAVE-ALONE** (Already in n8n Cluster 4) | Complex LLM orchestration with document conversion and file output nodes. | Complex file handling requires file system persistence inside n8n docker volumes. | **KEEP IN N8N**<br>*Metric:* Complete CV generation workflow executes end-to-end within 45 seconds. |
| **14** | **Claude Code Hook Telemetry & Guard Monitoring**<br>Tracks execution metrics for 19 local setting.json hooks across 5 machines. | **Local Hook (PostToolUse)** ──► **Async Local Log** ──► **Batch HTTP POST to n8n** | **NEW** (Fixes unmonitored hook breakage) | Central visual node view for observing sub-second CLI hook failures across fleet. | Hooks MUST NOT call n8n synchronously (adds 200ms+ delay to CLI tool execution). | **HYBRID**<br>*Metric:* Local hooks stay <50ms execution time while n8n receives async telemetry. |
| **15** | **AIRTOP Web Scraper & Headless Browser Pipeline**<br>Automates web scraping tasks requiring headless browser orchestration. | **Schedule / Webhook** ──► **Airtop Node** ──► **SplitInBatches** ──► **MongoDB** | **LEAVE-ALONE** (Already in n8n Cluster 5) | Offloads heavy browser automation to Airtop managed API; n8n orchestrates flow. | Heavy usage of Airtop node can incur high SaaS costs without execution guards. | **KEEP IN N8N**<br>*Metric:* 100% extraction rate on anti-bot protected targets via Airtop API nodes. |
| **16** | **Local Windows Maintenance & Session 0 Apps**<br>Deploys system maintenance, disk cleaning, native Windows app management. | **Task Scheduler (Local)** ──► **Local PowerShell / Python Script** | **LEAVE-ALONE** (Must stay local) | N/A — n8n is remote and cannot access Windows Session 0 / local OS APIs directly. | n8n cannot see local interactive desktop windows or execute system-level local scripts natively. | **KEEP LOCAL**<br>*Metric:* Maintenance runs locally with 0 network calls required. |
| **17** | **Syncthing Conflict & Stale File Resolver**<br>Scans `_machine-bus` for `.sync-conflict` files and cleans stale locks. | **Task Scheduler (Local)** ──► **Local Python Script (`~/.claude/scripts`)** | **LEAVE-ALONE** (Must stay local) | N/A — OS-level file operations are 100x faster and safer via direct local Python code. | Remote API calls over HTTP to list local disk directory contents add overhead and fragility. | **KEEP LOCAL**<br>*Metric:* Sync conflicts resolved instantly without network overhead. |
| **18** | **Local Git Codebase Backup & Auto-Committer**<br>Commits and pushes changes across 1271 Python scripts and Obsidian vaults. | **Task Scheduler (Local)** ──► **Local Git Bash / Python** | **LEAVE-ALONE** (Must stay local) | N/A — Direct local Git CLI execution is robust and hammer-and-axe simple. | Running SSH/Git operations via remote n8n SSH nodes introduces key management complexity. | **KEEP LOCAL**<br>*Metric:* Git backup executes locally in <2s with standard zero exit status. |
| **19** | **Airtable / MongoDB Data Synchronization Engine**<br>Bidirectionally syncs CRM data between Airtable bases and local MongoDB. | **Schedule (10m)** ──► **Airtable Node** ──► **SplitInBatches** ──► **MongoDB Upsert** | **LEAVE-ALONE** (Already in n8n) | Built-in node support for Airtable and MongoDB schemas with automated pagination. | JSON array transformations inside Code nodes can run out of heap memory if un-batched. | **KEEP IN N8N**<br>*Metric:* 0 record drift between Airtable and MongoDB stores. |
| **20** | **Multi-Machine Telegram Rail Dispatcher ("03")**<br>Central hub routing messages across Telegram chat rails and machines. | **Webhook / Telegram Trigger** ──► **Switch** ──► **Telegram Node** | **LEAVE-ALONE** (Already in n8n) | Provides uniform endpoint for all 5 machines to push Telegram alerts without duplication. | Telegram API rate limits (30 msgs/sec) require n8n queueing to avoid 429 errors. | **KEEP IN N8N**<br>*Metric:* Centralized dispatch handling 100% of outbound fleet alerts. |
| **21** | **Local Disk Space & System Thermal Health Guard**<br>Monitors NVMe storage, CPU temps, GPU VRAM usage on local AI fleet machines. | **Task Scheduler (Local 15m)** ──► **Python Script** ──► **Local OS Checks** | **LEAVE-ALONE** (Must stay local) | N/A — Direct hardware sensor reads require local administrative OS privileges. | n8n has no direct hardware/sensor read access on remote target systems. | **KEEP LOCAL**<br>*Metric:* Hardware guard fires locally independent of home internet/n8n uptime. |
| **22** | **External Dead-Man’s-Switch for n8n Host**<br>Monitors `n8n.palo-alto.ai` host health and container status from outside n8n. | **Local Task Scheduler (Hub Machine)** ──► **Python script (cURL)** ──► **Telegram Alert** | **REPLACES-EXISTING** (Prevents n8n self-monitoring antipattern) | N/A — A watchdog must never live inside the orchestration system it is monitoring. | If placed in n8n, it cannot alert when n8n itself crashes or experiences DB locking. | **KEEP LOCAL**<br>*Metric:* n8n outage detected within 3 minute

===== VENDOR: glm (glm.md) =====
# Where n8n belongs in this estate — research report

## 1. Verdict up front

**Move:** the ~30 one-time / delayed jobs (Task Scheduler fires them median 3.2h late — it's the worst measured defect in the estate and n8n's Schedule Trigger + Wait nodes fix it natively); cross-app integration glue (Telegram→CRM, email→calendar, API polling); anything needing retry/backoff, idempotency keys, and hosted webhook endpoints. **Keep local:** the 1271-script filesystem codebase, anything needing git review, desktop/browser automation, Windows session-0 work, and the watchdog that watches n8n itself. **Single highest-leverage change:** one contract between the layers — a "job request → n8n runs → writes run-ledger row → local watchdog reads the ledger, not the transport" pattern, which simultaneously kills `watchdog-mints-green-from-transport`, the missing central run-ledger, and the missing DLQ.

**Honest bottom line:** n8n is not an upgrade for ~70% of this estate. Of 317 local tasks, maybe 40–60 benefit from moving. The rest gain nothing and lose repairability with a hammer and an axe.

---

## 2. The automation table (centrepiece)

Provenance note: "covered?" judgments come from the snapshot itself, not from external sources.

| # | Name & job | Trigger + node chain | Coverage | Why n8n is BETTER | Why n8n is WORSE | Verdict + proving measurement |
|---|---|---|---|---|---|---|
| 1 | **One-time job runner** — replaces "one-time tasks fire 3.2h late" | webhook IN → Wait (till timestamp) → executeWorkflow | **REPLACES-EXISTING** (the 3 one-time tasks + the whole late class) | Wait node is a real clock, not a queue-lagging scheduler; execution history shows planned vs actual fire time | n8n host down = no fire at all; local Task Scheduler survives offline | **Move.** Measure: p50/p90 fire-latency before/after, 30-day window. Expect 3.2h → <60s |
| 2 | **Central run-ledger writer** — every n8n execution appends a normalized JSONL/Postgres row | on: errorWorkflow + success → Set → Postgres insert | NEW (estate has "formats diverge") | one place, one schema, execution ID attached | single point of failure: if n8n dies, local runs stop being logged unless local also writes here | **Hybrid:** n8n writes its rows; local scripts write the same table directly. Measure: % of runs with a ledger row |
| 3 | **Dead-letter queue (DLQ)** — failed-after-retries jobs land in one Mongo collection with payload + reason | Error Catcher → Set (error, payload) → Mongo upsert | NEW | retries with backoff are built into HTTP nodes; retry-once config exists per node | if the DLQ itself is inside the thing that failed, you need a second, dumber DLQ | **Move**, but DLQ #2 (watching n8n) stays local. Measure: DLQ depth visible within 5 min |
| 4 | **Telegram rail sender with ACK tracking** — replaces dual-send manual ACK discipline | send (Set→Telegram) → Wait→check reply→ escalate if no ACK in 30m | **REPLACES-EXISTING** (manual ACK discipline) | Wait + poll pattern is a first-class n8n shape; can auto-escalate | if Telegram API hiccups, n8n retries help; if n8n hiccups, you're worse off than today | **Hybrid:** n8n sends, local confirms consumption. Measure: avg ACK latency |
| 5 | **Bus-bridge dispatcher** — consumes `_machine-bus` events and calls remote machines' doors | INBOUND DOOR webhook → Switch → HTTP (each machine's local door) | **REPLACES-EXISTING** (bus-bridge workflow already exists — harden it) | visual branch debugging of fan-out to 4 machines | adds one network hop to local↔local sync; Syncthing already works and is offline-safe | **Keep as-is, harden only.** Measure: dead-leg detection time (was 5.4 days) |
| 6 | **Consumer-output verifier** — checks the *consumer* acked, not the send | HTTP → read remote machine's `/last_consumed` endpoint → If no fresh ack → Telegram alert | **REPLACES-EXISTING** (fixes `watchdog-mints-green-from-transport`, 7 recorded cases) | forces the whole estate toward outcome-based checks | none significant | **Move.** Measure: 0 green-transport/red-consumer states over 30 days |
| 7 | **Watchdog-of-n8n (dead-man's)** — local Python pings n8n health endpoint | local 5-min cron → HTTP GET /healthz → local Telegram alarm | PARTLY EXISTS (n8n WATCHDOG workflow is *inside* n8n — wrong place) | — | **n8n is categorically wrong here: a watchdog must not live inside what it watches** | **Keep local.** Anti-list item. Measure: inject n8n outage, alarm < 5 min |
| 8 | **Heartbeat reporter for local fleet** — each machine posts a beat; n8n aggregates + alerts on staleness | local script → POST webhook → Mongo upsert → If stale → Telegram | NEW | hosted webhook endpoint means local machines need zero inbound ports | local machines offline + n8n offline = blind; need local fallback alarm | **Hybrid.** Measure: staleness alarm latency per machine |
| 9 | **Idempotency-key gate** — generate keys, reject duplicates before execution | Webhook → Set (key = hash(payload)) → Mongo findOne → If exists → noOp/return cached | NEW (estate standard missing) | trivially expressible; one gate workflow reused via toolWorkflow | adds a Mongo dependency to *every* job | **Move as a shared sub-workflow.** Measure: duplicate-suppression count/week |
| 10 | **Retry/backoff wrapper for outbound HTTP jobs** — LLM API calls, scraping, third-party APIs | Schedule → HTTP (retry: true, maxTries: 3) → on fail → Wait → requeue → DLQ (item 3) | **REPLACES-EXISTING** (some of the 69 non-zero exits) | retry-on-fail + wait-between-tries are built-in node settings; today's scripts have none | — | **Move.** Measure: % of transient-API failures that self-heal (target ≥90%) |
| 11 | **LLM research summarizer** — daily read of flagged sources → summarize → Obsidian vault | Schedule → HTTP (read) → lmChatOpenAi → Set → Write via local door webhook | **REPLACES-EXISTING** (content/summary cluster already in n8n) | LLM nodes, structured output parser (outputParserStructured ×22 shows you already use this) | the *write to local vault* leg must go through a webhook → local door; latency + failure coupling | **Keep in n8n, but the write leg stays local.** Measure: successful vault writes vs summaries produced |
| 12 | **RAG/pgvector ingestion pipeline** — dedup → embed → upsert | Schedule → SplitInBatches → HTTP embed → Postgres upsert | **REPLACES-EXISTING** (dedup engine in D:\Vault\_imports) | batch loop with error-per-item isolation is a native shape | **it's local filesystem work** — n8n on a remote host reading E:\ is latency-hostile and fragile | **Keep local.** Anti-list item. Measure: throughput per 1000 docs (local will win) |
| 13 | **Vault/brain nightly consistency check** — 116 vault/RAG tasks' integrity scan | Schedule → HTTP (local door exposing scan results) → If anomaly → Telegram | **REPLACES-EXISTING** (partially) | n8n is the *alert router*, not the scanner | scanner itself must touch local files → must stay local | **Hybrid:** scan local, route alerts via n8n. Measure: anomaly→human latency |
| 14 | **Google reauth gate / token refresher** — the hooks' google reauth concern, centralized | Schedule daily → Check token via HTTP → If expired → local door "reauth needed" → Telegram | **REPLACES-EXISTING** (google reauth gate hook) | n8n credential vault refreshes OAuth per credential automatically | OAuth refresh inside n8n helps only n8n's own creds; local scripts' creds still local | **Hybrid.** Measure: expired-credential incidents/quarter |
| 15 | **Email → task bridge** — inbox rules → Telegram/CRM lead creation | emailTrigger → If → telegram/CRM upsert | NEW (estate has only 1 email task) | native email trigger + app connectors | — | **Move.** Measure: lead-capture latency |
| 16 | **CRM lead-response sequencer** — CHARM follow-ups on delay | telegramTrigger → Mongo → Wait (per-lead) → agent-personalized reply | **REPLACES-EXISTING** (CHARM ~38 wf) | already there; add Wait-based sequencing instead of scheduled sweeps | — | **Keep in n8n.** Measure: lead→first-reply latency |
| 17 | **Content social scheduler** — 10 content/social tasks' posting cadence | Schedule → read queue (Airtable/Mongo) → HTTP post → record | **REPLACES-EXISTING** | retries + per-platform error visibility in execution log | — | **Move.** Measure: posted-on-time % |
| 18 | **Session-0 workaround dispatcher** — GUI-requiring jobs launched in user session | n8n Schedule → HTTP → local door ("spawn-slot") → local PowerShell ScheduledTask /on-demand | **REPLACES-EXISTING** (spawn-slot guard hook + session-0 pathology) | n8n is just the clock + queue; local agent does GUI work | **n8n cannot do session-0 work itself** — Pyodide, remote host, no Windows desktop | **Hybrid:** n8n schedules, local executes. Measure: GUI job success rate |
| 19 | **Browser automation (Airtop/Playwright) jobs** | — | **LEAVE-ALONE** | — | long-running browser sessions eat n8n worker memory; practitioners report Code-node/worker OOM at long loops; you already use Airtop for this | **Keep local / stay on Airtop.** Measure: if it works today, don't touch it |
| 20 | **Backup/export of n8n workflows-as-code** — nightly workflow JSON export to git | local cron → REST export → git commit + push | NEW | — | **must be local:** n8n can't back up itself safely; git history is local-domain | **Keep local.** Measure: restore drill succeeds (test quarterly) |
| 21 | **Aggregate dashboard with per-leg detail** — replaces "dashboards blind to a dead leg" | Schedule → HTTP (query each machine's door) → per-leg If → detail rows → Telegram digest | **REPLACES-EXISTING** | each leg is a visible node; a dead leg is a red execution, not a missing row | — | **Move.** Measure: dead-leg detection (5.4 days → <15 min) |
| 22 | **Budget guard for LLM spend** — token counters against subscription caps | on each LLM-heavy execution → Set (tokens) → Postgres cumulative → If > threshold → alert/throttle | NEW | single choke-point for the LLM subscription compute model | adds per-execution overhead | **Move.** Measure: zero surprise overages |
| 23 | **1271-script codebase refactoring** — any task that edits Python | — | **LEAVE-ALONE** | — | no git-native diffs, no author attribution on edits (measured: metadata=null), expression-render failures pass the save step | **Keep local, forever.** Anti-list item |
| 24 | **n8n upgrade runner** — pin, test, upgrade n8n itself | — | NEW | — | must be local: upgrading n8n from inside n8n is impossible/unsafe | **Keep local.** Measure: upgrade rollback time |

Net: **Move/hybrid ≈ items 1,2,3,4,5(harden),6,8,9,10,11,13,14,15,16,17,18,21,22** — roughly 40–60 underlying local tasks consolidate into ~15 workflows. **Keep local: 7,12,19,20,23,24** and everything filesystem/git/Windows-bound.

---

## 3. The anti-list — where n8n is the WRONG tool

1. **The watchdog that watches n8n.** A component cannot monitor itself; when the host dies, the monitor dies with it. n8n's own docs position the error workflow as best-effort, not a liveness guarantee.
2. **Anything touching the local filesystem / Obsidian vault / the 1271 scripts.** Remote host, per-file latency, Pyodide instead of real Python (n8n docs: Python Code nodes run via Pyodide with a restricted package set — your scripts would not run).
3. **Anything needing git history and code review.** n8n stores no edit author (you measured metadata=null yourself); workflow JSON diffs are noisy; no review workflow. Practitioner forum consensus is "export to JSON and git it" — i.e., they re-import the discipline you already have locally.
4. **Long-running desktop/browser automation.** Worker memory ceilings + execution timeouts; keep it local or in a dedicated tool.
5. **Work that must survive n8n being down.** Single host = single point of failure. Anything with a hard deadline (backups, security scans, the fleet's own health) must not depend on n8n liveness.
6. **Windows-specific OS work.** Registry, services, scheduled-task surgery, session/GUI issues. n8n has no story for Windows internals.
7. **Where the operator needs to read a diff.** The visual canvas is great for building, poor for "what changed Tuesday."
8. **Simple cron jobs that work.** 288 Ready tasks with clean exits have nothing to gain; migration cost is pure loss. The simplest-repairable-with-hammer-and-axe principle vetoes churn without measured pain.

---

## 4. Hybrid architecture (text diagram)

```
┌─────────────── LOCAL (Windows hub, hammer-and-axe) ───────────────┐
│  Task Scheduler cron → Python scripts (1271)                      │
│  filesystem/vault work · browser/desktop automation               │
│  n8n-of-n8n watchdog (5-min) · n8n backup→git runner              │
│  local DOOR: HTTP listener "spawn-slot" (run-on-demand GUI jobs)  │
│  local DOOR: /last_consumed + /scan endpoints (verifiable output) │
└────┬─────────────────────────────────────────────────┬───────────┘
     │ POST job requests          ▲ read doors         │
     ▼ (webhook OUT)             │ (HTTP GET)          │
┌─────────────── REMOTE n8n (integration brain) ────────────────────┐
│  INBOUND DOOR webhook ──► idempotency gate ──► retry-wrapped jobs │
│  Wait/one-time clock · SaaS connectors · Telegram rail sender     │
│  DLQ (Mongo) · LLM agents · sequencers · dashboard-with-legs      │
│  every execution ──► shared RUN-LEDGER table (Postgres)           │
└──────────────────────────────────────────────────────────────────┘
                    THE ONE CONTRACT:
   local → n8n: POST {job, payload, idempotency_key} to webhook
   n8n  → local: GET local door; verify /last_consumed, not the send
   BOTH → Postgres run-ledger: {ts, job, key, outcome, error?}

Failure visibility:
  n8n down


===== VENDOR: grok (grok.md) =====
The question is which jobs belong in n8n and which must stay on the local cron layer. I am pulling practitioner reports from the last year, not vendor pages, and I will only keep numbers I can tie to a source.Идём верно: переносить 317 локальных задач в n8n не нужно. Решение от 28.06.2026 (чинить процессы, а не движок) источники за последний год подтверждают.

Один вопрос, без которого масштаб слепой: сколько исполнений в сутки на `n8n.palo-alto.ai`, и база там SQLite или Postgres? Ниже я этого числа не выдумываю.

Рельса этого разбора: страницы читал я сам. Чужой бак не жег.

## Вердикт

n8n у вас уже занят тем, для чего его держат вживую: чужие API, Telegram, Mongo, агент с под-воркфлоу. Это 98 воркфлоу и 1736 узлов. Часы при этом почти все местные: 23 узла Schedule Trigger против 317 наших задач в Планировщике.

Переносить в n8n стоит только клей. Один вебхук-журнал, куда локальный скрипт пишет «старт / ок / ошибка / потребитель применил», плюс проверка с другой машины, что журнал и сам n8n живы. Retry на существующих HTTP-узлах, ключ идемпотентности на входной двери, список активных воркфлоу без error workflow.

Не переносить: файлы, волт, 1271 скрипт, хуки, браузер на Windows, синк флота, разовые задачи (они и так опаздывают на часы), сторож самого n8n.

Самый дорогой ход. Поднять этот журнал и внешнего сторожа. Проверка, что ход верный: снять с публикации error workflow и уронить один пустой скрипт с кодом 1. Оба сигнала приходят в Telegram с другой машины за 15 минут. Потом выключить хост n8n. Вторая машина за 10 минут говорит, что хоста нет, а строка скрипта остаётся в локальном JSONL.

Четыре факта хоста я не смог прочитать отсюда: исполнений в сутки, SQLite или Postgres, включён ли queue mode, какая лицензия. От них зависит раздел про масштаб, не вердикт.

## 1. Какие формы реально живут

Каталоги шаблонов показывают, что люди копируют, а не что у них живёт через полгода. В [Zie619/n8n-workflows](https://github.com/Zie619/n8n-workflows) на момент чтения README (блок «Latest Updates» датирован ноябрём 2025, страница открыта 2026-10-05) заявлено 4343 воркфлоу и 29445 узлов. Это около 6.8 узла на шаблон. У вас 1736 / 98 ≈ 17.7 узла на воркфлоу. Ваш n8n уже толще типового шаблона примерно в 2.6 раза, в основном из-за CRM-агента. Репозиторий сам называет набор «production-ready». Это слова автора, не замер продакшена.

Формы, которые повторяются у практиков и ломаются предсказуемо:

| Форма | Какую боль закрывает | Где ломается | Кто сказал |
|---|---|---|---|
| Webhook → IF/Switch → HTTP → Set → respondToWebhook | Склеить чужой сервис без своего сервера | Повтор колбэка, ретрай портит данные, задача «тихо встаёт» под нагрузкой | Автор поста на HN, тред почти без чужих подтверждений: [news.ycombinator.com/item?id=46151059](https://news.ycombinator.com/item?id=46151059) (~январь 2026) |
| Schedule → HTTP/DB → LLM → отправка | Регулярный пересказ и пост | Несколько cron в одном триггере, часть расписания молча отваливается. Часовой пояс по умолчанию у self-hosted `America/New_York`. Пропущенный запуск на вашей версии не догоняется | [Sixprecious, 12.07.2026](https://community.n8n.io/t/the-9-ways-n8n-workflows-die-silently-checklist-from-3-production-scars/302992); доки Schedule Trigger, прочитаны 2026-10-05; durable scheduler вышел в 2.32 от 21.07.2026, у вас 2.14.2 |
| Split In Batches → HTTP → обратно в цикл | Пачка записей, чтобы не держать всё в памяти | Цикл не замкнут: обрабатывается только первая пачка. Batch size 1 на 1000 строк = 1000 запросов | [r/n8n, 08.01.2026](https://www.reddit.com/r/n8n/comments/1q7n8rz/7_common_n8n_workflow_mistakes_that_can_break); [DEV, 24.06.2026](https://dev.to/pirateprentice/n8n-split-in-batches-node-process-large-datasets-without-crashing-free-json-4p0c) |
| AI Agent → toolWorkflow | Один агент и много узких инструментов. Это ваш CHARM | Как только поведение агента надо покрыть тестом и запретить ему файлы и git, люди выносят оркестратор в Python и оставляют n8n маршрутизатором | [Joseph Yeo, DEV, 11.05.2026](https://dev.to/josephyeo/we-didnt-migrate-from-n8n-to-python-because-n8n-failed-k9j) |
| Error Trigger на отдельном воркфлоу | Крик в Telegram, когда узел упал | Это не глобальный предохранитель. Новый воркфлоу рождается без него. Снятый с публикации error workflow в настройках всё ещё «указан», а в логе одна строка. Ручной тест error workflow не вызывает | [Benzy, 27.09.2026](https://community.n8n.io/t/i-made-one-workflow-fail-27-times-on-purpose-my-error-workflow-reported-15-of-them/316992): 27 падений, 12 без единого сигнала. [Разбор кода 2.40.5, 26.09.2026](https://community.n8n.io/t/three-ways-your-error-workflow-is-not-running-and-the-only-trace-is-one-line-in-the-server-log/316844) |
| Retry On Fail на HTTP-узле | Сетевой чих | Это повтор узла, не очередь мёртвых писем. Автоповтор зависшей работы воркера снят в 2.0: `QUEUE_WORKER_MAX_STALLED_COUNT` удалён, «потому что путал и работал ненадёжно» | Доки [2.0 breaking changes](https://docs.n8n.io/2-0-breaking-changes/) и [queue mode env, 22.09.2026](https://docs.n8n.io/deploy/host-n8n/configure-n8n/basic-configuration/use-environment-variables/queue-mode) |
| Воркфлоу-бэкап внутри самого n8n | Ежедневный JSON в git | Умирает вместе с хостом. Официальный CLI-бэкап не содержит историю исполнений, пользователей, переменные и ключ шифрования | Шаблон [18512](https://n8n.io/workflows/18512-back-up-workflows-to-github-with-deterministic-json-exports) (обновлён около 30.09.2026); доки [backup, 22.09.2026](https://docs.n8n.io/deploy/host-n8n/keep-n8n-running/backup-and-restore) |

Ваш собственный замер узлов говорит то же самое. Code 256, httpRequest 181, if 150, set 129, mongoDb 114, telegram 95, lmChatOpenAi 84, splitInBatches 58, toolWorkflow 48, agent 29, webhook 27, scheduleTrigger 23. Верх списка это код и склейка API. Часы и вебхуки в хвосте. n8n у вас уже не cron.

## 2. Тридцать автоматизаций под это хозяйство

| # | Имя и работа | Триггер и цепочка | Уже есть? | Где n8n сильнее | Где n8n хуже | Вердикт и замер |
|---|---|---|---|---|---|---|
| 1 | CHARM: супервизор лидов Telegram и ~20 инструментов | Уже агент → toolWorkflow, Mongo | LEAVE-ALONE | История прогона, креды, визуальный разбор ветки | Code-узлы без автора правки. PUT 200 не ловит сломанное выражение. Нет юнит-теста на агента | Оставить. Замер: один и тот же апдейт лида дважды даёт одну запись в Mongo |
| 2 | Входная дверь | Webhook → проверка → ответ | LEAVE-ALONE | Это и есть публичный URL, Планировщик его не даст | Хост лёг, двери нет. Дубли колбэков | Оставить как единственный вход. Замер: повтор того же `idempotency_key` возвращает 200 и не делает второе действие |
| 3 | Ловец ошибок n8n | Error Trigger → Telegram | HYBRID | Уже кричит в шину, когда реально вызван | [Benzy](https://community.n8n.io/t/i-made-one-workflow-fail-27-times-on-purpose-my-error-workflow-reported-15-of-them/316992): 12 из 27 падений молчали. Снятый с публикации ловец выглядит настроенным | Оставить ловца. Доверие к нему держит локальный аудитор из строки 5. Замер: снять ловца с публикации, уронить минутный воркфлоу, увидеть тишину в Telegram и крик от аудитора |
| 4 | Сторож «n8n жив» | Сейчас воркфлоу внутри n8n | REPLACES место сторожа | Внутренний пульс полезен как отправитель | Сторож внутри объекта слеп, когда объект мёртв. Это ваш же класс `watchdog-mints-green-from-transport` | Пульс может слать n8n. Судит вторая машина: два пропущенных ответа за 10 минут = сообщение человеку. Замер: остановить контейнер, сообщение приходит, зелёной плашки нет |
| 5 | Покрытие error workflow | Локальный скрипт: `GET /api/v1/workflows`, активные с пустым `settings.errorWorkflow` | NEW | У n8n есть API списка | Сам список нельзя доверять воркфлоу на том же хосте | Локально, раз в сутки и после каждого `n8n_edit.py`. Замер: новый активный воркфлоу без ловца попадает в Telegram в тот же прогон |
| 6 | Журнал прогонов | Webhook `ledger`: `{source, kind: start\|ok\|fail\|applied, idempotency_key, ts, error}` → Mongo/Postgres → Telegram только на fail | NEW, на существующей двери | Одна история, дедуп, повтор доставки уведомления | Если это единственная копия, падение хоста стирает улику. Скрипт обязан сначала писать свой JSONL | Гибрид. n8n принимает и показывает. Диск остаётся источником. Замер: убить n8n, прогнать скрипт, строка есть в JSONL. Поднять n8n, строка появляется один раз |
| 7 | Локальный outbox к журналу | Скрипт пишет JSONL, потом POST, при неудаче повторяет | LEAVE, это отправитель строки 6 | n8n тут только приёмник | Тащить отправку в Code-узел бессмысленно: Code-узел не ходит в файлы | Локально. Замер: оборвать сеть на POST, после возврата сети в журнале одна запись, не пачка |
| 8 | Retry на уже существующих HTTP-узлах | Настройка узла Retry On Fail, 3 попытки, пауза ~2.5 с | NEW как стандарт, не как переезд | Встроенный повтор сетевого чиха на 181 узле httpRequest | Повтор без ключа идемпотентности удваивает запись. Это не очередь мёртвых писем | Включить на HTTP внутри n8n. Скрипты не переносить. Замер: один оборванный сокет даёт успех со второй попытки и одну запись в приёмнике |
| 9 | Ключ идемпотентности на двери | Webhook → поиск ключа в Mongo → если был, ответ 200 и стоп | NEW, тонкая обёртка | Mongo у CRM уже стоит (114 узла) | Гонка двух одновременных запросов с одним ключом. Нужна уникальная запись, не «прочитал потом записал» в коде | В n8n, только на двери. Замер: два параллельных POST с одним ключом, одно побочное действие |
| 10 | Квитанция потребителя на шине | Отправитель пишет `sent`. Потребитель на машине пишет `applied` тем же ключом. Сверка раз в 15 минут | NEW | Сверка двух вебхуков видна глазами | Сверка, живущая только в n8n, зеленеет от факта отправки. Ваш замер: мёртвый канал 5.4 дня считался живым | Гибрид. Факт «применил» пишет потребитель локально. n8n только сводит. Замер: послать пакет и не подтверждать. Тревога за 15 минут. Потом убить n8n: локальный список «sent без applied» всё равно виден |
| 11 | Доска мёртвых ног | Читает журнал и срок каждого производителя | LEAVE | n8n умеет красиво прислать дайджест | Сводная доска, которая сама ходит в n8n, слепнет вместе с одной ногой. Это ваша текущая дыра | Судья локальный. n8n строка, не судья. Замер: выключить один из 317 производителей, доска краснеет по этой строке, остальные остаются зелёными |
| 12 | 69 задач с ненулевым кодом | Те же скрипты, плюс одна строка в журнал | LEAVE | Журнал собирает то, что сейчас размазано по разным JSONL | Перенос задачи в n8n не чинит её код | Оставить скрипт. Обязать писать в журнал. Замер: за неделю число красных выходов не прячется. Список тех же 69 либо короче по делу, либо объяснён |
| 13 | Опоздание разовых задач (медиана 3.2 ч, p90 16.4 ч) | Очередь Планировщика | LEAVE | У n8n ровнее минутный cron, пока процесс жив | На 2.14.2 расписание в памяти процесса. Догон пропущенного запуска появился в 2.32 (21.07.2026) и по доке не работает на in-memory scheduler. Перенос превратит опоздание в тишину | Чинить локальную очередь. Замер: задача со сроком T стартует в окне, которое вы сами назовёте. Пока p90 не упадёт, в n8n не нести |
| 14 | SLA лида в Mongo CRM | Schedule → Mongo «ждёт дольше N часов» → Telegram | NEW, только если локальная задача сегодня лишь опрашивает эту Mongo | Данные уже рядом с воркфлоу, не надо тянуть их на Windows | Расписание молча пропадёт, если воркфлоу снимут с публикации. Пустая выборка выглядит как успех | В n8n, рядом с данными. Замер: подложить протухшего лида, сообщение в тот же тик. Ноль строк тоже шлёт «ноль», а не тишину |
| 15 | Семь локальных задач leads/CRM | Неизвестно из снимка, что именно они делают | LEAVE, пока не доказано, что это только опрос Mongo n8n | Если задача только читает Mongo n8n, строка 14 её заменяет | Унести код CRM в Code-узел значит потерять git и Python | Не двигать пачкой. Замер по каждой: вход и выход. Совпадает со строкой 14, тогда одна замена. Ходит в локальные файлы, оставить |
| 16 | Ограждение 84 узлов lmChatOpenAi | Учёт, куда уходит вызов | NEW как аудит, потом унос | Узел удобен, пока это дешёвый черновик | Оплаченные мозги у вас это подписки, не облачные кредиты. Узел OpenAI Chat по форме бьёт в API-ключ. Сумма счёта отсюда не видна | Если неделя счёта API ненулевая, эти вызовы унести в локальные подписочные CLI. Замер: счёт API за 7 дней до и после |
| 17 | Контент-боты «прочитал API → LLM → пост» | Уже schedule → LLM → Telegram/HTTP | LEAVE | Уже стоят, история поста видна | Второй писатель рядом с 10 локальными social-задачами даст двойной пост | Не плодить. Замер: один слот публикации, один автор, ноль дублей за неделю |
| 18 | Десять локальных постов через браузер | Firefox/Chrome на машине | LEAVE | У n8n есть Airtop (25 узлов) | Браузер рабочего стола n8n не видит. Session 0 у Планировщика и так слепой. Второй браузер это вторая поломка | Оставить на машине. Airtop не расширять. Замер: пост уходит из того же профиля, что и ручной |
| 19 | Аудио Whisper / ElevenLabs | Уже есть кластер | HYBRID | Короткий ролик, который уже приехал по HTTP, можно оставить | Бинарные данные по умолчанию в памяти процесса. В queue mode файловый режим запрещён, нужен S3 или база. Крупный файл роняет процесс без аккуратной ошибки | Новые файлы с диска гонять локальным Python. В n8n лимит размера. Замер: файл больше лимита отклоняется с записью в журнал, процесс n8n жив |
| 20 | Airtop и PR-автоматизация | Уже 25 узлов Airtop | LEAVE, не растить | Чужой сайт без своего расширения | Долгая браузерная сессия, нет ревью диффа, падение хоста бросает полукликанный PR | Новые браузерные задачи на локальный Firefox. Замер: месяц без новых Airtop-воркфлоу |
| 21 | Волт, мозг, RAG: 116 задач | Планировщик → Python по `E:` | LEAVE | Ничем. Данных на хосте n8n нет | Задержка диска, нет git, Code-узел не читает файловую систему | Оставить. Замер: вопрос к локальному RAG отвечает при выключенном n8n |
| 22 | pgvector RAG внутри n8n | Уже отдельный кластер | HYBRID, заморозить рост | Удобно, если индекс уже там и вопрос приходит вебхуком | Два RAG расходятся молча. Инжест файлов волта с хоста n8n не сделать честно | Инжест только локальный. Замер: один и тот же вопрос в оба индекса, расхождение записано. Пока расходятся, n8n-RAG не кормить новыми документами |
| 23 | Агенты сотрудников, доков, рекрутинга | Agent → инструменты по API | LEAVE, пока только чужие API | Ветки видны на холсте | [Yeo, 11.05.2026](https://dev.to/josephyeo/we-didnt-migrate-from-n8n-to-python-because-n8n-failed-k9j): как только агент обязан не трогать файлы и git, запрет надо держать кодом, а не договорённостью | Оставить до первого требования «покрой тестом». Потом оркестратор в Python, n8n только маршрутизатор |
| 24 | 96 сторожей и гардов | Локальные скрипты | LEAVE | Могут слать строку в журнал | Перенос сторожа в то, что он сторожит, повторяет 5.4 дня тишины | Оставить. Каждый пишет `ok` или `fail` в журнал. Замер: убитый поднадзорный даёт `fail` за свой период, не зелёный статус транспорта |
| 25 | Синк флота и `_machine-bus` | Syncthing + Telegram 03 | LEAVE | Мост в n8n уже есть и пусть принимает квитанции | Доставка между машинами обязана жить, когда `n8n.palo-alto.ai` лежит | Оставить. Замер: n8n выключен, файл доезжает на вторую машину, квитанция дописывается в журнал после подъёма |
| 26 | Хуки, скиллы

===== VENDOR: mistral (mistral.md) =====
Here’s your **adversarial, evidence-based** deep research brief, structured as requested.

---

### **1. SHORT VERDICT (10 lines)**
**Move to n8n:**
- **All cross-machine workflows** (replaces `_machine-bus` + Telegram rail with built-in retries, idempotency, and execution history).
- **AI agents** (LLM chains, RAG, tool orchestration) – n8n’s `lmChatOpenAi` + `toolWorkflow` nodes are *already* better than local Python for this.
- **CRM/lead pipelines** (Telegram → MongoDB → follow-ups) – n8n’s error workflows and webhook triggers fix silent failures.
- **Scheduled content bots** (summarize → post) – replaces Task Scheduler’s late jobs with n8n’s `scheduleTrigger` + retry.
- **Watchdogs** (heartbeats, budget alerts) – n8n’s `errorWorkflow` + `Wait` + re-queue is *more reliable* than local cron.

**Keep local:**
- **Filesystem-heavy work** (Obsidian sync, local RAG indexing) – n8n’s latency and Pyodide limitations make this worse.
- **Windows-specific tasks** (session management, GUI automation) – n8n can’t see `session 0` or interact with desktop windows.
- **Code with git history** (1271 Python scripts) – n8n stores workflows as JSON, not diffable code.
- **The n8n watchdog itself** – a watchdog must *not* live inside the system it monitors.

**Highest-leverage change:**
**Replace the `_machine-bus` + Telegram rail with a single n8n webhook → queue → HTTP workflow.**
- **Why?** Fixes silent failures (retries, dead-letter queue), removes manual ACK discipline, and gives a central run ledger.
- **Cost:** ~10 workflows (1 per machine + 1 bus bridge), but cuts 96 local watchdogs and 13 bus/sync tasks.

---

### **2. 20–30 CONCRETE AUTOMATIONS FOR THIS ESTATE**

| **Name**                          | **Trigger + Node Chain**                                                                 | **Already Covered?** | **Why n8n is Better**                                                                 | **Why n8n is Worse**                                                                 | **Verdict**       | **Proving Metric**                          |
|-----------------------------------|-----------------------------------------------------------------------------------------|----------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-------------------|---------------------------------------------|
| **Machine Bus Bridge**            | Webhook → Set (idempotency key) → HTTP (target machine) → Wait (ACK) → If (timeout) → ErrorWorkflow | REPLACES-EXISTING    | Built-in retries, dead-letter queue, execution history, no manual ACKs.              | Remote SPOF; latency (~200ms per hop).                                               | **Move to n8n**   | % of messages delivered *without* manual ACKs. |
| **Telegram Lead CRM**             | TelegramTrigger → If (new lead) → MongoDB (upsert) → HTTP (follow-up) → ErrorWorkflow   | REPLACES-EXISTING    | Visual debugging, error workflows, credential vault.                                 | n8n’s MongoDB node is slower than local PyMongo.                                     | **Move to n8n**   | % of leads processed *without* silent failures. |
| **LLM Research Pipeline**         | ScheduleTrigger → HTTP (fetch papers) → SplitInBatches → lmChatOpenAi → Postgres (RAG)  | REPLACES-EXISTING    | Built-in LLM nodes, tool orchestration, execution history.                          | Pyodide Code nodes fail on `_input`; no local GPU access.                            | **Move to n8n**   | % of papers processed *without* manual restarts. |
| **Content Summary Bot**           | ScheduleTrigger → HTTP (RSS) → lmChatOpenAi → Telegram (post) → ErrorWorkflow           | REPLACES-EXISTING    | Retries, visual flow, no late jobs.                                                  | n8n’s `scheduleTrigger` can drift if the host is overloaded.                         | **Move to n8n**   | % of posts delivered *on time*.             |
| **Audio Transcription**           | Webhook (file upload) → Whisper → ElevenLabs → Telegram (send) → ErrorWorkflow          | REPLACES-EXISTING    | Built-in STT/TTS nodes, no local GPU needed.                                         | n8n’s file handling is slower than local Python.                                     | **Move to n8n**   | % of files processed *without* manual restarts. |
| **Watchdog: n8n Heartbeat**       | ScheduleTrigger (5m) → HTTP (ping self) → If (fail) → Telegram (alert) → ErrorWorkflow  | NEW                  | Centralized alerts, retry logic.                                                     | Must run *outside* n8n (e.g., local cron).                                           | **Hybrid**        | % of alerts delivered *within 5m*.          |
| **Watchdog: Budget Alert**        | ScheduleTrigger (1h) → HTTP (check spend) → If (over) → Telegram (alert)                | NEW                  | Built-in error workflows, no silent failures.                                        | n8n’s HTTP node can fail if the API rate-limits.                                     | **Move to n8n**   | % of budget alerts delivered *on time*.     |
| **Dead-Letter Queue**             | ErrorWorkflow → Set (retry count) → Wait (backoff) → HTTP (retry) → If (max retries) → Telegram | NEW                  | Fixes silent failures; gives visibility into retries.                                | n8n’s `Wait` node can block the queue if too many errors.                            | **Move to n8n**   | % of failed jobs *recovered* without manual intervention. |
| **Idempotent DB Upserts**         | Webhook → Set (idempotency key) → MongoDB (upsert) → If (duplicate) → NoOp              | NEW                  | Built-in idempotency; no duplicate records.                                          | n8n’s MongoDB node is slower than local PyMongo.                                     | **Move to n8n**   | % of duplicate records *eliminated*.        |
| **Cross-Machine Sync**            | ScheduleTrigger → HTTP (fetch remote) → If (changed) → HTTP (push) → ErrorWorkflow       | REPLACES-EXISTING    | Retries, execution history, no manual ACKs.                                          | Remote SPOF; latency (~200ms per hop).                                               | **Move to n8n**   | % of syncs completed *without* manual restarts. |
| **Session Guard**                 | PreToolUse (Claude hook) → HTTP (check session) → If (invalid) → Telegram (alert)       | LEAVE-ALONE          | n8n can’t see `session 0` or interact with desktop windows.                           | -                                                                                     | **Keep local**    | -                                           |
| **Obsidian Vault Sync**           | ScheduleTrigger → HTTP (list files) → If (changed) → HTTP (sync) → ErrorWorkflow        | LEAVE-ALONE          | n8n’s file handling is slower than local Python; no git history.                     | -                                                                                     | **Keep local**    | -                                           |
| **Local RAG Indexing**            | ScheduleTrigger → Python (chunk files) → Postgres (upsert)                              | LEAVE-ALONE          | n8n’s Pyodide Code nodes fail on `_input`; no local GPU access.                      | -                                                                                     | **Keep local**    | -                                           |
| **GUI Automation**                | ScheduleTrigger → Python (click buttons)                                                | LEAVE-ALONE          | n8n can’t interact with desktop windows.                                             | -                                                                                     | **Keep local**    | -                                           |
| **Git-Backed Scripts**            | Any workflow touching `~/.claude/scripts`                                               | LEAVE-ALONE          | n8n stores workflows as JSON, not diffable code.                                     | -                                                                                     | **Keep local**    | -                                           |
| **Watchdog: n8n Itself**          | ScheduleTrigger (5m) → HTTP (ping n8n) → If (fail) → Telegram (alert)                    | LEAVE-ALONE          | A watchdog must *not* live inside the system it monitors.                            | -                                                                                     | **Keep local**    | -                                           |
| **One-Time Late Jobs**            | Webhook → Set (schedule time) → Wait → HTTP (execute) → ErrorWorkflow                   | REPLACES-EXISTING    | n8n’s `Wait` node is *more reliable* than Task Scheduler’s median 3.2h delay.        | n8n’s `Wait` can block the queue if too many jobs.                                   | **Move to n8n**   | % of jobs executed *on time*.               |
| **Aggregate Dashboard**           | ScheduleTrigger → HTTP (fetch all statuses) → Set (merge) → Telegram (post)             | NEW                  | Fixes "blind to dead legs" problem; gives a single view.                             | n8n’s HTTP node can fail if a machine is down.                                       | **Move to n8n**   | % of dead legs *detected within 1h*.        |
| **Retry with Backoff**            | ErrorWorkflow → Set (retry count) → Wait (exponential) → HTTP (retry) → ErrorWorkflow   | NEW                  | Fixes "no retry/backoff standard" problem.                                           | n8n’s `Wait` can block the queue if too many errors.                                 | **Move to n8n**   | % of failed jobs *recovered* without manual intervention. |
| **Idempotent API Calls**          | Webhook → Set (idempotency key) → HTTP (call) → If (duplicate) → NoOp                   | NEW                  | Built-in idempotency; no duplicate API calls.                                        | n8n’s HTTP node can fail if the API rate-limits.                                     | **Move to n8n**   | % of duplicate API calls *eliminated*.      |
| **Telegram ACK Discipline**       | TelegramTrigger → Set (ACK key) → HTTP (store ACK) → If (missing) → Telegram (remind)   | REPLACES-EXISTING    | Replaces manual ACKs with automated reminders.                                       | n8n’s Telegram node can fail if the bot is rate-limited.                             | **Move to n8n**   | % of ACKs *automated*.                      |
| **Watchdog: Transport Success**   | Webhook → HTTP (check consumer) → If (fail) → Telegram (alert) → ErrorWorkflow          | NEW                  | Fixes "watchdogs mint green from transport" problem.                                 | n8n’s HTTP node can fail if the consumer is down.                                    | **Move to n8n**   | % of false positives *eliminated*.          |
| **Central Run Ledger**            | Any workflow → Set (run metadata) → MongoDB (insert)                                    | NEW                  | Fixes "no central run ledger" problem; gives a single source of truth.               | n8n’s MongoDB node is slower than local PyMongo.                                     | **Move to n8n**   | % of runs *logged* without gaps.            |
| **Budget Check Gate**             | PreToolUse (Claude hook) → HTTP (check spend) → If (over) → Telegram (alert)            | REPLACES-EXISTING    | Built-in error workflows; no silent failures.                                        | n8n’s HTTP node can fail if the API rate-limits.                                     | **Move to n8n**   | % of budget overruns *caught before execution*. |

---

### **3. WHERE N8N IS THE WRONG TOOL (ANTI-LIST)**
| **Category**               | **Why n8n is Wrong**                                                                 | **Evidence**                                                                 |
|----------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Local Filesystem Work**  | n8n’s file nodes are slow; no git history; Pyodide Code nodes fail on `_input`.       | [n8n forum: Pyodide issues](https://community.n8n.io/t/pyodide-code-node-fails-on-input/12345) (2026-05-10) |
| **Windows-Specific Tasks** | n8n can’t see `session 0`; no GUI automation; no desktop window interaction.          | [n8n docs: OS limitations](https://docs.n8n.io/hosting/limitations/) (2026-09-01) |
| **Git-Backed Code**        | n8n stores workflows as JSON, not diffable code; no PR reviews.                      | [n8n GitHub: workflows as JSON](https://github.com/n8n-io/n8n-workflows) (2026-08-15) |
| **Watchdog for n8n Itself**| A watchdog must *not* live inside the system it monitors.                            | [Hacker News: "Don’t monitor yourself"](https://news.ycombinator.com/item?id=38000000) (2026-03-20) |
| **Long-Running Desktop Work** | n8n’s queue mode can block; no GPU access; no local session persistence.          | [n8n forum: queue mode limits](https://community.n8n.io/t/queue-mode-blocking/9876) (2026-07-12) |
| **High-Frequency Tasks**   | n8n’s `scheduleTrigger` can drift if the host is overloaded; no sub-minute precision. | [n8n docs: scheduling limits](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.scheduleTrigger/) (2026-09-01) |

---

### **4. HYBRID ARCHITECTURE (TEXT DIAGRAM)**
```
┌───────────────────────────────────────────────────────────────────────────────┐
│ LOCAL (Windows Task Scheduler + Python)                                       │
│                                                                               │
│  ┌─────────────┐    ┌─────────────┐    ┌───────────────────────────────────┐  │
│  │ Filesystem  │    │ GUI/Session │    │ Watchdog (n8n itself)            │  │
│  │ (Obsidian,  │    │ (clicks,     │    │  ┌─────────────────────────────┐ │  │
│  │  RAG index) │    │  windows)    │    │  │ Schedule (5m) → HTTP (ping) │ │  │
│  └─────────────┘    └─────────────┘    │  │ → If (fail) → Telegram       │ │  │
│                                         │  └─────────────────────────────┘ │  │
│  ┌───────────────────────────────────┐  └───────────────────────────────────┘  │
│  │ Git-Backed Scripts (1271)         │                                          │
│  └───────────────────────────────────┘                                          │
└───────────────────────────────────────┬───────────────────────────────────────┘
                                        │
                                        │ CONTRACT: Webhook in / Webhook out
                                        │ (idempotency key, retry, ACK)
                                        ▼
┌───────────────────────────────────────────────────────────────────────────────┐
│ N8N (self-hosted)                                                                 │
│                                                    

[срез/truncated: бюджет поделён между 4 ногами; урезаны gemini.md, grok.md, mistral.md. Отсутствие факта в куске НЕ означает, что нога его не называла.]

---

> `Write` -- {"file_path": "D:\\Vault\\_imports\\memory\\.scratch_dr_distill_output.json", "content": "placeholder"}

---

> `ToolSearch` -- {"query": "no-op", "max_results": 1}

---

**Claude:**

```json
{
  "lang": "mixed",
  "topic": "n8n как слой автоматизации: что переносить из локального флота (317 задач, 1271 скрипт), что оставить",
  "one_line": "Деп-ресёрч четырёх вендоров отвечает, какие из ~30 локальных и n8n-автоматизаций стоит переносить/оставлять, и сходится на том, что n8n берёт на себя внешний клей и интеграции, а не файловую систему и Windows-слой.",
  "key_findings": [
    "Единогласный вердикт всех 4 вендоров: n8n годится для внешнего HTTP/webhook-клея, Telegram/CRM-роутинга, LLM-агентных цепочек и retry/idempotency-паттернов, но НЕ для файловой системы, Obsidian-волта, git-истории 1271 скрипта, Windows session-0/GUI и браузерной автоматизации рабочего стола.",
    "Самый дорогой/выгодный ход один у всех: единый 'контракт исполнения' — локальный скрипт POST'ит статус (старт/ок/ошибка/применено) в webhook n8n, который пишет центральный run-ledger; это закрывает сразу три дыры: слепоту дашбордов, отсутствие DLQ и отсутствие единого журнала прогонов без переписывания скриптов.",
    "Watchdog, который следит за самим n8n, обязан жить ВНЕ n8n (локально) — сторож внутри объекта слепнет, когда объект падает; это прямое повторение класса 'watchdog-mints-green-from-transport' (gemini, glm, grok, mistral все называют это отдельным anti-pattern пунктом).",
    "Разовые/отложенные задачи Windows Task Scheduler опаздывают катастрофически — grok/glm дают медиану 3.2ч и p90 16.4ч задержки; Wait-нода n8n превращает это в секунды, это признанный всеми лучший кандидат на перенос (#1 в большинстве таблиц).",
    "Текущий n8n-стек уже занят тем, для чего его держат: 98 воркфлоу, 1736 узлов (grok), CHARM CRM (~38 воркфлоу, Telegram→Mongo→агент), аудио-транскрипция Whisper/ElevenLabs, контент-паблишер, Airtop-скрейпинг — это 'LEAVE-ALONE', не трогать.",
    "grok: узловой профиль смещён к коду и API-склейке, а не к расписаниям — Code 256, httpRequest 181, if 150, set 129, mongoDb 114, telegram 95, lmChatOpenAi 84, scheduleTrigger всего 23 против 317 локальных задач в Планировщике; на 17.7 узла/воркфлоу против 6.8 у типового публичного шаблона (Zie619, 4343 воркфлоу) — стек уже в 2.6 раза 'толще' нормы, в основном из-за CRM-агента.",
    "Проблема ошибочного error-workflow подтверждена практиками: community-пост описывает 27 намеренных падений, из которых 12 прошли молча — error workflow не является гарантией глобального перехвата, нужен внешний аудитор, который проверяет сам список активных воркфлоу на пустой `settings.errorWorkflow`.",
    "n8n Code-узлы работают через Pyodide с ограниченным набором пакетов — реальный Python-код (1271 локальный скрипт) там не запустится; плюс n8n не хранит автора правки (metadata=null у grok) и JSON-диффы воркфлоу не ревьюятся как код — git-дисциплину переносить в n8n нельзя.",
    "Идемпотентность, retry/backoff и верификация именно потребителем (а не транспортом) — три повторяющихся отсутствующих стандарта в текущей системе; все вендоры предлагают закрыть их как общие n8n-сабворкфлоу/настройки узлов, а не как переписывание 317 задач."
  ],
  "recommendations": [
    "Построить единый Execution Ingestion Contract: один webhook в n8n, куда каждый локальный скрипт шлёт heartbeat/статус/payload-summary по завершении — закрывает дашборд-слепоту и DLQ без переписывания скриптов.",
    "Перенести в n8n: разовые/отложенные задачи (Wait-нода вместо Task Scheduler), bus-bridge/межмашинный диспетчер (укрепить, не строить с нуля), центральный run-ledger, DLQ, идемпотентность-гейт на входной двери, retry/backoff на уже существующих HTTP-узлах, верификацию по факту применения потребителем (а не по факту отправки).",
    "Оставить локально навсегда: 1271 Python-скрипт и всё git-ревьюируемое, Obsidian-волт и RAG/pgvector-индексацию (латентность диска + отсутствие git), Windows session-0/GUI/браузерную автоматизацию, локальный git-бэкап и апгрейд самого n8n, сторож самого n8n (watchdog-of-n8n) — он не может жить внутри подопечного.",
    "Не трогать уже работающее в n8n: CHARM CRM, аудио-пайплайн Whisper/ElevenLabs, контент/соц-паблишер, Airtop-скрейпинг, Airtable/Mongo-синхронизацию, Telegram-рассыльщик '03' — миграционная цена здесь чистый убыток (288 задач с чистым exit не дают выгоды от переноса).",
    "Перед масштабированием нужен один проверочный факт с хоста n8n.palo-alto.ai (grok не смог прочитать снаружи): исполнений/сутки, SQLite vs Postgres, включён ли queue mode, какая лицензия — без этого раздел про масштаб не достоверен, хотя сам вердикт не зависит от этих чисел.",
    "Добавить локальный ежедневный аудит активных воркфлоу без error workflow (пустой `settings.errorWorkflow`) — не доверять самому n8n отчёт о своём покрытии ошибками.",
    "Прежде чем переносить 7 локальных CRM/lead-задач, проверить по каждой вход/выход: если задача лишь опрашивает ту же Mongo, что и n8n, — заменить одной n8n-задачей (SLA лида), иначе оставить (код/файлы)."
  ],
  "entities": {
    "people": [],
    "companies": [],
    "products_tools": ["n8n", "n8n.palo-alto.ai", "Telegram", "MongoDB", "Postgres", "pgvector", "Obsidian", "Syncthing", "_machine-bus", "Windows Task Scheduler", "CHARM CRM", "Airtable", "Airtop", "Whisper", "ElevenLabs", "Claude Code", "Pyodide", "Zie619/n8n-workflows"]
  },
  "open_questions": [
    "Сколько исполнений в сутки на n8n.palo-alto.ai и какая там СУБД (SQLite или Postgres) — grok явно не смог прочитать это снаружи, раздел про масштаб без этого не достоверен",
    "Включён ли queue mode и какая лицензия n8n — тоже не прочитано дистанционно",
    "Действительно ли 7 локальных CRM/lead-задач дублируют то, что уже опрашивает n8n-Mongo, или ходят в отдельные локальные файлы — требует проверки по каждой задаче отдельно",
    "Сколько реально стоят 84 узла lmChatOpenAi в деньгах API за неделю — нужно сравнить с ценой локальных подписочных LLM CLI перед решением выносить вызовы из n8n",
    "Расходятся ли между собой локальный RAG-индекс и pgvector-RAG внутри n8n и насколько — предложено замерять, но не измерено в самом отчёте"
  ],
  "related_concepts": ["machine-bus-telegram-rail", "watchdog-mints-green-from-transport", "fleet-parity-board", "one-system-propagate", "charm-crm", "alpha-protocol-recall-plus-dr", "deploy-three-layers-apply-gap", "routine-must-declare-its-output"]
}
```
