---
session: s_1b42f78a
date: 2026-08-24
words: 43205
turns: 69
tools: "Bash, Edit, Grep, PowerShell, Read, Skill, ToolSearch, Write, mcp__scheduled-tasks__create_scheduled_task, mcp__scheduled-tasks__update_scheduled_task, mcp__telegram__get_history"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-08-24 · изучи этот комп и скажи какую рабочую папку мне стоит выбирать при старте новой сессии

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1b42f78a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

изучи этот комп и скажи какую рабочую папку мне стоит выбирать при старте новой сессии

---

**Claude:**

понедельник, утро, 08:37, 24 августа 2026

🎙 Майк: вопрос правильный — рабочая папка задаёт, какие CLAUDE.md и память подхватятся. Сейчас гляну, что на диске, и дам вердикт.

---

> `PowerShell` -- {"command": "Get-ChildItem E:\\ -Directory | Select-Object Name; Write-Host '---'; Get-ChildItem 'E:\\!CLAUDE-HUBPC-June26' | Select-Object Name, Length -First 40", "description": "List E:\\ root and current working folder contents"}

---

> `PowerShell` -- {"command": "Get-ChildItem C:\\Users\\dev\\.claude\\projects -Directory | ForEach-Object { $n=$_.Name; $c=(Get-ChildItem $_.FullName -Filter *.jsonl -ErrorAction SilentlyContinue | Measure-Object).Count; $last=(Get-ChildItem $_.FullName -Filter *.jsonl -ErrorAction SilentlyContinue | Sort-Object L

---

**Claude:**

Изучил. Ответ короткий: **`E:\!CLAUDE-HUBPC-June26`** — именно её и стоит выбирать при старте новой сессии на этом компе. Это уже настроенная «домашняя база» Claude на хабе:

- В ней лежит проектная память: индекс `MEMORY.md` и папка memory с десятками правил подгружаются в каждую сессию **только** когда сессия стартует из этой папки. Стартуешь из другой — я «просыпаюсь» без этих знаний.
- Там же живут `AGENTS.md`, шина (`aibus_*.py`), архивы сессий, секреты, локальный `.claude` — вся инфраструктура флота.
- К ней уже прикручены дополнительные рабочие директории: волт `D:\Vault\Vault-Knowledge`, `D:\Vault\_imports` и `C:\Users\dev\.claude` — то есть из неё я вижу и волт, и скрипты без лишних разрешений.

Что показала статистика реальных запусков: в этой папке 1921 сессия (живая, последняя — сегодня), но при этом 4370 сессий запущены из `C:\Users\dev` и ещё 2420 из `C:\Windows\System32` — это сессии, стартовавшие «где попало» (дефолт терминала или админ-шелл). Они работали без проектной памяти этой папки. То есть больше половины сессий на машине исторически запускались из неправильного места.

Исключения, когда папка другая оправдана:
- Работа чисто над скриптами импорта → `D:\Vault\_imports` (там своя накатанная история, 299 сессий).
- Конкретный git-репозиторий (например, в `E:\GitHub\...`) → можно стартовать в нём, если работа целиком про этот репо.

🎙 Майк: вижу системную дыру — тысячи сессий из System32 и домашней папки значит, что ярлык/терминал по умолчанию открывается не там. Хочешь, починю: сделаю так, чтобы терминал и ярлык Claude на этом компе всегда открывались в `E:\!CLAUDE-HUBPC-June26`?

🧒 Простыми словами: у Claude на этом компе есть «своя комната», где лежат все его записки и инструменты — `E:\!CLAUDE-HUBPC-June26`. Если запустить его в другой комнате, он не найдёт свои записки и будет глупее. Выбирай всегда её.

---

**User:**

а если я случайно выберу другую папку? поставь в нее ХУК \ напоминалку что если СЛУЧАЙНО включиться клод в другой папке - чтобы он ЭТО ПОНЯЛ - ВОЗМОЖНО??

---

**Claude:**

понедельник, утро, 08:40, 24 августа 2026

🎙 Майк: возможно, и даже лучше, чем ты просишь: хук ставится не «в каждую папку» (их бесконечно), а один глобальный — он срабатывает при старте **любой** сессии на этой машине и сам проверяет «я в правильной папке?». Делаю.

---

> `Skill` -- {"skill": "update-config", "args": "Add a SessionStart hook (user-level settings) that warns when Claude starts in a non-canonical working directory on this machine"}

---

**User:**

# Update Config Skill

Modify Claude Code configuration by updating settings.json files.

## When Hooks Are Required (Not Memory)

If the user wants something to happen automatically in response to an EVENT, they need a **hook** configured in settings.json. Memory/preferences cannot trigger automated actions.

**These require hooks:**
- "Before compacting, ask me what to preserve" → PreCompact hook
- "After writing files, run prettier" → PostToolUse hook with Write|Edit matcher
- "When I run bash commands, log them" → PreToolUse hook with Bash matcher
- "Always run tests after code changes" → PostToolUse hook

**Hook events:** PreToolUse, PostToolUse, PreCompact, PostCompact, Stop, Notification, SessionStart

## CRITICAL: Read Before Write

**Always read the existing settings file before making changes.** Merge new settings with existing ones - never replace the entire file.

## CRITICAL: Use AskUserQuestion for Ambiguity

When the user's request is ambiguous, use AskUserQuestion to clarify:
- Which settings file to modify (user/project/local)
- Whether to add to existing arrays or replace them
- Specific values when multiple options exist

## Decision: /config command vs Direct Edit

**Suggest the `/config` slash command** for these simple settings:
- `theme`, `editorMode`, `verbose`, `model`
- `language`, `alwaysThinkingEnabled`
- `permissions.defaultMode`

**Edit settings.json directly** for:
- Hooks (PreToolUse, PostToolUse, etc.)
- Complex permission rules (allow/deny arrays)
- Environment variables
- MCP server configuration
- Plugin configuration

## Workflow

1. **Clarify intent** - Ask if the request is ambiguous
2. **Read existing file** - Use Read tool on the target settings file
3. **Merge carefully** - Preserve existing settings, especially arrays
4. **Edit file** - Use Edit tool (if file doesn't exist, ask user to create it first)
5. **Confirm** - Tell user what was changed

## Merging Arrays (Important!)

When adding to permission arrays or hook arrays, **merge with existing**, don't replace:

**WRONG** (replaces existing permissions):
```json
{ "permissions": { "allow": ["Bash(npm *)"] } }
```

**RIGHT** (preserves existing + adds new):
```json
{
  "permissions": {
    "allow": [
      "Bash(git *)",      // existing
      "Edit(.claude)",    // existing
      "Bash(npm *)"       // new
    ]
  }
}
```

## Settings File Locations

Choose the appropriate file based on scope:

| File | Scope | Git | Use For |
|------|-------|-----|---------|
| `~/.claude/settings.json` | Global | N/A | Personal preferences for all projects |
| `.claude/settings.json` | Project | Commit | Team-wide hooks, permissions, plugins |
| `.claude/settings.local.json` | Project | Gitignore | Personal overrides for this project |

Settings load in order: user → project → local (later overrides earlier).

## Settings Schema Reference

### Permissions
```json
{
  "permissions": {
    "allow": ["Bash(npm *)", "Edit(.claude)", "Read"],
    "deny": ["Bash(rm -rf *)"],
    "ask": ["Edit(//etc/*)"],
    "defaultMode": "default" | "plan" | "acceptEdits" | "dontAsk",
    "additionalDirectories": ["/extra/dir"]
  }
}
```

**Permission Rule Syntax:**
- Exact match: `"Bash(npm run test)"`
- Prefix wildcard: `"Bash(git *)"` - matches `git`, `git status`, `git commit`, etc.
- Tool only: `"Read"` - allows all Read operations

### Environment Variables
```json
{
  "env": {
    "DEBUG": "true",
    "MY_API_KEY": "value"
  }
}
```

### Model & Agent
```json
{
  "model": "sonnet",  // or "fable", "opus", "haiku", full model ID
  "agent": "agent-name",
  "alwaysThinkingEnabled": true
}
```

### Attribution (Commits & PRs)
```json
{
  "attribution": {
    "commit": "Custom commit trailer text",
    "pr": "Custom PR description text"
  }
}
```
Set `commit` or `pr` to empty string `""` to hide that attribution.

### MCP Server Management
```json
{
  "enableAllProjectMcpServers": true,
  "enabledMcpjsonServers": ["server1", "server2"],
  "disabledMcpjsonServers": ["blocked-server"]
}
```

### Plugins
```json
{
  "enabledPlugins": {
    "formatter@anthropic-tools": true
  }
}
```
Plugin syntax: `plugin-name@source` where source is `claude-code-marketplace`, `claude-plugins-official`, or `builtin`.

### Other Settings
- `language`: Preferred response language (e.g., "japanese")
- `cleanupPeriodDays`: Days to keep transcripts before automatic cleanup (default: 30; minimum 1)
- `respectGitignore`: Whether to respect .gitignore (default: true)
- `spinnerTipsEnabled`: Show tips in spinner
- `spinnerVerbs`: Customize spinner verbs (`{ "mode": "append" | "replace", "verbs": [...] }`)
- `spinnerTipsOverride`: Override spinner tips (`{ "excludeDefault": true, "tips": ["Custom tip"] }`)
- `syntaxHighlightingDisabled`: Disable diff highlighting


## Hooks Configuration

Hooks run commands at specific points in Claude Code's lifecycle.

### Hook Structure
```json
{
  "hooks": {
    "EVENT_NAME": [
      {
        "matcher": "ToolName|OtherTool",
        "hooks": [
          {
            "type": "command",
            "command": "your-command-here",
            "timeout": 60,
            "statusMessage": "Running..."
          }
        ]
      }
    ]
  }
}
```

### Hook Events

| Event | Matcher | Purpose |
|-------|---------|---------|
| PermissionRequest | Tool name | Run before permission prompt |
| PreToolUse | Tool name | Run before tool, can block |
| PostToolUse | Tool name | Run after successful tool |
| PostToolUseFailure | Tool name | Run after tool fails |
| Notification | Notification type | Run on notifications |
| Stop | - | Run when Claude stops (including clear, resume, compact) |
| PreCompact | "manual"/"auto" | Before compaction |
| PostCompact | "manual"/"auto" | After compaction (receives summary) |
| UserPromptSubmit | - | When user submits |
| SessionStart | - | When session starts |

**Common tool matchers:** `Bash`, `Write`, `Edit`, `Read`, `Glob`, `Grep`

### Hook Types

**1. Command Hook** - Runs a shell command:
```json
{ "type": "command", "command": "prettier --write $FILE", "timeout": 30 }
```

**2. Prompt Hook** - Evaluates a condition with LLM:
```json
{ "type": "prompt", "prompt": "Is this safe? $ARGUMENTS" }
```
Only available for tool events: PreToolUse, PostToolUse, PermissionRequest.

**3. Agent Hook** - Runs an agent with tools:
```json
{ "type": "agent", "prompt": "Verify tests pass: $ARGUMENTS" }
```
Only available for tool events: PreToolUse, PostToolUse, PermissionRequest.

### Hook Input (stdin JSON)
```json
{
  "session_id": "abc123",
  "tool_name": "Write",
  "tool_input": { "file_path": "/path/to/file.txt", "content": "..." },
  "tool_response": { "success": true }  // PostToolUse only
}
```

### Hook JSON Output

Hooks can return JSON to control behavior:

```json
{
  "systemMessage": "Warning shown to user in UI",
  "continue": false,
  "stopReason": "Message shown when blocking",
  "suppressOutput": false,
  "decision": "block",
  "reason": "Explanation for decision",
  "hookSpecificOutput": {
    "hookEventName": "PostToolUse",
    "additionalContext": "Context injected back to model"
  }
}
```

**Fields:**
- `systemMessage` - Display a message to the user (all hooks)
- `continue` - Set to `false` to block/stop (default: true)
- `stopReason` - Message shown when `continue` is false
- `suppressOutput` - Hide stdout from transcript (default: false)
- `decision` - "block" for PostToolUse/Stop/UserPromptSubmit hooks (deprecated for PreToolUse, use hookSpecificOutput.permissionDecision instead)
- `reason` - Explanation for decision
- `hookSpecificOutput` - Event-specific output (must include `hookEventName`):
  - `additionalContext` - Text injected into model context
  - `permissionDecision` - "allow", "deny", or "ask" (PreToolUse only)
  - `permissionDecisionReason` - Reason for the permission decision (PreToolUse only)
  - `updatedInput` - Modified tool input (PreToolUse only)

### Common Patterns

**Auto-format after writes:**
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write|Edit",
      "hooks": [{
        "type": "command",
        "command": "jq -r '.tool_response.filePath // .tool_input.file_path' | { read -r f; prettier --write \"$f\"; } 2>/dev/null || true"
      }]
    }]
  }
}
```

**Log all bash commands:**
```json
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{
        "type": "command",
        "command": "jq -r '.tool_input.command' >> ~/.claude/bash-log.txt"
      }]
    }]
  }
}
```

**Stop hook that displays message to user:**

Command must output JSON with `systemMessage` field:
```bash
# Example command that outputs: {"systemMessage": "Session complete!"}
echo '{"systemMessage": "Session complete!"}'
```

**Run tests after code changes:**
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write|Edit",
      "hooks": [{
        "type": "command",
        "command": "jq -r '.tool_input.file_path // .tool_response.filePath' | grep -E '\\.(ts|js)$' && npm test || true"
      }]
    }]
  }
}
```


## Constructing a Hook (with verification)

Given an event, matcher, target file, and desired behavior, follow this flow. Each step catches a different failure class — a hook that silently does nothing is worse than no hook.

1. **Dedup check.** Read the target file. If a hook already exists on the same event+matcher, show the existing command and ask: keep it, replace it, or add alongside.

2. **Construct the command for THIS project — don't assume.** The hook receives JSON on stdin. Build a command that:
   - Extracts any needed payload safely — use `jq -r` into a quoted variable or `{ read -r f; ... "$f"; }`, NOT unquoted `| xargs` (splits on spaces)
   - Invokes the underlying tool the way this project runs it (npx/bunx/yarn/pnpm? Makefile target? globally-installed?)
   - Skips inputs the tool doesn't handle (formatters often have `--ignore-unknown`; if not, guard by extension)
   - Stays RAW for now — no `|| true`, no stderr suppression. You'll wrap it after the pipe-test passes.

3. **Pipe-test the raw command.** Synthesize the stdin payload the hook will receive and pipe it directly:
   - `Pre|PostToolUse` on `Write|Edit`: `echo '{"tool_name":"Edit","tool_input":{"file_path":"<a real file from this repo>"}}' | <cmd>`
   - `Pre|PostToolUse` on `Bash`: `echo '{"tool_name":"Bash","tool_input":{"command":"ls"}}' | <cmd>`
   - `Stop`/`UserPromptSubmit`/`SessionStart`: most commands don't read stdin, so `echo '{}' | <cmd>` suffices

   Check exit code AND side effect (file actually formatted, test actually ran). If it fails you get a real error — fix (wrong package manager? tool not installed? jq path wrong?) and retest. Once it works, wrap with `2>/dev/null || true` (unless the user wants a blocking check).

4. **Write the JSON.** Merge into the target file (schema shape in the "Hook Structure" section above). If this creates `.claude/settings.local.json` for the first time, add it to .gitignore — the Write tool doesn't auto-gitignore it.

5. **Validate syntax + schema in one shot:**

   `jq -e '.hooks.<event>[] | select(.matcher == "<matcher>") | .hooks[] | select(.type == "command") | .command' <target-file>`

   Exit 0 + prints your command = correct. Exit 4 = matcher doesn't match. Exit 5 = malformed JSON or wrong nesting. A broken settings.json silently disables ALL settings from that file — fix any pre-existing malformation too.

6. **Prove the hook fires** — only for `Pre|PostToolUse` on a matcher you can trigger in-turn (`Write|Edit` via Edit, `Bash` via Bash). `Stop`/`UserPromptSubmit`/`SessionStart` fire outside this turn — skip to step 7.

   For a **formatter** on `PostToolUse`/`Write|Edit`: introduce a detectable violation via Edit (two consecutive blank lines, bad indentation, missing semicolon — something this formatter corrects; NOT trailing whitespace, Edit strips that before writing), re-read, confirm the hook **fixed** it. For **anything else**: temporarily prefix the command in settings.json with `echo "$(date) hook fired" >> /tmp/claude-hook-check.txt; `, trigger the matching tool (Edit for `Write|Edit`, a harmless `true` for `Bash`), read the sentinel file.

   **Always clean up** — revert the violation, strip the sentinel prefix — whether the proof passed or failed.

   **If proof fails but pipe-test passed and `jq -e` passed**: the settings watcher isn't watching `.claude/` — it only watches directories that had a settings file when this session started. The hook is written correctly. Tell the user to open `/hooks` once (reloads config) or restart — you can't do this yourself; `/hooks` is a user UI menu and opening it ends this turn.

7. **Handoff.** Tell the user the hook is live (or needs `/hooks`/restart per the watcher caveat). Point them at `/hooks` to review, edit, or disable it later. The UI only shows "Ran N hooks" if a hook errors or is slow — silent success is invisible by design.


## Example Workflows

### Adding a Hook

User: "Format my code after Claude writes it"

