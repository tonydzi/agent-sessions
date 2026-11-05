---
session: s_9ec139e3
date: 2026-09-22
words: 6813
turns: 1
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are the independent adversarial reviewer. Read only the exact git diff pasted below. D…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9ec139e3` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are the independent adversarial reviewer. Read only the exact git diff pasted below. Do not edit files and do not run tools. The artifact migrates a node-local SQLite workclaim authority from legacy paths to a stable non-virtualized path. Acceptance is fail-closed: exactly one writable authority per node; distinct physical SQLite files must never be treated as one authority merely because contents match; after cutover every legacy route must refuse SQLite create/write while a rollback snapshot remains recoverable elsewhere; missing/corrupt/ambiguous sources block; active claims/consumers block; rollback remains reversible; no shared SQLite across machines; deploy evidence must bind every delivered file SHA and successful deploy_apply/store-health. Examine especially: identical physical sources, source_left_untouched, imported-provider consumers invisible in argv, exact verify semantics, races/TOCTOU, Windows and POSIX behavior, rollback. Report findings ordered P0/P1/P2 with exact file and line. Final line must be exactly `VERDICT: APPROVE` or `VERDICT: REQUEST_CHANGES`.

EXACT DIFF d1f268acb..HEAD, only these files:
diff --git a/.gitattributes b/.gitattributes
index 4b16554d3..8050beca2 100644
--- a/.gitattributes
+++ b/.gitattributes
@@ -1,5 +1,7 @@
 /_shared/workclaim.py text eol=lf
 /_shared/_test_workclaim.py text eol=lf
 /_shared/_test_workclaim_store_durability.py text eol=lf
 /_shared/_test_workclaim_toctou.py text eol=lf
 /retro_lost_scan.py text eol=lf
+/workclaim_store_cutover.py text eol=lf
+/_test_workclaim_store_cutover.py text eol=lf
diff --git a/_shared/_test_workclaim_toctou.py b/_shared/_test_workclaim_toctou.py
index 4fbc8f34d..d8ee79e69 100644
--- a/_shared/_test_workclaim_toctou.py
+++ b/_shared/_test_workclaim_toctou.py
@@ -26,160 +26,162 @@ MUTATIONS THIS TEST MUST KILL (source edit -> named case):
 - accept a missing/wrong retro question-id -> ``MUTANT_retro_mark_done_question_*``
 - permit non-atomic retro reopen -> ``MUTANT_retro_force_forbidden``
 - resurrect a released SHA1-era file claim -> ``MUTANT_legacy_import_fingerprint_fence``
 - reduce legacy history to last-value/source-path state -> ``MUTANT_legacy_import_*``
 - overwrite the only legacy source before SQLite COMMIT -> ``MUTANT_legacy_import_crash_mirror``
 - let expired SQLite state mask a live SHA1-era owner -> ``MUTANT_live_legacy_fences_expired_sqlite_takeover``
 - trust colliding SHA1 filenames without embedded identity -> ``MUTANT_legacy_embedded_identity``
 - ignore triggers outside question tables -> ``MUTANT_question_cross_table_trigger``
 - skip migration of an exact proven Git identity -> ``MUTANT_question_v2_identity_remap``
 - accept a legacy path identity without Git provenance -> ``MUTANT_question_legacy_path_provenance``
 - skip current-version path-to-Git drift validation -> ``MUTANT_question_current_identity_validation``
 - silently collapse two old aliases during identity migration -> ``MUTANT_question_identity_collision``
 - reset the global epoch after the final question file releases -> ``MUTANT_question_epoch_full_release``
 - omit the migrated v2 epoch floor -> ``MUTANT_question_identity_epoch_floor``
 - map JSON question-busy to a non-busy exit code -> ``MUTANT_question_busy_json_rc``
 - import a legacy file before honoring completion -> ``MUTANT_completion_before_legacy``
 - accept two simultaneous owners for one question -> ``MUTANT_question_simultaneous_owner_lookup``
 - migrate identity after its worktree provenance disappeared -> ``MUTANT_question_removed_worktree_guard``
 - reject an absent leaf despite an exact live Git identity -> ``MUTANT_question_missing_git_leaf_rejected``
 - accept a last-value ``legacy_import_seen`` schema -> ``MUTANT_legacy_import_schema``
 - publish a question mirror before authority commits -> ``MUTANT_question_mirror_precommit``
 - let a delayed old mirror overwrite a newer epoch -> ``MUTANT_question_mirror_epoch_guard``
 - split mirror comparison from removal -> ``MUTANT_mirror_remove_without_gate``
 - coerce generic bool/float/string epochs -> ``MUTANT_generic_epoch_coercion``
 - coerce question bool/float/string epochs -> ``MUTANT_question_epoch_coercion``
 - report release success without deleting the exact file mapping -> ``MUTANT_question_release_noop``
 - report live renewal without persisting its heartbeat/TTL -> ``MUTANT_question_renew_noop``
 - normalize a retro receipt's exact question id -> ``MUTANT_retro_mark_done_question_normalization``
 - remove the frozen ``complete_question`` API name -> ``MUTANT_complete_question_compatibility``
 - remove one of the four LF checkout rules -> ``MUTANT_missing_eol_attribute``
 - trust a logical identity resolved before the DB gate -> ``MUTANT_question_locked_identity_recheck``
 - drop canonical uniqueness during that namespace race -> ``MUTANT_question_canonical_uniqueness``
 - leave an upgraded schema without canonical uniqueness -> ``MUTANT_question_canonical_index_contract``
 - split consumer check from DONE write -> ``rejected_retro_check_write_gap``
 - stat/remove a stale lockfile without a token -> ``rev2_stale_lock_double_winner``
 
 Normal mode tests the current source. ``--red-evidence --report ABSOLUTE.json``
 is the single mutation command: it proves named failures on rejected SHA
 69D0.../rev2 and the generated copies. It never mutates live/worktree files,
 deletes its temp lab, and atomically checkpoints a report outside that lab.
 """
 
 import argparse
 import hashlib
 import io
 import json
 import os
 import signal
 import sqlite3
 import subprocess
 import sys
 import tempfile
 import threading
 import time
 import traceback
 import types
 from contextlib import redirect_stderr, redirect_stdout
 from pathlib import Path
 
 
 # These tests repeatedly materialise same-sized mutant modules within one
 # filesystem timestamp tick.  Never let CPython serve an earlier candidate's
 # bytecode to a later child or in-process loader.
 sys.dont_write_bytecode = True
 for _stream in (sys.stdout, sys.stderr):
     if hasattr(_stream, "reconfigure"):
         _stream.reconfigure(encoding="utf-8")
 
 
 HERE = Path(__file__).resolve().parent
 ROOT = HERE.parent
 SOURCE = HERE / "workclaim.py"
 RETRO = ROOT / "retro_lost_scan.py"
 ATTRIBUTES = ROOT / ".gitattributes"
 PORTABLE_PATHS = (
     "_shared/workclaim.py",
     "_shared/_test_workclaim.py",
     "_shared/_test_workclaim_store_durability.py",
     "_shared/_test_workclaim_toctou.py",
     "retro_lost_scan.py",
+    "workclaim_store_cutover.py",
+    "_test_workclaim_store_cutover.py",
 )
 EXPECTED_LF_ATTRIBUTES = tuple(
     "/%s text eol=lf" % path for path in PORTABLE_PATHS)
 REJECTED_COMMIT = "bb67acd44"
 REV2_COMMIT = "91287a2ca"
 REJECTED_SHA256 = "69D0B8188FF60A8744AE84284ABA9877B8C96CCEA4B0D64C0CDA8C89D96A0478"
 CANDIDATE_WORKCLAIM_SHA256 = "F30387FE35A97331B47104D46B626B6881998700A3CAF660D2D5922FDBAC7241"
 CANDIDATE_RETRO_SHA256 = "99B154B00F56A2DC937D5CE54D7A5CBEFBA4BE812923341D06B3E3AB0CBFC270"
 TOTAL = 0
 FAILS = []
 HARNESS_FAILURES = []
 CHECK_RECORDS = []
 MUTATION_RECORDS = []
 DURABLE_REPORT_PATH = None
 RUN_STARTED_TS = None
 RUN_MODE = None
 FATAL_ERROR = None
 
 
 def child_env():
     env = os.environ.copy()
     env["PYTHONDONTWRITEBYTECODE"] = "1"
     return env
 
 
 def _captured_text(value):
     if value is None:
         return ""
     if isinstance(value, bytes):
         return value.decode("utf-8", errors="replace")
     return str(value)
 
 
 def _terminate_process_tree(process):
     """Best-effort bounded tree teardown; its result is evidence, not a kill."""
     notes = []
     if process.poll() is not None:
         return True, "already-exited"
     if os.name == "nt":
         try:
             killed = subprocess.run(
                 ["taskkill", "/PID", str(process.pid), "/T", "/F"],
                 text=True, capture_output=True, timeout=10)
             notes.append("taskkill_rc=%r out=%r err=%r" %
                          (killed.returncode, killed.stdout, killed.stderr))
         except (OSError, subprocess.TimeoutExpired) as exc:
             notes.append("taskkill=%r" % exc)
     else:
         try:
             os.killpg(process.pid, signal.SIGKILL)
             notes.append("killpg=ok")
         except ProcessLookupError:
             notes.append("killpg=already-exited")
         except OSError as exc:
             notes.append("killpg=%r" % exc)
     try:
         process.wait(timeout=10)
     except subprocess.TimeoutExpired:
         process.kill()
         notes.append("top-process-kill=fallback")
         try:
             process.wait(timeout=5)
         except subprocess.TimeoutExpired:
             notes.append("top-process-still-live")
     return process.poll() is not None, "; ".join(notes)
 
 
 def run_captured(argv, timeout, env=None):
     """Run one bounded process group and turn timeout into data, never RED."""
     kwargs = {
         "text": True,
         "stdout": subprocess.PIPE,
         "stderr": subprocess.PIPE,
         "env": env,
     }
     if os.name == "nt":
         kwargs["creationflags"] = getattr(
             subprocess, "CREATE_NEW_PROCESS_GROUP", 0)
     else:
         kwargs["start_new_session"] = True
diff --git a/_test_workclaim_store_cutover.py b/_test_workclaim_store_cutover.py
new file mode 100644
index id_c9083e08..a7874b5f0
--- /dev/null
+++ b/_test_workclaim_store_cutover.py
@@ -0,0 +1,531 @@
+# -*- coding: utf-8 -*-
+"""Hermetic acceptance + mutation grid for workclaim_store_cutover.py.
+
+Every apply/verify/rollback uses an isolated HOME, scripts pair, bus, usage
+ledger, and SQLite DB. The live provider/scanner/store bytes are snapshotted
+around the full run. rail: local CPython stdlib; zero LLM/network tokens.
+"""
+
+from __future__ import print_function
+
+import hashlib
+import io
+import json
+import os
+import shutil
+import sqlite3
+import subprocess
+import sys
+import tempfile
+from pathlib import Path
+
+
+ROOT = Path(__file__).resolve().parent
+TOOL = ROOT / "workclaim_store_cutover.py"
+PROVIDER = ROOT / "_shared" / "workclaim.py"
+SCANNER = ROOT / "retro_lost_scan.py"
+EXPECTED_PROVIDER = "F30387FE35A97331B47104D46B626B6881998700A3CAF660D2D5922FDBAC7241"
+EXPECTED_SCANNER = "99B154B00F56A2DC937D5CE54D7A5CBEFBA4BE812923341D06B3E3AB0CBFC270"
+TOTAL = 0
+FAILURES = []
+
+
+def check(name, condition, detail=""):
+    global TOTAL
+    TOTAL += 1
+    if condition:
+        print("PASS", name)
+    else:
+        print("FAIL", name, detail)
+        FAILURES.append(name)
+
+
+def sha(path):
+    digest = hashlib.sha256()
+    with io.open(str(path), "rb") as stream:
+        for chunk in iter(lambda: stream.read(1024 * 1024), b""):
+            digest.update(chunk)
+    return digest.hexdigest().upper()
+
+
+def file_state(path):
+    path = Path(path)
+    if not path.exists():
+        return None
+    stat = path.stat()
+    return {"size": stat.st_size, "sha256": sha(path),
+            "mtime_ns": getattr(stat, "st_mtime_ns", int(stat.st_mtime * 1e9))}
+
+
+def production_snapshot():
+    target = Path.home() / ".claude" / "state" / "workclaim" / "workclaim.sqlite3"
+    local = Path(os.environ.get("LOCALAPPDATA") or (Path.home() / ".claude"))
+    legacy = local / "AntonAgents" / "workclaim" / "workclaim.sqlite3"
+    paths = [PROVIDER, SCANNER, TOOL, target, Path(str(target) + "-wal"),
+             Path(str(target) + "-shm"), legacy, Path(str(legacy) + "-wal"),
+             Path(str(legacy) + "-shm")]
+    return {str(path): file_state(path) for path in paths}
+
+
+def parse_payload(result):
+    lines = [line for line in (result.stdout or "").splitlines() if line.strip()]
+    if not lines:
+        return None
+    try:
+        return json.loads(lines[-1])
+    except Exception:
+        return None
+
+
+def replace_once(text, old, new, label):
+    count = text.count(old)
+    if count != 1:
+        raise AssertionError("%s needle count=%d" % (label, count))
+    return text.replace(old, new, 1)
+
+
+class Lab(object):
+    def __init__(self, base, tool_text=None):
+        self.base = Path(base)
+        self.home = self.base / "home"
+        self.scripts = self.home / ".claude" / "scripts"
+        self.provider = self.scripts / "_shared" / "workclaim.py"
+        self.scanner = self.scripts / "retro_lost_scan.py"
+        self.tool = self.scripts / "workclaim_store_cutover.py"
+        self.bus = self.base / "bus"
+        self.local = self.base / "local"
+        self.target = self.home / ".claude" / "state" / "workclaim" / "workclaim.sqlite3"
+        self.legacy = self.local / "AntonAgents" / "workclaim" / "workclaim.sqlite3"
+        self.provider.parent.mkdir(parents=True)
+        self.bus.mkdir(parents=True)
+        self.local.mkdir(parents=True)
+        shutil.copy2(str(PROVIDER), str(self.provider))
+        shutil.copy2(str(SCANNER), str(self.scanner))
+        self.tool.write_text(tool_text if tool_text is not None else
+                             TOOL.read_text(encoding="utf-8-sig"), encoding="utf-8")
+        self.env = os.environ.copy()
+        self.env.update({
+            "HOME": str(self.home), "USERPROFILE": str(self.home),
+            "LOCALAPPDATA": str(self.local), "MACHINE_BUS_DIR": str(self.bus),
+            "WORKCLAIM_SCRIPTS_ROOT": str(self.scripts),
+            "WORKCLAIM_CUTOVER_USAGE": str(self.base / "usage.jsonl"),
+            "WORKCLAIM_USAGE": str(self.base / "provider-usage.jsonl"),
+            "CLAUDE_OPERATOR": "robot:cutover-test",
+        })
+        self.env.pop("WORKCLAIM_DB", None)
+        self.env.pop("WORKCLAIM_MUTEX_DB", None)
+
+    def run(self, *args, env=None):
+        merged = self.env.copy()
+        if env:
+            merged.update(env)
+        return subprocess.run([sys.executable, "-B", str(self.tool)] + list(args),
+                              env=merged, text=True, capture_output=True, timeout=90)
+
+    def source_env(self, source):
+        env = self.env.copy()
+        env["WORKCLAIM_DB"] = str(source)
+        return env
+
+    def seed(self, source=None, unit="u1", active=False):
+        source = Path(source or self.legacy)
+        source.parent.mkdir(parents=True, exist_ok=True)
+        code = (
+            "import importlib.util,sys;"
+            "s=importlib.util.spec_from_file_location('seed_wc',sys.argv[1]);"
+            "m=importlib.util.module_from_spec(s);s.loader.exec_module(m);"
+            "r=m.claim('cutover-test',sys.argv[2],'TEST-HOLDER',ttl_sec=3600);"
+            "assert r.ok,r;"
+            "active=(sys.argv[3]=='1');"
+            "assert active or m.complete('cutover-test',sys.argv[2],'TEST-HOLDER',r.epoch,lambda meta:None);"
+            "print(r.epoch)"
+        )
+        result = subprocess.run(
+            [sys.executable, "-B", "-c", code, str(self.provider), unit,
+             "1" if active else "0"], env=self.source_env(source),
+            text=True, capture_output=True, timeout=60)
+        if result.returncode != 0:
+            raise AssertionError("seed failed rc=%s out=%r err=%r" %
+                                 (result.returncode, result.stdout, result.stderr))
+        return source
+
+    def mirror(self, epoch):
+        path = self.bus / "_claims" / "test" / "unit.claim"
+        path.parent.mkdir(parents=True, exist_ok=True)
+        path.write_text(json.dumps({"epoch": epoch, "holder": "SURVIVOR"}),
+                        encoding="utf-8")
+        return path
+
+    def receipt(self, deploy_id):
+        return self.target.parent / "cutover-receipts" / (deploy_id + ".json")
+
+
+def with_lab(callback, tool_text=None):
+    with tempfile.TemporaryDirectory(prefix="workclaim-cutover-test-") as tmp:
+        return callback(Lab(tmp, tool_text))
+
+
+def inventory_case(lab):
+    before = sorted((str(path.relative_to(lab.base)), sha(path))
+                    for path in lab.base.rglob("*") if path.is_file())
+    result = lab.run("inventory")
+    payload = parse_payload(result)
+    after = sorted((str(path.relative_to(lab.base)), sha(path))
+                   for path in lab.base.rglob("*")
+                   if path.is_file() and path.name != "usage.jsonl")
+    before_no_usage = [item for item in before if item[0] != "usage.jsonl"]
+    ok = bool(result.returncode == 0 and payload and payload.get("ok")
+              and payload["code_pair"]["provider_sha256"] == EXPECTED_PROVIDER
+              and payload["code_pair"]["scanner_sha256"] == EXPECTED_SCANNER
+              and not lab.target.exists() and before_no_usage == after)
+    return ok, {"rc": result.returncode, "payload": payload,
+                "stderr": result.stderr, "unchanged": before_no_usage == after}
+
+
+def missing_source_case(lab):
+    result = lab.run("apply", "--deploy-id", "missing-source")
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == "legacy-source-missing" and
+                not lab.target.exists() and not lab.receipt("missing-source").exists()), payload
+
+
+def empty_seed_case(lab, deploy_id="empty-seed"):
+    lab.mirror(7)
+    result = lab.run("apply", "--deploy-id", deploy_id, "--allow-empty-seed")
+    payload = parse_payload(result)
+    receipt_path = lab.receipt(deploy_id)
+    receipt = json.loads(receipt_path.read_text(encoding="utf-8")) if receipt_path.is_file() else None
+    verify = lab.run("verify", "--deploy-id", deploy_id)
+    verify_payload = parse_payload(verify)
+    ok = bool(result.returncode == 0 and payload and payload.get("ok")
+              and payload.get("source_kind") == "explicit-empty-seed"
+              and payload["snapshot"]["global_epoch"] > 7
+              and receipt and receipt.get("status") == "committed"
+              and receipt.get("source") is None
+              and receipt["mirrors"]["max_epoch"] == 7
+              and verify.returncode == 0 and verify_payload and verify_payload.get("ok"))
+    return ok, {"apply_rc": result.returncode, "apply": payload,
+                "verify_rc": verify.returncode, "verify": verify_payload,
+                "apply_err": result.stderr, "verify_err": verify.stderr}
+
+
+def source_migration_case(lab, deploy_id="source-migration", wal=False,
+                          duplicate=False):
+    source = lab.seed()
+    if wal:
+        con = sqlite3.connect(str(source))
+        try:
+            con.execute("PRAGMA journal_mode=WAL")
+            con.execute("UPDATE epochs SET last_epoch=last_epoch")
+            con.commit()
+        finally:
+            con.close()
+    before_sha = sha(source)
+    before_size = source.stat().st_size
+    extra = []
+    if duplicate:
+        twin = lab.base / "identical.sqlite3"
+        src = sqlite3.connect(str(source))
+        dst = sqlite3.connect(str(twin))
+        try:
+            src.backup(dst)
+            dst.commit()
+        finally:
+            src.close()
+            dst.close()
+        extra = ["--legacy-db", str(twin)]
+    result = lab.run(*((extra or []) + ["apply", "--deploy-id", deploy_id]))
+    payload = parse_payload(result)
+    verify = lab.run("verify", "--deploy-id", deploy_id)
+    verify_payload = parse_payload(verify)
+    receipt = (json.loads(lab.receipt(deploy_id).read_text(encoding="utf-8"))
+               if lab.receipt(deploy_id).is_file() else None)
+    ok = bool(result.returncode == 0 and payload and payload.get("ok")
+              and payload.get("source") == str(source)
+              and source.is_file() and source.stat().st_size == before_size
+              and sha(source) == before_sha and receipt
+              and Path(receipt["rollback_snapshot"]).is_file()
+              and payload["snapshot"]["counts"]["completions"] == 1
+              and verify.returncode == 0 and verify_payload and verify_payload.get("ok"))
+    return ok, {"apply_rc": result.returncode, "apply": payload,
+                "verify_rc": verify.returncode, "verify": verify_payload,
+                "source_unchanged": source.is_file() and sha(source) == before_sha,
+                "stderr": result.stderr}
+
+
+def divergent_case(lab):
+    lab.seed(lab.legacy, "one")
+    other = lab.base / "other.sqlite3"
+    lab.seed(other, "two")
+    result = lab.run("--legacy-db", str(other), "apply", "--deploy-id", "divergent")
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == "legacy-sources-diverge" and
+                not lab.target.exists()), payload
+
+
+def live_claim_case(lab):
+    lab.seed(active=True)
+    result = lab.run("apply", "--deploy-id", "live-claim")
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == "live-authority-claim" and
+                not lab.target.exists()), payload
+
+
+def active_process_case(lab):
+    env = {"WORKCLAIM_CUTOVER_TEST_MODE": "1",
+           "WORKCLAIM_CUTOVER_TEST_PROCESS_LIST":
+               "python /tmp/.claude/scripts/retro_lost_scan.py list"}
+    result = lab.run("apply", "--deploy-id", "active-process",
+                     "--allow-empty-seed", env=env)
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == "active-consumer-process" and
+                not lab.target.exists()), payload
+
+
+def code_hash_case(lab, which):
+    path = lab.provider if which == "provider" else lab.scanner
+    with io.open(str(path), "a", encoding="utf-8") as stream:
+        stream.write("\n# drift\n")
+    result = lab.run("apply", "--deploy-id", which + "-drift", "--allow-empty-seed")
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == which + "-hash" and
+                not lab.target.exists()), payload
+
+
+def partial_target_case(lab):
+    lab.target.parent.mkdir(parents=True, exist_ok=True)
+    lab.target.write_bytes(b"")
+    before = file_state(lab.target)
+    result = lab.run("apply", "--deploy-id", "partial", "--allow-empty-seed")
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == "target-without-receipt" and
+                file_state(lab.target) == before), payload
+
+
+def idempotent_case(lab):
+    first = lab.run("apply", "--deploy-id", "idempotent", "--allow-empty-seed")
+    snapshot = file_state(lab.target)
+    second = lab.run("apply", "--deploy-id", "idempotent", "--allow-empty-seed")
+    payload = parse_payload(second)
+    return bool(first.returncode == 0 and second.returncode == 0 and payload and
+                payload.get("ok") and payload.get("command") == "verify" and
+                file_state(lab.target) == snapshot), payload
+
+
+def verify_drift_case(lab):
+    applied = lab.run("apply", "--deploy-id", "verify-drift", "--allow-empty-seed")
+    if applied.returncode != 0:
+        return False, {"apply": parse_payload(applied)}
+    con = sqlite3.connect(str(lab.target))
+    try:
+        con.execute("UPDATE epochs SET last_epoch=last_epoch+1 WHERE k='__global_epoch__'")
+        con.commit()
+    finally:
+        con.close()
+    verify = lab.run("verify", "--deploy-id", "verify-drift")
+    payload = parse_payload(verify)
+    return bool(verify.returncode == 4 and payload and
+                payload.get("reason") == "target-drift"), payload
+
+
+def source_drift_case(lab):
+    source = lab.seed()
+    applied = lab.run("apply", "--deploy-id", "source-drift")
+    if applied.returncode != 0:
+        return False, {"apply": parse_payload(applied)}
+    con = sqlite3.connect(str(source))
+    try:
+        con.execute("UPDATE epochs SET last_epoch=last_epoch+1 WHERE k='__global_epoch__'")
+        con.commit()
+    finally:
+        con.close()
+    verify = lab.run("verify", "--deploy-id", "source-drift")
+    payload = parse_payload(verify)
+    return bool(verify.returncode == 4 and payload and
+                payload.get("reason") == "legacy-source-drift"), payload
+
+
+def rollback_case(lab):
+    applied = lab.run("apply", "--deploy-id", "rollback", "--allow-empty-seed")
+    if applied.returncode != 0:
+        return False, {"apply": parse_payload(applied)}
+    rolled = lab.run("rollback", "--deploy-id", "rollback")
+    payload = parse_payload(rolled)
+    parked = lab.target.parent / "rollback" / "rollback" / "post-cutover.sqlite3"
+    return bool(rolled.returncode == 0 and payload and payload.get("ok")
+                and not lab.target.exists() and parked.is_file()
+                and payload.get("status") == "rolled-back-store-only"), payload
+
+
+def rollback_drift_case(lab):
+    applied = lab.run("apply", "--deploy-id", "rollback-drift", "--allow-empty-seed")
+    if applied.returncode != 0:
+        return False, {"apply": parse_payload(applied)}
+    con = sqlite3.connect(str(lab.target))
+    try:
+        con.execute("UPDATE epochs SET last_epoch=last_epoch+1 WHERE k='__global_epoch__'")
+        con.commit()
+    finally:
+        con.close()
+    rolled = lab.run("rollback", "--deploy-id", "rollback-drift")
+    payload = parse_payload(rolled)
+    return bool(rolled.returncode == 4 and payload and
+                payload.get("reason") == "rollback-after-state-drift" and
+                lab.target.is_file()), payload
+
+
+def env_override_case(lab):
+    result = lab.run("apply", "--deploy-id", "env-override", "--allow-empty-seed",
+                     env={"WORKCLAIM_DB": str(lab.base / "wrong.sqlite3")})
+    payload = parse_payload(result)
+    return bool(result.returncode == 4 and payload and
+                payload.get("reason") == "authority-env-override" and
+                not lab.target.exists()), payload
+
+
+def mutation_checks(tool_text):
+    results = []
+    old = (
+        "    code = assert_code_pair(args.scripts_root, args.expected_provider_sha,\n"
+        "                            args.expected_scanner_sha)\n"
+        "    consumers = active_consumers()"
+    )
+    new = (
+        "    code = {'provider_sha256': args.expected_provider_sha.upper(),\n"
+        "            'scanner_sha256': args.expected_scanner_sha.upper()}\n"
+        "    consumers = active_consumers()"
+    )
+    mutant = replace_once(tool_text, old, new, "code_pair_gate")
+    def code_mutant(lab):
+        lab.provider.write_text(lab.provider.read_text(encoding="utf-8") + "\n# drift\n",
+                                encoding="utf-8")
+        result = lab.run("apply", "--deploy-id", "m-code", "--allow-empty-seed")
+        return result.returncode != 4 or (parse_payload(result) or {}).get("reason") != "provider-hash"
+    results.append(("MUTANT_code_pair_gate", with_lab(code_mutant, mutant)))
+
+    mutant = replace_once(tool_text,
+        "        if not sources and not args.allow_empty_seed:\n",
+        "        if False and not sources and not args.allow_empty_seed:\n",
+        "missing_source_gate")
+    def missing_mutant(lab):
+        result = lab.run("apply", "--deploy-id", "m-missing")
+        return result.returncode == 0 and lab.target.is_file()
+    results.append(("MUTANT_missing_source_gate", with_lab(missing_mutant, mutant)))
+
+    mutant = replace_once(tool_text,
+        "    if consumers:\n        raise CutoverError(\"active-consumer-process\", consumers)\n    provider, _scanner = provider_paths(args.scripts_root)",
+        "    if False and consumers:\n        raise CutoverError(\"active-consumer-process\", consumers)\n    provider, _scanner = provider_paths(args.scripts_root)",
+        "process_guard")
+    def process_mutant(lab):
+        env = {"WORKCLAIM_CUTOVER_TEST_MODE": "1",
+               "WORKCLAIM_CUTOVER_TEST_PROCESS_LIST":
+                   "python /tmp/.claude/scripts/retro_lost_scan.py list"}
+        result = lab.run("apply", "--deploy-id", "m-process", "--allow-empty-seed", env=env)
+        return result.returncode == 0 and lab.target.is_file()
+    results.append(("MUTANT_process_guard", with_lab(process_mutant, mutant)))
+
+    mutant = replace_once(tool_text,
+        "    if target.exists():\n        raise CutoverError(\"target-without-receipt\", {\"path\": str(target)})",
+        "    if False and target.exists():\n        raise CutoverError(\"target-without-receipt\", {\"path\": str(target)})",
+        "target_guard")
+    def target_mutant(lab):
+        lab.target.parent.mkdir(parents=True, exist_ok=True)
+        lab.target.write_bytes(b"")
+        result = lab.run("apply", "--deploy-id", "m-target", "--allow-empty-seed")
+        return result.returncode != 4 or (parse_payload(result) or {}).get("reason") != "target-without-receipt"
+    results.append(("MUTANT_target_guard", with_lab(target_mutant, mutant)))
+
+    mutant = replace_once(tool_text,
+        "            epoch_before, epoch_after = raise_epoch_floor(stage, mirror[\"max_epoch\"])",
+        "            epoch_before = staged_before[\"global_epoch\"]; epoch_after = epoch_before",
+        "epoch_fence")
+    mutant = replace_once(mutant,
+        "            if staged_after[\"global_epoch\"] <= mirror[\"max_epoch\"]:",
+        "            if False and staged_after[\"global_epoch\"] <= mirror[\"max_epoch\"]:",
+        "epoch_fence_selfcheck")
+    def epoch_mutant(lab):
+        lab.mirror(7)
+        result = lab.run("apply", "--deploy-id", "m-epoch", "--allow-empty-seed")
+        payload = parse_payload(result) or {}
+        return result.returncode == 0 and payload.get("snapshot", {}).get("global_epoch", 0) <= 7
+    results.append(("MUTANT_epoch_fence", with_lab(epoch_mutant, mutant)))
+
+    mutant = replace_once(tool_text,
+        "    if snapshot[\"digest\"] != baseline[\"digest\"]:\n",
+        "    if False and snapshot[\"digest\"] != baseline[\"digest\"]:\n",
+        "verify_digest")
+    def verify_mutant(lab):
+        applied = lab.run("apply", "--deploy-id", "m-verify", "--allow-empty-seed")
+        if applied.returncode != 0:
+            return False
+        con = sqlite3.connect(str(lab.target))
+        try:
+            con.execute("UPDATE epochs SET last_epoch=last_epoch+1 WHERE k='__global_epoch__'")
+            con.commit()
+        finally:
+            con.close()
+        result = lab.run("verify", "--deploy-id", "m-verify")
+        return result.returncode == 0
+    results.append(("MUTANT_verify_digest", with_lab(verify_mutant, mutant)))
+    return results
+
+
+def main():
+    before = production_snapshot()
+    check("source_hashes_pinned", sha(PROVIDER) == EXPECTED_PROVIDER and
+          sha(SCANNER) == EXPECTED_SCANNER,
+          "provider=%s scanner=%s" % (sha(PROVIDER), sha(SCANNER)))
+    cases = [
+        ("inventory_is_read_only", inventory_case),
+        ("missing_source_fails_closed", missing_source_case),
+        ("explicit_empty_seed_fences_mirror", empty_seed_case),
+        ("single_source_preserved", source_migration_case),
+        ("wal_source_preserved", lambda lab: source_migration_case(lab, "wal-source", wal=True)),
+        ("identical_aliases_are_one_authority", lambda lab: source_migration_case(lab, "identical-alias", duplicate=True)),
+        ("divergent_sources_block", divergent_case),
+        ("live_claim_blocks", live_claim_case),
+        ("active_consumer_process_blocks", active_process_case),
+        ("provider_hash_mismatch_blocks", lambda lab: code_hash_case(lab, "provider")),
+        ("scanner_hash_mismatch_blocks", lambda lab: code_hash_case(lab, "scanner")),
+        ("partial_target_not_overwritten", partial_target_case),
+        ("apply_is_idempotent_via_receipt", idempotent_case),
+        ("verify_detects_target_drift", verify_drift_case),
+        ("verify_detects_legacy_source_drift", source_drift_case),
+        ("rollback_parks_unchanged_target", rollback_case),
+        ("rollback_refuses_advanced_state", rollback_drift_case),
+        ("authority_env_override_blocks", env_override_case),
+    ]
+    for name, callback in cases:
+        ok, detail = with_lab(callback)
+        check(name, ok, repr(detail))
+
+    tool_text = TOOL.read_text(encoding="utf-8-sig")
+    try:
+        mutations = mutation_checks(tool_text)
+    except Exception as exc:
+        check("mutation_needles_present", False, repr(exc))
+        mutations = []
+    else:
+        check("mutation_needles_present", True)
+    for name, killed in mutations:
+        check(name, killed, "mutant survived")
+
+    after = production_snapshot()
+    check("production_snapshot_unchanged", before == after,
+          "before=%r after=%r" % (before, after))
+    if FAILURES:
+        print("FAILURES", json.dumps(FAILURES, ensure_ascii=False))
+        print("RESULT %d/%d passed" % (TOTAL - len(FAILURES), TOTAL))
+        return 1
+    print("RESULT %d/%d passed" % (TOTAL, TOTAL))
+    return 0
+
+
+if __name__ == "__main__":
+    raise SystemExit(main())
diff --git a/workclaim_store_cutover.py b/workclaim_store_cutover.py
new file mode 100644
index id_c9083e08..ea5103371
--- /dev/null
+++ b/workclaim_store_cutover.py
@@ -0,0 +1,858 @@
+# -*- coding: utf-8 -*-
+"""Fail-closed, node-local cutover for the workclaim SQLite authority.
+
+What: inventory, migrate/bootstrap, verify, and reversibly park one node's
+``~/.claude/state/workclaim/workclaim.sqlite3`` authority.
+Input: the already-installed exact provider/scanner pair plus an optional
+legacy node-local SQLite source. Output: an atomic target DB, rollback snapshot,
+and a durable JSON receipt. Caller: an explicit per-node deployment step.
+Breaks: stale code, ambiguous sources, live consumers/claims, corrupt schemas,
+or missing explicit consent for an empty seed all stop with rc=4 before switch.
+Fix: inspect the JSON reason, drain the named consumer, or resolve the named DB;
+never merge SQLite files and never sync the target DB between nodes.
+
+rail: local CPython stdlib + an already-paid fleet transport; zero LLM/API calls.
+"""
+
+from __future__ import print_function
+
+import argparse
+import contextlib
+import datetime
+import glob
+import hashlib
+import io
+import json
+import os
+import re
+import socket
+import sqlite3
+import subprocess
+import sys
+import tempfile
+import time
+from pathlib import Path
+
+
+EXPECTED_PROVIDER_SHA = "F30387FE35A97331B47104D46B626B6881998700A3CAF660D2D5922FDBAC7241"
+EXPECTED_SCANNER_SHA = "99B154B00F56A2DC937D5CE54D7A5CBEFBA4BE812923341D06B3E3AB0CBFC270"
+EXPECTED_TABLES = (
+    "claims", "completions", "epochs", "legacy_import_seen",
+    "question_claims", "question_meta", "question_owners", "transitions",
+)
+GLOBAL_EPOCH_KEY = "__global_epoch__"
+DEPLOY_ID_RE = re.compile(r"^[A-Za-z0-9][A-Za-z0-9._-]{0,119}$")
+
+
+class CutoverError(RuntimeError):
+    """An expected safety stop that must be returned as structured RED."""
+
+    def __init__(self, reason, detail=None):
+        RuntimeError.__init__(self, str(reason))
+        self.reason = str(reason)
+        self.detail = detail
+
+
+def utc_now():
+    return datetime.datetime.now(datetime.timezone.utc).strftime("%Y-%m-%dT%H:%M:%SZ")
+
+
+def node_name():
+    return os.environ.get("COMPUTERNAME") or socket.gethostname()
+
+
+def scripts_root():
+    override = os.environ.get("WORKCLAIM_SCRIPTS_ROOT")
+    return Path(override).expanduser().resolve() if override else Path.home() / ".claude" / "scripts"
+
+
+def default_target():
+    return Path.home() / ".claude" / "state" / "workclaim" / "workclaim.sqlite3"
+
+
+def default_bus_dir():
+    override = os.environ.get("MACHINE_BUS_DIR")
+    if override:
+        return Path(override).expanduser()
+    root = scripts_root()
+    try:
+        sys.path.insert(0, str(root))
+        import menv  # type: ignore
+        value = menv.get("MACHINE_BUS_DIR") or menv.get("OBSIDIAN_VAULT")
+        if value:
+            path = Path(value)
+            return path if path.name == "_machine-bus" else path / "_machine-bus"
+    except Exception:
+        pass
+    return Path.home() / "Obsidian" / "Vault-Knowledge" / "_machine-bus"
+
+
+def usage_path():
+    override = os.environ.get("WORKCLAIM_CUTOVER_USAGE")
+    return Path(override).expanduser() if override else Path.home() / ".claude" / "usage" / "workclaim-store-cutover.jsonl"
+
+
+def count(event, outcome, extra=None):
+    """Best-effort use counter; authority decisions never depend on telemetry."""
+    try:
+        path = usage_path()
+        path.parent.mkdir(parents=True, exist_ok=True)
+        row = {"ts": utc_now(), "node": node_name(),
+               "actor": os.environ.get("CLAUDE_OPERATOR", "robot"),
+               "event": str(event), "outcome": str(outcome)}
+        if extra:
+            row.update(extra)
+        with io.open(str(path), "a", encoding="utf-8") as stream:
+            stream.write(json.dumps(row, ensure_ascii=False, sort_keys=True) + "\n")
+    except Exception:
+        pass
+
+
+def sha256_file(path):
+    digest = hashlib.sha256()
+    with io.open(str(path), "rb") as stream:
+        for chunk in iter(lambda: stream.read(1024 * 1024), b""):
+            digest.update(chunk)
+    return digest.hexdigest().upper()
+
+
+def fsync_file(path):
+    # Windows rejects FlushFileBuffers on a descriptor opened read-only even
+    # though POSIX commonly permits fsync there. Open the already-created file
+    # read/write without truncation; this changes no bytes.
+    descriptor = os.open(str(path), os.O_RDWR)
+    try:
+        os.fsync(descriptor)
+    finally:
+        os.close(descriptor)
+
+
+def atomic_json(path, payload):
+    path = Path(path)
+    path.parent.mkdir(parents=True, exist_ok=True)
+    tmp = path.with_name(path.name + ".tmp-%d" % os.getpid())
+    with io.open(str(tmp), "w", encoding="utf-8", newline="\n") as stream:
+        json.dump(payload, stream, ensure_ascii=False, indent=2, sort_keys=True)
+        stream.write("\n")
+        stream.flush()
+        os.fsync(stream.fileno())
+    os.replace(str(tmp), str(path))
+
+
+def sqlite_ro(path, immutable=False):
+    uri = Path(path).resolve().as_uri() + "?mode=ro"
+    if immutable:
+        uri += "&immutable=1"
+    con = sqlite3.connect(uri, uri=True, timeout=10, isolation_level=None)
+    con.row_factory = sqlite3.Row
+    con.execute("PRAGMA query_only=ON")
+    return con
+
+
+def typed(value):
+    if value is None:
+        return ["null", None]
+    if isinstance(value, bytes):
+        return ["blob", value.hex()]
+    if isinstance(value, bool):
+        return ["int", int(value)]
+    if isinstance(value, int):
+        return ["int", value]
+    if isinstance(value, float):
+        return ["float", repr(value)]
+    return ["text", str(value)]
+
+
+def _digest_payload(tables, ignore_global_epoch=False):
+    normalized = []
+    for table in sorted(tables):
+        entry = tables[table]
+        rows = entry["rows"]
+        if ignore_global_epoch and table == "epochs":
+            rows = [row for row in rows
+                    if not (row and row[0] == ["text", GLOBAL_EPOCH_KEY])]
+        normalized.append([table, entry["columns"], rows])
+    blob = json.dumps(normalized, ensure_ascii=False, separators=(",", ":"),
+                      sort_keys=False).encode("utf-8")
+    return hashlib.sha256(blob).hexdigest().upper()
+
+
+def semantic_snapshot(path):
+    con = sqlite_ro(path)
+    try:
+        integrity = str(con.execute("PRAGMA integrity_check").fetchone()[0])
+        if integrity != "ok":
+            raise CutoverError("integrity", {"path": str(path), "value": integrity})
+        fk = con.execute("PRAGMA foreign_key_check").fetchone()
+        if fk is not None:
+            raise CutoverError("foreign-key", {"path": str(path), "row": list(fk)})
+        present = sorted(row[0] for row in con.execute(
+            "SELECT name FROM sqlite_master WHERE type='table' "
+            "AND name NOT LIKE 'sqlite_%'").fetchall())
+        if present != sorted(EXPECTED_TABLES):
+            raise CutoverError("schema", {"path": str(path), "tables": present})
+        table_data = {}
+        counts = {}
+        for table in EXPECTED_TABLES:
+            columns = [str(row[1]) for row in con.execute(
+                "PRAGMA table_info(%s)" % table).fetchall()]
+            values = []
+            for row in con.execute("SELECT * FROM %s" % table).fetchall():
+                values.append([typed(value) for value in tuple(row)])
+            values.sort(key=lambda item: json.dumps(
+                item, ensure_ascii=False, separators=(",", ":")))
+            table_data[table] = {"columns": columns, "rows": values}
+            counts[table] = len(values)
+        epoch_row = con.execute(
+            "SELECT last_epoch FROM epochs WHERE k=?", (GLOBAL_EPOCH_KEY,)).fetchone()
+        global_epoch = int(epoch_row[0]) if epoch_row is not None else 0
+        maxima = []
+        for table, column in (("claims", "epoch"), ("completions", "epoch"),
+                              ("question_owners", "epoch"),
+                              ("legacy_import_seen", "imported_epoch"),
+                              ("epochs", "last_epoch")):
+            row = con.execute("SELECT MAX(%s) FROM %s" % (column, table)).fetchone()
+            if row is not None and row[0] is not None:
+                maxima.append(int(row[0]))
+        now = time.time()
+        live_claims = int(con.execute(
+            "SELECT COUNT(*) FROM claims WHERE since_ts + ttl_sec > ?", (now,)).fetchone()[0])
+        live_questions = int(con.execute(
+            "SELECT COUNT(*) FROM question_owners WHERE since_ts + ttl_sec > ?", (now,)).fetchone()[0])
+        return {
+            "path": str(Path(path).resolve()), "integrity": integrity,
+            "counts": counts, "global_epoch": global_epoch,
+            "epoch_floor": max(maxima or [0]),
+            "live_claims": live_claims, "live_question_owners": live_questions,
+            "digest": _digest_payload(table_data, False),
+            "state_digest": _digest_payload(table_data, True),
+        }
+    finally:
+        con.close()
+
+
+def provider_paths(root=None):
+    root = Path(root or scripts_root())
+    return root / "_shared" / "workclaim.py", root / "retro_lost_scan.py"
+
+
+def assert_code_pair(root, expected_provider, expected_scanner):
+    provider, scanner = provider_paths(root)
+    facts = {"provider": str(provider), "scanner": str(scanner),
+             "provider_exists": provider.is_file(), "scanner_exists": scanner.is_file()}
+    if not provider.is_file() or not scanner.is_file():
+        raise CutoverError("code-pair-missing", facts)
+    facts["provider_sha256"] = sha256_file(provider)
+    facts["scanner_sha256"] = sha256_file(scanner)
+    if facts["provider_sha256"] != expected_provider.upper():
+        raise CutoverError("provider-hash", facts)
+    if facts["scanner_sha256"] != expected_scanner.upper():
+        raise CutoverError("scanner-hash", facts)
+    return facts
+
+
+def provider_env(db_path=None):
+    env = os.environ.copy()
+    env.pop("WORKCLAIM_MUTEX_DB", None)
+    if db_path is None:
+        env.pop("WORKCLAIM_DB", None)
+    else:
+        env["WORKCLAIM_DB"] = str(Path(db_path).resolve())
+    env["WORKCLAIM_USAGE"] = str(usage_path())
+    return env
+
+
+def provider_health(provider, db_path=None):
+    result = subprocess.run(
+        [sys.executable, "-B", str(provider), "store-health"],
+        env=provider_env(db_path), text=True, capture_output=True, timeout=45)
+    try:
+        payload = json.loads((result.stdout or "").strip().splitlines()[-1])
+    except Exception:
+        payload = None
+    return result, payload
+
+
+def provider_bootstrap(provider, db_path):
+    code = (
+        "import importlib.util,json,os,sys;"
+        "p=sys.argv[1];"
+        "s=importlib.util.spec_from_file_location('cutover_workclaim',p);"
+        "m=importlib.util.module_from_spec(s);s.loader.exec_module(m);"
+        "c=m._connect();c.close();"
+        "print(json.dumps(m.store_health(),sort_keys=True))"
+    )
+    result = subprocess.run(
+        [sys.executable, "-B", "-c", code, str(provider)],
+        env=provider_env(db_path), text=True, capture_output=True, timeout=60)
+    try:
+        payload = json.loads((result.stdout or "").strip().splitlines()[-1])
+    except Exception:
+        payload = None
+    if result.returncode != 0 or not payload or not payload.get("ok"):
+        raise CutoverError("provider-bootstrap", {
+            "rc": result.returncode, "stdout": result.stdout[-1000:],
+            "stderr": result.stderr[-1000:], "health": payload,
+        })
+    return payload
+
+
+def candidate_paths(target, extras=None):
+    target = Path(target).expanduser().absolute()
+    home = Path.home()
+    local = Path(os.environ.get("LOCALAPPDATA") or (home / ".claude"))
+    values = [
+        ("target", target),
+        ("legacy-default", local / "AntonAgents" / "workclaim" / "workclaim.sqlite3"),
+        ("legacy-posix", home / ".claude" / "AntonAgents" / "workclaim" / "workclaim.sqlite3"),
+    ]
+    package_pattern = str(local / "Packages" / "OpenAI.Codex_*" / "LocalCache" /
+                          "Local" / "AntonAgents" / "workclaim" / "workclaim.sqlite3")
+    values.extend(("legacy-msix", Path(item)) for item in sorted(glob.glob(package_pattern)))
+    values.extend(("explicit", Path(item).expanduser().absolute()) for item in (extras or []))
+    output = []
+    seen = []
+    for kind, path in values:
+        key = os.path.normcase(os.path.realpath(os.path.abspath(str(path))))
+        if key in seen:
+            continue
+        seen.append(key)
+        output.append((kind, path))
+    return output
+
+
+def raw_probe(kind, path, provider):
+    result = {"kind": kind, "path": str(path), "exists": path.is_file()}
+    if not path.is_file():
+        return result
+    try:
+        result.update({"size": path.stat().st_size, "sha256": sha256_file(path)})
+        con = sqlite_ro(path)
+        try:
+            result["integrity"] = str(con.execute("PRAGMA integrity_check").fetchone()[0])
+            result["tables"] = sorted(row[0] for row in con.execute(
+                "SELECT name FROM sqlite_master WHERE type='table' "
+                "AND name NOT LIKE 'sqlite_%'").fetchall())
+        finally:
+            con.close()
+        health_result, health = provider_health(provider, path)
+        result["current_health_rc"] = health_result.returncode
+        result["current_health"] = health
+    except Exception as exc:
+        result["error"] = "%s: %s" % (type(exc).__name__, str(exc))
+    return result
+
+
+def mirror_epoch(bus_dir):
+    root = Path(bus_dir) / "_claims"
+    maximum = 0
+    parsed = 0
+    invalid = []
+    if not root.is_dir():
+        return {"root": str(root), "files": 0, "parsed": 0, "invalid": [], "max_epoch": 0}
+    files = sorted(root.rglob("*.claim"))
+    for path in files:
+        try:
+            payload = json.loads(path.read_text(encoding="utf-8-sig"))
+            value = payload.get("epoch")
+            if value is None or isinstance(value, bool):
+                continue
+            value = int(value)
+            if value <= 0:
+                continue
+            maximum = max(maximum, value)
+            parsed += 1
+        except Exception as exc:
+            invalid.append({"path": str(path), "error": type(exc).__name__})
+    return {"root": str(root), "files": len(files), "parsed": parsed,
+            "invalid": invalid[:20], "max_epoch": maximum}
+
+
+def process_rows():
+    injected = os.environ.get("WORKCLAIM_CUTOVER_TEST_PROCESS_LIST")
+    if injected is not None and os.environ.get("WORKCLAIM_CUTOVER_TEST_MODE") == "1":
+        return [{"pid": 999999, "name": "python", "executable": "python",
+                 "command": line} for line in injected.splitlines() if line.strip()]
+    if os.name == "nt":
+        command = ["powershell", "-NoProfile", "-Command",
+                   "Get-CimInstance Win32_Process | Select-Object ProcessId,Name,ExecutablePath,CommandLine | ConvertTo-Json -Compress"]
+        result = subprocess.run(command, text=True, capture_output=True, timeout=30)
+        if result.returncode != 0:
+            raise CutoverError("process-inventory", {"rc": result.returncode,
+                                                       "stderr": result.stderr[-1000:]})
+        payload = json.loads(result.stdout or "[]")
+        if isinstance(payload, dict):
+            payload = [payload]
+        return [{"pid": int(row.get("ProcessId") or 0),
+                 "name": str(row.get("Name") or ""),
+                 "executable": str(row.get("ExecutablePath") or ""),
+                 "command": str(row.get("CommandLine") or "")} for row in payload]
+    result = subprocess.run(["ps", "-eo", "pid=,comm=,args="], text=True,
+                            capture_output=True, timeout=30)
+    if result.returncode != 0:
+        raise CutoverError("process-inventory", {"rc": result.returncode,
+                                                   "stderr": result.stderr[-1000:]})
+    rows = []
+    for line in result.stdout.splitlines():
+        match = re.match(r"\s*(\d+)\s+(\S+)\s+(.*)$", line)
+        if match:
+            rows.append({"pid": int(match.group(1)), "name": match.group(2),
+                         "executable": match.group(2), "command": match.group(3)})
+    return rows
+
+
+def active_consumers():
+    current = os.getpid()
+    matches = []
+    for row in process_rows():
+        if row["pid"] == current:
+            continue
+        runtime = (row.get("name", "") + " " +
+                   row.get("executable", "")).lower()
+        if not any(token in runtime for token in ("python", "pypy")):
+            continue
+        command = row["command"].replace("\\", "/").lower()
+        if "retro_lost_scan.py" in command or "/_shared/workclaim.py" in command:
+            matches.append(row)
+    return matches
+
+
[EMAIL]
+def cutover_lock(target, deploy_id):
+    lock = Path(str(target) + ".cutover.lock")
+    lock.parent.mkdir(parents=True, exist_ok=True)
+    try:
+        fd = os.open(str(lock), os.O_CREAT | os.O_EXCL | os.O_WRONLY, 0o600)
+    except FileExistsError:
+        raise CutoverError("cutover-lock", {"path": str(lock)})
+    try:
+        with os.fdopen(fd, "w", encoding="utf-8") as stream:
+            json.dump({"deploy_id": deploy_id, "pid": os.getpid(),
+                       "node": node_name(), "ts": utc_now()}, stream, sort_keys=True)
+            stream.flush()
+            os.fsync(stream.fileno())
+        yield lock
+    finally:
+        try:
+            lock.unlink()
+        except FileNotFoundError:
+            pass
+
+
+def backup_sqlite(source, destination, hold_lock=False):
+    source = Path(source)
+    destination = Path(destination)
+    destination.parent.mkdir(parents=True, exist_ok=True)
+    try:
+        destination.unlink()
+    except FileNotFoundError:
+        pass
+    locker = None
+    reader = None
+    target = None
+    try:
+        if hold_lock:
+            locker = sqlite3.connect(str(source), timeout=15, isolation_level=None)
+            locker.execute("PRAGMA busy_timeout=15000")
+            locker.execute("BEGIN IMMEDIATE")
+        reader = sqlite_ro(source)
+        target = sqlite3.connect(str(destination), timeout=15, isolation_level=None)
+        reader.backup(target)
+        target.commit()
+        target.close()
+        target = None
+        fsync_file(destination)
+        return locker
+    except BaseException:
+        if locker is not None:
+            try:
+                locker.rollback()
+            except Exception:
+                pass
+            locker.close()
+        raise
+    finally:
+        if reader is not None:
+            reader.close()
+        if target is not None:
+            target.close()
+
+
+def release_sqlite_lock(locker):
+    if locker is not None:
+        try:
+            locker.rollback()
+        finally:
+            locker.close()
+
+
+def stage_candidate(source, provider, directory):
+    fd, name = tempfile.mkstemp(prefix=".candidate-", suffix=".sqlite3", dir=str(directory))
+    os.close(fd)
+    path = Path(name)
+    path.unlink()
+    try:
+        backup_sqlite(source, path, hold_lock=False)
+        provider_bootstrap(provider, path)
+        return semantic_snapshot(path)
+    finally:
+        for suffix in ("", "-wal", "-shm", "-journal"):
+            try:
+                Path(str(path) + suffix).unlink()
+            except FileNotFoundError:
+                pass
+
+
+def inspect_sources(target, provider, extras=None):
+    existing = [(kind, path) for kind, path in candidate_paths(target, extras)
+                if kind != "target" and path.is_file()]
+    valid = []
+    invalid = []
+    Path(target).parent.mkdir(parents=True, exist_ok=True)
+    for kind, path in existing:
+        try:
+            snapshot = stage_candidate(path, provider, Path(target).parent)
+            valid.append({"kind": kind, "path": str(path),
+                          "raw_sha256": sha256_file(path), "snapshot": snapshot})
+        except Exception as exc:
+            invalid.append({"kind": kind, "path": str(path),
+                            "error": "%s: %s" % (type(exc).__name__, str(exc))})
+    if invalid:
+        raise CutoverError("legacy-source-invalid", invalid)
+    digests = sorted({item["snapshot"]["digest"] for item in valid})
+    if len(digests) > 1:
+        raise CutoverError("legacy-sources-diverge", valid)
+    for item in valid:
+        snap = item["snapshot"]
+        if snap["live_claims"] or snap["live_question_owners"]:
+            raise CutoverError("live-authority-claim", item)
+    return valid
+
+
+def raise_epoch_floor(path, mirror_max):
+    con = sqlite3.connect(str(path), timeout=15, isolation_level=None)
+    try:
+        con.execute("PRAGMA foreign_keys=ON")
+        con.execute("BEGIN IMMEDIATE")
+        row = con.execute("SELECT last_epoch FROM epochs WHERE k=?",
+                          (GLOBAL_EPOCH_KEY,)).fetchone()
+        before = int(row[0]) if row is not None else 0
+        desired = max(before, int(mirror_max) + 1)
+        con.execute(
+            "INSERT INTO epochs(k,last_epoch) VALUES(?,?) "
+            "ON CONFLICT(k) DO UPDATE SET last_epoch=excluded.last_epoch",
+            (GLOBAL_EPOCH_KEY, desired))
+        con.commit()
+        mode = str(con.execute("PRAGMA journal_mode=DELETE").fetchone()[0]).lower()
+        if mode != "delete":
+            raise CutoverError("journal-mode", {"value": mode})
+        return before, desired
+    except BaseException:
+        try:
+            con.rollback()
+        except Exception:
+            pass
+        raise
+    finally:
+        con.close()
+
+
+def receipt_paths(target, deploy_id):
+    base = Path(target).parent
+    return (base / "cutover-receipts" / (deploy_id + ".json"),
+            base / "rollback" / deploy_id)
+
+
+def inventory(args):
+    root = Path(args.scripts_root).expanduser().absolute()
+    provider, _scanner = provider_paths(root)
+    code = None
+    try:
+        code = assert_code_pair(root, args.expected_provider_sha,
+                                args.expected_scanner_sha)
+    except CutoverError as exc:
+        code = {"ok": False, "reason": exc.reason, "detail": exc.detail}
+    candidates = [raw_probe(kind, path, provider) if provider.is_file() else
+                  {"kind": kind, "path": str(path), "exists": path.is_file()}
+                  for kind, path in candidate_paths(args.target_db, args.legacy_db)]
+    return {"ok": True, "command": "inventory", "node": node_name(),
+            "target": str(args.target_db), "code_pair": code,
+            "candidates": candidates, "mirrors": mirror_epoch(args.bus_dir)}
+
+
+def verify_receipt(args, emit=True):
+    receipt_path, _rollback = receipt_paths(args.target_db, args.deploy_id)
+    if not receipt_path.is_file():
+        raise CutoverError("receipt-missing", {"path": str(receipt_path)})
+    receipt = json.loads(receipt_path.read_text(encoding="utf-8-sig"))
+    if receipt.get("status") != "committed" or receipt.get("deploy_id") != args.deploy_id:
+        raise CutoverError("receipt-invalid", receipt)
+    code = assert_code_pair(args.scripts_root, receipt["provider_sha256"],
+                            receipt["scanner_sha256"])
+    target = Path(args.target_db)
+    if not target.is_file() or target.is_symlink():
+        raise CutoverError("target-missing-or-symlink", {"path": str(target)})
+    provider, _scanner = provider_paths(args.scripts_root)
+    health_result, health = provider_health(provider, None)
+    if (health_result.returncode != 0 or not health or not health.get("ok") or
+            os.path.normcase(str(health.get("backend", ""))) !=
+            os.path.normcase(str(target.absolute()))):
+        raise CutoverError("default-health", {
+            "rc": health_result.returncode, "health": health,
+            "stderr": health_result.stderr[-1000:], "target": str(target),
+        })
+    snapshot = semantic_snapshot(target)
+    baseline = receipt["target_snapshot"]
+    if snapshot["digest"] != baseline["digest"]:
+        raise CutoverError("target-drift", {"expected": baseline, "actual": snapshot})
+    rollback_snapshot = Path(receipt["rollback_snapshot"])
+    if receipt.get("source"):
+        source = Path(receipt["source"])
+        if not source.is_file():
+            raise CutoverError("legacy-source-missing", {"path": str(source)})
+        if sha256_file(source) != receipt["source_raw_sha256"]:
+            raise CutoverError("legacy-source-drift", {
+                "path": str(source), "expected": receipt["source_raw_sha256"],
+                "actual": sha256_file(source)})
+        if not rollback_snapshot.is_file():
+            raise CutoverError("rollback-snapshot-missing", {"path": str(rollback_snapshot)})
+        backup_snapshot = semantic_snapshot(rollback_snapshot)
+        if backup_snapshot["state_digest"] != receipt["source_snapshot"]["state_digest"]:
+            raise CutoverError("rollback-snapshot-drift", backup_snapshot)
+    payload = {"ok": True, "command": "verify", "node": node_name(),
+               "deploy_id": args.deploy_id, "receipt": str(receipt_path),
+               "code_pair": code, "health": health, "snapshot": snapshot,
+               "source": receipt.get("source")}
+    if emit:
+        return payload
+    return payload
+
+
+def apply_cutover(args):
+    if os.environ.get("WORKCLAIM_DB") or os.environ.get("WORKCLAIM_MUTEX_DB"):
+        raise CutoverError("authority-env-override", {
+            "WORKCLAIM_DB": bool(os.environ.get("WORKCLAIM_DB")),
+            "WORKCLAIM_MUTEX_DB": bool(os.environ.get("WORKCLAIM_MUTEX_DB")),
+        })
+    target = Path(args.target_db).expanduser().absolute()
+    canonical = default_target().absolute()
+    if os.path.normcase(str(target)) != os.path.normcase(str(canonical)):
+        raise CutoverError("noncanonical-target", {"target": str(target),
+                                                    "canonical": str(canonical)})
+    receipt_path, rollback_dir = receipt_paths(target, args.deploy_id)
+    if receipt_path.is_file():
+        return verify_receipt(args, emit=False)
+    if target.exists():
+        raise CutoverError("target-without-receipt", {"path": str(target)})
+    code = assert_code_pair(args.scripts_root, args.expected_provider_sha,
+                            args.expected_scanner_sha)
+    consumers = active_consumers()
+    if consumers:
+        raise CutoverError("active-consumer-process", consumers)
+    provider, _scanner = provider_paths(args.scripts_root)
+    target.parent.mkdir(parents=True, exist_ok=True)
+    with cutover_lock(target, args.deploy_id):
+        if target.exists() or receipt_path.exists():
+            raise CutoverError("cutover-race", {"target": target.exists(),
+                                                "receipt": receipt_path.exists()})
+        sources = inspect_sources(target, provider, args.legacy_db)
+        if not sources and not args.allow_empty_seed:
+            raise CutoverError("legacy-source-missing", {
+                "hint": "rerun only after audited inventory with --allow-empty-seed"})
+        mirror = mirror_epoch(args.bus_dir)
+        if mirror["invalid"]:
+            raise CutoverError("mirror-parse", mirror)
+        rollback_dir.mkdir(parents=True, exist_ok=False)
+        intent = {"status": "preparing", "deploy_id": args.deploy_id,
+                  "node": node_name(), "ts": utc_now(), "target": str(target),
+                  "sources": sources, "code_pair": code, "mirrors": mirror,
+                  "allow_empty_seed": bool(args.allow_empty_seed)}
+        atomic_json(rollback_dir / "intent.json", intent)
+        stage = target.with_name(target.name + ".stage-" + args.deploy_id)
+        rollback_snapshot = rollback_dir / "source.sqlite3"
+        source_lock = None
+        activated = False
+        committed = False
+        source = Path(sources[0]["path"]) if sources else None
+        try:
+            for suffix in ("", "-wal", "-shm", "-journal"):
+                try:
+                    Path(str(stage) + suffix).unlink()
+                except FileNotFoundError:
+                    pass
+            if source is not None:
+                source_lock = backup_sqlite(source, stage, hold_lock=True)
+                provider_bootstrap(provider, stage)
+                staged_before = semantic_snapshot(stage)
+                expected = sources[0]["snapshot"]
+                if staged_before["digest"] != expected["digest"]:
+                    raise CutoverError("source-mutated-during-cutover", {
+                        "inventory": expected, "locked_copy": staged_before})
+                # Rollback evidence is a second online copy of the locked,
+                # current-schema stage. The legacy source itself stays byte-for-byte
+                # untouched and remains the actual old-route rollback authority.
+                backup_sqlite(stage, rollback_snapshot, hold_lock=False)
+            else:
+                provider_bootstrap(provider, stage)
+                staged_before = semantic_snapshot(stage)
+            if staged_before["live_claims"] or staged_before["live_question_owners"]:
+                raise CutoverError("live-authority-claim", staged_before)
+            # Empty-seed must remain empty all the way to activation. A stale
+            # binary creating the old default after inventory is a real race.
+            if source is None:
+                late = inspect_sources(target, provider, args.legacy_db)
+                if late:
+                    raise CutoverError("legacy-source-appeared", late)
+            epoch_before, epoch_after = raise_epoch_floor(stage, mirror["max_epoch"])
+            provider_bootstrap(provider, stage)
+            staged_after = semantic_snapshot(stage)
+            if staged_after["state_digest"] != staged_before["state_digest"]:
+                raise CutoverError("state-changed-during-fence", {
+                    "before": staged_before, "after": staged_after})
+            if staged_after["global_epoch"] <= mirror["max_epoch"]:
+                raise CutoverError("mirror-epoch-not-fenced", {
+                    "snapshot": staged_after, "mirrors": mirror})
+            os.replace(str(stage), str(target))
+            activated = True
+            fsync_file(target)
+            health_result, health = provider_health(provider, None)
+            if (health_result.returncode != 0 or not health or not health.get("ok") or
+                    os.path.normcase(str(health.get("backend", ""))) !=
+                    os.path.normcase(str(target))):
+                raise CutoverError("post-activation-health", {
+                    "rc": health_result.returncode, "health": health,
+                    "stderr": health_result.stderr[-1000:]})
+            target_snapshot = semantic_snapshot(target)
+            if target_snapshot["digest"] != staged_after["digest"]:
+                raise CutoverError("post-activation-drift", {
+                    "stage": staged_after, "target": target_snapshot})
+            receipt = {
+                "status": "committed", "deploy_id": args.deploy_id,
+                "node": node_name(), "ts": utc_now(), "target": str(target),
+                "physical_target": os.path.realpath(str(target)),
+                "provider_sha256": code["provider_sha256"],
+                "scanner_sha256": code["scanner_sha256"],
+                "source": str(source) if source is not None else None,
+                "source_kind": sources[0]["kind"] if sources else "explicit-empty-seed",
+                "source_raw_sha256": (sources[0]["raw_sha256"]
+                                        if sources else None),
+                "source_snapshot": sources[0]["snapshot"] if sources else None,
+                "rollback_snapshot": str(rollback_snapshot),
+                "rollback_dir": str(rollback_dir), "mirrors": mirror,
+                "epoch_before_fence": epoch_before,
+                "epoch_after_fence": epoch_after,
+                "target_snapshot": target_snapshot, "health": health,
+                "source_left_untouched": bool(source is not None and source.is_file()),
+            }
+            atomic_json(receipt_path, receipt)
+            committed = True
+            return {"ok": True, "command": "apply", "node": node_name(),
+                    "deploy_id": args.deploy_id, "receipt": str(receipt_path),
+                    "target": str(target), "source": receipt["source"],
+                    "source_kind": receipt["source_kind"], "health": health,
+                    "snapshot": target_snapshot}
+        except BaseException:
+            if activated and not committed and target.exists():
+                failed = rollback_dir / "failed-target.sqlite3"
+                os.replace(str(target), str(failed))
+            raise
+        finally:
+            release_sqlite_lock(source_lock)
+            for suffix in ("", "-wal", "-shm", "-journal"):
+                try:
+                    Path(str(stage) + suffix).unlink()
+                except FileNotFoundError:
+                    pass
+
+
+def rollback(args):
+    receipt_path, rollback_dir = receipt_paths(args.target_db, args.deploy_id)
+    if not receipt_path.is_file():
+        raise CutoverError("receipt-missing", {"path": str(receipt_path)})
+    receipt = json.loads(receipt_path.read_text(encoding="utf-8-sig"))
+    target = Path(args.target_db)
+    if not target.is_file():
+        raise CutoverError("target-missing", {"path": str(target)})
+    consumers = active_consumers()
+    if consumers:
+        raise CutoverError("active-consumer-process", consumers)
+    current = semantic_snapshot(target)
+    if current["digest"] != receipt["target_snapshot"]["digest"]:
+        raise CutoverError("rollback-after-state-drift", {
+            "receipt": receipt["target_snapshot"], "current": current})
+    if current["live_claims"] or current["live_question_owners"]:
+        raise CutoverError("live-authority-claim", current)
+    with cutover_lock(target, args.deploy_id + "-rollback"):
+        parked = rollback_dir / "post-cutover.sqlite3"
+        if parked.exists():
+            raise CutoverError("rollback-target-exists", {"path": str(parked)})
+        os.replace(str(target), str(parked))
+        payload = {"ok": True, "status": "rolled-back-store-only",
+                   "deploy_id": args.deploy_id, "node": node_name(),
+                   "ts": utc_now(), "parked_target": str(parked),
+                   "legacy_source": receipt.get("source"),
+                   "warning": "provider route/version must also be reverted before old service resumes"}
+        atomic_json(rollback_dir / "rollback.json", payload)
+        return payload
+
+
+def build_parser():
+    parser = argparse.ArgumentParser(description=__doc__.splitlines()[0])
+    parser.add_argument("--scripts-root", type=Path, default=scripts_root())
+    parser.add_argument("--target-db", type=Path, default=default_target())
+    parser.add_argument("--bus-dir", type=Path, default=default_bus_dir())
+    parser.add_argument("--legacy-db", action="append", default=[])
+    parser.add_argument("--expected-provider-sha", default=EXPECTED_PROVIDER_SHA)
+    parser.add_argument("--expected-scanner-sha", default=EXPECTED_SCANNER_SHA)
+    sub = parser.add_subparsers(dest="command", required=True)
+    sub.add_parser("inventory", help="read-only path/code/store inventory")
+    apply_p = sub.add_parser("apply", help="atomic cutover; rc=4 on every safety stop")
+    apply_p.add_argument("--deploy-id", required=True)
+    apply_p.add_argument("--allow-empty-seed", action="store_true")
+    verify_p = sub.add_parser("verify", help="recipient-side exact receipt verification")
+    verify_p.add_argument("--deploy-id", required=True)
+    rollback_p = sub.add_parser("rollback", help="park an unchanged new target")
+    rollback_p.add_argument("--deploy-id", required=True)
+    return parser
+
+
+def main(argv=None):
+    parser = build_parser()
+    args = parser.parse_args(argv)
+    args.scripts_root = Path(args.scripts_root).expanduser().absolute()
+    args.target_db = Path(args.target_db).expanduser().absolute()
+    args.bus_dir = Path(args.bus_dir).expanduser().absolute()
+    if hasattr(args, "deploy_id") and not DEPLOY_ID_RE.match(args.deploy_id):
+        parser.error("deploy-id must match %s" % DEPLOY_ID_RE.pattern)
+    event = args.command
+    try:
+        if args.command == "inventory":
+            payload = inventory(args)
+        elif args.command == "apply":
+            payload = apply_cutover(args)
+        elif args.command == "verify":
+            payload = verify_receipt(args)
+        else:
+            payload = rollback(args)
+        count(event, "ok", {"deploy_id": getattr(args, "deploy_id", None)})
+        print(json.dumps(payload, ensure_ascii=False, sort_keys=True))
+        return 0
+    except CutoverError as exc:
+        payload = {"ok": False, "command": event, "node": node_name(),
+                   "reason": exc.reason, "detail": exc.detail}
+        count(event, "red", {"reason": exc.reason,
+                              "deploy_id": getattr(args, "deploy_id", None)})
+        print(json.dumps(payload, ensure_ascii=False, sort_keys=True))
+        return 4
+    except BaseException as exc:
+        payload = {"ok": False, "command": event, "node": node_name(),
+                   "reason": "unexpected", "detail": "%s: %s" %
+                   (type(exc).__name__, str(exc))}
+        count(event, "error", {"error": type(exc).__name__,
+                                "deploy_id": getattr(args, "deploy_id", None)})
+        print(json.dumps(payload, ensure_ascii=False, sort_keys=True))
+        return 4
+
+
+if __name__ == "__main__":
+    raise SystemExit(main())
