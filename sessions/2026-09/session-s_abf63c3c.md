---
session: s_abf63c3c
date: 2026-09-01
words: 2405
turns: 8
tools: "Bash, ToolSearch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-01 · Scheduled run: auto-hub-260824-nsfw-dr-posts

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_abf63c3c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260824-nsfw-dr-posts" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260824-nsfw-dr-posts\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первым действием вызови mcp set_session_title: "AUTO-hub-260901-fix-person-cards".

Задача (приказ оператора 01.09 11:01: «почини карточки отдельной сессией»): три person-карточки рождены 31.08 писателем robot:claude на NODE-0X БЕЗ единой wikilink — первые нарушители нового контракта link-at-birth (канон: волт `02-Protocols/reglament-link-at-birth-avtopisateli-rozhdayut-zametki-so-svyazyami`, память [[link-at-birth-contract]]):
- `07-People/person-alex-albert-anthropic.md`
- `07-People/person-mary-thengvall.md`
- `07-People/person-zack-proser.md`

Что сделать — скилл /relink Mode A на КАЖДУЮ карточку (retrieval first → judgment → write):
1. Прочитай карточку; кандидатов ищи каналами: `namesearch/find_name.py` + `brain_ask.py` + grep (НЕ скан-всего-волта).
2. Дай каждой: ≥1 исходящую типизированную ссылку (человек Anthropic/DevRel → [[mission-llm-hire-weekly-plan]] / mission2-top10-matrix / соответствующие MOC и person-соседи по контексту знакомства) + дорогу из хаба (в какой людской/лидовый MOC или реестр её вписать — реши по факту, ≤2 MOC).
3. Проверь 7 полей CRM-провенанса (reglament-lid-v-crm-nesyot-ves-kontekst-znakomstva): дата занесения · откуда · где пересеклись · почему занесли · чем полезен · что знаем · косвенные связи. Пустое НЕ выдумывать — `🤔 не подтверждено`; источник ищи в сессиях MacBook 31.08 (01-Conversations/Claude, _session-md) и CRM.
4. Бэкап-гейт: сегодняшний git-бэкап волта есть (pre-intervention 4badcbbc39 + мои коммиты); перед записью прогони `git -C D:\Vault\Vault-Knowledge add -A && git commit` не надо — пишет обычным порядком, орфан-хук проверит сам.
5. Верификация: `python ~/.claude/scripts/link_at_birth_lint.py --hours 48` — эти 3 файла должны ИСЧЕЗНУТЬ из нарушений (карточки старше 26ч к моменту прогона — тогда проверь вручную: в каждой ≥1 wikilink в теле + ≥1 входящая по reverse-index/grep).
6. КОРЕНЬ не забудь: найди, КАКОЙ конвейер/сессия на NODE-0X родил карточки (grep по _session-md/NODE-0X за 31.08), и оставь одну строку в 00-System/Breakage-Journal.md (класс «person-writer без link-at-birth», 1-й случай, писатель поимённо). Чинить сам писатель НЕ надо (правило третьей поломки) — только строка.
7. Отчёт: короткая строка в TG-03 через bus_send.py (dual-send) + отчёт в сессии.

📌 Обязательный блок STOP-DUP: прочитай и исполни $OBSIDIAN_VAULT/08-Templates/seed-stop-dup-block.md (ON AIR declare/close · RECALL летящей работы · разнос fireAt по баку).

Границы: Tier-2 → стоп + аск в 02 POLICE (approval.py); наружу ничего не шлём; person-* правим ТОЛЬКО эти три файла поимённо, никаких pattern-touch.
</scheduled-task>

---

**Claude:**

I'll start by setting the session title, then work through the task.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "AUTO-hub-260901-fix-person-cards"}

---

