---
session: s_c547efdb
date: 2026-09-22
words: 1499
turns: 4
tools: "Bash, Grep, ToolSearch, WebSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · List real, currently-maintained open-source projects (2025-2026) that auto-fill job applic…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c547efdb` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

List real, currently-maintained open-source projects (2025-2026) that auto-fill job application forms on Greenhouse, Lever, Ashby or Workday. For each: repo name, GitHub URL, last commit recency, license, what it actually automates (field mapping? resume parsing? submission?), and whether it does anything that risks an account ban (captcha solving, fingerprint spoofing, mass submission). Exclude paid SaaS and anything whose main feature is CAPTCHA bypass. Be concrete and skeptical: if a project is abandoned or vaporware, say so.

---

> `Bash` -- {"command": "grep -l \"burned-rail-gets-a-probe-quota-not-a-ban\\|greenhouse-one-live-code-per-mailbox\" \"C:\\Users\\dev\\.claude\\projects\\C--Users-dev--claude-scripts\\memory\\\"*.md 2>/dev/null", "description": "Find matched memory files"}

---

> `ToolSearch` -- {"query": "WebSearch", "max_results": 3}

---

> `Grep` -- {"pattern": "burned-rail-gets-a-probe-quota-not-a-ban|greenhouse-one-live-code-per-mailbox", "path": "C:\\Users\\dev\\.claude\\projects\\C--Users-dev--claude-scripts\\memory", "output_mode": "files_with_matches"}

---

> `WebSearch` -- {"query": "open source GitHub 2026 auto-apply job application Greenhouse Lever Ashby Workday form filler"}

---

> `ToolSearch` -- {"query": "WebFetch", "max_results": 2}

---

> `Bash` -- {"command": "gh --version 2>&1 | head -3", "description": "Check gh CLI availability"}

---

