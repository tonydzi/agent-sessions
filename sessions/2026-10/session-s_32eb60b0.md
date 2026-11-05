---
session: s_32eb60b0
date: 2026-10-03
words: 4197
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-03 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_32eb60b0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author.
The author (Codex) wrote the change below. Review it on its own merits. Do NOT use any tools
or read other files; review ONLY the diff provided. Be concrete and skeptical.

CRITICAL OUTPUT CONTRACT: the VERY LAST line of your reply must be exactly
  ===VERDICT=== <value>
where <value> is one bare word: APPROVE (no blocking issues) or
REQUEST_CHANGES (one or more MED/HIGH issues). No backticks, no bold, no
brackets, nothing else on that line. State it exactly once, on that final
line only -- do not repeat the marker anywhere else in your reply.

Write your review first, then the contract line last.

## What Codex was asked to do (context)
Task: independent safety review of the Google/Firefox logout investigation's cleanup repair.
Author: Codex. Reviewer: Claude Opus (only formal reviewer assigned). Operator: dev. Host: HUB-01.

Proven old defect (offline reproduction of actual source with mocked delete/network/browser):
dr_ff_collect --no-copy defaults false, but dr_ff_rail.copy_profile switches its own local no_copy to true for a rotating session and returns the ORIGINAL profile. Collector finally still tests the original argparse flag then rmtree(prof.parent, ignore_errors=True). For AutoFF this selects C:\Users\dev\AppData\Local. The actual delete function was replaced by a Mock in reproduction; no profiles or cookies were modified.

Acceptance:
1. Only a temporary root allocated by this invocation may be removed. Return path shape or requested CLI mode alone is NOT proof of ownership.
2. Original profile and any directory containing it always survive, including original profiles located in Temp/ffrail-existing/p.
3. In-place return has no owned roots; actual clone records mkdtemp result BEFORE copytree so partial copy can be cleaned.
4. Fail closed for source/candidate aliases, symlinks/junctions, malformed paths, canonicalization failure. Ordinary temporary clone cleanup still works.
5. Both consumers, collector and rail main, use explicit recorded ownership. Profile lock depends on ACTUAL profile mode.
6. Failure during copy, driver creation, waiting, or quit must not permit broad deletion; preserve existing Windows timer repair.
7. Tests must be safe: no live browser, network, cookie values, real profile mutation. Mock rmtree at production call boundary. Real filesystem fixtures must stay in their own fresh temporary directory. Regression should detect the old caller behavior.
8. Keep API compatible for existing callers that expect Path from copy_profile.

Evidence scope: actual collector launch Oct2 19:01:31.133 UTC without --no-copy is recorded in Claude transcript98c27f3c, after SIGALRM repair. Completion at19:21:20UTC, output only pipeline code0; exact finally execution not recorded. AutoFF present18:41UTC, absent21:55UTC. This supports a strong incident hypothesis, but the patch must not claim this later evening event proves the user's prior daily morning logouts.

Review only supplied diff. Do not execute browser scripts, delete anything, or modify files. Report real correctness/data-loss issues and exact lines. A clean unit suite is not evidence of next-morning user outcome or fleet deployment.

RE-REVIEW CONTEXT after REQUEST_CHANGES in review-20261003-034425.md:
The previous medium finding explicitly said omitted handlers "almost certainly" use a driver. This is a source claim to verify, not an assumption to preserve. Here is the COMPLETE actual collector exception handler (unchanged by patch):

    except (TimeoutError, KeyboardInterrupt) as e:
        # KeyboardInterrupt = Windows timer interrupt_main
        if isinstance(e, KeyboardInterrupt):
            e = TimeoutError(f"hard timeout {a.timeout + 120}s (win-alarm)")
        print(f"FAIL: {e}", file=sys.stderr)
        return 3

The Russian message literals were translated above for readability; the executable names/control flow are exact. There is NO reference to d, driver, or prof. dr_ff_rail.main has NO except handler at all; it has the try/finally shown in the diff. The module-level fallback only prints the caught exception and sys.exit(4), without touching profiles/drivers.

The author is adding acquisition-stage TimeoutError and KeyboardInterrupt tests for BOTH consumers so this claim is now directly exercised before driver assignment, in addition to the earlier copy/driver OSError tests. Judge their actual outputs and structure, not guesses about omitted lines.

Other prior findings:
- Dropping ignore_errors makes the SAME unsuccessful rmtree visible; it does not newly cause leftover locked files. Retry/chmod is not necessary to remove the proven data-loss defect and is not added in this bounded fix. Existing ff_profile_sweeper is separate; no claim of zero orphan temp files.
- Parent alias test is renamed to reflect rejecting a root outside the exact temp parent. Canonical checks are intentionally conservative/fail-closed; do not demand removing a safety check solely because it overlaps another check.
- Inventory in canonical scripts: copy_profile is called by the two converted mains and _probe_gemini_menu.py with explicit True (in-place), no parent deletion. Collector has no remaining shutil use. Legacy copies in D:/Vault/_imports are under a separate reachability audit; acceptance is the two current production entry points, not fleet deployment or every historical source snapshot.

