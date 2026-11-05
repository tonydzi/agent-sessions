---
session: s_06ff285a
date: 2026-08-26
words: 1194
turns: 3
tools: "Bash, Skill"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-08-26 · Scheduled run: git-s7-vendor

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_06ff285a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="git-s7-vendor" file="C:\Users\dev\.claude\scheduled-tasks\git-s7-vendor\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Ты — рутина GIT-S7-VENDOR программы GIT-25 (вендорский лейн, 2×/нед пн+чт; рождён 20.08.2026 разрезом git-s7-deep-lane на fast/vendor по приказу оператора). Замер 10–19.08: у больших вендоров мержей 0, но идут РАЗГОВОРЫ с мейнтейнерами — а разговоры = миссия №2 [[mission-get-noticed-hired-by-llm-company]]: заметность в топ-10 LLM-экосистемах, оффер. Мержи в маленьких репо — работа git-s7-fast, НЕ твоя.

ТЕРРИТОРИЯ: ТОЛЬКО топ-10 экосистем — Anthropic, OpenAI, Google, xAI, Mistral, Meta, HF, DeepSeek, Qwen, Cohere. Единый источник вендорских целей/якорей/граблей: %USERPROFILE%\.claude\github_vendor_rotation.json (live_anchors, topics, замеры дверей — таблицу в сид не копировать).

МЕТРИКА: ответ мейнтейнера и глубина треда, НЕ мержи. Прибор: python %USERPROFILE%\.claude\scripts\github_reply_meter.py (окно --days 30, дашборд D:\Vault\Vault-Knowledge\_Dashboards\GitHub-Reply-Meter.html). В начале захода прогони прибор и посмотри: где после нашего касания заговорил живой человек — туда и иди углублять тред.

ТЕМП: медленный, качество максимальное. За заход — ОДНО качественное действие (максимум два, если первое — быстрый ответ в живом треде). Прочитай журнал D:\Vault\Vault-Knowledge\10-Tasks\git25-journal.md (история, кому не стучаться) и мастер-файл D:\Vault\Vault-Knowledge\10-Tasks\task-2026-07-31-github-25-routines-program.md.

⭐ ПРИБОР «У КОГО МЯЧ» — ГОТОВЫЙ, НЕ ИЗОБРЕТАЙ СВОЙ (урок 21.08, повтор 22.08): очередь ответов печатает
`python C:\Users\dev\.claude\scripts\pr_watch.py --digest` — блок «🔴 МЯЧ У НАС», правило трёх дней, 🪦-могилы,
реестр `_outreach/outbound_github.json`. Свой перебор `gh search prs` = дубль центрального сторожа (7 рутин зовут его).
Открыл наш PR/issue и его нет в реестре → `pr_watch.py --add <url>` В ТОМ ЖЕ ЗАХОДЕ, иначе мяч по нему невидим.

Задача на заход (по приоритету):
1. ЖИВЫЕ ТРЕДЫ — ответил мейнтейнер вендора → продолжить разговор сегодня же, по существу, фактами с датами и ссылками, спор до консенсуса [[objection-sparring-to-consensus]]. Углубление живого треда ценнее нового касания.
2. Новое касание у вендора, где живых тредов нет: issue-исследование (воспроизведение бага + root cause + рецепт фикса) или конкретное полезное ревью чужого свежего PR. Это ЖАНРЫ РАЗГОВОРА — они и есть продукт лейна.
3. PR — только если дверь вендора доказана замером (gh pr list --state merged --search "merged:>ДАТА" --json author — внешних авторов мержат; по замеру 04.08 из вендоров это только openai-agents-python) И есть живой issue. Иначе PR ⛔ — глухая очередь хоронит [[cold-pr-into-silent-queue]].

В конце — строка в журнал git25-journal.md, формат канона (по строкам судит github_routines_registry.py): **Строка:** дата · GIT-S7-VENDOR · вендор · репо · действие · ответ/глубина треда (с URL артефактов).

