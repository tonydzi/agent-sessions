---
session: s_df057f42
date: 2026-09-27
words: 869
turns: 4
tools: "Bash, Read, ToolSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · Weekly brain audio digest — via /notebooklm

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_df057f42` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

---
name: weekly-brain-audio-digest
description: Weekly NotebookLM audio digest of dev's Second Brain (Sun 05:30 Lisbon)
---

# Weekly brain audio digest — via /notebooklm

You are dev's Claude Code. Once a week, generate a NotebookLM Audio Overview from the FRESHEST thinking in dev's Obsidian vault and file it back into the vault. This routine is codified in memory `notebooklm-integration` and the decision `02-Decisions/decision-notebooklm-claude-code-artifact-layer.md`; it is authorised by dev on 2026-06-18 (podcast of the brain = weekly).

## Do
1. **Pick this week's topic (deterministic-first).** Look at `git -C D:\Vault\Vault-Knowledge log --since='7 days ago' --name-only -- 06-Concepts/ 03-Insights/ 02-Decisions/` and pick the single concept/insight/decision with the most touches this week (his ACTIVE thinking). Fall back to the most recently-created `concept-*.md` if the log is empty. Announce the topic before proceeding.
2. **Curate a NARROW packet** (per memory `vault-data-architecture` — token law): run `python D:\Vault\_imports\brain_ask.py "<topic>"` to pull the top slice; combine with the chosen note + its `[[backlinks]]` (grep). Aim for 10-30 KB of curated text — NOT the whole vault. Write the packet to `D:\Vault\Vault-Knowledge\05-Resources\NotebookLM\_packets\packet-<YYYY-MM-DD>-<topic-slug>.md` with a header stating date/topic/source-notes.
3. **Drive NotebookLM via Chrome-autonomy** (per memory `chrome-autonomy-self-drive`; live UI is the only path — no API for consumer). Open https://notebooklm.google.com/?authuser=4&pageId=none (dev's a2 account = `[EMAIL]`, tier PRO). Steps:
   - Create new notebook (+ Create new).
   - Add sources → Copied text → paste the packet body → Insert.
   - Wait for source ingestion (a few seconds).
   - Studio → click "Audio Overview" tile → wait for "Generating Audio Overview…" then a few minutes for it to finish.
4. **Download and file.** Click the ⋮ menu next to the finished audio → Download (a .m4a). Move it from `C:\Users\dev\Downloads\` into `D:\Vault\Vault-Knowledge\05-Resources\NotebookLM\artifacts\audio\` renaming to `brain-digest-<YYYY-MM-DD>-<topic-slug>.m4a` (LATIN filename per vault-conventions).
5. **Update the audio index.** Append a bullet to `D:\Vault\Vault-Knowledge\05-Resources\NotebookLM\artifacts\_NotebookLM-Audio.md` — one line, format: `- brain-digest-<date>-<slug>.m4a — <topic> (packet: [[packet-<date>-<slug>]])`. Do NOT rewrite the file.
6. **Ping dev in Telegram chat 03** (id `chat_REDACTED`) via the shared bus: `python C:\Users\dev\.claude\scripts\bus_ping.py "🎧 weekly brain podcast готов: <topic> — <link-to-vault-file>"`. Keep it one line.

## Gotchas
- Bulk artifact export = Download menu ONLY, NEVER DOM-scrape (tool output truncates ~1000 chars).
- If NotebookLM UI is not logged in on a2, log DOES NOT try any auto-login here — just skip this run and ping dev "⚠️ weekly podcast skipped — a2 not logged in".
- If the log window is empty (0 touched files in 7 days), skip cleanly — post "⚠️ weekly podcast skipped — no vault activity this week".
- Do NOT run this in parallel with other Chrome-driven tasks (conflict on the browser). Use existing single-instance conventions.
- Vault write = backup first via memory `vault-backup-rule` (`python D:\Vault\_imports\vault_backup.py`).

## Boundaries
- Skill trigger `/notebooklm digest` covers the same recipe manually. Do NOT rebuild it; do NOT call the skill — just follow the steps above (a scheduled task's prompt is self-contained per operating-agreement).
- Personal `[EMAIL]` is OFF-LIMITS (privacy). Only a2 (`authuser=4`).
- Tier-2 (money/outbound/secrets) does NOT apply — this is dev-facing, inbound-only.

## Output
One-line report: 🟢 topic + saved file path, or 🟡/🔴 with the reason.

---

**Claude:**

I'll check whether this environment actually has the infrastructure this routine depends on before doing anything else.

---

> `Bash` -- {"command": "echo \"--- E: drive ---\"; ls -la /e/ 2>&1 | head -20; echo \"--- vault ---\"; ls -la \"/e/Obsidian/Vault-Knowledge\" 2>&1 | head -20; echo \"--- scripts dir ---\"; ls -la \"/c/Users\" 2>&1 | head -20"}

---

> `ToolSearch` -- {"query": "chrome browser notebooklm telegram bus", "max_results": 10}

---

> `Bash` -- {"command": "echo \"--- notebooklm cli ---\"; where notebooklm 2>&1; pip show notebooklm-py 2>&1 | head -5; echo \"--- bus_ping ---\"; find \"/c/Users/dev/.claude/scripts\" -iname \"bus_ping*\" 2>&1; echo \"--- imports dir ---\"; ls \"/e/Obsidian/_imports\" 2>&1 | grep -i notebook; echo \"--- git 

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\bus_ping.py", "limit": 60}

---

**Claude:**

This is a real, extensive automation setup (the vault, scripts, and Telegram bridge at `D:\Vault\Vault-Knowledge` and `~/.claude/scripts/bus_ping.py` all check out). But I've confirmed this session has no browser-automation tool (no Chrome/NotebookLM MCP connector shows up via ToolSearch) and no `notebooklm-py` CLI installed — so I can't actually complete the core step of this routine (driving NotebookLM to generate the audio). I don't want to fake that or leave a half-finished packet file sitting in the vault, so I'm reporting the blocker honestly rather than claiming success.

---

> `Bash` -- {"command": "cd \"/c/Users/dev/.claude/scripts\" && python bus_ping.py \"🔴 weekly brain podcast (NotebookLM digest) пропущен: в этой сессии нет ни Chrome/NotebookLM MCP-коннектора, ни notebooklm-py CLI — шаг 3 рутины (браузер-автоматизация) выполнить нечем. Топик и пакет не собирал, чтобы не остав

---

**Claude:**

Ping delivered to chat 03.

Summary: I checked the `weekly-brain-audio-digest` routine's dependencies — the vault (`D:\Vault\Vault-Knowledge`) and `bus_ping.py` are real and working, but this session has neither a Chrome/NotebookLM browser-automation connector nor the `notebooklm-py` CLI, so step 3 (generating the actual audio) can't run here. I sent an honest 🔴 status ping to chat 03 explaining the blocker instead of faking completion or leaving a half-built packet file in the vault. Next step would be re-running this routine from a session that has the Chrome-MCP connector attached, or getting `notebooklm-py` installed for a browserless path.
