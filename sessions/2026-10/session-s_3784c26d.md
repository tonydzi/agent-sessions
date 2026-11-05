---
session: s_3784c26d
date: 2026-10-27
words: 3156
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3784c26d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup call, may be Russian, English or mixed). Do NOT summarize loosely; extract grounded structured facts.

MEETING TITLE: Emili <> Tony
CALENDAR INVITEES (names/emails, use to name speakers): [EMAIL], [EMAIL], [EMAIL]

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
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Здравствуйте, Амилия.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Пожалуйста, пять минут.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я немножко на низкой площадке с четырьмя людьми, поэтому...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо.
[Emili Khachatryan] Без проблем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Здравствуйте.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Добрый день.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Рита много про Вас хорошего рассказывала.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Говорит, Вы познакомились недавно.
[Emili Khachatryan] Да, мы познакомились на конференции.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Меня зовут оператор.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Очень приятно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Спасибо большое.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Наверное, живете где-нибудь в Испании или в Лондоне, в Англии.
[Emili Khachatryan] Да-да, в Испании, в Мадриде.
[Emili Khachatryan] А вы?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я сейчас в Португалии.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сейчас каникулы детские.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я обычно между Сан-Франциско и Португалией.
[Emili Khachatryan] В обеих местах прекрасная погода, представляю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну так, средняя Сан-Франциско.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ладненько, давайте, ну там, я не знаю, если вы были, там всегда тучки, ветрено, как в Лондоне.
[Emili Khachatryan] Я в Калифорнии бывала, в Сан-Франциско нет.
[Emili Khachatryan] В Калифорний было хорошо, но...
[Emili Khachatryan] В Калифорнии,.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Кажется, в Сан Франциско он отличается.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он всегда плохая погода.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Расскажите, пожалуйста, чем вы занимаетесь?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я хочу сказать, что вот мы...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, я, допустим, сейчас еще работаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я работаю в инкубаторе, инкубировали стартапы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но, честно, все это потихонечку надоедает, и я хочу найти себе какую-нибудь работу в ИИ-лаборатории.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, и так мы с Рита экспериментируем со всякими ИИ-агентами и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, в общем, объединяем их в всякие сформы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Пытаемся сделать какие-то коллаборации.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сделали штуку, которая типа второго мозга.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В общем, эксперименты.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Пока сжигаем деньги на токены.
[Emili Khachatryan] Да, она немного мне рассказывала.
[Emili Khachatryan] На самом деле, очень интересно звучит всё, что вы делаете, все процессы, которые автоматизируете и занимаетесь.
[Emili Khachatryan] Также насчёт стартапов у меня… У самой был стартап где-то год с половиной назад.
[Emili Khachatryan] То есть я не начала её активно продвигать, но вот всегда интерес был к стартапам.
[Emili Khachatryan] Университет работает в Pixar как product manager.
[Emili Khachatryan] Быть product manager, это как у самой, чтобы был продукт, стартап, поэтому мне очень нравится тут работать.
[Emili Khachatryan] И атмосфера также очень быстрая, стартапная, очень много экспериментов всегда, также работаем с нейронками.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ясно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А вы сейчас в какой компании работаете?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Чем вы занимаетесь?
[Emili Khachatryan] В PicsArt продакт менеджмент занимаюсь, продукт называется PicsArt Flow.
[Emili Khachatryan] Это Notepad Canvas, чтобы генерировать там AI-видео, имиджи, поэтому очень много всего получается сделать там, даже делать краткометражные фильмы.
[Emili Khachatryan] Тут на нашем продукте можно сделать.
[Emili Khachatryan] И это больше как creative platform, но все тоже работает с CI-шким, с co-pilot, и тоже сама использую очень часто, чтобы автоматизировать мои процессы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, если хотите, если вам это интересно, вот эти наши наработки, что мы сделали, мы можем с вами поделиться.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я не знаю, насколько это вам актуально, но вот мы там все, что мы там наделали, мы можем поделиться.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сопротивление, если вы насколько активно пользуетесь и любитель всех вот этих и автоматизаций.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Рада поделиться.
[Emili Khachatryan] Да, да, было бы очень интересно рассмотреть.
[Emili Khachatryan] И с Рита мы также разговаривали, например, мы были на ивенте Эбгала, и очень понравилось, как они пригласили очень много стартапов, очень много также спикеров из больших компаний, и мы с ней тоже обсуждали, что можно что-то такое организовать для вашего стартап-нетворка.
[Emili Khachatryan] Чтобы привести разных людей как connection point, потому что сейчас онлайн-платформы, конечно, классные для знакомства, для networking, как LinkedIn или всякие еще, но всегда вот такие вот face-to-face human конференции, в них намного больше импакта, нежели просто когда платформа онлайн, поэтому у нас была идея, можно так сработаться, так же организовать что-то.—.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А Pixar— это большая компания?— Да-да.— Это Pixar, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это чуть-чуть другая.—.
[Emili Khachatryan] Да-да-да.
[Emili Khachatryan] It's the first unicorn company in Armenia.
[Emili Khachatryan] И у нас есть офисы во всем мире.
[Emili Khachatryan] И она большая компания.
[Emili Khachatryan] То есть у нас 150 миллионов активных юзеров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я, прошу прощения, пытаюсь тут для детей купить какие-то активности.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И пока просто туплю, если честно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я понял, что вы первая компания.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, тогда какая идея?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если вот, я не знаю, сколько вы сами, у вас токены датируются, не датируются.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если готовы денег поджигать, то мы можем дать вам какие-нибудь автоматизации, которые там сильно жизнь облегчат.
[Emili Khachatryan] Немножко вас плохо слышно, это связи.
[Emili Khachatryan] Можете еще раз повторить, пожалуйста.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если вы готовы деньги сжигать, то с удовольствием поделитесь нашими наработками.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы сами как вообще оцениваете себя?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Насколько вы опытный пользователь проекта и автомобилизации?
[Emili Khachatryan] Ну, я довольно опытно пользуюсь им, то есть свои процессы очень легко автоматизирую, чтобы во время одной фулл-тайм работы тоже делать другую фулл-тайм работу.
[Emili Khachatryan] То есть использую не только быстро, но и качественно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Японцы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Тогда дайте мне вашу телегу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я сделал в Телеге группу, и в Телеграме Наш робот даст вашему роботу инструкции, как работать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы кодекс подключили к телеграмму или ватсапу?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У вас это уже работает?
[Emili Khachatryan] Нет, к телеграмме или ватсапу не подключала, потому что у меня кодекс компании, поэтому компанию не подключаю к своему персональному.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А, я понял.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, давайте посмотрим.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сейчас объясним.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот этот кодекс у нас подключен к личным телеграммам и ватсапам, потому что мы всю настройку ведем через кодекс.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Всю настройку мы ведем через мессенджер.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мессенджер говорит вашему кодексу, есть такая функция, попробуй ее использовать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И мы с вами будем пользоваться.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У нас канал коммуникации как раз вот мессенджер.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот если вам такой окей, то вот.
[Emili Khachatryan] Да, это нормально, конечно.
[Emili Khachatryan] Можем там общаться и держаться в связи.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Тогда дайте мне ваш килограмм, пожалуйста.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Напишите мне сюда или прикройте.
[Emili Khachatryan] Сейчас напишу.
[Emili Khachatryan] И номер телефона тоже.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Секунду.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вижу Эмили.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Очень красивое имя.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так, написал вам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Спасибо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] На всякий случай скину вам скриншот с нашего митинга, чтобы не загадывался.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Тогда, ну, Короче, если вам нужно что-то по Долине, то всегда обращайтесь, пожалуйста.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Буду рад.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И я тогда попрошу наш Клод, чтобы он тогда скинул фолап звонка, и он даст вам какие-то промпты, типа, даже как у нас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А вы дадите вашему Клоду или Кодексу, значит, типа, посмотри на вот то, что эти чуваки мне предлагают, и...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ну, конечно, или вы прозвоните, возьмете промпты, ставите свой, и сказать, вот, типа, так-так, я предлагаю тот-то, посмотри, насколько бы интересно.
[Emili Khachatryan] Хорошо, да.
[Emili Khachatryan] Мы также можем пообщаться, подумать насчет будущей коллаборации, как можем сделать коллаборацию, потому что у меня неттворк также людей от больших компаний.
[Emili Khachatryan] То есть не только неттворк от больших компаний, можно присоединиться к стартапам и сделать интересный или ивент, или интересный комьюнити.
[Emili Khachatryan] То есть об этом можно сделать немножко такой брейнстерминг и понять, как это все можно использовать для присутствия.
[Emili Khachatryan] То есть не только жалко деньги, но и так же получать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Имели короткую идею.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Смотрите, мы хотим с Рита начать вести коллектив-коллы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть мы раньше ввели коллектив-коллы, на которые инженеры приходят, делятся своими наработками.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть инженер пришел, он велел спикером, он выступил 5-10 минут, показал себя автоматизацией.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] К нему на звонок пришли и обычные люди, и тоже инженеры.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Звонки на английском, на русском.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Отдельно на английском, отдельно на русском.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть инженеры и инженеры, и какие-то бездевы, которые там активно power-using.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вот если вам интересно ходить, либо вы хотите помочь в соорганизации, то да, вот здесь можно, давайте, как-то коллаборацию строим.
[Emili Khachatryan] Да-да, конечно, поможем в соорганизации.
[Emili Khachatryan] Сделать коллаборацию насчет этого тоже.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Как в вашем плане, в вашем видении обычно выглядит коллаборация?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть что для вас коллаборации?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Просто обмен пиар-анонсами или что-то более такое, что-то большее?
[Emili Khachatryan] Не, не только пиар, но и все процессы придумать, понять, как это можно структурировать, и best practices from other conferences, потому что я во многих конференциях, например, участвовала и онлайн, и оффлайн.
[Emili Khachatryan] Вот все, весь этот experience можно использовать в этом.
[Emili Khachatryan] То есть это не просто пиар или не просто в социальных сетях подвигать, но также структуру вместе делать и организовать именно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, я вижу, Эмиль, да, вы в этом разбираетесь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Давайте подумаем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В общем, давайте пока поразмыслим.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я тоже подумаю, какие возможны коллаборации, возможности у нас с нашей стороны.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Больше, мне кажется, у нас, если мы говорим про это, все равно я и инженерами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А инженеры это не oil, вы понимаете, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А я это там, наверное, это the HHS, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть лабораторий там есть в тележке и попробую наших работников подружить.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Готовы?
[Emili Khachatryan] Хорошо.
[Emili Khachatryan] Немножко связь прервалась, но я, по-моему, поняла.
[Emili Khachatryan] Да-да-да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я говорю, что наши роботы подружены друг с другом, и я хотел сказать, что инженер— это не oil, а AI-инженер— это типа double, не oil.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что вот все наши ивенты и так далее, которые мы делаем, мы делаем именно для этой когорты, для этой аудитории.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо.
[Emili Khachatryan] Прекрасно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если можете, понакидайте какие-то вещи обычные, может, у вас есть какое-то портфолио, может, у вас есть какие-то ссылочки на ивенты, Лума, там что-то еще.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть я бы тоже повникал, что конкретно вы занимаетесь, или какие-то ваши коллабы, которые вы сделали.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я сразу подумал, потому что у меня доступ к тысячам стартапов, к тысячам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И к тысячам инженеров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть, соответственно, ну и не только стартапы, но еще большой ангельский нетворк.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть стартапы которые уже не стартапы а которые уже подняли серьезные раунды, сделали какие-то экзиты, стали ангелами и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И они тоже могут быть очень powerful.
[Emili Khachatryan] Да, будет очень интересно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Спасибо большое.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я извиняюсь, надо тут бежать.
[Emili Khachatryan] Вам тоже спасибо.
[Emili Khachatryan] Хорошего дня.
[Emili Khachatryan] Хорошего отдыха, до свидания.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Пока-пока.