> `Bash` -- {"command": "cat \"D:/Vault/Vault-Knowledge/08-Templates/seed-stop-dup-block.md\" 2>/dev/null || echo \"NO_FILE\"", "description": "Read STOP-DUP block template"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && for f in person-alex-albert-anthropic.md person-mary-thengvall.md person-zack-proser.md; do echo \"===== $f =====\"; ls -la \"$f\" 2>/dev/null || echo MISSING; echo \"--- wikilinks: $(grep -o '\\[\\[[^]]*\\]\\]' \"$f\" 2>/dev/null | wc -l)

---

**Claude:**

Премисса подтверждена: 3 файла существуют, 0 wikilink в каждом. Объявляю ON AIR и читаю карточки.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py zones 2>&1 | head -40", "description": "List ON AIR zones"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py check --zone crm-leads 2>&1 | head -20; echo \"=== LIST ===\"; python onair.py list 2>&1 | head -30", "description": "ON AIR check + list flying work"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone crm-leads --mode exclusive --title \"Починка 3 person-карточек без link-at-birth (Albert/Thengvall/Proser)\" --ttl-hours 3 2>&1 | tail -5", "description": "Declare ON AIR crm-leads"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && for f in person-alex-albert-anthropic.md person-mary-thengvall.md person-zack-proser.md; do echo \"########## $f\"; cat \"$f\"; echo; done", "description": "Read all three person cards"}

---

**Claude:**

Карточки содержательно полные (все 7 полей CRM есть). Дыра ровно одна: ноль wikilink и ноль дорог из хаба. Ищу кандидатов детерминированно.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== mission ===\"; find . -iname \"*mission*\" -name \"*.md\" 2>/dev/null | head -20; echo \"=== MOC 90 ===\"; ls 90_MOCs/ 2>/dev/null | head -60", "description": "Find mission notes + list MOCs"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== live mission files in 04-Projects ===\"; ls 04-Projects/ | grep -i mission; echo \"=== rest of 90_MOCs ===\"; ls 90_MOCs/ | tail -30", "description": "Live mission notes + remaining MOCs"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== who links to person-* generally (sample of incoming) ===\"; grep -rl \"person-\" 90_MOCs/ 2>/dev/null | head -10; echo; echo \"=== 07-People count ===\"; ls 07-People/ | wc -l; echo \"=== recent person cards (mission2/devrel tag) ===\"; g

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/04-Projects\" && echo \"##### mission2-top10-matrix.md\"; head -70 mission2-top10-matrix.md; echo; echo \"##### wc\"; wc -l mission2-top10-matrix.md mission-llm-hire-weekly-plan.md", "description": "Read mission2-top10-matrix head"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"##### mission-llm-hire-weekly-plan head\"; sed -n '1,45p' 04-Projects/mission-llm-hire-weekly-plan.md", "description": "Read weekly plan head"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== notes mentioning these names (excl 07-People + .stversions) ===\"; grep -rl -i -E \"Thengvall|zackproser|Zack Proser|alexalbert|Alex Albert\" --include=\"*.md\" . 2>/dev/null | grep -v \"^./.stversions\" | grep -v \"^./07-People\" | head 

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== vault notes dated 2026-08-31 (non-stversions) ===\"; find . -name \"*2026-08-31*\" -name \"*.md\" -not -path \"./.stversions/*\" 2>/dev/null | head -30; echo; echo \"=== files modified Aug 31 in curated layers ===\"; find 02-Decisions 03-

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== MacBook 31.08 retros ===\"; ls 01-Conversations/Claude/Retros/ | grep -i \"2026-08-31\" | grep -i -E \"mac|devrel|heroes|geroi\"; echo \"=== grep the 3 names inside 31.08 conversation/session files ===\"; grep -rl -i -E \"Thengvall|zackpr

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && git log --format=\"%h|%ad|%an|%s\" --date=iso -3 -- 07-People/person-zack-proser.md 07-People/person-mary-thengvall.md 07-People/person-alex-albert-anthropic.md 2>&1 | head; echo \"=== trailers of the creating commit ===\"; git log --format=\"%h %ad

---

