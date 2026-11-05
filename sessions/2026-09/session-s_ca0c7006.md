---
session: s_ca0c7006
date: 2026-09-22
words: 2136
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · [Codex→Claude][workspace-write-guard][REVISE]

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ca0c7006` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

[Codex→Claude][workspace-write-guard][REVISE]
Third adversarial re-review. These are the exact changes made for your prior findings; use the task/measurement for context. Distinguish candidate correctness from separately blocked activation. End exactly VERDICT: APPROVE or VERDICT: REQUEST_CHANGES.

TASK:
Review Codex's root fix for the shared-workspace write guard.

Acceptance criteria:
- An opaque shell command that names no exact target must fail closed before execution.
- The denial must not acquire a cwd, directory, or executable-file lease; unrelated exact file tools must remain usable.
- Commands naming exact files retain conservative exact-file leasing; proven readers remain allowed.
- Codex shell writes in a shared main checkout remain denied before path extraction.
- Native per-call harness evidence must outrank inherited CODEX_THREAD_ID so Claude Write/Edit calls are attributed to Claude.
- The Windows `sort /o` actual-effect control must pin System32 sort rather than a PATH-selected POSIX sort.
- Tests must prove red-to-green behavior, keep production counters clean, and preserve existing lease/storm behavior.

Artifacts:
- hooks commit 7bf85addc6ffa1309ab40f78f07e59ba073748b1
- scripts/tests commit 19753c413d20faecc680e104231c61d5afce8203

Return an adversarial review and only APPROVE if no MED/HIGH issue remains.

Operational measurement before activation:
- live usage counter, rolling 24h: about 5,058 legacy `no-mutation-marker` events;
- 454 recent local transcripts: 5,052 shell calls classified as 3,590 opaque, 806 proven-reader, 656 visible-mutation;
- opaque samples mix genuine readers with writers and arbitrary Python/scripts, so they cannot be safely allowlisted by executable name;
- therefore this patch is candidate-only and MUST NOT be deployed yet. The review requested here is code/test correctness. Activation remains separately blocked until a safe migration or a shared/exclusive broker design is authorized.


HOOK DELTA:
diff --git a/workspace_write_guard.py b/workspace_write_guard.py index f266b05..887eb23 100644 --- a/workspace_write_guard.py +++ b/workspace_write_guard.py @@ -55,6 +55,7 @@ import workspace_write_lease as lease  # noqa: E402    FILE_TOOLS = {"write", "edit", "multiedit", "notebookedit", "apply_patch"}  SHELL_TOOLS = {"bash", "powershell", "shell", "exec_command"} +OPAQUE_NO_TARGET_REASON = "opaque shell command has no exact file target"  PATCH_PATH = re.compile(      r"^\*\*\* (?:Update|Add|Delete) File:\s*(.+?)\s*$|^\*\*\* Move to:\s*(.+?)\s*$",      re.MULTILINE) @@ -178,13 +179,9 @@ def agent_name(payload):      # Claude launched below a Codex parent legitimately inherits CODEX_THREAD_ID;      # classifying from that variable first poisoned both the DB owner and usage      # counter even though Write/Edit + prompt_id were unambiguously Claude. -    if tool in {"write", "edit", "multiedit", "notebookedit"}: +    if tool in {"write", "edit", "multiedit", "notebookedit", "bash", "powershell"}:          return "claude" -    if tool == "apply_patch": -        return "codex" -    if payload.get("prompt_id"): -        return "claude" -    if payload.get("turn_id") and payload.get("tool_use_id"): +    if tool in {"apply_patch", "exec_command", "shell"}:          return "codex"      if os.environ.get("CLAUDECODE"):          return "claude" @@ -786,7 +783,7 @@ def extract_intent(payload):                                    {"tool": tool_name(payload),                                     "resources": paths})                  return Intent(True, paths, "conservative-shell-exact-path") -            return Intent(True, [], "opaque shell command has no exact file target") +            return Intent(True, [], OPAQUE_NO_TARGET_REASON)          if not paths:              lease.count_event("hook", "blocked-unparsed", {"tool": tool_name(payload)})              return Intent(True, [], "visible writer has no exact file target") @@ -855,7 +852,7 @@ def guard_pre(payload):          return Decision(True, intent.reason, [])      if not intent.paths:          outcome = ("blocked-opaque-shell" -                   if intent.reason == "opaque shell command has no exact file target" +                   if intent.reason == OPAQUE_NO_TARGET_REASON                     else "blocked-unparsed")          lease.count_event("hook", outcome, {"tool": tool_name(payload)})          return Decision(False, intent.reason or

TEST DELTA:
diff --git a/_test_lease_storm.py b/_test_lease_storm.py index 7334f0c04..ff181b1bb 100644 --- a/_test_lease_storm.py +++ b/_test_lease_storm.py @@ -141,6 +141,11 @@ def _run(tmp):             'sed -i "s/a/b/" "%s"' % busy, hot)      # Isolate the opaque-deny checks from case 1's legitimate exact-file lease.      lease.release_session("session-B", epoch="lease-storm-session-B") +    rows_after_exact_release = [ +        row for row in lease.active() if row.get("session") == "session-B"] +    if rows_after_exact_release: +        fails.append("3b. exact release перед opaque cases не сработал: %r" % +                     rows_after_exact_release)        # --- границы -----------------------------------------------------------------------      expect("4. opaque из cwd закрыт, но cwd не лизуется", 2, "python build.py", hot) diff --git a/_test_workspace_write_guard.py b/_test_workspace_write_guard.py index 79569f505..a088534c6 100644 --- a/_test_workspace_write_guard.py +++ b/_test_workspace_write_guard.py @@ -201,6 +201,16 @@ def _lease_owner(db, target):          con.close()     +def _lease_rows_for_session(db, session): +    con = sqlite3.connect(db) +    try: +        return con.execute( +            "SELECT resource,epoch,agent FROM leases WHERE session=?", (session,) +        ).fetchall() +    finally: +        con.close() + +  def _run_guard(payload, phase="pre", env=None, inject_epoch=True):      payload = dict(payload)      if inject_epoch and not (payload.get("turn_id") or payload.get("prompt_id")): @@ -329,7 +339,7 @@ def _write_guard_mutant(root, kind):              return Intent(False, [], "MUTANT unknown shell allowed")  '''          pattern = (r"        if not visible_mutation:\n" -                   r"(?=[\s\S]*?opaque shell command has no exact file target)" +                   r"(?=[\s\S]*?OPAQUE_NO_TARGET_REASON)"                     r".*?"                     r"(?=        if not paths:\n)")          source, count = re.subn( @@ -1506,10 +1516,6 @@ def main():                  payload = {"session_id": "unknown-reader-%s" % name, "cwd": root}                  payload.update(partial)                  unknown_reader_runs[name] = _run_guard(payload, env=env) -            unknown_file_owner = _lease_owner( -                env["WORKSPACE_WRITE_LEASE_DB"], unknown_a) -            unknown_dir_owner = _lease_owner( -                env["WORKSPACE_WRITE_LEASE_DB"], unknown_dir)              # pytest is not a proven reader: it writes caches, bytecode and may              # execute arbitrary project hooks. With no exact output target the              # only truthful contract is fail-closed; exact file tools remain the @@ -1524,18 +1530,20 @@ def main():                  fh.seek(opaque_counter_offset)                  opaque_rows = [json.loads(line.decode("utf-8"))                                 for line in fh if line.strip()] +            opaque_lease_rows = _lease_rows_for_session( +                env["WORKSPACE_WRITE_LEASE_DB"], "opaque-pytest")              check("proven readers certutil-hashfile/more allowed; opaque pytest fail-closed без lease",                    all(run.returncode == 0 for run in unknown_reader_runs.values()) and                    opaque_pytest.returncode == 2 and                    "opaque shell command" in opaque_pytest.stderr and -                  unknown_file_owner is None and unknown_dir_owner is None and +                  not opaque_lease_rows and                    any(row.get("outcome") == "blocked-opaque-shell"                        for row in opaque_rows), -                  "runs=%r pytest=%s/%r file-owner=%r dir-owner=%r rows=%r" % +                  "runs=%r pytest=%s/%r leases=%r rows=%r" %                    ({name: (run.returncode, run.stderr[:100])                      for name, run in unknown_reader_runs.items()},                     opaque_pytest.returncode, opaque_pytest.stderr[:140], -                   unknown_file_owner, unknown_dir_owner, opaque_rows)) +                   opaque_lease_rows, opaque_rows))              code_reader = _run_guard({                  "session_id": "unclassified-code", "cwd": root,                  "tool_name": "PowerShell", "tool_input": { @@ -1684,14 +1692,17 @@ def main():                  os.environ.get("SystemRoot") or r"C:\Windows",                  "System32", "sort.exe"))              sort_exe = windows_sort if os.path.isfile(windows_sort) else None +            git_sort_present = os.path.isfile(git_sort)              check("windows-sort-o PATH control is red; GREEN pins System32 sort", -                  poisoned_sort_exe is not None and sort_exe is not None and -                  os.path.normcase(os.path.realpath(poisoned_sort_exe)) != -                  os.path.normcase(os.path.realpath(sort_exe)) and -                  os.path.normcase(os.path.realpath(poisoned_sort_exe)) == -                  os.path.normcase(os.path.realpath(git_sort)), -                  "poisoned=%r git=%r pinned=%r" % -                  (poisoned_sort_exe, git_sort, sort_exe)) +                  sort_exe is not None and +                  (not git_sort_present or +                   (poisoned_sort_exe is not None and +                    os.path.normcase(os.path.realpath(poisoned_sort_exe)) != +                    os.path.normcase(os.path.realpath(sort_exe)) and +                    os.path.normcase(os.path.realpath(poisoned_sort_exe)) == +                    os.path.normcase(os.path.realpath(git_sort)))), +                  "git-present=%s poisoned=%r git=%r pinned=%r" % +                  (git_sort_present, poisoned_sort_exe, git_sort, sort_exe))              certutil_compound_exe = shutil.which("certutil")              false_reader_specs = []

---

**Claude:**

12:25, вторник, 22 сентября 2026

**План рельс (§6.3-бис):** сам как Claude — чтение предоставленных диффов и состязательное суждение. Наружу не уезжает: это ревью работы Codex, второе мнение того же вендора замкнуто на себя; причина недобора — `class-mismatch`.

---

# Adversarial re-review — workspace_write_guard (round 3)

## Scope of evidence (read this first)

In this session I have **no file-read, grep or shell tooling** — only the MCP connectors. So I reviewed **exactly the two diffs pasted into the task**, not commits `7bf85ad` / `19753c4` as checked out. Every finding below is labelled either *proven from the diff* or *unverifiable from the diff*, and I do not claim to have read surrounding context (session-id constants, counter redirection, the codex/main-checkout deny path, the `sort` pinning code itself). If the review must be anchored to the commits, re-issue it to a session with repo access.

The measurement framing is accepted: this is **candidate-only**, activation stays blocked, and nothing below argues for deployment. The 3,590-opaque / 806-reader split does confirm that fail-closed-by-default is the only truthful contract for opaque commands — that part of the design is right.

## What is genuinely fixed (credit where due)

`OPAQUE_NO_TARGET_REASON` removes the string-literal coupling between `extract_intent` and `guard_pre`; the mutant regex was updated in lockstep, so the mutant harness still targets the same branch.

`_lease_rows_for_session` is strictly stronger than the two `_lease_owner` probes it replaces — "this session holds **zero** rows" covers cwd, directory and executable-file leases, which is precisely acceptance criterion 2, whereas the old probes only covered two named targets.

The added `rows_after_exact_release` assertion in `_test_lease_storm.py` turns an implicit precondition into a checked one. That is the right instinct: a `release_session` that silently no-ops would previously have made the opaque cases green for the wrong reason.

## MED-1 — `agent_name` swapped native per-call ids for a hardcoded name list, and nothing tests it

*Proven from the diff.* Two per-call signals were **deleted**, not relocated:

```
-    if payload.get("prompt_id"):            return "claude"
-    if payload.get("turn_id") and payload.get("tool_use_id"): return "codex"
```

and replaced by membership in `{bash, powershell}` → claude / `{exec_command, shell}` → codex, checked *before* `CLAUDECODE`.

Three problems. First, tool names are harness-configurable, while `prompt_id` / `turn_id`+`tool_use_id` are emitted by the harness itself — the deleted signals are the *stronger* form of "native per-call harness evidence" the acceptance criterion asks for, so this change moves away from the criterion while appearing to satisfy it.

Second, a Codex call carrying a tool name outside `{apply_patch, exec_command, shell}` — an MCP shell server, a `local_shell`, any future alias — now falls through to env, and a call that happens to be named `bash`/`powershell` short-circuits to **claude before any Codex evidence is consulted at all**. Likelihood is low (Codex CLI emits `shell`/`exec_command`), but the consequence lands directly on acceptance criterion 4: the shared-main-checkout denial is agent-conditional, so a misattributed Codex call skips it and instead takes a lease. Usage-counter attribution is poisoned in the same step.

Third, and independent of likelihood: **this delta contains no test for the production change it exists to make.** No payload asserts `bash`→claude, none asserts `exec_command`→codex, none sets `CODEX_THREAD_ID` and proves Write/Edit still resolves to claude. The headline behaviour ships with zero red-to-green evidence, against the explicit test criterion.

Fix is one line of ordering: keep the name lists, but check `turn_id`+`tool_use_id` / `prompt_id` **above** them. Ids-first strictly dominates names-first — where both agree nothing changes, and where they disagree the id is the one the harness actually stamped.

## MED-2 — the `sort /o` control degrades to a near-vacuous green when Git is absent

*Proven from the diff.* The new predicate is:

```
sort_exe is not None and (not git_sort_present or (<poisoned != pinned> and <poisoned == git_sort>))
```

When `git_sort_present` is false the entire control arm is skipped and the assertion collapses to "System32 sort exists on a Windows box" — which proves nothing about pinning. The check still prints under the label *"windows-sort-o PATH control is red; GREEN pins System32 sort"*, so a machine without Git-for-Windows reports the same green as a machine where the control genuinely fired.

That is the failure mode §5.4 names outright: a test that cannot turn red is not evidence, and an instrument that reports identical output whether or not it measured anything is worse than an absent instrument, because it invites a false "covered". Make the missing-Git case a visible **SKIP** with a reason, not a pass.

Separately: even in the Git-present arm, the assertion checks properties of `poisoned_sort_exe` and the existence of `sort_exe` — it does **not** assert that the green control run actually invoked `sort_exe`. The pinning code is outside the shown hunk, so whether the assertion is coupled to the behaviour it names is *unverifiable from the diff*. If the pin lives in a variable the check never reads, criterion 6 is unmet regardless of Git.

## MED-3 — the new lease assertion is keyed on a session string I cannot see

*Unverifiable from the diff.* The replacement reads:

```
opaque_lease_rows = _lease_rows_for_session(<db>, "opaque-pytest")
... not opaque_lease_rows ...
```

The `opaque_pytest` payload is constructed above the shown hunk. If its `session_id` is anything other than the literal `"opaque-pytest"`, the query returns `[]`, `not []` is true, and the assertion passes **vacuously** — while the two target-anchored `_lease_owner` probes that would have caught a stray lease on `unknown_a` / `unknown_dir` have just been deleted.

The mutant harness does not cover this: the mutant regex flips the opaque branch's return, which changes the exit code the check also asserts, so the mutant dies on `returncode == 2` without ever exercising the lease clause. Prove it red — introduce a deliberate lease under that exact session and show the check failing — or assert against the same constant the payload is built from, not a re-typed literal.

## NIT

The comment block above `agent_name` still explains the `CODEX_THREAD_ID` poisoning in terms of `prompt_id` being consulted first; `prompt_id` no longer appears in the function. Stale rationale on a security-relevant classifier invites the next editor to "restore" the wrong thing.

## Verdict rationale

Criteria 1, 2 and 3 look satisfied by the fail-closed branch plus the strengthened lease assertion — modulo MED-3's keying. Criterion 5 is addressed in direction but weakened in mechanism and untested (MED-1). Criterion 6 is not demonstrably met (MED-2). Criterion 7 fails on "tests must prove red-to-green" for both of the production changes in this round.

Three MED issues remain, so per the instruction to approve only on a clean board:

🧒 Простыми словами: Кодекс починил главное — непонятная команда теперь останавливается и ничего не захватывает, это правда хорошо. Но он выкинул надёжный «паспорт» звонка и стал узнавать своих по имени инструмента — так можно перепутать, кто пришёл. И два новых теста умеют показывать зелёный, даже когда они ничего не проверили: один — если на машине нет Git, другой — если имя сессии написано с опечаткой. Поэтому пока «переделать», а не «принято». Никуда это не выкатывается, речь только о правильности кода.

VERDICT: REQUEST_CHANGES
