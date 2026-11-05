---
session: s_cb9ab513
date: 2026-10-06
words: 2337
turns: 5
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · В папке D:\Vault\_imports падает тест `_test_dr_fact_lint.py` (exit 1). Он проверяет модул…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_cb9ab513` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

В папке D:\Vault\_imports падает тест `_test_dr_fact_lint.py` (exit 1). Он проверяет модуль `dr_fact_lint.py` — прибор, который ловит СФАБРИКОВАННЫЕ конкретные ссылки в синтез-нотах дипресёрчей.

Прогон: `cd D:/Vault/_imports && PYTHONUTF8=1 python _test_dr_fact_lint.py`

Падает ровно один кейс, остальные 10 групп зелёные:
```
FAILS (1): no ✅ for the fabricated ref
```

Контекст, почему это важно, а не косметика: реестр рельс `~/.claude/dr_rails.json` фиксирует замером 05.10.2026, что рельса **mistral источники ФАБРИКУЕТ** (проверенные ссылки community.n8n.io/t/.../12345 и news.ycombinator.com/item?id=38000000 не существуют), а **glm работает без веба вообще**. Память [[dr-rails-fabricate-sources]]: из 5 рельс ссылкам можно верить у ОДНОЙ (grok), кворум этого не ловит. `dr_fact_lint.py` — единственная дверь, которая должна ловить такие ссылки до того, как они уедут в волт и в публичные посты. Пока его собственный тест красный, доверять его вердиктам нельзя (§5.4 «индикатор — тоже claim»).

Что НЕ является причиной: это падение НЕ связано с правкой `dr_synthesize.py` от 06.10 (там лечение статусов реестра в обе стороны, бэкап `dr_synthesize.py.bak-notestatusheal-20261006`, тест `_test_dr_synth_note_exists_flips_status.py` зелёный 3/3). `_test_dr_fact_lint.py` не импортирует `dr_synthesize` вовсе.

Задача:
1. Прочитать `dr_fact_lint.py` и выяснить, что именно ждёт упавший кейс и почему вердикт расходится. Проверить гипотезу «кейсу нужна сеть / внешний запрос» — если так, тест обязан это объявлять (§5.5: прибор не имеет права быть слепым, строка «не могу судить N из M, причина»), а не падать молча.
2. Починить корень, а не кейс. Если врёт тест — править тест; если врёт прибор — править прибор. Решить, кто из двух прав, ДО правки.
3. Доказать красным: тест обязан краснеть на сломанном коде (§5.4 [[red-first-or-the-test-is-fake]]).
4. Прогнать соседей: `_test_dr_fold.py`, `_test_dr_gate.py`, `_test_dr_file_dedup.py`, `_test_dr_quality.py`, `_test_dr_durable.py`, `_test_dr_collect_closed_debt.py` — на 06.10 все шесть зелёные, они обязаны остаться зелёными.
5. После починки прогнать `dr_fact_lint.py --dir` по 03-Insights и доложить, сколько нот несут неподтверждённые конкретные ссылки — особенно ноты, где в frontmatter `source` содержит mistral или glm.

Наружу ничего не публиковать. Правки кода коммитить самому с трейлерами Assisted-by / Machine / Account / Operator (§5.11).

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && ls -la _test_dr_fact_lint.py dr_fact_lint.py 2>&1 | head -20; echo \"---\"; wc -l _test_dr_fact_lint.py dr_fact_lint.py", "description": "List the lint module and its test"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python _test_dr_fact_lint.py 2>&1 | tail -40", "description": "Run the failing test"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python _test_dr_fact_lint.py 2>&1 | head -25", "description": "Head of test output"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && cat -n _test_dr_fact_lint.py", "description": "Read the test file"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && cat -n dr_fact_lint.py", "description": "Read dr_fact_lint.py"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git log --oneline -8 -- dr_fact_lint.py _test_dr_fact_lint.py 2>&1 | head; echo \"--- status\"; git status --porcelain dr_fact_lint.py _test_dr_fact_lint.py 2>&1 | head", "description": "Git history for the two files"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python dr_fact_lint.py --selftest; echo \"rc=$?\"", "description": "Run the built-in selftest"}

---

**Claude:**

Причина ясна. Прежде чем править — зафиксирую вердикт, кто врёт.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && cp dr_fact_lint.py dr_fact_lint.py.bak-tallylegend-20261006 && cp _test_dr_fact_lint.py _test_dr_fact_lint.py.bak-tallylegend-20261006 && ls -la *.bak-tallylegend-20261006", "description": "Backup both files before editing"}

---

> `Bash` -- {"command": "mkdir -p \"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad/mut\" && cd /e/Obsidian/_imports && python - <<'EOF'\n# mutant M1: judge ALWAYS says plausible (the classic green-lying i

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && SCR=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad/mut\" && PYTHONUTF8=1 python _test_dr_fact_lint.py \"$SCR/mut_always_ok.py\" 2>&1 | grep -E \"FAIL|

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python - <<'EOF'\nimport os\nsrc = open('dr_fact_lint.py', encoding='utf-8').read()\nout = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_cb9ab513\\scratchpad\\m

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && SCR=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad/mut\" && echo \"=== M2 (no symbol on rows) vs CURRENT test ===\" && PYTHONUTF8=1 python _test_dr_fa

---

**Claude:**

Вердикт доказан уликами. Теперь правка.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python - <<'PYEOF'\nimport io, re\np = '_test_dr_fact_lint.py'\ns = open(p, encoding='utf-8').read()\norig = s\n\n# --- 1) docstring: name the defect class so it does not come back -------------\ns = s.replace(\n'''RED-first contract (CLAUDE.md §5.4): the same

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && grep -n \"TALLY_RE = \" _test_dr_fact_lint.py && PYTHONUTF8=1 python -W error::SyntaxWarning -c \"import ast;ast.parse(open('_test_dr_fact_lint.py',encoding='utf-8').read())\" && echo \"syntax clean\" && PYTHONUTF8=1 python _test_dr_fact_lint.py 2>&1 | tail -6

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python - <<'PYEOF'\np = 'dr_fact_lint.py'\ns = open(p, encoding='utf-8').read()\no = s\n\n# 1) docstring: the legend trap + bump date\ns = s.replace(\n'''  --annotate: в конец заметки дописывается секция''',\n'''  Последняя строка «Итог: N ссылок · ✅ a · ⚠️ b 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && sed -n '433,442p' dr_fact_lint.py | cat -A | sed -n '1,10p' | cut -c1-120", "description": "Inspect the broken line"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python - <<'PYEOF'\np = 'dr_fact_lint.py'\ns = open(p, encoding='utf-8').read()\nbad = '        rows = \"\\n\".join(verdict_rows(out))'\ngood = '        rows = (\"%s\" %% chr(10)).join(verdict_rows(out))'  # placeholder, replaced below\nassert bad in s\ns = s.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python -c \"\np='dr_fact_lint.py'\ns=open(p,encoding='utf-8').read()\nnl='\\\"'+chr(92)+'n\\\"'\ns=s.replace('chr(10).join(verdict_rows(out))', nl+'.join(verdict_rows(out))')\nopen(p,'w',encoding='utf-8').write(s)\n\" && sed -n '437p' dr_fact_lint.py && PYTHON

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && ls red_proof.py 2>/dev/null && PYTHONUTF8=1 python red_proof.py --help 2>&1 | head -30", "description": "Check red_proof.py interface"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/red_proof.py /c/Users/dev/.claude/scripts/_shared/red_proof.py 2>/dev/null; echo \"---\"; PYTHONUTF8=1 python /c/Users/dev/.claude/scripts/red_proof.py --help 2>&1 | head -40", "description": "Locate red_proof.py in the skills scripts dir"}

---

> `Bash` -- {"command": "SCR=\"/c/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad/mut\"\ncd /e/Obsidian/_imports && python - <<PYEOF\nimport os\nd = r\"$SCR\"\npairs = {\n # M1 judge always green\n \"m1_old\"

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && python - <<'PYEOF'\nimport os\nd = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_cb9ab513\\scratchpad\\mut\"\nos.makedirs(d, exist_ok=True)\npairs = {\n \"m1_ol

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && M=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad/mut\"\nfor n in m1 m2 m3 m4; do\necho \"================ MUTANT $n\"\nPYTHONUTF8=1 python /c/Users/An

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && M=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad/mut\"\npython - <<'PYEOF'\nimport os, shutil, subprocess, sys, tempfile\nM = r\"C:\\Users\\dev\\App

---

**Claude:**

Красное доказано на 4 разных сломах. Теперь соседи.

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && for t in _test_dr_fold.py _test_dr_gate.py _test_dr_file_dedup.py _test_dr_quality.py _test_dr_durable.py _test_dr_collect_closed_debt.py; do printf \"%-38s \" \"$t\"; PYTHONUTF8=1 python \"$t\" >/tmp/o 2>&1; rc=$?; echo \"rc=$rc  $(tail -1 /tmp/o | cut -c1-70

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && grep -rln \"dr_fact_lint\" --include=*.py --include=*.md . 2>/dev/null | head -10; echo \"--- gh:\"; gh auth status 2>&1 | head -6", "description": "Find consumers and check gh auth"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && timeout 60 grep -ln \"dr_fact_lint\" *.py *.md 2>/dev/null | head; echo \"--- skills:\"; timeout 60 grep -rln \"dr_fact_lint\" /c/Users/dev/.claude/skills 2>/dev/null | head", "description": "Scoped consumer search"}

---

> `Bash` -- {"command": "timeout 60 gh auth status 2>&1 | head -8; echo \"rc=$?\"", "description": "Check gh auth status"}

---

> `Bash` -- {"command": "timeout 90 grep -rliE \"fact.?lint|факт.?линт\" /c/Users/dev/.claude/skills 2>/dev/null | head; echo \"---insights:\"; ls /e/Obsidian/Vault-Knowledge/03-Insights/insight-DR-*.md 2>/dev/null | wc -l; ls /e/Obsidian/Vault-Knowledge/03-Insights/*.md 2>/dev/null | wc -l", "description": "

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python - <<'PYEOF'\nimport glob, importlib.util, os, collections\nspec = importlib.util.spec_from_file_location(\"m\", \"dr_fact_lint.py\")\nm = importlib.util.module_from_spec(spec); spec.loader.exec_module(m)\nfiles = sorted(glob.glob(r\"E:\\Obs

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad\" && PYTHONUTF8=1 python dr_fact_lint.py --dir \"D:/Vault/Vault-Knowledge/03-Insights\" --cache \

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_cb9ab513/scratchpad\" && cd /e/Obsidian/_imports && PYTHONUTF8=1 python - <<PYEOF\nimport re, os, collections\ntxt = open(r\"$SC/sweep.txt\", encod

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/03-Insights && PYTHONUTF8=1 python - <<'PYEOF'\nimport glob, re, collections\nfiles = sorted(glob.glob(\"insight-DR-*.md\"))\nsrcs = collections.Counter(); vend = collections.Counter(); vend_files = collections.defaultdict(list)\nfor p in files:\n    t = o

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/03-Insights && timeout 60 grep -n \"browser-use#5048\\|puppeteer#4860\\|claude-code#76727\" insight-DR-DR26-08-14-MACANTON-01-2117-browser-and-screen-rails.md insight-DR-DR26-09-22-HUB-02-1159-*.md 2>/dev/null | cut -c1-320 | head -8", "description": "Insp

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/03-Insights && for pat in \"cookbooks#677\" \"smolagents#2656\" \"browser-use#5048\" \"pyautogui#589\" \"openai-cookbook#2772\"; do echo \"### $pat\"; timeout 40 grep -ho \".\\{0,170\\}$pat.\\{0,110\\}\" insight-DR-*.md 2>/dev/null | head -2; echo; done", 

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/03-Insights && PYTHONUTF8=1 python - <<'PYEOF'\nimport re\nbad = [\"insight-DR-DR26-07-16-MACANTON-01-1533-anthropic-oss-contribution-map-после-pr-784-где-и-.md\",\n\"insight-DR-DR26-07-16-MACANTON-01-1533-anthropic-oss-contribution-map.md\",\n\"insight-DR

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/03-Insights && for pat in \"issues/5048\" \"issues/589\" \"pull/2772\" \"pull/677\" \"issues/2656\"; do echo \"### $pat\"; timeout 40 grep -ho \".\\{0,150\\}$pat.\\{0,130\\}\" insight-DR-*.md 2>/dev/null | head -2; echo; done", "description": "Pull the URL

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python - <<'PYEOF'\nimport glob, importlib.util, json, re, os\nspec = importlib.util.spec_from_file_location(\"m\", \"dr_fact_lint.py\")\nm = importlib.util.module_from_spec(spec); spec.loader.exec_module(m)\ncache = json.load(open(r\"C:\\Users\\dev

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git log -3 --format='%h %an <%ae>%n%B' | head -30; echo \"=== branch/root:\"; git rev-parse --abbrev-ref HEAD; git rev-parse --show-toplevel; hostname", "description": "Check commit trailer convention in the vault repo"}

---

> `Bash` -- {"command": "ls /c/Users/dev/.claude/scripts/code_provenance_lint.py 2>/dev/null && timeout 60 PYTHONUTF8=1 python /c/Users/dev/.claude/scripts/code_provenance_lint.py --help 2>&1 | head -25", "description": "Check the provenance lint door requirements"}

---

> `Bash` -- {"command": "PYTHONUTF8=1 timeout 60 python /c/Users/dev/.claude/scripts/code_provenance_lint.py --help 2>&1 | head -28", "description": "Provenance lint help"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git ls-files | grep -c \"\\.bak-\" ; echo \"--- tracked example:\"; git ls-files | grep \"\\.bak-\" | tail -3; echo \"--- status:\"; git status --porcelain dr_fact_lint.py _test_dr_fact_lint.py dr_fact_lint.py.bak-tallylegend-20261006 _test_dr_fact_lint.py.bak

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git --no-pager diff --stat && git --no-pager diff dr_fact_lint.py | head -60", "description": "Review the instrument diff"}

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && git add -- dr_fact_lint.py _test_dr_fact_lint.py && git commit -q -F - <<'MSGEOF'\ndr_fact_lint: вердикт судим по СТРОКЕ ссылки, а не по всему выводу (4 фальшивые проверки)\n\nПадала одна проверка `_test_dr_fact_lint.py` -- «no ✅ for the fabricated ref». Сети 

---

> `Bash` -- {"command": "cd /e/Obsidian/_imports && PYTHONUTF8=1 python _test_dr_fact_lint.py 2>&1 | grep -c \"PASS\" ; PYTHONUTF8=1 python _test_dr_fact_lint.py >/dev/null 2>&1; echo \"test rc=$?\"; PYTHONUTF8=1 python dr_fact_lint.py --selftest >/dev/null 2>&1; echo \"selftest rc=$?\"", "description": "Final 

---

**Claude:**

**06.10.2026, 16:05 (Лиссабон)** · [dr_fact_lint.py](D:/Vault/_imports/dr_fact_lint.py) · коммит `891737c0`

## 1. Причина: врал ТЕСТ, прибор был прав

Гипотеза «кейсу нужна сеть» **опровергнута**: тест герметичен, `fetch_issue`/`gh_ready` замонкипатчены, gh не зовётся вообще.

Настоящая причина — последняя строка отчёта:

```
Итог: 1 ссылок · ✅ 0 · ⚠️ 1 · ❓ 0 · ⚪ 0
```

Это **легенда**: она печатает все четыре символа даже при нуле. А проверка искала символ подстрокой по всему stdout:

```python
check("no ✅ for the fabricated ref", "✅" not in out, out)   # ложно ВСЕГДА
```

Прибор при этом вёл себя безупречно: ссылка разрешилась через алиас, реальный заголовок показан, overlap 0.00, вердикт `⚠️ MISMATCH`, exit 2. Контракт прибора (докстринг, строки 18‑21) легенду не запрещает — менять отчёт под удобство подстроки было бы наоборот.

## 2. Один корень дал ЧЕТЫРЕ дефекта, красный был только один

Это и есть причина чинить корень, а не кейс. Доказано мутантами (копии в temp, боевой файл не тронут):

| улика | что было ДО правки |
|---|---|
| «no ✅ for the fabricated ref» | красная на **здоровом** приборе — шума много, информации ноль |
| «✅ verdict printed», «❓ printed», «⚪ unresolvable printed» | **зелёные** на мутанте M2, который вообще не печатает символы в строках ссылок |
| символьная половина `--selftest` | та же болезнь внутри самого прибора |
| лжущая строка «Итог» (M3) | **неотличима** от здорового прибора: та же одна FAIL с тем же именем |

Класс — `fake-check-is-worse-than-no-check`, пятый случай за 06.10.

**Лечение:** символы судим через `row_for(out, ref)` (строка конкретной ссылки) + `tally(out)` (разобранный счёт «Итог»). Пропавшая строка «Итог» теперь **валит** проверку (`tally() -> {}`), а не удовлетворяет её молча. Внутри прибора — `verdict_rows()`, и `--selftest` сверяет символ по строкам ссылок.

## 3. Красное доказано (`red_proof.py`, 4 разных слома)

```
M1  judge всегда ✅          -> 9 FAIL  (строка + счёт + rc + аннотация + --selftest)
M2  строки без символа       -> 6 FAIL  (ровно 4 символьные проверки + --selftest)
M3  «Итог» врёт зелёным      -> 3 FAIL  (ровно три проверки счёта; ДО правки — 0)
M4  строки «Итог» нет вовсе  -> 5 FAIL  (счёт не удовлетворяется пустотой)
```
Каждое утверждение называет то, что слом **меняет** — строку или число, не факт существования.

## 4. Соседи — все шесть зелёные

`_test_dr_fold` · `_test_dr_gate` · `_test_dr_file_dedup` · `_test_dr_quality` · `_test_dr_durable` · `_test_dr_collect_closed_debt` — `rc=0`. Свой тест 40/40, `--selftest` 3/3.

## 5. Живой прогон `--dir` по 03-Insights (gh авторизован, 38 запросов)

**492 ноты · 63 с конкретными ссылками · 212 ссылок · exit 2.**

**8 нот несут неподтверждённые конкретные ссылки** (35 ⚠️ MISMATCH + 5 ❓ not found).

⚠️ **Слепая зона прибора, которую обязан назвать (§5.5): 170 из 212 ссылок (80%) = ⚪ unresolvable — не судились вовсе.** Судить прибор смог только 42.

И вердикт «35 подмен сути» читать нельзя — я разложил его сам:
- **20 из 35** сидят на строках вида `Источники: [browser-use 5048](url), [PyAutoGUI 589](url), \`chatgpt B1\`` — содержательного утверждения рядом нет вовсе, overlap 0.00 **по построению**. Все 20 — в одной ноте `DR26-08-14-...-browser-and-screen-rails`.
- Ещё две находки — ложняки другого вида: нота `DR26-07-23-hf-hiring-lever` поймана на фразе, которая сама **документирует** выдумку («рекомендация P1 'smolagents #2656 = governance hooks' в 0742 — ВЫДУМКА»), а `claude-code#76727` — живой тред с верным содержанием, просто пересказанным, а не процитированным.
- **Прецедент, под который прибор строился, он ловит:** `DR26-08-25-...-0742` → `smolagents#2656` ⚠️ MISMATCH.

