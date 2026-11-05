---
session: s_69da237d
date: 2026-10-01
words: 1267
turns: 1
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are an INDEPENDENT senior code reviewer from a DIFFERENT vendor than the author

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_69da237d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
Read-only independent review. No tools. Codex must use the same explicit --connect brokers as Claude; no new WhatsApp link owners, no cross-account credentials. Three tests passed and both fresh configured clients initialized and listed 17 tools. Review correctness and risks.

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
--- a/index.js
+++ b/index.js
@@ -77,7 +77,13 @@
         if (!raw || !raw.url || !raw.key || !raw.pid) {
             return undefined;
         }
-        process.kill(raw.pid, 0);
+        try {
+            process.kill(raw.pid, 0);
+        } catch (err) {
+            // EPERM is an inaccessible process, not a dead broker. The caller
+            // still checks the loopback port and authenticates the MCP proxy.
+            if (err.code !== "EPERM") throw err;
+        }
         return { url: raw.url, key: raw.key };
     }
     catch {
@@ -381,4 +387,4 @@
     console.error("Fatal error:", err);
     process.exit(1);
 });
-//# sourceMappingURL=index.js.map+//# sourceMappingURL=index.js.map
--- a/wa_vendor_patch.py
+++ b/wa_vendor_patch.py
@@ -196,7 +196,13 @@
         if (!raw || !raw.url || !raw.key || !raw.pid) {
             return undefined;
         }
