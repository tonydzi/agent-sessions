---
session: s_67bb72e4
date: 2026-09-05
words: 15896
turns: 98
tools: "Bash, Skill, ToolSearch, computer, find, javascript_tool, mcp__ccd_session_mgmt__set_session_title, mcp__claude-in-chrome__browser_batch, mcp__claude-in-chrome__computer, mcp__claude-in-chrome__find, mcp__claude-in-chrome__get_page_text, mcp__claude-in-chrome__javascript_tool"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-05 · Scheduled run: auto-hub-260825-fleet-debt-drain

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_67bb72e4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

<scheduled-task name="auto-hub-260825-fleet-debt-drain" file="C:\Users\dev\.claude\scheduled-tasks\auto-hub-260825-fleet-debt-drain\SKILL.md">
This is an automated run of a scheduled task. The user is not present to answer questions. For implementation details, execute autonomously without asking clarifying questions — make reasonable choices and note them in your output. "write" actions (e.g. MCP tools that send, post, create, update, or delete), only take them if the task file asks for that specific action. When in doubt, producing a report of what you found is the correct output.

Первым делом переименуй себя: set_session_title("DR-runner: веер Playwright DR26-09-04-HUB-01-2323").

⛳ ВХОД: разогнать веер по заказу DR26-09-04-HUB-01-2323 (тема: Playwright для нашего типа работ — пять лейнов против Selenium-Firefox рельсы) и собрать кворум.

📛 ON AIR: первым делом объяви себя — `python ~/.claude/scripts/onair.py check --zone vault-imports/dr-fanout`, чисто → `onair.py declare --zone vault-imports/dr-fanout --mode collab --title "веер DR26-09-04-HUB-01-2323 Playwright" --ttl-hours 6`; в конце `onair close`. Зона занята соседом — НЕ править параллельно: читай его табличку, договаривайся в 03 или бери другой кусок.
👤 КОНСОЛИДАТОР: если по этой теме поднято больше ОДНОГО исполнителя — консолидатор ЭТА СЕССИЯ (dr-runner-playwright). Он сводит результаты и объявляет «готово»; остальные сдают ему кусок и НЕ пишут свой финальный вердикт. Исполнитель один — эта строка не действует.
🔁 RECALL ЛЕТЯЩЕЙ РАБОТЫ (до постройки, не после): `onair.py list` (кто сейчас в воздухе) + свежие панели `~/.claude/scripts/cc-review/bridge-state/usage.jsonl` (вопрос уже гонялся соседом → читай леджер, добавляй ДЕЛЬТУ, панель заново не гоняй — STOP-DUP) + `00-System/Breakage-Journal.md` (этот класс уже разбирали?). Нашёл чужой готовый артефакт — ПЕРЕИСПОЛЬЗУЙ, свой не рожай.
🪫 БАК И СМЕРТЬ ПРИ РОЖДЕНИИ: пачку fireAt-сидов разноси с учётом бака подписки (одна ночь + шаг 15 мин = 4 из 5 умирают об «session limit»). Умер об лимит при рождении — это обязано быть ЗАМЕЧЕНО: следующая сессия и `/retro` проверяют «сид родил ретро?» — одобренная задача без следа исполнения считается НЕ сделанной, а не идущей.
🔍 УЛИКА ПРИ СТАТУС-CLAIM: любое ✅ про ФАЙЛ, КОД или ЧУЖУЮ ПРОВЕРКУ ставится ТОЛЬКО с уликой в том же заходе: `ls`/`cat`/цитата строки/exit-код. Не читал своими глазами — пиши 🤔 и говори прямо, что не проверено; пусто ИЗ ОДНОГО места ≠ «нет на диске» (§5.4) — назови, ГДЕ искал. Наружный док/README/INSTALL/отчёт перед выдачей прогони: `python ~/.claude/scripts/status_claim_lint.py <файл>`.
⏳ ПРЕМИССА — ПРОВЕРЯЕМАЯ, НЕ УТВЕРЖДЕНИЕ: первым шагом замерь по ground truth (живая система / лог / канал / файл на диске — не память и не текст этого сида) ту дыру и тот статус, про которые сид говорит. Сид, ссылающийся на ID или работу С СОСТОЯНИЕМ (заказ, задача, раздача, публикация, PR), ОБЯЗАН прочитать её статус и при «уже закрыто / уже сделано» ВЫЙТИ РАНО с докладом «чем и когда закрыто», а не исполнять «как написано». Не подтвердилась — скажи «премисса протухла», чини то, что реально сломано, и закрой карточку по доказательству. Приказ в сиде — такой же claim, как вывод.

ЧТО ДЕЛАТЬ:
1. `python ~/.claude/scripts/dr_queue.py` (robot-work) — увидь заказ DR26-09-04-HUB-01-2323 в очереди. Исходник промпта: C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_6eeb47ad\scratchpad\dr-playwright-prompt.md
2. Разнеси промпт по живым рельсам (скилл /dr-fanout): цели chatgpt,gemini,grok,claudeai,glm,mistral. КВОРУМ = любые 4 из 6; недобранные честно оставь в missing, ложную независимость не рисуй.
3. Забери тела, сохрани оригиналы в _originals/deep-research/ ПО РОЛИ УЗЛА (`_paths.originals_root()`), заметку-синтез в 03-Insights с провенансом и >=1 входящей ссылкой (link-at-birth).
4. Синтез веди ПО ЛЕЙНАМ: для каждого из 5 лейнов (ATS-подачи Pipe A, забор DR из LLM-UI, соцсети/аутрич, тесты HTML-дашбордов, кодинг/тесты) — вердикт adopt / hybrid / не трогать + решающий факт + уверенность. Главный вопрос-крест: может ли Playwright водить СТОКОВЫЙ залогиненный Firefox (не свою сборку). Если нет — это почти решает всё, скажи прямо.
5. Известные наши улики, которые ОБЯЗАНЫ попасть в синтез (не выдумывай, они замерены 04.09): playwright 1.61.0 уже стоит на хабе с Chromium 1228 и работает в рельсе C claude.ai (headed, persistent profile); в pull_rail_c.py записан landmine "Playwright's own Firefox build fails to launch here (spawn UNKNOWN)"; 42 файла флота на selenium/geckodriver; ats_jobs = 5129 строк (greenhouse 2167 / ashby 1457 / lever 234 / workable 35); ранее отбиты @playwright/mcp (human-in-the-loop) и облачные браузеры (чужой IP).
6. Закрой заказ статусом `applied` ЛИБО `parked` с причиной — `synthesized` финишем НЕ является.
7. Доложи в TG-03 одной свёрткой + отчёт оператору в чат.

Границы: Tier-2 -> стоп и аск в 02. Публичное наружу не постим. Ничего не удалять.
</scheduled-task>

---

**Claude:**

I'll start by setting the session title and checking the ground truth of this order before executing.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 3}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py 2>&1 | head -60", "description": "Check DR queue state"}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "DR-runner: веер Playwright DR26-09-04-HUB-01-2323"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py robot-work 2>&1 | head -80", "description": "Show DR robot-work queue"}

---

**Claude:**

Order confirmed in `dispatch`. Now the premise check + ON AIR declaration.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py status --id DR26-09-04-HUB-01-2323 2>&1 | head -40; echo \"=== ONAIR ===\"; python onair.py check --zone vault-imports/dr-fanout 2>&1 | head -20", "description": "Check DR order status and ON AIR zone"}

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_6eeb47ad/scratchpad/dr-playwright-prompt.md\" 2>&1; echo \"---SIZE---\"; wc -c \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/e9a0590b-275c-44f4-aa4e-37b88

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py status DR26-09-04-HUB-01-2323 2>&1 | head -40", "description": "Check DR order status"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python onair.py declare --zone vault-imports/dr-fanout --mode collab --title \"веер DR26-09-04-HUB-01-2323 Playwright\" --ttl-hours 6 2>&1 | head -20", "description": "Declare ON AIR"}

---

**Claude:**

Premise holds: `approved | 0/6 results`. Now RECALL of flying work before dispatching.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && echo \"=== ONAIR LIST ===\"; python onair.py list 2>&1 | head -25; echo; echo \"=== USAGE LEDGER (playwright mentions) ===\"; grep -i playwright cc-review/bridge-state/usage.jsonl 2>&1 | tail -5 | cut -c1-400; echo \"(exit $?)\"", "description": "RECALL flying wo

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; grep -in \"playwright\" \"$V/00-System/Breakage-Journal.md\" 2>&1 | tail -20; echo \"=== selenium ===\"; grep -in \"selenium\\|geckodriver\" \"$V/00-System/Breakage-Journal.md\" 2>&1 | tail -15", "description": "Check Breakage Journal for this class"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_6eeb47ad/scratchpad/dr-playwright-prompt.md\"", "description": "Read DR prompt"}

---

**Claude:**

Prompt is solid. Now checking the fanout rails.

---