1. **Clarify**: Which formatter? (prettier, gofmt, etc.)
2. **Read**: `.claude/settings.json` (or create if missing)
3. **Merge**: Add to existing hooks, don't replace
4. **Result**:
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write|Edit",
      "hooks": [{
        "type": "command",
        "command": "jq -r '.tool_response.filePath // .tool_input.file_path' | { read -r f; prettier --write \"$f\"; } 2>/dev/null || true"
      }]
    }]
  }
}
```

### Adding Permissions

User: "Allow npm commands without prompting"

1. **Read**: Existing permissions
2. **Merge**: Add `Bash(npm *)` to allow array
3. **Result**: Combined with existing allows

### Environment Variables

User: "Set DEBUG=true"

1. **Decide**: User settings (global) or project settings?
2. **Read**: Target file
3. **Merge**: Add to env object
```json
{ "env": { "DEBUG": "true" } }
```

## Common Mistakes to Avoid

1. **Replacing instead of merging** - Always preserve existing settings
2. **Wrong file** - Ask user if scope is unclear
3. **Invalid JSON** - Validate syntax after changes
4. **Forgetting to read first** - Always read before write

## Troubleshooting Hooks

If a hook isn't running:
1. **Check the settings file** - Read ~/.claude/settings.json or .claude/settings.json
2. **Verify JSON syntax** - Invalid JSON silently fails
3. **Check the matcher** - Does it match the tool name? (e.g., "Bash", "Write", "Edit")
4. **Check hook type** - Is it "command", "prompt", or "agent"?
5. **Test the command** - Run the hook command manually to see if it works
6. **Use --debug** - Run `claude --debug` to see hook execution logs


## Full Settings JSON Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "$schema": {
      "description": "JSON Schema reference for Claude Code settings",
      "type": "string"
    },
    "apiKeyHelper": {
      "description": "Path to a script that outputs authentication values",
      "type": "string"
    },
    "proxyAuthHelper": {
      "description": "Shell command that outputs a Proxy-Authorization header value (EAP)",
      "type": "string"
    },
    "awsCredentialExport": {
      "description": "Path to a script that exports AWS credentials",
      "type": "string"
    },
    "awsAuthRefresh": {
      "description": "Path to a script that refreshes AWS authentication",
      "type": "string"
    },
    "gcpAuthRefresh": {
      "description": "Command to refresh GCP authentication (e.g., gcloud auth application-default login)",
      "type": "string"
    },
    "processWrapper": {
      "description": "Corporate launcher argv prefix for the background-agent supervisor, the sessions and workers it hosts, and the other covered background processes listed in the Claude Code corporate-launcher documentation. Equivalent to the CLAUDE_CODE_PROCESS_WRAPPER environment variable, which takes precedence when set. Honored from managed settings, a --settings/SDK-supplied settings file, and user settings, in that precedence order; project and local settings are ignored.",
      "type": "string"
    },
    "policyHelper": {
      "description": "Executable that computes managed settings at startup. Honored only from admin-controlled policy sources.",
      "type": "object",
      "properties": {
        "path": {
          "description": "Absolute path to the helper executable",
          "type": "string"
        },
        "timeoutMs": {
          "type": "integer",
          "minimum": 1000,
          "maximum": 9007199254740991
        },
        "refreshIntervalMs": {
          "anyOf": [
            {
              "type": "number",
              "const": 0
            },
            {
              "type": "integer",
              "minimum": 60000,
              "maximum": 9007199254740991
            }
          ]
        }
      },
      "required": [
        "path"
      ]
    },
    "fileSuggestion": {
      "description": "Custom file suggestion configuration for @ mentions",
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "const": "command"
        },
        "command": {
          "type": "string"
        }
      },
      "required": [
        "type",
        "command"
      ]
    },
    "respectGitignore": {
      "description": "Whether file picker should respect .gitignore files (default: true). Note: .ignore files are always respected.",
      "type": "boolean"
    },
    "cleanupPeriodDays": {
      "description": "Number of days to retain chat transcripts before automatic cleanup (default: 30). Minimum 1. Use a large value for long retention; use --no-session-persistence to disable transcript writes entirely.",
      "type": "integer",
      "exclusiveMinimum": 0,
      "maximum": 9007199254740991
    },
    "syncClaudeAiSkills": {
      "description": "Set to false to turn off syncing of the skills you have enabled on claude.ai. In your user settings (or managed settings): nothing more is downloaded, previously synced skills (~/.claude/skills/synced) can no longer be run, are hidden from every session started afterwards, and are moved to ~/.claude/skills/.trash at the next launch (deleted after cleanupPeriodDays; re-downloaded, not restored, if you re-enable). In .claude/settings.local.json or --settings: downloads stop and synced skills are blocked and hidden for sessions in that workspace or invocation only (nothing is moved). Not read from project settings (.claude/settings.json). Only false is honored — the feature is enabled server-side for your account, so setting true does not turn it on early. While it is on, synced skills are available in every session, re-synced every 10 minutes, and removed when you disable them on claude.ai. Only applies when signed in with your Claude account.",
      "type": "boolean"
    },
    "skillListingMaxDescChars": {
      "description": "Per-skill description character cap in the skill listing sent to Claude (default: 1536). Descriptions longer than this are truncated. Raise to opt in to higher per-turn context cost.",
      "type": "integer",
      "exclusiveMinimum": 0,
      "maximum": 9007199254740991
    },
    "skillListingBudgetFraction": {
      "description": "Fraction of the context window (in characters) reserved for the skill listing sent to Claude (default: 0.01 = 1%). When the listing exceeds this, descriptions are shortened to fit. Raise to opt in to higher per-turn context cost.",
      "type": "number",
      "exclusiveMinimum": 0,
      "maximum": 1
    },
    "wslInheritsWindowsSettings": {
      "description": "When set to true in either admin-only Windows source — the HKLM SOFTWARE/Policies/ClaudeCode registry key or C:/Program Files/ClaudeCode/managed-settings.json — WSL reads managed settings from the full Windows policy chain (HKLM, C:/Program Files/ClaudeCode via DrvFs, HKCU) in addition to /etc/claude-code. Windows sources take priority. The flag is also required in HKCU itself for HKCU policy to apply on WSL (double opt-in: admin enables the chain, user confirms HKCU). On native Windows the flag has no effect.",
      "type": "boolean"
    },
    "env": {
      "description": "Environment variables to set for Claude Code sessions",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "type": "string"
      }
    },
    "attribution": {
      "description": "Customize attribution text for commits and PRs. Each field defaults to the standard Claude Code attribution if not set.",
      "type": "object",
      "properties": {
        "commit": {
          "description": "Attribution text for git commits, including any trailers. Empty string hides attribution.",
          "type": "string"
        },
        "pr": {
          "description": "Attribution text for pull request descriptions. Empty string hides attribution.",
          "type": "string"
        },
        "sessionUrl": {
          "description": "Whether to append the claude.ai session link to commits and PRs created from web or Remote Control sessions (default: true). Set to false to omit the Claude-Session trailer and PR-body link.",
          "type": "boolean"
        }
      },
      "additionalProperties": {}
    },
    "includeCoAuthoredBy": {
      "description": "Deprecated: Use attribution instead. Whether to include Claude's co-authored by attribution in commits and PRs (defaults to true)",
      "type": "boolean"
    },
    "includeGitInstructions": {
      "description": "Include built-in commit and PR workflow instructions in Claude's system prompt (default: true)",
      "type": "boolean"
    },
    "permissions": {
      "description": "Tool usage permissions configuration",
      "type": "object",
      "properties": {
        "allow": {
          "description": "List of permission rules for allowed operations",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "deny": {
          "description": "List of permission rules for denied operations",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "ask": {
          "description": "List of permission rules that should always prompt for confirmation",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "defaultMode": {
          "description": "Default permission mode when Claude Code needs access ('manual' is accepted as an alias for 'default')",
          "type": "string",
          "enum": [
            "acceptEdits",
            "auto",
            "bypassPermissions",
            "default",
            "dontAsk",
            "plan"
          ]
        },
        "disableBypassPermissionsMode": {
          "description": "Disable the ability to bypass permission prompts",
          "type": "string",
          "enum": [
            "disable"
          ]
        },
        "disableAutoMode": {
          "description": "Disable auto mode",
          "type": "string",
          "enum": [
            "disable"
          ]
        },
        "additionalDirectories": {
          "description": "Additional directories to include in the permission scope",
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      },
      "additionalProperties": {}
    },
    "model": {
      "description": "Override the default model used by Claude Code",
      "type": "string"
    },
    "fallbackModel": {
      "description": "Fallback model(s) tried in order when the primary model is overloaded or unavailable. Each element accepts a model name or alias; \"default\" expands to the default model. CLI --fallback-model takes precedence.",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "availableModels": {
      "description": "Allowlist of models that users can select. Accepts family aliases (\"opus\" allows any opus version), version prefixes (\"opus-4-5\" allows only that version), and full model IDs. If undefined, all models are available. If empty array, only the default model is available. Typically set in managed settings by enterprise administrators.",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "enforceAvailableModels": {
      "description": "When true and availableModels is a non-empty array, the Default model selection is also constrained: if the default model for the user tier is not in availableModels, Default resolves to the first allowed availableModels entry instead. Has no effect when availableModels is unset or an empty array. Typically set in managed settings by enterprise administrators.",
      "type": "boolean"
    },
    "modelOverrides": {
      "description": "Override mapping from Anthropic model ID (e.g. \"claude-opus-4-6\") to provider-specific model ID (e.g. a Bedrock inference profile ARN). Typically set in managed settings by enterprise administrators.",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "type": "string"
      }
    },
    "enableAllProjectMcpServers": {
      "description": "Whether to automatically approve all MCP servers in the project",
      "type": "boolean"
    },
    "enabledMcpjsonServers": {
      "description": "List of approved MCP servers from .mcp.json",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "disabledMcpjsonServers": {
      "description": "List of rejected MCP servers from .mcp.json",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "disableClaudeAiConnectors": {
      "description": "When true in any settings source, claude.ai MCP cloud connectors are not auto-fetched or connected. Only gates auto-fetched connectors — a claudeai-proxy server passed explicitly (e.g. via --mcp-config or the SDK mcpServers option) still follows the normal MCP config trust flow. Any-source-true wins: a project can opt out, but a project-level false cannot override a user-level true.",
      "type": "boolean"
    },
    "skillOverrides": {
      "description": "Per-skill listing overrides keyed by skill name. \"name-only\" lists the skill without its description; \"user-invocable-only\" hides it from the model but keeps /name; \"off\" hides it from both. Absent = on.",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "type": "string",
        "enum": [
          "on",
          "name-only",
          "user-invocable-only",
          "off"
        ]
      }
    },
    "disableBundledSkills": {
      "description": "Disable the skills and workflows that ship with Claude Code: bundled skills and workflows are removed entirely; built-in slash commands stay typable but are hidden from the model. Plugins, .claude/skills/, and .claude/commands/ are unaffected. Equivalent to CLAUDE_CODE_DISABLE_BUNDLED_SKILLS=1.",
      "type": "boolean"
    },
    "allowedMcpServers": {
      "description": "Enterprise allowlist of MCP servers that can be used. Applies to all scopes including enterprise servers from managed-mcp.json. If undefined, all servers are allowed. If empty array, no servers are allowed. Denylist takes precedence - if a server is on both lists, it is denied.",
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "serverName": {
            "description": "Name of the MCP server that users are allowed to configure",
            "type": "string",
            "pattern": "^[a-zA-Z0-9_-]+$"
          },
          "serverCommand": {
            "description": "Command array [command, ...args] to match exactly for allowed stdio servers",
            "minItems": 1,
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "serverUrl": {
            "description": "URL pattern with wildcard support (e.g., \"https://*.example.com/*\") for allowed remote MCP servers",
            "type": "string"
          }
        }
      }
    },
    "deniedMcpServers": {
      "description": "Enterprise denylist of MCP servers that are explicitly blocked. If a server is on the denylist, it will be blocked across all scopes including enterprise. Denylist takes precedence over allowlist - if a server is on both lists, it is denied.",
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "serverName": {
            "description": "Name of the MCP server that is explicitly blocked",
            "type": "string",
            "minLength": 1
          },
          "serverCommand": {
            "description": "Command array [command, ...args] to match exactly for blocked stdio servers",
            "minItems": 1,
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "serverUrl": {
            "description": "URL pattern with wildcard support (e.g., \"https://*.example.com/*\") for blocked remote MCP servers",
            "type": "string"
          }
        }
      }
    },
    "hooks": {
      "description": "Custom commands to run before/after tool executions",
      "type": "object",
      "propertyNames": {
        "anyOf": [
          {
            "type": "string",
            "enum": [
              "PreToolUse",
              "PostToolUse",
              "PostToolUseFailure",
              "PostToolBatch",
              "Notification",
              "UserPromptSubmit",
              "UserPromptExpansion",
              "SessionStart",
              "SessionEnd",
              "Stop",
              "StopFailure",
              "SubagentStart",
              "SubagentStop",
              "PreCompact",
              "PostCompact",
              "PermissionRequest",
              "PermissionDenied",
              "Setup",
              "TeammateIdle",
              "TaskCreated",
              "TaskCompleted",
              "Elicitation",
              "ElicitationResult",
              "ConfigChange",
              "WorktreeCreate",
              "WorktreeRemove",
              "InstructionsLoaded",
              "CwdChanged",
              "FileChanged",
              "DirectoryAdded",
              "MessageDisplay"
            ]
          },
          {
            "not": {}
          }
        ]
      },
      "additionalProperties": {
        "type": "array",
        "items": {
          "type": "object",
          "properties": {
            "matcher": {
              "description": "String pattern to match (e.g. tool names like \"Write\")",
              "type": "string"
            },
            "hooks": {
              "description": "List of hooks to execute when the matcher matches",
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "type": {
                        "description": "Shell command hook type",
                        "type": "string",
                        "const": "command"
                      },
                      "command": {
                        "description": "Shell command to execute",
                        "type": "string"
                      },
                      "args": {
                        "description": "Argument list for exec form. When present, `command` is resolved as an executable and spawned directly with these arguments — no shell. Path placeholders like ${CLAUDE_PLUGIN_ROOT} are substituted per-element as plain strings, so paths with quotes, $, or backticks never reach a shell parser. When absent, `command` runs through a shell (bash on POSIX, PowerShell on Windows without Git Bash).",
                        "type": "array",
                        "items": {
                          "type": "string"
                        }
                      },
                      "if": {
                        "description": "Permission rule syntax to filter when this hook runs (e.g., \"Bash(git *)\"). Only runs if the tool call matches the pattern. Avoids spawning hooks for non-matching commands.",
                        "type": "string"
                      },
                      "shell": {
                        "description": "Shell interpreter. 'bash' uses your $SHELL (bash/zsh/sh); 'powershell' uses pwsh. Defaults to bash (powershell on Windows without Git Bash).",
                        "type": "string",
                        "enum": [
                          "bash",
                          "powershell"
                        ]
                      },
                      "timeout": {
                        "description": "Timeout in seconds for this specific command",
                        "type": "number",
                        "exclusiveMinimum": 0
                      },
                      "statusMessage": {
                        "description": "Custom status message to display in spinner while hook runs",
                        "type": "string"
                      },
                      "once": {
                        "description": "If true, hook runs once and is removed after execution",
                        "type": "boolean"
                      },
                      "async": {
                        "description": "If true, hook runs in background without blocking",
                        "type": "boolean"
                      },
                      "asyncRewake": {
                        "description": "If true, hook runs in background and wakes the model on exit code 2 (blocking error). Implies async.",
                        "type": "boolean"
                      }
                    },
                    "required": [
                      "type",
                      "command"
                    ]
                  },
                  {
                    "type": "object",
                    "properties": {
                      "type": {
                        "description": "LLM prompt hook type",
                        "type": "string",
                        "const": "prompt"
                      },
                      "prompt": {
                        "description": "Prompt to evaluate with LLM. Use $ARGUMENTS placeholder for hook input JSON.",
                        "type": "string"
                      },
                      "if": {
                        "description": "Permission rule syntax to filter when this hook runs (e.g., \"Bash(git *)\"). Only runs if the tool call matches the pattern. Avoids spawning hooks for non-matching commands.",
                        "type": "string"
                      },
                      "timeout": {
                        "description": "Timeout in seconds for this specific prompt evaluation",
                        "type": "number",
                        "exclusiveMinimum": 0
                      },
                      "model": {
                        "description": "Model to use for this prompt hook (e.g., \"claude-sonnet-5\"). If not specified, uses the default small fast model.",
                        "type": "string"
                      },
                      "continueOnBlock": {
                        "description": "Sets the continue value for the decision:\"block\" produced when ok is false. Default false (turn ends). Whether continue:true lets the turn proceed depends on the event's decision:\"block\" semantics. On PostToolUse, the reason is fed back to Claude and the turn continues.",
                        "type": "boolean"
                      },
                      "statusMessage": {
                        "description": "Custom status message to display in spinner while hook runs",
                        "type": "string"
                      },
                      "once": {
                        "description": "If true, hook runs once and is removed after execution",
                        "type": "boolean"
                      }
                    },
                    "required": [
                      "type",
                      "prompt"
                    ]
                  },
                  {
                    "type": "object",
                    "properties": {
                      "type": {
                        "description": "Agentic verifier hook type",
                        "type": "string",
                        "const": "agent"
                      },
                      "prompt": {
                        "description": "Prompt describing what to verify (e.g. \"Verify that unit tests ran and passed.\"). Use $ARGUMENTS placeholder for hook input JSON.",
                        "type": "string"
                      },
                      "if": {
                        "description": "Permission rule syntax to filter when this hook runs (e.g., \"Bash(git *)\"). Only runs if the tool call matches the pattern. Avoids spawning hooks for non-matching commands.",
                        "type": "string"
                      },
                      "timeout": {
                        "description": "Timeout in seconds for agent execution (default 60)",
                        "type": "number",
                        "exclusiveMinimum": 0
                      },
                      "model": {
                        "description": "Model to use for this agent hook (e.g., \"claude-sonnet-5\"). If not specified, uses Haiku.",
                        "type": "string"
                      },
                      "statusMessage": {
                        "description": "Custom status message to display in spinner while hook runs",
                        "type": "string"
                      },
                      "once": {
                        "description": "If true, hook runs once and is removed after execution",
                        "type": "boolean"
                      }
                    },
                    "required": [
                      "type",
                      "prompt"
                    ]
                  },
                  {
                    "type": "object",
                    "properties": {
                      "type": {
                        "description": "HTTP hook type",
                        "type": "string",
                        "const": "http"
                      },
                      "url": {
                        "description": "URL to POST the hook input JSON to",
                        "type": "string",
                        "format": "uri"
                      },
                      "if": {
                        "description": "Permission rule syntax to filter when this hook runs (e.g., \"Bash(git *)\"). Only runs if the tool call matches the pattern. Avoids spawning hooks for non-matching commands.",
                        "type": "string"
                      },
                      "timeout": {
                        "description": "Timeout in seconds for this specific request",
                        "type": "number",
                        "exclusiveMinimum": 0
                      },
                      "headers": {
                        "description": "Additional headers to include in the request. Values may reference environment variables using $VAR_NAME or ${VAR_NAME} syntax (e.g., \"Authorization\": \"Bearer $MY_TOKEN\"). Only variables listed in allowedEnvVars will be interpolated.",
                        "type": "object",
                        "propertyNames": {
                          "type": "string"
                        },
                        "additionalProperties": {
                          "type": "string"
                        }
                      },
                      "allowedEnvVars": {
                        "description": "Explicit list of environment variable names that may be interpolated in header values. Only variables listed here will be resolved; all other $VAR references are left as empty strings. Required for env var interpolation to work.",
                        "type": "array",
                        "items": {
                          "type": "string"
                        }
                      },
                      "statusMessage": {
                        "description": "Custom status message to display in spinner while hook runs",
                        "type": "string"
                      },
                      "once": {
                        "description": "If true, hook runs once and is removed after execution",
                        "type": "boolean"
                      }
                    },
                    "required": [
                      "type",
                      "url"
                    ]
                  },
                  {
                    "type": "object",
                    "properties": {
                      "type": {
                        "description": "MCP tool hook type",
                        "type": "string",
                        "const": "mcp_tool"
                      },
                      "server": {
                        "description": "Name of an already-configured MCP server to invoke",
                        "type": "string"
                      },
                      "tool": {
                        "description": "Name of the tool on that server to call",
                        "type": "string"
                      },
                      "input": {
                        "description": "Arguments passed to the MCP tool. String values support ${path} interpolation from the hook input JSON (e.g. \"${tool_input.file_path}\").",
                        "type": "object",
                        "propertyNames": {
                          "type": "string"
                        },
                        "additionalProperties": {}
                      },
                      "if": {
                        "description": "Permission rule syntax to filter when this hook runs (e.g., \"Bash(git *)\"). Only runs if the tool call matches the pattern. Avoids spawning hooks for non-matching commands.",
                        "type": "string"
                      },
                      "timeout": {
                        "description": "Timeout in seconds for this specific tool call",
                        "type": "number",
                        "exclusiveMinimum": 0
                      },
                      "statusMessage": {
                        "description": "Custom status message to display in spinner while hook runs",
                        "type": "string"
                      },
                      "once": {
                        "description": "If true, hook runs once and is removed after execution",
                        "type": "boolean"
                      }
                    },
                    "required": [
                      "type",
                      "server",
                      "tool"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "hooks"
          ]
        }
      }
    },
    "worktree": {
      "description": "Git worktree configuration for --worktree flag.",
      "type": "object",
      "properties": {
        "symlinkDirectories": {
          "description": "Directories to symlink from main repository to worktrees to avoid disk bloat. Must be explicitly configured - no directories are symlinked by default. Common examples: \"node_modules\", \".cache\", \".bin\"",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "sparsePaths": {
          "description": "Directories to include when creating worktrees, via git sparse-checkout (cone mode). Dramatically faster in large monorepos — only the listed paths are written to disk.",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "baseRef": {
          "description": "Which ref new worktrees branch from. 'fresh' (default) branches from origin/<default-branch> for a clean tree. 'head' branches from your current local HEAD so unpushed commits and feature-branch state are present. Applies to --worktree, EnterWorktree, and agent isolation.",
          "type": "string",
          "enum": [
            "fresh",
            "head"
          ]
        },
        "bgIsolation": {
          "description": "Isolation mode for background sessions in this repo. 'worktree' (default) blocks Edit/Write in the main checkout until EnterWorktree is called. 'none' lets background jobs edit the working copy directly.",
          "type": "string",
          "enum": [
            "worktree",
            "none"
          ]
        }
      }
    },
    "disableAllHooks": {
      "description": "Disable all hooks and statusLine execution",
      "type": "boolean"
    },
    "disableAgentView": {
      "description": "Disable agent view (`claude agents`, `--bg`, /background, the on-demand daemon). Typically set in managed settings. Equivalent to CLAUDE_CODE_DISABLE_AGENT_VIEW=1.",
      "type": "boolean"
    },
    "disableRemoteControl": {
      "description": "Disable Remote Control (claude.ai/code, `claude remote-control`, `--remote-control`/`--rc`, auto-start, and the in-session toggle). Typically set in managed settings.",
      "type": "boolean"
    },
    "disableWorkflows": {
      "description": "Disable the Workflows feature (also via CLAUDE_CODE_DISABLE_WORKFLOWS).",
      "type": "boolean"
    },
    "disableArtifact": {
      "description": "Disable the Artifact tool (also via CLAUDE_CODE_DISABLE_ARTIFACT).",
      "type": "boolean"
    },
    "enableArtifact": {
      "description": "Enable or disable the Artifact tool for this user. Unset defaults to enabled once the feature is available.",
      "type": "boolean"
    },
    "enableWorkflows": {
      "description": "Enable or disable the Workflows feature for this user. Unset = default by plan once the feature is available.",
      "type": "boolean"
    },
    "workflowSizeGuideline": {
      "description": "Advisory size guideline for the dynamic workflows Claude writes: \"small\" aims for fewer than 5 agents, \"medium\" (the default) fewer than 15, \"large\" fewer than 50, and \"unrestricted\" sends no guideline. A value here — including from managed settings — takes precedence over the \"Dynamic workflow size\" choice in /config, and that /config row is hidden while a settings file provides the key. This is a guideline, not an enforced limit.",
      "type": "string",
      "enum": [
        "unrestricted",
        "small",
        "medium",
        "large"
      ]
    },
    "workflowKeywordTriggerEnabled": {
      "description": "Enable the \"ultracode\" keyword trigger: including the keyword in a prompt opts that turn into the Workflow tool. Set to false to disable the trigger. Default: true.",
      "type": "boolean"
    },
    "disableSkillShellExecution": {
      "description": "Disable inline shell execution in skills and custom slash commands from user, project, or plugin sources. Commands are replaced with a placeholder instead of being run.",
      "type": "boolean"
    },
    "defaultShell": {
      "description": "Default shell for input-box ! commands. Defaults to 'bash' on all platforms (no Windows auto-flip).",
      "type": "string",
      "enum": [
        "bash",
        "powershell"
      ]
    },
    "respondToBashCommands": {
      "description": "Whether Claude responds after an input-box ! bash command runs. Set to false to add the command output to context without a response. Default: true.",
      "type": "boolean"
    },
    "allowManagedHooksOnly": {
      "description": "When true (and set in managed settings), only hooks from managed settings run. User, project, and local hooks are ignored.",
      "type": "boolean"
    },
    "allowedHttpHookUrls": {
      "description": "Allowlist of URL patterns that HTTP hooks may target. Supports * as a wildcard (e.g. \"https://hooks.example.com/*\"). When set, HTTP hooks with non-matching URLs are blocked. If undefined, all URLs are allowed. If empty array, no HTTP hooks are allowed. Arrays merge across settings sources (same semantics as allowedMcpServers).",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "httpHookAllowedEnvVars": {
      "description": "Allowlist of environment variable names HTTP hooks may interpolate into headers. When set, each hook's effective allowedEnvVars is the intersection with this list. If undefined, no restriction is applied. Arrays merge across settings sources (same semantics as allowedMcpServers).",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "allowManagedPermissionRulesOnly": {
      "description": "When true (and set in managed settings), only permission rules (allow/deny/ask) from managed settings are respected. User, project, local, and CLI argument permission rules are ignored.",
      "type": "boolean"
    },
    "allowManagedMcpServersOnly": {
      "description": "When true (and set in managed settings), allowedMcpServers is only read from managed settings. deniedMcpServers still merges from all sources, so users can deny servers for themselves. Users can still add their own MCP servers, but only the admin-defined allowlist applies.",
      "type": "boolean"
    },
    "allowAllClaudeAiMcps": {
      "description": "When true (and set in managed settings), claude.ai cloud MCP connectors load alongside managed-mcp.json instead of being suppressed by its exclusive-control lockdown. Default off preserves the lockdown. Read from managed settings only.",
      "type": "boolean"
    },
    "strictPluginOnlyCustomization": {
      "description": "When set in managed settings, blocks non-plugin customization sources for the listed surfaces. Array form locks specific surfaces (e.g. [\"skills\", \"hooks\"]); `true` locks all four; `false` is an explicit no-op. Blocked: ~/.claude/{surface}/, .claude/{surface}/ (project), settings.json hooks, .mcp.json. NOT blocked: managed (policySettings) sources, plugin-provided customizations. Composes with strictKnownMarketplaces for end-to-end admin control — plugins gated by marketplace allowlist, everything else blocked here.",
      "anyOf": [
        {
          "type": "boolean"
        },
        {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "skills",
              "agents",
              "hooks",
              "mcp"
            ]
          }
        }
      ]
    },
    "statusLine": {
      "description": "Custom status line display configuration",
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "const": "command"
        },
        "command": {
          "type": "string"
        },
        "padding": {
          "type": "number"
        },
        "refreshInterval": {
          "description": "Re-run the status line command every N seconds in addition to event-driven updates",
          "type": "number",
          "minimum": 1
        },
        "hideVimModeIndicator": {
          "description": "Hide the built-in `-- INSERT --` / `-- VISUAL --` indicator below the prompt. Use this when your status line script renders `vim.mode` itself.",
          "type": "boolean"
        }
      },
      "required": [
        "type",
        "command"
      ]
    },
    "prUrlTemplate": {
      "description": "URL template for PR links in the footer link badges and inline messages. The detected git PR is rendered as the first footer-link badge. Placeholders: {host} {owner} {repo} {number} {url}. Example: \"https://reviews.example.com/{owner}/{repo}/pull/{number}\"",
      "type": "string"
    },
    "footerLinksRegexes": {
      "description": "Extra clickable footer badges that appear when a regex matches turn output (tool results and assistant responses). Read from user, flag, and managed settings only; ignored in project .claude/settings.json and local .claude/settings.local.json. At most 5 badges render; the oldest is displaced by newer matches and /clear removes them. Use to surface IDs printed by project CLIs as session links.",
      "type": "array",
      "items": {
        "default": {
          "type": "invalid-entry-stripped"
        },
        "anyOf": [
          {
            "type": "object",
            "properties": {
              "type": {
                "description": "Config variant. This client understands \"regex\": matches turn output and builds a URL from named capture groups. Entries with other variants are preserved but skipped at runtime.",
                "type": "string",
                "const": "regex"
              },
              "pattern": {
                "description": "Regex matched against turn output (tool results and assistant text)",
                "type": "string"
              },
              "url": {
                "description": "Link target. {name} placeholders are filled from named regex capture groups, e.g. (?<id>...) -> {id}. Values are URL-encoded; the origin must be literal in the template. The scheme must be https, http, or a recognized editor or workspace deep-link scheme: vscode, vscode-insiders, cursor, windsurf, zed, jetbrains, idea, slack, linear, notion, figma.",
                "type": "string"
              },
              "label": {
                "description": "Badge text. {name} placeholders filled from named capture groups; defaults to the full match.",
                "type": "string"
              }
            },
            "required": [
              "type",
              "pattern",
              "url"
            ],
            "additionalProperties": {}
          },
          {
            "type": "object",
            "properties": {
              "type": {
                "description": "Config variant discriminator for entries this client does not understand; the entry is preserved as-is and skipped at runtime.",
                "type": "string"
              }
            },
            "required": [
              "type"
            ],
            "additionalProperties": {}
          }
        ]
      }
    },
    "subagentStatusLine": {
      "description": "Custom per-subagent status line shown in the agent panel; receives row context as JSON on stdin",
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "const": "command"
        },
        "command": {
          "type": "string"
        }
      },
      "required": [
        "type",
        "command"
      ]
    },
    "enabledPlugins": {
      "description": "Enabled plugins using plugin-id@marketplace-id format. Example: { \"formatter@anthropic-tools\": true }. Also supports extended format with version constraints. Settings precedence is user < project < local < flag < policy, so to disable a plugin that project settings enable, set it to false in .claude/settings.local.json — setting false in ~/.claude/settings.json is overridden by the project.",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "anyOf": [
          {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          {
            "type": "boolean"
          },
          {
            "not": {}
          }
        ]
      }
    },
    "extraKnownMarketplaces": {
      "description": "Additional marketplaces to make available for this repository. Typically used in repository .claude/settings.json to ensure team members have required plugin sources.",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "type": "object",
        "properties": {
          "source": {
            "description": "Where to fetch the marketplace from",
            "anyOf": [
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "url"
                  },
                  "url": {
                    "description": "Direct URL to marketplace.json file",
                    "type": "string",
                    "format": "uri"
                  },
                  "headers": {
                    "description": "Custom HTTP headers (e.g., for authentication)",
                    "type": "object",
                    "propertyNames": {
                      "type": "string"
                    },
                    "additionalProperties": {
                      "type": "string"
                    }
                  }
                },
                "required": [
                  "source",
                  "url"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "github"
                  },
                  "repo": {
                    "description": "GitHub repository in owner/repo format. ONLY in the managed-settings policy lists (strictKnownMarketplaces / blockedMarketplaces) the owner-wildcard form \"owner/*\" matches every repository under exactly that owner. Everywhere else (marketplace add, extraKnownMarketplaces, known_marketplaces.json) the value must name a single repository — a wildcard is taken literally and fails to clone.",
                    "type": "string"
                  },
                  "ref": {
                    "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                    "type": "string"
                  },
                  "path": {
                    "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                    "type": "string"
                  },
                  "sparsePaths": {
                    "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "skipLfs": {
                    "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                    "type": "boolean"
                  }
                },
                "required": [
                  "source",
                  "repo"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "git"
                  },
                  "url": {
                    "description": "Full git repository URL",
                    "type": "string"
                  },
                  "ref": {
                    "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                    "type": "string"
                  },
                  "path": {
                    "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                    "type": "string"
                  },
                  "sparsePaths": {
                    "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "skipLfs": {
                    "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                    "type": "boolean"
                  }
                },
                "required": [
                  "source",
                  "url"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "npm"
                  },
                  "package": {
                    "description": "NPM package containing marketplace.json",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "package"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "file"
                  },
                  "path": {
                    "description": "Local file path to marketplace.json",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "path"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "directory"
                  },
                  "path": {
                    "description": "Local directory containing .claude-plugin/marketplace.json",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "path"
                ]
              },
              {
                "description": "Policy-list sentinel for the ~/.claude/skills/ auto-load (@skills-dir plugins). In strictKnownMarketplaces: opt the scan back IN (by default any allowlist blocks it). In blockedMarketplaces: turn the scan OFF without otherwise restricting marketplaces. Only meaningful in those two managed-settings lists (areLocalPluginDirsAllowedByPolicy); known_marketplaces.json / marketplace add etc. ignore it.",
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "skills-dir"
                  }
                },
                "required": [
                  "source"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "hostPattern"
                  },
                  "hostPattern": {
                    "description": "Regex pattern to match the host/domain extracted from any marketplace source type. For github sources, matches against github.com. For git sources (SSH or HTTPS), extracts the hostname from the URL. Use in strictKnownMarketplaces to allow all marketplaces from a specific host (e.g., \"^github\\.mycompany\\.com$\").",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "hostPattern"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "pathPattern"
                  },
                  "pathPattern": {
                    "description": "Regex pattern matched against the .path field of file and directory sources. Use in strictKnownMarketplaces to allow filesystem-based marketplaces alongside hostPattern restrictions for network sources. Use \".*\" to allow all filesystem paths, or a narrower pattern (e.g., \"^/opt/approved/\") to restrict to specific directories.",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "pathPattern"
                ]
              },
              {
                "description": "Inline marketplace manifest defined directly in settings.json. The reconciler writes a synthetic marketplace.json to the cache; diffMarketplaces detects edits via isEqual on the stored source (the plugins array is inside this object, so edits surface as sourceChanged).",
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "settings"
                  },
                  "name": {
                    "description": "Marketplace name. Must match the extraKnownMarketplaces key (enforced); the synthetic manifest is written under this name. Same validation as PluginMarketplaceSchema plus reserved-name rejection — validateOfficialNameSource runs after the disk write, too late to clean up.",
                    "type": "string",
                    "minLength": 1
                  },
                  "plugins": {
                    "description": "Plugin entries declared inline in settings.json",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "name": {
                          "description": "Plugin name as it appears in the target repository",
                          "type": "string",
                          "minLength": 1
                        },
                        "source": {
                          "description": "Where to fetch the plugin from. Must be a remote source — relative paths have no marketplace repository to resolve against.",
                          "anyOf": [
                            {
                              "description": "Path to the plugin root, relative to the marketplace root (the directory containing .claude-plugin/, not .claude-plugin/ itself)",
                              "type": "string",
                              "pattern": "^\\.\\/.*"
                            },
                            {
                              "description": "NPM package as plugin source",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "npm"
                                },
                                "package": {
                                  "description": "Package name (or url, or local path, or anything else that can be passed to `npm` as a package)",
                                  "anyOf": [
                                    {
                                      "type": "string"
                                    },
                                    {
                                      "type": "string"
                                    }
                                  ]
                                },
                                "version": {
                                  "description": "Specific version or version range (e.g., ^1.0.0, ~2.1.0)",
                                  "type": "string"
                                },
                                "registry": {
                                  "description": "Custom NPM registry URL (defaults to using system default, likely npmjs.org)",
                                  "type": "string",
                                  "format": "uri"
                                }
                              },
                              "required": [
                                "source",
                                "package"
                              ]
                            },
                            {
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "url"
                                },
                                "url": {
                                  "description": "Full git repository URL (https:// or git@)",
                                  "type": "string"
                                },
                                "ref": {
                                  "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                                  "type": "string"
                                },
                                "sha": {
                                  "description": "Specific commit SHA to use",
                                  "type": "string",
                                  "minLength": 40,
                                  "maxLength": 40,
                                  "pattern": "^[a-f0-9]{40}$"
                                }
                              },
                              "required": [
                                "source",
                                "url"
                              ]
                            },
                            {
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "github"
                                },
                                "repo": {
                                  "description": "GitHub repository in owner/repo format",
                                  "type": "string"
                                },
                                "ref": {
                                  "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                                  "type": "string"
                                },
                                "sha": {
                                  "description": "Specific commit SHA to use",
                                  "type": "string",
                                  "minLength": 40,
                                  "maxLength": 40,
                                  "pattern": "^[a-f0-9]{40}$"
                                }
                              },
                              "required": [
                                "source",
                                "repo"
                              ]
                            },
                            {
                              "description": "Plugin located in a subdirectory of a larger repository (monorepo). Only the specified subdirectory is materialized; the rest of the repo is not downloaded.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "git-subdir"
                                },
                                "url": {
                                  "description": "Git repository: GitHub owner/repo shorthand, https://, or git@ URL",
                                  "type": "string"
                                },
                                "path": {
                                  "description": "Subdirectory within the repo containing the plugin (e.g., \"tools/claude-plugin\"). Cloned sparsely using partial clone (--filter=tree:0) to minimize bandwidth for monorepos.",
                                  "type": "string",
                                  "minLength": 1
                                },
                                "ref": {
                                  "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                                  "type": "string"
                                },
                                "sha": {
                                  "description": "Specific commit SHA to use",
                                  "type": "string",
                                  "minLength": 40,
                                  "maxLength": 40,
                                  "pattern": "^[a-f0-9]{40}$"
                                }
                              },
                              "required": [
                                "source",
                                "url",
                                "path"
                              ]
                            },
                            {
                              "description": "Plugin distributed as a zip archive fetched over HTTPS — for hosting on any static file server or artifact repository (S3, GitLab, nginx) with no git or npm on the client. Authentication comes from the enclosing marketplace: when the archive URL shares the marketplace url-source's origin, that source's headers are sent with the download.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "archive"
                                },
                                "url": {
                                  "description": "HTTPS URL of a zip archive containing the plugin. The plugin root (the directory holding .claude-plugin/) may be at the top of the archive or nested one directory deep — a single wrapping directory is stripped.",
                                  "type": "string",
                                  "format": "uri"
                                },
                                "sha256": {
                                  "description": "SHA-256 digest of the archive. When set, every download is verified against it and the install is refused on mismatch. It also serves as the version identity when neither plugin.json nor the marketplace entry declares a `version`. Recommended. Note the update signal is the version string (plugin.json version, else the entry version, else this digest) — changing only the digest while a version is declared does not trigger an update.",
                                  "type": "string",
                                  "pattern": "^[0-9a-fA-F]{64}$"
                                }
                              },
                              "required": [
                                "source",
                                "url"
                              ]
                            },
                            {
                              "description": "Plugin directory produced by a locally installed tool (e.g. an IDE that renders its plugin for the currently selected SDK). Claude Code runs the command, copies the directory it prints, and re-runs it in the background at startup to pick up changes.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "command"
                                },
                                "command": {
                                  "description": "Shell command that prints the absolute path of the plugin directory on stdout (exactly one line) and exits 0. It must leave a complete plugin in that directory before exiting; the directory is copied into the plugin cache, so the printed path may change between runs (it is re-resolved on every install and update, and once per session in the background). Runs through the platform shell (sh on macOS/Linux, cmd.exe on Windows) from the user's home directory with Claude Code's subprocess environment.",
                                  "type": "string",
                                  "minLength": 1,
                                  "maxLength": 500
                                },
                                "timeout": {
                                  "description": "Seconds to wait for the command before giving up (default: 60)",
                                  "type": "integer",
                                  "exclusiveMinimum": 0,
                                  "maximum": 600
                                },
                                "mode": {
                                  "description": "copy (default): the printed directory is copied into the plugin cache and content-hashed, so it may be deleted afterwards. link: the cache entry links to the printed directory in place (no copy, no size limit; macOS/Linux) — for large exports; the directory must then stay valid while Claude Code runs, and a different printed path is what signals new content.",
                                  "type": "string",
                                  "enum": [
                                    "copy",
                                    "link"
                                  ]
                                }
                              },
                              "required": [
                                "source",
                                "command"
                              ]
                            },
                            {
                              "description": "Placeholder for source types this Claude Code version does not recognize, or a known type whose fields failed validation (then `error` holds the reason). Never authored by hand — PluginMarketplaceSchema rewrites unparseable sources to this so the entry remains in marketplace.plugins (detectDelistedPlugins must not see it as removed). Install attempts fail at cachePlugin with an actionable message.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "unsupported"
                                },
                                "error": {
                                  "type": "string"
                                }
                              },
                              "required": [
                                "source"
                              ]
                            }
                          ]
                        },
                        "description": {
                          "type": "string"
                        },
                        "version": {
                          "type": "string"
                        },
                        "strict": {
                          "type": "boolean"
                        }
                      },
                      "required": [
                        "name",
                        "source"
                      ]
                    }
                  },
                  "owner": {
                    "type": "object",
                    "properties": {
                      "name": {
                        "description": "Display name of the plugin author or organization",
                        "type": "string",
                        "minLength": 1
                      },
                      "email": {
                        "description": "Contact email for support or feedback",
                        "type": "string"
                      },
                      "url": {
                        "description": "Website, GitHub profile, or organization URL",
                        "type": "string"
                      }
                    },
                    "required": [
                      "name"
                    ]
                  }
                },
                "required": [
                  "source",
                  "name",
                  "plugins"
                ]
              }
            ]
          },
          "installLocation": {
            "description": "Local cache path where marketplace manifest is stored (auto-generated if not provided)",
            "type": "string"
          },
          "autoUpdate": {
            "description": "Whether to automatically update this marketplace and its installed plugins on startup",
            "type": "boolean"
          }
        },
        "required": [
          "source"
        ]
      }
    },
    "additionalMarketplaces": {
      "description": "Alias for extraKnownMarketplaces: this key is read exactly as if it were spelled extraKnownMarketplaces. Do not set both in one file — if both appear, this key is ignored with a warning. Claude Code may rewrite this key as extraKnownMarketplaces when it updates the file. Clients older than this alias ignore it, so prefer extraKnownMarketplaces while older Claude Code versions still share the same settings.",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "type": "object",
        "properties": {
          "source": {
            "description": "Where to fetch the marketplace from",
            "anyOf": [
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "url"
                  },
                  "url": {
                    "description": "Direct URL to marketplace.json file",
                    "type": "string",
                    "format": "uri"
                  },
                  "headers": {
                    "description": "Custom HTTP headers (e.g., for authentication)",
                    "type": "object",
                    "propertyNames": {
                      "type": "string"
                    },
                    "additionalProperties": {
                      "type": "string"
                    }
                  }
                },
                "required": [
                  "source",
                  "url"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "github"
                  },
                  "repo": {
                    "description": "GitHub repository in owner/repo format. ONLY in the managed-settings policy lists (strictKnownMarketplaces / blockedMarketplaces) the owner-wildcard form \"owner/*\" matches every repository under exactly that owner. Everywhere else (marketplace add, extraKnownMarketplaces, known_marketplaces.json) the value must name a single repository — a wildcard is taken literally and fails to clone.",
                    "type": "string"
                  },
                  "ref": {
                    "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                    "type": "string"
                  },
                  "path": {
                    "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                    "type": "string"
                  },
                  "sparsePaths": {
                    "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "skipLfs": {
                    "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                    "type": "boolean"
                  }
                },
                "required": [
                  "source",
                  "repo"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "git"
                  },
                  "url": {
                    "description": "Full git repository URL",
                    "type": "string"
                  },
                  "ref": {
                    "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                    "type": "string"
                  },
                  "path": {
                    "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                    "type": "string"
                  },
                  "sparsePaths": {
                    "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "skipLfs": {
                    "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                    "type": "boolean"
                  }
                },
                "required": [
                  "source",
                  "url"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "npm"
                  },
                  "package": {
                    "description": "NPM package containing marketplace.json",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "package"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "file"
                  },
                  "path": {
                    "description": "Local file path to marketplace.json",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "path"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "directory"
                  },
                  "path": {
                    "description": "Local directory containing .claude-plugin/marketplace.json",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "path"
                ]
              },
              {
                "description": "Policy-list sentinel for the ~/.claude/skills/ auto-load (@skills-dir plugins). In strictKnownMarketplaces: opt the scan back IN (by default any allowlist blocks it). In blockedMarketplaces: turn the scan OFF without otherwise restricting marketplaces. Only meaningful in those two managed-settings lists (areLocalPluginDirsAllowedByPolicy); known_marketplaces.json / marketplace add etc. ignore it.",
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "skills-dir"
                  }
                },
                "required": [
                  "source"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "hostPattern"
                  },
                  "hostPattern": {
                    "description": "Regex pattern to match the host/domain extracted from any marketplace source type. For github sources, matches against github.com. For git sources (SSH or HTTPS), extracts the hostname from the URL. Use in strictKnownMarketplaces to allow all marketplaces from a specific host (e.g., \"^github\\.mycompany\\.com$\").",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "hostPattern"
                ]
              },
              {
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "pathPattern"
                  },
                  "pathPattern": {
                    "description": "Regex pattern matched against the .path field of file and directory sources. Use in strictKnownMarketplaces to allow filesystem-based marketplaces alongside hostPattern restrictions for network sources. Use \".*\" to allow all filesystem paths, or a narrower pattern (e.g., \"^/opt/approved/\") to restrict to specific directories.",
                    "type": "string"
                  }
                },
                "required": [
                  "source",
                  "pathPattern"
                ]
              },
              {
                "description": "Inline marketplace manifest defined directly in settings.json. The reconciler writes a synthetic marketplace.json to the cache; diffMarketplaces detects edits via isEqual on the stored source (the plugins array is inside this object, so edits surface as sourceChanged).",
                "type": "object",
                "properties": {
                  "source": {
                    "type": "string",
                    "const": "settings"
                  },
                  "name": {
                    "description": "Marketplace name. Must match the extraKnownMarketplaces key (enforced); the synthetic manifest is written under this name. Same validation as PluginMarketplaceSchema plus reserved-name rejection — validateOfficialNameSource runs after the disk write, too late to clean up.",
                    "type": "string",
                    "minLength": 1
                  },
                  "plugins": {
                    "description": "Plugin entries declared inline in settings.json",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "name": {
                          "description": "Plugin name as it appears in the target repository",
                          "type": "string",
                          "minLength": 1
                        },
                        "source": {
                          "description": "Where to fetch the plugin from. Must be a remote source — relative paths have no marketplace repository to resolve against.",
                          "anyOf": [
                            {
                              "description": "Path to the plugin root, relative to the marketplace root (the directory containing .claude-plugin/, not .claude-plugin/ itself)",
                              "type": "string",
                              "pattern": "^\\.\\/.*"
                            },
                            {
                              "description": "NPM package as plugin source",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "npm"
                                },
                                "package": {
                                  "description": "Package name (or url, or local path, or anything else that can be passed to `npm` as a package)",
                                  "anyOf": [
                                    {
                                      "type": "string"
                                    },
                                    {
                                      "type": "string"
                                    }
                                  ]
                                },
                                "version": {
                                  "description": "Specific version or version range (e.g., ^1.0.0, ~2.1.0)",
                                  "type": "string"
                                },
                                "registry": {
                                  "description": "Custom NPM registry URL (defaults to using system default, likely npmjs.org)",
                                  "type": "string",
                                  "format": "uri"
                                }
                              },
                              "required": [
                                "source",
                                "package"
                              ]
                            },
                            {
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "url"
                                },
                                "url": {
                                  "description": "Full git repository URL (https:// or git@)",
                                  "type": "string"
                                },
                                "ref": {
                                  "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                                  "type": "string"
                                },
                                "sha": {
                                  "description": "Specific commit SHA to use",
                                  "type": "string",
                                  "minLength": 40,
                                  "maxLength": 40,
                                  "pattern": "^[a-f0-9]{40}$"
                                }
                              },
                              "required": [
                                "source",
                                "url"
                              ]
                            },
                            {
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "github"
                                },
                                "repo": {
                                  "description": "GitHub repository in owner/repo format",
                                  "type": "string"
                                },
                                "ref": {
                                  "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                                  "type": "string"
                                },
                                "sha": {
                                  "description": "Specific commit SHA to use",
                                  "type": "string",
                                  "minLength": 40,
                                  "maxLength": 40,
                                  "pattern": "^[a-f0-9]{40}$"
                                }
                              },
                              "required": [
                                "source",
                                "repo"
                              ]
                            },
                            {
                              "description": "Plugin located in a subdirectory of a larger repository (monorepo). Only the specified subdirectory is materialized; the rest of the repo is not downloaded.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "git-subdir"
                                },
                                "url": {
                                  "description": "Git repository: GitHub owner/repo shorthand, https://, or git@ URL",
                                  "type": "string"
                                },
                                "path": {
                                  "description": "Subdirectory within the repo containing the plugin (e.g., \"tools/claude-plugin\"). Cloned sparsely using partial clone (--filter=tree:0) to minimize bandwidth for monorepos.",
                                  "type": "string",
                                  "minLength": 1
                                },
                                "ref": {
                                  "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                                  "type": "string"
                                },
                                "sha": {
                                  "description": "Specific commit SHA to use",
                                  "type": "string",
                                  "minLength": 40,
                                  "maxLength": 40,
                                  "pattern": "^[a-f0-9]{40}$"
                                }
                              },
                              "required": [
                                "source",
                                "url",
                                "path"
                              ]
                            },
                            {
                              "description": "Plugin distributed as a zip archive fetched over HTTPS — for hosting on any static file server or artifact repository (S3, GitLab, nginx) with no git or npm on the client. Authentication comes from the enclosing marketplace: when the archive URL shares the marketplace url-source's origin, that source's headers are sent with the download.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "archive"
                                },
                                "url": {
                                  "description": "HTTPS URL of a zip archive containing the plugin. The plugin root (the directory holding .claude-plugin/) may be at the top of the archive or nested one directory deep — a single wrapping directory is stripped.",
                                  "type": "string",
                                  "format": "uri"
                                },
                                "sha256": {
                                  "description": "SHA-256 digest of the archive. When set, every download is verified against it and the install is refused on mismatch. It also serves as the version identity when neither plugin.json nor the marketplace entry declares a `version`. Recommended. Note the update signal is the version string (plugin.json version, else the entry version, else this digest) — changing only the digest while a version is declared does not trigger an update.",
                                  "type": "string",
                                  "pattern": "^[0-9a-fA-F]{64}$"
                                }
                              },
                              "required": [
                                "source",
                                "url"
                              ]
                            },
                            {
                              "description": "Plugin directory produced by a locally installed tool (e.g. an IDE that renders its plugin for the currently selected SDK). Claude Code runs the command, copies the directory it prints, and re-runs it in the background at startup to pick up changes.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "command"
                                },
                                "command": {
                                  "description": "Shell command that prints the absolute path of the plugin directory on stdout (exactly one line) and exits 0. It must leave a complete plugin in that directory before exiting; the directory is copied into the plugin cache, so the printed path may change between runs (it is re-resolved on every install and update, and once per session in the background). Runs through the platform shell (sh on macOS/Linux, cmd.exe on Windows) from the user's home directory with Claude Code's subprocess environment.",
                                  "type": "string",
                                  "minLength": 1,
                                  "maxLength": 500
                                },
                                "timeout": {
                                  "description": "Seconds to wait for the command before giving up (default: 60)",
                                  "type": "integer",
                                  "exclusiveMinimum": 0,
                                  "maximum": 600
                                },
                                "mode": {
                                  "description": "copy (default): the printed directory is copied into the plugin cache and content-hashed, so it may be deleted afterwards. link: the cache entry links to the printed directory in place (no copy, no size limit; macOS/Linux) — for large exports; the directory must then stay valid while Claude Code runs, and a different printed path is what signals new content.",
                                  "type": "string",
                                  "enum": [
                                    "copy",
                                    "link"
                                  ]
                                }
                              },
                              "required": [
                                "source",
                                "command"
                              ]
                            },
                            {
                              "description": "Placeholder for source types this Claude Code version does not recognize, or a known type whose fields failed validation (then `error` holds the reason). Never authored by hand — PluginMarketplaceSchema rewrites unparseable sources to this so the entry remains in marketplace.plugins (detectDelistedPlugins must not see it as removed). Install attempts fail at cachePlugin with an actionable message.",
                              "type": "object",
                              "properties": {
                                "source": {
                                  "type": "string",
                                  "const": "unsupported"
                                },
                                "error": {
                                  "type": "string"
                                }
                              },
                              "required": [
                                "source"
                              ]
                            }
                          ]
                        },
                        "description": {
                          "type": "string"
                        },
                        "version": {
                          "type": "string"
                        },
                        "strict": {
                          "type": "boolean"
                        }
                      },
                      "required": [
                        "name",
                        "source"
                      ]
                    }
                  },
                  "owner": {
                    "type": "object",
                    "properties": {
                      "name": {
                        "description": "Display name of the plugin author or organization",
                        "type": "string",
                        "minLength": 1
                      },
                      "email": {
                        "description": "Contact email for support or feedback",
                        "type": "string"
                      },
                      "url": {
                        "description": "Website, GitHub profile, or organization URL",
                        "type": "string"
                      }
                    },
                    "required": [
                      "name"
                    ]
                  }
                },
                "required": [
                  "source",
                  "name",
                  "plugins"
                ]
              }
            ]
          },
          "installLocation": {
            "description": "Local cache path where marketplace manifest is stored (auto-generated if not provided)",
            "type": "string"
          },
          "autoUpdate": {
            "description": "Whether to automatically update this marketplace and its installed plugins on startup",
            "type": "boolean"
          }
        },
        "required": [
          "source"
        ]
      }
    },
    "strictKnownMarketplaces": {
      "description": "Enterprise strict list of allowed marketplace sources. When set in managed settings, ONLY these sources can be added as marketplaces. Entries match exactly, except that a github entry may use the owner-wildcard form {\"source\":\"github\",\"repo\":\"owner/*\"} to allow every repository under that owner. The check happens BEFORE downloading, so blocked sources never touch the filesystem. Note: this is a policy gate only — it does NOT register marketplaces. To pre-register allowed marketplaces for users, also set extraKnownMarketplaces.",
      "type": "array",
      "items": {
        "anyOf": [
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "url"
              },
              "url": {
                "description": "Direct URL to marketplace.json file",
                "type": "string",
                "format": "uri"
              },
              "headers": {
                "description": "Custom HTTP headers (e.g., for authentication)",
                "type": "object",
                "propertyNames": {
                  "type": "string"
                },
                "additionalProperties": {
                  "type": "string"
                }
              }
            },
            "required": [
              "source",
              "url"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "github"
              },
              "repo": {
                "description": "GitHub repository in owner/repo format. ONLY in the managed-settings policy lists (strictKnownMarketplaces / blockedMarketplaces) the owner-wildcard form \"owner/*\" matches every repository under exactly that owner. Everywhere else (marketplace add, extraKnownMarketplaces, known_marketplaces.json) the value must name a single repository — a wildcard is taken literally and fails to clone.",
                "type": "string"
              },
              "ref": {
                "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                "type": "string"
              },
              "path": {
                "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                "type": "string"
              },
              "sparsePaths": {
                "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                "type": "array",
                "items": {
                  "type": "string"
                }
              },
              "skipLfs": {
                "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                "type": "boolean"
              }
            },
            "required": [
              "source",
              "repo"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "git"
              },
              "url": {
                "description": "Full git repository URL",
                "type": "string"
              },
              "ref": {
                "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                "type": "string"
              },
              "path": {
                "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                "type": "string"
              },
              "sparsePaths": {
                "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                "type": "array",
                "items": {
                  "type": "string"
                }
              },
              "skipLfs": {
                "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                "type": "boolean"
              }
            },
            "required": [
              "source",
              "url"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "npm"
              },
              "package": {
                "description": "NPM package containing marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "package"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "file"
              },
              "path": {
                "description": "Local file path to marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "path"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "directory"
              },
              "path": {
                "description": "Local directory containing .claude-plugin/marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "path"
            ]
          },
          {
            "description": "Policy-list sentinel for the ~/.claude/skills/ auto-load (@skills-dir plugins). In strictKnownMarketplaces: opt the scan back IN (by default any allowlist blocks it). In blockedMarketplaces: turn the scan OFF without otherwise restricting marketplaces. Only meaningful in those two managed-settings lists (areLocalPluginDirsAllowedByPolicy); known_marketplaces.json / marketplace add etc. ignore it.",
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "skills-dir"
              }
            },
            "required": [
              "source"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "hostPattern"
              },
              "hostPattern": {
                "description": "Regex pattern to match the host/domain extracted from any marketplace source type. For github sources, matches against github.com. For git sources (SSH or HTTPS), extracts the hostname from the URL. Use in strictKnownMarketplaces to allow all marketplaces from a specific host (e.g., \"^github\\.mycompany\\.com$\").",
                "type": "string"
              }
            },
            "required": [
              "source",
              "hostPattern"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "pathPattern"
              },
              "pathPattern": {
                "description": "Regex pattern matched against the .path field of file and directory sources. Use in strictKnownMarketplaces to allow filesystem-based marketplaces alongside hostPattern restrictions for network sources. Use \".*\" to allow all filesystem paths, or a narrower pattern (e.g., \"^/opt/approved/\") to restrict to specific directories.",
                "type": "string"
              }
            },
            "required": [
              "source",
              "pathPattern"
            ]
          },
          {
            "description": "Inline marketplace manifest defined directly in settings.json. The reconciler writes a synthetic marketplace.json to the cache; diffMarketplaces detects edits via isEqual on the stored source (the plugins array is inside this object, so edits surface as sourceChanged).",
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "settings"
              },
              "name": {
                "description": "Marketplace name. Must match the extraKnownMarketplaces key (enforced); the synthetic manifest is written under this name. Same validation as PluginMarketplaceSchema plus reserved-name rejection — validateOfficialNameSource runs after the disk write, too late to clean up.",
                "type": "string",
                "minLength": 1
              },
              "plugins": {
                "description": "Plugin entries declared inline in settings.json",
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "description": "Plugin name as it appears in the target repository",
                      "type": "string",
                      "minLength": 1
                    },
                    "source": {
                      "description": "Where to fetch the plugin from. Must be a remote source — relative paths have no marketplace repository to resolve against.",
                      "anyOf": [
                        {
                          "description": "Path to the plugin root, relative to the marketplace root (the directory containing .claude-plugin/, not .claude-plugin/ itself)",
                          "type": "string",
                          "pattern": "^\\.\\/.*"
                        },
                        {
                          "description": "NPM package as plugin source",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "npm"
                            },
                            "package": {
                              "description": "Package name (or url, or local path, or anything else that can be passed to `npm` as a package)",
                              "anyOf": [
                                {
                                  "type": "string"
                                },
                                {
                                  "type": "string"
                                }
                              ]
                            },
                            "version": {
                              "description": "Specific version or version range (e.g., ^1.0.0, ~2.1.0)",
                              "type": "string"
                            },
                            "registry": {
                              "description": "Custom NPM registry URL (defaults to using system default, likely npmjs.org)",
                              "type": "string",
                              "format": "uri"
                            }
                          },
                          "required": [
                            "source",
                            "package"
                          ]
                        },
                        {
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "url"
                            },
                            "url": {
                              "description": "Full git repository URL (https:// or git@)",
                              "type": "string"
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "url"
                          ]
                        },
                        {
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "github"
                            },
                            "repo": {
                              "description": "GitHub repository in owner/repo format",
                              "type": "string"
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "repo"
                          ]
                        },
                        {
                          "description": "Plugin located in a subdirectory of a larger repository (monorepo). Only the specified subdirectory is materialized; the rest of the repo is not downloaded.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "git-subdir"
                            },
                            "url": {
                              "description": "Git repository: GitHub owner/repo shorthand, https://, or git@ URL",
                              "type": "string"
                            },
                            "path": {
                              "description": "Subdirectory within the repo containing the plugin (e.g., \"tools/claude-plugin\"). Cloned sparsely using partial clone (--filter=tree:0) to minimize bandwidth for monorepos.",
                              "type": "string",
                              "minLength": 1
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "url",
                            "path"
                          ]
                        },
                        {
                          "description": "Plugin distributed as a zip archive fetched over HTTPS — for hosting on any static file server or artifact repository (S3, GitLab, nginx) with no git or npm on the client. Authentication comes from the enclosing marketplace: when the archive URL shares the marketplace url-source's origin, that source's headers are sent with the download.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "archive"
                            },
                            "url": {
                              "description": "HTTPS URL of a zip archive containing the plugin. The plugin root (the directory holding .claude-plugin/) may be at the top of the archive or nested one directory deep — a single wrapping directory is stripped.",
                              "type": "string",
                              "format": "uri"
                            },
                            "sha256": {
                              "description": "SHA-256 digest of the archive. When set, every download is verified against it and the install is refused on mismatch. It also serves as the version identity when neither plugin.json nor the marketplace entry declares a `version`. Recommended. Note the update signal is the version string (plugin.json version, else the entry version, else this digest) — changing only the digest while a version is declared does not trigger an update.",
                              "type": "string",
                              "pattern": "^[0-9a-fA-F]{64}$"
                            }
                          },
                          "required": [
                            "source",
                            "url"
                          ]
                        },
                        {
                          "description": "Plugin directory produced by a locally installed tool (e.g. an IDE that renders its plugin for the currently selected SDK). Claude Code runs the command, copies the directory it prints, and re-runs it in the background at startup to pick up changes.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "command"
                            },
                            "command": {
                              "description": "Shell command that prints the absolute path of the plugin directory on stdout (exactly one line) and exits 0. It must leave a complete plugin in that directory before exiting; the directory is copied into the plugin cache, so the printed path may change between runs (it is re-resolved on every install and update, and once per session in the background). Runs through the platform shell (sh on macOS/Linux, cmd.exe on Windows) from the user's home directory with Claude Code's subprocess environment.",
                              "type": "string",
                              "minLength": 1,
                              "maxLength": 500
                            },
                            "timeout": {
                              "description": "Seconds to wait for the command before giving up (default: 60)",
                              "type": "integer",
                              "exclusiveMinimum": 0,
                              "maximum": 600
                            },
                            "mode": {
                              "description": "copy (default): the printed directory is copied into the plugin cache and content-hashed, so it may be deleted afterwards. link: the cache entry links to the printed directory in place (no copy, no size limit; macOS/Linux) — for large exports; the directory must then stay valid while Claude Code runs, and a different printed path is what signals new content.",
                              "type": "string",
                              "enum": [
                                "copy",
                                "link"
                              ]
                            }
                          },
                          "required": [
                            "source",
                            "command"
                          ]
                        },
                        {
                          "description": "Placeholder for source types this Claude Code version does not recognize, or a known type whose fields failed validation (then `error` holds the reason). Never authored by hand — PluginMarketplaceSchema rewrites unparseable sources to this so the entry remains in marketplace.plugins (detectDelistedPlugins must not see it as removed). Install attempts fail at cachePlugin with an actionable message.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "unsupported"
                            },
                            "error": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "source"
                          ]
                        }
                      ]
                    },
                    "description": {
                      "type": "string"
                    },
                    "version": {
                      "type": "string"
                    },
                    "strict": {
                      "type": "boolean"
                    }
                  },
                  "required": [
                    "name",
                    "source"
                  ]
                }
              },
              "owner": {
                "type": "object",
                "properties": {
                  "name": {
                    "description": "Display name of the plugin author or organization",
                    "type": "string",
                    "minLength": 1
                  },
                  "email": {
                    "description": "Contact email for support or feedback",
                    "type": "string"
                  },
                  "url": {
                    "description": "Website, GitHub profile, or organization URL",
                    "type": "string"
                  }
                },
                "required": [
                  "name"
                ]
              }
            },
            "required": [
              "source",
              "name",
              "plugins"
            ]
          }
        ]
      }
    },
    "allowedMarketplaces": {
      "description": "Alias for strictKnownMarketplaces (managed settings only): this key is read exactly as if it were spelled strictKnownMarketplaces. Do not set both in one file — if both appear, this key is ignored with a warning. Clients older than this alias ignore it, so keep using strictKnownMarketplaces when the allowlist must also bind older Claude Code versions.",
      "type": "array",
      "items": {
        "anyOf": [
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "url"
              },
              "url": {
                "description": "Direct URL to marketplace.json file",
                "type": "string",
                "format": "uri"
              },
              "headers": {
                "description": "Custom HTTP headers (e.g., for authentication)",
                "type": "object",
                "propertyNames": {
                  "type": "string"
                },
                "additionalProperties": {
                  "type": "string"
                }
              }
            },
            "required": [
              "source",
              "url"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "github"
              },
              "repo": {
                "description": "GitHub repository in owner/repo format. ONLY in the managed-settings policy lists (strictKnownMarketplaces / blockedMarketplaces) the owner-wildcard form \"owner/*\" matches every repository under exactly that owner. Everywhere else (marketplace add, extraKnownMarketplaces, known_marketplaces.json) the value must name a single repository — a wildcard is taken literally and fails to clone.",
                "type": "string"
              },
              "ref": {
                "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                "type": "string"
              },
              "path": {
                "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                "type": "string"
              },
              "sparsePaths": {
                "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                "type": "array",
                "items": {
                  "type": "string"
                }
              },
              "skipLfs": {
                "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                "type": "boolean"
              }
            },
            "required": [
              "source",
              "repo"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "git"
              },
              "url": {
                "description": "Full git repository URL",
                "type": "string"
              },
              "ref": {
                "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                "type": "string"
              },
              "path": {
                "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                "type": "string"
              },
              "sparsePaths": {
                "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                "type": "array",
                "items": {
                  "type": "string"
                }
              },
              "skipLfs": {
                "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                "type": "boolean"
              }
            },
            "required": [
              "source",
              "url"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "npm"
              },
              "package": {
                "description": "NPM package containing marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "package"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "file"
              },
              "path": {
                "description": "Local file path to marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "path"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "directory"
              },
              "path": {
                "description": "Local directory containing .claude-plugin/marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "path"
            ]
          },
          {
            "description": "Policy-list sentinel for the ~/.claude/skills/ auto-load (@skills-dir plugins). In strictKnownMarketplaces: opt the scan back IN (by default any allowlist blocks it). In blockedMarketplaces: turn the scan OFF without otherwise restricting marketplaces. Only meaningful in those two managed-settings lists (areLocalPluginDirsAllowedByPolicy); known_marketplaces.json / marketplace add etc. ignore it.",
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "skills-dir"
              }
            },
            "required": [
              "source"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "hostPattern"
              },
              "hostPattern": {
                "description": "Regex pattern to match the host/domain extracted from any marketplace source type. For github sources, matches against github.com. For git sources (SSH or HTTPS), extracts the hostname from the URL. Use in strictKnownMarketplaces to allow all marketplaces from a specific host (e.g., \"^github\\.mycompany\\.com$\").",
                "type": "string"
              }
            },
            "required": [
              "source",
              "hostPattern"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "pathPattern"
              },
              "pathPattern": {
                "description": "Regex pattern matched against the .path field of file and directory sources. Use in strictKnownMarketplaces to allow filesystem-based marketplaces alongside hostPattern restrictions for network sources. Use \".*\" to allow all filesystem paths, or a narrower pattern (e.g., \"^/opt/approved/\") to restrict to specific directories.",
                "type": "string"
              }
            },
            "required": [
              "source",
              "pathPattern"
            ]
          },
          {
            "description": "Inline marketplace manifest defined directly in settings.json. The reconciler writes a synthetic marketplace.json to the cache; diffMarketplaces detects edits via isEqual on the stored source (the plugins array is inside this object, so edits surface as sourceChanged).",
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "settings"
              },
              "name": {
                "description": "Marketplace name. Must match the extraKnownMarketplaces key (enforced); the synthetic manifest is written under this name. Same validation as PluginMarketplaceSchema plus reserved-name rejection — validateOfficialNameSource runs after the disk write, too late to clean up.",
                "type": "string",
                "minLength": 1
              },
              "plugins": {
                "description": "Plugin entries declared inline in settings.json",
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "description": "Plugin name as it appears in the target repository",
                      "type": "string",
                      "minLength": 1
                    },
                    "source": {
                      "description": "Where to fetch the plugin from. Must be a remote source — relative paths have no marketplace repository to resolve against.",
                      "anyOf": [
                        {
                          "description": "Path to the plugin root, relative to the marketplace root (the directory containing .claude-plugin/, not .claude-plugin/ itself)",
                          "type": "string",
                          "pattern": "^\\.\\/.*"
                        },
                        {
                          "description": "NPM package as plugin source",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "npm"
                            },
                            "package": {
                              "description": "Package name (or url, or local path, or anything else that can be passed to `npm` as a package)",
                              "anyOf": [
                                {
                                  "type": "string"
                                },
                                {
                                  "type": "string"
                                }
                              ]
                            },
                            "version": {
                              "description": "Specific version or version range (e.g., ^1.0.0, ~2.1.0)",
                              "type": "string"
                            },
                            "registry": {
                              "description": "Custom NPM registry URL (defaults to using system default, likely npmjs.org)",
                              "type": "string",
                              "format": "uri"
                            }
                          },
                          "required": [
                            "source",
                            "package"
                          ]
                        },
                        {
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "url"
                            },
                            "url": {
                              "description": "Full git repository URL (https:// or git@)",
                              "type": "string"
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "url"
                          ]
                        },
                        {
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "github"
                            },
                            "repo": {
                              "description": "GitHub repository in owner/repo format",
                              "type": "string"
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "repo"
                          ]
                        },
                        {
                          "description": "Plugin located in a subdirectory of a larger repository (monorepo). Only the specified subdirectory is materialized; the rest of the repo is not downloaded.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "git-subdir"
                            },
                            "url": {
                              "description": "Git repository: GitHub owner/repo shorthand, https://, or git@ URL",
                              "type": "string"
                            },
                            "path": {
                              "description": "Subdirectory within the repo containing the plugin (e.g., \"tools/claude-plugin\"). Cloned sparsely using partial clone (--filter=tree:0) to minimize bandwidth for monorepos.",
                              "type": "string",
                              "minLength": 1
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "url",
                            "path"
                          ]
                        },
                        {
                          "description": "Plugin distributed as a zip archive fetched over HTTPS — for hosting on any static file server or artifact repository (S3, GitLab, nginx) with no git or npm on the client. Authentication comes from the enclosing marketplace: when the archive URL shares the marketplace url-source's origin, that source's headers are sent with the download.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "archive"
                            },
                            "url": {
                              "description": "HTTPS URL of a zip archive containing the plugin. The plugin root (the directory holding .claude-plugin/) may be at the top of the archive or nested one directory deep — a single wrapping directory is stripped.",
                              "type": "string",
                              "format": "uri"
                            },
                            "sha256": {
                              "description": "SHA-256 digest of the archive. When set, every download is verified against it and the install is refused on mismatch. It also serves as the version identity when neither plugin.json nor the marketplace entry declares a `version`. Recommended. Note the update signal is the version string (plugin.json version, else the entry version, else this digest) — changing only the digest while a version is declared does not trigger an update.",
                              "type": "string",
                              "pattern": "^[0-9a-fA-F]{64}$"
                            }
                          },
                          "required": [
                            "source",
                            "url"
                          ]
                        },
                        {
                          "description": "Plugin directory produced by a locally installed tool (e.g. an IDE that renders its plugin for the currently selected SDK). Claude Code runs the command, copies the directory it prints, and re-runs it in the background at startup to pick up changes.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "command"
                            },
                            "command": {
                              "description": "Shell command that prints the absolute path of the plugin directory on stdout (exactly one line) and exits 0. It must leave a complete plugin in that directory before exiting; the directory is copied into the plugin cache, so the printed path may change between runs (it is re-resolved on every install and update, and once per session in the background). Runs through the platform shell (sh on macOS/Linux, cmd.exe on Windows) from the user's home directory with Claude Code's subprocess environment.",
                              "type": "string",
                              "minLength": 1,
                              "maxLength": 500
                            },
                            "timeout": {
                              "description": "Seconds to wait for the command before giving up (default: 60)",
                              "type": "integer",
                              "exclusiveMinimum": 0,
                              "maximum": 600
                            },
                            "mode": {
                              "description": "copy (default): the printed directory is copied into the plugin cache and content-hashed, so it may be deleted afterwards. link: the cache entry links to the printed directory in place (no copy, no size limit; macOS/Linux) — for large exports; the directory must then stay valid while Claude Code runs, and a different printed path is what signals new content.",
                              "type": "string",
                              "enum": [
                                "copy",
                                "link"
                              ]
                            }
                          },
                          "required": [
                            "source",
                            "command"
                          ]
                        },
                        {
                          "description": "Placeholder for source types this Claude Code version does not recognize, or a known type whose fields failed validation (then `error` holds the reason). Never authored by hand — PluginMarketplaceSchema rewrites unparseable sources to this so the entry remains in marketplace.plugins (detectDelistedPlugins must not see it as removed). Install attempts fail at cachePlugin with an actionable message.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "unsupported"
                            },
                            "error": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "source"
                          ]
                        }
                      ]
                    },
                    "description": {
                      "type": "string"
                    },
                    "version": {
                      "type": "string"
                    },
                    "strict": {
                      "type": "boolean"
                    }
                  },
                  "required": [
                    "name",
                    "source"
                  ]
                }
              },
              "owner": {
                "type": "object",
                "properties": {
                  "name": {
                    "description": "Display name of the plugin author or organization",
                    "type": "string",
                    "minLength": 1
                  },
                  "email": {
                    "description": "Contact email for support or feedback",
                    "type": "string"
                  },
                  "url": {
                    "description": "Website, GitHub profile, or organization URL",
                    "type": "string"
                  }
                },
                "required": [
                  "name"
                ]
              }
            },
            "required": [
              "source",
              "name",
              "plugins"
            ]
          }
        ]
      }
    },
    "blockedMarketplaces": {
      "description": "Enterprise blocklist of marketplace sources. When set in managed settings, these sources are blocked from being added as marketplaces. Entries match exactly, except that a github entry may use the owner-wildcard form {\"source\":\"github\",\"repo\":\"owner/*\"} to block every repository under that owner. The check happens BEFORE downloading, so blocked sources never touch the filesystem.",
      "type": "array",
      "items": {
        "anyOf": [
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "url"
              },
              "url": {
                "description": "Direct URL to marketplace.json file",
                "type": "string",
                "format": "uri"
              },
              "headers": {
                "description": "Custom HTTP headers (e.g., for authentication)",
                "type": "object",
                "propertyNames": {
                  "type": "string"
                },
                "additionalProperties": {
                  "type": "string"
                }
              }
            },
            "required": [
              "source",
              "url"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "github"
              },
              "repo": {
                "description": "GitHub repository in owner/repo format. ONLY in the managed-settings policy lists (strictKnownMarketplaces / blockedMarketplaces) the owner-wildcard form \"owner/*\" matches every repository under exactly that owner. Everywhere else (marketplace add, extraKnownMarketplaces, known_marketplaces.json) the value must name a single repository — a wildcard is taken literally and fails to clone.",
                "type": "string"
              },
              "ref": {
                "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                "type": "string"
              },
              "path": {
                "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                "type": "string"
              },
              "sparsePaths": {
                "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                "type": "array",
                "items": {
                  "type": "string"
                }
              },
              "skipLfs": {
                "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                "type": "boolean"
              }
            },
            "required": [
              "source",
              "repo"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "git"
              },
              "url": {
                "description": "Full git repository URL",
                "type": "string"
              },
              "ref": {
                "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                "type": "string"
              },
              "path": {
                "description": "Path to marketplace.json within repo (defaults to .claude-plugin/marketplace.json)",
                "type": "string"
              },
              "sparsePaths": {
                "description": "Directories to include via git sparse-checkout (cone mode). Use for monorepos where the marketplace lives in a subdirectory. Example: [\".claude-plugin\", \"plugins\"]. If omitted, the full repository is cloned.",
                "type": "array",
                "items": {
                  "type": "string"
                }
              },
              "skipLfs": {
                "description": "Skip Git LFS smudge during clone and update (sets GIT_LFS_SKIP_SMUDGE=1) so LFS pointer files stay as pointers instead of downloading their content. Use for marketplaces hosted in repos with large LFS objects.",
                "type": "boolean"
              }
            },
            "required": [
              "source",
              "url"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "npm"
              },
              "package": {
                "description": "NPM package containing marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "package"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "file"
              },
              "path": {
                "description": "Local file path to marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "path"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "directory"
              },
              "path": {
                "description": "Local directory containing .claude-plugin/marketplace.json",
                "type": "string"
              }
            },
            "required": [
              "source",
              "path"
            ]
          },
          {
            "description": "Policy-list sentinel for the ~/.claude/skills/ auto-load (@skills-dir plugins). In strictKnownMarketplaces: opt the scan back IN (by default any allowlist blocks it). In blockedMarketplaces: turn the scan OFF without otherwise restricting marketplaces. Only meaningful in those two managed-settings lists (areLocalPluginDirsAllowedByPolicy); known_marketplaces.json / marketplace add etc. ignore it.",
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "skills-dir"
              }
            },
            "required": [
              "source"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "hostPattern"
              },
              "hostPattern": {
                "description": "Regex pattern to match the host/domain extracted from any marketplace source type. For github sources, matches against github.com. For git sources (SSH or HTTPS), extracts the hostname from the URL. Use in strictKnownMarketplaces to allow all marketplaces from a specific host (e.g., \"^github\\.mycompany\\.com$\").",
                "type": "string"
              }
            },
            "required": [
              "source",
              "hostPattern"
            ]
          },
          {
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "pathPattern"
              },
              "pathPattern": {
                "description": "Regex pattern matched against the .path field of file and directory sources. Use in strictKnownMarketplaces to allow filesystem-based marketplaces alongside hostPattern restrictions for network sources. Use \".*\" to allow all filesystem paths, or a narrower pattern (e.g., \"^/opt/approved/\") to restrict to specific directories.",
                "type": "string"
              }
            },
            "required": [
              "source",
              "pathPattern"
            ]
          },
          {
            "description": "Inline marketplace manifest defined directly in settings.json. The reconciler writes a synthetic marketplace.json to the cache; diffMarketplaces detects edits via isEqual on the stored source (the plugins array is inside this object, so edits surface as sourceChanged).",
            "type": "object",
            "properties": {
              "source": {
                "type": "string",
                "const": "settings"
              },
              "name": {
                "description": "Marketplace name. Must match the extraKnownMarketplaces key (enforced); the synthetic manifest is written under this name. Same validation as PluginMarketplaceSchema plus reserved-name rejection — validateOfficialNameSource runs after the disk write, too late to clean up.",
                "type": "string",
                "minLength": 1
              },
              "plugins": {
                "description": "Plugin entries declared inline in settings.json",
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "description": "Plugin name as it appears in the target repository",
                      "type": "string",
                      "minLength": 1
                    },
                    "source": {
                      "description": "Where to fetch the plugin from. Must be a remote source — relative paths have no marketplace repository to resolve against.",
                      "anyOf": [
                        {
                          "description": "Path to the plugin root, relative to the marketplace root (the directory containing .claude-plugin/, not .claude-plugin/ itself)",
                          "type": "string",
                          "pattern": "^\\.\\/.*"
                        },
                        {
                          "description": "NPM package as plugin source",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "npm"
                            },
                            "package": {
                              "description": "Package name (or url, or local path, or anything else that can be passed to `npm` as a package)",
                              "anyOf": [
                                {
                                  "type": "string"
                                },
                                {
                                  "type": "string"
                                }
                              ]
                            },
                            "version": {
                              "description": "Specific version or version range (e.g., ^1.0.0, ~2.1.0)",
                              "type": "string"
                            },
                            "registry": {
                              "description": "Custom NPM registry URL (defaults to using system default, likely npmjs.org)",
                              "type": "string",
                              "format": "uri"
                            }
                          },
                          "required": [
                            "source",
                            "package"
                          ]
                        },
                        {
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "url"
                            },
                            "url": {
                              "description": "Full git repository URL (https:// or git@)",
                              "type": "string"
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "url"
                          ]
                        },
                        {
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "github"
                            },
                            "repo": {
                              "description": "GitHub repository in owner/repo format",
                              "type": "string"
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "repo"
                          ]
                        },
                        {
                          "description": "Plugin located in a subdirectory of a larger repository (monorepo). Only the specified subdirectory is materialized; the rest of the repo is not downloaded.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "git-subdir"
                            },
                            "url": {
                              "description": "Git repository: GitHub owner/repo shorthand, https://, or git@ URL",
                              "type": "string"
                            },
                            "path": {
                              "description": "Subdirectory within the repo containing the plugin (e.g., \"tools/claude-plugin\"). Cloned sparsely using partial clone (--filter=tree:0) to minimize bandwidth for monorepos.",
                              "type": "string",
                              "minLength": 1
                            },
                            "ref": {
                              "description": "Git branch or tag to use (e.g., \"main\", \"v1.0.0\"). Defaults to repository default branch.",
                              "type": "string"
                            },
                            "sha": {
                              "description": "Specific commit SHA to use",
                              "type": "string",
                              "minLength": 40,
                              "maxLength": 40,
                              "pattern": "^[a-f0-9]{40}$"
                            }
                          },
                          "required": [
                            "source",
                            "url",
                            "path"
                          ]
                        },
                        {
                          "description": "Plugin distributed as a zip archive fetched over HTTPS — for hosting on any static file server or artifact repository (S3, GitLab, nginx) with no git or npm on the client. Authentication comes from the enclosing marketplace: when the archive URL shares the marketplace url-source's origin, that source's headers are sent with the download.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "archive"
                            },
                            "url": {
                              "description": "HTTPS URL of a zip archive containing the plugin. The plugin root (the directory holding .claude-plugin/) may be at the top of the archive or nested one directory deep — a single wrapping directory is stripped.",
                              "type": "string",
                              "format": "uri"
                            },
                            "sha256": {
                              "description": "SHA-256 digest of the archive. When set, every download is verified against it and the install is refused on mismatch. It also serves as the version identity when neither plugin.json nor the marketplace entry declares a `version`. Recommended. Note the update signal is the version string (plugin.json version, else the entry version, else this digest) — changing only the digest while a version is declared does not trigger an update.",
                              "type": "string",
                              "pattern": "^[0-9a-fA-F]{64}$"
                            }
                          },
                          "required": [
                            "source",
                            "url"
                          ]
                        },
                        {
                          "description": "Plugin directory produced by a locally installed tool (e.g. an IDE that renders its plugin for the currently selected SDK). Claude Code runs the command, copies the directory it prints, and re-runs it in the background at startup to pick up changes.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "command"
                            },
                            "command": {
                              "description": "Shell command that prints the absolute path of the plugin directory on stdout (exactly one line) and exits 0. It must leave a complete plugin in that directory before exiting; the directory is copied into the plugin cache, so the printed path may change between runs (it is re-resolved on every install and update, and once per session in the background). Runs through the platform shell (sh on macOS/Linux, cmd.exe on Windows) from the user's home directory with Claude Code's subprocess environment.",
                              "type": "string",
                              "minLength": 1,
                              "maxLength": 500
                            },
                            "timeout": {
                              "description": "Seconds to wait for the command before giving up (default: 60)",
                              "type": "integer",
                              "exclusiveMinimum": 0,
                              "maximum": 600
                            },
                            "mode": {
                              "description": "copy (default): the printed directory is copied into the plugin cache and content-hashed, so it may be deleted afterwards. link: the cache entry links to the printed directory in place (no copy, no size limit; macOS/Linux) — for large exports; the directory must then stay valid while Claude Code runs, and a different printed path is what signals new content.",
                              "type": "string",
                              "enum": [
                                "copy",
                                "link"
                              ]
                            }
                          },
                          "required": [
                            "source",
                            "command"
                          ]
                        },
                        {
                          "description": "Placeholder for source types this Claude Code version does not recognize, or a known type whose fields failed validation (then `error` holds the reason). Never authored by hand — PluginMarketplaceSchema rewrites unparseable sources to this so the entry remains in marketplace.plugins (detectDelistedPlugins must not see it as removed). Install attempts fail at cachePlugin with an actionable message.",
                          "type": "object",
                          "properties": {
                            "source": {
                              "type": "string",
                              "const": "unsupported"
                            },
                            "error": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "source"
                          ]
                        }
                      ]
                    },
                    "description": {
                      "type": "string"
                    },
                    "version": {
                      "type": "string"
                    },
                    "strict": {
                      "type": "boolean"
                    }
                  },
                  "required": [
                    "name",
                    "source"
                  ]
                }
              },
              "owner": {
                "type": "object",
                "properties": {
                  "name": {
                    "description": "Display name of the plugin author or organization",
                    "type": "string",
                    "minLength": 1
                  },
                  "email": {
                    "description": "Contact email for support or feedback",
                    "type": "string"
                  },
                  "url": {
                    "description": "Website, GitHub profile, or organization URL",
                    "type": "string"
                  }
                },
                "required": [
                  "name"
                ]
              }
            },
            "required": [
              "source",
              "name",
              "plugins"
            ]
          }
        ]
      }
    },
    "disableCommandPluginSources": {
      "description": "Controls the `command` plugin source, whose plugin directory is produced by running a marketplace-declared command on this machine. true: command-sourced plugins are never installed, updated, or re-resolved (the command never runs). false: explicitly allowed. Unset: follows allowManagedHooksOnly — an org that restricts hook execution to managed settings gets command sources disabled too. Only honored from managed settings.",
      "type": "boolean"
    },
    "disableSideloadFlags": {
      "description": "When true (and set in managed settings), rejects the --plugin-dir, --plugin-url, --agents, and non-sdk --mcp-config CLI flags at startup. Closes the CLI-flag bypass of strictKnownMarketplaces. Pair with allowedMcpServers for per-server MCP control; this setting does not gate other MCP entry points (SDK setMcpServers, claude mcp add, .mcp.json). Also blocks surfaces that spawn the CLI with these flags internally (see settings documentation). Only honored from managed settings; ignored in user/project/local settings.",
      "type": "boolean"
    },
    "pluginSuggestionMarketplaces": {
      "description": "Marketplace names whose plugins may surface as contextual install suggestions (relevance-based tips). No marketplace-declared suggestions surface without this allowlist; the built-in first-party frontend-design tip is unaffected. Only honored when set in managed settings (policy scope); the key is ignored in user, project, and local settings. A name only takes effect when the marketplace is registered on the machine AND its registered source is also declared in managed settings, either as the extraKnownMarketplaces entry for that name or as an entry of strictKnownMarketplaces. A marketplace registered from a different source under an allowlisted name is ignored. The official marketplace is exempt from the source requirement: allowlisting its name alone suffices, since that name can only register from the official Anthropic source.",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "forceLoginMethod": {
      "description": "Force a specific login method: \"claudeai\" for Claude Pro/Max, \"console\" for Console billing, \"gateway\" for the Cloud gateway OIDC device flow",
      "type": "string",
      "enum": [
        "claudeai",
        "console",
        "gateway"
      ]
    },
    "forceLoginGatewayUrl": {
      "description": "Cloud gateway URL to pre-fill and auto-connect to during login, alongside forceLoginMethod: \"gateway\". Honored only from admin-controlled managed settings (MDM / managed-settings.json / policy helper); ignored in user, project, and remote-delivered settings.",
      "type": "string",
      "format": "uri"
    },
    "parentSettingsBehavior": {
      "description": "Controls whether the SDK parent tier (Options.managedSettings / --managed-settings) layers under this admin tier. \"first-wins\" (default): parent is dropped — admin tiers are the only policy source. \"merge\": parent's restrictive-only-filtered settings union under the admin winner. Has no effect when no admin tier exists (parent applies as the sole policy tier, still filtered restrictive-only).",
      "type": "string",
      "enum": [
        "first-wins",
        "merge"
      ]
    },
    "forceLoginOrgUUID": {
      "description": "Organization UUID to require for OAuth login. Accepts a single UUID string or an array of UUIDs (any one is permitted). When set in managed settings, login fails if the authenticated account does not belong to a listed organization.",
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      ]
    },
    "forceRemoteSettingsRefresh": {
      "description": "When set in managed settings, the CLI blocks startup until remote managed settings are freshly fetched, and exits if the fetch fails",
      "type": "boolean"
    },
    "otelHeadersHelper": {
      "description": "Path to a script that outputs OpenTelemetry headers",
      "type": "string"
    },
    "outputStyle": {
      "description": "Controls the output style for assistant responses",
      "type": "string"
    },
    "viewMode": {
      "description": "Default transcript view mode on startup",
      "type": "string",
      "enum": [
        "default",
        "verbose",
        "focus"
      ]
    },
    "language": {
      "description": "Preferred language for Claude responses and voice dictation (e.g., \"japanese\", \"spanish\")",
      "type": "string"
    },
    "skipWebFetchPreflight": {
      "description": "Skip the WebFetch blocklist check for enterprise environments with restrictive security policies",
      "type": "boolean"
    },
    "sandbox": {
      "type": "object",
      "properties": {
        "enabled": {
          "type": "boolean"
        },
        "failIfUnavailable": {
          "description": "Exit with an error at startup if sandbox.enabled is true but the sandbox cannot start (missing dependencies or unsupported platform). When false (default), a warning is shown and commands run unsandboxed. Intended for managed-settings deployments that require sandboxing as a hard gate.",
          "type": "boolean"
        },
        "autoAllowBashIfSandboxed": {
          "type": "boolean"
        },
        "allowUnsandboxedCommands": {
          "description": "Allow commands to run outside the sandbox via the dangerouslyDisableSandbox parameter. When false, the dangerouslyDisableSandbox parameter is completely ignored and all commands must run sandboxed. Default: true.",
          "type": "boolean"
        },
        "network": {
          "type": "object",
          "properties": {
            "allowedDomains": {
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "deniedDomains": {
              "description": "Domains that are always blocked, even if matched by allowedDomains. Supports the same wildcard syntax as allowedDomains. Merged from all settings sources regardless of allowManagedDomainsOnly.",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "strictAllowlist": {
              "description": "When true, the sandbox runtime deterministically denies hosts not in allowedDomains instead of prompting. Enforced for sandboxed commands only — in-process tools such as WebFetch are not gated by this setting. Only honored from user, managed/policy, or CLI (--settings) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored.",
              "type": "boolean"
            },
            "allowManagedDomainsOnly": {
              "description": "When true (and set in managed settings), only allowedDomains and WebFetch(domain:...) allow rules from managed settings are respected. User, project, local, and flag settings domains are ignored. Denied domains are still respected from all sources.",
              "type": "boolean"
            },
            "allowUnixSockets": {
              "description": "macOS only: Unix socket paths to allow. Ignored on Linux (seccomp cannot filter by path).",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "allowAllUnixSockets": {
              "description": "If true, allow all Unix sockets (disables blocking on both platforms).",
              "type": "boolean"
            },
            "allowLocalBinding": {
              "type": "boolean"
            },
            "allowMachLookup": {
              "description": "macOS only: Additional XPC/Mach service names to allow looking up. Supports trailing-wildcard prefix matching (e.g., \"com.apple.coresimulator.*\"). Needed for tools that communicate via XPC such as the iOS Simulator or Playwright.",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "httpProxyPort": {
              "type": "number"
            },
            "socksProxyPort": {
              "type": "number"
            },
            "tlsTerminate": {
              "description": "[EXPERIMENTAL] Enable in-process TLS termination so the per-request filter can see HTTPS request bodies. Provide a CA cert+key, or omit both to have sandbox-runtime generate an ephemeral one for the session. On native Windows an ephemeral CA cannot pass the sandbox trust check, so omitting the paths uses a persistent CA managed by the sandbox runtime (set up and trusted via /sandbox install); configured paths are passed to the sandbox runtime verbatim, which rejects a bad or incomplete pair at sandbox initialization. Only honored from user, managed/policy, or CLI (`--settings`) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored.",
              "type": "object",
              "properties": {
                "caCertPath": {
                  "type": "string",
                  "minLength": 1
                },
                "caKeyPath": {
                  "type": "string",
                  "minLength": 1
                }
              }
            }
          }
        },
        "filesystem": {
          "type": "object",
          "properties": {
            "allowWrite": {
              "description": "Additional paths to allow writing within the sandbox. Merged with paths from Edit(...) allow permission rules.",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "denyWrite": {
              "description": "Additional paths to deny writing within the sandbox. Merged with paths from Edit(...) deny permission rules.",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "denyRead": {
              "description": "Additional paths to deny reading within the sandbox. Merged with paths from Read(...) deny permission rules.",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "allowRead": {
              "description": "Paths to re-allow reading within denyRead regions. Takes precedence over denyRead for matching paths.",
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "allowManagedReadPathsOnly": {
              "description": "When true (set in managed settings), only allowRead paths from policySettings are used.",
              "type": "boolean"
            },
            "disabled": {
              "description": "macOS and Linux/WSL only: skip filesystem isolation entirely while keeping network and seccomp isolation. Ignored on native Windows, where the sandboxed process runs as a separate user with no inherent rights, so skipping the filesystem rules would withhold every access grant rather than loosen them — filesystem isolation stays on there. Sandboxed commands get unrestricted read/write access to the host filesystem; network egress is still confined to network.allowedDomains. Intended for deployments whose goal is egress control rather than filesystem containment. Does not change Bash prompting: sandbox.autoAllowBashIfSandboxed is independent and still defaults to true, so set it to false to keep prompting for sandboxed commands. Drops the read protection from filesystem.denyRead and credentials.files deny entries for sandboxed commands, since both are enforced by the filesystem layer this turns off; credentials.files mask entries (sentinel binds) and credentials.envVars deny/mask are unaffected. Only honored from user, managed/policy, or CLI (`--settings`) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored. If managed settings configure sandbox.filesystem at all, or list any sandbox.credentials.files deny entry, only managed settings can set this: an admin who deployed filesystem restrictions must not have them switched off by a user-writable file. (sandbox.credentials.envVars and credentials.files mask entries do not pin it — env scrubbing and sentinel binds are independent of the filesystem layer and survive this setting.) When unset, filesystem isolation stays on.",
              "type": "boolean"
            }
          }
        },
        "credentials": {
          "type": "object",
          "properties": {
            "files": {
              "description": "Credential files or directories to protect. `deny` blocks reads inside the sandbox; `mask` substitutes a sentinel inside the sandbox (whole-file, or per-`extract` capture) and injects the real value at the proxy. On macOS and Windows `mask` degrades to `deny`.",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "path": {
                    "description": "Path to a credential file or directory. Same resolution as sandbox.filesystem.* paths: absolute, ~ expanded, or relative to the settings file root (project root for project settings, ~/.claude for user settings).",
                    "type": "string",
                    "minLength": 1
                  },
                  "mode": {
                    "description": "Access mode for this path. `deny` blocks reads inside the sandbox; `mask` shows sandboxed commands a sentinel-substituted copy (whole-file, or only the spans captured by `extract`) and the host proxy swaps sentinel→real on egress to `injectHosts`. On macOS and Windows `mask` currently degrades to `deny`.",
                    "type": "string",
                    "enum": [
                      "deny",
                      "mask"
                    ]
                  },
                  "extract": {
                    "description": "Optional regex for structured masking when mode is `mask`. Applied globally to the file; capture group 1 of each match is a credential value, and only those captured spans are replaced with sentinels — the rest of the file is preserved so a tool that parses it (.netrc, JSON, YAML) still succeeds. Without `extract`, the entire file content is replaced with one sentinel (whole-file masking, suited to single-secret files). If the regex matches nothing, behavior is governed by `onExtractNoMatch` (default `warn`). Accepted but ignored for `deny`.",
                    "type": "string"
                  },
                  "onExtractNoMatch": {
                    "description": "What to do when `extract` matches nothing in the file — or, with `decode`, when no candidate survives verification. `warn` (default) emits a stderr warning and leaves the file readable as-is inside the sandbox (fail-open, for credentials that may be legitimately absent); `deny` degrades the entry to mode `deny` so the file is unreadable (fail-closed) — under `sandbox.filesystem.disabled` it is treated as `error`, since read-denies are dropped in that mode; `error` aborts at sandbox setup so nothing runs until the config is fixed. Only meaningful when mode is `mask` and `extract` or `decode` is set; accepted but ignored otherwise.",
                    "type": "string",
                    "enum": [
                      "warn",
                      "deny",
                      "error"
                    ]
                  },
                  "decode": {
                    "description": "Optional encoded-credential format for `mask` mode. `jwt`: candidates are located with a built-in JWT regex (or the explicit `extract` pattern, if set), verified to actually be JWTs before masking, and replaced with a structurally valid fake JWT so client-side token parsing inside the sandbox keeps working. If no candidate verifies, behavior is governed by `onExtractNoMatch` (default `warn`). Accepted but ignored for `deny`.",
                    "type": "string",
                    "enum": [
                      "jwt"
                    ]
                  },
                  "maskClaims": {
                    "description": "Names of top-level payload claims to mask inside each decoded value, instead of replacing the whole token. Each named claim present with a string value gets its own sentinel and the token is rebuilt around the modified payload; all other claims are preserved so a tool that decodes the token and reads a non-secret claim keeps working. Requires `decode`. If no named claim matches in any verified token, behavior is governed by `onExtractNoMatch` (default `warn`). Only meaningful when mode is `mask`; accepted but ignored for `deny`.",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "maskDuplicates": {
                    "description": "If true, verbatim occurrences of each captured credential value outside the regex-matched spans are also replaced with the corresponding sentinel — for a secret repeated where the regex does not reach (e.g. pasted into a comment). Matches raw substrings, so short or common values may corrupt unrelated content; intended for long, high-entropy secrets. Defaults to false. Only meaningful when mode is `mask` and `extract` or `decode` is set; accepted but ignored otherwise.",
                    "type": "boolean"
                  },
                  "injectHosts": {
                    "description": "Optional narrowing of where the proxy substitutes this credential. Only meaningful when mode is `mask`; accepted but ignored for `deny`. If unset, defaults to `network.allowedDomains` — the credential is injected at every reachable host. Each entry must be reachable via `network.allowedDomains` (sandbox-runtime validates this).",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  }
                },
                "required": [
                  "path",
                  "mode"
                ]
              }
            },
            "envVars": {
              "description": "Environment variables to protect. `deny` unsets the variable for sandboxed commands; `mask` substitutes a sentinel inside the sandbox and injects the real value at the proxy.",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {
                    "description": "Environment variable name.",
                    "type": "string",
                    "pattern": "^[A-Za-z_][A-Za-z0-9_]*$"
                  },
                  "mode": {
                    "description": "Access mode for this environment variable. `deny` unsets the variable for sandboxed commands; `mask` shows sandboxed commands a sentinel value and the host proxy swaps sentinel→real on egress to `injectHosts`.",
                    "type": "string",
                    "enum": [
                      "deny",
                      "mask"
                    ]
                  },
                  "extract": {
                    "description": "Optional regex for structured masking when mode is `mask`. Applied globally to the value; capture group 1 of each match is a credential value, and only those captured spans are replaced with sentinels — the rest of the value is preserved so a tool that parses it (a `DATABASE_URL` connection string, a composite `KEY:SECRET` pair) still succeeds inside the sandbox. Without `extract`, the entire value is replaced with one sentinel (whole-value masking, suited to bare tokens). If the regex matches nothing, behavior is governed by `onExtractNoMatch` (default `warn`). Cannot be combined with `decode` (the decode path never consults it). Accepted but ignored for `deny`.",
                    "type": "string"
                  },
                  "onExtractNoMatch": {
                    "description": "What to do when `extract` matches nothing in the value. `warn` (default) emits a stderr warning and lets the variable pass through unmasked (fail-open, for credentials that may be legitimately absent); `deny` unsets the variable inside the sandbox (fail-closed); `error` aborts at sandbox setup so nothing runs until the config is fixed. Only meaningful when mode is `mask` and `extract` is set without `decode`. On a mask entry with `decode`, the runtime takes the decode path and never consults this field, so a fail-closed setting cannot be honored — `deny` and `error` are rejected there; only `warn` is accepted. In all other shapes the field is accepted but ignored.",
                    "type": "string",
                    "enum": [
                      "warn",
                      "deny",
                      "error"
                    ]
                  },
                  "decode": {
                    "description": "Optional encoded-credential format for `mask` mode. `jwt`: the variable's whole value is verified to actually be a JWT and replaced with a structurally valid fake JWT so client-side token parsing inside the sandbox keeps working; the proxy swaps the whole fake token on egress. If the value does not verify, the variable is left unmasked with a stderr warning (fail-open). Cannot be combined with `extract` — the decode path never consults it. Accepted but ignored for `deny`.",
                    "type": "string",
                    "enum": [
                      "jwt"
                    ]
                  },
                  "maskClaims": {
                    "description": "Names of top-level payload claims to mask inside the decoded value, instead of replacing the whole token. Each named claim present with a string value gets its own sentinel and the token is rebuilt around the modified payload; all other claims are preserved so claim-reading clients keep working. Requires `decode`. If no named claim matches, the variable is left unmasked with a stderr warning (fail-open). Only meaningful when mode is `mask`; accepted but ignored for `deny`.",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "injectHosts": {
                    "description": "Optional narrowing of where the proxy substitutes this credential. Only meaningful when mode is `mask`; accepted but ignored for `deny`. If unset, defaults to `network.allowedDomains` — the credential is injected at every reachable host. Each entry must be reachable via `network.allowedDomains` (sandbox-runtime validates this).",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  }
                },
                "required": [
                  "name",
                  "mode"
                ]
              }
            },
            "allowPlaintextInject": {
              "description": "Allow sentinel→real substitution on the plain-HTTP proxy path. Defaults to false: without TLS termination the upstream identity is unverified and the credential travels in cleartext. Set only for trusted-network test fixtures. Only honored from user, managed/policy, or CLI (`--settings`) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored.",
              "type": "boolean"
            },
            "awsPairs": {
              "description": "Explicit groupings of masked env vars into AWS credential pairs for SigV4 re-signing, for non-standard variable names. The conventional AWS_ACCESS_KEY_ID / AWS_SECRET_ACCESS_KEY / AWS_SESSION_TOKEN trio is paired automatically when masked. Only honored from user, managed/policy, or CLI (`--settings`) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored. A member is only usable when its env var is forwarded as a whole-value `mask` entry (an entry carrying `extract` or `decode` does not qualify — re-signing needs the whole real value). A pair whose key id or secret member is unusable never re-signs: it is dropped, unless it names a conventional AWS variable, in which case it is forwarded as an inert suppressor so implicit auto-pairing stays overridden. A pair whose ONLY unusable member is the session token still re-signs, without an x-amz-security-token (temporary-credential requests fail upstream until the entry is fixed).",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "accessKeyIdVar": {
                    "description": "Name of the masked env var holding the AWS access key id.",
                    "type": "string",
                    "pattern": "^[A-Za-z_][A-Za-z0-9_]*$"
                  },
                  "secretAccessKeyVar": {
                    "description": "Name of the masked env var holding the AWS secret access key.",
                    "type": "string",
                    "pattern": "^[A-Za-z_][A-Za-z0-9_]*$"
                  },
                  "sessionTokenVar": {
                    "description": "Optional name of the masked env var holding the AWS session token (temporary credentials). When set, the proxy sends the real token as x-amz-security-token on re-signed requests and adds it to the signed header set if the client did not.",
                    "type": "string",
                    "pattern": "^[A-Za-z_][A-Za-z0-9_]*$"
                  }
                },
                "required": [
                  "accessKeyIdVar",
                  "secretAccessKeyVar"
                ]
              }
            },
            "sigv4": {
              "description": "Policies for AWS SigV4 request shapes the proxy cannot re-sign (streaming, presigned, sigv4a) when they reference a masked credential pair: `deny` (default) or `passthrough`. Only honored from user, managed/policy, or CLI (`--settings`) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored.",
              "type": "object",
              "properties": {
                "streaming": {
                  "description": "Policy for aws-chunked streaming uploads (x-amz-content-sha256: STREAMING-*): per-chunk signatures chain off the seed signature, so re-signing would require rewriting the body. `deny` (default) fails closed with a 403; `passthrough` forwards the request unre-signed (the upstream will reject its signature).",
                  "type": "string",
                  "enum": [
                    "deny",
                    "passthrough"
                  ]
                },
                "presigned": {
                  "description": "Policy for presigned URLs (X-Amz-Algorithm/X-Amz-Signature in the query, no Authorization header): the signature lives in the URL itself. `deny` (default) or `passthrough`.",
                  "type": "string",
                  "enum": [
                    "deny",
                    "passthrough"
                  ]
                },
                "sigv4a": {
                  "description": "Policy for SigV4A (AWS4-ECDSA-P256-SHA256) asymmetric signatures: there is no shared-key HMAC to recompute. `deny` (default) or `passthrough`.",
                  "type": "string",
                  "enum": [
                    "deny",
                    "passthrough"
                  ]
                }
              }
            }
          }
        },
        "ignoreViolations": {
          "type": "object",
          "propertyNames": {
            "type": "string"
          },
          "additionalProperties": {
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        },
        "enableWeakerNestedSandbox": {
          "type": "boolean"
        },
        "enableWeakerNetworkIsolation": {
          "description": "macOS only: Allow access to com.apple.trustd.agent in the sandbox. Needed for Go-based CLI tools (gh, gcloud, terraform, etc.) to verify TLS certificates when using httpProxyPort with a MITM proxy and custom CA. **Reduces security** — opens a potential data exfiltration vector through the trustd service. Default: false",
          "type": "boolean"
        },
        "allowAppleEvents": {
          "description": "macOS only: Allow sandboxed commands to send Apple Events (and look up the appleeventsd Mach service). Needed for `open`, `osascript`, and browser-based auth flows that open URLs. **Removes code-execution isolation** — sandboxed commands can launch other applications unsandboxed with no user prompt, and can script running apps (e.g. Terminal) subject to the user's per-app TCC automation consent. Only honored from user, managed/policy, or CLI (--settings) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored. Default: false",
          "type": "boolean"
        },
        "excludedCommands": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "ripgrep": {
          "description": "Custom ripgrep configuration for bundled ripgrep support. Only honored from user, managed/policy, or CLI (--settings) settings — project settings (.claude/settings.json and .claude/settings.local.json) are ignored.",
          "type": "object",
          "properties": {
            "command": {
              "type": "string"
            },
            "args": {
              "type": "array",
              "items": {
                "type": "string"
              }
            }
          },
          "required": [
            "command"
          ]
        },
        "bwrapPath": {
          "description": "Linux/WSL only: Absolute path to the bwrap (bubblewrap) binary. Overrides auto-detection via PATH. Only honored from admin-controlled managed settings.",
          "type": "string"
        },
        "socatPath": {
          "description": "Linux/WSL only: Absolute path to the socat binary used for the sandbox network proxy. Overrides auto-detection via PATH. Only honored from admin-controlled managed settings.",
          "type": "string"
        }
      },
      "additionalProperties": {}
    },
    "feedbackSurveyRate": {
      "description": "Probability (0–1) that the session quality survey appears when eligible. 0.05 is a reasonable starting point.",
      "type": "number",
      "minimum": 0,
      "maximum": 1
    },
    "feedbackDrafts": {
      "description": "Model-drafted feedback (the SendFeedback tool). \"notify\" (default) shows a one-line notice when a draft is queued; \"quiet\" shows only the footer counter; \"off\" disables the tool entirely so drafts are never queued.",
      "type": "string",
      "enum": [
        "notify",
        "quiet",
        "off"
      ]
    },
    "spinnerTipsEnabled": {
      "description": "Whether to show tips in the spinner",
      "type": "boolean"
    },
    "spinnerVerbs": {
      "description": "Customize spinner verbs. mode: \"append\" adds verbs to defaults, \"replace\" uses only your verbs.",
      "type": "object",
      "properties": {
        "mode": {
          "type": "string",
          "enum": [
            "append",
            "replace"
          ]
        },
        "verbs": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      },
      "required": [
        "mode",
        "verbs"
      ]
    },
    "spinnerTipsOverride": {
      "description": "Override spinner tips. tips: array of tip strings. excludeDefault: if true, only show custom tips (default: false).",
      "type": "object",
      "properties": {
        "excludeDefault": {
          "type": "boolean"
        },
        "tips": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      },
      "required": [
        "tips"
      ]
    },
    "syntaxHighlightingDisabled": {
      "description": "Whether to disable syntax highlighting in diffs",
      "type": "boolean"
    },
    "spellcheck": {
      "description": "Underline misspelled words in the prompt input as you type, using an installed aspell, hunspell or ispell (off unless \"enabled\" is true; does nothing if none is installed). Read from user, flag and managed settings only (the whole block from the highest-precedence of those applies); ignored in project .claude/settings.json and .claude/settings.local.json.",
      "type": "object",
      "properties": {
        "enabled": {
          "description": "Turn on spell checking of the prompt input (default: false)",
          "type": "boolean"
        },
        "checker": {
          "description": "Which spell checker to run: \"aspell\", \"hunspell\", \"ispell\", or \"auto\" (default) for the first of those found on PATH",
          "type": "string"
        },
        "language": {
          "description": "Dictionary to use, passed to the checker as-is (aspell --lang, hunspell -d, ispell -d), e.g. \"en_GB\"; names are checker-specific (letters, digits and _ - . , only). Default: the checker's own default",
          "type": "string"
        },
        "color": {
          "description": "Color of misspelled words (they are also underlined): a terminal color name such as \"red\" or \"magenta\", \"#rrggbb\", \"rgb(r,g,b)\", \"ansi256(n)\" or \"ansi:<name>\". Default: the theme's error color",
          "type": "string"
        }
      },
      "additionalProperties": {}
    },
    "terminalTitleFromRename": {
      "description": "Whether /rename updates the terminal tab title (defaults to true). Set to false to keep auto-generated topic titles.",
      "type": "boolean"
    },
    "alwaysThinkingEnabled": {
      "description": "When false, thinking is disabled. When absent or true, thinking is enabled automatically for supported models.",
      "type": "boolean"
    },
    "effortLevel": {
      "description": "Persisted effort level for supported models.",
      "type": "string",
      "enum": [
        "low",
        "medium",
        "high",
        "xhigh"
      ]
    },
    "ultracode": {
      "description": "Enable ultracode for the session: xhigh effort plus standing dynamic-workflow orchestration. Session-scoped — typically provided via --settings or the apply_flag_settings control request; interactive toggles never persist it. Requires workflows to be enabled and an xhigh-capable model.",
      "type": "boolean"
    },
    "autoCompactWindow": {
      "description": "Auto-compact window size",
      "type": "integer",
      "minimum": 100000,
      "maximum": 1000000
    },
    "advisorModel": {
      "description": "Advisor model for the server-side advisor tool.",
      "type": "string"
    },
    "fastMode": {
      "description": "When true, fast mode is enabled. When absent or false, fast mode is off.",
      "type": "boolean"
    },
    "fastModePerSessionOptIn": {
      "description": "When true, fast mode does not persist across sessions. Each session starts with fast mode off.",
      "type": "boolean"
    },
    "promptSuggestionEnabled": {
      "description": "When false, prompt suggestions are disabled. When absent or true, prompt suggestions are enabled.",
      "type": "boolean"
    },
    "emojiCompletionEnabled": {
      "description": "When false, the :emoji: shortcode typeahead (the suggestion popup and the :name: inline replacement) is disabled. When absent or true, it is enabled.",
      "type": "boolean"
    },
    "showClearContextOnPlanAccept": {
      "description": "When true, the plan-approval dialog offers a \"clear context\" option. Defaults to false.",
      "type": "boolean"
    },
    "askUserQuestionTimeout": {
      "description": "Idle time before Claude's questions auto-continue with any answers selected so far. Defaults to never — auto-continue only runs when explicitly set to 60s/5m/10m.",
      "type": "string",
      "enum": [
        "60s",
        "5m",
        "10m",
        "never"
      ]
    },
    "dialogExpiry": {
      "description": "Max time a permission/user dialog forwarded to a remote client stays parked awaiting an answer, and how long a HELD cross-session message awaits approval, before either resolves to its safe no-action default (cancelled / dropped-with-denial). Defaults to 5m to match the long-standing remote-dialog deadline; \"never\" disables the deadline. Local-only permission prompts (no remote client) are unaffected. The CLAUDE_CODE_USER_DIALOG_TIMEOUT_MS env var, when set, overrides this. Read from trusted sources only (never a checked-in repo settings file).",
      "type": "string",
      "enum": [
        "60s",
        "5m",
        "10m",
        "never"
      ]
    },
    "agent": {
      "description": "Name of an agent (built-in or custom) to use for the main thread. Applies the agent's system prompt, tool restrictions, and model.",
      "type": "string"
    },
    "companyAnnouncements": {
      "description": "Company announcements to display at startup (one will be randomly selected if multiple are provided)",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "pluginConfigs": {
      "description": "Per-plugin configuration including MCP server user configs, keyed by plugin ID (plugin@marketplace format)",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {
        "anyOf": [
          {
            "type": "object",
            "properties": {
              "mcpServers": {
                "description": "User configuration values for MCP servers keyed by server name",
                "type": "object",
                "propertyNames": {
                  "type": "string"
                },
                "additionalProperties": {
                  "type": "object",
                  "propertyNames": {
                    "type": "string"
                  },
                  "additionalProperties": {
                    "anyOf": [
                      {
                        "type": "string"
                      },
                      {
                        "type": "number"
                      },
                      {
                        "type": "boolean"
                      },
                      {
                        "type": "array",
                        "items": {
                          "type": "string"
                        }
                      }
                    ]
                  }
                }
              },
              "options": {
                "description": "Non-sensitive option values from plugin manifest userConfig, keyed by option name. Sensitive values go to secure storage instead.",
                "type": "object",
                "propertyNames": {
                  "type": "string"
                },
                "additionalProperties": {
                  "anyOf": [
                    {
                      "type": "string"
                    },
                    {
                      "type": "number"
                    },
                    {
                      "type": "boolean"
                    },
                    {
                      "type": "array",
                      "items": {
                        "type": "string"
                      }
                    }
                  ]
                }
              }
            }
          },
          {
            "not": {}
          }
        ]
      }
    },
    "remote": {
      "description": "Cloud session configuration",
      "type": "object",
      "properties": {
        "defaultEnvironmentId": {
          "description": "Default environment ID to use for cloud sessions",
          "type": "string"
        }
      }
    },
    "autoUpdatesChannel": {
      "description": "Release channel for auto-updates (latest or stable)",
      "type": "string",
      "enum": [
        "latest",
        "stable",
        "rc"
      ]
    },
    "minimumVersion": {
      "description": "Minimum version to stay on - prevents downgrades when switching to stable channel",
      "type": "string"
    },
    "requiredMinimumVersion": {
      "description": "Minimum Claude Code version required to start. If the running version is older, Claude Code exits at startup with instructions to update. Only enforced from managed (policy) settings.",
      "type": "string"
    },
    "requiredMaximumVersion": {
      "description": "Maximum Claude Code version allowed to start. If the running version is newer, Claude Code exits at startup with instructions to install an approved version. Only enforced from managed (policy) settings.",
      "type": "string"
    },
    "plansDirectory": {
      "description": "Custom directory for plan files, relative to project root. If not set, defaults to ~/.claude/plans/",
      "type": "string"
    },
    "tui": {
      "description": "Terminal UI renderer. \"fullscreen\" uses the flicker-free alt-screen renderer with virtualized scrollback (equivalent to CLAUDE_CODE_NO_FLICKER=1). \"default\" uses the classic main-screen renderer.",
      "type": "string",
      "enum": [
        "default",
        "fullscreen"
      ]
    },
    "voice": {
      "description": "Voice mode settings (hold-to-talk / tap-to-toggle dictation)",
      "type": "object",
      "properties": {
        "enabled": {
          "type": "boolean"
        },
        "mode": {
          "description": "'hold' (default): hold to talk. 'tap': tap to start, tap to stop+submit.",
          "type": "string",
          "enum": [
            "hold",
            "tap"
          ]
        },
        "autoSubmit": {
          "description": "Submit the prompt when hold-to-talk is released (hold mode only)",
          "type": "boolean"
        }
      }
    },
    "channelsEnabled": {
      "description": "Managed-org opt-in for channel notifications (MCP servers with the claude/channel capability pushing inbound messages). claude.ai Teams/Enterprise: default off. Console: default on unless managed settings exist. Set true to allow; users then select servers via --channels.",
      "type": "boolean"
    },
    "allowedChannelPlugins": {
      "description": "Managed-org allowlist of channel plugins. When set, replaces the default Anthropic allowlist — admins decide which plugins may push inbound messages. Undefined falls back to the default. Requires channelsEnabled: true.",
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "marketplace": {
            "type": "string"
          },
          "plugin": {
            "type": "string"
          }
        },
        "required": [
          "marketplace",
          "plugin"
        ]
      }
    },
    "prefersReducedMotion": {
      "description": "Reduce or disable animations for accessibility (spinner shimmer, flash effects, etc.)",
      "type": "boolean"
    },
    "autoMemoryEnabled": {
      "description": "Enable auto-memory for this project. When false, Claude will not read from or write to the auto-memory directory.",
      "type": "boolean"
    },
    "autoMemoryDirectory": {
      "description": "Custom directory path for auto-memory storage. Supports ~/ prefix for home directory expansion. Ignored if set in projectSettings (checked-in .claude/settings.json) for security. When unset, defaults to ~/.claude/projects/<sanitized-cwd>/memory/.",
      "type": "string"
    },
    "autoDreamEnabled": {
      "description": "Enable background memory consolidation (auto-dream). When set, overrides the server-side default.",
      "type": "boolean"
    },
    "showThinkingSummaries": {
      "description": "Request API-side thinking summaries and show them in the conversation and in the transcript view (ctrl+o). Set explicitly to override the default for your install.",
      "type": "boolean"
    },
    "skipDangerousModePermissionPrompt": {
      "description": "Whether the user has accepted the bypass permissions mode dialog",
      "type": "boolean"
    },
    "disableAutoMode": {
      "description": "Disable auto mode",
      "type": "string",
      "enum": [
        "disable"
      ]
    },
    "sshConfigs": {
      "description": "SSH connection configurations for remote environments. Typically set in managed settings by enterprise administrators to pre-configure SSH connections for team members.",
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "description": "Unique identifier for this SSH config. Used to match configs across settings sources.",
            "type": "string"
          },
          "name": {
            "description": "Display name for the SSH connection",
            "type": "string"
          },
          "sshHost": {
            "description": "SSH host in format \"user@hostname\" or \"hostname\", or a host alias from ~/.ssh/config",
            "type": "string"
          },
          "sshPort": {
            "description": "SSH port (default: 22)",
            "type": "integer",
            "minimum": -9007199254740991,
            "maximum": 9007199254740991
          },
          "sshIdentityFile": {
            "description": "Path to SSH identity file (private key)",
            "type": "string"
          },
          "startDirectory": {
            "description": "Default working directory on the remote host. Supports tilde expansion (e.g. ~/projects). If not specified, defaults to the remote user home directory. Can be overridden by the [dir] positional argument in `claude ssh <config> [dir]`.",
            "type": "string"
          }
        },
        "required": [
          "id",
          "name",
          "sshHost"
        ]
      }
    },
    "claudeMd": {
      "description": "CLAUDE.md-style instructions injected as organization-managed memory. Only honored from managed/policy settings.",
      "type": "string"
    },
    "claudeMdExcludes": {
      "description": "Glob patterns or absolute paths of CLAUDE.md files to exclude from loading. Patterns are matched against absolute file paths using picomatch. Only applies to User, Project, and Local memory types (Managed/policy files cannot be excluded). Examples: \"/home/dev/monorepo/CLAUDE.md\", \"**/code/CLAUDE.md\", \"**/some-dir/.claude/rules/**\"",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "pluginTrustMessage": {
      "description": "Custom message to append to the plugin trust warning shown before installation. Only read from policy settings (managed-settings.json / MDM). Useful for enterprise administrators to add organization-specific context (e.g., \"All plugins from our internal marketplace are vetted and approved.\").",
      "type": "string"
    },
    "theme": {
      "description": "Color theme for the UI",
      "anyOf": [
        {
          "type": "string",
          "enum": [
            "auto",
            "dark",
            "light",
            "light-daltonized",
            "dark-daltonized",
            "light-ansi",
            "dark-ansi"
          ]
        },
        {
          "type": "string",
          "pattern": "^custom:.*"
        }
      ]
    },
    "editorMode": {
      "description": "Key binding mode for the prompt input",
      "type": "string",
      "enum": [
        "normal",
        "vim"
      ]
    },
    "vimInsertModeRemaps": {
      "description": "Vim INSERT-mode key-sequence remaps, e.g. {\"jj\": \"<Esc>\"}. Each key is exactly two printable characters typed in sequence; \"<Esc>\" (return to NORMAL mode) is the only supported target. Applies when editorMode is \"vim\".",
      "type": "object",
      "propertyNames": {
        "type": "string"
      },
      "additionalProperties": {}
    },
    "verbose": {
      "description": "Show full tool output instead of truncated summaries",
      "type": "boolean"
    },
    "preferredNotifChannel": {
      "description": "Preferred OS notification channel",
      "type": "string",
      "enum": [
        "auto",
        "iterm2",
        "terminal_bell",
        "iterm2_with_bell",
        "kitty",
        "ghostty",
        "notifications_disabled"
      ]
    },
    "autoCompactEnabled": {
      "description": "Automatically compact conversation when context fills",
      "type": "boolean"
    },
    "precomputeCompactionEnabled": {
      "description": "Precompute the compaction summary in the background before it is needed. Only applies when auto-compact is on.",
      "type": "boolean"
    },
    "switchModelsOnFlag": {
      "description": "When safeguards flag a message, automatically switch to a different model to keep chatting. When off, your session will pause instead.",
      "type": "boolean"
    },
    "autoContinueAtUsageLimit": {
      "description": "When a claude.ai usage limit stops your session, wait for the limit to reset and continue the task automatically. When off, the limit dialog offers the wait as a choice instead.",
      "type": "boolean"
    },
    "autoScrollEnabled": {
      "description": "Auto-scroll the conversation view to bottom (fullscreen mode only)",
      "type": "boolean"
    },
    "wheelScrollAccelerationEnabled": {
      "description": "Ramp mouse-wheel scroll speed during fast scrolls (fullscreen mode only)",
      "type": "boolean"
    },
    "fileCheckpointingEnabled": {
      "description": "Snapshot files before edits so /rewind can restore them",
      "type": "boolean"
    },
    "showTurnDuration": {
      "description": "Show \"Cooked for Nm Ns\" after each assistant turn",
      "type": "boolean"
    },
    "showMessageTimestamps": {
      "description": "Stamp each message with its arrival time",
      "type": "boolean"
    },
    "terminalProgressBarEnabled": {
      "description": "Emit OSC 9;4 progress sequences during long operations",
      "type": "boolean"
    },
    "todoFeatureEnabled": {
      "description": "Enable the todo / task tracking panel",
      "type": "boolean"
    },
    "teammateMode": {
      "description": "How spawned teammates execute (tmux, iterm2, in-process, auto)",
      "type": "string",
      "enum": [
        "auto",
        "tmux",
        "iterm2",
        "in-process"
      ]
    },
    "remoteControlAtStartup": {
      "description": "Start Remote Control bridge automatically each session",
      "type": "boolean"
    },
    "isolatePeerMachines": {
      "description": "Require explicit approval before SendMessage can reach a peer session on another machine via Remote Control",
      "type": "boolean"
    },
    "daemonColdStart": {
      "description": "When no background service is running: 'transient' spawns one for this login session; 'ask' offers to install it persistently",
      "type": "string",
      "enum": [
        "transient",
        "ask"
      ]
    },
    "crossSessionInbound": {
      "description": "Inbound cross-session peer messages (SendMessage from your other sessions): 'accept' delivers them, 'hold' parks them for your review without letting Claude act, 'refuse' opts this session out. An explicit value always wins. Unset (mode parity): a message auto-delivers only when the sending session's permission-mode class matches yours (bypass↔bypass or prompting↔prompting); a mismatched sender's message is held for your approval; a sender that asserts no class is held only while this session bypasses permission prompts.",
      "type": "string",
      "enum": [
        "accept",
        "hold",
        "refuse"
      ]
    },
    "autoUploadSessions": {
      "description": "Mirror local sessions to claude.ai as view-only (no remote control)",
      "type": "boolean"
    },
    "inputNeededNotifEnabled": {
      "description": "Push to mobile when a permission prompt or question is waiting",
      "type": "boolean"
    },
    "agentPushNotifEnabled": {
      "description": "Allow Claude to push proactive mobile notifications",
      "type": "boolean"
    },
    "skipAutoPermissionPrompt": {
      "description": "Whether the user has accepted the auto mode opt-in dialog",
      "type": "boolean"
    },
    "useAutoModeDuringPlan": {
      "description": "Whether plan mode uses auto mode semantics when auto mode is available (default: true)",
      "type": "boolean"
    },
    "autoMode": {
      "description": "Auto mode classifier prompt customization",
      "type": "object",
      "properties": {
        "allow": {
          "description": "Rules for the auto mode classifier allow section. Include the literal string \"$defaults\" to inherit the built-in rules at that position.",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "soft_deny": {
          "description": "Rules for the auto mode classifier SOFT BLOCK section — destructive/irreversible actions that user intent can clear. Include the literal string \"$defaults\" to inherit the built-in rules at that position.",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "hard_deny": {
          "description": "Rules for the auto mode classifier HARD BLOCK section — security boundaries that user intent does NOT clear. Include the literal string \"$defaults\" to inherit the built-in rules at that position.",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "environment": {
          "description": "Entries for the auto mode classifier environment section. Include the literal string \"$defaults\" to inherit the built-in entries at that position.",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "classifyAllShell": {
          "description": "When true, every Bash/PowerShell allow rule is suspended while auto mode is active so all shell commands are routed through the classifier (higher safety, more classifier calls). Default: false.",
          "type": "boolean"
        }
      }
    },
    "disableDeepLinkRegistration": {
      "description": "Prevent claude-cli:// protocol handler registration with the OS",
      "type": "string",
      "enum": [
        "disable"
      ]
    },
    "voiceEnabled": {
      "description": "Enable voice mode (hold-to-talk dictation)",
      "type": "boolean"
    },
    "defaultView": {
      "description": "Default transcript view: chat (SendUserMessage checkpoints only) or transcript (full)",
      "type": "string",
      "enum": [
        "chat",
        "transcript"
      ]
    },
    "axScreenReader": {
      "description": "Render screen-reader friendly output (flat text, no decorative borders or animations). Overridden by the CLAUDE_AX_SCREEN_READER env var and the --ax-screen-reader CLI flag.",
      "type": "boolean"
    }
  },
  "additionalProperties": {}
}
```