-        process.kill(raw.pid, 0);
+        try {
+            process.kill(raw.pid, 0);
+        } catch (err) {
+            // EPERM is an inaccessible process, not a dead broker. The caller
+            // still checks the loopback port and authenticates the MCP proxy.
+            if (err.code !== "EPERM") throw err;
+        }
         return { url: raw.url, key: raw.key };
     }
     catch {
@@ -374,6 +380,20 @@
             raise SystemExit("G3: main() anchor not found — vendor layout changed")
         idx = idx.replace(G3_ANCHOR, G3_REPLACE, 1)
         changed.append("G3")
+
+    # Upgrade already patched G2/G3 installations as well as clean installs.
+    old_probe = "        process.kill(raw.pid, 0);\n        return { url: raw.url, key: raw.key };"
+    new_probe = """        try {
+            process.kill(raw.pid, 0);
+        } catch (err) {
+            // EPERM is an inaccessible process, not a dead broker. The caller
+            // still checks the loopback port and authenticates the MCP proxy.
+            if (err.code !== "EPERM") throw err;
+        }
+        return { url: raw.url, key: raw.key };"""
+    if old_probe in idx:
+        idx = idx.replace(old_probe, new_probe, 1)
+        changed.append("G3/EPERM")
 
     idx, did = _apply_g1(idx, "index.js")
     if did:
--- a/config.toml
+++ b/config.toml
@@ -118,12 +118,12 @@
 args = [ "C:\\mcp\\telegram-mcp\\main.py", "C:\\TG-Media" ]
 
 [mcp_servers.whatsapp]
-command = "node"
-args = [ "C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\\index.js" ]
+command = "python"
+args = [ "C:\\Users\\dev\\.claude\\scripts\\wa_codex_proxy.py", "--account", "main" ]
 
 [mcp_servers.whatsapp2]
-command = "node"
-args = [ "C:\\Users\\dev\\AppData\\Roaming\\npm\\node_modules\\@sjawhar\\whatsapp-mcp\\dist\\index.js", "--wa-account=wa2" ]
+command = "python"
+args = [ "C:\\Users\\dev\\.claude\\scripts\\wa_codex_proxy.py", "--account", "wa2" ]
 
 [mcp_servers.whatsapp2.env]
 XDG_DATA_HOME = "C:\\Users\\dev\\.local\\share\\wa-wa2"
--- a/wa_codex_proxy.py
+++ b/wa_codex_proxy.py
@@ -0,0 +1,52 @@
+"""Codex WhatsApp: use the existing account broker, never own a WhatsApp link.
+
+Assisted-by: Codex; Machine: HUB-01; Operator: dev.
+Secrets stay in the broker descriptor. See docs/wa_codex_proxy.md.
+"""
+import argparse
+import json
+import os
+from pathlib import Path
+import shutil
+import subprocess
+import sys
+
+
+def connection(account, home):
+    if account not in ("main", "wa2"):
+        raise ValueError("unsupported account")
+    data = home / ".local" / "share"
+    if account == "wa2":
+        data /= "wa-wa2"
+    descriptor = json.loads((data / "whatsapp-mcp/store/.broker.json").read_text(encoding="utf-8"))
+    expected = "http://10.0.0.0:%s/mcp" % (8791 if account == "main" else 8792)
+    if descriptor.get("url") != expected:
+        raise ValueError("broker URL does not match account loopback endpoint")
+    key = descriptor.get("key")
+    if not isinstance(key, str) or not key.strip():
+        raise ValueError("broker key missing")
+    return data, expected, key
+
+
+def main():
+    parser = argparse.ArgumentParser(description=__doc__)
+    parser.add_argument("--account", required=True, choices=("main", "wa2"))
+    args = parser.parse_args()
+    try:
+        home = Path.home()
+        data, url, key = connection(args.account, home)
+        node = shutil.which("node")
+        entry = home / "AppData/Roaming/npm/node_modules/@sjawhar/whatsapp-mcp/dist/index.js"
+        if not node or not entry.is_file():
+            raise ValueError("installed WhatsApp MCP or node missing")
+        env = dict(os.environ)
+        env.update(XDG_DATA_HOME=str(data), WHATSAPP_MCP_URL=url, MCP_API_KEY=key)
+        # Inherit stdio unchanged: it carries MCP JSON-RPC, never status output.
+        return subprocess.call([node, str(entry), "--wa-account=" + args.account, "--connect"], env=env)
+    except (OSError, ValueError, KeyError):
+        print("WhatsApp broker configuration unavailable; no direct client started", file=sys.stderr)
+        return 3
+
+
+if __name__ == "__main__":
+    sys.exit(main())
--- a/_test_wa_codex_proxy.py
+++ b/_test_wa_codex_proxy.py
@@ -0,0 +1,41 @@
+"""Account isolation and fail-closed tests; no real credentials or network."""
+import json
+from pathlib import Path
+import tempfile
+import unittest
+from unittest.mock import patch
+import wa_codex_proxy as proxy
+
+
+class BrokerTests(unittest.TestCase):
+    def test_accounts_and_missing_descriptor(self):
+        with tempfile.TemporaryDirectory() as tmp:
+            home = Path(tmp)
+            for account, rel, port in (("main", "", 8791), ("wa2", "wa-wa2", 8792)):
+                path = home / ".local/share" / rel / "whatsapp-mcp/store/.broker.json"
+                with self.assertRaises(OSError):
+                    proxy.connection(account, home)
+                path.parent.mkdir(parents=True, exist_ok=True)
+                path.write_text(json.dumps({"url": f"http://10.0.0.0:{port}/mcp", "key": account}))
+                data, url, key = proxy.connection(account, home)
+                self.assertEqual(key, account)
+                self.assertEqual(data, path.parents[2])
+                for bad in ("http://example.com/mcp", f"http://10.0.0.0:{8792 if port == 8791 else 8791}/mcp"):
+                    path.write_text(json.dumps({"url": bad, "key": "fake"}))
+                    with self.assertRaises(ValueError):
+                        proxy.connection(account, home)
+
+    def test_missing_configuration_never_spawns(self):
+        with patch.object(proxy.sys, "argv", ["proxy", "--account", "wa2"]), patch.object(proxy, "connection", side_effect=OSError), patch.object(proxy.subprocess, "call") as spawn:
+            self.assertEqual(proxy.main(), 3)
+            spawn.assert_not_called()
+
+    def test_explicit_proxy_and_account_environment(self):
+        with patch.object(proxy.sys, "argv", ["proxy", "--account", "wa2"]), patch.object(proxy, "connection", return_value=(Path("isolated"), "http://10.0.0.0:8792/mcp", "test-only")), patch.object(proxy.shutil, "which", return_value="node"), patch.object(proxy.Path, "is_file", return_value=True), patch.object(proxy.subprocess, "call", return_value=0) as spawn:
+            self.assertEqual(proxy.main(), 0)
+            self.assertEqual(spawn.call_args.args[0][-2:], ["--wa-account=wa2", "--connect"])
+            self.assertEqual(spawn.call_args.kwargs["env"]["XDG_DATA_HOME"], "isolated")
+
+
+if __name__ == "__main__":
+    unittest.main()
--- a/wa_codex_proxy.md
+++ b/wa_codex_proxy.md
@@ -0,0 +1,20 @@
+# Codex WhatsApp broker connection
+
+Status: artifact.proposed. Reviewer: Claude via cc_review.py. 2026-10-01.
+Author: Codex; machine HUB-01; operator dev.
+
+Consumer: Codex config.toml mcp_servers.whatsapp and whatsapp2.
+Before: direct vendor launch with heuristic broker discovery; Windows EPERM could
+be treated as broker death. After: explicit --connect, like Claude's configuration.
+The wrapper reads only the chosen account's existing broker descriptor. No copied
+cookies or WhatsApp credentials. Broker URL must match its fixed loopback endpoint.
+Missing/invalid configuration fails closed; it never starts a direct link owner.
+
+Run: python wa_codex_proxy.py --account main (or wa2); stdin/stdout are MCP.
+Test: python _test_wa_codex_proxy.py. Live acceptance requires initialize/tools/list
+through both configured commands; cached profile does not prove WhatsApp socket health.
+Broker failure: restore the broker, not a parallel direct client. Missing WhatsApp
+pairing is separate and requires the phone. Existing running MCP clients need reconnect.
+Rollback: config.toml.pre-20261001-wa-proxy.bak; no auth or message database changes.
+Usage evidence: broker MCP requests and live acceptance transcript; no extra log writer
+in the secret-handling proxy. Rail: local Python/Node, no paid model API.

--- DIFF END ---