> `Skill` -- {"skill": "dr-fanout", "args": "DR26-09-04-HUB-01-2323"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\dr-fanout

# /dr-fanout — раздать Deep Research по 6 LLM и собрать консенсус

> Финал Alpha Protocol на автомате. Каналы: **ChatGPT** (chatgpt.com) · **Gemini** (gemini.google.com) · **Grok** (grok.com) · **claude.ai** (claude.ai) · **GLM** (chat.z.ai) · **Mistral Le Chat** (chat.mistral.ai, с 05.08.2026 — дверь ещё не открыта, см. рецепт). Механика = Claude-in-Chrome MCP (живой залогиненный Chrome оператора). Канон: [[alpha-protocol-recall-plus-dr]], decision-multi-llm-vendor-independence (гетеро-консенсус), [[chrome-autonomy-self-drive]], [[browser-work-on-peers-not-hub]] (строго локально).
>
> ⭐ **КВОРУМ 4 (из 5, с 05.08 — из 6)** (приказ оператора 04.08.2026: «я бы считал что ДР выполнен если сделано 4 из 5 ЛЛМ»). `dr_queue.derive_status` закрывает заказ, когда собраны ЛЮБЫЕ 4 рельсы (из 5, а с 05.08.2026 — из 6) — одна молчащая рельса больше не держит запись заложником (замер: gemini 32 заказа / 6 отчётов). ⛔ Кворум НЕ отменяет пятую рельсу: недобранное плечо продолжает светиться в `status` строкой «⚠️ кворум 4/5, не собрано: …» и в `robot-work` полем `missing_quorum_ok` — «сойдёт» должно быть ВИДНО. Узкий веер (3 цели) по-прежнему требует все 3: кворум = `min(4, сколько заказано)`. ⭐ Шестая рельса (Mistral) планку НЕ подняла — она добавлена, чтобы 4 набиралось легче. Гейт: `python ~/.claude/scripts/_test_dr_quorum.py`.
>
> ⭐ **ВЕЕР 04.08.2026 = ПЯТЬ РЕЛЬС** (два прямых распоряжения оператора в один день): «теперь ВСЕГДА добавляй КЛОД.аи в ДРы» + «glm ТОЖЕ ИСПОЛЬЗУЕМ ДЛЯ ДР… ВХОД ЧЕРЕЗ ббПЛАТИНУМ». Машинная истина дефолта — `dr_start.py --targets` (`chatgpt,gemini,grok,claudeai,glm`); ⛔ сокращать веер молча нельзя, снятие рельсы = `dr_queue.py retarget --drop` с доказанными дверями (обе новые рельсы уже в `BROWSER_RAILS`).

## ⭐ ЗАЧЕМ ЭТО ВООБЩЕ: замкнутая петля САМООБУЧЕНИЯ (dev 04.08.2026)

> «Это очень удобная штука для самообучения ИИ — когда ИИ сама заказывает ДР.»

Скилл выглядит как «разослать промпт по сайтам», но это только транспорт. Настоящая ценность — **петля,
в которой ИИ сама чинит свои пробелы**, и человек в ней не курьер, а владелец решений:

```
① пробел      RECALL по волту+памяти не отвечает на вопрос → GAP назван вслух (Alpha Protocol)
② заказ       ИИ САМА нумерует DR и разносит промпт по 5 рельсам (мандат 14.07: без «+», квоты не экономим)
③ сбор        доказательство работы, не красивый текст: 0 searches / 0 citations = `dead`, не `collected`
④ синтез      гетеро-кворум (разные вендоры = разные обучающие базы) → insight-DR + Decision Memo
⑤ ЗАПИСЬ      вывод уходит в ДОМА правил (CLAUDE.md · Библия · память · скилл) — §8.4/§8.6
⑥ следующая сессия стартует уже умнее. Петля замкнулась.
```

**Шаг ⑤ — единственное, что отличает самообучение от «почитал и забыл».** DR без записи в дом = потраченная
квота: замер 29.07 — 184 из 246 отчётов висели в статусе `synthesized` и никуда не легли. Отсюда жёсткая
клауза §9.1: у каждого DR есть КОНЕЦ (`applied` с «что поменяли» либо `parked` с «почему не берём»).

**Три опоры, без которых петля врёт сама себе:**
1. **Гетерогенность.** Пять рельс = пять разных моделей. Один вендор, спрошенный пять раз, — это не пять мнений.
2. **Доказательство работы.** У отчёта должны быть источники/поиски/время думанья. Красивый текст из
   параметрической памяти неотличим от исследования на вид — и отравляет синтез молча.
3. **Обратная сторона той же монеты — рельсы РЕВЬЮ** (`secondop.py`, CLAUDE.md §4.3): DR-веер учит,
   ломатель проверяет. Локальные headless: `codex` · `grok` · `gemini` (04.08); веб-дверь: `glm` и остальные.
   Тот же принцип «дверь закрыта ≠ вендор мёртв» и тот же запрет тихой подмены вендора.

**Безлюдный режим:** `dr_headless_dispatch.py` (04.08) гоняет grok/codex без человека. ⚠️ Провал там судится
по РАЗМЕРУ выхода, а не по exit-коду: ведущий `---` YAML-фронтматтера убивал обе рельсы при честном exit 0 и
файле в 0 байт.

## ⭐ Что уже решено (фундамент, не переисследовать) — обновлено 2026-07-16
1. **Браузерный слой = Firefox-first** (Decision Memo `02-Decisions/decision-2026-07-16-browser-automation-layer.md`, DR26-07-16-HUB-01, уверенность high). Chrome 127+ шифрует куки (ABE) и с апреля 2026 привязывает сессии к железу (DBSC) → внешнее извлечение куки невозможно без malware-техник. **Firefox куки открыты** (plaintext SQLite, DBSC не реализует) → выделенный per-service Firefox-профиль + Playwright `launch_persistent_context`; Chrome CDP-attach только как fallback для строго-Chromium сайтов. Хаб-стек уже поднят: `firefox_cookies.py` (`~/.claude/scripts/_shared/`), профили `D:\AutomationBrowsers\Firefox\`.
2. **Живой Chrome-MCP (Claude-in-Chrome) остаётся осознанным anti-ban путём** для действий «как человек в реальном сеансе» (fb-post/x-post едут так). Для dr-fanout выбор пути исполнения (живой Chrome-MCP vs headless Firefox-Playwright) уточняется идущим DR (см. п.4).
3. **CLI-обход НЕ даёт Deep Research по подписке** (проверено 15.07): Codex CLI / Gemini CLI = только web search; настоящий Deep Research потребительской подписки программно не дёргается (Google DR-агент = платный API отдельно). ⇒ браузерная веб-морда — единственная дорога к DR по подпискам, значит делаем её анти-хрупкой, а не бежим от неё.
4. **ToS-риск, острее всего у Grok:** xAI AUP прямо запрещает автоматический/не-человеческий доступ (риск suspension/termination). Задокументированных банов за автоматизацию СВОЕГО аккаунта нет, но текст явный → Grok-канал гнать в человеческом темпе; решение «оставить/притормозить/заменить на Claude.ai» — за оператором.
5. **Grok — просто продолжаем использовать** (решение оператора 2026-07-16). xAI AUP формально запрещает автоматизацию, но охота идёт за масс-скрейпингом (штраф $15k/1M запросов), а наш темп естественно крошечный (несколько DR в день максимум) → мы не мишень. Ценность третьего независимого голоса > управляемого риска. НЕ городить лимиты/троттлинг ([[ak47-simplicity]]) — Grok в обычной ротации; если сам вендор упрётся (капча/challenge) — доложить и пропустить этот канал, без драмы.
6. **Путь исполнения — ГИБРИДНЫЙ, под каждого вендора свой** (решение оператора 2026-07-16, «и так и так»). Не один способ на всех:
   | Вендор | Путь | Почему |
   |---|---|---|
   | **Grok** | живой Chrome-MCP, человеческий темп | ToS-чувствителен → действуем как человек в реальном сеансе (макс anti-ban, как fb-post [[chrome-autonomy-self-drive]]); headless-бот тут = максимум риска |
   | **ChatGPT** | выделенный Firefox-профиль headless (безлюдно) ИЛИ живой Chrome-MCP | ToS мягче; извлечение отчёта = backend JSON (работает в обоих); для расписания без человека → Firefox |
   | **Gemini** | выделенный Firefox-профиль headless (безлюдно) | двухфазный (план→Start research), терпим к автоматизации; кандидат №1 на полностью безлюдный прогон |
   Принцип: чем жёстче ToS/бан-чувствительность вендора → тем ближе к «живой человек в сеансе» (Chrome-MCP); чем терпимее + важнее безлюдность → тем ближе к выделенному Firefox-профилю (Playwright persistent, фундамент HUB-01).
7. **✅ Оркестрация — ПОДТВЕРЖДЕНА внешним DR** (`DR26-07-14-FLEE-01`, синтез ChatGPT+Grok 2026-07-16, выжимка `03-Insights/insight-DR-DR26-07-14-FLEE-01-*`). Оба вендора независимо: ядро = **durable state-machine + job-ledger, НЕ «долгоживущий автономный браузер-агент»**; локальный ledger-FSM достаточен для одно-хозяйного хаба. Оба независимо советуют **НЕ строить безлюдную Grok-автоматизацию** (xAI AUP + enforcement реален: >52k банов в 2026, Reuters 15.07) → наша матрица п.6 уже это соблюдает (Grok только живой Chrome-MCP, никогда в демоне). **Безлюдное расписание стартуем с 2 вендоров: ChatGPT + Gemini.**
8. **Вендор-логику держать ТОНКОЙ, оркестрацию — общей.** UI-специфичные репо мрут быстро (`chatgpt-automation-mcp` архив 27.04.2026, `browserbase/gemini-browser` архив 20.05.2026). Всё вендор-специфичное = сменные «адаптеры» внизу; автомат/ledger сверху не меняется.
9. **⚠️ ОТКРЫТО — официальный путь для Gemini:** Deep Research Agent / **Interactions API** (`background=True` + polling, collaborative_planning) — production-ready, снимает самый хрупкий и медленный браузерный канал. НО ⚠️ УСЛОЖНЕНИЕ + неясен биллинг: входит ли в подписку Ultra или это отдельные деньги (ChatGPT-отчёт: «НЕ то же free-with-subscription»). **Проверить биллинг ДО стройки** ([[prefer-included-limits-before-paid-api]]) — если платный, не заводить без «+» оператора.

## ✅ GEMINI-ДР НА NODE-0X — РАБОЧИЙ РЕЦЕПТ, пройден вживую 01.08.2026 (DR26-08-01-MACANTON-02-659)

Приказ оператора голосом 01.08: «делать чтобы через ГЕМИНИ!!!» ⇒ `gemini` вернулся в `DEFAULT_TARGETS` (`dr_queue.py`).
Дверь ровно одна и она **НЕ API**: живой Chrome под `[EMAIL]` («Punk», платный AI Pro). Шаги, каждый проверен:

1. `list_connected_browsers` → набор МЕНЯЕТСЯ между заходами (в этом прогоне за 10 минут стало 2 Chrome вместо 1). Взял свой сам, `select_browser`, у оператора НЕ спрашивал ([[browser-and-account-pick-yourself]]).
2. `navigate` на `https://gemini.google.com/app?authuser=[EMAIL]` → **скриншот** (innerText врёт). Признак живой сессии: «What's the vibe, Punk?» + селектор `Pro Extended`. Аккаунт подтверждать `aria-label` кнопки профиля: `Google Account: Punk Crypto ([EMAIL])`.
3. Транспорт промпта — `window.name`, направление **localhost → gemini** (обратное COOP рвёт): `python3 -m http.server` в скретчпаде → `navigate` на файл → `window.name = await fetch(location.href).then(r=>r.text())` → `navigate` на gemini. Замер: 5656 симв. и 100 кириллических доехали 1-в-1.
4. Чип Deep research ставить в ПУСТОМ композере: «+» (`Upload & tools`) → `More tools` → `Deep research`. ⚠️ Кликать по **ref** из `find`, не по координатам: клик по координатам подменю промахнулся молча, меню закрылось без чипа, и это видно только скриншотом. Признак успеха: плейсхолдер меняется на `What do you want to research?` и рядом появляется пилюля `Deep research`.
5. Вставка — только JS: фокус в `.ql-editor` → каретка в конец → `document.execCommand('insertText', false, txt)` (сел с первого раза; синтетический paste держим фолбэком). Сверять ДВУМЯ мерками: длина (`innerText` даёт +60 симв. на блочных переносах — это норма) и счётчик кириллицы (обязан совпасть точно).
6. Send → **двухфазность**: `Generating research plan` (~1 мин) → `find` кнопку `Start research` → клик по ref. Доказательство старта: «I'm on it… you can leave this chat» + карточка `Creating your report…` с чипами реальных источников внизу.

⛔ API-ключ ДР-рельсой НЕ является и не станет без денег. Замер 01.08, 3 чередования подряд в одной минуте (`probe2.py`): `gemini-flash-lite-latest` без `google_search` → 200 все три раза, с `google_search` → 429 все три раза, БЕЗ имени метрики и без `violations` — подпись «квота грунтинга 0 на free tier». Первый прогон, где 429 приходил и на plain-запросы, был собственным RPM (быстрый цикл по 6 моделям) — отделяется паузой 65 с, иначе ловишь ложный диагноз. Побочно: `gemini-2.5-flash` → 404 «no longer available to new users», `gemini-2.5-pro` на free-tier → `limit: 0`.

🔒 Дверь против рецидива: `dr_queue.py retarget --drop <браузерная рельса>` теперь ТРЕБУЕТ `--doors` с ≥2 проверенными дверями отдельными аргументами (гейт судит действие, не подстроку в reason). Ложный drop снимается `dr_queue.py restore <ID> --restore gemini --why "<чем доказано>"`.

## 🔴 GEMINI НА NODE-0X — читать ПЕРВЫМ, если Gemini «просит залогиниться» (разбор 31.07.2026, два ложных диагноза подряд)

**Симптом-обманка:** `gemini.google.com` показывает «Sign in» + Flash-Lite, куки `.google.com` в профиле есть все (`SID`, `LSID`, `__Secure-1PSID`) — выглядит как протухшая сессия. Я выдал ДВА неверных диагноза («сессия протухла» → ask оператору, отозван; «гео-блок на NODE-0X» → заказ хабу, отозван), прежде чем нашёл настоящие причины. Обе ошибки ловились скриншотом и вопросом «а ЧЕЙ это браузер?».

**Настоящих причин две, обе проверены:**
1. **⚠️ Chrome-MCP ≠ эта машина.** «Gemini isn't currently supported in your country» я увидел в Chrome через MCP — а из трёх подключённых Chrome тот оказался на ноуте Норы (IP в России, там Gemini закрыт). Свой IP я мерил curl-ом с NODE-0X (Вена, AT) и склеил факты с двух разных машин. **Правило: IP меряется ИЗНУТРИ того браузера, где виден симптом** (`fetch('https://ipinfo.io/json')` в той же вкладке). На NODE-0X гео-блока НЕТ — проверено изнутри Firefox: country-block False.
2. **Стена Google-consent («Before you continue to Google»)** перехватывает страницу, и ПОД ней рендерится разлогиненная оболочка — по DOM неотличимо от «разлогинен». Снимается трастед-кликом Selenium; кнопка ищется ТОЛЬКО по вложенному span: `//button[.//span[normalize-space(text())='Reject all']]` — поиск по `b.text` её НЕ находит (текст в потомке). После клика стена не возвращается.

**Остаток после снятия стены:** куки Google в AutoFF реально не аутентифицируют → нужен ОДИН живой вход оператора: `firefox -no-remote -profile ~/.claude/browser-profiles/autoff https://gemini.google.com/app` окном, дальше рельса безлюдная. Свежий логин отличается по `creationTime` кук (не `lastAccessed` — его обновляет любой пинг).

⚡ **Порядок диагностики (30 секунд, а не два часа):** (1) скриншот — видимый текст первичен, `document.body.innerText` в фоновой вкладке отдаёт 0–324 симв. и врёт; (2) IP изнутри ТОГО ЖЕ браузера; (3) только потом гипотезы про сессию.

**⛔ Прежде чем снять gemini через `retarget --drop` с формулировкой «на этом узле рельсы нет» (рецидив 01.08: раннер снял рельсу с 6 заказов, а рельса была жива в другом Chrome под Punk/`a@`):**
1. `list_connected_browsers` и обойти **КАЖДЫЙ** подключённый Chrome, не первый попавшийся; набор браузеров меняется между заходами — «в 06:00 был корп» ≠ «в 14:00 нет личного».
2. В каждом браузере пробовать вход **`https://gemini.google.com/app?authuser=[EMAIL]`** — даже если по умолчанию профиль открывает корп-аккаунт, authuser-редирект достаёт личный, если он залогинен в том же Chrome.
3. Причина drop обязана ПОИМЁННО перечислить проверенные двери (сколько Chrome обошёл, что показал каждый, пробовал ли authuser). «Chrome — корп-аккаунт» без счёта браузеров = недоказанный claim ([[prichina-kak-claim]]).
4. Drop = «leg не собран в этом заходе», а НЕ «узел мёртв» — вечные выводы про узел в reason не писать.

Гипотезы, уже проверенные и **опровергнутые** — не тратить на них время заново:
1. «клон профиля теряет `storage/`/localStorage» — полная `rsync`-копия профиля ведёт себя так же;
2. «виноват headless» — headed идентичен;
3. «куки не долиты из WAL» — `cookies.sqlite-wal` 0 байт, снимки полные;
4. «живой Firefox держит сессию в памяти» — штатный SIGTERM, `cookies.sqlite` не изменился ни на байт;
5. «гео-блок на австрийском IP» — НЕТ: изнутри Firefox на NODE-0X блока нет; блок был на ЧУЖОМ Chrome (RU IP).
10. **⭐ ChatGPT-канал по умолчанию = Pro + инструмент «Web search», а НЕ чип Deep research** (замер 2026-08-04, разбор инцидента 26.07). Чип DR на этом аккаунте резолвится в `deep-research-mini`: ран обрывается посреди плана (`status: completed`, шаги 3–5 `pending`, 5–7 мин вместо 20–40) и открывает мало источников (12 уникальных URL при запрошенных 15–25). Тот же вопрос через **Pro + Web search** дал 73 поисковых запроса и 31 прочитанную страницу (`DR26-07-26-ZB-02-harari-alpha-chatgpt.md`, там же вендорский журнал поиска). ⇒ ChatGPT в веере = Web search-рельса; DR-чип — только когда явно нужен длинный автономный ран. ✅ **Тест проведён 04.08** (один ран, чип DR, пикер Pro, чат `6a71e627`): `resolved_model_slug = gpt-5-thinking` — ни полного DR, ни mini; 3m44s, обрыв на шаге 2, отчёт 13.4 КБ и **citations = 0** (URL набраны текстом, маркеров 【…】 нет) ⇒ сегодня чип DR отвечает из памяти по-настоящему. Лестница деградации канала: `deep-research` → `deep-research-mini` (21–26.07, поиск был) → `gpt-5-thinking` (04.08, поиска нет). Заодно закрыто: модель в пикере ни при чём — outer turn у DR всегда `gpt-5-5-instant`. 🤔 Причина (квота vs политика вендора) не доказана: эндпоинта с лимитами в вебе нет (`/backend-api/*limits*` = 404). ⇒ Практический вывод не меняется: **ChatGPT-канал = Web search**, DR-чип на `a2@` не тратить.

## Жёсткие рамки (читать первыми)
1. **⭐ Мандат оператора (2026-07-14, supersedes квота-гейт 05.07): любое количество DR, БЕЗ спроса.** «Делай любое количество депрезёрчей, не спрашивай меня, не беспокойся по поводу лимитов» — ChatGPT при выжатой квоте деградирует мягко (лайтовее отчёт, не отказ), гетеро-веер на 3 вендора компенсирует. Запускаю сам, докладываю постфактум. Единственное «но»: не жечь квоту на ДУБЛИ — дедуп-проверка Шага 0 обязательна.
2. **Браузер строго локально** на машине, где идёт сессия. Ничего не просить у других машин.
3. **Аккаунты оператора:** если сайт разлогинен → логин по [[social-auth-autonomous]] (креды в store); CAPTCHA/2FA-стена → позвать оператора одной фразой + скриншот.
4. **Ничего не отправляем КРОМЕ промпта** в композер DR. Не трогать другие чаты/настройки.
5а. ⛔ **`get_page_text` ВРЁТ НА СПИСКАХ (замер 2026-07-29/31).** Границу знать точно:
   для СТАТЬИ/сплошного текста он годится (на нём и держится вынос отчётов ниже), но для
   **динамического списка** — recents, сайдбар чатов, лента, инбокс — он отдаёт заглушку
   («Choose from your existing conversations…»), тогда как `read_page (filter: all)` на той же
   странице показывает все элементы. Замер: X-инбокс — `get_page_text` «пусто», `read_page`
   15 тредов; форма Anthropic — «пусто», а там кнопка Apply. ⇒ **вывод «список пуст» имеет
   право на жизнь ТОЛЬКО из `read_page`**. Пустота из одного метода — не пустота
   ([[check-all-places-not-one]]); это ложная тишина, а она дороже громкой ошибки.
5. **ANTI-RECENTS при забО́ре отчёта:** ища готовый DR-чат/отчёт в веб-UI (ChatGPT/Gemini/Grok), НЕ заключай «отчёта нет» из беглого списка recents — используй встроенный ПОИСК по ключам/ID + Projects/архив + подтверди активный аккаунт по email. Сперва реестр (`_DR-Registry.md`, Шаг 0), потом UI-поиск, и только потом вывод «нет». Канон: память [[web-ui-search-not-recents]] (инцидент Woom 2026-07-23).
6. **⭐ МОДЕЛИ ПО РОЛЯМ КОНВЕЙЕРА (dev 14.08.2026, «всё правильно — обнови скилл»).** Три роли, три планки:
   - **Курьер-сессия fanout (этот скилл: вставить промпт в композеры, забрать ссылки, леджер) = Sonnet, эффорт low.** Работа механическая; Fable/Opus на разносе = жжение бака без прироста качества. Поднимая ДР-сессию слотом — модель на задаче через MCP не задаётся и в карточке не видна: проверь фактическую модель ПЕРВОЙ строкой транскрипта прогона (`"model":` в jsonl); поехал Fable → один прогон дотерпеть (выхода у курьера мало), на повторе перевесить на Sonnet-слот.
   - **Чужие вендоры внутри их DR = всегда их САМАЯ умная модель + максимальное рассуждение** (§6.3, список сверять у вендора, не по памяти) — это уже зашито в рецептах ниже.
   - **Синтез-консенсус (Шаг 4) = Fable (fallback Opus), эффорт высокий** — это мышление и Decision Memo, курьеру его не отдавать: курьер довозит отчёты до `_originals` и реестра, синтез — отдельный заход умной моделью.

## Шаг 0 — вход
⭐ **ДЕДУП ПЕРЕД КВОТОЙ (dev 2026-07-14):** прежде чем жечь DR-квоты — проверь, не готов ли отчёт уже. (1) Есть ID в промпте → его строка в реестре: `grep "<DR-ID>" "$OBSIDIAN_VAULT/_DR-Registry.md"` — статус `collected`/`synthesized` = СТОП, fan-out не нужен: доложи «уже собран», покажи файлы (`_originals\deep-research\*<DR-ID>*`, `03-Insights\insight-DR-<id>*`), иди в Шаг 4 (синтез). (2) ID нет → grep реестра по ключевым словам темы: та же тема в `issued` → переиспользуй ТОТ ID; в `collected+` → покажи готовое, спроси, нужен ли вообще новый прогон. Ночной `dr_collect.py` (хаб 05:05) флипает статусы по экспортам сам — реестр свежее памяти сессии.
⭐ Номер DR обязателен (dev 2026-07-03): если у промпта ещё нет ID `DRYY-MM-DD-МАШИНА-NN` — выделить: `python $IMPORTS_ROOT/dr_registry.py new "<тема>" --tool chatgpt,gemini,grok` и поставить ID первой строкой промпта (`# DR26-07-03-ZB-01 — <тема>`). Код машины скрипт определяет сам (своя очередь у каждого компа — дублей при синке нет). Канон: `reglament-numeratsiya-dr-i-reestr`.
Промпт берём: из текущего чата (только что сэмитили по Альфе) / из файла, что укажет оператор. «+» НЕ спрашиваем (мандат 14.07) — объявляю строкой `🚀 DR-fanout: разношу <ID> в ChatGPT+Gemini+Grok` и еду.

## Шаг 0.5 — тюнинг промпта под вендоров (обязательно)
Перед раздачей приклеить к телу промпта: `§1 УНИВЕРСАЛЬНЫЙ ADD-ON` из [[dr-platform-playbook]] (`08-Templates\dr-platform-playbook.md`) — всегда, всем; **плюс платформенный блок §2 (Grok) / §3 (Gemini) / §4 (ChatGPT)** под каждого конкретного вендора. Тело (из `deep-research-prompt-template.md`) + §1 одинаковы у всех; платформенный блок различается НАМЕРЕННО (играет на сильную сторону: Grok=реалтайм/X+жёсткие цитаты, Gemini=правка плана/официоз/глубина). ID `DRYY-MM-DD-МАШИНА-NN` первой строкой у всех.

## Шаги 1-3 — АВТОМАТ submit → probe → collect (per vendor)
> Ядро надёжности v2, ✅ подтверждено внешним DR (см. п.7). Каждый вендор проходит автомат независимо; сломался на шаге — падает В ФОЛБЭК того шага, не роняя остальных. Золотое правило: **probe перед burn** — ни одна DR-квота не тратится, пока не доказано: (а) режим включён, (б) промпт целиком, (в) ран стартовал.
>
⭐ **ВОРОТА ПЕРЕД `collected` (правило 04.08, дверь построена 14.08).** Прежде чем назвать легу собранной,
записать её в `_originals` и флипнуть реестр — прогнать пороги:
```
python3 ~/.claude/scripts/dr_leg_gate.py <файл-леги>
```
exit 0 = годна · exit 1 = `collected-EMPTY`, в синтез НЕ идёт. Три порога: объём ≥5000 · источники (ссылки/годы) ·
движок не сказал сам, что поиск не работал. **`exit 0` вендора ничего не доказывает:** `grok --tools ""` отключает
поиск и отдаёт 243 байта преамбулы нулевым кодом — так лега DR26-07-26 пролежала «собранной» 5 дней.
Не прошло → гнать по ДРУГОЙ оси (авторизация · движок · аккаунт · браузер), а не тем же параметром;
рельса выглядит мёртвой → сперва `deploy_check.py` (см. `/secondop`). Легу без источников НЕ сохраняем даже
«чтобы было»: по ней примут решение. Канон: `reglament-vneshnyaya-lega-schitaetsya-sobrannoy-tolko-posle-porogov`.

> **Состояния** (ledger = `_drafts/DR-FANOUT-<DR-ID>-*.md`, ключ = DR-ID → resume идемпотентен): `staged → mode_verified → submitted → started → waiting → ready → collected → delivered`. Аварийные: `needs_reauth` · `drift_suspected` · `probe_failed` · `aborted`. ⭐ **Человеко-гейта ровно два — `needs_reauth` и `drift_suspected`; всё остальное безлюдно** (консенсус DR).
> **Локаторы:** ARIA/role первыми → CSS → и только затем LLM/vision. ⛔ Семантический/LLM-поиск элемента — ТОЛЬКО в dry-run/repair-режиме, НИКОГДА на квота-сабмите (консенсус DR).

Инструменты одним ToolSearch: `tabs_context, navigate, computer, read_page, tabs_create, form_input, get_page_text, read_console_messages`.

### СОСТОЯНИЕ 1 — SUBMIT (включить DR-режим + вставить промпт)
Новая вкладка → дождаться загрузки → залогинен? (нет → [[social-auth-autonomous]]; стена 2FA/CAPTCHA → скриншот + пропустить вендора). Затем **найти DR-режим ГЛЯДЯ на страницу** (не по памяти — UI плывёт у всех троих):
- **ChatGPT** (аккаунт dev.**a2**@gmail.com): сперва селектор модели → **Pro, максимальная** (сейчас GPT-5.6) + максимальный уровень думания; затем композер → меню инструментов («+»/«Tools») → «Deep research». ⭐ dev 21.07: всегда самая умная модель, имя меняется — принцип нет.
- **Gemini** (аккаунт dev.**a**@gmail.com, личный): ⚠️ 31.07 в Chrome этот аккаунт (индекс u/2) отдал МАРКЕТИНГОВЫЙ ЛЕНДИНГ, а не приложение; рабочее приложение было под `dev@` — перед прогоном проверять глазами, какой аккаунт реально открывает app. Прежняя пометка: **платный Google AI Pro, 5 ТБ, с 06.01.2026** (проверено 28.07) — DR ≈20/день, лимиты ~4×, контекст 1M → тяжёлые ДР сюда гоним УВЕРЕННО, это НЕ урезанный бесплатный тир (память [[gemini-two-rails-free-api-vs-paid-ai-pro]]; «free» = только API-ключ ломателя /tt, другая рельса). Модель = **Pro** (сейчас 3.1), ⛔ НЕ Flash (тихо откатывается — проверять!); включить **Extended thinking** (галочка справа возле микрофона); «+» → «Deep Research» → промпт → Enter → план → **дожать OK/Start**.
- **Grok** (аккаунт **avvalon**@icloud.com — с двумя «v», проверено 31.07 — там же Twitter оператора): ⭐ dev 21.07 — режим **Heavy** ДЕФОЛТ (куплена максимальная подписка; supersedes прежнее «Expert, Heavy не трогать»). Отдельной DR-кнопки нет → в тело промпта добавить строку «Search the web extensively and cite sources»; следить, чтобы селектор не свалился в Expert/Fast (тихий деграде ZB-03 20.07). Методика «DR-grade в Grok Heavy» (собрано 21.07, DR26-07-21-HUB-02): **Heavy сам и есть Deep Research** — рой 8–16 суб-агентов, ищут параллельно и спорят; Expert теперь одноагентный и для citation-heavy слабее; DeepSearch/DeeperSearch убраны и растворены в Heavy. Без принуждения Heavy отвечает из памяти → в промпт обязательно: «search the web and X extensively» + 15–25 первичных источников + короткая цитата и точный URL на каждое утверждение + «cite ONLY URLs you actually opened» + финальный проход верификации. Доказательство настоящего прогона: «Thought for» в минутах + счётчик «N sources»; мгновенный ответ без источников = деграде, перезапуск. Квоты = недельный общий пул (Settings → Usage, в процентах), контекст 256k–500k, прогон 5–20+ мин. Экспорта одной кнопкой нет (выделить-скопировать); Share = ПУБЛИЧНАЯ ссылка ⛔. Полный шаблон промпта — в `_originals\deep-research\DR26-07-21-HUB-02-grok-heavy-playbook-grok.md`, раздел «(b) Reusable Prompt TEMPLATE»; синтез — `insight-DR-DR26-07-21-HUB-02-grok-heavy-as-a-deep-research-engine`.
- **claude.ai** (аккаунт dev.**a2**@gmail.com, Claude Max, org `a673590f`) — в дефолте с 04.08.2026 («теперь ВСЕГДА добавляй КЛОД.аи в ДРы»). ⚠️ ПЕРВЫМ ДЕЛОМ проверить, ПОД КЕМ открыт claude.ai: `GET /api/organizations` → должен быть `a673590f`; под `bbplatinum` это ДРУГОЙ аккаунт (та же ловушка, что топит ночной `claudeai-sync`, [[claudeai-sync-needs-a2-account]]). ⛔⛔ **Вход НЕ через logout в живом Chrome оператора** (приказ оператора 30.08, свип #595c4751, канон `reglament-hab-brauzernye-lichnosti-bb-i-roboty`): его Chrome = `dev` ВСЕГДА, робот там не выходит из аккаунта и не переключает его — это и был корень «Chrome постоянно вылогинивает». a2 живёт ТОЛЬКО в выделенном профиле `_chrome_profile_a2`; сессия мертва → перелогин ТОЛЬКО его: `python $IMPORTS_ROOT/claude-ai/railc_login_a2.py` (magic-link просится сам, ссылку несёт Gmail-коннектор a2; ⛔ «Continue with Google» = попап, расширению НЕ виден — не тратить на него заход). Пулл оттуда же: `pull_rail_c.py --run --profile=a2`. DR-режим = **Research** в меню инструментов композера (рядом со скрепкой); модель — самая умная из доступных. Приватный URL чата = `claude.ai/chat/…`.
  - ⛔ **МОДАЛКА «Suggested connectors» ТИХО ДЕРЖИТ РАН (замер 05.08.2026, HUB).** После Send чат создаётся, URL меняется на `/chat/…`, снаружи выглядит как стартовавший Research — **а поиск не начинается вообще**, пока в диалоге «Suggested connectors … Skip / Confirm» не нажат **Skip**. Простояло ~10 минут; сразу после клика пошло «Searching for sources…». ⇒ У claude.ai probe-after-start обязан включать проверку модалки, иначе получишь `not-collected` при полностью живой сессии. Skip выбираем осознанно: сторонние коннекторы внешнему ДР не нужны и тянут приватность.
  - ⏱ **Research тут ДОЛГИЙ:** в этом же прогоне рельса шла 1 час и не завершилась, пока остальные четыре уже сдали отчёты. Не бракуй по времени — кворум закрывается без неё, а отчёт подберёт ночной `dr_collect.py`.
- **GLM** (chat.z.ai, Z.ai/Zhipu) — в дефолте с 04.08.2026 («glm ТОЖЕ ИСПОЛЬЗУЕМ ДЛЯ ДР»). 🔑 **ВХОД = Google SSO под `[EMAIL]` («ббПлатинум») — прямое указание оператора**, пароль в [[credential-store]] (`secrets\google_bb.env`), подаёт его САМ Chrome. ⛔ API-ключ z.ai не подставлять: рельса ПОДПИСОЧНАЯ, ключ = поштучная оплата мимо правила «выгребай лимиты» (CLAUDE.md §6.3). Приватный URL чата = `chat.z.ai/c/…` (образец от оператора: `chat.z.ai/c/s_be3e1bb6`).
  - ✅ **ЗАМЕР ДВЕРИ 04.08.2026, NODE-0X** (не claim — читано со страницы): сессия ЖИВА в **Chrome «Browser 2»**, а в «Browser 1» стоит `Sign in` ⇒ проверять ОБА подключённых Chrome, один профиль ничего не доказывает ([[check-all-places-not-one]]). Аккаунт подтверждён запросом `/api/v1/auths/` → `[EMAIL]`, имя «PaloAlto Ai Research Lab» — этим и проверять, а не глазами по аватарке.
  - ✅ **ЛОКАТОРЫ КОМПОЗЕРА (замерены там же):** редактор = обычный **`<textarea>`** внутри `form` (⛔ НЕ ProseMirror, `isPM:false`) ⇒ в каскаде `paste_verify.js` садится нативный React-сеттер, синтетический paste не нужен. Три кнопки в композере: `+` (файлы) · 🌐 **глобус = веб-поиск** · «атом» с `aria-label="Deep think enabled"` (по умолчанию ВКЛЮЧЁН, синий) — **рядом с надписью `Deep Think` стоит выпадающий селектор УРОВНЯ (`Max` и более слабые), и «включён» ≠ «Max»** · `aria-label="Send Message"`. Селектор модели — слева сверху; список 04.08: **GLM-5.2 (NEW, флагман)** · GLM-5.1 · GLM-5-Turbo · GLM-5V-Turbo · GLM-4.7. По правилу «всегда самая умная» **переключено на GLM-5.2** (было 5.1).
  - ⭐ **ДР-РЕЖИМ ЕСТЬ, ОН СПРЯТАН ПОД ГЛОБУСОМ** (найдено в первом живом прогоне 04.08, DR26-08-04-ZB-11-2142 — утренняя запись «отдельной кнопки Deep Research нет» была верна про видимую панель и неверна про рельсу). Клик по 🌐 открывает меню с двумя режимами: `Search` («Single-round search, quickly get information») и **`Advanced Search`** («Multi-round search, in-depth research and analysis») — тумблер, **по умолчанию ВЫКЛЮЧЕН**. ⛔ Без него рельса отдаёт однораундовый ответ: файл в `results/` появится, а разведки в нём не будет — тот же класс тихого брака, что Grok в Expert вместо Heavy. Порядок сабмита: селектор модели → **GLM-5.2** (дефолт 5.1, переключать руками) → 🌐 → `Advanced Search` ON → **Deep Think = `Max`** (см. пункт ниже — отдельный обязательный шаг) → JS-вставка в `<textarea>` → Send.
  - 🔧 **ПРИБОР:** `~/.claude/skills/dr-fanout/glm_probe.js` (read-only чтение композера, ничего не кликает) + судья `~/.claude/scripts/glm_probe.py` (0 LLM, exit-код, счётчик `_glm_probe_usage.jsonl`). Тесты: `_test_glm_probe.py` (14 проверок) · `_test_glm_probe.js` (node, DOM-заглушка со скриншотов + 5 мутантов). ⚠️ Заглушка ≠ живой chat.z.ai: селекторы списаны с замера 04.08 и скриншотов 31.08 — первый живой прогон обязан сверить `evidence`-строки; не совпало = UI поплыл, чинить ассет, а не обходить гейт.
  - ⭐⭐ **DEEP THINK = ВСЕГДА `Max` (приказ оператора 31.08.2026, со скриншотом композера; память `glm-deep-think-must-be-max`).** Отдельный шаг, а не деталь модели: у «Deep Think» есть выпадашка уровня, и заказ уходит на том уровне, что стоит в поле — тихий брак того же класса, что `Advanced Search` OFF и Grok в Expert вместо Heavy. Порядок: **сначала выставить `Max`, потом вставлять промпт и жать Send** (после вставки композер растёт и элементы уезжают). ✅ Проверка перед Send = ПРОЧИТАТЬ со страницы, что в композере написано `Deep Think  Max`; не прочитал — считай, что не выставил ([[prichina-kak-claim]]). Не читается / выпадашка не поддалась → рельса идёт в `missing`, а не «сойдёт и так».
  - ✅ **ПРОГОН ПОДТВЕРЖДЁН 04.08 21:47** (NODE-0X, Chrome «Browser 1» — утром живой была «Browser 2», ⇒ проверять ОБЕ, а не помнить): промпт 3400 симв. сел нативным React-сеттером, чат `chat.z.ai/c/86f270ee-…`, доказательство старта = текст в потоке «Начинаю многошаговое исследование… серию параллельных поисков». Кнопка Send уезжает вниз вместе с растущим композером — брать её координату ПОСЛЕ вставки, иначе клик попадёт в пустоту (первый клик так и пропал).
- **Mistral Le Chat** (chat.mistral.ai) — шестая рельса с 05.08.2026 («добавь мистраль шестой рельсой»). Взят вместо третьей китайской осознанно: GLM/Qwen/DeepSeek делят корпус и источники, Le Chat тянет европейские — веер растёт независимостью мнений, а не количеством. ДР-режим в Le Chat = **Deep Research** в панели инструментов композера (рядом с веб-поиском); модель — самая умная из доступных.
  - ✅ **ДВЕРЬ ОТКРЫТА С 26.08.2026** (замер, не claim): первый боевой прогон 6-й рельсы — `DR26-08-25-HUB-03-2301/results/mistral.md`, **40 168 б, 26.08 07:11**, хаб. Аккаунт оператор завёл, вход дальше ведётся самостоятельно.
  - ⚠️ **НО КАЧЕСТВО ЛЕГИ НЕ ДОКАЗАНО**: в том же заказе mistral вернул **0 проверяемых ссылок** — тело есть, разведки в нём нет. Перед синтезом гонять `dr_leg_gate.py --strict`: такая лега в кворум СБОРА входит, в кворум ПОДТВЕРЖДЕНИЯ — нет ([[quorum-is-a-counter-not-proof]]).
  - 🔑 Вход = Google SSO под `[EMAIL]` (та же почта, что у ChatGPT и claude.ai), пароль подаёт САМ Chrome. Локаторы Deep Research в композере до сих пор **по документации, не по замеру** — дописать с первого живого прогона с этого узла.
  - 📜 ИСТОРИЯ (не стирать): с 05.08 по 26.08 здесь стояло «аккаунта нет» — верный на день замера и протухший через 3 недели; 21 день строка врала всем узлам. Запрет тоже claim и протухает ([[ban-is-a-claim-recheck-before-workaround]]).
- Вставка промпта — ТОЛЬКО через JS, НИКОГДА `computer type` (каждый Enter = отправка, улетит обрезок, квота сгорит). ⭐ **Каскад `paste_verify.js`** (рядом со скиллом, от NODE-0X 07-16, лечит брак 07-10 «execCommand не сел»; форевер-фикс Grok-ProseMirror 07-17 FLEE-03): прочитать файл `~/.claude/skills/dr-fanout/paste_verify.js`, выполнить его тело через `javascript_tool`, затем `window.__drPasteVerify(PROMPT, "chatgpt"|"gemini"|"grok")`. Он сам перебирает методы (⭐ **синтетический paste-event для ProseMirror/TipTap** → execCommand → нативный React-сеттер textarea → node-параграфы Quill/CE → directSet), сверяет length+head+tail после КАЖДОГО (для ProseMirror читает `el.innerText`, а НЕ textarea-зеркало) и возвращает `{ok, method, gotLen, wantLen, isPM, ...}`.
  - ⚠️ **Grok 4.5 = TipTap/ProseMirror contenteditable** (`div.tiptap.ProseMirror`), а видимый `<textarea>` — это СКРЫТОЕ ЗЕРКАЛО: заполнение textarea (nativeSetter) даёт `ok:true`, но форма/React из зеркала НЕ обновляются → Submit-кнопка не рендерится, Enter=no-op, ран не стартует. **Настоящий редактор надо заполнять синтетическим paste-event** (`ClipboardEvent('paste',{clipboardData:DataTransfer})`) → ProseMirror штатно адоптит текст → `button[type="submit"]` появляется enabled → клик. Каскад теперь целит ProseMirror ПЕРВЫМ и делает это сам; textarea оставлен последним фолбэком.
  - Ручной фолбэк (если ассет недоступен): для Grok/ChatGPT — `const ed=document.querySelector('.tiptap.ProseMirror')||document.querySelector('.ProseMirror'); ed.focus(); window.getSelection().selectAllChildren(ed); const dt=new DataTransfer(); dt.setData('text/plain',PROMPT); ed.dispatchEvent(new ClipboardEvent('paste',{clipboardData:dt,bubbles:true,cancelable:true}))`; Gemini (Quill+TrustedHTML CSP) — `<p>`-параграфы через `createElement`/`textContent` + `dispatchEvent(new InputEvent('input'))`.
- Путь исполнения по вендору — гибрид (см. п.6 «что решено»): **Grok = живой Chrome-MCP**; **Gemini/ChatGPT = живой Chrome-MCP сейчас, выделенный Firefox-профиль для безлюдного расписания** (фундамент HUB-01).

### СОСТОЯНИЕ 2 — PROBE (доказать до траты квоты)  ⭐ сердце v2
НЕ жать Send, пока три проверки не зелёные:
1. **Режим включён:** на странице видна активная плашка Deep research / Expert (read_page/screenshot подтверждает, а не память). ⭐ **GLM = ДВА факта разом: `Advanced Search` ON И в композере читается `Deep Think  Max`** (dev 31.08 — «не забывай включать Deep Think на Max» + «это тоже должно быть ВКЛЮЧЕНО ADVANCED SEARCH», оба со скриншотами). Глазами не судим — есть ПРИБОР:
   ```bash
   python3 ~/.claude/scripts/glm_probe.py js     # → инъекция в javascript_tool, вернёт JSON-вердикт
   python3 ~/.claude/scripts/glm_probe.py verdict '<этот JSON>'   # exit 0 = Send можно, 3 = нельзя
   ```
   Судья пересчитывает всё сам и поле `ok` из браузера игнорирует; fail-closed — «не прочитал» = запрет (меню глобуса закрыто → открыть и прогнать probe снова). exit 3 и не чинится → рельса `glm` в `missing`.
2. **Промпт целиком:** вердикт = `ok` от `__drPasteVerify` (length + head + tail сверены каскадом). `ok:false` → каскад сам перебирает методы; 2 неудачи подряд → пропустить вендора, квота цела, пинг в леджер. (Ручная проверка без ассета: `editor.innerText.length` ≈ длине И совпали первые/последние ~60 символов.)
3. Только теперь Send/Run.
Затем **доказать старт** (иначе «отправил» ≠ «пошёл»):
- ChatGPT: план/«starting research»/счётчик источников растёт.
- **Gemini ДВУХФАЗНЫЙ:** сперва генерит план и ЖДЁТ кнопку «Start research» — ОБЯЗАТЕЛЬНО дожать, иначе ресёрч не начнётся. Подтверждение: «Great, I'm on it… Researching N websites».
- Grok: «Researching…»/searched web N results.
- Старт не подтвердился за 2 попытки-с-переосмотром → НЕ перезапускать вслепую (жжёт) → пометить в леджере `probe-failed`, пропустить вендора, доложить.

### СОСТОЯНИЕ 3 — LEDGER (сразу после старта каждого вендора)
Записать/дополнить `$OBSIDIAN_ROOT/_drafts/DR-FANOUT-<DR-ID>-<slug>.md`: тема · промпт целиком · время старта · по вендору {started|skipped+причина|probe-failed} · URL вкладки. Это единственная страховка от «забыли забрать» при безлюдном прогоне — коллектор (см. ниже) работает по этому файлу.

### СОСТОЯНИЕ 3.5 — ДОЛОЖИТЬ оператору: промпт + ССЫЛКИ (обязательно, dev 17.07)
Как только вендор перешёл в `started` — **сразу в диалог оператору, не дожидаясь отчёта**: полный текст промпта блоком ```text``` (paste-ready) + строка `🔗 <vendor>: <url>` на КАЖДЫЙ стартовавший чат. Живая сессия → в ответ; безлюдный прогон → в TG-03 через `bus_send.py`.
- URL брать из того же снимка вкладки, что и probe (`tabs_context_mcp` / `page.url`) — он уже содержит id чата.
- **Ссылка = приватный URL чата** (`chatgpt.com/c/…` · `gemini.google.com/app/…` · `grok.com/chat/…` · `claude.ai/chat/…` · `chat.z.ai/c/…`). ⛔ Публичный share-линк (`/share/…`, `g.co/gemini/share/…`) — это ПУБЛИКАЦИЯ наружу (индексировалось Google), только по явной просьбе оператора.
- Не снял URL → сказать честно, с причиной; молча пропустить нельзя.
- Зачем: оператор смотрит с телефона и забирает результат сам по этой ссылке — она его точка входа. Канон: `reglament-vneshniy-resech-vsegda-promt-i-ssylka-v-chat`, память [[dr-prompt-paste-in-chat]].

### СОСТОЯНИЕ 4 — COLLECT (через ~20-40 мин, по леджеру)

> ⭐ **ПЕРЕД ЛЮБЫМ «Chrome-MCP недоступен» — ОДНА КОМАНДА (замер 06.08.2026, хаб, DR26-08-06-HUB-01-1055).**
> `Claude in Chrome is not connected` и пустой `list_connected_browsers` в 1 случае из 1 означали,
> что **Chrome просто не запущен**: `Get-Process chrome` → 0. Лечение: `Start-Process
> "C:\Program Files\Google\Chrome\Application\chrome.exe"` → подождать ~12 с → `tabs_context_mcp`.
> Расширение подключилось, все 4 тела веера снялись подряд за ~5 минут.
> **Цена не проверки:** параллельная сессия записала в реестр «chatgpt: тело не снято, Chrome-MCP
> не подключён», подняла лишнее замещающее плечо через Codex CLI и оставила в реестре строку
> «рельса недоступна», которая переживёт сессию. Ноль процессов ≠ мёртвая рельса
> ([[dead-verdict-expires]], память `chrome-mcp-dead-check-process-first`).
> Chrome ЖИВ, а расширение молчит → вот это настоящая поломка, тогда Firefox/эскалация.

> ⛔⛔ **ПЕРВОЕ, ЧТО ЧИТАЕШЬ ПЕРЕД БРАКОВКОЙ (замер 04.08, ZB-04 — я сам на этом попался).**
> **Строка `Research completed in Nm · 0 citations` НЕ ЯВЛЯЕТСЯ ДОКАЗАТЕЛЬСТВОМ ПУСТОГО РАНА.**
> 04.08 я забраковал ChatGPT-ран по этой строке, написал файл-вердикт `dead` — а потом
> достал backend и получил **35 citations · 34 рабочих URL · тело 17 622 симв.** Отчёт был
> живой и полный. Файл-вердикт пришлось удалять, заметку синтеза — переписывать дважды.
> **Ни один вендор не бракуется, пока не прочитан МАШИННЫЙ признак** (ChatGPT — `citations`
> из `widget_state`; Grok — «N sources»; Gemini — список источников). Нет доступа к признаку =
> статус `not-collected` («не смог прочитать»), **а НЕ `dead`** («вендор не работал»).
> Это два разных факта, и путать их — врать в данных.
>
> ✅ **ДОЛГ ЗАКРЫТ ЗАМЕРОМ 04.08 — и он оказался хуже, чем я предполагал.**
> Перепроверены ВСЕ забракованные по счётчику прогоны волны ZB, у которых в леджерах остался
> chat-URL. **4 из 4 — живые отчёты с источниками, выброшенные не глядя:**
>
> | DR | прежний вердикт | по backend | тело |
> |---|---|---|---|
> | ZB-01 sci-fi (26.07) | `dead` ×2, «таблица целиком ИЗ ПАМЯТИ» | **57 citations** | 15 162 |
> | ZB-02 Харари (26.07) | `dead` ×2, «отчёт из памяти» | **106 citations** | 25 423 |
> | ZB-03 пантеон (26.07) | канал `dead`, ушли в обход через Web search | **52 citations** | 22 828 |
> | ZB-04 HackerNoon (28.07) | `dead`, «в синтез НЕ берём» | **108 citations** | 18 185 |
>
> У ZB-01 ChatGPT-вендора в волте не было ВООБЩЕ — веер шёл двумя вендорами вместо трёх.
> Все четыре подняты и лежат в `_originals` с пометкой `recovered_from`.
> **Вывод жёстче прежнего:** ноль в счётчике не значил ничего ни разу. Единственный признак —
> `citations` из backend. Формулировку «рельса ChatGPT DR сломана системно» из старых леджеров
> не цитировать: она построена на приборе, который сам не проверяли.
DR думает 10-40 мин. По каждой started-вкладке: готов → извлечь (лестница ниже) → сохранить **verbatim** в `$OBSIDIAN_ROOT/_originals/deep-research/<DR-ID>-<slug>-<vendor>.md` (провенанс сверху: source/topic/date/origin) → `dr_registry.py update <DR-ID> --status collected --file "<путь>"`. ⭐ **ГЕЙТ ДОКАЗАТЕЛЬСТВА РАБОТЫ (21.07, DR26-07-21-HUB-02; ⚠️ ПЕРЕСМОТРЕН 04.08 — см. ниже):** перед сохранением прочитать доказательство прогона — Grok: «N sources» + «Thought for…»; Gemini: список источников; **ChatGPT: НЕ строку над виджетом.** Она у DR-виджета врёт: «0 citations · 0 searches» стоит у ВСЕХ connector-прогонов этого аккаунта, в том числе у тех, чьи отчёты мы приняли и использовали (21.07 HUB-02) — в backend'е у них 40–106 живых цитат. Настоящее доказательство ChatGPT-DR = `mapping[*].message.metadata.chatgpt_sdk.widget_state` → `JSON.parse` → `report_message.metadata.citations.length` (и `resolved_model_slug` там же). Пусто/0 цитат в citations → `dead`; ненулевой массив → искал, каким бы ни был счётчик. Для Grok/Gemini прежний порядок в силе: нет источников → `dead`, не `collected`. Не готов → отметить, вернуться позже. Безлюдный режим: ночной `dr_collect.py` (хаб) сам подхватит DR-ID из истории/Downloads и флипнет статус — ручной сбор нужен, только если отчёт нужен СЕЙЧАС.

**Фолбэк-лестница извлечения** — общий порядок (консенсус DR): **официальный export/share → backend JSON → DOM-scrape → эскалация человеку**. DOM — низший приоритет, не первый. Далее по вендорам:
- **ChatGPT** (отчёт в КРОСС-ДОМЕННОМ sandbox-iframe `connector_openai_deep_research` — JS туда не лезет, синтет-клики игнорит):
  1. **Backend JSON (основной, без кликов, ✅ 2026-07-14):** page-JS `s=await fetch('/api/auth/session').then(r=>r.json()); conv=await fetch('/backend-api/conversation/<id>',{headers:{Authorization:'Bearer '+s.accessToken}}).then(r=>r.json())` → Blob-download JSON → на диске Python: `mapping[<node>].message.metadata.chatgpt_sdk.widget_state` (JSON-строка → `json.loads`) → `report_message.content.parts[0]`. Узел = walk по «Executive Summary».
  2. **Без widget_state** (часть DR, ✅ DR26-07-11-HUB-02): отчёт прямо в `mapping[*].message.content.parts[0]` — walk по mapping, самая длинная строка >3000 симв.
  3. ⚠️ **РЕГРЕССИЯ 04.08: «Export to Markdown» синтет-кликом БОЛЬШЕ НЕ РАБОТАЕТ (ZB-04).** Меню по координатному клику открывается, но клики по ПУНКТАМ меню не доходят: меню остаётся открытым, Escape его не закрывает, `Copy contents` не меняет буфер (проверено сентинелом), `Export to Markdown` не создаёт файл (проверено `ls Downloads` ×3). Меню живёт в кросс-доменном iframe, куда синтет-клики не проходят. **Не тратить на этот путь больше одной попытки — путь 1 (backend JSON) 04.08 отработал с первого раза на том же самом чате.** Ниже — прежнее описание пути на случай, если UI откатят:
  3-бис. ⭐ **Меню виджета «Export to Markdown» — работало синтет-кликом, безлюдно (✅ 2026-07-17, HUB-06; ❌ 04.08 — см. выше):** новый connector-формат DR не отдаёт widget_state ВООБЩЕ (пути 1-2 мертвы) и невидим для find/accessibility-tree → только КООРДИНАТНЫЙ клик: иконка download в шапке виджета (правый верх, рядом с expand) → меню `Copy contents / Export to Markdown / Export to Word / Export to PDF` → **Export to Markdown** → `deep-research-report.md` в Downloads (проверить `ls`!) → переложить в `_originals` с провенансом. Человека звать НЕ нужно.
  4. ⚠️ **Rate-limit врёт молча:** при «Too many requests» backend отдаёт mapping БЕЗ widget_state → выглядит как «отчёта нет», хотя отчёт готов и виден на экране. «Пусто из API» ≠ «нет отчёта» → сверься со СКРИНШОТОМ до вывода, подожди пару минут.
  5. ⚠️ Открывать `iframe.src` отдельной вкладкой БЕСПОЛЕЗНО — песочница пустая, контент прилетает через postMessage.
- **Gemini:** отчёт в `STRUCTURED-CONTENT-CONTAINER` (канвас, same-origin) → `innerText` узла с заголовком → Blob-download → фолбэк: рендер в `<pre>` + get_page_text.
- **Grok:** отчёт в основном потоке → `document.querySelector('main').innerText`, отрезать эхо-промпт и хвост-подсказки → Blob-download. ⭐ Якорь обрезки: **«Thought for…» надёжнее первого «Executive Summary»** (проверено на прогоне FLEE-01 — экстракт зацепил эхо промпта).
- **Общий на всех:** большой текст мимо обрезки дисплея (JS-тул режет ~1500, get_page_text ~50k/проход) → Blob-download → Read из Downloads. ⚠️ **Blob-download может ТИХО не долететь** (2026-07-14: grok — да, chatgpt/gemini — нет; `a.click()` без ошибки, блок невидим) → ВСЕГДА `ls Downloads` после; не долетело → фолбэк `pre.textContent=txt; document.body.replaceChildren(pre)` (TrustedHTML-safe) → get_page_text кусками. Клипборд-пути (navigator.clipboard виснет; execCommand/Ctrl+C нужен жест) — НЕ тратить попытки.
- ⭐ **Полевое подтверждение 2026-07-21 (добор веера 14.07, 5 отчётов 16–85 KB — Blob НЕ долетел ни разу, Chrome multiple-downloads):** дефолтом сразу бери `get_page_text`, Blob не пробуй. Что нового узнали: (а) вывод >50 KB харнес САМ персистит в `tool-results/toolu_*.json` на диск → читаешь Read'ом, контекст не жжёшь; <50 KB приходит in-band; (б) жёсткий кап 50000 симв/проход обходится сдвигом окна видимого текста (паддинг/подмена узлов) + склейкой двух срезов по overlap последних ~300 симв — так собран отчёт 77k; (в) клипборд не просто «виснет», он отдаёт СТАРОЕ содержимое буфера оператора = ложный успех, всегда сверяй длину и первые слова; (г) **поиск чата в Grok по названию** — не UI (Ctrl+K мёртв, OneTrust-баннер ест клики), а same-origin `fetch('/rest/app-chat/conversations?pageSize=50',{credentials:'include'})` → `{conversations:[{conversationId,title}]}`; (д) **Gemini = SPA**: свежий `navigate` на URL чата грузит отчёт надёжнее синтетического клика по сайдбару (сайдбар лениво рендерит пустой текст); (е) возврат сырых заголовков чатов из JS ловит контент-фильтр (`BLOCKED: Cookie/query string`) → возвращай короткий статус-токен, не данные.
- ⭐ **Полевое подтверждение 2026-07-21 ВЕЧЕР (сбор HUB-02):** (а) **вброшенная на страницу СВОЯ кнопка не обходит запрет жестов** — синтетический/координатный клик по ней не считается user gesture, blob так и не качается (onclick-счётчик = 0; не изобретать заново); (б) **клики и клавиши расширения могут вообще не доходить до страницы** (окно без фокуса): симптом — Send нажат, а поле ввода не пустеет; лечение — программный `document.querySelector('button[data-testid="send-button"]').click()` из JS, React принимает его как настоящий (проверено: сабмит ушёл, композер опустел); (в) большой текст из DOM — сперва в копилку `window.__x`, offsets искать вторым вызовом, резать уже в Python из персиста `tool-results\`; (г) выделение узла Range+addRange и Ctrl+C поверх — буфер остаётся ПУСТ (не путать со «старым содержимым»: и такое, и такое бывает — потому `Get-Clipboard` сверять всегда).
- ⭐⭐ **Blob-download у ChatGPT: ОДНА ЗАГРУЗКА = ОДНА СВЕЖАЯ ВКЛАДКА (замер 04.08, аудит 4 отчётов).** Первый `a.click()` в новой вкладке скачивается всегда; **второй и последующие в ТОЙ ЖЕ вкладке молча не долетают** — это Chrome «multiple automatic downloads», блок тихий, ошибки в JS нет, `ls Downloads` пуст. Лечение дешёвое и надёжное: `tabs_create_mcp` → `navigate` на chatgpt.com → одна загрузка → следующая вкладка. Проверено: 4 отчёта, 4 вкладки, 4 файла. ⛔ Не лечить это перезагрузкой той же вкладки (пробовал — блок держится) и не пытаться отдать текст на локальный приёмник (`fetch` на `http://10.0.0.0` с chatgpt.com **режет CSP**, `Failed to fetch` — путь закрыт, не тратить попытки). ⚠️ На тяжёлых чатах сборка строки и Blob в одном вызове упирается в **CDP-таймаут 45 с** → разбить на два вызова: первый кладёт текст в `window.__H`, второй только качает.
- ⭐ **Полевой замер 04.08 (ZB-04, сбор трёх вендоров с ноута) — рельсы по вендорам разошлись, запомнить раскладку:**
  - **ChatGPT → ТОЛЬКО backend JSON (путь 1).** Отработал с первого раза; всё остальное мертво (см. регрессию выше). ⚠️ Мой промах, чтобы не повторяли: я дёрнул `/backend-api/conversation/<id>` **без заголовка Authorization** → **404**, и прочитал это как «пути нет». 404 тут = «нет токена», а не «нет отчёта». Bearer обязателен: `s=await fetch('/api/auth/session').then(r=>r.json())` → `Authorization:'Bearer '+s.accessToken`.
  - **Gemini → Blob-download РАБОТАЕТ** (`new Blob([document.body.innerText])` + `a.click()`, файл лёг в Downloads с первой попытки, 99 KB). Отменяет прежний совет «Blob не пробуй, сразу get_page_text» — для Gemini он неверен. Тело отчёта попадает в `body.innerText` целиком вместе с хвостом «Sources read but not used» (это ценно — сохранять весь снимок).
  - **Grok → Blob и data-URI НЕ работают** (CSP режет, `a.click()` молча без файла), `navigator.clipboard.writeText` → **CDP-таймаут 45 с**. Работает `get_page_text` — забрал весь отчёт одним проходом.
  - **Чтение больших срезов через JS ловит контент-фильтр:** `body.innerText.slice(a,b)` на странице с URL-ами вернул `[BLOCKED: Cookie/query string data]`. Короткие статус-выражения (`.length`, `.indexOf`) проходят. ⇒ **данные тащить файлом/`get_page_text`, а не возвратом из JS.**
  - **Буфер обмена — общий на машину и врёт (§3.6):** после «копирования» в нём лежал чужой текст из параллельной сессии. Лечение, которое сработало: **писать сентинел ДО** (`SENTINEL-...`) и сверять после — иначе «успешная» копия неотличима от невыполненной.
- ⚠️ **Вендор может ОТКАЗАТЬСЯ отвечать** (Gemini, тема анти-бан аутрича — счёл обходом защит). Отказ = валидный результат: сохранить verbatim в `_originals` как обычный файл, статус `collected`, а в Decision Memo явно пометить «консенсуса нет, база = N вендоров» и не выдавать single-vendor за веер.

## Шаг 4 — синтез-консенсус (Alpha Protocol step 4)

> ⛔ **ГЕЙТ ПЕРЕД ПЕРВОЙ БУКВОЙ СИНТЕЗА (04.08, ZB-04): «а его уже не синтезировали?»**
> Порядок: `dr_registry.py list | grep <DR-ID>` **+** `ls 03-Insights | grep <DR-ID>`.
> - статус `synthesized`/`applied` **или** уже есть `insight-DR-<DR-ID>-*` → **НОВУЮ заметку НЕ создавать.**
>   Дописать в существующую датированный раздел «ПОПРАВКА <дата>: что нового и что это меняет».
> - **⛔ Статус в реестре не понижать.** 04.08 я сбил `applied` → `collected` командой сбора и стёр
>   факт, что DR давно закрыт. Перед `update --status` посмотреть текущий статус: назад по
>   лестнице (`applied` → `collected`) двигаться только осознанно, с `--note` о причине.
>
> Замер цены: у ZB-04 **две** insight-заметки за один час 28.07 от двух сессий, плюс 04.08
> третий веер по уже закрытому DR. Прямое следствие §8.4 (одобрение старше суток исполняется
> только после RECALL «не сделано ли уже») и §7.7 (табличка ON AIR не выставлялась ни разу).

Прочитать все собранные отчёты → таблица «сошлись / разошлись / уникальное у каждого» → Decision Memo (проблема · знания · DR · варианты · риски · рекомендация). Гетеро-принцип: расхождения НЕ сглаживать — показать оператору как развилки. Memo → `02-Decisions/` (если решение) или отчёт в чат. Леджер закрыть (`status: collected`).

⭐ **ВЕНДОРОВ НЕ УСРЕДНЯЕМ — ценность веера в СТОЛКНОВЕНИИ, а не в кворуме (замер волны DR26-07-26).** Три вендора дали трёх РАЗНЫХ победителей, потому что судили по трём разным критериям (замысел · недостающие механизмы · доказанный выход) — и это честнее любого единого рейтинга. Одинаковый ответ трёх вендоров — сигнал СЛАБЫЙ; поймать ОДНОГО вендора на подлоге — сильный.

В синтезе ОБЯЗАТЕЛЬНЫ две секции: **(а) расхождения с указанием КРИТЕРИЯ каждого вендора**; **(б) «прямое опровержение внутри веера»**, если оно было. Усреднить = потерять главное.

Пример 26.07: ChatGPT опроверг цифру Gemini (21x LLM-Wiki против RAG) по первоисточнику — цифра оказалась честной, но приклеенной к чужому объекту.

⭐ **Шаг 5 — ЗАКРЫТЬ РАЗВЕДКУ (dev 27.07, обязателен).** `synthesized` — не финиш: отчёт написан, а система не изменилась. Каждый ДР доводится до одного из двух терминальных статусов, оба требуют `--note`:
- `dr_registry.py update <ID> --status applied --note "<что реально поменяли: Decision Memo / правка в проде / новая рутина>"`
- `dr_registry.py update <ID> --status parked --note "<почему не берём и что изменит решение>"`

`parked` — легальный и честный финал, не поражение ([[gate-implement-critical-only]]: не всё исследованное обязано быть внедрено). Гейт в `dr_registry.py` v3.3 роняет попытку без причины (exit 1). Повод правила: 27.07 в реестре 184 из 246 разведок висели `synthesized`, до `02-Decisions` дошло ~20 — отличить «кормит систему» от «просто лежит» было нельзя. Канон: память [[dr-finish-applied-or-parked]], CLAUDE.md §9.1.

## ⛔ ПОЛЕВЫЕ ДАННЫЕ НОЧИ 26.07.2026 (партия ZB-01…ZB-05, ноут NODE-0X) — читать перед запуском
1. ~~**🔴 ChatGPT Deep Research = `dead` на 26.07, «он просто НЕ ИСКАЛ, отдав таблицу из памяти».**~~ ⛔ **ВЫВОД ОПРОВЕРГНУТ 04.08 разбором backend'а — симптом был реален, причина названа неверно.** Что оказалось на самом деле: (а) счётчик «0 citations · 0 searches» стоит у ВСЕХ 10 DR-прогонов 21–26.07, включая принятые и использованные — он не про поиск, `story_events` у connector-DR всегда пуст; (б) те же «мёртвые» прогоны несут 40–106 цитат с живыми URL в `widget_state.report_message.metadata.citations` (одна проверена вживую на странице-источнике); (в) настоящая деградация другая — `resolved_model_slug: deep-research-mini` у всех прогонов и обрыв посреди плана (шаги 3–5 `pending` при `status: completed`, 5–7 мин вместо 20–40), отсюда мало источников и «красиво, но пусто» на глаз; (г) веб-поиск на аккаунте НЕ выключен (`beta_settings.browsing: true`, `disable_web_search: false`) — усиление промпта не помогало не потому, что вендор не искал. **Правило теперь:** ChatGPT-канал гнать через Pro + Web search (п.10 «что решено»), а если запущен DR-чип — судить по `citations`, а не по счётчику. Retry больше двух раз по-прежнему не жечь.
2. **🔑 Gemini: заходить ТОЛЬКО по имени аккаунта, индекс `u/N` НЕ СТАБИЛЕН.** ⛔ Правка 27.07 (supersedes «всегда `u/7`»): `https://gemini.google.com/u/7/app` открылся под `[EMAIL]` — free-тариф, модель Flash, кнопка Upgrade. Индексы переезжают между сессиями, «мой номер» запоминать нельзя. **Рабочий вход:** `https://gemini.google.com/app?authuser=[EMAIL]` (редиректит на нужный `u/N` сам). Детект аккаунта без кликов, ОБЯЗАТЕЛЬНО до вставки промпта: `document.querySelector('a[aria-label*="Google Account"]').getAttribute('aria-label')` + проверка `document.body.innerText.includes('Upgrade')` (true = free-аккаунт). Без этой сверки отчёт молча уедет на Flash и будет выглядеть просто «слабоватым». Переключатель аккаунтов живёт в кросс-доменном iframe — `find`/скролл его не берут.
3. **Gemini молча откатывает модель на Flash-Lite** в каждой новой вкладке. Смотреть селектор ГЛАЗАМИ перед каждым запуском; Deep research переехал в «+» → **More tools** → «Deep research» (в первом уровне меню его больше нет).
4. **ChatGPT: порядок «чип → промпт», а НЕ наоборот** (supersedes прежняя заметка ZB-02 20.07). Чип «Deep research» — это инлайн-нода ВНУТРИ ProseMirror, встающая по позиции каретки: кликнешь в середину текста — расщепит предложение (ловилось как `chipIdx:470` посреди фразы). Рабочий порядок: (а) включить Deep research в ПУСТОМ композере — чип встаёт первым узлом; (б) поставить каретку в КОНЕЦ (`range.selectNodeContents(ed); range.collapse(false)`); (в) синтетический paste-event — вставка в коллапсированную каретку ничего не заменяет, чип выживает. ⚠️ Повторный paste при `selectNodeContents` НЕ заменяет текст, а ДОПИСЫВАЕТ (получишь удвоение) → чистить только живыми клавишами `ctrl+a` + `Delete`.
5. **Gemini-забор: `querySelector('.markdown-main-panel')` берёт ПЕРВУЮ панель = research-план, а не отчёт.** Сохранишь 1.7 KB плана вместо 33.8 KB отчёта и не заметишь. Правильно: якорь на заголовок отчёта → `h2('ПЛАН ИССЛЕДОВАНИЯ').closest('.markdown-main-panel').innerText`.
6. **Вынос большого текста:** `javascript_tool` режет вывод на ~1000-1500 симв. Единственный рабочий путь — сложить в `window.__R`, СРАЗУ подменить body на `<pre>` и СРАЗУ `get_page_text` (кап ~50k, отчёт 33.8k прошёл одним проходом). Подмена body ломает страницу → `window.__R` теряется при перезагрузке, порядок нарушать нельзя. Blob-download не пробовать (полевые заметки 21.07: не долетает).
7. **«Начать исследование» жать ДВАЖДЫ-с-переосмотром:** первый `find` находит кнопку, но клик приходит раньше, чем она смонтирована. Повторный `find` даёт новый ref — второй клик срабатывает. Доказательство старта = канвас «Starting research…» / «Прекрасно. Вы можете закрыть этот чат», а не факт клика.
8. **🔁 ДЕДУП — на КАЖДОМ вендоре, а не только в реестре.** Инцидент 03:0x: реестр показал ZB-03 = `issued`, дедуп по истории Grok дал «чисто» (похожий чат оказался от 22:49 UTC = ДО создания промптов партии) → запустил. А в Gemini Recents уже висел свой `DR26-07-26-ZB-03` от параллельной сессии → лишний прогон Gemini DR. Реестр = первый фильтр, история КАЖДОГО вендора, куда шлёшь = второй, обязательный. Это [[check-all-places-not-one]], применённое к вендорам вместо дисков.

9. **Корневой композер ChatGPT ОБЩИЙ на все вкладки — свой же черновик поедет за тобой.** 27.07: открыл вторую вкладку под ZB-04 — там лежал ZB-03 из первой; paste-event ДОПИСАЛ (8303 симв. вместо 4175), а `execCommand selectAll+delete` визуально очистил, но ProseMirror восстановил состояние и дописал снова (12450). Лечится только живой клавиатурой: клик в композер → `ctrl+a` → `Delete` → сверить `innerText.length===0` → и лишь потом paste.
10. **`ctrl+a`+`Delete` сносит и ЧИП режима** (Web search / Deep research) — прогон уйдёт без поиска, и это не видно в тексте промпта. Порядок для ChatGPT: очистить → вставить промпт → **включить чип заново** → сверить → Send. И ещё: текст чипа попадает в `innerText` композера то префиксом `Web search\n`, то суффиксом `\nWeb search` → при сверке длины срезать его с ОБОИХ концов, иначе ловишь ложный mismatch и начинаешь «чинить» целый промпт.

## ⭐ ПОЛЕ 31.07.2026 (NODE-0X, DR26-07-29-MACANTON-01-1302) — рельсы вендоров и три молчаливые грабли
0. **ВЫБОР БРАУЗЕРА И АККАУНТА — МОЙ, ВСЕГДА** (dev 31.07, канон `reglament-brauzer-i-akkaunt-vybiray-sam-nikogda-ne-sprashivay`). Три подключённых Chrome → беру сам, не пошёл → следующий, потом Firefox. ⛔ Вопрос «какой браузер/аккаунт взять?» оператору запрещён. Цена нарушения замерена в этот же день: вендор выпал из веера при живом пути.
1. **Рельса Gemini на 31.07 = ТОЛЬКО живой Chrome.** Оба CLI-пути мертвы: бесплатный ключ AI Studio отдаёт 429 (один на весь флот), OAuth — `IneligibleTierError` (Code Assist for individuals закрыт, миграция в Antigravity). Аккаунт Gemini = `dev.a`, НЕ `a2`. Путь в UI: «+» → **More tools** → **Deep research** (в меню первого уровня его НЕТ), затем двухфазность — план → кнопка **«Начать исследование»**, доказательство старта = «Researching N websites…».
2. **⛔ Не клонировать профиль Firefox, который держит живой GUI-браузер.** На диск попадает вчерашний слепок (свежие куки живут в памяти процесса) → селениум видит «Sign in» на сайте, где сессия на самом деле жива. Я сделал из этого вывод «сессия мертва на стороне Google» и он был неверным.
3. **`pbcopy` без UTF-8 локали убивает кириллицу.** Вставка «проходит успешно», в композере мойибаке, длина расходится в 1,5 раза. Всегда `export LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8` перед `pbcopy`, и сверять поле не только длиной, но счётчиком кириллицы: `(t.match(/[а-яА-Я]/g)||[]).length`.
4. **Забор ChatGPT DR:** `widget_state` может быть ПУСТ — отчёт лежит в `mapping[*].message.content.parts[0]` (взять самую длинную строку по ВСЕМУ mapping, а не по цепочке от `current_node`). `body.innerText` про готовность ВРЁТ — держится на ~12 КБ сайдбара, даже когда библиография из 69 источников уже отрисована; готовность проверять СКРИНШОТОМ. И читать первую строку отчёта: «## Продолжение отчёта — с §N» = половина не доехала.
5. **Забор Gemini DR:** отчёт в `structured-content-container` (их несколько — брать самый длинный), надёжнее всего `get_page_text`, харнес сам персистит >50 КБ в `tool-results/*.json`, оттуда режем питоном.
6. **Проверка цитат в ДВА шага, не в один.** (а) все ссылки на код ответа — детерминированно, 0 токенов; (б) **прочитать содержание у 3–5 утверждений, на которых стоит решение**. Замер 31.07: 30/30 ссылок Grok живые, но ссылка ChatGPT на JCR вела на статью про делимость цен, а Grok выдал настройку Zapier за поведение продукта. Писать «цитаты проверены» после одного шага (а) — ложь. [[live-url-is-not-a-verified-citation]]

## ⭐ ПОЛЕ 28.07.2026 (ZB-04-2349, ноут NODE-0X) — транспорт промпта и забор отчёта решены
1. **🔑 ТРАНСПОРТ ПРОМПТА = `window.name`, а не инлайн в javascript_tool.** Промпт 12 КБ инлайном на трёх вендоров = ~37 КБ контекста плюс риск экранирования. Рабочий путь, 0 токенов: `navigate` вкладку на локальный файл промпта → `window.name = await fetch(location.href).then(r=>r.text())` → `navigate` ТУ ЖЕ вкладку на сайт вендора → `window.name` доезжает целиком (проверено 12 224 / 12 279 / 12 467 знаков). Раздача: крошечный HTTP-сервер из скретчпада.
   ⚠️ **Исключение — Gemini:** COOP на `google.com` рвёт browsing context, и при уходе С gemini на localhost `window.name` обнуляется. Обратное направление (localhost → gemini) работает.
2. **🔑 ЗАБОР ОТЧЁТА = POST на локальный сервер, текст в мой контекст не попадает.** Тот же приём наоборот: в чате вендора сложить текст в `window.name` → `navigate` на `http://10.0.0.0:<порт>/sink` → оттуда `fetch('/save?name=raw-<vendor>.txt',{method:'POST',body:window.name})`. Сервер пишет файл, дальше проверяю полноту Python-ом (разделы, число URL) за копейки. Так забраны отчёты 16 КБ / 34 КБ / 83 КБ.
   ⚠️ **Для Gemini** (COOP убивает window.name) работает **фрагмент URL**: `location.href='http://10.0.0.0:<порт>/sink#'+encodeURIComponent(txt)` → на sink-странице `decodeURIComponent(location.hash.slice(1))` → POST. Фрагмент на сервер не уходит, приватность цела.
3. **Что НЕ работает, не тратить попытки:** `fetch` с страницы вендора на 10.0.0.0 (CSP `connect-src` — режут и chatgpt.com, и gemini.google.com) · отправка формой на localhost (CSP `form-action`) · CDP `ctrl+v` (клавиша доходит, вставки нет) · кнопка «Copy contents» в UI (нужен фокус окна, а окно фоновое — буфер молча не меняется; всегда сверять `Get-Clipboard` с сентинелом).
4. **🔴 ChatGPT Deep Research — ПЯТЫЙ подряд `0 citations · 0 searches`** (4 раза 26.07 + 1 раз 28.07, аккаунт `dev.a2@`, 15 минут «думал» и выдал внешне красивый, но пустоватый отчёт — ⚠️ 04.08: «из памяти» неверно, он искал, но урезанно; счётчик врёт, см. п.1 полевых данных). Web search на том же аккаунте и той же модели ищет нормально (90+ запросов, 80+ страниц, 168 URL в отчёте). ⇒ **Не тратить DR-чип на этом аккаунте: ChatGPT-канал вести сразу через Web search** + в тело промпта строку «перечисли выполненные запросы и реально открытые URL перед финальным отчётом». Экономит 15 минут и один прогон.
5. **ChatGPT DR стал ДВУХФАЗНЫМ, как Gemini:** после Send показывает карточку плана с `Edit / Cancel / Start` и автостартом по таймеру ~30 с. Кнопку дожимать.
6. **ChatGPT: `execCommand insertText` сел, синтетический paste-event НЕ сел** — ровно наоборот, чем у Grok (там paste-event с первого раза). Каскад нужен обоим, порядок методов по вендору разный. Чип режима ставить в ПУСТОМ композере, потом каретка в конец, потом вставка — чип выживает.
7. **Gemini: кнопка «Начать исследование» остаётся видимой и enabled после успешного клика.** Доказательство старта — не исчезновение кнопки, а канвас `Прекрасно. Вы можете закрыть этот чат` + `Researching N websites`. И `bodyLen` у Gemini скачет на порядок (327 887 → 14 403 за ре-рендер), как признак старта не годится.
8. **Gemini-забор: брать панель по МАКСИМАЛЬНОЙ длине**, а не первую. На готовом отчёте `.markdown-main-panel` было три штуки: 1861 (план), 144, 34 444 (отчёт). Панель отчёта рендерится лениво — если её нет, кликнуть карточку отчёта в ленте.
9. **Grok Heavy: 485 sources и НОЛЬ инлайн-ссылок.** Источники отданы абзацем с перечнем доменов, анкоров на странице 2. `innerText` ничего не теряет, но проверяемость Grok-фактов низкая — спорные цифры сверять руками (в этом прогоне Grok ошибся: заявил, что платных ускорителей нет, а Story Boost за $159,99 существует).
10. **Два подключённых Chrome в MCP.** Один может быть чистым профилем, разлогиненным везде. Проверять аккаунт (`/api/auth/session` у ChatGPT, `aria-label` у Gemini, `Sign in` в тексте у Grok) ДО вывода «разлогинен, зовите оператора».

11. **⭐ Blob-download на chatgpt.com РАБОТАЕТ — и это единственный способ забрать отчёт целиком (27.07, supersedes полевую заметку 21.07 «Blob не долетает»).** Замер: отчёт 73 144 симв. приехал файлом 97 992 байта, второй — 60 623 симв., оба с первого раза. `get_page_text` для таких объёмов НЕПРИГОДЕН: режет на 50 000 симв. **и отрезает ровно хвост — раздел Proof of work**, то есть само доказательство, что вендор искал. Порядок: собрать текст последнего `[data-message-author-role="assistant"]` в `window.__R` → Blob + `a.click()` → **обязательно `ls Downloads`** → перенести скриптом с провенансом. Контекст сессии при этом не тратится вообще — текст идёт диск-в-диск. ⚠️ Трюк «добить пэддингом до >50 КБ, чтобы get_page_text persist-нул на диск» НЕ работает: тул иногда персистит, а иногда режет инлайном — поведение непредсказуемо, не закладываться.
12. **`exit 0` от `brain_embed_update.py` при занятом локе — НЕ баг и не враньё.** В коде осознанно: `busy_code = 3 if index_age_hours() > STALE_HOURS else 0` (порог 26 ч). Код отвечает на вопрос «индекс протух по часам?», а НЕ «мой запрос выполнился?». После записи новых заметок это разные вопросы: свежий по часам индекс их всё равно не содержит. ⇒ После реиндекса проверять ФУНКЦИОНАЛЬНО — запросом к `brain_ask.py` на фразу, которой нет нигде, кроме новых файлов. Счётчик `harari ×N` в `_brain_e5_meta.pkl` не доказательство: там пути файлов, не текст чанков.

## Ошибки/грабли (не вошедшее в автомат)
- ⚠️ **Фоновая/свёрнутая вкладка Chrome (проверено 2026-07-17):** viewport 0×0, layout заморожен → синтетические JS-клики и Radix/Angular-кнопки (Gemini «Start research», ChatGPT «+»-меню) НЕ срабатывают, а `computer` кликает мимо. Лечение: `tabs_create_mcp` → новая вкладка (получает layout даже в фоновом окне) → открыть тот же URL разговора → `find` → `computer left_click ref` (CDP-trusted). Промпт при этом уже отправлен — теряется только «дожать кнопку», не квота.
- ⭐ **«started» в леджере ≠ реально запущено (инцидент HUB-06, 16→17.07):** три вендора помечены started, по факту работал ОДИН. Gemini висел на непрожатой кнопке «Start research» (страница = только промпт, panel=0), Grok вообще не отправлен (path остался `/`, промпт в композере). Потеряна ночь. → **probe-after-start обязателен и доказателен:** path сменился на /chat/ · виден индикатор прогресса · объём страницы вырос. Вставка ≠ отправка; отправка ≠ старт. Состояние `submitted` без подтверждённого `started` = не started.
- ⭐ **ChatGPT DR останавливается на research-плане (проверено 2026-07-20, ZB-02):** первый ран (~12 мин, «0 citations · 0 searches») может выдать ТОЛЬКО research-план + output-structure, БЕЗ настоящего ресёрча, и завершиться (`finished_successfully`, end_turn). Это НЕ баг вставки/старта — ран реально шёл, но выродился в план. Лечение: follow-up в тот же чат «Proceed now: execute this plan and write the FULL final report… Do not stop at the plan» → второй ран (у нас 65 мин) даёт полный отчёт с живыми URL. При сборе: если backend-JSON longest-part начинается с «Research Plan:» и в mapping только один widget с планом — это план, не отчёт; пнуть, не сохранять как collected. (Gemini/Grok этим не страдают — план у Gemini отдельная фаза с кнопкой.)
- ⚠️ **Плашка DR-режима ChatGPT живёт ВНУТРИ редактора (ZB-02, 20.07):** каскад `paste_verify` (directSet/execCommand) чистит редактор и СТИРАЕТ чип «Deep research» → probe покажет `chip:false`. Порядок: сначала вставить промпт, ПОТОМ включить Deep research поверх (меню «+» → Deep research), затем сверить чип и Send. Иначе улетит обычный чат, квота DR цела но ответ не тот.
- ✅ **Grok, зеркало textarea/contenteditable — КОРЕНЬ найден и вылечен (FLEE-03, 17.07):** Grok 4.5 = TipTap/ProseMirror contenteditable (`div.tiptap.ProseMirror`); видимый `<textarea>` — СКРЫТОЕ зеркало. Заполнение textarea (nativeSetter/value+InputEvent) даёт `ok:true`, но React/PM-состояние из зеркала не обновляется → Submit не рендерится, Enter=no-op (ровно это жгло время 07-10 и 07-17). **Фикс в каскаде:** целить `.tiptap.ProseMirror` ПЕРВЫМ + синтетический paste-event (`ClipboardEvent('paste',{clipboardData:DataTransfer})`) → PM адоптит текст → `button[type="submit"]` появляется enabled → клик. Проверено вживую 17.07 (FLEE-03 Grok `/c/e621f761`). Если UI снова уплывёт и paste-event не сработает → новый чат + probe, не жечь время.
- ⭐ **«ChatGPT DR молча не ищет» — симптом реален, диагноз был ложный (заведено 26.07, вскрыто 04.08).** Счётчик «Research completed in Xm · 0 citations · 0 searches» — сломанная телеметрия connector-DR, а не отчёт о поиске: он одинаково нулевой у прогонов с 40–106 цитатами. Что делать при виде нуля: (1) НЕ объявлять канал `dead` по счётчику — открыть backend `widget_state.report_message.metadata.citations` (`resolved_model_slug` рядом); (2) не гнать «усиленный» повтор — усиливать нечего, вендор искал; (3) реальная слабость канала = `deep-research-mini` + обрыв посреди плана → ChatGPT ведём через Pro + Web search (замер: 73 запроса / 31 страница против 12 URL у mini). Правило «два `dead` подряд = не гнать третий раз тем же способом» остаётся, но `dead` теперь ставится по цитатам, не по счётчику. Урок шире DR: индикатор, по которому мы объявляем что-то мёртвым, сам обязан быть проверен — [[prichina-kak-claim]].
- ⭐ **Корневой композер `chatgpt.com/` — общий на аккаунт и его рвут параллельные сессии (26.07.2026).** Черновик синкается между сессиями: за один прогон там побывали чужие `ZB-05` и `ZB-06`, мои вставки соседняя сессия откатывала своим React-состоянием, а один раз моя строка успела прилипнуть в хвост ЧУЖОГО промпта (вычистить не удалось — правки не держались). ⛔ Правило: при работе в параллель **не трогать корневой композер**; вести прогон внутри СВОЕГО `/c/<id>` (композер пер-чатовый, не оспаривается), новый чат создавать только когда корневой пуст. Перед вставкой всегда читать композер: непустой + чужой ID = стоп, а не «перезапишу».
- Разлогин посреди ресёрча → отчёт может потеряться: после логина проверить историю чатов вендора, DR обычно сохраняется в истории.
- Длинный отчёт обрезается в get_page_text → прокрутить/раскрыть («Show more») перед чтением; сверить конец текста с концом отчёта.
- ⛔ Никогда не заводить ПЛАТНЫЙ API-путь как «фолбэк» без согласования ([[prefer-included-limits-before-paid-api]]).
- Один и тот же промпт всем вендорам ДОСЛОВНО, кроме намеренного платформенного блока §2/§3/§4 (иначе консенсус грязный).
- ⚠️ **Аккаунт может флагнуть автоматизацию:** на прогоне FLEE-01 ChatGPT показал баннер «Suspicious activity detected» при старте DR из автоматизации (НЕ заблокировал, ресёрч пошёл). Это ровно тот failure-mode, что предсказали оба DR-вендора. Увидел баннер → не паниковать и не долбить ретраями; отметить в леджере, продолжать. Повторяется системно → `drift_suspected`, доложить оператору.
- ⚠️ **Session longevity никто не публикует** (консенсус DR) → forced re-auth считать НЕИЗБЕЖНЫМ, не строить на таймере. `needs_reauth` = первоклассное состояние + пинг человеку out-of-band (02/QQQ).
- ⏳ **Полностью безлюдный ЗАПУСК** — следующий шаг стройки (архитектура известна из DR: ledger-FSM + выделенный Firefox-профиль + cron/systemd; старт с ChatGPT+Gemini). Пока безлюден только СБОР (ночной `dr_collect.py`); запуск требует живой сессии с браузером. Дыра осознана, закрывается после решения оператора по «дежурной браузер-сессии на хабе».

## /tt — как проверить v2 (после прихода FLEE-01 или при правке)
Не гонять живой DR ради теста (жжёт квоту). Проверять по частям: (1) probe-логика — на уже открытой вкладке проверить, что детект режима+длины работает БЕЗ Send; (2) извлечение — на УЖЕ собранном прошлом DR (backend JSON / innerText) прогнать парсер, сверить с сохранённым `_originals`; (3) леджер+dr_collect — прогнать на существующем DR-ID. Живой end-to-end — только когда реально нужен ресёрч.


ARGUMENTS: DR26-09-04-HUB-01-2323

---

**Claude:**

Now let me check the browser rail availability before dispatching.

---

> `Bash` -- {"command": "powershell -NoProfile -Command \"Get-Process chrome -ErrorAction SilentlyContinue | Measure-Object | Select-Object -ExpandProperty Count\" 2>&1; echo \"--- firefox ---\"; powershell -NoProfile -Command \"Get-Process firefox -ErrorAction SilentlyContinue | Measure-Object | Select-Object 

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers,mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__javascript_tool,mcp__claude-in-chrome__read_page,mcp__claude-in-chrome__tabs_create_mcp,mcp__claude-in-chrome__find,mcp__claude-in-chrome__c

---

**Claude:**

Chrome is running (17 processes). Checking MCP connection.

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

**Claude:**

One local Chrome. Now preparing the tuned prompt (ID header + universal add-on).

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; ls -la \"$V/08-Templates/dr-platform-playbook.md\" 2>&1; echo \"=== §1 UNIVERSAL ===\"; sed -n '/§1/,/§2/p' \"$V/08-Templates/dr-platform-playbook.md\" 2>&1 | head -60", "description": "Read universal DR add-on"}

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_67bb72e4/scratchpad\"; mkdir -p \"$SC/dr\"; SRC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_6eeb47ad/scratchpad/dr-playwright-pr

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; sed -n '/^## §2\\./,/^## §5\\./p' \"$V/08-Templates/dr-platform-playbook.md\" | grep -n \"^```\" | head; echo \"=== BLOCKS ===\"; awk '/^## §2\\./,/^## §5\\./' \"$V/08-Templates/dr-platform-playbook.md\" | sed -n '1,200p' | grep -v \"^>\" | head -120",

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; awk '/^## .2\\./,/^## .5\\./' \"$V/08-Templates/dr-platform-playbook.md\" | head -130", "description": "Extract vendor platform blocks"}

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; grep -n \"^## \" \"$V/08-Templates/dr-platform-playbook.md\"", "description": "List playbook sections"}

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; sed -n '80,180p' \"$V/08-Templates/dr-platform-playbook.md\"", "description": "Read vendor blocks 2-5"}

