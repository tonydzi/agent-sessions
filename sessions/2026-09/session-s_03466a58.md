---
session: s_03466a58
date: 2026-09-22
words: 1737
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · -*- coding: utf-8 -*-

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_03466a58` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

--- CONTEXT ---
# -*- coding: utf-8 -*-
"""PreToolUse/Stop adapter for the shared Claude/Codex write lease.

Purpose: translate both harness payloads into one atomic local file lease. Codex
reports canonical `apply_patch`; Claude reports Write/Edit/MultiEdit/NotebookEdit.

Контракт лизы (22.09.2026, fail-closed после opaque-process incident):
  * файловый инструмент (Write/Edit/MultiEdit/NotebookEdit/apply_patch) лизует ТОТ
    САМЫЙ файл, который правит -- это 99% записей агента и главная защита;
  * shell-инструмент без OS isolation ВСЕГДА блокируется. Статический PreToolUse
    hook не может доказать startup/profile/env/config, полный набор outputs, поздний
    stdin/PTY, lifetime потомков и path identity. Разрешать по argv/manifest нельзя.
Почему так: лиза на ПАПКУ + `overlaps()`, матчащий предка в обе стороны, превращала
одну правку в получасовой замок на всю папку. Замер 14.09 после половинчатой утренней
правки: 198 блокировок, 137 (69%) -- запрос ПАПКИ, 86 из них `~/.claude/scripts`,
36 пострадавших сессий, включая ЧТЕНИЕ файла и `cd`, который запирал сессию насмерть.
Вернуть shell execution можно только отдельной рельсой, которая делает shared MAIN
недоступным/readonly и владеет всем process tree до завершения. Worktree и scratch
не являются такой изоляцией. UNC/device/volume spellings и существующие hardlink
aliases для file-tools fail-closed: pathname lease не доказывает physical identity.
Межмашинной защиты здесь нет: SQLite -- mutex только этого узла; между машинами остаются
On Air/шина/worktree ownership. Извлечение абсолютного пути здесь Windows-only
(`C:\\...`); перенос этого hook на Unix без отдельного path-parser не защищает `/tmp/...`.

Input: hook JSON on stdin. Output: silence on allow; Claude deny is stderr + rc=2,
while Codex payloads with turn/tool ids receive structured deny on stdout + rc=0.
Caller: trusted `constitution_guard.cmd` (PreToolUse), direct `--phase stop`
SubagentStop registration, and `turnstate_hook.py` (root Stop).
Rail: local Python + `scripts/workspace_write_lease.py`, 0 LLM, 0 network.
Test: `_test_workspace_write_guard_fail_closed.py` (new contract),
`_test_lease_storm.py` and `_test_workspace_write_lease.py` (provider).
updated: 2026-09-22
"""
from __future__ import annotations

import argparse
import json
import os
import re
import sys
from dataclasses import dataclass, field
from pathlib import Path

SCRIPTS = os.environ.get("WORKSPACE_WRITE_LEASE_MODULE_DIR") or os.path.join(
    os.path.expanduser("~"), ".claude", "scripts")
if SCRIPTS not in sys.path:
    sys.path.insert(0, SCRIPTS)
import workspace_write_lease as lease  # noqa: E402

FILE_TOOLS = {"write", "edit", "multiedit", "notebookedit", "apply_patch"}
SHELL_TOOLS = {"bash", "powershell", "shell", "exec_command"}
PATCH_PATH = re.compile(
    r"^\*\*\* (?:Update|Add|Delete) File:\s*(.+?)\s*$|^\*\*\* Move to:\s*(.+?)\s*$",
    re.MULTILINE)
SHELL_MUTATION = re.compile(
    r"(?i)(?:\b(?:set-content|add-content|out-file|new-item|remove-item|move-item|"
    r"copy-item|rename-item|clear-content|tee-object|tee|rm|del|erase|mv|cp|touch|"
    r"truncate)\b|\bsed\s+-[^\r\n]*i\b|\bperl\s+-[^\r\n]*p?i\b|"
    r"\bgit\s+apply\b|(?:^|\s)patch(?:\s|$)|(?<![<>])>{1,2}(?![>&]))")
POWERSHELL_WRITE_ALIASES = {
    "ac", "clc", "copy", "cpi", "mi", "move", "ni", "rd", "ri", "rmdir",
    "ren", "rni", "sc",
}
POWERSHELL_WRITE_ALIAS_COMMAND = re.compile(
    r"(?i)(?:^|[;|&{}\r\n])\s*(?:ac|clc|copy|cpi|mi|move|ni|rd|ri|rmdir|"
    r"ren|rni|sc)(?=\s|$)")
ENV_ASSIGNMENT = re.compile(r"^[A-Za-z_][A-Za-z0-9_]*=.*$", re.DOTALL)
NULL_REDIRECTION = re.compile(
    r"(?i)(?<!\S)(?:\d|\*)?>\s*(?:\$null\b|nul\b|/dev/null\b)")
ABS_QUOTED = re.compile(r"[\"']([A-Za-z]:[\\/][^\"'\r\n]+)[\"']")
ABS_BARE = re.compile(r"(?<![\w])([A-Za-z]:[\\/][^\s\"'|&;<>]+)")
SED_WRITE_ABS = re.compile(
    r"(?i)(?:^|[\s;\"'])w\s+([A-Za-z]:[\\/][^\"'\r\n;]+)")
SEGMENT_SPLIT = re.compile(r"\|\||&&|[;|\r\n]")
# Чтение -- не запись. Словарь намеренно широкий: это ровно те команды, которыми наши
# сессии ЧИТАЮТ файлы в bypass-режиме (например cat/head/Get-Content), и
# каждая из них, не попав сюда, брала 30-минутную лизу ЗАПИСИ на читаемый файл.
# Команды с собственным языком/писательскими режимами (sed/awk/find/sort/env) сюда
# намеренно не входят: безопаснее точная консервативная лиза, чем prefix-allow bypass.
READ_ONLY_COMMAND = re.compile(
    r"(?i)^(?:"
    r"git\s+(?:status|diff|log|show|rev-parse|ls-files|check-ignore|cat-file)\b|"
    r"rg\b|grep\b|egrep\b|fgrep\b|findstr\b|ls\b|dir\b|pwd\b|cd\b|whoami\b|"
    r"where\b|which\b|type\b|cat\b|head\b|tail\b|cut\b|"
    r"uniq\b|tr\b|wc\b|jq\b|diff\b|stat\b|echo\b|printf\b|"
    r"printenv\b|basename\b|dirname\b|realpath\b|readlink\b|"
    r"du\b|df\b|"
    r"get-content\b|get-childitem\b|get-child-item\b|get-item\b|get-filehash\b|"
    r"get-command\b|get-location\b|get-date\b|get-process\b|get-service\b|"
    r"get-ciminstance\b|"
    r"test-path\b|resolve-path\b|select-string\b|"
    r"select-object\b|where-object\b|sort-object\b|measure-object\b|"
    r"format-table\b|format-list\b|out-string\b|write-output\b|write-host\b|"
    r"more(?:\.com)?\b|certutil(?:\.exe)?(?:\s+-[^\s]+)*\s+-hashfile\b"
    r")")


@dataclass
class Intent:
    mutating: bool
    paths: list[str] = field(default_factory=list)
    reason: str = ""


@dataclass
class Decision:
    ok: bool
    reason: str = ""
    paths: list[str] = field(default_factory=list)


def tool_name(payload):
    return str(payload.get("tool_name") or payload.get("tool") or "").strip()


def _shell_dialect(tool):
    """Quoting belongs to the outer tool, not to the child command it launches."""
    tool = str(tool or "").strip().lower()
    if tool == "bash":
        return "posix"
    if tool == "powershell":
        return "powershell"
    # Generic exec/shell tools use the platform default in this Windows-local
    # guard. Keep the branch explicit so the same source is honest on a POSIX host.
    return "powershell" if os.name == "nt" else "posix"
--- DIFF ---
diff --git a/workspace_write_guard.py b/workspace_write_guard.py
index fedd4ba..561477e 100644
--- a/workspace_write_guard.py
+++ b/workspace_write_guard.py
@@ -4,24 +4,20 @@
 Purpose: translate both harness payloads into one atomic local file lease. Codex
 reports canonical `apply_patch`; Claude reports Write/Edit/MultiEdit/NotebookEdit.
 
-Контракт лизы в две строки (14.09.2026, починка класса lease-storm):
+Контракт лизы (22.09.2026, fail-closed после opaque-process incident):
   * файловый инструмент (Write/Edit/MultiEdit/NotebookEdit/apply_patch) лизует ТОТ
     САМЫЙ файл, который правит -- это 99% записей агента и главная защита;
-  * shell лизует ТОЛЬКО абсолютные файлы, которые НАЗЫВАЕТ. Видимый writer (`>`,
-    `sed -i`, `rm`, `tee`, `Set-Content`, ...) делает это явно; неизвестная форма с
-    named exact file лизуется консервативно. cwd/каталог не лизуются НИКОГДА,
-    доказанная читающая команда не лизует ничего, а запускаемая программа (первый
-    токен сегмента) целью записи не считается.
+  * shell-инструмент без OS isolation ВСЕГДА блокируется. Статический PreToolUse
+    hook не может доказать startup/profile/env/config, полный набор outputs, поздний
+    stdin/PTY, lifetime потомков и path identity. Разрешать по argv/manifest нельзя.
 Почему так: лиза на ПАПКУ + `overlaps()`, матчащий предка в обе стороны, превращала
 одну правку в получасовой замок на всю папку. Замер 14.09 после половинчатой утренней
 правки: 198 блокировок, 137 (69%) -- запрос ПАПКИ, 86 из них `~/.claude/scripts`,
 36 пострадавших сессий, включая ЧТЕНИЕ файла и `cd`, который запирал сессию насмерть.
-Честные дыры: файл, который дочерний скрипт пишет, но НЕ НАЗЫВАЕТ в командной строке
-(`python build.py`), не виден. Динамический writer с названным абсолютным файлом всё
-равно получает консервативную точную лизу; без названной цели остаётся той же дырой.
-Видимый writer с относительной целью не пропускается: guard не знает mutex-ключа и
-fail-closed блокирует команду. Неизвестная команда с абсолютным файлом лизует этот
-файл; только доказанные reader-формы и команды без точной файловой цели идут без лизы.
+Вернуть shell execution можно только отдельной рельсой, которая делает shared MAIN
+недоступным/readonly и владеет всем process tree до завершения. Worktree и scratch
+не являются такой изоляцией. UNC/device/volume spellings и существующие hardlink
+aliases для file-tools fail-closed: pathname lease не доказывает physical identity.
 Межмашинной защиты здесь нет: SQLite -- mutex только этого узла; между машинами остаются
 On Air/шина/worktree ownership. Извлечение абсолютного пути здесь Windows-only
 (`C:\\...`); перенос этого hook на Unix без отдельного path-parser не защищает `/tmp/...`.
@@ -31,9 +27,9 @@ while Codex payloads with turn/tool ids receive structured deny on stdout + rc=0
 Caller: trusted `constitution_guard.cmd` (PreToolUse), direct `--phase stop`
 SubagentStop registration, and `turnstate_hook.py` (root Stop).
 Rail: local Python + `scripts/workspace_write_lease.py`, 0 LLM, 0 network.
-Test: `_test_lease_storm.py` (класс), `_test_workspace_write_guard.py`,
-`_test_workspace_write_lease.py`.
-updated: 2026-09-21
+Test: `_test_workspace_write_guard_fail_closed.py` (new contract),
+`_test_lease_storm.py` and `_test_workspace_write_lease.py` (provider).
+updated: 2026-09-22
 """
 from __future__ import annotations
 
@@ -183,6 +179,14 @@ def _resolve(value, cwd):
     return lease.norm_path(value, cwd=cwd)
 
 
+def _unsafe_path_namespace(value):
+    """Path spellings whose physical identity a pathname lease cannot prove."""
+    raw = str(value or "").strip().replace("/", "\\")
+    return bool(
+        raw.startswith("\\\\") or
+        raw.lower().startswith(("\\??\\", "\\device\\", "\\global??\\")))
+
+
 def _safe_resolve(value, cwd):
     """norm_path, но мусорный токен даёт "" вместо исключения (парсим сырой shell)."""
     try:
@@ -728,6 +732,8 @@ def extract_intent(payload):
                 raw_paths.append(next(group for group in match.groups() if group is not None))
         paths = []
         for value in raw_paths:
+            if _unsafe_path_namespace(value):
+                return Intent(True, [], "unsafe-path-namespace")
             try:
                 paths.append(_resolve(value, cwd))
             except Exception:
@@ -825,6 +831,19 @@ def _codex_shared_checkout_shell_write(payload, intent=None):
 
 
 def guard_pre(payload):
+    tool = tool_name(payload).lower()
+    if tool in SHELL_TOOLS:
+        reason = (
+            "unisolated shell execution is forbidden: a static PreToolUse/Stop "
+            "guard cannot prove startup env/profile/config, complete outputs, "
+            "path identity, later stdin/PTY input, or process-tree lifetime; "
+            "use an exact file tool or a separate OS-isolated execution rail")
+        lease.count_event("hook", "blocked-unisolated-shell",
+                          {"tool": tool_name(payload),
+                           "session": session_id(payload),
+                           "resources": []})
+        return Decision(False, reason, [])
+
     # Protocol rule 3 is structural, not a writer-keyword list: in a shared Git
     # main checkout Codex shell is a read-only rail. Unknown/non-reader commands
     # must use apply_patch even when their output is hidden or relative.
@@ -842,7 +861,26 @@ def guard_pre(payload):
         return Decision(True, intent.reason, [])
     if not intent.paths:
         lease.count_event("hook", "blocked-unparsed", {"tool": tool_name(payload)})
-        return Decision(False, "write intent found, but target path could not be parsed", [])
+        detail = (": %s" % intent.reason) if intent.reason else ""
+        return Decision(
+            False, "write intent found, but target path could not be parsed%s" % detail, [])
+    for target in intent.paths:
+        if not os.path.exists(target) or os.path.isdir(target):
+            continue
+        try:
+            if os.stat(target).st_nlink > 1:
+                lease.count_event(
+                    "hook", "blocked-hardlink-alias",
+                    {"tool": tool_name(payload),
+                     "session": session_id(payload),
+                     "resources": [target]})
+                return Decision(
+                    False,
+                    "existing hardlink aliases cannot be fenced by pathname",
+                    [target])
+        except OSError:
+            return Decision(
+                False, "existing output identity could not be proven", [target])
     sid = session_id(payload)
     if not sid:
         lease.count_event("hook", "blocked-no-session", {"tool": tool_name(payload)})

---

**Claude:**

## Review — workspace_write_guard.py (fail-closed shell block + UNC/hardlink hardening)

**Scope note:** reviewing only the supplied excerpt + diff, no tool access, so anything outside the shown lines (rest of `extract_intent`, `session_id`, `lease.norm_path`) is treated as unverified.

### Resolved from prior review
`tool_name()` always returns `str(...).strip()`, defaulting to `""` — it can never be `None`. `SHELL_TOOLS` entries are already lowercase, and `guard_pre` now does `tool = tool_name(payload).lower()` before the membership test, so case mismatches (e.g. Claude reporting `"Bash"`) are normalized correctly. Both prior concerns are non-issues in this version.

### Findings

1. **Dead code left behind by the policy change (low severity, correctness-neutral).**
   `guard_pre` now unconditionally returns `Decision(False, ...)` for any tool in `SHELL_TOOLS` before the "Protocol rule 3" structural check, `extract_intent`'s shell-parsing branch, and `_codex_shared_checkout_shell_write` ever run. All the shell-oriented machinery — `SHELL_MUTATION`, `READ_ONLY_COMMAND`, `POWERSHELL_WRITE_ALIASES`/`POWERSHELL_WRITE_ALIAS_COMMAND`, `ABS_QUOTED`/`ABS_BARE`, `SED_WRITE_ABS`, `ENV_ASSIGNMENT`, `NULL_REDIRECTION`, `SEGMENT_SPLIT`, `_shell_dialect` — is now unreachable for `SHELL_TOOLS` payloads. Not a functional bug (early return is correct and fail-closed), but in a security-critical guard, live-looking dead code is a hazard: a future edit that reorders or narrows the new top-of-function block could silently reactivate the old permissive read/write parsing without anyone noticing it was supposed to be retired. Worth pruning or at least commenting "unreachable, kept for X" to avoid confusing the next editor.

2. **Unverified completeness of the new UNC/device-path and hardlink defenses (plausible, not confirmed).**
   `_unsafe_path_namespace()` is only shown wired into the `raw_paths` loop that appears (via `PATCH_PATH`/multi-match handling) to be the `apply_patch` branch of `extract_intent`. The docstring claims the fail-closed UNC/device/hardlink protection applies to "file-tools" broadly, but the excerpt doesn't show whether the single-path branch used for plain `Write`/`Edit`/`MultiEdit`/`NotebookEdit` (`tool_input.file_path` → `_resolve`) runs through the same `_unsafe_path_namespace` gate before calling `_resolve`/`norm_path`. If that branch resolves the raw path directly without the new guard, an agent could hand `Write` a `\\?\`, `\??\`, or `\Device\`-spelled target and bypass exactly the physical-identity fencing this change is meant to close — for the tool class that represents "99% of the agent's file writes" per the docstring's own framing. I can't confirm this from the given fragment; it needs to be checked against the rest of `extract_intent` before treating the new protection as covering all file tools.

Everything else in the diff is internally consistent: the shell-block reason string, the `count_event` telemetry, the `intent.reason` propagation into the "could not be parsed" deny message, and the hardlink `st_nlink > 1` check (with fail-closed `OSError` handling) all wire together correctly and match the stated contract.

FINAL_VERDICT: APPROVE