> `Bash` -- {"command": "for repo in jdw004/internship_newsletter jdw004/fulltime_newsletter simonfong6/auto-apply neonwatty/job-apply-plugin vincent1313-oss/auto-apply utably/utably-browser-plugin; do\necho \"=== $repo ===\"\ngh api repos/$repo --jq '{full_name, description, pushed_at, updated_at, license: .li

---

> `WebSearch` -- {"query": "AIHawk Jobs_Applier_AI_Agent GitHub 2026 renamed LinkedIn cease and desist Greenhouse support"}

---

> `Bash` -- {"command": "for repo in feder-cr/Jobs_Applier_AI_Agent_AIHawk jdw004/internship_newsletter vincent1313-oss/auto-apply neonwatty/job-apply-plugin utably/utably-browser-plugin simonfong6/auto-apply; do\necho \"=== $repo ===\"\ngh api repos/$repo --jq '{full_name, description, created_at, pushed_at, l

---

> `WebSearch` -- {"query": "\"greenhouse\" OR \"lever\" OR \"ashby\" job application autofill browser extension github open source 2025 2026 resume parser"}

---

> `Bash` -- {"command": "for repo in Shivamshuroy448/jobfill-extension ritsth/job-autofill-extension argabizaky/job-autofill-extension Adarsh350/Jobfill-Extension boymeetsblockchain/autofill-extension jeffistyping/workpls subramanya1997/Autofill; do\necho \"=== $repo ===\"\ngh api repos/$repo --jq '{full_name, 

---

> `Bash` -- {"command": "for repo in neonwatty/job-apply-plugin ritsth/job-autofill-extension utably/utably-browser-plugin; do\necho \"############ $repo ############\"\ngh api repos/$repo/readme --jq '.content' 2>&1 | base64 -d 2>/dev/null | head -c 3000\necho\necho \"---END---\"\ndone", "description": "Fetch 

---

> `Bash` -- {"command": "for repo in jdw004/internship_newsletter vincent1313-oss/auto-apply Adarsh350/Jobfill-Extension; do\necho \"############ $repo ############\"\ngh api repos/$repo/readme --jq '.content' 2>&1 | base64 -d 2>/dev/null | head -c 2000\necho\necho \"---END---\"\ndone", "description": "Fetch RE

---

> `Bash` -- {"command": "for repo in vincent1313-oss/auto-apply Adarsh350/Jobfill-Extension ritsth/job-autofill-extension neonwatty/job-apply-plugin jdw004/internship_newsletter; do\necho \"=== $repo commits ===\"\ngh api \"repos/$repo/commits?per_page=1\" -i 2>&1 | grep -i \"^link:\" \ngh api \"repos/$repo/con

---

> `Bash` -- {"command": "gh api repos/vincent1313-oss/auto-apply/readme --jq '.content' | base64 -d | sed -n '30,90p'", "description": "Read more of vincent1313 auto-apply README for risk details"}

---

> `Bash` -- {"command": "echo \"=== devdattatalele/auto-apply repo ===\"\ngh api repos/devdattatalele/auto-apply --jq '{full_name, description, created_at, pushed_at, license: .license.spdx_id, stars: .stargazers_count, forks: .forks_count, open_issues: .open_issues_count}' 2>&1\necho\necho \"=== npm job-auto-a

---

> `Bash` -- {"command": "echo \"=== Shivamshuroy448/jobfill-extension ===\"\ngh api repos/Shivamshuroy448/jobfill-extension/readme --jq '.content' 2>&1 | base64 -d 2>/dev/null | head -c 800\necho\necho \"---\"\necho \"=== boymeetsblockchain/autofill-extension file tree ===\"\ngh api repos/boymeetsblockchain/aut

---

**Claude:**

[⏰ 23.09.2026, 00:46, среда]

🎙 Майк: рельсы — это была моя работа целиком: живой GitHub API (`gh api`) + WebSearch, без чужих LLM (задача разовая, не архитектурная, панель не звал).

Собрал и проверил живыми данными (звёзды, дата последнего коммита, лицензия, README) — не по памяти. Порядок: от наиболее живых к мёртвым/подозрительным.

## Живые и реально что-то делающие

| Репо | Последний коммит | Лицензия | Что реально автоматизирует | Риск бана |
|---|---|---|---|---|
| **[neonwatty/job-apply-plugin](https://github.com/neonwatty/job-apply-plugin)** — 111★, MIT | сегодня (22.09.26) | MIT | Плагин-скилл для Claude Code/Codex. Парсит резюме → маппит поля на Greenhouse/Ashby/Lever/Rippling/Workday → видимый браузер (Chrome/Codex Browser) заполняет форму → **останавливается перед Submit, жмёшь сам**. | Низкий — намеренно не сабмитит сам, "current forms unverified" честно написано в README |
| **[ritsth/job-autofill-extension](https://github.com/ritsth/job-autofill-extension)** («Little AI Helper») — 13★, MIT, есть CI+CodeQL | сегодня | MIT | Chrome-расширение, опубликовано в Chrome Web Store. Заполняет поля на Greenhouse/Lever/Workday/Ashby + AI-черновики ответов на открытые вопросы + бейдж visa-sponsorship. Только fill, **не сабмитит**. | Низкий — тот же паттерн: заполнил и остановился |
| **[devdattatalele/auto-apply](https://github.com/devdattatalele/auto-apply)** (апстрим, 1★, стух с апреля) + живой форк **[vincent1313-oss/auto-apply](https://github.com/vincent1313-oss/auto-apply)** (создан ВЧЕРА, 7 коммитов, 0★) | форк: сегодня; апстрим: 15.04.26 (**5+ мес тишины**) | MIT, npm-пакет `job-auto-apply` (v1.2.0, тоже с апреля) | Playwright-движок: scan→plan→fill→**submit**→OTP через Gmail IMAP→скриншот-лог. Заявлен full submit на Greenhouse/Ashby/Lever/Workday (вкл. создание аккаунта), Gem — тоже full, iCIMS/SmartRecruiters — только detection. Есть `batch` команда — **массовый апплай**. | **Средний** — сам сабмитит + явный bulk-режим = риск триггернуть анти-бот на объёме. Капчу не решает, фингерпринт не спуфит — но апстрим мёртв 5 месяцев, живёт только вчерашний форк одного человека с 0 звёзд. Доверия к "оно правда работает на всех этих ATS" — ноль, никто не проверил |
| **[utably/utably-browser-plugin](https://github.com/utably/utably-browser-plugin)** — 1★, Apache-2.0 | сегодня | Apache-2.0 | Расширение-клиент к SaaS-трекеру Utably (компания). Основная фича — импорт вакансий в трекер; автозаполнение Greenhouse/Lever/Ashby — **вторичная** фича, только контактные/анкетные поля. | Низкий, но это фронтенд платного продукта, не самостоятельный автозаполнитель |
| **[Adarsh350/Jobfill-Extension](https://github.com/Adarsh350/Jobfill-Extension)** — 1★, MIT | сегодня | MIT | Заявляет offline Chrome-расширение без зависимостей на Greenhouse/Lever/Workday/Ashby/iCIMS/Bayt. ⚠️ Скептически: репо весит **27 МБ** при заявленном "zero dependencies" — это ненормально для vanilla-JS расширения, похоже на закоммиченные бинарники/ассеты; все статусы "✅" в таблице — маркетинг, не факт (1 звезда, один автор). | Низкий по дизайну (offline), но верить README на слово не стоит |

## Заявлено, но НЕ то, чем кажется

- **[jdw004/internship_newsletter](https://github.com/jdw004/internship_newsletter)** и **fulltime_newsletter** — в поиске всплывают как "scrape/apply", но собственный README прямо пишет: `src/apply/ # FUTURE auto-apply scaffold (not yet implemented)`. Это **дайджест-бот** (тянет вакансии через API Greenhouse/Lever/Ashby/Workday и шлёт email/Discord), автозаполнения форм там **нет вообще**. Не включаю в рабочий список — описание вводит в заблуждение.

## Мёртвые (всплывают в поиске, но заброшены)

- **[simonfong6/auto-apply](https://github.com/simonfong6/auto-apply)** — последний коммит 28.08.2019, репо 5 КБ. Мёртв 7 лет.
- **[jeffistyping/workpls](https://github.com/jeffistyping/workpls)** — последний коммит 26.09.2022. Мёртв 4 года.
- **[subramanya1997/Autofill](https://github.com/subramanya1997/Autofill)** — последний коммит 27.12.2022. Мёртв ~4 года.

## Слишком свежие, чтобы оценивать (созданы 1–8 дней назад, 0★)

- **[Shivamshuroy448/jobfill-extension](https://github.com/Shivamshuroy448/jobfill-extension)** — броский маркетинговый README ("AI Question Copilot", "ResumeSync Engine"), но ссылка на Chrome Web Store ведёт на общую страницу магазина, а не на конкретное расширение — похоже, ещё не опубликовано. Лицензии нет. Запах vaporware.
- **[boymeetsblockchain/autofill-extension](https://github.com/boymeetsblockchain/autofill-extension)** — вообще без описания, голый скелет расширения (8 файлов), непонятно что делает.

## ⛔ Специально не включаю в список, но стоит знать

**feder-cr/Jobs_Applier_AI_Agent_AIHawk** (бывший «AIHawk», 31 626★, некогда самый известный auto-apply бот) — **репозиторий переименован в `invisible_playwright_mcp`**, описание теперь: *«Anti-detect agentic stealth browser: undetected browsing... No captchas»*. Проект полностью сменил профиль с «заполни мне заявку» на генерик anti-detect/stealth-browsing MCP-сервер — ровно та категория (обход детекта, "no captchas" как фича), которую ты просил исключить. Это живой кейс: самый популярный OSS-автозаполнитель job-форм в итоге стал инструментом обхода бана, а не наоборот — потому что LinkedIn выкатил ему cease-and-desist в 2025.

---

**Вывод, если коротко и цинично:** реально рабочих и живых — три: `neonwatty/job-apply-plugin` (безопаснее всего — не сабмитит сам), `ritsth/job-autofill-extension` (опубликован в сторе, только fill), и `devdattatalele/auto-apply`/форк `vincent1313-oss` (единственный, кто реально сабмитит + держит OTP + bulk-режим, но апстрим мёртв 5 месяцев, а форк — вчерашний, 0 звёзд, никем не проверен). Всё остальное — либо заброшено, либо младше недели и непроверяемо, либо вообще не делает то, что написано в описании.

🧒 Простыми словами: я не гадал, а зашёл на GitHub через специальную дверь (`gh api`) и посмотрел дату последнего коммита, лицензию и настоящий текст инструкции у каждого проекта — как проверить, свежий хлеб в магазине или просрочен, посмотрев на этикетку, а не на рекламную вывеску. Из десятка найденных реально рабочих и живых — три штуки, остальное либо умерло, либо родилось вчера и ещё не факт что работает, либо (как AIHawk) перестало быть тем, чем называется.

Sources:
- [neonwatty/job-apply-plugin](https://github.com/neonwatty/job-apply-plugin)
- [ritsth/job-autofill-extension](https://github.com/ritsth/job-autofill-extension)
- [utably/utably-browser-plugin](https://github.com/utably/utably-browser-plugin)
- [Adarsh350/Jobfill-Extension](https://github.com/Adarsh350/Jobfill-Extension)
- [jdw004/internship_newsletter](https://github.com/jdw004/internship_newsletter)
- [vincent1313-oss/auto-apply](https://github.com/vincent1313-oss/auto-apply)
- [devdattatalele/auto-apply](https://github.com/devdattatalele/auto-apply)
- [simonfong6/auto-apply](https://github.com/simonfong6/auto-apply)
- [jeffistyping/workpls](https://github.com/jeffistyping/workpls)
- [subramanya1997/Autofill](https://github.com/subramanya1997/Autofill)
- [feder-cr/Jobs_Applier_AI_Agent_AIHawk (now invisible_playwright_mcp)](https://github.com/feder-cr/Jobs_Applier_AI_Agent_AIHawk)
- [Shivamshuroy448/jobfill-extension](https://github.com/Shivamshuroy448/jobfill-extension)
- [boymeetsblockchain/autofill-extension](https://github.com/boymeetsblockchain/autofill-extension)

---

**User:**

Stop hook feedback:
СТОП: ты заявил, что пароля/доступа НЕТ, но обход поверхностей не прогонялся.
Замер 10.09.2026: пароль codeindexer.dev месяц лежал в чате паролей SSS, пока три сессии объявляли «пароля нет», проверив store и Chrome. Сутки работы.

Прогони дверь и повтори вывод по её результату:
  python ~/.claude/scripts/cred_hunt.py <сервис|домен|почта>
Она обходит store, chrome-passwords.csv, чат паролей SSS и ВСЕ личные диалоги. exit 1 = пусто везде (тогда «нет» законно, дальше /gmail и спросить оператора), exit 2 = поверхность недоступна, «нет» утверждать НЕЛЬЗЯ.
Класс: CLAUDE.md §5.4 check-all-places-not-one, семья vyvod-po-odnoy-poverhnosti (110 случаев с 27.07, порог §5.10 давно пройден).

---

**Claude:**

Это, похоже, ложное срабатывание — в моём ответе про auto-apply репозитории нет ни одного заявления «пароля/доступа нет» ни к какому сервису. Я проверял публичные GitHub-репозитории через `gh api` (не требует логина) и WebSearch — credential-claims там просто неоткуда взяться.

Возможные кандидаты, за что мог зацепиться детектор — но ни один не про пароль/доступ:
- «Лицензии нет» (Shivamshuroy448) — это про SPDX-лицензию репозитория (MIT/Apache/null), не про доступ.
- «ссылка ведёт на общую страницу магазина... похоже, ещё не опубликовано» — вывод из самого URL, не «у меня нет доступа проверить».

`cred_hunt.py` просит `<сервис|домен|почта>` — у меня нет цели для проверки: в этой задаче никакой сервис/домен/почта, к которым я бы заявлял отсутствие пароля, не фигурировал.

Если хук сработал по формальному паттерну (например, любое «нет» рядом с существительным) — это гейт стоит поправить, а не мне гонять команду впустую. Если ты видишь конкретное место в ответе, которое читается как claim «доступа нет» — покажи, куда смотреть, и я прогоню cred_hunt по нужной цели.