---

**Claude:**

Now building the six per-vendor prompt files.

---

> `Bash` -- {"command": "SC=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_67bb72e4/scratchpad/dr\"; B=\"$SC/base.md\"\ncat \"$B\" > \"$SC/grok.md\"; cat >> \"$SC/grok.md\" <<'EOF'\n\nGROK-SPECIFIC:\n- Use your deepest research mode (maximum iterations). Sear

---

**Claude:**

Six prompts ready. Starting the local transport server.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_67bb72e4/scratchpad/dr\" && (python -m http.server 8791 --bind 10.0.0.0 >/dev/null 2>&1 &) ; sleep 2; curl -s -o /dev/null -w \"%{http_code} \" http://10.0.0.0:8791/base.md; curl -s 

---

> `mcp__claude-in-chrome__tabs_context_mcp` -- {"createIfEmpty": true}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_1367eb44, "url": "https://grok.com"}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "wait", "duration": 3}}, {"name": "javascript_tool", "input": {"tabId": id_1367eb44, "action": "javascript_exec", "text": "JSON.stringify({url:locat

---

**Claude:**

Grok is logged in. Loading the prompt via `window.name` transport.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_1367eb44, "url": "http://10.0.0.0:8791/grok.md"}}, {"name": "javascript_tool", "input": {"tabId": id_1367eb44, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); JSON.stringify({len:window.name.length

---

> `mcp__claude-in-chrome__read_page` -- {"tabId": id_1367eb44, "filter": "interactive", "max_chars": 4000}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_1367eb44, "action": "left_click", "ref": "ref_31"}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "wait", "duration": 1}}, {"name": "read_page", "input": {"tabId": id_1367eb44, "filter": "all", "max_chars": 3000}}]}

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_1367eb44, "query": "model option Heavy / Expert / Fast in model selector menu"}

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_1367eb44, "action": "screenshot"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_1367eb44, "action": "left_click", "coordinate": [1144, 271]}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "wait", "duration": 1}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "screenshot"}}]}

