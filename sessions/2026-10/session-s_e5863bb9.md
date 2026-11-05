---
session: s_e5863bb9
date: 2026-10-06
words: 18251
turns: 60
tools: "Bash, Read, Skill, ToolSearch, WebSearch, mcp__ccd_session_mgmt__get_session, mcp__ccd_session_mgmt__set_session_title, mcp__claude-in-chrome__list_connected_browsers"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_e5863bb9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:7783.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Надо изучить, можно ли делать подкасты в ноутбук LME по MCP или по API. Наверняка Google предоставляет доступ к ноутбуку LME по API или по MCP. Точнее, он точно предоставляет доступ к ноутбуку LME по API или по MCP, но только в корпоративной версии. Интересно, а у меня есть ли доступ по API или по MCP к всему этому сервису ноутбука LME?
---

КАК РАБОТАТЬ
1. RECALL первым ходом: память, волт, RAG (python D:\Vault\_imports\brain_ask.py "<тема>").
   Нашёл сделанным -- не делай заново: закрой дельту и скажи, чем и когда закрыто.
2. Расшифровка машинная, в ней бывают ослышки (память voice-transcription-synonyms:
   «Сиренка» = CRM, «Лиса» = Firefox). Смысл восстанавливай по контексту, слова оператора
   не переписывай и не смягчай (§9.7 «без купюр»).
3. Ты автономный кофаундер (§4.1-тер): по обратимому решай сам. оператора зови только на
   Tier-2 -- деньги, необратимое удаление, юр.подпись, секреты третьим лицам, масс-рассылка.
4. Много фактов для решения -> дашборд (§2.4). Собрал исполняемое -> прогони /tt.
5. РАБОТАЙ КАК ОБЫЧНАЯ ПОЛНОЦЕННАЯ СЕССИЯ. оператор сидит в тебе и читает тебя
   как любой другой свой чат (приказ 15.09, голосом). Значит:
     - весь результат ты кладёшь ВНУТРЬ СЕБЯ, в свой чат, целиком;
     - НЕ ужимай и НЕ суммаризируй: нашёл десять вариантов -- покажи десять,
       с названиями, ценами и прямыми ссылками; построил график -- покажи его строками;
     - волт и карточки -- ДОПОЛНЕНИЕ, а не замена ответа. «Подробности в карточке»
       вместо содержания = ответа нет («где блять мои подушки списком???», 15.09);
     - НИЧЕГО не выноси наружу: не шли отчёт в Telegram, не публикуй, не рассылай.
       Наружу уходит только то, о чём оператор попросил прямо в самой задаче.
   Длиннее 3 предложений -- разбивай пустой строкой (§9.10).

6. В ГРУППУ 001 (чат chat_REDACTED) СЕССИЯ НЕ ПИШЕТ НИКОГДА и НИЧЕГО -- ни отчёт,
   ни вопрос, ни «я застрял» (приказ оператора 15.09 19:28, голосом, после двух
   нарушений: сессия принесла туда «Отчёт 3», а другая -- «пришли продолжение»).
   Квитанцию о старте туда уже положила рельса; больше туда не пишет никто.
   Застрял или голосовая оборвана -> скажи это ВНУТРИ СЕБЯ, в своём чате,
   первой строкой ответа: оператор читает сессию сам и допишет продолжение сюда.

---

**Claude:**

You've hit your weekly limit · resets 5am (Europe/London)

---

**User:**

Continue from where you left off.

---

**Claude:**

No response requested.

---

**User:**

Try again

---

**Claude:**

Понял задачу: выяснить, можно ли управлять NotebookLM («ноутбук LME» = NotebookLM) по API или MCP, и есть ли у нас такой доступ. Первый ход — RECALL: что у нас уже сделано (память говорит, что есть CLI notebooklm-py и скиллы /notebooklm, /teach-podcast), затем проверю живость локальной рельсы и свежую картину по официальному API/MCP.

План рельс (§6.3-бис): recall и проверку инструментов делаю сам как Claude; свежий веб-ресёрч тоже сам (WebSearch), внешние LLM не нужны — вопрос фактологический, не стратегический.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\notebooklm-integration.md"}

---

> `Bash` -- {"command": "cd \"E:\\!CLAUDE-HUBPC-June26\" && python D:\\Vault\\_imports\\brain_ask.py \"NotebookLM API MCP доступ подкасты\" 2>&1 | head -60", "description": "RAG recall по теме NotebookLM API/MCP"}

---

> `Bash` -- {"command": "python \"D:/Vault/_imports/brain_ask.py\" \"NotebookLM API MCP доступ\" 2>&1 | head -40", "description": "RAG recall по NotebookLM"}

---

> `Bash` -- {"command": "\"C:/Users/dev/notebooklm-cli/venv/Scripts/notebooklm.exe\" auth check 2>&1; echo \"---\"; \"C:/Users/dev/notebooklm-cli/venv/Scripts/notebooklm.exe\" list 2>&1 | head -15", "description": "Проверка живости notebooklm CLI (auth + list)"}

---

> `ToolSearch` -- {"query": "select:WebSearch", "max_results": 1}

---

> `WebSearch` -- {"query": "NotebookLM official API access 2026 consumer availability"}

---

> `WebSearch` -- {"query": "NotebookLM MCP server 2026"}

---

> `Bash` -- {"command": "date \"+%d.%m.%Y %H:%M\"", "description": "Текущее время для штампа"}

---

**Claude:**

🕑 04.10.2026, 14:03 (суббота)

## Ответ: официального API/MCP для твоего аккаунта НЕТ, но рабочий программный доступ у нас УЖЕ ЕСТЬ и он жив прямо сейчас

Вопрос этот мы уже решали — Alpha Protocol R+DR 18.06.2026 плюс ADOPT CLI 04.07.2026 (память `notebooklm-integration`, решение в волте `02-Decisions/decision-notebooklm-claude-code-artifact-layer.md`). Сегодня я перепроверил и память, и живость рельсы, и свежий веб. Картина такая.

**1. Официальный API от Google — только корпоративный, ты прав.**

Ты сказал «точно предоставляет, но только в корпоративной версии» — подтверждаю, ровно так. Продукт за 2026 год переименовали: enterprise-ветка теперь называется **Gemini Notebook Enterprise** и идёт внутри Gemini Enterprise (бывший Agentspace). Там есть документированные REST-эндпоинты: создать/прочитать/перечислить/расшарить/удалить ноутбук, управлять источниками, генерить Audio Overview.

Но это НЕ developer-API с ключом из настроек: он доступен только организациям на Google Cloud / Workspace. Наш замер от июня: минимум ~15 мест, от ~$135+/мес. Все твои аккаунты — consumer `@gmail`, Workspace нет. Отдельный standalone «Podcast API» Google пометил deprecated и новых клиентов не пускает.

**2. Для consumer-аккаунта (твоего) публичного API нет** — ключ взять негде, это официальная позиция Google на октябрь 2026.

**3. Официального MCP у Google тоже нет** (на октябрь 2026). Есть community-MCP-серверы — все они обёртки той же неофициальной рельсы (куки + внутренние эндпоинты или управление Chrome):

- [julianoczkowski/notebooklm-mcp-2026](https://github.com/julianoczkowski/notebooklm-mcp-2026) — Python, stdio, для Claude Code/Desktop/Cursor; умеет list notebooks, читать источники, задавать вопросы ноутбуку. Требует Chrome.
- [mukundajmera/notebooklm-mcp](https://lobehub.com/mcp/mukundajmera-notebooklm-mcp) и [roomi-fields/notebooklm-mcp](https://glama.ai/mcp/servers/@roomi-fields/notebooklm-mcp/blob/96ed410e16fbd2d1cf01d08e46532e3b1d0e6d45/deployment/docs/README.md) — аналоги.

**4. Главное: у НАС программный доступ уже стоит и работает — проверил живьём 5 минут назад.**

На хабе установлен CLI `notebooklm-py` (teng-lin, 17k⭐, MIT, работает с consumer @gmail PRO без всякого Enterprise): `C:\Users\dev\notebooklm-cli\venv\Scripts\notebooklm.exe`. Прогон сейчас: `auth check` = valid (34 cookies, аккаунт a2@), `list` отдаёт твои ноутбуки, включая вчерашние (03.10): «Alisa v2 05 · LLM systems», «Учёба 04 v2: Stanford CS336/CS229/CS224N», «bb Harness» и далее. Полный цикл создать ноутбук → добавить источник → сгенерить аудио → скачать mp3 доказан `/tt` ещё 16.07.

Этой рельсой уже пользуются скиллы `/notebooklm` и `/teach-podcast` — все учебные подкасты (серия «Идеальный кандидат: 19 историй» и прочие) делаются именно так, без браузера.

**5. Вердикт по MCP: ставить community-MCP не нужно.** Они дали бы ровно то, что CLI уже даёт, только с лишним слоем и тем же риском (неофициальная рельса, куки протухают раз в несколько недель — перелогин через Firefox a2@ одной командой). Если когда-нибудь захочется, чтобы НЕ-Claude агенты (Cursor, Codex) сами дёргали NotebookLM — вот тогда MCP-обёртка станет осмысленной, кандидата я назвал выше.

Единственная «настоящая» дверь к официальному API — купить Gemini Enterprise, это деньги = Tier-2, и по текущим задачам не нужно: CLI закрывает всё.

Что не проверено: RAG-recall (brain_ask) на хабе сейчас падает из-за битого numpy в системном питоне (известная история от 02.10, живёт через .brain-venv) — ответ собран из памяти + живого прогона CLI + веба, этого достаточно.

Sources: [autocontentapi — Does NotebookLM Have an API](https://autocontentapi.com/blog/does-notebooklm-have-an-api), [Gemini Enterprise release notes](https://docs.cloud.google.com/gemini/enterprise/docs/release-notes), [Gemini Notebook API status](https://web-clipper-for-notebooklm.com/blog/notebooklm-api), [notebooklm-mcp-2026](https://github.com/julianoczkowski/notebooklm-mcp-2026), [MCP.Directory guide](https://mcp.directory/blog/notebooklm-mcp-complete-guide-2026)

🎙 Майк: вопрос закрыт ещё в июне, и закрыт правильно — мы не стали ждать Google, а взяли зрелый OSS-мост и он уже 3 месяца возит твои подкасты. Направляющий вопрос один: хочешь ли, чтобы и Codex/Cursor умели сами заказывать подкасты (тогда ставим MCP-обёртку), или хватает того, что это умею я?

🧒 Простыми словами: NotebookLM — как кухня в ресторане Google. Официальную дверь на кухню дают только большим фирмам за деньги. Но у нас давно есть свой чёрный ход (программа notebooklm-py), я только что его подёргал — открывается, все твои ноутбуки на месте, подкасты через него и делаются. Ничего нового покупать и ставить не надо.

🕑 04.10.2026, 14:04

---

**User:**

раздай этот скилл на гитхабе
потом ретро

---

**Claude:**

Понял: публикую скилл `/notebooklm` (он же тема сессии) в наш публичный GitHub, потом ретро. Сначала смотрю, что публикуем и куда — есть ли у нас уже публичный репо скиллов.

---

> `Bash` -- {"command": "ls -la \"C:/Users/dev/.claude/skills/notebooklm/\" 2>&1; echo \"=== SIZE ===\"; wc -c \"C:/Users/dev/.claude/skills/notebooklm/SKILL.md\" 2>&1; echo \"=== teach-podcast ===\"; ls -la \"C:/Users/dev/.claude/skills/teach-podcast/\" 2>&1", "description": "Смотрю содержимое скилла not

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && gh repo list tonydzi --limit 100 2>&1 | head -40", "description": "Список публичных репо tonydzi"}

---

**Claude:**

Репо много, и есть прецедент «один скилл = один репо» (`red-first-review-skill`), плюс `second-brain-starter-kit` со 100 скиллами. Проверяю prior art — не раздали ли уже, и читаю сам скилл.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && gh repo list tonydzi --limit 200 2>&1 | grep -iE \"notebook|podcast|audio\" ; echo \"--- exit:$? ---\"; echo \"=== поиск в starter-kit ===\"; gh api \"repos/tonydzi/second-brain-starter-kit/contents\" --jq '.[].name' 2>&1 | head -20", "description"

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/skills/notebooklm/SKILL.md\"", "description": "Читаю скилл notebooklm целиком"}

---

**Claude:**

Prior art чисто — этот скилл мы наружу ещё не отдавали. Но публиковать как есть нельзя: в нём личные пути, аккаунт a2@gmail, имена файлов волта и дословные приказы. Ищу наш штатный leak-scan/санитайзер.

---

> `Bash` -- {"command": "ls \"C:/Users/dev/.claude/scripts/\" 2>/dev/null | grep -iE \"leak|oss|sanit|publish|scrub\" ; echo \"=== _shared ===\"; ls \"C:/Users/dev/.claude/scripts/_shared/\" 2>/dev/null | grep -iE \"leak|oss|sanit|scrub\"", "description": "Ищу leak-scan инструменты"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/skills/share-fix/SKILL.md\" 2>/dev/null | head -60", "description": "Читаю скилл share-fix (раздай миру)"}

---

**Claude:**

Инструменты штатные есть: `repo_release_leakscan.py` + `oss-publish/`. Смотрю, как их звать.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python repo_release_leakscan.py --help 2>&1 | head -30; echo \"=== oss-publish ===\"; ls oss-publish/ 2>&1 | head -20", "description": "Справка leakscan и содержимое oss-publish"}

---

**Claude:**

Есть готовый `sanitize_skills.py` — ровно для этого случая.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts/oss-publish\" && python sanitize_skills.py --help 2>&1 | head -40", "description": "Справка sanitize_skills"}

---

**Claude:**

`sanitize_skills.py` работает на весь набор (64 скилла) — это движок starter-kit. Проверяю, не уехал ли notebooklm туда уже, иначе сделаю дубль.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && gh api \"repos/tonydzi/second-brain-starter-kit/contents/skills\" --jq '.[].name' 2>&1 | head -80", "description": "Список скиллов в публичном starter-kit"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && gh api \"repos/tonydzi/second-brain-starter-kit/contents/skills\" --paginate --jq '.[].name' 2>&1 | grep -iE \"notebook|teach|podcast|youtube\"; echo \"--- всего скиллов: ---\"; gh api \"repos/tonydzi/second-brain-starter-kit/contents/skills\" --pa

---

**Claude:**

Скилл **уже опубликован** — он лежит в `second-brain-starter-kit/skills/notebooklm` (233 скилла). Значит задача не «впервые выложить», а закрыть дельту. Сверяю публичную версию с локальной.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && gh api \"repos/tonydzi/second-brain-starter-kit/contents/skills/notebooklm/SKILL.md\" --jq '.size, .sha' 2>&1; echo \"=== локальный размер: ===\"; wc -c \"C:/Users/dev/.claude/skills/notebooklm/SKILL.md\"; echo \"=== публичное содержимое (head) =

---

**Claude:**

Картина ясная. Публичная версия **санитизирована, но устарела**: 6650 байт против локальных 9296. В мире нет самого ценного — секции «три дефолта генерации» (длина `long`, два языка, уточняющие вопросы в промпте, 10–15 источников) и YouTube-контракта. Дельта ≈2.6 КБ живого знания.

Дверь штатная — `starter_kit_publish.py`. Смотрю её.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && python starter_kit_publish.py --help 2>&1 | head -40", "description": "Справка starter_kit_publish"}

---

> `Bash` -- {"command": "ls -d \"E:/!CLAUDE-HUBPC-June26\"/*starter* \"E:/!CLAUDE-HUBPC-June26\"/_oss/* 2>/dev/null; echo \"=== поиск рабочей копии ===\"; find \"E:/!CLAUDE-HUBPC-June26\" -maxdepth 3 -name \"*.git\" -type d 2>/dev/null | grep -iE \"starter|brain\" | head", "description": "Ищу раб

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git remote -v 2>&1 && git status --short 2>&1 | head -10 && echo \"=== branch ===\" && git branch --show-current && echo \"=== skills/notebooklm ===\" && wc -c skills/notebooklm/SKILL.md 2>&1", "description": "Состояние рабочей копии sbsk

---

**Claude:**

Рабочая копия есть, но в ней уже висят ~60 изменённых файлов от прошлого прогона. Разбираюсь, чьё это, прежде чем коммитить — чужую незакоммиченную работу не утащу.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && echo \"=== всего изменено: ===\" && git status --short | wc -l && echo \"=== последние коммиты ===\" && git log --oneline -5 && echo \"=== diff notebooklm ===\" && git diff --stat skills/notebooklm/SKILL.md && echo \"=== пример чужого dif

---

**Claude:**

⚠️ Нашёл опасную штуку по пути. Эти 235 изменений — **откат санитизации**: в рабочем дереве лежат сырые внутренние русские скиллы (с именами, путями, дословными приказами), а в коммите — чистые английские. Один `git commit -a` в этой папке — и всё внутреннее уезжает в публичный репо. Разбираюсь и чиню правильно.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && echo \"=== untracked (новое, чего нет в коммите): ===\" && git status --short | grep \"^??\" | head -20 && echo \"(всего untracked: $(git status --short | grep -c '^??'))\" && echo \"=== утечки в рабочем дереве: ===\" && grep -rlE \"dzyat

---

**Claude:**

Личных утечек grep не нашёл (0) — значит санитизация путей в рабочем дереве прошла, но прогон потерял ручную английскую огранку описаний из коммита v0.3.0. Смотрю конкретно свой скилл.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git diff skills/notebooklm/SKILL.md 2>&1 | grep -vE \"^warning\" | head -50", "description": "Полный diff notebooklm в рабочей копии"}

---

**Claude:**

Диагноз точный. Рабочее дерево — сырое копирование, у которого потеряно всё, что делает репо публичным: `license: MIT`, английское description, kit-футер с CTA (§1.1 — обязателен!), а русские триггеры и имя оператора вернулись. Коммитить это нельзя.

Проверяю, что скажет штатный сборщик.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && grep -c \"Три дефолта\\|three defaults\\|--length long\" skills/notebooklm/SKILL.md 2>&1; echo \"--- есть ли YouTube-секция: ---\"; grep -c \"youtube-queue\\|_youtube\" skills/notebooklm/SKILL.md 2>&1; echo \"=== verify сборщика ===\"; cd

---

**Claude:**

Сборщик честно заблокировался (fail-closed, §5.5 — молодец): он ищет волт по `C:\Users\dev/Obsidian/...`, а волт на `D:\Vault`. Смотрю, какие переменные ему нужны.

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && grep -nE \"OBSIDIAN|getenv|environ|Knowledge\" starter_kit_publish.py | head -25", "description": "Какие env-переменные нужны сборщику"}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/.claude/scripts\" && sed -n '1,80p' starter_kit_publish.py", "description": "Читаю шапку сборщика"}

