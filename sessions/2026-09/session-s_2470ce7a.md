---
session: s_2470ce7a
date: 2026-09-19
words: 3900
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-19 · You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2470ce7a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup call, may be Russian, English or mixed). Do NOT summarize loosely; extract grounded structured facts.

MEETING TITLE: Планерка вечер
CALENDAR INVITEES (names/emails, use to name speakers): [EMAIL], [EMAIL], [EMAIL], [EMAIL]

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
[CryptoPunk Dz2] Можно ещё одного ребёнка дать?
[CryptoPunk Dz2] Но если у нас двое детей, то что?
[CryptoPunk Dz2] Почему такая лиса?
[CryptoPunk Dz2] Где Артур?
[CryptoPunk Dz2] Девочки, привет.
[Nataly L] Как вы?
[CryptoPunk Dz2] Привет.
[CryptoPunk Dz2] Хорошо.
[Nataly L] Как ваши там права?
[Nataly L] Почти в кармане?
[CryptoPunk Dz2] Ну, работают.
[CryptoPunk Dz2] Работаем над этим.
[Hanna Yavtukhovska] Человеческое удостоверение.
[CryptoPunk Dz2] Да, а я, знаете, чем занимаюсь ещё?
[CryptoPunk Dz2] Сегодня Алиса и Артур не пошли в школу.
[CryptoPunk Dz2] На Алису я подала этот абсен...
[CryptoPunk Dz2] Нагречку поняли?
[Nataly L] Предупреждение о том, что она не придёт.
[CryptoPunk Dz2] Да-да-да.
[CryptoPunk Dz2] А вот на Артура нет, и я не знаю, где его подать.
[CryptoPunk Dz2] Я не понимаю, где его подать.
[CryptoPunk Dz2] Ну вот, допустим, я захожу в приложение, понимаете, там только Алиса, а я с телефона сейчас.
[CryptoPunk Dz2] Тут просто этот, только в телефоне в App Store, прикиньте.
[CryptoPunk Dz2] Да, ну а если я зайду отсюда и пошерю?
[Nataly L] А на сайте школы ничего даже рядом нету, да?
[CryptoPunk Dz2] Ну, они просто сказали скачать приложение, то есть, что всё в приложении.
[CryptoPunk Dz2] Ну вот, Алиса у нас есть.
[CryptoPunk Dz2] Сейчас я давайте выключу здесь и зайду.
[CryptoPunk Dz2] А так?
[Nataly L] Так, нормально.
[CryptoPunk Dz2] Да, отлично.
[CryptoPunk Dz2] Так, значит, есть тут такой вообще поширить экран или нет?
[Nataly L] Да везде же есть.
[CryptoPunk Dz2] Я имею в виду в телефоне.
[Nataly L] В телефоне есть.
[CryptoPunk Dz2] А?
[Nataly L] Есть.
[Nataly L] Есть в телефоне.
[Nataly L] Как иначе?
[CryptoPunk Dz2] Ещё раз.
[CryptoPunk Dz2] Если хочешь, я зайду из.
[Nataly L] Телефона тоже и тебе скажу, куда нажать.
[CryptoPunk Dz2] Я знаю.
[CryptoPunk Dz2] Сейчас я попробую.
[CryptoPunk Dz2] Подожди.
[CryptoPunk Dz2] Я постараюсь.
[CryptoPunk Dz2] Share information.
[CryptoPunk Dz2] Information chat.
[CryptoPunk Dz2] Ещё варианты.
[CryptoPunk Dz2] Интересно.
[CryptoPunk Dz2] Здесь просто камера.
[CryptoPunk Dz2] Она нам не нужна.
[CryptoPunk Dz2] О, я нашла.
[Nataly L] Пока ты нашла, то мы звонок отменили, который сейчас у оператора будет.
[Nataly L] Был бы.
[CryptoPunk Dz2] А что это?
[Nataly L] Я же говорю, что это наша бывшая девушка.
[Nataly L] Она у нас работала.
[Nataly L] И она живёт во Франции, кстати.
[Nataly L] Вот.
[Nataly L] Я думаю, что просто оператору сейчас не очень удобно с ней разговаривать.
[CryptoPunk Dz2] Угу.
[Nataly L] Я ей написала.
[Nataly L] Но он сказал, что да, что как бы не будет ни звонка.
[CryptoPunk Dz2] Отлично.
[CryptoPunk Dz2] Вот, смотри.
[CryptoPunk Dz2] Видишь?
[CryptoPunk Dz2] Приложение.
[CryptoPunk Dz2] Так.
[CryptoPunk Dz2] Вот я захожу сюда.
[CryptoPunk Dz2] Тут Велора Академии.
[CryptoPunk Dz2] Понятно.
[CryptoPunk Dz2] А, может быть...
[CryptoPunk Dz2] Да.
[CryptoPunk Dz2] Как я быстро же сориентировалась.
[Nataly L] Ну вот видишь, иногда стоит, да.
[Nataly L] Стоит привлечь внимание, и сразу же, хупс, всё находится.
[CryptoPunk Dz2] Понимаете, да?
[Nataly L] Это чудо, мэджик.
[CryptoPunk Dz2] Как это так отлично.
[CryptoPunk Dz2] Где у нас тут этот...
[CryptoPunk Dz2] Я поняла, там просто...
[CryptoPunk Dz2] Сегодня.
[CryptoPunk Dz2] Ром 18, окей.
[Nataly L] Мне так нравится.
[Nataly L] Я думаю, что Ханна уже тоже всех за деток запомнила, что все детки на «А».
[Nataly L] Мне это правда очень нравится.
[CryptoPunk Dz2] А, ещё нет.
[CryptoPunk Dz2] Я ещё не рассказала про детей, потому что до деток не дошли.
[Nataly L] А, ну вот.
[Nataly L] Ханна, у оператора все детки на «А».
[Nataly L] И, кстати, знаешь, это не вся семья на «А».
[Nataly L] Анна, оператор, и потом идут Артур, Алиса, Аарон, Амир.
[CryptoPunk Dz2] Да.
[Nataly L] Да, вообще.
[CryptoPunk Dz2] Всё, девочки, я её сделала.
[Nataly L] Молодец!
[CryptoPunk Dz2] Как это я так быстро вообще?
[CryptoPunk Dz2] Я в шоке.
[CryptoPunk Dz2] Я сидела тут, наверное, минут десять, просто игралась с этим, не понимала.
[Nataly L] Это, знаешь, Рита, задачи по щелчку пальца просто решаются, понимаешь?
[Nataly L] Секунды на задачу.
[CryptoPunk Dz2] Давай я тебе, Ханне, ещё в одну группу добавлю.
[CryptoPunk Dz2] О, напиши мне в Ватсапе, пожалуйста, мой номер.
[CryptoPunk Dz2] Запиши себе 373-788-38571.
[Nataly L] Напиши сюда, хоть Ханна скопирует.
[CryptoPunk Dz2] 788-385711.
[CryptoPunk Dz2] Да, мне в Ватсапе.
[CryptoPunk Dz2] Я тебе сейчас ещё в одну группы добавлю.
[CryptoPunk Dz2] Тут Анна что-то хочет сказать.
[CryptoPunk Dz2] Не знаю, вы слышите или нет.
[Hanna Yavtukhovska] Да.
[CryptoPunk Dz2] Я ничего не слышу.
[Nataly L] Ну, если ты про разговор какой-то внешний.
[CryptoPunk Dz2] А, про разговор внешний не слышно, да?
[Nataly L] Нет, мне нет.
[CryptoPunk Dz2] Так, ты мне написала в WhatsApp?
[CryptoPunk Dz2] Отлично, я сейчас добавлю ещё одну группу.
[CryptoPunk Dz2] Представься, скажи, что ты наша новая сотрудница.
[CryptoPunk Dz2] Это Анна, у нас жена оператора.
[CryptoPunk Dz2] Там есть одна задача, давай её сейчас подхватим.
[CryptoPunk Dz2] Послушай её, пожалуйста, я сейчас тоже в процессе слушания.
[CryptoPunk Dz2] Извини.
[CryptoPunk Dz2] Секретсанта,.
[Hanna Yavtukhovska] Да?
[CryptoPunk Dz2] Угу.
[CryptoPunk Dz2] Послушай, пожалуйста, что она говорит.
[CryptoPunk Dz2] Там есть два новых сообщения.
[CryptoPunk Dz2] Ты их не слышишь или слышишь?
[CryptoPunk Dz2] Так, это один и это второй.
[CryptoPunk Dz2] Я тебя еще перешлю в личный чат, хорошо?
[Hanna Yavtukhovska] Да-да, хорошо, я слушаю то, что она писала.
[CryptoPunk Dz2] Я еще личный чат тебе перешлю.
[CryptoPunk Dz2] Рита,.
[Hanna Yavtukhovska] У меня только одна аудио.
[CryptoPunk Dz2] Да, я тебе сейчас второе пришлю.
[Hanna Yavtukhovska] Я вижу, что ты ответила на...
[Hanna Yavtukhovska] Да,.
[CryptoPunk Dz2] Ты предыдущие не видишь письма.
[Hanna Yavtukhovska] Всё можешь, сделай мне форвард в личку.
[CryptoPunk Dz2] Да-да-да-да, я так и хочу, просто я опять не могу тебя найти.
[Hanna Yavtukhovska] У меня нет фотки.
[Hanna Yavtukhovska] А ты у меня не прочитала.
[Hanna Yavtukhovska] Блин, я твою Рита написала, подожди.
[CryptoPunk Dz2] Нет-нет, ты всё, ты мне написала.
[CryptoPunk Dz2] Сто процентов мне, я знаю.
[CryptoPunk Dz2] Сейчас я тебя добавлю просто в друзья.
[CryptoPunk Dz2] Всё, наверное, вот так тебе легче.
[CryptoPunk Dz2] Да, я тебе сейчас отправлю.
[CryptoPunk Dz2] Да, я нашла тебе всё нормально.
[CryptoPunk Dz2] Вот, два голосовых там.
[CryptoPunk Dz2] И то, которое ты прослушала, и перед этим.
[CryptoPunk Dz2] Он говорит, что я пока вчера платил, но подтверждение он оплату не скинул.
[CryptoPunk Dz2] Вот денег у меня на секунду нет.
[CryptoPunk Dz2] А вот я ему зрякаю-зрякаю, он трубку не берет.
[CryptoPunk Dz2] А позвоните, пожалуйста, ему на сотовую, может быть, не знаю откуда вы звоните.
[CryptoPunk Dz2] Позвоните и скажите ему, представьтесь там, я не знаю, может быть, представиться адвокатом или юристом.
[CryptoPunk Dz2] Спросить, в чем дело, да, и как бы, что я начну процедуру взыскания, если он...
[CryptoPunk Dz2] Не гасит сумму, денег до сих пор нет, что-то обещает.
[CryptoPunk Dz2] Сначала один-два дня, потом еще один-два дня, потом еще два дня, потом еще один, потом якобы он сходил вчера, сделал платеж через банк, но никаких подтверждений не выслал.
[CryptoPunk Dz2] Денег до сих пор нет.
[CryptoPunk Dz2] Не может быть, с поиска банка, на поиске банка деньги еще не сутки.
[CryptoPunk Dz2] Уже сутки прошли, и никаких денег нету.
[CryptoPunk Dz2] Вот, поэтому подумайте, как можно сказать на кого-то, позвоните кто-нибудь из вас, да, ему на номер и скажите потом по результату.
[Nataly L] Жду пока.
[CryptoPunk Dz2] Девочки, может быть, ну как бы намекнуть или сказать, что если будут такие проблемы с платежами, то как бы выселять надо его как-то.
[CryptoPunk Dz2] Причем там по-дурацки, я знаете, посмотрела в Польше, там просто, блин, не выселишь ни плательщиков.
[CryptoPunk Dz2] Их можно три месяца ждать, и только потом можно процедуру выселения поставить.
[CryptoPunk Dz2] Вот.
[CryptoPunk Dz2] И как бы просто жесть.
[CryptoPunk Dz2] Плюс еще там вот как-то я вовремя не зарегистрировала договор.
[CryptoPunk Dz2] Там у нас есть обращенная процедура выселения.
[CryptoPunk Dz2] Но вот я Рите говорила, что я договор вовремя не зарегистрировала, но якобы вот этот вот азиатальный договор, который выселяешь быстро, потом быстрее выселяешь, он не действует.
[CryptoPunk Dz2] Ну, примерно так.
[Nataly L] Ну что, давай я.
[Hanna Yavtukhovska] Займусь этой задачей, хочешь?
[CryptoPunk Dz2] Что ты планируешь делать?
[Hanna Yavtukhovska] Я планирую сейчас почитать, что вообще можно сказать.
[Hanna Yavtukhovska] И я могу позвонить, представиться как бы юристом Анне.
[CryptoPunk Dz2] У тебя голос юриста.
[CryptoPunk Dz2] Ты там на криминалиста хотела или на кого ты там хотела?
[Hanna Yavtukhovska] На криминалиста.
[CryptoPunk Dz2] Вот, отлично.
[Hanna Yavtukhovska] Это уже когда ни с кем разговаривать не надо.
[Hanna Yavtukhovska] Это уже когда всё.
[CryptoPunk Dz2] Ну, слушай.
[CryptoPunk Dz2] Когда уже тело мертво.
[CryptoPunk Dz2] Это близко.
[Nataly L] Юристы-криминалисты.
[Hanna Yavtukhovska] Я займусь полностью этой задачей, то есть оставляю её мне.
[Hanna Yavtukhovska] Я сейчас почитаю, что можно ему сказать, попытаюсь ему дозвониться.
[Hanna Yavtukhovska] Если он не возьмет трубку, я ему могу написать в WhatsApp, в Телеграме.
[CryptoPunk Dz2] Да, я думаю, что будет отлично.
[CryptoPunk Dz2] Ну, как бы полностью нет.
[CryptoPunk Dz2] Я в любом случае буду сейчас этой задачей дальше заниматься.
[CryptoPunk Dz2] Я тоже хочу посмотреть, потому что документы все у меня, вот, которые мне Анна прислала.
[CryptoPunk Dz2] И, допустим, если мы будем что-то писать, меня Анна просила этот договор в PDF.
[CryptoPunk Dz2] Сейчас я его в PDF переделаю, и, возможно, там можно будет что-то подать.
[CryptoPunk Dz2] Да, Анна, сейчас занимаемся вашей задачей.
[CryptoPunk Dz2] Сначала звоним, короче.
[CryptoPunk Dz2] После этого Анна просила, скорее всего, этот документ как-то там его в налоговую подать, потом в прокуратуру.
[CryptoPunk Dz2] Короче, куда-то она тут просила.
[CryptoPunk Dz2] Поэтому сначала звоним, потом мы занимаемся документооборотом.
[CryptoPunk Dz2] Примерно так.
[CryptoPunk Dz2] Давай?
[Hanna Yavtukhovska] Идёт.
[CryptoPunk Dz2] Да, тогда позвони, пожалуйста, или напиши, и позвони и напиши, наверное, это даже будет лучше.
[CryptoPunk Dz2] Если он ответит, скажет, что он ответил, после этого решим, что делать дальше.
[CryptoPunk Dz2] Вот план такой.
[Hanna Yavtukhovska] Идёт.
[Hanna Yavtukhovska] Договорились.
[CryptoPunk Dz2] Да, давай.
[CryptoPunk Dz2] Супер, спасибо.
[Hanna Yavtukhovska] Читаем, да, не за что.
[Hanna Yavtukhovska] Абсолютно тебе спасибо.
[Hanna Yavtukhovska] Всё, я тогда читаю, и я вернусь к тебе.
[Nataly L] Да-да, конечно.
[CryptoPunk Dz2] Я на связи, я здесь, не отключаюсь.
[CryptoPunk Dz2] Извините, я немножко пошалила.
[CryptoPunk Dz2] Ситуация следующая.
[CryptoPunk Dz2] Я отправила тебе два договора.
[CryptoPunk Dz2] Вот если ты посмотришь их.
[CryptoPunk Dz2] Ты же здесь, да?
[CryptoPunk Dz2] Наверное, ты меня слышишь.
[CryptoPunk Dz2] Я отправила два договора, и один это предыдущий жилец, там Мэри какая-то, Мария, не знаю как её, и второй это вот как раз этот парень, но с ним Крат, как-то так его зовут, вот.
[CryptoPunk Dz2] Редактор.
[Hanna Yavtukhovska] Субтитров А.Синецкая Корректор А.Егорова.
[CryptoPunk Dz2] Ханна, что там у нас с этой задачей?
[CryptoPunk Dz2] Есть какая-то информация?
[CryptoPunk Dz2] Ты здесь или нет?
[CryptoPunk Dz2] Ханна, ты здесь?
[CryptoPunk Dz2] ПОКА!
[CryptoPunk Dz2] Слышишь меня?
[CryptoPunk Dz2] Слышишь?
[CryptoPunk Dz2] Едем к еду.
[CryptoPunk Dz2] Редактор субтитров А.Семкин Корректор А.Егорова Редактор субтитров А.Семкин Корректор А.Егорова Что ты делаешь?
[CryptoPunk Dz2] Почему?
[CryptoPunk Dz2] Ты не будешь спать?
[CryptoPunk Dz2] Ты уже спишь.
[CryptoPunk Dz2] Это?
[CryptoPunk Dz2] Угу.
[CryptoPunk Dz2] И нынешний рейтинг.
[CryptoPunk Dz2] Ну ладно, ладно.
[CryptoPunk Dz2] Если ты хочешь, я могу уничтожить.
[Hanna Yavtukhovska] Ку-ку.
[Nataly L] Девочки, кто-то что-то говорил сейчас?
[Hanna Yavtukhovska] Это я была.
[CryptoPunk Dz2] Я тоже слышала.
[Hanna Yavtukhovska] Я просто перепроверить, как у вас дела.
[Nataly L] У нас, знаешь, кстати, я тебе тоже, Ханна, скажу, у нас иногда бывает так, что вот мы же все работаем, да, параллельно, и вот, например, я наушники откладываю и реагирую только, вот, если там меня зовут по имени, потому что, ну, как бы обычно не слушают, да, там, что вы обсуждаете, или вот когда тихо-тихо, а потом вот звук, и я не знаю, кто что говорил, но я одеваю наушники.
[Hanna Yavtukhovska] Да-да, я с ума отошла от компьютера, чуть пошла вниз, потому что у меня уже этот ку-ку, и я читала этот, ну, агримент, этот договор.
[Hanna Yavtukhovska] Конечно, там особо не за что прикопаться, честно вам сказать.
[Hanna Yavtukhovska] И да, и в Польше защищён не владелец квартиры, а тот, кто её снимает.
[Hanna Yavtukhovska] То есть это должно быть registry letter, да, как бы врученное.
[Hanna Yavtukhovska] И должен быть подключён настоящий адвокат, а не я.
[Hanna Yavtukhovska] Ну, как бы с практикой, legal practice, да, что была компания в Польше.
[Hanna Yavtukhovska] Поэтому давайте будем надеяться, что он просто заплатит.
[Hanna Yavtukhovska] Самый лучший вариант.
[Hanna Yavtukhovska] И потом, конечно, можно его выселить, если он не подходит как квартирант.
[Hanna Yavtukhovska] Ну, конечно, это не...
[Hanna Yavtukhovska] Я не думаю,.
[CryptoPunk Dz2] Что Анна же не заключила, я так понимаю, как-то правильно договор.
[CryptoPunk Dz2] То есть там есть какая-то разница между тем, как она заключала ранее договор и как она заключила сейчас.
[CryptoPunk Dz2] Я, если честно, я подробно и сильно не изучала.
[CryptoPunk Dz2] Ты смотрела эту информацию?
[Hanna Yavtukhovska] Да, я его перевела весь чатом GPT.
[Hanna Yavtukhovska] Но там просто, что да, если 7 дней не оплачено, то можно как бы выселять.
[Hanna Yavtukhovska] То, что она писала на русском.
[Hanna Yavtukhovska] Вот в этом WhatsApp.
[Hanna Yavtukhovska] Видела вот это сообщение?
[CryptoPunk Dz2] Да, да, видела.
[Hanna Yavtukhovska] В польском, а потом на русском перевела.
[Hanna Yavtukhovska] Да.
[Hanna Yavtukhovska] Вот.
[Hanna Yavtukhovska] Но арендатор обязан возместить административные расходы, но как бы их же никаких нет, что ему предъявить.
[Hanna Yavtukhovska] Анна же не обращалась, ну знаешь, никаким лоэром, никому.
[CryptoPunk Dz2] Обратиться.
[Hanna Yavtukhovska] Вот, поэтому это когда уже она обратится.
[CryptoPunk Dz2] Ну так вот, я думаю, что мы будем ей в этом помогать.
[CryptoPunk Dz2] Да.
[CryptoPunk Dz2] Можно ей это предложить, то есть сказать, что вот мы можем обратиться к Лаваку, но как-то она и говорила, она и просила нас.
[CryptoPunk Dz2] Ну, изначально она просила, чтобы мы с ним поговорили просто.
[Hanna Yavtukhovska] Ну да.
[Hanna Yavtukhovska] Он ей писал, что он...
[Hanna Yavtukhovska] Он не.
[CryptoPunk Dz2] Писал, он нам не отвечает, я имею в виду.
[Hanna Yavtukhovska] Да-да, нет, он нам из Индии не отвечает.
[CryptoPunk Dz2] Ну вот.
[CryptoPunk Dz2] То я думаю, что мы можем написать в соответствующее...
[CryptoPunk Dz2] Куда там.
[CryptoPunk Dz2] Вот это пишет.
[Hanna Yavtukhovska] В коллекторское агентство.
[CryptoPunk Dz2] Угу.
[Hanna Yavtukhovska] Те, кто собирает...
[Hanna Yavtukhovska] Ну, по сути, они, честно сказать, делают то же самое, что мы с тобой можем делать, звонить и шантажировать.
[Hanna Yavtukhovska] Просто они это делают за деньги ещё сверху.
[Hanna Yavtukhovska] Вот, как бы, ну...
[Hanna Yavtukhovska] Мы можем это сделать бесплатно.
[CryptoPunk Dz2] Ну как, бесплатно.
[Hanna Yavtukhovska] Веном 2004 года рождения.
[Hanna Yavtukhovska] Боже, я не знаю, это сколько им лет?
[Hanna Yavtukhovska] Господи, пристань.
[Hanna Yavtukhovska] Я в 2004-м уже курила.
[Hanna Yavtukhovska] Это...
[Hanna Yavtukhovska] 21?
[Hanna Yavtukhovska] 22?
[Hanna Yavtukhovska] Боже.
[Hanna Yavtukhovska] Кошмар.
[Hanna Yavtukhovska] Боже.
[CryptoPunk Dz2] Не, ну мы-то тоже не самые собрались.
[CryptoPunk Dz2] Я 97-го, не прямо уж далеко ушла.
[Hanna Yavtukhovska] Ну извини, это ещё с 90-х, тут уже 2000-е начинают наступать, дышать.
[CryptoPunk Dz2] Ну да, да, да.
[CryptoPunk Dz2] Ну ладно, ладно.
[Hanna Yavtukhovska] Ну я на самом деле почувствовала, когда познакомилась с девушкой в 2005-го или 2004-го в компании, в корпорации.
[Hanna Yavtukhovska] Я поняла, что мне вообще очень сложно вести разговоры, не знаю, что и спрашивать.
[CryptoPunk Dz2] Так,.
[Hanna Yavtukhovska] Я позвоню ему еще раз.
[CryptoPunk Dz2] Вот.
[Hanna Yavtukhovska] Я вот придумала, что звонить каждые 10 минут.
[CryptoPunk Dz2] А вот я думаю, может быть...
[Hanna Yavtukhovska] Я занимаюсь заполнением ту-вторую ссылочки для прав.
[Hanna Yavtukhovska] Окей, хорошо.
[CryptoPunk Dz2] Я тебе права отправила.
[Hanna Yavtukhovska] Ага, я заполняю ту-вторую ссылочку.
[Hanna Yavtukhovska] Помнишь, там было две ссылочки?
[Hanna Yavtukhovska] Одна ссылочка от школы, а вторая ссылочка от государства.
[Hanna Yavtukhovska] Вот эта ссылочка от государства, где можно онлайн зарегистрироваться.
[Hanna Yavtukhovska] Там, конечно, такое себе удовольствие.
[Hanna Yavtukhovska] Они просят...
[Hanna Yavtukhovska] Как бы этот сервис, он...
[Hanna Yavtukhovska] Не отвечают.
[Hanna Yavtukhovska] Это сервис для граждан, типа как внутренний регистрационный портал.
[CryptoPunk Dz2] Так, а может они можем зарегистрироваться для граждан?
[Nataly L] Мы как будто граждане.
[Hanna Yavtukhovska] Да, вот в том-то и дело.
[Hanna Yavtukhovska] У него же паспорт другой.
[CryptoPunk Dz2] Короче, надо переходить.
[CryptoPunk Dz2] Давай вместе сядем, давай вот это заполним, а то сядем вместе.
[Hanna Yavtukhovska] Да, давай я школу заполню.
[Hanna Yavtukhovska] Школа легче, здесь просто как бы форма а-ля Google форм.
[Hanna Yavtukhovska] Не хватало прав.
[Hanna Yavtukhovska] Да, я знаю.
[CryptoPunk Dz2] А там можно идти сесть, да.
[Hanna Yavtukhovska] Да, вместе, хорошо.
[Hanna Yavtukhovska] Ну, всё, я дозвонилась.
[CryptoPunk Dz2] Да ты можешь сейчас включить экран, я всё равно же на связи, я просто...
[CryptoPunk Dz2] Я здесь.
[CryptoPunk Dz2] Да, ты можешь пошерить, как бы нет смысла.
[CryptoPunk Dz2] Если тебе так удобнее, конечно, ты можешь идти, но если тебе удобнее со мной, то давай лучше со мной.
[Hanna Yavtukhovska] Давай, смотри, я шерю.
[Hanna Yavtukhovska] Сейчас, сейчас, share with audio.
[CryptoPunk Dz2] Блин, почему?
[CryptoPunk Dz2] Да, всё нормально.
[Hanna Yavtukhovska] Открыла её.
[Hanna Yavtukhovska] Видишь, я не могу этот сайт перевести на английский, да, поэтому я телефон забыла.
[CryptoPunk Dz2] Окей, ну не надо, я тут тебе скажу, что нужно.
[CryptoPunk Dz2] Так, шаг 1, шаг 2, шаг 3, шаг 4, шаг 5.
[CryptoPunk Dz2] Значит, идентификационный документ, дальше proof of examination, ангабы фон информационен, то есть получение информации, заполнение информации, анбагин, короче, подтверждение этого всего, фото и так далее, эрстехилька, первая помощь и БЦЛ-макоплата.
[CryptoPunk Dz2] Примерно так.
[CryptoPunk Dz2] Начинается?
[Hanna Yavtukhovska] Да.
[CryptoPunk Dz2] Припал, бла-бла-бла, виза, бла-бла-бла.
[CryptoPunk Dz2] Нам подходит виза, если что.
[Hanna Yavtukhovska] Окей.
[Hanna Yavtukhovska] Хорошо.
[Hanna Yavtukhovska] Погнали.
[Hanna Yavtukhovska] Начинается.
[CryptoPunk Dz2] Да, бит аус велен.
[CryptoPunk Dz2] А, кстати, тут английский, если хочешь.
[CryptoPunk Dz2] Нет?
[Hanna Yavtukhovska] Не вижу нигде.
[Hanna Yavtukhovska] Это он, щас, я включу Национальность, окей, Поланд Да?
[CryptoPunk Dz2] Поланд, да, угу Дальше Ну тут только один выбор Да Один И как что онлайн, ого Вот.
[CryptoPunk Dz2] Офигеть.
[Hanna Yavtukhovska] Умножение от Bandaid.
[Hanna Yavtukhovska] Вот это Bandaid.
[Hanna Yavtukhovska] Да, ты видишь, как digital local.
[CryptoPunk Dz2] Да.
[Hanna Yavtukhovska] Online ID-карта.
[Hanna Yavtukhovska] Ну, давай попробуем.
[CryptoPunk Dz2] Ну, давай.
[Hanna Yavtukhovska] Сайнап никогда об этом не знаешь?
[Hanna Yavtukhovska] Проверить можно?
[Hanna Yavtukhovska] На всякий случай.
[CryptoPunk Dz2] Посмотрим, да.
[Hanna Yavtukhovska] У нас что-то есть.
[Hanna Yavtukhovska] Не хочу закрывать это окошко.
[CryptoPunk Dz2] Один.
[Hanna Yavtukhovska] У меня просто такое же в Бельгии есть, и оно всё...
[Hanna Yavtukhovska] Нет, у оператора его нет.
[CryptoPunk Dz2] Нет, у оператора его нет.
[Hanna Yavtukhovska] Оно просто всё привязано, знаешь, там бельгийский банк, бельгийские номера телефона, всё тупо вот около.
[CryptoPunk Dz2] Нет.
[CryptoPunk Dz2] Плохо, плохо, не получается.
[Hanna Yavtukhovska] Да, поэтому придётся подавать эти документы физически.
[CryptoPunk Dz2] Да, ему придётся физически, не получается так.
[CryptoPunk Dz2] Ну, то есть ему надо будет трекать на экзамен, ну, как я и говорила, и пойти подать их.
[CryptoPunk Dz2] Примерно так.
[CryptoPunk Dz2] А у него тоже же этот могут идти попросить.
[CryptoPunk Dz2] Блин.
[Hanna Yavtukhovska] Я думаю, что...
[Hanna Yavtukhovska] Смотри.
[Hanna Yavtukhovska] Блин, может, всё-таки попробовать?
[Hanna Yavtukhovska] UID, not German.
[Hanna Yavtukhovska] Только...
[Hanna Yavtukhovska] У нас есть только паспорт.
[CryptoPunk Dz2] Давай попробуем?
[Hanna Yavtukhovska] Ну, слушай, не получится, не получится.
[CryptoPunk Dz2] Кстати, у меня экран твой белый стал, я ничего не вижу.
[Hanna Yavtukhovska] Белый?
[Hanna Yavtukhovska] А, ну стой.
[Hanna Yavtukhovska] А, странно.
[Hanna Yavtukhovska] А, ещё раз.
[Hanna Yavtukhovska] Ещё раз.
[Hanna Yavtukhovska] Вот так, я нажала, да.
[Hanna Yavtukhovska] Куда бы я ни переходила, она будет всё равно показывать.
[Hanna Yavtukhovska] Смотри, есть EU identity non-German.
[Hanna Yavtukhovska] Отлично, окей.
[CryptoPunk Dz2] Допустим, да.
[Hanna Yavtukhovska] Давай, пробуем.
[CryptoPunk Dz2] Давай.
[Hanna Yavtukhovska] Блин, мои дети нашли свисток.
[Hanna Yavtukhovska] Я выброшу.
[Hanna Yavtukhovska] Чтобы не свистят.
[Hanna Yavtukhovska] Поланд.
[Hanna Yavtukhovska] Блин, он хочет теперь, чтобы по-польски.
[CryptoPunk Dz2] Этого у нас тоже нет.
[Hanna Yavtukhovska] А что у нас есть?
[Hanna Yavtukhovska] Короче, давай соберем документы и он физически их подаст.
[CryptoPunk Dz2] Это у нас нету сто процентов, а через Португалию, если допустим.
[Hanna Yavtukhovska] Давай.
[CryptoPunk Dz2] Что там, там же этот финансаж вложится или что там нужно, да?
[CryptoPunk Dz2] Пробуем через Португалию.
[Hanna Yavtukhovska] Боже, зачем я закрыла?
[Hanna Yavtukhovska] Можно открыть, пожалуйста?
[CryptoPunk Dz2] Так,.
[Hanna Yavtukhovska] Вот это было.
[Hanna Yavtukhovska] А, да, я закрыла, потому что открылось в новом окне.
[CryptoPunk Dz2] Португал?
[Hanna Yavtukhovska] Ну-ка.
[Hanna Yavtukhovska] А такое у нас есть?
[CryptoPunk Dz2] Картао, дети, дадао.
[CryptoPunk Dz2] Да, вроде, да.
[Hanna Yavtukhovska] А мы такое делали для этой клиники.
[CryptoPunk Dz2] Да.
[Hanna Yavtukhovska] И он захотел, чтобы мы скачали, помнишь?
[CryptoPunk Dz2] А если с мобильным там что-то?
[Hanna Yavtukhovska] Да, вернёмся.
[CryptoPunk Dz2] Да, мобильное было.
[Hanna Yavtukhovska] Так.
[Hanna Yavtukhovska] Форрест.
[CryptoPunk Dz2] Что за фигня?
[Hanna Yavtukhovska] Ничего, мы будем встречаться и нам откроется.
[CryptoPunk Dz2] Всё окей.
[Hanna Yavtukhovska] Сейчас мы его докладываем.
[CryptoPunk Dz2] Так, давай попробуем в Португалу.
[CryptoPunk Dz2] Попробуем через мобильный.
[Hanna Yavtukhovska] Муфтит что ли, да?
[CryptoPunk Dz2] Да, да.
[CryptoPunk Dz2] Давай это, да.
[Hanna Yavtukhovska] Давай.
[Hanna Yavtukhovska] Окей.
[CryptoPunk Dz2] Уже лучше?
[Hanna Yavtukhovska] Да, 50% мы прошли.
[CryptoPunk Dz2] У нас есть номер телефона, если что.
[Hanna Yavtukhovska] Да, а ПИН?
[CryptoPunk Dz2] А, да, я сфотографирую и посмотрю, что это вообще.
[CryptoPunk Dz2] Подождите, что это такое?
[CryptoPunk Dz2] Сейчас я узнаю, если вдруг есть, будет очень хорошо.

---

**Claude:**

You've hit your weekly limit · resets 4am (Europe/London)
