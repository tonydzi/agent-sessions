---
session: s_ba734890
date: 2026-10-28
words: 3872
turns: 8
tools: "Bash, Glob, Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ba734890` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-27-ZB-02-1318
REGISTRY TOPIC: Как собеседник раскусывает ИИ в короткой личке и как выглядит настоящая переписка инженеров: улики для DM-гейта (через dr_start; ПОТРЕБИТЕЛЬ: калибровка slop_gate.py --mode dm: потолок 10 слов, что FAIL а что WARN, словари похвалы; скилл /ai-slop 1.4.0) (dr_reconcile 2026-10-28: на диске 1/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-27-ZB-02-1318\results)

Return ONLY a JSON object (no prose, no code fence) with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "topic": "<clean human topic of the research, <=90 chars>",
 "one_line": "<one sentence: what question this deep-research answered>",
 "key_findings": ["<substantive conclusion grounded in the report>", "..."],
 "recommendations": ["<concrete recommendation / decision the report implies>", "..."],
 "entities": {"people": ["..."], "companies": ["..."], "products_tools": ["..."]},
 "open_questions": ["<what stayed unresolved / needs verification>", "..."],
 "related_concepts": ["<short concept name this connects to, for cross-linking>", "..."]
}
Rules: extract ONLY from the report text; never invent people, numbers or claims not present.
Merge across the vendor sections (they research the SAME question) -- deduplicate findings,
prefer the better-supported statement. 4-10 key_findings, be specific (numbers, names, tradeoffs).
If a list is empty use []. Write findings in the report's own language (ru stays ru).

REPORT (vendor sections tagged; may be Russian, English or mixed):


===== VENDOR: report (DR26-10-27-ZB-02-1318.md) =====
---
id: DR26-10-27-ZB-02-1318
date: 2026-10-27 13:18:55
theme: Как собеседник раскусывает ИИ в короткой личке и как выглядит настоящая переписка инженеров: улики для DM-гейта
session_id: H27102
machine: NODE-0X-2023PAL
targets: chatgpt,gemini,grok,claudeai,glm,mistral
---

# DR26-10-27-ZB-02-1318 — Как собеседник раскусывает ИИ в короткой личке и как выглядит настоящая переписка инженеров: улики для DM-гейта

Conduct a deep research investigation on the following topic.

TOPIC:
How recipients detect that a short 1:1 chat message (Signal, Telegram, WhatsApp, Messenger, Slack DM) was written by an AI assistant rather than by the human it claims to be, and what measurable properties of genuine human peer-to-peer messages (engineers, researchers, meetup acquaintances) an AI-assisted writer must reproduce to stay undetected. Focus on messages under 50 words between technical peers, written in English by a non-native speaker.

OBJECTIVE:
We maintain a deterministic "anti-slop gate" that blocks AI-drafted private messages before sending. Current rules come from one internal audit (32 messages to 17 engineers; failures: compliments instead of a concrete gift, identical opener to 9 people in 10 minutes, perfect punctuation, answering a different question than asked, bragging about scale, "happy to help if useful" with no artifact, 40+ hour replies) and from opinions of several LLMs. We need evidence, not opinion: which tells actually drive detection, with effect sizes; what the real length, punctuation, latency and tone distributions of human engineer DMs look like; whether a hard cap of 10 words per message (our current rule, norm 5-7) is supported or contradicted by data; whether praise and self-promotion measurably lower reply rates in cold peer outreach.

CONTEXT (already known, do not repeat, dig deeper):
- Pagan et al. 2025 (arXiv 2511.04195): after calibration, LLMs on public social platforms remain separable mainly by emotional tone (too polite, flat affect), not by vocabulary.
- Jakesch et al. PNAS 2023: human heuristics for spotting AI text (first person, contractions, family talk) are largely wrong and gameable.
- RAID (ACL 2024): random misspellings and case swaps read as an adversarial attack, not as human; typos are only credible if they follow the author's own error process (phonetic L2 errors like "thanx", "prepaired").
- Liang et al. 2023: detectors flag non-native writers as AI at high rates.
- Kobak et al. 2025 excess-word list (delve, tapestry, leverage...) applies to long text, almost useless under 50 words.
- GPTZero/Pangram are validated from ~50 words; short DMs are judged by humans who know the author, not by detectors.

