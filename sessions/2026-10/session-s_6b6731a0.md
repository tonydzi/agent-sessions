---
session: s_6b6731a0
date: 2026-10-18
words: 1848
turns: 5
tools: "Agent, Bash, ToolSearch, WebFetch, Write, mcp__ccd_session_mgmt__set_session_title"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-18 · Есть места, где владельцы своих AI-проектов выкладывают файлы `CLAUDE.md`, `AGENTS.md` и п…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_6b6731a0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Есть места, где владельцы своих AI-проектов выкладывают файлы `CLAUDE.md`, `AGENTS.md` и похожие инструкции для AI-агентов.

Нужно:
- найти такие места, в первую очередь на GitHub;
- проверить, есть ли другие сайты/репозитории/подборки с такими файлами;
- посмотреть чужие `CLAUDE.md` / `AGENTS.md` и взять полезные идеи;
- подумать, что можно улучшить в нашем документе;
- подготовить исследование на эту тему;
- после исследования перейти к практическим действиям: опубликовать/обновить наш файл и внедрить полезные находки.
__Перевела: GPT-5.5 + whisper__

• • • • •

Нужно найти места, где владельцы ИИ-агентов выкладывают свои файлы `CLAUDE.md` и `AGENTS.md` — точно на GitHub, возможно есть и другие сайты/репозитории/каталоги.

Задачи:
1. Провести deep research на тему публичных `CLAUDE.md` и `AGENTS.md`.
2. Найти площадки, репозитории или подборки, где такие файлы публикуют.
3. Посмотреть чужие файлы и извлечь из них полезные идеи для наших документов.
4. Подготовить, куда можно выкладывать наши `CLAUDE.md` / `AGENTS.md`.
5. После исследования предложить следующие действия.
__Перевела: GPT-5.5 + 11labs__

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\"; timeout 60 python D:/Vault/_imports/brain_ask.py \"публикация CLAUDE.md AGENTS.md awesome каталог\" 2>&1 | head -40; echo ---; ls public-repos/; echo ---; grep -rli \"awesome-claude\\|agents.md\\b\\|claude-md\" D:/Vault/Vault-Knowledge/03-Insig

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos\"; for r in claude-bible tonydzi agent-sessions; do echo \"== $r\"; ls $r | head -30; (cd $r && git remote -v 2>/dev/null | head -1 && git log --oneline -3 2>/dev/null); done; echo; grep -o \"AGENTS.md\\` опубликовано[^.]*\" -r D:/Vault/

---

> `Bash` -- {"command": "set -o pipefail; cd \"E:/!CLAUDE-HUBPC-June26/public-repos\"; for r in claude-bible tonydzi agent-sessions; do echo \"== $r\"; ls $r | head -30; (cd $r; git remote -v 2>/dev/null | head -1; git log --oneline -3 2>/dev/null); done; grep -o \"AGENTS.md. опубликовано.\\{0,300\\}\" ~/.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; head -60 README.md; echo; find templates examples docs -maxdepth 2 | head -40; git status -s | head", "description": "Read claude-bible README and layout"}

---

