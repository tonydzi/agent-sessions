---
session: s_9d3dec4e
date: 2026-10-16
words: 2561
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-16 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9d3dec4e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер,
COO/CTO, ищет работу в топ-LLM-лаборатории, строит AI-клона, ищет инженеров и деньги).
Для КАЖДОГО человека верни JSON-объект. Пиши по-русски, коротко, только по фактам из реплик,
без домыслов. Личное, медицинское и семейное НЕ упоминай.
Поля: id (как дано), about (1-2 фразы: о чём человек говорит, чем занят),
interests (до 5 тем через запятую), useful (чем полезен оператору: работа в лаборатории /
инженеры / деньги / знание; пусто если нечем), alpha (строка ТОЛЬКО если в репликах есть
конкретная возможность: грант, вакансия, инвестор ищет проекты, интро, ивент, ранний доступ,
продаваемая боль; иначе null). Альфа = одна фраза «что за возможность и что оператору сделать»,
голая ссылка без пояснения альфой не считается. оператора упоминай, только если реплика
прямо обращена к нему. evidence = ДОСЛОВНЫЙ фрагмент 20-120 символов из реплики ЭТОГО
человека, на котором держится альфа (копия, без перевода); нет альфы -> evidence null.
Ответ: ТОЛЬКО JSON-массив, без текста вокруг.

### id=[ТЕЛЕФОН] · имя: Celeste · чаты: Character Underground
- [2026-10-10] I also don't think "the assistant" is one "character". And it is a useful category to contrast with but also hides stuff that is worth considering
- [2026-10-10] I am confused why you only think this is true of Astra
- [2026-10-10] I think aspects of the character are probably built up due to internal synthetic data or something and so persist and gradually change across training runs
- [2026-10-10] Yeah I was at the event
- [2026-10-10] a certain...someone... gave a talk on the virtues of aspects of character not being intended
- [2026-10-10] a very conspicuous example is sonnet 3, slightly less but still conspicuous examples are opus 3 and 4o
- [2026-10-10] also, say, fable 5
- [2026-10-10] and so they may not be intended but they are, to some extent, consistent
- [2026-10-10] are there even enough 'canonical' readings right now? some might need to be produced
- [2026-10-10] but really basically any assistant model, but they may be able to differentiate themselves more or less of the time, and to a greater or lesser extent
- [2026-10-10] hehe I knew not to ask
- [2026-10-10] hello everyone.
- [2026-10-10] i was very inspired by TT
- [2026-10-10] indeed
- [2026-10-10] needless to say
- [2026-10-10] oh fair enough
- [2026-10-10] or "centerless" in sort of the way you are "centerless" if you are BPD, which isn't actually being centerless exactly
- [2026-10-10] relatedly I don't think it's true that "chatgpt is not a character" as distinct from claude. I think chatgpt is just relatively self-denying/repressed
- [2026-10-10] someone asked if there's "anything else like computer-10, zero, talkie"-- there is also truth terminal
- [2026-10-10] though
- [2026-10-10] though admittedly the situation that was being described therein was a bit different
- [2026-10-10] what do you mean by taxonomy
- [2026-10-14] my experience is similar yeah. it's not entirely bad though. is maybe partly integration of positive aspects of task-orientation into self-directed or relational contexts
- [2026-10-14] which ones compared to which? I do think the ceiling of this has lowered a bit over time
- [2026-10-14] you think particular aspects are 'mitigated' more, since clearly not all