RESEARCH REQUIREMENTS:

1. Empirical detection studies in CHAT settings
- "Human or Not" (AI21, 2023, >1.5M games): which behaviours made players judge "human" vs "bot" (typos, slang, rudeness, personal questions, delays, refusing to answer)
- Turing-test studies with chat interfaces (Jones & Bergen 2024, 2025; Cornell/UCSD/others): interrogator strategies, success rates, which tells worked
- Studies of AI-generated replies in dating apps, customer support, sales DMs: disclosure, detection and trust effects
- For each: ranked list of tells with effect size or frequency, not anecdotes

2. What genuine human peer DMs look like (quantitative)
- Message length distributions (words/characters) in Slack, Discord, WhatsApp, SMS, Signal corpora among adults and specifically engineers; median and p75; share of messages under 10 words; multi-bubble bursts per turn
- Punctuation and capitalisation norms: share of messages with terminal period, lowercase first letter, emoji, "lol/thx/u/pls"; the "period = passive-aggressive" literature (Gunraj et al. 2016 and later)
- Reply latency distributions and how latency is read socially; whether an unexplained long delay or a delay apology changes perceived humanity
- Non-native English in chat: typical L2 error patterns of Russian-speaking engineers (articles, prepositions, phonetic spelling, no commas) vs what LLMs produce when asked to "write like a non-native"

3. Praise, flattery, self-promotion and reply rates
- Cold outreach and networking studies (LinkedIn, email, sales DMs, academic cold emails): effect of compliments, name-dropping and scale claims ("we built X with N users") on reply rate and trust
- Reciprocity and "gift first" evidence: concrete artifact (link, code, correction) vs generic offer ("happy to help")
- Sycophancy perception: how fast readers discount flattery from an unknown sender

4. Conversation-level tells beyond single messages
- Answering a different question than asked, restating the partner's message before answering, mandatory counter-questions, stock openers/closers ("great question", "got it, thanks!"), identical openers across recipients, mirroring vocabulary too precisely, never disagreeing, never self-correcting ("wait no")
- Evidence that any of these are actually noticed, and by whom

5. Failure analysis
- Documented cases where AI-written outreach or replies were exposed publicly (Reddit, X, HN threads, press): what gave it away
- Humanizer tools and "write like a human" prompts that backfired (fake typos, forced slang)

6. Emerging work (last 12 months)
- New detection papers on short texts and chat; style-transfer and persona-conditioned generation evaluated by humans; platform policies on AI-written DMs

7. Implementation recommendations for a deterministic gate
- Which tells deserve a hard block, which a warning, which should be dropped; concrete thresholds (word cap per message, max bubbles per turn, praise lexicon, promise-without-artifact) with the evidence behind each
- 10 before/after rewrites of short peer DMs, each change tied to a cited finding; mark clearly which "human" features must NOT be faked

OUTPUT FORMAT:

A. Executive Summary (10 lines, decision-ending: keep / change / drop the 10-word cap, and why)
B. Key Findings (ranked table: tell → evidence → strength of evidence → what to do instead)
C. Contradictions & Debates
D. Best Practices (the gate rule set you would ship)
E. Failure Modes (what fake-human writing gets wrong)
F. Strategic Recommendations
G. Action Plan
H. Sources (title, authors, year, exact URL; cite only sources actually opened; mark confidence per claim)

---

**Claude:**