---

**Claude:**

{"lang":"ru","one_line":"Знакомственный звонок оператора с Эмили Хачатрян (продакт-менеджер PicsArt, Мадрид, знакомая Риты) об обмене AI-автоматизациями и совместной организации ивентов/коллабораций для стартап- и инженерного нетворка.","participants":[{"name":"[ИМЯ] [ФАМИЛИЯ]","role":"our-side","channel":"microphone"},{"name":"Emili Khachatryan","role":"lead","channel":"speaker"}],"commitments":[{"owner":"Emili Khachatryan","what":"Написать оператору свой Telegram и номер телефона","due":"сразу, во время звонка","quote":"Сейчас напишу."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Создать Telegram-группу, где робот оператора даст роботу Эмили инструкции по автоматизациям","due":"","quote":"Я сделал в Телеге группу, и в Телеграме Наш робот даст вашему роботу инструкции, как работать."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Скинуть Эмили скриншот с митинга, чтобы она не потеряла контекст","due":"сразу после звонка","quote":"На всякий случай скину вам скриншот с нашего митинга, чтобы не загадывался."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Попросить Claude отправить фоллоуап звонка с промптами, которые Эмили сможет дать своему Claude/Codex","due":"после звонка","quote":"И я тогда попрошу наш Клод, чтобы он тогда скинул фолап звонка, и он даст вам какие-то промпты"},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Подумать, какие коллаборации возможны с их стороны","due":"","quote":"Я тоже подумаю, какие возможны коллаборации, возможности у нас с нашей стороны."},{"owner":"Emili Khachatryan","what":"Помочь в соорганизации коллектив-коллов и совместной коллаборации","due":"","quote":"Да-да, конечно, поможем в соорганизации."},{"owner":"Emili Khachatryan","what":"Прислать портфолио, ссылки на ивенты (Luma и т.п.) и прошлые коллаборации","due":"","quote":"Если можете, понакидайте какие-то вещи обычные, может, у вас есть какое-то портфолио, может, у вас есть какие-то ссылочки на ивенты, Лума, там что-то еще."}],"facts":[{"fact":"Эмили живёт в Мадриде, Испания","quote":"Да-да, в Испании, в Мадриде."},{"fact":"Эмили познакомилась с Ритой на конференции","quote":"Да, мы познакомились на конференции."},{"fact":"Эмили работает продакт-менеджером в PicsArt над продуктом PicsArt Flow (canvas для генерации AI-видео и изображений)","quote":"В PicsArt продакт менеджмент занимаюсь, продукт называется PicsArt Flow."},{"fact":"PicsArt — первый единорог Армении, офисы по миру, 150 млн активных пользователей","quote":"It's the first unicorn company in Armenia."},{"fact":"У Эмили был свой стартап около 1,5 лет назад, активно не продвигала","quote":"У самой был стартап где-то год с половиной назад."},{"fact":"Эмили считает себя опытным пользователем AI-автоматизаций, совмещает две full-time работы","quote":"свои процессы очень легко автоматизирую, чтобы во время одной фулл-тайм работы тоже делать другую фулл-тайм работу."},{"fact":"Codex у Эмили корпоративный, к личным Telegram/WhatsApp не подключён","quote":"у меня кодекс компании, поэтому компанию не подключаю к своему персональному."},{"fact":"оператор работает в инкубаторе, хочет перейти в AI-лабораторию, с Ритой экспериментирует с ИИ-агентами и «вторым мозгом»","quote":"я хочу найти себе какую-нибудь работу в ИИ-лаборатории."},{"fact":"оператор заявляет доступ к тысячам стартапов, инженеров и большому ангельскому нетворку","quote":"у меня доступ к тысячам стартапов, к тысячам."},{"fact":"оператор с Ритой планируют collective-calls: инженеры выступают 5-10 минут, отдельно на английском и русском","quote":"инженер пришел, он велел спикером, он выступил 5-10 минут, показал себя автоматизацией."},{"fact":"Эмили с Ритой были на ивенте Эбгала и обсуждали организацию офлайн-ивента для стартап-нетворка","quote":"мы были на ивенте Эбгала, и очень понравилось, как они пригласили очень много стартапов"}],"objections":[{"objection":"Эмили не подключала рабочий Codex к личным мессенджерам (корпоративное ограничение)","by":"Emili Khachatryan","quote":"у меня кодекс компании, поэтому компанию не подключаю к своему персональному."}],"alpha":[{"signal":"Эмили — PM в PicsArt (единорог, 150M MAU) с нетворком в больших компаниях; потенциальный партнёр для ивентов и дистрибуции аудитории AI-инженеров","why":"Даёт канал к корпоративному нетворку и опыт организации конференций, которого нет у команды оператора","quote":"у меня неттворк также людей от больших компаний."},{"signal":"Коллаборация мыслится как совместная структура и организация ивентов с best practices, а не просто взаимный пиар","why":"Эмили готова вкладывать операционный опыт — реальное со-организаторство","quote":"это не просто пиар или не просто в социальных сетях подвигать, но также структуру вместе делать и организовать именно."},{"signal":"Идея передавать промпты/автоматизации через мессенджер-группу между роботами оператора и Эмили (бот-to-бот онбординг)","why":"Тестирует мультивендорную применимость продукта на чужом Claude/Codex (dogfooding вовне)","quote":"Наш робот даст вашему роботу инструкции, как работать."},{"signal":"Корпоративный Codex Эмили изолирован от личных каналов — интеграцию придётся строить через её личный агент или копипаст промптов","why":"Ограничивает автоматизацию доставки; нужен вариант без подключения рабочего аккаунта","quote":"к телеграмме или ватсапу не подключала, потому что у меня кодекс компании"}]}