Please reconsider the prior MED finding using the supplied actual handler. A failed hypothesis does not require changing correct code to make it look like the proposed fix. Report only concrete remaining defects; identify any claim requiring unprovided context instead of inventing that context.

Fresh re-review validation: 39/39 tests pass, including make_driver TimeoutError and copytree KeyboardInterrupt before driver assignment in both mains, plus in-place rail TimeoutError lock release. AST inspection confirms collector handler does not load d/driver/prof and rail try has zero handlers. Implementation source is unchanged from the first review; tests now exercise the hypothesized window and parent test name is corrected.

Reachability inventory completed: both copies of dr_queue.py lines680-690 generate explicit ~/.claude/scripts/dr_ff_rail.py and dr_ff_collect.py commands; canonical dr_latecomer_sweep.py resolves adjacent collector; secondop.py and cv_dr_topup_run.py select C:/Users/dev/.claude/scripts/dr_ff_rail.py. Windows DR Runner and DR-Queue-Robot also enter canonical scripts. No configured scheduled/action route to D:/Vault/_imports/dr_ff_*.py found in audited set; those legacy copies remain manually reachable, unmodified and outside current production entry points. No claim of fleet coverage.

The first review's phrase 'age-based AppData sweep already caused damage' is not supported by the incident evidence: the proven flaw was wrong ownership in collector cleanup, not the age-based sweeper. Avoid using that premise to require unrelated retry/chmod behavior.

Check, in priority order:
1. CORRECTNESS bugs (logic errors, off-by-one, wrong conditions, unhandled cases, races).
2. SECURITY (injection, secrets in code, unsafe input, path/permission issues).
3. BREAKAGE (does it break callers, contracts, or existing behavior?).
4. SIMPLIFICATION / dead code (is there a simpler, equally-correct form? AK-47).

Rules:
- Fix the ROOT cause, not the symptom. If you propose a fix, make it the simplest correct one.
- Only report REAL issues. If the diff is clean, say so plainly.
- For each finding give: `file:line` | severity (high/med/low) | what's wrong | the fix.

Format:
SUMMARY: <one or two sentences>
FINDINGS:
- file:line | severity | issue | fix
(repeat; write "none" if no findings)
Then the contract line from the output contract above, last.