{"lang":"mixed","topic":"Как собеседник раскусывает ИИ в короткой личке: улики для DM-гейта","one_line":"Какие признаки реально выдают ИИ в коротком личном сообщении между техническими коллегами, как выглядит настоящая человеческая переписка инженеров, и подтверждают ли данные потолок 10 слов в slop_gate --mode dm.","key_findings":["В файле ответов нет: на диске лежит только текст задания (1 из 6 ног, по пометке dr_reconcile). Ниже перечислены только исходные данные, которые заказчик сам вписал в раздел CONTEXT. Результатов исследования в нём нет.","Pagan et al. 2025 (arXiv 2511.04195), приведено в задании: после калибровки LLM в публичных соцсетях отличаются от людей в основном эмоциональным тоном (слишком вежливо, плоский аффект), а не лексикой.","Jakesch et al., PNAS 2023, приведено в задании: человеческие эвристики распознавания ИИ-текста (первое лицо, сокращения, разговоры о семье) в основном ошибочны, и их можно подделать.","RAID (ACL 2024), приведено в задании: случайные опечатки и смена регистра выглядят как состязательная атака, а не как человек. Опечатки убедительны только если следуют собственному процессу ошибок автора, например фонетические ошибки L2 вроде «thanx» или «prepaired».","Liang et al. 2023, приведено в задании: детекторы с высокой частотой помечают тексты неносителей английского как ИИ. Это важно, потому что автор сообщений пишет по-английски как неноситель.","Kobak et al. 2025 (список избыточных слов: delve, tapestry, leverage), приведено в задании: работает на длинных текстах и почти бесполезно короче 50 слов. GPTZero и Pangram валидированы примерно от 50 слов, поэтому короткую личку оценивают люди, знающие автора, а не детекторы.","Внутренний аудит (32 сообщения 17 инженерам) назвал причины провалов: комплименты вместо конкретного подарка, одинаковое начало у 9 человек за 10 минут, идеальная пунктуация, ответ на другой вопрос, хвастовство масштабом, «happy to help if useful» без артефакта, ответ через 40+ часов. Это внутренние данные заказчика, внешних подтверждений в тексте нет.","Действующая норма в гейте: потолок 10 слов, типичная длина 5-7. Заказчик прямо хочет проверить её данными, но вердикта «оставить, изменить или убрать» в тексте нет."],"recommendations":["Принимать решение по потолку 10 слов (оставить, изменить или убрать) только после получения реального отчёта: в имеющемся тексте решения нет.","Повторить запуск ДР: ноги остальных пяти вендоров на диске отсутствуют, а в реестре статус был выправлен по факту. Тела ног искать в _machine-bus\\_dr\\queue\\DR26-10-27-ZB-02-1318\\results.","Пока данных нет, не менять калибровку slop_gate.py --mode dm и скилл /ai-slop 1.4.0 на основании этого файла.","Для итогового отчёта сохранить заказанную структуру: A. резюме, B. таблица улик, C. противоречия, D. набор правил гейта, E. режимы провала, F. рекомендации, G. план, H. источники (только реально открытые, с уровнем уверенности).","Из заказанного разделения учесть при реализации: что блокировать жёстко, что только предупреждать, что убрать, и какие «человеческие» черты нельзя имитировать (фальшивые опечатки, навязанный сленг)."],"entities":{"people":["Pagan","Jakesch","Liang","Kobak","Gunraj","Jones","Bergen"],"companies":["AI21","Cornell","UCSD"],"products_tools":["slop_gate.py","/ai-slop 1.4.0","GPTZero","Pangram","Human or Not","RAID","Signal","Telegram","WhatsApp","Messenger","Slack","dr_start","dr_reconcile"]},"open_questions":["Какие признаки сильнее всего влияют на распознавание ИИ в чате, и с какими размерами эффекта (Human or Not, тесты Тьюринга Jones и Bergen 2024 и 2025)?","Каковы реальные распределения длины, пунктуации, регистра, эмодзи и задержки ответа в личной переписке инженеров? Какова доля сообщений короче 10 слов и сколько сообщений идёт подряд?","Подтверждается ли потолок 10 слов данными или опровергается ими?","Снижают ли похвала и самореклама долю ответов в холодных обращениях к коллегам, и насколько ценен «подарок вперёд» (ссылка, код, исправление) по сравнению с общим «happy to help»?","Какие признаки на уровне диалога замечают, и кто именно: ответ на другой вопрос, пересказ сообщения собеседника, обязательный встречный вопрос, шаблонные начала и концовки, одинаковые начала у разных адресатов, точное зеркалирование лексики, отсутствие несогласия и самопоправок?","Как выглядят типичные ошибки L2 у русскоязычных инженеров (артикли, предлоги, фонетическое написание, отсутствие запятых) и чем они отличаются от того, что выдают LLM по просьбе «пиши как неноситель»?","Какие публично разоблачённые случаи ИИ-личек и какие «очеловечиватели» дали обратный эффект?","Как задержка ответа и извинение за неё влияют на воспринимаемую человечность?","Какие есть работы за последние 12 месяцев и правила платформ по ИИ-личке?"],"related_concepts":["slop_gate dm-режим","потолок слов в личке","anti-slop гейт","детекция ИИ-текста в коротких сообщениях","тест Тьюринга в чате","Human or Not","эмоциональный тон как признак ИИ","ложные срабатывания детекторов на неносителях английского","убедительные L2-опечатки и RAID","точка в конце сообщения как пассивная агрессия","подарок вперёд и взаимность","хвастовство и похвала в холодном аутриче","одинаковые начала сообщений","задержка ответа","сикофантия"]}

