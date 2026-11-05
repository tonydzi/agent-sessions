---
session: s_27fbc09d
date: 2026-10-04
words: 8291
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-04 · You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_27fbc09d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup call, may be Russian, English or mixed). Do NOT summarize loosely; extract grounded structured facts.

MEETING TITLE: Планерка утро
CALENDAR INVITEES (names/emails, use to name speakers): [EMAIL], [EMAIL], [EMAIL], [EMAIL], [EMAIL]

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
[CryptoPunk Dz2] Привет, Эдит.
[CryptoPunk Dz2] Доброе утро.
[CryptoPunk Dz2] Так, я тут заполняю оператору визу, блядь, она у него, оказывается, не была сделана.
[CryptoPunk Dz2] Просто, блядь, с оператором это тоже...
[CryptoPunk Dz2] Он говорил, что окей, я не посмотрела, потом я посмотрела, увидела, что на паспорт Португалии нихера у него нету визы, и я сейчас заполняю визу, и я пытаюсь, пытаюсь это заполнить.
[CryptoPunk Dz2] Так и живём.
[CryptoPunk Dz2] Только информация, которую я в душе не ебу.
[CryptoPunk Dz2] Просто.
[CryptoPunk Dz2] Ладно.
[CryptoPunk Dz2] Изя, всё.
[CryptoPunk Dz2] Ну не шелести, пожалуйста.
[CryptoPunk Dz2] Сейчас.
[[ИМЯ] [ФАМИЛИЯ]] Вот так.
[[ИМЯ] [ФАМИЛИЯ]] Доброе утро.
[[ИМЯ] [ФАМИЛИЯ]] Угу.
[[ИМЯ] [ФАМИЛИЯ]] Привет,.
[Nataly L] Девочки.
[CryptoPunk Dz2] Доброе утро.
[[ИМЯ] [ФАМИЛИЯ]] Привет, доброе утро.
[[ИМЯ] [ФАМИЛИЯ]] Ну,.
[Nataly L] Есть у него что-то, куда он там едет или там за песенами идёт?
[CryptoPunk Dz2] Ну, велики, например.
[Nataly L] На велики он всегда ходит, да?
[CryptoPunk Dz2] Да, с четырёх до семи он на великах.
[CryptoPunk Dz2] Также...
[CryptoPunk Dz2] Остальное смотрите в календаре, в котором все эти встречи.
[[ИМЯ] [ФАМИЛИЯ]] Хорошо,.
[Nataly L] Спасибо.
[CryptoPunk Dz2] Эдита, ты тут?
[CryptoPunk Dz2] Да.
[CryptoPunk Dz2] Напиши, пожалуйста, там, где у нас есть группа Car Wash, как его, не помню, как его зовут, короче, напиши, что Денис опоздает на 30 минут.
[CryptoPunk Dz2] Можно ли, чтобы помыть машину через 30 минут?
[CryptoPunk Dz2] Денис пришел отвозить в школу детей.
[CryptoPunk Dz2] Нора, привет, ты здесь?
[Nataly L] Да, да.
[CryptoPunk Dz2] Короче, я вчера выяснила, что у оператора нет визы.
[Nataly L] Куда нет визы?
[CryptoPunk Dz2] В Америку?
[CryptoPunk Dz2] В Америке.
[Nataly L] Ты шутишь.
[CryptoPunk Dz2] Нет, я не шучу, я заполняю.
[CryptoPunk Dz2] И я до хрена не знаю, как это всё описать, потому что...
[CryptoPunk Dz2] Вот, допустим, вопрос.
[CryptoPunk Dz2] Have you ever been issued a passport or national identity card for travel by any other country?
[CryptoPunk Dz2] Мне Изя говорит, как будто здесь «но» надо писать.
[CryptoPunk Dz2] Тут есть пояснение.
[CryptoPunk Dz2] Сейчас я колбасу продержу.
[CryptoPunk Dz2] Вот.
[CryptoPunk Dz2] Это первый вопрос.
[CryptoPunk Dz2] Второй, я не уверена в фамилиях антоновских родителей.
[CryptoPunk Dz2] Сейчас я вот пытаюсь тут почти, я восстанавливаю, я уже нашла его российский паспорт.
[CryptoPunk Dz2] Уже и то, и то уже, господи, что я только не понаходила.
[CryptoPunk Dz2] Значит, Елена Николаевна Зацковская, но мне надо знать, как это пишется.
[CryptoPunk Dz2] Папа Олег Стефанович.
[CryptoPunk Dz2] Только мне надо это понимать, как это пишется теперь на английском.
[Nataly L] Так, подожди, скажи, Рита, а как быстро эта виза ему подтвердится?
[CryptoPunk Dz2] Я смотрела, что она там в течение 24, до максимум 72-х часов, вот.
[CryptoPunk Dz2] Поэтому у нас, ну то есть, мы пока….
[[ИМЯ] [ФАМИЛИЯ]] Притык.
[CryptoPunk Dz2] Мы впритык, но… потому что у нас как было?
[CryptoPunk Dz2] оператор сказал, нет, вроде всё окей, сначала проверь, потом нет, всё окей, короче, мы потом как-то это всё замяли, и оператор вчера такой типа, надо проверить визу?
[CryptoPunk Dz2] Проверила и поняла, что её нет.
[CryptoPunk Dz2] Отлично.
[Nataly L] Знаешь, по написаниям, если оператор не на связи, у Ани попроси.
[Nataly L] У неё обычно документы такие под рукой.
[Nataly L] Если не найдёшь, я тебе, и оператор не отвечает, я тебе скажу, через кого восстановить.
[Nataly L] Можно через Лену Кондрычеву, можно через Любу.
[Nataly L] С Любой никогда не контактировала?
[CryptoPunk Dz2] Нет, с Любой никогда не контактировала.
[CryptoPunk Dz2] В основном, я не могу понять, что за чат Карлос, потому что, возможно, меня нет там.
[CryptoPunk Dz2] Сейчас я посмотрю.
[CryptoPunk Dz2] Если что, я тебя туда не добавила.
[CryptoPunk Dz2] Сейчас.
[CryptoPunk Dz2] И...
[CryptoPunk Dz2] Диета, ладно, я тебя туда не добавила.
[CryptoPunk Dz2] Всё, я тебя туда добавила.
[CryptoPunk Dz2] Напиши ему, пожалуйста.
[CryptoPunk Dz2] Так...
[CryptoPunk Dz2] Валерий его зовут?
[CryptoPunk Dz2] Нет, его не Валерий зовут, его зовут Густаво.
[[ИМЯ] [ФАМИЛИЯ]] Вот.
[CryptoPunk Dz2] И я не понимаю, как, во-первых, вот этот вопрос мне обработать.
[CryptoPunk Dz2] Have you ever been issued a passport or national identity card for travel by any other country?
[CryptoPunk Dz2] Не понимаю.
[CryptoPunk Dz2] Ну, то есть, я написала no, но, ну, как, я спорила тут с Изей, потому что ChatGPT мне одно говорит, Изя мне другое говорит, и я понятия не имею, что здесь писать на самом деле.
[CryptoPunk Dz2] Вот.
[CryptoPunk Dz2] Потом в LinkedIn профайлы не просят.
[Nataly L] Но формально ты его можешь написать LinkedIn Profile, просто он не откроется.
[CryptoPunk Dz2] А какой у него LinkedIn Profile?
[Nataly L] Сейчас я тебе найду.
[Nataly L] Сейчас я тебя найду и Ринкетин отправлю.
[[ИМЯ] [ФАМИЛИЯ]] Ты.
[CryptoPunk Dz2] Меня прямо здесь отправь.
[CryptoPunk Dz2] Хорошо.
[CryptoPunk Dz2] А вот в таком поле, например, что писать?
[CryptoPunk Dz2] Ну, то есть, есть ли у вас настоящий или предыдущий работодатель?
[CryptoPunk Dz2] Он же был, нет?
[CryptoPunk Dz2] Ты не знаешь?
[Nataly L] Еще нет.
[CryptoPunk Dz2] Скорее всего нет.
[CryptoPunk Dz2] Это же скорее всего нет.
[[ИМЯ] [ФАМИЛИЯ]] Да, читайте, что мы можем подсказать.
[[ИМЯ] [ФАМИЛИЯ]] Я заполняла тоже много американских виз, только здесь из бельгийского посольства, но я думаю, что у них эти анкетные вопросы одинаковые.
[CryptoPunk Dz2] Хорошо.
[[ИМЯ] [ФАМИЛИЯ]] Если вдруг.
[[ИМЯ] [ФАМИЛИЯ]] Я заполнила по-французскому начальнику, у которого вообще не было гражданства.
[[ИМЯ] [ФАМИЛИЯ]] Ну, поняла, есть.
[[ИМЯ] [ФАМИЛИЯ]] оператор, их у тебя есть?
[CryptoPunk Dz2] Да, ну вот у меня есть вопрос.
[CryptoPunk Dz2] Have you a member of the CBP Global Entry Next Century Program?
[CryptoPunk Dz2] Специальные программы пограничной таможенной службы США для надежных путешествий.
[CryptoPunk Dz2] Они платные и позволяют предварительно одобренным лицам проходить границу в ускоренном режиме через автоматические киоски.
[[ИМЯ] [ФАМИЛИЯ]] Честно говоря, такое я не сталкивалась с этим.
[CryptoPunk Dz2] Ну вот.
[[ИМЯ] [ФАМИЛИЯ]] Что-то новое.
[CryptoPunk Dz2] Угу.
[CryptoPunk Dz2] А вот на этот вопрос, как ты бы ответил?
[CryptoPunk Dz2] Я бы ответила yes, потому что это.
[[ИМЯ] [ФАМИЛИЯ]] Логично, вот даже у него же несколько паспортов, португальские, но португальская...
[[ИМЯ] [ФАМИЛИЯ]] Мне просто, ну.
[CryptoPunk Dz2] Говорит он типа...
[CryptoPunk Dz2] То есть вот как будто это немножко другое...
[CryptoPunk Dz2] Было ли когда-то.
[[ИМЯ] [ФАМИЛИЯ]] У вас, да, для вас выпущен документ?
[[ИМЯ] [ФАМИЛИЯ]] Другой страной для путешествий.
[[ИМЯ] [ФАМИЛИЯ]] Ну, как я понимаю, да?
[[ИМЯ] [ФАМИЛИЯ]] По фактам, жестко.
[[ИМЯ] [ФАМИЛИЯ]] Ну, как бы, да.
[[ИМЯ] [ФАМИЛИЯ]] То есть, у него есть паспорт польский, у него есть ID португальская, и эти документы можно просто указать, если там дальше идут ниже поля.
[[ИМЯ] [ФАМИЛИЯ]] Они, наверное, интересуются, какие-нибудь документы.
[CryptoPunk Dz2] National Identity Card Number, Document Number, Expiration Year, Passport Number, National Identity Card Number.
[CryptoPunk Dz2] Просто перед этим уже были вопросы, например, смотри, перед этим, если я иду в Previous, тут есть такой вопрос.
[[ИМЯ] [ФАМИЛИЯ]] Ты можешь пошарить свой экран?
[CryptoPunk Dz2] Да, я могу пошарить свой экран.
[CryptoPunk Dz2] Вот, смотри, перед этим, допустим, был вопрос.
[CryptoPunk Dz2] То есть да, то есть это я написала.
[CryptoPunk Dz2] И тут единственное еще, только я тоже сомневаюсь.
[CryptoPunk Dz2] How did you acquire citizenship and nationality from this country?
[CryptoPunk Dz2] То есть я написала, что true parents.
[CryptoPunk Dz2] Есть еще by birth, но у него by birth я не написала, потому что country of birth у него Беларусь, and city of birth это Минск.
[[ИМЯ] [ФАМИЛИЯ]] А Польша каким образом у него?
[[ИМЯ] [ФАМИЛИЯ]] Это второе гражданство?
[[ИМЯ] [ФАМИЛИЯ]] Может лучше Польшу ему указать, чем российским гражданством?
[CryptoPunk Dz2] Я это понимаю, но понимаешь, в чем прикол?
[CryptoPunk Dz2] По российскому паспорту он уже ездил, и они в любом случае его увидят.
[[ИМЯ] [ФАМИЛИЯ]] Ну да, да, это верно тогда, если он ездил.
[CryptoPunk Dz2] И он даже на визу подавался, то есть там российский паспорт, он фигурировал у него очень часто, и нам нет смысла его скрывать.
[CryptoPunk Dz2] Понимаешь?
[[ИМЯ] [ФАМИЛИЯ]] А ты не хочешь подать две национальности?
[[ИМЯ] [ФАМИЛИЯ]] Ну, две национальности и россиянки?
[CryptoPunk Dz2] А я не знаю его белорусский...
[CryptoPunk Dz2] Ну, то есть я не уверена, что у него есть белорусский паспорт.
[CryptoPunk Dz2] Он нигде не фигурирует.
[CryptoPunk Dz2] У него только польский и российский.
[[ИМЯ] [ФАМИЛИЯ]] Окей, я поняла.
[CryptoPunk Dz2] То есть я даже не уверена, что у него что-то есть в Беларуси.
[CryptoPunk Dz2] Нора, ты не знаешь, у него ничего же белорусского нет, у него нет паспорта?
[Nataly L] Мне кажется, нет и не было.
[Nataly L] От того, что он там родился, это еще не говорит о том, что у него там паспорт.
[CryptoPunk Dz2] Я знаю только про российский, я знаю только про польский.
[CryptoPunk Dz2] А в чем проблема польского?
[CryptoPunk Dz2] Нет, тут видишь, вопрос.
[CryptoPunk Dz2] Are you now a citizen or national of any other country?
[CryptoPunk Dz2] То есть ты сейчас гражданин, допустим, какой-то другой страны.
[CryptoPunk Dz2] То есть он гражданин.
[CryptoPunk Dz2] У него паспорт действующий, российский, до 2027 года.
[CryptoPunk Dz2] И он по нему ездил раньше.
[CryptoPunk Dz2] То есть он получал по нему какие-то визы.
[CryptoPunk Dz2] Но это 100%, потому что есть документы, где он прямо свой российский паспорт указывал.
[CryptoPunk Dz2] И он по нему ездил, он не по-польскому ездил.
[CryptoPunk Dz2] Они в любом случае видят в системе.
[[ИМЯ] [ФАМИЛИЯ]] Ну да.
[CryptoPunk Dz2] Ну вот.
[CryptoPunk Dz2] Поэтому в любом случае указываем российский.
[CryptoPunk Dz2] Подожди, ты это делаешь на вот эту визу онлайн, да?
[CryptoPunk Dz2] Ты делаешь на основе его residence, на основе португальского residence?
[[ИМЯ] [ФАМИЛИЯ]] На основе чего?
[CryptoPunk Dz2] На основе его польского паспорта, по которому он летит.
[[ИМЯ] [ФАМИЛИЯ]] Да.
[CryptoPunk Dz2] Интересно.
[CryptoPunk Dz2] А почему?
[CryptoPunk Dz2] Ну напиши да просто и всё тогда.
[CryptoPunk Dz2] Нет, там мне написало, я вот здесь не понимаю, что писать.
[CryptoPunk Dz2] Have you ever been issued a passport or national identity card for travel by any other country?
[CryptoPunk Dz2] Что именно issued?
[CryptoPunk Dz2] Issued в каком плане?
[CryptoPunk Dz2] Да понятия не имею, ты меня так спрашиваешь, как будто я, если бы я знала, я бы не спрашивала.
[CryptoPunk Dz2] Я думаю, что да.
[[ИМЯ] [ФАМИЛИЯ]] Мне кажется, что да.
[[ИМЯ] [ФАМИЛИЯ]] Только как бы ничего не вижу такого, чтобы вскрывать в этом.
[CryptoPunk Dz2] Просто как бы этот вопрос уже был, и он немножко другой, то есть если уже, то есть смотри, как будто логика такая, если они уже спрашивают в одном поле, что, допустим, являетесь ли вы гражданином, то это как будто вопрос про еще что-то, то есть про дополнительные какие-то паспорта, то есть, ну, понимаешь, да?
[CryptoPunk Dz2] Ну вот, короче, так ладно, посмотрим сейчас, идём дальше.
[CryptoPunk Dz2] Нора, а ты мне отправила этот...
[CryptoPunk Dz2] Я.
[Nataly L] Лидки один ищу, потому что у него их было много, я ищу, который там поживее был.
[CryptoPunk Dz2] Хорошо.
[CryptoPunk Dz2] Facebook page ID.
[CryptoPunk Dz2] А что это значит?
[CryptoPunk Dz2] Провайдер?
[CryptoPunk Dz2] Платформ?
[CryptoPunk Dz2] То есть ещё одно что ли?
[[ИМЯ] [ФАМИЛИЯ]] Где-где?
[CryptoPunk Dz2] Тогда провайдер, платформ, но как будто это ещё допом какая-то.
[CryptoPunk Dz2] Суши мидия.
[CryptoPunk Dz2] Не будем в это, наверное.
[CryptoPunk Dz2] I do not have an online presence.
[[ИМЯ] [ФАМИЛИЯ]] Не, убираем.
[[ИМЯ] [ФАМИЛИЯ]] У него есть.
[CryptoPunk Dz2] Убираем.
[[ИМЯ] [ФАМИЛИЯ]] Нажми на эту платформу.
[[ИМЯ] [ФАМИЛИЯ]] Что там они хотят тебе предложить?
[CryptoPunk Dz2] Ну, до хрена платформы.
[[ИМЯ] [ФАМИЛИЯ]] Откуда, да?
[CryptoPunk Dz2] Может, YouTube ещё можно указать.
[[ИМЯ] [ФАМИЛИЯ]] Нет,.
[CryptoPunk Dz2] Я же не знаю.
[CryptoPunk Dz2] Ммм...
[[ИМЯ] [ФАМИЛИЯ]] Там-парам-парам,.
[CryptoPunk Dz2] Парам-пам-пам Икс, ну почему ты не открываешься, блядь, вот тебе муку.
[CryptoPunk Dz2] Вот котёныш.
[CryptoPunk Dz2] Я решила на небесе, решили, чтобы Денис приехал на полчаса покоить.
[CryptoPunk Dz2] Хорошо.
[Nataly L] Рита, вот бери этот LinkedIn.
[Nataly L] Это вот из последних, но он тогда...
[CryptoPunk Dz2] Я так понимаю, что ему надо...
[CryptoPunk Dz2] А, LinkedIn Profiling, окей.
[CryptoPunk Dz2] Всё окей.
[CryptoPunk Dz2] Подходит.
[CryptoPunk Dz2] Сюда, сюда, сюда.
[CryptoPunk Dz2] Есть, есть, есть.
[CryptoPunk Dz2] Facebook остался.
[CryptoPunk Dz2] Угу.
[[ИМЯ] [ФАМИЛИЯ]] Вам слышно, да, как приходят у меня сообщения в WhatsApp?
[CryptoPunk Dz2] Угу.
[CryptoPunk Dz2] Угу.
[[ИМЯ] [ФАМИЛИЯ]] Хорошо.
[[ИМЯ] [ФАМИЛИЯ]] Как это выключить?
[CryptoPunk Dz2] Ну, нормально.
[[ИМЯ] [ФАМИЛИЯ]] Не знаю, у меня уже...
[CryptoPunk Dz2] Ну, короче, не будем как-то это указать, да?
[[ИМЯ] [ФАМИЛИЯ]] Всё,.
[CryptoPunk Dz2] Facebook есть, LinkedIn, Twitter, Instagram окей.
[CryptoPunk Dz2] Эм...
[CryptoPunk Dz2] Нора, ты не знаешь, у оператора родители и Олег, и Елена, они на его фамилии, ну, Дзетковский.
[Nataly L] Ну, мама точно Дзетковская, а папа, ну, он же был, он же умер.
[Nataly L] Я думаю, что это такой же.
[CryptoPunk Dz2] Да, Дзетковский Олег, Дзеткувская Елена, окей.
[CryptoPunk Dz2] Смотри меня, офигеть.
[CryptoPunk Dz2] Нет, ну я же сказала, нет.
[CryptoPunk Dz2] И чё ты...
[CryptoPunk Dz2] Вот падла, выбивает.
[CryptoPunk Dz2] Ладно.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас.
[CryptoPunk Dz2] Фейсбук сюда.
[CryptoPunk Dz2] Линкедин сюда.
[CryptoPunk Dz2] Твиттер тоже есть где-то.
[CryptoPunk Dz2] Вернись.
[CryptoPunk Dz2] Твиттер.
[CryptoPunk Dz2] Сюда.
[CryptoPunk Dz2] Не осталось ещё у нас.
[Nataly L] Внеси туда медиум.
[Nataly L] Американцы его любят.
[CryptoPunk Dz2] Сейчас посмотрим, есть оно или нет.
[CryptoPunk Dz2] Нету тут медиума, прикинь.
[Nataly L] Можно его добавлять, в смысле, или нельзя?
[CryptoPunk Dz2] Можно.
[Nataly L] Можно.
[Nataly L] Тебе давать ссылку?
[CryptoPunk Dz2] Давай.
[CryptoPunk Dz2] Social media.
[CryptoPunk Dz2] Identify other platform provider.
[CryptoPunk Dz2] Is their username, handle, screen name, or other information similar to your social media profile?
[[ИМЯ] [ФАМИЛИЯ]] Ну-ка.
[CryptoPunk Dz2] Даёшь мне?
[Nataly L] Да-да, сейчас дам.
[Nataly L] Сюда также вставляем.
[[ИМЯ] [ФАМИЛИЯ]] Отлично,.
[CryptoPunk Dz2] Спасибо.
[[ИМЯ] [ФАМИЛИЯ]] Идём.
[CryptoPunk Dz2] Дальше.
[CryptoPunk Dz2] Есть ли путешествия, происходящие в транзите в другой стране?
[CryptoPunk Dz2] Нет.
[[ИМЯ] [ФАМИЛИЯ]] Да.
[CryptoPunk Dz2] U.S.
[CryptoPunk Dz2] Point of contact information.
[[ИМЯ] [ФАМИЛИЯ]] А-а-а!
[CryptoPunk Dz2] Нора, а ты не знаешь, что в таком случае мы пишем?
[CryptoPunk Dz2] У меня нет никакой информации об этом.
[[ИМЯ] [ФАМИЛИЯ]] Это.
[Nataly L] Обязательно, да?
[CryptoPunk Dz2] Ага, я вообще без понятия, где он останавливается.
[Nataly L] А вы не бронировали ему ничего?
[[ИМЯ] [ФАМИЛИЯ]] Какой-то ивент, где он там будет, нельзя организаторов писать.
[Nataly L] Слушай, phone number можно его написать на самом деле?
[Nataly L] Его американский номер.
[CryptoPunk Dz2] Понимаешь, они могут и звонить, вот в чём прикол.
[Nataly L] Но он и ответит.
[CryptoPunk Dz2] Ну, смотри, видишь?
[[ИМЯ] [ФАМИЛИЯ]] Point of contact.
[CryptoPunk Dz2] Да.
[[ИМЯ] [ФАМИЛИЯ]] Знаешь, они такие, если написать его номер телефона, они позвонят, он возьмет трубку, они могут это как, знаешь, умышленно...
[[ИМЯ] [ФАМИЛИЯ]] Вскрывание, да-да-да.
[[ИМЯ] [ФАМИЛИЯ]] Конечно, наши американцы чуть по-другому.
[Nataly L] Тут можно...
[Nataly L] У него есть товарищ, один вообще суперхороший товарищ, который точно согласится дать все свои данные.
[Nataly L] Может быть, оператор у него выжить, я не знаю.
[Nataly L] Надо у оператора спросить, кого он даст.
[Nataly L] Если он тебе там скажет имя, фамилию, которое ты не распознаешь, ты мне скажи, я тебе найду этого человека.
[Nataly L] И мы его добавим.
[CryptoPunk Dz2] Здесь я Анну могу указать, здесь понятно.
[CryptoPunk Dz2] Вот это надо дозаполнить.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас.
[CryptoPunk Dz2] Позвоню оператору.
[CryptoPunk Dz2] Если бы оператор ещё отвечал, было бы вообще отлично.
[[ИМЯ] [ФАМИЛИЯ]] Уже.
[CryptoPunk Dz2] Можно, наверное, только посмотреть, что дальше.
[CryptoPunk Dz2] Не можем, ясно.
[CryptoPunk Dz2] Кого же запомнить?
[CryptoPunk Dz2] Ты там говоришь, товарищ какой-то есть?
[CryptoPunk Dz2] Может, ты его знаешь?
[Nataly L] Я думаю, что ему можно написать, но лучше с оператором посоветоваться.
[Nataly L] Вдруг он, знаешь, в последний момент с ним поругался, а мы такие пишем.
[CryptoPunk Dz2] Давай мы на него напишем, а потом, если нет, я извиню, я просто хочу пройти дальше.
[CryptoPunk Dz2] Есть ли там какие-то еще вопросы, которые я могу у него спросить?
[CryptoPunk Dz2] Ты же видишь, он не отвечает по 10 часов.
[CryptoPunk Dz2] Ему ещё вчера вечером об этом звонило, он не брал трубку.
[Nataly L] Поэтому я и спрашивала у Эдиты, что в планах у оператора, потому что он сегодня звонок пропустил, а там звонок был с человеком из лобстеров, который оператор сам хотел.
[CryptoPunk Dz2] Дай его, пожалуйста, мне сюда информацию, я пока его вставлю.
[Nataly L] Я поищу.
[CryptoPunk Dz2] Что мы скажем, вот мы его вставили окне,.
[[ИМЯ] [ФАМИЛИЯ]] Всё.
[[ИМЯ] [ФАМИЛИЯ]] Девочки, я буду звонить этому Алексею.
[[ИМЯ] [ФАМИЛИЯ]] Если что, я тут сижу.
[[ИМЯ] [ФАМИЛИЯ]] Хорошо?
[CryptoPunk Dz2] Да, хорошо.
[CryptoPunk Dz2] Так, тут я пока заполню.
[CryptoPunk Dz2] Анна.
[CryptoPunk Dz2] Так, нет, это не то.
[CryptoPunk Dz2] Это не сюда.
[CryptoPunk Dz2] Это сюда.
[[ИМЯ] [ФАМИЛИЯ]] Анна.
[[ИМЯ] [ФАМИЛИЯ]] Имейл-адрес.
[[ИМЯ] [ФАМИЛИЯ]] Или вот.
[CryptoPunk Dz2] Этот написать, а вот Зинковский.
[[ИМЯ] [ФАМИЛИЯ]] Другой Имел.
[CryptoPunk Dz2] Сюда Анну Так, эти лица.
[[ИМЯ] [ФАМИЛИЯ]] Угу.
[CryptoPunk Dz2] Я.
[Nataly L] Сейчас тебя сюда отправлю.
[Nataly L] Это Мюррей.
[Nataly L] Они с оператором очень неплохо дружили.
[Nataly L] Вот.
[Nataly L] Я предполагаю, что он может поехать к нему.
[Nataly L] У него есть контакт в его Телеграм.
[Nataly L] Открытый номер телефона.
[Nataly L] Ну и фамилия, имя у него верные.
[Nataly L] А адрес?
[Nataly L] Ну, не знаю.
[Nataly L] Можно адрес поискать на самом деле.
[Nataly L] Он прям...
[Nataly L] Или можно, знаешь, дать предыдущий адрес оператора в Пало-Альто.
[Nataly L] Потому что Мюррой там в Пало-Альто же и жил.
[Nataly L] То есть они там вообще соседями были.
[CryptoPunk Dz2] Давай.
[CryptoPunk Dz2] Если у тебя есть, давай его.
[Nataly L] Сейчас поищу.
[CryptoPunk Dz2] Если что, мы, конечно, потом поменяем.
[CryptoPunk Dz2] Перед тем, как отправим.
[CryptoPunk Dz2] Но пока хотя бы мы заполним для того, чтобы я дальше шла.
[CryptoPunk Dz2] Country code KLMNPortugal Так, её фон номера где-то у меня тоже есть Где-то он есть, есть в тикетцах Нет, не в тикетцах, он есть у Анны У Анны, у Анны, а где он у Анны, непонятно Плюс тридцать один Вот он наверное, да?
[[ИМЯ] [ФАМИЛИЯ]] Нет Ваш.
[CryptoPunk Dz2] Номер Ваш номер Где-то там у неё было в Saved Files Когда я подавала, где-то вот здесь Show Finder.
[[ИМЯ] [ФАМИЛИЯ]] Или.
[CryptoPunk Dz2] Они оператора номер указывали?
[CryptoPunk Dz2] Наверное оператора номер указывали, блин.
[[ИМЯ] [ФАМИЛИЯ]] Угу.
[CryptoPunk Dz2] А где её номер?
[[ИМЯ] [ФАМИЛИЯ]] Угу.
[CryptoPunk Dz2] Сейчас я напишу её.
[[ИМЯ] [ФАМИЛИЯ]] Редактор субтитров А.Семкин Корректор А.Егорова.
[CryptoPunk Dz2] Это ты мне скинула, да?
[Nataly L] Кого?
[CryptoPunk Dz2] Вот это Мюррей.
[Nataly L] А, Мюррей, да, я тебе скинула его.
[Nataly L] А адрес не скинула.
[Nataly L] Адрес ищу.
[[ИМЯ] [ФАМИЛИЯ]] Это.
[CryptoPunk Dz2] Артист?
[Nataly L] Он...
[Nataly L] Нет, он, знаешь, он организатор.
[CryptoPunk Dz2] Он, а...
[CryptoPunk Dz2] Это он, да?
[Nataly L] Юрий, да, это он, да.
[CryptoPunk Dz2] Вот, это всё его.
[CryptoPunk Dz2] Ну, то есть, может, их может быть много?
[Nataly L] Я про это...
[Nataly L] Да-да-да, это этот.
[CryptoPunk Dz2] Угу.
[CryptoPunk Dz2] Хорошо.
[[ИМЯ] [ФАМИЛИЯ]] New.
[CryptoPunk Dz2] Lens, и вот такие фамилии, да?
[[ИМЯ] [ФАМИЛИЯ]] Угу.
[CryptoPunk Dz2] Желательно Анну Антоновну можно договорила.
[CryptoPunk Dz2] Этот номер телефона американский.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас.
[Nataly L] Мюре возьми.
[Nataly L] У него в аккаунте оригинальный номер телефона.
[[ИМЯ] [ФАМИЛИЯ]] В.
[CryptoPunk Dz2] Аккаунте оригинальный номер телефона.
[CryptoPunk Dz2] Это обойти.
[Nataly L] В аккаунт зайди к нему и ты увидишь.
[Nataly L] В шапке положи.
[CryptoPunk Dz2] Если в Инстаграме, то нет.
[Nataly L] Я тебе не инсту дала, я тебе дала на телеграм.
[Nataly L] Зайди в телеграм.
[CryptoPunk Dz2] А, телеграм, окей.
[Nataly L] А мне кажется, в инсте не пишется номер, если сам не напишешь, да?
[CryptoPunk Dz2] Да, всё верно.
[CryptoPunk Dz2] Да, супер.
[CryptoPunk Dz2] Теперь надо его адрес или адрес...
[CryptoPunk Dz2] А, нигде у него тут не просвележивается в их контактах адреса.
[CryptoPunk Dz2] Случаем.
[Nataly L] У него там есть юридический адрес, вот где они вместе с оператором всякие конференции проводили.
[Nataly L] Вот я бы думала, как бы его это указать, может быть.
[CryptoPunk Dz2] Здесь какой-то адрес, оператор Зитковский, а это, наверное, его Лома, Верди, Ави, Пало-Альто, Калифорния, бла-бла-бла.
[CryptoPunk Dz2] Уже есть какое-то письмо, видишь?
[Nataly L] Вот бери вот это и всё, как бы нам же без разницы уже, какой адрес.
[Nataly L] Я хочу просто дальше пройти.
[[ИМЯ] [ФАМИЛИЯ]] Да,.
[CryptoPunk Dz2] Давай возьмём его пока что.
[CryptoPunk Dz2] Адрес line, так, там где-то куски, это понятно, city palo alto, убираем, сюда, state california, да, california, убираем.
[CryptoPunk Dz2] Дальше, apartment number 684, скорее всего, сюда, long number, А вот этот код, его куда-то нужно или нет?
[CryptoPunk Dz2] Вот так.
[[ИМЯ] [ФАМИЛИЯ]] Почему?
[CryptoPunk Dz2] Интересно, а почему адрес неправильный?
[Nataly L] Что штат пишется как CA, или это выбрано?
[Nataly L] Он выбран.
[CryptoPunk Dz2] Забирается.
[Nataly L] Хорошо.
[CryptoPunk Dz2] Palo Alto.
[CryptoPunk Dz2] Может здесь что-то ещё нужно добавить?
[CryptoPunk Dz2] Да вроде не должно быть, нет?
[CryptoPunk Dz2] А, окей.
[CryptoPunk Dz2] А тогда apartment number не нужно, наверное.
[CryptoPunk Dz2] Да, вот так, Пало-Альто, Калифорния, бла-бла-бла.
[[ИМЯ] [ФАМИЛИЯ]] Да,.
[CryptoPunk Dz2] Пусть будет у него, да?
[Nataly L] Ну, с учётом того, что вы просто какой-то адрес рандомный написали, пусть будет.
[CryptoPunk Dz2] Ну почему рандомный?
[CryptoPunk Dz2] Это адрес из письма.
[CryptoPunk Dz2] Какой-то давности.
[CryptoPunk Dz2] Да, какой-то давности, где-то же...
[CryptoPunk Dz2] Ну, в.
[Nataly L] Общем, адрес некий существует, нам подойдёт.
[CryptoPunk Dz2] Да, пока так.
[CryptoPunk Dz2] И нужен этот номер телефона Анны в Португалии.
[CryptoPunk Dz2] Найди где-то в переписке с Анной, у меня Анна Дедковская, есть её португальский номер, она где-то мне давала.
[CryptoPunk Dz2] Плюс 351, что-то там такое.
[CryptoPunk Dz2] Поищи, пожалуйста, в Телеграме.
[CryptoPunk Dz2] Где-то у меня был её португальский номер, но я бог понятия не знаю где.
[[ИМЯ] [ФАМИЛИЯ]] Так, секвенцирация.
[CryptoPunk Dz2] Окей, сейв подойдёт.
[CryptoPunk Dz2] Так, это не то.
[CryptoPunk Dz2] Возвращаемся сюда.
[CryptoPunk Dz2] Это не то Да блин, не то.
[[ИМЯ] [ФАМИЛИЯ]] Говорю Так, сюда вот Что такое?
[CryptoPunk Dz2] Да что такое, да что такое всё Где-то у неё точно есть какой-то предупрежский номер.
[CryptoPunk Dz2] Я ещё знала, где и как он.
[CryptoPunk Dz2] Я вроде искала-искала, но не могла найти.
[CryptoPunk Dz2] Угу.
[[ИМЯ] [ФАМИЛИЯ]] Отлично.
[CryptoPunk Dz2] Всё, подходит сюда.
[CryptoPunk Dz2] Вот так.
[CryptoPunk Dz2] Туковская Анна, Затковская 2, бла-бла-бла.
[CryptoPunk Dz2] Адрес есть, идём дальше.
[CryptoPunk Dz2] Конечно, вернёмся.
[CryptoPunk Dz2] Так.
[CryptoPunk Dz2] Нет.
[CryptoPunk Dz2] Вы были арестованы?
[CryptoPunk Dz2] Криминальный преступник совершил серьезное повреждение свойства или серьезное повреждение?
[CryptoPunk Dz2] Нет.
[CryptoPunk Dz2] Виолетование в связи с новой законодательностью?
[CryptoPunk Dz2] Нет.
[CryptoPunk Dz2] Вы болеете?
[[ИМЯ] [ФАМИЛИЯ]] Нет.
[CryptoPunk Dz2] Слушай, но вот эту часть мы уже не отмечаем, смотри.
[CryptoPunk Dz2] Это как,.
[[ИМЯ] [ФАМИЛИЯ]] Знаешь, есть эти организации, которые помогают тебе подать на визу, как визовые агентства.
[CryptoPunk Dz2] Так, next.
[CryptoPunk Dz2] Ну и осталось оплатить, если...
[CryptoPunk Dz2] Ну опять же осталось у оператора уточнить и оплатить.
[CryptoPunk Dz2] Слушайте, а давайте мне помогите ещё раз сверить всю информацию, кто откроет оператора паспорт португальский.
[CryptoPunk Dz2] Блять, польский.
[CryptoPunk Dz2] Ханна, давай ты откроешь?
[CryptoPunk Dz2] У тебя есть время.
[CryptoPunk Dz2] Алё.
[[ИМЯ] [ФАМИЛИЯ]] Алё-у.
[CryptoPunk Dz2] Блин, кто куда пропал?
[CryptoPunk Dz2] Меня не слышно?
[CryptoPunk Dz2] Алё-алё-алё.
[[ИМЯ] [ФАМИЛИЯ]] Алё-алё-алё-алё.
[CryptoPunk Dz2] Девочки, меня не слышно?
[[ИМЯ] [ФАМИЛИЯ]] Девочки?
[CryptoPunk Dz2] Девочки, меня слышно или нет?
[CryptoPunk Dz2] Девочки, меня слышно?
[[ИМЯ] [ФАМИЛИЯ]] Алё.
[[ИМЯ] [ФАМИЛИЯ]] Алё.
[CryptoPunk Dz2] Девочки, а кто ещё здесь?
[[ИМЯ] [ФАМИЛИЯ]] Я тут.
[[ИМЯ] [ФАМИЛИЯ]] Аня.
[[ИМЯ] [ФАМИЛИЯ]] Ханна.
[CryptoPunk Dz2] Секундочку.
[CryptoPunk Dz2] Секундочку, секундочку.
[CryptoPunk Dz2] Открой, пожалуйста, Антонен Паспорт, этот португальский.
[CryptoPunk Dz2] Я хочу, чтобы мы сверили ещё раз все данные.
[[ИМЯ] [ФАМИЛИЯ]] Открыть?
[[ИМЯ] [ФАМИЛИЯ]] Сейчас, секунду.
[[ИМЯ] [ФАМИЛИЯ]] Так, ещё секунду.
[[ИМЯ] [ФАМИЛИЯ]] Ты будешь диктовать или мне диктовать?
[[ИМЯ] [ФАМИЛИЯ]] Польский паспорт, да, открыла.
[CryptoPunk Dz2] Да, польский.
[CryptoPunk Dz2] А я сейчас пошерю экран, мы сейчас вместе сверим.
[[ИМЯ] [ФАМИЛИЯ]] Так.
[CryptoPunk Dz2] Смотрим, смотрим.
[CryptoPunk Dz2] Next.
[CryptoPunk Dz2] Сейчас я кое-что тут еще проверю по этому.
[CryptoPunk Dz2] Ну, блядь, опять она не открывается.
[CryptoPunk Dz2] Почему family name Стефанович?
[CryptoPunk Dz2] Есть такое отчество Степанович?
[[ИМЯ] [ФАМИЛИЯ]] Да, как Степанович, Степан.
[CryptoPunk Dz2] Ой, эта фамилия.
[[ИМЯ] [ФАМИЛИЯ]] Степанович.
[[ИМЯ] [ФАМИЛИЯ]] Ну, я думаю, что есть такая фамилия, да.
[[ИМЯ] [ФАМИЛИЯ]] Степановище, знаешь, какая-то.
[CryptoPunk Dz2] А где ты взяла эту информацию, что именно его фамилия Стефанович?
[CryptoPunk Dz2] Покажи мне именно эту строку.
[[ИМЯ] [ФАМИЛИЯ]] Не-не-не, я не...
[[ИМЯ] [ФАМИЛИЯ]] Ну не тебе, я не тебе.
[CryptoPunk Dz2] А, сори, я испугалась.
[CryptoPunk Dz2] Я не тебе.
[[ИМЯ] [ФАМИЛИЯ]] Сори, Рита, у меня просто такое состояние, поняла, вот это, нестабильное.
[[ИМЯ] [ФАМИЛИЯ]] И я, вот это, реагирую сильно.
[CryptoPunk Dz2] Все нормально, я разговариваю с Клодом.
[[ИМЯ] [ФАМИЛИЯ]] Все-все, я молчу.
[CryptoPunk Dz2] Я бы у тебя такое не спросила.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас.
[CryptoPunk Dz2] Мне надо просто в одну монетку достовериться, я в любом случае буду ещё у оператора спрашивать информацию.
[CryptoPunk Dz2] Угу.
[[ИМЯ] [ФАМИЛИЯ]] Ладно,.
[CryptoPunk Dz2] Оставим Стефанович.
[CryptoPunk Dz2] Пока что поменяем.
[CryptoPunk Dz2] Хорошо.
[CryptoPunk Dz2] Криптопанк, Криптопанк.
[CryptoPunk Dz2] Где ты у меня?
[CryptoPunk Dz2] Ты прыгнёшь, кажется.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас.
[CryptoPunk Dz2] Дойдём до чего-то более-менее понятного.
[CryptoPunk Dz2] Идём дальше, идём дальше, идём дальше.
[CryptoPunk Dz2] Так, ты открыла, да?
[[ИМЯ] [ФАМИЛИЯ]] Да, вижу.
[CryptoPunk Dz2] Ты видишь экран мой, да?
[[ИМЯ] [ФАМИЛИЯ]] Сейчас сек, я так сделаю.
[CryptoPunk Dz2] Так, [ФАМИЛИЯ], [ФАМИЛИЯ].
[CryptoPunk Dz2] Дальше first name оператор.
[CryptoPunk Dz2] Дальше passport number 0355693.
[CryptoPunk Dz2] Issuing country Poland.
[CryptoPunk Dz2] Date February 12, 2019.
[CryptoPunk Dz2] Всё верно, да?
[Nataly L] Да.
[CryptoPunk Dz2] Exploration date February 12, 2029.
[CryptoPunk Dz2] Country of citizenship nationality Poland.
[CryptoPunk Dz2] Не понимаю, почему там не было возможности national identification number, personal identification number указать.
[CryptoPunk Dz2] Ладно.
[CryptoPunk Dz2] Окей, если мы сделаем Edit.
[CryptoPunk Dz2] Вот смотри.
[[ИМЯ] [ФАМИЛИЯ]] Не разрешает, да?
[[ИМЯ] [ФАМИЛИЯ]] Заблокировано поле.
[CryptoPunk Dz2] Почему?
[[ИМЯ] [ФАМИЛИЯ]] Не знаю.
[[ИМЯ] [ФАМИЛИЯ]] Может быть это только если у тебя U.S.
[[ИМЯ] [ФАМИЛИЯ]] Паспорт?
[[ИМЯ] [ФАМИЛИЯ]] Тогда можно запомнить.
[[ИМЯ] [ФАМИЛИЯ]] Я бы оставила, не трогала.
[CryptoPunk Dz2] Next.
[CryptoPunk Dz2] Okay, next.
[CryptoPunk Dz2] Okay, next...
[CryptoPunk Dz2] И next.
[CryptoPunk Dz2] Так.
[CryptoPunk Dz2] Дальше.
[CryptoPunk Dz2] Sex mail.
[CryptoPunk Dz2] Date of birth August 27, 1983.
[CryptoPunk Dz2] City of birth Minsk.
[CryptoPunk Dz2] Country of birth Belarus.
[CryptoPunk Dz2] Северно, да?
[CryptoPunk Dz2] Вот здесь как будто северно или нет, или есть кое-что?
[[ИМЯ] [ФАМИЛИЯ]] Да, верно.
[[ИМЯ] [ФАМИЛИЯ]] Я не нашла никаких ошибок.
[CryptoPunk Dz2] Ну, главное, номер паспорта.
[CryptoPunk Dz2] 0355-693.
[[ИМЯ] [ФАМИЛИЯ]] 0355-693.
[[ИМЯ] [ФАМИЛИЯ]] 0355.
[[ИМЯ] [ФАМИЛИЯ]] 0355 693.
[[ИМЯ] [ФАМИЛИЯ]] 0356.
[[ИМЯ] [ФАМИЛИЯ]] 0356 693.
[CryptoPunk Dz2] 0356 693.
[[ИМЯ] [ФАМИЛИЯ]] 0356.
[Nataly L] 0356 693.
[CryptoPunk Dz2] 0356 693.
[CryptoPunk Dz2] 0366.
[[ИМЯ] [ФАМИЛИЯ]] 0366 0366.
[CryptoPunk Dz2] Country of citizenship nationality in Russia.
[CryptoPunk Dz2] How did you acquire citizenship nationality from this country through parents?
[CryptoPunk Dz2] Допустим, допустим.
[CryptoPunk Dz2] Have you ever been a citizen of a national country?
[CryptoPunk Dz2] Ну, там было no, просто там нельзя было отметить yes.
[CryptoPunk Dz2] Email address.
[CryptoPunk Dz2] Окей.
[CryptoPunk Dz2] Допустим, если что, потом поменяем.
[CryptoPunk Dz2] Дальше идём.
[CryptoPunk Dz2] Personal information.
[CryptoPunk Dz2] Are you known by any other names of Alice?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Yes, я написала.
[CryptoPunk Dz2] Это то, что мы обсуждали, помнишь?
[CryptoPunk Dz2] Сейчас я тебе скину его эти даты.
[CryptoPunk Dz2] Вернее, этот паспорт.
[CryptoPunk Dz2] Пожалуйста, давай его вместе сверим.
[CryptoPunk Dz2] Паспорт, паспорт, это пиздец.
[CryptoPunk Dz2] Где нахрен его паспорт?
[[ИМЯ] [ФАМИЛИЯ]] Вот он.
[CryptoPunk Dz2] Так.
[CryptoPunk Dz2] Донат.
[CryptoPunk Dz2] Давай.
[CryptoPunk Dz2] Десктоп.
[[ИМЯ] [ФАМИЛИЯ]] Отлично.
[CryptoPunk Dz2] Так.
[CryptoPunk Dz2] Телеграм.
[CryptoPunk Dz2] Рита.
[CryptoPunk Dz2] Открывайся.
[CryptoPunk Dz2] Так.
[CryptoPunk Dz2] Где ты у меня?
[CryptoPunk Dz2] Где ты у меня, где ты у меня?
[CryptoPunk Dz2] Вот ты у меня.
[CryptoPunk Dz2] Вот, или видел, пожалуйста, open сюда.
[CryptoPunk Dz2] Так, давай сверять.
[CryptoPunk Dz2] Document number id_e5689c3f.
[[ИМЯ] [ФАМИЛИЯ]] Да?
[CryptoPunk Dz2] Ты открыла?
[[ИМЯ] [ФАМИЛИЯ]] id_e5689c3f.
[[ИМЯ] [ФАМИЛИЯ]] Подожди, нет, не открыла, не тот сек.
[[ИМЯ] [ФАМИЛИЯ]] Вот, она открыла.
[[ИМЯ] [ФАМИЛИЯ]] А у меня этого паспорта не было, так, я себе сохраню.
[CryptoPunk Dz2] Ну, не было ни у кого, я не знаю, где он взял.
[CryptoPunk Dz2] 1-3-5-4-7-3-0.
[[ИМЯ] [ФАМИЛИЯ]] 7-3-0, Да.
[CryptoPunk Dz2] Russian year, 507 passport number, Russian, так, всё окей.
[CryptoPunk Dz2] Your contact information.
[CryptoPunk Dz2] Ро, Фернандо, Венюс, Ромаль, Х8, Сити, Синтра, Лизабон, Португал, Мобайл, Португалос, 35.
[CryptoPunk Dz2] Окей.
[CryptoPunk Dz2] Дальше.
[CryptoPunk Dz2] Social media.
[CryptoPunk Dz2] Facebook есть, LinkedIn есть, Twitter есть, Instagram есть.
[CryptoPunk Dz2] Other medium.
[CryptoPunk Dz2] Окей.
[CryptoPunk Dz2] Ну, насколько я знаю, нет.
[CryptoPunk Dz2] Потому что, скорее всего, он на этой матери фамилии.
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] So, is your travel to the U.S.
[CryptoPunk Dz2] Occurring in transit to another country?
[[ИМЯ] [ФАМИЛИЯ]] No.
[CryptoPunk Dz2] Ну, типа, ты транзитом через Америку в другую сторону?
[CryptoPunk Dz2] Нет.
[CryptoPunk Dz2] U.S.
[CryptoPunk Dz2] Point of contact information name, address, city, United States, номер телефона.
[CryptoPunk Dz2] Тот же самый.
[CryptoPunk Dz2] Ever since I've been in contact with Russia.
[CryptoPunk Dz2] [ФАМИЛИЯ] Анна, [ФАМИЛИЯ], Португал, её номер телефона.
[CryptoPunk Dz2] Дальше.
[CryptoPunk Dz2] Вот он живёт.
[CryptoPunk Dz2] Ну тут понятно, типа вот это холера, диастерия, бла-бла-бла.
[CryptoPunk Dz2] Have you been arrested or convicted for a crime that resulted in serious damage or fraud or serious harm to another person or government authority?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Have you ever violated any law related to processing using and distributing illegal drugs?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Do you seek to engage in or have you ever engaged in terrorist activities, such as sabotage?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Have you ever committed fraud or misrepresented yourself and obtained or ceased to obtain a visa?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Are you currently seeking employment in the U.S.
[CryptoPunk Dz2] States, or were you previously employed in the United States without prior permission from the U.S government?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Have you ever been denied a U.S visa or plan for this year's current and previous passports, or have you ever been refused admission to your application for a mission port of entry?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Have you ever stayed in the United States longer than the admission period granted to you by the U.S government?
[CryptoPunk Dz2] No.
[CryptoPunk Dz2] Куба, Ирак, Иран, Либия, бла-бла-бла, no.
[[ИМЯ] [ФАМИЛИЯ]] Почему.
[CryptoPunk Dz2] Мне не даёт дальше пройти?
[CryptoPunk Dz2] Потому что, наверное, мне нужно это всё подтвердить сначала, а потом надо занедлить.
[CryptoPunk Dz2] Ай, бум-бум-бум-бум-бум.
[[ИМЯ] [ФАМИЛИЯ]] Мне нужно занести это в календарь.
[[ИМЯ] [ФАМИЛИЯ]] Календарь на этой второй почте.
[Nataly L] Девочки, оператор не появился случайно?
[CryptoPunk Dz2] Нет, я еще не могу ему вызвониться.
[Nataly L] У него звонок просто стоит, я вот не знаю, он на него пойдет или нет, опять вызвонит.
[Nataly L] Я сегодня позвонила, наверное, раз пятьдесят.
[CryptoPunk Dz2] Я просто сегодня не сдерживала себя.
[CryptoPunk Dz2] Отвечает мне оператор.
[CryptoPunk Dz2] Слушай, у меня есть такое впечатление, что они пришли за пятым ребенком.
[Nataly L] Это, конечно, мило, но тогда предлагаю отменить все звонки.
[CryptoPunk Dz2] Да, потому что они вчера уехали в отель, сейчас ребёнок возит в школу детей, и они так и не вернулись.
[[ИМЯ] [ФАМИЛИЯ]] Знаешь, у меня есть хотя бы фора доделать всё, что я не сделала вчера, и я боюсь вот эти бензиновые баки вообще предлагать, потому что я не шарю, но ничего.
[CryptoPunk Dz2] Ну, смотри, если он даёт какое-то фото, ты должна, грубо говоря, найти такие же.
[[ИМЯ] [ФАМИЛИЯ]] Я поняла, да.
[[ИМЯ] [ФАМИЛИЯ]] Я сейчас максимально делаю активность.
[[ИМЯ] [ФАМИЛИЯ]] Я поняла, что помнишь, я написала не в ту школу по поводу обедов.
[[ИМЯ] [ФАМИЛИЯ]] Мне кажется, нужно этой Александре продублировать это письмо по поводу обедов, потому что у Анны будет митинг с ней.
[CryptoPunk Dz2] Обязательно.
[[ИМЯ] [ФАМИЛИЯ]] Обязательно.
[[ИМЯ] [ФАМИЛИЯ]] И если она спросит по обеду, а она...
[[ИМЯ] [ФАМИЛИЯ]] Александра ничего не знает про обеды, то мне кажется, будет конфликт.
[CryptoPunk Dz2] Обязательно, да.
[CryptoPunk Dz2] Обязательно!
[[ИМЯ] [ФАМИЛИЯ]] Вот, поэтому я сейчас вот этим занимаюсь.
[CryptoPunk Dz2] Конфликт будет у нас.
[CryptoPunk Dz2] Конфликт будет у нас, и нам не поздороваться.
[[ИМЯ] [ФАМИЛИЯ]] Ну да, да, я не за них переживаю.
[CryptoPunk Dz2] Не за них переживай, Александра.
[CryptoPunk Dz2] Мне нравится.
[[ИМЯ] [ФАМИЛИЯ]] Я и так уже начинаю чуть-чуть так поджимать хвост.
[[ИМЯ] [ФАМИЛИЯ]] Так, сейчас я это делаю.
[CryptoPunk Dz2] Короче, Нора, у нас есть время, конечно, там, знаешь, официальный срок рассмотрения заявки ЕСТа составляет до 72 часов, то есть трое суток.
[CryptoPunk Dz2] То есть мы успеваем, у нас в запасе есть около четырёх дней.
[CryptoPunk Dz2] Но нам желательно сейчас это всё оплатить, прямо вот сейчас.
[CryptoPunk Dz2] Для того, чтобы сейчас оплатить и сейчас подтвердить, мне нужен оператор.
[CryptoPunk Dz2] Я не могу это сделать без оператора, ебаный в рот, его нет нигде.
[Nataly L] Слушай, подожди пока.
[Nataly L] Вот смотри, дадим ещё часа два ему, чтобы появиться.
[Nataly L] Я надеюсь, что он придёт на второй звонок.
[Nataly L] Вот.
[Nataly L] У него там гарьерный консультант.
[Nataly L] Ну, то есть, как бы, соответствует его основной ещё задаче.
[Nataly L] Я надеюсь что он на него придёт, появится и уже включится вот в эти вот задачки.
[Nataly L] Держим пальчики, короче.
[[ИМЯ] [ФАМИЛИЯ]] И активно работаем.
[CryptoPunk Dz2] Ну это такая, довольно-таки, как бы щепетильная задача.
[CryptoPunk Dz2] Вот.
[CryptoPunk Dz2] У меня есть ещё одна такая, с ящиком.
[CryptoPunk Dz2] Я тоже её там пытаюсь доделать до конца.
[[ИМЯ] [ФАМИЛИЯ]] Она же отвечает на...
[[ИМЯ] [ФАМИЛИЯ]] Отвечала Ватсапе на мои сообщения, поэтому она...
[[ИМЯ] [ФАМИЛИЯ]] Она мне не отвечает.
[[ИМЯ] [ФАМИЛИЯ]] Она в отеле...
[[ИМЯ] [ФАМИЛИЯ]] Ну если она с ним в отеле, то она может ответить, а он, видишь...
[CryptoPunk Dz2] Он тоже может идти, но не хочет.
[[ИМЯ] [ФАМИЛИЯ]] Да,.
[CryptoPunk Dz2] По почте смотри.
[CryptoPunk Dz2] То есть, почту я сейчас сделаю.
[CryptoPunk Dz2] Ну, пытаюсь, по крайней мере.
[CryptoPunk Dz2] Я её в любом случае сделаю.
[CryptoPunk Dz2] И вот эту почту будешь указывать тогда.
[[ИМЯ] [ФАМИЛИЯ]] Ты мне покажешь, наверное, на экране, да, сейчас?
[CryptoPunk Dz2] Я пытаюсь, да, её сделать.
[CryptoPunk Dz2] Ну, это вторая задача, которая очень важная.
[CryptoPunk Dz2] оператор не хочет, чтобы это была франшиза, но у нас нет информации, это франшизы или не франшизу.
[[ИМЯ] [ФАМИЛИЯ]] Так, я пойду одену линзу, потому что начинаю уже косить.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас сек.
[CryptoPunk Dz2] Давай напишем им письмо, уточним эту информацию на вот этот greenmail, бла-бла-бла.
[CryptoPunk Dz2] Напиши в драфте в АУ, я перепроверю, отправлю.
[[ИМЯ] [ФАМИЛИЯ]] Отлично.
[[ИМЯ] [ФАМИЛИЯ]] Я уже наловчилась на четвёртый день с этими линзами.
[CryptoPunk Dz2] И как тебе?
[[ИМЯ] [ФАМИЛИЯ]] Слушай, нормально.
[[ИМЯ] [ФАМИЛИЯ]] Я просто вообще слепая камбалом.
[[ИМЯ] [ФАМИЛИЯ]] Мне реально очень тяжело, ну, без очков быть.
[[ИМЯ] [ФАМИЛИЯ]] И у меня очки...
[[ИМЯ] [ФАМИЛИЯ]] А ты вблизи как?
[CryptoPunk Dz2] Видишь нормально или вблизи?
[[ИМЯ] [ФАМИЛИЯ]] Вблизи тоже уже плохо.
[[ИМЯ] [ФАМИЛИЯ]] У меня всё плохо.
[[ИМЯ] [ФАМИЛИЯ]] У меня просто катаракта ещё на одном глазу при этом.
[[ИМЯ] [ФАМИЛИЯ]] Ну, развилась, видимо, из-за стресса всё вот это время.
[[ИМЯ] [ФАМИЛИЯ]] И мне дети разломали две пары очков.
[[ИМЯ] [ФАМИЛИЯ]] Просто вылома рядушки, потому что я их оставила на столе.
[[ИМЯ] [ФАМИЛИЯ]] А я не знаю, как у вас, но тут в Бельгии срок ожидания изготовления очков, ну, типа месяц.
[[ИМЯ] [ФАМИЛИЯ]] И я заказала новое, но пока мне нужна альтернатива, я ничего не вижу, ну, я за руль вообще не могу сесть без очков.
[[ИМЯ] [ФАМИЛИЯ]] А у меня их просто нет.
[[ИМЯ] [ФАМИЛИЯ]] То есть я еду и держу вот так вот, я ехала из магазина оптики и держала стекла в руках, в одной руке, и вот так с одним глазом ехала.
[[ИМЯ] [ФАМИЛИЯ]] Один глаз прикрыла, а один— это жесть.
[[ИМЯ] [ФАМИЛИЯ]] Думала, если полиция остановит, будут очень сильно смеяться.
[Nataly L] Да,.
[[ИМЯ] [ФАМИЛИЯ]] И сейчас, да, нормально.
[[ИМЯ] [ФАМИЛИЯ]] Первые два дня ужасно было.
[[ИМЯ] [ФАМИЛИЯ]] Такое чувство, что песок в глазах, знаешь, оно беспокоило и раздражало нервную систему.
[[ИМЯ] [ФАМИЛИЯ]] А вот сейчас уже вот на какой?
[[ИМЯ] [ФАМИЛИЯ]] Субботу, да, в субботу я нашла их.
[CryptoPunk Dz2] Блин, ну вот оператор, значит, он в этом пишет, а мне не отвечает.
[CryptoPunk Dz2] Ну вот что за дебилизм?
[CryptoPunk Dz2] Вот скажите мне, пожалуйста.
[CryptoPunk Dz2] Тем самым позвонить.
[[ИМЯ] [ФАМИЛИЯ]] На этой почти.
[[ИМЯ] [ФАМИЛИЯ]] Почему же я подумала, что на другой?
[CryptoPunk Dz2] Мне так понравился ответ оператора, девочки, это пиздец.
[[ИМЯ] [ФАМИЛИЯ]] Меня же слышно, да?
[[ИМЯ] [ФАМИЛИЯ]] Какой?
[[ИМЯ] [ФАМИЛИЯ]] Да-да, я ищу просто.
[[ИМЯ] [ФАМИЛИЯ]] В каком окне?
[CryptoPunk Dz2] Я ему говорю вот это все.
[CryptoPunk Dz2] Он говорит такой...
[CryptoPunk Dz2] Ну, я его спрашиваю, во-первых, можем ли мы указать, как контактное лицо такого-то, такого-то.
[CryptoPunk Dz2] Я говорю, какая фамилия отца.
[CryptoPunk Dz2] Вот это вся история.
[CryptoPunk Dz2] Паспорт российский указываю или нет.
[CryptoPunk Dz2] Он такой...
[CryptoPunk Dz2] Ну, я ничего не знаю.
[CryptoPunk Dz2] Контактного лица у меня нет.
[CryptoPunk Dz2] Давай спросим у Лены, как она заполняла.
[CryptoPunk Dz2] Пиши, Лень.
[CryptoPunk Dz2] Заебись история.
[CryptoPunk Dz2] Я ему сказала, ну, Рэй, он не захотел его добавлять.
[CryptoPunk Dz2] Но как?
[CryptoPunk Dz2] Он не сказал нет, но и не сказал да.
[[ИМЯ] [ФАМИЛИЯ]] Как бы ничего не сказал.
[CryptoPunk Dz2] Ну как, я его конкретно спросила, он такой, давай Лену узнаем.
[CryptoPunk Dz2] Ну оператор, это не ответ на вопрос.
[[ИМЯ] [ФАМИЛИЯ]] Это.
[CryptoPunk Dz2] Не ответ на вопрос, Она такая, блин.
[CryptoPunk Dz2] Дай бог, она мне ответит.
[CryptoPunk Dz2] Она не очень меня любит.
[[ИМЯ] [ФАМИЛИЯ]] Кто-то колено это...
[[ИМЯ] [ФАМИЛИЯ]] Лена—.
[CryptoPunk Dz2] Это помощница, которая была на протяжении восьми лет работала.
[CryptoPunk Dz2] Ну, она и до сих пор там, они что-то помогают.
[CryptoPunk Dz2] И, ну, она тоже, знаешь, это так, мне так иногда это раздражает.
[CryptoPunk Dz2] Ну, типа, смотри, она мне пишет.
[CryptoPunk Dz2] «Доброе утро, Рита.
[CryptoPunk Dz2] Можно ли не писать на письма, которые мне отвечают?» Я говорю, это знаешь, как будто я беру просто так рандомное письмо, и я смотрю, что это Лена пишет.
[CryptoPunk Dz2] Я такая, о, мне же нехуй чем больше заняться.
[CryptoPunk Dz2] У меня же не такие личные задачи.
[CryptoPunk Dz2] Я такая, о, я возьму вот это, которое Лене ответили, и, блядь, вот отвечу нахуй на него, понимаешь?
[CryptoPunk Dz2] Вот...
[CryptoPunk Dz2] А что ты мне пишешь?
[CryptoPunk Dz2] Я говорю, меня попросила Анна.
[CryptoPunk Dz2] То есть, привет, меня попросила Анна, она даже ничего не написала.
[CryptoPunk Dz2] Понимаешь, меня просто скидывает Анна и говорит, напиши.
[CryptoPunk Dz2] Я, значит, беру это письмо, нахожу и пишу.
[CryptoPunk Dz2] Это же не значит, что я от себя, блядь, захотела и написала.
[CryptoPunk Dz2] Пиздец.
[[ИМЯ] [ФАМИЛИЯ]] Ты знаешь, с такими людьми очень сложно работать, и у меня есть такая коллега, Надя Петрова.
[[ИМЯ] [ФАМИЛИЯ]] Которая работала 9 лет в российском посольстве здесь, в Бельгии, и это оставило определенный след вообще на ее поведение.
[[ИМЯ] [ФАМИЛИЯ]] Не то чтобы против российского посольства, нет.
[[ИМЯ] [ФАМИЛИЯ]] Просто у нее нет понимания, что дела должны быть сделаны.
[[ИМЯ] [ФАМИЛИЯ]] Вот у нее есть только активность показывать, писать вот письма, то, все.
[[ИМЯ] [ФАМИЛИЯ]] Плюс у нее есть определенная степень аутизма.
[[ИМЯ] [ФАМИЛИЯ]] То есть у нее отсутствует интеллектуальный, эмоциональный вообще интеллект, да.
[[ИМЯ] [ФАМИЛИЯ]] То есть она не понимает, что можно говорить, что нельзя.
[[ИМЯ] [ФАМИЛИЯ]] Сейчас, короче, она мне сталкерит, потому что я отказываюсь ей помогать, она меня заебала.
[[ИМЯ] [ФАМИЛИЯ]] Я раньше ее вытягивала на своих плечах, а сейчас она меня просто заебала.
[[ИМЯ] [ФАМИЛИЯ]] У меня как бы есть что делать.
[[ИМЯ] [ФАМИЛИЯ]] И она меня сталкерит и плачет, и пишет в HR письма, и жалуется своему начальнику, начальнице, что четыре года назад я ей ответила в имейле ok.done и не написала dear Надя.
[[ИМЯ] [ФАМИЛИЯ]] Ну, поняла?
[[ИМЯ] [ФАМИЛИЯ]] Я просто написала, ок, да, ну, всё, у меня не было времени.
[[ИМЯ] [ФАМИЛИЯ]] И вот она вот эта у меня сталкерита, так как это японская компания, то все носятся с ней как с писаной торбой, потому что в Бельгии Блин, реально могут уволить за какой-то характер, еще что-то.
[[ИМЯ] [ФАМИЛИЯ]] И компании не нужны, знаешь, эти разбирательства.
[[ИМЯ] [ФАМИЛИЯ]] Потому что неизвестно, насколько она может пойти, знаешь, по инстанциям выше.
[[ИМЯ] [ФАМИЛИЯ]] Короче, и я от этого смотрю, беру попкорн и думаю, понятно.
[[ИМЯ] [ФАМИЛИЯ]] Но мы все ржем с нее, потому что особо меня притянуть за уши нельзя.
[[ИМЯ] [ФАМИЛИЯ]] Это просто как бы не было конфликта, ничего не было такого.
[[ИМЯ] [ФАМИЛИЯ]] Ну вот я понимаю, что это такой же человек, вот как вот это.
[[ИМЯ] [ФАМИЛИЯ]] Могла бы ты мне не писать, а могла бы ты мне написать?
[[ИМЯ] [ФАМИЛИЯ]] А бы могла удалить мне эти переписки?
[[ИМЯ] [ФАМИЛИЯ]] Мне это неинтересно.
[[ИМЯ] [ФАМИЛИЯ]] Я говорю, в смысле могла удалить переписки?
[[ИМЯ] [ФАМИЛИЯ]] Это наша работа.
[[ИМЯ] [ФАМИЛИЯ]] Интересно, неинтересно?
[[ИМЯ] [ФАМИЛИЯ]] Ну, короче, поэтому я очень завидую фрилансу.
[[ИМЯ] [ФАМИЛИЯ]] Потому что корпорат— это ад.
[[ИМЯ] [ФАМИЛИЯ]] Ненавижу корпоративную работу.
[CryptoPunk Dz2] Ну, ты тоже знаешь, у фриланса есть такие...
[[ИМЯ] [ФАМИЛИЯ]] Ну, да.
[[ИМЯ] [ФАМИЛИЯ]] В фрилансе, мне кажется, страшно заболеть.
[CryptoPunk Dz2] Да-да.
[[ИМЯ] [ФАМИЛИЯ]] В Франции можно, знаешь, плюнуть, взять, допустим, в Бельгии можно, типа, взять больничный, потому что у тебя burnout, или ты себя плохо чувствуешь на две недели, тебе никто слова не скажет, знаешь.
[[ИМЯ] [ФАМИЛИЯ]] А в Фрилансе конечно, в этом плане...
[CryptoPunk Dz2] Ну, если ты болеешь, то всё, не будет у тебя работы.
[[ИМЯ] [ФАМИЛИЯ]] Просто работаешь больной, и всё.
[CryptoPunk Dz2] В этом, да.
[[ИМЯ] [ФАМИЛИЯ]] Ну, вот эти вот все...
[[ИМЯ] [ФАМИЛИЯ]] Интриги, скандалы, расследования, которые делают...
[[ИМЯ] [ФАМИЛИЯ]] Ну, она такая, знаешь,.
[CryptoPunk Dz2] Ну, немножко психанутая, честно.
[CryptoPunk Dz2] Я как бы, пусть об этом слушают Fireflies, не похер, но она реально психованная.
[CryptoPunk Dz2] Она постоянно что-то там кричала, она что-то там, короче...
[CryptoPunk Dz2] Ну, она такая, ну, нездоровые у них отношения были, именно даже рабочие, личные, не знаю.
[CryptoPunk Dz2] Такая, типа, психованная немножко баба.
[[ИМЯ] [ФАМИЛИЯ]] Она взрослая?
[CryptoPunk Dz2] Да.
[[ИМЯ] [ФАМИЛИЯ]] У неё на паузе началась, поэтому она психует.
[[ИМЯ] [ФАМИЛИЯ]] Так бывает тоже.
[CryptoPunk Dz2] Слушай, не знаю.
[CryptoPunk Dz2] Не знаю почему, но...
[CryptoPunk Dz2] Она очень расстроилась, когда она ушла.
[CryptoPunk Dz2] Хотя она сама ушла, она хлопнула дверью и съебалась.
[CryptoPunk Dz2] Ну так она типа...
[CryptoPunk Dz2] Ты необычная женщина, где под пятьдесят.
[CryptoPunk Dz2] И ты идёшь всегда.
[[ИМЯ] [ФАМИЛИЯ]] Да, не люблю такое поведение.
[[ИМЯ] [ФАМИЛИЯ]] Все пришли работать, свои психи и характеры дом показывают.
[[ИМЯ] [ФАМИЛИЯ]] Самоотверждение это к хорошему не приводит.
[CryptoPunk Dz2] Она просто расстроилась, что оператор её убрал с чата, а оператор её убрал с одного чата, потому что она должна была только одним вопросом заниматься.
[CryptoPunk Dz2] Она распылялась, и она под одним вопросом ничего не делала.
[CryptoPunk Dz2] Это был важный вопрос.
[CryptoPunk Dz2] Она говорит, давай я тебя сейчас уберу, как бы, потому что, ну типа, сделай, пожалуйста, это, и я тебя верну, как бы, потому что тут очень много людей, ты расправляешься, ты делаешь другое, а она такая, всё, ты меня убрал, ну хорошо, бе-бе!
[CryptoPunk Dz2] Вот.
[CryptoPunk Dz2] Хлопнула дверь и ушла.
[CryptoPunk 
...[truncated]

---

**Claude:**

```json
{
  "lang": "ru",
  "one_line": "Внутренняя команда (Рита, Нора, Ханна) в панике заполняет и пытается подать онлайн-анкету на американскую визу для оператора, обнаружив в последний момент, что у него её нет, и упирается в то, что сам оператор недоступен для уточнения данных и оплаты.",
  "participants": [
    {"name": "Рита (CryptoPunk Dz2)", "role": "our-side", "channel": "unknown"},
    {"name": "Нора (Nataly L)", "role": "our-side", "channel": "unknown"},
    {"name": "Ханна / Эдита (канал '[ИМЯ] [ФАМИЛИЯ]')", "role": "our-side", "channel": "unknown"},
    {"name": "оператор (субъект визы, на звонке не присутствует)", "role": "other", "channel": "unknown"}
  ],
  "commitments": [
    {"owner": "Рита", "what": "Оплатить и подтвердить визовую анкету сразу, как только выйдет на связь оператор", "due": "как можно скорее, в рамках ~72ч/4 дней окна", "quote": "Нам желательно сейчас это всё оплатить, прямо вот сейчас. Для того, чтобы сейчас оплатить и сейчас подтвердить, мне нужен оператор."},
    {"owner": "Ханна", "what": "Позвонить Алексею (карьерный консультант/контакт)", "due": "", "quote": "Девочки, я буду звонить этому Алексею. Если что, я тут сижу."},
    {"owner": "Ханна", "what": "Занести встречу/дело в календарь на второй почте", "due": "", "quote": "Мне нужно занести это в календарь. Календарь на этой второй почте."},
    {"owner": "Ханна", "what": "Продублировать письмо Александре по поводу школьных обедов, чтобы не возник конфликт на митинге", "due": "", "quote": "Мне кажется, нужно этой Александре продублировать это письмо по поводу обедов, потому что у Анны будет митинг с ней."},
    {"owner": "Рита", "what": "Написать черновик письма с уточнением, франшиза ли это или нет, и передать на проверку перед отправкой", "due": "", "quote": "Давай напишем им письмо, уточним эту информацию на вот этот greenmail, бла-бла-бла. Напиши в драфте в АУ, я перепроверю, отправлю."},
    {"owner": "Рита", "what": "Написать организатору Car Wash (группа), что Денис опоздает на 30 минут", "due": "", "quote": "Напиши, пожалуйста, там, где у нас есть группа Car Wash... напиши, что Денис опоздает на 30 минут."}
  ],
  "facts": [
    {"fact": "У оператора нет визы в США, и команда срочно заполняет анкету", "quote": "Короче, я вчера выяснила, что у оператора нет визы... В Америку? В Америке."},
    {"fact": "Срок рассмотрения визовой заявки — до 72 часов", "quote": "официальный срок рассмотрения заявки ЕСТа составляет до 72 часов, то есть трое суток."},
    {"fact": "У оператора польский паспорт № 0356693 (ошибочно сначала записали 0355693), выдан 12.02.2019, истекает 12.02.2029", "quote": "passport number 0355693. Issuing country Poland. Date February 12, 2019... Exploration date February 12, 2029."},
    {"fact": "У оператора также действующий российский паспорт № id_e5689c3f, по которому он ранее ездил и подавался на визы", "quote": "По российскому паспорту он уже ездил, и они в любом случае его увидят... он по нему ездил, он не по-польскому ездил."},
    {"fact": "оператор родился 27 августа 1983 года в Минске, Беларусь, но белорусского паспорта у него нет", "quote": "Date of birth August 27, 1983. City of birth Minsk. Country of birth Belarus... у него нет паспорта."}
  ],
  "objections": [
    {"objection": "Опасение писать товарищу оператора (Мюррею) как контактному лицу без согласования с самим оператором", "by": "Нора", "quote": "Я думаю, что ему можно написать, но лучше с оператором посоветоваться. Вдруг он, знаешь, в последний момент с ним поругался, а мы такие пишем."}
  ],
  "alpha": [
    {"signal": "оператор систематически недоступен (не отвечает по 10+ часов, пропустил звонок с 'человеком из лобстеров', которого сам хотел), что блокирует критичные по времени задачи (оплата визы)", "why": "Повторяющийся блокер: срочные процессы с жёстким дедлайном (72ч на визу) зависят от решения/подтверждения оператора, а он недоступен — риск пропустить дедлайн или важные контакты", "quote": "Я не могу это сделать без оператора... его нет нигде." },
    {"signal": "Решение указывать российское гражданство/паспорт в анкете, а не скрывать его, так как иммиграционная система США уже видит историю поездок по этому паспорту", "why": "Правильная стратегия раскрытия информации в анкете снижает риск отказа/флага за несовпадение данных", "quote": "По российскому паспорту он уже ездил, и они в любом случае его увидят... нам нет смысла его скрывать."},
    {"signal": "Как заполнять поле 'online presence/social media' когда нет аккаунта на платформе — использовать LinkedIn, даже если профиль не открывается по ссылке", "why": "Практический процессный приём для будущих похожих анкет", "quote": "Но формально ты его можешь написать LinkedIn Profile, просто он не откроется."},
    {"signal": "Нора целый день прозвонила оператору «раз пятьдесят» и предлагает отменить остальные звонки дня, подозревая, что он с женой 'ушёл за пятым ребёнком'", "why": "Сигнал о реальной недоступности ключевого человека и риске каскадной отмены рабочих звонков в течение дня", "quote": "Я сегодня позвонила, наверное, раз пятьдесят... тогда предлагаю отменить все звонки."}
  ]
}
```
