---
session: s_b8805469
date: 2026-10-15
words: 3874
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-15 · You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b8805469` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup call, may be Russian, English or mixed). Do NOT summarize loosely; extract grounded structured facts.

MEETING TITLE: Kate Yanchenko: 1-on-1 with Tony
CALENDAR INVITEES (names/emails, use to name speakers): [EMAIL]

Return ONLY a JSON object, no prose, with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "one_line": "<=1 sentence, what this call was about>",
 "participants": [{"name":"<best-known name or handle>","role":"<our-side|lead|other>","channel":"microphone|speaker|unknown"}],
 "commitments": [{"owner":"<name>","what":"<promise/next step>","due":"<date/relative or ''>","quote":"<verbatim transcript snippet proving it>"}],
 "facts": [{"fact":"<atomic fact about the lead/project: numbers, stage, product>","quote":"<verbatim snippet>"}],
 "objections": [{"objection":"<concern/pushback raised>","by":"<name>","quote":"<snippet>"}],
 "alpha": [{"signal":"<non-obvious insight worth acting on: intro, timing, competitive, deal term; for INTERNAL/team calls: a decision made, a risk flagged, a recurring blocker, a process/idea worth adopting>","why":"<why it matters>","quote":"<snippet>"}]
}
Rules: EVERY item MUST include a verbatim "quote" copied from the transcript (not paraphrased). If a category is empty, use []. Never invent people or facts not in the transcript. Map channel 'microphone' = our side (the account owner), 'speaker' = the counterpart, using the participant list.
INTERNAL/TEAM calls (planerka, standup, planning, ops sync between our own people): these are NOT a reason to return empty categories — STILL extract commitments (who promised what) and alpha (decisions taken, risks/blockers surfaced, ideas/process improvements worth keeping). facts/objections may be [] if genuinely absent.
CRITICAL: ALWAYS return the JSON object, even if the call is NOT a VC/deal-flow call (personal, family, logistics, test, small talk). In that case set one_line to describe what it actually was and use [] only for the categories that truly have nothing. NEVER reply with prose or a refusal instead of the JSON.

TRANSCRIPT (speaker channel in brackets; 'microphone'=our account owner, 'speaker'=counterpart):
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, что я помню, как это работает.
[Memo Guleryuz] У тебя есть какой-то ноутбук?
[Memo Guleryuz] Новый или старый?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это 3-4 года назад мой ноутбук, но я его просто ремонтировал, но я думаю, что у меня есть много пайтона в позиции.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думал, что, если я его ремонтирую, я уничтожу процессор, но теперь он замерзает на моем компьютере.
[Jonathan Archer] Вы могли бы спросить Cloud Code или Codex, чтобы сделать диагноз.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я знаю, я знаю, я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так, лоадим модели.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот, я вижу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Теперь вы можете изменить модели, я могу использовать много...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я заинтересован, будет ли он заряжаться.
[Memo Guleryuz] Я имею ввиду, что он заряжается на нашей стороне, потому что это довольно медленно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, так что...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, здесь вы должны.
[Memo Guleryuz] Увидеть ультра-плюс и лайт-пуллбэк-чейн, плюс все другие модели, и вы можете использовать клауд-код здесь.
[Jonathan Archer] Сейчас у вас есть Клодс, вы почти соединялись с Гроком, но вы закрыли эту кнопку, и вы увидите, что на странице предпринимателей OpenLLM вы можете соединять всех этих предпринимателей.
[Jonathan Archer] Вы можете соединить Кодекс, Кимми, Грок, Керсер, Мюз, а также принести API-ключи.
[Jonathan Archer] Вы увидите, что рядом с кнопкой написано «Локальный».
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я закончу, не волнуйтесь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Моя предложение.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если вы хотите, я могу организовать митинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы можем организовать один в реальной жизни митинг и один онлайн митинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я могу приносить много инженеров, но, может быть, не много, скажем, 50 инженеров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] 30-50 Инженеров Я собираюсь поставить это на Luma.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И вы просто должны сделать презентацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я также сделаю хорошее видео на YouTube после того, как мы закончим митап.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я имею в виду онлайн митап.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, вы знаете, мне не нужно ничего, просто давайте сделаем это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я могу сделать митап, может быть, в следующей неделе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужно немного времени, чтобы объявить, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, давайте начнем с онлайн.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если онлайн, вы счастливы с онлайном, вы можете сделать онлайн, вы знаете, Я могу найти место, поговорить с владельцами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы можем также пытаться разговаривать с этими парнями, которые создали YC Guys.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это сотрудничество в SF, которое называется Corgi.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы знаете Corgi, верно?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, может быть, мы можем их спросить, потому что они делают много YC Meetups, и мы можем попросить их использовать, может быть, их сеть, чтобы привлечь какие-то YC Guys.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но, вы знаете, у меня тоже есть много инженеров, и это не проблема, чтобы привлечь 30-50 инженеров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, говоря о инвесторах, если бы вы могли показать мне вашу декорацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы знаете, все инвесторы сейчас спрашивают только о одной вещь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что это за мод?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] MOAT.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Однако, что я вижу сейчас, множество инвесторов готовы инвестировать в характеристики, так что вы в порядке.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Характеристика теперь инвестируемая.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Инвесторы инвестируют в характеристики.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хармония немного трудно монетизировать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хармонии имеют очень низкий использование, только инженеры могут использовать их.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это все еще возможно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я вижу, как это работает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я попробую...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, Анжел, я хотел бы.
[Jonathan Archer] Поделиться с вами, что мы, как заготовки заготовок.
[Jonathan Archer] Мы мета-лайер.
[Jonathan Archer] Мы гораздо более важны, чем заготовки, потому что мы открытый лайер для всех AI.
[Jonathan Archer] Теперь мы начали работать над интеграцией в команду.
[Jonathan Archer] Команда будет этой дашборд, где манажеры могут видеть всю использованность, могут быть соединенные памяти между командами.
[Jonathan Archer] Это очень просто, чтобы загрузить МСП на все компьютеры.
[Jonathan Archer] И для личного пользователя мы сможем достигать больше, чем для разработчиков.
[Jonathan Archer] На данный момент логинный процесс немного тяжелый для разработчиков, но с аппой для десктопа он будет намного более стремленным, так что кто-то может начать использовать его сразу, и они смогут получать наиболее от него.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, окей.
[Jonathan Archer] И также, я бы сказал, что, к сожалению, мы уходим на воскресенье в субботу.
[Jonathan Archer] Да, мы уходим на воскресенье в субботу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, что это хорошо делать онлайн-эвенты.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас есть онлайн-эвент, делайте онлайн-евент.
[Jonathan Archer] Хорошо, давайте сделаем это онлайн, и потом я передам вам мой дек, наш дек, сейчас для того, чтобы вы посмотрели.
[Jonathan Archer] Если у вас есть кто-то в вашей сети, кто бы хотел бы провести встречу с нами в следующие несколько дней, мы полностью доступны поговорить с инвесторами до воскресенья, и это то, что мы здесь делаем.
[Jonathan Archer] И здесь, когда мы говорим о использовании OpenLLM Pro, вы можете использовать TechWeek, под субтитрами на левом, есть промокод, который вы можете вложить в TechWeek.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я хочу поддержать вас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Плюс одна больше.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто пару кофе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы купили кофе, кофе и я.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В любом случае, спасибо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если все в порядке, давайте попробуем организовать онлайн-митинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я принесу моих инженеров, кого я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я также принесу потрясающего гостя, который может вас интервьюировать, и этот гость имеет опыт в фондозировании.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он работал в инкубаторах, работал с стартапами, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это может задать вам правильную вопрос.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И потом, это видео, YouTube, Вы можете использовать это позже для вашего фонаря, потому что это будет замечательным демо-звуком.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ок?
[Jonathan Archer] Отлично.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ок, отлично.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так, что мне нужно?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужна ваша дека, и потом я сделаю некоторые материалы, которые я отправлю моим инженерам, и вы должны их принять, потому что я не хочу делать...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я не хочу написать что-то, на что вам не комфортно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Отлично.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я понимаю, что у вас есть проблемы с финансами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Тим, на самом деле, это хорошая идея, потому что у меня был звонок.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Почему я поздно приехал?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня был звонок с человеком, который делает продажи B2B.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он называется Мехди.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он антропический интегратор, но не только антропический.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он работает с B2B-кустомерами и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это, наверное, твой потенциальный кустомер.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У тебя есть две опции, чтобы продать продукт— через интеграторы или прямо в корпорации.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прямо в корпорации всегда сложнее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы должны иметь сельский департамент, который делает интеграцию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это довольно больно.
[Memo Guleryuz] оператор, я хочу показать вам что-то там.
[Memo Guleryuz] Это мой экран.
[Memo Guleryuz] Я на разделе разработки.
[Memo Guleryuz] Это мой экран?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, это твой экран.
[Memo Guleryuz] Теперь мы добавляем это.
[Memo Guleryuz] Это наш следующий шаг в направлении Enterprise и Teams.
[Memo Guleryuz] У вас будет такой маркетплейс, и вы можете включить любые эти интеграции.
[Memo Guleryuz] Это применяется для всех членов команды.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага, окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это будет огромное для команд.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Огромное, окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если я сделаю NEMCP и так далее, то я могу привести МСП к вашему маркетплейсе, верно?
[Memo Guleryuz] Да, и мы поддержим даже публичные и приватные рынки, так что мы можем проверить вас и сказать, что это оператор, и если вам нравится оператор и его продукт, мы можем его включить прямо сейчас.
[Jonathan Archer] Да, это огромное.
[Jonathan Archer] Мы можем стать огромным каналом распространения.
[Jonathan Archer] И когда мы говорим о продаже B2B, как вы упомянули, я хотел бы сказать, что мы уже начали общаться с консультантами.
[Jonathan Archer] Например, этот крутой парень, с которым вы меня приглашали в Cloud Coder House.
[Jonathan Archer] Я встретился с ним, и я пошел сфотографироваться, и он стал моим другом.
[Jonathan Archer] И он сказал, что он начнет пытаться пустить OpenLLM к его клиентам.
[Jonathan Archer] И мы встретили еще одного консультанта на понедельник вечером.
[Jonathan Archer] Он тоже начнет поддерживать OpenLLM, нам просто нужно получить последовательный звонок с ним.
[Jonathan Archer] И мы уже думали о том, как эти люди могут быть партнерами распространения, а также, кто они, как они называются, я не знаю, открывающие и инкубаторы, правильно?
[Jonathan Archer] У тебя есть инкубатор, ты можешь зайти в все компании в твоем инкубаторе и сказать, о, ты должен использовать OpenLLM, потому что это замечательный продукт, и он поможет твоей команде быть намного быстрее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Согласен, согласен.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, и ты сейчас вернешься в Латам, или ты отправишься в США?
[Jonathan Archer] Нет, мы вернемся обратно в Латам сейчас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, что это не имеет значения.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] На данный момент, вы можете просто выбрать Google Meet и Zoom для закрытия договора.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вам не нужно быть в NBA.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что это не проблема.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Однако, в ноябре будет большая конференция, также LM-конференция, AI-конференция.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы будете в NSF, нет?
[Jonathan Archer] Я могу быть, особенно если...
[Jonathan Archer] Вы осознаете о конференции?
[Jonathan Archer] Я не осознаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Попрошу вас, Клод, дать вам информацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это будет между 10 и 12 ноября.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это будет большая конференция с 10 до 12 ноября.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это больше как, вы знаете, вы должны быть приглашены.
[Jonathan Archer] AI Engineer Code Summit.
[Jonathan Archer] Аппликация только, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И я надеюсь, что будет много финансовых событий.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но есть еще один конкурент, построенный в 1200-х годах, организованный Церебрал Вэлли.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да,.
[Jonathan Archer] Я слышал.
[Jonathan Archer] Они организатор хак-атона, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Они строят коммунизм, организуют мероприятия, у них есть список всех мероприятий, AI мероприятиях, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто, как мы знаем, хаб для всех.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но, в любом случае, для начала, подробно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Позвольте мне помочь вам с этим мероприятием.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нравится этот продукт.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Думаю, с кем я могу вас представить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И может быть, я не знаю, может быть позже, вы можете добавить меня в вашу команду, в случае, если я могу принести вашу цену, окей?
[Jonathan Archer] Да, конечно, я думаю, что есть много возможностей для этого.
[Jonathan Archer] Одна вещь, которую нам нужно сделать, это улучшить финансирование, чтобы мы могли платить людям.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Расскажите о ваших стоимостях.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сколько вы зарабатываете сейчас в месяц, и сколько вы будете зарабатывать?
[Jonathan Archer] На данный момент у нас очень мало денег.
[Jonathan Archer] Мы просто платим небольшие зарплаты Memo и DOA.
[Jonathan Archer] DOA, извините, это наш инженер UI-UX, но это очень-очень маленькая зарплата для того, чтобы они приехали.
[Jonathan Archer] И, да, наши цены на поддержку OpenLLM довольно низкие, может быть, 500 долларов в месяц.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошая идея.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В моей опыте я заработал денег на стартапы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, что за предстоящее время это будет примерно 1 млн.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] 1-2 Млн.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Зависит от...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Зависит от ценов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я думаю, что 1-2 млн.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это вполне возможно.
[Jonathan Archer] Да, оператор, кстати, мы поднимаем 1 миллион, и я думаю, что это очень действительно.
[Jonathan Archer] И теперь это время наступить, эти следующие 2 недели и первые 2 недели ноября, так что мы действительно благодарны за всю поддержку, которую мы получили.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, окей, окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я подумаю, и я буду делать что-то интересное.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Благодарю вас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Будьте в курсе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я ищу вашу декорацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужна ваша декорация, чтобы лучше понять вас, лучше презентировать вас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужна ваша декорация.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Рекламная декорация с хорошим написанием, потому что это единственное, что, знаете, инвесторы сейчас ищут.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас есть какие-то треки в ваших трекинговых слайдах, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас есть идея о размере рынка торговых средств, я расскажу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что это приятно, Мему, Джонатан.
[Memo Guleryuz] Да, это просто потрясающе.
[Memo Guleryuz] Очень приятно познакомиться с вами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, вы хорошая команда, и вы знаете, мы можем сделать что-то.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И да, я также попробую провести день, используя это немного больше.
[Jonathan Archer] Потрясающе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, но, кстати, вы пробовали другие проекты, которые я вам рассказал, BB и так далее?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] I can tell which I'm using right now.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] CC Switch, BB, OpenChamber, CCGUI.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] You're not familiar with any, right?
[Jonathan Archer] No, I'm not.
[Memo Guleryuz] No.
[Memo Guleryuz] These are competitions that you found?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет, я использую ваши компетенты, это типа компетентов, но вы должны быть осознанными.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто агрегаторы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Конечно, если вы позиционируете себя как харлес, маркетинг и так далее, позиционирование очень важно, но что я вам сказал, это просто агрегаторы харлеса.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, мы посмотрим.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо, спасибо.

---

**Claude:**

{"lang":"mixed","one_line":"dev had an intro/partnership call with the OpenLLM team (Memo Guleryuz, Jonathan Archer), a multi-LLM harness/aggregator startup raising $1M: he offered to organize an online meetup, review their deck and help with investor and distribution intros.","participants":[{"name":"[ИМЯ] [ФАМИЛИЯ]","role":"our-side","channel":"microphone"},{"name":"Memo Guleryuz","role":"lead","channel":"speaker"},{"name":"Jonathan Archer","role":"lead","channel":"speaker"}],"commitments":[{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Organize an online meetup (post on Luma, bring 30-50 engineers, record a YouTube video afterwards), starting online first, possibly next week","due":"next week","quote":"Я могу сделать митап, может быть, в следующей неделе."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Bring a guest with fundraising/incubator experience to interview the OpenLLM team at the meetup","due":"","quote":"Я также принесу потрясающего гостя, который может вас интервьюировать, и этот гость имеет опыт в фондозировании."},{"owner":"Jonathan Archer","what":"Send their pitch deck to dev","due":"","quote":"Хорошо, давайте сделаем это онлайн, и потом я передам вам мой дек, наш дек, сейчас для того, чтобы вы посмотрели."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Prepare materials for his engineers about OpenLLM and get the team's approval before sending","due":"","quote":"Мне нужна ваша дека, и потом я сделаю некоторые материалы, которые я отправлю моим инженерам, и вы должны их принять"},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Ask the Corgi (SF collaboration that runs YC meetups) people to use their network to draw YC folks to the meetup","due":"","quote":"Мы можем также пытаться разговаривать с этими парнями, которые создали YC Guys."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Think about intros to people who could help and try using the product more himself","due":"","quote":"Думаю, с кем я могу вас представить."},{"owner":"Jonathan Archer","what":"Connect with another consultant who will support OpenLLM (needs a follow-up call)","due":"","quote":"Он тоже начнет поддерживать OpenLLM, нам просто нужно получить последовательный звонок с ним."}],"facts":[{"fact":"OpenLLM positions itself as a meta-layer/open layer over all AI coding tools (Claude, Codex, Kimi, Grok, Cursor, etc.) with API key support and local mode","quote":"Вы можете соединить Кодекс, Кимми, Грок, Керсер, Мюз, а также принести API-ключи."},{"fact":"They are building a Teams offering: manager dashboard with usage visibility, shared memory across teams, and an integrations marketplace (public and private) applied to all team members","quote":"Команда будет этой дашборд, где манажеры могут видеть всю использованность, могут быть соединенные памяти между командами."},{"fact":"Desktop app is planned to simplify the currently heavy developer login process","quote":"но с аппой для десктопа он будет намного более стремленным"},{"fact":"Team is currently raising $1M, with the push over the next 2 weeks and first 2 weeks of November","quote":"мы поднимаем 1 миллион, и я думаю, что это очень действительно."},{"fact":"Very little cash: only small salaries paid to Memo and a UI/UX engineer; OpenLLM Pro support pricing about $500/month","quote":"наши цены на поддержку OpenLLM довольно низкие, может быть, 500 долларов в месяц."},{"fact":"Team is returning to LatAm and is available to talk to investors until Sunday","quote":"мы полностью доступны поговорить с инвесторами до воскресенья"},{"fact":"Memo's marketplace will support public and private marketplaces where dev could list his MCP","quote":"мы поддержим даже публичные и приватные рынки, так что мы можем проверить вас и сказать, что это оператор"},{"fact":"They are already engaging consultants as distribution partners, one of whom will push OpenLLM to his clients","quote":"он сказал, что он начнет пытаться пустить OpenLLM к его клиентам."}],"objections":[{"objection":"dev: investors ask about MOAT now; harnesses are hard to monetize and have low usage since only engineers use them (though still investable)","by":"[ИМЯ] [ФАМИЛИЯ]","quote":"Хармония немного трудно монетизировать."},{"objection":"dev: direct sales to corporations are hard and painful because they require a dedicated integration department; integrators are the alternative channel","quote":"Прямо в корпорации всегда сложнее.","by":"[ИМЯ] [ФАМИЛИЯ]"},{"objection":"dev: the competitors he uses (CC Switch, BB, OpenChamber, CCGUI) are just harness aggregators, so positioning matters; the OpenLLM team was not familiar with them","by":"[ИМЯ] [ФАМИЛИЯ]","quote":"Это просто агрегаторы."}],"alpha":[{"signal":"Investors currently ask only about moat, but many are willing to invest in harness/feature plays; OpenLLM needs a deck with traction, tracking slides and market size","why":"Frames how to pitch the company and what dev needs from the deck to represent them to investors","quote":"Однако, что я вижу сейчас, множество инвесторов готовы инвестировать в характеристики, так что вы в порядке."},{"signal":"Distribution via integrators/consultants and incubators is a route to B2B; dev met an Anthropic integrator (Mehdi) who is a potential customer/channel","why":"Concrete intro path for OpenLLM and validates their consultant-partner strategy","quote":"Он антропический интегратор, но не только антропический."},{"signal":"AI Engineer Code Summit, Nov 10-12 in SF, application-only; Cerebral Valley is another events hub","why":"Timing for in-person investor/partner contact; Jonathan was unaware of the conference","quote":"Это будет между 10 и 12 ноября."},{"signal":"dev may join the OpenLLM team later to bring their price/revenue; he estimates $1-2M revenue is realistic depending on pricing","why":"Potential role for dev and a revenue benchmark against their current tiny $500/mo pricing","quote":"И может быть, я не знаю, может быть позже, вы можете добавить меня в вашу команду, в случае, если я могу принести вашу цену, окей?"},{"signal":"A recorded online meetup with a fundraising-experienced guest doubles as a demo video the team can reuse in their fundraising","why":"Cheap, low-cost way to give OpenLLM investor-facing content while dev gains content for his channel","quote":"И потом, это видео, YouTube, Вы можете использовать это позже для вашего фонаря, потому что это будет замечательным демо-звуком."}]}
