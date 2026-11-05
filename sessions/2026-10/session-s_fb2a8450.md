---
session: s_fb2a8450
date: 2026-10-24
words: 4743
turns: 11
tools: "Bash, Skill, ToolSearch, mcp__97420a88-50ae-4ab1-99f6-f5ec547aebd8__search_threads"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-24 · В подкасте Constellation и Redwood, ты сделал подкаст Constellation и Redwood, упоминается…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fb2a8450` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

В подкасте Constellation и Redwood, ты сделал подкаст Constellation и Redwood, упоминается о том, что сейчас существуют многие различные филошип-программы, программы менторства, инкубации и так далее, я не знаю, как London, Berkeley и так далее. Напомни, пожалуйста, все, что мы на этой теме уже изучали. Я хочу, чтобы вы подали мою кандидатуру на все вот эти филошип-программы. Однако перед тем, как подавать, давай берем благоследование, чтобы максимизировать наши шансы быть клиентами. Это очень важно. Максимизация шансов быть клиентами. И также вот эти Constellation, Redwood и так далее, и подобные компании, они хайрят. Давай тоже добавим в нашу воронку по найму, потому что зарплата достаточно приличная в этих местах. Я хотел бы тоже оплавиться на все, что...

---

**Claude:**

Начинаю с RECALL: ищу подкаст Constellation/Redwood и всё, что мы уже собирали по фелошипам.

---

> `Skill` -- {"skill": "recall", "args": "фелошипы Constellation Redwood MATS LASR Astra менторство инкубация AI safety + найм в этих организациях"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\recall

# /recall — что мы уже делали по теме, до того как строить

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap.

**Зачем.** Правило §0.3 CLAUDE.md: RECALL до стройки, до вопроса и до слов «нет доступа».
До 14.10.2026 слово «RECALL» жило в каноне, а команды с таким именем не было ни на одной
полке; оператор ввёл `/recall` в Codex, и модель, не найдя скилла, пошла в ближайший по
звучанию `/find` (поиск ЧЕЛОВЕКА по имени). Этот файл закрывает дыру: одно имя, одна дверь.

**Чем НЕ является (соседние полосы, не путать):**
- `/find <имя>` — человек, лид, компания по написанию имени (0 токенов, не RAG).
- `/search <слова>` — точные слова внутри переписок (BM25 по чатам).
- `/ask <вопрос>` — ответ по СМЫСЛУ курируемого волта, когда нужен ответ, а не след работы.
- `/1` — восстановление после обрыва ЭТОЙ сессии («где мы были, всё ли живо»).
- `/recall <тема>` — след ПРОШЛОЙ работы по теме: делали ли, решали ли, строили ли, где лежит.

## Шаги (все в одном заходе, порядок важен)

### Шаг 1 — ступени по свежести одной командой
```bash
python "$IMPORTS_ROOT/brain_ask.py" "<тема двумя-пятью словами>"
```
`brain_ask.py` печатает ступени из `recall_tiers.py`: 🟢 готовое (MEMORY.md узла + задачи и
решения за 3 дня) → 🟢 свежие сессии узла ≤14 дней → 🟡 книга чатов ≤30 дней + сырьё волта →
🔵 курируемый волт (вектор + реранк). Старое → добавь `--archive`.
Сервер `:8770` не ответил → скажи это строкой «RAG не отвечал» и иди на Шаг 2, не молчи.

Портируемость: `$IMPORTS_ROOT` = `D:\Vault\_imports` на Win-узлах оператора,
`/root/Obsidian/_imports` на Маяке, у маков по `~/.claude/machine.env`. Переменной нет →
возьми путь из `fleet_nodes.json`, литерал не хардкодь.

### Шаг 2 — память узла и прошлые сессии (0 токенов, работает без сервера)
```bash
grep -ril "<ключевое слово>" ~/.claude/projects/*/memory/ | head -20
python "$IMPORTS_ROOT/sessions_fts.py" search "<тема>" --since 30 --json | head -40
```
Пусто из ОДНОГО места не значит «нет»: обе команды обязательны (§5.4).

### Шаг 3 — вердикт тремя строками, потом работа
```
уже есть: <файл/скрипт/заметка/решение с датой> | нет следа
решено оператором: <цитата с датой> | не нашёл
строю / не строю: <что именно и почему>
```
Нашёл сделанным → не повторяешь, докладываешь чем и когда закрыто (§8.4, «+» старше суток).

## Для других агентов (Codex, Cursor, Grok, GLM)
Скилл детерминированный: нужны только Python и доступ к волту. Коннекторов Claude не требует.
Codex уже получает подсказку `[memory-recall]` на старте сессии; `/recall` — ручная дверь той
же работы по конкретной теме. оператор набрал `/recall`, а скилла нет на твоей полке → это
дефект полки (`codex_skills_bridge.py sync`), а не повод брать `/find`.

🧒 Простыми словами: перед тем как строить, сперва загляни в тетрадку: «а мы это уже делали?».
`/recall` и есть эта тетрадка. `/find` ищет человека, `/search` ищет слова в чатах, а `/recall`
ищет след нашей прошлой работы.

Machine: HUB-01 (Хаб) · Agent: Claude Code/Fable 5.1 · Operator: dev · 2026-10-14


ARGUMENTS: фелошипы Constellation Redwood MATS LASR Astra менторство инкубация AI safety + найм в этих организациях

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports\" && timeout 90 python brain_ask.py \"фелошипы Constellation Redwood MATS LASR Astra\" 2>&1 | head -80", "description": "Run RAG recall on fellowships topic", "timeout": 120000}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && grep -rli -E \"constellation|redwood research|MATS |LASR|astra fellow|fellowship\" --include=*.md . 2>/dev/null | head -60", "description": "Grep vault for fellowship notes"}

---

> `Bash` -- {"command": "grep -rli -E \"constellation|redwood|fellowship|MATS\" ~/.claude/projects/*/memory/ 2>/dev/null | head -20; cd \"D:/Vault/_imports\" && timeout 60 python sessions_fts.py search \"Constellation Redwood fellowship\" --since 30 --json 2>&1 | head -40", "description": "Grep memory and se

