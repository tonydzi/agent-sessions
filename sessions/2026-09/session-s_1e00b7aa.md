---
session: s_1e00b7aa
date: 2026-09-21
words: 1899
turns: 7
tools: "Bash, Grep, PowerShell, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are the independent cross-vendor reviewer for a safety-critical Windows Telegram doorb…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1e00b7aa` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are the independent cross-vendor reviewer for a safety-critical Windows Telegram doorbell patch. READ ONLY. Do not edit any file and do not run commands that mutate production state. Inspect these exact files:
C:\Users\dev\.claude\scripts\tg_doorbell.py
C:\Users\dev\.claude\scripts\_test_tg_doorbell.py
Expected frozen SHA256: source CBD7FA5C82FBCCF1F819B5C015E1D70BC2269F396C472C6009EB4F5A9DE969E2; test FEB55DFEF2B14ED81BD7EE74BB759C1D26149082B67AF15579DDF7B04DC153F0.
Acceptance: addressed message causes exactly one wake; irrelevant message causes zero wake and zero LLM; duplicate/restart no repeated wake; crash/recovery safe; foreign staging preserved; owned staging exactly deleted or FAIL; every RED kills old/mutant code; test scaffold itself cannot false-green by deleting/mutating RED rows, invocations, check/fails/verdict, temp isolation, or sentinel assertions; production state unchanged before green canary; rollback is provable. Known local evidence to challenge, not trust: 59 GREEN + 34 RED = 93/93 twice rc0; independent baseline rc0; exact W1/V1 rc2; external frozen matrix 17/17, survivors 0, prod drift {}, residue 0, sentinels 17/17. Windows-only scope is intentional.
Return exactly one verdict line first: VERIFY or BLOCK. Then concise numbered findings ordered by severity with file:line. If VERIFY, state what you inspected and any explicit boundary. Focus on ways official PASS could still be false-green and on cleanup/crash/idempotency correctness.

---

**Claude:**

[⏰ оператор написал: понедельник, утро, 09:15, 21 сентября 2026]

I'll inspect the frozen artifacts read-only.

---

