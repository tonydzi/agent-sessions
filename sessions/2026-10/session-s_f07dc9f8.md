---
session: s_f07dc9f8
date: 2026-10-25
words: 1395
turns: 8
tools: "Bash, Grep, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-25 · Weekly brain audio digest — via /notebooklm

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f07dc9f8` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

---
name: weekly-brain-audio-digest
description: Weekly NotebookLM audio digest of dev's Second Brain (Sun 05:30 Lisbon)
model: claude-sonnet-5-5
effort: medium
tier_migrated: down-20261012
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

Запускаю недельный подкаст по инструкции рутины. Сначала выбираю тему по активности в волте за 7 дней и читаю память по NotebookLM.

---

> `Bash` -- {"command": "git -C D:/Vault/Vault-Knowledge log --since='7 days ago' --name-only --format= -- 06-Concepts/ 03-Insights/ 02-Decisions/ | sort | uniq -c | sort -rn | head -30", "description": "Count vault files touched in last 7 days"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\C--Windows-System32\\memory\\notebooklm-integration.md"}

---

**Claude:**

Самая активная содержательная заметка за неделю: `insight-2026-10-16-claude-customize-catalog-audit` (6 касаний). `_Ledger` и `alpha-backlog` это журналы, их не беру. Читаю заметку и собираю пакет.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && wc -c 03-Insights/insight-2026-10-16-claude-customize-catalog-audit.md && cat 03-Insights/insight-2026-10-16-claude-customize-catalog-audit.md && echo ---- && grep -rl \"claude-customize-catalog-audit\" --include=*.md . | head -20 && echo ---- && timeou

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && wc -c 03-Insights/insight-2026-10-16-claude-customize-catalog-audit.md && cat 03-Insights/insight-2026-10-16-claude-customize-catalog-audit.md", "description": "Read the chosen insight note"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && grep -rl \"claude-customize-catalog-audit\" --include=*.md . ; echo \"exit=$?\"", "description": "Find backlinks to the chosen note"}

---

> `Bash` -- {"command": "timeout 120 python /e/Obsidian/_imports/brain_ask.py \"claude customize catalog audit skills\" > /tmp/brain_ask_out.txt 2>&1; echo \"exit=$?\"; wc -c /tmp/brain_ask_out.txt", "description": "Run brain_ask RAG query and save output"}

---

> `Read` -- {"file_path": "/tmp/brain_ask_out.txt"}

---

> `Grep` -- {"pattern": "claude-customize-catalog-audit", "path": "D:\\Vault\\Vault-Knowledge", "output_mode": "files_with_matches", "head_limit": 20}

---

**Claude:**

Бэкап волта перед записью (правило `vault-backup-rule`), затем читаю RAG-срез и собираю пакет.

---

> `Bash` -- {"command": "cat /tmp/brain_ask_out.txt | head -c 7500; echo; echo ----; python -I /e/Obsidian/_imports/vault_backup.py; echo \"backup exit=$?\"", "description": "Show RAG slice and run vault backup before writes"}

---

**Claude:**

Бэкап заблокирован: в индексе 1586 файлов на удаление, из них 1441 в `_originals` без восстановимой копии. Это похоже на опасное массовое удаление, поэтому `--force` не трогаю. Проверяю состояние только на чтение.

---

> `Bash` -- {"command": "git status --porcelain | awk '{print $1}' | sort | uniq -c; echo ----; git status --porcelain | grep '^D' | head -5; echo ----; git diff --cached --stat | tail -1; git log -1 --format='%h %ci %s'", "description": "Inspect git status read-only before any vault write"}

---

> `Bash` -- {"command": "git status --porcelain | grep '^ D\\|^D ' | head -5; echo ----; git status --porcelain | grep '^ D' | wc -l; git status --porcelain | grep '^D ' | wc -l; echo ----; git status --porcelain | grep '^ M\\|^M ' | head -30; echo ----; git ls-files _originals/github-evidence/2026-10-24 | wc -

---

**Claude:**

Вскрылось серьёзнее, чем лимит бэкапа: 1586 файлов из `_originals` есть в git, но на диске их нет (`D` в рабочем дереве, не в индексе). Это стоп-лист §0.6. Проверяю, идёт ли это сейчас, ещё только на чтение.

---

> `Bash` -- {"command": "date -u '+now_utc=%F %T'; ls -la _originals | head -20; echo ----; find _originals -newer e378c23 -type f 2>/dev/null | wc -l; echo ----; ls -la --time-style=+%F_%T _originals/codex-sessions/ 2>&1 | head; echo ----; tasklist 2>/dev/null | grep -i -E 'syncthing|python|git' | head", "desc

---

**Claude:**

`_originals` на диске почти пуст: остались только `_RECONCILE-LEDGER.md` и `omi/`, изменения шли 04:50–04:56 UTC, а сейчас 05:34, и git-процессы ещё запущены. Пока причину не знаю, в волт ничего не пишу. Подкаст на этой неделе пропускаю с названной причиной и сообщаю в чат 03.

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/bus_ping.py\" \"⚠️ weekly podcast пропущен: в волте пропадают файлы _originals (на диске 1586 из git, сейчас почти пусто, сбой 04:50-04:56 UTC). Бэкап заблокирован tripwire, в волт ничего не пишу, --force не делаю. Нужен разбор: кто удаляет (recon

---

**Claude:**

🔴 Недельный подкаст не сделан: в волте пропадают файлы `_originals`, и я остановился до любых записей.

**Что сделано**
- Тема выбрана: `03-Insights/insight-2026-10-16-claude-customize-catalog-audit.md`, 6 касаний за неделю. Журналы `_Ledger` и `alpha-backlog` пропустил как не концепты.
- RAG-срез через `brain_ask.py` получен: 12 попаданий, в основном по аудиту каталога и связанным инсайтам.
- Пакет в волт не записан. Аудио в NotebookLM не генерировал.
- Пинг в чат 03 отправлен (`PING OK`).

**Что нашёл**
- `vault_backup.py` заблокирован tripwire: в индексе 1586 файлов на удаление, 1441 из них в `_originals` без восстановимой копии. Файлы есть в git (HEAD `e378c23`, «backup: pre-intervention»), но на диске их нет.
- Сейчас в `_originals` остались только `_RECONCILE-LEDGER.md` (8 МБ, 04:50 UTC) и папка `omi/`. Изменения шли 04:50–04:56 UTC, на момент проверки было 05:34 UTC, и процессы `git.exe` и `syncthing.exe` ещё работали. Пропадание может продолжаться.
- Причину не знаю. Вероятные кандидаты: reconcile или синк, но проверено это не было.

**Что НЕ делал**
- Не запускал `--force` и не восстанавливал файлы из git: это запись в волт при неясной причине, поэтому нужно твоё решение.
- Ничего не удалял. Синк и процессы не останавливал, потому что это решение за тобой.

**Что нужно от тебя / что дальше**
1. Посмотреть, кто и что удаляет `_originals` (reconcile, синк, чистка?). Пока причина не найдена, лучше притормозить синк на хабе.
2. Когда волт будет в порядке, подкаст этой недели можно прогнать вручную через `/notebooklm`. Пакет и аудио будут тогда записаны уже после бэкапа.

🧒 **Простыми словами**
Подкаст я не сделал, потому что в папке с оригиналами пропадают файлы: на диске почти пусто, а в истории git они есть. Я не стал ничего «чинить» силой и ничего не удалял, чтобы не сделать хуже. Тебе ушло сообщение в чат 03. Сначала нужно понять, кто что стирает, и только потом делать подкаст.
