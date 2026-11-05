---
session: s_f3b5f39f
date: 2026-09-01
words: 2923
turns: 28
tools: "Bash, ToolSearch, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-01 · Scheduled run: auto-hub-260824-nsfw-dr-posts

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f3b5f39f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260824-nsfw-dr-posts" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260824-nsfw-dr-posts\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

ПЕРВЫМ ДЕЛОМ переименуй эту сессию: вызови mcp__ccd_session_mgmt__set_session_title с title "AUTO-hub-260901-fb-session-watchdog".

⛳ ВХОД: сессия починки КЛАССА fb-session-logged-out (≥4 датированных случая в 00-System\Breakage-Journal.md, класс системный по §5.10). FB-лейн хаба стоял 19.08–01.09, потому что смерть сессии замечали только полным браузерным заходом рутины раз в сутки. 25.08 в журнале назван дешёвый 0-LLM предчек — за 7 дней не построен. С 01.09 FB-рельса = FIREFOX (приказ оператора, Библия reglament-firefox-po-maksimumu-i-zamer §Поправка 01.09): живость сессии теперь читается С ДИСКА бесплатно (cookies.sqlite профиля 646yqiss.default-release, cookie c_user/xs).

📛 ON AIR: первым делом объяви себя — `python ~/.claude/scripts/onair.py check --zone arch-system`, чисто → `onair.py declare --zone arch-system --mode collab --title "fb-session-watchdog" --ttl-hours 3`; в конце `onair close`. Зона занята соседом — НЕ править параллельно: читай его табличку, договаривайся в 03 или бери другой кусок.
👤 КОНСОЛИДАТОР: если по этой теме поднято больше ОДНОГО исполнителя — консолидатор ЭТА сессия. Он сводит результаты и объявляет «готово»; остальные сдают ему кусок и НЕ пишут свой финальный вердикт. Исполнитель один — эта строка не действует.
🔁 RECALL ЛЕТЯЩЕЙ РАБОТЫ (до постройки, не после): `onair.py list` + свежие панели `~/.claude/scripts/cc-review/bridge-state/usage.jsonl` + `00-System/Breakage-Journal.md` (класс fb-session-logged-out уже разбирали — читай ВСЕ его строки). Сессия AUTO-hub-260901-fb-backfill-firefox сегодня же переводит рутину fb-reply-daily на Firefox — её артефакты ПЕРЕИСПОЛЬЗУЙ, не дублируй. Задача task-2026-08-10-browser-rail-down-forever-fix (P0, open) — смежный класс, сверься и перелинкуй.
🪫 БАК И СМЕРТЬ ПРИ РОЖДЕНИИ: пачку fireAt-сидов разноси с учётом бака подписки. Умер об лимит при рождении — это обязано быть ЗАМЕЧЕНО: следующая сессия и `/retro` проверяют «сид родил ретро?».
🔍 УЛИКА ПРИ СТАТУС-CLAIM: любое ✅ про ФАЙЛ, КОД или ЧУЖУЮ ПРОВЕРКУ — только с уликой в том же заходе (ls/cat/цитата/exit-код). Не читал — пиши 🤔. Пусто из одного места ≠ «нет» — назови, ГДЕ искал.
⏳ ПРЕМИССА — ПРОВЕРЯЕМАЯ: первым шагом замерь по ground truth, что предчека ДЕЙСТВИТЕЛЬНО нет (grep по ~/.claude/scripts на fb_session/fb_precheck/c_user) и что класс не закрыт соседом. Уже сделано → выйди рано с докладом «чем и когда закрыто».