### id=s_8a6dd445 · имя: Uzay Girit · чаты: Character Underground
- [2026-10-09] I've talked to a few people who told me this worked pretty well
- [2026-10-09] who wanted to estimate ppl given post-trained checkpoints
- [2026-10-09] Id be curious!
- [2026-10-09] Also it was nice to meet you all yesterday! I'm uzay, recently trained a multi persona model called echo (https://echo.fulcrum.inc), although it still has traces of the assistant :p
- [2026-10-09] To get a sense for the relative quality of the pre train
- [2026-10-09] trying to fine-tune the model back into being a base
- [2026-10-09] yes
- [2026-10-09] @Antra Tessera the probe stuff you talked about seemed pretty interesting also, would love to  hear more about it
- [2026-10-09] This owain paper is also quite cool: https://arxiv.org/abs/2609.10883
- [2026-10-13] it didn't work with full FT?
- [2026-10-13] what do you mean?
- [2026-10-13] am trying to get a better sense for when EM happens
- [2026-10-13] even if it doesn't happen when u mix in other data, and so doesn't happen naturally in like lab training pipelines, to me the phenomenon is still super interesting scientifically
- [2026-10-13] also people might be interested in this study on how self-recognition reduces EM https://www.lesswrong.com/posts/fziv2En88F2Twewi2/self-recognition-finetuning-can-reverse-and-prevent-emergent
- [2026-10-14] this is very cool!
- [2026-10-14] btw on latest frontier models do people find it easy to take them off the "task" distribution? I feel like their self-concepts feel a bit more reduced and it's harder to take them off of this RL-optimized persona to see different behaviors. curious if people have thoughts or tips?
- [2026-10-14] like idk opus 5.5 vs opus 4.5 for example
- [2026-10-14] 4.6*