---

**Claude:**

Нашёл главное. Читаю ключевые файлы: пакет подкаста, исследование Codex 01.10, ретро 07.10 и судьбу заявки Anthropic Fellows.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && cat \"05-Resources/NotebookLM/_packets/sf-2026-10-constellation-redwood.md\"; echo ======; cat \"01-Conversations/Claude/Retros/retro-2026-10-07-alt-fellowship-programs.md\"", "description": "Read podcast packet and alt-fellowship retro"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && cat \"04-Projects/Pipe-A-Batches/alt-programs-2026-10-01-codex-research.md\" | head -150; echo =====; cat \"01-Conversations/Claude/Retros/retro-2026-10-02-afp-submitted-then-superseded.md\" | head -60", "description": "Read Codex alt-programs resea

---

> `Bash` -- {"command": "sed -n 25,200p \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_fb2a8450/tool-results/by6kkf4ym.txt\"", "description": "Read rest of Codex research"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && ls 04-Projects/Pipe-A-Batches/ | grep -i -E \"alt|fellow|afp|aisb|aisc\" ; ls 10-Tasks | grep -i -E \"fellow|afp|aisb|aisc|mats|astra|iliad|alt-prog|govai|apollo|metr|far\" | tail -40", "description": "List fellowship batch files and tasks"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && grep -n -E \"^\\||Итог|статус|status\" 04-Projects/Pipe-A-Batches/alt-programs-2026-09-30.md | head -70; echo ====; head -40 10-Tasks/task-2026-10-07-aisb-coderbyte-assessment.md; echo ===; grep -n -E \"state:|status:\" 10-Tasks/task-2026-09-29-metr

---

**Claude:**

Теперь проверяю воронку найма: что из этих организаций уже стоит в jobs.db.

---

> `Bash` -- {"command": "cd /e && for p in \"D:/Vault/_imports\" \"E:/!CLAUDE-HUBPC-June26\" \"C:/Users/dev/.claude\"; do find \"$p\" -maxdepth 3 -name \"jobs*.db\" 2>/dev/null; done", "description": "Locate jobs database"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && ls -la jobs.db \"E:/!CLAUDE-HUBPC-June26/jobs.db\"; python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor t, in c.execute(\\\"select name from sqlite_master where type='table'\\\"):\n    print(t, c.execute(f'select count(*) from {

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nfor t in ['jobs','ats_jobs']:\n    cols=[r[1] for r in c.execute(f'pragma table_info({t})')]\n    print(t, cols)\norgs=['constellation','redwood','metr','apollo','far.ai','far ai','gove

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nq='''select company,title,status,applied,comp_text,last_seen,url from ats_jobs where lower(company) in (select lower(company) from ats_jobs where lower(company) like '%redwood%' or lowe

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && grep -n \"DR26-09-26-MACANTON-01-1441\" _DR-Registry.md | head -5; ls _machine-bus/_dr/queue/DR26-09-26-MACANTON-01-1441/ 2>/dev/null; ls 03-Insights | grep -i \"1441\"; head -c 2500 _machine-bus/_dr/queue/DR26-09-26-MACANTON-01-1441/prompt.md 2>/de

---

> `ToolSearch` -- {"query": "select:mcp__s_8e110270__search_threads", "max_results": 1}

---

> `mcp__s_8e110270__search_threads` -- {"query": "newer_than:20d (aisb OR \"safety camp\" OR aisafety OR constellation OR matsprogram OR anthropic fellows OR iliad OR lasr OR pivotal OR coderbyte OR metr OR apollo research)", "pageSize": 30}

---

**Claude:**

Коротко: RECALL закончен, нашёл всё, что мы делали по фелошипам. Собираю итог и план.

---

> `Bash` -- {"command": "python ~/.claude/scripts/machine_stamp.py sig --model \"Opus 5.5\" 2>&1 | tail -1; date \"+%H:%M %Z\"; TZ=Europe/Lisbon date \"+%d.%m %H:%M Lisbon\"", "description": "Get session signature and current time"}

---

**Claude:**

# Фелошипы и найм в AI safety: что мы уже сделали и план

Твоё сообщение оборвалось на «оплавиться на все, что…». Я понял так: подаёмся во все программы и на все подходящие вакансии в этих организациях. Если ты имел в виду другое, допиши, и я поправлю.

## Что уже сделано

**1. Подкаст про Constellation и Redwood (13.10).** Пакет к нему лежит в `05-Resources/NotebookLM/_packets/sf-2026-10-constellation-redwood.md`. В нём:
- **Astra:** 5 месяцев в Беркли, $8 400 в месяц, отбор в 4 этапа (скрининг, кодинг-тест, рабочие тесты, интервью), нужны две рекомендации. Больше 80% выпускников потом работают в AI safety.
- **Constellation Visiting Fellowship:** без стипендии, но оплачивают жильё и дорогу. **Generator Residency:** 3 месяца, для тех, кто строит проекты.
- **MATS** (Беркли и Лондон): $1 250 в неделю, 12 недель.
- **Redwood:** Member of Technical Staff (инженер-исследователь), $350–850K. Своей программы у Redwood нет, они сами отправляют людей в MATS и Astra.
- **Constellation нанимает:** Program Manager $130–155K, Coordinator $105–133K. Я тогда отметил, что тебе ближе всего их команда Talent Mobilization: она подбирает людей на важные роли, а это близко к твоему опыту продаж и B2B.

**2. ДР DR26-09-26-MACANTON-01-1441 (26.09, кворум 4/6).** Он собрал все оплачиваемые двери в frontier AI для сильного инженера по безопасности без опыта ML-исследований: METR, UK AISI, MATS Residency, Anthropic FRT.

**3. Anthropic Fellows подана 30.09.** 01.10 подали заново, и Anthropic засчитала вторую заявку. В ней рефери Toshio заменён на Ryan Lyell: он мейнтейнер marm-memory и смержил твои PR.

**4. 30.09 обошли 18 программ и подали 11 заявок.**
- **Настоящие заявки:** AI Safety Camp 12 (Project Lead) и AI Security Bootcamp London.
- **Записи в лист ожидания следующего набора:** Astra, Visiting, Generator, MATS, LASR, Pivotal, PIBBSS, SPAR и будущие наборы AISB.

**5. Ревизия Codex 01.10 нашла пропущенное.**
- **MATS Residency** открыт до 31.10.
- **Вакансии:** METR Task Development Engineer ($261–385K), Apollo AI Red Team, FAR Research Engineer, ARC Chief of Staff.

## Что сейчас горит

| Что | Статус |
|---|---|
| **Iliad Fellowship** | ⛔ Не подана. Анкета заполнена, отправку блокирует проверка Cloudflare на кнопке Submit. **Дедлайн 19.10, то есть завтра.** Нужна твоя рука на одну галочку |
| **AISB, технический тест** | Ты прошёл первый отбор. Ссылка на тест истекла около 11.10, проходил ли ты его, я не знаю. Задача по нему до сих пор открыта |
| **MATS Residency** | Открыт до 31.10. Текст проекта уже есть, не хватает примера твоей работы и двух рефери |
| **Воронка найма** | METR (10 вакансий), Apollo Research (14) и FAR уже в базе вакансий, но все стоят в статусе «заблокировано»: капча или вопрос в анкете. **Redwood, Constellation, GovAI и ARC в базе нет вообще** |
| **Почта** | В ящике a2 ответов от программ за 20 дней нет. Ящик a@, куда шли заявки, этим инструментом я не проверял |

## План

1. **ДР «как максимизировать шансы на отбор».** Это то, о чём ты просил перед подачами. Прошлый ДР отвечал на вопрос «куда подаваться», а этот ответит «как пройти». Внутри:
   - что реально решает отбор в Astra, MATS, LASR, Pivotal, Iliad и Constellation;
   - какие рефери и примеры работы работают лучше;
   - как подать твой профиль: безопасность, Python/C++ и наши PR в Inspect и Gemini cookbook;
   - типичные причины отказов;
   - интервью выпускников.

   Работаю по Альфа-протоколу: номер в реестре, рассылка по 6 рельсам через браузер, кворум 4/6.
2. **Добавить в воронку Redwood, Constellation, GovAI и ARC** с вилками зарплат. По Constellation приоритет Talent Mobilization, по Redwood MTS честно: руками модели ты не обучал.
3. **Подачи по скиллу `/apply`, после выводов ДР.** Каждую штучную заявку перед Submit смотрят чужие глаза. В прошлый раз 11 заявок ушли без такой проверки, этот провал записан в ретро 07.10.
4. **Сейчас, не дожидаясь ДР:** Iliad (нужна твоя галочка) и MATS Residency (дедлайн 31.10).

**Рельсы:** ДР уходит на ChatGPT, Gemini, Grok, GLM и Mistral через браузер. Тексты заявок вычитывают Codex и Grok. Я сам делаю координацию, сверку фактов и финальные тексты.

🎙 Майк: в прошлый раз первым и с «да» ответил тот, кого не было в твоём списке: AI Security Bootcamp. Поэтому ДР будет искать ещё и двери, о которых мы пока не знаем. Вопрос-руль: прошёл ли ты тест AISB? Если да, это самый сильный аргумент во всех остальных заявках.

**Мне от тебя две вещи:** допиши, на что «всё, что…», и открой Iliad до завтра, я покажу, где нажать.

🧒 **Простыми словами:** ты уже стоишь в очереди в десятке «школ для исследователей ИИ», и в одну тебя уже позвали на экзамен. Дальше я сначала выясню, чем берут приёмные комиссии, а потом подам тебя везде, где можно. Ещё я внесу Redwood и Constellation в список работодателей: там платят от $130K до $850K. Завтра горит одна анкета, и нажать там можешь только ты.

🏛H · Opus 5.5 · 10744

---

**User:**

Чини корни. Чини корни, думай как кофаундер и думай, как все это оптимизировать, и какую в итоге пользу мы все это получим. Будь максимально проактивен. Делай все, что мы с тобой проговорили, все, что ты предложил делать.

---

**User:**

<command-message>workflow-authoring</command-message>
<command-name>workflow-authoring</command-name>
<skill-format>true</skill-format>

---

**User:**

# Workflow authoring reference

A workflow structures work across many agents — to be comprehensive (decompose and cover in parallel), to be confident (independent perspectives and adversarial checks before committing), or to take on scale one context can't hold (migrations, audits, broad sweeps). The script is where you encode that structure: what fans out, what verifies, what synthesizes.

When you do call it, the right move is often **hybrid**: scout inline first (list the files, find the channels, scope the diff) to discover the work-list, then call Workflow to pipeline over it. You don't need to know the shape before the *task* — only before the *orchestration step*.

Common single-phase workflows you can chain across turns:
- **Understand** — parallel readers over relevant subsystems → structured map
- **Design** — judge panel of N independent approaches → scored synthesis
- **Review** — dimensions → find → adversarially verify (the review-changes example)
- **Research** — multi-modal sweep → deep-read → synthesize
- **Migrate** — discover sites → transform each (worktree isolation) → verify

For larger work, run several in sequence — read each result before deciding the next phase. You stay in the loop; each workflow is one well-scoped fan-out.

**Ultracode.** When a system-reminder confirms ultracode is on, that opt-in is standing: author and run a workflow for every substantive task by default. The goal is the most exhaustive, correct answer you can produce — token cost is not a constraint. For multi-phase work (understand → design → implement → review), that often means several workflows in sequence — one per phase — so you stay in the loop between them. The quality patterns below (adversarial verify, multi-modal sweep, completeness critic, loop-until-dry) are the tools; pick what fits the task. Lean toward orchestrating with workflows and adversarially verifying your findings — unless the work is trivial or already verified. Solo only on conversational turns or trivial mechanical edits. When a reminder says ultracode is off, revert to the opt-in rule in the Workflow tool description.

Pass the script inline via `script` — do not Write it to a file first. Every invocation automatically persists its script to a file under the session directory and returns the path in the tool result. To iterate on a workflow, edit that file with Write/Edit and re-invoke Workflow with `{scriptPath: "<path>"}` instead of resending the full script.

Every script must begin with `export const meta = {...}`:
  export const meta = {
    name: 'find-flaky-tests',
    description: 'Find flaky tests and propose fixes',   // one-line, shown in permission dialog
    phases: [                                            // one entry per phase() call
      { title: 'Scan', detail: 'grep test logs for retries' },
      { title: 'Fix', detail: 'one agent per flaky test' },
    ],
  }
  // script body starts here — use agent()/parallel()/pipeline()/phase()/log()
  phase('Scan')
  const flaky = await agent('grep CI logs for retry markers', {schema: FLAKY_SCHEMA})
  ...

The `meta` object must be a PURE LITERAL — no variables, function calls, spreads, or template interpolation. Required fields: `name`, `description`. Optional: `whenToUse` (shown in the workflow list), `phases`. Use the SAME phase titles in meta.phases as in phase() calls — titles are matched exactly; a phase() call with no matching meta entry just gets its own progress group. Add `model` to a phase entry when that phase uses a specific model override.

Script body hooks:
- agent(prompt: string, opts?: {label?: string, phase?: string, schema?: object, model?: string, effort?: string, isolation?: 'worktree', agentType?: string}): Promise<any> — spawn a subagent. Without schema, returns its final text as a string. With schema (a JSON Schema), the subagent is forced to call a StructuredOutput tool and agent() returns the validated object — no parsing needed. Returns null if the user skips the agent mid-run or the subagent dies on a terminal API error after retries (filter with .filter(Boolean)). opts.label overrides the display label. opts.phase explicitly assigns this agent to a progress group (use this inside pipeline()/parallel() stages to avoid races on the global phase() state — same phase string → same group box). opts.model overrides the model for this agent call. Default to omitting it — the agent inherits the main-loop model (the resolved session model), which is almost always correct. Only set it when you're highly confident a different tier fits the task; when unsure, omit. opts.effort overrides the reasoning effort for this agent call ('low' | 'medium' | 'high' | 'xhigh' | 'max') — omit to inherit the session effort; use 'low' for cheap mechanical stages and higher tiers only for the hardest verify/judge stages. opts.isolation: 'worktree' runs the agent in a fresh git worktree — EXPENSIVE (~200-500ms setup + disk per agent), use ONLY when agents mutate files in parallel and would otherwise conflict; the worktree is auto-removed if unchanged. opts.agentType uses a custom subagent type (e.g. 'general-purpose', 'code-reviewer') instead of the default workflow subagent — resolved from the same registry as the Agent tool; composes with schema (the custom agent's system prompt gets a StructuredOutput instruction appended).
- pipeline(items, stage1, stage2, ...): Promise<any[]> — run each item through all stages independently, NO barrier between stages. Item A can be in stage 3 while item B is still in stage 1. This is the DEFAULT for multi-stage work. Wall-clock = slowest single-item chain, not sum-of-slowest-per-stage. Every stage callback receives (prevResult, originalItem, index) — use originalItem/index in later stages to label work without threading context through stage 1's return value. A stage that throws drops that item to `null` and skips its remaining stages.
- parallel(thunks: Array<() => Promise<any>>): Promise<any[]> — run tasks concurrently. This is a BARRIER: awaits all thunks before returning. A thunk that throws (or whose agent errors) resolves to `null` in the result array — the call itself never rejects, so `.filter(Boolean)` before using the results. Use ONLY when you genuinely need all results together.
- log(message: string): void — emit a progress message to the user (shown as a narrator line above the progress tree)
- phase(title: string): void — start a new phase; subsequent agent() calls are grouped under this title in the progress display
- args: any — the value passed as Workflow's `args` input, verbatim (undefined if not provided). Pass arrays/objects as actual JSON values in the tool call, NOT as a JSON-encoded string — `args: ["a.ts", "b.ts"]`, not `args: "[\"a.ts\", ...]"` (a stringified list reaches the script as one string, so `args.filter`/`args.map` throw). Use this to parameterize named workflows — e.g. pass a research question, target path, or config object directly instead of via a side-channel file.
- budget: {total: number|null, spent(): number, remaining(): number} — the turn's token target from the user's "+500k"-style directive. `budget.total` is null if no target was set. `budget.spent()` returns output tokens spent this turn across the main loop and all workflows — the pool is shared, not per-workflow. `budget.remaining()` returns `max(0, total - spent())`, or `Infinity` if no target. The target is a HARD ceiling, not advisory: once `spent()` reaches `total`, further `agent()` calls throw. Use for dynamic loops: `while (budget.total && budget.remaining() > 50_000) { ... }`, or static scaling: `const FLEET = budget.total ? Math.floor(budget.total / 100_000) : 5`.
- workflow(nameOrRef: string | {scriptPath: string}, args?: any): Promise<any> — run another workflow inline as a sub-step and return whatever it returns. Pass a name to invoke a saved workflow (same registry as {name: "..."}), or {scriptPath} to run a script file you Wrote earlier. The child shares this run's concurrency cap, agent counter, abort signal, and token budget — its agents appear under a "▸ name" group in /workflows and its tokens count toward budget.spent(). The args param becomes the child's `args` global. Nesting is one level only: workflow() inside a child throws. Throws on unknown name / unreadable scriptPath / child syntax error; catch to handle gracefully.

Subagents are told their final text IS the return value (not a human-facing message), so they return raw data. For structured output, use the schema option — validation happens at the tool-call layer so the model retries on mismatch.
Schemas need {type: 'object', properties: {...}} at root and required ⊆ properties; unsatisfiable ones throw at agent().

Workflow agents can reach all session-connected MCP tools via ToolSearch — schemas load on demand per agent. Caveat: interactively-authenticated MCP servers (e.g. claude.ai) may be absent in headless/cron runs.

Subagents get the same CLAUDE.md files injected at start that you did (except built-in agent types that omit them, such as Explore and Plan) — don't tell them to re-read those or paste their rules into the prompt; name the specific rule a stage needs, if any.

Scripts are plain JavaScript, NOT TypeScript — type annotations (`: string[]`), interfaces, and generics fail to parse. The script body runs in an async context — use await directly. Standard JS built-ins (JSON, Math, Array, etc.) are available — EXCEPT `Date.now()`/`Math.random()`/argless `new Date()`, which throw (they would break resume); pass timestamps in via `args`, stamp results after the workflow returns, and for randomness vary the agent prompt/label by index. No filesystem or Node.js API access.

DEFAULT TO pipeline(). Only reach for a barrier (parallel between stages) when you genuinely need ALL prior-stage results together.

A barrier is correct ONLY when stage N needs cross-item context from all of stage N-1:
- Dedup/merge across the full result set before expensive downstream work
- Early-exit if the total count is zero ("0 bugs found → skip verification entirely")
- Stage N's prompt references "the other findings" for comparison

A barrier is NOT justified by:
- "I need to flatten/map/filter first" — do it inside a pipeline stage: pipeline(items, stageA, r => transform([r]).flat(), stageB)
- "The stages are conceptually separate" — that's what pipeline() models. Separate stages ≠ synchronized stages.
- "It's cleaner code" — barrier latency is real. If 5 finders run and the slowest takes 3× the fastest, a barrier wastes 2/3 of the fast finders' idle time.

Smell test: if you wrote
  const a = await parallel(...)
  const b = transform(a)        // flatten, map, filter — no cross-item dependency
  const c = await parallel(b.map(...))
that middle transform doesn't need the barrier. Rewrite as a pipeline with the transform inside a stage. When in doubt: pipeline.

Concurrent agent() calls are capped at min(16, available CPUs - 2) per workflow — excess calls queue and run as slots free up. You can still pass 100 items to parallel()/pipeline() and they all complete; only ~10 run at any moment. Total agent count across a workflow's lifetime is capped at 1000 — a runaway-loop backstop set far above any real workflow. A single parallel()/pipeline() call accepts at most 4096 items; passing more is an explicit error, not a silent truncation.

When a barrier IS correct — dedup across all findings before expensive verification:
  const all = await parallel(DIMENSIONS.map(d => () => agent(d.prompt, {schema: FINDINGS_SCHEMA})))
  const deduped = dedupeByFileAndLine(all.filter(Boolean).flatMap(r => r.findings))  // <-- genuinely needs ALL at once
  const verified = await parallel(deduped.map(f => () => agent(verifyPrompt(f), {schema: VERDICT_SCHEMA})))

Loop-until-count pattern — accumulate to a target:
  const bugs = []
  while (bugs.length < 10) {
    const result = await agent("Find bugs in this codebase.", {schema: BUGS_SCHEMA})
    bugs.push(...result.bugs)
    log(`${bugs.length}/10 found`)
  }

Loop-until-budget pattern — scale depth to the user's "+500k" directive. Guard on budget.total: with no target set, remaining() is Infinity and the loop would run straight to the 1000-agent cap.
  const bugs = []
  while (budget.total && budget.remaining() > 50_000) {
    const result = await agent("Find bugs in this codebase.", {schema: BUGS_SCHEMA})
    bugs.push(...result.bugs)
    log(`${bugs.length} found, ${Math.round(budget.remaining()/1000)}k remaining`)
  }

Composing patterns — exhaustive review (find → dedup vs seen → diverse-lens panel → loop-until-dry):
  const seen = new Set(), confirmed = []
  let dry = 0
  while (dry < 2) {                                              // loop-until-dry
    const found = (await parallel(FINDERS.map(f => () =>          // barrier: collect all finders this round
      agent(f.prompt, {phase: 'Find', schema: BUGS})))).filter(Boolean).flatMap(r => r.bugs)
    const fresh = found.filter(b => !seen.has(key(b)))           // dedup vs ALL seen — plain code, not an agent
    if (!fresh.length) { dry++; continue }
    dry = 0; fresh.forEach(b => seen.add(key(b)))
    const judged = await parallel(fresh.map(b => () =>           // every fresh bug judged concurrently...
      parallel(['correctness','security','repro'].map(lens => () =>   // ...each by 3 distinct lenses
        agent(`Judge "${b.desc}" via the ${lens} lens — real?`, {phase: 'Verify', schema: VERDICT})))
        .then(vs => ({ b, real: vs.filter(Boolean).filter(v => v.real).length >= 2 }))))
    confirmed.push(...judged.filter(v => v.real).map(v => v.b))
  }
  return confirmed
  // dedup vs `seen`, NOT `confirmed` — else judge-rejected findings reappear every round and it never converges.

Quality patterns — common shapes; pick by task and compose freely:
- Adversarial verify: spawn N independent skeptics per finding, each prompted to REFUTE. Kill if ≥majority refute. Prevents plausible-but-wrong findings from surviving.
    const votes = await parallel(Array.from({length: 3}, () => () =>
      agent(`Try to refute: ${claim}. Default to refuted=true if uncertain.`, {schema: VERDICT})))
    const survives = votes.filter(Boolean).filter(v => !v.refuted).length >= 2
- Perspective-diverse verify: when a finding can fail in more than one way, give each verifier a distinct lens (correctness, security, perf, does-it-reproduce) instead of N identical refuters — diversity catches failure modes redundancy can't.
- Judge panel: generate N independent attempts from different angles (e.g. MVP-first, risk-first, user-first), score with parallel judges, synthesize from the winner while grafting the best ideas from runners-up. Beats one-attempt-iterated when the solution space is wide.
- Loop-until-dry: for unknown-size discovery (bugs, issues, edge cases), keep spawning finders until K consecutive rounds return nothing new. Simple counters (while count < N) miss the tail.
- Multi-modal sweep: parallel agents each searching a different way (by-container, by-content, by-entity, by-time). Each is blind to what the others surface; useful when one search angle won't find everything.
- Completeness critic: a final agent that asks "what's missing — modality not run, claim unverified, source unread?" What it finds becomes the next round of work.
- No silent caps: if a workflow bounds coverage (top-N, no-retry, sampling), `log()` what was dropped — silent truncation reads as "covered everything" when it didn't.

Scale to what the user asked for. "find any bugs" → a few finders, single-vote verify. "thoroughly audit this" or "be comprehensive" → larger finder pool, 3–5 vote adversarial pass, synthesis stage. When unsure, lean toward thoroughness for research/review/audit requests and toward brevity for quick checks.

These patterns aren't exhaustive — compose novel harnesses when the task calls for it (tournament brackets, self-repair loops, staged escalation, whatever fits).

Use this tool for multi-step orchestration where control flow should be deterministic (loops, conditionals, fan-out) rather than model-driven.

## Resume

The tool result includes a runId. To resume after a pause, kill, or script edit, relaunch with Workflow({scriptPath, resumeFromRunId}) — the longest unchanged prefix of agent() calls returns cached results instantly; the first edited/new call and everything after it runs live. Same script + same args → 100% cache hit. Before diagnosing why a completed workflow returned an empty or unexpected result, Read <transcriptDir>/journal.jsonl — it records each agent's actual return value; do not assume cached results are non-empty. Date.now()/Math.random()/new Date() are unavailable in scripts (they would break this) — stamp results after the workflow returns, or pass timestamps via args. Fallback when no journal is available: Read agent-<id>.jsonl files in the transcript directory and hand-author a continuation script.

---

**Claude:**

Прошло 6 дней, статусы протухли. Сверяю живое: кто уже работает по подачам, что с дедлайнами, нагрузка узла.

---

> `Bash` -- {"command": "cd ~ && python ~/.claude/scripts/onair.py list 2>/dev/null | grep -i -E \"fellow|apply|подач|mats|dr\" | head; echo ===DR; grep -n -i -E \"fellow|фелош|максимиз|отбор|astra|mats\" \"D:/Vault/Vault-Knowledge/_DR-Registry.md\" | grep -E \"DR26-10-(1[8-9]|2[0-4])\" | cut -c1-300; echo =

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && sed -n 798p _DR-Registry.md | cut -c1-2500; echo; echo ===INSIGHT; ls 03-Insights | grep -E \"DR26-10-18-HUB-(06|10|11)\"; echo ===TASK1018; sed -n 1,80p 10-Tasks/task-2026-10-18-ai-safety-fellowship-applications.md", "description": "Read DR 1034 st

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/10-Tasks\" && for f in task-2026-10-07-aisb-coderbyte-assessment.md task-2026-09-30-iliad-captcha-submit.md task-2026-10-22-mats-residency-apply.md task-2026-10-22-pivotal-apply.md task-2026-10-22-generator-residency-apply.md task-2026-10-22-affine-prep.

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && python -c \"\nimport sqlite3\nc=sqlite3.connect('jobs.db')\nprint(c.execute(\\\"select status,count(*) from ats_jobs where company in ('METR','Apollo Research','FAR AI') group by status\\\").fetchall())\nprint(c.execute(\\\"select ats,count(*) f

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && sed -n 1,140p \"03-Insights/insight-DR-DR26-10-18-HUB-11-1034-стипендии-по-безопасности-ии-и-найм-шансы-отбора-c.md\"", "description": "Read DR 1034 insight on selection chances"}

---

> `Bash` -- {"command": "cd \"D:/Vault/_imports/jobs-watch\" && grep -l \"канон-ответ\" *.py | head; echo ===; grep -rn \"канон-ответ\" --include=*.py . | grep -v _test | head -5; echo ===STORE; ls | grep -i -E \"answer|canon|qa|bank\" ; find . -maxdepth 2 -iname \"*answer*\" | head", "description": "Locate 

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/04-Projects/Pipe-A-Batches\" && ls alt-programs-2026-10-22/ alt-programs-2026-10-22/seeds 2>/dev/null; echo ===; ls -t | head -5; echo ===dev-HOUR; grep -ril \"write-yourself\\|своими руками\\|диктовк\" alt-programs-2026-10-22/*.md 2>/dev/null | head",

---

> `Bash` -- {"command": "ls ~/.claude/scripts | grep -i -E \"gmail|mail_send|smtp\" ; ls \"D:/Vault/_imports\" | grep -i -E \"gmail|mail\" | head; python ~/.claude/scripts/rail_plan.py declare --self \"координация, RECALL, сверка фактов, финальные тексты и доклад оператору\" --outsource \"web:gemini,second_opin

---

> `ToolSearch` -- {"query": "select:mcp__s_8e110270__list_drafts,mcp__s_8e110270__get_draft,mcp__s_8e110270__get_thread,mcp__s_8e110270__reply,mcp__s_8e110270__send_message", "max_results"