OUTCOME (АК-47, 5 почему по серии уже сделано — корень «смерть сессии видна только дорогим заходом»):
1. `~/.claude/scripts/_shared/fb_session_check.py` — 0 LLM, 0 сети: читает c_user/xs из cookies.sqlite системного Firefox-профиля хаба (копия во временный файл против лока), exit 0 = жива / 1 = мертва; печатает возраст lastAccessed. Docstring по §5.8 (назначение·вход/выход·кто дёргает·рельса·updated). Тест `_test_fb_session_check.py`, тест обязан краснеть на фикстуре без c_user.
2. Врезать предчек ШАГОМ 0.5 в `C:\Users\dev\.claude\scheduled-tasks\fb-reply-daily\SKILL.md`: мертва → аск D в 02 через approval.py + СТОП без браузерного захода (экономия полного прогона).
3. Сторож по §5.5 (не живёт в том, что сторожит): строка в существующий суточный сторож/крон (например cron_watchdog или Housekeeping) — сессия мертва >6ч → алерт в 03 с ИМЕНЕМ больного и ЛЕЧЕНИЕМ («залогинься в Firefox хаба»). Нового 24/7-робота НЕ строить.
4. /tt на артефакт (сломать нарочно: подсунуть профиль без c_user). Строка «класс закрыт» в Breakage-Journal + вердикт 🌍 (/share-fix порог переносимости).
5. Отчёт в 03 через bus_send.py: что построено, exit-коды тестов, что врезано куда.
ГРАНИЦЫ: логины/куки НЕ трогать (только чтение); Tier-2 к оператору; рельса исполнителя = локальный код, LLM не жечь на детерминированное.
</scheduled-task>

---

**Claude:**

I'll start by renaming the session, then run the premise check before building anything.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && ls _shared/ | grep -i -E \"fb|face\" ; echo \"--- grep fb_session/precheck/c_user ---\"; grep -ril -E \"fb_session|fb_precheck|c_user\" ~/.claude/scripts/ 2>/dev/null | head -20; echo \"--- exit $? ---\"", "description": "Premise check: does an FB session prechec

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "AUTO-hub-260901-fb-session-watchdog"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n -E \"fb_session|fb_precheck|c_user\" git25-tools/session_backend_diff.py _test_session_wait_detect.py | head -10; echo \"=== onair ===\"; python ~/.claude/scripts/onair.py check --zone arch-system 2>&1 | head -20", "description": "Verify grep hits are fal

---

**Claude:**

Premise confirmed — the 3 grep hits are false positives (`sc_user_state_none`, `rec_user` matching the `c_user` substring). No FB precheck exists.

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py declare --zone arch-system --mode collab --title \"fb-session-watchdog\" --ttl-hours 3 2>&1 | tail -5; echo \"=== list ===\"; python ~/.claude/scripts/onair.py list 2>&1 | head -20", "description": "Declare ON AIR in arch-system zone"}

---

> `Bash` -- {"command": "grep -n -i \"fb-session-logged-out\\|fb.session\\|logged.out\" \"$OBSIDIAN_VAULT/00-System/Breakage-Journal.md\" 2>/dev/null | head -30; echo \"=== vault var ===\"; echo \"$OBSIDIAN_VAULT\"", "description": "Read all fb-session-logged-out lines in Breakage Journal"}

---

**Claude:**

Class confirmed: 4 dated cases, precheck named 25.08 still not built. Now RECALL of the sibling session's flying work so I reuse instead of duplicate.

---

