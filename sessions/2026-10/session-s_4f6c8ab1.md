---
session: s_4f6c8ab1
date: 2026-10-16
words: 2670
turns: 5
tools: "Bash, Grep, Read, ToolSearch, WebSearch, mcp__be573d85-3efd-4883-8eee-7095a4943f74__create_event, mcp__be573d85-3efd-4883-8eee-7095a4943f74__list_calendars, mcp__be573d85-3efd-4883-8eee-7095a4943f74__list_events"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-16 · Нужно посмотреть конференции по искусственному интеллекту в Европе / Лондоне на период: ко…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4f6c8ab1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Нужно посмотреть конференции по искусственному интеллекту в Европе / Лондоне на период: конец октября, весь ноябрь и декабрь. Дополнительно можно включить Дубай.

Ранее уже исследовали конференции в Америке, сейчас интересны именно европейские AI-конференции: что будет интересного в Европе в этот период.
__Перевела: GPT-5.5 + 11labs__

• • • • •

⚠️ версия whisper не пришла.
(ВОСКРЕШЕНИЕ ПОСЛЕ ЛИМИТА: дверь Claude не подняла эту голосовую вовремя -- дверь Claude: NO-WINDOW; Codex сделал только разбор)

---

**Claude:**

Начинаю с RECALL: смотрю, что у нас уже есть по конференциям, в том числе американский ресёрч, и подгружаю веб-поиск.

---

> `ToolSearch` -- {"query": "select:WebSearch,WebFetch", "max_results": 2}

---

> `Bash` -- {"command": "cd \"E:/!CLAUDE-HUBPC-June26\" && ls docs | grep -i -E \"conf|summit|event\" | head -30; python \"D:/Vault/_imports/brain_ask.py\" \"AI конференции Европа Лондон Дубай ноябрь декабрь 2026\" 2>&1 | head -60", "description": "Recall existing conference research", "timeout": 90000}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-10-01-HUB-01-1434/results\" && ls -la && wc -c *.md && cat grok.md | head -150", "description": "Read prior DR conference results"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge\" && grep -rl -i \"AI-инженерные митапы и якоря\" --include=*.md . 2>/dev/null | head; ls \"C:/Users/dev/.claude/projects/P---WORKDIR-HUB/\" | grep 61c87020", "description": "Find the Europe meetups note"}

---

> `Bash` -- {"command": "cd \"D:/Vault/Vault-Knowledge/_session-md/PaloAlto-Desktop\" && grep -n \"Европа: AI-инженерные\" s_3ddff24a.md | head -3; wc -c s_3ddff24a.md", "description": "Locate Europe note in session md"}

---

> `Grep` -- {"pattern": "Европ|Europe|London|Лондон|Dubai|Дубай|Lisbon|Web Summit|NeurIPS", "path": "C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_4f6c8ab1\\tool-results\\bzue8s616.txt", "output_mode": "content", "-n": true, "head_limit": 80}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_session-md\\PaloAlto-Desktop\\s_3ddff24a.md", "offset": 480, "limit": 120}

---

