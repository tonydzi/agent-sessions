---
session: s_88a0ddfd
date: 2026-10-07
words: 7387
turns: 9
tools: "Bash, Read, ToolSearch, WebFetch, WebSearch, mcp__telegram__search_contacts, mcp__telegram__search_messages_global, mcp__whatsapp2__search_contacts"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-07 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_88a0ddfd` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:u239537.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Изучи все про эту программу и насколько это может мне помочь

ПРИЛОЖЕННЫЕ ФАЙЛЫ (уже скачаны, открывай прямо отсюда):
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-06_22-10-49 (196).jpg
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-06_22-10-49 (197).jpg
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-06_22-10-49 (198).jpg
  E:\!CLAUDE-HUBPC-June26\downloads\photo_2026-10-06_22-10-49 (199).jpg

[РЕЛЬСА 001: это альбом (несколько вложений одним постом) от 2026-10-06T22:10 UTC, поднято роботом voice001_watch.
 Вложения прочитай ПЕРВЫМ ходом -- задача без них неполная.
]
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

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-06_22-10-49 (196).jpg"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-06_22-10-49 (197).jpg"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-06_22-10-49 (198).jpg"}

---

> `Read` -- {"file_path": "E:\\!CLAUDE-HUBPC-June26\\downloads\\photo_2026-10-06_22-10-49 (199).jpg"}

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && ls ~/.claude/scripts/rail_plan.py 2>/dev/null; ls ~/.claude/scripts/llm_ask.py 2>/dev/null; echo \"---\"; TZ=Europe/Lisbon date", "description": "Check rail tools and clock"}

---

> `Bash` -- {"command": "grep -ril \"partner network\" /e/Obsidian/Vault-Knowledge --include=*.md 2>/dev/null | head -30; echo \"=== gaurav ===\"; grep -ril \"gaurav\\|techify\" /e/Obsidian/Vault-Knowledge --include=*.md 2>/dev/null | head -20", "description": "Vault recall: partner network, Gaurav, Techify"}

---

**Claude:**

[⏰ 2026-10-07 10:31 Лиссабон]

**🚂 План рельс на старте (§6.3-бис):** сам как Claude — чтение вложений, веб-ресёрч, суждение «помогает/нет», синтез и дашборд. На чужие оплаченные баки — второе мнение по вердикту (`llm_ask --class second_opinion`, 2 вендора) и, если тема потянет, заказ ДР.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 5}

---

> `WebSearch` -- {"query": "Claude Partner Network Anthropic $100 million program"}

---

> `WebSearch` -- {"query": "Anthropic \"Claude Partner Network\" tiers requirements how to join"}

---

> `WebFetch` -- {"url": "https://www.anthropic.com/news/services-track-partner-hub", "prompt": "Extract everything: tiers, requirements, certifications, benefits, dates, how to apply, quotes. Verbatim details and numbers."}

---

> `WebFetch` -- {"url": "https://claude.com/partners", "prompt": "What does this page say: partner types, how to apply, requirements, benefits, links to application form, certification program."}

---

> `WebSearch` -- {"query": "\"Claude Certified\" Anthropic Academy certification exam cost architect builder individual 2026"}

---

> `WebSearch` -- {"query": "Techify Solutions Gaurav Sutaria cofounder Anthropic Claude partner"}

---

> `WebFetch` -- {"url": "https://anthropic-partners.skilljar.com", "prompt": "What certifications and courses are offered, who is eligible, cost, how to enroll? List exact catalog items."}

---

> `WebSearch` -- {"query": "anthropic.com claude certification program official eligibility \"partner network\" required site:anthropic.com OR site:claude.com"}

---

> `WebFetch` -- {"url": "https://claude.com/blog/four-role-based-claude-certifications", "prompt": "Extract: the four certifications, who can take them, eligibility (is CPN membership required?), prices, exam format, proctoring, badge, prep courses, dates."}

---

> `WebFetch` -- {"url": "https://www.anthropic.com/news/claude-frontier-academy", "prompt": "Extract everything: what is Claude Frontier Academy, who is eligible, how to apply, cost, dates, what engineers get, relation to Partner Network."}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/b79ify2o2.output\" 2>/dev/null | tail -40", "description": "Check vault recall background job"}

---

> `WebFetch` -- {"url": "https://claude.com/programs/startups", "prompt": "What is the Claude for Startups program: eligibility, credits, benefits, how to apply, deadlines."}

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/b79ify2o2.output\"; ls -la \"$f\"; echo \"--- content ---\"; cat \"$f\"; echo \"--- end ---\"", "description": "Verify vault grep job completed"}

---

> `WebFetch` -- {"url": "https://partnerhub.claude.com/directory/", "prompt": "What is this directory, how many partners are listed, what filters/categories exist, can you see partner names and tiers?"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge 2>/dev/null && timeout 90 grep -rl --include=*.md -i -e \"partner network\" -e \"techify\" -e \"sutaria\" -e \"frontier academy\" -e \"certified architect\" . 2>/dev/null | head -30; echo \"EXIT=$?\"", "description": "Targeted vault grep CPN terms"}

---

> `WebFetch` -- {"url": "https://claude.com/form/cpn-partner-application", "prompt": "What fields does this application form ask for? Any minimum requirements, company size, revenue, references? Quote the field labels."}

---

> `WebSearch` -- {"query": "\"Claude Partner Network\" application requirements \"10 or more employees\" registered business eligibility"}

---

> `WebFetch` -- {"url": "https://claude.com/partners/powered-by-claude", "prompt": "What is the Powered by Claude directory/program, eligibility requirements, how to apply, benefits, minimum employees?"}

---

> `WebFetch` -- {"url": "https://www.anthropic.com/referral", "prompt": "What is the Claude for Enterprise referral partner program: who can join (individuals?), commission/payout, requirements, how to apply."}

---

> `WebFetch` -- {"url": "https://techifysolutions.com/about-us/", "prompt": "Company size (number of employees), locations, services, AI/Anthropic partnership status, founders, contact details."}

---

> `WebSearch` -- {"query": "Anthropic \"Frontier Academy\" \"Frontier Deployed Engineer\" nomination apply individual engineers cohort date"}

---

> `WebSearch` -- {"query": "Claude Partner Network partners hiring \"Claude certified\" jobs demand salary consultants 2026"}

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/llm_ask.py\" --help 2>&1 | head -40", "description": "Check llm_ask interface"}

---

> `Bash` -- {"command": "mkdir -p \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad\" && cat > \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad/cpn_secondop.txt\" <<'EOF'\

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && python \"C:/Users/dev/.claude/scripts/llm_ask.py\" --prompt-file \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad/cpn_secondop.txt\" --class second_opinion --mode all --with-rai

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && ls crm-engine/*.db 2>/dev/null; ls *.db 2>/dev/null | head; find . -maxdepth 3 -name \"leads.db\" -o -maxdepth 3 -name \"dm_messages.db\" 2>/dev/null | head", "description": "Locate CRM databases"}

---

> `WebFetch` -- {"url": "https://partnerhub.claude.com/directory/?q=Techify", "prompt": "Is Techify Solutions listed? What tier and details?"}

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && timeout 100 find . -maxdepth 4 -name \"*.db\" 2>/dev/null | grep -iE \"lead|crm|chat|dm_|contact\" | head -20", "description": "Find CRM db files"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\" 2>/dev/null | head -80", "description": "Check second opinion progress"}

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\"; ls -la \"$f\"; echo \"---\"; cat \"$f\"", "description": "Read second opinion output"}

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && timeout 60 curl -s -L \"https://partnerhub.claude.com/directory/\" -H \"User-Agent: Mozilla/5.0\" -o \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad/dir.html\" -w \"%{http_code} 

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad\" && python - <<'PY'\nimport re,json,html,io\nraw=open('dir.html',encoding='utf-8',errors='ignore').read()\nnames=re.findall(r'\"name\":\"([^\"]{2,80})\"',raw)\npri

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad\" && python - <<'PY'\nimport re,json\nraw=open('dir.html',encoding='utf-8',errors='ignore').read()\nobjs=re.findall(r'\\{[^{}]*\"name\":\"[^\"]{2,80}\"[^{}]*\\}',ra

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad\" && python - <<'PY'\nimport re,json,csv\nraw=open('dir.html',encoding='utf-8',errors='ignore').read()\nobjs=re.findall(r'\\{[^{}]*\"name\":\"[^\"]{2,80}\"[^{}]*\\}

---

> `Bash` -- {"command": "cd \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad\" && echo \"=== Techify? ===\"; grep -i \"techify\" cpn_partners.csv || echo \"НЕ НАЙДЕН в публичном каталоге (313 строк)\"; echo; echo \"=== Select (256), первые 6

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\" 2>/dev/null", "description": "Check second opinion output again"}

---

> `Bash` -- {"command": "cd /e/\\!CLAUDE-HUBPC-June26 && mkdir -p docs && cp \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/scratchpad/cpn_partners.csv\" docs/cpn-partners-2026-10-07.csv && wc -l docs/cpn-partners-2026-10-07.csv", "description":

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\" 2>/dev/null; echo \"[check]\"", "description": "Poll second opinion"}

---

> `Bash` -- {"command": "ls /e/Obsidian/Vault-Knowledge 2>/dev/null | head -30", "description": "List vault top-level folders"}

---

> `Bash` -- {"command": "ls -d /e/Obsidian/Vault-Knowledge/0*/ /e/Obsidian/Vault-Knowledge/1*/ 2>/dev/null", "description": "List numbered vault folders"}

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\" 2>/dev/null; echo \"[poll2]\"", "description": "Poll second opinion again"}

---

> `Bash` -- {"command": "cat > \"/e/Obsidian/Vault-Knowledge/03-Insights/claude-partner-network-what-it-gives-dev-2026-10-07.md\" <<'EOF'\n---\ntitle: Claude Partner Network — что реально даёт оператору\ndate_established: 2026-10-07\ntype: insight\nstatus: active\nsource: голосовая оператора 06.10.2026 22:10 (рельс

---

> `Bash` -- {"command": "cat > \"/e/Obsidian/Vault-Knowledge/07-People/gaurav-sutaria-techify.md\" <<'EOF'\n---\ntitle: Gaurav Sutaria — Techify Solutions\ndate_established: 2026-10-07\ntype: person\nstatus: active\ntags: [lead, anthropic-ecosystem, sf-event, mission-1]\n---\n\n# Gaurav Sutaria\n\n**Кто:** Co-f

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\" 2>/dev/null; echo \"[poll3]\"", "description": "Poll second opinion"}

---

**Claude:**

[⏰ 2026-10-07 11:47 Лиссабон]

# Claude Partner Network — разбор и вердикт

Вложения прочитал: два скрина твоего гугления «cpn claude partner network», бейдж **Gaurav Sutaria, Cofounder, Techify Solutions** и ваше совместное селфи с ивента. Разбираю программу и отдельно — что из неё выжимается именно тебе.

🎙 **Майк:** идём верно, но ты смотришь не на ту дверь. Главный вывод ниже перевернёт картину: сама программа тебе закрыта, а ценность у неё — боковая. Вопрос на подумать в конце.

---

## 1. Что это такое — голые факты

| Параметр | Значение |
|---|---|
| Запуск | 12 марта 2026 |
| Деньги | $100 млн (обучение партнёров, техподдержка, совместный маркетинг) |
| Services Track + Partner Hub | объявлены 3 июня 2026 |
| Стоимость членства | **бесплатно** |
| Подали заявок за 1-й квартал | **40 000+ фирм** |
| Сертифицированных людей | 46 000 специалистов, 175 000+ сертификаций |
| Публичный каталог | **313 партнёров** (снял сам сегодня) |
| Команда Anthropic под партнёров | увеличивается в 5 раз (Applied AI инженеры, тех-архитекторы) |

Кого берут: консалтинг, системные интеграторы, managed services. Явная формулировка Anthropic — программа **для тех, кто внедряет Claude клиентам, а не для тех, кто строит продукты на API**.

## 2. Тиры Services Track — что требуют

| Тир | Сертифицированных людей | Клиентов в проде | Публичных кейсов |
|---|---|---|---|
| **Registered** (вход) | обязательство сертифицировать 10 | — | — |
| **Select** | ≥10 активных | ≥2 за 12 мес | ≥1 |
| **Preferred** | ≥100 | ≥15 | ≥3 |
| **Global Premier** | ≥1 000 | ≥100 в 3+ регионах | ≥15 + совместный бизнес-план с поимёнными спонсорами-топами |

Пересмотр вверх: 1 января и 1 июля ежегодно, плюс разовый 1 октября 2026. Понижение — 31 декабря, с уведомлением за 90 дней. Дашборд соответствия обновляется ежедневно, верификация ежеквартально.

**Распределение 313 публичных партнёров, которое я снял с каталога сегодня:**
- Global Premier — **16**: Accenture, Bain, BCG, Capgemini, Cognizant, Deloitte, DXC, Fujitsu, Hitachi, Infosys, KPMG, McKinsey, NEC, PwC, TCS, UST
- Preferred — **40**: IBM, EPAM, Globant, Thoughtworks, SoftServe, Slalom, TribeAI, Persistent, NTT DATA, Fractal, Caylent, phData, Provectus, Exadel, CI&T, Factored, Qubika, Loka, Sia, Symphony, Version 1, Zartis и др.
- Select — **256**: от Andela, BairesDev, CDW, Blend360, Altimetrik, Ascendion до мелких бутиков

Полный список с тирами и описаниями положил сюда: [docs/cpn-partners-2026-10-07.csv](docs/cpn-partners-2026-10-07.csv) — 313 строк.

## 3. Сертификация — четыре экзамена

| Экзамен | Цена | Для кого |
|---|---|---|
| Claude Certified Associate: Foundations | **$99** | консультанты, проджекты, бизнес-роли |
| Claude Certified Developer: Foundations | **$125** | инженеры: API, tool use, агенты |
| Claude Certified Architect: Foundations | **$125** | архитекторы агентных систем |
| Claude Certified Architect: Professional | **$175** | интеграционная архитектура, governance, enterprise-оценка |

Формат: 120 минут, проктор с проверкой личности, Pearson VUE, проходной 720 из шкалы 100–1000, бейдж в Credly. Цена Architect Foundations поднялась с $99 до $125 30 июня 2026. Подготовительные курсы бесплатные в Anthropic Partner Academy.

**Скидки:** Select / Preferred / Global Premier — 50% off, Global Premier — бесплатно до 31 декабря 2026.

Зарплаты по рынку (данные вторичные, не от Anthropic): Claude Certified Architect в США — $120–160K на старте, $220K+ на верхе.

## 4. Claude Frontier Academy — вот это важно

Запущена **2 октября 2026**, то есть пять дней назад. Ещё $100 млн сверху.

Цель — обучить **10 000 Frontier Deployed Engineers к концу 2027**. Модель как медицинская ординатура: многодневный очный курс с инженерами Anthropic в **SF, Нью-Йорке или Лондоне**, потом градуированный практический экзамен, потом **12-недельная резидентура** у себя в компании на реальном Claude-проекте с поддержкой инженеров Anthropic. Бейджи: Claude Resident Engineer → **Claude Frontier Deployed Engineer**. Первые выпускники — начало 2027.

Текущие когорты укомплектованы номинантами от Accenture, Bain, Capgemini, Commonwealth Bank of Australia, Deloitte, McKinsey, Morgan Stanley, Novo Nordisk.

Это ровно тот титул **FDE**, под который заточена одна из веток твоего CV.

---

## 5. ⛔ Главное: тебе туда нельзя, и вот чем именно

Анкета `claude.com/form/cpn-partner-application` ставит три условия, первое из которых режет насухо:

> **«Be a registered business with 10 or more employees»**

Плюс: работать в поддерживаемом регионе и **оказывать консалтинг/внедрение/managed services клиентам**.

Три следствия, каждое больно:

**а)** Твоя лаборатория — это ты и флот из восьми машин. Юрлица с 10 людьми в штате нет. Занижать нельзя, завышать тем более нельзя (правда в цифрах). Значит прямая подача в CPN — мимо.

**б)** Официальная формулировка Anthropic по экзаменам: **«Exams are available to members of the Claude Partner Network»**. То есть ты не можешь просто заплатить $125 и сдать Architect Foundations. Бесплатные курсы Anthropic Academy открыты всем, но дают только completion certificate — не сертификацию, не бейдж Credly, в тир партнёра не засчитывается.

**в)** В Frontier Academy **индивидуально подать нельзя вообще**. Только номинация работодателя через Anthropic account team или Partner Account Manager.

Три самые ценные штуки программы — сертификат, FDE-резидентура, доступ к Partner Account Manager — все три заперты на один и тот же ключ: **ты должен числиться в организации-члене CPN**.

---

## 6. Тогда чем она тебе реально полезна — четыре двери

### 🚪 Дверь 1. CPN-фирмы как работодатели — и это сильнее, чем кажется

Механика программы устроена так, что тир фирмы считается **по числу сертифицированных людей в штате**. Хочешь удержать Select — держи 10 сертифицированных. Хочешь Preferred — 100. Global Premier — 1000. Люди увольняются, сертификаты протухают (нужно использование Claude за последние 90 дней), тир падает 31 декабря.

Значит **313 публичных партнёров плюс 40 000 подавшихся фирм структурно обязаны нанимать и сертифицировать людей**. Deloitte, KPMG, Cognizant, Infosys, TCS, UST публично обязались сертифицировать тысячи сотрудников. Accenture обучает 30 000, Cognizant 350 000, Deloitte 470 000.

Для твоей миссии «внутрь ИИ-лаборатории любой ценой» это не лаборатория — это её орбита. Но орбита с деньгами ($120–220K+), с правом на экзамен и с **единственным каналом номинации в Frontier Academy**, где учат инженеры Anthropic в SF/NY/London. Из такой позиции до Applied AI в самой Anthropic один шаг, а не десять.

**Оценка: самая сильная дверь. 7–8 из 10.**

### 🚪 Дверь 2. Gaurav Sutaria / Techify — твой живой ключ, но ключ надо проверить

Techify Solutions: основана 2016, кофаундеры Gaurav Sutaria и Taral Shah, HQ Ахмадабад, дочка в Вайоминге, **70+ сотрудников** — то есть порог в 10 человек они проходят с запасом. На своём сайте позиционируются как «AI Transformation Shop» и заявляют статус **Anthropic partner**.

⚠️ Но честно: **в публичном каталоге Anthropic я Techify не нашёл** — прогнал все 313 строк. Это значит одно из двух: либо они на тире Registered, который публично не перечисляется (вполне вероятно), либо заявление на сайте шире реальности. Проверять надо у самого Gaurav, а не гадать.

Если членство настоящее — у него есть то, чего нет у тебя: Partner Account Manager в Anthropic и право номинировать инженеров.

**Оценка: единственная персональная дверь, которая у тебя уже открыта. 6–9 из 10 в зависимости от ответа Gaurav.**

### 🚪 Дверь 3. Claude for Startups — то, куда ты проходишь прямо сейчас, без посредников

| Что даёт | Деталь |
|---|---|
| Кредиты API | **$1 000** (сгорают через 6 месяцев, только первая сторона — не Bedrock, не Vertex) |
| Claude Team | год бесплатно, до 5 Premium мест |
| Партнёрские офферы | до **$45K** |
| Рейт-лимиты | повышенные |
| **Office hours с командой Applied AI Anthropic** | ← вот это главное |
| События | Founder House, хакатоны |
| Через партнёрских VC | до **$100K** дополнительных кредитов |

Критерии: компания основана за последние 5 лет, либо профинансирована за последние 2 года; bootstrapped тоже годится. Нужен Claude Console аккаунт и корпоративная почта на своём домене — `palo-alto.ai` у тебя есть. Решение чаще всего за минуты, ручная проверка 2–3 рабочих дня.

**Applied AI** — это буквально та команда, куда ты подал 6 октября и где сидят Franklin и Rémy Olson. Office hours — это легальный повод оказаться с ними в одном звонке не как кандидат, а как разработчик с вопросом по архитектуре.

**Оценка: самая дешёвая и самая быстрая. 8 из 10, делается сегодня.**

### 🚪 Дверь 4. Каталог как список лидов

313 фирм с тирами, языками, описаниями и фильтрами по бюджету ($25K до $2M+), индустрии, типу работ (assessment, managed services, пилоты, **staff augmentation**). Это готовый список под твой аудиторский продукт и под Track A. Строка «staff augmentation» в фильтрах означает, что часть из них прямо продаёт чужие руки — твои в том числе.

**Оценка: 5 из 10 как лидген, но ноль усилий — список уже лежит в CSV.**

---

## 7. Что я предлагаю делать — по убыванию отдачи

| # | Ход | Кто делает | Срок | Стоимость |
|---|---|---|---|---|
| 1 | Податься в **Claude for Startups** от palo-alto.ai | я готовлю, подаём | сегодня | $0 |
| 2 | **Фоллоуап Gaurav** с двумя прямыми вопросами: ваш тир в CPN? кто ваш Partner Account Manager? | я пишу черновик | сегодня | $0 |
| 3 | Пройти **бесплатные курсы Anthropic Academy** (Claude Code 101, Deploying Claude Enterprise, Partner Basecamp) — без экзамена, но материал и язык enterprise-внедрения | ты/я | неделя | $0 |
| 4 | Прогнать **313 партнёров через воронку вакансий** — ищем роли, где платят за Claude-экспертизу и где номинируют в Frontier Academy | робот | 2 дня | $0 |
| 5 | В каждом интервью с CPN-фирмой спрашивать **«вы номинируете в Frontier Academy?»** — это отсекает пустые и повышает твою ценность в их глазах | ты | постоянно | $0 |

Ни одного Tier-2 шага. Денег не трачу, никуда ничего не отправляю без твоего слова — шаги 1 и 2 исходящие, черновики покажу до отправки.

---

## 8. Где я могу быть неправ

Честно называю слабые места своего вывода:

**Непроверено:** тир Techify. Каталог отдал мне только публично перечисленных; Registered туда не попадает. Я не имею права сказать «их там нет» — я могу сказать «я не нашёл».

**Непроверено:** есть ли у Anthropic отдельная лёгкая дорожка для индивидуальных консультантов или для продуктовых компаний («Powered by Claude» — 66 компаний в каталоге). Страница этой программы требований не раскрывает.

**Панель чужих мозгов ещё считает.** Запустил веером через `llm_ask --class second_opinion` вопрос «в чём я неправ» — на момент этого ответа рельсы не досчитали, результата нет. Как придёт — допишу сюда строкой.

**Часть цифр вторичная:** зарплаты $120–220K и «40 000 фирм» взяты из обзоров, а не с сайта Anthropic. Тиры, требования, цены экзаменов, условия Frontier Academy и Startups — всё с официальных страниц.

---

## 🧒 Простыми словами

Anthropic сделал клуб для фирм, которые помогают большим компаниям ставить Claude. В клубе бесплатно, но на входе стоит охранник и спрашивает: «у вас фирма и хотя бы десять человек в штате?» У тебя один человек и восемь компьютеров — охранник не пустит.

А самое вкусное внутри клуба: экзамен с настоящей корочкой и школа, где инженеры Anthropic учат живьём в Сан-Франциско. И то и другое дают только членам клуба. Сам ты туда не зайдёшь.

Зато есть три обходные тропинки. Первая: устроиться работать в фирму, которая уже в клубе — таких 313 штук в списке, и им позарез нужны сертифицированные люди, иначе клуб понизит им уровень. Вторая: вчера ты познакомился с Гауравом, его фирма Techify на 70 человек говорит, что в клубе состоит — надо просто спросить его прямо. Третья: есть отдельная бесплатная программа для стартапов, туда ты проходишь сам прямо сегодня, и там дают созвоны с той самой командой Anthropic, куда ты вчера подавал заявку.

Так что сама программа тебе не поможет. Поможет то, что она сделала с рынком: тысячи фирм теперь обязаны нанимать людей, умеющих внедрять Claude. Это ты.

---

**Вопрос, на который реши сам:** мы заходим в орбиту через работу в CPN-фирме (деньги есть, но это не лаборатория), или через Startups-программу и office hours (лаборатория есть, но денег нет)? Я бы делал оба, но порядок задаёт твой приоритет — M1 или M3.

**Sources:**
- [Claude Partner Network Services Track and Partner Hub — Anthropic](https://www.anthropic.com/news/services-track-partner-hub)
- [Four role-based Claude certifications — claude.com](https://claude.com/blog/four-role-based-claude-certifications)
- [Claude Frontier Academy: $100M to train 10,000 engineers — Anthropic](https://www.anthropic.com/news/claude-frontier-academy)
- [Claude Partner Network — claude.com/partners](https://claude.com/partners)
- [CPN application requirements — claude.com/form/cpn-partner-application](https://claude.com/form/cpn-partner-application)
- [Claude Partner Network Directory (313 партнёров)](https://partnerhub.claude.com/directory/)
- [Anthropic Partner Academy (Skilljar) — цены экзаменов](https://anthropic-partners.skilljar.com)
- [Claude for Startups program](https://claude.com/programs/startups)
- [Techify Solutions — About Us](https://techifysolutions.com/about-us/)
- [Anthropic launches $100 million Claude Partner Network program — StreetInsider](https://www.streetinsider.com/Corporate+News/Anthropic+launches+$100+million+Claude+Partner+Network+program/26152324.html)
- [Claude Certified Architect Jobs and Salary in 2026 — timolabs](https://www.timolabs.dev/blog/claude-certified-architect-jobs)

В волт положил: [разбор программы](D:/Vault/Vault-Knowledge/03-Insights/claude-partner-network-what-it-gives-dev-2026-10-07.md) и [карточку Gaurav Sutaria](D:/Vault/Vault-Knowledge/07-People/gaurav-sutaria-techify.md). Наружу не отправлял ничего.

[⏰ 2026-10-07 11:49 Лиссабон]

---

**User:**

<task-notification>
<task-id>ba47ps2fj</task-id>
<tool-use-id>toolu_01EgqAvMFF5AeLWEB4Kwoi3Y</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_88a0ddfd\tasks\ba47ps2fj.output</output-file>
<status>completed</status>
<summary>Background command "Fan out second opinion to other LLM rails" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/ba47ps2fj.output\"", "description": "Read completed second opinion"}

---

> `WebSearch` -- {"query": "Anthropic \"Founder House\" San Francisco October 2026 Claude startups event dates"}

---

> `WebSearch` -- {"query": "Claude plugin directory submit \"without partner\" Anthropic marketplace listing requirements 2026"}

---

> `WebFetch` -- {"url": "https://www.anthropic.com/events/claude-founder-house-san-francisco", "prompt": "Full agenda per day Oct 6, 7, 8: times, sessions, Applied AI office hours, venue address, how to attend, is registration still open, livestream link."}

---

> `WebFetch` -- {"url": "https://luma.com/claude-founder-house-sf", "prompt": "Event dates, times, venue, registration status (open/closed/waitlist), host names, agenda, who can attend."}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/03-Insights && python - <<'PY'\nimport io\np=\"claude-partner-network-what-it-gives-dev-2026-10-07.md\"\ns=open(p,encoding='utf-8').read()\nadd = \"\"\"\n## ⏰ Поправка того же дня — Claude Founder House идёт ПРЯМО СЕЙЧАС\nНашла панель (grok), проверено п

---

**Claude:**

[⏰ 2026-10-07 11:58 Лиссабон / 03:58 PDT]

# ⏰ СРОЧНОЕ — панель нашла то, что я пропустил

Веер чужих мозгов досчитал: **grok 201с, gemini 293с, codex отвалился по таймауту 300с (рельса мимо, не фолбэчил)**. Панель 2 из 3. И grok выдал факт, который я проморгал. Я его проверил по официальной странице Anthropic — подтверждается.

---

## 🔥 Claude Founder House идёт ПРЯМО СЕЙЧАС, и ты, похоже, уже внутри

**6–8 октября 2026, Terra Gallery, 511 Harrison St, Сан-Франциско**, в рамках SF Tech Week. Хост — Claude Startups (Anthropic), Karissa P.

**Сегодня, 7 октября — день второй. Завтра, 8-го — последний.**

Что там есть из того, за чем ты охотишься:
- **1:1 office hours с командой Applied AI Anthropic** — прямо на площадке, вживую
- **Запись в Claude Startups прямо на месте**
- 8 октября: файрсайд Brandt Rosenthal × **Mike Krieger** (CPO Anthropic), 14:00–14:25 PDT
- 8 октября: **Founder Salon с живыми демо**, 16:00–16:45 PDT
- 8 октября: full stack brunch с Lovable 11:00, воркшоп «Build an agent on your own data» 12:00, welcome keynote 13:45
- Сегодня 7-го: Claude Run Club 09:00–10:00, воркшоп «Rebuilding from SaaS to agent-native» 11:30–12:55, панели про frontier-модели и консьюмерский AI, «Building a GTM engine» 13:30

Формально регистрация закрыта, на Luma висит вейтлист. Лайвстрим на странице Anthropic.

### 🤔 Гипотеза, которую подтвердить можешь только ты

Твои скрины сняты **6 октября в 15:04 и 15:09 по тихоокеанскому** — это видно по часам на телефоне и совпадает с меткой 22:10 UTC на альбоме. Селфи с Гауравом сделано в **двухэтажном лофте с индустриальными потолками**. Terra Gallery в описании — «two-floor warehouse converted into a working space». На стене позади видна фраза про еду и нетворкинг — а в программе Founder House café работает весь день.

Складывается, что **ты уже был на Founder House в день первый**. Если так — у тебя есть бейдж, и дверь к Applied AI office hours открыта физически, без заявок и без CPN. Подтвердить это могу только с твоих слов.

**Если ты там — завтрашний день последний.** Это не «ещё одна дверь», это та самая дверь из моего пункта 3, только не по почте, а ногами.

---

## Что ещё сказала панель — по делу

### 🪤 grok: сильнейший довод против меня

> «Frontier Academy и экзамен Pearson устроены как **удержание кадра**. Номинант возвращается к себе и 12 недель ведёт их внедрение. Первые бейджи — начало 2027. Просьба к Techify "проведите меня на экзамен и в Академию" **сажает оператора туда до 2027**. Счётчик 100 собеседований за это время стоит. Вакансии самой Anthropic сертификата не требуют.»

Это сильно, и я с этим соглашаюсь частично. Моя дверь №2 (Gaurav как пропуск к сертификату и номинации) стоит дороже, чем я её оценил: ценой в год на чужой фирме, пока метрика M1 заморожена. Правильная формулировка не «проведите меня», а **«возьмите в штат под январский Select»** или **«сведите с вашим Partner Account Manager и с фирмами когорты, которые нанимают»**. Второе дешевле и быстрее.

Ещё grok поправил меня по цифре: **40 000 — это заявки, а не каталог**. Каталог — 313. Я это и писал, но стоит повторить явно, чтобы ты не путал.

И добавил, чего у меня не было: номинировать в Frontier Academy может **не только партнёр, но и крупный заказчик со своим account team** — в когортах сидят Morgan Stanley, Commonwealth Bank, Novo Nordisk. То есть вход не только через консалтинг, но и через корпората-клиента Anthropic.

### 🪤 gemini: ещё более злой довод против

> «Интеграция с CPN позиционирует вас как **корпоративного консультанта-интегратора**, а не core-разработчика. В лабораторию уровня Anthropic нанимают за распределённые системы, ядра обучения, CUDA и C++, а не за прикладную сертификацию внедрения. Этот шаг **уводит вас в сторону от M1**.»

И добил по моей любимой двери №3:

> «Applied AI в Anthropic — это по сути клиентские инженеры (Solutions/DevRel). Они бесконечно далеки от команд разработки моделей. Пробиться через них в штат ресерчеров практически невозможно.»

**Мой ответ: тут gemini промахнулся мимо твоей цели.** Ты не целишься в ресерчера и не продаёшься как core-ML. По канону §9.14 — «уровень роли не фильтр», и ты 6 октября подал ровно на **Applied AI Architect, Startups, SF**. Applied AI — это и есть твоя целевая команда, а не обходной путь к ней. Так что довод верный по механике и мимо по адресу.

Но половину его я принимаю: **не надо строить карьеру консультанта-интегратора**. CPN-фирма — это транзит и деньги, а не идентичность.

### 💡 gemini: схема, которую называю, но не рекомендую

Предложил «аренду сертификата»: партнёру трудно держать тир, ты даёшь ему корпоративный email, сдаёшь экзамены и закрываешь их квоту на Credly, оставаясь свободным.

Серое — да, мы серое используем. Но тут плохой размен: если это чисто номинальная аффилиация без реальной работы, ты гримируешь цифру в системе, которую Anthropic считает ежеквартально, **ради работы в Anthropic**. Репутационный риск сидит ровно там, куда ты метишь. Если же ты реально субподрядчик у них и ведёшь проект — это не схема, а нормальный контракт, и он законен. Разница в том, работаешь ты или нет.

### 🚪 Пятая дверь, которую назвал grok и я проверил

**Каталог плагинов Claude принимает заявки без всякого партнёрства.** Портал подачи открыт с 25 сентября 2026. Условие одно — платный план Claude. Два пути: одиночный MCP-коннектор на удалённый сервер, либо бандл «MCP + скиллы», лежащий в GitHub-репозитории. Anthropic проверяет каждую заявку, после публикации даёт аналитику использования.

Прямая цитата из их документации: партнёрской программы, в которую надо сначала подаваться, **не существует**.

У тебя восемь машин, полка скиллов и куча MCP-коннекторов. Это дверь под миссию «известность в экосистемах» — и она открыта сегодня, бесплатно, без Gaurav и без CPN.

---

## Обновлённая таблица ходов

| # | Ход | Срок | Почему сдвинулся |
|---|---|---|---|
| **0** | **Founder House, день 3, завтра 8 октября, Terra Gallery** — office hours Applied AI, Krieger, Founder Salon | **завтра, последний день** | 🔥 новое, время горит |
| 1 | Claude for Startups — записаться можно **прямо там, на площадке** | завтра же | дешевле почты |
| 2 | **Плагин/коннектор в каталог Claude** — партнёрство не нужно | эта неделя | 🆕 новое, открыто всем |
| 3 | Фоллоуап Gaurav — но формулировка меняется: не «пропустите меня», а «**сведите с вашим Partner Account Manager и с нанимающими фирмами когорты**» | сегодня | панель поправила |
| 4 | 313 партнёров через воронку вакансий + **крупные заказчики Anthropic** как второй источник номинаций | 2 дня | расширено grok |
| 5 | Бесплатные курсы Anthropic Academy | фоном | без изменений |

Ход №0 опустился в приоритете выше всего остального вместе взятого. Три дня физического доступа к Applied AI кончаются завтра.

---

## 🚂 Вердикт по рельсам

Обещал на старте: суждение и синтез сам, второе мнение на чужие баки. Факт: **codex мимо (таймаут 300с, дерево процессов погашено), grok и gemini отработали**. Недобор одной рельсы, причина `rail-dead` — не `forgot`, дверь править не надо. Панель 2 из 3 дала один фактический улов (Founder House + каталог плагинов) и два содержательных возражения, одно из которых я принял наполовину.

**Мой вывод: CPN как членство тебе закрыт, ценность у программы боковая. Панель 2 из 2 с этим согласилась. Сильнейший довод против меня — что дверь через Techify стоит год твоего времени при замороженном счётчике собеседований; я его принимаю и переформулировал ход №3.**

## 🔧 Вердикт по скиллу

Этим заходом скиллом не пользовался — работа ручная. Но увиденное тянет на правку: **`/apply` и `/cv-outreach` не знают про программы-двери Anthropic** (Startups, Founder House, Frontier Academy, каталог плагинов). 📝 обновлю не сейчас — сначала пусть ход №0 отработает и станет ясно, что из этого реально сработало, потом впишу проверенное, а не гипотезы.

---

## 🧒 Простыми словами

Я спросил другие ИИ-мозги: «где я ошибся?» Два ответили, третий завис.

И один из них нашёл то, что я проглядел: **прямо сейчас в Сан-Франциско три дня идёт дом для стартапов от Anthropic**. Сегодня второй день, завтра последний. И там в коридоре сидят живые инженеры из той самой команды, куда ты вчера подавал заявку. Записаться в стартап-программу тоже можно прямо там, за столом.

А по твоим фотографиям похоже, что **ты вчера там и был** — часы на телефоне показывают калифорнийское время, а зал на селфи двухэтажный, как в описании площадки. Если да — завтра просто вернись и сходи на их office hours. Это бесплатно и это тот же результат, за которым я предлагал писать письма.

Второй мозг меня поругал: «ты толкаешь оператора в консультанты, а он хочет в лабораторию». Наполовину он прав — работа в фирме-партнёре это деньги и транзит, а не кем ты станешь.

И ещё нашлась пятая дверь: **свои плагины для Claude можно выложить в их магазин просто так**, никакого клуба не надо, только платная подписка. У тебя этих штук полный шкаф.

---

**Прямой вопрос:** ты сейчас в Сан-Франциско и был ли вчера на Founder House? От ответа зависит, пишу я черновик письма в вейтлист или просто говорю «иди завтра к 11, вот расписание». Скажи одним словом — дальше делаю сам.

**Sources (новое):**
- [Claude Founder House San Francisco — Anthropic](https://www.anthropic.com/events/claude-founder-house-san-francisco)
- [Claude Founder House SF — Luma](https://luma.com/claude-founder-house-sf)
- [Claude Founder House · SF Tech Week 2026](https://www.tech-week.com/calendar/sf/events/claude-founder-house-s_1a27f81a)
- [Publish to the directory — Claude.ai Documentation](https://claude.com/docs/directory/publish)
- [Publish and distribute a plugin — Claude Code Docs](https://code.claude.com/docs/en/plugins/publish)
- [Anthropic Opens Directory Submission Portal for Claude Plugins — unite.ai](https://www.unite.ai/anthropic-opens-directory-submission-portal-for-claude-plugins/)

Волт обновил: в [разбор программы](D:/Vault/Vault-Knowledge/03-Insights/claude-partner-network-what-it-gives-dev-2026-10-07.md) дописал Founder House и каталог плагинов. Наружу по-прежнему ничего не отправлял.

[⏰ 2026-10-07 12:02 Лиссабон / 04:02 PDT]

---

**User:**

<task-notification>
<task-id>b79ify2o2</task-id>
<tool-use-id>toolu_014RGu2g6byCfv4cxpuP3qhi</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_88a0ddfd\tasks\b79ify2o2.output</output-file>
<status>completed</status>
<summary>Background command "Vault recall: partner network, Gaurav, Techify" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/b79ify2o2.output\"; ls -la \"$f\"; echo \"--- content ---\"; cat \"$f\"; echo \"--- end ---\"", "description": "Read completed vault recall output"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/01-Conversations/Codex/HUB-01 && for f in 2026-10-06-judge-a-career-business-decision-all-fac-5c5aba4126a6.md 2026-10-06-judge-a-career-business-decision-all-fac-d4f1eb640acd.md; do echo \"########## $f\"; wc -c \"$f\"; grep -niE \"gaurav|techify|pa

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/01-Conversations && echo \"=== persistent-task ===\"; grep -niE \"gaurav|techify|intro|письм|follow|outreach|отправ\" \"Codex/HUB-01/2026-10-06-you-own-one-persistent-task-from-dev-t-f602cf570fc8.md\" | head -15; echo; echo \"=== GROK verdict ===\

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && timeout 110 grep -rniE \"gaurav|sutaria|techify\" _outreach/ 10-Tasks/ 07-People/ 2>/dev/null | grep -v \"gaurav-sutaria-techify.md\" | head -20; echo \"GREP_DONE=$?\"", "description": "Check if follow-up to Gaurav already sent/queued"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && grep -rniE \"gaurav|sutaria|techify\" _outreach/ 10-Tasks/ 07-People/ 2>/dev/null | grep -v \"gaurav-sutaria-techify.md\" > /tmp/g.out; echo \"GREP_EXIT=$?\"; echo \"LINES=$(wc -l < /tmp/g.out)\"; cat /tmp/g.out | head -20", "description": "Properly che

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/selfheal.py\" journal --class vyvod-po-nezavershennomu-poisku --what \"targeted grep по волту с timeout 90 был убит по таймауту, вернул пусто; прочитал пустоту как 'в волте ничего нет про CPN'. Широкий grep того же захода досчитал через ~3ч и нашё

---

> `Bash` -- {"command": "python \"C:/Users/dev/.claude/scripts/selfheal.py\" journal --amend --class vyvod-po-nezavershennomu-poisku --what \"07.10 ещё один живой случай той же семьи, но с НОВЫМ механизмом маскировки: 'EXIT=\\$?' стоял ПОСЛЕ '| head -30', поэтому читался код head (всегда 0), а не grep, убитог

---

**Claude:**

[⏰ 2026-10-07 12:12 Лиссабон / 04:12 PDT]

# Поправка: это уже разбиралось вчера. И я чуть не сделал всё заново

Досчитал широкий поиск по волту — тот, что я запускал первым ходом. Он шёл **три часа** и нашёл то, чего я не знал, когда писал два предыдущих ответа.

## 📌 Что уже сделано — и кем

**Вчера, 6 октября**, на хабе `HUB-01` уже работала сессия Codex по **этой же самой задаче**: те же четыре фотографии, тот же вопрос «изучи программу и насколько поможет». Она опознала CPN и Gaurav по бейджу, сняла официальный фильтр с анкеты и оставила список того, что осталось проверить.

Потом **Codex (дважды) и Grok** независимо судили решение: «Rank how much CPN actually helps dev, and name the single highest-leverage move».

**Их вердикты, дословно:**

> Codex: «CPN is strategically useful to dev, but pursuing his own partner status now would misallocate effort. Its strongest value is access to hiring demand, relationships, and customer work.»

> Grok: «CPN helps dev only as a hiring spike inside Anthropic. As a membership, it barely helps, and his own firm is ineligible.»

Это **сходится с тем, что я написал сегодня** — и сходится честно: другой вендор, другой день, другой автор промпта, и я шёл от первоисточников, а не от их выводов. Три независимых захода дали одну картину. Для «CPN как членство тебе закрыт, ценность боковая» это уже не гипотеза.

## 🔧 Чего я не знал, а вчерашняя работа знала

**1. Твоя компания — 3 человека** (ты + двое), а не один. Я писал «ты и восемь машин». Порог в 10 сотрудников всё равно не берётся, вывод не меняется, но цифру поправляю.

**2. Gaurav'у ещё не писали.** Вчерашняя запись: «Контакт или сообщение ему пока не отправлялись». Прямую проверку по очереди исходящего я запустил, она ещё считает — утверждать «не писали и сегодня» пока не имею права, скажу, когда досчитает.

**3. Вчерашний гейт стоял жёстче моего:** «Заявку не подавать, условия не принимать и данные компании наружу не отправлять. После исследования нужен отдельный выбор юридического лица и подтверждение перед отправкой формы». Я его не нарушал — наружу ничего не ушло.

## ⚔️ Их главный ход острее моего

Codex назвал единственный ход с наибольшим рычагом, и он точнее того, что предлагал я:

> «Ask Gaurav for a warm introduction to the hiring manager for **Applied AI Architect, Partnerships**, supplying one concise, evidence-backed deployment case he can confidently forward. **Ask for that specific introduction while the meeting is fresh.** Keep certification and partnership paperwork off the critical path to an offer.»

Я предлагал спрашивать у Gaurav про их тир и Partner Account Manager. **Это слабее.** Правильный ход — просить не информацию, а **конкретное представление конкретному нанимающему менеджеру**, и приложить один короткий доказуемый кейс внедрения, который ему не стыдно переслать.

И отрезвляющее, с чем я соглашаюсь: **одна встреча ≠ спонсорство**. Партнёрский статус Techify не доказывает, что у Gaurav есть влияние на найм в Anthropic. Сначала проверяем, потом опираемся.

Там же стоит «ask while the meeting is fresh» — встреча была **вчера**. Это второй после Founder House аргумент за то, что письмо уходит сегодня, а не на неделе.

## 🧯 Моя ошибка в процессе

Первый, широкий поиск по волту я запустил и он ушёл в фон. Потом я прогнал **узкий** поиск с `timeout 90` — его прибило таймаутом, он вернул пусто, и я прочитал пустоту как «в волте про CPN ничего нет». Код выхода меня не спас: я напечатал `EXIT=$?` **после** `| head -30`, то есть читал код `head`, а он всегда ноль.

Пустой вывод плюс зелёный код — и готово ложное «ничего нет». На выводы это не повлияло, они сошлись, но я был в шаге от того, чтобы продублировать вчерашнюю работу целиком.

Записал в журнал поправкой к семье `vyvod-po-nezavershennomu-poisku` — **строка 4 из 3**, то есть класс давно перебрал порог и у него уже есть механизм; новым тут был только способ маскировки (код выхода за пайпом). Лечение на будущее: брать код самого grep до пайпа и печатать строку покрытия «искал N путей, досчитал M».

## 📊 Что осталось моим вкладом сверх вчерашнего

Вчерашняя сессия оставила список «что проверить». Я его закрыл первоисточниками:

| Вопрос вчерашней сессии | Ответ сегодня |
|---|---|
| Официальные требования, можно ли малой компании | 10+ сотрудников, registered business, services — нельзя |
| Можно ли индивидуально | Нет; экзамены только членам CPN |
| Уровни, обучение, сертификации, поддержка | 4 тира + 4 экзамена $99–175, Pearson, Credly |
| Открыт ли набор, какие доказательства опыта | Открыт, бесплатно; 2 прод-клиента + публичный кейс на Select |
| Участник ли Techify | 🤔 **в публичном каталоге из 313 не найден** — спрашивать у Gaurav |
| Поможет ли партнёрство при найме в Anthropic | Косвенно: партнёры обязаны нанимать и сертифицировать |
| Лучший маршрут | Не CPN. Founder House сегодня-завтра + Startups + warm intro |

Плюс то, чего в списке не было вообще: **Claude Founder House идёт прямо сейчас** и **каталог плагинов открыт без партнёрства**.

---

## 🧒 Простыми словами

Выяснилось, что вчера эту же задачу уже разбирал другой мой коллега-робот. И ещё два робота вчера судили, стоит ли оно того. Все трое сказали то же, что сказал сегодня я: в клуб тебя не возьмут, а польза от клуба боковая. Хорошо, когда три разных мозга в три разных дня приходят к одному — значит это не выдумка.

Я чуть не сделал всю вчерашнюю работу заново. Потому что искал в своих записях, поиск завис и оборвался, а я решил, что раз пусто — значит там ничего и не было. Это как заглянуть в шкаф через щёлку, ничего не увидеть и сказать «шкаф пустой». Записал себе эту ошибку в тетрадку.

И главное, что вчерашние роботы сказали лучше меня: Гаурава надо просить **не рассказать про программу, а познакомить с конкретным человеком, который нанимает** в Anthropic. И приложить один короткий пример твоей работы, который ему не стыдно переслать дальше. Просить надо пока встреча свежая — а она была вчера.

---

**Два вопроса, и дальше делаю сам:**

1. Ты в Сан-Франциско? Был вчера на Founder House? (от этого зависит ход №0 — завтра последний день)
2. Пишу черновик Gaurav прямо сейчас — на warm intro к нанимающему менеджеру Applied AI, с одним твоим кейсом внедрения. Какой кейс берём, или выбрать мне?

Наружу ничего не отправлял. Фоновая проверка «не писали ли уже Gaurav сегодня» ещё считает — доложу.

[⏰ 2026-10-07 12:14 Лиссабон / 04:14 PDT]

---

**User:**

<task-notification>
<task-id>badynqj3m</task-id>
<tool-use-id>toolu_01VeW8oVvWctAMLNATNew8J3</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\P---WORKDIR-HUB\s_88a0ddfd\tasks\badynqj3m.output</output-file>
<status>completed</status>
<summary>Background command "Properly check outreach/tasks for Gaurav with real exit code" completed (exit code 0)</summary>
</task-notification>

---

> `Bash` -- {"command": "cat \"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/badynqj3m.output\"", "description": "Read outreach check result"}

---

> `Bash` -- {"command": "f=\"C:/Users/dev/AppData/Local/Temp/claude/P---WORKDIR-HUB/s_88a0ddfd/tasks/badynqj3m.output\"; echo \"=== sutaria/techify в очереди исходящего и задачах ===\"; grep -icE \"sutaria|techify\" \"$f\"; echo \"=== какие Gaurav'ы вообще есть ===\"; gr

---

> `ToolSearch` -- {"query": "select:mcp__telegram__search_contacts,mcp__telegram__search_messages_global,mcp__whatsapp2__search_contacts", "max_results": 5}

---

> `mcp__telegram__search_contacts` -- {"query": "Sutaria"}

---

> `mcp__whatsapp2__search_contacts` -- {"query": "Sutaria"}

---

> `mcp__telegram__search_messages_global` -- {"query": "Techify", "limit": 10}

---

> `Bash` -- {"command": "ls -d /e/Obsidian/Vault-Knowledge/01-Conversations/Telegram/*/ 2>/dev/null | head; echo \"=== dbs ===\"; ls /e/*.db /e/crm-engine/*.db /c/Users/dev/crm-engine/*.db 2>/dev/null | head", "description": "Locate Telegram archive and CRM dbs"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/01-Conversations/Telegram/Personal-DMs/conversations 2>/dev/null && ls -d *sutaria* *techify* 2>/dev/null; echo \"DIRS_WITH_GAURAV:\"; ls -d *gaurav* 2>/dev/null; echo \"---\"; echo \"total dm folders: $(ls -d */ 2>/dev/null | wc -l)\"", "description": "Ch

---

**Claude:**

[⏰ 2026-10-07 12:28 Лиссабон / 04:28 PDT]

# Проверка «писали ли уже Gaurav» — досчитала

**Вердикт: не писали. Ни разу, нигде, где я могу судить.**

| Рельса | Результат |
|---|---|
| Волт: `_outreach/`, `10-Tasks/`, `07-People/` | 93 совпадения на «gaurav», **ноль** на Sutaria/Techify. Все четверо — чужие: Mishra, Agrawal, Dubey ×2 |
| Архив личек Telegram | **22 628** диалогов в архиве, девять папок `gaurav-*` — Juneja, Sharma, Mishra, Mitawa, Dubey и др. **Sutaria нет** |
| WhatsApp, контакты | «No contacts found matching Sutaria» |
| **Живой Telegram MCP** | ⚠️ **не могу судить** — две попытки, обе молчали по 300 секунд и были прибиты. Рельса мёртвая, это не ответ «нет» |
| Gmail | не проверял |

**Покрытие: 3 рельсы из 5.** Архив личек — снимок, не живая телега, так что он говорит про «до последнего синка», а не про прямо сейчас. Но вместе с вчерашней записью Codex («контакт или сообщение ему пока не отправлялись») картина однозначная: канал холодный, переписки нет, карточки до сегодняшнего дня тоже не было — я её завёл.

Значит **первое касание ещё не сделано**, и оно твоё, свежее, со вчерашней встречи.

---

# 📨 Черновик письма Gaurav

Пишу от первого лица, **без Майкрофта** — по карв-ауту 14.09 всё, что касается трудоустройства, идёт твоим голосом. Слов «founder» и «не-кодер» про тебя нет.

**Не отправляю.** Это выходит за рамки того, о чём ты просил («изучи программу»), и вчерашняя сессия отдельно поставила гейт на исходящее по этой линии. Жду твоё «+».

Канал: туда, где вы обменялись контактами. Если не обменивались — скажи, найду вторую дверь.

---

> Gaurav — great meeting you yesterday at the house. Loved what you said about Techify moving from a dev shop to an AI transformation practice; that transition is the hard part and most shops stall halfway through it.
>
> One concrete ask, and I'll keep it short because I know how the week goes.
>
> I'm going after **Applied AI Architect, Partnerships** at Anthropic. If you know the hiring manager or anyone on that team through your Anthropic account contact, a one-line intro from you would carry further than my application sitting in a queue.
>
> What I'd bring, in one sentence: **[КЕЙС — одно предложение, см. ниже]**
>
> Happy to send a short write-up you can forward as-is, so it costs you nothing but a paste.
>
> And separately — curious where Techify sits in the Partner Network right now, and whether you're nominating engineers into Frontier Academy. If that's something you're building out, there may be a way for us to be useful to each other beyond this intro.
>
> dev
> github.com/tonydzi

---

## Какой кейс вставляем — решай ты, цифры я не выдумываю

Два варианта, оба правдивые:

**А. Оркестрация.** «Я держу в проде парк из восьми машин с мульти-агентными Claude Code сессиями — своя шина между узлами, реестр рутин, гейты качества на исходящее — и это работает без меня в ночную смену.» Сильно тем, что это ровно та боль, которую Applied AI решает у enterprise-клиентов.

**Б. Аудит.** Твоя zero-trust линия и agent-leash. Сильно тем, что это продукт, а не описание инфраструктуры, и его можно показать.

Моя рекомендация — **А**, потому что роль называется Architect, Partnerships: им нужен человек, который разворачивает чужие внедрения, а не продаёт свой продукт. Но если у Б есть живой внешний пользователь — Б бьёт А, потому что это чужой клиент, а не свой стенд.

Скажи букву, или скажи «выбери сам» — выберу и вставлю.

---

## 🚦 Где мы по всей задаче

| Ход | Статус |
|---|---|
| Разобрать программу | ✅ сделано, первоисточники, три независимых вердикта сошлись |
| Founder House, день 3 — завтра 8 окт | ⏳ **ждёт твоего ответа: ты в SF?** |
| Письмо Gaurav | ⏳ черновик выше, ждёт «+» и выбора кейса |
| Claude for Startups | ⏳ готов подавать, можно прямо на площадке |
| Плагин в каталог Claude | ⏳ дверь открыта, партнёрство не нужно |
| 313 партнёров в воронку вакансий | ⏳ запущу, как скажешь |
| Волт | ✅ разбор + карточка Gaurav + CSV на 313 строк |

Наружу по-прежнему ушло ноль сообщений.

---

## 🧒 Простыми словами

Проверил три места: твои рабочие записи, архив всех личных переписок в телеге (двадцать две тысячи диалогов) и контакты ватсапа. Гаурава Сутарии нет нигде — вы вчера познакомились, и с тех пор ему никто ничего не писал. Четвёртое место, живую телегу, проверить не смог: она два раза молчала по пять минут и отвалилась. Так что честно: три двери из пяти.

Написал за тебя короткое письмо. Главное в нём — не «расскажи мне про программу», а «познакомь меня с человеком, который нанимает». И приписка, чтобы ему было легко: «пришлю готовый текст, тебе останется только переслать».

Письмо не отправил. Ты просил изучить программу, а не писать людям. Жмёшь плюс — отправляю.

**Нужны от тебя три слова:** ты в SF? буква кейса (А или Б)? плюс на отправку?

[⏰ 2026-10-07 12:30 Лиссабон / 04:30 PDT]
