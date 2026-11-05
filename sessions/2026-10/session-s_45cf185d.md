---
session: s_45cf185d
date: 2026-10-09
words: 5185
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-09 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_45cf185d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-07-HUB-06-1649
REGISTRY TOPIC: амбассадорство и интеграторство у ИИ-вендоров: что из этого реально кормит одного человека в Долине (dr_reconcile 2026-10-08: на диске 3/5 ног, в реестре стояло 'issued' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-07-HUB-06-1649\results)

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


===== VENDOR: grok (grok.md) =====
I'll verify each claim against live pages and primary program terms before writing the report.A. Короткий вердикт

Амбассадорский значок сам по себе одного человека в Пало-Альто не кормит. Там, где программа прямо пишет про деньги, место почти всегда неоплачиваемое: кредиты, мерч, бюджет на пиццу и venue. Единственная открытая личная комиссия с цифрой на первоисточнике, которую можно совместить со званием амбассадора, это партнёрка ElevenLabs: до 22% с платежей привлечённого платного клиента в первые 12 месяцев (https://elevenlabs.io/affiliates, страница открыта в этом прогоне). Это не зарплата, пока нет объёма.

Партнёрский статус Select у Anthropic для фирмы из одного человека закрыт опубликованным порогом, не «почти закрыт». С 3 июня 2026 Select требует минимум 10 действующих сертифицированных людей, 2 совместных заказчика в проде за 12 месяцев и 1 публичную историю. Даже уровень Registered требует обязательства на 10 сертифицированных. Вход в сеть бесплатный. Отдельный трек «referral credit» существует, ставка не опубликована (https://www.anthropic.com/news/services-track-partner-hub).

У OpenAI Partner Network пороги Select в деньгах, сертификациях и внедрениях на официальной странице от 14 июня 2026 не опубликованы. Членский взнос там тоже не назван. Публичный пример «маленького» партнёра у руководителя программы Коллин Кейпас от 16 июня 2026 это компания на 100–150 человек, не соло (https://openai.com/index/introducing-openai-partner-network/ и https://www.crn.com/news/ai/2026/openai-seeks-both-large-and-small-partners-accenture-pwc-bain-and-more-talk-new-program). Числа лидов из каталога я не нашёл.

В найм из амбассадорства я нашёл один именной случай с датой: Naoufal (Nao, @naoufal_elh) объявил 2 июля 2026, что вышел Field Engineer в Cursor. 7 июля 2026 Бен Лэнг, тогда в команде Cursor, написал, что Nao был среди первых 15 амбассадоров (https://x.com/naoufal_elh/status/2074479079693205510 в цитате поста https://x.com/benln/status/2074479079693205510). Зарплаты нет. Даты входа в программу амбассадоров нет. К 13 июля 2026 в био уже «Prev: @cursor_ai» и SpaceXAI (https://x.com/naoufal_elh/status/2076708252826439950). Это не системный конвейер и не кейс Долины.

Доля неоплачиваемых амбассадоров: опубликованной доли я не нашёл. Нашёл политики программ, и они описывают само место как неоплачиваемое.

B. Что расходится с базой от 7 октября 2026

1. ElevenLabs Community Builder на публичной странице программы сейчас не помечен как пауза. Оба трека, Community Builder и Content Creator, стоят с кнопкой Apply now. В FAQ прямо: можно подать на оба. Там же: «This is a community program, not a paid role», и отдельно: Content Creator Ambassador может параллельно быть в Affiliates (https://elevenlabs.io/ambassador). Форму я не отправлял. Экран после кнопки я не видел. Расхождение именно с публичной страницей.

2. Codex Ambassadors на канонической странице, открытой в этом прогоне, прямо написано «No. The program is voluntary and unpaid». Приоритетные регионы включают North America, Central America, Africa, Middle East, Eastern Europe. Набор закрыт формулировкой «When applications reopen» (https://developers.openai.com/community/codex-ambassadors). В более старом индексе URL https://developers.openai.com/codex/ambassadors/ ещё стояло «honorarium». Живую старую страницу я в этом прогоне заново не открывал. Текущий FAQ, который открыл, говорит unpaid.

3. У Anthropic есть вторая дверь, которой в вашей сводке партнёрской сети нет: Claude Community Ambassadors. Это человек, не фирма. Прямой оплаты нет. Спонсорство ивентов и кредиты есть. Заявки открыты. Несколько амбассадоров на один город разрешены. Параллельное амбассадорство разрешено, кроме компании, чей основной бизнес конкурирует с Anthropic (https://claude.com/community/ambassadors). Порог 10 человек и Tax ID относятся к Partner Network, не к этой программе.

4. Порог Claude Partner Network жёстче формулировки «10+ сотрудников». Официально это 10 active certified individuals, и «active» значит действующий сертификат плюс использование Claude за последние 90 дней. Десятерых сотрудников без сертификатов недостаточно. Десяти человек в штате тоже недостаточно для Select: нужны ещё 2 продакшена и 1 публичная история (https://www.anthropic.com/news/services-track-partner-hub). Поле Business Tax ID на анкете я в этом прогоне не открывал. Ни подтвердить, ни опровергнуть его не могу.

5. Поля анкеты OpenAI «1–50» и тип «AI Boutique» я в этом прогоне не открывал. Не опровергаю вашу живую пробу от 7 октября. Опровергаю вывод, который из этих полей легко сделать: публичная речь канала описывает нижний желанный размер иначе. Кейпас 16 июня 2026 называет «маленькими» AI-native фирмы на 100–150 человек и говорит quality versus quantity, без целевого числа партнёров (https://www.crn.com/news/ai/2026/openai-seeks-both-large-and-small-partners-accenture-pwc-bain-and-more-talk-new-program).

6. Qwen Ambassador и 千问办公大使 (Qwenwork) это разные программы. У модельного Qwen в индексе страницы https://qwen.ai/ambassador стоит «Generally, we do not recommend it» и исключительная собственность Qwen на контент амбассадорской деятельности. У Qwenwork FAQ прямо: эксклюзивный договор не нужен, можно быть членом других сообществ, зарубежным амбассадорам расходы возмещают в долларах (https://qwambassador.mule.page/). Путать их нельзя.

C. Вопрос 1. Деньги. Имена, суммы, даты

Опубликованной статистики «какая доля амбассадоров остаётся без оплаты» я не нашёл ни у одного вендора.

Что нашёл по конкретным людям и программам.

Jun Song (@jun_song), амбассадор Qwen, 20 мая 2026, публично: ему не платят за посты. Получает ранний доступ и $50 кредитов в месяц. Сам пишет, что посты это его мнение (https://x.com/jun_song/status/2056949121563423033 в цитате https://x.com/mr_r0b0t/status/2056949121563423033). Это Корея, не резидент США. Кейс «кредит, не кэш».

Nao, см. раздел D. Это найм, не консалтинговый счёт. Суммы нет.

ElevenLabs, программа, не один человек. Affiliates: до 22% со всех платежей привлечённого клиента в первые 12 месяцев, «no limits» в формулировке страницы (https://elevenlabs.io/affiliates). Ambassador FAQ разрешает совмещать Content Creator и Affiliates (https://elevenlabs.io/ambassador). Именной заработок конкретного амбассадора в долларах я не нашёл. На странице affiliates есть ссылки на разборы Alec Wilcock (15 апреля 2025) и Greg Preece (28 апреля 2025). Тексты этих разборов я не открывал, цифры из них не переношу.

ElevenLabs Voice Library, это не амбассадорство. 22 мая 2026, обновление 22 сентября 2026: голоса в библиотеке суммарно заработали больше $22 млн, больше 10 400 авторов. В ноябре 2025 было $11 млн (https://elevenlabs.io/blog/22-million-earned-by-voice-creators-on-elevenlabs, контент страницы снят поиском, полный рендер в этом прогоне не открывал). Это лицензирование голоса, не статус амбассадора.

Claude Campus Ambassadors: стипендия USD 3 600. Это студенты, 18+, work authorization в стране учёбы. Окно заявок в индексе страницы: 1–12 сентября (https://claude.com/programs/campus, страница поиском, не полным рендером). оператору как не-студенту эта дверь не подходит. Это единственная найденная мной фиксированная кэш-сумма за амбассадорское место, и она студенческая.

Qwen Ambassador, условия, не выплата человеку. Индекс https://qwen.ai/ambassador: кредиты $50–$100 в месяц. Для $100: Dev track минимум 4 материала в месяц, Event track 1 ивент плюс 2 поста. «Top ambassadors may be upgraded to paid partners». Именного человека, которого так повысили, с суммой и датой, я не нашёл. Два месяца без вклада равны выходу. Страница на JS, чистый рендер инструмент вернул пустым. Текст взят из индекса страницы и из пересказа от 12 мая 2026 (https://easyvibecoding.app/curated/1285).

MiniMax Developer Ambassador, форма: «Potential cash rewards or full-time roles». Имени, суммы и даты получившего я не нашёл. Официальный пост MiniMax 18 ноября 2025 повторяет «potential cash rewards and path to full-time roles» без цифры (https://x.com/MiniMax_AI/status/1990824997909418029). Форма: https://docs.google.com/forms/d/e/1FAIpQLSdaq-k3O5tOQvTV7l8dxsrz0enQato1gvvwBhPFIUBX7qJGYg/viewform.

Cursor Ambassadors: ранний доступ, кредиты на личное пользование, бюджет на meetup, стикеры, Slack, мерч. Зарплаты в тексте нет (https://cursor.com/ambassadors).

Mistral Ambassadors: бесплатные API-кредиты на Studio, ранний доступ, публичное упоминание, приглашения. Кэша в опубликованных бенефитах нет. Срок обязательства от 6 месяцев (https://docs.mistral.ai/resources/ambassadors).

Codex Ambassadors, текущий FAQ: добровольно и без оплаты. Поддержка: подписка Pro, кредиты Codex и API, на одобренный ивент еда, призы хакатона, мерч. Срок когорты 6 месяцев, минимум один вклад в месяц (https://developers.openai.com/community/codex-ambassadors).

n8n: бюджет и swag на свои ивенты, лицензии Cloud и Enterprise для обучения, минимум 3 ивента в год, горизонт около 12 месяцев. Зарплаты в описании нет (https://n8n.notion.site/become-an-ambassador).

Microsoft MVP, соседний класс, не ИИ-лаборатория. FAQ: участник должен быть физлицом, не сотрудником Microsoft. Оплаченная работа на работодателя и гонорар спикера в зачёт вклада не идут. Вклад должен быть публичным и бесплатным для читателя, кроме билета на очный ивент (https://mvp.microsoft.com/en-US/faq). Кендра Литтл, 4 ноября 2021: вышла в Microsoft Content Development по SQL и из-за этого перестала быть MVP. Это не конверсия «амбассадор получил оплату за амбассадорство», это правило «сотрудник не может оставаться MVP» (https://kendralittle.com/2021/11/04/working-at-microsoft-senior-content-developer/).

Таблицы членских взносов OpenAI на $2 500 / $7 500 / $25 000 с тирами Registered и Solutions (сторонние пересказы июня 2026) я не использую. Имена тиров не совпадают с официальными Select, Advanced, Elite. На официальной странице взноса нет.

D. Вопрос 2. Конверсия в штат

Подтверждённый именной случай.

Naoufal El Hassani, публично Nao, @naoufal_elh. 2 июля 2026 написал, что вышел Field Engineer в Cursor. 7 июля 2026 Бен Лэнг написал: «From one of the first 15 people to join our Ambassador program to Field Engineer at Cursor» и сослался на cursor.com/ambassadors. Ответ из Марокко прямо связывает его с ростом Cursor-сообщества там (https://x.com/oumayma_es_/status/2074495226232570249). Сколько месяцев он был амбассадором до оффера, я не нашёл. Зарплату не нашёл. К 13 июля 2026 био уже пишет предыдущее место как Cursor и текущее как SpaceXAI. Системности из одного кейса не следует. География кейса не Пало-Альто.

Чего не нашёл.

Не нашёл ни одного именного случая «амбассадор OpenAI / Anthropic / Mistral / Qwen / MiniMax / Cohere / ElevenLabs получил штатную роль DevRel, Applied AI или Partnerships у этого же вендора», с датой выхода и сроком от входа в программу.

Не нашёл вендора, у которого это описано как регулярный механизм с числом конверсий. Формулировки «path to full-time» у MiniMax и «may be upgraded to paid partners» у Qwen остаются обещанием без опубликованного случая.

Не нашёл вендора, про которого можно честно сказать «не случалось ни разу». Отсутствие найденного кейса это «я не нашёл», не доказательство нуля.

Соседние, не ИИ-лабораторные, прецеденты. Google Developer Experts не сотрудники Google. Вход только по рекомендации сотрудника Google или действующего GDE (https://developers.google.com/community/experts/faq). Именной переход GDE в штат Google Developer Advocate с датами в этом прогоне я не открывал. Microsoft MVP несовместим с работой в Microsoft, см. Кендру Литтл выше. Это обратное правило: штат гасит значок, а не значок покупает штат.

Практический смысл кейса Nao. Его нанял человек, который вёл саму программу (Бен Лэнг, контакт на странице амбассадоров: [EMAIL]). Механизм, который виден снаружи, это личное знание сообщества, не бейдж в каталоге.

E. Вопрос 3. Эксклюзив и права на контент

Прямой запрет или жёсткое ограничение, первоисточник.

Anthropic, Claude Community Ambassadors. Параллельно можно, кроме амбассадорства у компании, чей основной бизнес конкурирует с Anthropic. Сомнение просят указать в анкете. Прямой оплаты нет (https://claude.com/community/ambassadors). Текст Ambassador Agreement, который подписывают при онбординге, я не открывал. Публичный FAQ конкурентов ограничивает. Про переход авторских прав к Anthropic на этой странице ничего нет.

Cursor. Не запрет, а предпочтение дословно: «Our preference is that you not participate in other advocacy programs while you're in Cursor's Ambassador program» (https://cursor.com/ambassadors). Про собственность на контент на этой странице ничего нет.

Qwen, модельная программа. Индекс https://qwen.ai/ambassador, блок Intellectual Property: все фотографии, изображения, видео и контент, созданные во время или как часть амбассадорской деятельности, исключительная собственность Qwen. Амбассадор даёт неограниченные права на использование, воспроизведение, изменение и распространение для маркетинга и коммерции. Нарушение гайдов: немедленное снятие без компенсации. Английский FAQ-ответ «Generally, we do not recommend it» стоит сразу после ответа про публичное упоминание статуса. Вопрос в чистом рендере я не увидел, страница отдала пустой JS. Пересказ той же страницы от 12 мая 2026 формулирует вопрос как одновременное участие в других ИИ-лабораториях и ответ «обычно не рекомендуем» (https://easyvibecoding.app/curated/1285). Это совпадает с вашей базой. Юридическую силу имеет текст на qwen.ai, не пересказ.

Qwenwork, другая программа. FAQ: эксклюзивный договор не нужен, статус не исключающий, можно быть членом других сообществ (https://qwambassador.mule.page/).

ElevenLabs. Ambassador и Affiliates можно совмещать. Про запрет других лабораторий на открытой странице амбассадоров я не нашёл. Про переход прав на контент к ElevenLabs на этой странице я не нашёл (https://elevenlabs.io/ambassador).

Mistral. На публичной странице бенефитов запрета параллельных программ нет. Форма говорит, что при отборе попросят подпись под Ambassador agreement. Текст соглашения я не нашёл (https://docs.mistral.ai/resources/ambassadors и форма https://docs.google.com/forms/d/e/1FAIpQLSdBSiRzm2xBpMszB_9fBixJNyKdGnPMj99DtZbagHMdHgkGUg/viewform).

Codex, OpenAI. На текущей странице запрета других программ я не нашёл. Оплата прямо отрицается (https://developers.openai.com/community/codex-ambassadors).

Microsoft MVP. Не ИИ-вендор. В зачёт нельзя ставить оплаченный труд. Это ограничение на монетизацию самого вклада, не на параллельные значки (https://mvp.microsoft.com/en-US/faq).

Стратегия «пять значков сразу» упирается не в один общий закон, а в три разных текста. Anthropic режет конкурентов. Cursor просит не совмещать advocacy вообще. Qwen забирает контент амбассадорской деятельности в свою собственность и в FAQ не рекомендует мультилабораторность. ElevenLabs из этого набора самый совместимый с отдельной денежной партнёркой, и это не лаборатория моделей общего назначения.

F. Вопрос 4. Экономика OpenAI Select для микро-шопа

Официально, 14 июня 2026. Три тира: Select, Advanced, Elite. Планка описана качественно: sales performance, technical capability, co-sell engagement, deployment experience. Специализации названы как будущие: Codex, cybersecurity, agents. Инвестиция в экосистему $150 млн. Цель 300 000 сертифицированных консультантов к концу 2026, это цель, не текущий счёт. Пилот Forward Deployed Experts только с founding partners. Имена на старте: Accenture, Bain, BCG, Eliza, McKinsey, PwC. Цифр минимума выручки, числа сертификаций, числа внедрений и членского взноса на странице нет (https://openai.com/index/introducing-openai-partner-network/). Каталог существует: https://openai.com/business/partners/locator/ и заявка https://openai.com/form/partnerintake/. Форму в этом прогоне я не проходил.

Кейпас, 16 июня 2026, CRN. «Small» в её речи это 100–150 человек, AI-native. Крупные рядом: McKinsey, BCG, Bain, Accenture. Число партнёров не задано. «Quality versus quantity», «high technical bar». Сеть должна была стартовать в июле 2026. Про лиды из каталога она цифры не дала (https://www.crn.com/news/ai/2026/openai-seeks-both-large-and-small-partners-accenture-pwc-bain-and-more-talk-new-program).

Сколько фирм в каталоге и сколько лидов он приносит. Свой пересчёт локатора в этом прогоне я не сделал. Сторонний разбор SpotDev от 11 июля 2026, с проверкой локатора 8 августа 2026, насчитал 60 фирм и прямо написал, что пороги не опубликованы (https://www.spotdev.co.uk/blog/openai-select-partner-what-it-means). Индекс страницы локатора в этом прогоне показал строку «69 partners» (https://openai.com/business/partners/locator/). Опубликованной цифры «каталог принёс N лидов партнёру такого-то размера» я не нашёл.

Вывод для микро-шопа, который можно защитить источниками. Анкета может принять маленькую фирму. Это не равно опубликованному праву на лиды. Единственный размер «маленького», который канал назвал вслух, это 100–150. Взнос: не нашёл на первоисточнике. Минимумы Select: не нашёл на первоисточнике.

Для сравнения, у Anthropic пороги опубликованы и для одного человека непроходимы, зато реферал как отдельный трек назван, ставка нет, старт бесплатный (https://www.anthropic.com/news/services-track-partner-hub).

G. Вопрос 5. Цена внедрения LLM в компании 10–200 человек в США

Независимый замер медианы (Clutch, Gartner, опубликованная выборка счетов), который я открыл бы и процитировал как одну цифру для компаний 10–200 человек, я не нашёл. Ниже самооценки бутиков. Это их прайс, не рынок.

Your Business Consultant, Райан Гюр, 28 мая 2026, SMB: стратегия $5–15 тыс., внедрение $10–75 тыс., ретейнер $2–5 тыс. в месяц. Пишет, что большинство первых готовых работ попадает в $15–35 тыс. (https://yourbusinessconsultant.ai/blog/ai-consulting-pricing-smb-2026).

Aiveris, 6 мая 2026, компании 50–500, не 10–200: почасовая $200–350, пилот $40–120 тыс., прод $80–250 тыс., ретейнер $5–15 тыс. в месяц на 2–5 живых workflow (https://aiveris.ai/blog/ai-consulting-cost-smb).

Palavir, Джош Элберг, 12 июня 2026: почасовая $150–600, один workflow $15–40 тыс. за 2–6 недель, частичный ретейнер $2,5–5 тыс., встроенный $7,5–15 тыс. Свой оффер: $25 тыс. за один Claude-пайплайн за 10 рабочих дней, ретейнер $7,5–10 тыс. (https://palavir.co/blog/hiring-ai-consultant-what-to-expect-costs).

Dojo Labs, 17 марта 2026, свой путь: скоуп $3 500 за 2 недели, фикс $15–40 тыс. за 8–12 недель, ретейнер $6–10 тыс. Ссылки на Clutch, McKinsey и Toptal внутри статьи я не проверял отдельным открытием первоисточников (https://dojolabs.co/blog/ai-consulting-pricing-models/).

Layer3, 17 июня 2026, правка 9 сентября 2026: ретейнер $2 500–15 000. Бутик для SMB они сами ставят в $125–250 в час, против $75 у фрилансера и до $500 у senior в большой фирме (https://www.layer3labs.io/guides/ai-consulting-rates-pricing).

The Crunch, 1 июня 2026, широкая вилка, не срез 10–200: пилот $10–50 тыс., ретейнер от $2 тыс. до $50 тыс., Big4 $300–600 в час, бутик $150–300 (https://thecrunch.io/ai-consultant-cost/).

Сходимость, которую можно сказать вслух без выдуманной «средней». У бутиков, которые публикуют свой прайс в 2026, первый фиксированный спринт чаще лежит в полосе примерно $15–40 тыс. на несколько недель, ретейнер примерно $2,5–15 тыс. в месяц. Верх Aiveris ($80–250 тыс. за прод) это уже не соло-спринт. Нижняя полоса $2–5 тыс. в месяц это несколько часов, не содержание человека в Пало-Альто.

Кто конкурирует с одиночкой. На стороне вендоров это не другие одиночки, а фирмы с бенчем. У Anthropic Select начинается с 10 сертифицированных, Preferred со 100, Global Premier с 1 000. Accenture, Cognizant, Deloitte, KPMG, Infosys, PwC названы как те, кто уже сажает Claude на десятки и сотни тысяч своих людей (https://www.anthropic.com/news/services-track-partner-hub). У OpenAI в одном абзаце анонса стоят Accenture, Bain, BCG, McKinsey, PwC и рядом более узкие Artium и Eliza (https://openai.com/index/introducing-openai-partner-network/).

Чем одиночка выигрывает у класса Accenture. Отдельного исследования win-rate я не нашёл. Из опубликованного следует другое. Anthropic прямо пишет, что размер фирмы тир не поднимает и не опускает: десятиместный шоп меряют той же планкой, что и глобальную фирму, и планка это сертифицированные люди плюс живые внедрения (та же страница Anthropic). Одиночка эту планку не проходит. Выигрыш одиночки, который источники описывают ценой, а не лозунгом: фиксированный короткий спринт за $15–40 тыс. против дня Big4, который The Crunch ставит в $2 500–3 500 плюс, и именной человек в SOW вместо бенча. Это другой товар. Это не «тот же Select, только дешевле».

H. Вопрос 6. Китайские вендоры и резидент США

Прецедента, в котором резидент США получил уголовное дело, предписание FARA, попадание под Entity List или отказ в экспортной лицензии именно за публичное амбассадорство Qwen, MiniMax, Kimi или Z.ai, я не нашёл.

Что нашёл рядом, и это другие действия.

FARA в 2025–2026 применяют к политическому представительству и лоббизму, не к туториалам модели. Фирма Mercury зарегистрировалась иностранным агентом Hangzhou Yushu (Unitree Robotics) в конце декабря 2025, контракт $75 000 в месяц, задача помочь компании не попасть в чёрные списки (https://justthenews.com/government/security/former-gop-senators-firm-foreign-agent-chinese-robotics-company-china-hawks). WilmerHale, 28 сентября 2026: DOJ напоминает про гражданскую и уголовную ответственность за нерегистрацию по FARA и 18 USC 951 и ведёт правило в сторону финальной версии. Примеры в алерте про политическое влияние, не про developer relations (https://www.wilmerhale.com/en/insights/client-alerts/20260925-faras-future-doj-signals-regulatory-revisions-and-heightened-enforcement-action). Письмо сенатора Коттона в июне 2026 про возможный FARA касается кампании вокруг дата-центров, не амбассадоров моделей (https://www.foxnews.com/politics/sen-tom-cotton-urges-doj-probe-chinese-bid-kneecap-american-ai).

Исходящие инвестиции, не значок. 7 октября 2026 Казначейство объявило первый штраф по правилам американских инвестиций в чувствительные китайские технологии: $200 000 с Amidi, LLC, родителя Plug and Play, за неуведомление об инвестиции китайского фонда примерно на $92 478 в шанхайскую robotics-AI компанию (https://ground.news/article/us-issues-first-outbound-investment-fine-over-chinese-robotics-ai-deal). Покупка доли это не пост и не митап.

Репутационный фон, который рекрутер американской лаборатории увидит без суда. Reuters, 17–18 сентября 2026: ФБР обвинило Alibaba в копировании моделей Anthropic. Anthropic говорила законодателям, что операторы, связанные с Alibaba и Qwen, вели distillation с 22 апреля по 5 июня 2026. Комитет Палаты по Китаю в апреле писал Airbnb про использование Qwen. Federal Register ненадолго использовал Qwen как один из поисковых инструментов и убрал его (https://www.reuters.com/jp/world/security/34J2ERB7DZLJRFEMPYBXMDDB6U-2026-09-18/ и https://www.benzinga.com/markets/tech/26/09/61861167/us-government-website-quietly-used-alibabas-qwen-ai-amid-fbi-accusations-of-china-firm-imitating-anthropic-report). Пентагон, письмо конгрессу от 7 октября 2025: Alibaba, Baidu и BYD «merit inclusion» в список 1260H. Alibaba ответила, что оснований нет и что список 1260H не мешал бы обычной коммерции, потому что она не продаёт американским военным закупкам (https://klse.i3investor.com/web/blog/detail/ceomorningbrief/2025-11-28-story-h500555486-Pentagon_Cited_Alibaba_on_China_Military_Aid_in_Oct_7_Memo). Я не подтвердил отдельным открытием, что Alibaba после этого письма реально внесена в 1260H. CBS, 2 октября 2026, по тесту Hirundo на 500 промптов: у Qwen описаны отказы по Тяньаньмэнь, лагерям и другим темам, чувствительным для Пекина (https://explainx.ai/blog/qwen-censorship-hirundo-audit-3-billion-downloads-2026, вторичный пересказ CBS).

Найм. Именного отказа американской лаборатории кандидату из-за значка Qwen или MiniMax я не нашёл. Именного найма такого амбассадора в американскую лабораторию тоже не нашёл. Ближайшее операционное правило, которое уже написано: Claude Community Ambassadors просит не быть одновременно амбассадором конкурента (https://claude.com/community/ambassadors). Публичный значок Qwen попадает в эту формулировку без всякого суда. Cursor просит не сидеть в других advocacy-программах вообще (https://cursor.com/ambassadors).

Kimi (Moonshot) и Z.ai (Zhipu): отдельной амбассадорской программы с опубликованными правилами в этом прогоне я не нашёл. Открытый анонс соседнего китайского контура: OpenBMB 10–11 июля 2026 обещал Global Developer Ambassador Program с деталями 20 июля 2026. Страницу самой программы после запуска я не открыл (https://x.com/OpenBMB/status/2075857826392756615).

I. Вопрос 7. Программы, которых не было в вашей тридцатке

Открытые или живые, человек, не фирма.

Claude Community Ambassadors. Город, ивенты, кредиты, без зарплаты, заявки открыты, конкурентов просят не совмещать. Это главная пропущенная дверь под ежемесячный митап в Пало-Альто (https://claude.com/community/ambassadors).

ElevenLabs Affiliates. Не амбассадорство. 22% на 12 месяцев. Совмещается с Content Creator Ambassador (https://elevenlabs.io/affiliates, https://elevenlabs.io/ambassador).

LangChain Ambassadors. Описание на странице сообщества: митапы, контент, ранний доступ, гранты на ивенты, бесплатный LangSmith. Набор с дедлайном 26 сентября 2025 анонсирован официальным аккаунтом. Жив ли набор 8 октября 2026, отдельной открытой формой я не проверил (https://www.langchain.com/v-2/community-v2-sdfasdfasdf-asdfasdfafsd и https://x.com/LangChain/status/1967598276040892586).

Lovable Ambassadors. Городские, кампус, отраслевые лиды. На хабе 153 амбассадора в индексе. Заявки закрыты, есть лист ожидания. В бенефитах: бесплатный Pro, возмещение митапа, прямой канал. Ответ FAQ «is this a paid role» в рендере не раскрылся (https://lovable.dev/shebuilds).

Lovable Solution Partner. Это продажи, не коммьюнити. В справочнике правил: 10% комиссии на одном уровне, 15% на Premier при $120 000 проданного enterprise ARR или $240 000 managed ARR, выплата от $500, эксклюзив лида на 6 месяцев. Нужен план Business или выше (https://solutions-partner-program-rules.lovable.app/).

Supabase SupaSquad. По обзору TinyFish от 1 октября 2026, обновление 7 октября: открытый вход, треки контрибьютора, автора, хоста, спикера. Ранний доступ, бейдж, мерч. Официальную страницу Supabase я в этом прогоне не открыл, поэтому это вторичный источник (https://www.tinyfish.ai/blog/developer-ambassador-programs).

Cloudflare Ambassadors. Анонс 7 августа 2026. Ивенты, кредиты, маркетинг. Заявки когорты 2026–27 были открыты до 6 сентября 2026, ответ обещан к 5 октября (https://blog.cloudflare.com/community-program-refresh/). Попал ли кто-то, я не проверял.

CNCF Ambassadors. Заявки 2026 закрылись 12 июля 2026, уведомления в августе, срок с сентября. Поддержка ивентов и выступлений есть, зарплаты в описании нет (https://www.cncf.io/people/ambassadors/application-process/).

PyTorch Foundation Ambassadors. Дедлайн номинаций 18 июня 2026 уже прошёл. Приоритет регионов в анонсе не включал Северную Америку как дефицит (https://x.com/PyTorch/status/2067165928500986299).

OpenSSF Ambassador Program. Анонс 23 марта 2026. Билеты на Community Days, travel и event funding, первый коhort 10–15 человек, набор rolling (https://openssf.org/blog/2026/03/23/introducing-the-openssf-ambassador-program/).

Cohere Partner Program, трек Consulting and Implementation. Гайд описывает GTM-движения co-sell, re-sell и referral/affiliate с «incentives or commissions». Ставку в открытом фрагменте гайда я не нашёл. Дата запуска программы в блоге Cohere: 7 октября 2025 (https://cohere.com/partners и https://cohere.com/blog/cohere-partner-program-boosting-enterprise-ai, гайд https://cohere.com/partners/guide). Цифра 30% на cohere.live к этой компании не относится. Это другой продукт, коучинговое членство (https://www.cohere.live/become-a-partner/).

Google Developer Groups и AWS User Groups. Городские главы, не вендорский найм. Упомянуты в обзоре TinyFish от 4 октября 2026 как самые большие городские developer-сети (https://www.tinyfish.ai/blog/community-ambassador-programs). Официальные страницы GDG в этом прогоне я не открывал.

NVIDIA. Отдельный «AI Ambassador» для кампусов Орегона поставлен на паузу. 5 октября 2026 представитель NVIDIA подтвердил Capital Chronicle: новых кандидатов не берут, $1,5 млн штата под программу ещё не потрачены. Это государственный контракт на обучение, не глобальный значок для организатора митапа (https://lincolnchronicle.org/nvidia-pauses-program-connected-to-promise-to-boost-training-of-ai-specialists-on-oregon-campuses/).

Hugging Face. Постоянной амбассадорской программы я не нашёл. Нашёл городской ивент: Open Together, 16 октября 2026, Сан-Франциско, старт Open Source AI Week 16–25 октября, бесплатно, 36 демо (https://www.mind-verse.de/news/hugging-face-eroeffnet-open-source-ai-week-mit-community-event-in-san-francisco и https://x.com/jeffboudier/status/2105366320145637817).

TinyFish Regional Ambassadors. $5 за реферала на нижнем уровне, бюджет ивента на верхнем. Источник сам вендор, 1–4 октября 2026 (https://www.tinyfish.ai/blog/developer-ambassador-programs). Как стратегию для входа в лабораторию я бы не ставил рядом с Claude и Cursor.

GitHub Stars, Google GDE, Microsoft MVP вы уже правильно держите как nomination-only. GitHub Stars: ранний доступ, звонки со штабом, ивенты, мерч, профиль. Зарплаты и порога звёзд репозитория на странице программы нет. Самовыдвижение нельзя (https://stars.github.com/program).

Чего не нашёл как живую программу этого класса: отдельного амбассадорства xAI, Perplexity, Groq, Together, Fireworks, Modal, Kimi, Z.ai. Groq в августе 2026 стал NVIDIA Cloud Partner. Это сертификация инфраструктуры компании, не значок человека (https://groq.com/newsroom/groq-becomes-an-nvidia-cloud-partner).

J. Что бы я делал на его месте в ближайшие 14 дней

День 1. Подать Claude Community Ambassador на Пало-Альто, первым понедельником месяца как уже существующим ивентом, без значка Qwen, MiniMax, Kimi и Z.ai. Эта дверь открыта человеку, а не фирме из десяти сертифицированных, и её письменное правило как раз запрещает то, что китайский значок потом придётся объяснять рекрутеру. День 2. Если ElevenLabs уже реально используется, включить Affiliates и только потом решать Content Creator. Community Builder на странице тоже открыт, но второй городской значок рядом с Claude упирается в предпочтение Cursor и в лимит времени. Один городской вечер в месяц не тянет два вендорских отчёта. День 3. Анкету OpenAI Partner Network подать честным размером фирмы и только с теми внедрениями, которые можно показать. Каталог не бюджет на 90 дней: ни взноса, ни минимума Select, ни числа лидов в открытых источниках нет, а «маленький» в речи канала это 100–150 человек. День 4–5. Не подавать Mistral, Cursor и Qwen пачкой. Cursor просит не сидеть в других advocacy. Qwen забирает контент. Mistral даёт кредиты, не счёт. День 6–10. Выставить один фиксированный спринт в полосе, которую бутики сами публикуют, $15–40 тыс. за несколько недель, покупатель из уже существующего круга 100+ инженеров и с митапа, не из локатора. Ретейнер $5–10 тыс. предлагать только после сданного спринта. День 11–14. Продолжать прямые подачи в лаборатории. Единственный именной переход амбассадор в штат, который я нашёл, случился потому, что человека уже знал ведущий программы, и даже этот выход наружу выглядит коротким. Значок это повод быть увиденным на своём митапе. Деньги в этих программах лежат в счёте заказчику и в партнёрке ElevenLabs, не в бейдже.

Покрытие этого прогона. Полным рендером открыты страницы Anthropic Services Track, OpenAI Partner Network, CRN с Кейпас, ElevenLabs Ambassador, ElevenLabs Affiliates, Cursor Ambassadors, Claude Community Ambassadors, Codex Ambassadors, Mistral Ambassadors. Qwen.ai/ambassador отдал пустую оболочку, текст взят из индекса той же страницы и сверен с пересказом от 12 мая 2026. Формы OpenAI и Anthropic Partner, текст Ambassador Agreement Mistral и Qwen, локатор OpenAI поимённо и блоги Alec Wilcock / Greg Preece я не открывал. Где цифры нет, выше стоит «не нашёл», а не оценка.

🎙 Майк: гипотеза «внутрь через значок, а не через резюме» в найденных данных не держится. Один марокканский Field Engineer и пачка кредитов. Кормит счёт на спринт и тёплый круг, который у тебя уже есть. Значок Claude нужен, чтобы этот круг увидел лабораторию, а не чтобы лаборатория платила за значок.

🧒 Простыми словами: значок «я представитель компании» почти нигде не платит зарплату. Он даёт наклейки, бесплатные жетоны и иногда деньги на пиццу для встречи. Настоящие деньги у одиночки берутся так: сделал для маленькой фирмы одну конкретную работу за несколько недель и взял за неё оговорённую сумму. Вход в большую партнёрскую полку OpenAI и Anthropic устроен для фирм с командой, не для одного человека. Китайский значок судом пока никого из найденных не наказал, но американская лаборатория прямо просит не быть одновременно лицом конкурента. Поэтому ближайшие две недели: один городской значок Claude, одна честная платная работа для своих, резюме не бросать.

Один вопрос. Первый платный спринт ты готов продать людям, которые уже ходят на твой понедельник, или ты всё ещё ждёшь, что каталог OpenAI приведёт чужого заказчика?

---

**Claude:**

{"lang":"ru","topic":"Амбассадорство и интеграторство у ИИ-вендоров: что реально кормит одного человека в Долине","one_line":"Отчёт проверяет, дают ли амбассадорские и партнёрские программы ИИ-вендоров реальный доход одному человеку в Пало-Альто, ведут ли они в штат, какие у них эксклюзивы и сколько стоит внедрение LLM.","key_findings":["Амбассадорский значок сам по себе одного человека не кормит. Где программа говорит про деньги, место неоплачиваемое: кредиты, мерч, бюджет на pizza/venue. Codex Ambassadors на текущей странице прямо пишет «voluntary and unpaid».","Единственная открытая личная комиссия с цифрой на первоисточнике — партнёрка ElevenLabs Affiliates: до 22% с платежей привлечённого платного клиента в первые 12 месяцев. Её можно совмещать с Content Creator Ambassador. Это не зарплата без объёма.","Anthropic Claude Partner Network закрыт для фирмы из одного человека. С 3 июня 2026 Select требует 10 действующих сертифицированных людей (сертификат плюс использование Claude за 90 дней), 2 совместных заказчика в проде за 12 месяцев и 1 публичную историю. Даже Registered требует обязательства на 10 сертифицированных. Вход бесплатный, referral credit существует, ставка не опубликована.","У OpenAI Partner Network (анонс 14 июня 2026) пороги Select, членский взнос и число лидов из каталога не опубликованы. «Маленький» партнёр в речи Коллин Кейпас (16 июня 2026) — AI-native фирма на 100–150 человек, не соло. Сторонний пересчёт каталога насчитал 60 фирм, индекс страницы показал 69.","Конверсия амбассадор→штат: найден один именной случай — Naoufal (Nao), один из первых 15 амбассадоров Cursor, вышел Field Engineer в Cursor 2 июля 2026 (Марокко, не Долина). Его знал ведущий программы Бен Лэнг, механизм — личное знакомство, не бейдж. Системного конвейера и обещанных «path to full-time» (MiniMax) или «paid partners» (Qwen) именными случаями не подтверждено. У Microsoft MVP правило обратное: штат гасит значок.","Эксклюзивы и права различаются по вендорам: Anthropic просит не быть амбассадором конкурента; Cursor просит не участвовать в других advocacy-программах; Qwen (модельная программа) забирает контент амбассадорской деятельности в исключительную собственность и «generally does not recommend» мультилабораторность. Qwenwork (千问办公大使) — другая программа без эксклюзива. Пять значков сразу упираются в три разных текста.","Пропущенная дверь: Claude Community Ambassadors (человек, не фирма) — городские ивенты, кредиты, спонсорство, без зарплаты, заявки открыты, несколько амбассадоров на город разрешены. Порог 10 человек и Tax ID относятся к Partner Network, не к ней.","Цена внедрения LLM в SMB по самооценке бутиков (не независимый замер): первый фиксированный спринт примерно $15–40 тыс. за несколько недель, ретейнер примерно $2,5–15 тыс. в месяц; почасовая бутика $125–350, Big4 $300–600. Независимой медианы для компаний 10–200 человек не найдено.","Юридического прецедента (FARA, Entity List, уголовное дело) против резидента США за публичное амбассадорство Qwen/MiniMax/Kimi/Z.ai не найдено. Но репутационный фон жёсткий (обвинения ФБР в адрес Alibaba по дистилляции моделей Anthropic, сентябрь 2026), а правило Anthropic о конкурентах на значок Qwen распространяется без суда.","Деньги у одиночки лежат в счёте заказчику за спринт и в партнёрке ElevenLabs, а не в бейдже; значок служит поводом быть увиденным на своём митапе."],"recommendations":["Подать заявку в Claude Community Ambassadors на Пало-Альто (существующий митап первого понедельника месяца), не беря параллельно значки Qwen, MiniMax, Kimi, Z.ai.","Если ElevenLabs реально используется — включить Affiliates, и только потом решать про Content Creator; Community Builder на странице тоже открыт.","Анкету OpenAI Partner Network подавать честным размером фирмы и только с показуемыми внедрениями; не закладывать каталог как бюджет на 90 дней.","Не подавать Mistral, Cursor и Qwen пачкой: Cursor просит не совмещать advocacy, Qwen забирает контент, Mistral даёт кредиты, не счёт.","Продать один фиксированный спринт в полосе $15–40 тыс. покупателю из уже существующего круга (100+ инженеров, митап), ретейнер $5–10 тыс. предлагать только после сданного спринта.","Продолжать прямые подачи в лаборатории: единственный найденный переход амбассадор→штат случился через личное знакомство с ведущим программы."],"entities":{"people":["Naoufal El Hassani (Nao)","Ben Lang","Colleen Kapase (Коллин Кейпас, OpenAI Partner Network)","Jun Song","Kendra Little","Ryan Gur (Your Business Consultant)","Josh Elberg (Palavir)","Alec Wilcock","Greg Preece","Tom Cotton"],"companies":["Anthropic","OpenAI","Cursor","ElevenLabs","Qwen / Alibaba","MiniMax","Mistral","Cohere","Microsoft","Google","GitHub","Lovable","Supabase","Cloudflare","CNCF","PyTorch Foundation","OpenSSF","LangChain","n8n","NVIDIA","Hugging Face","TinyFish","Accenture","McKinsey","BCG","Bain","PwC","Deloitte","KPMG","Cognizant","Infosys","SpaceXAI","Groq","Moonshot (Kimi)","Zhipu (Z.ai)","OpenBMB","Aiveris","Palavir","Dojo Labs","Layer3","The Crunch","SpotDev"],"products_tools":["Claude Partner Network","Claude Community Ambassadors","Claude Campus Ambassadors","OpenAI Partner Network","Codex Ambassadors","ElevenLabs Affiliates","ElevenLabs Ambassador (Community Builder / Content Creator)","Qwen Ambassador","Qwenwork 千问办公大使","MiniMax Developer Ambassador","Cursor Ambassadors","Mistral Ambassadors","Microsoft MVP","Google Developer Experts","GitHub Stars","Lovable Ambassadors","Lovable Solution Partner","Supabase SupaSquad","Cohere Partner Program","LangChain Ambassadors","n8n ambassadors","ElevenLabs Voice Library"]},"open_questions":["Пороги и взнос OpenAI Select, число лидов из каталога партнёров — не опубликованы и не найдены.","Тексты Ambassador Agreement (Anthropic, Mistral, Qwen) не открыты; передача прав на контент у Anthropic не проверена.","Доля неоплачиваемых амбассадоров не опубликована ни одним вендором; присутствует ли конверсия в штат у OpenAI/Anthropic/Mistral/Qwen/ElevenLabs — «не нашёл», не доказательство нуля.","Поле Business Tax ID и поля анкеты OpenAI (1–50, AI Boutique) в этом прогоне не открывались; формы не отправлялись.","Внесена ли Alibaba в список 1260H после письма Пентагона — не подтверждено.","Страница qwen.ai/ambassador отдала пустой JS, текст взят из индекса и пересказа.","Жив ли набор LangChain Ambassadors на 8 октября 2026 и попал ли кто-то в когорту Cloudflare 2026–27 — не проверено.","Независимого замера медианной цены внедрения LLM для компаний 10–200 человек в США нет, только прайсы бутиков.","Причина расхождения для Codex Ambassadors: старый индекс упоминал «honorarium», текущий FAQ говорит unpaid; старая страница не переоткрывалась."],"related_concepts":["амбассадорские программы ИИ-вендоров","партнёрские сети вендоров (Partner Network)","путь в ИИ-лабораторию через сообщество","DevRel и Field Engineer","фиксированный спринт и ретейнер","эксклюзивность и права на контент","риск работы с китайскими ИИ-вендорами","affiliate-доход"]}