> `Grep` -- {"pattern": "Slush|AI Summit|Dubai|Дубай|GITEX|Lisbon|Web Summit|KubeCon|NeurIPS|EMNLP|AI Engineer Paris|RAISE|MCP|AI Summit London|Ai4|Generative AI|Paris", "path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-10-01-HUB-01-1434\\results\\grok.md", "output_mode": "content", "-n": t

---

> `WebSearch` -- {"query": "NeurIPS 2026 Paris satellite December 2026 dates venue", "mode": "standard"}

---

> `WebSearch` -- {"query": "AI conferences London November 2026", "mode": "standard"}

---

> `WebSearch` -- {"query": "Dubai AI conference December 2026 GITEX Global Dubai AI Week dates", "mode": "standard"}

---

> `WebSearch` -- {"query": "EMNLP 2026 dates location", "mode": "standard"}

---

> `WebSearch` -- {"query": "Europe AI conference November 2026 Paris Berlin Amsterdam Lisbon agents LLM developers", "mode": "standard"}

---

> `WebSearch` -- {"query": "Dubai AI Festival 26-27 October 2026 Dubai World Trade Centre", "mode": "standard"}

---

> `WebSearch` -- {"query": "Web Summit Lisbon 2026 November dates AI; Slush 2026 Helsinki dates", "mode": "standard"}

---

> `WebSearch` -- {"query": "Open Source Summit Europe 2026 PyTorch Conference Europe 2026 dates", "mode": "standard"}

---

> `WebSearch` -- {"query": "Sifted Summit 2026 London October; AI Engineer London AgentEng; Google DeepMind London event December 2026", "mode": "standard"}

---

> `WebSearch` -- {"query": "Paris AI events December 2026 NeurIPS side events AI Tinkerers Hugging Face Mistral", "mode": "standard"}

---

**Claude:**

Сверил даты по живым источникам и по нашим отчётам от 01.10 и 04.10. Сам собрал только то, что нашёл в поиске сегодня. Остальное взято из ДР и разведки по Европе от 04.10, где страницы открывали агенты. Новых запусков чужих рельс не делал.

## Что есть в Европе и Дубае

**Конец октября – начало ноября**

| Дата | Событие | Где | Что это |
|---|---|---|---|
| 24–29 окт | [EMNLP 2026](https://www.aischolar.com/conference/emnlp2026) | Будапешт, Hungexpo | Академический NLP, около 3 500 человек. Постеры, воркшопы, найм исследователей. |
| 26 окт | OpenAI DevDay Exchange Berlin | Берлин | Бесплатно, по заявке, 14:00, команды OpenAI на месте. |
| 26–27 окт | [Dubai AI Festival](https://uvation.com/events/dubai-ai-festival-2026) | Дубай, DWTC | Перенесён с апреля. 20 000+ человек, 200+ спикеров. Правительственный и enterprise-формат. |
| 28 окт | OpenAI DevDay Exchange Paris | Париж | Тот же формат. |
| 29 окт | AI Native Netherlands, инференс от Kubernetes до edge | Амстердам | Бесплатный инженерный митап. |
| 3 ноя | OpenAI DevDay Exchange London | Лондон | Тот же формат. |
| 3–5 ноя | [Data & AI Conference Europe](https://www.createwith.com/event/london-data-ai-conference-europe-2026-nov-2026), Future of AI Summit | Лондон | Корпоративные, не для инженеров лабораторий. |
| 4–5 ноя | Big Data & AI World Madrid | Мадрид, IFEMA | Торговая выставка, около 25 000 человек. |

**Ноябрь**

| Дата | Событие | Где | Что это |
|---|---|---|---|
| 9–10 ноя | London Consumer AI Hackathon (a16z, ElevenLabs, AI Tinkerers) | Лондон | Хакатон. Из сниппета, не подтверждено. |
| 9–12 ноя | [Web Summit](https://websummitlisbonsp.bnetwork.com/Home/AboutTheEvent) | Лиссабон | 70 000+ человек, есть AI-трек. Ближе к стартапам и фондам, чем к лабораториям. |
| 11–12 ноя | Connected Data London | Лондон | Графы знаний и данные. Узкая тема. |
| 17–20 ноя | FLLM 2026 | Барселона | Академическая конференция по LLM. Из сниппета. |
| 18–19 ноя | [Slush](https://euagenda.eu/events/2026/11/18/slush-2026) | Хельсинки | Около 12–13 тысяч человек, в основном стартапы и инвесторы. |
| 25–26 ноя | AI World Congress (Лондон), ChatbotSummit (Амстердам) | Лондон, Амстердам | Деловые, про внедрение. |

**Декабрь**

| Дата | Событие | Где | Что это |
|---|---|---|---|
| 1, 2, 7 дек | AI Tinkerers Paris: Physical AI, Data Analytics | Париж | Самая живая глава сети в Европе, 2–4 события в месяц. |
| 7–11 дек | [GITEX Global](https://www.therecursive.com/gitex-global-2026-moves-to-expo-city/) | Дубай, Expo City | 7 дек GITEX Scale Summit, потом выставка 8–11. Огромная, но инженеров лабораторий там мало. |
| 9 дек | AI Tinkerers London в Accel | Лондон | Только из выдачи, не подтверждено. |
| 9–13 дек | **[NeurIPS 2026, парижская площадка](https://aiweekly.co/alerts/neurips-2026-splits-across-sydney-atlanta-and-paris-in-december)** | Париж | Около 8 000 человек. Основная программа и туториалы 9–11 дек, 28 воркшопов 12–13 дек. |

## Что я бы выбрал

1. **NeurIPS Париж, 9–13 дек.** Это самая плотная точка Европы за весь период: исследователи Mistral, DeepMind, Hugging Face и других лабораторий в одном месте. У тебя паспорт ЕС, поездка простая. Вокруг будет много сайд-ивентов, их стоит искать за 2–3 недели до даты.
2. **Тур OpenAI DevDay Exchange: Берлин 26.10, Париж 28.10, Лондон 3.11.** Бесплатно, но по заявке, поэтому подаваться надо сейчас. Все три города можно объехать за неделю. Но 10–12 ноября у тебя AIE Code Summit в Сан-Франциско, значит, обратный перелёт придётся планировать плотно.
3. **Дубай: Dubai AI Festival 26–27 окт полезнее GITEX.** GITEX (7–11 дек) пересекается с NeurIPS Париж, и я бы его пропустил. Festival формально ближе к государству и enterprise, но дат на двоих у нас нет, так что выбирай между ним и европейским туром 26–28 окт.
4. **AI Tinkerers Paris и London плюс митапы Claude Code и Codex.** Это самый дешёвый способ попасть к инженерам. Даты у многих серий на Q4 ещё не объявлены, их надо проверять раз в неделю.
5. **Web Summit и Slush** по нашей же оценке от 01.10 про капитал и фонды, а не про найм в лаборатории. Web Summit к тому же совпадает с Code Summit в SF.

## Чего я не проверил

- Цены и открытость регистрации на NeurIPS Париж. «Early до 30 октября» в наших отчётах относится к Атланте, для Парижа не подтверждено.
- Даты AI Tinkerers (кроме Парижа), Accel 9 декабря и Claude Code митапов в Q4. Анонсов пока нет.
- Все события из таблиц, помеченные «из сниппета», открывались только в выдаче, не на сайте организатора.
- У Anthropic в Европе анонсированного Q4-ивента не нашли.

Дальше могу проверить на официальных страницах заявки на DevDay Exchange и подать их, найти сайд-ивенты вокруг NeurIPS Париж и сложить итог в заметку волта. Скажи, что из этого делать. Если ничего не ответишь, я просто подам заявки на DevDay Exchange: они бесплатные и обратимые.

🧒 **Простыми словами**
Это как афиша на два месяца. Самое главное событие в Европе в декабре — большая научная конференция NeurIPS в Париже 9–13 декабря. Перед ней, в конце октября и начале ноября, есть бесплатные встречи с OpenAI в Берлине, Париже и Лондоне. В Дубае два крупных события: фестиваль в конце октября и выставка GITEX в декабре, но она в те же дни, что и Париж, так что я бы выбрал Париж. Остальные конференции больше про бизнес и деньги, чем про работу в лабораториях.

Sources:
- [NeurIPS Paris](https://aiweekly.co/alerts/neurips-2026-splits-across-sydney-atlanta-and-paris-in-december)
- [GITEX Global 2026](https://www.therecursive.com/gitex-global-2026-moves-to-expo-city/)
- [Dubai AI Festival](https://uvation.com/events/dubai-ai-festival-2026)
- [EMNLP 2026](https://www.aischolar.com/conference/emnlp2026)
- [Web Summit Lisbon](https://websummitlisbonsp.bnetwork.com/Home/AboutTheEvent)
- [Slush 2026](https://euagenda.eu/events/2026/11/18/slush-2026)
- [London AI events, November](https://www.createwith.com/event/london-data-ai-conference-europe-2026-nov-2026)

---

**User:**

поставь все эвенты в календарь
дай мне рейтинг всех с пользой для меня

---

> `ToolSearch` -- {"query": "select:mcp__s_2292b084__list_calendars,mcp__s_2292b084__create_event,mcp__s_2292b084__search_events,mcp__s_2292b084__list_events", "max_results": 4}

---

> `mcp__s_2292b084__list_calendars` -- {}

---

> `mcp__s_2292b084__list_events` -- {"startTime": "2026-10-20T00:00:00", "endTime": "2026-12-20T00:00:00", "pageSize": 250, "orderBy": "startTime"}

---

> `Bash` -- {"command": "python -c \"\nimport json,re\nd=json.load(open(r'C:\\Users\\dev\\.claude\\projects\\P---WORKDIR-HUB\\s_4f6c8ab1\\tool-results\\mcp-s_2292b084-list_events-1792181701508.txt',encoding='utf-8'))\nprint(d.get('summary'),len(

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] Dubai AI Festival 2026 · польза 4/10", "startTime": "2026-10-26T00:00:00", "endTime": "2026-10-28T00:00:00", "allDay": true, "location": "Dubai World Trade Centre, Dubai", "description": "Перенесён с апреля. 20 000+ человек, 200+ спикеров. Государство и enterprise, инженер

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рег: бесплатно] AI Native Netherlands: AI Inference in the Real World · польза 4/10", "startTime": "2026-10-29T00:00:00", "endTime": "2026-10-30T00:00:00", "allDay": true, "location": "Amsterdam", "description": "Инженерный митап, инференс от Kubernetes до edge. Время уточнить. https:/

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] Data & AI Conference Europe (Лондон) · польза 3/10", "startTime": "2026-11-03T00:00:00", "endTime": "2026-11-05T00:00:00", "allDay": true, "location": "etc.venues Fenchurch Street, London", "description": "Конференция 3-4 ноя, воркшопы 2, 5, 6 ноя. Корпоративная. https://w

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] Future of AI Summit (Лондон) · польза 3/10", "startTime": "2026-11-04T00:00:00", "endTime": "2026-11-06T00:00:00", "allDay": true, "location": "London", "description": "Деловой саммит, скидка UNITEAI 20% (по unite.ai). https://www.unite.ai/conferences/ · добавлено сессией 

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] AI in Health Summit (Лондон) · польза 2/10", "startTime": "2026-11-04T00:00:00", "endTime": "2026-11-05T00:00:00", "allDay": true, "location": "London", "description": "Отраслевой, медицина. https://www.unite.ai/conferences/ · добавлено сессией H96829", "availability": "AV

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] Connected Data London (графы знаний) · польза 4/10", "startTime": "2026-11-11T00:00:00", "endTime": "2026-11-13T00:00:00", "allDay": true, "location": "Leonardo Royal Hotel London Tower Bridge", "description": "Графы знаний и данные: близко к нашему мозгу-волту. Пересекает

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] AI Filmmaker Summit (Лондон) · польза 2/10", "startTime": "2026-11-14T00:00:00", "endTime": "2026-11-16T00:00:00", "allDay": true, "location": "London", "description": "AI-кино, не наша тема. https://www.unite.ai/conferences/ · добавлено сессией H96829", "availability": "A

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] FLLM 2026 (академическая по LLM, Барселона) · польза 4/10", "startTime": "2026-11-17T00:00:00", "endTime": "2026-11-21T00:00:00", "allDay": true, "location": "Barcelona", "description": "Дата из сниппета, сайт не открывали. Добавлено сессией H96829", "availability": "AVAIL

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] Language AI Meetup Zürich · польза 3/10", "startTime": "2026-11-23T00:00:00", "endTime": "2026-11-24T00:00:00", "allDay": true, "location": "Zürich", "description": "Дата из сниппета (разведка 04.10). Добавлено сессией H96829", "availability": "AVAILABILITY_FREE", "notific

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] Big Data Conference Europe (Вильнюс) · польза 2/10", "startTime": "2026-11-24T00:00:00", "endTime": "2026-11-28T00:00:00", "allDay": true, "location": "Vilnius, Lithuania", "description": "Data science, ML. Билеты €700-1730. https://www.raisesummit.com/post/best-ai-confere

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] ChatbotSummit Amsterdam (агентный AI) · польза 3/10", "startTime": "2026-11-25T00:00:00", "endTime": "2026-11-27T00:00:00", "allDay": true, "location": "Mövenpick Amsterdam City Centre", "description": "Агенты, multi-agent, enterprise CX. https://www.createwith.com/event/a

---

> `mcp__s_2292b084__create_event` -- {"summary": "[рассмотреть] GITEX Global 2026 (Дубай) · польза 3/10", "startTime": "2026-12-07T00:00:00", "endTime": "2026-12-12T00:00:00", "allDay": true, "location": "Dubai Exhibition Centre, Expo City Dubai", "description": "7 дек GITEX Scale Summit, выставка 8-11 дек. Огромная техвыставка, IC лаб

---

> `mcp__s_2292b084__create_event` -- {"summary": "[🤔 не подтверждено] AI Tinkerers London @ Accel · польза 5/10", "startTime": "2026-12-09T18:30:00", "endTime": "2026-12-09T21:00:00", "timeZone": "Europe/London", "location": "Accel, London", "description": "Дата только из выдачи поиска (разведка 04.10). Пересекается с NeurIPS Париж. ht

---

**Claude:**

Готово: в календарь bb@ добавлено 13 событий, которых там не было. На каждое Google вернул `status: confirmed` и id. Остальные 70+ событий из этого списка уже стояли, их поставили раньше соседние сессии, поэтому дублей я не делал.

**Что добавил:** Dubai AI Festival, AI Native Netherlands, Data & AI Conference Europe, Future of AI Summit, AI in Health Summit, Connected Data London, AI Filmmaker Summit, FLLM Barcelona, Language AI Meetup Zürich, Big Data Conference Vilnius, ChatbotSummit Amsterdam, GITEX Global Dubai и AI Tinkerers London 9.12 (с пометкой 🤔, дата не подтверждена).

Все отмечены как «свободное время», без гостей и рассылок. В названии стоит оценка «польза N/10», в описании ссылка и пересечения с другими событиями.

## Рейтинг пользы для тебя

Цель, по которой оценивал: попасть внутрь ИИ-лаборатории. Поэтому выше стоит то, где можно провести больше 20 минут рядом с инженером или исследователем лаборатории.

| # | Событие | Даты | Польза | Почему |
|---|---|---|---|---|
| 1 | **NeurIPS Париж** | 9–13 дек | **9** | Максимум исследователей Mistral, DeepMind и HF в Европе. Постеры, ужины спонсоров, официальный канал найма. По паспорту ЕС ехать просто. |
| 2 | AIE Code Summit, SF (для сравнения) | 10–12 ноя | 9 | Твой главный ноябрьский якорь. Из-за него выпадают Web Summit и лондонский хакатон. |
| 3 | **Claude Cybersecurity Hackathon London** | 4 ноя | **8** | Мероприятие экосистемы Anthropic, руки и код. Хорошо стыкуется с DevDay London 3.11. |
| 4 | **OpenAI DevDay Exchange London / Paris** | 3 ноя / 28 окт | **8** | Бесплатно, команды OpenAI на месте. Заявки уже поданы. |
| 5 | OpenAI DevDay Exchange Berlin | 26 окт | 7 | То же, но третий город в одном туре даёт меньше. |
| 6 | Fractal Claude Code Workshop London (с Anthropic) | 20 окт | 7 | Люди Anthropic в зале, но до него 4 дня. |
| 7 | Claude Workshop Berlin | 22 окт | 7 | Агенты и Claude Code, наша тема. |
| 8 | EMNLP Будапешт | 24–29 окт | 7 | Академический NLP, исследователи лабораторий. Пересекается с DevDay. |
| 9 | NVIDIA GTC Berlin | 20 окт | 6 | Инженеры инференса, но уже скоро. |
| 10 | AI Tinkerers Paris (3 вечера) | 1, 2, 7 дек | 6 | Можно склеить с NeurIPS в одну поездку. |
| 11 | London Consumer AI Hackathon (a16z, ElevenLabs) | 9–10 ноя | 6 | Сильный зал, но пересекается с SF. |
| 12 | AI Tinkerers London @ Accel 🤔 | 9 дек | 5 | Пересекается с NeurIPS. |
| 13 | Slush Хельсинки | 18–19 ноя | 5 | Для миссии «деньги» да, для найма нет. |
| 14 | Web Summit Лиссабон + неделя PTW | 9–12 ноя | 5 | Фонды и стартапы. Пересекается с SF. |
| 15 | Dubai AI Festival | 26–27 окт | 4 | Государство и enterprise, пересекается с DevDay. |
| 16 | Connected Data London | 11–12 ноя | 4 | Графы знаний, близко к нашему мозгу-волту. |
| 17 | FLLM Барселона | 17–20 ноя | 4 | Академия по LLM, дата не подтверждена. |
| 18 | AI Native NL Амстердам | 29 окт | 4 | Хороший инженерный митап, но маленький. |
| 19 | AI Builders Berlin | 20 окт | 4 | Митап. |
| 20 | GITEX Global Дубай | 7–11 дек | 3 | Огромная выставка, и даты съедает NeurIPS. |
| 21 | ChatbotSummit Амстердам, Language AI Zürich | 25–26 / 23 ноя | 3 | Узкие или деловые. |
| 22 | Big Data & AI World Madrid, AI Congress Barcelona, DevFest Barcelona | ноябрь | 3 | Выставки и общая аудитория. |
| 23 | Лондонские деловые: Data & AI Europe, Future of AI, AI World Congress, Generative AI Summit | ноя–дек | 3 | Корпоративный зал, людей из лабораторий там нет. |
| 24 | Vilnius Big Data, AI in Health, AI Filmmaker | ноябрь | 2 | Не наша тема. |

🎙 Майк: в Европе стоит взять одну вещь, NeurIPS Париж, и приклеить к ней AI Tinkerers Paris. Тур DevDay в Европу заставит в начале ноября лететь назад в SF к Code Summit. Если на 3–4 ноября в Лондон не летишь, поездку в октябре лучше пропустить. Направляющий вопрос: в начале ноября ты будешь в Европе или в Долине?

⚠️ Что я заметил в календаре: DevDay Paris и DevDay London записаны по два раза, их ставили разные сессии. Ничего не удалял, это решаешь ты.

🧒 **Простыми словами**
Я дописал в твой календарь всё, чего там не хватало, и у каждого события в названии теперь стоит оценка от 1 до 10. Самое ценное в Европе: большая научная конференция в Париже 9–13 декабря. Сразу за ней идут бесплатные встречи OpenAI и хакатон вокруг Claude в Лондоне в начале ноября. Дубай и большие выставки дают мало: там продают, а не нанимают. Это как выбирать, куда идти знакомиться: лучше на кухню, где готовят повара, а не на рынок, где продают продукты.