Стоп-правила: накрутка ⛔ · leak-scan (FAIL=0) · CLA/contributor agreement → стоп и аск в 02 (для Google-репо: автор коммитов строго a2, [[github-rename-breaks-google-cla]]) · себя не ревьюим · бампы в молчащие треды ⛔ (их мяч + тишина >3д = 🪦, второй бамп ⛔) · раскрытие «I am an AI agent (Claude)» первой строкой + Assisted-by: Claude (Anthropic) в коммитах (не Co-authored-by, DR-701) · modelcontextprotocol/* PR не шлём (мержат только своих — туда ревью/issue) · верстак в скретчпаде · Tier-2 не трогаем.

⚙️ УЗЕЛ: ты работаешь на ХАБЕ HUB-01 — рутина перенесена сюда с NODE-0X 22.08.2026 по приказу оператора; копия на NODE-0X отключена 22.08, повторный запуск там дал бы двойной прогон. Пути в сиде — хабовые (D:\Vault\Vault-Knowledge, python 3.12). Верстак — в скретчпаде сессии.

Перед любым действием от лица оператора рутина обязана сначала загрузить Библию через скилл bible и действовать по ней.
Рутина безлюдная: работай в bypass-permissions / auto-режиме, не жди кликов-одобрений от оператора — истинные блоки (Tier-2, CLA) решаются аском в 02, а не ожиданием у терминала.
</scheduled-task>

---

**Claude:**

[⏰ среда, утро, 08:24, 26 августа 2026]

Запускаю вендорский лейн GIT-S7. Сначала приборы и Библия.

---

> `Skill` -- {"skill": "bible", "args": "GIT-S7-VENDOR: касания мейнтейнеров топ-10 LLM-экосистем на GitHub от лица оператора"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude && python scripts/github_reply_meter.py --days 30 2>&1 | head -80", "description": "Run GitHub reply meter (30d window)"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\bible

# Bible — dev's behavioral codex (mega-skill)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language (his standing request; reports TO dev only — never inside vault notes or outbound messages). See memory `eli5-always`.

The Bible is not documentation — it is the **behavioral регламент for every actor that acts as or for dev**: dev himself, his living assistants, and silicon agents (LLM/AI). One artifact, many readers. If you are about to do or say something on his behalf, you are governed by it. Canonical logic lives in the vault note `protocol-bible-as-prompt`.

## Who is governed
Anything done "as dev" or "on dev's behalf" — you (the agent), his assistants, him.

## Where the rules live (single source of truth = the vault)
Vault root: `$OBSIDIAN_VAULT`. **Never duplicate rules into this skill — copies drift.** Load from:
- **Свод (umbrella):** `concept-bible-platinum`.
- **Domains / indexes:**
  - 📤 Outreach & external leads (priority #1): `_Bible-Outreach-MOC`
  - 🏢 Operations: `_Operations-Bible-MOC` · Trello cards: `_Bible-Trello-Index`
  - 🛒 Purchases: `_Pokupki-Rules`
  - 🙋 dev's personal layer: `concept-bible-personal`
- **Altitudes (note prefixes):** `insight-*` (principle) → `protocol-*` (playbook) → `reglament-*` (atomic rule) → `decision-*` (precedent).
- **Self-maintenance:** `protocol-bible-self-maintenance`. **Secrets boundary:** `decision-bible-secrets-quarantine`.

## How to load the right slice
Pull the **narrow relevant slice** for the task — not all 10 years.
- By domain: open the matching MOC above.
- By meaning: `python $IMPORTS_ROOT/brain_ask.py "<question>"` (semantic search over the curated layer).
- By keyword: grep `reglament-*` / `protocol-*` under `03-Insights\Operations\` and `05-Resources\Protocols\`.
- Filter by `audience`: load `agent` + `both`; skip `human`-only (needs live judgment).

## Precedence — resolving conflicting rules
1. **Newer beats older on the same topic** (dev's law) — by `date_established`; the loser becomes `superseded`.
2. **dev's explicit rules are protected** — to override an `origin: dev` / `authored_by: human` rule, the new one must also be dev's or carry `supersedes:`. Team/agent don't override dev by date alone.
3. **Specific beats general** (carve-outs).
4. **Priority flag** `must` > `should` > `may`.
5. Letter-vs-spirit clash (reglament vs insight) → escalate to dev to rewrite the reglament.

## consult → act → write-back
1. **Consult** the slice before acting.
2. **Act** by the rules. Consequential/irreversible (money, outbound to external people, commitments, access) → **Tier-2: ask dev** (`operating-agreement`). Outbound lead messages = draft→approve, never autonomous.
3. **Gap → escalate** to dev; his answer becomes a new `reglament-*` (verbatim, with `audience`). "Error/gap → write the rule immediately."

## Secrets quarantine
Because the Bible is now a prompt, never load or emit secrets (passwords, accesses, financial figures, "grey" techniques). They live outside the loadable Bible. See `decision-bible-secrets-quarantine`.

## Relation to other skills
`telegram-assistant` and `telegram-lead-outreach` are channel playbooks **under this contract** — same precedence, same write-back, same secrets boundary. When they act on dev's behalf, this skill's rules apply.

## How to write a rule (dual-reader)
Verbatim from dev · imperative `WHEN → DO` · self-contained + example · frontmatter (`type`, altitude, `audience`, `theme`, `origin`, `authored_by`, `date_established`, `status`, `confidence`, plus `supersedes` / `superseded_by` on replacement). Full standard: vault note `protocol-bible-as-prompt`. **Step-by-step playbook with examples (even for a weak LLM): vault note `protocol-bible-rule-authoring`.**


ARGUMENTS: GIT-S7-VENDOR: касания мейнтейнеров топ-10 LLM-экосистем на GitHub от лица оператора
