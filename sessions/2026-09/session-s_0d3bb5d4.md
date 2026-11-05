---
session: s_0d3bb5d4
date: 2026-09-21
words: 703
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · Formal review round 3 of 3. Review only this final mutation-oracle repair. The prior full…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0d3bb5d4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Formal review round 3 of 3. Review only this final mutation-oracle repair. The prior full mutation run returned rc=3 because two deliberate mutants raised sqlite3.IntegrityError('UNIQUE constraint failed: question_claims.canonical_file') before the internal case serialized FAIL_CASE. The global harness contract is strict: unexpected crash/timeout/missing report is rc=3 and never a semantic kill. Decide whether these two case-local catches honestly convert a directly caused, exact invariant violation into semantic rc=1 without hiding candidate failures. Candidate normal run is 52/52 and mutation preflight is 71/71 on harness SHA A93550EEE9CB5C24107FDD69BFAC209106F7905BBAB7D107AF393B445039117B. Also note rollout boundary: this artifact is node-local strict core only and explicitly non-deployable until controlled stop-the-world drain; do not request a legacy no-epoch shim. End with VERDICT per reviewer contract.


DIFF:
diff --git a/_shared/_test_workclaim_toctou.py b/_shared/_test_workclaim_toctou.py
--- a/_shared/_test_workclaim_toctou.py
+++ b/_shared/_test_workclaim_toctou.py
@@ question_current_path_to_git_transition_fails_closed
-        result = wc.claim_question(
-            "Q-CURRENT-GIT", str(target_path), "implementer", "NEW")
+        claim_error = None
+        try:
+            result = wc.claim_question(
+                "Q-CURRENT-GIT", str(target_path), "implementer", "NEW")
+        except sqlite3.IntegrityError as exc:
+            # A mutant that trusts the stale path identity reaches the
+            # canonical-file UNIQUE fence. That is a semantic failure of the
+            # mutant, not evidence that the mutation harness itself crashed.
+            result = None
+            claim_error = (type(exc).__name__, exc.args)
@@
-                and not result.ok and result.reason == "backend-error"
+                and result is not None
+                and not result.ok and result.reason == "backend-error"
@@
+                    "claim_error": claim_error,
@@ multi_file_question
-        wrong_question = wc.claim_question(
-            "Q-OTHER", first_path, "implementer", "B")
+        wrong_question_error = None
+        try:
+            wrong_question = wc.claim_question(
+                "Q-OTHER", first_path, "implementer", "B")
+        except sqlite3.IntegrityError as exc:
+            # Removing logical-file uniqueness lets the mutant run into the
+            # independent canonical-file UNIQUE fence. Record the exact
+            # semantic mismatch so it becomes FAIL_CASE/rc=1, never a false
+            # kill via an uncaught harness exception.
+            wrong_question = None
+            wrong_question_error = (type(exc).__name__, exc.args)
@@
-            and not wrong_question.ok and wrong_question.reason == "busy"
+            and wrong_question is not None
+            and not wrong_question.ok and wrong_question.reason == "busy"
@@
-                              wrong_question.reason),
+                              (wrong_question.reason
+                               if wrong_question is not None else None)),
+            "wrong_question_error": wrong_question_error,

---

**Claude:**

15:54, понедельник, 21 сентября 2026

Let me read the actual files before judging the diff.

---

> `Bash` -- {"command": "ls && git status --short && git diff --stat", "description": "List repo and diff stat"}

---

> `Bash` -- {"command": "wc -l _shared/_test_workclaim_toctou.py _shared/_test_workclaim.py _shared/workclaim.py retro_lost_scan.py 2>/dev/null", "description": "Line counts of touched files"}

---

> `Bash` -- {"command": "git diff --stat -- _shared/ retro_lost_scan.py", "description": "Diff stat of source files"}

---

> `Bash` -- {"command": "grep -n \"IntegrityError\\|claim_error\\|wrong_question_error\" _shared/_test_workclaim_toctou.py | head -60", "description": "Find the catch sites"}

---

> `Bash` -- {"command": "sed -n '1630,1760p' _shared/_test_workclaim_toctou.py", "description": "Read first case"}

---

> `Bash` -- {"command": "sed -n '2400,2600p' _shared/_test_workclaim_toctou.py", "description": "Read second case"}

---

> `Bash` -- {"command": "ls _shared/ | grep -i -E \"mutat|workclaim|oracle\" ", "description": "Find mutation harness files"}

---

> `Bash` -- {"command": "grep -n \"FAIL_CASE\\|rc=3\\|returncode\\|MUTAT\\|mutant\" _shared/_test_workclaim_toctou.py | head -40", "description": "Find harness contract in toctou file"}

---

> `Bash` -- {"command": "sed -n '100,320p' _shared/_test_workclaim_toctou.py", "description": "Read mutation harness contract"}

---

> `Bash` -- {"command": "sed -n '2995,3110p' _shared/_test_workclaim_toctou.py", "description": "Read case entrypoint"}

---

> `Bash` -- {"command": "grep -n \"^import\\|^from\" _shared/_test_workclaim_toctou.py | head -20", "description": "Check sqlite3 import"}

---

> `Bash` -- {"command": "grep -n \"def _connect\\|def claim_question\\|def _question_conn\\|finally:\\|con.close()\\|contextmanager\" _shared/workclaim.py | head -50", "description": "Check connection handling"}

---

> `Bash` -- {"command": "sed -n '1432,1470p' _shared/workclaim.py; echo ---; sed -n '1240,1270p' _shared/workclaim.py", "description": "Read claim_question body start"}

---

> `Bash` -- {"command": "sed -n '1470,1560p' _shared/workclaim.py", "description": "Read claim_question DB section"}

---

> `Bash` -- {"command": "awk 'NR>=1560 && NR<=1680' _shared/workclaim.py | grep -n \"except\\|finally\\|_transition_release\\|raise\" | head -30; echo \"=== absolute:\"; grep -n \"except BaseException\\|except Exception\\|finally:\" _shared/workclaim.py | awk -F: '$1>1470 && $1<1720'", "description": "Find exce

---

> `Bash` -- {"command": "sed -n '1612,1625p' _shared/workclaim.py; echo \"=== _transition_release ===\"; grep -n \"def _transition_release\" -A 25 _shared/workclaim.py | head -40", "description": "Check rollback path"}

---

> `Bash` -- {"command": "grep -n \"wrong_question\\b\" _shared/_test_workclaim_toctou.py; echo \"=== result uses in case1 region ===\"; sed -n '1700,1740p' _shared/_test_workclaim_toctou.py | grep -n \"result\"", "description": "Check variable uses"}

---

> `Bash` -- {"command": "grep -n \"argv\\|--mode\\|def main\\|add_argument\\|sys.exit\" _shared/_test_workclaim_toctou.py | tail -40", "description": "Find test CLI modes"}
