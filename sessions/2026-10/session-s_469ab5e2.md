---
session: s_469ab5e2
date: 2026-10-24
words: 4739
turns: 14
tools: "Bash, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-24 · У нас вроде похожая организация работы может бывать в чате 001

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_469ab5e2` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

У нас вроде похожая организация работы может бывать в чате 001


Давай спроектируем как нам построить что то подобные??


Цитата: Погуляли по берегу Темзы с техдиром Dwelly Димой Хануковым и он поделился отличным ИИ-сетапом: запускать две модели от ведущих лабораторий, OpenAI и Anthropic, в режиме конкуренции. 

Управлять всем этим через третьего агента-оркестратора (у Димы это Hermes). То есть оркестратор дает задачу Codex’у и проверяет через Claude Code, или наоборот, пока они не договорятся. 

У нейросетей от каждого производителя свои «слепые пятна», а так получается полное покрытие. Учитывая, что все это в родных харнесах по подписке — не слишком дорого. И как я сам не догадался?

Для финального код ревью Дима рекомендует qodo.

---

**Claude:**

Сначала RECALL: проверю, что у нас уже есть похожего, и классифицирую эту сессию (001 или нет).

---

> `Bash` -- {"command": "cd ~ && python \"C:\\Users\\dev\\.claude\\scripts\\voice001_collaboration.py\" describe --session-id s_469ab5e2 --wait-seconds 0 2>&1 | head -40", "description": "Classify session as 001 or not"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python brain_ask.py \"оркестратор Codex Claude Code конкуренция ревью цикл implementer reviewer qodo\" 2>&1 | head -60", "description": "RECALL vault for existing orchestration designs"}

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && ls docs/agent-protocol.md; sed -n 1,80p docs/agent-protocol.md; ls ~/.claude/skills/codex-review ~/.claude/skills/llm-pact 2>/dev/null; grep -ril \"qodo\" ~/.claude/projects/P---WORKDIR-HUB/memory 2>/dev/null | head; grep -rli \"hermes\"

---

> `Bash` -- {"command": "cd ~/.claude/projects/P---WORKDIR-HUB/memory && for f in codex-review-skill unified-coding-interface-impossible grok-second-reviewer-rail; do echo \"=== $f\"; sed -n 1,30p $f.md | cut -c1-400; done; echo \"=== qodo/hermes hits\"; grep -i -h \"qodo\\|hermes\" yc-batches-our-

---

> `Bash` -- {"command": "cd ~/.claude/projects/P---WORKDIR-HUB/memory && grep -h \"15.06.2026\" declined-decisions-archive.md | cut -c1-900 | head -2; ls ~/.claude/scripts | grep -i -E \"cc_review|codex_bridge|secondop|coding_outsource|aibus_lite|workspace_write\" | head; ls ~/.claude/scripts/cc-re

---

**Claude:**

План рельс: проектирую сам (синтез), чужим рельсам ничего не отдаю: исполнения пока нет. Сессия не опознана как 001 (`session_not_mapped`), поэтому обмен с напарником не запускаю.

## Что у нас уже есть (RECALL)

Две трети схемы Димы уже построены, нового строить почти не надо:

| Роль у Димы | У нас |
|---|---|
| Codex пишет, Claude проверяет и наоборот | `/codex-review` (`cc_review.py` Claude→Codex, `codex_review.py` обратно, двусторонне на хабе с 14.07) |
| Живой диалог двух моделей до согласия | `/llm-pact` + `codex_bridge.py`: реплики `PROPOSE→COUNTER→VERIFY→ACCEPT/BLOCK`, потолок 3 раунда, тупик уходит арбитру |
| Контракт «кто пишет, кто ревьюит» | `docs/agent-protocol.md`: implementer пишет `artifact.proposed`, ревьюер только читает, мерж только человек или интегратор |
| Защита от двух писателей | `workspace_write_lease.py`, `onair.py`, один worktree на пишущего |
| Третий глаз | `secondop.py` (Codex, Grok) и `/tt` |

Hermes мы уже рассматривали (22.06 и 05.08) и отклонили. Причина: Anthropic с 09.01 закрыла подписочный OAuth для сторонних агентов, а «единый» Hermes держится на поштучных API-ключах, то есть против §6.3. У Димы это не мешает, потому что обе модели идут в родных CLI.

## Чего не хватает

Не хватает **одного цикла-исполнителя**. Сейчас пару собирает человек или сессия вручную. Дима поставил над ними оркестратор, который гоняет цикл сам.

## Проект: `duel` (АК-47, около 200 строк)

Оркестратор — **не LLM**, а детерминированный скрипт (шаг 1 из §6.1 «дешёвый инструмент первым»). Он не думает, он гоняет конечный автомат:

```
задача + acceptance + зона файлов
        │
   [lease + worktree]            ← один писатель
        │
   WRITER (A) ──artifact.proposed──► REVIEWER (B)
     codex exec / claude -p            claude -p / codex exec
        ▲                                   │
        └────── REQUEST_CHANGES ◄───────────┤
                  (≤3 раунда)          APPROVE
                                            │
                                  FINAL: qodo + /tt
                                            │
                                  человек мержит