---

**Claude:**

Menu open. Selecting Heavy.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_1367eb44, "action": "left_click", "coordinate": [1041, 413]}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "screenshot"}}]}

---

**Claude:**

Heavy selected. Now the paste cascade.

---

> `Bash` -- {"command": "wc -c ~/.claude/skills/dr-fanout/paste_verify.js 2>&1; head -c 600 ~/.claude/skills/dr-fanout/paste_verify.js", "description": "Read paste_verify asset size"}

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_1367eb44, "action": "javascript_exec", "text": "const P = window.name;\nconst ed = document.querySelector('.tiptap.ProseMirror') || document.querySelector('.ProseMirror');\nif(!ed) { JSON.stringify({err:'no editor', hasTextarea: !!document.querySelector('textarea')}) } else {\ned.focus();

---

**Claude:**

Paste verified (head/tail match, cyrillic 40/40). Sending.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_1367eb44, "action": "javascript_exec", "text": "const b=document.querySelector('button[type=\"submit\"]');\nif(!b){ JSON.stringify({err:'no submit btn'}) } else { const dis=b.disabled; b.click(); await new Promise(r=>setTimeout(r,3000)); JSON.stringify({wasDisabled:dis, url:location.href,

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_1367eb44, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({tail:t.slice(-350), thinking:/Think|Search|source|Research/i.test(t.slice(-2000))})"}

