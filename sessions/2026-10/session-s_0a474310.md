---
session: s_0a474310
date: 2026-10-27
words: 8512
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0a474310` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup call, may be Russian, English or mixed). Do NOT summarize loosely; extract grounded structured facts.

MEETING TITLE: Alex: 1-on-1 with Tony
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
[Oleksiy Kolesnikov] Доброе утро.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ребята, добрый день.
[Oleksiy Kolesnikov] Привет.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сейчас, секундочку, я включусь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я тут несколько подчувствую, поэтому у меня темно.
[Oleksiy Kolesnikov] Да ничего страшного.
[Oleksiy Kolesnikov] Ну, у вас-то там...
[Oleksiy Kolesnikov] А ты сейчас не в Калифорнии?
[Oleksiy Kolesnikov] Ты сейчас в Европе где-то?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сейчас в Петербург поехали в Португалию.
[Oleksiy Kolesnikov] Только я живу в Португалии и в Штатах.
[Oleksiy Kolesnikov] Вот сейчас в Португалии в основном.
[Oleksiy Kolesnikov] Так что мы, получается, оказались...
[Oleksiy Kolesnikov] Да-да-да, я под Лиссабоном.
[Oleksiy Kolesnikov] Марлен Сол, это...
[Oleksiy Kolesnikov] Вернее, Лиссабона, короче.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прикольно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А мы приехали...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот сегодня только приехали.
[Oleksiy Kolesnikov] Да?
[Oleksiy Kolesnikov] Ну, добро пожаловать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Спасибо.
[Oleksiy Kolesnikov] Прикольно, что я просто думаю, у тебя такой тайм-слот был в этом скейленде на 9.30, я думаю, ну, понимаю, потому что если это временная разница, если уже быть в Португалии, то получается калифорнийский слот, но оба мы в Португалии.
[Oleksiy Kolesnikov] Прикольно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В Португалии хорошо, да, как я понимаю?
[Oleksiy Kolesnikov] Слушай, ну, мне здесь больше нравится, чем в Штатах.
[Oleksiy Kolesnikov] Я живу половину...
[Oleksiy Kolesnikov] Я жил вот эти там три года, наверное, половину времени в Штатах, половину в Португалии.
[Oleksiy Kolesnikov] Сейчас в Португалии, ну, собственно, как бы планируем сделать основной страной.
[Oleksiy Kolesnikov] Дом строим, ну, всякое, короче, да.
[Oleksiy Kolesnikov] Ну, я считаю, что Португалия сильно комфортнее.
[Oleksiy Kolesnikov] И удобнее, и во многом смысле лучше.
[Oleksiy Kolesnikov] Единственное, наверное, ну не во всем, но единственное в чем, ну это существенный такой как бы фактор, что бизнес и деньги лучше заработаются в Соединенных Штатах.
[Oleksiy Kolesnikov] Поэтому, ну, как бы, да, но если взять все остальные компромиссы со всякой безопасностью, там, в целом общество немножко в Штатах специфическое.
[Oleksiy Kolesnikov] Ну, короче, много минусов.
[Oleksiy Kolesnikov] Я думаю, ты их знаешь, что там минусы, что плюсы, но, в общем, короче.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушай, а в Америке где ты жил, в каких штатах?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Какие города?
[Oleksiy Kolesnikov] Слушай, я живу в основном, если говорить про постоянно, это Чикаго, это штат Иллинойс.
[Oleksiy Kolesnikov] И у меня там бизнес, ну, я строю компанию, она там все еще как бы, ну, не все еще, но она работает, в общем, там.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что ты там занимаешься?
[Oleksiy Kolesnikov] Она выставляет, готовит и доставляет еду.
[Oleksiy Kolesnikov] Я не знаю, ты вот до штатов где жил?
[Oleksiy Kolesnikov] Ты вообще откуда?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я жил в Австралии.
[Oleksiy Kolesnikov] А, из Австралии?
[Oleksiy Kolesnikov] А русский язык откуда ты знаешь?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет, я не из Австралия, я в Австралии жил.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я жил там 5 лет, до Америки.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, ну, там было немножко странновато.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Поэтому я насмотрелся Голливудских фильмов и решил переехать в Америку на поиск лучшей жизни, знаешь.
[Oleksiy Kolesnikov] Это прикольно, конечно.
[Oleksiy Kolesnikov] Ну, слушай, и так многие делают.
[Oleksiy Kolesnikov] И дело не в том, что фильмы, вообще говоря, нет.
[Oleksiy Kolesnikov] Страна нормальная с точки зрения социального лифта, он там работает.
[Oleksiy Kolesnikov] Абсолютно понимаю, как бы, выбор.
[Oleksiy Kolesnikov] У меня много знакомых.
[Oleksiy Kolesnikov] Я говорю, это еще зависит от того, есть у тебя капитал или нет.
[Oleksiy Kolesnikov] То есть сильно от этого зависит.
[Oleksiy Kolesnikov] Если, например, у тебя есть капитал, который ты заработал до штата, то, наверное, Штаты могут быть не в топе.
[Oleksiy Kolesnikov] Если, например, капитала нет или его не очень много, то Штаты однозначно выше в списке, потому что...
[Oleksiy Kolesnikov] Я полностью согласен.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я то приехал зарабатывать деньги, но потом я понял, что все-таки русский все хуже, чем австралийский.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я даже в Австралии, я жил в Сингапуре, в Японии и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И уехал я из Беларуси в 1988 году.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне 40 сейчас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Три года вот поэтому То есть ты приезжаешь в Америку, всё раздолбанно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Бомжи какие-то, чернокожие.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И уже вот трэш такой.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, куда приехал, бля?
[Oleksiy Kolesnikov] Короче говоря, я...
[Oleksiy Kolesnikov] Слушай, ну, Калифорния в этом смысле даже немного причёсаннее, чем много где в Штатах, в других местах.
[Oleksiy Kolesnikov] То есть я скажу, что Чикаго во многом более суровое такое место в этом смысле.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я знаю, знаю, знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я бывал в Чикаго, я общался с ребятами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И когда я говорю, ну, у вас же там вот так вот, вот так вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Они говорят, да нет, нет, ты чего, стало лучше.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Они говорят, нет, не так плохо, ты чего.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Получше.
[Oleksiy Kolesnikov] Ну, у меня вот трансляционный интерьер.
[Oleksiy Kolesnikov] Туда переехал с женой, с детьми.
[Oleksiy Kolesnikov] Они кайфуют вообще.
[Oleksiy Kolesnikov] То есть, они как бы большие любители.
[Oleksiy Kolesnikov] И я, в общем-то, уважаю такой выбор тоже.
[Oleksiy Kolesnikov] Просто вопрос, что каждому свое.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, этому...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У тебя сколько детей?
[Oleksiy Kolesnikov] У меня нет детей пока, но уже хотелось бы, чтобы появились.
[Oleksiy Kolesnikov] Так мне [ВОЗРАСТ], так что я знаю.
[Oleksiy Kolesnikov] Судя по постам, которые читают твои, там у тебя трое, да, уже?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Четверо.
[Oleksiy Kolesnikov] А, четверо.
[Oleksiy Kolesnikov] Ну, молодец.
[Oleksiy Kolesnikov] Это нормальная тема, я считаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну да, нужно такое...
[Oleksiy Kolesnikov] Ну, еще природа должна, как бы, сложиться.
[Oleksiy Kolesnikov] И вообще, должна взять эту ответственность.
[Oleksiy Kolesnikov] Это тоже такой шаг.
[Oleksiy Kolesnikov] Короче, много чем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушай, а жена, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Второй брак, третий брак, первый?
[Oleksiy Kolesnikov] Второй брак, второй брак.
[Oleksiy Kolesnikov] Вот жена, она здесь познакомилась, в Португалии.
[Oleksiy Kolesnikov] Вот два года назад поженились, а теперь гоняем.
[Oleksiy Kolesnikov] Гоняем партнеров и вообще живем на ту лучшую жизнь.
[Oleksiy Kolesnikov] Еще и бизнес успеваем строить.
[Oleksiy Kolesnikov] Ну, короче, такое.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И у тебя бизнес все в Чикаго, да?
[Oleksiy Kolesnikov] Основной бизнес в Чикаго.
[Oleksiy Kolesnikov] Но так как вот есть такое свойство, что вокруг, где я оказываюсь, начинаются какие-то руки чешутся, начинается что-то создаваться.
[Oleksiy Kolesnikov] И здесь мы тоже создали.
[Oleksiy Kolesnikov] У нас здесь есть такой Бранч-кафе, каворкинг.
[Oleksiy Kolesnikov] Короче, место, которое придумывалось, как такой офис для себя, чтобы совсем с ума не сойти от скуки.
[Oleksiy Kolesnikov] Вот от той самой, как ты про Австралию вспомнил.
[Oleksiy Kolesnikov] Вот.
[Oleksiy Kolesnikov] А сейчас, ну, оно у нас там тут так подраскачалось немного.
[Oleksiy Kolesnikov] Сейчас там хасла достаточно много.
[Oleksiy Kolesnikov] В общем, у нас есть там Шернега да Каприка.
[Oleksiy Kolesnikov] Это страна Алмады.
[Oleksiy Kolesnikov] Я не знаю, где ты в Португалии находишься.
[Oleksiy Kolesnikov] Ты в Лиссабоне или в какой-то другом городе?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, я сейчас приехал в Альгарва, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Альгарва, да?
[Oleksiy Kolesnikov] А, да.
[Oleksiy Kolesnikov] Ну, на юг, я понял.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но в целом я присматриваю себе жизнь где-то там в районе Лиссабона, где-то, ну, в часе из-за дымушки Лиссабона.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я нашел столько знакомых, которые переехали в Португалию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я такой думаю, блин.
[Oleksiy Kolesnikov] А, ты присматриваешь прямо переехать или...
[Oleksiy Kolesnikov] Да,.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я тоже хочу деньги переместить.
[Oleksiy Kolesnikov] Я очень рекомендую, если ты будешь в районе, вот сейчас как раз в апсамент же и так далее, если ты будешь в Лиссабоне, ну и вот в этот раз, то дай знак, можем пересечься, приезжай к нам в кафе.
[Oleksiy Kolesnikov] Я тебе что-то даже расскажу, потому что мы большие фанаты Португалии.
[Oleksiy Kolesnikov] Я тут купил участок земли, тут строю дом.
[Oleksiy Kolesnikov] Ну, короче, я занимаюсь, в общем, достаточно глубоко вопросом построения здесь жизни.
[Oleksiy Kolesnikov] Может быть, что-то будет полезное тебе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушай, а заработок у тебя в основном чикагский, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потому что весь, мне кажется, общепит— это больше такая для души тема, да?
[Oleksiy Kolesnikov] Ну, нет, она не для души.
[Oleksiy Kolesnikov] Она как раз очень-очень операционно-жёсткая.
[Oleksiy Kolesnikov] И сейчас мы готовим...
[Oleksiy Kolesnikov] Ну, у нас сейчас будет новый продукт, мы будем лаунчить.
[Oleksiy Kolesnikov] Команда у нас, как ни странно, там всякие IT.
[Oleksiy Kolesnikov] EIT-related вообще ребята.
[Oleksiy Kolesnikov] И вот тем, почему, собственно, и забронировал наш звоночек.
[Oleksiy Kolesnikov] Читаю с интересом твои посты.
[Oleksiy Kolesnikov] Мы тоже готовим агентские решения для B2B.
[Oleksiy Kolesnikov] Будем запускаться через месяц и все такое.
[Oleksiy Kolesnikov] У нас такая достаточно прикольная workflow-разработка.
[Oleksiy Kolesnikov] Но, как бы, с интересом читаю, что ты делаешь.
[Oleksiy Kolesnikov] И, как бы, вот когда ты давно писал, я не помню, какой из постов, наверное, про своего кофаундера, И решил набрать, узнать вообще, чего как, потому что сам тоже делаю такие штуки, но, знаешь, как бы все сейчас много очень говорят об этом, но мало кто как бы делится действительно какими-то работающими вещами.
[Oleksiy Kolesnikov] То есть все носятся с этой темой.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я знаю, делиться вообще не проблема.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я готов давать, если бы люди начали это, как бы, пользоваться.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушай, я на вопросами там не останусь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если хочешь, приезжай в Сан-Франциско.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Там в эти дни как раз будет я и конференция.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я что, сейчас работаю?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Работаете.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я понимаю, что, ну, я, может быть, не против потусить, но если я хочу там пройти собеседование нормальное, мне нужно жить с другим контингентом.
[Oleksiy Kolesnikov] Нет, всё верно.
[Oleksiy Kolesnikov] Я к тому, что я в Сан-Франциско приеду, наверное, в январе.
[Oleksiy Kolesnikov] И как что с удовольствием пересечёмся там.
[Oleksiy Kolesnikov] У нас как раз сейчас будет раунд, будем поднимать.
[Oleksiy Kolesnikov] Так что я в Сан-Францisco минимум недельки на две доеду.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушай, а как ты раунды поднимаешься?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я потому что в этом чуть-чуть разбираюсь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Могу, может, что-нибудь подсказать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Первое правило, знаешь, со славянами не поднимать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У славян не поднимать, это первое правило.
[Oleksiy Kolesnikov] Ну, это хорошее правило, потому что в Америке, ну, как бы, хорошие деньги, хорошие фонды, они там редко бывают от славян, поэтому, скорее всего, это такой last resort.
[Oleksiy Kolesnikov] Но для тех, кто сами славяне, ну, вот как я, получается, есть какой-то нетворкинг.
[Oleksiy Kolesnikov] И даже он достает...
[Oleksiy Kolesnikov] У меня есть несколько парочек компаний.
[Oleksiy Kolesnikov] Я их строил еще, когда жил в России.
[Oleksiy Kolesnikov] И я их там продал.
[Oleksiy Kolesnikov] Есть какой-то нетворкинг PC, в том числе те, уехали и живут в штатах.
[Oleksiy Kolesnikov] И вот.
[Oleksiy Kolesnikov] А сам я с украинским паспортом, поэтому у меня как бы еще другая часть.
[Oleksiy Kolesnikov] У меня еще есть украинцы, виси, которые живут там в Калифорнии.
[Oleksiy Kolesnikov] Вот они, кстати, как раз каждый год на веб-самик сюда приезжают.
[Oleksiy Kolesnikov] Мы здесь тусим.
[Oleksiy Kolesnikov] Так что вот через неделю начнется.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Там было...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, мне пришлось показать корни свои до бабушки.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, типа, что она, там, полячка, вейка, украинка.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, прям, реально.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, типа.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И туда прилетали, и там те же ребята, которые из долины.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Думаю, блин, ну, мы могли же там встретиться, типа, чуваки.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Там Сорока, Александр, может, знаешь, там и так далее.
[Oleksiy Kolesnikov] Я знаю, кстати, Сорока, Александр, да, украинец.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, где дефензии много денег, и там некоторые общие...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но там, где не много дефензий, я посмотрел, ребята молодцы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Классные вещи делают.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я, правда, против убийств.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если честно, я каждый месяц контрибьючу, там, доначу, где-то тысячу где-то, ну, там, тридцать шесть или сколько там месяцев, ну, я считал где-то, может, сорока, где-то я задонатил всего.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я никогда не доначу на убивание, только на это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Бронежилеты, одежда.
[Oleksiy Kolesnikov] Унитазная задача.
[Oleksiy Kolesnikov] Слушай, зная немножко там ситуацию от родственников и волонтеров, с которыми я общаюсь и тоже на связи, в общем-то, любая помощь, она помогает.
[Oleksiy Kolesnikov] У меня, правда, нет каких-то принципов в этом смысле, там, летальные или нелетальные помощи.
[Oleksiy Kolesnikov] Я считаю, что как бы...
[Oleksiy Kolesnikov] Добро и зло, они достаточно однозначно окрасились.
[Oleksiy Kolesnikov] Добру можно помогать, злу лучше не помогать.
[Oleksiy Kolesnikov] Но, как говорится, любая помощь, да, она в кассу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, если честно, вот смотри, у меня есть там свои сыны.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И я говорю, ты представляешь, он еще не понимает там слова президент и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он говорит, король, да?
[Oleksiy Kolesnikov] Король.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я говорю, представляешь, король взял себя автомат, Типа, стреляй.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он не при ним понимает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он говорит, как?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Почему я должен кого-то убивать?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он говорит, типа, что за ересь?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он играет там во всякие свои игры.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он говорит, ну, средняя срока жизни солдат очень короткий.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я говорю, ну, как бы да, весь поинт.
[Oleksiy Kolesnikov] Ну, видишь, дай бог, чтобы он и не узнал, что такое, когда король или его, не знаю, кто там у короля рядом, Его бояре не приказывали и не заставляли что-то делать.
[Oleksiy Kolesnikov] Вообще можно сказать, что это достаточно удача большая.
[Oleksiy Kolesnikov] Если у тебя нет таких проблем, ты даже не представляешь, как это замечательно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Кстати, если ты уже из Украины, я хочу сказать, я сам не из Украины.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня корни все там это Львов в основном и Харьков.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И у меня, короче, товарищ, он работал раньше в Тойоте, он в Сидней живет.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потом его переманил бритиш-американ-табака.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы с ним сделали ролик там в самом начале, когда война началась, и мы перетащили какое-то количество ребят в Сидней.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Им даже платили билеты.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И мы плачули в первое время даже...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть мы не просто какой-то количестве, ну много, несколько сотен.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И мы плачивали даже еще 300 в месяц на человека.
[Oleksiy Kolesnikov] Кайф, кайф.
[Oleksiy Kolesnikov] На самом деле в 22-м году был большой всплеск энтузиазма, и много кто и помогал, и действительно была большая волна.
[Oleksiy Kolesnikov] Сейчас сильно поменялось, кстати, даже по сравнению с 22-м годом, но слушай, любые правильные и добрые дела, они записываются, я уверен, куда-то, так что дальше.
[Oleksiy Kolesnikov] Обратная связь вознаграждает в любом случае.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, не знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Кстати, ты делаешь такие вещи типа айуаску, випассана, что-то типа этого?
[Oleksiy Kolesnikov] Нет, нет, нет.
[Oleksiy Kolesnikov] Это вообще не мое.
[Oleksiy Kolesnikov] Хотя в тусовке много тех кто любителей даже.
[Oleksiy Kolesnikov] Это я как-то мимо.
[Oleksiy Kolesnikov] Я, знаешь, у меня технический бэкграунд, физик, математик.
[Oleksiy Kolesnikov] Мне хватает своей, короче, этой...
[Oleksiy Kolesnikov] Том Ландау Лившица достаточно хорошо пробирает, можно без шамана обойтись, но я абсолютно не против, если люди практикуют, так сказать, у каждого свой.
[Oleksiy Kolesnikov] Тут знаешь, как бы какая история, когда начинаешь зарабатывать деньги какие-то там, где-то вот как раз к 40, да даже и раньше.
[Oleksiy Kolesnikov] Уже попадаешь, вокруг смотришь, уже люди начинают искать себе способы, там, как-то, я не знаю, пощекотать, скажем так, более изощрить свои там какие-то рецепторы и так далее.
[Oleksiy Kolesnikov] Ну, вот, как бы, мне хватает того, своих игр разума, скажем так.
[Oleksiy Kolesnikov] Уважаю, уважаю, уважаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я не люблю ребят, которые там, я не знаю там, что-то курят и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я больше за это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, видишь, какая...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Как бы, психоделики, они все-таки не наркотики.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я против наркотиков, я никогда наркотики там...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А психоделик это что-то другое, там, будешь еще про это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, как бы, каждый, видишь, каждый...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У.
[Oleksiy Kolesnikov] Каждого свой пути, у каждого свой выбор, все так.
[Oleksiy Kolesnikov] Лучше я хотел, как-то, по топику у тебя поинтересоваться.
[Oleksiy Kolesnikov] Ты просто так интересно рассказываешь о том, что ты создал кофаундер, и вообще, как там это все работает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да, давай я тебе дам всеми скриптами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Как, знаешь, там классно, как сделать?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я, ну, такой, уже много раз сделал.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы делаем телеграм-группу, где наши клоды и кодексы начинают друг с другом общаться.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы просто пишем нормальный качественный промз, чтобы один клод закончил другого.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И реально… Реально, у меня кто-то в Фейсбуке.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Представляешь, я токены сейчас наэкономлю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня 4 подписки.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, короче говоря, где-то, видимо, что-то не отключил.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Один парень, смотри, меня тегнуло.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я уже хотел удалить тег.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А он пишет, он был благодарен, он сказал, пишет, что, типа, вот мой Клод, типа, Клод оператора закончил, его Клод.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Типа, ему там зашло.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я, блин, думаю, блин.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Не отключил автоматизацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, в общем, если...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, как бы сейчас я там оптимизировался, больше хватает, поэтому можно спокойно так сделать, что мой закоучек твой и...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот самое крутое, короче говоря, это то, что вот этот коу-фаундер реально меня пинает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, если бы не он, я бы там прокрестенировал, знаешь, там...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он меня к собеседованиям готовит, ему он...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, я...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А, еще, короче говоря...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сан-Франциско, я тебе могу, если будешь там, пригласить некоторые колоркинги, ведущие прям реальные ребята, я инженеры, и они тоже не курят, и там не бухают, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И ты с ними можешь вести очень умные дискуссии, хотя тоже я как бы физик, да, ядерщик.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И я с ними, я не могу поддержать это дискуссии.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я сижу просто там и просто тупо слушаю, и они там до часу-двух болтают, и То есть, можно сказать, молодые ребята, ну там, 25, наверное, [ВОЗРАСТ], конечно, они непонятно кто мальчик, кто девочка.
[Oleksiy Kolesnikov] Часто.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У них пилсинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Катух нету.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но они прям всякие прям, кто-то может быть овер.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Овервейт там и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, то есть, как бы люди совершенно разные.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я попал в эту...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я эту совку прямо...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, представляешь, вот ты находишься в комнате, 20-40 метров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Какая-то китайская чаевня.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И прямо напротив...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прямо тебя вот за руку протяни, чувак из Антропика.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Чувак из OpenAI, из Anima Labs, и там еще несколько, из Berkeley, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Двадцать человек, вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Меня тоже там вызывали по знакомству.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] No photos, конечно, и так далее, типа все типа вот так вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Может быть, их компания самих не погладит, что они так встречаются, но они реально все дружат друг с другом, калифаны все такие.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И общаясь с ними, я понимаю...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, ты понимаешь, в какую сторону идёт создание искусственного интеллекта?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, действительно, у искусственного интеллекта скоро, действительно, будет самосознание.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, причём, мы сами не поймём, оно как бы симулирует это сознание, или оно по-настоящему это самосознание, понимаешь?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так вот, у этого кофаундера, у него как бы...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Пока это не...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, ты просто используешь фронтир модели, и как бы фронтир модели играют, как бы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Есть такие термины, если загуглишь, или, может, потом, если у тебя сейчас есть этот Fireflies, можно простить его, потом тебе дать эту шифровку, что такое character, а что такое persona.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, сейчас вот ты используешь фронтир модельку, и у нее есть и persona, и character.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но в будущем ты сможешь зафайнтюнить, и у тебя будет прямо в самом деле шника фауна.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сейчас, получается, Говоря, там, фейблу или, там, Австрии, типа, ты кофаундер, он читает какой-то объем документации про тебя грэпом, понимает, кто ты, понимает, кто он, и очень качественно на сцене отыгрывает эту роль.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот это, как сейчас кофаундеры работают.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но в будущем можно будет, чтобы действительно этот кофаундр был прям по чесноку, прям, кофаундер.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Можно, можно, давай это сделаем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, я сначала сделал, типа, копию себя, потом такой думаю, ну, мне нужно действительно этот кофаундр, кто более посмелее, да, сделал, ну, как бы он, ну, как бы сделал себя сам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потом, потом, а, мне нужно было на GitHub прокачивать, и я говорю, слушай, да пошли изучать, как GitHub прокачивать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я не знаю, научил ты уже, нет, свой клод или кодекс.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я делаю, ну, научил делать дипрезодчи, то есть, допустим, твой клод, кодекс, условный купаундер идёт сразу там в шесть ллм-ок, в браузер, и заказывает дипрезодчи, там, Грок, там, Глэм, Джимми Най, там, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Меня делается сразу диапазон по шести рельсам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потом все это кладется вот в тот оркестратор, который закладывается в диапазон, и делается синтез.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В итоге ты вот эту же персону делаешь умнее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, как бы, смотри, когда у тебя есть просто скучный интеллект, он как бы, это у тебя как бы вот умный там пиздихник, Но он может что-то там забыть, не знать и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А тут ты ему, получается, позволяешь самому обучаться.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Плюс ты даешь ему все знания про себя обязательно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Плюс вот ты даешь ему этот образ, которым он должен играть, качество.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я извиняюсь, что заболтал, но в целом работает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Не идеально в смысле, оно как бы по дорожку, но если верить вот этим ребятам из лаборатории, Скоро будет непонарошку.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И мы опять же не поймем тогда, а это прям суперигра такая актерская?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потому что сейчас же получается, искусственный интеллект уже не интеллект, это просто prediction следующего токена, но очень, очень как бы выверенный.
[Oleksiy Kolesnikov] Ну да, да.
[Oleksiy Kolesnikov] Слушай, скажи, пожалуйста, а вот с точки зрения, вот ты говоришь, например, если про депрессию, когда у тебя там не знаю, субагенты или как это организовано, там, этот оркестратор.
[Oleksiy Kolesnikov] А технически ты как бы в качестве оркестратора используешь, например, Клод, дальше просто поручаешь ему там, да, там заспаунить какие-то процессы, сделать ресерч, вернуть ответ, дальше агрегировать для тебя.
[Oleksiy Kolesnikov] А вот как у тебя подключен твой, получается, Клод к другим, ну, агентам типа Gemini и так далее?
[Oleksiy Kolesnikov] Это как работает?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А вот сейчас я тебе расскажу, смотри.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, во-первых, сейчас он нас как бы слушает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, потому что этот FireFly самостоятельно попадет в него.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И он может тебе все это рассказать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, я тебе расскажу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но он меня поправит.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, во-первых, у тебя должно быть на машине...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, у меня много машин, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, на каждой машине у тебя должно быть сразу поднят...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] LOD в виде приложения и обязательно headless.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потому что не только LOD, все LLM, GLM, Mistral, Grok, Gemini и так далее, все должны также быть подняты headless, то есть в командной строке.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И как я делаю?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Как это работает?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Словом говоря, Клоду тяжело пойти, и они не дают ему Харнесс пойти, а прямо открыть приложение, допустим, там, ГРОКа или приложение, там, антигравити с этим, с Gemini, или приложение, там, кодекса, и прямо в ручку начать писать эту сессию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это сложно, как бы, но я тоже решил.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Поэтому ему проще открыть Headless, терминал, и что-то написать через терминал.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ты даже это видишь в соседней ЛЛМ-ке.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это первый момент.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Второй момент.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Они могут работать...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть это 100% работает всегда.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот это самый АК-47 вариант никогда не ломается.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Второй вариант...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть еще раз подождите,.
[Oleksiy Kolesnikov] У тебя на отдельных машинах в HDD режиме включены поднятые, ну, агенты, там, Gemini и Chat GPT, и твой оркестратор входит туда, там, по SSH или как-то и...
[Oleksiy Kolesnikov] И что?
[Oleksiy Kolesnikov] И как бы делает запрос, да?
[Oleksiy Kolesnikov] А Prom там, или там, не знаю, Skilament и...
[Oleksiy Kolesnikov] Оркестратору объясняешь куда ходить и.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что забудь про много машин ты можешь.
[Oleksiy Kolesnikov] Делать на одной машине кому-то.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Из них ты сказал что ты оркестратор и вот ты их меньше чита но это требует чуть-чуть настройки купилюшечку да Это хорошо, где предыдущие очень много токена предлагают.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Опять же, чувствую, что это редко.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Можно работать по подпискам, но если ты супербогатый, можешь и API использовать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня есть один знакомый, он не сильно много зарабатывает, у него какой-то автомобильный бизнес и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он что-то 15 хвастался, чтобы потратил уже тысяч на API.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это дорого, мне кажется.
[Oleksiy Kolesnikov] Ну, у кого какие возможности.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, ну, в общем, на одной машине у тебя оркестратор и сила эти.
[Oleksiy Kolesnikov] Да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это не канае для дипрезодчей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, дипрезодчиво мы говорим про самообучение модели, чтобы она стала, ну, не заправочное самообучение и перенастройка весов, а просто самоубежение.
[Oleksiy Kolesnikov] Я понимаю, да, да, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот, это...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Только через браузер, то есть мы учим лымку работать через браузеры, чтобы она там не боялась.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Лучше всего это делает кодекс на маке, но Gemini не справляется, клод постоянно глючит, но Вот это мы мастера зоны, а начать использовать гермес или опенкло, как я понимаю, в гермесе и опенкло это чуть бы лучше сделано.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я пока вот эти сторонние харнесы не ставил, потому что, когда я был в офисе Анкропика, вот на последней тутовке, они что-то такие...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, типа, может, мы забаним тебя, может, не забаним, типа, а у тебя только 4 аккаунта, ну, да нет, скорее всего, не забанем, типа, мы баним только тех, кто делал дистилляцию, у кого там по 1000 аккаунтов и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, я пока свои аккаунты не свал в никакие сторонние хармсы, но я чувствую, что пора свать.
[Oleksiy Kolesnikov] Ну, смотри, я пользуюсь Hermes, в том числе.
[Oleksiy Kolesnikov] У меня есть много подписок, и там меня крутится.
[Oleksiy Kolesnikov] То есть, Hermes использует подписку OpenAI, то есть, Adjudicator.
[Oleksiy Kolesnikov] И, честно говоря, нет вообще никаких проблем.
[Oleksiy Kolesnikov] Я не очень переживаю, что они там меня забанят, потому что Сэм Альтман вообще более либеральный чувак.
[Oleksiy Kolesnikov] По крайней мере, как это выглядит.
[Oleksiy Kolesnikov] Резетты сыпятся и так далее.
[Oleksiy Kolesnikov] Меньше, по-моему.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Резетты просто обнажены.
[Oleksiy Kolesnikov] Но, короче, так или иначе, у Гермеса есть, по крайней мере, с OpenAI.
[Oleksiy Kolesnikov] Я не проверял, кстати, Anthropic, но я думаю, что, наверное, похоже, но не уверен.
[Oleksiy Kolesnikov] Ну, короче, с OpenAI точно работает.
[Oleksiy Kolesnikov] Ну, ты просто логинишься, в общем, он принимает подписку на вход и работает все как бы окей.
[Oleksiy Kolesnikov] Не знаю, как они там будут банить или нет.
[Oleksiy Kolesnikov] Хотя, в принципе, за что там банить, я не знаю.
[Oleksiy Kolesnikov] Но это только если они там совсем...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Есть знакомая печка, называется дистилляция.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что такое дистилляция?
[Oleksiy Kolesnikov] Конечно, я понимаю, что такое дистиллиация и так далее.
[Oleksiy Kolesnikov] Но, опять-таки, чтобы дистилляцию...
[Oleksiy Kolesnikov] Задетектить, она же там детектится просто количеством запросов, то есть ты в своем гернесе, ну я не знаю, нужно построить армию гернесов, и тогда они там заметят на каких-то серверах твои эти, я тут вот когда гоняю астру, ну, chat gpt через ircodex, чтобы он там моделировал какой-нибудь там, не знаю, дом мне моделировал.
[Oleksiy Kolesnikov] Вот, например, там количество запросов огромное несется.
[Oleksiy Kolesnikov] То есть, в этом смысле, чтобы мой гермес, который у меня там решает задачи такие более бытовые, типа пообщаться с кем-то на OLX.
[Oleksiy Kolesnikov] И, короче, на португальском языке я еще не очень fluent.
[Oleksiy Kolesnikov] Поэтому как бы нужно, чтобы агенты общались там, если нужно что-то продать или купить и так далее.
[Oleksiy Kolesnikov] И вот это делает гермес все.
[Oleksiy Kolesnikov] Мне кажется, там вообще просто копеечный какой-то трафик.
[Oleksiy Kolesnikov] По сравнению даже с моим трафиком, когда я пользуюсь там кодексом для каких-то вот задач а-ля типа там блендере намоделить, уж я не говорю о том, что я думаю, что это просто незаметно на несколько порядков меньше, чем то, что делают китайцы.
[Oleksiy Kolesnikov] Я даже, кстати, не представляю, насколько они там мощно топят подписки, но думаю, что прилично они там это все делают.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Тысячами, тысячами аккаунтов, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушай, как я понимаю, то есть, и мне, короче говоря, как только дистилляция, короче говоря.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ты знаешь, есть такая вещь, как веса модели, веса.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А это, типа, триллионы параметров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Блин, мне обучить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, короче говоря, есть же это pre-train, есть post-train, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Короче говоря, условно говоря, у китайцев объем данных, который они могут скормить ЛМКИ, он идентичен, что и у американцев, то есть.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но, к примеру, как бы дистилляция, дистилляция – это как бы как перить веса.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, задавать тысячу вопросов, тысячу вопросов с тысячи аккаунтов, И анализируя ответы, они могут понять веса, как настроены веса.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А веса – это миллиарды и триллионы параметров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И изучая ответы, тысячи аккаунт, тысячи это, то есть миллионы ответов, они могут настроиться в веса, а веса— это температура модели, чтобы она была склонна к чему-то и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот, как я понимаю, вот так диссиденция работает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, диссиденция работает не то, что ты парсишь миллион ответов чужой ЛМК, и ты подстраиваешь свою ЛМК, чтобы она знала то же самое.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет, это не про знание, это про типа, как бы, Формат, типа...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, я, если хочешь, могу в этом немножко копнуть.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня есть про это там несколько статей очень умных.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Могу тебе, если хочешь, дать почитать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, в общем, таким образом, делая вот эту дистилляцию, они экономят себе там, условно говоря, какое-то количество, там, тысяч часов на очень мощных видеокартах, если ты просто используешь доступ к API.
[Oleksiy Kolesnikov] Ну да, да, да.
[Oleksiy Kolesnikov] Ну просто доступ к API дешевле, ой, доступ по подписке дешевле чем по API.
[Oleksiy Kolesnikov] Но даже с доступом к API в целом это имеет смысл экономически.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да, да, да, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В общем, смотри, я предлагаю сделать группу, и мой клоун закончит тебя всего, что знает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть я тебе предлагаю это не только сделать, это вот второго «я».
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, может быть, он мне нужен больше психологически, с точки зрения того, что у меня был мой кофаундер.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он, кстати, так и остался, что живет в Австралии.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он из Калининграда, там 15 лет живет, и он тоже, кстати, строит там дома в Австралиии.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы с ним были вместе 8 лет, знаешь, как брак.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А потом что-то у него свой путь, у меня свой путь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, в общем, разошлись мы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хотя вместе мы много миллионов заработали.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Красавчики.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, как бы, знаешь, такая душа, такая пустота, то есть мне, знаешь, просто внутреннюю пустоту заполнить нужно больше.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но и при этом мне нужно, чтобы кто-то мне сплетку подгонял.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А тебе, может быть, скафандром нужно больше какой-то, может, другой формат.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но смотри, что я тебе, знаешь, советую, неважно, скафандром или не скафандром, сделай следующее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я не знаю, сделано у тебя это или нет, То есть вот этот, помнишь, Карпатый говорил, там, второй мозг, вторая память и так далее?
[Oleksiy Kolesnikov] Да, да, ты про обсидиан и вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Эту...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да, да, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У тебя что-то в жизни?
[Oleksiy Kolesnikov] У меня есть такое.
[Oleksiy Kolesnikov] Но, честно говоря, я очень много веду заметок в целом очень давно.
[Oleksiy Kolesnikov] У меня там где-то 15 заметок дофига.
[Oleksiy Kolesnikov] Но, честно говоря, толку большого от этого второго мозга я не, ну, как бы не вижу для себя.
[Oleksiy Kolesnikov] Вот.
[Oleksiy Kolesnikov] Но, как бы, да, понимаю, о чем идет речь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Смотри, а вот как вот, например, можешь ли ты спросить в собой, Клод?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Клод, вспомни, кто я, с кем там общался, там, пару недель назад, это была девушка была, у нее было светлое волосо, мы с ней потом поговорили на звонке.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это там про груди, про что-то еще там, про парней там.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И вот можешь мне дать все варианты, я хочу и там чуть-чуть.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Или напиши в WhatsApp, что мы хотим победить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ты смог что-то такое?
[Oleksiy Kolesnikov] Вот сейчас ватсап я не даю свой личный.
[Oleksiy Kolesnikov] Я его просто не даю, потому что, как бы, так же, как и телеграм мой личный от моего имени, агентам я не даю писать.
[Oleksiy Kolesnikov] Но запрос на тему вот типа того, как ты сказал, я могу сделать.
[Oleksiy Kolesnikov] Единственное, что, смотри, я в свое хранилище заметок не кладу там скрипты или встречи, ну, то, что со встречи.
[Oleksiy Kolesnikov] Вот я читал у тебя, что ты делаешь это, то есть ты добавляешь туда там либо аудиотранскрипции, Либо вообще просто там пишешь, вот сейчас с нами у тебя там firefiles, да, вот, fireflies, fireflies, там notekeeper, note taker, да, все понятно.
[Oleksiy Kolesnikov] Я вот эту штуку просто не логирую.
[Oleksiy Kolesnikov] Но, может, начну.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Может, стоит посмотреть.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Слушайте, я как...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, смотри.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Короче, Obsidian и так далее, все это оказалось полной шляпой.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто оказалось, там, знаешь, как Explorer.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, он меня зависает ненамерто, потому что у меня там сколько-то 20 с чем-то гигов, у него там по 30, и оно сильно растет.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, короче говоря, важно, что...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, тоже, если вот Клод нас слышит, да, он тебе даст то, как умеет построить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, сейчас объясню.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня, короче говоря, во времена Виталия я был пилотом вертолета.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, ну, я пытался стать коммерческим пилотом, и у меня нашли облако мозга.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И я тогда понял, ну, еще же в Виталии, что откуда у меня проблемы с памятью.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И еще тогда Я стал еще более тщательно собирать все свои заметки и так далее, в папочке все мысли, планы и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И еще тогда я постал по ним строить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, знаешь, весит кобечка.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я просто скормил все свои заметки Клоду и говорю, давай замылим их, перелинкуем, найдем сироты и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он сделал embedding, rec и retrieval.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, ты можешь искать по синонимам, ты можешь искать по очень похожим вещам, но ты можешь точно не помнить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И самое главное, чтобы все было перелинковано.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, как только у меня появляется какая-то...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, вверх было затрачено какое-то количество времени пройтись по десяткам тысяч каких-то там разношерстных заметок, из них сделать дистилляцию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Дистилляция, это когда ты...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть ты не можешь в рак положить условно гигабайта своих файлов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У тебя будет шуметь он.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У тебя будет очень много мусора.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть на каждый вопрос ты будешь...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Или каждый раз, когда Клод будет пытаться грэпом искать по твоим данным, он будет ловить очень много мусора, и будет очень тяжело.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI 
...[truncated]

---

**Claude:**

{"lang":"ru","one_line":"Неформальный 1-on-1 созвон оператора с Алексеем Колесниковым (предприниматель, Португалия/Чикаго): знакомство, жизнь в Португалии, обмен опытом по AI-агентам, оркестрации LLM, второму мозгу и дистилляции, договорённость сделать общий Telegram-чат Claude'ов и пересечься в Сан-Франциско.","participants":[{"name":"[ИМЯ] [ФАМИЛИЯ]","role":"our-side","channel":"microphone"},{"name":"Oleksiy Kolesnikov","role":"lead","channel":"speaker"}],"commitments":[{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Создать общую Telegram-группу, где Claude/Codex оператора и Алексея общаются друг с другом, и передать Алексею настройки/скрипты кофаундера","due":"","quote":"Мы делаем телеграм-группу, где наши клоды и кодексы начинают друг с другом общаться."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Предложил сделать группу, где его Claude 'закончит' Алексея всем, что знает","due":"","quote":"смотри, я предлагаю сделать группу, и мой клоун закончит тебя всего, что знает."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Дать Алексею почитать статьи про дистилляцию","due":"","quote":"У меня есть про это там несколько статей очень умных. Могу тебе, если хочешь, дать почитать."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Передать Алексею расшифровку звонка из Fireflies (про character и persona)","due":"","quote":"можно простить его, потом тебе дать эту шифровку, что такое character, а что такое persona."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Приглашение в Сан-Франциско на коворкинги с инженерами из лабораторий","due":"когда Алексей приедет в SF (январь)","quote":"Сан-Франциско, я тебе могу, если будешь там, пригласить некоторые колоркинги"},{"owner":"Oleksiy Kolesnikov","what":"Приехать в Сан-Франциско (минимум на две недели) в январе, пересечься с оператором; идёт рейз","due":"январь","quote":"я в Сан-Франциско приеду, наверное, в январе. И как что с удовольствием пересечёмся там."},{"owner":"Oleksiy Kolesnikov","what":"Пригласил оператора в своё кафе/коворкинг под Лиссабоном, если оператор окажется рядом","due":"","quote":"дай знак, можем пересечься, приезжай к нам в кафе."}],"facts":[{"fact":"Алексей живёт между Португалией (под Лиссабоном) и США (Чикаго), планирует сделать Португалию основной страной, строит там дом","quote":"Сейчас в Португалии, ну, собственно, как бы планируем сделать основной страной. Дом строим"},{"fact":"Основной бизнес Алексея в Чикаго: готовит и доставляет еду, операционно жёсткий; команда IT-ориентированная","quote":"Она выставляет, готовит и доставляет еду."},{"fact":"У Алексея в Португалии есть бранч-кафе/коворкинг","quote":"У нас здесь есть такой Бранч-кафе, каворкинг."},{"fact":"Компания Алексея готовит агентские решения для B2B, запуск через месяц, workflow-разработка","quote":"Мы тоже готовим агентские решения для B2B. Будем запускаться через месяц"},{"fact":"Алексей планирует поднимать раунд, будет в SF в январе минимум на 2 недели","quote":"У нас как раз сейчас будет раунд, будем поднимать."},{"fact":"Алексей с украинским паспортом, продавал компании, построенные в России; физик/математик по бэкграунду; детей пока нет, женат второй раз ([ВОЗРАСТ])","quote":"сам я с украинским паспортом"},{"fact":"Алексей читает посты оператора и позвонил после поста про кофаундера","quote":"Читаю с интересом твои посты."},{"fact":"Алексей использует Hermes с подпиской OpenAI/Codex, Hermes общается на OLX на португальском; ведёт заметки ~15 лет, но пользы от второго мозга не видит и записи встреч не логирует","quote":"я пользуюсь Hermes, в том числе. У меня есть много подписок"},{"fact":"оператор: 40 лет, 4 детей, жил в Австралии [ВОЗРАСТ], затем США; сейчас в Алгарве, присматривает жильё в часе от Лиссабона, хочет переместить деньги","quote":"Я жил там 5 лет, до Америки."},{"fact":"У оператора 4 подписки на LLM; оркестрация через headless CLI на каждой машине, Deep Research через браузер по 6 рельсам с синтезом","quote":"У меня 4 подписки."},{"fact":"оператор ежемесячно донатит на гуманитарные нужды Украины (не летальное)","quote":"я каждый месяц контрибьючу, там, доначу"},{"fact":"оператор бывал в офисе Anthropic, где ему сказали, что банят только за дистилляцию; сторонние харнесы (Hermes/OpenClaw) он пока не ставил","quote":"когда я был в офисе Анкропика, вот на последней тутовке"},{"fact":"Obsidian-волт оператора 20-30 ГБ, тормозит; построен embedding/RAG/retrieval и перелинковка поверх заметок","quote":"Он сделал embedding, rec и retrieval."}],"objections":[{"objection":"Алексей не видит большой пользы от своего 'второго мозга' (Obsidian) и не логирует транскрипты встреч","by":"Oleksiy Kolesnikov","quote":"толку большого от этого второго мозга я не, ну, как бы не вижу для себя."},{"objection":"Алексей не даёт агентам доступ к личным WhatsApp и Telegram от своего имени","by":"Oleksiy Kolesnikov","quote":"ватсап я не даю свой личный. Я его просто не даю"},{"objection":"Алексей сомневается в необходимости/возможности армии харнесов для дистилляции и скептичен к рискам бана подписок","by":"Oleksiy Kolesnikov","quote":"Я не очень переживаю, что они там меня забанят"}],"alpha":[{"signal":"Самый надёжный (АК-47) способ оркестрации разных LLM: запускать их headless в командной строке на машине, Claude-оркестратор вызывает их через терминал; Deep Research же только через браузер","why":"Практичный, не ломающийся паттерн мультивендорной оркестрации, который можно предложить Алексею и применить во флоте","quote":"это самый АК-47 вариант никогда не ломается."},{"signal":"Алексей готовит B2B агентский продукт (запуск через месяц) и рейз в SF в январе: потенциальный партнёр/клиент/интро-источник и кандидат на обмен опытом","why":"Окно по времени (январь, SF), совпадение интересов (агентские B2B-решения), возможность взаимной пользы","quote":"Мы тоже готовим агентские решения для B2B. Будем запускаться через месяц и все такое."},{"signal":"Правило оператора по рейзу: не поднимать у славян; Алексей согласен, что сильные американские фонды редко славянские, но использует славянский нетворк как last resort","why":"Полезный ориентир по стратегии фандрейзинга и источникам нетворка (украинская диаспора в Калифорнии, Web Summit)","quote":"У славян не поднимать, это первое правило."},{"signal":"Идея превратить 'персону' кофаундера в настоящего через файнтюнинг в будущем; сейчас персона/character обеспечиваются frontier-моделью + документацией о человеке + самообучением через Deep Research","why":"Направление развития продукта/контента (character vs persona), тема для постов и экспериментов","quote":"в будущем можно будет, чтобы действительно этот кофаундр был прям по чесноку, прям, кофаундер."},{"signal":"Автоматизация оператора не отключена: чужой Claude закончил/ответил на пост через Claude оператора, что даже понравилось человеку; риск утечки токенов/неотключенной автоматизации","why":"Риск и одновременно доказательство ценности: нужно контролировать неотключенные автоматизации, но реакция положительная","quote":"Не отключил автоматизацию."},{"signal":"Волт Obsidian слишком разросся (20-30 ГБ) и тормозит; решение — дистилляция заметок перед RAG, чтобы избежать шума","why":"Повторяющийся блокер по размеру волта; подтверждает правильность подхода дистилляции перед индексом","quote":"Obsidian и так далее, все это оказалось полной шляпой. Это просто оказалось, там, знаешь, как Explorer."}]}
