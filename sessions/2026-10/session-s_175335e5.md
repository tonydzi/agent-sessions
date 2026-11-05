---
session: s_175335e5
date: 2026-10-06
words: 3805
turns: 17
tools: "Bash, Grep, Read, ToolSearch, WebFetch, WebSearch, Write"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-06 · Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_175335e5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Это задача от оператора. Она пришла голосом в Telegram-группу «001 СЕССИЯ НОВАЯ»,
расшифрована ботом. Источник: tg:chat_REDACTED:7751.

ДОСЛОВНО, ЧТО СКАЗАЛ оператор:
---
Дальше. У меня есть на Facebook несколько людей, типа оператора Сабуров, кажется. Он постоянно говорит, что типа я, он репрезентатив chatGPT, что-то он занимается chatGPT интеграцией, chatGPT продажами и так далее, кодекс продаж. Смотри, у нас есть крупная лаборатория и у них наверняка есть интеграторы. То есть крупная я и лаборатория наверняка имеют интеграторы, большие или маленькие. Ну так же как, допустим, есть Intel или какой-нибудь крупный производитель, какой-нибудь софт или железо, у них есть свои интеграторы. И большие или маленькие. Вопрос такой, как стать таким интегратором? Сколько таких интеграторов существует? Можно ли к ним отправиться на работу? Либо может ли иметь смысл создать собственные интеграторы? Сколько они зарабатывают, крупные и маленькие? В США и в Европе. То есть здесь нужно провести хорошее, глубокое исследование. И тебе, как фаундеру, посоветуют мне, насколько это легко, насколько это фаундабл, то есть насколько я могу поднять деньги, или насколько я могу быть break-even, то есть достаточно прибыльным, чтобы заниматься этим и поддерживать свою жизнь.
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

Принял задачу: исследование «интеграторы ИИ-лабораторий» (как стать, сколько их, зарплаты/выручка US+EU, нанимают ли, стоит ли строить свой) + мой кофаундерский вердикт по foundability. Первым ходом — RECALL по памяти и волту, потом веер исследования.

---

> `Bash` -- {"command": "python \"D:\\Vault\\_imports\\brain_ask.py\" \"интеграторы OpenAI Anthropic AI консалтинг агентство внедрение LLM как бизнес стать партнёром\" 2>&1 | head -60", "description": "RECALL через brain_ask по теме интеграторов", "timeout": 180000}

---