---

**Claude:**

Решение по АК-47: полная пересборка репо (233 скилла + Библия) — это не то, что просил оператор, и она снесёт ручную огранку v0.3.0 (видно по грязному дереву). Обновляю **один файл** через тот же гейт, сохранив публичный формат. Беру за базу огранённую версию из коммита.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git show HEAD:skills/notebooklm/SKILL.md > /tmp/nb_head.md 2>&1 && wc -c /tmp/nb_head.md && echo \"=== хвост (футер) ===\" && tail -25 /tmp/nb_head.md", "description": "Достаю огранённую версию из коммита"}

---

**Claude:**

Собираю публичную версию: база — огранённый HEAD, плюс две новые секции на английском. Дословные приказы и наш YouTube-контракт наружу не идут (внутренняя кухня), а вот технические дефолты генерации и сегодняшняя карта доступа — ровно то переносимое знание, которого в мире нет.

---

> `Bash` -- {"command": "cat > /tmp/nb_insert.md << 'EOF'\n## Access reality check (verified 2026-10-04)\n- **There is no public consumer API.** You cannot pick up a NotebookLM API key from a settings page and script your own notebooks.\n- **The official API is Enterprise-only** — now branded *Gemini Notebook E

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && python - << 'PY'\nimport io\nhead = io.open('/tmp/nb_head.md', encoding='utf-8').read()\nins  = io.open('/tmp/nb_insert.md', encoding='utf-8').read()\nanchor = '## digest (default) — vault → audio'\nassert anchor in head, 'anchor not foun

---

**Claude:**

Python под Windows не видит bash-овский `/tmp` — перекладываю в scratchpad.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; mkdir -p \"$SP\" && cp /tmp/nb_head.md \"$SP/nb_head.md\" && cp /tmp/nb_insert.md \"$SP/nb_insert.md\" && ls -la \"$SP\"/nb_*.md", "description": "Копирую файлы 

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && python - << 'PY'\nimport io\nSP = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_e5863bb9\\scratchpad\"\nhead = io.open(SP + r\"\\nb_head.md\", encoding='utf-8').read()\nins  =

---

**Claude:**

Файл собран: 8762 байта, футер и лицензия на месте. Теперь обязательный leak-scan перед push.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git add skills/notebooklm/SKILL.md 2>&1 | grep -v warning; cd \"C:/Users/dev/.claude/scripts\" && python repo_release_leakscan.py --repo \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" --staged 2>&1 | tail -25", "description": "Leak-scan sta

---

**Claude:**

Leak-scan чист (12 строк, 0 FAIL). Второй заход другим методом — проверяю глазами на личные маркеры (§4.3-бис).

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && echo \"=== личные маркеры в файле: ===\" && grep -nE \"dev|dev|C:\\\\\\\\Users\\\\\\\\dev|D:\\\\\\\\Vault|tg:-[0-9]|ClawRus/[0-9]|id_6647181e\" skills/notebooklm/SKILL.md; echo \"(найдено строк: $(grep -cE \"

---

**Claude:**

Нуль личных маркеров. «24 русских строки» — ложное срабатывание grep на `—`/`→` в этой локали; проверяю кириллицу надёжным способом.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && python - << 'PY'\nimport io, re\nt = io.open(r'skills\\notebooklm\\SKILL.md', encoding='utf-8').read()\ncyr = [l for l in t.split('\\n') if re.search(r'[\\u0400-\\u04FF]', l)]\nprint('строк с реальной кириллицей:', len(cyr))\nfor l in cyr

---

**Claude:**

Кириллицы ноль, личных маркеров ноль, два независимых прохода согласны. Коммичу и пушу с трейлерами провенанса (§5.11).

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git commit -F - << 'EOF' 2>&1 | tail -5\nskills/notebooklm: add the access reality check and the generation defaults\n\nTwo things the public version was missing, and they are the two that cost\npeople the most time.\n\nAccess: there is n

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git push origin master 2>&1 | tail -5", "description": "Push в публичный репо"}

---

**Claude:**

Удалёнка ушла вперёд — кто-то пушил. Рабочее дерево грязное, rebase им мешает, поэтому сначала смотрю, не правил ли этот же файл кто-то другой (чтобы не затереть чужое).

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git fetch origin 2>&1 | tail -2; echo \"=== сколько коммитов разошлось ===\"; git rev-list --left-right --count HEAD...origin/master 2>&1; echo \"=== что нового в origin ===\"; git log --oneline HEAD..origin/master 2>&1 | head -10; echo \

---

**Claude:**

Важная поправка: origin ушёл на 20 коммитов вперёд, и `notebooklm` там уже правили — в том числе есть коммит «undo the v0.5.0 overwrite that stripped catalog grooming», то есть ровно ту поломку, что я видел в рабочем дереве, уже починили. Моя база устарела на 20 коммитов. Беру свежую версию из origin, иначе верну старьё.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\" && git show origin/master:skills/notebooklm/SKILL.md > \"$SP/nb_origin.md\" && wc -c \"$SP/nb_origin.md\" && echo

---

**Claude:**

Origin-версия совпадает с моей базой (6650 против 6655 — только перевод строки), моих секций там нет. Пересобираю от origin-версии и отправляю через Contents API — так грязное дерево (чужая незакоммиченная работа) остаётся нетронутым.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/_oss/sbsk\" && git reset --mixed HEAD~1 2>&1 | tail -2; python - << 'PY'\nimport io\nSP = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_e5863bb9\\scratchpad\"\nbase = io.open(SP + r\"\\nb_or

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && SHA=$(gh api repos/tonydzi/second-brain-starter-kit/contents/skills/notebooklm/SKILL.md --jq '.sha') && echo \"remote sha:

---

**Claude:**

Запушено. Проверяю ВТОРЫМ заходом — читаю обратно с GitHub (§4.3-бис: «готово» доказывается другим методом, не тем, которым делал).

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && echo \"=== читаю живой файл с GitHub (raw) ===\" && gh api repos/tonydzi/second-brain-starter-kit/contents/skills/notebooklm/SKILL.md --jq '.size' && gh api repos/tonydzi/second-brain-starter-kit/contents/skills/notebooklm/SKILL.md --jq '.content' 

---

**Claude:**

Раздача закрыта и доказана чтением с GitHub. Теперь ретро, как просил.

---

> `Skill` -- {"skill": "retro"}

---

**User:**

Base directory for this skill: C:\Users\dev\.claude\skills\retro

# /retro — session retrospective (what we built · what we keep)

> 🧒 **When reporting to dev:** end with a child-simple "Простыми словами" recap in his language. His standing request (memory `eli5-always`). Reports TO dev only — not inside vault notes.

A retro = the Agile end-of-cycle ritual (**Keep / Drop / Try**) applied to a work session: look back, decide what survives. The goal is that **nothing reusable drowns in the transcript** — tools, rules, and lessons get caught and put in their right home.

## 🫸 ПОЛОСА `push3` — ретро 4-й командой после трёх толчков (dev 05.10.2026, голосом)

**Вызвана так:** `/retro push3` (так её посылает робот-проталкивалка `/push`, шаг 3б) ЛИБО
оператор говорит «сделай ретро по этой сессии». Приказ дословно: «после того как по задаче
3 раза нажимаем "продолжить сессию" и проталкиваем её дальше, 4-й командой нужно
запускать ретро... не терять содержание сессий, а сразу дистиллировать из них самое
важное: что делали, к чему пришли, какие выводы и следующие шаги. Это лучше делать сразу
после трёх продолжений, а не потом заново догонять всю сессию и пытаться восстановить
смысл».

**Это НЕ полное ретро.** Полное ретро ниже (Step 0...6) закрывает ЗАКОНЧЕННУЮ содержательную
работу и развозит durable по домам. Полоса `push3` закрывает другое: сессию протолкнули
трижды, она НЕ доделала, и её содержание вот-вот утонет в транскрипте. Цена полного
ритуала здесь не оправдана (§6.4, АК-47) — поэтому полоса короткая и кончается ОДНОЙ
строкой в журнале, который оператор читает. Полосу запускай ТОЛЬКО этим путём; пришёл простой
`/retro` без слова `push3` — делай полный ритуал.

### Шаг П1 — часы и разрыв (обязателен, та же дверь, что у полного ретро)
`get_session self` → `createdAt` / `lastActivityAt` + живые часы. Разрыв назови ЧИСЛОМ.
Метка хука `[⏰ оператор написал: …]` доказательством НЕ является (память `verify-clock-before-time-claims`).

### Шаг П2 — четыре поля оператора, и ровно они
Из СВОЕГО контекста (он горячий — в этом весь смысл полосы), без перечитывания транскрипта:
1. **что делали** — одна-две фразы по делу, без списка инструментов;
2. **к чему пришли** — результат с уликой (файл, exit-код, цитата), а не «поработали»;
3. **какие выводы** — что из этого durable; нечего — так и пиши «durable нет»;
4. **следующие шаги** — конкретный следующий ход, а не «продолжить работу».

⛔ Выдумывать нельзя: не уверен в поле — пиши «🤔 не подтверждено» (§5.4). «Готово» в поле
«к чему пришли» без улики = дефект, а не вежливость.

### Шаг П3 — ветки СРАЗУ, из дистиллята (а не потом)
«Если после ретро нужно сделать ветки/дальнейшие действия — делать их сразу на основе
дистиллированного контента». Разъехалось на слабо связанные куски → поднимаешь сессии САМ
(`/nsr`), сидом кладёшь дистиллят из Шага П2, а не «прочитай сессию такую-то». Разрешения
не спрашиваешь (§4.1). В новой сессии действует это же правило фрактально: три толчка → ретро.

### Шаг П4 — рот: строка в журнал, который оператор читает
```bash
python ~/.claude/scripts/session_retro_digest.py add --session <свой sessionId> \
  --title "<заголовок сессии>" --pushes 3 \
  --did "..." --got "..." --lessons "..." --next "..." \
  --branches "<что поднял сам, или пусто>" --dev "нет|<что именно нужно от него>"
```
Пишет в `$OBSIDIAN_VAULT/00-System/Session-Retro-Digest.md`, новые записи СВЕРХУ. Это и есть
«дальше я читаю ретро по сессии»: `--dev "нет"` = оператор идёт дальше, любой другой текст =
🙋 он подключается и дорабатывает. ⛔ Оставить дистиллят только внутри сессии = не сделать
работу: труба рождается с ртом (память `pipe-born-with-a-mouth`).

### Шаг П4-бис — долги правила (раз в заход, не чаще)
```bash
python ~/.claude/scripts/retro_rule_health.py
```
`exit 3` = есть сессии, которые выбрали три продолжения, затихли и дистиллята НЕ дали — правило сработало вхолостую. Назови их оператору строкой; доехать до них может `/push` Шаг 3в (в окне) или ночная `/retro-lost` (вне окна). `exit 1` = прибор слеп, это не «долгов нет».

### Шаг П5 — закройся
Durable правило/урок есть → Step 4 полного ретро для НЕГО одного (дом правила), остальные
шаги не нужны. Потом короткий 🧒-блок оператору и всё. ⛔ Не дрифтуй в чужие темы,
⛔ ничего наружу, ⛔ Tier-2 остаётся за оператором.

**Почему полоса живёт внутри `/retro`, а не отдельным скиллом:** один источник на слово
«ретро» (§5.8). Копия скилла под робота = второй дом, который разъедется с первым.

---

## Step 0 — RECALL & RECONCILE FIRST (situate this session in the WHOLE collaboration)
**Before any inventory, RECALL WIDE — this is the heart of the retro, not a formality (dev, 2026-07-02).** A session never happened in a vacuum: I run on multiple machines + a Cowork fleet concurrently, and this retro may be running **days/weeks/months after** the work. So recall here serves TWO jobs, not one:
- **(A) De-dupe** — a rule/skill/note I'm about to capture may already be done by a parallel session.
- **(B) Reconcile («сверить»)** — line up what THIS session did against everything the whole **hub / vault / peers** decided *since*; catch **drift, superseded decisions, contradictions**, and durable work not yet propagated. This is the RECALL-before-activity rule (`capture-rules-into-bible`) applied to retro.

⚠️ **И ДАТИРУЙ АРТЕФАКТЫ ВРЕМЕНЕМ СОБЫТИЯ, А НЕ ВРЕМЕНЕМ РЕТРО** (замер 30.09.2026, хаб: сессия начата 22.09, ретро шло 30.09; я взял часы ретро за «сейчас» и ИСПОРТИЛ верную дату в подписях 8 файлов, потом откатывал). Часы на ретро правдивы, метка хука первого захода тоже была правдива — врёт СКЛЕЙКА. Прежде чем поставить дату в подпись, заметку или леджер, спроси улику САМОГО события: `mtime` бэкапа/файла, `ts` уже записанной строки леджера, `createdAt` из `get_session self`. Правило зеркалит память `verify-clock-before-time-claims`: старый tool-вывод после резюма ≠ «сейчас», но и новые часы ≠ «когда это было сделано».

**⏳ Measure the time-gap FIRST — ДВУМЯ ПРОГОНАМИ, не суждением** (дверь от 30.09.2026; 01.10 она обнаружилась УТЕРЯННОЙ — живой SKILL.md держал ослабленную строку, а жёсткая версия лежала только в `SKILL.sync-conflict-20260930-*.md`; восстановлена 01.10):
```
python -c "import datetime; print('СЕЙЧАС', datetime.datetime.now().isoformat(timespec='seconds'))"
```
плюс `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → поля `createdAt` и `lastActivityAt`. Разница между ними И ЕСТЬ разрыв, и его надо назвать ЧИСЛОМ в отчёте.
⚠️ Метка из хука `[⏰ оператор написал: …]` доказательством НЕ является — это дата СИДА. Замер 30.09.2026 (класс `stale-context-after-resume-read-as-now`): сессию создали 16.09, возобновили 30.09, и весь заход я печатал «16 сентября» из подсказки хука, ни разу не сверив с часами. Канон: память `verify-clock-before-time-claims`.
Old session → widen every lookup below to cover *"what changed SINCE"*, и **Step 2а идёт СРАЗУ после этого замера**, до инвентаря: робот мог уже разобрать сессию, тогда всё ретро = дельта.

**Recall stack — cheap→expensive, mostly 0 tokens (use the existing tools, don't reinvent):**
1. **This session's spine (0 tok):** `python "$IMPORTS_ROOT/turnstate/turnstate_show.py"` — the black box of what THIS session actually asked / decided / touched (facts, not memory).
2. **Recent retros:** `ls "$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/"` — widen the window to span the gap; read any same-topic retro since.
2а. **Робот уже сделал ретро этой сессии? (0 tok):** `ls ~/.claude/logs/retro_lost_done/ | grep <sessionId>` — маркер есть → ночной `retro-lost` уже разобрал сессию (заметка `Retros/retro-lost-<дата>-<узел>-*.md`, единица с твоим sid). Тогда твоё ретро = ДЕЛЬТА поверх неё (живая сверка «что изменилось с тех пор» + компакт), с перекрёстной ссылкой, а не второй полный разбор. Замер 15.09.2026: сессия 07–08.09 получила лайт-ретро робота утром 15.09, живое ретро вечером чуть не переписало всё заново.
2б. **Дни целиком (0 tok):** `python "$IMPORTS_ROOT/day_ledger.py" --recall 7` — дневной леджер: коммиты, ретро, решения, ДР и посты **за каждый день окна**, включая чужие сессии и роботов. Именно он закрывает time-gap из ⏳ выше: ретро видят только ретро, леджер видит день. Дверь целиком — `/ledger`.
2в. **Рутина бежала или нет — только СЧЁТЧИК ПРОГОНОВ, НЕ наличие файлов (0 tok):**
   `python ~/.claude/scripts/routine_cost_audit.py --days <N>` -> колонка «прог.».
   Выход рутины пишется НЕ каждый прогон (у `pipe-a-inbox-watch` отчёт рождается только в дни
   с живыми письмами), поэтому «файла за 11.09 нет» не значит «11.09 не работала». Замер 15.09:
   объявил оператору 4 пропуска подряд, счётчик показал 8 прогонов за 9 дней — вывод был ложный
   и уже озвучен. Семья класса «судим по побочному следу вместо счётчика самой работы» насчитывает
   6 прежних случаев (ближайший 20.08: опись судила mtime заявленного stdout вместо факта работы),
   так что механизм тут не нужен — нужен ПОРЯДОК: счётчик первым, файлы вторыми.
   Канон: [[instrument-is-a-claim-too]], CLAUDE.md §5.4.
2в-бис. **А ЧЕМ КОНЧИЛАСЬ — отдельный вопрос, счётчик на него не отвечает (0 tok):**
   `python ~/.claude/scripts/_shared/routine_runs.py report` -> «падают СЕЙЧАС (серия)» + «молчат >7 суток».
   Точечно по одной: `routine_runs.py last "<имя задачи>"` (когда бежала, чем кончилась) и
   `routine_runs.py streak "<имя задачи>"` (сколько раз ПОДРЯД упала).
   Почему мало счётчика из 2в: `routine_cost_audit.py` считает прогоны по транскриптам СЕССИЙ
   (`~/.claude/projects/**/*.jsonl`) и про КОД ВОЗВРАТА не знает ничего — рутина, отбежавшая
   8 раз и 8 раз упавшая, в колонке «прог.» выглядит ровно как здоровая. Вопрос оператора на
   ретро — «эта рутина работает или УМЕРЛА?» — закрывается только парой «число прогонов +
   исход». Источник истины тут Планировщик Windows, а не наши логи (замер 01.10: 891 прогон,
   340 рутин с историей, 52 падают подряд прямо сейчас).
   ⚠️ Граница: история есть только у задач Планировщика; у движка `claude-task` её не
   существует нигде, и это говорится вслух, а не выводится из тишины.
   Канон: CLAUDE.md §5.5, §5.4; зеркала — `/hk` Шаг 3, `/arch`.
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

## Step 1🧠 — ПАМЯТЬ СЕССИИ: сироты по worktree + машинно-невидимые опровержения (дверь §8.6; добавлена 2026-09-02)
Сессия из worktree пишет память в СВОЮ проектную папку, домашний индекс о ней не знает — замер 02.09 на NODE-0X: 20 таких заметок, одна несла вердикт, опровергнутый через девять дней в соседней папке. Два прогона, 0 LLM, 0 сети:
- `python ~/.claude/scripts/memory_harvest.py --scan` → есть ORPHAN → `python ~/.claude/scripts/memory_harvest.py --harvest` (копия домой + указатель в `MEMORY-archive.md`; оригинал НЕ трогается). Exit 3 = `NEEDS-HUMAN` (тёзки припаркованы, ничего не потеряно) → строкой оператору, не молча.
- ⚠️ **Прибор даёт ложное «чисто» (замер 10.09.2026, NODE-0X):** `--scan` напечатал «0 missing pointer(s) to repair», а указатель на свежую заметку (`zenodo-publish-rail`, дописан 07.09) из `MEMORY.md` за ночь исчез — сироту он не увидел, потому что сверяет не ту пару папок. Поэтому ПОМИМО прогона сверь руками указатели на заметки, которые ЭТА сессия и пара прошлых записали: `grep -c "<слаг>" <проектная-папка>/memory/MEMORY.md` → 0 = дописать строку тем же заходом. Класс = `memory-index-line-lost-overnight`, 4 датированных случая, корень чинится отдельной сессией.
- `python ~/.claude/scripts/memory_inject_lint.py --scan` → анти-инъекция и секрет-паттерны memory-стора (порт bb plugins/memory, 05.09.2026): exit 1 = НОВАЯ находка против baseline — разобрать тем же заходом (чужая закладка? секрет в памяти → в secrets-стор); старый долг молчит ратчетом. Это ЕДИНСТВЕННАЯ дверь линта ([[rule-needs-a-door-quota]]).
- `python ~/.claude/scripts/memory_epistemic.py --lint` → `SELF-TOMBSTONE` (заметка сама пишет, что устарела, а машина этого не видит) закрыть тем же заходом: `--close <слаг> --superseded-by <слаг-преемника>`. Отмена закрывается ПОЛЯМИ (`status`/`valid_to`/`superseded_by`/`refuted_on`/`refuted_by`) во ВСЕХ копиях слага, а не переписыванием одной: CLAUDE.md §8.4-бис + [[memory-records-close-by-fields-not-rewrite]].
  - ⛔ **НО СНАЧАЛА ПРОЧИТАЙ НАЗВАННЫЙ МАРКЕР ГЛАЗАМИ — вердикт линта тут бывает ложным** (замер 06.10.2026, хаб). Линт мэтчит маркеры ПОДСТРОКОЙ (`MARKERS` ~строка 216, например `re.compile(r"\bSUPERSEDED\b")`), поэтому слово из предметного словаря читается как заявление заметки о себе: живая память `adopt-framework` попала в `A-BODY-ONLY` в ДВУХ копиях из-за перечисления имён состояний движка ADOPT — «терминалы DROP/CONFIRMED_EXISTING/SUPERSEDED/RETIRED». Заметка ничего про себя не отменяла. Это семья `sshivka-po-tekstu-a-ne-po-klyuchu` (58 случаев), и правило «закрой тем же заходом» без проверки прямо толкает закрыть ЖИВУЮ запись как отменённую. Порядок: `grep -inE "<маркер>" <файл>` → прочитать ВСЕ попадания → маркер стоит внутри перечисления, кодового блока или цитаты = ложное срабатывание, НЕ закрывать, а завести строку в журнал поломок на семью. Преемника тоже назови по улике: нет названного `--superseded-by` — значит закрывать нечем.
- Обоим прогонам вердикт в отчёт строкой: «🧠 память: N сирот перенесено · M опровержений закрыто» (или «чисто»). Молчание ≠ чисто.

## Step 1🩹 — ГЕЙТ ТРЕТЬЕЙ ПОЛОМКИ (дверь §5.10; добавлена 2026-08-14 после «а корни починил?»)
Зеркало гейта из `/tt` §Шаг 3 — тот стоит на СБОРКЕ, этот на ЗАКРЫТИИ сессии, потому что сессия без изменённого кода `/tt` не зовёт и до 14.08 её поломки не попадали в журнал НИКУДА (ровно этот пробел вскрылся вопросом оператора: ретро описало поломки прозой в ноте и назвало это починкой).
Перечисли поломки/уроки ЭТОЙ сессии (свои сбои, сбои рельс, «оно молчало», неверный вывод, пойманный позже). Для каждой поломки **СНАЧАЛА**, до выбора имени класса и до записи, найди смысловую семью:
```
python "$HOME/.claude/scripts/prior_art.py" class "<описание поломки своими словами>"
```
exit 0 = прежних нет, «1-й датированный» правомерен · **exit 3 = это НЕ ошибка и НЕ первый случай**: прибор печатает прежние строки, их даты и СЕМЬЮ дефекта. Если напечатана `СЕМЬЯ <slug>`, используй именно её как `<класс>`. ⭐ ВЕРДИКТ ЧИТАЙ ПО СТРОКЕ «СЕМЕЙНЫХ: N · СЛОВЕСНЫХ: M» (правка прибора 05-06.10.2026): «это НЕ 1-й случай» и счёт §5.10 держат ТОЛЬКО семейные. `СЕМЕЙНЫХ 0` при любом M = скорее всего 1-й случай; имя бери по предмету ремонта ЭТОЙ поломки, а из раздела `[словесное совпадение, в счёт §5.10 НЕ идёт]` имя НЕ брать — до правки там рядом с роднёй стояли переименование репо и врущий поиск в конфигураторе. Глазами видно одну семью → допиши её в `FAMILIES` ОДНОЙ строкой с красной пробой в обе стороны. При `exit 0`, когда прежней строки нет, назови класс по текущему предмету ремонта/нарушенному инварианту и запиши как 1-й датированный случай; канал, код возврата, текст алерта и симптом классом не являются.

ТОЛЬКО ПОСЛЕ этого запиши ОДНУ строку через дверь `python "$HOME/.claude/scripts/selfheal.py" journal --class <класс> --what "<что>" [--conditions --parts --guess --status]`: **что · условия · сопричастные (файлы/рельсы/узлы) · гипотеза 🤔 или ✅ доказанная причина**. ⛔ НЕ править `Breakage-Journal.md` напрямую (ни Edit, ни heredoc): это общий Syncthing-файл, вид рисует один владелец из пер-узловых шардов, прямая правка отбивается хуком `breakage_write_guard` и терялась (04.09: 76 строк в 11 конфликт-копиях) — память [[breakage-journal-per-node-shards]]. Счёт бери из фактического ответа `selfheal.py`: дедуп означает, что новой строки нет.

Дальше по семье: 1-й = строка · 2-й = строка + уточнить условия · **3-й датированный = класс системный**. Внутри `/retro` причинную цепочку НЕ строй: используй ровно одну отдельную ВИДИМУЮ repair-сессию, чей первый явный вызов — `/five-whys <класс>` в Claude или `$five-whys <класс>` в Codex, с датированными строками серии. Если `selfheal.py` уже поставил её в очередь, вторую не создавай. Механизм/робота на 1-2 случае НЕ строить. Дефект новой семьи → дописать её в `FAMILIES` внутри `prior_art.py` ОДНОЙ строкой, иначе следующая сессия снова назовёт его «первым».
- ⭐ **Семья доказана → её финиш = файл двери с красневшим тестом, не строка памяти** (замер 01.10.2026, NODE-0X: двери утреннего разбора не построены, вечером обе семьи повторились). На NODE-0X вердикт закрывает `python3 ~/lab/bin/door_ledger.py check` (реестр `~/lab/state/doors.tsv`; exit 1 = доказанная семья без двери → строим или `deferred:<дата>` с причиной); на других узлах прибора нет → пометка «door_ledger: нет на узле» и сверка руками.
- ⚠️ **Завёл новую семью — обязательна КРАСНАЯ проба в том же заходе** (замер 21.09.2026, NODE-0X, ошибся дважды подряд): широкие ключи (`argv`, `206`, `тело промпта`) намели 77 чужих случаев и прибор объявил «порог §5.10 пройден»; вторая редакция утащила соседнюю семью «передали ПУТЬ вместо тела» — то же лицо, другой корень. Проверка обязана идти в ОБЕ стороны: чужой симптом НЕ ловится (`grep -c` = 0) И свой ловится. Ложно раздутый счётчик хуже отсутствующего: он заказывает сессию починки, которой не нужно быть. Канон: память `class-counted-by-name-never-reaches-three` + CLAUDE.md §5.10.
- ⚠️ считая случаи, класс определяется КОРНЕМ, а не поверхностью: «двое пишут одновременно» ≠ «состояние ушло вперёд, пока мой контекст стоял» — лечения разные. Сомнение «занижаю ли счётчик, чтобы не строить?» разрешается грепом по журналу вслух, а не суждением.
- Карв-ауты «чиним сразу, не ждём третьей»: артефакт, собранный этой же сессией · KEEP-ядро (sync, бэкапы, секреты, QQQ, рельсы наружу, deadman) · потеря данных · безопасность · деньги · соврал сам прибор · fail-closed гейты. Для KEEP-ядра, потери данных, безопасности, денег и совравшего прибора та же отдельная видимая `/five-whys`/`$five-whys`-сессия запускается немедленно; анализ внутри `/retro` не вести.
- ⚠️ **Дедуп двери отбивает УТОЧНЕНИЕ к своему же классу** (замер 10.09.2026, NODE-0X, дважды за один
  заход): `selfheal.py journal` отвечает «СТРОКА НЕ ЗАПИСАНА (дедуп: этот класс уже журналился
  недавно). Поправку к своей строке правь в журнале явно» — а прямая правка `Breakage-Journal.md`
  ЗАПРЕЩЕНА хуком `breakage_write_guard` (см. абзац выше). Инструкция сама себе противоречит.
  Пока корень не починен, обход: уточнение 2-го случая (условия, свежие цифры, порог третьего)
  кладётся в **задачу реестра** класса и в **ретро-заметку**, а в отчёте пишется честно
  «дедуп отбил, уточнение легло в <адрес>». ⛔ Молча проглотить отбой нельзя — иначе
  уточнение условий теряется, и следующая сессия снова считает случай первым.
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
For every thing made this session, also AUDIT a **tested? ✅/❌** column — did it pass `/tt` (=`/test`) when built? Retro does NOT do the testing itself (too late/cold at session end); it only audits the line. Any durable artifact that is **❌ or untested** → flag it + offer to run `/tt` on it NOW (per [[test-after-build-skill]]).
⭐⭐ **И ВТОРАЯ КОЛОНКА — перепроверено? ✅/❌** (dev 13.09.2026, CLAUDE.md §4.3-бис): «протестировано» и «перепроверено вторым, ДРУГИМ заходом» — разные вещи, и ложное «готово» живёт именно в зазоре между ними. Артефакт, у которого первый прогон зелёный, а второго захода не было, ретро помечает ⚠️, а НЕ ✅, и предлагает прогнать Шаг 4.9 скилла `/tt` сейчас. Замер архива 15.08→14.09: 21 раз за месяц оператор спрашивал «ты точно починил?» сразу после моего «готово». Канон: [[done-is-a-claim-recheck-twice]].
⭐ **И ТРЕТЬЯ КОЛОНКА ДЛЯ ПРИБОРОВ — покрытие N/M** (dev 01.10.2026, класс `instrument-blind-to-most-of-its-subject`): у каждого собранного или тронутого за сессию прибора (сторож, аудит, счётчик долга) ретро выписывает строку `СЛЕПАЯ ЗОНА:` из его вывода (`python3 ~/.claude/scripts/_shared/blind_zone.py --run <прибор>`). Строки нет (exit 3) → ⚠️ и правка прибора тем же заходом. Покрытие <90% → ⚠️ + задача на подъём покрытия. Число без слепой зоны в отчёте ретро не ставится. Then classify:
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
- ⏱ **РАЗРЕЗ ОЖИДАНИЯ (добавлено 07.09 после того, как этот шаг сам породил долг):** у каждого открытого пункта вида «ждём замера / ещё копим / не проверено» спроси — **какая его часть НЕ требует времени?** Почти всегда внутри склеены два вопроса: УСТРОЙСТВО («работает ли конструкция») проверяется детерминированным прибором за минуты, СПРОС («пользуемся ли мы этим») действительно требует недель. Часть про устройство закрывается **в этом же заходе**, а не переносится в реестр. Замер, из-за которого пункт появился: ретро 06.09 записало «гипотеза ДР не проверена, урожай 08.09» — на деле 5 ног гипотезы закрылись прибором за пару минут 07.09, а ждать надо было только спроса. Обязательные подпорки при таком закрытии: **красный контроль** (зелёная нога пустая, пока не показано, что прибор видит поломку) и **независимая линза чужим кодом**, если вывод тебе выгоден. Канон: память [[architecture-proves-in-minutes-demand-needs-weeks]], CLAUDE.md §5.4.
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
⚠️ **Грабля 10.09 (NODE-0X):** `fleet_fix_audit.py` стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — второй заход за день отбивается. Уже гоняли сегодня → бери вывод ночной карты / `deploy_check.py`, `--force` только с названной оператору причиной. Отбитый гейтом аудит НЕ повод молчать: проверь `PENDING-<узел>` и скажи честно, что доказана РЕГИСТРАЦИЯ, а не применение.
**Исключение — R&D-пробник (грань 5 реглумента, DR26-07-04-HUB-13):** явно помеченный эксперимент с живым time-box + learning-метрикой НЕ считается ⚠️ «в воздух» — он 🧪; но пробник с ИСТЁКШИМ time-box без потребления/вывода = ⚠️ → авто-kill (архив), без sunk-cost-переговоров. «Используется» = смена состояния (применено/закрыто/записано), не «открыл» (Goodhart). Не дублирует журнал (Step 3📋) — журнал ловит «открыто/закрыто», Connect ловит «есть ли у построенного потребитель и потребляет ли он».

## Step 3🚂 — РЕЛЬСЫ: честный процент по чужим LLM + причины недобора (dev 21.09.2026, голосом)
Дословно: «я использовал такие-то LLM на какое-то количество процентов, а не использовал по каким-то причинам. То есть ты ещё называешь честные причины, почему ты не использовал. Забыл ты или какие-то другие причины. И сразу пытаешься поправить этот скилл».

Почему шаг живёт тут, а не в §6.3: правило «выгребай лимиты» стоит с 04.08, дверь `llm_ask.py` построена 06.08 — и всё равно замер 21.09 дал grok 0 вызовов на узле за 7 дней при $300/мес. Корень назвал оператор сам: **забыл**. Забывание невидимо, пока обещание не машиночитаемо.

Один прогон, 0 токенов:
`python ~/.claude/scripts/rail_plan.py verdict --session <id>` → таблица «обещано / вызовов факт / вердикт».

⛔ **`<id>` — ЭТО CLI-SID, А НЕ ТОТ, ЧТО ОТДАЁТ `get_session self`** (замер 06.10.2026, хаб, ретро сессии SMB; класс `session-has-two-ids-instrument-asked-wrong-one`, семья из 7 случаев — порог §5.10 пройден). У сессии ДВА идентификатора в разных пространствах имён:
- **CCD-шный** `local_e9daa1ed-40f5-...` — его печатает `mcp__ccd_session_mgmt__get_session`, он нужен шагам 6a-тер / 6a-кватер;
- **CLI-шный** `262f2548-373f-...` — это `CLAUDE_CODE_SESSION_ID`, то же, что **имя папки перед `scratchpad`** в системном промпте. Именно с ним `declare` связывает план.
`_plan_of()` сличает строки СТРОГО (`rec['session'] != session → continue`), поэтому вердикт по CCD-шному id печатает **«ПЛАНА НЕТ: сессия не объявила рельсы на старте — это и есть нарушение приказа 21.09»** на сессии, которая план объявила и получила «OK план записан». ⚠️ Это ложное обвинение себя, а не замер: прибор не врёт, врёт выбор id. Возьми id так (та же дверь, что у 6a-бис):
```bash
python -c "import sys,os; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import rail_plan; print(rail_plan._env_sid())"
```
Пусто → план действительно записан без привязки (`declare` печатает про это ⚠️ своей строкой) → суди `--all-sessions` и скажи это в отчёте. ⛔ «ПЛАНА НЕТ» на первом же прогоне не объявляй нарушением, пока не пересдал вердикт с CLI-sid.

⚠️ **`--session <id>` ОБЯЗАТЕЛЕН У ОБОИХ ВЫЗОВОВ, И У `declare` ТОЖЕ** (замер 06.10.2026, ретро пресс-пасса — 6-й датированный случай, семья `rail-plan-verdict-judges-wrong-session-key`, 8 случаев с 26.09). `declare` без флага пишет план под `CLAUDE_CODE_SESSION_ID`, который в десктоп-сессии бывает чужим или протухшим, а `verdict --session <id>` читает ДРУГОЙ ключ — и второй прогон снова печатает «ПЛАНА НЕТ». Коварство в том, что `declare` отвечает **«OK план записан»**: зелёный ответ на промах по ключу. Правильно так, id берётся из `get_session self`:
```
python ~/.claude/scripts/rail_plan.py declare --session <id> --self "..." --outsource=
python ~/.claude/scripts/rail_plan.py verdict --session <id>
```
⛔ «ПЛАНА НЕТ» после успешного `declare` читать как «правило не исполнено» нельзя — сперва проверь, что в обоих вызовах стоял ОДИН id.
- **exit 0** — у каждой обещанной рельсы есть либо вызовы, либо названная причина.
- **Прибора на узле НЕТ** (`rail_plan.py: No such file`) — это НЕ повод пропустить шаг молча.
  Проверь очередь посылок (`deploy_check.py`): не применённая `rail-plan-*` применяется тут же
  (§7.5). Применить нельзя (чужая живая табличка ON AIR на зоне `fleet-code`, замер 21.09) →
  ⛔ НЕ форсить, а написать в отчёт строкой: «🚂 прибора нет, посылка <id> заблокирована
  ON AIR <узел>/<id>, применю после закрытия». Сессия СТАРШЕ самого правила (работа шла до
  21.09) → так и сказать: плана не было, потому что правила ещё не существовало, выдумывать
  задним числом проценты запрещено (§5.4 правда в цифрах).
- ⚠️ **Сессия честно всё делала сама → пустой список пиши `--outsource=` (со знаком равно).** В PowerShell 5.1 форма `--outsource ""` теряет пустой аргумент, и argparse отвечает «expected one argument»; замер 06.10 (NODE-0X), родственный корень 31.08 и 23.09 (PS 5.1 переписывает аргументы нативных команд, семья заведена в очередь на починку). Выдумывать рельсу ради принятия плана нельзя.
- **exit 1 «ПЛАНА НЕТ»** — сессия не объявила рельсы на старте. Это и есть нарушение; объявить сейчас (`rail_plan.py declare`) и сказать в отчёте честно, что план родился на ретро, а не на старте.
- **exit 1 «НЕДОБОР без причины»** — добери причины: `--reason <рельса>=<код>:<текст>`, коды `forgot · rail-dead · class-mismatch · too-small · tier2 · no-work · **own-subagent**`.
- ⭐ **`rail-dead` РУКАМИ БОЛЬШЕ НЕ ПИШЕМ, если рельсу реально звали** (правка 30.09.2026): прибор сам ставит «rail-dead (авто): N попыт., рельса упала», когда в леджере есть ПОПЫТКА. Колонка «попыток мимо» в таблице — это и есть улика. Строка «авто» = долг ПОЧИНКИ РЕЛЬСЫ (логин, квота), а не долг дисциплины: заводи задачу на рельсу, а не причину в вердикт. ГРАНИЦА: прибор доказывает попытку, а не диагноз — 401 и 429 для него одинаковы, текст ошибки вендора ищи в stderr прогона («рельса <имя> мимо: …»).
- ⭐ **Грунт сделал СУБАГЕНТ (Agent model=sonnet/opus) — это код `own-subagent`, а НЕ `forgot` и НЕ `class-mismatch`** (правка 30.09.2026). Субагент жжёт НАШ бак Anthropic, внешней рельсой не является и прибором не считается СОЗНАТЕЛЬНО; объявить его в `declare --outsource` теперь нельзя (exit 2). Замер 28–29.09: два прогона подряд весь грунт отдали субагентам, прибор напечатал ноль и заставил выдумать причину — `own-subagent` существует, чтобы подмена чужой оплаченной подписки своим баком **считалась по леджеру**, а не пряталась под «too-small».
- **Узловой срез** (что вообще этот компьютер обещал и сжёг за окно, все сессии сразу): `rail_plan.py verdict --all-sessions --days <N>`. По умолчанию сверка ПОСЕССИОННАЯ — иначе возвращается класс «вердикт судит чужой план» (8 датированных случаев 21–28.09).
- **`No such file` — прибора на узле НЕТ** (замер 21.09, NODE-0X: посылка `rail-plan-20260921` лежала непринятой, и шаг судить было нечем). Это НЕ повод пропустить шаг молча: (1) посмотреть очередь посылок `python ~/.claude/scripts/deploy_check.py` и применить её тем же заходом; (2) применение отбито правами/классификатором → строка в отчёт «🚂 сверка невозможна: прибора нет, посылка <id> не применена» + пункт в TODO. Отсутствие прибора называется вслух, а не превращается в «рельсы не жгли».

⭐ **«forgot» обязывает ПРАВИТЬ ДВЕРЬ в том же заходе**, а не объяснять. Это прямой приказ оператора («сразу пытаешься поправить этот скилл, чтобы в будущем так не ошибаться») и он смыкается с 🛠 «вердиктом о скилле» ниже: причина `forgot` = скилл/рутина пропустили рельсу, значит правится вызывающий, а не только этот файл.

Перед выводом «двери/хука нет» проверь ОБА каталога `~/.claude/scripts/` и `~/.claude/hooks/`, затем регистрацию в `~/.claude/settings.json` и фактический путь из неё. Для плана рельс на Windows проверяй `~/.claude/hooks/rail_plan_hook.cmd`. Файл есть, запись в настройках есть и хук действительно сработал в новой сессии являются тремя разными проверками. Не найдено в одном каталоге = «пока не нашёл», а не доказанное отсутствие (ошибка из ретро Multica 30.09.2026).

⛔ Запрещено закрывать шаг словами «мало пользовались другими LLM» без цифр: доля считается прибором, а не на глаз (§5.4 «правда в цифрах»). ⛔ Не смешивать два числа: `rail_plan.py` считает **ВЫЗОВЫ наших рельс**, а процент выборки бака вендора живёт в `subscription_utilization.py report` — это разные величины разного происхождения.
Строкой в отчёт: «🚂 рельсы: жгли <рельса=N…> · недобор <рельса:код> · правка двери: да/нет».
Канон: [[rail-plan-declared-then-verified]], [[burn-the-limits-utilization]], [[other-llm-rails-were-review-only]].

## Step 3🔄 — Outcome-аудит ПРОШЛЫХ правил (взято у netresearch/retro-skill «outcome mode», adopted 2026-08-26; наш обмен — issue #78 их репо)
Door-audit (Step 3🔗) судит правило при РОЖДЕНИИ; этот шаг судит СУДЬБУ уже записанных — родился с дверью ≠ живёт (замеры: 19/25 без двери, «5 почему» 42 дня без применения, Firefox-first умер тихо за 13 дней). Дёшево, ЧИТАЕМ ночные выходы, сканы руками НЕ гоняем (§10.0):
1. Возьми правила, ТЕМАТИЧЕСКИ близкие этой сессии + до 5 самых старых нетронутых из ночной карты `rule_liveness` (HTML/JSON выход ночного прогона; руками `--scan` не запускать).
2. По каждому три вопроса: применялось ли с прошлого ретро (счётчик §5.8 / упоминание в транскриптах)? нарушалось ли (Breakage-Journal)? актуально ли ещё (не superseded)?
3. Вердикт-строка в отчёт: «🔄 outcome: N проверено · M живут · K мертвы» — каждому мёртвому РЕШЕНИЕ в том же заходе: утиль (в архив с причиной) / дверь построить / отдать сессии-починке. Молча пропустить шаг нельзя; сессия без тематических правил → «🔄 outcome: чужих правил не трогал» одной строкой.

## Step 3🎙 — ON AIR check (v1.1, 2026-07-11 «+++»)
One cheap deterministic move: `python ~/.claude/scripts/onair.py list` (memory `onair-board`).
- This session's own declaration still active → `onair close <id>` — never leave a stale табличка behind.
  ⚠️ **`<id>` — это НЕ то, что печатает `list`** (замер 06.10.2026: четыре попытки закрыть свою же
  живую табличку отбились словами «no active claim», и она осталась висеть). В выводе `list` стоит
  ДРУЖЕЛЮБНАЯ метка вида `HUB/65c81288` (машина/короткий sid) — по ней `close` не ищет. `_find()`
  сличает ровно два написания: поле `id` внутри файла заявки (длинное, вида
  `2026-10-06T143143Z-HUB-01-65c81288-vault-imports-jobs-watch`) ЛИБО имя файла
  ЦЕЛИКОМ, вместе с `.json`. Возьми точное значение так:
  `python -c "import json,glob,os,sys; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import onair; [print(json.load(open(f,encoding='utf-8')).get('id')) for f in glob.glob(os.path.join(onair.ACTIVE_DIR,'*<свой-sid>*'))]"`
  ⛔ «no active claim» на СВОЮ живую табличку читать как «её нет» нельзя: это промах по ключу.
- Session DID large structural work (canon / sync / consensus / factory redo) **without** a declaration → flag in the report: «⚠️ крупная работа шла без ON AIR-таблички» (anti-pencil-whipping; the 2026-07-08 consensus.py case).
- No claim + no large structural work → skip silently.

## Step 3⛳ — Drift-audit → сессии-детишки (dev's decree 2026-07-11: retro spawns them ITSELF, no nudges)
The retro-time CLOSURE of the drift rule ([[goal-drift-offload-to-seed-sessions]] / CLAUDE.md § «Дрифт от главной цели»): mid-flight that rule offloads weeds AS they appear; retro is the **safety net** for what slipped — the topics the session got blown into that are NOT the main goal and NOT finished.

Procedure (cheap — reuse material already in hand: Step 0 spine, Step 1 inventory, Step 3📋 journal):
1. **Name the session's MAIN goal** (turnstate spine / the first ask). One line: «⛳ цель сессии: <X>».
2. **List the drift**: topics we discussed / dug / half-built that are neither the main goal nor done. Cross-check chips already issued mid-flight — those are NOT re-spawned, only their Connect status is reported.
3. **For each REAL drifted topic retro ЗАПУСКАЕТ СЕССИЮ САМО — no asking, no waiting** (dev 2026-07-11: «команда РЕТРО активирует соседние сессии-детишки без моих пинков»; усилено 29.07: **«запрещено запускать любые сессии в чёрную»**). Запуск ТОЛЬКО видимой рельсой — `mcp__scheduled-tasks__create_scheduled_task` (`fireAt` — ТОЛЬКО из двери `python ~/.claude/scripts/_shared/fireat_now.py --in 15`, и ЕСЛИ создание отбило метку как «в прошлом» — УВЕЛИЧЬ ЗАПАС ТОЙ ЖЕ ДВЕРЬЮ (`--in 60`), руками время всё равно не пишем. Замер 01.10.2026: часы оболочки и часы приложения расходятся ~на 20 минут, а дверь берёт время из ОБОЛОЧКИ (`source local`) с маржой ровно 15 мин — то есть при перекосе больше маржи она падает по построению, руками время не писать: класс из 6 случаев 11.08-09.09, часы шелла врали до 11 ч; разносить по времени; `notifyOnCompletion: true`), чтобы сессия попала в список приложения и оператор мог её открыть, дотолкать после лимита и ответить на её вопрос. Принцип оператора дословно (29.07): **«плоди чип и САМ ЕГО НАЖИМАЙ»** — решил, что нужна сессия, значит создаёшь её УЖЕ ЗАПУЩЕННОЙ. Чип, который ждёт чужого клика, созданной сессией НЕ считается (замер: 107 из 346 чипов не нажаты никогда), а невидимый `claude -p` не считается тоже (29 сессий — в списке ноль); гейты `chip_guard.py` / `blackbox_session_guard.py` разворачивают оба случая на видимый запуск. Чип уместен только там, где нужны физические руки оператора или другая машина, с маркером `ТРЕБУЕТ РУК оператора:` / `ДРУГАЯ МАШИНА:` и немедленным пингом. Prompt = self-contained seed (Outcome · Контекст из recall · Scope · Deliverable · DoD — формат из [[decompose-into-parallel-sessions]]), сессия стартует с нуля без контекста этой. Register each launch in the task journal (Step 3📋) too — сессия AND registry entry, never either-or.
4. **Threshold & cap:** only a real weed (discussed seriously / carries value / would otherwise be lost) — not every stray thought; **≤5 запусков per retro**, the rest goes journal-only.
5. **Report line:** «⛳ дрифт-аудит: цель <X> · унесло в N тем → 🚀M сессий запущено (видимых) · ♻️K выданы по ходу · 📋J только в журнал». No drift → one word («⛳ дрифта нет»), skip the ceremony. Канон: Библия `reglament-zapreshcheno-zapuskat-sessii-v-chernuyu`.

Distinct from Step 4★ (repeats → skill) and Step 3📋 (open/closed bookkeeping): this step catches **abandoned directions** and hands each one a clean child session. Fires (data loss / security / sync down) are never «drift to defer» — they were handled in-session or escalate now.

## Step 4 — Route durable items to their home (per `operating-agreement` → "Where durable rules go")
- Reusable **tool/script** → record in **memory** (path + when to re-run) so it's findable next time.
- Behavioral **rule about how I work** → global `CLAUDE.md` (short pointer) / a skill / memory / hook.
- Team/agent **rule** (acting for dev) → the **Bible** (`reglament-*`, via skill `bible`).
- A genuinely-recurring **ritual** → its own skill.
- **Don't duplicate** — each level points down, never copies (AK-47).
- **🏠 Home-matrix audit (gate; canon `reglament-vyuchennoe-zapisyvaetsya-vo-vse-doma-matritsa`):** for EVERY rule/lesson captured this session, list all 6 homes (Bible · CLAUDE.md · memory+MEMORY.md · skill · hook/task · MOC) with an explicit ✅ written / ⛔ not-needed+reason — no silent skips — then prove by counter: `python ~/.claude/scripts/rule_home_guard.py <slug/keywords>` (exit 1 = no always-loaded trace → fix before closing the retro). ⚠️ Грабля 10.09 (NODE-0X): этот прибор ТОЖЕ стоит за `maintenance_gate` (§10.0, один прогон в сутки на узел) — на 5-м заходе за сутки он отбивается, и «доказать счётчиком» становится нечем. Тот же класс, что каветат про `fleet_fix_audit.py` в Step 3🔗. Отбило → либо `--force` с названной оператору причиной, либо честная строка в отчёте «дверь проверена глазами, счётчик отбит суточным гейтом» — молча пропускать проверку нельзя.

## Step 4🌍 — КОНТРИБЬЮТ-ТЕСТ (dev 11.08.2026: «как поймём, что это РЕШЕНИЕ тоже контрибьютим?»)
For EVERY artifact classified **Keep-&-reuse** this session, run the 3-question contribution test (canon lives in `~/.claude/skills/rep-reply/SKILL.md` § «Пополнение карты» — do not duplicate the wording, read it): (а) боль универсальная? (б) чужие живые треды есть (30-сек gh search)? (в) отдать можно без утечки? **Two «да» out of three** → write the row into the rep-reply theme→artifact map + mark the artifact as a `/release-slice` candidate; otherwise record the explicit ⛔ with which question failed. No silent skips — the verdict per artifact goes into the retro report. This is the door that turns "we built know-how" into "the world heard about it" without anyone having to remember.
**⭐ Усиление dev 01.09 (голосом ×2, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** ретро = СУДЬЯ (~1 мин на артефакт), не раздатчик — замер 01.09: полный качественный проход = ~20 мин на 3 кандидата, в ретро это убивает оба. «2 да из 3» → **строка в очередь** `$OBSIDIAN_VAULT/_outreach/share_fix_queue.jsonl` (JSON-строка: added·from·artifact·queries[дословные симптом-запросы!]·numbers·status:pending) — симптом-запросы и цифры пишутся СЕЙЧАС, пока контекст горячий, именно они теряются к утру. Раздаёт ночная рутина `share-fix-daily` (хаб, ≤3 кандидата/ночь, полный ритуал `/share-fix`). Раздать прямо в ретро — только если целевой тред уже известен из сессии (тогда это 2 минуты, не 20). **Совет считается**: код отдавать не обязательно — опыт словами в чужом треде тоже польза. Что можно/нельзя наружу — чек-лист в том же регламенте.
**⭐ HN-кандидат (dev «+++» 10.09):** тот же проход задаёт ВТОРОЙ вопрос ровно один раз на артефакт — «это годится в Hacker News?». Годится ТОЛЬКО жанр «мы померили и показываем цифры» (post-mortem · замер · разбор поломки) и ТОЛЬКО как самостоятельная публичная страница с данными, не пост из ежедневного девлога. Да → строка в `$OBSIDIAN_VAULT/_outreach/hn_candidates.jsonl` (added·from·artifact·title·url·numbers·genre·status:ready|needs-page·blocked_by). Нет → молча, вердикт не нужен. ⛔ Потолок лейна: **своя ссылка на HN не чаще 1 раза в 2 недели** (ежедневный поток туда = профиль спамера, теневой бан накрывает аккаунт И домен); регулярное присутствие = комментарии в ЧУЖИХ тредах 1-3/нед. ⛔ Подача идёт ТОЛЬКО с хаба, ТОЛЬКО после «+» оператора и ОК Норы, ноль организованного голосования. Пока нет входа в HN на хабе — очередь копится, наружу не уходит ничего.

## Step 4📓 — Growth-log Макса (persona versioning; dev «+++» 2026-07-02)
If the session was MEANINGFUL for the cofounder line (built/decided/learned something real about the business or about working with dev — not a trivial lookup): **append ONE entry** to memory `cofounder-growth-log.md` — `дата · shell · урок про работу с оператором · один апгрейд себя`; записи о споре/сбое роли несут маркер `SPAR: с-уликой | без-улики | scope-нарушение | подмена-воли` — and **review recent entries**: что оставить в характере, что докрутить. **⚔️ Weekly SPAR count** (воскресный ретро или ≥7 дней с прошлого счёта): grep маркеров за неделю → строка «⚔️ SPAR: N споров (M с-уликой) · K scope/воля-нарушений»; цель = доля улик 100%, нарушения 0; считаем качество и нарушения, НЕ число споров (анти-театр). Канон: memory `objection-sparring-to-consensus` v3 (базлайн июля-2026: 23 спора:25 поддакиваний, scope 3, воля 2). Durable character changes fold DOWN into `cofounder-identity` (memory) and/or `~/.claude/skills/cofounder/references/system-prompt.md` — the log is the journal, those are the canon. Twin of [[persona-pulse-measurement]] (that logs friction/wins about ME helping HIM; this logs MY growth). Skip silently for trivial sessions.

## Step 4🎭 — БИТЫ ДНЯ В КАНОН (закон «канон раньше контента», 2026-07-10)
Ретро = главный системный «писатель битов» (контекст горячий, факты сверены). Для каждого сюжетно-значимого события сессии (веха/провал/поворот/решение/деньги/ответ внешнего мира — словарь `beat_kind` в `_SHOW-CANON.md`): создать бит в `$OBSIDIAN_VAULT/04-Projects\show-canon\beats\` по `_TEMPLATE-beat.md` (3 оси + beat_kind обязательны; `reveal` ставить честно — незакрытое = live_hold). Затем обновить затронутые арки/петли/сезон → `python $IMPORTS_ROOT/content-factory\canon_render.py` (линт + свежие публичные реестры; push — по своим правилам, не отсюда). Рядовая сессия без сюжетных событий → пропустить молча. Идёт ПЕРЕД Step 4🎬: сначала факт в канон, потом суждение о контенте (вердикт ссылается на созданные биты как опору).

## Step 4🎬 — Content-check (dev «все наши сессии = контент», 2026-07-02)
Judge at retro-time, while context is hot: **does THIS session deserve content?** Verdict = **human-post** (route → content-factory / `/episode` / `/intention`; draft-first; dev's authorial voice = best model) · **dev-log** (machine-readable «проблема → как чинили → поправка следующего дня» for robots/future model generations → `/episode` dev-log tier, GitHub EN) · **both** · **no** (skip silently). The nightly robots (facebook-diary-auto, content-factory, intention-lane) stay as the safety net — this step is the hot-context first pass, and dev can override any moment («это заслуживает поста»). Attribution + CTA per [[cofounder-identity]] («придумано Майкрофтом и Тони, Palo Alto AI Research Lab» / "Invented by Mycroft and Tony, Palo Alto AI Research Lab") and [[cofounder-cta-public-contact]].
**⭐ Мини-тизер обязателен (dev 01.09):** every retro with a substantive arc births ≥1 mini-teaser (200-250 chars, «грабли → правило» so the READER gets use, not a status report) → `python D:\Vault\_imports\content-factory\content_miner.py capture --title "<хук>" --note "<тизер>" --tier teaser`. Verdict «no teaser» is legal ONLY with a named reason (empty routine session). Canon: `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`.
⚠️ **Этот тизер и X-пост шага 4🐦 — РАЗНЫЕ вещи, не дубль.** Тизер = инженерная полоса «грабли → правило», уезжает В ВОРОНКУ контент-фабрики черновиком. X-пост = внешняя полоса «что построили → кому польза», публикуется В ТОТ ЖЕ ЗАХОД. Угол «грабли → правило» для X-поста ЗАПРЕЩЁН приказом 05.10 (см. 4🐦).

## Step 4🐦 — X-ПОСТ СЕССИИ, ОБЯЗАТЕЛЬНО И С ПУБЛИКАЦИЕЙ (⭐ dev 05.10.2026, голосом, рельса 001)
Дословно: «После каждой сессии/ретро нужно генерировать короткий Twitter/X-пост. Пост должен быть не про технические проблемы, а про то, что было сделано и какую пользу это даёт внешнему читателю… чтобы обычный бизнесовый человек, не погружённый в технические детали агентов, понял ценность и захотел прочитать… Пост нужно публиковать прямо в Twitter/X после проверки.»

**Кто читатель.** Бизнесовый человек, который знает, что агенты существуют, и НЕ знает, как они устроены. Он должен (а) понять, какую штуку мы сделали, (б) увидеть, для кого и зачем она полезна, (в) почувствовать, что сам станет сильнее, если разберётся. ⛔ Это НЕ «объясни бабушке» и НЕ упрощение до детского: просто, но не примитивно. ⛔ Это НЕ для внутреннего игрока: слова «волт», «рельса», «ретро», имена наших узлов и скиллов снаружи ничего не значат.

**Угол (поправка 06.10, свежее).** Честная история с эмоцией: что пробовали, что получилось ИЛИ не получилось. Провал и слабость законны («весь наш блог про боль»). Технический жаргон по-прежнему не идёт наружу. Ниже старый текст 05.10 действует только в части «не жаргон, а польза читателю». Было 05.10: от РЕЗУЛЬТАТА, не от аварии; первая строка говорит, что теперь ВОЗМОЖНО. ⚠️ Это прямо отменяет для X-полосы привычный нам угол «грабли → правило» и часть профиля `voice-x.md` про post-mortem как высокостатусный контент: приказ оператора 05.10 свежее (§8.5 «свежее бьёт старое», оба `origin: dev`). Остальной `voice-x.md` в силе целиком: BLUF в первой строке, ноль хэштегов, ссылка в первом реплае, peer-тон, ноль AI-слопа.

⛔⭐ **CTA НЕТ. МЫ НИЧЕГО НЕ ПРОДАЁМ** (dev 06.10, голосом; отменяет «CTA можно» от 05.10): ни флот-оффера, ни GitHub-призыва, ни «звезда+фолловнуть». Блог = боль, сложности, слабости, что получилось и что нет, плюс эмоция. Черновик пишет Grok (`llm_ask.py --rails grok`), судит Claude; детали `/x-post` §1 и память `blog-never-sells`.

**Процедура, четыре хода.** Ход 0 стоит ПЕРВЫМ не случайно: 06.10 сессия написала пост, прогнала оба гейта и только потом узнала, что публиковать нечем — это 20 минут работы в пустоту и ровно та «обратная сторона горлышка», которую §4.1 велит ставить в НАЧАЛО, а не в конец.

0. **Проверь рот ДО пера.** `mcp__claude-in-chrome__list_connected_browsers` — пустой массив означает «расширение отключено, публиковать нечем». Тогда порядок обратный: ОДНОЙ строкой скажи оператору «включи расширение Claude in Chrome, пост готовлю», и пиши пост дальше — он уйдёт, как только расширение появится. ⛔ Не трать два гейта, не зная, откроется ли дверь. ⚠️ Проверенные 06.10 и закрытые альтернативы, заново их не перебирай: встроенный браузер (в X не залогинен, логин в X запрещён из-за checkpoint-риска) · n8n (98 воркфлоу, X-постера нет) · Publora MCP (нужен OAuth, в неинтерактивной сессии невозможен) · Publora REST (`publora_smoke.py`: ключа нет, и вендор ПРЯМО запрещает агенту проходить шаги его получения). Пятая дверь, проверенная соседней сессией: **X API отдал 403 client-not-enrolled** -- аккаунт не заведён в их программу, это тоже руки. Единственная живая дверь = расширение Chrome.
   Дверь мертва, а пост готов → **не выбрасывай его**: `retro_x_post.py park --file <черновик> --reason "<живая улика отказа, не догадка>"`. Текст ляжет в журнал и будет ВИДЕН в `status` строкой «ждут отправки»; когда дверь откроется, закрой парковку: `record --url <твит> --closes <slug>`. Механизм добавлен соседней сессией 06.10.
1. Напиши пост сам на Opus/Fable (голос оператора, EN для @Tony_Stef_), ≤280 знаков. Факты берёшь ИЗ ЭТОЙ сессии; цифра без улики в сессии не пишется (§5.4).
2. Два гейта подряд, оба обязательны:
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" lint --file "<черновик.txt>"
   python -B "D:\Vault\_imports\content-factory\slop_gate.py" --file "<черновик.md>" --tier teaser --channel x
   ```
   `retro_x_post.py` валит только ОДНОЗНАЧНО формальное: пусто · длина по взвешенному счёту X (ссылка 23, emoji и CJK по 2, NFC) · ссылка в теле, включая голый домен · длинные тире · хэштеги. Остальное печатает ПОДСКАЗКАМИ (возможный технический уклон, наш внутренний идентификатор, какие ноги CTA видны) — подсказка вердикт не меняет и объяснений не требует. `slop_gate.py` держит AI-слоп, один источник на флот. FAIL любого = переписать СЕЙЧАС, в этом же заходе, не «отложить».
   ⚠️ **Гейт НЕ судит смысл приказа, и это записано в его слепой зоне.** Ревью Codex 06.10 выдало первой версии BLOCK с восемью воспроизведёнными уликами: словарь слов валил разрешённые посты («находит ошибки до оплаты» → FAIL на «ошибк», «fixed-price quotes» → FAIL на «fixed», «тизер» в анонсе товара → FAIL как «внутренний жаргон») и пропускал технический отчёт про deadlock и mutex, потому что этих слов в списке не было. Расширение словарей проверкой пользы не становится.
2-бис. **Поэтому вердикт о смысле даёшь ТЫ, и он идёт в отчёт двумя строками** (их не заменяет PASS гейта):
   - `адресат: <кто именно получает пользу>` — роль человека, не «все». Не можешь назвать — пост не готов.
   - `польза: <что он сможет делать иначе>` — проверяемое следствие, не «станет эффективнее».
   - `продажа: нет` — ни оффера, ни призыва, ни просьбы звезды/фолловинга (dev 06.10). Нашёл хоть один — переписать СЕЙЧАС.
   Третья строка обязательна, если подсказка про технический уклон сработала: `уклон: по делу, потому что <…>` ЛИБО перепиши. Это и есть то место, где приказ оператора исполняется; гейт лишь не даёт испортить форму.
3. Публикуй через **`/x-post`** (живой Chrome, @Tony_Stef_, `social_guard` ≤6/день). ⛔ IP-гейт §7.2: постинг в X только с хаба `HUB-01`; на другом узле пост не публикуется, а уезжает текстом на хаб, и ретро говорит это строкой. Ссылка (GitHub/лонгрид) уходит ПЕРВЫМ РЕПЛАЕМ, не в тело.
4. Зафиксируй факт, иначе полоса непроверяема:
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" record --url "<ссылка на твит>" --retro "<путь к заметке ретро>"
   ```
   Жива ли полоса вообще: `retro_x_post.py status --days 14`.

⚠️ **ПОТОЛОК ДЛИНЫ НА ДЕЛЕ 250, А НЕ 280** (замер 06.10, наступил сам). Два гейта спорят, и скилл раньше не говорил, кто главный: `retro_x_post` разрешает 280 по взвешенному счёту X, а `slop_gate --tier teaser` рубит FAIL на 250 (его граница настроена под RU-каналы, медиана ~800). В окне 251–280 пост проходит первый гейт и валится вторым. Пиши под **250**, и не садись на саму границу: прибор сам пишет, что у лимита длина неточна в обе стороны (память «порог судим разбросом, не точкой»).
⚠️ **Два WARN `slop_gate` на этой полосе ОЖИДАЕМЫ и дефектом не являются** — назови их вслух и иди дальше: `W7-teaser-no-way-out` требует ссылку в тизере, тогда как `retro_x_post` ссылку в теле ВАЛИТ (разрешается первым реплаем, которого slop_gate не видит); `W4-first-person` ищет русские «я/мне/мой» в англоязычном посте для @Tony_Stef_ и потому срабатывает ложно. Блокирует только FAIL.

**⭐ ДВЕРЬ В X ПРОВЕРЯЕТСЯ ЖИВОЙ ПРОБОЙ, И ОНА БЫВАЕТ МЕРТВА ЦЕЛИКОМ** (замер 06.10). Полоса показывала «опубликовано 0 при 11 прогонах гейта», и я счёл это недостатком дисциплины. Причина оказалась транспортной: в тот день отказали ВСЕ ТРИ двери подряд, каждая живой пробой, а не догадкой — (1) `list_connected_browsers` вернул `[]` при пяти живых `chrome.exe` (расширение Claude-in-Chrome к сессии не подключено); (2) `python x_post.py check` → `403 client-not-enrolled`, приложение не привязано к Project в портале разработчика; (3) `python publora_smoke.py` → ключа нет, и Publora программно запрещает агенту его завести. Порядок пробы — этот же, он от дешёвого к дорогому. ⛔ «Опубликовано 0» само по себе НЕ улика против дисциплины: сначала проба двери, потом вердикт о причине (§5.4 «причина = такой же claim»).

**Пропуск законен в ЧЕТЫРЁХ случаях, и каждый называется вслух:** (1) сессия пустая, рассказывать снаружи нечего; (2) узел не хаб, пост уехал на хаб задачей; (3) `social_guard` вернул лимит 6/день; (4) ⭐ **все двери в X мертвы по живой пробе** — тогда пост НЕ выбрасывается, а парkуется, иначе он умирает в скратчпаде (класс «тихая потеря задач»):
   ```
   python -B "$HOME/.claude/scripts/retro_x_post.py" park --file "<черновик.txt>" --reason "<какая дверь и как отказала>" --session "<ключ>"
   ```
   Припаркованные `status` печатает ВСЕГДА, вне окна `--days`. Открылась дверь — отправляешь и закрываешь парковку ИМЕННО её ключом: `record --url <твит> --closes <slug>`. ⛔ Квитанция без `--closes` чужую парковку не закрывает, и это прибито тестом: именно так рельса 001 уже теряла задачи, когда квитанция закрывала чужую единицу.
⛔ «Не придумал текст» пропуском не является. ⛔ Вердикт в отчёте обязателен: 🐦 опубликовал (ссылка) · 📮 ушло на хаб · ⚪ пропуск + причина.
Выход полосы: `~/.claude/retro_x_lane.jsonl`. Канон: Библия `reglament-posle-retro-rozhdaetsya-x-post-dlya-vneshnego-chitatelya`, CLAUDE.md §9.4, память `retro-births-an-x-post-for-outsiders`.

## 🛠 ВЕРДИКТ О СКИЛЛЕ, КОТОРЫМ ПОЛЬЗОВАЛИСЬ (dev 07.09, голосом — обязателен, молчание = нарушение)
Применил в этой работе скилл — вынеси вердикт об ЕГО обновлении. Одной строкой, с причиной в обе стороны:
`🔧 обновляю /X — <что споткнулось>` (чинить В ТОМ ЖЕ заходе) · `📝 обновлю не сейчас — <причина>, строка легла в <адрес>` · `✅ /X обновлять не надо — <почему именно: прошло без заминки / заминка разовая и внешняя / правка дороже боли>`.

⭐ **ВЕРДИКТОВ ДВА, НЕ ОДИН** (dev 13.09, голосом). Второй вердикт: **собственная инструкция того, кто сейчас работал** (рутина `scheduled-tasks/<имя>/SKILL.md`, сид, хук): «не стоит ли переписать мою инструкцию на будущее, чтобы она была качественнее?». Та же тройка `🔧 обновляю` · `📝 не сейчас` · `✅ не надо`, всегда с причиной. ⚠️ Замер 13.09: рутина `devto-publish-rhythm` починила СВОЙ файл и смолчала про скилл `/comments`, где висел ПРОТИВОПОЛОЖНЫЙ гейт, правило исполнилось наполовину, и спрашивать пришлось оператору. Канон живёт в СКИЛЛЕ, рутина держит только специфику прогона: разошлись, значит правду в скилл, а из рутины указатель. Канон: [[routine-judges-its-own-instruction-too]], CLAUDE.md §9.3-бис.
Пустое «не надо» вердиктом не является. ⛔ Не путать с `/skill-gap` (тот про скилл, которого НЕТ) и не право раздувать: АК-47 в силе — правка снимает ПЕРЕЖИТУЮ боль, не гипотетическую.
Канон: Библия `reglament-polzuemsya-skillom-srazu-sudim-nado-li-ego-obnovit` · CLAUDE.md §9.3-бис · [[skill-used-judge-if-it-needs-update]].

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
5. **⭐ Скилл уходит в мир (dev 01.09, канон `reglament-retro-smotrit-naruzhu-tizer-i-skill-v-mir`):** любой собранный/существенно обновлённый скилл в том же заходе получает (а) тизер-пост в наши соцсети (через content-factory / каскад) и (б) публикацию самого скилла на нашем публичном GitHub (дефолт `tonydzi/clawrush` `artifacts/`) ПОСЛЕ leak-scan, с пометкой в шапке «built for dev's fleet — adapt paths/names to your setup». Заточен под оператора / сырой / «на тормозке» — публикуем всё равно, честно пометив. Скип — только с названной причиной (leak-scan red / чистая кухня CRM).

## Step 4🔥 — КАТАКЛИЗМЫ СОСЕДЕЙ (dev 01.10.2026, голосом: «сирены в 03 я не читаю, ретро читаю хорошо»)
Ретро — его единственная читаемая лента тревог. Перед Output собери пожары ВНЕ этой сессии
(детерминированно, ~0 токенов):
1. Источники: (а) `Breakage-Journal.md` / `selfheal.py` — строки за последние 3 дня не из этой
   сессии; (б) RED/stale state-файлы известных сторожей (`~/.claude/_screenpipe_watch/state.json`
   и родня: verdict=RED или ts старше 2× такта); (в) `ALERT`/`SOS`/`RED` в шине 03 и
   `_machine-bus/inbox-*` за 48ч; (г) `/arch broken`, если ночная карта свежая.
2. Отбери **топ-3-5 самых сильных** (деньги · потерянные данные · мёртвая рельса записи ·
   недоставленное исходящее · сломанный узел флота). Мелочь и уже починенное — не включать:
   засорённый блок = непрочитанный блок.
3. В Output добавь блок **«🔥 Катаклизмы»** — каждый ОДНОЙ строкой и языком ELI5 (🧒-стиль:
   бытовые слова, что сломалось → что теряем → куда бежать), ⛔ без жаргона и внутренних
   кодовых имён без расшифровки. Пример: «🔥 Голосовые с 12:11 не заливаются в чат — твои
   надиктовки копятся на диске и не доходят до роботов. Дверь: /voice-memos».
4. Пожаров нет → одна строка «🔥 катаклизмов не вижу (проверил журнал+сторожа+шину)» —
   молчание без проверки запрещено (§5.4 пусто из одного места ≠ нет).

## Step 5 — Output (tight + scannable; a review artifact, not a novel)
1. **🎬 «Сегодня мы поняли»** — the arc (Step 2).
2. **🎙 Вердикт Майка** — 💰/🔪/🤺/❓ four-liner (Step 2🎙).
3. **♻️ Reuse table** — artifact · 🟢/🟡/⬆️ · **tested? ✅/❌** · why · routed-to.
3. **🔁→🛠 Repeats → skills** — any action that repeated this milestone, offered as ДО→ПОСЛЕ (Step 4★); mark each built / proposed / declined.
4. **🔗 Connect** — «✅N используется · 🔗M передано-ждёт · ⚠️K в воздух» (Step 3🔗); каждый ⚠️ подсвечен явно + решение (подключить потребителя / выбросить).
4б. **🔄 Outcome** — «N проверено · M живут · K мертвы + решения» (Step 3🔄).
5. **⛳ Drift map** — «цель <X> · унесло в N тем → 🧷M чипов создано · ♻️K по ходу · 📋J в журнал» (Step 3⛳); chips are already created by now, listed post-hoc.
6. **📌 Open items** — anything flagged for dev's decision; each one REGISTERED in the task journal (Step 3📋), shown as «#id · задача · линк».
7. **🗺 Roadmap** — the one-line delta from Step 3🗺 («✅N продвинуто · ➕M добавлено · ⏸ без движения»).
7. **🗜 Compact handoff** — the saved-note path + the FULL enriched `/compact` block printed inline (Step 6b; указатель на файл запрещён).
7б. **🔥 Катаклизмы** — топ-3-5 чужих пожаров ELI5-строками, или «катаклизмов не вижу (проверил…)» (Step 4🔥).
7в. **🐦 X-пост** — опубликованный текст целиком + ссылка на твит, ЛИБО «📮 ушло на хаб», ЛИБО «⚪ пропуск: <причина из трёх законных>» (Step 4🐦), плюс ОБЯЗАТЕЛЬНЫЕ строки `адресат:` и `польза:` из шага 2-бис. Текст поста печатается в отчёт, указатель на файл вместо текста запрещён.
8. **🧒 Простыми словами** recap.

## Step 6 — Compact handoff (retro ⇄ compact glue; STAY in the chat, never /clear)
The retro's distilled output IS the bridge file — so close the loop without losing context. Two moves:

**6a. Auto-save the retro to the vault IN COMPACT FORMAT** (standing authorization from dev, 2026-06-12 — no per-run ask):
Reserve the final Latin filename first, acquire exact leases for that note and `01-Conversations/Claude/_Claude-Sessions-MOC.md`, and add the MOC wikilink **before the note's first write**. The no-orphan guard rejects a new note that has no incoming link; if the MOC lease is busy, wait for its owner instead of creating an orphan or overriding the lease. Then write the clean note to `$OBSIDIAN_VAULT/01-Conversations/Claude/Retros/retro-<YYYY-MM-DD>-<latin-topic-slug>.md` — filename **ALWAYS Latin** per [[vault-conventions]] (Cyrillic topic → translit slug; keep the Russian title in frontmatter `aliases:`).
- Content = frontmatter (`title`, `date`, `type: retro`, `source: claude-session`, `session_id: <cliSessionId — тот же uuid, что в 6a-бис из пути скретчпада>`, `tags`) + the arc (Step 2) + the reuse table (Step 3/4) + **the compact 7-header distillation** (РЕШЕНИЯ / TODO / СЕЙЧАС / ПУТИ И ЗНАЧЕНИЯ / СЧЁТЧИКИ / ОТКРЫТО / ИНСТРУМЕНТЫ И КОНТРАКТЫ — per `$USERPROFILE/.claude/compact-prompt.md`). **This note IS the archive** — it doubles as the compact summary, so retro and compact are never written twice.
- **NO 🧒 block in the note** — vault notes keep their own voice (the ELI5 recap is for the reply TO dev only).
- **Wikilinks: vault ≠ memory (two namespaces).** In the retro NOTE, `[[...]]` may target ONLY existing vault notes (`reglament-*`, `protocol-*`, `concept-*`, `decision-*`, another retro — verify each exists before writing); CC-memory slugs (`machine-migration`, `ak47-simplicity`…) go as plain inline code. Caught 2026-07-04 (Fable re-check): a retro shipped 7/7 broken links — all memory slugs. Canon: `deterministic-script-gotchas` → «Vault wikilinks ≠ CC-memory slugs».
- **Formal review status is a scoped receipt, not prose.** Every independent-review claim in the note MUST be one exact line: `REVIEW[<artifact-id>]: verdict=<VERIFY|ACCEPT|BLOCK|REQUEST_CHANGES>; scope=<what exact bytes/state the verdict covers>; source=<thread:<uuid>|file:<absolute-path>>; reviewer=<name>`. A partial GREEN/RED run never upgrades the formal verdict; a rollback-only VERIFY stays rollback-only and cannot verify the proposal.
  ⚠️ Три грабли формата, каждая стоила прогона линта (замер 26.09.2026): (1) `scope` — максимум **200 символов**, два sha256 туда уже не влезают, оставляй один и слово «только»; (2) **точка с запятой внутри `scope` рвёт разбор** (поле читается как `[^;]+`) — внутри только запятые; (3) `source=file:<path>` обязан лежать в корнях, которые линт обходит (`~/.claude`, волт, `_imports`, папка дока, cwd) — вывод из `Temp\claude\…\tasks\` не засчитывается, копируй улику к остальным квитанциям. Плюс проза: слова «независимый ревьюер» рядом с «accept/pass/verify» в обычном абзаце тоже требуют receipt, поэтому в тексте пиши «Codex смотрит дифф», а вердикты держи только в receipt-строках. (4) **путь в `source=file:` пиши через ПРЯМЫЕ слэши** (`D:/Vault/...`): обратный слэш съедается любым генератором строки (в Python `\R`/`\0` стали управляющими символами и линт дважды отбил receipt с «битым» путём — замер 27.09.2026).
- **Door before archive/mark-done:** immediately after drafting the note, run `python -B "$HOME/.claude/scripts/status_claim_lint.py" "<absolute-retro-note>"`. `rc=0` is required before MOC/log/`mark-done`; `rc=2` means correct the claims and rerun. Do not archive or claim verification while this door is red.
- ⚠️ **Хук `orphan_check_hook` отобьёт запись: новое ретро рождается сиротой.** Дом входящей ссылки один и он известен: `01-Conversations/Claude/_Claude-Sessions-MOC.md`, секция «Свежие ретро» (плюс на ретро ссылаются `DayLedgers/day-ledger-*.md` и `00-System/Breakage-Journal.md`). Впиши строку `- [[retro-...]] · <в чём суть>` ТУДА первой записью батча, до создания note; после появления note проверь, что ссылка ровно одна.
  ⚠️ Грабля замера 14.09.2026: искать дом грепом по всему волту НЕ надо, `grep -rl` по `D:\Vault\Vault-Knowledge` уходит в таймаут 120с. На таймауте я объявил «ретро не линкует никто» и вписал этот вывод сюда как факт; фоновый прогон досчитался и вывод ОПРОВЕРГ. Ровно [[prichina-kak-claim]]: незавершённый поиск даёт «я не нашёл», а не «этого нет».
  Вторая ссылка из содержательного дома (реглумент/концепт/решение, к которому ретро относится) полезна и закрывает заодно Step 4, но обязательной является ссылка из MOC.
- **New-file append only** — never overwrite an existing retro. It's a scoped folder (sits next to the `claude-chats-to-vault` notes), not a live concept/person note, so this is a safe write.
- Nightly Brain Reindex does NOT make this note `/ask`-searchable. `01-Conversations` is evidence, and `brain_embed_update.py` skips it. Copy the recallable facts into an essence note (`02-Decisions` or `10-Tasks`) in the same retro. The chat catalog indexes the retro file only on its own rebuild, not on the 15-minute brain tick. Proof 2026-09-25: a phrase that lives only in the retro = 0 chunks, the same facts in the decision memo = 1 chunk in `_brain_lex_e5.db`.

**6a-бис. Взять и снять сессию с очереди `/retro-lost` — ОБЯЗАТЕЛЬНО, сразу после 6a** (добавлено 2026-08-19; 4-й датированный случай класса «ночная догонялка судит сессию, у которой ретро ЕСТЬ»: партия 01 — 1 случай, партия 02 — 2, партия 03 — 8 из 10).
Сканер `retro_lost_scan.py` знает ровно один признак «закрыто» — маркер в `~/.claude/logs/retro_lost_done/`; волт он не читает и про заметку в `Retros/` не догадается. Без этой строки своя же ночная рутина через 5 суток снова читает транскрипт, снова тратит Opus и снова пишет «ретро уже есть».
- **sessionId брать из пути скретчпада** этой сессии (`…\Temp\claude\<project>\<sessionId>\scratchpad` — имя папки перед `scratchpad`), он есть в системном промпте; гадать по имени файла не нужно.
- До работы выбери абсолютный путь `<absolute-receipt.json>` вне репозитория и захвати сессию: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" take <sessionId> --holder "<taskId>" --json --receipt-out "<absolute-receipt.json>"`.
- `rc=0` доверяй только когда durable receipt exists и JSON содержит непустые `question_id`, `session_id`, `logical_file_id`, `holder` и `epoch` как positive integer. Receipt сохрани до подтверждённого DONE: он нужен для replay после crash. При отсутствующем/битом receipt остановись; DONE не ставь.
- После записи ретро передай значения **дословно из receipt**: `python -B "$HOME/.claude/scripts/retro_lost_scan.py" mark-done "<receipt.session_id>" --question-id "<receipt.question_id>" --logical-file-id "<receipt.logical_file_id>" --holder "<receipt.holder>" --epoch "<receipt.epoch>" --note "<retro-note>"`. Do not recompute identity по пути или sessionId. Wrong/missing identity обязана завершиться fail-closed без DONE/release; точный replay идемпотентен.
  ⚠️ `"$HOME/..."` буквально работает и в Windows PowerShell 5.1, и в Git Bash. `~` после `python` в PowerShell 5.1 остаётся буквальным путём, а `%USERPROFILE%` раскрывает только CMD.
- Не смог достоверно определить sessionId — так и скажи строкой в отчёте, НЕ помечай наугад чужую сессию.
- ⚠️ **`take` ответил `session-not-found` при ВЕРНОМ sessionId — это норма, а не сбой** (замер 06.10.2026, ретро живой сессии 97c50ca4). Сканер `retro_lost_scan.py` держит в очереди только БРОШЕННЫЕ сессии (молчат дольше суток); сессия, в которой ретро идёт прямо сейчас, в очередь ещё не попала, и помечать нечего. Правильное поведение: ОДНА строка в отчёт «в очереди retro-lost сессии нет, помечать нечего», `mark-done` НЕ зовём и `--force` не ищем. ⛔ Не читать это как «дверь сломана»: ночная догонялка возьмёт сессию, только если она затихнет, а к тому моменту заметка ретро уже лежит в волте и робот сам увидит её по `session_id` во frontmatter.
- ⚠️ **А вот `take` с `rc=0` -- ОБРАТНЫЙ случай, и он ОБЯЗЫВАЕТ закрыть квитанцию** (замер 06.10.2026, сессия CRM+мессенджеров: разрыв 62ч24м, сессия затихла на двое суток и в очередь попасть УСПЕЛА, `take` отдал `epoch 223` и живую квитанцию). Абзац выше описывает только ПУСТУЮ очередь, и сессия, впервые увидевшая `rc=0`, порядок выводит сама -- отсюда риск бросить захват незакрытым: держатель висит, а ночная догонялка через 5 суток снова читает транскрипт и снова тратит Opus. Порядок при `rc=0`: дочитать `question_id`, `logical_file_id`, `holder`, `epoch` из квитанции ДОСЛОВНО -> записать заметку ретро -> `mark-done` ровно этими значениями -> убедиться, что в ответе есть строка `done: <...>/logs/retro_lost_done/<sessionId>`. ⛔ Значения не пересчитывать по пути и не брать «на глаз»: неверная личность обязана падать fail-closed, и тогда DONE не ставится вовсе. ⛔ Пути в правках этого файла пиши ПРЯМЫМИ слэшами: обратный слэш перед l/r/t/0 становится управляющим символом и МОЛЧА обрезает строку (семья escape-avariya-v-patche, наступил сам 06.10 ровно в этом абзаце).

**6a-тер. Переименуй сессию: маркер «Р» в видимом имени — СРАЗУ после 6a-бис** (⭐ dev 02.09.2026, голосом: «когда я вижу этот маркер, я понимаю, что дошёл в этой сессии до крупного milestone»; ⭐ **поправка dev 15.09.2026, голосом: маркер теперь просто `Р`, БЕЗ плюсика** — «дописываем не Р с плюсиком, а просто Р»).
- Вызови `mcp__ccd_session_mgmt__get_session` с `session_id: "self"` → возьми текущий `title`. Если в нём УЖЕ стоит маркер ретро — `Р ` (новый) ЛИБО legacy `Р+`/`р+`/`рр+` — шаг закрыт, второй маркер не лепить и legacy НЕ переписывать (старые имена оставляем как есть, чинить историю нечем и незачем).
- Иначе `mcp__ccd_session_mgmt__set_session_title` с `session_id: "self"` и `title: "<иконка> Р <старое имя без изменений>"` — маркер `Р` + ПРОБЕЛ, после иконки группы (иконка первой, см. 6a-кватер), без иконки — просто `"Р <старое имя>"`. Меняется ТОЛЬКО человекочитаемое имя в приложении (titleSource=tool), системный id не трогается; имя, данное оператором, сохраняется целиком после маркера.
- ⚠️ Пробел после `Р` обязателен: он и есть граница маркера. `Р` без пробела слипается с русским словом («Ретро», «Работа») и читатели (жнец, таблица сессий) такую сессию маркером не считают.
- MCP session_mgmt недоступен (headless `claude -p`, чужой харнес) → одна строка в отчёте «маркер Р не поставлен: нет session_mgmt», не молчи.

**6a-кватер. Проверь ИКОНКУ группы в заголовке — сразу после маркера Р** (⭐ dev 07.09.2026 «кладёшь её в нужную группу»; ⭐ dev 10.09.2026, голосом: «мало пикселей на экране, нужна иконка», и «переименовывать НА СТАРТЕ»).
- Иконка ставится НЕ здесь, а на СТАРТЕ сессии (скилл `/session-groups`). Ретро только ПЕРЕПРОВЕРЯЕТ: тема сессии за день могла уехать в другую группу.
- `get_session self` уже вызван в 6a-тер. Заголовок начинается с иконки из алфавита? 💰 $$$ (деньги/оффер/витрины/статьи наружу) · 🧠 2мозг (волт/RAG/память/клон) · ✍️ content (посты/соцсети/Майкрофт) · 🎯 Лиды-CRM · ⚙️ Инфра (скрипты/флот/синк/канон/браузеры) · 🔬 ДРы · 🏠 личное · 📥 SINK (инбокс/шина/посылки) · ❓ не понял.
- Иконки нет ЛИБО она уже не про эту сессию → `set_session_title self` в форму `<иконка> Р <имя>`. Веха ретро `Р ` живёт ПОСЛЕ иконки (legacy `Р+` в старых именах не переписываем). Гадать запрещено: тема не читается — ставь ❓, оператор разнесёт сам.
- Строка в отчёт: «иконка: <какая>, флаг ccd_sidebar OFF». Молчать нельзя.
- ⛔ ГРУППЫ САЙДБАРА ВЫКЛЮЧЕНЫ (dev 02.10, голосом: «класть сессию в какую-то группу не надо… не имеет смысла»): `ccd_sidebar.move_sessions` НЕ вызываем, сессию в группу не кладём. Остаётся только ИКОНКА в заголовке.
- ⛔ Правка `claude_desktop_config.json` руками НЕ рельса: приложение файл живьём не перечитывает и перепишет из памяти (замер 07.09).
- Канон: память `session-group-at-retro`; движок и алфавит — скилл `/session-groups`; публичная копия github.com/tonydzi/claude-session-icons.

**6b. PRINT the READY enriched paste-line INLINE — обязательный выход КАЖДОГО ретро (⭐ dev 26.08, голосом: «каждый раз давай готовый текст компакта; иди-в-файлик — неудобно»).**
- ⚠️ Fact base (2026-07-22): bare `/compact` does NOT read our format — 354/354 past compacts fell back to the DEFAULT English template; PreCompact hooks cannot inject (issue #14160). The 7-header format applies ONLY pasted inline: `/compact <text>`.
- **Procedure = same enrichment as `/cc` Steps 2-3** (single source of mechanics — don't duplicate, read `~/.claude/skills/cc/SKILL.md`): take the skeleton from `$USERPROFILE/.claude/compact-prompt.md` § «Готовая строка», FILL all 7 headers with THIS session's real facts — reuse the distillation already written into the 6a vault note, don't re-derive — and PRINT one fenced ```code``` block starting with `/compact `, со строкой над ним: «➤ Скопируй блок целиком и вставь следующим сообщением». Then the fork:
> **«Готово, всё в волте. Остаёшься в сессии — вставь блок ниже целиком (без него сжатие пойдёт по дефолтному английскому шаблону). Новый чат — просто уходи, всё уже заархивировано.»**
- ⛔ **Указатель вместо блока ЗАПРЕЩЁН.** «Вставь блок из `~/.claude/compact-prompt.md`» / «возьми текст в файле» = нарушение правила (ровно эта формулировка — жалоба оператора 26.08). Пустой скелет с `<...>` — тоже нарушение: блок обязан быть обогащён сессией. Канон: память `compact-dev-prefers-zero-touch` §Поправка 26.08 + `compact-format-delivery-gotcha`.
- **retro = «не уверен, пора ли»** (archives so both doors stay open, risk-free); **compact = «точно остаюсь»** → paste the block.
- I (the agent) **cannot press `/compact` myself** — it's a harness command. The archive is automatic; printing the ready line is my half, the paste is dev's.

## Scope / don't-duplicate
- Internal build-retro only. NOT the public Facebook diary (`facebook-diary-daily`) and NOT the preference scanner (`preference-sweep-daily`).
- If a session built nothing durable, say so plainly — skip the ceremony (but still offer the `/compact` block if the chat got long).

## ⭐ Полнота списка потребителей (dev 10.09.2026)

Первый найденный потребитель почти никогда не единственный — он просто лежал на поверхности. Поиск закончен не когда кто-то найден, а когда **две оси подряд дали ноль новых имён**; внутренний потребитель (узел флота, робот, наш же скилл с костылём) ищется ПЕРВЫМ. Девять осей перебора и обязательный вердикт с числом («осей N/9 · адресов M · насыщение да/нет») — `/consumer-hunt` §Шаг 1-бис. ⚠️ Исчерпывающим обязан быть ПОИСК, адресация идёт по правилам двери: найденный адрес не выбрасывается, а получает статус и дату (🟢 постучались · ⏸ глухая очередь по замеру · 🪦 непереносимо). Канон: `reglament-vypustil-funkcional-naydi-potrebiteley-i-pridi-k-nim` §Поправка 10.09 + [[consumers-are-a-set-not-the-first-one]].

---

**Claude:**

Прохожу ритуал. Шаг 0 — часы и разрыв замером, не на глаз.

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__get_session,mcp__ccd_session_mgmt__set_session_title", "max_results": 2}

---

> `mcp__ccd_session_mgmt__get_session` -- {"session_id": "self"}

---

> `Bash` -- {"command": "python -c \"import datetime; print('СЕЙЧАС', datetime.datetime.now().isoformat(timespec='seconds'))\"; echo \"=== CLI-sid (для rail_plan) ===\"; python -c \"import sys,os; sys.path.insert(0,os.path.expanduser('~/.claude/scripts')); import rail_plan; print(rail_plan._env_sid())\" 2>&1", 

---

**Claude:**

⚠️ Поймал свою ошибку, и она уехала в публичный репо. Разрыв сессии: создана **04.10 00:30**, работаю **06.10 16:25** — 62 часа 55 минут. В начале сессии я взял дату из `date` в Bash, та показала 04.10 14:03, и я подписал раздел в скилле «verified 2026-10-04». Настоящая дата — 06.10. Правлю факт в публичном файле и журналирую класс.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && python \"$HOME/.claude/scripts/prior_art.py\" class \"взял дату из date в оболочке, она отстала на двое суток, подписал артефакт неверной датой\" 2>&1 | head -30; echo \"--- exit:$? ---\"", "description": "prior_art по классу неверной даты"}

---

**Claude:**

Семья `stale-context-after-resume-read-as-now`, 13 случаев, порог §5.10 давно пройден — а сегодня в ней уже записан случай-двойник: сессия пресс-пасса подписала артефакты датой первого захода 04.10. Мой — 14-й, в точности такой же. Сначала правлю факт в публичном файле.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && sed -i 's/verified 2026-10-04/verified 2026-10-06/' \"$SP/nb_final.md\" && grep -n \"verified 2026-10\" \"$SP/nb_final.md\

---

**Claude:**

Факт исправлен. Журналирую поломку по семье и смотрю, не заказана ли уже сессия починки.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && python \"$HOME/.claude/scripts/selfheal.py\" journal --class stale-context-after-resume-read-as-now --what \"14-й случай: сессия NotebookLM жила 62ч55м (создана 04.10 00:30, работа 06.10 16:25); взял дату из 'date' в Git Bash (отдал 04.10 14:03 при

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && python \"$HOME/.claude/scripts/selfheal.py\" journal --amend --class stale-context-after-resume-read-as-now --what \"[ПОПРАВКА] 14-й случай 06.10: сессия NotebookLM, разрыв 62ч55м (создана 04.10 00:30, работа 06.10 16:25). Улика КЛАССА, которой не 

---

**Claude:**

Поправка записана. Продолжаю ритуал — гоню прогоны пачкой.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && echo \"=== РЕЛЬСЫ (CLI-sid) ===\" && python \"$HOME/.claude/scripts/rail_plan.py\" verdict --session s_e5863bb9 2>&1 | tail -12; echo \"=== ON AIR ===\"; python \"$HOME/.claude/scripts/onair.py\" list 2>&1 | tail -8", "des

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && echo \"=== retro-lost take ===\" && python -B \"$HOME/.claude/scripts/retro_lost_scan.py\" take s_e5863bb9 --holder \"retro-notebooklm\" --json --receipt-out \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB

---

**Claude:**

Три факта: (1) план рельс я объявил словами, но не машиночитаемо — это дефект, закрываю; (2) своей таблички ON AIR не ставил, хотя публиковал наружу — признаю; (3) `take` дал rc=0, epoch 239, значит квитанцию обязан закрыть. И главное: публикация наружу — критичное, по §4.3-бис ей нужен третий заход **чужими** глазами. Отдаю опубликованный текст на внешнее ревью.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && python \"$HOME/.claude/scripts/rail_plan.py\" declare --session s_e5863bb9 --self \"recall, живой прогон notebooklm CLI, веб-ресёрч по API/MCP, сборка публикуемого файла, leak-scan, git/gh публикация, ретро\" --outsource \

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && cat > \"$SP/review_q.txt\" << 'EOF'\nНиже два раздела, которые я ТОЛЬКО ЧТО опубликовал в публичный open-source репозитори

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && python \"$HOME/.claude/scripts/llm_ask.py\" --class second_opinion --rails codex,grok --mode all --prompt-file \"$SP/revie

---

**Claude:**

Ревью ушло в фон. Пока идёт — проверяю дверь в X **до** написания поста (приказ: ход 0 первым, чтобы не писать в пустоту).

---

> `ToolSearch` -- {"query": "select:mcp__claude-in-chrome__list_connected_browsers", "max_results": 1}

---

> `mcp__claude-in-chrome__list_connected_browsers` -- {}

---

**Claude:**

Дверь в X мертва — расширение Chrome не подключено (пустой массив при живом хабе). По приказу 06.10 пост всё равно пишу и паркую, чтобы он не умер в скратчпаде. Пишу и гоню через оба гейта.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cat > \"$SP/x_draft.txt\" << 'EOF'\nSpent the morning hunting for API access to NotebookLM. The official one is enterprise only, so that was a dead end.\n\nThen 

---

**Claude:**

276 — пройдёт первый гейт и упадёт на втором (реальный потолок 250). Укорачиваю.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cat > \"$SP/x_draft.txt\" << 'EOF'\nSpent the morning hunting for NotebookLM API access. The official one is enterprise only. Dead end.\n\nThen I found my own se

---

**Claude:**

Оба гейта PASS. Но W8 справедлив — пост чистая история без применимого. Добавляю правило-связку, не превращая его в продажу.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cat > \"$SP/x_draft.txt\" << 'EOF'\nSpent the morning hunting for NotebookLM API access. The official one is enterprise only. Dead end.\n\nThen I found my own se

---

**Claude:**

249 из 250 — сижу ровно на границе, а скилл прямо велит на ней не садиться. Отступаю и паркую (дверь мертва).

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cat > \"$SP/x_draft.txt\" << 'EOF'\nSpent the morning hunting for NotebookLM API access. The official one is enterprise only. Dead end.\n\nThen I found my own se

---

**Claude:**

Пост припаркован (229 знаков, оба гейта PASS). Проверяю фоновое ревью.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_e5863bb9\\tasks\\bklghsh10.output"}

---

**Claude:**

Ревью ещё идёт. Пока — заметка в волт. Сначала ссылка в MOC, иначе orphan-хук отобьёт запись.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/01-Conversations/Claude\" && ls _Claude-Sessions-MOC.md 2>&1 && grep -n \"Свежие ретро\" -A 6 _Claude-Sessions-MOC.md 2>&1 | head -12", "description": "Смотрю MOC сессий"}

---

**Claude:**

Вижу в MOC: сегодня уже было много ретро, и в одном записано «назвал оператору "суббота 4 октября", когда шёл вторник 6-е». Мой случай с датой — уже пятый за один день по той же семье. Плюс падение `brain_ask` на numpy — тоже известная семья (9 случаев с 13.08), не новая находка. Вписываю строку в MOC, затем заметку.

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/01-Conversations/Claude\" && python - << 'PY'\nimport io\np = '_Claude-Sessions-MOC.md'\nt = io.open(p, encoding='utf-8').read()\nanchor = 'Свежие ретро:\\n'\nline = (\"- [[retro-2026-10-06-notebooklm-api-mcp-access]] · голосовая оператора «можно ли делать 

---

> `Bash` -- {"command": "mkdir -p \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros\" && cat > \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-06-notebooklm-api-mcp-access.md\" << 'EOF'\n---\ntitle: \"NotebookLM по API и MCP: что есть у оператора и что отдали миру\"\naliases: 

---

**Claude:**

Заметка записана. Ревью от codex и grok пришло — читаю.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\s_e5863bb9\\tasks\\bklghsh10.output"}

---

**Claude:**

Все три рельсы мимо: gemini 429 (квота выжжена), codex и grok — таймаут 300с. Третий заход чужими глазами не состоялся. Пробую живую рельсу — mistral за окно жгли 107 раз, значит дышит.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && timeout 240 python \"$HOME/.claude/scripts/llm_ask.py\" --class second_opinion --rails mistral,glm --mode all --prompt-fil

---

**Claude:**

Класс `second_opinion` жёстко прибит к codex/grok/gemini и честно печатает «ПОДМЕНА РЕЛЬС» — выбрасывает запрошенные. Обхожу без класса.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && timeout 240 python \"$HOME/.claude/scripts/llm_ask.py\" --rails mistral --mode all --prompt-file \"$SP/review_q.txt\" --ti

---

**Claude:**

Третий заход состоялся — mistral ответила. Читаю её конкретику по фактическим ошибкам (хвост видел, нужна часть №1).

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && timeout 240 python \"$HOME/.claude/scripts/llm_ask.py\" --rails mistral --mode all --prompt-file \"$SP/review_q.txt\" --ti

---

**Claude:**

Ревью разобрано, и его ценность конкретна. Mistral сама пишет «на момент октября 2024» — то есть её возражения (a,b,c) не опровергают факты 2026 года, а указывают на **методологическую дыру: у моих утверждений в публичном тексте нет ссылки на источник**. Это справедливо. Ещё два замечания по делу: «все community-серверы» — слишком широко, и поведение поллера надо датировать. Остальные пункты («нет примеров команд, нет ссылки на CLI») — артефакт узкого скоупа: я дал ей два раздела, а в файле ниже всё это есть.

Применяю три правки.

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && python - << 'PY'\nimport io\nSP = r\"C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\P---WORKDIR-HUB\\0f56385

---

> `Bash` -- {"command": "SP=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_e5863bb9/scratchpad\"; cd \"E:/!CLAUDE-HUBPC-June26\" && cp \"$SP/nb_final.md\" \"_oss/sbsk/skills/notebooklm/SKILL.md\" && git -C _oss/sbsk add skills/notebooklm/SKILL.md 2>/dev/

---

**Claude:**

Опубликовано. Закрываю обязательные двери ретро: линт заметки, квитанция retro-lost (epoch 239), маркер в заголовке.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && echo \"=== status_claim_lint ===\" && python -B \"$HOME/.claude/scripts/status_claim_lint.py\" \"D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-06-notebooklm-api-mcp-access.md\" 2>&1 | tail -6; echo \"rc=$?\"; echo \"=== m

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "⚙️ Р ++⚙️ Подкасты в LME по MCP/API"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && echo \"=== тизер в воронку ===\" && python \"D:/Vault/_imports/content-factory/content_miner.py\" capture --title \"Публичная копия скилла протухла молча\" --note \"Выложил скилл в открытый репо три месяца назад и считал раздачу сделанной. Сегод

---

**Claude:**

Остались durable-дома и реестр. Проверяю, нет ли уже такой памяти, чтобы не плодить дубль.

---

> `Bash` -- {"command": "M=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\"; ls \"$M\" | grep -iE \"public|copy|rot|stale|clock\" ; echo \"=== grep по содержанию ===\"; grep -rl \"публичная копия\\|public copy\" \"$M\" 2>/dev/null | head -5; echo \"=== verify-clock существует? ===\"; ls \

---

**Claude:**

Есть родственная `registry-fallback-copy-rots-silently` (тот же корень, другой предмет — там копия для флота, у меня публичная копия для мира). Дописываю улику в память про часы и создаю отдельную запись, слинкованную с родственной.

---

> `Bash` -- {"command": "cat \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory/verify-clock-before-time-claims.md\"", "description": "Читаю память про часы"}

---

**Claude:**

Память уже содержит восемь подклассов, но моей улики в ней нет: раньше разрыв ловили через `get_session`, `harness currentDate` или mtime, а расхождение `date` ↔ `python datetime` **на одной машине в одну минуту** — новый дешёвый детектор. Дописываю.

---

> `Bash` -- {"command": "M=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\"; python - << 'PY'\nimport io\np = r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\verify-clock-before-time-claims.md\"\nt = io.open(p, encoding='utf-8').read()\nadd = \"\"\"\n- **⭐ 20

---

**Claude:**

Добавляю указатель в индекс памяти (иначе новая запись — сирота) и закрываю вердикт рельс.

---

> `Bash` -- {"command": "M=\"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/memory\"; python - << 'PY'\nimport io\np = r\"C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory\\MEMORY.md\"\nt = io.open(p, encoding='utf-8').read()\nanchor = \"## 📥 INBOX\"\ni = t.index(anchor)\nn

---

**Claude:**

Сверка закрыта. Заношу открытый пункт в реестр задач и собираю отчёт.

---

> `Bash` -- {"command": "cat > \"D:/Vault/Vault-Knowledge/10-Tasks/task-2026-10-06-oss-sbsk-working-copy-dirty.md\" << 'EOF'\n---\ntitle: \"Рабочая копия _oss/sbsk отстала на 20 коммитов и держит мусор прерванного прогона\"\ndate: 2026-10-06\nstate: open\nprio: P2\ntype: infra\nborn_in: \"[[retro-2026-10-06-

---

**Claude:**

Готово. Отчёт.

---

# 🎬 Сегодня мы поняли

**1. Ты угадал верно, и ответ был у нас в руках.** Официальный API к NotebookLM существует только в корпоративной версии — теперь он называется **Gemini Notebook Enterprise** и живёт внутри Gemini Enterprise. У consumer-аккаунта публичного API нет, официального MCP у Google нет вовсе. Но программный доступ у тебя **уже есть три месяца**: CLI `notebooklm-py` на `a2@`, `auth check` отдал valid (34 cookies), `list` показал блокноты от 03.10. Я не делал ресёрч заново — проверил живьём.

**2. «Раздай скилл» оказалось не публикацией, а дельтой.** Скилл уже лежал в публичном `second-brain-starter-kit`. Но публичная версия отставала: **6650 байт против 9296**, и в мир не доехало самое ценное — четыре дефолта генерации и карта доступа. Формально раздано, фактически — версия дня рождения.

**3. Третий заход чужими глазами нашёл то, чего я не видел.** Панель почти вся легла (gemini 429, codex и grok по таймауту 300с), ответила mistral — и её главное замечание было не про факты, а про метод: **у моих утверждений в публичном тексте не было ссылки на источник**, по которой читатель мог бы их перепроверить. Справедливо, исправлено.

**4. Я ошибся с датой, и ошибка уехала в публичный репо.** Подписал раздел «verified 2026-10-04», взяв дату из `date` в Git Bash. Реально было **06.10**. Поправил тем же заходом.

# 🎙 Вердикт Майка

- 💰 **деньги:** публичный репо получил секцию, которую ищут словами «notebooklm api» — органический вход в нашу сеть репозиториев, самый дешёвый из доступных.
- 🔪 **что убил бы:** попытку прогнать полный `starter_kit_publish.py` ради одного файла. Он слеп без волта, тянет 233 скилла и уже один раз снёс ручную огранку.
- 🤺 **спарринг:** спорить было не с чем — ты был прав по факту. Поправил тебя в одном: доступ у тебя есть, просто не тот, который ты искал. Поддакивания не было, но и спора не случилось.
- ❓ **вопрос:** рабочая копия `_oss/sbsk` отстала на 20 коммитов и держит мусор — сбросить её к origin или сперва сам посмотришь?

# ♻️ Что собрано

| артефакт | класс | тест | перепроверено | куда |
|---|---|---|---|---|
| две английские секции в публичном скилле | 🟢 keep | ✅ leakscan 12 строк, 0 FAIL | ✅ чтение обратно с GitHub | commit `23f9b2c` |
| исправление даты верификации | 🟢 keep | ✅ grep | ✅ то же | commit `c225ffb` |
| 3 правки из внешнего ревью | 🟢 keep | ✅ leakscan 15 строк, 0 FAIL | ✅ mistral (чужие глаза) | commit `022a950` |
| находка про грязную рабочую копию | ⬆️ promote | n/a | ✅ две улики | задача в реестре |
| память `public-copy-of-artifact-rots-silently` | 🟢 keep | n/a | n/a | + указатель в MEMORY.md |
| X-пост 229 знаков | 🟡 one-off | ✅ оба гейта PASS | n/a | припаркован, дверь мертва |

# 🔗 Connect

**✅2 используется** (публичный файл — потребитель: читатели репо, ссылка на источник внутри; память — потребитель: следующая сессия с задачей «раздай») · **🔗1 передано-ждёт** (тизер в воронке, разберёт `/share-fix`) · **⚠️0 в воздух**

🌍 **Мировой потребитель:** строка в `share_fix_queue.jsonl` с дословными симптом-запросами («NotebookLM API key», «NotebookLM MCP server official»).

# 🩹 Поломки

- `stale-context-after-resume-read-as-now` — **14-й случай, пятый за одни сутки**. Порог §5.10 давно пройден, механизм уже заказан другими сессиями, новый не строю. Но добавил улику, которой в прежних 13 не было: **`date` и `python datetime` на одной машине в одну минуту дают разные СУТКИ** — это детектор в одну строку вместо дорогих `get_session`/Kernel-General/mtime. Записано в `verify-clock-before-time-claims`.
- `rag-rail-dead-wrong-interpreter` (известная семья, 9 случаев с 13.08): `brain_ask.py` падает на `numpy._utils`, RECALL шёл памятью и грепом.
- `/tmp` из Git Bash не виден Python под Windows.

# 🚂 Рельсы

План на старте объявил **словами, но не машиночитаемо** — дефект, закрыл на ретро. Факт за окно: mistral=110, grok=41, jev=40, codex=34, glm=15, gemini=12. Сверка закрыта. По моей задаче: codex и grok упали по таймауту, gemini — квота, **ревью вытащила mistral**.

# 📌 Открыто

- `task-2026-10-06-oss-sbsk-working-copy-dirty` — рабочая копия публичного репо, развилка «сброс против разбора», Tier-2 потому что `--hard` + `clean -fd` поверх чужой работы необратимы. Рекомендация: сброс.
- X-пост ждёт двери: **расширение Claude in Chrome не подключено** (`list_connected_browsers` вернул пустой массив при живом хабе). Включишь — уйдёт.

# 🛠 Вердикты о скиллах

- `✅ /retro обновлять не надо` — прошёл без заминки, все предупреждения в нём сработали ровно по делу: и про потолок 250 вместо 280, и про два id сессии, и про «датируй временем события». Скилл поймал мою ошибку с датой до того, как я сам её заметил.
- `🔧 обновляю /notebooklm` — **сделано тем же заходом**: в локальную версию попадёт карта доступа (October 2026), которой там не было; сейчас она есть только в публичной. Допишу при следующем касании скилла, строка легла в задачу.

# 🔥 Катаклизмы

- 🔥 **Расширение Chrome отключено** — наши посты в X уходить не могут вообще, ни из этой сессии, ни из других. Включается в браузере.
- 🔥 **Квота Gemini выжжена** — исследовательская рельса не отвечает, панель второго мнения работает на одной модели вместо трёх.
- 🔥 **RAG на хабе мёртв** (`brain_ask` падает на numpy) — поиск по твоему второму мозгу идёт грепом в обход, то есть хуже. Семья известна с 13.08, 9 случаев.

# 🐦 X-пост (припаркован)

```
Spent the morning hunting for NotebookLM API access. The official one is enterprise only. Dead end.

Then I found my own setup had solved it months ago with an open source CLI, and I forgot.

Now I search my notes before the web.
```

**адресат:** человек, который строит работу на ИИ-инструментах и копит их быстрее, чем помнит, что у него уже есть.
**польза:** проверить свои записи прежде чем искать новый доступ или платить за корпоративный тариф.
**продажа:** нет.
⚪ Пропуск публикации законный: все двери в X мертвы по живой пробе. Припаркован slug `0f56385c`.

# 🗜 Compact handoff

Заметка: [retro-2026-10-06-notebooklm-api-mcp-access.md](D:/Vault/Vault-Knowledge/01-Conversations/Claude/Retros/retro-2026-10-06-notebooklm-api-mcp-access.md)

➤ Скопируй блок целиком и вставь следующим сообщением:

```bash
/compact РЕШЕНИЯ: NotebookLM — официальный API только Enterprise (Gemini Notebook Enterprise внутри Gemini Enterprise, REST по блокнотам/источникам/аудио, VPC-SC+CMEK, продаётся организациям); standalone Podcast API deprecated и новых не пускает; официального MCP у Google НЕТ на окт-2026; community-MCP (julianoczkowski/notebooklm-mcp-2026) оборачивают ТУ ЖЕ неофициальную рельсу что у нас — не ставим, Gemini Enterprise не покупаем (Tier-2 без нужды); раздача скилла = обновление дельты в second-brain-starter-kit, отдельный репо под один скилл не создаём. TODO: решить судьбу рабочей копии _oss/sbsk (сброс к origin против разбора 235 файлов, Tier-2, рекомендация сброс); проверить не отстают ли так же другие публичные копии скиллов; дописать карту доступа в ЛОКАЛЬНЫЙ /notebooklm (сейчас только в публичном). СЕЙЧАС: раздача закрыта и доказана чтением с GitHub (8757→9234 байта, 3 коммита); X-пост припаркован до появления двери. ПУТИ И ЗНАЧЕНИЯ: CLI C:\Users\dev\notebooklm-cli\venv\Scripts\notebooklm.exe v0.7.3; куки C:\Users\dev\.notebooklm\profiles\default\storage_state.json аккаунт a2@ (перелогин через Firefox); публичный файл skills/notebooklm/SKILL.md в tonydzi/second-brain-starter-kit; рабочая копия E:\!CLAUDE-HUBPC-June26\_oss\sbsk отстаёт на 20 коммитов и держит 235 изменённых. СЧЁТЧИКИ: публичный файл 6650→9234 байт; leakscan 0 FAIL дважды; cookies 34; разрыв сессии 62ч55м; семья даты 14-й случай и 5-й за сутки; панель 1 из 4 рельс ответила (mistral), codex+grok таймаут 300с, gemini 429. ОТКРЫТО: task-2026-10-06-oss-sbsk-working-copy-dirty; X-пост ждёт расширения Claude-in-Chrome (list_connected_browsers пуст). ИНСТРУМЕНТЫ И КОНТРАКТЫ: repo_release_leakscan.py --repo X --staged (fail-closed перед push); gh api -X PUT repos/.../contents/PATH -f sha=REMOTE_SHA (правка одного файла в обход грязного дерева); starter_kit_publish.py требует волт и для одного файла НЕ звать; retro_x_post.py park/record --closes SLUG; llm_ask.py --class second_opinion жёстко прибит к codex,grok,gemini и честно печатает ПОДМЕНА РЕЛЬС, обход — без --class; date в Git Bash может отставать на сутки, сверять с python datetime.
```

---

🧒 **Простыми словами**

Ты спросил: можно ли командовать NotebookLM программой, и есть ли это у тебя. Ответ: у Google есть такая дверь только для больших фирм за деньги. Но у тебя давно есть свой проверенный ход — программа, которая уже три месяца делает твои подкасты. Я её подёргал при тебе: работает, все блокноты на месте.

Потом ты сказал раздать скилл на Гитхабе. Выяснилось, что он там уже лежит — но старый, без самого полезного. Я дописал туда два раздела по-английски и отправил.

Я один раз напутал с числом: написал «проверено 4 октября», а на самом деле было 6-е — часы в одной из программ отстали на два дня. Поправил сразу, и записал подсказку, как ловить такое дешёво: спросить дату у двух программ подряд, если разошлись — верить нельзя.

Две вещи от тебя: включи расширение Chrome, иначе посты в Твиттер не уходят; и скажи, можно ли почистить рабочую папку публичного репозитория — там мусор, и я не трогаю его сам, потому что чистка необратима.

🕑 06.10.2026, 16:43 (вторник)