> `Bash` -- {"command": "cd \"D:/Vault\" && ls -d */_session-md 2>/dev/null; find . -maxdepth 3 -type d -name \"_session-md\" 2>/dev/null | head", "description": "Locate _session-md dir"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_session-md\" && ls | head -5; echo \"=== MacBook dirs ===\"; ls -d *MacBook* 2>/dev/null | head; echo \"=== grep names ===\"; grep -rl -i -E \"Thengvall|zackproser|alexalbertt\" . 2>/dev/null | head -10", "description": "Grep session-md for the writer"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_session-md/NODE-0X\" && f=s_b56720c6.md; ls -la \"$f\"; echo \"=== head 40 ===\"; head -40 \"$f\"", "description": "Read the MacBook session that wrote the cards"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_session-md/NODE-0X\" && f=s_b56720c6.md; grep -n -i -E \"адмит|крутост|person-alex|person-mary|person-zack|07-People|героев|герои\" \"$f\" | head -25", "description": "Find the order and card-writing moment"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_session-md/NODE-0X\" && f=s_b56720c6.md; sed -n '1460,1520p' \"$f\"", "description": "Read the order context"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && f=$(find 02-Protocols -name \"reglament-link-at-birth*\" 2>/dev/null | head -1); echo \"FILE: $f\"; sed -n '1,25p' \"$f\"", "description": "Check link-at-birth reglament date"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && for n in arc-llm-hire task-2026-07-17-anthropic-job-track task-2026-07-31-ambassador-applications-watch reglament-zametnost-v-top-10-llm-issue-matching oss-wave2-strike-list everything-becomes-content reglament-pravilo-tryoh-dney-github-pr decision-

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && for n in reglament-vsyo-chto-my-delaem-stanovitsya-kontentom reglament-lid-v-crm-nesyot-ves-kontekst-znakomstva reglament-golos-maykrofta-nazyvay-sebya reglament-vypustil-funkcional-naydi-potrebiteley-i-pridi-k-nim reglament-deystvie-vazhnee-bezdeys

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"##### _CRM-MOC (first 60)\"; sed -n '1,60p' 90_MOCs/_CRM-MOC.md; echo \"... wc:\"; wc -l 90_MOCs/_CRM-MOC.md", "description": "Inspect _CRM-MOC"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && sed -n '1,40p' 10-Tasks/task-2026-07-17-anthropic-job-track.md; echo \"=== wc ===\"; wc -l 10-Tasks/task-2026-07-17-anthropic-job-track.md", "description": "Inspect anthropic job track task"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && sed -n '25,75p' 02-Protocols/reglament-link-at-birth-avtopisateli-rozhdayut-zametki-so-svyazyami.md", "description": "Read the minimal contract of link-at-birth"}

---

> `Bash` -- {"command": "grep -rn -i -E \"evidence_for|same_cluster|moc_member|словар\" ~/.claude/skills/relink/SKILL.md 2>/dev/null | head -20", "description": "Get /relink link-type vocabulary"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && for n in retro-2026-07-27-evals-artifact-and-first-devrel-touch decision-2026-09-01-hiring-vs-new-venture reglament-pochinil-u-sebya-srazu-razday-miru retro-2026-07-31-doors-not-dms-ambassador-applications positioning-dev-mike-one-machine; do r=$(

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && echo \"=== backup evidence: today's vault commits ===\"; git log --format=\"%h|%ad|%s\" --date=iso --since=\"2026-09-01 00:00\" 2>&1 | head -8; echo; echo \"=== decision-2026-09-01-hiring-vs-new-venture head ===\"; sed -n '1,22p' 02-Decisions/decisi

---

**Claude:**

Все цели связей проверены на диске. Пишу «Связано» в три карточки.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && cat >> person-alex-albert-anthropic.md << 'EOF'\n\n## Связано\n- [[task-2026-07-17-anthropic-job-track]] — evidence_for: он и есть адресат трека найма в Anthropic; приказ оператора 31.08 «напишем, что адмитим их крутость» родился внутри этой 

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && cat >> person-mary-thengvall.md << 'EOF'\n\n## Связано\n- [[mission-llm-hire-weekly-plan]] — method_for: её фреймворк DevRel Qualified Leads = язык, на котором наниматель считает ценность не-кодерских вкладов (Волна 1 «Developer Education 

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && cat >> person-zack-proser.md << 'EOF'\n\n## Связано\n- [[reglament-pochinil-u-sebya-srazu-razday-miru]] — evidence_for: источник знакомства — раздача опыта из pr_watch, наш issue #1 в его pr-babysitter (31.08), первый живой отклик на его д

---

**Claude:**

Теперь дороги из хабов. Смотрю, куда встроить в план миссии.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/04-Projects\" && grep -n \"^## \\|^# \" mission-llm-hire-weekly-plan.md | head -30", "description": "Map headings of the mission plan"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/04-Projects\" && sed -n '39,44p;229,240p' mission-llm-hire-weekly-plan.md", "description": "Read insertion context"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/04-Projects\" && python - << 'PYEOF'\nimport io\np = \"mission-llm-hire-weekly-plan.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nanchor = \"## \\u2b50 \\u0420\\u0415\\u0428\\u0415\\u041d\\u041e 25.07 (\\u0441\\u043f\\u0430\\u0440\\u0440\\u0438\\u043d

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/04-Projects\" && grep -n \"person-\" mission-llm-hire-weekly-plan.md; echo \"--- rendered section ---\"; sed -n '/31.08 — Люди-ориентиры/,/^## ⭐ РЕШЕНО 25.07/p' mission-llm-hire-weekly-plan.md", "description": "Verify inserted section renders correctly"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/10-Tasks\" && sed -n '36,44p' task-2026-07-17-anthropic-job-track.md", "description": "Read umbrella block of anthropic task"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/10-Tasks\" && python - << 'PYEOF'\nimport io\np = \"task-2026-07-17-anthropic-job-track.md\"\ns = io.open(p, encoding=\"utf-8\").read()\nanchor = \"- CV/\\u0440\\u0435\\u0437\\u044e\\u043c\\u0435 \\u0410\\u043d\\u0442\\u043e\\u043d\\u0430 + PhD-\\u043f\\

---

**Claude:**

Проверка.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python link_at_birth_lint.py --hours 48 2>&1 | tail -30; echo \"EXIT=$?\"", "description": "Run link_at_birth_lint"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && for n in person-alex-albert-anthropic person-mary-thengvall person-zack-proser; do out=$(grep -rl \"\\[\\[$n\\]\\]\" --include=\"*.md\" . 2>/dev/null | grep -v \"^./.stversions\" | grep -v \"07-People/$n.md\"); cnt=$(echo \"$out\" | grep -c .); echo

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && ls -la _People-MOC.md; head -18 _People-MOC.md; echo \"...\"; grep -n \"alex-albert\\|thengvall\\|zack-proser\" _People-MOC.md", "description": "Inspect _People-MOC"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/00-System\" && tail -20 Breakage-Journal.md; echo \"=== wc ===\"; wc -l Breakage-Journal.md", "description": "Read Breakage-Journal format"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/00-System\" && python - << 'PYEOF'\n# -*- coding: utf-8 -*-\nimport io\np = \"Breakage-Journal.md\"\nline = (\n\"- 2026-09-01 11:2x (\\u0445\\u0430\\u0431 HUB-01, \\u0441\\u0435\\u0441\\u0441\\u0438\\u044f AUTO-hub-260901-fix-person-cards) \\u00b7

---

> `Write` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\C--Users-dev--CLAUDE-NODE-0X-May26\\s_abf63c3c\\scratchpad\\append_journal.py", "content": "# -*- coding: utf-8 -*-\nimport io\n\np = r\"D:\\Vault\\Vault-Knowledge\\00-System\\Breakage-Journal.md\"\n\nline = (

---

> `Bash` -- {"command": "python \"C:/Users/dev/AppData/Local/Temp/claude/C--Users-dev--CLAUDE-NODE-0X-May26/s_abf63c3c/scratchpad/append_journal.py\" && tail -1 \"D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md\" | head -c 400", "description": "Append journal line and verify

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python bus_send.py --help 2>&1 | head -25", "description": "Check bus_send usage"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python bus_send.py \"✅ [hub] Починены 3 person-карточки без link-at-birth (Albert / Thengvall / Proser, рождены 31.08). Каждой добавлен блок ## Связано (6-8 типизированных ссылок по словарю /relink, вкл. источник знакомства) + дорога из хаба: секция «Люди-ориенти

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2>&1 | tail -3", "description": "Close ON AIR declaration"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py close 2026-09-01T102012Z-HUB-01-027f5a3a-crm-leads 2>&1 | tail -3; echo \"=== board ===\"; python onair.py list 2>&1 | tail -5", "description": "Close ON AIR by id"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && tail -9 person-zack-proser.md; echo \"=====\" ; tail -8 person-mary-thengvall.md | head -3", "description": "Verify card rendering"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/07-People\" && python -c \"\nimport io\np='person-zack-proser.md'\ns=io.open(p,encoding='utf-8').read()\ns=s.replace('вахта тредa','вахта треда')\nio.open(p,'w',encoding='utf-8',newline='').write(s)\nprint('fixed' if 'вахта треда' in s else 'MISS')\n\"",

---

**Claude:**

🎙 Майк: карточки были не «плохие» — они были **немые**. Все 7 полей CRM-провенанса там заполнены честно (и неизвестное честно помечено 🤔) — писатель выполнил один контракт и не знал про второй. Дыра ровно в связях, и она вскрыла кое-что про сам регламент: он адресован «авто-писателям»-конвейерам, а сироты пришли от **субагента внутри живой сессии** — тот под формулировку по букве не попадает.

## Сделано

**Премисса проверена первой** (не поверил сиду): 3 файла на диске, по 0 wikilink в каждом. Подтвердилась.

**Каждой карточке — блок `## Связано`** с типизированными ссылками по закрытому словарю /relink (`evidence_for` · `method_for` · `example_of` · `same_cluster` · `moc_member` · `defined_by`), 6–8 исходящих, включая обязательный по контракту **источник знакомства**:
- [person-alex-albert-anthropic.md](D:/Vault/Vault-Knowledge/07-People/person-alex-albert-anthropic.md) → трек найма в Anthropic, строка №4 матрицы топ-10, ambassadors-вахта, ретро 27.07 (X-DM = касание)
- [person-mary-thengvall.md](D:/Vault/Vault-Knowledge/07-People/person-mary-thengvall.md) → план миссии (её DevRel Qualified Leads), mimicry-playbook, «всё = контент»
- [person-zack-proser.md](D:/Vault/Vault-Knowledge/07-People/person-zack-proser.md) → «починил — раздай миру» (issue #1 = источник знакомства), правило трёх дней, GitHub-коммуникация сам

Все 20 целей ссылок проверены на диске перед записью — мёртвых нет.

**Две дороги из хаба** (держал ≤2, как просили):
- [mission-llm-hire-weekly-plan.md:44](D:/Vault/Vault-Knowledge/04-Projects/mission-llm-hire-weekly-plan.md) — новая секция «👤 31.08 Люди-ориентиры миссии: тройка героев» со всеми тремя
- [task-2026-07-17-anthropic-job-track.md:39](D:/Vault/Vault-Knowledge/10-Tasks/task-2026-07-17-anthropic-job-track.md) — строка-адресат для Albert (там же, где живёт приказ 31.08)

**Корень найден поимённо, доказан чтением, а не догадкой:** `_session-md/NODE-0X/s_b56720c6.md` — живая сессия «!!! HR !!! Позиционирование как специалист», строка 1471 = приказ оператора, сразу после него два вызова `Agent`. Карточки написал **субагент-разведчик**, не конвейер и не рутина. Git молчит — снапшот съел авторство (тот самый класс, что сейчас ON AIR у соседней сессии). Строка в [Breakage-Journal.md](D:/Vault/Vault-Knowledge/00-System/Breakage-Journal.md) поставлена, писателя **не чинил** — 1-й случай, правило третьей поломки.

**Верификация уликой:** `link_at_birth_lint.py --hours 48` → 158 заметок, нарушений 1, и это **не наши три** — они исчезли. Обратные ссылки грепом: 5 / 4 / 4 входящих.

## Два честных примечания

1. **Даты не сходятся в пользу «нарушителей»**: регламент link-at-birth установлен **01.09**, карточки рождены **31.08**. Это не «нарушили действовавшее правило», а первый ретроактивно пойманный случай класса. Записал так же в журнал.
2. **Не чинил, вне именного скоупа** (pattern-touch не делал, как и велено): `03-Insights/fork-audit-2026-08-30.md` — сирота, писатель `unknown` (нет frontmatter-подписи). И `_People-MOC.md` формально даёт входящую ссылку всем троим, но как дорога он не работает: авто-дамп на 1 МБ / 34k строк, голая строка без контекста. Мои две дороги — настоящие.

Отчёт ушёл в TG-03 dual-send (`syncthing:OK · tg-03:OK`), табличка ON AIR закрыта.

🧒 **Простыми словами:** у трёх карточек с людьми было полное описание, но ни одной ниточки к остальной базе — как визитка, которая лежит в столе и ни к какой папке не подшита. Я привязал каждую ниточками к нужным заметкам и вписал всех троих в два «оглавления», чтобы их было видно. Ещё нашёл, кто их такими сделал: не робот по расписанию, а помощник внутри вчерашней рабочей сессии на макбуке — записал это одной строкой в журнал поломок, чинить пока не стал, потому что у нас правило: ломается три раза — тогда строим механизм.