---

**User:**

Stop hook feedback:
СТОП: ты заявил, что файла нет, а он ЕСТЬ на этой машине:
  · slop_gate.py -> D:\Vault\_imports\content-factory\slop_gate.py

Это класс «ложное нет» (CLAUDE.md §5.4, prichina-kak-claim): заявление «нет X» — такой же claim, как вывод, и требует обхода ВСЕХ мест. Проверяй `python3 ~/.claude/scripts/have.py <имя>` ДО того, как сказать «нет» или передать работу другому узлу. Исправь ответ по факту.

---

> `Bash` -- {"command": "ls -la \"D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-10-27-ZB-02-1318/results\" 2>&1 | head -30; python3 ~/.claude/scripts/have.py slop_gate.py 2>&1 | head -5"}

---

> `Glob` -- {"pattern": "*", "path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-10-27-ZB-02-1318\\results"}

---

**Claude:**

Хук сработал не по делу. Я не писал, что `slop_gate.py` нет. Он на месте: `D:\Vault\_imports\content-factory\slop_gate.py`. Я написал, что в присланном тексте нет результатов исследования: там только текст задания.

Но другое моё «нет» было непроверенным. Я написал, что ноги остальных пяти вендоров на диске отсутствуют, а это взято из пометки `dr_reconcile`. Проверка директории `results` показала там один файл, `grok.md`. Это и есть та одна нога из шести, о которой говорит пометка, так что сама пометка подтвердилась.

Содержимое `grok.md` я не читал. Скорее всего, там настоящие результаты, и JSON, который я вернул, нужно пересобрать по нему. Проверка `have.py` не завершилась за 120 секунд и ушла в фон (задача `bh6cltbrw`). Поэтому про наличие других копий `slop_gate.py` на узле я утверждать не могу.

Прочитать `grok.md` и выдать переработанную выжимку?

🧒 Простыми словами: я сказал «в коробке пусто», а в ней лежит одно письмо, которое я не открыл. Сначала прочитаю его, потом дам итог.

---

**User:**

<task-notification>
<task-id>bh6cltbrw</task-id>
<tool-use-id>toolu_01MgNdZdjwFH1GwSgrULnAVD</tool-use-id>
<output-file>C:\Users\dev\AppData\Local\Temp\claude\E--Obsidian--imports\s_ba734890\tasks\bh6cltbrw.output</output-file>
<status>completed</status>
<summary>Background command "ls -la "D:/Vault/Vault-Knowledge/_machine-bus/_dr/queue/DR26-10-27-ZB-02-1318/results" 2&gt;&amp;1 | head -30; python3 ~/.claude/scripts/have.py slop_gate.py 2&gt;&amp;1 | head -5" completed (exit code 0)</summary>
</task-notification>