> `Bash` -- {"command": "ls -la ~/.claude/scripts/_shared/ | grep -i -E \"firefox|cookie|fb\"; echo \"=== recent scripts changed today ===\"; find ~/.claude/scripts -name \"*.py\" -newermt \"2026-09-01\" 2>/dev/null | head -20; echo \"=== fb-reply-daily skill ===\"; ls -la ~/.claude/scheduled-tasks/fb-reply-dai

---

**Claude:**

`firefox_cookies.py` already exists — must read it before building (one source, zero copies).

---

> `Bash` -- {"command": "cat ~/.claude/scripts/_shared/firefox_cookies.py", "description": "Read existing firefox_cookies.py to reuse"}

---

**Claude:**

Reusing this engine instead of duplicating it. Checking consumers + current ground truth.

---

> `Bash` -- {"command": "grep -rn \"firefox_cookies\\|read_cookies\" ~/.claude/scripts/ \"$OBSIDIAN_VAULT/_imports\" 2>/dev/null --include=*.py --include=*.md | grep -v \"^.*firefox_cookies.py:\" | head -20", "description": "Find consumers of read_cookies"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && python firefox_cookies.py --profile 646yqiss.default-release --domain facebook.com --count 2>&1 | head -30", "description": "Ground truth: is FB session alive in Firefox profile right now"}

---

**Claude:**

FB session is **alive right now** in Firefox (`c_user` + `xs` present). Reading the consumer skill and picking the watchdog host.

---

> `Bash` -- {"command": "cat ~/.claude/scheduled-tasks/fb-reply-daily/SKILL.md", "description": "Read fb-reply-daily SKILL.md"}

---

**Claude:**

Engine + test first (collision-free). The sibling session owns `content-factory`; `SKILL.md` wiring I'll coordinate after.

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && python - <<'PY'\nimport re, pathlib\np = pathlib.Path(\"firefox_cookies.py\")\ns = p.read_text(encoding=\"utf-8\")\nold_sig = 'def read_cookies(profile: Path, domain: str | None = None) -> list[dict]:'\nnew_sig = 'def read_cookies(profile: Path, domain: s

---

**Claude:**

Now the checker itself.

---

> `Bash` -- {"command": "cat > ~/.claude/scripts/_shared/fb_session_check.py <<'PYEOF'\n#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"\nfb_session_check.py -- ДЕШЁВЫЙ ПРЕДЧЕК ЖИВОСТИ FB-СЕССИИ (0 LLM, 0 сети).\n\nНАЗНАЧЕНИЕ: за доли секунды сказать \"FB-сессия жива / мертва\", читая cookies.sqlite\nсис

---

**Claude:**

Works (exit 0). Fixing the escape warning — that's the known "backslash in non-raw string" class.

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && grep -n 'Breakage-Journal' fb_session_check.py | cat -A | head -3", "description": "Inspect the actual backslash bytes"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && python - <<'PY'\nimport pathlib\np = pathlib.Path(\"fb_session_check.py\")\ns = p.read_text(encoding=\"utf-8\")\ns = s.replace(\"00-System\\\\Breakage-Journal.md\", \"00-System/Breakage-Journal.md\", 1)\np.write_text(s, encoding=\"utf-8\")\nprint(\"ok\")\

---

**Claude:**

Clean now. Writing the test — it must go **red** on a fixture without `c_user`.

---

> `Bash` -- {"command": "cat > ~/.claude/scripts/_shared/_test_fb_session_check.py <<'PYEOF'\n#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"\n_test_fb_session_check.py -- регресс на предчек живости FB-сессии.\n\nСТОРОЖ ДОЛЖЕН КРАСНЕТЬ: главный кейс -- профиль-фикстура БЕЗ c_user обязана дать\n\"мертва\

---

**Claude:**

15/15 green. But a green test is itself a claim — proving it can go **red** by deliberately breaking the engine.

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared && cp fb_session_check.py /tmp/fb_ok.py && python - <<'PY'\nimport pathlib\np = pathlib.Path(\"fb_session_check.py\")\ns = p.read_text(encoding=\"utf-8\")\n# ломаем нарочно: требуем ТОЛЬКО xs (как будто c_user не важен) -- ровно та ошибка,\n# из-за которой р

---

**Claude:**

Guard genuinely goes red on the exact failure mode, restored green. Now the watchdog host (§5.5 — must not live in what it guards).

---

> `Bash` -- {"command": "ls ~/.claude/scripts/ | grep -i -E \"watchdog|housekeep\" ; echo \"=== cron_watchdog head ===\"; head -40 ~/.claude/scripts/cron_watchdog.py 2>/dev/null", "description": "Find existing daily watchdogs"}

---

> `Bash` -- {"command": "ls -la ~/.claude/scheduled-tasks/fb-reply-daily/SKILL.md; echo \"=== has step 0.5 already? ===\"; grep -n \"0\\.5\\|fb_session_check\\|Firefox\\|firefox\" ~/.claude/scheduled-tasks/fb-reply-daily/SKILL.md | head", "description": "Check if sibling already edited the skill"}

---

**Claude:**

`cron_watchdog.py` is the right host — independent scheduled task, 0 LLM, already hosts a non-cron check. Reading that pattern to mirror it.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"def check_agent_sos\" -A 45 cron_watchdog.py | head -60; echo \"=== where called ===\"; grep -n \"check_agent_sos\\|def main\\|reds\\.\\|reds =\" cron_watchdog.py | head -30", "description": "Read the agent-SOS extra-check pattern in cron_watchdog"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '436,520p' cron_watchdog.py", "description": "Read state + main of cron_watchdog"}

---

**Claude:**

Adding the watchdog check into `cron_watchdog.py` with its own small state (self-contained, injectable).

---

> `Bash` -- {"command": "cd ~/.claude/scripts && grep -n \"^ME_HOST\\|ME_HOST =\\|SOS_PREFIXES =\\|^HUB\\|HUB-01\" cron_watchdog.py | head", "description": "Find ME_HOST and hub constants"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport pathlib\np = pathlib.Path(\"cron_watchdog.py\")\ns = p.read_text(encoding=\"utf-8\")\n\nanchor = \"def load_state():\"\nassert anchor in s\n\nblock = '''# --- FB-сессия (класс fb-session-logged-out, 4 датированных случая) --------------\n#

---

**Claude:**

Runs clean, no FB red (correct — session alive). Fixing the escape warning again (heredoc collapses backslashes here).

---

> `Bash` -- {"command": "cd ~/.claude/scripts && sed -n '485,490p' cron_watchdog.py", "description": "Inspect the warning line"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport pathlib\np = pathlib.Path(\"cron_watchdog.py\")\ns = p.read_text(encoding=\"utf-8\")\nbad = '\"%%USERPROFILE%%\\\\.claude\\\\scripts\\\\_shared\\\\fb_session_check.py\"'\ngood = 'r\"%%USERPROFILE%%\\\\.claude\\\\scripts\\\\_shared\\\\fb_se

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport pathlib\nB = chr(92)\np = pathlib.Path(\"cron_watchdog.py\")\ns = p.read_text(encoding=\"utf-8\")\nbad = '\"%%USERPROFILE%%' + B + '.claude' + B + 'scripts' + B + '_shared' + B + 'fb_session_check.py\"'\ngood = '\"%%USERPROFILE%%/.claude/s

---

**Claude:**

Clean. `[]` is correct — first sighting of death doesn't alert. Now the regression test for the watchdog lane.

---

> `Bash` -- {"command": "cat > ~/.claude/scripts/_test_cron_watchdog_fb_session.py <<'PYEOF'\n#!/usr/bin/env python3\n# -*- coding: utf-8 -*-\n\"\"\"\n_test_cron_watchdog_fb_session.py -- регресс на FB-лейн внешнего крана-сторожа.\n\nСУДИМ ДЕЙСТВИЕ, НЕ ПОДСТРОКУ: проверяем, что check_fb_session РЕАЛЬНО молчит н

---

**Claude:**

Test caught a real bug: `dead_since = st.get(...) or now` treats a falsy `0` as missing, so the stamp never sticks. Fixing with an explicit `None` check.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python - <<'PY'\nimport pathlib\np = pathlib.Path(\"cron_watchdog.py\")\ns = p.read_text(encoding=\"utf-8\")\nbad = '    dead_since = st.get(\"dead_since\") or now'\ngood = ('    dead_since = st.get(\"dead_since\")\\n'\n        '    if dead_since is None:        

---

**Claude:**

12/12 green. Verifying I didn't break the existing watchdog regressions.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && for t in _test_cron_watchdog.py _test_cron_watchdog_absent.py; do echo \"--- $t ---\"; python $t 2>&1 | tail -4; echo \"exit=$?\"; done", "description": "Run pre-existing cron_watchdog tests for regressions"}

---

**Claude:**

Gate hit — but this is regression-proving a file I just edited, not a maintenance run. Forcing with reason stated.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && for t in _test_cron_watchdog.py _test_cron_watchdog_absent.py; do echo \"--- $t --- (--force: я ТОЛЬКО ЧТО правил cron_watchdog.py, обязан доказать что не сломал сторожа 20+ задач)\"; python $t --force 2>&1 | tail -5; echo \"exit=$?\"; done", "description": "Forc

---

**Claude:**

No regressions. Now wiring Step 0.5 into the routine — checking the sibling session's status first (it owns the FB→Firefox move).

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py list 2>&1 | head; echo \"=== skill mtime now ===\"; ls -la ~/.claude/scheduled-tasks/fb-reply-daily/SKILL.md", "description": "Re-check sibling ON AIR status and file mtime"}

---

**Claude:**

Sibling hasn't touched the file. Inserting Step 0.5 (additive). Checking `approval.py ask` signature first.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python approval.py ask --help 2>&1 | head -25", "description": "Read approval.py ask usage"}

---

> `Bash` -- {"command": "cd ~/.claude/scheduled-tasks/fb-reply-daily && cp SKILL.md SKILL.md.bak-pre-precheck-20260901 && python - <<'PY'\nimport pathlib\np = pathlib.Path(\"SKILL.md\")\ns = p.read_text(encoding=\"utf-8\")\nanchor = \"1. ПРЕДОХРАНИТЕЛЬ:\"\nassert anchor in s, \"anchor not found\"\n\nblock = '''

---

**Claude:**

Wired. Now the journal line closing the class, and the provenance commit.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python vault_backup.py 2>&1 | tail -3; echo \"backup exit=$?\"", "description": "Vault backup before write"}

---

> `Bash` -- {"command": "cd ~/.claude && git -C ~/.claude status --porcelain 2>/dev/null | head -20; echo \"=== branch ===\"; git -C ~/.claude branch --show-current 2>/dev/null", "description": "Check git state of ~/.claude"}

---

**Claude:**

Backup already ran today (gate confirms) — no need to force. Checking which repo owns `scripts/`.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && git rev-parse --show-toplevel 2>/dev/null; echo \"--- status ---\"; git status --porcelain 2>/dev/null | head -20", "description": "Find the repo owning scripts and its status"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && git add _shared/fb_session_check.py _shared/_test_fb_session_check.py _shared/firefox_cookies.py cron_watchdog.py _test_cron_watchdog_fb_session.py && git status --porcelain --cached | head", "description": "Stage my files"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && git diff --cached --name-only && git commit -q -F - <<'MSG'\nfb: дешёвый 0-LLM предчек живости FB-сессии + внешний сторож (класс fb-session-logged-out)\n\nКласс системный: 4 датированных случая (23.08, 25.08, 31.08, 01.09).\nКорень: смерть FB-сессии была видна ТО

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python code_provenance_lint.py 2>&1 | tail -8; echo \"lint exit=$?\"", "description": "Verify provenance lint passes"}

---

**Claude:**

Lint clean, 0 violations. Now the journal line closing the class.

---

> `Bash` -- {"command": "tail -5 \"$OBSIDIAN_VAULT/00-System/Breakage-Journal.md\" | cut -c1-300", "description": "Read journal tail to match format"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport os, io, pathlib\nv = os.environ.get(\"OBSIDIAN_VAULT\") or r\"D:\\Vault\\Vault-Knowledge\"\np = pathlib.Path(v) / \"00-System\" / \"Breakage-Journal.md\"\nline = (\n\"\\n- 2026-09-01 11:55-12:1x (хаб HUB-01, отдельная сессия починки класса `AUTO-hub-260

---

**Claude:**

Final verification run, then report to 03.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== 1. live precheck ===\"; python _shared/fb_session_check.py; echo \"exit=$?\"; echo \"=== 2. engine test ===\"; python _shared/_test_fb_session_check.py | tail -2; echo \"=== 3. watchdog lane test ===\"; python _test_cron_watchdog_fb_session.py | tail -

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== 1. live precheck ===\"; python _shared/fb_session_check.py; echo \"exit=$?\"; echo \"=== 2. engine test ===\"; python _shared/_test_fb_session_check.py | tail -2; echo \"=== 3. watchdog lane test ===\"; python _test_cron_watchdog_fb_session.py | tail -

---

**Claude:**

All green. Reporting to 03 and closing ON AIR.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python bus_send.py ALL \"$(cat <<'MSG'\n✅ КЛАСС ЗАКРЫТ: fb-session-logged-out (4 датированных случая — 23.08, 25.08, 31.08, 01.09)\n\nКОРЕНЬ: смерть FB-сессии была видна ТОЛЬКО дорогим полным заходом рутины в браузер раз в сутки. Между заходами лейн стоял молча —

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close --zone arch-system 2>&1 | tail -3; echo \"=== board ===\"; python ~/.claude/scripts/onair.py list 2>&1 | head -5", "description": "Close ON AIR declaration"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close 2>&1 | tail -3; echo \"=== board ===\"; python ~/.claude/scripts/onair.py list 2>&1 | head -5", "description": "Close ON AIR (no --zone arg)"}

---

> `Bash` -- {"command": "python ~/.claude/scripts/onair.py close 2026-09-01T105507Z-HUB-01-fa29b5aa-arch-system 2>&1 | tail -3; echo \"=== board ===\"; python ~/.claude/scripts/onair.py list 2>&1 | head -5", "description": "Close ON AIR by id"}

---

> `Bash` -- {"command": "M=~/.claude/projects/C--Users-dev--CLAUDE-NODE-0X-May26/memory/deterministic-script-gotchas.md; ls -la $M 2>/dev/null && tail -4 $M", "description": "Check gotchas memory file"}

---

> `Bash` -- {"command": "python - <<'PY'\nimport io, pathlib\np = pathlib.Path.home() / \".claude/projects/C--Users-dev--CLAUDE-NODE-0X-May26/memory/deterministic-script-gotchas.md\"\nline = (\n\"\\n- **`x = state.get(\\\"k\\\") or now` МОЛЧА теряет стамп, если значение falsy-`0` (01.09.2026, хаб, сторож FB-сесс

---

**Claude:**

[⏰ вторник, день, 12:0x, 1 сентября 2026]

🎙 **Майк:** класс закрыт, но главное не предчек — а то, что **тест поймал баг, из-за которого сторож не сработал бы ни разу**. `dead_since = st.get(...) or now`: ноль falsy, стамп перезаписывался каждый прогон, разница всегда 0. В проде `now` — настоящий epoch, так что баг спал бы тихо, и мы бы месяц считали, что сторож стоит. Вопрос на подумать: сколько ещё наших «зелёных» сторожей никогда не краснели на живом железе?

## Что сделано

**Премисса проверена первой** — предчека действительно не было. Три грепа по `fb_session|fb_precheck|c_user` дали 3 файла, все — ложные срабатывания на подстроке (`sc_user_state_none`, `rec_user`). Иронично: ровно тот класс «детектор судит подстроку», что уже в журнале.

**Не дублировал соседа.** `_shared/firefox_cookies.py` уже умел резолвить профиль и копировать БД мимо лока — предчек стал тонкой обёрткой над ним, а не второй копией.

| Артефакт | Что |
|---|---|
| [fb_session_check.py](../../.claude/scripts/_shared/fb_session_check.py) | 0 LLM, 0 сети. exit 0 жива / 1 мертва / **2 не определил (fail-closed)**, возраст `lastAccessed`, секреты не печатает |
| [SKILL.md:12](../../.claude/scheduled-tasks/fb-reply-daily/SKILL.md:12) | Шаг 0.5 — мертва ⇒ аск D + СТОП **без** захода в браузер |
| [cron_watchdog.py](../../.claude/scripts/cron_watchdog.py) | `check_fb_session()` — сторож снаружи (§5.5), алерт в 03 при простое >6ч. Нового робота не заводил |
| 2 теста | 15/15 + 12/12, **оба доказаны красными** на сломанном движке |

## Улики, не слова

- живой замер: `c_user`+`xs` на месте, exit 0, возраст 0.0ч — **сессия сейчас жива**
- саботаж `REQUIRED → только xs` ⇒ 4 FAIL, exit 1 — сторож умеет краснеть
- прежние `_test_cron_watchdog*.py` после моей правки ALL PASS (не сломал сторожа 20+ задач)
- `code_provenance_lint` OK, 0 нарушений; коммит `431d37523`, 4 трейлера

## Чего я НЕ сделал — говорю прямо

**Второй корень остался.** 31.08 замерено: **547 из 561 аска в 02 умерли молча (98%)**. Предчек экономит прогон и будит 03 — но если 02 не читается, руки не придут. Это отдельный класс, здесь не чинился.

**🌍 раздача не выполнена.** Ядро переносимо (приём «проверь сессию с диска до дорогого захода браузера» лечит молча-разлогиненных Selenium/Playwright-ботов у посторонних), обвязка наша. В треды и gist в этом заходе не ходил — не выдаю за сделанное.

Соседу `fb-backfill-firefox` в 03 сказано: `SKILL.md` тронут только вставкой Шага 0.5, бэкап рядом, мержить поверх а не перезаписывать.

🧒 **Простыми словами:** раньше робот каждый день заходил в Фейсбук через браузер — долго — и только там узнавал, что нас разлогинило. Так лейн простоял 12 дней впустую. Теперь он сначала за долю секунды заглядывает в файлик на диске: «мы вообще залогинены?» Нет — сразу останавливается и зовёт на помощь, браузер не открывает. И отдельный сторож, который живёт в стороне, крикнет в общий чат, если мы разлогинены дольше 6 часов. Ещё тест нашёл настоящую поломку: сторож считал ноль за «ничего нет» и из-за этого не крикнул бы никогда — починил.
