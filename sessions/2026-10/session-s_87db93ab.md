---
session: s_87db93ab
date: 2026-10-15
words: 8113
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-15 · You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_87db93ab` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are extracting structured deal-flow data from ONE verbatim call transcript (VC/startup call, may be Russian, English or mixed). Do NOT summarize loosely; extract grounded structured facts.

MEETING TITLE: Mehdi Tabdili: 1-on-1 with Tony
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
[Memo Guleryuz] Так.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Продолжение следует...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ты будешь их оставлять?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Оставлю только те процессы, где последнее вновление было давно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] То есть самый старый, имею в виду перициду, не самый старый, а начатый, когда была последняя информация, последняя запись, последний символ.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Привет, Мэнг Дин.
[Jonathan Archer] Привет, как дела?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Как дела?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Привет, Мэнь Дин, как дела?
[Mehdi Tabdili] Хорошо, а ты?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо, сэр.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы встретились в Сан-Франциско, верно?
[Mehdi Tabdili] Да, мы встретились в Сан-Францисско, в доме Альфреда Пикса.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Понятно, хорошо, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что, честно говоря, у меня нет времени.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если это возможно, давайте поговорим о вашем продукте и о том, что вы создаете.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Может быть, это поможет вам немного.
[Mehdi Tabdili] Да, я имею в виду, что мы не создаем ничего, да?
[Mehdi Tabdili] Мы – компания AI-интеграции.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да.
[Mehdi Tabdili] Мы, в основном, имеем клиентов, которые уже имеют платные лицензии и пытаются создать воркфлоры, или они пытаются и они помогают нам выбирать.
[Mehdi Tabdili] Так что я думал, что вы можете помочь, если вы можете, потому что вы сами, если вы можете найти клиентов, мы можем поделиться с вами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня есть несколько клиентов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Наш предыдущий инкубатор проводил множество консультаций B2B для корейских, японских и тайских клиентов, для бизнес-клиентов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Foxconn, например, был одним из наших клиентов.
[Mehdi Tabdili] Поксун?
[Mehdi Tabdili] Да, Поксун, конечно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] АНА, это одна из самолетов Японии, тоже одна из наших клиентов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Много корейских клиентов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что, у нас есть...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У нас есть, так сказать, армия.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы проводим много консультаций для предприятий.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потому что некоторые предприятия...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы, как инженеры, мы тоже делали много интеграций, Мы называем это AI-хайп, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] 4 Или больше лет назад.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Поэтому у нас было много связей в Азии.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но вы не хотите мне сказать, что вы интегратор энтропии, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Дайте мне размеры проверки, которые вам интересны для работы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Размеры проверки, которые вы хотели бы получить из обычных компаний.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы не так большие.
[Mehdi Tabdili] У нас около 20 людей, которые получили антропические сертификации.
[Mehdi Tabdili] У меня есть компания, которую я продал 1,5 года назад.
[Mehdi Tabdili] Это было, в основном, для сети, сети безопасности, сети инфраструктуры.
[Mehdi Tabdili] В прошлом году я начал эту вентуру с моим партнером, с которым мы продали предыдущую компанию в сети.
[Mehdi Tabdili] Это мы начали очень поздно, в прошлом году, мы вошли в антропический партнер-программ, и тогда у нас было много людей, которые просто реагировали органично, через онлайн, и через связи, которые помогают с антропической интеграцией, и тому подобное.
[Mehdi Tabdili] И то, что мы пытаемся решить сейчас, потому что очень часто clients come to us, they want to set it up, right, set up the accesses.
[Mehdi Tabdili] Иметь все, что связывает их внутренние системы с имейсом, SharePoint, с работой, все разные вещи.
[Mehdi Tabdili] Так что мы, потому что наши цели до сих пор были маленькими и медленными бизнесами, и мы использовали их как фиксированные цены, да?
[Mehdi Tabdili] Говоря, что они будут платить вам X сумму, чтобы сделать это.
[Mehdi Tabdili] Но я думаю, что мы начинаем двигаться в сторону управления сервисами, чтобы сказать, что для тех, кто не имеет специфическую команду Cloud, мы заплачем вам эту сумму за это поддержку в месяц.
[Mehdi Tabdili] Вот мы и находимся сейчас.
[Mehdi Tabdili] Но мы растем довольно долго, 6-8 месяцев, когда мы начали это, и мы видим много людей, которые приходят к нам, и мы не делали Hardcore, как маркетинг или отдельное оборудование.
[Mehdi Tabdili] Все до сих пор было просто органическим.
[Mehdi Tabdili] У нас есть некоторая сеть для нашей...
[Mehdi Tabdili] Приватная сеть, которую покупала наша предыдущая компания.
[Mehdi Tabdili] Они владеют, как сотни разных компаний, и они больше находятся в индустриальной инфраструктуре.
[Mehdi Tabdili] Так что у нас есть какие-то связи, которые мы пытаемся использовать.
[Mehdi Tabdili] Но чтобы поделиться размером, у нас 20 людей, которые мы можем импортировать прямо сейчас.
[Mehdi Tabdili] Я имею в виду, что половина из них сейчас работают на наших клиентах, как мы говорим.
[Mehdi Tabdili] Но у нас есть другие партнеры.
[Mehdi Tabdili] Я не волнуюсь о скалировании, сколько людей мы можем принести.
[Mehdi Tabdili] Я думаю, что это больше о том, сколько...
[Mehdi Tabdili] Какие клиенты, какие проекты мы можем...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, вопрос был в том, какие стоимость-чек-сайты вам интересны для того, чтобы делать это с клиентами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сколько лицензий, сколько денег, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что, что я бы хотел, чтобы...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы можете дать мне все материалы, что вы обычно делаете с клиентами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И у меня есть какие-то лиды.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если вы хотите платить комиссию, я могу принести вам клиента.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но перед тем, дайте мне все материалы, я проверю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Talk with my friends, talk with my boss, and then we can maybe bring you a couple of customers.
[Mehdi Tabdili] Yes, and I think just to understand, just to have you, this, the arrangement we have with the people that bring us businesses can be very profitable, because just think about it for a consulting gig, right?
[Mehdi Tabdili] So let's say we get a project for a year.
[Mehdi Tabdili] Так что, кто-то вкладывает в это, и, скажем, мы платим 20% от их цены, правильно?
[Mehdi Tabdili] Так что вы получаете плату, вашу комиссию, куда-либо это деньги приходят, вы получаете плату также.
[Mehdi Tabdili] Но если вы привезете еще один проект, то он будет построен над этим, и над этим.
[Mehdi Tabdili] Поэтому каждый раз, когда вы привезете кого-то другого, первый не уйдет.
[Mehdi Tabdili] Так что у вас будет постоянная зарплата, которая приходит к вам.
[Mehdi Tabdili] Так что комиссия, как мы ее обычно устанавливали, и это было в предыдущем бизнесе, если вы не сделаете просто одновременную фигуру, потому что вы хотите иметь долгосрочную отношение.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Пожалуйста, дайте мне материалы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, возможно, дайте мне календарь, чтобы я мог позвонить с вами, и, возможно, через несколько дней я вернусь и расскажу вам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Потому что сейчас я ищу партнера, у которого есть скилл.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Википедия, интеграция, работа с компаниями и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это то, на что мы сейчас смотрим, потому что у нас недостаточно опыта и опыта.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Однако у нас есть канал, и это не американские лидеры.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мой босс, он японец, поэтому у нас есть азиатский рынок.
[Mehdi Tabdili] Я могу поделиться с вами нашим питчтеком, нашими использованиями.
[Mehdi Tabdili] Я могу даже прислать вам сампл-пропозицию, которую мы прислали, чтобы вы получили идею о среднем расстоянии контракта, который у нас есть.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я действительно должен уйти.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прошу прощения, у меня очень много мероприятий.
[Mehdi Tabdili] Не волнуйтесь, не волнуйтесь.
[Mehdi Tabdili] Я прислал вам это, и мы можем подсчетить последовательность на следующей неделе или когда у вас есть время.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Спасибо большое, Сим.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прошу прощения, я не сделал правильный разговор.
[Jonathan Archer] Не проблема.
[Jonathan Archer] Это криптопанк?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это только мой ник.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Простите.
[Jonathan Archer] Потому что в вашем профиле есть криптопанк.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, у меня есть несколько криптопанков.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Возвращаясь к криптовалюте.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я платил слишком много, честно говоря.
[Jonathan Archer] Ну, я имею в виду, что любой NFT может вернуться к пунктам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я думаю, что да.
[Jonathan Archer] Я думаю, что они имеют OG статус.
[Jonathan Archer] Все остальные, например, Apes и прочее, это как-то грязно, но пункты имеют настоящий ценовой коллектор.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Согласен, согласен.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Возьмите минуточку, я покажу вам мой экран, и, возможно, вы сможете проводить меня через инсталляцию, если это возможно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Могу я?
[Jonathan Archer] Конечно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, секунду.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прошу прощения.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И так далее, что вы сейчас делаете?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Есть какие-то успехи из прошлой недели?
[Jonathan Archer] Да, мы только что закрыли договор.
[Jonathan Archer] Наш новый ангел прилетел на борт, и это было круто.
[Jonathan Archer] Мы сейчас отправим его в безопасное место.
[Jonathan Archer] У нас еще несколько мероприятий.
[Jonathan Archer] Сегодня мы поедем в TechCrunch, чтобы узнать, с кем мы можем встретиться.
[Jonathan Archer] Я присылал множество приглашений и месседжей через LinkedIn и Twitter.
[Jonathan Archer] Посмотрим, что мы можем сделать в последние минуты.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А что насчет митинга?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы еще не готовы к митингу?
[Jonathan Archer] Я думаю, что мы можем организовать один.
[Jonathan Archer] Я бы хотел организовать один на фридай.
[Jonathan Archer] Я ждал, чтобы услышать от вас от этого парня, который мог бы нам помочь организовать митинг.
[Jonathan Archer] Но я не нашел места, где мы можем это сделать.
[Jonathan Archer] И, честно говоря, наш бюджет довольно тяжелый, так что у нас не так много капитала, чтобы это сделать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я согласен, я согласен.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Знаешь, стоимость митапа, обычно это просто стоимость пиццы.
[Jonathan Archer] Да, это замечательно, тогда мы можем это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сделать...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это как это должно быть, неправильно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, окей, окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И это, я не знаю, 300-400 баксов, это максимум.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Прошу прощения, мне нужно отдать разрешение, чтобы поделиться экраном.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А как насчет ваших пользователей?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сколько у вас пользователей?
[Jonathan Archer] У нас было около тысячи людей, которые пришли на платформу.
[Jonathan Archer] У нас было около 70 установленных Daemons, и они работают на компьютере, и у нас есть несколько платных клиентов.
[Jonathan Archer] И у нас есть еще несколько бесплатных тестов, которые скоро будут конвертированы.
[Jonathan Archer] Что-то, что я забыл сказать, мы получили партнерство с gravity.ai, поэтому мы начнем продавать ады на бесплатном уровне и даем немного бесплатного инфраструктура.
[Jonathan Archer] Таким образом, у нас появится новый ревенюсный стрим для бесплатного уровня, и мы сможем достичь больше пользователей, которые просто хотят смотреть какие-то ады для инфраструктуры.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Понятно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Странно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, так...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] 80 Тысяч регистрированных пользователей, и, может быть, активных пользователей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Обычно активные пользователи— это 5% из...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, точно.
[Jonathan Archer] Или примерно 50%.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И кодер, кто кодер?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Кодер ты или...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Моя мама.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Теперь мы все стали кодерами, да?
[Jonathan Archer] Да, точно.
[Jonathan Archer] Я виброкодер, я не кодер.
[Jonathan Archer] Вчера я встретил этого парня, у него есть платформа, где можно купить дом в одном клик-чек-оуте.
[Jonathan Archer] И ты можешь купить дом с какими-то инстантными заключениями.
[Jonathan Archer] И я спросил, как он это построил, и он сказал, что он виброкодировал его.
[Jonathan Archer] О, боже мой.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Можешь посмотреть?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, могу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, подождите.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что я должен сделать?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Создать локальную аппу?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Скинуть для сегодня?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Или...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Волт?
[Jonathan Archer] Ты уже скачивал фразу для восстановления?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да, у меня есть фраза для восстановления, но скажите, почему мне нужна фраза для восстановления?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Для чего она нужна?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я слышал, что я могу записать это в конференцию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Какие вещи будут записываться?
[Memo Guleryuz] Ваши воспоминания, ваши ключи API будут закреплены с этим.
[Memo Guleryuz] Также мы только что запускаем обновление.
[Memo Guleryuz] Вот почему, надеемся, мы сможем получить это для этого события.
[Memo Guleryuz] Мы просто запишем это в датабасе и дадим 6-дюймовому пину, который будет закреплен.
[Memo Guleryuz] Так что вам не нужно закреплять это самостоятельно.
[Memo Guleryuz] И также мы получаем десктоп-апп.
[Memo Guleryuz] Так что, да, люди могут просто загрузить это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, в любом случае, это выглядит спокойно, я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Интересно, как криптовалюта, но вы можете просто закрепить контейнер, если вы используете гугл и жемейл.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я надеюсь, что все хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Может быть, я ошибаюсь?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, я должен найти ошибку, которую я сделал, верно?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, интересно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Проблема здесь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, в любом случае, давайте я сделаю это еще раз.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что я должен сделать?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ладно, я просто выберу сейчас.
[Jonathan Archer] Да, может быть, мы можем установить новую фразу о восстановлении.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, я могу это сделать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что это только для того, чтобы сохранить некоторые мои вещи на вашей...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так.
[Jonathan Archer] Что, в основном, да, это для того, чтобы закрепить вашу память, чтобы мы не могли видеть их, ваши ключи API, такие вещи.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, так что начнем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужно донатить что-то или я просто использую...
[Memo Guleryuz] Позвольте просто проверить.
[Memo Guleryuz] Я считаю, что этот болт...
[Memo Guleryuz] Этот болт сфиксирует вас очень счастливо.
[Memo Guleryuz] Не сфиксируется, но болт сформируется, и вы не будете делать эти вещи.
[Memo Guleryuz] Но если вы зайдете на левое место, где ваш пользователь, нажмите на это, на нижнюю кнопку, на нижнюю.
[Memo Guleryuz] На нижнюю, нижнюю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, нажмите.
[Memo Guleryuz] Угу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу.
[Memo Guleryuz] О, окей.
[Memo Guleryuz] Сеттинги.
[Memo Guleryuz] Я думаю, это под фокусом.
[Memo Guleryuz] Можешь скроллить на сайдбаре?
[Memo Guleryuz] Можешь скроллить на сайтбаре?
[Memo Guleryuz] Угу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да.
[Memo Guleryuz] Да, сеттинги...
[Memo Guleryuz] Угу.
[Memo Guleryuz] Угу.
[Memo Guleryuz] И потом...
[Memo Guleryuz] Волк.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Волк.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[Memo Guleryuz] Волк заблокирован.
[Memo Guleryuz] Я думаю, что у тебя нет новой фразы, да?
[Jonathan Archer] У меня есть, но по какой-то причине она не работает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ладно, теперь я ищу новую фразу.
[Memo Guleryuz] Да, я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей и это подтверждает комментарий, что это.
[Memo Guleryuz] Окей, я сделаю это,.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, теперь я понимаю, что я могу предоставить Окей, я понял.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Открываю вот это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, теперь я должен подключить мой, я не знаю, плот, правильно?
[Memo Guleryuz] Да.
[Memo Guleryuz] Так что теперь идите вверх, скройте на сайд-бар.
[Memo Guleryuz] Окей, подключаю, правильно?
[Memo Guleryuz] Или добавьте устройство, да.
[Memo Guleryuz] Вам нужно добавить устройство, так что нажмите на это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, нет ключей.
[Memo Guleryuz] Нет ключей, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо, я подключаю мой плот, правильно.
[Memo Guleryuz] Угу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[Memo Guleryuz] Сетап девайс.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сетап девайс.
[Memo Guleryuz] Ты просто должен это вставить сейчас.
[Memo Guleryuz] Заводи этот керол-коммент.
[Memo Guleryuz] Ты должен его копировать снизу, да.
[Memo Guleryuz] И потом на терминал.
[Memo Guleryuz] Теперь у нас будет десктоп-апс, поэтому тебе не нужно делать эти вещи.
[Memo Guleryuz] Это придет и мы сейчас это строим.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу.
[Memo Guleryuz] Так что это будет очень легко.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У меня сейчас есть CLI или нормальная аппликация?
[Jonathan Archer] Сейчас у тебя оба.
[Jonathan Archer] У тебя есть CLI, но также есть веб-апп, где ты можешь общаться с моделями через веб-интерфейс.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу, угу, угу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[Jonathan Archer] Вы можете видеть, что он приближается к паре.
[Jonathan Archer] Также он подключен к кодексу Cloud Kimi Groxy Ali.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу.
[Jonathan Archer] Таким образом, мы можем подключиться полноценно.
[Memo Guleryuz] Окей, теперь мы можем вернуться к сайту.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу.
[Memo Guleryuz] Включаем сайт.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу, хорошо, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, используем этот устройство.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, включаем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Угу, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Включаем.
[Memo Guleryuz] И...
[Memo Guleryuz] Это открытие страницы, это просто...
[Memo Guleryuz] Я не знаю...
[Memo Guleryuz] Я вижу, дай секунду...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей...
[Jonathan Archer] Мы можем...
[Jonathan Archer] Как дела у тебя, оператор?
[Jonathan Archer] Как техническая неделя?
[Jonathan Archer] Ты поддерживаешь много людей?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, но, честно говоря, на субботу, на мероприятии, ребята строят очень похоже на то, что вы строите.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Они YC, XYC.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Однако, их продукты гораздо более примитивные, менее развиты, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я могу проверить мои записи, но просто ключевые записи.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] YC, XYC, я получил донат 500K и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И целый, они сделали митап тоже.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это стоимость пиццы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Много YC парней пришли.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И вы знаете, YC парни обычно, вы знаете, инвестируют в нас, YC парня.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И вы должны просто копировать эту стратегию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я был удивлен тем, что плохой продукт мог привлечь много внимания, и было много разработчиков, которые пришли на встречу, и все они установили продукт, так что было, я не знаю, 50 разработчиков, все эти макси, все установили продукт.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И это было тоже трудно, но, вы знаете, это было как...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я не знаю, если вы знакомы с MUSE или Instinct и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это был еще один форк, копийка MUSE или Instinct.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это было очень примитивно, очень-очень-очень...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это Лайда ЛЛМ?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет, нет, нет.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Имя было безумным, и UI было ужасным.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И так далее.
[Memo Guleryuz] Теперь, если вы закройте эту страницу, и зайдите в ваш OpenRR, вы можете закрыть этот диалог.
[Memo Guleryuz] Теперь вы связаны с CloudCore.
[Memo Guleryuz] После того, как вы сейчас соединены с Cloud Code, вы можете добавить другие вещи.
[Memo Guleryuz] Вы можете добавить кодексы, кимики.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но только это сейчас, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Или я могу добавить больше?
[Memo Guleryuz] Вы можете добавить многое больше.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, но по дефолту сейчас только это, да?
[Jonathan Archer] Да.
[Memo Guleryuz] И также у вас есть использование, которое мы даем вам на бесплатном тесте сейчас.
[Memo Guleryuz] Это 2 миллиона токов на каше.
[Memo Guleryuz] На DeepSeek 4.1 Slash, у вас есть диаграмма.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Зачем у вас есть аппликации?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Аппликации в аппликациях?
[Memo Guleryuz] Вы можете использовать...
[Memo Guleryuz] Вы используете десктоп-аппликацию?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да, я использую.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А, я понял, вы меняете, вы делаете...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я понимаю, что вы делаете, окей.
[Memo Guleryuz] На десктопе это намного проще.
[Memo Guleryuz] Но сейчас все, что нужно сделать, чтобы запустить это на десктоп, вы можете просто зайти в терминал снова.
[Memo Guleryuz] Если вы зайдете в терминал, и затем нажмите опен LLM chat gpt.
[Memo Guleryuz] Нет, там нет S в конце.
[Memo Guleryuz] Если вы запустите это сейчас,.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто пропаганда.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, это пропаганда.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага, и...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, я надеюсь, что это...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это рекомендовано.
[Memo Guleryuz] Окей, теперь если вы просто комментируете пространство и зайдёте в спотлайт, и нажмёте на открыть LLM, Чат-ГПТ?
[Memo Guleryuz] У вас есть Чат-ГПТ-апп?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, есть.
[Memo Guleryuz] Окей, значит, нужно было добавить чат-ГПТ в опубликацию на вашем лаунче.
[Memo Guleryuz] Может быть, это не показывает...
[Memo Guleryuz] Так, это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Должна быть в опубликации, верно?
[Memo Guleryuz] Да, должно быть здесь.
[Jonathan Archer] Ларри, это здесь.
[Memo Guleryuz] Чат-ГпТ.
[Memo Guleryuz] Если мы начнем это сейчас, то мы не будем использовать это в дальнейшем.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] А что насчет UI?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я помню, что ты показал мне очень хорошую UI, как зелёный и так далее, эти цвета, черный и зелёный.
[Memo Guleryuz] Вы можете изменить его на Darkteam, если хотите, на сайте.
[Memo Guleryuz] Теперь с десктоп-аппой у вас будет то же самое UI в вашем десктопе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, измените.
[Memo Guleryuz] Я думаю, что вы не можете использовать OpenAI LAMP в ChatGPT, если вы используете один.
[Memo Guleryuz] Я не уверен.
[Memo Guleryuz] Я не попробовал.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я помню, как это работает.
[Memo Guleryuz] Какой смартфон у вас?
[Memo Guleryuz] Это новый или старый?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это три-четыре года назад мой смартфон, но я его просто ремонтировал.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я думаю, что у меня есть много пайтеров в позиции.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думал, что если я его ремонтирую, я убью процессор, но теперь он замерзает в моем компьютере.
[Jonathan Archer] Вы можете спросить Cloud Code или Codex, чтобы сделать диагноз.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я знаю, я знаю, я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я знаю, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так, лоадим модели здесь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я вижу, вы можете менять модели здесь, я могу использовать много...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я.
[Memo Guleryuz] Заинтересован, это будет лоадить.
[Memo Guleryuz] Я имею в виду, это будет лоадить на нашей стороне, потому что это довольно медленно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да.
[Memo Guleryuz] Здесь вы можете увидеть ультра, плюс и лайт, и все остальные модели.
[Memo Guleryuz] Вы можете использовать клад-код здесь.
[Jonathan Archer] Right now you'll have Clouds connected.
[Jonathan Archer] You almost connected Grok, but you closed that tab.
[Jonathan Archer] And so you'll see, like, on the providers page of OpenLLM, you can connect all these providers.
[Jonathan Archer] So you can connect CodeX, Kimi, Grok, Cursor, Muse, and then you could also bring API keys.
[Jonathan Archer] And you'll see here, next to the tab, it says local.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я закончу сам, не волнуйтесь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Моя рекомендация.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если хотите, я могу организовать митинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы можем провести один в реальной жизни митинг и один онлайн митинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я могу привезти много инженеров, но, может быть, не много, скажем, 50 инженеров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] 30-50 Инженеров I'm going to make...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] I'm going to post it on Luma.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И вы просто должны сделать презентацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я также сделаю хорошее видео на YouTube после того, как мы закончим митап.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я имею в виду онлайн митап.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, вы знаете, мне не нужно ничего, просто давайте сделаем это.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я могу сделать митап, может быть, в следующей неделе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужно немного времени, чтобы объявить, и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, давайте начнем с онлайна.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если онлайн, вы счастливы с онлайном, вы можете сделать онлайн, Я могу найти место, поговорить с владельцами.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы также можем пытаться разговаривать с этими парнями, которые создали YC-группу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это сотрудничество в SF, которое называется Corgi, если вы помните.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы знаете Corgi, да?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, может быть, мы можем их спросить, потому что они делают много YC Meetups, и мы можем попросить их использовать, может быть, их сеть, чтобы привлечь некоторые YC Guys.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но, вы знаете, у меня тоже есть много инженеров, и это не проблема, чтобы привлечь 30-50 инженеров.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, говоря о инвесторах, если бы вы могли показать мне вашу декорацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы знаете, все инвесторы сейчас спрашивают только о одной вещь.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что такое мод?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] МОАТ.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Однако, что я вижу сейчас, множество инвесторов готовы инвестировать в характеристики.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Итак, характеристики теперь инвестируемые.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Инвесторы инвестируют в характеристики.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Даже, вы знаете, характеристики трудно монетизировать, и характеристики имеют очень низкий использование, только инженеры могут их использовать.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это все еще возможно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я вижу, как это работает.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, я попробую Да, я хотел бы.
[Jonathan Archer] Поделиться с вами, что мы, как заготовки заготовок, мы мета-лайер.
[Jonathan Archer] Мы гораздо более важны, чем заготовки, потому что мы открытый лайер для всех AI.
[Jonathan Archer] Теперь мы начали работать над интеграцией в команду.
[Jonathan Archer] Команда будет этой дашборд, где манажеры могут видеть всю использованность, могут быть соединенные памяти между командами, это очень легко донатить МЦП на всех компьютерах.
[Jonathan Archer] Также для личного пользователя, мы сможем достигать больше, чем для разработчиков.
[Jonathan Archer] Сейчас это немного тяжелее для разработчиков, логинный процесс, но с аппаратом Desktop это будет намного более стремленно, так что кто-то может начать использовать его сразу, и они смогут получать наиболее из этого.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, окей.
[Jonathan Archer] И также, я бы сказал, что, к сожалению, мы уходим на субботу.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага, мы согласны.
[Jonathan Archer] У нас будет конкурс на следующей неделе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Тогда, вы знаете, я думаю, что это хорошо, чтобы делать онлайн-конкурсы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас есть онлайн-конкурсы, делайте онлайн-конкурсы.
[Jonathan Archer] Да, хорошо, давайте сделаем это онлайн, и потом я передам вам мой дек, наш дек, сейчас, чтобы вы посмотрели.
[Jonathan Archer] Если у вас есть кто-то в вашей сети, кто бы хотел бы провести встречу с нами в следующие несколько дней, мы полностью доступны, чтобы поговорить с инвесторами до воскресенья, и это то, что мы здесь делаем.
[Jonathan Archer] И здесь, когда мы говорим о использовании OpenLLM Pro, вы можете использовать технику, Под субтитрами на левой стороне есть промо-код, и вы можете поставить танк-жизни.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, я хочу поддержать вас, вы знаете, плюс один больше...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто стоимость капли кофе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мы купили кофе, кофе и я.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В любом случае, спасибо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас все в порядке, давайте попробуем организовать онлайн-митинг.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я принесу моих инженеров, тех, кого я знаю.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я также принесу потрясающего гостя, который может вас интервьюировать, и этот гость имеет опыт в фондозировании.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он работал в инкубаторах, работал с стартовыми компаниями и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он может задать вам правильные вопросы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И потом, это видео, YouTube, Вы можете также использовать это позже для вашего фонаря, потому что это будет хороший демо-звонок.
[Jonathan Archer] Отлично.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Отлично.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Что мне нужно?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужна ваша дека, и потом я сделаю некоторые материалы, которые я отправлю моим инженерам, и вы должны оправдать это, потому что я не хочу делать Я не хочу написать что-то, на что вам не комфортно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я понял, что у вас есть характеристики, и Тим, на самом деле, это хорошая идея, потому что я только что получил звонок.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Почему я поздно?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я получил звонок с человеком, который делает продажи B2B.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Он называется Мехди, он антропический интегратор, но не только антропический, он работает с B2B клиентами и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это, наверное, твой потенциальный клиент.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] У тебя есть две опции, чтобы продать продукт, через интеграторы или прямо в компаниях, но прямо это всегда сложнее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ты должен иметь сельский департамент, который делает интеграцию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это довольно больно.
[Memo Guleryuz] оператор, я хочу показать тебе что-то там.
[Memo Guleryuz] Это мой экран.
[Memo Guleryuz] Я на отделении разработки.
[Memo Guleryuz] Это мой экран?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, это твой экран.
[Memo Guleryuz] Теперь мы добавляем это, это наш следующий шаг в направлении Enterprise и Teams.
[Memo Guleryuz] У вас будет такой маркетплейс, и вы можете включить любые из этих интеграций, которые соответствуют всем членам команды.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага, окей, так...
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это будет огромное для команд.
[Memo Guleryuz] Огромное.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если мы сделаем NEMCP и так далее, я могу привезти МСП к вашему маркетплейсе, верно?
[Memo Guleryuz] Да, и мы поддержим даже публичные и приватные рынки, так что мы можем проверить вас и сказать, что это оператор.
[Memo Guleryuz] Если вам нравится оператор и его продукт, мы можем его включить прямо сейчас.
[Jonathan Archer] Да, это огромное.
[Jonathan Archer] Мы можем стать огромным каналом распространения.
[Jonathan Archer] И когда мы говорим о продаже B2B, как вы упомянули, я хотел бы сказать, что мы уже начали общаться с консультантами.
[Jonathan Archer] Например, этот крутой парень, с которым вы меня приглашали в Cloud Coder House.
[Jonathan Archer] Я встретился с ним, и я пошел сфотографироваться, и он стал моим другом.
[Jonathan Archer] И он сказал, что он начнет пытаться продавать OpenLLM для своих клиентов.
[Jonathan Archer] И мы встретили еще одного консультанта на понедельник вечером.
[Jonathan Archer] Он тоже начнет поддерживать OpenLLM, нам просто нужно сделать последовательный звонок с ним.
[Jonathan Archer] И мы уже думали о том, как эти люди станут партнерами распространения, а также, кто они, как они называются, я не знаю, открывающие и инкубаторы, правильно?
[Jonathan Archer] У тебя есть инкубатор, ты можешь зайти в все компании в твоем инкубаторе и сказать, о, ты должен использовать OpenLLM, потому что это замечательный продукт, и он поможет твоей команде быть намного быстрее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Ага, ага, ага.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Окей, и ты сейчас вернешься в Латам, или ты отправишься в США?
[Jonathan Archer] Нет, мы вернемся в Латам сейчас.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, что это не имеет значения.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] На данный момент, вы можете просто выбрать Google Meet и Zoom для закрытия договора.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Не нужно быть в NBA.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что это не проблема.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Однако, в ноябре будет большая конференция, а также ЛМ-конференция, AI-конференция.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы будете в NSF сейчас?
[Jonathan Archer] Я могу быть, особенно если...
[Jonathan Archer] Вы уверены?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Вы уверены о конференции?
[Jonathan Archer] Нет, я не уверен.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Попрошу вас, Клод, дать информацию.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это будет между 10 и 12 ноября.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Эти три дня будут большие мероприятия.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Будут конференции от 10 до 12.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но это больше как, вы знаете, вы должны быть приглашены.
[Jonathan Archer] AI Engineer Code Summit.
[Jonathan Archer] Аппликация только, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, да.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И я надеюсь, что будет много сайтов.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но есть еще один вариант, который стоит 12 тысяч, организован по церебральному вилле.
[Jonathan Archer] Да, я слышал, что они организатор хак-атона, верно?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, они строят коммуники, организуют мероприятия, у них есть список всех мероприятий, AI-мероприятий и так далее.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто, как мы знаем, хаб для всех.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но, в любом случае, для начала, подсказка.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Позвольте мне помочь вам с этим мероприятием.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нравится этот продукт.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Думаю, с кем я могу вас представить?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И, может быть, позже вы можете добавить меня в вашу команду, в случае, если я смогу приобрести вашу цену.
[Jonathan Archer] Да, конечно.
[Jonathan Archer] Я думаю, что для этого есть много возможностей.
[Jonathan Archer] Одно, что нам нужно сделать, это обеспечить финансирование, чтобы мы могли платить людям.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Расскажите нам о ваших ценах.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Сколько вы зарабатываете в месяц и сколько вы зарабатываете?
[Jonathan Archer] На данный момент у нас очень мало денег.
[Jonathan Archer] Мы просто платим небольшие зарплаты Memo и DOA.
[Jonathan Archer] DOA, извините, это наш инженер UI-UX, но это очень-очень маленькая зарплата для того, чтобы они приехали.
[Jonathan Archer] И да, наши цены, чтобы поддерживать OpenLLM, довольно низкие.
[Jonathan Archer] Может быть, 500 долларов в месяц.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошая идея.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] В моем случае, я заработал деньги на стартапы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я думаю, что за предстоящее время, это примерно 1 млн.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] 1 Млн-2 млн, зависит от цены.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но я думаю, что 1 млн до 2 млн, это вполне возможно.
[Jonathan Archer] Да.
[Jonathan Archer] оператор, кстати, мы вырастим 1 миллион, и я думаю, что это очень действительно.
[Jonathan Archer] И теперь это время наступить.
[Jonathan Archer] Эти следующие 2 недели и первые 2 недели ноября.
[Jonathan Archer] Так что мы действительно благодарны за всю поддержку, которую мы получили.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Хорошо, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я подумаю, и я буду делать что-то интересное.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Большое спасибо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Будьте в курсе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Я ищу вашу деку.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужна ваша деку, чтобы лучше понять вас, лучше представить вам.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Мне нужна ваша деку, последняя деку, с хорошим рейтингом, потому что это единственное, что, знаете, инвесторы сейчас ищут.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас есть какие-либо интересные моменты в ваших интересных слайдах, хорошо.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Если у вас есть идея о размере рынка зацепок, скажите мне.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Так что, это приятно, Мему, Джонатан.
[Memo Guleryuz] Да, потрясающе, чувак.
[Memo Guleryuz] Очень приятно познакомиться с тобой.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, вы, ребята, хорошая команда, и, вы знаете, надеемся, что мы сможем сделать что-то.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] И да, я также попробую провести день, используя это немного больше.
[Jonathan Archer] Потрясающе.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Да, но, кстати, вы пробовали другие проекты, которые я вам рассказал, BB и так далее?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] I can tell which I'm using right now.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] CC Switch, BB, OpenChamber, CCGUI.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] You're not familiar with any, right?
[Jonathan Archer] No, I'm not.
[Memo Guleryuz] No.
[Memo Guleryuz] These are competitions that you found?
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Нет, это конкуренты, которые я использую, это какие-то конкуренты.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но вы должны быть осознательны.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Это просто агрегаторы.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Конечно, если вы позиционируете себя, например, на рынке, то позиционирование очень важно.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Но что я вам сказал, это просто агрегаторы.
[Memo Guleryuz] Да, мы проверим.
[[ИМЯ] [ФАМИЛИЯ] (Palo Alto AI Research Lab)] Спасибо!

---

**Claude:**

{"lang":"mixed","one_line":"оператор (Palo Alto AI Research Lab) провёл короткий звонок с Мехди Табдили (интегратор Anthropic, предложил партнёрскую комиссию за клиентов), затем помогал команде OpenLLM (Джонатан Арчер, Memo Guleryuz) настроить продукт и обсуждал онлайн-митап, дек и интро к инвесторам.","participants":[{"name":"[ИМЯ] [ФАМИЛИЯ]","role":"our-side","channel":"microphone"},{"name":"Mehdi Tabdili","role":"lead","channel":"speaker"},{"name":"Jonathan Archer","role":"lead","channel":"speaker"},{"name":"Memo Guleryuz","role":"lead","channel":"speaker"}],"commitments":[{"owner":"Mehdi Tabdili","what":"Прислать питчдек, кейсы использования и пример коммерческого предложения; созвониться на следующей неделе","due":"следующая неделя","quote":"Я могу поделиться с вами нашим питчтеком, нашими использованиями."},{"owner":"Mehdi Tabdili","what":"Отправить материалы и согласовать следующий созвон","due":"следующая неделя","quote":"Я прислал вам это, и мы можем подсчетить последовательность на следующей неделе или когда у вас есть время."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Проверить материалы Мехди, обсудить с друзьями и боссом, затем, возможно, привести пару клиентов за комиссию","due":"через несколько дней","quote":"Talk with my friends, talk with my boss, and then we can maybe bring you a couple of customers."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Организовать онлайн-митап (30-50 инженеров), выложить на Luma, после записать видео на YouTube","due":"следующая неделя","quote":"Я могу сделать митап, может быть, в следующей неделе."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Привести гостя с опытом в фандрайзинге и инкубаторах для интервью с командой OpenLLM","due":"","quote":"Я также принесу потрясающего гостя, который может вас интервьюировать, и этот гость имеет опыт в фондозировании."},{"owner":"Jonathan Archer","what":"Передать оператору актуальный дек","due":"сейчас","quote":"давайте сделаем это онлайн, и потом я передам вам мой дек, наш дек, сейчас, чтобы вы посмотрели."},{"owner":"[ИМЯ] [ФАМИЛИЯ]","what":"Подумать, с кем представить OpenLLM, и поискать интро к инвесторам","due":"","quote":"Думаю, с кем я могу вас представить?"},{"owner":"Memo Guleryuz","what":"Проверить конкурентов-агрегаторов (CC Switch, BB, OpenChamber, CCGUI), названных оператором","due":"","quote":"Да, мы проверим."}],"facts":[{"fact":"Компания Мехди: интегратор Anthropic, около 20 человек с сертификациями Anthropic, партнёр по программе Anthropic, растёт 6-8 месяцев органически.","quote":"У нас около 20 людей, которые получили антропические сертификации."},{"fact":"Мехди продал предыдущую сетевую компанию 1,5 года назад и запустил текущий бизнес с партнёром.","quote":"У меня есть компания, которую я продал 1,5 года назад."},{"fact":"Бизнес-модель Мехди: фиксированные цены для малого бизнеса, движение в сторону managed services с ежемесячной поддержкой.","quote":"Но я думаю, что мы начинаем двигаться в сторону управления сервисами"},{"fact":"Партнёрская комиссия Мехди порядка 20% и повторяется с каждого проекта на всём протяжении сотрудничества.","quote":"скажем, мы платим 20% от их цены, правильно?"},{"fact":"Клиенты предыдущего инкубатора оператора включали Foxconn и ANA, много корейских, японских и тайских B2B-клиентов; босс оператора японец.","quote":"Foxconn, например, был одним из наших клиентов."},{"fact":"OpenLLM: около 1000 человек пришло на платформу, около 70 установленных демонов, несколько платных клиентов, партнёрство с gravity.ai (реклама на бесплатном тире).","quote":"У нас было около тысячи людей, которые пришли на платформу."},{"fact":"OpenLLM только что закрыла нового ангела; цена подписки порядка 500 долларов в месяц; денег мало, платят небольшие зарплаты инженерам; планируют поднять 1 млн.","quote":"оператор, кстати, мы вырастим 1 миллион, и я думаю, что это очень действительно."},{"fact":"OpenLLM подключается к Claude Code, Codex, Kimi, Grok, Cursor и другим провайдерам, есть CLI и веб-приложение, десктоп-апп в разработке, бесплатный тест 2 млн токенов на DeepSeek.","quote":"Также он подключен к кодексу Cloud Kimi Groxy Ali."},{"fact":"OpenLLM строит командный дашборд и маркетплейс MCP-интеграций для Teams/Enterprise (публичный и приватный).","quote":"Теперь мы добавляем это, это наш следующий шаг в направлении Enterprise и Teams."},{"fact":"Мероприятие AI Engineer Code Summit 10-12 ноября, вход по приглашению; альтернативный вариант за 12 тысяч от Cerebral Valley.","quote":"Это будет между 10 и 12 ноября."},{"fact":"Стоимость митапа по оценке оператора 300-400 долларов (пицца); у OpenLLM бюджет очень ограничен.","quote":"И это, я не знаю, 300-400 баксов, это максимум."}],"objections":[{"objection":"Нет денег и места для проведения митапа в оффлайне, бюджет тяжёлый","by":"Jonathan Archer","quote":"И, честно говоря, наш бюджет довольно тяжелый, так что у нас не так много капитала, чтобы это сделать."},{"objection":"Продукт сложно монетизировать: инвесторы спрашивают про moat, а у dev-инструментов низкое использование и только инженеры пользуются","by":"[ИМЯ] [ФАМИЛИЯ]","quote":"Даже, вы знаете, характеристики трудно монетизировать, и характеристики имеют очень низкий использование, только инженеры могут их использовать."},{"objection":"Конкуренты (CC Switch, BB, OpenChamber, CCGUI) по сути агрегаторы, важно позиционирование","by":"[ИМЯ] [ФАМИЛИЯ]","quote":"Но вы должны быть осознательны."},{"objection":"Сейчас логин-процесс тяжеловат для разработчиков, пока нет десктоп-аппа","by":"Jonathan Archer","quote":"Сейчас это немного тяжелее для разработчиков, логинный процесс"},{"objection":"У оператора нет времени, нужно быстро закончить первый разговор","by":"[ИМЯ] [ФАМИЛИЯ]","quote":"Так что, честно говоря, у меня нет времени."}],"alpha":[{"signal":"Мехди (Anthropic-интегратор) платит ~20% повторяющейся комиссии за приведённых клиентов, и оператор может использовать азиатский канал (Foxconn, ANA, корейские клиенты) как реферальный","why":"Готовая партнёрская модель с рекуррентной комиссией, закрывает недостаток у оператора интеграционной экспертизы","quote":"Если вы хотите платить комиссию, я могу принести вам клиента."},{"signal":"оператор видит возможность сводить OpenLLM с интеграторами: Мехди — потенциальный канал/клиент OpenLLM (продавать через интеграторов проще, чем напрямую)","why":"Интро между двумя лидами создаёт ценность для обеих сторон и позиционирует оператора как коннектор","quote":"Это, наверное, твой потенциальный клиент."},{"signal":"Консультанты уже начали продавать OpenLLM своим клиентам; инкубаторы названы каналом дистрибуции","why":"Дистрибуция через интеграторов и инкубаторы подтверждается самой командой","quote":"Он сказал, что он начнет пытаться продавать OpenLLM для своих клиентов."},{"signal":"Окно сбора 1 млн у OpenLLM: следующие 2 недели и первые 2 недели ноября; нужны интро к инвесторам и свежий дек","why":"Чёткий срок, в который интро оператора максимально ценны; торг об условиях/доле возможен (оператор намекнул войти в команду)","quote":"Эти следующие 2 недели и первые 2 недели ноября."},{"signal":"оператор предложил позже войти в команду OpenLLM","why":"Потенциальная позиция/доля для оператора в обмен на привлечение инвесторов и сообщества","quote":"И, может быть, позже вы можете добавить меня в вашу команду, в случае, если я смогу приобрести вашу цену."},{"signal":"оператор заметил конкурирующий YC-продукт, который привлёк 50 разработчиков на митапе с затратами в стоимость пиццы; стратегию митап + YC-сеть (Corgi) стоит копировать","why":"Дешёвый проверенный growth-канал для OpenLLM и контент для оператора (Luma, YouTube)","quote":"И вы должны просто копировать эту стратегию."},{"signal":"Инвесторы сейчас готовы вкладывать в dev-tools, но спрашивают только про moat","why":"Дек OpenLLM должен отвечать на вопрос про moat (мета-слой над всеми AI) и размер рынка","quote":"Что такое мод?"}]}
