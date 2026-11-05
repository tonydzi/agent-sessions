---
session: s_d3a2a6a0
date: 2026-09-22
words: 1467
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · diff --git a/workspace_write_guard.py b/workspace_write_guard.py

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d3a2a6a0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

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

## Review: workspace_write_guard.py

**Scope:** Reviewed only the diff. Net effect: shell tools are now unconditionally denied at the top of `guard_pre`, a new `_unsafe_path_namespace` check blocks UNC/NT-device path spellings during path extraction, and a new hardlink-alias check denies writes to existing files with `st_nlink > 1`.

### Findings

**1. [High] Unverified null/case-safety on the sole enforcement point of the new contract — `guard_pre`, top of function**
```python
tool = tool_name(payload).lower()
if tool in SHELL_TOOLS:
```
This line is now the entire security guarantee described in the module docstring ("shell-инструмент без OS isolation ВСЕГДА блокируется"). Two risks, neither verifiable from the diff alone:
- If `tool_name(payload)` can return `None` for a malformed/unrecognized payload (plausible — elsewhere in the retained code, e.g. `{"tool": tool_name(payload)}` is logged raw without a `.lower()` or null-guard, suggesting the rest of the file doesn't assume it's always a non-empty string), `.lower()` raises `AttributeError`. Whether the calling harness then fails open (executes the shell command anyway) or fails closed is not shown here, but an unhandled exception at the very first line of a fail-closed gate is exactly the kind of thing that silently defeats it.
- `tool in SHELL_TOOLS` assumes every entry in `SHELL_TOOLS` is already lowercase. `SHELL_TOOLS` isn't defined in this diff, so its casing can't be confirmed. If any entry is mixed-case, the lowered `tool` will never match it and that shell tool slips through the new gate entirely — a silent fail-open on the diff's headline change.
Given this is billed as an unconditional fail-closed gate, both need explicit verification (or a defensive `tool_name(payload) or ""` and a confirmed-lowercase `SHELL_TOOLS`) before trusting the contract.

**2. [Medium] Likely dead code left behind the new early-return — `guard_pre`, after the SHELL_TOOLS block**
The retained comment/logic immediately below ("Protocol rule 3 is structural... Codex shell is a read-only rail... `intent = extract_intent(payload)`") and the shell-argv-parsing branch inside `extract_intent` (the `raw_paths` regex loop that the new `_unsafe_path_namespace` check was spliced into) appear to only ever have been reachable for shell-tool payloads. If `SHELL_TOOLS` covers everything that previously drove that parsing path, this logic is now unreachable in production — it still "works" but is dead weight that can rot silently or mislead a future maintainer into thinking shell writes are still discriminated by writer-keyword instead of blanket-denied. Worth confirming and trimming, or leaving an explicit comment noting it's intentionally retained (e.g. for tests/other callers).

**3. [Low] TOCTOU / redundant check in the new hardlink-alias loop — `guard_pre`, new `for target in intent.paths` block**
```python
if not os.path.exists(target) or os.path.isdir(target):
    continue
try:
    if os.stat(target).st_nlink > 1:
```
`os.path.exists` and the subsequent `os.stat` are two separate syscalls; the file can be created/removed/replaced between them. Not a security hole here since the `except OSError` branch already fails closed on a vanished file, but the `exists()` pre-check is redundant (a bare `try: os.stat(...) except OSError: continue`-or-deny would be simpler and race-free) — matches the file's own AK-47/simplicity intent stated elsewhere in the module's comments.

**4. [Low] Hardlink check doesn't cover symlinks/reparse points — same block**
The stated goal is "pathname lease does not prove physical identity." `st_nlink` only catches hardlink aliasing; a symlink or NTFS junction at `target` pointing at a different physical file has `st_nlink` of 1 on the link's resolved target and would pass through unflagged, while `os.stat` (which follows the link) silently resolves to a different physical file than the leased pathname. This may be intentionally out of scope (docstring says "existing hardlink aliases," not symlinks), but if the broader goal is "path identity," it's an open gap worth calling out explicitly rather than leaving implicit.

**5. [Info] `_unsafe_path_namespace` coverage looks correct** — `\\` (UNC and `\\?\`/`\\.\` device forms both start with two backslashes so both are caught), `\??\`, `\Device\`, `\GLOBAL??\` are all covered case-insensitively. No issue found here.

### Verdict rationale
The direction of the change (fail-closed shell denial, UNC/device-path rejection, hardlink-alias rejection) is sound and matches the stated contract. But finding #1 sits directly on the critical path of that contract's enforcement and cannot be confirmed safe from the diff alone — a `None`/mixed-case slip here silently reopens exactly the hole this diff exists to close. That, combined with the likely dead code in #2, is enough to ask for a second pass before merging.

FINAL_VERDICT: REQUEST_CHANGES