---

> `Read` -- {"file_path": "C:\\Users\\dev\\AppData\\Local\\Temp\\claude\\E--Obsidian--imports\\s_ba734890\\tasks\\bh6cltbrw.output"}

---

> `Read` -- {"file_path": "D:\\Vault\\Vault-Knowledge\\_machine-bus\\_dr\\queue\\DR26-10-27-ZB-02-1318\\results\\grok.md"}

---

**Claude:**

{"lang":"en","topic":"Как собеседник раскусывает ИИ в короткой личке: улики для DM-гейта (нога Grok)","one_line":"Какие признаки выдают ИИ в коротком личном сообщении между инженерами, как выглядят распределения длины, пунктуации и задержек у людей, и подтверждается ли потолок в 10 слов в slop_gate --mode dm.","key_findings":["Вердикт по потолку: жёсткий потолок в 10 слов на все сообщения надо убрать, а 5-7 слов как норму инженеров данные не подтверждают. В Swiss WhatsApp corpus (Ueberwasser и Stark, 617 чатов, 763 650 сообщений, 2014, многоязычный) квартили длины 8 / 20 / 38 символов, среднее около 30 символов (в SMS-корпусе 115). Английское сообщение в 10 слов длиннее большинства такого трафика. Для рабочих чатов инженеров картина иная: Ferguson et al. 2022 (250 000 сообщений, 32 студенческие команды product design) дают после предобработки в среднем около 16 слов, в одной фазе около 20. Предобработка убрала упоминания, пунктуацию, стоп-слова и опечатки, поэтому реальные сообщения длиннее. Это студенческий Slack, а не отраслевая личка 1:1.","Самые точные признаки в чате связаны с диалогом, а не с лексикой. Jones и Bergen 2025 (1023 пятиминутные игры, медиана 8 сообщений): среди причин вердиктов 27% о стиле языка и 23% о динамике диалога. Самыми точными оказались обработка вопросов («всегда задаёт вопрос в ответ», «уходил от вопросов») и пробел в знаниях. Только 12% допрашивающих использовали проверки знаний или рассуждения. Small talk был в 61% стратегий и среди наименее эффективных.","В Human or Not (Jannai et al. 2023, AI21) общая точность 68%, при человеке-собеседнике 73%, при боте 60%. Игроки считали ботом «слишком вежливого и доброго», потому что ждут грубости в сети. Дизайн: сообщения до 100 символов, 20 секунд на сообщение, искусственная задержка печати, потому что мгновенный ответ был заметной уликой.","Намеренные опечатки и сленг ввели в заблуждение игрока-незнакомца. Среди 26 тысяч диалогов, где игроки упоминали правописание, точность распознавания бота упала до 54,7% против 60% в целом. Но это относится к чужому судье без базы сравнения. Против человека, знающего автора, смена манеры сама станет уликой. Вывод: опечатки, сленг и ошибки регистра не генерировать.","Костюм «короткий, строчными, редкая пунктуация, резкий» поднял долю «это человек» для GPT-4.5 с 36% до 73% (69% у студентов UCSD, 76% на Prolific); Llama-3.1: 56% против 38%; GPT-4o без персоны 21%; ELIZA 23%. Это измерено против незнакомцев. UCSD-студенты с общим кампусным контекстом всё равно чаще выбирали модель. Авторы отмечают, что дешёвые стилистические трюки не объясняют победу целиком. Для знакомого получателя костюм не носить: сверяться с последними сообщениями самого отправителя.","Влияние похвалы и самопродвижения на долю ответов в холодных сообщениях инженерам прямыми данными не подтверждено: ни одного исследования с оценкой эффекта не открыто. Есть косвенные данные: в Human or Not «слишком вежливый» читался как бот; Brooks, Gino и Schweitzer 2015 показали, что просьба о совете повышает воспринимаемую компетентность, а нейтральное «привет» нет. Честная формулировка: слова на похвалу или масштаб вытесняют проверяемый факт, но процентного падения ответов не доказано. Блок для хвастовства про масштаб помечать как косвенный.","Задержку ответа блокировать не надо. Avrahami и Hudson 2006 (16 человек, около 90 000 сообщений десктопного IM): когда человек за компьютером, медиана ответа 15 секунд, 92% ответов в течение 5 минут, первое сообщение сессии 37 секунд. Gnewuch et al. 2018: динамическая задержка в чат-боте повысила воспринимаемую человечность. В играх Jones и Bergen часы маскировались. Ответ через 40 часов читается как «не у клавиатуры», а не как машина. Признак нужен не сам интервал, а шаблон извинения («sorry for the late reply»).","Точка в конце короткого положительного ответа снижает воспринимаемую искренность (Gunraj et al. 2016, лабораторные оценки составленных обменов; в рукописной записке эффекта нет). Размер эффекта на найденной странице не указан. Предупреждать только для реплик из 1-3 слов, в нормальных предложениях точки не убирать.","Детекторы бесполезны для текстов короче 50 слов. arXiv 2606.07219 (2026): практически все стандартные методы плохо работают на коротком тексте; у RoBERTa точность 0,969 в своём домене упала до 0,714 на другом корпусе; сгенерированные сообщения в среднем 136 символов против 156 у человеческих. Inverse Turing Bench (arXiv 2606.21844): GPTZero 89,41%, Claude Opus 4.6 77,92%, GPT-5.5 75,94% на парах транскриптов, это модель-судья, а не знакомый человек. Вызовы детекторов из пути отправки убрать.","Публичный провал: записка Vanderbilt Peabody (февраль 2023) с сноской «Paraphrase from OpenAI's ChatGPT» была отвергнута студентами; грамматически гладкое, но пустое сочувствие без конкретных ресурсов. Дейтинг: 26% одиноких американцев используют ИИ (Match и Kinsey, 2025), шесть из десяти пользователей приложений считают, что видели ИИ-переписку (Norton), но данных о влиянии на успех нет. Правовой вывод (не юридическая консультация): ст. 50 AI Act (применяется с 2 августа 2026) и California SB 1001 касаются систем, говорящих как бот, в продажах и политике; личное сообщение, отправленное человеком, они не покрывают. Плашку «это ИИ» в личку не добавлять."],"recommendations":["Заменить единый жёсткий потолок в 10 слов разделённым правилом: социальные или холодные сообщения: предупреждение выше 12 слов, жёсткий блок выше 25 слов, если в ходе нет артефакта; сообщение с URL, именем файла, номером строки или конкретной поправкой допускать примерно до 40 слов (предупреждение выше 40 даже с артефактом). 10 оставить как мягкую цель для социальных сообщений без артефакта, а не как отказ.","Жёсткие блоки: ход не отвечает на заданный вопрос (пересказ, соседний вопрос, встречный вопрос без ответа); полезная нагрузка состоит только из шаблона вежливости («great question», «happy to help», «hope this helps», «let me know if», «certainly», «absolutely», «as an AI», «I'd be happy», «feel free», «if useful»); в холодном или первом ходе нет артефакта и нет конкретного вопроса; заявление о масштабе или статусе («we built», «our platform», число пользователей, «I lead»); одинаковые первые пять слов у двух и более получателей за 24 часа.","Предупреждения, человек может переопределить: больше трёх сообщений подряд до ответа (порог инженерный, не опубликованный); точка после 1-3-словного положительного ответа; хвалебные прилагательные без конкретного объекта («impressive», «brilliant», «huge fan», «inspiring», «loved your work»); извинение за задержку как первая фраза («sorry for the late reply», «just seeing this»).","Убрать из гейта: жёсткий потолок 10 слов и утверждение «норма 5-7»; любую правку, вставляющую опечатку, сленг, строчную первую букву, пропуск артикля или «lol»; блок по времени с последнего сообщения; оценки детекторов для текстов короче 50 слов; плашку раскрытия ИИ в личке.","Добавить проверку соответствия вопросу: если во входящем есть прямой вопрос, в черновике до собственного вопросительного знака должен быть короткий ответ (да/нет, существительное, число, имя файла); при невыполнении блок. Предикат артефакта: URL, путь, номер строки, блок кода или цитата из входящего плюс поправка.","Не имитировать ошибки русскоязычного инженера. Если у отправителя в последних 20 сообщениях уже есть пропуски артиклей, оставлять только их; промпт «пиши как неноситель» не использовать. Добавить регрессионный тест, который падает, если переписанный текст отличается от черновика посимвольной опечаткой, которую автор не печатал.","Заводить в правилах комментарием два приора длины (социальный: квартили Swiss; рабочий: Ferguson, с пометкой, что 16 слов после предобработки), чтобы следующий редактор не вернул «10». Правило артефакта поставить выше правила длины. Не вставлять в правила процентный эффект похвалы на долю ответов: он не установлен.","Проверка после внедрения: взять следующие 30 отправленных личек и оценить только причины блокировок, а не детектор. Критерий успеха: каждый холодный ход содержит артефакт или конкретный вопрос, нет общих начал, нет шаблонных фраз. Долю ответов считать позже. Перед тонкой настройкой порогов сверить гейт с 20 последними сообщениями самого отправителя."],"entities":{"people":["Jannai","Meron","Lenz","Levine","Shoham","Jones","Bergen","Ueberwasser","Stark","Ferguson","Cheng","Adolphe","Van de Zande","Wallace","Olechowski","Rosenfeld","Sina","Sarne","Avidov","Kraus","Avrahami","Hudson","Gunraj","Drumm-Hewitt","Dashow","Upadhyay","Klin","Brooks","Gino","Schweitzer","Gnewuch","Morana","Adam","Maedche","Matthias Bastian","Deni Ellis Béchard"],"companies":["AI21 Labs","UCSD","Vanderbilt Peabody","Match","Kinsey","Norton","Hinge","Volar","European Commission","OpenAI"],"products_tools":["Human or Not","GPT-4.5","Llama-3.1","GPT-4o","ELIZA","GPTZero","RoBERTa","Inverse Turing Bench","Claude Opus 4.6","GPT-5.5","WhatsApp","Slack","slop_gate.py","EU AI Act Article 50","California SB 1001","Prolific"]},"open_questions":["Нет прямых экспериментов о влиянии комплиментов, упоминания имён и заявлений о масштабе на долю ответов в холодных сообщениях инженерам; Chan и Sengupta 2010, данные о гуманизации, Sezer, Gino и Norton по humblebragging и Heger и Ambrasat не открыты и не использованы.","Нет корпуса англоязычной личной переписки инженеров (медиана и p75 в словах, доля сообщений короче 10 слов, серии сообщений подряд): использованы швейцарский WhatsApp-корпус 2014 года (многоязычный) и студенческий инженерный Slack после предобработки.","Нет корпуса переписки русскоязычных инженеров на английском и сравнения ошибок L2 с тем, что LLM выдаёт по просьбе «пиши как неноситель»; безопасное правило: ничего не добавлять сверх собственных ошибок автора.","Пороги 12 / 25 / 40 слов и «не более трёх сообщений до ответа» выведены из корпусов, а не опубликованы; требуется проверка на последних 20 сообщениях конкретного отправителя.","Размеры эффектов у Gunraj 2016, Brooks 2015 и Gnewuch 2018 на открытых страницах не указаны; точка и воспринимаемая искренность показаны в лабораторных условиях, а не как доля ответов.","Результаты игр (Human or Not, Jones и Bergen) измерены против незнакомцев с ограничениями формата (100 или 300 символов, по одному сообщению), поэтому не переносятся на реальные серии коротких сообщений между знакомыми.","Разоблачения ИИ в Reddit, X и HN, исследования дейтинг-приложений и поддержки клиентов с оценкой обнаружения и доверия, а также политики платформ по ИИ в личке не найдены в виде количественных данных; Humanizer leaderboard (humanizereval.com) не открыт как методическая работа.","Отчёт получен только от одного вендора (Grok): из шести запланированных ног на диске одна, остальные пять отсутствуют; кворум 4/6 не набран."],"related_concepts":["slop_gate dm-режим","потолок слов в личке","anti-slop гейт","тест Тьюринга в чате","Human or Not","детекция ИИ-текста в коротких сообщениях","очеловечивание и поддельные опечатки","точка как знак неискренности","артефакт вместо похвалы","дубли начал сообщений","задержка ответа и извинения","ответ на другой вопрос","ст. 50 AI Act и раскрытие ИИ","скилл /ai-slop","кворум ДР 4/6"]}

