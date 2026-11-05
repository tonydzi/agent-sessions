---
session: s_0369fc74
date: 2026-10-11
words: 1557
turns: 2
tools: "Bash, ToolSearch, WebFetch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-11 · Use live web search. Today is 2026-10-11. For each product below, find the CANONICAL offic…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0369fc74` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Use live web search. Today is 2026-10-11. For each product below, find the CANONICAL official GitHub repository URL and official website, then answer the specific checks. Every answer must carry a direct URL you actually opened and the retrieval date. If you cannot verify, write NOT VERIFIED. Do not guess. Do not substitute similarly named projects.

Products:
1. Orca, described as "AI Orchestrator / Agent Development Environment" running Claude Code, Codex, Grok Build, DeepSeek Harness, ZCode side by side in git worktrees, allegedly ~88k GitHub stars, MIT. Candidate repos seen: stablyai/orca, orca-cli/orca. Which one, if any, is the real product? Does it ship a native Windows build? Does it start agents with permissions bypassed by default (e.g. --dangerously-skip-permissions or equivalent)? Any open issues about Windows crashes in the last 60 days?
2. Superset (superset.sh, "agentic IDE", Elastic License 2.0). Is Windows supported in the current official release matrix? Cite the README or docs line.
3. Emdash (emdash.sh, "Agent Development Environment", Apache-2.0). Windows installer available? Local-first / telemetry policy line? Star count?
4. Desktop CC GUI / ccgui (zhukunpenglinyutong/desktop-cc-gui?). License? Is the Baidu Tongji analytics still present in the current source? Cite file path if you can.
5. CC Switch (~142k stars claimed). Canonical repo? What does it actually do (router/config manager vs workspace)?
6. bb (get-bb/bb, getbb.app). Latest release version and date; native Windows status (WSL2 only or native alpha?).
7. OpenChamber. Does it run only OpenCode as the harness, or multiple native harnesses?
8. First-party harnesses: do these exist as official products, by whom, and in what form factor (CLI/TUI/desktop): Grok Build (xAI), DeepSeek Harness, ZCode (Z.ai/Zhipu), Google Antigravity.