```

**Правила цикла:**
1. Писатель выбирается по классу задачи и остатку бака (`subscription_utilization.py`), ревьюер всегда другой вендор. Роли меняются между задачами, а не посреди одной.
2. Ревьюер получает diff, acceptance и задание опровергнуть критерии (это уже в `/codex-review`).
3. Потолок 3 раунда. Тупик → `BLOCK` → арбитр (третий вендор: Grok через `secondop`). Дальше человек.
4. Выход цикла: `APPROVE` от ревьюера, зелёные тесты, затем финальный проход через qodo, затем человек.
5. Каждый раунд пишет строку в JSONL: кто, вердикт, число замечаний, токены. По этому логу потом меряем, окупается ли дуэль.

**Где живёт:** скрипт `~/.claude/scripts/duel.py` и скилл `/duel`. Скилл должен проходить экзамен на всех вендорах (§9.3-кватер).

## Развилки, где нужна оговорка

- **Claude в роли писателя вне родного харнеса нельзя.** Значит `claude -p` вызывается только как родной CLI. Но в моих заметках от 22.06 стоит, что с 15.06 `claude -p` на подписке идёт через отдельный платный пул. Это надо проверить живым запросом до постройки, сейчас это непроверенный claim.
- **Qodo** у нас не встречался. Нужно проверить: есть ли у него CLI или GitHub-приложение, чем платим и работает ли он по подписке. Он годится как последний шаг только если его можно вызвать без поштучного API.
- **Польза не доказана.** Данные у нас есть только по ревью: гетеро-пара ловит больше (замер `tap`: 69.8% против 53.1%). Что полная дуэль «писатель + ревьюер» лучше обычного «писатель + `/codex-review`», мы не мерили.

## Предложение: сперва тень (§5.7)

1. **Проба, 1 день.** Живой `claude -p` (какой пул тратится), `codex exec` с `--skip-git-repo-check`, и поиск CLI у qodo.
2. **Тень, 2 недели.** `duel.py` крутится на 5-10 реальных задачах флота рядом с обычным путём, дата урожая пишется в `Shadow-First-Queue.md`. Метрики: баги, пойманные ревьюером, раунды до APPROVE, токены на задачу.
3. **Решение.** Если ловит заметно больше обычного ревью, включаем по умолчанию для кода, который идёт наружу (PR, флот). Если нет, оставляем `/codex-review`.

**Куда я бы целился:** не во «всё через дуэль», а в код с внешней дверью (PR в чужие репо, раскатка на флот). Там цена ошибки выше цены удвоенных токенов.

Начинаю с пробы (шаг 1) и вернусь с цифрами? Или ты хочешь сперва прогнать идею через напарника в чате 001?

🧒 **Простыми словами:** У нас уже есть два «повара» (Claude и Codex) и правило «один готовит, другой пробует». Дима добавил «шефа» — программу, которая сама гоняет блюдо туда-сюда, пока второй повар не скажет «вкусно». Шефа нам надо написать простым скриптом. Сначала проверим, не дорого ли это и правда ли так лучше, и только потом включим везде.

🏛H · Sonnet 5.5 · 97688

---

**User:**

Stop hook feedback:
СТОП: ты заявил ОТСУТСТВИЕ ('ничего не отдаю: исполнения пока нет'), а поиск этой сессии ещё НЕ ДОСЧИТАЛ:
  . фоновая задача ЕЩЁ БЕЖИТ: C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_469ab5e2\tasks\bxes187kf.output

Пока поиск не вернулся, законная формулировка ОДНА: «я не нашёл (поиск
не завершён)», а НЕ «этого нет» (CLAUDE.md §5.4, prichina-kak-claim).
Замер 14.09.2026: греп по волту убит на 120с -> объявлено «ретро не
линкует ни один MOC» и вписано в скилл /retro как ЗАМЕР; фоновый прогон
досчитался и вывод ОПРОВЕРГ.
Замер 06.10.2026: «RECALL чист, Булаева в волте нет» при бегущем грепе;
тот нашёл MOC его канала И наше решение 15.09 с обзором 15 планировщиков
-- то есть ВСЮ prior art. Вердикт выдан без половины фактов, переписан
дважды.

Что сделать: дочитай вывод фоновой задачи (Read по её .output --
завершённая дописывает «[exited with code N]»), либо перепиши ответ на
«я не нашёл», либо назови задачу не относящейся к поиску одной строкой.
Класс: vyvod-po-nezavershennomu-poisku (9 строк журнала с 01.09.2026,
порог §5.10 пройден втрое). НЕ путать с vyvod-po-odnoy-poverhnosti:
там место ответило, здесь ответа ещё НЕ БЫЛО.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_469ab5e2\\tasks\\bxes187kf.output"}

---

**Claude:**

Фоновая задача `brain_ask.py` (поиск по волту) так и не вернула вывод: файл пуст, код выхода не записан. Поэтому я исправляю формулировку.

**Исправление:** я не писал, что «в волте ничего нет», но в ответе стоило прямо сказать про этот поиск. Поиск по волту не завершён, и я не нашёл там ничего про оркестратор, дуэль Codex и Claude или Qodo. Это не значит, что там пусто. Мой список «что у нас уже есть» собран из других источников: `docs/agent-protocol.md`, скиллов `llm-pact` и `codex-review` и файлов памяти. Эти источники ответили полностью. Волт молчит, потому что поиск завис, а не потому что там пусто.

Фразу «исполнения пока нет» я имел в виду так: в этом ответе я ничего не отдавал чужим рельсам. Это про мои действия, не про содержимое волта.

Что нужно сделать до начала постройки: перезапустить `brain_ask.py` с коротким запросом и таймаутом побольше, а также сделать `grep` по волту на слова «Hermes», «qodo», «duel» и «оркестратор». Тогда вывод про «чего не хватает» опирается на полный поиск. Запускаю это как шаг 0 пробы, если ты согласен с планом.

🧒 **Простыми словами:** Я искал в большой библиотеке, но библиотекарь так и не вернулся с ответом. Другие полки я проверил целиком. Поэтому правильно говорить «в библиотеке я пока не нашёл», а не «там ничего нет». Библиотеку проверю ещё раз, прежде чем строить.

🏛H · Sonnet 5.5 · 97688

---

**User:**

<task-notification>
<task-id>bxes187kf</task-id>
<tool-use-id>toolu_017TFkeDppE8psMQN2QLfNFY</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_469ab5e2\tasks\bxes187kf.output</output-file>
<status>completed</status>
<summary>Background command "RECALL vault for existing orchestration designs" completed (exit code 0)</summary>
</task-notification>

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_469ab5e2\\tasks\\bxes187kf.output"}

---

> `Bash` -- {"command": "cd ~/.claude/projects/P---WORKDIR-HUB/memory && sed -n 1,25p agent-teams-scoped-adoption.md | cut -c1-500", "description": "Read agent-teams memory note"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\insight-DR-DR26-08-02-ZB-04-2324-multi-llm-coding-orchestration-claude-code-as-orch.md"}

---

**Claude:**

Поиск досчитался (exit 0), и он **меняет мой проект**. Покрытие у него неполное: 573 из 705 свежих сессий не прочитаны, поверхность скрыта секрет-гейтом. «Больше ничего нет» я из этого не утверждаю. Уже найденное достаточно, чтобы поправить то, что я сказал раньше.

## Что нашлось и что меняется

**1. Deep Research DR26-08-02-ZB-04-2324 уже разобрал эту архитектуру.** Это «Claude Code оркестрирует внешние CLI-агентов». Я в прошлом ответе писал «проверим, окупается ли», но у нас уже есть три вывода:

- **Дуэль, где оркестратор сам решает, кто лучше, не доказана.** Контролируемых исследований нет. Идея Димы идёт из практики, а не из измерений. Это сходится с моей оговоркой «польза не доказана».
- **Петля «пока не договорятся» вредна.** Мой потолок в 3 раунда оказался слишком щедрым. DR рекомендует такую политику: один целевой ремонт тем же исполнителем с уликой, затем один свежий заход другого вендора, затем Claude забирает задачу себе. Всего 2 попытки. Исследования ремонта по кругу спорят, а повторные попытки на неудачном коде якорятся на ошибке.
- **Мелкие задачи через делегирование убыточны.** У обёртки фиксированная цена около 5–7 тысяч токенов. Делегировать стоит ограниченные задачи на 30–120 минут человеческой работы. Безопасность, архитектура и миграции остаются у Claude.

**2. Оркестратор у нас уже решён в пользу детерминированной обёртки, а не третьего LLM.** DR разводит полномочия: Claude отвечает за замысел, критерии приёмки и финальное ревью. Обёртка-скрипт отвечает за worktree, процессы, границу секретов и git. Внешний CLI получает только изолированный diff и не может коммитить и пушить. Это совпадает с моим `duel.py`.

**3. Два предупреждения, которых в моём проекте не было:**
- **Код выхода 0 ничего не доказывает.** Antigravity может тихо отказать в действии и всё равно вернуть 0. Валидатор обязан сам перезапускать тесты и не верить словам исполнителя.
- **Worktree не защищает секреты.** Перед запуском исполнителя нужно вычистить из окружения ключи и токены и закрыть сеть.

**4. Решение о Teams (25.06) не мешает.** Agent Teams приняты узко, только для разовой разведки и ревью. Для дуэли они не подходят: цикл с кодом идёт через скрипт, а не через Teams.

## Исправленный проект

`duel.py` остаётся детерминированным скриптом, но с политикой ремонта из DR:

```
спека (шаблон-контракт, одинаков для обоих вендоров)
  → A пишет в worktree (без секретов, без сети, без права на git)
  → валидатор сам гоняет тесты, не верит A
  → B ревьюит
  → 1 целевой ремонт у A → 1 свежий заход у B → Claude забирает
  → FINAL: qodo + /tt → человек мержит