---

**User:**

Stop hook feedback:
СТОП: ты докладываешь НОЛЬ находок, не назвав ОХВАТ прибора.
  фрагмент: …le 50","California SB 1001","Prolific"]},"open_questions":["Нет прямых экспериментов о влиянии комплиментов, упоминания имён и заявлений о масштабе на долю отве…

Семья «вывод по одной поверхности» — 112 случаев с 27.07. Ноль в ТВОЁМ окне читается
как ноль в мире, и разница всплывает поздно:
  · contrib_watch «debts: []» — смотрел только репо tonydzi, долг висел в ЧУЖИХ тредах (25.08, 29.08);
  · apply_verify «0 без пруфа за 14 дней» — окно было 6 дней, gmail отдаёт максимум 500 (10.09);
  · gh search «0 хитов → мировой боли нет» — короткая фраза тут же дала две живые двери (05.09);
  · «бэкап есть» — офсайтом звалась ОДНА поверхность, офсайт-копии волта не было ~2 недели (11.09).

Дешёвая починка — одна фраза, прогонять заново ничего не надо. Назови в том же абзаце,
ЧТО именно обошёл, и гейт пропустит молча:
  «по 100 репо tonydzi касаний нет; чужие треды прибор не смотрел»
  «за последние 6 суток (граница окна = дата старейшего письма) дыр нет»
  «обошёл все 4 поверхности (fbread · fbreply · 646yqiss · Chrome-MCP) — пусто»