---

**Claude:**

✅ **Grok started** — Heavy swarm running: `grok.com/c/s_8d4cabcc`. Next rail: GLM.

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_eeb90dde, "url": "http://10.0.0.0:8791/glm.md"}}, {"name": "javascript_tool", "input": {"tabId": id_eeb90dde, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); window.name.length"}}, {"name": "naviga

---

**Claude:**

GLM logged in as `dev`. Reading composer state with the probe.

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_eeb90dde, "action": "screenshot"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_eeb90dde, "action": "left_click", "coordinate": [1145, 136]}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "wait", "duration": 1}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "left_click", "coordinate": [331, 26

---

**Claude:**

Model GLM-5.3, Deep Think already Max. Checking the model list for anything smarter.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_eeb90dde, "action": "left_click", "coordinate": [371, 26]}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "wait", "duration": 1}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "screenshot"}}]}

---

**Claude:**

GLM-5.3 is the flagship. Now enabling Advanced Search under the globe.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_eeb90dde, "action": "key", "text": "Escape"}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "left_click", "coordinate": [581, 411]}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "wait", "duration": 1}}, {"name": "

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_eeb90dde, "action": "left_click", "coordinate": [581, 411]}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_eeb90dde, "action": "screenshot"}}]}

---

**Claude:**