--- DIFF START ---
diff --git a/_test_dr_ff_collect_cleanup.py b/_test_dr_ff_collect_cleanup.py
new file mode 100644
index id_c9083e08..db9752670
--- /dev/null
+++ b/_test_dr_ff_collect_cleanup.py
@@ -0,0 +1,366 @@
+#!/usr/bin/env python3
+"""Offline ownership regression; actual main/copy functions, fake browser/rmtree.
+
+Fixtures only in a fresh TemporaryDirectory; no production profiles or network.
+DR_FF_CLEANUP_OLD_REF=<git commit> runs against the old source from git show.
+Consumer: dr_ff_collect / dr_ff_rail. rail: stdlib, local CPU, 0 LLM.
+"""
+from __future__ import annotations
+import contextlib
+import io
+import os
+from pathlib import Path
+import shutil
+import subprocess
+import sys
+import tempfile
+import types
+import unittest
+from unittest.mock import Mock, patch
+
+HERE = Path(__file__).resolve().parent
+
+
+def source(name):
+    old = os.environ.get("DR_FF_CLEANUP_OLD_REF")
+    if old:
+        return subprocess.check_output([
+            "git", "-C", str(HERE), "show", f"{old}:{name}.py",
+        ]).decode("utf-8-sig")
+    return (HERE / (name + ".py")).read_text(encoding="utf-8-sig")
+
+
+class Fixture(unittest.TestCase):
+    def setUp(self):
+        self.tmp = tempfile.TemporaryDirectory(prefix="test-dr-ff-cleanup-")
+        self.root = Path(self.tmp.name).resolve()
+        self.temp = self.root / "temp"
+        self.temp.mkdir()
+        self.base = self.root / "original-profile"
+        self.base.mkdir()
+        (self.base / "prefs.js").write_text("// fixture", encoding="utf-8")
+        (self.root / "prompt.txt").write_text("fixture", encoding="utf-8")
+        self.stack = contextlib.ExitStack()
+        self.addCleanup(self.tmp.cleanup)
+        self.addCleanup(self.stack.close)
+        old_path = sys.path[:]
+        self.stack.callback(lambda: sys.path.__setitem__(slice(None), old_path))
+        self.stack.enter_context(patch.dict(os.environ, {
+            "FF_ALLOW_CLONE_SESSION": "", "FF_ALLOW_INPLACE_HUMAN": "",
+        }))
+        self.fs = types.ModuleType("firefox_selenium")
+        self.fs.AUTOFF_DIR = str(self.base)
+        self.fs.find_stock_firefox = lambda: "fixture-firefox-never-started"
+        self.fs._is_human_profile = Mock(return_value=False)
+        self.fs.has_rotating_session = Mock(return_value=False)
+        self.rail = types.ModuleType("dr_ff_rail")
+        self.stack.enter_context(patch.dict(sys.modules, {
+            "firefox_selenium": self.fs, "dr_ff_rail": self.rail,
+        }))
+        self.collect = types.ModuleType("dr_ff_collect")
+        for module in (self.rail, self.collect):
+            module.__file__ = str(HERE / (module.__name__ + ".py"))
+            exec(compile(source(module.__name__), module.__file__, "exec"), module.__dict__)
+        self.stack.enter_context(patch.object(tempfile, "gettempdir", return_value=str(self.temp)))
+        self.delete = self.stack.enter_context(patch.object(shutil, "rmtree"))
+        self.stack.enter_context(patch.object(self.rail.time, "sleep"))
+        self.err = self.stack.enter_context(contextlib.redirect_stderr(io.StringIO()))
+        self.stack.enter_context(contextlib.redirect_stdout(io.StringIO()))
+        self.driver = Mock()
+        self.driver.current_url = "https://accounts.google.com/login"
+        self.driver.execute_script.return_value = True
+        for module in (self.rail, self.collect):
+            self.stack.enter_context(patch.object(module, "make_driver", return_value=self.driver))
+        self.stack.enter_context(patch.object(self.collect, "wait_stable", return_value="x" * 4000))
+        self.stack.enter_context(patch.object(self.collect, "harvest_links", return_value=""))
+        self.alarm = Mock()
+        self.collect.signal = types.SimpleNamespace(SIGALRM=14, signal=Mock(), alarm=self.alarm)
+        self.lock = self.stack.enter_context(patch.object(self.rail, "profile_lock", side_effect=self.create_lock))
+
+    def create_lock(self, profile):
+        lock = Path(profile) / ".dr_ff_rail.lock"
+        lock.touch()
+        return lock
+
+    def run_main(self, module, *flags):
+        argv = [module.__name__, "--rail", "gemini", "--out", str(self.root / "out.txt"),
+                "--profile-dir", str(self.base)]
+        if module is self.rail:
+            argv += ["--prompt-file", str(self.root / "prompt.txt")]
+        with patch.object(sys, "argv", argv + list(flags)):
+            return module.main()
+
+    def assert_owned_cleanup(self):
+        roots = list(self.temp.glob("ffrail-*"))
+        self.assertEqual(len(roots), 1)
+        self.assertEqual(self.delete.call_count, 1)
+        self.assertEqual(Path(self.delete.call_args.args[0]), roots[0])
+        self.assertTrue((self.base / "prefs.js").is_file())
+
+
+class CollectTests(Fixture):
+    def test_rotating_default_never_deletes_source(self):
+        self.fs.has_rotating_session.return_value = True
+        self.assertEqual(self.run_main(self.collect), 0)
+        self.delete.assert_not_called()
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_explicit_no_copy_never_deletes_source(self):
+        self.assertEqual(self.run_main(self.collect, "--no-copy"), 0)
+        self.delete.assert_not_called()
+
+    def test_real_clone_cleans_only_its_own_root(self):
+        self.assertEqual(self.run_main(self.collect), 0)
+        self.assert_owned_cleanup()
+
+    def test_existing_ffrail_source_is_not_owned(self):
+        self.base = self.temp / "ffrail-existing" / "p"
+        self.base.mkdir(parents=True)
+        self.fs.has_rotating_session.return_value = True
+        self.assertEqual(self.run_main(self.collect), 0)
+        self.delete.assert_not_called()
+
+    def test_copy_failure_cleans_recorded_root(self):
+        with patch.object(shutil, "copytree", side_effect=OSError("fixture copy failure")):
+            with self.assertRaisesRegex(OSError, "fixture copy"):
+                self.run_main(self.collect)
+        self.assert_owned_cleanup()
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_driver_failure_cleans_recorded_root(self):
+        self.collect.make_driver.side_effect = RuntimeError("fixture driver failure")
+        with self.assertRaisesRegex(RuntimeError, "fixture driver"):
+            self.run_main(self.collect)
+        self.assert_owned_cleanup()
+        self.driver.quit.assert_not_called()
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_driver_timeout_before_assignment_returns_three(self):
+        self.collect.make_driver.side_effect = TimeoutError("fixture startup timeout")
+        self.assertEqual(self.run_main(self.collect), 3)
+        self.assert_owned_cleanup()
+        self.driver.quit.assert_not_called()
+        self.assertIn("FAIL: fixture startup timeout", self.err.getvalue())
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_copy_interrupt_before_profile_assignment_returns_three(self):
+        with patch.object(shutil, "copytree", side_effect=KeyboardInterrupt()):
+            self.assertEqual(self.run_main(self.collect), 3)
+        self.assert_owned_cleanup()
+        self.collect.make_driver.assert_not_called()
+        self.driver.quit.assert_not_called()
+        self.assertIn("win-alarm", self.err.getvalue())
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_timeout_still_cleans_clone_and_cancels_alarm(self):
+        self.collect.wait_stable.side_effect = TimeoutError("fixture timeout")
+        self.assertEqual(self.run_main(self.collect), 3)
+        self.assert_owned_cleanup()
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_keyboard_interrupt_still_cleans_clone(self):
+        self.collect.wait_stable.side_effect = KeyboardInterrupt()
+        self.assertEqual(self.run_main(self.collect), 3)
+        self.assert_owned_cleanup()
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_quit_error_still_cleans_clone(self):
+        self.driver.quit.side_effect = KeyboardInterrupt()
+        self.assertEqual(self.run_main(self.collect), 0)
+        self.assert_owned_cleanup()
+        self.assertEqual(self.alarm.call_args.args, (0,))
+
+    def test_windows_timer_remains_until_quit_then_cancels(self):
+        timers = []
+        class Timer:
+            def __init__(self, seconds, callback):
+                self.seconds, self.cancelled = seconds, False
+                timers.append(self)
+            def start(self):
+                pass  # No thread or interrupt is ever started in this test.
+            def cancel(self):
+                self.cancelled = True
+        self.collect.signal = types.SimpleNamespace()
+        self.driver.quit.side_effect = lambda: self.assertFalse(timers[-1].cancelled)
+        with patch("threading.Timer", Timer):
+            self.assertEqual(self.run_main(self.collect), 0)
+        self.assertEqual([t.seconds for t in timers], [1020, 30])
+        self.assertTrue(all(t.cancelled for t in timers))
+        self.assert_owned_cleanup()
+
+
+class RailTests(Fixture):
+    def test_rotating_copy_override_locks_actual_source(self):
+        self.fs.has_rotating_session.return_value = True
+        self.assertEqual(self.run_main(self.rail, "--copy"), 2)
+        self.lock.assert_called_once_with(self.base)
+        self.delete.assert_not_called()
+        self.assertFalse((self.base / ".dr_ff_rail.lock").exists())
+
+    def test_inplace_default_locks_source_and_never_deletes(self):
+        self.assertEqual(self.run_main(self.rail), 2)
+        self.lock.assert_called_once_with(self.base)
+        self.delete.assert_not_called()
+
+    def test_explicit_no_copy_never_deletes(self):
+        self.assertEqual(self.run_main(self.rail, "--no-copy"), 2)
+        self.delete.assert_not_called()
+
+    def test_clone_cleans_own_root_without_source_lock(self):
+        self.assertEqual(self.run_main(self.rail, "--copy"), 2)
+        self.lock.assert_not_called()
+        self.assert_owned_cleanup()
+
+    def test_existing_ffrail_source_is_not_owned(self):
+        self.base = self.temp / "ffrail-existing" / "p"
+        self.base.mkdir(parents=True)
+        self.fs.has_rotating_session.return_value = True
+        self.assertEqual(self.run_main(self.rail, "--copy"), 2)
+        self.delete.assert_not_called()
+
+    def test_copy_failure_cleans_recorded_root(self):
+        with patch.object(shutil, "copytree", side_effect=OSError("fixture copy failure")):
+            with self.assertRaisesRegex(OSError, "fixture copy"):
+                self.run_main(self.rail, "--copy")
+        self.assert_owned_cleanup()
+
+    def test_clone_driver_failure_cleans_recorded_root(self):
+        self.rail.make_driver.side_effect = RuntimeError("fixture driver failure")
+        with self.assertRaisesRegex(RuntimeError, "fixture driver"):
+            self.run_main(self.rail, "--copy")
+        self.assert_owned_cleanup()
+        self.driver.quit.assert_not_called()
+
+    def test_inplace_driver_failure_releases_lock(self):
+        self.rail.make_driver.side_effect = RuntimeError("fixture driver failure")
+        with self.assertRaisesRegex(RuntimeError, "fixture driver"):
+            self.run_main(self.rail)
+        self.assertFalse((self.base / ".dr_ff_rail.lock").exists())
+        self.delete.assert_not_called()
+
+    def test_driver_timeout_before_assignment_propagates_and_cleans_clone(self):
+        self.rail.make_driver.side_effect = TimeoutError("fixture startup timeout")
+        with self.assertRaisesRegex(TimeoutError, "fixture startup timeout"):
+            self.run_main(self.rail, "--copy")
+        self.assert_owned_cleanup()
+        self.lock.assert_not_called()
+        self.driver.quit.assert_not_called()
+
+    def test_inplace_driver_timeout_releases_source_lock(self):
+        self.rail.make_driver.side_effect = TimeoutError("fixture startup timeout")
+        with self.assertRaisesRegex(TimeoutError, "fixture startup timeout"):
+            self.run_main(self.rail)
+        self.lock.assert_called_once_with(self.base)
+        self.assertFalse((self.base / ".dr_ff_rail.lock").exists())
+        self.delete.assert_not_called()
+
+    def test_copy_interrupt_before_profile_assignment_propagates(self):
+        with patch.object(shutil, "copytree", side_effect=KeyboardInterrupt()):
+            with self.assertRaises(KeyboardInterrupt):
+                self.run_main(self.rail, "--copy")
+        self.assert_owned_cleanup()
+        self.rail.make_driver.assert_not_called()
+        self.lock.assert_not_called()
+        self.driver.quit.assert_not_called()
+
+    def test_quit_interrupt_still_cleans_clone(self):
+        self.driver.quit.side_effect = KeyboardInterrupt()
+        with self.assertRaises(KeyboardInterrupt):
+            self.run_main(self.rail, "--copy")
+        self.assert_owned_cleanup()
+
+
+class OwnershipTests(Fixture):
+    def test_copy_records_root_before_copy_failure(self):
+        owned = []
+        def fail_copy(base, destination, **kwargs):
+            self.assertEqual(owned, [destination.parent])
+            raise OSError("fixture partial copy")
+        with patch.object(shutil, "copytree", side_effect=fail_copy):
+            with self.assertRaisesRegex(OSError, "fixture partial"):
+                self.rail.copy_profile(False, self.base, owned_temp_roots=owned)
+        self.assertEqual(len(owned), 1)
+
+    def test_inplace_does_not_register_source_as_owned(self):
+        owned = []
+        self.assertEqual(self.rail.copy_profile(True, self.base, owned_temp_roots=owned), self.base)
+        self.assertEqual(owned, [])
+
+    def test_helper_accepts_owned_temp_root_only(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        self.assertEqual(self.rail.cleanup_profile_roots([owned], self.base), 1)
+        self.delete.assert_called_once_with(owned)
+
+    def assert_refused(self, root, base=None):
+        self.assertEqual(self.rail.cleanup_profile_roots([root], base or self.base), 0)
+        self.delete.assert_not_called()
+        self.assertIn("cleanup refused", self.err.getvalue())
+
+    def test_source_root_is_refused_even_with_ffrail_prefix(self):
+        self.base = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        self.assert_refused(self.base)
+
+    def test_root_containing_source_is_refused(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        base = owned / "p"
+        base.mkdir()
+        self.assert_refused(owned, base)
+
+    def test_root_inside_source_is_refused(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        self.assert_refused(owned, self.temp)
+
+    def test_non_temp_root_is_refused(self):
+        owned = self.root / "ffrail-outside"
+        owned.mkdir()
+        self.assert_refused(owned)
+
+    def test_non_prefixed_root_is_refused(self):
+        owned = self.temp / "original-profile"
+        owned.mkdir()
+        self.assert_refused(owned)
+
+    def test_root_outside_temp_alias_refused(self):
+        alias_parent = self.root / "temp-alias"
+        owned = alias_parent / "ffrail-own"
+        original = Path.resolve
+        def resolve(path, *args, **kwargs):
+            return self.temp if path == alias_parent else original(path, *args, **kwargs)
+        with patch.object(Path, "resolve", resolve):
+            self.assert_refused(owned)
+
+    def test_relative_root_is_refused(self):
+        self.assert_refused(Path("ffrail-relative"))
+
+    def test_traversal_alias_is_refused(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        self.assert_refused(self.temp / "unused" / ".." / owned.name)
+
+    def test_symlink_root_is_refused(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        original = Path.is_symlink
+        with patch.object(Path, "is_symlink", lambda p: p == owned or original(p)):
+            self.assert_refused(owned)
+
+    def test_junction_root_is_refused(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        with patch.object(os.path, "isjunction", lambda p: Path(p) == owned, create=True):
+            self.assert_refused(owned)
+
+    def test_resolved_root_alias_is_refused(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        original = Path.resolve
+        def resolve(path, *args, **kwargs):
+            return self.base if path == owned else original(path, *args, **kwargs)
+        with patch.object(Path, "resolve", resolve):
+            self.assert_refused(owned)
+
+    def test_failed_removal_is_reported(self):
+        owned = Path(tempfile.mkdtemp(prefix="ffrail-"))
+        self.delete.side_effect = OSError("fixture access denied")
+        self.assertEqual(self.rail.cleanup_profile_roots([owned], self.base), 0)
+        self.assertIn("cleanup failed", self.err.getvalue())
+
+
+if __name__ == "__main__":
+    unittest.main(verbosity=2)
diff --git a/dr_ff_collect.py b/dr_ff_collect.py
index da75c9c85..916f6b6b2 100644
--- a/dr_ff_collect.py
+++ b/dr_ff_collect.py
@@ -11,15 +11,21 @@
 
 ВХОД   --rail gemini --out F [--timeout N] [--headed]
 ВЫХОД  файл --out; exit 0 · 2 нет чата · 3 текст мал
-updated: 2026-09-03
+ПРОФИЛИ  in-place источник никогда не удаляется; finally убирает только mkdtemp-корни,
+    записанные copy_profile до копирования, в том числе при сбое copy/driver.
+    Счётчик/ошибка очистки -- stderr общего cleanup_profile_roots.
+ТЕСТ  python -B _test_dr_ff_collect_cleanup.py (без браузера/сети/реального удаления).
+рельса: локальный Firefox; управление ресурсами и тесты stdlib, 0 LLM.
+updated: 2026-10-03
 """
 from __future__ import annotations
-import argparse, shutil, signal, sys, time
+import argparse, signal, sys, time
 from pathlib import Path
 
 HERE = Path(__file__).resolve().parent
 sys.path.insert(0, str(HERE))
-from dr_ff_rail import copy_profile, make_driver, wait_stable, harvest_links, RAILS  # noqa
+from dr_ff_rail import (copy_profile, cleanup_profile_roots, make_driver,
+                        wait_stable, harvest_links, RAILS)  # noqa
 
 
 def main():
@@ -70,11 +76,13 @@ def main():
             t.start()
             _alarm_timer[0] = t
 
-    _alarm(a.timeout + 120)
-
-    prof = copy_profile(a.no_copy, resolve_profile(a.profile_dir))
-    d = make_driver(prof, a.headed)
+    source = resolve_profile(a.profile_dir).resolve()
+    owned_temp_roots = []
+    d = None
     try:
+        _alarm(a.timeout + 120)
+        prof = copy_profile(a.no_copy, source, owned_temp_roots=owned_temp_roots)
+        d = make_driver(prof, a.headed)
         d.set_page_load_timeout(120)
         d.get(RAILS[a.rail][0])
         time.sleep(12)
@@ -132,14 +140,18 @@ def main():
         # патча гасила alarm в начале finally -- и процесс, честно отработавший таймаут и
         # напечатавший FAIL, повис уже в `d.quit()` на мёртвом geckodriver. Снаружи это
         # выглядит ровно как прежний вечный висяк: лог есть, вердикт есть, процесс жив.
-        _alarm(30)
         try:
-            d.quit()
-        except BaseException:
-            pass
-        _alarm(0)
-        if not a.no_copy:
-            shutil.rmtree(prof.parent, ignore_errors=True)
+            if d is not None:
+                _alarm(30)
+                try:
+                    d.quit()
+                except BaseException:
+                    pass
+        finally:
+            try:
+                _alarm(0)
+            finally:
+                cleanup_profile_roots(owned_temp_roots, source)
 
 
 if __name__ == "__main__":
diff --git a/dr_ff_rail.py b/dr_ff_rail.py
index 32efb402b..b10f685e8 100644
--- a/dr_ff_rail.py
+++ b/dr_ff_rail.py
@@ -21,14 +21,19 @@
 КТО ДЁРГАЕТ  DR-раннер узла, /dr-fanout, руками при добивке кворума
 ЧТО ЛОМАЕТСЯ
     • профиль AutoFF разлогинен -> видим страницу логина, exit 2 с адресом в сообщении
-    • профиль занят живым Firefox -> берём КОПИЮ профиля (-no-remote + свой -profile)
+    • профиль занят -> ждём замок или выходим; копия ротируемой сессии запрещена
     • вендор сменил селектор композера -> exit 2, чинить SELECTORS ниже
 КАК ПОНЯТЬ, ЧТО РАБОТАЕТ  --self-test (0 сети, 0 токенов) и размер файла --out
-updated: 2026-09-08
+ПРОФИЛИ  удаляем только корни mkdtemp, записанные текущим вызовом copy_profile;
+    in-place не передаёт владение источником. Сбой copy/driver тоже освобождает копию.
+    Отказ/ошибка очистки видны в stderr; замок определяется фактическим профилем.
+ТЕСТ  python -B _test_dr_ff_collect_cleanup.py (оффлайн, браузер/удаление подменены).
+рельса: локальный Firefox; очистка и тесты stdlib, 0 LLM.
+updated: 2026-10-03
 """
 from __future__ import annotations
 import argparse
-import os, os, shutil, subprocess, sys, tempfile, time
+import os, shutil, stat, subprocess, sys, tempfile, time
 from pathlib import Path
 
 HERE = Path(__file__).resolve().parent
@@ -166,8 +171,12 @@ def resolve_profile(name: str | None) -> Path:
     raise SystemExit(f"нет такого профиля: {name}")
 
 
-def copy_profile(no_copy: bool = True, base: Path | None = None) -> Path:
-    """Живой Firefox держит lock на профиле -> по умолчанию работаем на копии.
+def copy_profile(no_copy: bool = True, base: Path | None = None, *,
+                 owned_temp_roots: list[Path] | None = None) -> Path:
+    """По умолчанию работаем in-place; явная копия получает отдельный корень mkdtemp.
+
+    owned_temp_roots -- свежий список вызывающего кода. Записываем корень ДО copytree,
+    чтобы finally мог убрать и недокопированный профиль. Возврат base владения НЕ даёт.
 
     ⚠️ ГРАБЛЯ 02.09.2026 (замер на этом узле, заказ DR26-09-02-...-02-0343): для GOOGLE
     копия УБИВАЕТ сессию. Первый прогон на копии зашёл как Pro, Google в ходе сессии
@@ -206,10 +215,56 @@ def copy_profile(no_copy: bool = True, base: Path | None = None) -> Path:
     if no_copy:
         return base
     dst = Path(tempfile.mkdtemp(prefix="ffrail-"))
+    if owned_temp_roots is not None:
+        owned_temp_roots.append(dst)
     shutil.copytree(base, dst / "p", ignore=shutil.ignore_patterns("cache2", "startupCache", "*.lock", "lock"))
     return dst / "p"
 
 
+def cleanup_profile_roots(owned_temp_roots: list[Path], source: Path) -> int:
+    """Убрать только записанные корни mkdtemp, никогда не source или его предка.
+
+    Имя ffrail-* само по себе НЕ владение: список заполняет только copy_profile.
+    Перед rmtree проверяем прямого родителя Temp, ссылки/junction и пересечение
+    с захваченным источником. Неясная граница -> отказ в stderr, 0 удалений.
+    Возвращаем число убранных корней; ошибки удаления не маскируют исходный сбой.
+    """
+    removed = 0
+    for recorded in owned_temp_roots:
+        try:
+            root = Path(recorded)
+            temp_path = Path(tempfile.gettempdir())
+            temp = temp_path.resolve(strict=True)
+            src = Path(source).resolve()
+            if not root.is_absolute() or ".." in root.parts:
+                raise ValueError("relative/traversal path")
+            if (not root.name.startswith("ffrail-") or root.parent != temp_path
+                    or root.parent.resolve() != temp):
+                raise ValueError("not a direct ffrail-* child of Temp")
+            attrs = getattr(root.lstat(), "st_file_attributes", 0)
+            is_junction = getattr(os.path, "isjunction", lambda p: False)
+            if (root.is_symlink() or is_junction(root)
+                    or attrs & getattr(stat, "FILE_ATTRIBUTE_REPARSE_POINT", 0x400)):
+                raise ValueError("symlink/junction/reparse root")
+            actual = root.resolve(strict=True)
+            if actual != temp / root.name:
+                raise ValueError("root resolves to another location")
+            if src.is_relative_to(actual) or actual.is_relative_to(src):
+                raise ValueError("cleanup root intersects source profile")
+            if not root.is_dir():
+                raise ValueError("not a directory")
+        except (OSError, ValueError, RuntimeError) as exc:
+            print(f"[dr_ff_rail] cleanup refused: {recorded}: {exc}", file=sys.stderr)
+            continue
+        try:
+            shutil.rmtree(root)
+            removed += 1
+            print(f"[dr_ff_rail] cleanup removed owned root: {root}", file=sys.stderr)
+        except OSError as exc:
+            print(f"[dr_ff_rail] cleanup failed: {root}: {exc}", file=sys.stderr)
+    return removed
+
+
 def dismiss_overlays(driver) -> int:
     """Погасить вендорскую всплывашку, накрывшую композер.
 
@@ -819,10 +874,16 @@ def main():
     text = Path(a.prompt_file).read_text(encoding="utf-8")
 
     a.no_copy = not a.copy
-    prof = copy_profile(a.no_copy, resolve_profile(a.profile_dir))
-    _lock = profile_lock(prof) if a.no_copy else None
-    driver = make_driver(prof, a.headed)
+    source = resolve_profile(a.profile_dir).resolve()
+    owned_temp_roots = []
+    driver = None
+    _lock = None
     try:
+        prof = copy_profile(a.no_copy, source, owned_temp_roots=owned_temp_roots)
+        # copy_profile can forbid --copy for a rotating session and return source.
+        # Lock the profile actually used, independently of the requested flag.
+        _lock = profile_lock(prof) if prof.resolve() == source else None
+        driver = make_driver(prof, a.headed)
         driver.set_page_load_timeout(120)
         driver.get(url)
         time.sleep(8)
@@ -915,13 +976,17 @@ def main():
         return 0
     finally:
         try:
-            driver.quit()
-        except Exception:
-            pass
-        if _lock is not None:
-            Path(_lock).unlink(missing_ok=True)
-        if not a.no_copy and prof.parent.name.startswith("ffrail-"):
-            shutil.rmtree(prof.parent, ignore_errors=True)
+            if driver is not None:
+                try:
+                    driver.quit()
+                except Exception:
+                    pass
+        finally:
+            try:
+                if _lock is not None:
+                    Path(_lock).unlink(missing_ok=True)
+            finally:
+                cleanup_profile_roots(owned_temp_roots, source)
 
 
 if __name__ == "__main__":

--- DIFF END ---

---

**Claude:**

SUMMARY: The ownership rewrite is sound. Deletion now happens only on roots that `copy_profile` itself recorded from `mkdtemp` before `copytree`, the in-place path registers nothing, the rail lock follows the actual returned profile instead of the requested flag, and both `finally` blocks are nested so a quit failure cannot skip lock release or cleanup. I found no remaining data-loss or correctness defect; the four items below are LOW (leak surface, one dead condition, one diagnostic mislabel, one nit).

Withdrawal of the prior MED: with the actual collector handler supplied, `except (TimeoutError, KeyboardInterrupt)` touches only `e`, and `dr_ff_rail.main` has no handler at all, so widening the `try` to cover `copy_profile`/`make_driver` cannot hit an unbound `d`/`prof`/`driver`. The new tests (`test_driver_timeout_before_assignment_returns_three`, `test_copy_interrupt_before_profile_assignment_returns_three`, and the rail twins) exercise exactly that window and assert `make_driver.assert_not_called()` / `driver.quit.assert_not_called()`, which is the right shape of proof. Acceptance 1-6 and 8 hold on the code as written; acceptance 7 holds for the fixtures I can see (rmtree mocked at the production boundary, fixtures confined to a fresh `TemporaryDirectory`, and `addCleanup(self.tmp.cleanup)` registered before `addCleanup(self.stack.close)` so LIFO restores the real `rmtree` before `TemporaryDirectory._rmtree` needs it, which is easy to get wrong and is correct here).

FINDINGS:
- dr_ff_rail.py:217-219 (`copy_profile`, the new `if owned_temp_roots is not None: owned_temp_roots.append(dst)`) | low | In clone mode the kwarg is optional and defaults to `None`, so any caller that clones without passing a list silently creates a full profile copy under Temp that nothing in this process can ever reclaim. The two converted mains pass a list and `_probe_gemini_menu.py` passes in-place, so no current caller is affected, but the API now makes the leak the quiet default rather than an error. | Simplest correct fix: in the clone branch, when `owned_temp_roots is None`, print one `[dr_ff_rail] unowned clone root: {dst}` line to stderr before `copytree`, so a future caller's leak is visible instead of silent. Do not change the signature; acceptance 8 requires the existing positional contract.
- dr_ff_rail.py (`cleanup_profile_roots`, the third clause of the `not a direct ffrail-* child of Temp` condition: `or root.parent.resolve() != temp`) | low | This clause cannot change the outcome. It is only reached when `root.parent == temp_path`, and `temp` is defined as `temp_path.resolve(strict=True)`, so `root.parent.resolve()` resolves the same object and always equals `temp`. It reads as a second independent guard but adds none. | Either drop the clause, or keep it and say in the docstring that it is a deliberate redundant backstop; right now the code implies two checks where there is one. I am not asking for any of the other overlapping checks to go: `actual != temp / root.name` genuinely backstops a TOCTOU between `lstat` and `resolve`, and `not root.is_dir()` genuinely rejects a file.
- dr_ff_collect.py:79-85 (acquisition moved inside the `try`) | low | Widening the `try` makes the pre-existing handler reachable for a real operator Ctrl+C during `copytree`/`make_driver`. The handler unconditionally rewrites `KeyboardInterrupt` into `TimeoutError(f"hard timeout {a.timeout + 120}s (win-alarm)")`, so a genuine manual interrupt during profile copy will now be logged as a Windows watchdog timeout that never fired. The patch's own test `test_copy_interrupt_before_profile_assignment_returns_three` asserts `"win-alarm"` is in stderr, i.e. it pins the mislabel. In a file whose comments record an earlier investigation misled by exactly this kind of log, that matters. | Set a flag when the Windows timer callback actually runs (`_alarm_timer` already holds the Timer) and only rewrite the message when that flag is set; otherwise print `FAIL: interrupted`. Then change that test's assertion to the honest string.
- dr_ff_rail.py (`cleanup_profile_roots` loop body) | low | `temp_path`, `temp` and `src` are recomputed inside the per-root loop, and the list is not drained after a successful `rmtree`, so a second call on the same list would print a spurious `cleanup refused` (strict resolve fails on the removed dir). Neither bites today: both callers pass a one-element list and call the helper exactly once from `finally`. | Hoist the three path computations above the loop, and `owned_temp_roots.clear()`-equivalent by appending removed roots to a local and removing them, if and only if you expect a second consumer. Otherwise leave it and note "single call per process" in the docstring.

Claims I could not verify from the supplied diff, flagged rather than assumed either way: that `dr_ff_collect.py` has no other `shutil.` reference after the import was dropped (a surviving reference would be a `NameError` on a path the 39 tests may not reach), and that nothing else in either `main` reads `a.no_copy` or `prof` outside the `try`. Both are stated in the context inventory; the diff alone does not show them. Also, as the brief requires: 39/39 green here is evidence about ownership logic only, not about the next-morning Google/Firefox session outcome and not about fleet coverage of the unmodified `D:/Vault/_imports` copies.

===VERDICT=== APPROVE