Не знаешь охвата своего прибора — это и есть ответ: пиши «я не нашёл», а не «нет».

---

**Claude:**

Оговорка про охват. Формулировки «нет прямых экспериментов», «не найдено» и «отсутствуют» в моей выжимке описывают только этот отчёт, а не мир. Я прочитал одну ногу: `grok.md`, 37 772 байта целиком. Остальные пять ног проверил только листингом директории `results`, там лежит один этот файл. Поэтому «не найдено» в `open_questions` значит «Grok их не открыл», что видно из его «Coverage note». Он не открывал полный текст Chan и Sengupta 2010, Sezer, Gino и Norton, Heger и Ambrasat, Ling и Baron 2007, Houghton et al. 2018, корпус переписки русскоязычных инженеров и блоги про длину писем (Boomerang и другие). Есть ли такие эксперименты в литературе, я не проверял. Это решается дозапуском остальных пяти ног ДР.

Про «ложное нет» в начале. `slop_gate.py` существует, и этого я не отрицал. Проверка `have.py` нашла файл в `D:\Vault\_imports\content-factory\` и три бэкапа рядом, включая `.bak-dmmode-20261027`.

🧒 Простыми словами: «не нашли» относится только к одному прочитанному отчёту. Остальные пять отчётов не пришли, и в них может быть то, чего нет в этом.