Output: a table with columns product | canonical repo URL | website | license (from LICENSE file) | stars (date) | native Windows (yes/no/WSL/unknown) | key finding | source URLs. Then a short list of claims you could NOT verify.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebFetch` -- {"url": "https://github.com/stablyai/orca", "prompt": "Repo description, stars, license, README lines on Windows support, supported agents (Claude Code, Codex, Grok Build, DeepSeek, ZCode), worktrees, and any mention of dangerously-skip-permissions / permission bypass. Website link."}

---

> `WebFetch` -- {"url": "https://github.com/orca-cli/orca", "prompt": "Repo description, stars, license, what it is, Windows support."}

---

> `WebFetch` -- {"url": "https://github.com/superset-sh/superset", "prompt": "Stars, license, README lines on Windows/macOS/Linux platform support, website link."}

---

> `WebFetch` -- {"url": "https://github.com/generalaction/emdash", "prompt": "Stars, license, Windows installer availability, telemetry / local-first policy lines, website link."}

---

> `WebFetch` -- {"url": "https://github.com/zhukunpenglinyutong/desktop-cc-gui", "prompt": "Stars, license, what it is, Windows support, any analytics mention (Baidu Tongji / hm.baidu.com)."}

---

> `WebFetch` -- {"url": "https://github.com/farion1231/cc-switch", "prompt": "Stars, license, what it does (config manager / proxy / router), platforms incl. Windows."}

---

> `WebFetch` -- {"url": "https://github.com/get-bb/bb", "prompt": "Stars, license, latest release version and date, Windows support (WSL2 or native), website link."}

---

> `WebFetch` -- {"url": "https://github.com/btriapitsyn/openchamber", "prompt": "Stars, license, which harnesses supported (OpenCode only or multiple), Windows support."}

---

> `WebFetch` -- {"url": "https://api.github.com/repos/stablyai/orca/issues?state=open&per_page=60&labels=&sort=created&direction=desc", "prompt": "List issues created since 2026-08-12 whose title/body mention Windows crash, crash, or won't start. Give number, title, created_at, url. Also note any issue about danger

---

> `WebFetch` -- {"url": "https://api.github.com/search/issues?q=repo:stablyai/orca+dangerously-skip-permissions", "prompt": "List total_count and each item's title, number, html_url, created_at, state."}

---

> `WebFetch` -- {"url": "https://api.github.com/repos/get-bb/bb/releases?per_page=3", "prompt": "For each release: tag_name, name, published_at, html_url, prerelease, and any Windows asset names."}

---

> `WebFetch` -- {"url": "https://api.github.com/search/code?q=hm.baidu.com+repo:zhukunpenglinyutong/desktop-cc-gui", "prompt": "Report total_count and file paths of matches, or error message."}

---

> `Bash` -- {"command": "cd /tmp 2>/dev/null; gh api -X GET search/code -f q='hm.baidu.com repo:zhukunpenglinyutong/desktop-cc-gui' --jq '.total_count, (.items[]?.path)' 2>&1 | head; echo ---; gh api -X GET search/code -f q='baidu repo:zhukunpenglinyutong/desktop-cc-gui' --jq '.total_count, (.items[]?.path)' 2>

---

> `Bash` -- {"command": "cd \"$TEMP\"; D=$(date -u +%F); echo $D\nfor r in stablyai/orca orca-cli/orca superset-sh/superset generalaction/emdash zhukunpenglinyutong/desktop-cc-gui farion1231/cc-switch get-bb/bb btriapitsyn/openchamber; do echo \"$r: $(gh api repos/$r --jq '[.full_name,.stargazers_count,(.licens

---

> `Bash` -- {"command": "cd \"$TEMP\"\necho ---orca docs; gh api repos/stablyai/orca/contents/docs/site/content/docs/agents/supported.mdx --jq .content | base64 -d | grep -n -i -E 'skip-permissions|bypass|yolo|default|permission' | head -15\necho ---orca README win/agents; gh api repos/stablyai/orca/readme --jq

---

> `WebSearch` -- {"query": "Grok Build CLI xAI official coding agent", "mode": "standard"}

---

> `WebSearch` -- {"query": "DeepSeek Harness official coding agent CLI", "mode": "standard"}

---

> `WebSearch` -- {"query": "ZCode Z.ai Zhipu coding agent desktop official", "mode": "standard"}

---

> `WebSearch` -- {"query": "Google Antigravity agent-first IDE official", "mode": "standard"}

---

> `WebFetch` -- {"url": "https://x.ai/cli", "prompt": "What is Grok Build; form factor; platforms incl. Windows; who makes it."}

---

> `WebFetch` -- {"url": "https://deepseek-harness.github.io/deepseek-harness/", "prompt": "What is DeepSeek Harness; who publishes it; form factor (CLI/TUI/web); license; Windows."}

---

> `WebFetch` -- {"url": "https://zcode.z.ai/en/docs", "prompt": "What is ZCode; publisher; form factor; platforms incl. Windows."}

---

> `WebFetch` -- {"url": "https://antigravity.google/", "prompt": "What is Antigravity; publisher; form factors (IDE, CLI, desktop); platforms incl. Windows."}

---

**Claude:**

Все данные получены 2026-10-11. «Стороны» репозитория и звёзды взяты из GitHub API (`gh api repos/...`), остальное из README и открытых страниц.

| product | canonical repo | website | license | stars (2026-10-11) | native Windows | key finding | sources |
|---|---|---|---|---|---|---|---|
| 1. Orca | **stablyai/orca** (настоящий). `orca-cli/orca` — другой проект: Go-оркестратор, 4 звезды, последний push 2026-05-08 | onOrca.dev | MIT (GitHub API) | 89 277 | **yes**: `orca-windows-setup.exe`, подпись SignPath | Звёзды ~88k подтверждаются. Агенты Grok, DeepSeek Harness и ZCode есть в README. **Обход разрешений включён по умолчанию**: docs пишут, что для новых запусков подставляется флаг обхода (`--dangerously-skip-permissions` у Claude, `--dangerously-bypass-approvals-and-sandbox` у Codex, `--mode yolo` у ZCode). Отключается в Settings → Agents → Agent Permissions → Manual. | [repo](https://github.com/stablyai/orca), [supported.mdx](https://github.com/stablyai/orca/blob/main/docs/site/content/docs/agents/supported.mdx), [defaults](https://github.com/stablyai/orca/blob/main/src/shared/tui-agent-permissions.ts) |
| 2. Superset | superset-sh/superset | superset.sh | Elastic License 2.0 (`LICENSE.md`; API показывает NOASSERTION) | 15 059 | **no** | README, строка 27: «**Windows**: not yet available». Linux экспериментальный, macOS основной. | [repo](https://github.com/superset-sh/superset) |
| 3. Emdash | generalaction/emdash | emdash.com (docs на emdash.sh) | Apache-2.0 | 5 949 | **yes**: `.msi` и portable `.exe` | README: «local-first», состояние в локальной SQLite. Телеметрия опциональна, отключается в Settings или `TELEMETRY_ENABLED=false`. | [repo](https://github.com/generalaction/emdash) |
| 4. ccgui | zhukunpenglinyutong/desktop-cc-gui | mossx.ai/download | **MIT по README и текстовой выдаче, но файла LICENSE в корне репо нет** (API: none) | 4 459 | yes (NSIS `.exe`) | Baidu Tongji **присутствует** в текущем коде: `src/lib/analytics.ts` (на Windows/macOS грузится внешний `hm.js`), `src-tauri/src/baidu_tongji.rs` (транспорт для Linux), `src-tauri/tauri.conf.json`. Site ID зашит в коде. | [repo](https://github.com/zhukunpenglinyutong/desktop-cc-gui), [analytics.ts](https://github.com/zhukunpenglinyutong/desktop-cc-gui/blob/main/src/lib/analytics.ts) |
| 5. CC Switch | farion1231/cc-switch | ccswitch.io | MIT | 142 533 | yes (MSI, portable ZIP, ARM64) | Это не воркспейс. Это менеджер конфигов и провайдеров для Claude Code, Codex и Gemini CLI, плюс локальный прокси: конвертация форматов API и failover. | [repo](https://github.com/farion1231/cc-switch) |
| 6. bb | get-bb/bb | getbb.app | MIT | 4 232 | **native alpha + WSL2**. README: «expect problems», нужен Git for Windows | Последний стабильный релиз `desktop-v0.46.0`, опубликован 2026-10-09T22:43:44Z, есть Windows-ассет `bb-0.46.0-x64.exe`. Тег `desktop-nightly` — prerelease. | [releases](https://github.com/get-bb/bb/releases/tag/desktop-v0.46.0) |
| 7. OpenChamber | **openchamber/openchamber** (репо переехал, `btriapitsyn/openchamber` перенаправляется) | openchamber.dev | MIT | 11 416 | yes для Desktop. Для CLI/Web не проверено. | **Только OpenCode.** README: «uses OpenCode to run coding agents», другие харнессы не упомянуты. | [repo](https://github.com/openchamber/openchamber) |

**Orca и окно 60 дней (с 2026-08-12).** Открытых Windows-багов много. Поиск `windows crash` дал 96 открытых результатов, вот самые прямые:
- [#16759](https://github.com/stablyai/orca/issues/16759): ACCESS_VIOLATION в рендерере, 4 краха.
- [#19891](https://github.com/stablyai/orca/issues/19891): краш `conpty.node`.
- [#16797](https://github.com/stablyai/orca/issues/16797): демон терминала тихо падает и убивает PTY-сессии.
- [#23415](https://github.com/stablyai/orca/issues/23415): чужой `taskkill /T` убивает Orca.
- [#25270](https://github.com/stablyai/orca/issues/25270): `git worktree add/remove` убивает терминальные панели.
- [#14502](https://github.com/stablyai/orca/issues/14502): в Windows-сборке битый `zod`.

**Харнессы первой стороны (п. 8):**

| harness | вендор | форма | источник |
|---|---|---|---|
| Grok Build | xAI | CLI (`curl … x.ai/cli/install.sh`). Релиз по вторичным источникам ~май 2026, доступ по платным тарифам. | [mer.vin](https://mer.vin/2026/05/grok-build-cli-xai-terminal-coding-agent-with-plan-mode-subagents-and-headless-ci/), страница x.ai/cli отдала 403 |
| DeepSeek Harness (`dsh`) | DeepSeek, MIT, developer preview, август 2026 | основной вход — локальный веб-UI (`npx @deepseek-ai/dsh web`), плюс headless из терминала | [apidog](https://apidog.com/blog/what-is-deepseek-harness/) |
| ZCode | Z.ai, запуск 2026-07-01 | десктоп-приложение («ADE») | [zcode.z.ai/en/docs](https://zcode.z.ai/en/docs), [letsdatascience](https://letsdatascience.com/news/zai-launches-zcode-ai-coding-environment-c8a68202) |
| Google Antigravity | Google | IDE, CLI, десктоп «2.0», Python SDK; macOS, Windows, Linux | [antigravity.google](https://antigravity.google/) |

**NOT VERIFIED:**
- Grok Build: страница x.ai/cli вернула 403, дату запуска, тарифы и модель знаю только из блогов, источники расходятся.
- DeepSeek Harness: страница `deepseek-harness.github.io` открылась пустой, вендор, лицензия и форма взяты из вторичных статей. Репозиторий и звёзды не открывал, цифры из статей (36k–169k) противоречат друг другу.
- ZCode: на открытой странице нет названия издателя и нет Windows. Windows-поддержка взята из вторичных статей.
- ccgui: лицензия MIT заявлена в README, но файла LICENSE в корне нет. Остальную часть дерева репо не смотрел.
- OpenChamber: работает ли CLI/Web-вариант на Windows, не проверено.
- bb: страница README не называет версию, версия взята из API релизов.
- Orca: отдельно не проверял, влияет ли какой-то из Windows-багов на запуск агентов с обходом. Просмотрел только первую часть выдачи issues, остальное (~310 тыс. символов) не читал.

🧒 **Простыми словами:** Настоящий Orca — это `stablyai/orca`, у него ~89 тысяч звёзд и он работает на Windows. По умолчанию он запускает агентов без вопросов «можно ли?», это отключается одной настройкой. Superset пока без Windows. У ccgui в коде до сих пор стоит счётчик Baidu. CC Switch — переключатель настроек, а не рабочая среда. OpenChamber умеет только OpenCode. Про Grok Build, DeepSeek Harness и ZCode я знаю в основном из статей, официальные страницы либо закрыты, либо пустые, поэтому там стоит «не проверено».