Globe now enabled (blue). Running the deterministic probe to verify Advanced Search state.

---

> `Bash` -- {"command": "python ~/.claude/scripts/glm_probe.py js 2>&1 | head -c 3000", "description": "Get GLM probe JS"}

---

> `Bash` -- {"command": "ls ~/.claude/skills/dr-fanout/ 2>&1; echo \"--- find glm_probe ---\"; find ~/.claude -name \"*glm_probe*\" 2>/dev/null; find \"D:/Vault/_imports\" -name \"*glm_probe*\" 2>/dev/null | head", "description": "Search for glm_probe across locations"}

---

**Claude:**

`glm_probe.py` (the judge) is missing on this node — only the `.js` asset exists. Reading the composer directly instead.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_eeb90dde, "action": "javascript_exec", "text": "const form=document.querySelector('form')||document.body;\nconst btns=[...form.querySelectorAll('button')].map(b=>({al:b.getAttribute('aria-label'),t:(b.innerText||'').trim().slice(0,30),cls:(b.className||'').toString().slice(0,60)}));\nJSON

---

**Claude:**

Deep Think = Max, web search ON, GLM-5.3 flagship. The separate "Advanced Search" toggle no longer exists in today's UI. Pasting.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_eeb90dde, "action": "javascript_exec", "text": "const P=window.name;\nconst ta=document.querySelector('form textarea')||document.querySelector('textarea');\nif(!ta){JSON.stringify({err:'no textarea'})} else {\nconst setter=Object.getOwnPropertyDescriptor(window.HTMLTextAreaElement.prototy