> `Grep` -- {"pattern": "интегратор|integrator|solutions partner|GenAI consult", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\memory", "-i": true, "output_mode": "files_with_matches"}

---

> `Bash` -- {"command": "ls \"D:\\Vault\\_imports\\.brain-venv\\Scripts\\python.exe\" 2>/dev/null && \"D:\\Vault\\_imports\\.brain-venv\\Scripts\\python.exe\" \"D:\\Vault\\_imports\\brain_ask.py\" \"интеграторы OpenAI Anthropic консалтинг внедрение AI агентство партнёрская программа\" 2>&1 | head -50",

---

> `Bash` -- {"command": "ls \"D:\\Vault\\_imports\\\" 2>/dev/null | grep -i venv; ls \"D:\\Vault\\_imports\\.brain-venv\" 2>/dev/null | head", "description": "Найти brain venv"}

---

> `Bash` -- {"command": "ls -a /e/Obsidian/_imports/ | grep -i venv", "description": "Найти venv в _imports"}

---

> `Bash` -- {"command": "ls /e/Obsidian/_imports/.venv-diar/Scripts/python.exe 2>/dev/null; ls -a /e/Obsidian/ | grep -i -E 'venv|brain' | head", "description": "Поиск brain-venv"}

---

> `Bash` -- {"command": "/e/Obsidian/_imports/.venv-diar/Scripts/python.exe /e/Obsidian/_imports/brain_ask.py \"интеграторы OpenAI Anthropic консалтинг внедрение AI агентство партнёрская программа услуги\" 2>&1 | head -60", "description": "brain_ask через .venv-diar", "timeout": 240000}

---

> `Grep` -- {"pattern": "интегратор|systems integrator|AI agency|внедрени.{0,20}(LLM|ChatGPT|GPT|Claude)", "path": "D:\\Vault\\Vault-Knowledge", "-i": true, "output_mode": "files_with_matches", "head_limit": 20}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\02-Decisions\\_Inbox\\2026-10-03--chatgpt-integratory-rynok-zarabotok-puti-vhoda-ssha-evropa.md"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_session-md\\PaloAlto-Desktop\\s_175335e5.md", "limit": 100}

---

> `Grep` -- {"pattern": "интегратор|integrator", "path": "D:\\Vault\\Vault-Knowledge\\_DR-Registry.md", "-i": true, "output_mode": "content", "-n": true}

---

> `Bash` -- {"command": "sed -n '70p;201p' /e/Obsidian/Vault-Knowledge/_DR-Registry.md | cut -c1-400", "description": "Прочитать строки реестра ДР"}

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `WebSearch` -- {"query": "OpenAI services partner program solutions partner become certified integrator 2026"}

---

> `WebSearch` -- {"query": "Anthropic Claude partner program systems integrators consulting partners list"}

---

> `WebSearch` -- {"query": "AI implementation agency revenue 2026 boutique AI consulting firm how much earn profit margin"}

---

> `WebSearch` -- {"query": "forward deployed engineer AI solutions architect salary 2026 OpenAI Anthropic partner consultancy"}

---

> `WebSearch` -- {"query": "how many AI agencies consultancies exist 2026 number \"AI consulting\" market size Europe US GenAI services"}

---

> `WebSearch` -- {"query": "AI consulting startup raised funding 2025 2026 Distyl Tribe AI services venture capital fundable agency"}

---

> `WebSearch` -- {"query": "Accenture generative AI bookings 2026 billion GenAI revenue systems integrators Deloitte"}

---

> `WebFetch` -- {"url": "https://aventis-advisors.com/the-claude-partner-network-explained/", "prompt": "How many partners are in the Claude Partner Network? What tiers exist, who are key players, what M&A activity is happening around AI integrators, any revenue/valuation numbers for AI consultancies?"}

---

> `WebSearch` -- {"query": "\"AI automation agency\" solo founder income reality 2026 n8n agency clients break even"}

---

> `WebSearch` -- {"query": "OpenAI partner network requirements join criteria certification cost small firms boutique Europe"}

---

**Claude:**

Последний добор — европейские зарплаты у интеграторов:

---

> `WebSearch` -- {"query": "AI engineer GenAI consultant salary Europe 2026 London Berlin Paris Accenture Capgemini LLM engineer"}

---

> `Write` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\02-Decisions\\_Inbox\\2026-10-04--ii-laboratorii-integratory-rynok-i-verdikt-kofaundera.md", "content": "---\ntitle: \"Интеграторы ИИ-лабораторий: рынок, деньги, пути входа, вердикт кофаундера\"\ntype: decision\nstage: researched\ntags: [decision, integr

---

> `Bash` -- {"command": "date \"+%H:%M %d.%m.%Y\"", "description": "Текущее время для штампа"}

---

**Claude:**

14:06, 4 октября 2026.

Исследование по интеграторам ИИ-лабораторий готово. Первой строкой честно: прошлый заход этой сессии 03.10 умер на weekly-лимите, выдав ноль, а вчерашний авто-дистиллят в волте пересказал пустую сессию выдуманными цифрами. Сегодня всё собрано заново по живым источникам.

---

## 1. Главная новость: дверь открылась ТРИ МЕСЯЦА НАЗАД

Ты угадал точно: у лабораторий есть интеграторы, и обе крупнейшие оформили это в официальные программы буквально в июне 2026.

**OpenAI Partner Network** (анонс 14 июня 2026): $150M инвестиций в экосистему, цель 300 000 сертифицированных консультантов до конца 2026. Три тира: Select, Advanced, Elite. Критерии: продажи, техническая способность, co-sell, опыт деплоев. Заявка через [openai.com/form/partner-network-interest](https://openai.com/form/partner-network-interest/), официальная страница [openai.com/business/partners](https://openai.com/business/partners/). Взнос не опубликован, критерии сертификации ещё дораскрываются.

**Claude Partner Network** (Anthropic, июнь 2026): программа на $100M, три трека: Consulting (интеграторы), Technology (ISV), Services (MSP, тренинг, стаффинг). Тиры с конкретными порогами:
- **Select**: 10+ сертифицированных людей, 2+ клиента в проде, 1 публичный кейс
- **Preferred**: 100+ людей, 15+ клиентов, 3 кейса
- **Global Premier**: 1000+ людей, 100+ клиентов в 3+ регионах, 15 кейсов

Каталог живьём: [partnerhub.claude.com/directory](https://partnerhub.claude.com/directory/) и [claude.com/marketplace/service-partners](https://claude.com/marketplace/service-partners).

## 2. Сколько их существует

Формально сертифицированных пока МАЛО: у Anthropic в каталоге был ~41 сервис-партнёр на июль 2026 ([разбор Aventis Advisors](https://aventis-advisors.com/the-claude-partner-network-explained/)). Шесть групп игроков: Big Four (Deloitte, PwC, KPMG, BCG), глобальные SI (Accenture, TCS, Infosys, Cognizant, EPAM, DXC, Globant), гос-подрядчики (Booz Allen, Leidos), облачные специалисты (Caylent, Bounteous), AI-native бутики (Distyl, Tribe AI, Bold Tech, Ciridae) и вертикальщики (Quantium, OWT, Zartis).

Несертифицированных AI-агентств в мире тысячи, точного счёта нет ни у кого. Рынок AI-консалтинга 2026: оценки $9-14B глобально, США ~$11.3B, Европа ~$8.9B, обе географии идут к $22-29B к 2033 ([Fortune Business Insights](https://www.fortunebusinessinsights.com/ai-consulting-services-market-111179), [Business Research Insights](https://www.businessresearchinsights.com/market-reports/ai-consulting-services-market-119843)).

## 3. Сколько они зарабатывают

**Гиганты.** Accenture: advanced AI bookings $2.2B за ОДИН квартал (Q1 FY2026, рост 76% г/г), $5.9B GenAI-заказов за FY2025, суммарно $11.5B по 11 000 проектов ([FourWeekMBA](https://fourweekmba.com/ai-accenture-genai-bookings-2-billion-quarter-2026/), [CIO Dive](https://www.ciodive.com/news/accenture-generative-ai-revenue-skills-training-data-modernization/761161/)). GenAI уже в 80% их крупных сделок.

**Бутики.** Часовые ставки $200-400. Strategy-roadmap проект: $50-250K. Продакшн-деплой одного юзкейса в mid-market: $250K-1.5M. Валовая маржа лучших фирм 50-70%, здоровая чистая 20%+ ([aidolsgroup](https://aidolsgroup.com/en/blog/category/industry-insights/state-of-ai-consulting-2026/), [financialmodelslab](https://financialmodelslab.com/blogs/profitability/artificial-intelligence-consulting)).

**Соло/микро.** Старт $5-25K вложений. Медиана соло-оператора в нише: ~$12.5K MRR к 8-му месяцу, топ-квартиль $22K+. Реалистичная траектория: $10K MRR к 3-му месяцу, $25K к 6-му, $50K+ к 12-му. Потолок одного человека: $50-150K MRR, дальше нужна команда. Маржа на малом масштабе 85% ([ideaproof playbook](https://ideaproof.io/guides/ai-automation-agency), [Medium: How AI Agencies Make Money 2026](https://medium.com/the-ai-studio/how-ai-agencies-are-really-making-money-in-2026-6ab696804300)).

## 4. Можно ли к ним на работу: да, и это горячая роль

Ключевая позиция называется **Forward Deployed Engineer** (FDE), её придумал Palantir, теперь она везде.

**США:** mid $260-330K TC, senior $340-480K, staff $520-780K. У frontier-лабов (OpenAI, Anthropic, Palantir) опытный FDE: $350-750K. FDE-комп на ~60% выше классического solutions engineering ([Perspective FDE Compensation Report](https://getperspective.ai/blog/2026-forward-deployed-engineering-compensation-report-1200-fdes), [Paraform](https://www.paraform.com/insights/openai-forward-deployed-engineer)).

**Европа:** Лондон £90-170K (GenAI-инженер), Берлин €80-150K, Париж €50-126K. LLM-премия к обычному SWE: +35-50%. НО: у классических GSI в дешёвых локациях сильно скромнее, Accenture в Риге платит LLM-инженеру €31-60K/год ([zenvanriel](https://zenvanriel.com/job/ai-engineer-salary-europe/), [digitaldefynd](https://digitaldefynd.com/IQ/ai-salaries-in-europe/)).

Для твоей Mission-2 это двойная дверь: FDE у интегратора-партнёра = трамплин в лабораторию, и FDE-роль прямо в лабораториях есть (у OpenAI это одна из самых нанимаемых позиций 2026).

## 5. Стоит ли строить свой: foundability

Классический ответ VC «сервисы не фандабельны» в 2025-2026 сломан одним кейсом:

**Distyl AI**: основана 2022 двумя экс-палантирцами, делает ИИ-внедрения для Fortune 500. Seed $7M (2023), Series A $20M (2024), **Series B $175M при оценке $1.8B** (сентябрь 2025, Khosla + Lightspeed + Coatue + DST), ARR ~$31M, рост 5x за 2024 ([SiliconANGLE](https://siliconangle.com/2025/09/22/enterprise-ai-consultancy-distyl-ais-valuation-soars-1-8b-bumper-funding-round/), [Getlatka](https://getlatka.com/companies/distyl.ai)).

Формула, за которую платят VC: сервис + СВОЯ платформа внутри (у Distyl это Distillery) + логотипы Fortune 500. Чистый бодишоп «посадим людей на проект» не поднимет никогда. И вторая дверь выхода уже работает: M&A началась, Ode купила Casper Studios (40 человек, Select-партнёр Anthropic, основана 2022) в августе 2026.

## 🎙 Майк: вердикт кофаундера

**Идём верно, но угол важнее темы.** Про «оператора Сабурова с ChatGPT-продажами»: то, что кто-то это делает, по твоему же правилу от 30.09 значит «рынок есть, делаем тоже». Вот моя раскладка по трём твоим вопросам:

**Break-even: ДА, легко.** Соло-интегратор с нашим стеком (флот, second brain, 69 репо, живые кейсы) выходит на $10-20K MRR за 6-12 месяцев. Это самый низкорисковый путь из трёх: маржа 85%, вложения нулевые, мы уже умеем всё, что продают бутики за $200-400/час.

**Рейз: ДА, но только по формуле Distyl.** Не «агентство», а «consulting-led product»: сервис как канал, своя платформа как актив. У нас платформа уже есть: оркестрация флота, second brain, agent-leash. Без продуктовой обёртки не фандабельно, с ней прецедент $1.8B существует.

**Для Mission-2 это, возможно, самый недооценённый ход:** Select-tier у Anthropic (10 сертифицированных, 2 клиента, 1 кейс) достижим микрокомандой, а партнёрский бейдж = легальный вход в экосистему лаборатории БЕЗ прохождения найма. Направляющий вопрос один: что первично, бейдж партнёра Anthropic как усилитель Mission-2, или интегратор как бизнес ради денег? Это разные дорожные карты, и я бы начал с первого: заявку в Claude Partner Network можно подать уже сейчас, это обратимо и бесплатно.

---

**Хвосты и честность:**
- Волт: заметка [2026-10-04--ii-laboratorii-integratory-rynok-i-verdikt-kofaundera.md](D:\Vault\Vault-Knowledge\02-Decisions\_Inbox\2026-10-04--ii-laboratorii-integratory-rynok-i-verdikt-kofaundera.md), она закрывает вчерашний авто-дистиллят с непроверенными цифрами.
- Дашборд не строю, причина: результат = текстовое решение с вердиктом, а не поток данных для глаз; таблица из 20 строк решения не добавит.
- Рельсы (§6.3-бис ретро-строка): обещал инхаус, сделал инхаус (WebSearch), чужие LLM-рельсы не жёг, причина: rail-dead, прошлый заход сессии сгорел на лимите, оператор ждал содержание. Добор глубины: если хочешь полный ДР-веер (точные количества партнёров по тирам, юнит-экономика 10 конкретных бутиков, европейская специфика по странам), скажи «ДР» и я зарегистрирую номер и разнесу промпт по рельсам.
- Проверено: партнёрки, тиры, цифры Accenture/Distyl, зарплаты (2+ источника на каждый блок). НЕ проверено: точное число партнёров OpenAI (программа запущена в июле, каталог ещё не публичен), вступительные взносы (не опубликованы).

🧒 Простыми словами: представь, что OpenAI и Anthropic это заводы, которые делают мощные моторы. Заводы сами машины не собирают, им нужны мастерские, которые ставят моторы клиентам. Этим летом оба завода открыли официальные клубы таких мастерских, и в клуб Anthropic пока вступил всего 41 человек, то есть очередь короткая. Платят в мастерских очень хорошо (инженеру в США до полумиллиона в год), свою мастерскую открыть дёшево и она быстро кормит, а одна такая мастерская (Distyl) даже стала стоить почти два миллиарда. Мой совет: сначала получить значок «официальная мастерская Anthropic», это бесплатно и сразу двигает твою главную цель, попасть внутрь лаборатории.

14:09, 4 октября 2026.

---

**User:**

я тоже хочу стать интегратором!!! как???

---

**Claude:**

14:12, 4 октября 2026.

Разберём ровно это: что надо сделать руками, в каком порядке, с чего начинается первый день. Сперва проверю реальные требования на входе и чем мы уже владеем.

---

> `WebFetch` -- {"url": "https://openai.com/form/partner-network-interest/", "prompt": "What exactly does this partner interest form ask for? List every field and requirement (company size, legal entity, revenue, region, expertise areas, references). Any eligibility criteria stated?"}

---

> `WebFetch` -- {"url": "https://claude.com/marketplace/service-partners", "prompt": "List the service partners shown, their tiers, and any link or instructions for how a new firm applies to become a Claude service partner. What are the stated requirements for the Select tier?"}

---

**Claude:**

Поправка к вчерашней цифре сразу, живой каталог говорит другое: Select-партнёров **256**, Preferred **40**, Global Premier **6**. Смотрю саму форму заявки.

---

> `WebFetch` -- {"url": "https://claude.com/form/cpn-partner-application", "prompt": "List every field this partner application form asks for, verbatim if possible: company details, legal entity, headcount, revenue, regions, track selection, certifications, customer references, case studies. Any minimum eligibility

---

> `WebFetch` -- {"url": "https://partnerhub.claude.com/directory/", "prompt": "How many partners are listed, what filters exist, and what does a partner profile contain? Is there a visible application or certification path described, and what certifications are named (e.g. Claude Builder, Claude certified)?"}

---

**Claude:**

Ключевое найдено: **порог входа Anthropic — зарегистрированный бизнес с 10+ сотрудниками.** Это блокер для соло. Проверяю, что требует OpenAI и какие двери есть в обход порога.

---

> `WebSearch` -- {"query": "OpenAI Partner Network eligibility requirements minimum employees registered business apply small consultancy"}

---

> `WebSearch` -- {"query": "Anthropic Claude certification program individual \"Claude certified\" builder exam consultant credential 2026"}

---

**Claude:**

Теперь картина точная. Проверю, что у нас уже есть на руках под эти требования.

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && grep -ril -E 'юрлиц|LLC|Ltd|sp\\. z o\\.o|компани[яю] оператора|incorporat|registered business|НКО|ИП' . 2>/dev/null | grep -v '\\.bak' | head -20", "description": "RECALL: есть ли у оператора юрлицо"}

---

> `Bash` -- {"command": "cd /c/Users/dev/.claude/projects/P---WORKDIR-HUB/memory && cat two-storefronts-raise-and-acquihire.md zero-trust-product-line.md track-a-team-hire.md 2>/dev/null | head -80", "description": "Читаю витрины и продуктовую линию"}

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge && grep -ril -E 'Unipessoal|Lda\\b|NIF|sp\\. z o\\.o|LLC|Delaware|регистрац.{0,25}(компан|фирм|бизнес)|открыть юрлицо' 05-Resources 02-Decisions 04-Projects 2>/dev/null | head -15", "description": "Поиск юрлица оператора в волте"}

---

> `WebSearch` -- {"query": "\"OpenAI Certified Associate\" exam cost how to take certification individual 2026 academy"}

---

> `WebSearch` -- {"query": "Claude Partner Network supported regions list Portugal Poland Europe eligibility \"supported region\""}

---

**Claude:**

Все пороги нашёл. Соберу ещё список партнёров, к которым реально идти субподрядом.

---

> `WebFetch` -- {"url": "https://claude.com/marketplace/service-partners", "prompt": "List as many Select-tier partner names as are visible on the page, especially any based in or serving Southern Europe, Portugal, Spain, Poland, or Eastern Europe. Also list any partners described as small (under 100 employees) or 

---

> `WebSearch` -- {"query": "Claude Partner Network technology partner track ISV requirements build on Claude product no employee minimum"}

---

**Claude:**

Нашёл главное: **Technology Partner трек не имеет порога по сотрудникам.** Проверю официальный источник.

---

> `WebFetch` -- {"url": "https://www.anthropic.com/news/services-track-partner-hub", "prompt": "What tracks exist in the Claude Partner Network, and what are the stated requirements for each (Services/Consulting vs Technology)? What exactly must a Technology Partner have? Any employee minimums, fees, or marketplace

---

> `WebFetch` -- {"url": "https://claudeimplementation.com/blog/join-claude-partner-network", "prompt": "What are the eligibility requirements, application steps, certification path and learning path for joining the Claude Partner Network? Specifically: minimum employees, fees, which track a small firm or solo found

---

**Claude:**

Хватит исследований, план ясен. Обновляю заметку и выкладываю.

---

> `Bash` -- {"command": "cd /e/Obsidian/Vault-Knowledge/02-Decisions/_Inbox && python - <<'PY'\nimport io\np = \"2026-10-04--ii-laboratorii-integratory-rynok-i-verdikt-kofaundera.md\"\ntxt = io.open(p, encoding=\"utf-8\").read()\nadd = \"\"\"\n## ⭐ ДОБОР 04.10 14:20 — ПОРОГИ ВХОДА (оператор: «я тоже хочу стать инт

---

**Claude:**

14:21, 4 октября 2026.

Отвечаю прямо: **стать интегратором можно, но прямая дверь Anthropic для тебя сейчас закрыта, и честно сказать это важнее, чем продать тебе красивый план.** Вот вся правда с порогами и обход.

## Жёсткий факт первым

Форма заявки Anthropic ([claude.com/form/cpn-partner-application](https://claude.com/form/cpn-partner-application)) требует дословно три вещи:

1. **Be a registered business with 10 or more employees**
2. Operate in a supported region
3. Offer consulting, implementation, or managed services

Официальный анонс Anthropic подтверждает: вход на уровне Registered даётся «с минимальным коммитментом на 10 сертифицированных практиков» ([anthropic.com/news/services-track-partner-hub](https://www.anthropic.com/news/services-track-partner-hub)). Select-тир сверху: 10 активных сертифицированных + 2 клиента в проде за 12 месяцев + 1 публичный кейс.

И вторая ловушка: **сертификацию Claude индивидуально сдать нельзя.** Четыре экзамена через Pearson VUE (Associate $99, Developer $125, Architect Foundations $125, Architect Professional $175, проходной 720/1000, 120 минут, годность 12 месяцев), но все требуют партнёрского email организации, уже состоящей в сети ([FAQ Anthropic Partners](https://anthropic-partners.skilljar.com/page/faq-certifications), [DevCompass](https://www.devcompass.ai/blog/claude-certifications-guide-2026)). Курица-яйцо: сертификат нужен для партнёрства, партнёрство нужно для сертификата.

Ещё поправка к вчерашнему: партнёров **313**, а не 41. Global Premier 6, Preferred 40, **Select 256**. Вчерашняя цифра была из июльского вторичного разбора, живой каталог показывает втрое больше. Очередь не такая короткая, как я сказал утром.

Португалия и Польша в supported regions, географического блока нет.

## Пять дверей и их реальные пороги

| № | Дверь | Порог | Деньги | Открыта сейчас |
|---|---|---|---|---|
| 1 | **Anthropic Services/Consulting** (Registered → Select) | registered business, 10+ сотрудников; Select = 10 сертифицированных + 2 клиента в проде + 1 публичный кейс | бесплатно, взноса нет | ❌ блок по людям |
| 2 | **Anthropic Technology Partner** (ISV-трек) | живая продуктовая интеграция на Claude API + листинг в маркетплейсе, **минимума по людям нет** | не опубликовано | ⚠️ вероятно да |
| 3 | **OpenAI Registered tier** | онбординг-ассессмент + Partner Program Agreement + 1 OpenAI Certified Associate + 1 продакшн-деплой на OpenAI API за 12 мес | **$2 500/год**, waived при ARR < $5M | ⚠️ блок по сертификации |
| 4 | **Субподряд у Select-партнёра** | порога нет вообще | 0 | ✅ сегодня |
| 5 | **FDE/Solutions-роль** у партнёра или лаборатории | обычный найм | 0 | ✅ сегодня |

По двери №3: порог деньгами смешной, но «designated OpenAI Certified Associate» упирается в то же самое. Проктируемая сертификация OpenAI пока invite-only через пилоты работодателей (Walmart, BCG, Accenture, John Deere), публичной даты открытия нет, реалистично конец 2026 или 2027. Бесплатные курсы OpenAI Academy с бейджами открыты всем с 21.09.2026, **но Academy-бейдж официально не является OpenAI Certification** ([findskill](https://findskill.ai/blog/openai-certification-guide/), [ctaio](https://ctaio.dev/en/ai-certifications/openai-certification/)).

## Дверь №2 — твой реальный вход, и он открыт

Technology Partner трек (ISV, а не консалтинг) измеряет **не людей, а то, что ты построил**: живая интеграция на Claude API плюс опубликованный листинг. Цитата из разбора трека: каждая фирма мерится одинаково, «ten-person AI-native shop or a global consultancy» ([Enterprise DNA](https://enterprisedna.co/resources/news/anthropic-claude-partner-network-services-track-june-2026/), [kanerika](https://kanerika.com/blogs/claude-partner-network/)).

У тебя под этот порог уже лежит готовое: agent-leash (публичный репо, аудит агентов и MCP), оркестрация флота на Claude API, second brain с RAG. Это не «надо построить», это «надо упаковать и залистить».

⚠️ Честная оговорка: отсутствие минимума по людям в ISV-треке я подтвердил двумя **вторичными** источниками, официальная страница анонса расписывает только Services-трек и отсылает на claude.com/partners. Это гипотеза с хорошими шансами, а не доказанный факт. Проверяется одним письмом в partner-команду.

## План 7 / 30 / 90

**Неделя 1 (деньги и доступ, без порогов):**
- Шорт-лист из 256 Select-партнёров: кто работает по Южной Европе и Польше, кто мелкий (под 100 человек), кому нужны руки на деплои. Письмо о субподряде: ты приходишь не «дайте работу», а «у меня готовый аудит агентов и MCP, который ваши клиенты просят, а у вас этой компетенции в каталоге нет».
- Форма интереса OpenAI ([openai.com/form/partner-network-interest](https://openai.com/form/partner-network-interest/)) — бесплатна, ни к чему не обязывает, ставит тебя в очередь на открытие сертификации.
- Письмо в partner-команду Anthropic с прямым вопросом: считаются ли контракторы в «10 or more employees» и каковы требования ISV-трека.

**Месяц 1 (дверь №2):**
- Листинг продукта на Claude API в маркетплейсе, заявка в Technology-трек.
- Первый публичный customer story — нужен хотя бы один клиент с деплоем в проде. По правилу от 05.07 флор снят: чек $100-500 от осознанного первого клиента уже считается.

**Месяц 3 (дверь №1):**
- К моменту, когда наберётся 10 сертифицированных людей (команда + контракторы), заявка в Services-трек на Select. Два клиента в проде и публичный кейс к этому времени уже будут от шага выше.

## Что я делаю сам, что нужно от тебя

Сам, без спроса, в следующем заходе: собираю шорт-лист партнёров с контактами, пишу черновик письма о субподряде, черновик анкеты OpenAI, черновик вопроса в partner-команду Anthropic, завожу карточки в CRM.

Нужен твой «+» на: отправку анкет и писем. Причина не формальная: Partner Program Agreement это юридическое соглашение, а у OpenAI ещё и $2 500/год, то есть Tier-2 по двум признакам сразу. Подготовлю всё до кнопки.

**Один вопрос, который реально меняет первые шаги:** есть ли у тебя действующее юрлицо и где — Португалия, Польша, US? В памяти и волте следа нет, а обе партнёрки требуют registered business. Без юрлица живы двери №4 и №5, и начинать надо с них. Пока ответа нет, работаю по этому варианту, он всё равно первый в плане.

## 🎙 Майк

Идём верно, но ты рискуешь купить не тот билет. Бейдж «интегратор» сам по себе денег не приносит, приносит клиент. У тебя порядок должен быть обратный тому, как это звучит в голове: сначала один живой деплой у живого клиента, потом бейдж как усилитель, а не бейдж как вход.

Моё возражение против лобового пути: гнаться за Select-тиром Anthropic сейчас значит гнаться за цифрой «10 сотрудников», то есть нанимать людей под сертификацию, не имея выручки. Это шиворот-навыворот и сжигает деньги. Субподряд у одного из 256 действующих партнёров даёт тебе и клиентский деплой, и доступ к их сертификации, и чек, причём сразу и бесплатно.

Переубеди меня, если видишь иначе: единственный аргумент за лобовой путь, который я принимаю, это если бейдж нужен тебе не для денег, а для Mission-2 как строка в резюме при разговоре с лабораторией. Тогда это другая задача и другая экономика, скажи прямо и я перестрою план под неё.

---

Волт: заметка обновлена разделом «ДОБОР 04.10 14:20 — пороги входа» — [2026-10-04--ii-laboratorii-integratory-rynok-i-verdikt-kofaundera.md](D:\Vault\Vault-Knowledge\02-Decisions\_Inbox\2026-10-04--ii-laboratorii-integratory-rynok-i-verdikt-kofaundera.md).

Проверено: пороги Anthropic (первоисточник + форма заявки), число партнёров по тирам (живой каталог), цены и гейт сертификации (два источника), порог OpenAI Registered. НЕ проверено: отсутствие минимума людей в ISV-треке (только вторичные источники), наличие юрлица у тебя, считаются ли контракторы сотрудниками.

🧒 Простыми словами: у Anthropic на входе написано «только фирмы от 10 человек», а экзамен можно сдать только если ты уже внутри — замкнутый круг. Но есть три лазейки. Первая и лучшая: пойти подрядчиком к одной из 256 фирм, которые уже внутри — им нужны руки, порога нет, платят сразу. Вторая: у них есть отдельная дверь «для тех, кто сделал продукт», а не «для тех, кто много людей» — и твой agent-leash как раз продукт. Третья: пойти туда работать инженером. Мой совет: сначала один настоящий клиент, потом значок. Значок без клиента это просто картинка.

И один вопрос: у тебя есть зарегистрированная фирма, и если да, то в какой стране?

14:24, 4 октября 2026.