```

Пилот остаётся тем же, что DR сам и предложил: недельная тень с журналом и критерием переключения. Её дату урожая запишу в `Shadow-First-Queue.md`, когда решишь включать.

Qodo в волте и памяти не нашёлся, но покрытие поиска неполное. Проверю его отдельно и скажу, есть ли CLI и чем он оплачивается.

Начать с пробы: `claude -p` (какой пул тратится), `codex exec` и qodo?

🧒 **Простыми словами:** Оказалось, что мы это уже исследовали два месяца назад. Тогда выяснилось: хорошо, когда один пишет, а другой проверяет. А вот гонять их по кругу «пока не договорятся» не стоит. Лучше две попытки, а потом задачу забирает Claude. Ещё нельзя верить исполнителю на слово: тесты надо запускать самим. Из доказанного у нас пока только это, всё остальное проверим на недельной пробе.

🏛H · Sonnet 5.5 · 97688

---

**User:**

<local-command-caveat>The command below was run directly in Claude Code, not sent to you as a request, and its output goes straight to the user. It's recorded here as context for later messages.</local-command-caveat>

---

**User:**

<command-name>/model</command-name>
            <command-message>model</command-message>
            <command-args>claude-opus-5-5</command-args>

---

**User:**

<local-command-stdout>Set model to `claude-opus-5-5`</local-command-stdout>

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

Задача большая: пробы, сама постройка, тесты и тень. Сначала разведаю на месте, что уже лежит в `cc-review/`. Там есть `_test_implement.py`, то есть, возможно, исполнитель-делегат уже построен.

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review && ls -la | head -60; echo; sed -n 1,80p README-outsource.md | cut -c1-300", "description": "List cc-review dir and read outsource README"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review && L=bridge-state/outsource_ledger.jsonl; echo \"ledger rows: $(wc -l < $L 2>/dev/null)\"; tail -5 $L 2>/dev/null | cut -c1-300; echo \"--- impl states:\"; ls bridge-state | grep -c '^_impl-'; ls -t bridge-state | grep '^_impl-' | head -5; echo \"--- revie

---

> `Bash` -- {"command": "cd ~/.claude/scripts/cc-review && L=bridge-state/outsource_ledger.jsonl; echo \"ledger rows: $(wc -l < $L 2>/dev/null)\"; tail -5 $L 2>/dev/null | cut -c1-300; echo \"--- impl states: $(ls bridge-state | grep -c '^_impl-')\"; ls -t bridge-state | grep '^_impl-' | head -5; echo \"--- rev

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py same \"дуэль Codex Claude: авто-цикл implement review retry оркестратор\" ; echo \"rc=$?\"; cd cc-review && python outsource_digest.py --days 90; echo \"rc=$?\"", "description": "Check duplicate work and run outsource digest"}