---

**Claude:**

Exact match (11625/11625). Sending.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_eeb90dde, "action": "javascript_exec", "text": "const b=document.querySelector('button.sendMessageButton');\nif(!b){JSON.stringify({err:'no send'})} else { b.click(); await new Promise(r=>setTimeout(r,5000)); JSON.stringify({url:location.href, tail:document.body.innerText.slice(-300)}) }"

---

**Claude:**

✅ **GLM started**: `chat.z.ai/c/s_91b202c1`. Next: ChatGPT.

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_0919c18d, "url": "http://10.0.0.0:8791/chatgpt.md"}}, {"name": "javascript_tool", "input": {"tabId": id_0919c18d, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); window.name.length"}}, {"name": "na

---

**Claude:**

ChatGPT here is `[EMAIL]`, not the a2 account. Checking the plan and available accounts.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_0919c18d, "action": "javascript_exec", "text": "const s=await fetch('/api/auth/session').then(r=>r.json());\nconst a=await fetch('/backend-api/accounts/check/v4-2023-04-27',{headers:{Authorization:'Bearer '+s.accessToken}}).then(r=>r.json()).catch(e=>({err:String(e)}));\nconst accs=a.acco

---

**Claude:**

`prolite` = paid tier, so the door is live. Using it and recording which account. Reading the composer.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_0919c18d, "action": "screenshot"}}, {"name": "read_page", "input": {"tabId": id_0919c18d, "filter": "interactive", "max_chars": 2500}}]}

---

**Claude:**

Account is "Anna & Co · Pro", thinking already Extra High. Opening the tools menu.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_0919c18d, "action": "left_click", "ref": "ref_55"}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "wait", "duration": 1}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "screenshot"}}]}

---

**Claude:**

That switched to a live "Work" task that isn't mine — backing out without touching it.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_0919c18d, "url": "https://chatgpt.com/"}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "wait", "duration": 4}}, {"name": "javascript_tool", "input": {"tabId": id_0919c18d, "action": "javascript_exec", "text": "const ed=document.que

---

**Claude:**

Composer is clean but `window.name` was lost in the navigation. Re-transporting.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_0919c18d, "url": "http://10.0.0.0:8791/chatgpt.md"}}, {"name": "javascript_tool", "input": {"tabId": id_0919c18d, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); window.name.length"}}, {"name": "na

---

**Claude:**

Prompt carried, composer clean. Now enabling Deep research in the empty composer.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_0919c18d, "query": "plus button \"Add files and more\" in the message composer at bottom"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_0919c18d, "action": "left_click", "ref": "ref_262"}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "screenshot"}}]}

---

**Claude:**

Landed on the Work surface. Switching to Chat.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_0919c18d, "action": "left_click", "coordinate": [638, 20]}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "left_click", "coordinate": [403, 277]

---

**Claude:**

Menu open with Deep research. Enabling it in the empty composer.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_0919c18d, "action": "left_click", "coordinate": [454, 388]}}, {"name": "computer", "input": {"tabId": id_0919c18d, "action": "wait", "duration": 2}}, {"name": "javascript_tool", "input": {"tabId": id_0919c18d, "action": "javascript_exec", "text": "co

---

**Claude:**

Deep research chip active. Placing caret at end and pasting (execCommand — the method that works on ChatGPT).

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_0919c18d, "action": "javascript_exec", "text": "const P=window.name; const ed=document.querySelector('.ProseMirror');\ned.focus();\nconst r=document.createRange(); r.selectNodeContents(ed); r.collapse(false);\nconst s=window.getSelection(); s.removeAllRanges(); s.addRange(r);\ndocument.ex

---

**Claude:**

All three probes green: chip alive, head/tail match, cyrillic 40/40. Sending.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_0919c18d, "action": "javascript_exec", "text": "const b=document.querySelector('button[data-testid=\"send-button\"]')||document.querySelector('#composer-submit-button');\nif(!b){JSON.stringify({err:'no send', btns:[...document.querySelectorAll('form button')].map(x=>x.getAttribute('data-t

---

**Claude:**

✅ **ChatGPT started**: `chatgpt.com/c/s_b1917330`. Now Gemini.

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_261eebf4, "url": "http://10.0.0.0:8791/gemini.md"}}, {"name": "javascript_tool", "input": {"tabId": id_261eebf4, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); window.name.length"}}, {"name": "nav

---

**Claude:**

Gemini: Punk Crypto (a@), Pro Extended, paid. Opening the tools menu for Deep research.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_261eebf4, "query": "plus button \"Upload & tools\" next to the prompt input"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "ref": "ref_66"}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "screenshot"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "coordinate": [517, 335]}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "screenshot"}}]}

---

**Claude:**

Menu open. Opening "More tools" → Deep research (canon: click by ref, not coordinates).

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "coordinate": [582, 579]}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "screenshot"}}]}

---

**Claude:**

Submenu open. Clicking Deep research by ref (canon: coordinate clicks miss silently here).

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_261eebf4, "query": "Deep research menu item in the open submenu"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "ref": "ref_137"}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 2}}, {"name": "javascript_tool", "input": {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const ed=d

---

**Claude:**

Deep research confirmed (placeholder changed). Pasting.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const P=window.name; const ed=document.querySelector('.ql-editor');\ned.focus();\nconst r=document.createRange(); r.selectNodeContents(ed); r.collapse(false);\nconst s=window.getSelection(); s.removeAllRanges(); s.addRange(r);\ndocument.exec

---

**Claude:**

Paste verified. Sending (Gemini is two-phase — plan first, then Start research).

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const b=document.querySelector('button[aria-label*=\"Send\"], button.send-button');\nif(!b){JSON.stringify({err:'no send', labels:[...document.querySelectorAll('button')].map(x=>x.getAttribute('aria-label')).filter(Boolean).slice(-12)})}\nel

---

**Claude:**

Prompt submitted; Gemini is generating the plan. Writing the ledger while it works.

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; mkdir -p \"$V/_drafts\"; cat > \"$V/_drafts/DR-FANOUT-DR26-09-04-HUB-01-2323-playwright.md\" <<'EOF'\n---\ndr_id: DR26-09-04-HUB-01-2323\ntopic: Playwright для нашего типа работ — пять лейнов против Selenium-Firefox рельсы\nstarted: 2026-09-05 00:45 Li

---

**Claude:**

Now dozhimayu Gemini's "Start research" button.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_261eebf4, "query": "Start research button to begin the deep research plan"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 15}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "screenshot"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "screenshot"}}]}

---

**Claude:**

Caught it: the prompt is still sitting in the composer — the JS click didn't submit. Using a trusted click on the send arrow.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "coordinate": [1106, 401]}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 8}}, {"name": "

---

**Claude:**

Gemini submitted (`app/f2c458e4965def9d`), plan generating. While it plans, checking Mistral.

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_dce01eb6, "url": "http://10.0.0.0:8791/mistral.md"}}, {"name": "javascript_tool", "input": {"tabId": id_dce01eb6, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); window.name.length"}}, {"name": "na

---

**Claude:**

Mistral logged in as PaloAlto Ai Research Lab. Reading the composer.

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_dce01eb6, "action": "screenshot"}

---

**Claude:**

Opening Mistral's tools menu ("+") to find Deep Research.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [577, 342]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

**Claude:**

Menu open. Opening Tools to find Deep Research.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [610, 439]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

**Claude:**

Web search already on; no Deep Research here. Checking the "Fast" mode selector.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "key", "text": "Escape"}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 1}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1191, 335]}}, {"name": 

---

**Claude:**

Let me check Gemini's plan first — it's time-sensitive.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_261eebf4, "query": "Start research / Начать исследование button under the research plan"}

---

**Claude:**

Plan ready. Pressing "Начать исследование" (canon: click twice with re-look).

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "ref": "ref_349"}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 8}}, {"name": "javascript_tool", "input": {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const t=do

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_261eebf4, "action": "screenshot"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "scroll", "coordinate": [900, 400], "scroll_direction": "down", "scroll_amount": 5}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 3}}, {"name": "computer", "input": {"tabId": id_261eebf4, "ac

---

**Claude:**

The composer overlays the Start button. Scrolling it into view.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_261eebf4, "query": "Начать исследование button"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "scroll_to", "ref": "ref_560"}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "left_click", "ref": "ref_560"}}, {"name": "co

---

**Claude:**

Button pressed ("You said Начать исследование"). Waiting for the research to kick off.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "javascript_tool", "input": {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const t=document.

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_261eebf4, "action": "screenshot"}

---

**Claude:**

✅ **Gemini started** — "Приступаю. Я сообщу, как только ваше исследование будет готово." That's 4 rails = quorum. Continuing with Mistral.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1400, 200]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 1}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1191, 3

---

**Claude:**

Menu closed. Opening the "Fast" mode selector.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1210, 335]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

**Claude:**

Found it: Research mode ("Deep analysis with multiple sources"). Selecting it.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1039, 503]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "javascript_tool", "input": {"tabId": id_dce01eb6, "action": "javascript_exec", "text": "c

---

**Claude:**

Still "Fast" — clicking by ref instead.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1210, 335]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "find", "input": {"tabId": id_dce01eb6, "query": "Research mode option 'Deep analysis with

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "ref": "ref_54"}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "javascript_tool", "input": {"tabId": id_dce01eb6, "action": "javascript_exec", "text": "const f=doc

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_dce01eb6, "action": "screenshot"}

---

**Claude:**

Mistral moved Deep Research to the Work tab. Following it.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [974, 374]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 4}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

**Claude:**

Work tab with the `deep-research` skill chip active. Pasting.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_dce01eb6, "action": "javascript_exec", "text": "const P=window.name;\nif(!P||P.length<1000){JSON.stringify({err:'window.name lost', len:P?P.length:0})} else {\nconst ed=document.querySelector('.ProseMirror')||document.querySelector('[contenteditable=\"true\"]');\nconst ta=document.querySe

---

**Claude:**

Paste truncated at 118 chars. Falling back to execCommand.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_dce01eb6, "action": "javascript_exec", "text": "const P=window.name;\nconst ed=document.querySelector('.ProseMirror')||document.querySelector('[contenteditable=\"true\"]');\ned.focus();\nlet r=document.createRange(); r.selectNodeContents(ed); let s=getSelection(); s.removeAllRanges(); s.a

---

**Claude:**

execCommand landed it in full (cyr 40/40). Sending with a trusted click.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "find", "input": {"tabId": id_dce01eb6, "query": "send message submit arrow button in composer"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "ref": "ref_189"}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 8}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

**Claude:**

Mistral Work chat created. Verifying it actually started researching.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 10}}, {"name": "javascript_tool", "input": {"tabId": id_dce01eb6, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({url:location.href, len:t.length, tail:t.slice(-450)})"}

---

**Claude:**

✅ **Mistral started** (Work skill, "Running 16 actions"). Last rail: claude.ai.

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "navigate", "input": {"tabId": id_929112ea, "url": "http://10.0.0.0:8791/claudeai.md"}}, {"name": "javascript_tool", "input": {"tabId": id_929112ea, "action": "javascript_exec", "text": "window.name = await fetch(location.href).then(r=>r.text()); window.name.length"}}, {"name": "n

---

**Claude:**

claude.ai live as `dev` (+ "palo alto" org). Using it as-is — canon forbids switching accounts in dev's Chrome. Enabling Research.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}, {"name": "find", "input": {"tabId": id_929112ea, "query": "tools menu button in composer to enable Research"}}]}

---

**Claude:**

Opus 5 / High already set. Opening the tools menu for Research.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "left_click", "ref": "ref_136"}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}]}

---

**Claude:**

Web search already on. Enabling Research.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "left_click", "coordinate": [689, 292]}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}]}

---

**Claude:**

Research toggle now active (blue). Pasting.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_929112ea, "action": "javascript_exec", "text": "const P=window.name;\nconst ed=document.querySelector('.ProseMirror')||document.querySelector('[contenteditable=\"true\"]');\ned.focus();\nlet r=document.createRange(); r.selectNodeContents(ed); r.collapse(false); let s=getSelection(); s.rem

---

**Claude:**

Paste verified. Sending.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "find", "input": {"tabId": id_929112ea, "query": "send message button in composer"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "left_click", "ref": "ref_147"}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}]}

---

**Claude:**