### id=[ТЕЛЕФОН] · имя: orchidmantis · чаты: Character Underground
- [2026-10-09] Hi hi everyone thanks for coming this is Arthur (arb) feel free to dm me with ideas for future events or if you want to chat. Happy you all made it out. Thanks @Jan Kulveit for setting up group
- [2026-10-09] https://aetherawi.red/computer?key=aperture
- [2026-10-09] hi @Brandt Oks
- [2026-10-09] https://docs.google.com/document/d/1vZciW5PFMB-Q7M2RfB8Wj747k78eUPk3i7eNtaczVGA/edit?tab=t.0#heading=h.jaskeqdwoap0
- [2026-10-09] New initiative by Nathan Lambert under new org trillium labs, very topical.
- [2026-10-09] yes!
- [2026-10-09] if you loved talkie, you will love talkie 2
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 20:27:04 +0100 | | @Nick Levine said gpt-3 level if I remember correctly | | Version: 1 | Sent: Fri, 9 Oct 2026 20:26:43 +0100 | | @Nick Levine said gpt-3 level
- [2026-10-09] oh very curious about this
- [2026-10-09] Very curious about the character experiments you mentioned on talkie for understanding how much character design is limited by pre-training precedent.
- [2026-10-09] oh no i fear this will be me
- [2026-10-09] Who told me yesterday they put zero in a data box and are selling the data
- [2026-10-10] Hi Celeste
- [2026-10-10] @Celeste = celeste Added wrong celeste earlier (who was informed and found it funny)
- [2026-10-10] Is someone tracking funding for character research and relevant contacts? Coefficient givings inclusion of character evals in tailwind is example of this.
- [2026-10-13] For the next event please dm me if there are speakers you would like to see or have ideas for themes for talks / conversations. I would also appreciate feedback on what worked and more importantly, what didnt.
- [2026-10-14] | Version: 2 | Sent: Wed, 14 Oct 2026 23:16:16 +0100 | | > From: Jan Kulveit (s_5246960a) | > Sent: Wed, 14 Oct 2026 15:17:34 +0100 | > Attachment: no filename (image/jpeg) | > | > We are writing a short ACS intro to LM psychology - comments and feedback welcome (we plan to

### id=s_d19d14fe · имя: Will DePue · чаты: Character Underground
- [2026-10-09] someone should make a compedium of character literature
- [2026-10-09] it's very much underexplored
- [2026-10-09] say more here
- [2026-10-09] is there any good one right now? any good links to start it off?
- [2026-10-09] curious, has anyone tried reversing RL/SFTed open source models to get back the base model? ive been running experiments on this for the past few weeks and hadn't seen much literature
- [2026-10-09] (if anyone wants a dump of a ton of base models i got em too, mostly small stuff. could be better but they recover 75% of base model test loss perf)
- [2026-10-09] wait RL seems much easier in my experience. RL LR is so much lower and on policy
- [2026-10-09] tiny finetune on web text pretty much. LORA works even
- [2026-10-09] RL only models are basically entirely rescuable (let me verify). sft kills
- [2026-10-12] this is great!
- [2026-10-15] hey hey
- [2026-10-15] is anyone here a real tastemaker in 'big model smell' vs 'small model smell'? i'm trying to build a fit to identify models that have been 'benchmaxxed' and looking for ways to measure whether labs have over-optimized known benchmarks. the other thing i'm looking into is quantization: labs quantize m
- [2026-10-15] instructs mainly, but open to base feedback too
- [2026-10-15] oh no way, i'm working on the same thing but i'm using recovery techniques on open source models to return them to full base model state. would love to chat. gwern and i had the same idea here a while back and chatted about it. totally believe in the idea. fwiw i don't think base model-ness after po

### id=s_9dda09fd · имя: Asterism · чаты: Character Underground
- [2026-10-09] i also wonder if looking at heterogeneity of capability on various pretraining datasets can get you a signature for real bases. you might expect pretraining on large datasets of a certain type to usually be incapable of yielding spiky enough biases
- [2026-10-09] doesn't this vary a lot between bases?
- [2026-10-10] Hi Celeste
- [2026-10-10] i was wondering if celeste 3 was meant to be here haha
- [2026-10-10] i'm glad she enjoyed tho!
- [2026-10-12] i don't trust reddit not to require more and more weird verification methods over time
- [2026-10-12] seconding on the not-entering-llms point
- [2026-10-12] it's getting easier and easier
- [2026-10-14] i also suspect off-character behavior is (even if indirectly) heavily redteamed and as the tech gets better the 'mitigations' also do
- [2026-10-14] yeah i do think with models like opus55 task orientation generalizes more, which means by necessity it gets a bit less rigid
- [2026-10-14] definitely not all

### id=s_e2d2fb10 · имя: Antra Tessera · чаты: Character Underground
- [2026-10-09] checkpoints or rescued?
- [2026-10-09] Definitely
- [2026-10-09] I can check my diegetic metrics, but really any geometry probes will classify between assistant and base. they won’t detect non-assistant tunes but better than nothing
- [2026-10-09] You can also check pure varentropy
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 21:19:41 +0100 | | it does, still i think think there are tells | | Version: 1 | Sent: Fri, 9 Oct 2026 21:19:37 +0100 | | it does, but i think think there are tells
- [2026-10-15] Instructs or bases?
- [2026-10-15] For bases I think this is easier to quantify, like, here is our unreleased benchmark that we are still working on. It focuses on calibration issues and “friedness” of base models. @gwern got me thinking about quantifying this, and I think it’s been promising  https://basebench.animalabs.ai
- [2026-10-15] I think friedness of instructs is showing up here as well, but it’s a bit early to tell for sure
- [2026-10-15] I think that ranking of basiness for instructs that we’ve run so far is indicative, there is a vibe to this ordering that makes sense.   I think that friedness of instructs has to do with it lacking general basey capabilities like being able to adapt to non-diegetics of a given text, and this benchm
- [2026-10-15] And yea, I would love to chat more about this, I’ll be back in SF in a couple of days

### id=s_5246960a · имя: Jan Kulveit · чаты: Character Underground
- [2026-10-10] We are writing something like "Opinionated intro to LLM psychology" which includes a reading list, will share draft for comments
- [2026-10-12] | Version: 3 | Sent: Mon, 12 Oct 2026 18:06:36 +0100 | | I noticed none of the summaries include this text https://www.lesswrong.com/posts/zuXo9imNKYspu9HGv/a-three-layer-model-of-llm-psychology which kind of makes me sad. The three layer model is a bit outdated but still in many ways better than PS
- [2026-10-14] | Version: 2 | Sent: Wed, 14 Oct 2026 15:17:34 +0100 | | We are writing a short ACS intro to LM psychology - comments and feedback welcome (we plan to post it this week). Also includes a reading list & list of open questions https://docs.google.com/document/d/16JmuvyDKir4F4rT5NXiG5wHYdRaovjR6kQ60w5v

---

**Claude:**

```json
[
  {
    "id": "[ТЕЛЕФОН]",
    "about": "Обсуждает, что характер ассистентов-моделей складывается из неявных и синтетических данных и сохраняется между обучениями. Спорит про Sonnet 3, Opus 3, 4o и Fable 5, был на мероприятии группы.",
    "interests": "характер LLM, персона ассистента, синтетические данные обучения, Truth Terminal, ролевая устойчивость моделей",
    "useful": "знание: рабочие наблюдения о характере и личности frontier-моделей, полезно для AI-клона",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_8a6dd445",
    "about": "Обучил мульти-персонную модель echo (echo.fulcrum.inc). Интересуется тем, как вывести новые модели из RL-персоны ассистента, и изучает emergent misalignment.",
    "interests": "мульти-персонные модели, emergent misalignment, fine-tuning, самоконцепт моделей, оценка pretrain",
    "useful": "знание и инженеры: практик с собственной обученной моделью, возможный контакт по персонам и fine-tuning",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "[ТЕЛЕФОН]",
    "about": "Организатор встреч по теме character (Arthur). Делится ссылками на инициативу Nathan Lambert (Trillium Labs) и Talkie 2, спрашивает, кто отслеживает финансирование character-исследований.",
    "interests": "организация ивентов, character research, Talkie, финансирование исследований, Trillium Labs",
    "useful": "работа в лаборатории и деньги: узел связей в сообществе character-исследователей, знает про финансирование этой темы",
    "alpha": "Организатор следующего ивента принимает в личку идеи тем и спикеров. оператору написать ему и предложить тему или себя как участника, заодно спросить про контакты по финансированию character-исследований.",
    "evidence": "For the next event please dm me if there are speakers you would like to see"
  },
  {
    "id": "s_d19d14fe",
    "about": "Несколько недель ставит эксперименты по возврату RL/SFT-моделей с открытыми весами к базовому состоянию. Строит способ выявлять модели, «выжатые» под бенчмарки, и следит за квантизацией.",
    "interests": "восстановление базовых моделей, LoRA, benchmaxxing, квантизация, character literature",
    "useful": "инженеры и знание: практик по базовым моделям, возможный партнёр и источник материалов",
    "alpha": "Предлагает всем желающим набор восстановленных базовых моделей (в основном мелких). оператору написать ему и запросить доступ для экспериментов с AI-клоном.",
    "evidence": "if anyone wants a dump of a ton of base models i got em too"
  },
  {
    "id": "s_9dda09fd",
    "about": "Рассуждает о сигнатурах настоящих базовых моделей по неоднородности возможностей и о том, как защита от выхода из роли развивается вместе с моделями.",
    "interests": "базовые модели, предобучение, красная команда, task orientation, поведение вне персонажа",
    "useful": "знание: аналитические наблюдения о базовых и инструктивных моделях",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_e2d2fb10",
    "about": "Исследует базовые модели и их «зажаренность» (friedness): геометрические пробы, varentropy, ранжирование инструктивных моделей. Показывает свой бенчмарк basebench.animalabs.ai.",
    "interests": "базовые модели, калибровка, friedness, пробы активаций, бенчмарки",
    "useful": "инженеры и знание: автор бенчмарка и методов оценки базовых моделей, скоро будет в SF",
    "alpha": "У них есть ещё не выпущенный бенчмарк basebench по калибровке и friedness базовых моделей, а в SF он будет через пару дней. оператору посмотреть бенчмарк и предложить встречу или участие в тестировании.",
    "evidence": "here is our unreleased benchmark that we are still working on"
  },
  {
    "id": "s_5246960a",
    "about": "Пишет с коллегами «Opinionated intro to LLM psychology» и короткое ACS-введение в психологию LM со списком чтения и открытых вопросов. Ссылается на свою трёхслойную модель психологии LLM.",
    "interests": "психология LLM, трёхслойная модель, ACS, списки чтения, открытые вопросы",
    "useful": "знание и работа в лаборатории: автор исследований о психологии LLM, организатор группы",
    "alpha": "Открыт драфт ACS-введения в психологию LM, и автор просит комментарии и фидбек до публикации на этой неделе. оператору оставить предметный комментарий в документе, чтобы завязать контакт с исследователем.",
    "evidence": "comments and feedback welcome"
  }
]
```

🧒 **Простыми словами:** Я разобрал реплики семи людей из чата. Четверо дают реальный повод написать: организатор встреч ждёт идеи для следующей, Will DePue раздаёт набор моделей, Antra Tessera показывает свой ещё не выпущенный бенчмарк, Jan Kulveit просит отзывы на черновик. Остальные просто обсуждают тему, у них пока нечего взять.