> `PowerShell` -- {"command": "Get-FileHash -Algorithm SHA256 \"C:\\Users\\dev\\.claude\\scripts\\tg_doorbell.py\",\"C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py\" | Format-List Path,Hash; Get-Item \"C:\\Users\\dev\\.claude\\scripts\\tg_doorbell.py\",\"C:\\Users\\dev\\.claude\\scripts\\_test_tg_door

---

**Claude:**

Source hash mismatch. Let me establish what changed and inspect substantively.

---

> `PowerShell` -- {"command": "cd \"C:\\Users\\dev\\.claude\\scripts\"; git log --oneline -5 -- tg_doorbell.py _test_tg_doorbell.py; Write-Output \"--- DIFFSTAT ---\"; git diff --stat -- tg_doorbell.py _test_tg_doorbell.py; Write-Output \"--- HEAD HASHES ---\"; git show HEAD:scripts/tg_doorbell.py 2>$null | Out-Nul

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\tg_doorbell.py"}

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\.claude\\scripts\\workspace_write_lease.py\" status", "description": "Show workspace lease status"}

---

**Claude:**

Source is drifting under an active write lease. Continuing the substantive inspection.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\tg_doorbell.py", "offset": 1080, "limit": 650}

---

**Claude:**

Now the test scaffold — where false-green risk concentrates.

---

> `Grep` -- {"pattern": "^(def |class |REDS|GREENS|CASES|REGISTRY|SENTINEL|_SENT|TOTAL|EXPECT)", "path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "output_mode": "content", "-n": true, "head_limit": 300}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "offset": 1, "limit": 300}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "offset": 2290, "limit": 320}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "offset": 2609, "limit": 400}

---

> `Grep` -- {"pattern": "id_e161e2fc|id_f3b049aa|_PROD_SOURCE|getsource|CBD7FA|rev2[234]|_STAGING_FINALLY|_CLEANUP_POSTCHECK", "path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "output_mode": "content", "-n": true}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_tg_doorbell.py", "offset": 1963, "limit": 155}

---

> `PowerShell` -- {"command": "$d=\"$env:USERPROFILE\\.claude\\doorbell_doors.json\"; \"doors exists: $(Test-Path $d)\"; if(Test-Path $d){Get-Content $d}; $b=\"$env:LOCALAPPDATA\\claude-tgbus\"; \"statedir exists: $(Test-Path $b)\"; if(Test-Path $b){Get-ChildItem $b -Force | Select-Object Name,Length,LastWriteTime | 

---

**Claude:**

Production DB was written 9:18:59 — during this review. Inspecting it strictly read-only.

---

> `PowerShell` -- {"command": "$p=\"$env:LOCALAPPDATA\\claude-tgbus\\doorbell.sqlite3\"; python -c \"\nimport sqlite3,sys,os\np=os.environ['LOCALAPPDATA']+'/claude-tgbus/doorbell.sqlite3'\nfor s in ('-wal','-shm','-journal'):\n    print('sidecar',s,os.path.exists(p+s), os.path.getsize(p+s) if os.path.exists(p+s) else

---

> `Bash` -- {"command": "cat > /tmp/ro_probe.py <<'EOF'\nimport sqlite3, os\np = os.path.join(os.environ['LOCALAPPDATA'], 'claude-tgbus', 'doorbell.sqlite3')\nfor s in ('-wal', '-shm', '-journal'):\n    q = p + s\n    print('sidecar', s, os.path.exists(q), os.path.getsize(q) if os.path.exists(q) else '')\nc = s

---

> `Bash` -- {"command": "python -c '\nimport sqlite3, os\np = os.path.join(os.environ[\"LOCALAPPDATA\"], \"claude-tgbus\", \"doorbell.sqlite3\")\nfor s in (\"-wal\", \"-shm\", \"-journal\"):\n    q = p + s\n    print(\"sidecar\", s, os.path.exists(q), os.path.getsize(q) if os.path.exists(q) else \"\")\nc = sqli

---

> `Bash` -- {"command": "python -c '\nimport io, json, os\nu = os.path.join(os.path.expanduser(\"~\"), \".claude\", \"usage\", \"tg_doorbell.jsonl\")\nrows = [json.loads(l) for l in io.open(u, encoding=\"utf-8\") if l.strip()]\nprint(\"total\", len(rows), \"first\", rows[0][\"ts\"], \"last\", rows[-1][\"ts\"])\

---

> `Bash` -- {"command": "schtasks /query /fo LIST /v 2>/dev/null | grep -iE \"TaskName|Scheduled Task State|Next Run\" | grep -iB1 -A2 \"doorbell\" ; echo \"--- direct ---\"; schtasks /query /fo TABLE 2>/dev/null | grep -i doorbell; echo \"exit=$?\"", "description": "Check for a scheduled doorbell task"}

---

**Claude:**

BLOCK

**What I inspected:** both files byte-for-byte (`tg_doorbell.py` 1722 lines, `_test_tg_doorbell.py` 2959 lines), their SHA256, the live workspace lease table, the production state directory, the production SQLite DB (strictly `mode=ro` URI — no RW open, no sidecar touched), and the production usage counter.

---

### 1. The frozen source is not the source on disk — every cited result is about a different file
`tg_doorbell.py:1`

| file | expected | actual |
|---|---|---|
| source | `CBD7FA5C…9DE969E2` | **`5FD4074A226B981527B879C33A38113EE4A9E6769A1E09BA9C34E85B9109DE50`** |
| test | `FEB55DFE…4DC153F0` | `FEB55DFE…4DC153F0` ✅ |

Source mtime `09:14:45`, test mtime `08:50:56` — the source was written *after* the test was frozen. `workspace_write_lease.py status` shows `tg_doorbell.py` **still held** by `codex/s_fc1fd9f7`; a `git` read of the pair was refused by the lease guard mid-review. The artifact can still change while you read this. `93/93 twice rc0`, `17/17`, `survivors 0` are claims about `CBD7FA…`, which is not what is deployed. Corroborating internal evidence: the passport header stops at `REV21` (`tg_doorbell.py:181`) while the body carries rev22/23/24 logic (`:1240`, `:1308`, `:1355`, `:1529`).

### 2. The suite cannot detect that drift, by construction — this is the false-green mechanism
`_test_tg_doorbell.py:41,75,2929`

`_PROD_BEFORE` is snapshotted **at import time**, so `prod drift {}` proves only that the source didn't change *during* the run. There is no expected-SHA constant for `tg_doorbell.py` anywhere in the suite. A source already modified before the run passes the drift gate silently. `prod drift {}` is therefore not evidence that the tested artifact is the reviewed artifact — the two pieces of evidence you were told to trust are independent of each other in the wrong direction.

### 3. Production state is *not* unchanged, and the doorbell has been live since 2026-09-16
`%LOCALAPPDATA%\claude-tgbus\doorbell.sqlite3`

`user_version=7`, pinned to the **real** chat `chat_REDACTED`, `highwater=1904117`, `delivery: [('pending', 2)]`, DB written `9:18:59` — during this review. Usage counter: 89 rows, first `2026-09-16T19:33:54Z`, ticking every ~2 min through `08:19:14Z`. The acceptance item *"production state unchanged before green canary"* is false on observation.

### 4. Two real addressed messages have been silently dropped for hours, and nothing can ever escalate them
`tg_doorbell.py:800,861-864,771,776,894-898`

`~/.claude/doorbell_doors.json` **does not exist** → `doors={}` → `_door_for` returns `helper=None` → `stats["spooled"] += 1; continue` with no claim, no `attempts` increment, and not even a `misconfig-door` count. Confirmed in the counter: `spooled: 2` every tick since `08:06Z`, `delivered: 0`.

Even with the doors file present, both production helpers return `("gap", …)`, and the gap branch does `attempts=attempts-1` — exactly cancelling the `attempts+1` of the claim. **`MAX_ATTEMPTS`/`dead_letter` is unreachable on the gap path by construction.** So: no wake, no dead-letter, no age-based alarm, no bound. `tick` just returns rc3 forever (pending is dirty), which trains the operator to ignore rc3 — the one signal the doorbell depends on. Acceptance item *"addressed message causes exactly one wake"* is currently *zero* wakes, indefinitely.

### 5. The pinned identity — the value that decides where the doorbell points — is never asserted
`tg_doorbell.py:202-204`, `_test_tg_doorbell.py:197,2515`

`db.CHAT = -1` is set at import for the entire suite; `db.SENDERS` is mutated by REDs and restored from *whatever the module happens to hold*. No test pins `CHAT` to `chat_REDACTED` or `SENDERS` to `{id_f3b049aa}`. Compare `:151`, which *does* source-pin `_lock` to `bus_ping` via `inspect.getsource` — the technique exists in this file and was not applied to identity. An edit changing the pinned chat or widening the sender allowlist passes 93/93 green. That is the exact hinge of *"irrelevant message causes zero wake"*.

### 6. `recover()`'s epoch-release proof is dead code
`tg_doorbell.py:345-356,1332-1336,1350-1353`

`_epoch_release` wraps both `commit()` and `close()` in `except Exception: pass`. It cannot raise `Exception`. So `except Exception as e: release_fail = …` never fires and `if release_fail is not None: return 3` is unreachable. `EXPECTED_RED` (`:2829-2864`) has no epoch-release row, so no mutant would catch it. The rev23 comment at `:1529-1531` — *"a success verdict is never durable before exact staging cleanup and epoch release"* — is half unproven.

### 7. `recover()` exits 0 on `unproven` — the machine-readable rollback signal is not decisive
`tg_doorbell.py:1514-1517,1556`

`verdict` is `"unproven"` whenever sidecars are present or identity is unknown, yet `return 0 if reason is None else 3`. The crashed-WAL case — the case `recover` exists for — exits **0** while the report itself says `apply НЕ безопасен без ручного осмотра`. Any wrapper gating on exit code reads *unproven* as success. Prose is honest; the exit code is not.

### 8. Both passports are stale — the honest-coverage boundary the PASS leans on is out of date
`tg_doorbell.py:181`, `_test_tg_doorbell.py:6-12,17`

Test docstring says `updated: 2026-09-16 rev6` and its *ЧЕСТНАЯ КАРТА ПОКРЫТИЯ* lists **8** RED classes against an actual `EXPECTED_RED` of **34**. Neither passport documents the provisional-report protocol (`_downgrade_cleanup_report`, `_finalize_cleanup_report`) that now governs `report.json`.

### 9. One GREEN case certifies a lookup, not an invocation
`_test_tg_doorbell.py:179-182,185-191,2481-2485`

`_PROBE` is computed at **import**; `t_bus_ping_ownership_probe()` only re-reads that dict. The exact-once receipt gate therefore blesses a constant replay for this case — the precise "receipt without invocation" hole rev23 claims to close. (Its two REDs do run live, so the class is covered, just mis-certified.)

### 10. Minor — dead branch in the candidate-SHA seam
`tg_doorbell.py:1498-1501`. Both arms of `if not _CAND_SHA_GUARDED: … else: …` call `_sha_file(cand)` identically; only the `except` differs. Reads as if the seam toggles the call when it toggles the handler.

### 11. Minor — unbounded recovery bundles
`tg_doorbell.py:1398-1399`. Each `recover` creates a full DB copy next to the production DB, never cleaned. Intentional as evidence, but no retention policy.

---

### What I could *not* verify, explicitly
- The external meta-harness (`17/17`, `survivors 0`, `sentinels 17/17`) lives in `%TEMP%\tg-doorbell-meta-harness-*` under a lease held by **the same codex session that is still editing the source**. Self-referential evidence; I did not run it and would not treat it as independent.
- I did not execute either file. Running the suite writes to `%TEMP%` and imports `bus_ping`, and the target is mutating under an active lease — a run now would measure a moving artifact and tell you nothing about `CBD7FA…`.

### Honest credit where due
The scaffold hardening is real and better than most: AST node-hash freezing of the verdict funnel (`:2359-2448`), literal cardinality gates (59/34/93), identity fingerprints over both registries, static `red(...)` call-site binding against the manifest (`:2889-2906`), four-phase exact-once receipts, ownership-by-exact-mkdtemp-path rather than glob, and a foreign-sentinel survival assertion. Findings 2, 5 and 9 are gaps *in* that design, not an absence of it.

### To move this to VERIFY
1. Quiesce the lease, freeze the source, and publish its actual SHA; re-run the full matrix against that exact byte-sequence.
2. Add an expected-SHA pin for `tg_doorbell.py` inside the suite (finding 2) and source-level literal pins for `CHAT`/`SENDERS`/`ALLOWED_DOOR` (finding 5), each with its own RED.
3. Decide the gap-path contract: either an age-based escalation/dead-letter for spooled rows, or an explicit "GAP" health state distinct from dirty — and drain or dismiss the 2 live pending rows deliberately (that deletion is Tier-2, your call, not mine).
4. Split `recover` exit codes so `unproven` ≠ 0, or document that callers must parse `report.json` and never the rc.
5. Refresh both passports and the coverage map before re-freeze.

🧒 **Простыми словами:** Мне дали проверить два файла и сказали «вот их отпечатки пальцев». У теста отпечаток совпал, а у главного файла — **нет**: его кто-то переписал полчаса назад и **прямо сейчас держит открытым**. Значит все красивые цифры «93 из 93, всё зелёное» — про другой файл, не про тот, что лежит на диске.

Хуже: сам тест такое поймать не может. Он запоминает файл в момент старта и потом проверяет «не менялся ли он по ходу». Менялся ДО — он не заметит.

И ещё: звонок уже работает по-настоящему, в настоящем чате. Два настоящих сообщения лежат непрочитанными с 8 утра, дверь для доставки просто не настроена, а по устройству программы они **никогда** не попадут в «мёртвые письма» и никто про них не крикнет. Будильник тикает каждые 2 минуты и молчит.

Поэтому — BLOCK.