✅ **All 6 rails started** — full fanout, nothing in `missing`. Recording dispatch.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py dispatched DR26-09-04-HUB-01-2323 2>&1 | head -20; echo \"---status---\"; python dr_queue.py status DR26-09-04-HUB-01-2323 2>&1 | head -5", "description": "Mark DR dispatched"}

---

> `Bash` -- {"command": "V=\"D:/Vault/Vault-Knowledge\"; F=\"$V/_drafts/DR-FANOUT-DR26-09-04-HUB-01-2323-playwright.md\"\npython - <<'PY'\nimport re,io\np=r\"D:/Vault/Vault-Knowledge/_drafts/DR-FANOUT-DR26-09-04-HUB-01-2323-playwright.md\"\ns=open(p,encoding='utf-8').read()\ns=s.replace(\"status: dispatch

---

**Claude:**

Now the mandatory report to dev and TG-03 with links.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python bus_send.py --kind INFO --text \"DR26-09-04-HUB-01-2323 (Playwright, 5 лейнов) — веер РАЗНЕСЁН, 6/6 рельс стартовали с хаба HUB-01, missing пуст.\ngrok Heavy: https://grok.com/c/s_8d4cabcc\nglm GLM-5.3 DeepThink Max: https:

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python bus_send.py \"DR26-09-04-HUB-01-2323 (Playwright, 5 лейнов) — веер РАЗНЕСЁН с хаба HUB-01: 6/6 рельс стартовали, missing пуст.\ngrok Heavy: https://grok.com/c/s_8d4cabcc\nglm GLM-5.3 DeepThink Max: https://chat.z.ai/c/57865

---

**Claude:**

Dual-send OK. Now waiting on reports. Checking rail progress.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"tabId": id_1367eb44, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({v:'grok', len:t.length, tail:t.slice(-200)})"}}, {"name": "javascript_tool", "input": {"tabId": id_eeb90dde, "action": "javascript_exec", "text"

---

**Claude:**

**Grok is done — 816 sources.** Harvesting it now.

---

> `mcp__claude-in-chrome__get_page_text` -- {"tabId": id_1367eb44, "max_chars": "50000"}

---

**Claude:**

Grok delivered a 41KB document with a Download button — taking the official export path.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_1367eb44, "query": "Download button for the attached document DR26-09-04-Playwright-fleet-verdict.md"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_1367eb44, "action": "left_click", "ref": "ref_407"}}, {"name": "computer", "input": {"tabId": id_1367eb44, "action": "wait", "duration": 5}}]}

---

> `Bash` -- {"command": "cd ~/.claude/scripts/_shared 2>/dev/null && python -c \"import _paths; print(_paths.originals_root())\" 2>&1 || python -c \"\nimport sys; sys.path.insert(0,r'C:/Users/dev/.claude/scripts/_shared')\nimport _paths; print(_paths.originals_root())\" 2>&1", "description": "Resolve original

---

> `Bash` -- {"command": "find ~/.claude -name \"_paths.py\" 2>/dev/null; find \"D:/Vault/_imports\" -name \"_paths.py\" 2>/dev/null | head -3; echo \"=== downloads ===\"; ls -lt ~/Downloads 2>/dev/null | head -5", "description": "Locate _paths module and check download"}

---

**Claude:**

Download landed (41,330 bytes). Filing it to `_originals` with provenance.

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys, os, shutil, datetime\nsys.path.insert(0, r'D:/Vault/_imports')\nimport _paths\nroot = _paths.originals_root()\nprint(\"originals_root:\", root)\ndest_dir = os.path.join(root, \"deep-research\")\nos.makedirs(dest_dir, exist_ok=True)\nsrc = os.path.expandus

---

**Claude:**

Running the leg gate on Grok before counting it collected.

---

> `Bash` -- {"command": "python ~/.claude/scripts/dr_leg_gate.py \"D:/Vault/_originals/deep-research/DR26-09-04-HUB-01-2323-playwright-five-lanes-grok.md\" 2>&1; echo \"EXIT=$?\"", "description": "Gate the Grok leg"}

---

**Claude:**

Gate passed (57 verifiable sources). Recording the leg and checking the other rails.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py deliver DR26-09-04-HUB-01-2323 --target grok --file \"D:/Vault/_originals/deep-research/DR26-09-04-HUB-01-2323-playwright-five-lanes-grok.md\" 2>&1 | head -10 || python dr_queue.py deliver --help 2>&1 | head -20", "description": "Register gr

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"tabId": id_929112ea, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({v:'claudeai', len:t.length, tail:t.slice(-200)})"}}, {"name": "javascript_tool", "input": {"tabId": id_dce01eb6, "action": "javascript_exec", "t

---

**Claude:**

claude.ai hit the "Suggested connectors" modal — the canon trap that silently stalls the run. Clicking Skip.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_929112ea, "query": "Skip button in the suggested connectors dialog"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 5}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}]}

---

**Claude:**

claude.ai tab is busy — coming back to it. Harvesting Mistral, which is done.

---

> `mcp__claude-in-chrome__find` -- {"tabId": id_dce01eb6, "query": "download or export button for the canvas document / report"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "ref": "ref_1777"}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 2}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1264, 375]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 3}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "screenshot"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_dce01eb6, "action": "left_click", "coordinate": [1273, 418]}}, {"name": "computer", "input": {"tabId": id_dce01eb6, "action": "wait", "duration": 4}}]}

---

> `Bash` -- {"command": "sleep 6; ls -lt ~/Downloads 2>/dev/null | head -4", "description": "Check Mistral download"}

---

**Claude:**

Mistral downloaded (33,518 b). Filing and gating it.

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys, os\nsys.path.insert(0, r'D:/Vault/_imports')\nimport _paths\ndest_dir = os.path.join(_paths.originals_root(), \"deep-research\")\nsrc = os.path.expanduser(r\"~/Downloads/dr26-09-04-hub-01-2323-playwright-deep-research-analysis.md\")\nbody = open(src, enco

---

**Claude:**

Two legs collected. Back to claude.ai — the connectors modal is still blocking it.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "screenshot"}}]}

---

**Claude:**

claude.ai stopped: "No response on which connectors to enable" — the modal timed out. Restarting it and watching for the dialog.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_929112ea, "action": "javascript_exec", "text": "const P=\"Proceed now with the full research using web search only. Do NOT use any connectors - skip the connector selection entirely. Execute the plan and write the FULL final report per the brief above.\";\nconst ed=document.querySelector(

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "find", "input": {"tabId": id_929112ea, "query": "send message button"}}]}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "left_click", "ref": "ref_481"}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 8}}, {"name": "computer"

---

**Claude:**

claude.ai restarted. Checking the remaining three rails.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"tabId": id_eeb90dde, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({v:'glm', len:t.length, tail:t.slice(-180)})"}}, {"name": "javascript_tool", "input": {"tabId": id_0919c18d, "action": "javascript_exec", "text":

---

**Claude:**

Gemini is finishing. GLM and ChatGPT show no growth — checking with screenshots (innerText lies in background tabs).

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_eeb90dde, "action": "screenshot"}}]}

---

**Claude:**

GLM is alive (thinking indicator). Updating the ledger, then harvesting Gemini.

---

> `Bash` -- {"command": "python - <<'PY'\np=r\"D:/Vault/Vault-Knowledge/_drafts/DR-FANOUT-DR26-09-04-HUB-01-2323-playwright-five-lanes.md\"\nimport os\np2=r\"D:/Vault/Vault-Knowledge/_drafts/DR-FANOUT-DR26-09-04-HUB-01-2323-playwright.md\"\ns=open(p2,encoding='utf-8').read()\ns+=\"\"\"\n## Сбор (обновляет

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_261eebf4, "action": "wait", "duration": 10}}, {"name": "javascript_tool"

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_261eebf4, "action": "screenshot"}

---

**Claude:**

✅ **Gemini done** — report canvas rendered. Harvesting via Blob download (the method proven for Gemini).

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const cands=[...document.querySelectorAll('.structured-content-container, [class*=\"structured-content\"], .markdown-main-panel, message-content')].map(e=>({cls:(e.className||'').toString().slice(0,50), len:(e.innerText||'').length}));\ncand

---

**Claude:**

Report panel found (28,738 chars). Downloading the full page snapshot via Blob.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const panels=[...document.querySelectorAll('.markdown-main-panel')].map(e=>e.innerText);\npanels.sort((a,b)=>b.length-a.length);\nconst txt = \"=== GEMINI DEEP RESEARCH REPORT ===\\n\\n\" + panels[0] + \"\\n\\n=== FULL PAGE SNAPSHOT (plan + 

---

> `Bash` -- {"command": "sleep 4; ls -lt ~/Downloads/gemini-dr-playwright.txt 2>&1", "description": "Verify Gemini blob landed"}

---

**Claude:**

Blob landed (143,954 b). Filing and gating.

---

> `Bash` -- {"command": "python - <<'PY'\nimport sys, os\nsys.path.insert(0, r'D:/Vault/_imports')\nimport _paths\ndest_dir = os.path.join(_paths.originals_root(), \"deep-research\")\nsrc = os.path.expanduser(r\"~/Downloads/gemini-dr-playwright.txt\")\nbody = open(src, encoding='utf-8', errors='replace').rea

---

**Claude:**

Gemini's leg has 0 inline URLs — its citations are UI chips. Let me pull the actual source links.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const hrefs=[...new Set([...document.querySelectorAll('a[href^=\"http\"]')].map(a=>a.href).filter(h=>!/google\\.com\\/(intl|policies|support)|accounts\\.google/.test(h)))];\nJSON.stringify({n:hrefs.length, sample:hrefs.slice(0,5)})"}

---

**Claude:**

88 real source URLs exist as anchors. Appending them so the leg is verifiable.

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_261eebf4, "action": "javascript_exec", "text": "const hrefs=[...new Set([...document.querySelectorAll('a[href^=\"http\"]')].map(a=>a.href))].filter(h=>!/google\\.(com|ca)\\/intl|policies\\.google|support\\.google|accounts\\.google|myaccount\\.google/.test(h));\nconst txt=\"=== GEMINI SOUR

---

> `Bash` -- {"command": "sleep 4; SRC=~/Downloads/gemini-dr-sources.txt; ls -l \"$SRC\" 2>&1 && python - <<'PY'\nimport os\ndest=r\"D:/Vault/_originals/deep-research/DR26-09-04-HUB-01-2323-playwright-five-lanes-gemini.md\"\nsrc=os.path.expanduser(\"~/Downloads/gemini-dr-sources.txt\")\nadd=\"\\n\\n=== ИСТОЧН

---

**Claude:**

Second download in the same tab was silently blocked (the documented Chrome multi-download gotcha). Using a fresh tab.

---

> `mcp__claude-in-chrome__tabs_create_mcp` -- {}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": "[{\"name\": \"navigate\", \"input\": {\"tabId\": id_e410ae3d, \"url\": \"https://gemini.google.com/app/f2c458e4965def9d\"}}, {\"name\": \"computer\", \"input\": {\"tabId\": id_e410ae3d, \"action\": \"wait\", \"duration\": 10}}, {\"name\": \"javascript_tool\", \"input\": {\"tabId\": 46789993

---

> `mcp__claude-in-chrome__navigate` -- {"tabId": id_e410ae3d, "url": "https://gemini.google.com/app/f2c458e4965def9d"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": "[{\"name\": \"computer\", \"input\": {\"tabId\": id_e410ae3d, \"action\": \"wait\", \"duration\": 10}}, {\"name\": \"javascript_tool\", \"input\": {\"tabId\": id_e410ae3d, \"action\": \"javascript_exec\", \"text\": \"const hrefs=[...new Set([...document.querySelectorAll('a[href^=\\\"http\\\

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_e410ae3d, "action": "javascript_exec", "text": "await new Promise(r=>setTimeout(r,8000));\nconst hrefs=[...new Set([...document.querySelectorAll('a[href^=\"http\"]')].map(a=>a.href))].filter(h=>!/policies\\.google|support\\.google|accounts\\.google|myaccount\\.google|about\\/products/.tes

---

> `Bash` -- {"command": "sleep 4; SRC=~/Downloads/gemini-dr-sources.txt; if [ -f \"$SRC\" ]; then python - <<'PY'\nimport os\ndest=r\"D:/Vault/_originals/deep-research/DR26-09-04-HUB-01-2323-playwright-five-lanes-gemini.md\"\nsrc=os.path.expanduser(\"~/Downloads/gemini-dr-sources.txt\")\nadd=\"\\n\\n=== ИСТО

---

**Claude:**

Three legs green. Checking the remaining three for quorum.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_0919c18d, "action": "screenshot"}}]}

---

**Claude:**

ChatGPT DR still running. Checking claude.ai and GLM.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"tabId": id_929112ea, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({v:'claudeai', len:t.length, tail:t.slice(-250)})"}}, {"name": "javascript_tool", "input": {"tabId": id_eeb90dde, "action": "javascript_exec", "t

---

**Claude:**

✅ **GLM done.** Harvesting it via Blob (first download in that tab).

---

> `mcp__claude-in-chrome__javascript_tool` -- {"tabId": id_eeb90dde, "action": "javascript_exec", "text": "const hrefs=[...new Set([...document.querySelectorAll('a[href^=\"http\"]')].map(a=>a.href))].filter(h=>!/z\\.ai\\/(pricing|terms|privacy)|zhipu/.test(h));\nconst txt=document.body.innerText + \"\\n\\n=== SOURCE ANCHORS (\"+hrefs.length+\") =

---

> `Bash` -- {"command": "sleep 4; SRC=~/Downloads/glm-dr-playwright.txt; ls -l \"$SRC\" 2>&1 && python - <<'PY'\nimport sys, os\nsys.path.insert(0, r'D:/Vault/_imports')\nimport _paths\ndest_dir = os.path.join(_paths.originals_root(), \"deep-research\")\nsrc = os.path.expanduser(r\"~/Downloads/glm-dr-playwri

---

**Claude:**

**Quorum met — 4 legs collected.** Registering them.

---

> `Bash` -- {"command": "cd ~/.claude/scripts && python dr_queue.py attach --help 2>&1 | head -20; echo \"=== deliver help ===\"; python dr_queue.py deliver --help 2>&1 | head -20", "description": "Check attach/deliver syntax"}

---

> `Bash` -- {"command": "cd ~/.claude/scripts && D=\"D:/Vault/_originals/deep-research\"\nfor v in grok gemini mistral glm; do\n  python dr_queue.py attach DR26-09-04-HUB-01-2323 $v \"$D/DR26-09-04-HUB-01-2323-playwright-five-lanes-$v.md\" 2>&1 | head -3\ndone\necho \"=== STATUS ===\"; python dr_queue.py sta

---

**Claude:**

Quorum: `done | 4/6`. Now reading the other legs for synthesis while ChatGPT and claude.ai finish.

---

> `Bash` -- {"command": "D=\"D:/Vault/_originals/deep-research\"; echo \"######## GEMINI REPORT (первые 9000 симв. панели отчёта) ########\"; sed -n '/=== GEMINI DEEP RESEARCH REPORT ===/,$p' \"$D/DR26-09-04-HUB-01-2323-playwright-five-lanes-gemini.md\" | head -c 9000", "description": "Read Gemini report hea

---

**Claude:**

Gemini directly contradicts Grok on the iframe question — important. Reading GLM and Mistral verdicts.

---

> `Bash` -- {"command": "D=\"D:/Vault/_originals/deep-research\"; echo \"######## GLM ########\"; grep -n -A 40 -i \"вердикт\\|per-lane\\|Лейн 1\\|Lane 1\" \"$D/DR26-09-04-HUB-01-2323-playwright-five-lanes-glm.md\" | head -70", "description": "Read GLM verdict"}

---

> `Bash` -- {"command": "D=\"D:/Vault/_originals/deep-research\"; sed -n '196,340p' \"$D/DR26-09-04-HUB-01-2323-playwright-five-lanes-glm.md\"", "description": "Read GLM verdict table"}

---

> `Bash` -- {"command": "D=\"D:/Vault/_originals/deep-research\"; sed -n '1,120p' \"$D/DR26-09-04-HUB-01-2323-playwright-five-lanes-mistral.md\" | head -c 7000", "description": "Read Mistral verdict"}

---

**Claude:**

Strong picture from 4 legs. Checking the last two before synthesis.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "javascript_tool", "input": {"tabId": id_929112ea, "action": "javascript_exec", "text": "const t=document.body.innerText; JSON.stringify({v:'claudeai', len:t.length, tail:t.slice(-200)})"}}, {"name": "javascript_tool", "input": {"tabId": id_0919c18d, "action": "javascript_exec", "t

---

**Claude:**

claude.ai reached "Verdict" — waiting for it to finish.

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "inpu

---

> `mcp__claude-in-chrome__computer` -- {"tabId": id_929112ea, "action": "screenshot"}

---

> `mcp__claude-in-chrome__browser_batch` -- {"actions": [{"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "input": {"tabId": id_929112ea, "action": "wait", "duration": 10}}, {"name": "computer", "inpu

---

**Claude:**

You've hit your session limit · resets 2am (Europe/London)