> `Agent` -- {"description": "Map public CLAUDE.md/AGENTS.md venues", "model": "sonnet", "subagent_type": "general-purpose", "prompt": "Research task (read-only, web only, do not write files outside your reply). Today is 2026-10-18.\n\nGoal: build a verified map of WHERE people publicly share their AI-agent inst

---

> `Agent` -- {"description": "Mine exemplar CLAUDE.md files for ideas", "model": "sonnet", "subagent_type": "general-purpose", "prompt": "Research task (read-only, web only). Today is 2026-10-18.\n\nGoal: read 12-20 real, well-regarded public CLAUDE.md / AGENTS.md files and best-practice guides, and extract conc

---

> `Bash` -- {"command": "set -o pipefail; cd D:/Vault/Vault-Knowledge/03-Insights; sed -n 1,60p \"insight-DR-DR26-06-30-HUB-04-причины-разрастания-claude-md-контекстных-файлов-и.md\" | cut -c1-400; echo ====; cat \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible/ROADMAP.md\" | head -40; cat \"E:/!CLAU

---

> `Bash` -- {"command": "set -o pipefail; for r in Palo-Alto-AI-Research-Lab/claude-bible Palo-Alto-AI-Research-Lab/claude-consensus tonydzi/agent-sessions; do gh api repos/$r --jq '\"\\(.full_name) ★\\(.stargazers_count) forks \\(.forks_count) pushed \\(.pushed_at) topics \\(.topics)\"'; done; gh search issues

---

> `Bash` -- {"command": "gh pr view 135 -R GetBindu/awesome-claude-code-and-skills --json state,mergedAt,closedAt,comments --jq '{state,mergedAt,closedAt,c:[.comments[].body[0:300]]}'; gh search prs --author tonydzi \"awesome\" --limit 30 --json repository,title,state,url --jq '.[]|\"\\(.repository.nameWithOwne

---

> `Bash` -- {"command": "wc -lc ~/.claude/CLAUDE.md ~/.claude/AGENTS.md \"E:/!CLAUDE-HUBPC-June26/AGENTS.md\"; ls ~/.claude/scripts | grep -i -E \"leak|sanit|redact\" ", "description": "Measure canon size and find leak-scan tools"}

---

**Claude:**

Жду результаты исследователей.

---

> `Bash` -- {"command": "echo waiting", "description": "No-op while agents run"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; git remote set-url origin https://github.com/tonydzi/claude-bible.git; git fetch -q origin; git status -sb | head -3; git log --oneline origin/main -5; grep -rn -i \"founder\\|non-technical\\|5 machines\" --include=*.md . | 

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; git status -s | head; git pull -q --ff-only origin main; git log --oneline -1; ls; ls examples docs; grep -rn -i \"founder\\|non-technical\\|not a programmer\\|5 machines\" --include=*.md . | grep -v devlog | cut -c1-220", "

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; cat AGENTS.md | head -50; echo ===; sed -n 1,40p README.md; python -c \"import json,os;d=json.load(open(os.path.expanduser('~/.claude/fleet_nodes.json')));n=d.get('nodes',d);print(len(n))\"", "description": "Read current rep

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; sed -n 20,26p FOR-ROBOTS.md; sed -n 1,8p docs/the-day-my-ai-said-no.md; ls examples; head -30 examples/rule-no-blind-instruments.md", "description": "Read lines to fix and example format"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; python - <<'EOF'\nimport io,re\ndef sub(p,a,b):\n    s=io.open(p,encoding='utf-8').read(); assert a in s,(p,a); io.open(p,'w',encoding='utf-8',newline='\\n').write(s.replace(a,b)); print('ok',p)\nsub('FOR-ROBOTS.md','Built a

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; sed -i 's/A lone founder plus a religious metaphor/A lone operator plus a religious metaphor/' docs/why-a-bible.md; grep -c \"lone operator\" docs/why-a-bible.md; git diff --stat", "description": "Fix last founder mention an

---

> `Write` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\public-repos\\claude-bible\\examples\\global-claude-md-iron-rules.md", "content": "---\ntitle: \"A real global CLAUDE.md — the iron-rules layer, each rule paid for by a failure\"\ntype: example\ndate_established: 2026-10-18\nstatus: active\norigin: owner

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; grep -n \"examples/\" README.md; sed -n 1,30p CHANGELOG.md", "description": "Locate README table row and changelog head"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; sed -n 46,62p README.md", "description": "Read README example list section"}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; python - <<'EOF'\nimport io\np='README.md'; s=io.open(p,encoding='utf-8').read()\na=\"\"\"  pointed at the project's own documented procedure, which we had never read.\n\"\"\"\nb=a+\"\"\"- [**A real global CLAUDE.md, the iro

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; git add -A; python ~/.claude/scripts/repo_release_leakscan.py --repo . --staged; echo \"exit=$?\"; python ~/.claude/scripts/gh_pr_discipline.py --help 2>&1 | grep -i sign | head -3", "description": "Run fail-closed leak scan

---

**Claude:**

Leak-scan чистый (0 FAIL; 2 предупреждения про общий путь `~/.claude/CLAUDE.md`, личных данных там нет). Коммичу и пушу.

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; git -c core.autocrlf=false commit -q -F - <<'EOF'\ndocs: ship the real CLAUDE.md iron-rules layer, single-source CLAUDE.md -> AGENTS.md\n\n- examples/global-claude-md-iron-rules.md: the 20 rules at the top of our live\n  glo

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26/public-repos/claude-bible\"; gh release create v0.1.9 -R tonydzi/claude-bible --title \"v0.1.9: the real CLAUDE.md iron-rules layer\" --notes \"The repo now ships a real CLAUDE.md, not only the theory of one: the 20 iron rules from our live global CLAUD

---

> `Bash` -- {"command": "set -o pipefail; gh api repos/[СКРЫТО]/awesome-claude-md/contents/.github/ISSUE_TEMPLATE/new-example.md --jq .content | base64 -d; echo =====; gh api repos/[СКРЫТО]/awesome-claude-md/contents/CONTRIBUTING.md --jq .content | base64 -d | head -60; echo =====; gh api repos/[СКРЫТО]/awesome-agents-

---

> `Bash` -- {"command": "set -o pipefail; grep -n -i \"project_doc\" ~/.codex/config.toml; wc -c ~/.codex/AGENTS.md; gh api repos/[СКРЫТО]/awesome-agent-conventions/contents/.github/ISSUE_TEMPLATE/suggest-a-convention.yml --jq .content | base64 -d | head -60; gh api repos/[СКРЫТО]/awesome-agent-conventi

---

> `ToolSearch` -- {"query": "select:WebFetch", "max_results": 1}

---

> `WebFetch` -- {"url": "https://code.claude.com/docs/en/memory", "prompt": "Quote verbatim what the page says about (1) HTML comments in CLAUDE.md being stripped/not injected, (2) recommended size/line limit for CLAUDE.md, (3) AGENTS.md support, (4) @imports depth. Short quotes only."}

---

> `Bash` -- {"command": "grep -n -i \"html comment\\|200 lines\\|reduce adherence\\|four hops\\|4 hops\\|maximum depth\" \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/s_6b6731a0/tool-results/toolu_01ER9b32gZiXhjdSX8esCKEG.txt\" | cut -c1-300", "description": "Grep docs

---

> `Bash` -- {"command": "python - <<'EOF'\nimport io,re,os\ns=io.open(os.path.expanduser('~/.claude/CLAUDE.md'),encoding='utf-8').read()\nsecs=re.split(r'(?m)^(?=#{2,3} )',s)\nrows=sorted(((len(x.encode()),x.splitlines()[0][:70]) for x in secs),reverse=True)[:10]\nfor b,h in rows: print(b,h)\nprec=sum(len(l.enc

---

**Claude:**

Пишу итоговое исследование в волт.

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\03-Insights\\insight-2026-10-18-publichnye-claude-md-agents-md-gde-i-chto-vzyat.md", "content": "---\ntitle: \"Публичные CLAUDE.md и AGENTS.md: где их выкладывают и что взять себе\"\ntype: insight\nstage: distilled\ndate_established: 2026-10-18\nmachine:

---

> `Bash` -- {"command": "set -o pipefail; grep -l -i \"claude-md\\|CLAUDE.md\" D:/Vault/Vault-Knowledge/90_MOCs/*.md 2>/dev/null | head -5", "description": "Find MOC to link new note from"}

---

> `Bash` -- {"command": "f=D:/Vault/Vault-Knowledge/90_MOCs/_Claudedev-Alpha-MOC.md; cp \"$f\" \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_6b6731a0/scratchpad/MOC.bak\"; tail -5 \"$f\"; printf '\\n- [[insight-2026-10-18-publichnye-claude-md-agents-md-gd

---

> `ToolSearch` -- {"query": "select:mcp__ccd_session_mgmt__set_session_title", "max_results": 1}

---

> `mcp__ccd_session_mgmt__set_session_title` -- {"session_id": "self", "title": "🌍 · 📜🔎 Публичные CLAUDE.md и AGENTS.md · H61518"}

---

> `Bash` -- {"command": "set -o pipefail; gh api repos/tonydzi/claude-bible/contents/examples/global-claude-md-iron-rules.md --jq '.size'; gh api repos/tonydzi/claude-bible/contents/CLAUDE.md --jq '.content' | base64 -d; python ~/.claude/scripts/machine_stamp.py sig --model \"Opus 5.5\"", "description": "Verify

---

**Claude:**

Исследование готово, наш файл опубликован. Подать заявку в главный каталог должен ты сам: его правила требуют, чтобы заявку отправлял человек.

**Метод.** Это было собственное исследование, а не веер ДР по внешним LLM. Вопрос фактический, поэтому каждую площадку я проверил живьём через `gh api` и открытием страницы. Если нужен полный веер, запущу его отдельно.

## Где публикуют
| Площадка | Размер | Нам |
|---|---|---|
| **awesome-claude-code** | 56k★ | Главная цель. Заявка только через веб-форму, и подаёт человек. Мы проходим: 11★, репо старше 14 дней |
| awesome-claude-md ([СКРЫТО]) | 612★ | Пускают от 100★, нам пока рано |
| awesome-cursorrules, awesome-copilot | 40k★ | Только Cursor или Copilot, не наш формат |
| agents.md (Linux Foundation) | 25k★ | Это стандарт, а не каталог |
| aitmpl.com (claude-code-templates) | 1.3M загрузок | Туда подходят наши хуки, оформленные как компонент |

Спрос на такие файлы есть. Репозиторий, где лежит один CLAUDE.md, набрал 220k★. В поиске GitHub примерно 1.1 млн файлов AGENTS.md и 0.8 млн CLAUDE.md.

Прошлый урок: в августе каталог закрыл наш PR со словами «это документация и шаблоны, мало содержания».

## Что сделано
- **Опубликовал наш настоящий файл**, а не только описание подхода. В `tonydzi/claude-bible` вышел релиз v0.1.9, в нём наши 20 железных правил. Они обезличены, у каждого остался провал, из-за которого правило появилось. Ссылка: https://github.com/tonydzi/claude-bible/releases/tag/v0.1.9. Проверка утечек: 0 ошибок. Файл на GitHub на месте (9829 байт).
- Добавил `CLAUDE.md`, который просто подключает `AGENTS.md`. Так один файл читают и Claude, и Codex, Cursor и остальные агенты, как в репозиториях ruff и sentry.
- **Нашёл и исправил нарушение в публичном репо.** Там было написано «founder, non-technical» и «I'm not a programmer». Теперь стоит «engineering executive, Python/C++». Число машин исправил с 5 на 8.
- Исследование лежит в волте: `03-Insights/insight-2026-10-18-publichnye-claude-md-agents-md-gde-i-chto-vzyat.md`, ссылка на него добавлена в MOC.

## Что взять в наш CLAUDE.md (решаешь ты, это правка канона)
1. **Историю прятать в HTML-комментарии.** В документации Anthropic прямо сказано, что `<!-- -->` убирается до загрузки в контекст. Прецеденты и замеры остаются для людей, а токены на них не тратятся. Только разделы §9.2-бис и §7.13 занимают 6.5 KB, общая экономия примерно 6–10 KB из 90.
2. **Лестница приоритетов** из 5 строк, как у Harper Reed: безопасность, потом правда, потом твоя цель, потом правила репо, потом всё остальное.
3. **Если правило уже держит хук, в тексте оставить одну строку.** Например, правила про архивацию сессий и MCP сейчас пересказывают то, что делают хуки.
4. **Убрать из текста цифры, которые устаревают** («8 узлов», «36 проверок»). Вместо них ставить ссылку на реестр.
5. **Ошибка в структуре файла.** Раздел §9.2-бис стоит внутри §7.
6. **Codex по умолчанию молча обрезает AGENTS.md на 32 KiB.** На хабе лимит поднят до 256 KiB, наше зеркало в 98 KB помещается. Остальные узлы не проверены.

Для сравнения: файлы в изученных репозиториях занимают около 80 строк, личные файлы опытных людей 120–200 строк. Наш файл в 5–10 раз больше.

## Текст для формы awesome-claude-code
https://github.com/hesreallyhim/awesome-claude-code, кнопка «New issue», форма ресурса:
> **claude-bible** · https://github.com/tonydzi/claude-bible · Category: Memory & Context · A governance framework for CLAUDE.md and AGENTS.md: one rule per file with typed frontmatter, precedence, a routing tree (rulebook / agent config / memory / hook), and a real sanitized global CLAUDE.md whose 20 rules each cite the failure that produced them. MIT.

Если скажешь «+», следующим шагом проверю лимит Codex на остальных узлах флота и подготовлю компонент для aitmpl.

🧒 **Простыми словами:** люди выкладывают свои «инструкции для ИИ» на нескольких больших досках на GitHub. Самая большая на 56 тысяч звёзд. В прошлый раз нас туда не взяли: показали только рецепт, без самого блюда. Теперь блюдо выложено: наши 20 главных правил с историей, откуда взялось каждое. Осталось, чтобы ты сам нажал «отправить» на главной доске. А наш собственный файл правил примерно в 7 раз толще, чем у других. Его можно заметно похудеть, ничего не потеряв: историю спрятать в комментарии, которые ИИ не читает.

🏛H · Opus 5.5 · 61518