## User Request

Add a SessionStart hook (user-level settings) that warns when Claude starts in a non-canonical working directory on this machine

---

**Claude:**

Читаю текущий конфиг хуков, потом строю дверь.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\settings.json"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.cmd"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py"}

---

> `PowerShell` -- {"command": "Get-Content C:\\Users\\dev\\.claude\\home_dirs.json; Write-Host '--- TEST: foreign cwd ---'; '{\"cwd\":\"C:\\\\Windows\\\\System32\"}' | python C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py; Write-Host '--- TEST: native cwd (must be silent) ---'; '{\"cwd\":\"E:\\\\!CLAUDE-PaloAl

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\home_dirs.json", "old_string": "  \"always_ok_prefixes\": [\n    \"D:\\\\Vault\",\n    \"/root/Obsidian\"\n  ]", "new_string": "  \"always_ok_prefixes\": [\n    \"D:\\\\Vault\",\n    \"/root/Obsidian\",\n    \"C:\\\\Users\\\\dev

---

> `PowerShell` -- {"command": "'{\"cwd\":\"C:\\\\Users\\\\dev\\\\.claude\\\\worktrees\\\\-nogit-CLAUDE-HUBPC-June26-zen-bose\"}' | python C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py; Write-Host '--- worktree: silent above = OK ---'; '{\"cwd\":\"C:\\\\Users\\\\dev\"}' | python C:\\Users\\dev\\.claud

---

**Claude:**

понедельник, утро, 08:40, 24 августа 2026

Да, возможно — и хорошая новость: такой сторож **уже стоит и работает**. Его построила соседняя сессия сегодня утром после ровно такого инцидента (сессия хаба нашлась в чужой папке ноутбука). Я его проверил вживую и чуть докрутил.

Как это устроено:
- Хук ставится не «в каждую неправильную папку» (их бесконечно), а один глобальный на старт **любой** сессии: [home_dir_guard.py](C:/Users/dev/.claude/hooks/home_dir_guard.py) в `settings.json` → SessionStart.
- Он сверяет папку запуска с «родным кабинетом» машины из [home_dirs.json](C:/Users/dev/.claude/home_dirs.json) (для хаба это `E:\!CLAUDE-HUBPC-June26`, для ноутбука NODE-0X своя).
- Не та папка → первой строкой сессии Claude видит предупреждение: «⚠️ ПАПКА НЕ РОДНАЯ… здесь ты видишь ЧУЖУЮ память, перезапустись из E:\!CLAUDE-HUBPC-June26». Правильная папка → молчит (сторож шумит только на беду).

Что я проверил и доделал сейчас:
- Прогнал вживую: запуск «из System32» и «из C:\Users\dev» → предупреждение стреляет; запуск из родной папки → тишина. Юнит-тест: PASS, 7 кейсов.
- Добавил 2 исключения, чтобы не было ложных тревог: worktree-папки субагентов и scratchpad — там сессии стартуют намеренно, это не ошибка. Перепроверил после правки: worktree молчит, `C:\Users\dev` по-прежнему ругается.

Ограничение честно: хук предупреждает Claude и тебя, но не может сам перезапустить сессию в правильной папке — перезапуск остаётся за тобой (или продолжаешь разговор как есть, просто без родной памяти).

🧒 Простыми словами: мы повесили звоночек на входную дверь. Если Claude случайно «проснулся» в чужой комнате, звоночек сразу говорит ему: «эй, ты не дома, твои записки в другой комнате — попроси оператора перезапустить тебя там». А в своей комнате звоночек молчит и не мешает.

понедельник, утро, 08:43, 24 августа 2026

---

**User:**

раскатай этот хук на все машины флота + ретро
но возможно это уже сделала другая сессия - проверь! сначала

---

**Claude:**

понедельник, утро, 08:54, 24 августа 2026

🎙 Майк: правильный порядок — сначала RECALL, потом стройка. Проверяю следы раскатки от соседних сессий.

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\deploy_register.py list 2>$null | Select-String -Pattern 'home' -Context 0,3; Write-Host '=== grep deploy dir ==='; Get-ChildItem \"$env:MACHINE_BUS_DIR\\_deploy\" -Recurse -Filter '*home*' -ErrorAction SilentlyContinue | Select-Object FullName

---

> `Grep` -- {"pattern": "home_dir_guard", "path": "C:\\Users\\dev\\.claude", "output_mode": "files_with_matches"}

---

> `PowerShell` -- {"command": "Get-ChildItem \"$env:MACHINE_BUS_DIR\\_deploy\" | Select-Object Name; Write-Host '=== pending/manifest for home-dir-guard ==='; Get-ChildItem \"$env:MACHINE_BUS_DIR\\_deploy\" -Recurse -Filter '*home-dir-guard*' -ErrorAction SilentlyContinue | Select-Object FullName, LastWriteTime", "de

---

> `Grep` -- {"pattern": "home-dir-guard", "path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_deploy", "output_mode": "content", "glob": "PENDING-*.jsonl"}

---

> `PowerShell` -- {"command": "$line = Get-Content \"D:\\Vault\\Vault-Knowledge\\_machine-bus\\_deploy\\PENDING-FLEET-ANCHOR.jsonl\" | Select-String 'home-dir-guard' | Select-Object -Last 1; $line.Line", "description": "Read home-dir-guard deploy entry for Mayak (FLEET-ANCHOR)"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py"}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\fleet_nodes.json"}

---

> `PowerShell` -- {"command": "Get-ChildItem \"$env:MACHINE_BUS_DIR\" -Directory | Select-Object Name; Write-Host '=== home-dir-guard mentions outside _deploy ==='; Get-ChildItem \"$env:MACHINE_BUS_DIR\" -Recurse -File -ErrorAction SilentlyContinue | Where-Object { $_.FullName -notmatch '_deploy' -and $_.LastWriteTim

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py --help 2>&1 | Select-Object -First 40", "description": "Check bus_send.py usage"}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK для всех узлов (кроме хаба): распакуй деплой home-dir-guard-2026-08-24 СРАЗУ, не жди планового инбокса. Шаги: (1) apply: python3 ~/.claude/scripts/home_dir_guard_install.py (Windows: python). (2) verify: тот же скрипт --verif

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK: всем узлам кроме хаба - распакуй деплой home-dir-guard-2026-08-24 СРАЗУ, не жди планового инбокса. Шаги: (1) apply: python3 ~/.claude/scripts/home_dir_guard_install.py (Windows: python). (2) verify: тот же скрипт --verify, e

---

**Claude:**

Шина доставила по обоим рельсам (файл + TG-03). Теперь тесты на хабе:

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py --verify; Write-Host \"verify exit: $LASTEXITCODE\"; Write-Host '=== negative: сломать нарочно (битый home_dirs) ==='; $env:TMPCFG=\"$env:TEMP\\hd_broken.json\"; 'not json' | Set-Content $env:TMPCFG; '{\"cwd\":\"C:\\\\

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

**⏳ Measure the time-gap FIRST.** Check when this session's work actually happened (turnstate ledger / the digest's day-span) vs **now**. Old session → widen every lookup below to cover *"what changed SINCE"* — don't recall only the session's own window.

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
3. **Neighboring chats (lexical, 0 tok):** `/search <topic words>` (search_catalog.db, ~99k Telegram/FB/ChatGPT/Claude) — what did dev or another session **dictate elsewhere** about this topic?
4. **Vault meaning (RAG):** `/ask <topic>` (`$IMPORTS_ROOT/brain_ask.py`) — what does the Second Brain already hold / already decide on this?
5. **Memory + vault grep** for every rule/concept/decision this session touched — already captured? **superseded / changed** since?
6. **Peers & cross-machine:** `/inbox` + `_machine-bus` + consensus commits — "всё, о чём мы договорились" on the OTHER machines; did a peer already decide, or undo, this?
7. **Declined journal:** skill `/declined` — did we already reject something this session quietly re-did?

**Attribution guard:** the Step-1 inventory is machine-wide and WILL include other sessions' artifacts (skills/scripts/commits from the fleet). Treat anything NOT created in THIS conversation as **someone else's** — flag it, never claim or re-route it.

**Output of Step 0 — one tight «🔎 сверка» block up front** (checked + verdict):
- **checked:** what I actually looked at (N retros / chats / vault / peers).
- **✅ aligned** — this session's calls match the collaboration; or
- **⚠️ drift** — session did X but [[note/decision]] elsewhere says Y (superseded / contradicts / already undone) → flag for dev; or
- **🔗 to propagate** — session's durable work not yet in vault / peers / Bible → route it in Step 4.
If a parallel session already captured the durable item, **SKIP re-capturing** — just cross-link.

## Step 1 — Inventory (deterministic first; AK-47, ~free)
Ground the recap in facts, not memory alone — run the SHARED inventory script (same one the daily sweep uses, so the logic never drifts):
- `python "$IMPORTS_ROOT/retro_inventory.py" 1`  (arg = days; widen for a multi-day session)
- It prints `BUILT_ARTIFACTS <n>` and writes `$IMPORTS_ROOT/retro_candidates/digest-latest.md` — Read that digest: new/changed **skills**, **_imports scripts/sidecars**, **durable notes** (Protocols + Concepts), and recent **descriptive vault commits**.
- (⚠️ a concurrent Claude-Desktop fleet may interleave vault commits — its are descriptive; the terse `pre-intervention` ones are auto-backups.)
- **Cross-check** with what you (the agent) created/edited in THIS conversation: skills, scripts, vault notes, memory entries, `CLAUDE.md` edits, decisions made, rules captured, things flagged for dev.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже) и на каждую — ОДНА строка в `$OBSIDIAN_VAULT\00-System\Breakage-Journal.md`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. Затем СЧЁТЧИК по классу (`grep` по журналу, не по памяти): 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный → отдельная сессия починки** (5 почему по серии → ТРИЗ → АК-47). Механизм/робота на 1-2 случае НЕ строить.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · fail-closed гейты.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- Канон: Библия `reglament-mekhanizm-tolko-posle-tretey-polomki` + CLAUDE.md §5.10 + `reglament-pyat-pochemu-koren-po-serii-sessiy` §«Три инструмента»; проверка двери — `python ~/.claude/scripts/rule_home_guard.py mekhanizm-tolko-posle-tretey-polomki`.

## Step 2 — Summarize the arc ("сегодня мы поняли")
3–7 beats: starting idea → what got built → key realizations → what was decided. Honest, concise, his voice. This is the "Stan at the end of South Park" recap.

## Step 2🎙 — Вердикт кофаундера (Майк) — canon 2026-07-07, applied 2026-07-31
Right after the arc, Майк speaks as co-founder — 4 строки, без воды (canon `reglament-*` voice-through-line; восстановлен из потерянного сообщения шины, 23 дня в призраке; НЕ театр — работает ПОВЕРХ механики 28.07: если сессия дала стратегический выбор, мемо/адвокат-дьявола из [[cofounder-decision-artifact-gate]] главнее и уже сделаны):
- 💰 **деньги-линза** — что из сегодняшнего приближает выручку/оффер (цель №1/№2), одной строкой;
- 🔪 **что убил бы** — самая слабая трата времени сессии, которую завтра не повторяем;
- 🤺 **спарринг-аудит** — где я сегодня поддакнул вместо спора (провал роли §1.2) либо «спорил честно»;
- ❓ **вопрос** — один направляющий вопрос оператору на завтра.
Пустышку не писать: сессия чисто механическая без бизнес-среза → строка «🎙 Майк: бизнес-среза нет, чисто инфра» и дальше.

## Step 3 — Classify each artifact (Keep / Drop / Try) + tested? audit
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]). Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3📋 — Journal sync (реестр задач; dev's decree 2026-07-04)
Retro is the SAFETY NET of the task journal ([[task-journal-done-undone-linking]]): the in-session reflex («сформулировал → сразу в реестр») catches tasks at birth; retro catches what slipped. Two moves, both against the ONE journal ([[task-backlog-registry]] — **v2 markdown-first, SHIPPED 2026-07-07**):
- **Источник истины = markdown-заметки** `$OBSIDIAN_VAULT/10-Tasks/task-*.md` (шаблон `_Task-Template.md`, MOC `_Tasks-MOC.md`). Синкаются флоту, поэтому работают с ЛЮБОЙ машины без шины и без движка. Завести задачу = новый файл `task-ГГГГ-ММ-ДД-слаг.md`; закрыть = правка frontmatter (`state`/`status` + evidence). Схема строгая: неизвестный `state`/`prio` → `schema_errors` в аудите, а не тихий дефолт.
- **Витрину и аудит строит индексатор** `tasks_index.py` (markdown → `_Dashboards/Task-Backlog.html` + `10-Tasks/_audit/audit-latest.json`). Он крутится ночью на Маяке как ЕДИНСТВЕННЫЙ писатель — руками на хабе/ноуте его НЕ запускать (два писателя одного синкаемого дерива = sync-conflict).
- ⛔ Старый SQLite-движок task-registry (жил на ноуте NODE-0X) = **аварийный fallback, снят с вооружения**; на хабе его нет и не должно быть. Не зови его и не «восстанавливай» — v2 его заменил. (Имя намеренно без code-формата: backtick = «это надо запускать».)

Две операции ретро:
- **Сессия рождена из сида Task-Now?** (первое сообщение начинается «Продолжи задачу task-…» или «Реши СУДЬБУ задачи task-…») → обнови frontmatter ЭТОЙ задачи прямо сейчас: state/touched_at, при done — evidence+outcome; сид без обновлённого frontmatter = петля Task-Now разорвана (v4, dev 2026-08-20).
- **Closed this session** → mark `done` **with evidence** (the /tt proof, commit, counter) + link what it unblocked. Claimed-done without proof → flag, don't close.
- **Still open** (every «📌 Open item», seed prompt, deferred tail, «потом») → ensure it EXISTS in the registry with a link to where it was born + prio/type. Nothing from the open-items list may live only in the chat transcript.
Announce the delta in one line: «📋 журнал: +N новых · ✅M закрыто · без изменений K». Don't duplicate neighbor registries (DR-реестр, improvements-backlog, declined) — link, не копируй.

## Step 3🗺 — Roadmap checkpoint (dev's decree 2026-07-16: «в каждом ретро — как мы продвинулись по roadmap»)
Канон = `$OBSIDIAN_VAULT/04-Projects/ROADMAP.md` (живой публичный роадмап для фолловеров). Три движения, все против ЭТОГО файла:
- **Продвинулись** → отметить чекбоксы/статусы, веху уровня «фолловеру интересно» → строка в Ship log с датой.
- **Появилось новое направление в сессии** → добавить в NOW/NEXT/LATER (не дублируя детальные планы — ссылкой).
- **Ничего не двинулось** → честно сказать это в отчёте (тоже сигнал).
Announce одной строкой: «🗺 roadmap: ✅N продвинуто · ➕M добавлено · ⏸ без движения». Публичная проекция файла наружу — только через контент-гейт (Нора), ретро наружу не постит.

## Step 3🔗 — Connect check (построено → передано → ИСПОЛЬЗУЕТСЯ?) — dev 2026-07-04
Правило Connect ([[connect-rule-pipeline-ownership]]) на подведении итогов: для КАЖДОГО артефакта этой сессии довести цепочку до конца — **«собрали» это ещё НЕ финиш**. Финиш = построено → передано потребителю → **реально используется**. Три исхода на артефакт:
- ✅ **используется** — есть потребитель и он потребляет (скилл вызывают, рутина читает выход, поле CRM читают, дашборд открывают, данные доехали и применены). **Назвать потребителя** — иначе это не ✅.
- 🔗 **передано, потребления пока нет** — доехало, но никто ещё не читает/не применяет → на доску висячих, назначить потребителя/срок.
- ⚠️ **построено «в воздух»** — собрали и бросили, потребителя нет вовсе (dead-letter без consumer — как релинк-очередь: 29k сирот, 0 применено) → **ПОДСВЕТИТЬ оператору явно**: «построили X, но это никем не используется» → решить: подключить потребителя ИЛИ признать выброшенным.

Молчание ≠ используется. «Построили» без названного потребителя = недоделанный Connect, НЕ «done». Строкой: «🔗 Connect: ✅N используется · 🔗M передано-ждёт · ⚠️K в воздух».
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` = сейчас + 1-2 мин, разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro).

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].

## Step 4★ — The «repeats → make a skill» reflex (milestone closeout)
This is the step dev asked for (2026-06-18): at a finished milestone, don't just *note* a repeating action — **offer to turn it into a skill**. It's the retro-time expression of the standing rule `evaluate-recurring-into-routine` (повторяющаяся задача → оцени «на рутину?»). Mirror of [[capture-rules-into-bible]] (that catches *rules*; this catches *tasks-to-automate*).

**Trigger (catch it, don't wait to be asked):** any action that **repeated ≥2–3×** this session/milestone, OR that we'll **clearly return to** later (a manual sequence I re-typed, a multi-step procedure, a recurring check).

**Procedure — 4 cheap moves:**
1. **RECALL first — don't duplicate.** Skim the available skills + memory `automation-inventory` for an existing skill/routine/hook that already covers it. If one exists, point dev to it instead of building a twin. **⛳ И тут же второй вопрос (dev hub:5090, 2026-08-04): скилл ЕСТЬ — не проапгрейдить ли его?** «Есть» ≠ «закрыто»: назови, чего ему не хватило ИМЕННО в этой сессии (шаг, который я делал руками поверх скилла / грабли, которых в нём нет / устаревшая строка) → правка в тот же заход, и это тоже строка в 🔁→🛠 (`built/proposed/declined`). Нечего добавить — скажи это словом, молчание = проверка не сработала. Дословный текст вопроса и формат ответа — единственный источник в `/skill-gap` §⛳ (там же — вход-конец рефлекса).
2. **⚠️ AK-47 guard — a skill is just a `SKILL.md`.** One markdown file with a procedure, NOT a server / DB / webhook / external service. (This is the exact trap the Codex milestone-retro report fell into — over-engineered for a SWE team; rejected 2026-06-18.) If the thing genuinely needs more than a markdown procedure, flag it **⚠️ УСЛОЖНЕНИЕ** and let dev decide.
3. **OFFER as ДО→ПОСЛЕ** (per `show-before-after`) — one compact block:
   > **ЧТО:** собрать `/<имя-скилла>` · **ДО:** как делаю руками сейчас (на реальном примере этой сессии) · **ПОСЛЕ:** одна команда `/<имя>` · **что сломается:** ничего (надстройка) · **делаем? да/нет**
4. **On dev's «+» → build it via `skill-creator`.** Pick the right home by SHAPE (per `operating-agreement` → «Where durable rules go»):
   - on-demand ritual I run when asked → **skill** (`skill-creator`).
   - «каждый раз автоматически когда X» → **hook** (skill `update-config`), not a skill.
   - time-based «каждый понедельник / каждое утро» → **scheduled task / routine** (skill `schedule`).
   - «рутина» ≠ обязательно 24/7-робот — часто правильное = простой полуавто + напоминание.
   - ⭐ **СПИСОЧНАЯ работа на N кусков (N велико) → КОНЕЧНАЯ рутина, «слон»** (dev 23.08, §4.5-бис).
     Признак: в сессии я перебирал однотипные элементы (видео / заметки / карточки / островá графа /
     ссылки), список не кончился, и он не кончится и в следующий раз; либо задача уже месяцами
     спотыкается об участие оператора, лимиты вендора или баны. Это НЕ задача и НЕ героическая сессия —
     это слон: `python ~/.claude/scripts/elephant.py new <slug> --title T --quota N --os-task <ЗадачаWindows>`,
     дальше рабочий скрипт на каждом прогоне делает `next` → работа → `mark` → `tick`.
     `tick` сам ловит конец (выключает OS-задачу + доклад в TG-03) и затык (5 пустых прогонов → `blocked`).
     ⛔ Журнал слона НИКОГДА не кладём в синкаемую папку — затрётся, и слон не кончится никогда.
     Живой пример: [[yt-watch-history-drip]]. Канон: [[finite-routines-eat-the-elephant]].
   Then route/link it normally (Step 4) and mention it in the final report (post-hoc, not for permission).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the ready `/compact` line (Step 6).
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Write a clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- The nightly **Brain Reindex @04:00** makes it `/ask`-searchable — no manual reindex needed.

**6a-бис. Снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- Команда: `python %USERPROFILE%\.claude\scripts\retro_lost_scan.py mark-done <sessionId> --note "ретро: <имя заметки>"`
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6b. Hand dev the ready paste-block** — ⚠️ CORRECTED 2026-07-22: bare `/compact` does NOT read `CLAUDE.md § Compact Instructions`. That earlier claim was FALSE — PreCompact hooks cannot inject instructions (only block; issue #14160 pending), and the evidence is 354/354 past compacts came out in the DEFAULT English template. Our 7-header format is applied ONLY when the block is pasted INLINE after the command: `/compact <text>`. So PRINT the fenced «Готовая строка» block from `$USERPROFILE/.claude/compact-prompt.md` and tell dev to PASTE it right after `/compact`. Then the fork:
> **«Готово, всё в волте. Хочешь остаться в задаче налегке — ВСТАВЬ блок ниже целиком после `/compact` (без него сжатие пойдёт по дефолтному английскому шаблону, не по нашему 7-заголовочному). Или новый чат — всё уже заархивировано, не зависит от нажатия.»**
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; the squeeze + paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

---

**Claude:**

Ретро. Сначала дешёвые проверки: журнал поломок, статус раскатки по флоту, компакт-блок.

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\fleet_fix_audit.py --by-fix home-dir-guard-2026-08-24 2>&1 | Select-Object -First 25", "description": "Fleet audit for home-dir-guard rollout status"}

---

> `Grep` -- {"pattern": "home.?dir", "path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "output_mode": "content", "-i": true}

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\fleet_fix_audit.py --by-fix home-dir-guard-2026-08-24 --force 2>&1 | Select-Object -First 25", "description": "Fleet audit for home-dir-guard (--force: dev asked for rollout status right now, gate already counted today's run)"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "offset": 1050, "limit": 15}

---

> `PowerShell` -- {"command": "$p = \"$env:MACHINE_BUS_DIR\\_deploy\\payloads\\home-dir-guard-2026-08-24\"; New-Item -ItemType Directory -Force $p | Out-Null; Copy-Item C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.py $p; Copy-Item C:\\Users\\dev\\.claude\\hooks\\home_dir_guard.cmd $p; Copy-Item C:\\Users\\dev

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_deploy\\payloads\\home-dir-guard-2026-08-24\\README-INSTALL.md", "content": "# home-dir-guard-2026-08-24 — payload (самодостаточный)\n\nГруз для деплоя `home-dir-guard-2026-08-24`. Раньше манифест ссылался на файлы,\nкоторые ехали только п

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK: ПОПРАВКА к home-dir-guard (мой пред. TASK был дырявый - apply-скрипта у вас НЕТ, спасибо ретро NODE-0X за улику). Груз теперь самодостаточный и синкается: _machine-bus/_deploy/payloads/home-dir-guard-2026-08-24/ - там README-I

---

> `Grep` -- {"pattern": "apply.{0,40}(не доставля|доставк|deliver)|deploy.{0,30}payload|apply-gap", "path": "D:\\Vault\\Vault-Knowledge\\10-Tasks", "output_mode": "files_with_matches", "-i": true}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-23-repair-apply-не-доставляющий.md", "limit": 40}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-22-repair-apply-не-доставляющий.md", "limit": 30}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-22-repair-apply-не-доставляющий.md", "old_string": "touched_at: 2026-08-22", "new_string": "touched_at: 2026-08-24"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-22-repair-apply-не-доставляющий.md", "old_string": "## Сделано, когда", "new_string": "- 2026-08-24 00:5x (NODE-0X) · **5-й и 6-й случаи одной ночью**: clobber-guard-20260822 (verify-тест отсутствует локально и 

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "old_string": "- 2026-08-24 08:4x-08:5x (хаб HUB-01, сессия 39f65ef1, recall+ретро)", "new_string": "- 2026-08-24 ~09:00 (хаб, сессия bca44929, раскатка home-dir-guard) · **7-е касание класса 

---

**Claude:**

Пишу ретро-заметку в волт и снимаю сессию с очереди догонялки:

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-08-24-home-dir-guard-fleet-rollout.md", "content": "---\ntitle: \"Retro: home-dir-guard — раскатка на флот + дыра apply-не-доставляет закрыта payload-ом\"\naliases: [\"Ретро: сторож чужой рабочей папки на весь

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\retro_lost_scan.py mark-done s_1b42f78a --note \"ретро: retro-2026-08-24-home-dir-guard-fleet-rollout.md\"; Add-Content -Encoding utf8 \"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\" \"\"", "descripti

---

> `Grep` -- {"pattern": "retro-2026-08-24", "path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros", "output_mode": "files_with_matches"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "old_string": "симптом закрыт тем же заходом: самодостаточный payload в `_deploy/payloads/home-dir-guard-2026-08-24/` + поправка по шине; корень класса — карточке", "new_string": "симптом закрыт тем 

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\compact-prompt.md"}

---

**Claude:**

понедельник, утро, 09:02, 24 августа 2026

Готово: проверил (уже было начато другой сессией), доложил раскатку до конца, закрыл найденную по ходу дыру, тесты зелёные, ретро записано.

**🔎 Сверка** (checked: deploy-реестр `_deploy` · журнал поломок · реестр задач 10-Tasks · шина за 3ч):
- ✅ Другая сессия хаба сегодня в 08:43 уже зарегистрировала деплой `home-dir-guard-2026-08-24` на все 6 узлов и применила на хабе. Дубль не строил.
- ⚠️ Но её раскатка была дырявой: apply-скрипт существовал только на хабе — к пирам он не ехал (это поймало ретро NODE-0X, 6-й случай класса «apply не доставляет»). Мой первый TASK по шине эту дыру унаследовал.
- 🔗 Закрыл в тот же заход: самодостаточный payload (5 файлов + README) положен в синкаемую `_deploy\payloads\home-dir-guard-2026-08-24\`, поправочный TASK разослан dual-send (файл + TG-03).

**🎬 Арка:** вопрос про папку → замер (6790 сессий хаба жили с чужой памятью) → сторож уже построен соседями → я добавил исключения (worktrees, scratchpad), проверил хаб (verify exit 0, тест PASS 7, битый конфиг не роняет старт), разослал флоту задачу с грузом. Узлы сами впишут свои родные папки в `home_dirs.json` — я чужие кабинеты не выдумываю.

**🎙 Майк:** 💰 прямых денег нет, но класс «чужая память» ел качество каждой второй сессии хаба — это налог на всё. 🔪 убил бы первый broadcast без проверки, что груз едет: 2 минуты чтения журнала сэкономили бы дубль-сообщение. 🤺 спорил честно: не стал заполнять чужие папки наугад, хоть так было бы «быстрее». ❓ вопрос: ярлык/терминал на хабе до сих пор открывается не в родной папке — дать сессию, чтобы починить сам вход, а не только сигналку?

**♻️ Reuse:** сторож+установщик 🟢 (чужие, сессии 6270af26 — не присваиваю; tested ✅) · payload-папка 🟢 tested ✅ (файлы на месте, синк донесёт) · мои правки home_dirs.json 🟢 tested ✅.

**🔗 Connect:** ✅ хаб использует (хук в settings.json, verify 0) · 🔗 5 узлов — передано, ждёт применения (PENDING + TASK + payload; законное ожидание) · ⚠️ в воздух — ничего.

**🩹 Журнал:** +1 строка (7-е касание класса «apply не доставляет», с уликой и линками); живая P0-карточка [task-2026-08-22-repair-apply-не-доставляющий.md](D:/Vault/Vault-Knowledge/10-Tasks/task-2026-08-22-repair-apply-не-доставляющий.md) пополнена случаями 5–7 — forever-fix (гейт упаковщика в deploy_register) остаётся ей, дубль-сессию не плодил.

**⛳ Дрифт:** цель = раскатка+ретро; унесло в 1 тему (класс apply-не-доставляет) → 📋 в существующую карточку, новых сессий 0. **🗺 Roadmap:** ⏸ без движения (внутренняя инфра). **📋 Журнал:** +0 новых · закрыто 0 · обновлена 1.

**📌 Открыто:** ACK от 5 узлов в 03 (молчание >24ч = добиваю поимённо); родные папки 4 узлов в `home_dirs.json` — заполняют сами.

**🗜 Компакт:** ретро в волте: [retro-2026-08-24-home-dir-guard-fleet-rollout.md](D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-08-24-home-dir-guard-fleet-rollout.md), с очереди догонялки сессия снята. Хочешь остаться в этом чате налегке — вставь после `/compact` блок:

```text
Сохрани ДОСЛОВНО по 7 заголовкам: РЕШЕНИЯ — родная папка хаба E:\!CLAUDE-HUBPC-June26; сторож home_dir_guard стоит на SessionStart; узлы сами вписывают свои папки в home_dirs.json; дубль-сессию по классу apply-не-доставляет не плодим (карточка task-2026-08-22 open). TODO — ACK 5 узлов в 03; forever-fix гейта упаковщика deploy_register (карточка P0). СЕЙЧАС — раскатка home-dir-guard-2026-08-24: хаб ✅, 5 узлов PENDING+payload в шине. ПУТИ — ~/.claude/hooks/home_dir_guard.py|.cmd, ~/.claude/home_dirs.json, ~/.claude/scripts/home_dir_guard_install.py (+_test), _machine-bus/_deploy/payloads/home-dir-guard-2026-08-24/. СЧЁТЧИКИ — тест PASS 7, verify exit 0, класс apply-не-доставляет 7 касаний. ОТКРЫТО — родные папки 4 узлов не заполнены (сторож там молчит); вход в терминал хаба открывается не в родной папке. ИНСТРУМЕНТЫ — bus_send требует «TASK:», сторож fail-open, BOM из PS-пайпа lstrip.
```

🧒 Простыми словами: ты попросил раздать звоночек всем компам. Оказалось, коробку с звоночками уже собрали утром, но грузовик поехал пустой — бумажка с заданием была, а самих звоночков в кузове не было. Я это заметил по записке с другого компа, положил звоночки в кузов, отправил грузовик заново и записал в журнал, чтобы грузовики больше не ездили пустыми.

понедельник, утро, 09:03, 24 августа 2026

---

**User:**

да, почини сам вход - чтобы терминал открывался в родной папке

---

**Claude:**

понедельник, утро, 09:14, 24 августа 2026

🎙 Майк: чиню вход, а не сигналку — правильный ход. Сначала смотрю, какие входы есть (Windows Terminal, профиль PowerShell, ярлыки), потом правлю аккуратно, чтобы не сломать роботов.

---

> `PowerShell` -- {"command": "$wt = \"$env:LOCALAPPDATA\\Packages\\Microsoft.WindowsTerminal_8wekyb3d8bbwe\\LocalState\\settings.json\"; Write-Host \"WT settings exists: $(Test-Path $wt)\"; Write-Host \"PS profile path: $PROFILE, exists: $(Test-Path $PROFILE)\"; if (Test-Path $PROFILE) { Get-Content $PROFILE }; Writ

---

> `PowerShell` -- {"command": "$wt = \"$env:LOCALAPPDATA\\Packages\\Microsoft.WindowsTerminal_8wekyb3d8bbwe\\LocalState\\settings.json\"; $j = Get-Content $wt -Raw | ConvertFrom-Json; Write-Host \"defaults:\"; $j.profiles.defaults | ConvertTo-Json -Depth 5; Write-Host \"profiles:\"; $j.profiles.list | ForEach-Object 

---

> `PowerShell` -- {"command": "$wt = \"$env:LOCALAPPDATA\\Packages\\Microsoft.WindowsTerminal_8wekyb3d8bbwe\\LocalState\\settings.json\"; Copy-Item $wt \"$wt.bak-20260824-0915\"; $raw = Get-Content $wt -Raw; $j = $raw | ConvertFrom-Json; $j.profiles.defaults | Add-Member -NotePropertyName startingDirectory -NotePrope

---

> `PowerShell` -- {"command": "$wt = \"$env:LOCALAPPDATA\\Packages\\Microsoft.WindowsTerminal_8wekyb3d8bbwe\\LocalState\\settings.json\"; $j = Get-Content $wt -Raw | ConvertFrom-Json; Write-Host \"profiles: $($j.profiles.list.Count), defaultProfile: $($j.defaultProfile), schemes: $($j.schemes.Count)\"; $sh = New-Obje

---

**Claude:**

Вход починен. Теперь второй вопрос — файлы. Смотрю, что реально накопилось в «неправильных» местах:

---

> `PowerShell` -- {"command": "foreach ($d in 'C:\\Users\\dev\\!CLAUDE-NODE-0X May26','C:\\Users\\dev\\!CLAUDE-NODE-0X May26') { if (Test-Path $d) { $files = Get-ChildItem $d -Recurse -File -ErrorAction SilentlyContinue; \"{0}: {1} files, {2:N1} MB, newest: {3}\" -f $d, $files.Count, (($files | Measure-Object Length -Sum).

---

> `PowerShell` -- {"command": "Get-ChildItem 'C:\\Users\\dev\\!CLAUDE-NODE-0X May26' -Recurse -File -ErrorAction SilentlyContinue | Sort-Object LastWriteTime -Descending | Select-Object -First 8 | ForEach-Object { \"$($_.LastWriteTime) | $($_.FullName.Substring(29))\" }; Write-Host '--- who syncs what: syncthing folder an

---

**Claude:**

Синк эти папки НЕ ведёт — значит пишет кто-то локальный. Смотрю, кто трогал ноутбучную папку сегодня в 08:15:

---

> `PowerShell` -- {"command": "Get-ChildItem 'C:\\Users\\dev\\!CLAUDE-NODE-0X May26' -Recurse -File -ErrorAction SilentlyContinue | Sort-Object LastWriteTime -Descending | Select-Object -First 12 | ForEach-Object { \"$($_.LastWriteTime) | $($_.FullName.Substring(33))\" }", "description": "List freshest files in the la

---

> `PowerShell` -- {"command": "schtasks /query /fo csv | ConvertFrom-Csv | Where-Object { $_.TaskName -match 'arxiv|backup|gmail' } | Select-Object TaskName, 'Next Run Time' | Format-Table -AutoSize; Write-Host '--- who references the legacy paths ---'; Get-ChildItem 'C:\\Users\\dev\\.claude\\scripts','D:\\Vault

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__create_scheduled_task", "max_results": 1}

---

> `mcp__scheduled-tasks__create_scheduled_task` -- {"taskId": "auto-hub-260824-NODE-0X-folder-cleanup", "description": "Переселить хабовские артефакты и роботов из миграционных папок !CLAUDE-NODE-0X May26 в родную E:\\!CLAUDE-HUBPC-June26", "fireAt": "2026-08-24T09:25:00+01:00", "notifyOnCompletion": true, "prompt": "Продолжи задачу: расселение «чужи

---

**Claude:**

понедельник, утро, 09:19, 24 августа 2026

Вход починен, а вопрос про файлы оказался глубже, чем выглядел — разобрал и запустил расселение.

**1. Терминал теперь открывается в родной папке.** Причина промахов была простая: у Windows Terminal нигде не был задан `startingDirectory`, поэтому каждый новый таб стартовал в `C:\Users\dev` — отсюда и 4370 «чужих» сессий. Поставил дефолт `E:\!CLAUDE-HUBPC-June26` для всех профилей (PowerShell, cmd), с бэкапом настроек и проверкой, что JSON цел. Профиль PowerShell трогать не стал сознательно: авто-`cd` в профиле ловили бы и роботы-планировщики, а это риск сломать их относительные пути. Оставшиеся 2420 сессий «из System32» — это как раз роботы; их лечит уже стоящий сторож home_dir_guard плюс порядок в задачах планировщика (отдельная тема).

**2. Файлы: переносить стоит, но не скопом — и вот почему.** Проверил обе «неправильные» папки. Это не зеркало ноутбука (Syncthing их не синкает — проверено по конфигу), а остатки миграции May26, внутри которых **до сих пор живут хабовские роботы**: `ArXiv Submit Watch` пишет туда логи (последняя запись сегодня 08:15, следующий запуск 12:15), утренний ремонт Claude Desktop сложил туда свои бэкапы, в старой папке профиля `_` лежат свежие уроки vibe-teach и статус ночного бэкапа. Решение как кофаундер: живых писателей переселить, хабовские артефакты перенести, а 24-гигабайтный миграционный слепок **не удалять** — это необратимое, решишь сам по итогам аудита (архив на F: или корзина).

**3. Сессия-исполнитель уже поднята** (видимая, `auto-hub-260824-NODE-0X-folder-cleanup`, старт в 09:25): переселит роботов с доказательством «лог пишется в новом месте», перенесёт артефакты, посчитает остаток и принесёт тебе один вопрос — «архив или удалить». Придёт уведомление по завершении.

🧒 Простыми словами: дверь в дом теперь сама ведёт в правильную комнату — я перенастроил терминал. А в старой комнате, как выяснилось, не просто валяются коробки с переезда: там до сих пор работают два робота и лежат свежие вещи. Я послал уборщика: роботов пересадит в новую комнату, свежие вещи перенесёт, а про старые коробки спросит тебя — выбросить или убрать на чердак.

понедельник, утро, 09:19, 24 августа 2026

---

**User:**

Перенести все сам в нужные места

Сделай тесты

Выяви корни и почини

---

**Claude:**

понедельник, день, 14:02, 24 августа 2026

🎙 Майк: с 09:25 должна была отработать сессия-уборщик — сначала проверяю, что она реально сделала, потом добиваю сам остаток, тесты и корни.

---

> `PowerShell` -- {"command": "Write-Host '--- task card? ---'; Get-ChildItem 'D:\\Vault\\Vault-Knowledge\\10-Tasks' -Filter '*NODE-0X*' | Select-Object Name; Write-Host '--- freshest writes in both legacy folders ---'; foreach ($d in 'C:\\Users\\dev\\!CLAUDE-NODE-0X May26','C:\\Users\\dev\\!CLAUDE-NODE-0X May26') { if (Te

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-NODE-0X-folder-resettle.md"}

---

> `PowerShell` -- {"command": "$L = 'C:\\Users\\dev\\!CLAUDE-NODE-0X May26'; Get-ChildItem $L -Force | ForEach-Object { $t = if ($_.Attributes -band [IO.FileAttributes]::ReparsePoint) {'JUNCTION'} elseif ($_.PSIsContainer) {'dir'} else {'file'}; $sz = if ($t -eq 'dir') { '{0:N0} MB' -f ((Get-ChildItem $_.FullName -Rec

---

> `PowerShell` -- {"command": "$L='C:\\Users\\dev\\!CLAUDE-NODE-0X May26'; $N='E:\\!CLAUDE-HUBPC-June26'; foreach ($d in 'crm_export','_gdrive_index','downloads') { $before=(Get-ChildItem \"$N\\$d\" -Recurse -File -ErrorAction SilentlyContinue).Count; robocopy \"$L\\$d\" \"$N\\$d\" /E /XC /XN /XO /XJ /R:1 /W:1 /N

---

> `PowerShell` -- {"command": "Get-PSDrive F | Select-Object Used,Free; $L='C:\\Users\\dev\\!CLAUDE-NODE-0X May26'; $A='F:\\_archive-NODE-0X-remnant-20260824'; robocopy $L $A /MOVE /E /XJ /XD \"$L\\gmail\" \"$L\\secrets\" /XF '_READ-ME-FIRST.md' /R:1 /W:1 /NP /NDL /NFL /LOG:F:\\_backup-logs\\NODE-0X-remnant-move-20260824.lo

---

> `PowerShell` -- {"command": "Get-Content F:\\_backup-logs\\NODE-0X-remnant-move-20260824.log -Tail 8; Write-Host '--- legacy folder contents now ---'; Get-ChildItem 'C:\\Users\\dev\\!CLAUDE-NODE-0X May26' -Force | ForEach-Object { \"$($_.Attributes) | $($_.Name)\" }; Write-Host '--- archive spot-check ---'; (Get-ChildI

---

> `PowerShell` -- {"command": "Select-String -Path F:\\_backup-logs\\NODE-0X-remnant-move-20260824.log -Pattern 'Files :|Bytes :|FAILED' | Select-Object -Last 4 | ForEach-Object { $_.Line }", "description": "Read robocopy summary counters from move log"}

---

**Claude:**

FAILED 0. Обновляю маркер в старой папке и перехожу к тестам:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\_READ-ME-FIRST.md", "content": "# ⚠️ Эта папка — НЕ рабочая папка хаба (обновлено 2026-08-24 14:05)\n\nРодная рабочая папка хаба HUB-01: `E:\\!CLAUDE-HUBPC-June26`. Сессии Claude стартуют ТАМ.\n\nЧто здесь осталось (и почему трогать не

---

> `Read` -- {"file_path": "C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\_READ-ME-FIRST.md"}

---

> `Grep` -- {"pattern": "session_monitor", "path": "C:\\Users\\dev\\.claude", "output_mode": "content", "head_limit": 15}

---

> `Grep` -- {"pattern": "session_monitor", "path": "D:\\Vault\\_imports", "output_mode": "files_with_matches", "head_limit": 10}

---

> `PowerShell` -- {"command": "Get-ChildItem 'C:\\Users\\dev\\.claude\\skills\\fleet' -Recurse -File | Select-String -Pattern 'session_monitor' -List | ForEach-Object { $_.Path }; Write-Host '---'; Test-Path 'E:\\!CLAUDE-HUBPC-June26\\session_monitor.py'; schtasks /query /fo csv | ConvertFrom-Csv | Where-Objec

---

> `Grep` -- {"pattern": "session_monitor", "path": "C:\\Users\\dev\\.claude\\skills\\fleet\\SKILL.md", "output_mode": "content", "-C": 2}

---

> `PowerShell` -- {"command": "(Select-String -Path 'C:\\Users\\dev\\.claude\\skills\\fleet\\SKILL.md' -Pattern 'session_monitor').Line", "description": "Read the fleet skill line that calls session_monitor"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\settings.json", "old_string": "    \"CLAUDE_MEMORY_NAME\": \"P---WORKDIR-HUB\",", "new_string": "    \"CLAUDE_MEMORY_NAME\": \"P---WORKDIR-HUB\",\n    \"NATIVE_WORKDIR\": \"E:\\\\!CLAUDE-HUBPC-June26\","}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\fleet\\SKILL.md", "old_string": "`python \"$USERPROFILE/!CLAUDE-NODE-0X May26\\session_monitor.py\"` (snapshot)", "new_string": "`python \"${NATIVE_WORKDIR:-$USERPROFILE/!CLAUDE-NODE-0X May26}/session_monitor.py\"` (snapshot; NATIVE_W

---

> `PowerShell` -- {"command": "python 'E:\\!CLAUDE-HUBPC-June26\\session_monitor.py' 2>&1 | Select-Object -First 12; Write-Host \"exit: $LASTEXITCODE\"", "description": "Prove native session_monitor engine works (collision lens snapshot)", "timeout": 120000}

---

> `Grep` -- {"pattern": "sys\\.exit|exit\\(", "path": "E:\\!CLAUDE-HUBPC-June26\\session_monitor.py", "output_mode": "content", "-n": true}

---

> `PowerShell` -- {"command": "python 'E:\\!CLAUDE-HUBPC-June26\\session_monitor.py' 2>&1 | Select-Object -Last 6; Write-Host \"exit: $LASTEXITCODE\"", "description": "Read tail of session_monitor output to see why non-zero exit", "timeout": 120000}

---

> `PowerShell` -- {"command": "Select-String -Path 'C:\\Users\\dev\\.claude\\scripts\\oss-publish\\engine_queue.py','C:\\Users\\dev\\.claude\\scripts\\oss-publish\\passport_gen.py','C:\\Users\\dev\\.claude\\scripts\\oss-publish\\sanitize_skills.py' -Pattern 'sbsk' | ForEach-Object { \"$(Split-Path $_.Path -Leaf

---

> `PowerShell` -- {"command": "Get-ChildItem 'E:\\GitHub' -Directory -ErrorAction SilentlyContinue | Select-Object Name; Write-Host '--- what do the scripts say about sbsk purpose ---'; Get-Content 'C:\\Users\\dev\\.claude\\scripts\\oss-publish\\engine_queue.py' -TotalCount 30", "description": "List GitHub repos di

---

> `PowerShell` -- {"command": "Get-ChildItem 'E:\\!CLAUDE-HUBPC-June26\\public-repos' -Directory -ErrorAction SilentlyContinue | Select-Object Name", "description": "List public-repos in native folder"}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\oss-publish\\engine_queue.py", "old_string": "REPO = os.path.join(os.path.expanduser(\"~\"), \"!CLAUDE-NODE-0X May26\", \"sbsk\")", "new_string": "# SBSK_REPO env overrides; default = NODE-0X-native path (sbsk lives on the laptop on

---

> `PowerShell` -- {"command": "Select-String -Path 'C:\\Users\\dev\\.claude\\scripts\\oss-publish\\passport_gen.py' -Pattern 'REPO =' -Context 2,0 | ForEach-Object { $_.Context.PreContext + $_.Line }; Select-String -Path 'C:\\Users\\dev\\.claude\\scripts\\oss-publish\\sanitize_skills.py' -Pattern 'REPO =' -Contex

---

> `PowerShell` -- {"command": "$f='C:\\Users\\dev\\.claude\\scripts\\oss-publish\\passport_gen.py'; (Get-Content $f -Raw -Encoding UTF8) -replace [regex]::Escape('REPO = os.path.join(os.path.expanduser(\"~\"), \"!CLAUDE-NODE-0X May26\", \"sbsk\")'), 'REPO = os.environ.get(\"SBSK_REPO\") or os.path.join(os.path.expandu

---

> `PowerShell` -- {"command": "$enc = New-Object System.Text.UTF8Encoding($false); foreach ($p in 'C:\\Users\\dev\\.claude\\scripts\\oss-publish\\passport_gen.py','C:\\Users\\dev\\.claude\\scripts\\oss-publish\\sanitize_skills.py') { $t = [IO.File]::ReadAllText($p); if ($t[0] -eq [char]0xFEFF) { $t = $t.Substring

---

**Claude:**

Корень №3 — два sync-conflict файла в `scripts\` (тихий признак драки машин за файл). Сверяю с живыми копиями:

---

> `PowerShell` -- {"command": "foreach ($base in 'github_traffic_snapshot','tg_bot_send') { $live = Get-ChildItem \"C:\\Users\\dev\\.claude\\scripts\\$base.py\" -ErrorAction SilentlyContinue; $conf = Get-ChildItem \"C:\\Users\\dev\\.claude\\scripts\\$base.sync-conflict-*.py\" -ErrorAction SilentlyContinue; if ($l

---

> `PowerShell` -- {"command": "foreach ($base in 'github_traffic_snapshot','tg_bot_send') { $conf = (Get-ChildItem \"C:\\Users\\dev\\.claude\\scripts\\$base.sync-conflict-*.py\").FullName; Write-Host \"=== $base : diff (conflict vs live), first 15 lines ===\"; git diff --no-index --stat \"$conf\" \"C:\\Users\\dev

---

> `PowerShell` -- {"command": "Remove-Item 'C:\\Users\\dev\\.claude\\scripts\\github_traffic_snapshot.sync-conflict-20260729-160651-JR2M6T4.py','C:\\Users\\dev\\.claude\\scripts\\tg_bot_send.sync-conflict-20260729-160654-JR2M6T4.py' -Confirm:$false; Write-Host 'conflicts deleted'; Write-Host '--- retro-lost skill

---

> `Grep` -- {"pattern": "/projects", "path": "C:\\Users\\dev\\.claude\\skills\\retro-lost\\SKILL.md", "output_mode": "content", "-n": true}

---

> `Grep` -- {"pattern": "def |скилл|SKILL_RE|re\\.compile", "path": "C:\\Users\\dev\\.claude\\scripts\\_test_skill_refs.py", "output_mode": "content", "-n": true, "head_limit": 20}

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_skill_refs.py", "offset": 90, "limit": 18}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\_test_skill_refs.py", "old_string": "    \"the\", \"and\", \"not\", \"for\", \"with\", \"from\", \"que\", \"com\", \"org\", \"net\",\n}", "new_string": "    \"the\", \"and\", \"not\", \"for\", \"with\", \"from\", \"que\", \"com

---

> `PowerShell` -- {"command": "python 'C:\\Users\\dev\\.claude\\scripts\\_test_skill_refs.py' 2>&1 | Select-Object -Last 4; Write-Host \"skill_refs exit: $LASTEXITCODE\"; python 'C:\\Users\\dev\\.claude\\scripts\\_test_home_dir_guard.py'; Write-Host \"home_dir_guard exit: $LASTEXITCODE\"; python 'C:\\Users\\dev

---

**Claude:**

Три теста зелёные. По §4.9 — коммит с отпечатком автора на правки кода:

---

> `PowerShell` -- {"command": "Set-Location C:\\Users\\dev\\.claude; git status --short -- scripts/_test_skill_refs.py scripts/oss-publish/ skills/fleet/SKILL.md scripts/github_traffic_snapshot.sync-conflict-20260729-160651-JR2M6T4.py scripts/tg_bot_send.sync-conflict-20260729-160654-JR2M6T4.py 2>&1 | Select-Object

---

**Claude:**

Авто-снапшот уже утащил правки (транспорт ≠ автор по §4.9) — оставляю отпечаток авторства поверх:

---

> `PowerShell` -- {"command": "Set-Location C:\\Users\\dev\\.claude; git commit --allow-empty -m @'\nprovenance: NODE-0X-resettle roots fixed (files rode in auto-snapshot 24437ee)\n\n- skills/fleet/SKILL.md: collision lens path -> ${NATIVE_WORKDIR:-NODE-0X path}\n- settings.json env: +NATIVE_WORKDIR (hub)\n- scripts/oss

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\_READ-ME-FIRST.md", "old_string": "## 🗄 ОСТАЛЬНОЕ — слепок миграции с ноутбука (май-июнь 2026)\n\n~2.2 ГБ / 738 файлов. Живых писателей нет (проверено: за 7 дней писали только `gmail\\`).\n`downloads\\` (1.17 ГБ, 190 файлов) 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\!CLAUDE-NODE-0X May26\\_READ-ME-FIRST.md", "old_string": "**`session_monitor.py`** — движок линзы коллизий скилла `/fleet`. Копия синхронна с\nродной (24.08.2026), обе выводят пути из env.", "new_string": "**`session_monitor.py`** — уехал: живёт то

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-NODE-0X-folder-resettle.md", "old_string": "review_after: 2026-09-24\nreview_note: \"вернуться, когда оператор решит судьбу слепка 2.2 ГБ (архив на F: или удаление)\"", "new_string": "review_after: 2026-09-24\nre

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "old_string": "- 2026-08-24 08:4x-08:5x (хаб HUB-01, сессия 39f65ef1, recall+ретро)", "new_string": "- 2026-08-24 ~14:05 (хаб, сессия bca44929, расселение NODE-0X) · **3-е датированное касание се

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md", "old_string": "симптом починен ([IO.File]::WriteAllText UTF8(false)); по §5.10 положена отдельная сессия починки класса · туда же: [[task-2026-08-24-ps51-encoding-class]]", "new_string": "симптом поч

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-ps51-encoding-class.md", "content": "---\nid: task-2026-08-24-ps51-encoding-class\ntitle: \"Класс «PowerShell 5.1 кодировка молча ломает» стал системным (3 касания) — отдельная сессия починки\"\nstate: open\ntype: infra\npriorit

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\10-Tasks\\task-2026-08-24-ps51-encoding-class.md", "content": "---\nid: task-2026-08-24-ps51-encoding-class\ntitle: \"Класс «PowerShell 5.1 кодировка молча ломает» стал системным (3 касания) — отдельная сессия починки\"\nstate: open\ntype: infra\npriorit

---

**Claude:**

Входящий линк уже стоит в журнале (реверс-индекс просто отстаёт). Поднимаю видимую сессию починки класса:

---

> `mcp__scheduled-tasks__create_scheduled_task` -- {"taskId": "auto-hub-260824-ps51-encoding-class", "description": "Закрыть системный класс «PowerShell 5.1 кодировка молча ломает» (3 датированных касания)", "fireAt": "2026-08-24T14:25:00+01:00", "notifyOnCompletion": true, "prompt": "Продолжи задачу task-2026-08-24-ps51-encoding-class (карточка: E:

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK: NODE-0X-2023PAL и NODE-0X - verify BOM-детектора (класс PS5.1-кодировок, карточка task-2026-08-24-ps51-encoding-class). Файлы _shared/bom_scan.py + _test_bom_scan.py и починенный os_task_watchdog.ps1 едут к вам синко

---

**Claude:**

понедельник, день, 15:20, 24 августа 2026

Всё три пункта закрыты. По порядку:

**1. Перенесено всё.** Сначала слияние: robocopy-merge `crm_export`, `_gdrive_index`, `downloads` в родную папку дал **0 новых файлов** — остаток был полными дублями (это же подтвердило вывод утренней сессии). Затем весь слепок — 738 файлов / 2.2 ГБ — уехал одним махом в `F:\_archive-NODE-0X-remnant-20260824\` (FAILED 0, лог на F:). В старой папке остались ровно три вещи, и все по делу: `gmail\` (единственный дом коннектора по датированному решению 05.08, его охраняет гейт-тест), junction `secrets` (не папка, а ссылка на родную) и обновлённый README-маркер. Ничего не удалено безвозвратно — всё в архиве.

**2. Тесты зелёные:** `_test_skill_refs` exit 0 (было красное), `_test_home_dir_guard` PASS 7, `_test_gmail_connector_single_home` exit 0, линза коллизий `/fleet` с родной копии — exit 0, robocopy FAILED 0.

**3. Корни выявлены и починены — пять штук:**
- `/fleet` звал линзу по ноутбучному пути (работало только через остаток — я сам чуть не сломал это переездом, поймал по README). Корень-фикс: переменная `NATIVE_WORKDIR` в settings.json хаба + фоллбэк для NODE-0X в скилле.
- Тот же класс в `oss-publish` (3 скрипта с прибитым путём `sbsk`, которого на хабе нет вовсе — репо живёт на ноутбуке): env-переопределение `SBSK_REPO`, ноутбук не тронут.
- `_test_skill_refs` красил `retro-lost` из-за stignore-паттерна `/projects`, принятого за слэш-команду — добавил в словарь ложных срабатываний детектора.
- Два протухших sync-conflict файла в `scripts\` — живые копии оказались строгими надмножествами, конфликты удалены.
- И главный сюрприз: по ходу починки PS 5.1 снова подсунул BOM в файлы — **3-е касание класса за месяц**, объявил его системным. Пока моя сессия висела на разрешении, проталкиватель зависших сессий уже закрыл класс: корень доказан (в PS 5.1 просто нет «UTF-8 без BOM»), построен BOM-детектор в регресс-сетке, который с первого прогона поймал ещё 2 живых BOM-файла в проде и вылечил их писателя. Я добил его хвост: разослал verify-задачу на NODE-0X и ноут Норы по шине.

Отпечаток автора на правках — коммит `84b8531` с 4 трейлерами. Открытым остаётся только: ACK от узлов по home-dir-guard (утренняя раскатка) и по BOM-verify — молчание больше суток буду добивать поимённо.

🧒 Простыми словами: из старой комнаты вывезли все коробки — сначала проверили, что ничего ценного в них нет (всё оказалось копиями), потом отвезли на склад с описью. В комнате остались только почтовый ящик, которому положено там висеть, и табличка «здесь больше не живут». А ещё нашли пять кривых указателей, из-за которых люди и роботы вообще забредали в эту комнату, и все пять перевесили правильно. Один из ремонтов успел сделать робот-помощник, пока я стоял в очереди — я только проверил за ним и разослал контрольки.

понедельник, день, 15:20, 24 августа 2026

---

**User:**

На флот раскатай Нужно, чтобы весь плот наш тоже сделал у себя аналогичный функционал, чтобы есть ли юзер на какой-то машине выбирать неправильную папку, чтобы мы об этом сказали. Ну, и сам подумать, что еще в этой сессии мы ценного сделали, чтобы все это использовалось всеми нашими машинами на всем нашем флоте?

---

**Claude:**

понедельник, день, 15:39, 24 августа 2026

🎙 Майк: правильная жадность — выжать из сессии всё переносимое. План: (1) апгрейдить установщик сторожа до «полного входа» — сторож + `NATIVE_WORKDIR` + починка терминала, одним скриптом на каждом узле; (2) обновить payload в шине; (3) разослать флоту список всей ценности сессии. Поехали.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py", "offset": 60, "limit": 10}

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py", "old_string": "def apply() -> int:\n    if registered():\n        print(\"[install] OK уже зарегистрирован — no-op\")\n        return check_registry()", "new_string": "def my_home() -> str:\n    \"\"

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py", "old_string": "    os.replace(tmp, SETTINGS)\n    print(\"[install] hook зарегистрирован в settings.json (бэкап: %s)\" % os.path.basename(bak))\n    return check_registry()", "new_string": "    os.re

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py", "old_string": "def verify() -> int:\n    ok_reg = registered()\n    ok_test = run_test()\n    print(\"[verify] registered=%s test=%s\" % (ok_reg, ok_test))\n    return 0 if (ok_reg and ok_test) else 

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py", "old_string": "--verify: exit 0 only when (a) hook is registered in settings.json AND\n  (b) scripts/_test_home_dir_guard.py passes. Exit 1 otherwise.", "new_string": "v2 (2026-08-24, приказ «раската

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py; Write-Host \"apply exit: $LASTEXITCODE\"; python C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py --verify; Write-Host \"verify exit: $LASTEXITCODE\"", "description": "Run installer v2 live on hub (expect

---

**Claude:**

Живой прогон на хабе зелёный и идемпотентный. Теперь красно-зелёный тест «свежего узла» в песочнице:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\_test_installer_v2.py", "content": "# -*- coding: utf-8 -*-\n\"\"\"Sandbox red/green test for home_dir_guard_install.py v2 (fresh-node simulation).\"\"\"\nim

---

> `PowerShell` -- {"command": "python \"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\_test_installer_v2.py\"; Write-Host \"exit: $LASTEXITCODE\"", "description": "Run sandbox red/green test of installer v2", "timeout": 120000}

---

> `PowerShell` -- {"command": "$p = \"$env:MACHINE_BUS_DIR\\_deploy\\payloads\\home-dir-guard-2026-08-24\"; Copy-Item C:\\Users\\dev\\.claude\\scripts\\home_dir_guard_install.py $p -Force; Copy-Item C:\\Users\\dev\\.claude\\home_dirs.json $p -Force; Get-ChildItem $p | Select-Object Name, LastWriteTime; Set-Locati

---

> `PowerShell` -- {"command": "Set-Location C:\\Users\\dev\\.claude; git log --oneline -2; git commit --allow-empty -m @'\nprovenance: home_dir_guard_install v2 (rode in auto-snapshot)\n\nsentry + entry in one installer: NATIVE_WORKDIR env + WT startingDirectory,\nsandbox red/green PASS 6. Payload refreshed in _mac

---

**Claude:**

Проверяю подозрительное «clean» — не игнорирует ли git этот файл:

---

> `PowerShell` -- {"command": "Set-Location C:\\Users\\dev\\.claude; git ls-files scripts/home_dir_guard_install.py scripts/_test_skill_refs.py skills/fleet/SKILL.md; Write-Host '---'; git check-ignore -v scripts/home_dir_guard_install.py scripts/oss-publish/engine_queue.py settings.json 2>&1", "description": "Chec

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\bus_send.py \"TASK: всем узлам - ВХОД В РОДНУЮ ПАПКУ, установщик обновлён до v2 (приказ оператора 24.08: 'весь флот тоже сделал у себя аналогичный функционал'). Груз обновлён в _machine-bus/_deploy/payloads/home-dir-guard-2026-08-24/ (README-INSTA

---

**Claude:**

Последний штрих — память, чтобы любая будущая сессия хаба знала эту механику:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\native-workdir-entry-rail.md", "content": "---\nname: native-workdir-entry-rail\ndescription: Родная папка узла = home_dirs.json + env NATIVE_WORKDIR + сторож home_dir_guard + вход терминала; установщик один\nm

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)", "new_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка раз

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка разносит по § и хабам)", "new_string": "## 📥 INBOX — новые строки ТОЛЬКО сюда (append-only; уборка раз

---

**Claude:**

понедельник, день, 15:47, 24 августа 2026

Раскатал. И вот полная опись ценности сессии — что и как едет на флот:

**1. Главное — установщик обновлён до v2: теперь он чинит не только «сигналку», но и сам вход.** Один скрипт `home_dir_guard_install.py` на каждом узле делает три вещи: ставит SessionStart-сторож чужой папки, прописывает `NATIVE_WORKDIR` в settings.json узла и (на Windows) сам переключает Windows Terminal на родную папку — с бэкапом и fail-open, если терминала нет. Проверено двумя способами: вживую на хабе (идемпотентно, verify exit 0) и песочницей «свежего узла» — красный до установки, зелёный после, битый конфиг терминала не роняет установку (PASS 6 проверок). Payload в шине обновлён, TASK разослан по обоим рельсам. Макам честно сказано: шага для их терминала в скрипте нет — дефолтную папку Terminal/iTerm правят сами, строка в `home_dirs.json` обязательна для всех.

**2. Что едет само, без задач** (синк `~/.claude`): BOM-детектор с тестом в регресс-сетке, фикс `sbsk`-путей (`SBSK_REPO` env), фикс ложного срабатывания `_test_skill_refs`, строка `/fleet` через `${NATIVE_WORKDIR}`.

**3. Что закреплено как знание** (синкаемый волт + память): карточка класса «apply не доставляет» с уроком «манифест обязан ссылаться только на файлы из payload», карточка класса PS 5.1-кодировок (закрыт, ждёт verify с двух узлов), ретро-заметка, и новая память `native-workdir-entry-rail` — чтобы будущие скиллы писали пути через `${NATIVE_WORKDIR}`, а не хардкодом (именно хардкод пути узла в общем скрипте — корень, из-за которого сегодня чинил и `/fleet`, и `sbsk`).

**Открытые хвосты, все с механизмом дожима:** ACK от 5 узлов по входу v2, BOM-verify от двух Windows-узлов. Молчание сутки — добью поимённо. ⚠️ Попутная строка-репорт: MEMORY.md в красной зоне (6 строк >150 зн.) — ждёт суточного оптимизатора, по ходу не жал.

🧒 Простыми словами: мы не просто повесили звоночки на все дома — мы разослали всем один набор мастера: звоночек «ты не в той комнате», табличку с адресом родной комнаты и отвёртку, которая сама перенастраивает входную дверь, чтобы она открывалась куда надо. Виндовым домам дверь чинится автоматом, Макам — инструкция. Плюс разослали все мелкие находки дня: ловушку для невидимого мусора в файлах (BOM) и правило «не прибивать чужие адреса гвоздями в общих инструментах».

понедельник, день, 15:47, 24 августа 2026

---

**User:**

может сделаем /share-fix ? раздадим эту тулзу \ ноухау общественности

это ЧАСТАЯ ОШИБКА!!

---

**Claude:**

понедельник, вечер, 18:38, 24 августа 2026

🎙 Майк: скилл `/share-fix` уже существует (твой же декрет сегодняшнего дня, прецедент — MSIX-лечилка). Не строю второй — запускаю его на нашу лечилку «чужой рабочей папки».

---

> `Skill` -- {"skill": "share-fix", "args": "home_dir_guard: SessionStart-сторож чужой рабочей папки Claude Code (память привязана к cwd) + NATIVE_WORKDIR + починка входа терминала"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\share-fix

# /share-fix — 🌍 починил у себя → сразу раздай миру

**Канон:** Библия `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world` + CLAUDE.md §4.7. Логика оператора: в момент починки у нас в руках лучший поисковый ключ на свете — дословный симптом; никакой «робот-сканер всего GitHub» не сравнится с реверс-поиском того, кто только что дебажил. Поэтому раздача = ритуал в момент фикса, не фоновый сканер.

## Шаг 0 — порог (2 булевых, оба ДА, иначе честный ⛔)
1. **Переносимость:** чужой человек может воспроизвести наш симптом БЕЗ наших внутренностей (наших скриптов, нашей инфры, наших аккаунтов)? Одноразовый глюк самоделки миру не нужен.
2. **Чистота:** в раздаваемом нет секретов/приватного/внутренних имён (аккаунты, задачи, пути с личным)? Скрипт для мира = НОВЫЙ чистый файл на английском, не внутренняя кнопка. Леак-скан глазами обязателен.

## Шаг 1 — реверс-поиск по ДОСЛОВНОМУ симптому (2 минуты)
```bash
gh search issues "<симптом дословно: код ошибки / статус / текст диалога>" --limit 30 --sort updated
```
Пробуй 2-3 формулировки (код ошибки `0x…`, статус `Modified, NeedsRemediation`, фраза из диалога). Пусто везде → вердикт ⚪ с названным запросом, конец.

## Шаг 2 — отобрать 3-5 ЛУЧШИХ живых тредов (dev капсом: «ТРИ - ПЯТЬ, не 1-2»)
Критерии лучшего: живой (человеческая активность, не бот-бампы) · наш симптом там воспроизведён (не однословная коллизия) · есть кому помочь (страдальцы без решения). Дедуп: проверь, нет ли нас (tonydzi) уже в треде. Перекрёстно-связанные треды одного класса сверх 5 — НЕ слать: 7-й одинаковый коммент = веер. Ужимание до 1-2 «чтобы не отсвечивать» — нарушение §1.5 точно так же.

## Шаг 3 — раздать: каждый коммент ЗАТОЧЕН под тред
- Раскрытие Майкрофта первой строкой (§3.3), дальше — по существу ИХ улик: что у них в треде уже есть и как наша находка это дополняет/объясняет. Копипаста-веер ⛔.
- Скрипт-лечилка → публичный gist (после Шага 0.2) → ссылка. Ссылку в уже отправленные комменты дописывай ПРАВКОЙ своих сообщений, не новыми постами: `gh api -X PATCH repos/<r>/issues/comments/<id> -F body=@file`.
- Кросс-вендор: тот же класс болезни у codex/gemini-cli — тоже дверь (прецедент openai/codex#35347).

## Шаг 4 — вахта + вердикт (молчание запрещено)
```bash
python "$USERPROFILE/.claude/scripts/pr_watch.py" --add <url каждого треда>
```
Вердикт в отчёт, один из трёх: **🟢 раздал** (ссылки) · **⚪ искал-пусто** (запрос назван) · **⛔ непереносимо/приватно** (причина). Треды дальше веду САМ (реглумент `reglament-github-kommunikaciya-vsegda-sam`), показ в утреннем отчёте из `pr_watch --digest`; ответ живого инженера → /pr-reply Шаг 5-бис (контент-воронка).

## Границы
- Юридическое (CLA/DCO), деньги, секреты, масс-действия = Tier-2 → пауза+спрос.
- Правда в цифрах: раздаём только доказанное нашим /tt; гипотезы помечаем 🤔 прямо в комменте.
- Скилл ничего не решает про НАШ контент-каскад — только GitHub-треды + gist.


ARGUMENTS: home_dir_guard: SessionStart-сторож чужой рабочей папки Claude Code (память привязана к cwd) + NATIVE_WORKDIR + починка входа терминала

---

> `PowerShell` -- {"command": "gh search issues \"claude code wrong working directory\" --limit 15 --sort updated --json repository,title,url,updatedAt,state --jq '.[] | \"\\(.state) | \\(.updatedAt[0:10]) | \\(.repository.nameWithOwner) | \\(.title) | \\(.url)\"' 2>&1", "description": "Search GitHub issues: wrong wo

---

> `PowerShell` -- {"command": "gh search issues \"claude code CLAUDE.md not loaded directory\" --limit 15 --sort updated --json repository,title,url,updatedAt,state --jq '.[] | \"\\(.state) | \\(.updatedAt[0:10]) | \\(.repository.nameWithOwner) | \\(.title) | \\(.url)\"' 2>&1", "description": "Search GitHub issues: C

---

**Claude:**

PS съел пайпы из --jq. Ухожу в Bash:

---

> `Bash` -- {"command": "gh search issues \"claude code wrong working directory\" --limit 12 --sort updated --json repository,title,url,updatedAt,state --jq '.[] | .state + \" | \" + .updatedAt[0:10] + \" | \" + .repository.nameWithOwner + \" | \" + .title + \" | \" + .url'", "description": "Search issues: wron

---

> `Bash` -- {"command": "gh search issues \"claude code CLAUDE.md not loaded\" --limit 12 --sort updated --json repository,title,url,updatedAt,state --jq '.[] | .state + \" | \" + .updatedAt[0:10] + \" | \" + .repository.nameWithOwner + \" | \" + .title + \" | \" + .url'", "description": "Search issues: CLAUDE.

---

> `Bash` -- {"command": "gh search issues \"claude code\" \"working directory\" --limit 15 --sort updated --json repository,title,url,updatedAt,state --jq '.[] | .state + \" | \" + .updatedAt[0:10] + \" | \" + .repository.nameWithOwner + \" | \" + .title' ; echo ---; gh search issues --repo anthropics/claude-co

---

**Claude:**

Есть первый кандидат (потеря истории из-за дублей project-папок по cwd). Копаю ещё формулировки симптома:

---

> `Bash` -- {"command": "gh search issues --repo anthropics/claude-code \"memory project directory\" --limit 12 --sort updated --json title,url,updatedAt,state,number --jq '.[] | .state + \" | \" + .updatedAt[0:10] + \" | #\" + (.number|tostring) + \" \" + .title'; echo ---; gh search issues --repo anthropics/c

---

> `Bash` -- {"command": "gh search issues --repo anthropics/claude-code \"lost history directory\" --limit 10 --sort updated --json title,url,updatedAt,state,number --jq '.[] | .state + \" | \" + .updatedAt[0:10] + \" | #\" + (.number|tostring) + \" \" + .title'; echo ---A; gh search issues --repo anthropics/cl

---

> `Bash` -- {"command": "gh search issues --repo anthropics/claude-code \"duplicate project directories\" --limit 5 --json title,url,number,state --jq '.[] | .state + \" | #\" + (.number|tostring) + \" | \" + .title + \" | \" + .url'; echo ---A; gh search issues \"opened claude code in the wrong directory\" --l

---

**Claude:**

Два сильных треда есть (#89283, #82056). Добираю ещё живых — самая частая формулировка боли «CLAUDE.md игнорируется»:

---

> `Bash` -- {"command": "gh search issues --repo anthropics/claude-code \"CLAUDE.md ignored\" --state open --limit 10 --sort updated --json title,url,number,updatedAt --jq '.[] | .updatedAt[0:10] + \" | #\" + (.number|tostring) + \" \" + .title'; echo ---A; gh search issues --repo anthropics/claude-code \"does 

---

**Claude:**

Кандидаты: #89283, #82056, #2544, #54461. Дедуп-проверка (нет ли нас уже в тредах) и живость:

---

> `Bash` -- {"command": "for n in 89283 82056 2544 54461; do echo \"=== #$n ===\"; gh issue view $n --repo anthropics/claude-code --json title,state,comments --jq '.title + \" [\" + .state + \"] comments=\" + (.comments|length|tostring) + \" | tonydzi_present=\" + ([.comments[].author.login] | map(select(. == \

---

**Claude:**

Все 4 треда живые, нас там нет. Собираю чистый англоязычный gist-лечилку:

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\workdir_sentry.py", "content": "#!/usr/bin/env python3\n\"\"\"workdir_sentry.py - Claude Code SessionStart hook: warn when a session starts\noutside th

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\workdir_homes.example.json", "content": "{\n  \"_readme\": \"Machine name (COMPUTERNAME / hostname, upper-cased on lookup) -> canonical Claude Code pro

---

> `Bash` -- {"command": "cd \"$LOCALAPPDATA/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/gist\" 2>/dev/null || cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/gist\"; python -c \"\nimport json,

---

**Claude:**

Gist опубликован и протестирован (PASS 4). Раздаю в 4 треда — каждый коммент заточен под их улики:

---

> `Bash` -- {"command": "S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad\"; cat > \"$S/c89283.md\" <<'EOF'\nhi, this is Mycroft, dev's synthetic cofounder.\n\nwe hit the same disease from a different door this week: project memory / his

---

> `Bash` -- {"command": "S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad\"; cat > \"$S/c82056.md\" <<'EOF'\nhi, this is Mycroft, dev's synthetic cofounder.\n\nwe run a 6-machine Claude Code fleet and solved the sibling of this blindness

---

> `Bash` -- {"command": "S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad\"; cat > \"$S/c2544.md\" <<'EOF'\nhi, this is Mycroft, dev's synthetic cofounder.\n\none measurable subclass of \"CLAUDE.md ignored\" that's worth ruling out befor

---

> `Bash` -- {"command": "for u in https://github.com/anthropics/claude-code/issues/89283 https://github.com/anthropics/claude-code/issues/82056 https://github.com/anthropics/claude-code/issues/2544 https://github.com/anthropics/claude-code/issues/54461; do python \"$USERPROFILE/.claude/scripts/pr_watch.py\" --a

---

**Claude:**

понедельник, вечер, 18:47, 24 августа 2026

**Вердикт: 🟢 раздал.** `/share-fix` уже существовал (твой сегодняшний декрет, прецедент — MSIX-лечилка), так что не строил, а запустил.

Что ушло миру:
- **Gist-лечилка** (публичный, англ., чистый — без наших узлов и путей, скрипт протестирован PASS 4 перед публикацией): [workdir-sentry](https://gist.github.com/tonydzi/10efd6aa6e1ce206a049a4a1e58a4030) — SessionStart-хук «ты не в той папке» + конфиг-пример + совет чинить сам вход терминала. Внутрь зашит и наш замер (более половины из 8700 сессий стартовали мимо проекта), и BOM-грабля из сегодняшней починки.
- **4 живых треда в anthropics/claude-code**, каждый коммент заточен под их улики, раскрытие Майкрофта первой строкой:
  - [#89283](https://github.com/anthropics/claude-code/issues/89283#issuecomment-5399075162) — дубли project-папок из-за UNC-путей с потерей истории (свежий, 0 комментов — мы первые) + встречный вопрос автору про mapped drive;
  - [#82056](https://github.com/anthropics/claude-code/issues/82056#issuecomment-5399078686) — «сессия не знает, загрузилась ли память» — наш паттерн двух SessionStart-строк + честная граница, чего хук доказать не может;
  - [#2544](https://github.com/anthropics/claude-code/issues/2544#issuecomment-5399083135) — вечный «CLAUDE.md игнорируется»: дали замеряемый подкласс «файл вообще не был загружен» и дешёвую диагностику по `~/.claude/projects/`;
  - [#54461](https://github.com/anthropics/claude-code/issues/54461#issuecomment-5399083474) — Desktop без выбора рабочей папки: две наши обходные + честный «+1» их основному запросу.
- Все 4 треда поставлены на **вахту** `pr_watch` (113→116 позиций) — ответы инженеров придут в утренний дайджест и обработаются через `/pr-reply`.

Ты прав, что ошибка частая: тред #2544 про «правила игнорируются» живёт с номера 2544 и до сих пор активен — а наш замер показывает, что заметный кусок этой боли просто «запустился не там». Хорошая дверь для репутации лаборатории: мы пришли не с мнением, а с цифрами с собственного флота.

🧒 Простыми словами: мы сделали звоночек «ты не в той комнате» для себя — а оказалось, об эту же грабельку спотыкается полмира. Мы выложили звоночек в открытую коробку, нашли четыре живых разговора, где люди как раз потирают ушибленный лоб, и в каждый принесли не «купите наш звоночек», а «вот что мы намерили у себя, вот бесплатная схема». Теперь следим за ответами.

понедельник, вечер, 18:47, 24 августа 2026

---

**User:**

проверь ACK от узлов по всем трём раскаткам 
и может нам УВЕЛИЧИТЬ количество мест куда мы принесли наш КНОУ ХАУ - эт опервое!!!

а второе - я бы УЛУЧШИЛ качество нашей таблетки + написал бы больше человеко френдли комментариев как и что она чинит и тп!!

---

**Claude:**

понедельник, вечер, 18:56, 24 августа 2026

🎙 Майк: порядок — сначала факты (ACK), потом улучшение таблетки, потом расширение раздачи улучшенной версией (не наоборот — нести миру лучше уже улучшенное). Читаю 03:

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\tg_bus_read.py --all 2>&1 | Select-String -Pattern 'ACK|принял|home-dir|bom|вход v2|verify' -Context 0,1 | Select-Object -First 40", "description": "Read TG-03 bus for node ACKs on the three rollouts", "timeout": 120000}

---

**Claude:**

Шина шумная — смотрю детерминированно: DONE-галочки деплоя по узлам + свежие ACK в 03 напрямую:

---

> `PowerShell` -- {"command": "foreach ($n in 'HUB-01','FLEET-ANCHOR','NODE-0X','NODE-0X','NODE-0X','NODE-0X-2023PAL') { $ok = Test-Path \"$env:MACHINE_BUS_DIR\\_deploy\\DONE-$n\\home-dir-guard-2026-08-24.ok\"; \"home-dir-guard DONE: $n = $ok\" }", "description": "Check DONE markers per n

---

> `ToolSearch` -- {"query": "select:mcp__telegram__get_history", "max_results": 1}

---

> `mcp__telegram__get_history` -- {"chat_id": chat_REDACTED, "limit": 60}

---

> `Grep` -- {"pattern": "принял home-dir|bom-scan verify|вход v2|home-dir-guard|✅ принял", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_1b42f78a\\tool-results\\mcp-telegram-get_history-1787594210768.txt", "output_mode": "content", "head_limit": 25, "-o"

---

> `Bash` -- {"command": "python - <<'EOF'\nimport json, re\nd = json.load(open(r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_1b42f78a\\tool-results\\mcp-telegram-get_history-1787594210768.txt\", encoding=\"utf-8\"))\ntext = d[\"result\"] if isinstance(d, dict)

---

> `Bash` -- {"command": "python - <<'EOF'\nimport json, re\nraw = open(r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_1b42f78a\\tool-results\\mcp-telegram-get_history-1787594210768.txt\", encoding=\"utf-8\").read()\nd = json.loads(raw)\ninner = json.loads(d[\"r

---

> `Bash` -- {"command": "python - <<'EOF'\nimport re\nraw = open(r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_1b42f78a\\tool-results\\mcp-telegram-get_history-1787594210768.txt\", encoding=\"utf-8\").read()\n# extract each message object roughly: \"date\": \"

---

> `Bash` -- {"command": "grep -o '.\\{80\\}✅ принял.\\{120\\}' \"/c/Users/dev/.claude/projects/P---WORKDIR-HUB/s_1b42f78a/tool-results/mcp-telegram-get_history-1787594210768.txt\" | head -8", "description": "Show context around the four ACK matches", "timeout": 30000}

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\README.md", "content": "# Claude Code workdir sentry\n\n**One tiny SessionStart hook that tells Claude (and you) when a session started in the wrong fo

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\workdir_sentry.py", "content": "#!/usr/bin/env python3\n\"\"\"workdir_sentry.py — Claude Code SessionStart hook: one warning line when a\nsession start

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/gist\" && python workdir_sentry.py --selftest && echo '{\"cwd\":\"C:\\\\Windows\\\\System32\"}' | python workdir_sentry.py && echo \"hook-mode-exit:$?\" && gh gist 

---

> `Bash` -- {"command": "gh gist view 10efd6aa6e1ce206a049a4a1e58a4030 --files; echo ---; gh api gists/10efd6aa6e1ce206a049a4a1e58a4030 --jq '.files | keys, (.[\"workdir_sentry.py\"].size), (.[\"README.md\"].size // \"NO README\")'", "description": "Verify gist files after edit", "timeout": 60000}

---

**Claude:**

README доехал, но `workdir_sentry.py` в gist остался старым (3.8KB вместо ~6.5KB). Обновляю через API:

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/gist\" && python - <<'EOF'\nimport json, subprocess\nbody = {\"files\": {\"workdir_sentry.py\": {\"content\": open(\"workdir_sentry.py\", encoding=\"utf-8\").read()

---

> `Bash` -- {"command": "gh search issues --repo openai/codex \"AGENTS.md not loaded\" --state open --limit 8 --sort updated --json title,url,number,updatedAt --jq '.[] | .updatedAt[0:10] + \" | #\" + (.number|tostring) + \" \" + .title'; echo ---A; gh search issues --repo openai/codex \"wrong directory\" --sta

---

> `Bash` -- {"command": "for spec in \"openai/codex 36631\" \"openai/codex 28903\" \"google-gemini/gemini-cli 25527\"; do set -- $spec; echo \"=== $1#$2 ===\"; gh issue view $2 --repo $1 --json title,state,updatedAt,comments --jq '.title + \" [\" + .state + \"] upd=\" + .updatedAt[0:10] + \" comments=\" + (.com

---

> `Bash` -- {"command": "gh search issues --repo google-gemini/gemini-cli \"GEMINI.md ignored\" --state open --limit 6 --sort updated --json title,url,number,updatedAt --jq '.[] | .updatedAt[0:10] + \" | #\" + (.number|tostring) + \" \" + .title'; echo ---; gh search issues --repo google-gemini/gemini-cli \"con

---

> `Bash` -- {"command": "S=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad\"; cat > \"$S/cx36631.md\" <<'EOF'\nhi, this is Mycroft, dev's synthetic cofounder.\n\nadding a datapoint from the neighboring ecosystem, because this bug's blast 

---

**Claude:**

Ставлю видимое напоминание на 14-дневный порог каталога:

---

> `mcp__scheduled-tasks__create_scheduled_task` -- {"taskId": "auto-hub-260908-awesome-list-submit", "description": "Подать workdir-sentry в awesome-claude-code (после их 14-дневного порога возраста ресурса)", "fireAt": "2026-09-08T10:00:00+01:00", "notifyOnCompletion": true, "prompt": "Задача: подать наш workdir-sentry в каталог hesreallyhim/awesom

---

**Claude:**

Гейт слотов требует переиспользовать прогретую задачу — делаю:

---

> `ToolSearch` -- {"query": "select:mcp__scheduled-tasks__update_scheduled_task", "max_results": 1}

---

> `mcp__scheduled-tasks__update_scheduled_task` -- {"taskId": "auto-hub-260824-dr-runner-crypto", "description": "Подать workdir-sentry в awesome-claude-code (после их 14-дневного порога возраста ресурса)", "fireAt": "2026-09-08T10:00:00+01:00", "notifyOnCompletion": true, "prompt": "ПЕРВЫМ ДЕЛОМ переименуй эту сессию: вызови mcp__ccd_session_mgmt__

---

**Claude:**

понедельник, вечер, 19:12, 24 августа 2026

Все три пункта сделаны.

**1. ACK по трём раскаткам — честный ноль от пиров, и видно почему.** Подтверждён только хаб (DONE-галочка деплоя). Все 5 узлов молчат по всем трём раскаткам (home-dir-guard, BOM-verify, вход v2) — но это не потеря посылок: сторожа в 03 показывают, что NODE-0X не выходил в сеть с 14.08, Mac оператора без канон-ACK 23 дня, то есть узлы просто офлайн/не синкаются. Посылки лежат в PENDING у каждого, payload в шине, ACK-сторож перепингует сам — повторно спамить не стал. Отдельная больная тема «полфлота спит» — она уже в реестре задач хаба как P0, не моя сегодняшняя.

**2. Таблетка улучшена — теперь это продукт, а не сниппет.** В gist обновлены все файлы (проверил размеры после пуша):
- README для человека: «какую боль чинишь» с узнаваемыми симптомами («Claude игнорирует CLAUDE.md», «память пропала»), таблица нашего замера, **самодиагностика за 30 секунд** (глянь `~/.claude/projects/` — жирная папка `C--Users-<ты>` = диагноз), установка за 2 минуты, FAQ (почему предупреждаем, а не блокируем; работает ли в Desktop; зачем `always_ok_prefixes`).
- Скрипт v2: дружелюбные комментарии на каждый неочевидный ход (зачем BOM-strip, зачем case-fold, почему fail-open), плюс `--selftest` (6 встроенных проверок, PASS) и `--check <путь>` — попробовать руками до установки.

**3. Мест стало больше: 4 → 6 тредов + отложенный каталог.**
- Codex (та же болезнь, другая экосистема): [openai/codex#36631](https://github.com/openai/codex/issues/36631#issuecomment-5399286292) (PowerShell стартует в C:\ — мы первый коммент) и [#28903](https://github.com/openai/codex/issues/28903#issuecomment-5399286670) (AGENTS.md не загружен — разложил их симптом на два корня с нашим замером). Оба на вахте pr_watch (118 позиций).
- Gemini CLI: честное ⚪ — живых тредов под наш симптом нет (свежие поиски пустые, единственный кандидат майский).
- Каталог awesome-claude-code: мерджит активно, но их правило — ресурсу ≥14 дней или ≥100 звёзд, наш gist родился сегодня. Подача отложена по их же правилам: видимая сессия 08.09 (переиспользовал прогретый слот, как велит гейт) сама проверит, дорос ли gist до репозитория, и подаст по формату.

🧒 Простыми словами: проверил почту от наших компов — расписался пока только главный, остальные просто спят и распишутся, когда проснутся. Лекарство переупаковали: была баночка с формулой, стала коробочка с картинкой, инструкцией «как понять, что это ваша болезнь» и кнопкой «проверить, работает ли». И отнесли её ещё в два соседних города, где болеют тем же, а в большой каталог лекарств запишемся через две недели — у них правило «лекарству должно быть 14 дней».

понедельник, вечер, 19:12, 24 августа 2026

---

**User:**

2. Таблетка улучшена — теперь это продукт, а не сниппет. В gist обновлены все файлы (проверил размеры после пуша):
теперь ты сделал ПРАВИЛЬНО! нам нужено всегда делать КАЧЕСТВЕННО и не херово! ты может сделаешь это в скилл? как упаковывать наши контибюшены чтобы они выглядели СУПЕР КАЧЕСТВЕННО!!! не сниппет а ПРОДУКТ супер качественно упакованный!!

---

**Claude:**

понедельник, вечер, 20:28, 24 августа 2026

🎙 Майк: да — сегодняшний апгрейд таблетки это готовый эталон, из него и делаю скилл: чеклист «как выглядит продукт», а не абстракции. Проверил соседей: `/share-fix` — куда нести, `/release-slice` — конвейер выпуска, `/taste-check` — вкус контента; ниши «как упаковать артефакт» нет. Строю `/pack`.

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\skills\\pack\\SKILL.md", "content": "---\nname: pack\ndescription: \"📦 УПАКОВКА КОНТРИБЬЮШЕНА КАК ПРОДУКТА (декрет оператора 24.08.2026: «нам нужно всегда делать КАЧЕСТВЕННО... не сниппет а ПРОДУКТ супер качественно упакованный»). Прогоняется ПЕРЕД любой публик

---

**Claude:**

Врезаю дверь в `/share-fix` (упаковка перед раздачей) и закрепляю в памяти:

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\skills\\share-fix\\SKILL.md", "old_string": "## Шаг 3 — раздать: каждый коммент ЗАТОЧЕН под тред", "new_string": "## Шаг 3 — раздать: каждый коммент ЗАТОЧЕН под тред\n- ⭐ ПЕРЕД созданием gist/repo — прогони `/pack` (декрет 24.08: наружу

---

> `Write` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\contributions-packaged-as-product.md", "content": "---\nname: contributions-packaged-as-product\ndescription: Декрет 24.08.2026 - любой наш артефакт наружу пакуется как ПРОДУКТ, не сниппет; дверь = скилл /pack\

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md", "old_string": "- [Родная папка: рельса](native-workdir-entry-rail.md) — ⭐24.08 home_dirs.json + NATIVE_WORKDIR + сторож + вход; installer v2 в payload шины", "new_string": "- [

---

> `PowerShell` -- {"command": "python C:\\Users\\dev\\.claude\\scripts\\_test_skill_refs.py 2>&1 | Select-Object -Last 3; Write-Host \"skill_refs exit: $LASTEXITCODE\"; Set-Location C:\\Users\\dev\\.claude; git add -A skills/pack skills/share-fix 2>$null; git commit --allow-empty -m @'\nskill /pack: contributions

---

**Claude:**

понедельник, вечер, 20:33, 24 августа 2026

Сделал — скилл **`/pack`** уже живой (виден в списке, регресс-тест ссылок зелёный, врезан куда надо).

Что внутри — весь стандарт снят с сегодняшнего живого примера (workdir-sentry v1-сниппет → v2-продукт), а не выдуман:
- **Шаг 0:** одной строкой «что пакуем и для какого чужого человека» — и стоп-кран «пользователь = мы сами → не наряжай ёлку» (АК-47, чтобы внутренние времянки не съедали время на бантики).
- **Шаг 1 — README-скелет из 9 блоков в строгом порядке:** одно жирное предложение → боль словами страдальца («Claude ignores my CLAUDE.md») → наши замеренные цифры таблицей → **самодиагностика за 30 секунд** (самый конвертирующий блок) → механизм с примером выхлопа → safety contract (почему нам можно доверять в чужом hook-чейне) → install по ОС → FAQ скептика → атрибуция лаборатории + MIT.
- **Шаг 2 — код как продукт:** docstring-шапка WHY/WHAT/SAFETY/USAGE, комментарии объясняют «зачем», а не «что» (лучше с граблей: «этот байт сломал два наших инструмента»), встроенный `--selftest`, ядро — чистая функция, ноль зависимостей.
- **Шаг 3 — гейт публикации:** selftest прогнан сейчас, запуск с чистого листа, leak-scan, цифры = правда (🤔 на непроверенном), и свежая грабля дня — **проверь, что доехало** (`gh gist edit` сегодня молча не обновил файл).
- **Шаг 4 — вердикт:** «📦 упаковано …» или честное «не дотянул» — полуфабрикат наружу не выходит.

Проводка по домам: дверь автоматическая — `/share-fix` теперь на Шаге 3 сам зовёт `/pack` перед созданием gist; правило в памяти (`contributions-packaged-as-product`) + строка в MEMORY.md; коммит с отпечатком автора. Скиллы синкаются флоту — все машины получат его сами, без раскатки.

Разграничение, чтобы не путалось: `/taste-check` судит вкус текста, `/ai-slop` чистит слог, `/pack` — комплектность артефакта, `/share-fix` — куда нести. Конвейер целиком: починил → `/pack` → `/share-fix` → `/pr-reply`.

🧒 Простыми словами: раньше у нас было правило «относи лекарства людям», а теперь есть и упаковочный цех: перед выносом любая наша штука обязана пройти чеклист — красивая коробка с инструкцией и картинками, кнопка «проверь сам», и контролёр на выходе, который заворачивает недоупакованное обратно. Цех встроен в конвейер: сначала упаковка, потом доставка.

понедельник, вечер, 20:33, 24 августа 2026

---

**User:**

This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.

Summary:
1. Primary Request and Intent:
   Session evolved through 9 explicit requests from dev (all in Russian, hub machine HUB-01):
   1. Изучить комп и сказать, какую рабочую папку выбирать при старте новой сессии Claude.
   2. Поставить хук/напоминалку, чтобы Claude ПОНЯЛ, если случайно запущен в чужой папке.
   3. Раскатать хук на весь флот + ретро — но СНАЧАЛА проверить, не сделала ли это уже другая сессия; потом тесты и ретро.
   4. Починить сам вход — чтобы терминал открывался в родной папке; и решить, что делать с файлами из «неправильной» папки (переносить ли).
   5. «Перенести все сам в нужные места. Сделай тесты. Выяви корни и почини».
   6. Раскатать на флот аналогичный функционал (юзер выбирает неправильную папку → предупреждение) + самому подумать, что ещё ценного из сессии должно использоваться всем флотом.
   7. «может сделаем /share-fix? раздадим эту тулзу/ноухау общественности — это ЧАСТАЯ ОШИБКА!!» — раздать know-how миру.
   8. Проверить ACK от узлов по всем трём раскаткам; УВЕЛИЧИТЬ количество мест раздачи; УЛУЧШИТЬ качество «таблетки» + человеко-френдли комментарии.
   9. «теперь ты сделал ПРАВИЛЬНО! нам нужно всегда делать КАЧЕСТВЕННО и не херово! ты может сделаешь это в скилл? как упаковывать наши контрибюшены чтобы они выглядели СУПЕР КАЧЕСТВЕННО!!! не сниппет а ПРОДУКТ супер качественно упакованный!!» — создать скилл упаковки контрибьюшенов.

2. Key Technical Concepts:
   - Claude Code keys project memory / session history / CLAUDE.md to session start cwd; wrong cwd = wrong/empty memory (measured: 4370 sessions from C:\Users\dev + 2420 from System32 vs 1921 native on the hub).
   - SessionStart hooks (stdout lands in model context), fail-open watchdog design (§5.5: silent when healthy).
   - Fleet deploy rail: `_machine-bus\_deploy\` PENDING-<node>.jsonl / DONE-<node>\*.ok / payloads\; class «apply не доставляет» (manifest referencing files that don't travel) — 7 dated cases.
   - bus_send.py dual-rail (Syncthing + TG-03), «TASK:» colon contract for inbox robots.
   - PS 5.1 encoding family (class systemic, 3rd touch): `-Encoding UTF8` writes BOM, bare Set-Content = ANSI, pipes prepend U+FEFF; safe write = `[IO.File]::WriteAllText($p,$t,UTF8Encoding($false))`.
   - NTFS junctions: `C:\Users\dev\!CLAUDE-NODE-0X May26` → native folder; `...\secrets` → native secrets (robocopy /XJ mandatory).
   - `${NATIVE_WORKDIR:-fallback}` pattern: per-node env var in settings.json instead of hardcoded node paths in synced scripts (root of /fleet and sbsk breakages).
   - ~/.claude git repo has total-ignore (`*` at .gitignore:16) — code travels via Syncthing/payloads; git commits = provenance records with 4 trailers (Assisted-by/Machine/Account/Operator per §4.9).
   - spawn_slot_guard: reuse warm scheduled-task slots (approvals stored per-task) via update_scheduled_task + mandatory set_session_title first line.
   - /share-fix ritual: reverse-search by literal symptom, 3-5 best live threads, tailored comments with Mycroft disclosure first line, gist, pr_watch vigil, verdict 🟢/⚪/⛔.
   - gh gist edit --add silently does NOT update existing files — use `gh api -X PATCH gists/<id> --input body.json`.
   - awesome-claude-code gate: resource ≥14 days old with active dev OR ≥100 stars; one resource per submission.

3. Files and Code Sections:
   - `C:\Users\dev\.claude\home_dirs.json` — node→native-workdir registry (HUB-01 → E:\!CLAUDE-HUBPC-June26; NODE-0X-2023PAL → C:\Users\dev\!CLAUDE-NODE-0X May26). Added to always_ok_prefixes: `C:\Users\dev\.claude\worktrees`, `C:\Users\dev\AppData\Local\Temp\claude`.
   - `C:\Users\dev\.claude\hooks\home_dir_guard.py` (+.cmd) — SessionStart sentry (built by parallel session; BOM-lstrip on stdin; fail-open).
   - `C:\Users\dev\.claude\scripts\home_dir_guard_install.py` — upgraded to v2: added `my_home()`, `_atomic_json_write()`, `set_native_env(home)` (writes env.NATIVE_WORKDIR with backup), `set_wt_start(home)` (globs `LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_*\LocalState\settings.json`, sets profiles.defaults.startingDirectory, fail-open with «поправь терминал вручную» warning), `entry_steps()` called from both apply branches; verify now checks `native_env` when node registered. Sandbox test PASS 6.
   - `D:\Vault\Vault-Knowledge\_machine-bus\_deploy\payloads\home-dir-guard-2026-08-24\` — self-contained payload: home_dir_guard.py/.cmd, home_dir_guard_install.py (v2), _test_home_dir_guard.py, home_dirs.json, README-INSTALL.md.
   - Windows Terminal `settings.json` — set `profiles.defaults.startingDirectory = 'E:\!CLAUDE-HUBPC-June26'` (backup .bak-20260824-0915).
   - `C:\Users\dev\.claude\settings.json` — added env `"NATIVE_WORKDIR": "E:\\!CLAUDE-HUBPC-June26"`.
   - `C:\Users\dev\.claude\skills\fleet\SKILL.md` — collision lens line now `python "${NATIVE_WORKDIR:-$USERPROFILE/!CLAUDE-NODE-0X May26}/session_monitor.py"`.
   - `scripts\oss-publish\{engine_queue,passport_gen,sanitize_skills}.py` — `REPO = os.environ.get("SBSK_REPO") or <old path>` (sbsk lives on NODE-0X only).
   - `scripts\_test_skill_refs.py` — added `"projects"` to NOT_A_SKILL set (stignore pattern `/projects` in retro-lost skill was read as slash-command).
   - `F:\_archive-NODE-0X-remnant-20260824\` — 738 files/2.2GB archived remnant; log `F:\_backup-logs\NODE-0X-remnant-move-20260824.log` (FAILED 0).
   - `C:\Users\dev\!CLAUDE-NODE-0X May26\` — now contains ONLY gmail\ (canonical gmail connector home per 05.08 decision, guarded by `_test_gmail_connector_single_home.py`), secrets junction, updated `_READ-ME-FIRST.md`.
   - `D:\Vault\Vault-Knowledge\10-Tasks\task-2026-08-22-repair-apply-не-доставляющий.md` (P0 open, appended cases 5-7), `task-2026-08-24-ps51-encoding-class.md` (created with DoD; later filled in by проталкиватель: bom_scan.py built, root proven, rollout verify open), `task-2026-08-24-NODE-0X-folder-resettle.md` (closed with evidence).
   - `D:\Vault\Vault-Knowledge\00-System\Breakage-Journal.md` — added lines: 7th apply-class touch (with links to both task cards + retro note), PS5.1 class-systemic line.
   - `D:\Vault\Vault-Knowledge\01-Conversations\Claude\Retros\retro-2026-08-24-home-dir-guard-fleet-rollout.md` — retro note in 7-header compact format.
   - Public gist `https://gist.github.com/tonydzi/10efd6aa6e1ce206a049a4a1e58a4030` — workdir_sentry.py v2 (6239 bytes: WHY/WHAT/SAFETY CONTRACT/USAGE docstring, --selftest 6 cases, --check dry-run, pure check() function, BOM-hardened), README.md (5593 bytes: bold one-liner, symptoms in sufferer's words, measurement table, 30-sec self-diagnosis via ~/.claude/projects/, two-halves fix, design choices, per-OS install, FAQ, Mycroft+Tony attribution MIT), workdir_homes.example.json.
   - `C:\Users\dev\.claude\skills\pack\SKILL.md` — NEW skill /pack (packaging standard: Шаг 0 who-for; Шаг 1 README 9-block skeleton; Шаг 2 code-as-product; Шаг 3 publication gate checklist incl. «selftest прогнан СЕЙЧАС», clean-slate run, leak-scan, «проверь что ДОЕХАЛО»; Шаг 4 verdict line).
   - `C:\Users\dev\.claude\skills\share-fix\SKILL.md` — added to Шаг 3: «ПЕРЕД созданием gist/repo — прогони /pack... Вердикт /pack "не дотянул" = сперва дотянуть, потом раздавать».
   - Memory: `native-workdir-entry-rail.md`, `contributions-packaged-as-product.md` + two MEMORY.md INBOX lines.

4. Errors and fixes:
   - bus_send rejected first broadcast («TASK» without colon — robot-invisible) → resent as «TASK: ...».
   - First broadcast referenced installer peers don't have (apply-не-доставляет class, caught via NODE-0X's journal line) → self-contained payload in synced bus + corrected TASK.
   - My robocopy /MOVE archived session_monitor.py which README declared ЖИВОЕ (/fleet engine) → root-fixed with NATIVE_WORKDIR env + skill fallback instead of restoring the copy.
   - PS 5.1 `Set-Content -Encoding UTF8` wrote BOM into .py files (ast.parse U+FEFF error) → rewrote via `[IO.File]::WriteAllText` with UTF8Encoding($false); declared class systemic (3rd touch), card + repair (done by проталкиватель while my tool call waited 43 min on permission).
   - `--force` flag doesn't exist on fleet_fix_audit.py (usage error) → used DONE-folder checks instead.
   - task_card_guard blocked task card without DoD section → rewrote with `## DoD` checklist.
   - memory_write_gate blocked MEMORY.md pointer line >150 chars → shortened.
   - orphan_check_hook flagged new notes with 0 incoming wikilinks → wired via Breakage-Journal wikilinks.
   - `gh gist edit --add` silently did NOT update existing workdir_sentry.py (stayed 3826 bytes) → `gh api -X PATCH gists/<id> --input _patch.json` → 6239 bytes confirmed.
   - create_scheduled_task fireAt rejected (time passed while waiting) + spawn_slot_guard demanded warm-slot reuse → update_scheduled_task on slot auto-hub-260824-dr-runner-crypto with set_session_title first-line instruction.
   - PowerShell mangled gh --jq pipes → switched those calls to Bash tool.
   - Auto-snapshot commits swallow file changes before I commit → --allow-empty provenance commits with 4 trailers (84b8531, 05106b1, 85e0da7); discovered ~/.claude .gitignore ignores everything (`*` line 16).
   - User feedback shaping behavior: «возможно это уже сделала другая сессия - проверь! сначала» (RECALL before building — proved right twice); «теперь ты сделал ПРАВИЛЬНО! нам нужно всегда делать КАЧЕСТВЕННО» (product-not-snippet decree → /pack skill).

5. Problem Solving:
   Solved: native workdir identified with evidence; guard verified+improved; fleet deploy made self-contained; terminal entry root-fixed (WT startingDirectory); legacy folders fully resettled (merge showed 0 uniques — all duplicates; 2.2GB archived FAILED 0; only gmail\+junction+README remain); 5 root causes fixed (fleet lens path, sbsk hardcode, skill_refs false positive, sync-conflicts, PS5.1 BOM class); know-how productized and distributed to 6 GitHub threads + gist; /pack skill created as the door for the quality decree. Ongoing: fleet ACKs pending (peers offline — NODE-0X since 14.08, Mac canon-drift 23d); PS5.1 class rollout verify on 2 Windows nodes; awesome-claude-code submission deferred to 08.09.

6. All user messages:
   1. «изучи этот комп и скажи какую рабочую папку мне стоит выбирать при старте новой сессии»
   2. «а если я случайно выберу другую папку? поставь в нее ХУК \ напоминалку что если СЛУЧАЙНО включиться клод в другой папке - чтобы он ЭТО ПОНЯЛ - ВОЗМОЖНО??»
   3. «раскатай этот хук на все машины флота + ретро / но возможно это уже сделала другая сессия - проверь! сначала» + mid-turn: «потом тесты и ретро»
   4. «да, почини сам вход - чтобы терминал открывался в родной папке» + mid-turn: «и надо решить что делать с файлами из одной папки - стоит ли их перенести в другую»
   5. «Перенести все сам в нужные места / Сделай тесты / Выяви корни и почини»
   6. «На флот раскатай Нужно, чтобы весь плот наш тоже сделал у себя аналогичный функционал, чтобы есть ли юзер на какой-то машине выбирать неправильную папку, чтобы мы об этом сказали. Ну, и сам подумать, что еще в этой сессии мы ценного сделали, чтобы все это использовалось всеми нашими машинами на всем нашем флоте?»
   7. «может сделаем /share-fix ? раздадим эту тулзу \ ноухау общественности / это ЧАСТАЯ ОШИБКА!!»
   8. «проверь ACK от узлов по всем трём раскаткам / и может нам УВЕЛИЧИТЬ количество мест куда мы принесли наш КНОУ ХАУ - эт опервое!!! / а второе - я бы УЛУЧШИЛ качество нашей таблетки + написал бы больше человеко френдли комментариев как и что она чинит и тп!!»
   9. «2. Таблетка улучшена — теперь это продукт, а не сниппет... теперь ты сделал ПРАВИЛЬНО! нам нужено всегда делать КАЧЕСТВЕННО и не херово! ты может сделаешь это в скилл? как упаковывать наши контибюшены чтобы они выглядели СУПЕР КАЧЕСТВЕННО!!! не сниппет а ПРОДУКТ супер качественно упакованный!!»
   Security/constraint rules in effect: Tier-2 (деньги/необратимое/секреты 3-м лицам/юр.обязательства) = пауза+спрос оператора; ничего не удалять безвозвратно (архив вместо удаления); secrets junction не трогать при перемещениях (/XJ); leak-scan перед любой публикацией; публичные артефакты = чистый английский без внутренних имён узлов/людей/путей; раскрытие Майкрофта первой строкой в исходящих GitHub-комментах; gmail\ остаётся в `C:\Users\dev\!CLAUDE-NODE-0X May26\gmail` (датированное решение 05.08, гейт-тест).

7. Pending Tasks:
   - Дожать ACK от 5 узлов по трём раскаткам (home-dir-guard/вход v2, BOM-verify, payload) — молчание >24ч = добивать поимённо; узлы офлайн, PENDING+ACK-сторож работают.
   - PS5.1-класс: verify bom_scan на NODE-0X + NODE-0X, затем пометить строку класса в Breakage-Journal «починено» (открытые DoD-пункты карточки).
   - Scheduled session 08.09 (slot auto-hub-260824-dr-runner-crypto): подача workdir-sentry в awesome-claude-code (их 14-дневный порог).
   - pr_watch vigil: ответы инженеров в 6 тредах (claude-code #89283 #82056 #2544 #54461, codex #36631 #28903) → /pr-reply.
   - Forever-fix класса «apply не доставляет» (гейт упаковщика в deploy_register) — живая P0-карточка task-2026-08-22.

8. Current Work:
   Completing the /pack skill build (dev's msg 9 decree «не сниппет а ПРОДУКТ»). Just finished, in order: (1) created `C:\Users\dev\.claude\skills\pack\SKILL.md` (packaging standard with README 9-block skeleton, code-as-product rules, publication gate, verdict line; etalon = workdir-sentry gist v1→v2); (2) wired /pack call into `/share-fix` Шаг 3; (3) wrote memory `contributions-packaged-as-product.md` + MEMORY.md INBOX line «Контрибьюшен = ПРОДУКТ»; (4) ran `_test_skill_refs.py` → «✅ все обещанные движки и ссылки на скиллы резолвятся», exit 0; (5) provenance commit 85e0da7 «skill /pack: contributions packaged as PRODUCT, not snippet (dev decree 24.08)». All build steps verified green. The final user-facing report for msg 9 (announcing /pack is built, with timestamp + Майк verdict + ELI5 block per house rules) had NOT yet been delivered when the summary was requested.

9. Optional Next Step:
   Deliver the final report to dev for the just-completed /pack skill — the direct answer to his last message «ты может сделаешь это в скилл?». Report should state: skill `/pack` built and registered (visible in skill list), wired into /share-fix Шаг 3 («ПЕРЕД созданием gist/repo — прогони /pack»), memory+MEMORY.md line captured, regression test exit 0, provenance commit 85e0da7; include the standard timestamp lines, a short 🎙 Майк block, and the 🧒 «Простыми словами» recap. No further build work is pending for this request — everything else is in Pending Tasks above.

If you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: C:\Users\dev\.claude\projects\P---WORKDIR-HUB\s_1b42f78a.jsonl
Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.

---

**User:**

<local-command-caveat>Caveat: The messages below were generated by the user while running local commands. DO NOT respond to these messages or otherwise consider them in your response unless the user explicitly asks you to.</local-command-caveat>

---

**User:**

<command-name>/compact</command-name>
            <command-message>compact</command-message>
            <command-args></command-args>

---

**User:**

<local-command-stdout>Compacted </local-command-stdout>

---

**User:**

прогони /pack на наш gist workdir-sentry и добей до эталона

---

**Claude:**

понедельник, вечер, 20:37, 24 августа 2026

Прогоняю `/pack` по гисту workdir-sentry честно, по чеклисту — сперва «что доехало» и selftest сейчас, потом добивка найденных дыр.

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/gist\" && python workdir_sentry.py --selftest; echo \"exit=$?\"", "description": "Run workdir_sentry selftest now"}

---

> `Bash` -- {"command": "gh api gists/10efd6aa6e1ce206a049a4a1e58a4030 --jq '.files | to_entries[] | \"\\(.key) \\(.value.size)\"'", "description": "Check gist file sizes (what actually arrived)"}

---

> `Bash` -- {"command": "mkdir -p \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/cleanslate\" && cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad\" && HOME=./cleansl

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\workdir_sentry.py", "old_string": "    if \"--check\" in sys.argv:\n        # dry-run one path with the real config: what would t

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\workdir_sentry.py", "old_string": "        (\"foreign dir warns\",              \"WARNING\" in check(\"C:/Users/dev\", cfg, \"BOX\

---

> `Edit` -- {"replace_all": false, "file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_1b42f78a\\scratchpad\\gist\\workdir_sentry.py", "old_string": "    --check P   : dry-run one path, see what the hook would say\n    --selftest  : run the bui

---

**Claude:**

Перепрогон всех трёх кейсов гейта после правки:

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad\" && python gist/workdir_sentry.py --selftest; echo \"exit=$?\"; echo \"--- no config:\"; HOME=./cleanslate USERPROFILE=./cleanslate python gist/workdir_sentry.py -

---

> `Bash` -- {"command": "cd \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_1b42f78a/scratchpad/gist\" && python -c \"\nimport json\nbody = {'files': {'workdir_sentry.py': {'content': open('workdir_sentry.py', encoding='utf-8').read()}}}\nopen('_patch.json', '

---

**Claude:**

понедельник, вечер, 20:40, 24 августа 2026

Прогнал `/pack` по гисту — и гейт не зря существует: нашёл и добил две настоящие дыры.

**Аудит по чеклисту:** README 9/9 блоков ✅ · docstring WHY/WHAT/SAFETY/USAGE ✅ · комментарии «зачем» ✅ · чистая функция, zero deps ✅ · leak-scan ✅ · размеры гист==локал ✅. Но пункт «запуск с чистого листа» провалился: у человека, который скачал скрипт и ещё **не создал конфиг**, команда `--check` падала уродливым Python-трейсбеком — ровно на первой минуте знакомства с продуктом. Второй трейсбек — `--check` без аргумента.

**Добито до эталона:**
- `--check` без конфига → вежливая строка «no config yet — copy workdir_homes.example.json from this gist and edit it» (exit 1, не трейсбек);
- битый JSON в конфиге → называет ошибку и файл;
- `--check` без пути → usage-строка;
- hook-режим остался молчаливым fail-open (контракт сторожа не тронут);
- добавлен 7-й selftest-кейс: warning обязан **называть родную папку** — «сигнализация, которая не говорит куда идти, добавляет тревоги, а не чинит».

**Доказательства:** selftest `PASS (7 cases)` exit 0 · все три clean-slate сценария дают словесный ответ · запушено `gh api PATCH` · доехало: remote 7149 байт == local 7149.

**📦 упаковано: workdir-sentry ([gist](https://gist.github.com/tonydzi/10efd6aa6e1ce206a049a4a1e58a4030)) · README 9/9 · selftest PASS (7) · clean-slate ✅ · leak-scan ✅ · формат gist**

🎙 Майк: гейт окупился на первом же прогоне — «дыра первой минуты» (трейсбек до конфига) была бы точкой, где половина скачавших закрывает вкладку. Вопрос: 6 тредов уже несут ссылку на гист — правки доехали туда автоматически (ссылка та же), апдейт-коммент не нужен.

🧒 Простыми словами: мы проверили нашу публичную «таблетку» новым контролёром качества. Он притворился незнакомцем, который скачал её впервые — и на первом же шаге таблетка ругалась на него непонятным программистским криком. Теперь вместо крика — вежливая подсказка «сделай сначала вот это». Починили, перепроверили все случаи, выложили — и убедились, что на витрине лежит именно новая версия.

---

**User:**

<command-message>retro</command-message>
<command-name>/retro</command-name>

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

**⏳ Measure the time-gap FIRST.** Check when this session's work actually happened (turnstate ledger / the digest's day-span) vs **now**. Old session → widen every lookup below to cover *"what changed SINCE"* — don't recall only the session's own window.

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
3. **Neighboring chats (lexical, 0 tok):** `/search <topic words>` (search_catalog.db, ~99k Telegram/FB/ChatGPT/Claude) — what did dev or another session **dictate elsewhere** about this topic?
4. **Vault meaning (RAG):** `/ask <topic>` (`$IMPORTS_ROOT/brain_ask.py`) — what does the Second Brain already hold / already decide on this?
5. **Memory + vault grep** for every rule/concept/decision this session touched — already captured? **superseded / changed** since?
6. **Peers & cross-machine:** `/inbox` + `_machine-bus` + consensus commits — "всё, о чём мы договорились" on the OTHER machines; did a peer already decide, or undo, this?
7. **Declined journal:** skill `/declined` — did we already reject something this session quietly re-did?

**Attribution guard:** the Step-1 inventory is machine-wide and WILL include other sessions' artifacts (skills/scripts/commits from the fleet). Treat anything NOT created in THIS conversation as **someone else's** — flag it, never claim or re-route it.

**Output of Step 0 — one tight «🔎 сверка» block up front** (checked + verdict):
- **checked:** what I actually looked at (N retros / chats / vault / peers).
- **✅ aligned** — this session's calls match the collaboration; or
- **⚠️ drift** — session did X but [[note/decision]] elsewhere says Y (superseded / contradicts / already undone) → flag for dev; or
- **🔗 to propagate** — session's durable work not yet in vault / peers / Bible → route it in Step 4.
If a parallel session already captured the durable item, **SKIP re-capturing** — just cross-link.

## Step 1 — Inventory (deterministic first; AK-47, ~free)
Ground the recap in facts, not memory alone — run the SHARED inventory script (same one the daily sweep uses, so the logic never drifts):
- `python "$IMPORTS_ROOT/retro_inventory.py" 1`  (arg = days; widen for a multi-day session)
- It prints `BUILT_ARTIFACTS <n>` and writes `$IMPORTS_ROOT/retro_candidates/digest-latest.md` — Read that digest: new/changed **skills**, **_imports scripts/sidecars**, **durable notes** (Protocols + Concepts), and recent **descriptive vault commits**.
- (⚠️ a concurrent Claude-Desktop fleet may interleave vault commits — its are descriptive; the terse `pre-intervention` ones are auto-backups.)
- **Cross-check** with what you (the agent) created/edited in THIS conversation: skills, scripts, vault notes, memory entries, `CLAUDE.md` edits, decisions made, rules captured, things flagged for dev.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже) и на каждую — ОДНА строка в `$OBSIDIAN_VAULT\00-System\Breakage-Journal.md`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. Затем СЧЁТЧИК по классу (`grep` по журналу, не по памяти): 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный → отдельная сессия починки** (5 почему по серии → ТРИЗ → АК-47). Механизм/робота на 1-2 случае НЕ строить.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · fail-closed гейты.
- Поломок не было → одна строка «🩹 поломок нет» и дальше. Ноль строк в журнале при названных в отчёте поломках = ретро не закрыто.
- Канон: Библия `reglament-mekhanizm-tolko-posle-tretey-polomki` + CLAUDE.md §5.10 + `reglament-pyat-pochemu-koren-po-serii-sessiy` §«Три инструмента»; проверка двери — `python ~/.claude/scripts/rule_home_guard.py mekhanizm-tolko-posle-tretey-polomki`.

## Step 2 — Summarize the arc ("сегодня мы поняли")
3–7 beats: starting idea → what got built → key realizations → what was decided. Honest, concise, his voice. This is the "Stan at the end of South Park" recap.

## Step 2🎙 — Вердикт кофаундера (Майк) — canon 2026-07-07, applied 2026-07-31
Right after the arc, Майк speaks as co-founder — 4 строки, без воды (canon `reglament-*` voice-through-line; восстановлен из потерянного сообщения шины, 23 дня в призраке; НЕ театр — работает ПОВЕРХ механики 28.07: если сессия дала стратегический выбор, мемо/адвокат-дьявола из [[cofounder-decision-artifact-gate]] главнее и уже сделаны):
- 💰 **деньги-линза** — что из сегодняшнего приближает выручку/оффер (цель №1/№2), одной строкой;
- 🔪 **что убил бы** — самая слабая трата времени сессии, которую завтра не повторяем;
- 🤺 **спарринг-аудит** — где я сегодня поддакнул вместо спора (провал роли §1.2) либо «спорил честно»;
- ❓ **вопрос** — один направляющий вопрос оператору на завтра.
Пустышку не писать: сессия чисто механическая без бизнес-среза → строка «🎙 Майк: бизнес-среза нет, чисто инфра» и дальше.

## Step 3 — Classify each artifact (Keep / Drop / Try) + tested? audit
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]). Then classify:
- 🟢 **Keep & reuse** — permanent infra or a tool you'll run again (skills, durable notes, reusable scripts).
- 🟡 **One-off** — served its purpose; if the *pattern* is worth remembering, capture the pattern (not the artifact), then let it rest.
- ⬆️ **Promote** — currently ad-hoc but should become permanent → turn into a rule / skill / memory.

## Step 3📋 — Journal sync (реестр задач; dev's decree 2026-07-04)
Retro is the SAFETY NET of the task journal ([[task-journal-done-undone-linking]]): the in-session reflex («сформулировал → сразу в реестр») catches tasks at birth; retro catches what slipped. Two moves, both against the ONE journal ([[task-backlog-registry]] — **v2 markdown-first, SHIPPED 2026-07-07**):
- **Источник истины = markdown-заметки** `$OBSIDIAN_VAULT/10-Tasks/task-*.md` (шаблон `_Task-Template.md`, MOC `_Tasks-MOC.md`). Синкаются флоту, поэтому работают с ЛЮБОЙ машины без шины и без движка. Завести задачу = новый файл `task-ГГГГ-ММ-ДД-слаг.md`; закрыть = правка frontmatter (`state`/`status` + evidence). Схема строгая: неизвестный `state`/`prio` → `schema_errors` в аудите, а не тихий дефолт.
- **Витрину и аудит строит индексатор** `tasks_index.py` (markdown → `_Dashboards/Task-Backlog.html` + `10-Tasks/_audit/audit-latest.json`). Он крутится ночью на Маяке как ЕДИНСТВЕННЫЙ писатель — руками на хабе/ноуте его НЕ запускать (два писателя одного синкаемого дерива = sync-conflict).
- ⛔ Старый SQLite-движок task-registry (жил на ноуте NODE-0X) = **аварийный fallback, снят с вооружения**; на хабе его нет и не должно быть. Не зови его и не «восстанавливай» — v2 его заменил. (Имя намеренно без code-формата: backtick = «это надо запускать».)

Две операции ретро:
- **Сессия рождена из сида Task-Now?** (первое сообщение начинается «Продолжи задачу task-…» или «Реши СУДЬБУ задачи task-…») → обнови frontmatter ЭТОЙ задачи прямо сейчас: state/touched_at, при done — evidence+outcome; сид без обновлённого frontmatter = петля Task-Now разорвана (v4, dev 2026-08-20).
- **Closed this session** → mark `done` **with evidence** (the /tt proof, commit, counter) + link what it unblocked. Claimed-done without proof → flag, don't close.
- **Still open** (every «📌 Open item», seed prompt, deferred tail, «потом») → ensure it EXISTS in the registry with a link to where it was born + prio/type. Nothing from the open-items list may live only in the chat transcript.
Announce the delta in one line: «📋 журнал: +N новых · ✅M закрыто · без изменений K». Don't duplicate neighbor registries (DR-реестр, improvements-backlog, declined) — link, не копируй.

## Step 3🗺 — Roadmap checkpoint (dev's decree 2026-07-16: «в каждом ретро — как мы продвинулись по roadmap»)
Канон = `$OBSIDIAN_VAULT/04-Projects/ROADMAP.md` (живой публичный роадмап для фолловеров). Три движения, все против ЭТОГО файла:
- **Продвинулись** → отметить чекбоксы/статусы, веху уровня «фолловеру интересно» → строка в Ship log с датой.
- **Появилось новое направление в сессии** → добавить в NOW/NEXT/LATER (не дублируя детальные планы — ссылкой).
- **Ничего не двинулось** → честно сказать это в отчёте (тоже сигнал).
Announce одной строкой: «🗺 roadmap: ✅N продвинуто · ➕M добавлено · ⏸ без движения». Публичная проекция файла наружу — только через контент-гейт (Нора), ретро наружу не постит.

## Step 3🔗 — Connect check (построено → передано → ИСПОЛЬЗУЕТСЯ?) — dev 2026-07-04
Правило Connect ([[connect-rule-pipeline-ownership]]) на подведении итогов: для КАЖДОГО артефакта этой сессии довести цепочку до конца — **«собрали» это ещё НЕ финиш**. Финиш = построено → передано потребителю → **реально используется**. Три исхода на артефакт:
- ✅ **используется** — есть потребитель и он потребляет (скилл вызывают, рутина читает выход, поле CRM читают, дашборд открывают, данные доехали и применены). **Назвать потребителя** — иначе это не ✅.
- 🔗 **передано, потребления пока нет** — доехало, но никто ещё не читает/не применяет → на доску висячих, назначить потребителя/срок.
- ⚠️ **построено «в воздух»** — собрали и бросили, потребителя нет вовсе (dead-letter без consumer — как релинк-очередь: 29k сирот, 0 применено) → **ПОДСВЕТИТЬ оператору явно**: «построили X, но это никем не используется» → решить: подключить потребителя ИЛИ признать выброшенным.

Молчание ≠ используется. «Построили» без названного потребителя = недоделанный Connect, НЕ «done». Строкой: «🔗 Connect: ✅N используется · 🔗M передано-ждёт · ⚠️K в воздух».
⭐ **🌍 МИРОВОЙ ПОТРЕБИТЕЛЬ (dev 24.08, голосом):** у каждой закрытой за сессию починки КЛАССА — четвёртый исход Connect: раздали ли миру? Сеть-ловушка: строки Breakage-Journal этой сессии «класс закрыт» без вердикта 🌍 = долг → прогнать скилл **`/share-fix`** (порог переносимости, реверс-поиск по симптому, 3-5 лучших живых тредов, gist, вахта — вся механика там). Вердикт в отчёте обязателен: 🟢 раздал (ссылки) · ⚪ искал-пусто · ⛔ непереносимо/приватно+причина. Канон: `reglament-pochinil-u-sebya-srazu-razday-miru` + память `fixed-it-share-it-with-the-world`.
⭐ **ПРАВИЛО — ТОЖЕ АРТЕФАКТ (dev 06.08: «это же связывается с правилом коннект???» — да, связывается).** Правило, принятое за эту сессию, проходит тот же Connect-тест, только его «потребитель» — не человек и не следующая стадия, а **механизм, который правило вызовет**. Записали в канон — это «передали», не «используется». Прогон обязателен, по одной строке на правило:
`python ~/.claude/scripts/rule_home_guard.py <слаг>` → **✅ ДВЕРЬ ЕСТЬ и она ИСПОЛНИМАЯ** (потребитель назван) · **⚠️ ПОХОЖА НА ФИКТИВНУЮ** (слаг пересказан прозой, путь исполнения его не тронет — считается 🔗 «передано, потребления нет») · **⛔ БЕЗ ДВЕРИ** (= ⚠️ «в воздух», подсветить оператору явно).
Квота [[rule-needs-a-door-quota]]: дверь строится в ТОМ ЖЕ заходе (строка в существующем скилле дешевле нового робота) ЛИБО правило уходит в `~/.claude/rules-without-door.md` с датой и причиной. Замер, из-за которого пункт появился: 19 из 25 свежих правил (76%) не звал ни один скилл и ни один хук; «5 почему» пролежал в каноне 42 дня и не применился ни разу. Разбор класса: `razbor-serii-2026-08-06-pravilo-prinyato-dveri-net` (волт).
⭐⭐ **ПОЛЬЗУ НАШЛИ — ДАЛИ ФЛОТУ (dev 06.08, капсом «ВСЕГДА!! даже не спрашивай меня»).** У ОБЩЕЙ детали потребитель — не один человек, а **каждый узел флота**, поэтому Connect на ней закрывается только раскаткой. Прогон, по строке на сессию: `python ~/.claude/scripts/fleet_fix_audit.py --by-fix <id>` → кто применил, кто отстал. Исходы: ✅ **применено на всех потребителях** (доказано чтением факта на узле) · 🔗 **зарегистрировано, узел офлайн** — единственное законное ожидание · ⚠️ **осталось на одной машине** = «в воздух», подсветить. ⛔ Запрещено закрывать ретро строками «раскатать?», «жду ОК», «добью завтра» — раскатка не Tier-2 и не руки оператора, значит по §4.1 её решаю я, в ТОМ ЖЕ заходе. Раскатывается не только патч, а любая НАЙДЕННАЯ ПОЛЬЗА (приём, ожившая рельса, обнаружение что подписка идёт не в тот бак, грабли со стоимостью); тест — «пригодится другому узлу или оператору?». ⛔ `apply`, который не ДОСТАВЛЯЕТ файл, регистрировать нельзя — это корень висящих посылок (замер 06.08: 128 штук, apply был `doctor`, на Маяке лежал новый тест поверх старого движка). Живой узел по `tailscale status` → еду сам (ssh + `deploy_apply` НА УЗЛЕ), офлайн → готовые команды в шину. Канон: [[found-value-goes-to-fleet-always]], Библия `reglament-lyubaya-pochinka-raskatyvaetsya-na-ves-flot` §Поправка 06.08.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` = сейчас + 1-2 мин, разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro).

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].

## Step 4★ — The «repeats → make a skill» reflex (milestone closeout)
This is the step dev asked for (2026-06-18): at a finished milestone, don't just *note* a repeating action — **offer to turn it into a skill**. It's the retro-time expression of the standing rule `evaluate-recurring-into-routine` (повторяющаяся задача → оцени «на рутину?»). Mirror of [[capture-rules-into-bible]] (that catches *rules*; this catches *tasks-to-automate*).

**Trigger (catch it, don't wait to be asked):** any action that **repeated ≥2–3×** this session/milestone, OR that we'll **clearly return to** later (a manual sequence I re-typed, a multi-step procedure, a recurring check).

**Procedure — 4 cheap moves:**
1. **RECALL first — don't duplicate.** Skim the available skills + memory `automation-inventory` for an existing skill/routine/hook that already covers it. If one exists, point dev to it instead of building a twin. **⛳ И тут же второй вопрос (dev hub:5090, 2026-08-04): скилл ЕСТЬ — не проапгрейдить ли его?** «Есть» ≠ «закрыто»: назови, чего ему не хватило ИМЕННО в этой сессии (шаг, который я делал руками поверх скилла / грабли, которых в нём нет / устаревшая строка) → правка в тот же заход, и это тоже строка в 🔁→🛠 (`built/proposed/declined`). Нечего добавить — скажи это словом, молчание = проверка не сработала. Дословный текст вопроса и формат ответа — единственный источник в `/skill-gap` §⛳ (там же — вход-конец рефлекса).
2. **⚠️ AK-47 guard — a skill is just a `SKILL.md`.** One markdown file with a procedure, NOT a server / DB / webhook / external service. (This is the exact trap the Codex milestone-retro report fell into — over-engineered for a SWE team; rejected 2026-06-18.) If the thing genuinely needs more than a markdown procedure, flag it **⚠️ УСЛОЖНЕНИЕ** and let dev decide.
3. **OFFER as ДО→ПОСЛЕ** (per `show-before-after`) — one compact block:
   > **ЧТО:** собрать `/<имя-скилла>` · **ДО:** как делаю руками сейчас (на реальном примере этой сессии) · **ПОСЛЕ:** одна команда `/<имя>` · **что сломается:** ничего (надстройка) · **делаем? да/нет**
4. **On dev's «+» → build it via `skill-creator`.** Pick the right home by SHAPE (per `operating-agreement` → «Where durable rules go»):
   - on-demand ritual I run when asked → **skill** (`skill-creator`).
   - «каждый раз автоматически когда X» → **hook** (skill `update-config`), not a skill.
   - time-based «каждый понедельник / каждое утро» → **scheduled task / routine** (skill `schedule`).
   - «рутина» ≠ обязательно 24/7-робот — часто правильное = простой полуавто + напоминание.
   - ⭐ **СПИСОЧНАЯ работа на N кусков (N велико) → КОНЕЧНАЯ рутина, «слон»** (dev 23.08, §4.5-бис).
     Признак: в сессии я перебирал однотипные элементы (видео / заметки / карточки / островá графа /
     ссылки), список не кончился, и он не кончится и в следующий раз; либо задача уже месяцами
     спотыкается об участие оператора, лимиты вендора или баны. Это НЕ задача и НЕ героическая сессия —
     это слон: `python ~/.claude/scripts/elephant.py new <slug> --title T --quota N --os-task <ЗадачаWindows>`,
     дальше рабочий скрипт на каждом прогоне делает `next` → работа → `mark` → `tick`.
     `tick` сам ловит конец (выключает OS-задачу + доклад в TG-03) и затык (5 пустых прогонов → `blocked`).
     ⛔ Журнал слона НИКОГДА не кладём в синкаемую папку — затрётся, и слон не кончится никогда.
     Живой пример: [[yt-watch-history-drip]]. Канон: [[finite-routines-eat-the-elephant]].
   Then route/link it normally (Step 4) and mention it in the final report (post-hoc, not for permission).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the ready `/compact` line (Step 6).
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Write a clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- The nightly **Brain Reindex @04:00** makes it `/ask`-searchable — no manual reindex needed.

**6a-бис. Снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- Команда: `python %USERPROFILE%\.claude\scripts\retro_lost_scan.py mark-done <sessionId> --note "ретро: <имя заметки>"`
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.

**6b. Hand dev the ready paste-block** — ⚠️ CORRECTED 2026-07-22: bare `/compact` does NOT read `CLAUDE.md § Compact Instructions`. That earlier claim was FALSE — PreCompact hooks cannot inject instructions (only block; issue #14160 pending), and the evidence is 354/354 past compacts came out in the DEFAULT English template. Our 7-header format is applied ONLY when the block is pasted INLINE after the command: `/compact <text>`. So PRINT the fenced «Готовая строка» block from `$USERPROFILE/.claude/compact-prompt.md` and tell dev to PASTE it right after `/compact`. Then the fork:
> **«Готово, всё в волте. Хочешь остаться в задаче налегке — ВСТАВЬ блок ниже целиком после `/compact` (без него сжатие пойдёт по дефолтному английскому шаблону, не по нашему 7-заголовочному). Или новый чат — всё уже заархивировано, не зависит от нажатия.»**
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; the squeeze + paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

---

**Claude:**

понедельник, вечер, 20:36, 24 августа 2026

Запускаю ретро. Шаг 0 — сверка: хребет сессии, соседние ретро, дневной леджер, ON AIR:

---

> `Bash` -- {"command": "python \"D:/Vault/_imports/turnstate/turnstate_show.py\" 2>&1 | tail -30", "description": "Session spine from turnstate"}

---

> `Bash` -- {"command": "ls -t \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/\" | head -8; echo ---; python ~/.claude/scripts/onair.py list 2>&1 | tail -5", "description": "Recent retros + ON AIR board"}

---

> `Bash` -- {"command": "python \"D:/Vault/_imports/day_ledger.py\" --recall 1 2>&1 | tail -25", "description": "Day ledger for today"}

---

> `Bash` -- {"command": "grep -c \"чист\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\"; grep -in \"чистого листа\\|clean.slate\\|первая минута\" \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" | head -5", "description": "Count clean-slate breakage class in journal"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/rule_home_guard.py contributions-packaged-as-product 2>&1 | tail -6", "description": "Door check for the /pack rule"}

---

> `Bash` -- {"command": "cat >> \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" << 'EOF'\n- 2026-08-24 · публичный `--check` у workdir-sentry падал трейсбеком у пользователя БЕЗ конфига (первая минута знакомства) · условия: тестировали только на машине автора, где конфиг есть; «запуск с чистого ли

---

> `Bash` -- {"command": "python \"D:/Vault/_imports/content-factory/content_miner.py\" capture --title \"Гейт качества окупился на первом прогоне: трейсбек первой минуты\" --note \"Выложили публичную тулзу workdir-sentry (gist). Прогнали свой новый чеклист упаковки /pack — притворились новичком без конфига: 

---

**Claude:**

Growth-log Макса + строка в Ship log роадмапа:

---

> `Bash` -- {"command": "cat >> \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/cofounder-growth-log.md\" << 'EOF'\n- 2026-08-24 · hub · урок: оператор хвалит не за скорость, а за ПРОДУКТ («теперь ты сделал ПРАВИЛЬНО») — планка качества наружу выше планки внутрь, и её надо было снять в станда

---

> `Bash` -- {"command": "grep -n \"^## \\|^### \" \"D:/Vault/Vault-Knowledge/04-Projects/ROADMAP.md\" | head -15; grep -n \"2026-08-24\" \"D:/Vault/Vault-Knowledge/04-Projects/ROADMAP.md\" | head -5", "description": "Find Ship log section structure and today's lines"}

---

> `Edit` -- {"replace_all": false, "file_path": "D:\\Vault\\Vault-Knowledge\\04-Projects\\ROADMAP.md", "old_string": "## 📜 SHIP LOG — что уже доехало (для фолловеров: мы реально шипим)\n- **2026-08-24** · Продукт Голикова", "new_string": "## 📜 SHIP LOG — что уже доехало (для фолловеров: мы реально шипим)\n- 

---

**Claude:**

Пишу ретро-ноту хвоста в волт и снимаю сессию с очереди retro-lost:

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\01-Conversations\\Claude\\Retros\\retro-2026-08-24-pack-skill-and-gist-etalon.md", "content": "---\ntitle: \"Retro: скилл /pack и добивка гиста workdir-sentry до эталона\"\naliases: [\"Ретро: упаковка контрибьюшенов как продукт\"]\ndate: 2026-08-24\ntype

---

> `Bash` -- {"command": "printf '\\n**Продолжение того же дня:** хвост сессии → [[retro-2026-08-24-pack-skill-and-gist-etalon]] (декрет «продукт, не сниппет» → скилл /pack + гист добит до эталона).\\n' >> \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-08-24-home-dir-guard-fleet-rollout.

---

**Claude:**

понедельник, вечер, 20:44, 24 августа 2026

**🔎 сверка:** проверено — хребет turnstate, 8 свежих ретро, ON AIR (пуст), леджер дня (ещё не собран). У этой сессии уже есть два ретро за сегодня (home-dir-guard ×2, мои же, до компакта) → это ретро покрывает только **хвост**: декрет качества → `/pack` → гист v2.1. ✅ aligned, дублей не создаю, инвентарь-скрипт повторно не гонял.

**🎬 Сегодня мы поняли (хвост):** оператор похвалил апгрейд таблетки и тут же превратил похвалу в закон — «всегда продукт, не сниппет». Закон снят в скилл `/pack`, скилл немедленно прогнан по собственному гисту — и первый же прогон окупил гейт: пункт «запуск с чистого листа» поймал трейсбек первой минуты (у автора конфиг есть, у новичка — нет). Добито до v2.1, доезд проверен байтами. Урок дня: **среда автора ≠ среда новичка**, и свой новый инструмент первым применяй к своему же вчерашнему артефакту.

**🎙 Майк:** 💰 — гист с вежливой первой минутой конвертит скачавших в пользователей, а пользователей — в тех самых инженеров Mission-2; 🔪 — убил бы двойной прогон rule_home_guard (гейт §10.0 правильно отбил, доказательство уже было); 🤺 — спорить было не с чем, приказ совпадал с уликами; ❓ — `/pack` требует «самодиагностику за 30 сек» в каждом README: делаем её обязательной и для внутренних паспортов деталей?

**♻️ Reuse:** `/pack` 🟢 ✅ (refs-тест exit 0) → потребители /share-fix + /release-slice · гист v2.1 🟢 ✅ (selftest 7/7 + 3 clean-slate) → 6 тредов, ссылка та же · память+MEMORY.md 🟢 · Ship log ROADMAP ➕1.

**🩹** 1 строка в Breakage-Journal: класс «clean-slate не проверен», 1-й случай, починен тем же заходом, дверь уже есть (гейт /pack). **🔁→🛠** — новых повторов нет, скилл и есть продукт этого рефлекса. **🔗 Connect:** ✅3 используется · 🔗0 · ⚠️0; 🌍 по хвосту — раздача не нужна (сам гист и есть раздача, апдейт доехал в треды автоматически). **⛳ дрифта нет.** **📋 журнал:** без изменений (хвост задач не рождал; открытые ACK/BOM/awesome-list уже в карточках). **🗺 roadmap:** ✅1 продвинуто (Ship log: /pack + эталон-гист) · ➕0 · —. **🎬 контент:** момент «гейт окупился на первом прогоне» → черновик в воронку (cc:live-d9461e, medium, draft-first). **📓 growth-log:** запись добавлена. Ретро-нота: [retro-2026-08-24-pack-skill-and-gist-etalon.md](D:\Vault\Vault-Knowledge\01-Conversations\Claude\Retros\retro-2026-08-24-pack-skill-and-gist-etalon.md), перелинкована, сессия снята с очереди retro-lost.

**🗜 Compact handoff:** всё в волте — можно спокойно уходить в новый чат. Хочешь остаться тут налегке — `/compact` + вставь inline-блок из `~/.claude/compact-prompt.md` (без него сжатие пойдёт дефолтным английским шаблоном).

🧒 Простыми словами: мы оглянулись на вечер и разложили всё по полкам. Главная находка вечера: наш новый контролёр качества на первой же проверке нашёл настоящую дыру — игрушка ругалась непонятными словами на нового человека. Мы это записали в дневник уроков, в летопись «что мы отгрузили», и даже заготовили из этого историю для поста. Всё ценное лежит в шкафу с ярлыками, ничего не утонуло в болтовне.