**Про mistral и glm — ответ отрицательный, но не тот, которого ждали:** поле `source` вендора не несёт ни у одной ноты (369 `claude-synthesis`, 89 без поля, 24 `deep-research`, 1 `codex-synthesis`). Вендоры живут в других полях frontmatter: **mistral в 43 нотах, glm в 60**. Пересечение с восемью флагнутыми: mistral и glm названы ровно в **одной** — и это именно `DR26-08-14-browser-and-screen-rails`, та самая с 20 из 35 ⚠️.

## Что я НЕ сделал и почему

Порог `overlap 0.25` и семантику вердиктов не трогал: докстринг сам называет порог эвристикой, а добавление состояния «рядом нет утверждения» снимает exit 2 с цитатных строк — то есть меняет громкость двери, которая стоит перед публичными постами. Это твоё решение, не моё. Готов сделать в тот же заход, если скажешь: предикат «строка-цитата» + отдельный символ + тесты, 15 минут.

Наружу ничего не ушло. Бэкапы: `dr_fact_lint.py.bak-tallylegend-20261006`, `_test_dr_fact_lint.py.bak-tallylegend-20261006`.

🧒 **Простыми словами:** тест ругался не потому, что прибор плохой, а потому, что смотрел не туда. Прибор в конце отчёта пишет табличку-подпись «галочек 0, тревог 1» — и тест, увидев там слово «галочка», решал, что прибор одобрил выдумку. Я заставил тест смотреть на саму строчку про ссылку и на цифры в подписи. Пока правил, выяснилось, что ещё три проверки годами говорили «всё хорошо», даже если прибор вообще молчал — их тоже починил. Потом проверил 492 заметки: 8 несут ссылки, которые не подтвердились, но у 20 из 35 тревог прибор просто не нашёл, что сверять — там был голый список ссылок без слов. Это я честно назвал, а не выдал за 35 выдумок.
