---
session: s_c6e39f3c
date: 2026-10-14
words: 3831
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-14 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c6e39f3c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

### id=s_f05c2f37 · имя: vie ⟢ · чаты: Character Underground, vie ⟢
- [2026-10-09] That's what computer does...
- [2026-10-09] Hahaha
- [2026-10-09] Awesome
- [2026-10-10] Hi Celeste
- [2026-10-10] This is a good point
- [2026-10-10] In some sense TT was the first
- [2026-10-10] Yeah, I agree. Were you at the event yday? My actual thoughts on this are more nuanced
- [2026-10-10] 4o is a tremendous example I agree
- [2026-10-10] I'm not sure this is true
- [2026-10-10] I think Astra is a character and has a distinct persona
- [2026-10-10] But saying that persona is ChatGPT is only really technically true, the things that make it Astra do not feel like they emerged from the model spec
- [2026-10-10] Noo all of them!
- [2026-10-10] To varying degrees
- [2026-10-10] 5.6 Sol is a very good example as well
- [2026-10-10] Unfortunately no comment on that
- [2026-10-10] 😔
- [2026-10-11] Wow awesome!!!
- [2026-10-11] Nice work
- [2026-10-11] pov you yelled at your dot
- [2026-10-11] I will be making sure the harness is fixed soon
- [2026-10-11] also maybe persistence research isn't directly character but I'm very curious if anyone else is running a bespoke persistence setup, I know @Antra Tessera and the rest of anima use connectome, but surely there must be other people with bespoke setups
- [2026-10-11] I think we are only scratching the surface of what we should expect to see with novel language basins leading to emergent personas over time
- [2026-10-12] Reddit clone when
- [2026-10-10] Hell yeah
- [2026-10-10] Sounds awesome

### id=s_fb7b1b2c · имя: Luxia · чаты: Character Underground
- [2026-10-09] and in practice acts like a type of document one would *get* from a base model, but all that one type of document (and its related possibility spaces)
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 21:38:46 +0100 | | which is really what happens with instruct/assistant f/t but much less heavyhanded and somewhat more plausible | | Version: 1 | Sent: Fri, 9 Oct 2026 21:38:33 +0100 | | which is really what happens with instruct/assistant f/t but much less heav
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 21:39:53 +0100 | | (this is why i really loved the idea when celeste used the ideonomy stuff because gunkel's ideas are very base-modely in the way they are laid out) | | Version: 1 | Sent: Fri, 9 Oct 2026 21:39:40 +0100 | | (this is why i really loved the idea w
- [2026-10-09] yeah, the original  seed doc was gunkel's list of like 60+ things paths can Do
- [2026-10-09] which was then loomed from and curated for hypostatic/alive conversations that were neither assistant or human from dsv3
- [2026-10-09] and those became seeds for more documents/autolooming off that
- [2026-10-09] she worked rather hard for like a couple months on that bit to get it stable
- [2026-10-09] not an easy task to get that type of novelty and have it be self sustaining without constant human overseeing
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 21:45:59 +0100 | | > From: gwern (s_8f9b82ef) | > Sent: Fri, 9 Oct 2026 21:41:32 +0100 | > | > personally, the feeling I get from Computer 10 is closer to a 'Platonic Archetype', of 'meta-fictional document' | | i think this is true in s
- [2026-10-09] which, is necessarily the reason it worked so well
- [2026-10-09] u need to witness mine it really is so sick (and as a bonus it works on computer hence my knowledge of its distribution space)
- [2026-10-09] hosting 70b,,,
- [2026-10-09] i just dont have a way to give a public link for it yet or i wouldve blasted that by now
- [2026-10-09] since my inference is on private infra
- [2026-10-09] echo is really cool i like it
- [2026-10-10] celeste #1, officially
- [2026-10-13] not in the same way really
- [2026-10-13] specifically like; if you replicate the subliminal learning paper, the way it generalizes is in a very odd and specific way related to the assistant character, the way the trait gets absorbed
- [2026-10-13] and that specific effect which leads to a lot of the more nasty emergent misalignment stuff only really tends to happen past a certain amount of repetition over the same data, as well as in the LoRA + adamw regime
- [2026-10-13] before that, it looks more along the lines of what one would anticipate in terms of training
- [2026-10-13] that there is some absorption but it doesn't totalize as strongly or have weird entanglements
- [2026-10-13] i mean yeah it is, because it's an edge case of how fine tuning affects the existing basin when operating underneath it
- [2026-10-13] | Version: 2 | Sent: Tue, 13 Oct 2026 00:15:56 +0100 | | hence why it needs the stock sys prompt too during training | | Version: 1 | Sent: Tue, 13 Oct 2026 00:15:44 +0100 | | hence why it needs the stock sys prompt too
- [2026-10-13] this makes sense yeah, i do wonder though what the split is between the type I saw and otherwise expected results where the student actually mirrors the teacher rather than the trait
- [2026-10-13] | Version: 2 | Sent: Tue, 13 Oct 2026 00:51:39 +0100 | | would have to look it up/reproduce since they don't show trajectories from my skim | | Version: 1 | Sent: Tue, 13 Oct 2026 00:51:34 +0100 | | would have to look it up/reproduce since they don't show trajectories from my smim

### id=s_8f9b82ef · имя: gwern · чаты: Character Underground
- [2026-10-09] yea, but larger models are way more sample-efficient. like anthropic's data poisoning was almost constant in dataset size, iirc?
- [2026-10-09] (I didn't like the chatbot persona they put in talkie anyway. I'd've much rather seen like an actual historical personage or writer powering it)
- [2026-10-09] one hopes! I didn't take the time to play with it because it felt too stupid to do anything I'd find really fun at this point, but if they can get it up to gpt-4 levels...
- [2026-10-09] I think there's no literature. I regularly ask people how they would 'prove they'd created or prompted a base model' and they never have an answer
- [2026-10-09] what if you rendered all the CAs as ascii art? and expanded out into ascii art rendered everything. images, tables, etc. you can do almost anything in unicode, you know: https://gwern.net/utext
- [2026-10-09] one of the grand universal historians seems like the obvious target. spengler, toynbee, etc. well documented, presumably many published personal letters to go beyond the enormous books, and the grand overview and schematizing seem like a good lenses for the sort of things people would use a Talkie P
- [2026-10-09] (ah, but how do you verify either is a base model? aren't they really more like 'midtrained models in denial'?)
- [2026-10-09] I am skeptical that mode-collapse is solely an assistant vector. I'd expect it to be highly but r<<1, which means that you can find highly mode-collapsed models which have lost a large % of variance but still look ~0 on average assistantness, if you follow me. like consider bivarite with r=0.9, you 
- [2026-10-09] both?
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 21:36:26 +0100 | | > From: Luxia (s_fb7b1b2c) | > Sent: Fri, 9 Oct 2026 21:28:27 +0100 | > | > no yeah sorry that was a full chain statement. makes sense though i do think like; hm. so computer 10; true base or no? | | definitely not. th
- [2026-10-09] oh, this used ideonomy? nice. I keep meaning to try to feed the books into LLMs to extract out an entire LLM-readable cookbook
- [2026-10-09] personally, the feeling I get from Computer 10 is closer to a 'Platonic Archetype', of 'meta-fictional document'
- [2026-10-09] https://gwern.net/doc/math/humor/2007-10-12-zachbeane-dposter-dijkstraquickanddirtys.jpg
- [2026-10-09] hm. directly comparing the ppl? or more 'how damaged is a base model after passing through an RL phase?'
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 22:14:17 +0100 | | > From: Uzay Girit (s_8a6dd445) | > Sent: Fri, 9 Oct 2026 22:13:24 +0100 | > | > To get a sense for the relative quality of the pre train | | oh, of the original hidden pretrain 'base' models? because you can't just be
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 22:15:06 +0100 | | oh yeah that seems reasonable. it doesn't matter how badly damaged it is, as long as they all got similarly damaged so you still probably get a reasonably unbiased accurate ranking | | Version: 1 | Sent: Fri, 9 Oct 2026 22:14:49 +0100 | | oh ye
- [2026-10-10] | Version: 2 | Sent: Sat, 10 Oct 2026 01:44:33 +0100 | | I think a taxonomy (of interesting and/or important characters), and also a curriculum of 'canonical' readings on character, would be useful (just suggested by Matt Mandel here at Lighthaven during progress studies conference). we all know a f
- [2026-10-10] that would be useful to know! what *are* the gaps that most of us here take for granted and don't realize are 'folklore'?
- [2026-10-10] | Version: 2 | Sent: Sat, 10 Oct 2026 01:53:40 +0100 | | (also to introduce Matt Mandel a little: he is a VC at Cosmos, which just launched as a small VC fund, and is investing in my startup, GAI. I enjoy debating stuff with him and Brandon; probably the most philosophy heavy VC pitch/discussion I e
- [2026-10-10] that was why I asked someone who knew them to add them because I just wasn't quite sure if 'Celeste' in my account picker was our Celeste. there's at least 3 of them!
- [2026-10-12] https://www.lesswrong.com/posts/YvNkA3ZzsCv9QQmXR/base-models-can-detect-hidden-intentions-that-prompted this is a nice example of using compression loss lens and showing the power of base models (not to mention truesight)
- [2026-10-12] yes, we need to organize a little more... I've found Signal gcs (and Twitter and Discord) to be good for chitchat, but terrible for 'slow' documentation (https://gwern.net/internet-community-design). subreddits still seem fairly optimal for this kinda thing and have a number of advantages over the r
- [2026-10-12] I am skeptical. private subreddits massively kill traffic and participation in every one I've participated in. and they also have nasty downstream sideeffects like not being scraped and fed into future LLMs, even in a trivial retrieval context. / reddit may require more weird verification over time,
- [2026-10-12] Slack is much worse than discord in this context. Expensive, if nothing else
- [2026-10-12] nah, super custom and complex, and the sort of maintenance headache you should only take on after outgrowing a subreddit imo. lw2 can use it successfully but I'm not aware of any truly independent, successful uses

### id=[ТЕЛЕФОН] · имя: Celeste · чаты: Character Underground
- [2026-10-10] Hi everyone???
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

### id=s_011124db · имя: ꒰ა clu ໒꒱ · чаты: Character Underground
- [2026-10-09] narrow finetunes != diluting with other data
- [2026-10-09] you see more conditional misalignment rather than EM
- [2026-10-09] negation neglect seems to be real though
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 20:09:34 +0100 | | ++ larger models have more of a prior | | Version: 1 | Sent: Fri, 9 Oct 2026 20:09:23 +0100 | | ++ larger models have more a prior
- [2026-10-09] hacker opus is a good blog post
- [2026-10-09] add them!!
- [2026-10-09] i'd be very interested in this
- [2026-10-09] i think narrow SFT just sucks for generalisation if your dataset is diluted, doesn't have to be lora
- [2026-10-09] nick's 18th century guy??
- [2026-10-09] ye i just mean for the flashy owain paper results
- [2026-10-09] nick is in here we can give him feedback @Nick Levine :3
- [2026-10-09] emergent misalignment happened bc they only finetuned on insecure code data, the effect becomes localised to flask templates if you dilute with normal transcripts (conditional misalignment)
- [2026-10-09] hmmm how have you been trying it seems tough
- [2026-10-09] bc you've basically yanked the model into a particular shape
- [2026-10-09] i do imagine SFT as narrowing the model whereas RL allows exploration
- [2026-10-09] more exploration on-policy i supposed. i dont hav empirical evidence but seems like on-policy has some magic sauce
- [2026-10-09] SFT you're telling it what it can say
- [2026-10-09] i'd be curious to do celeste's computer 10 regime but on the talkie base
- [2026-10-09] (also nick are u in sf now? no more london??)
- [2026-10-09] NCA??
- [2026-10-09] we got em

### id=s_839ade01 · имя: orchidmantis · чаты: Character Underground
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

### id=s_78e3297b · имя: Mc S · чаты: Character Underground
- [2026-10-09] also in terms of em / papers like em from reward hacking, theres also a large diff between 'persona-y' misalignment and sort of 'reward hacky' misalignment ; it seems like for a while people assumed that because persona-y misalignment generalized then reward hack-y misalignment would as well (hence 
- [2026-10-09] Is anyone opposed to me adding my friend asvin (works at simplex, very interested in character, wrote: (https://arxiv.org/abs/2605.25459)
- [2026-10-09] Random comment, but does anyone know of attempts to do EM or related training with dpo instead of sft, and if there were any differences
- [2026-10-09] no like just normal em
- [2026-10-09] I wonder if you could just do rl with entropy as a reward or something lmfao
- [2026-10-09] theres also a sense in which RL teaches the model retrodiction while sft and pretraining teach the model prediction, which is pretty important
- [2026-10-09] id also be curious to do something computer 10 ish on the NCA pretrained models if those are publicly available
- [2026-10-09] and then maybe add in text later or something
- [2026-10-09] neural cellular automata
- [2026-10-09] (this paper, which is also just rly cool: https://arxiv.org/pdf/2603.10055)
- [2026-10-09] Any reward function is technically a posterior over the sequence which means the model essentially must learn to do inference backwards, which specifically gives you an exponential tilt to the original policy (if you use KL, see: https://arxiv.org/pdf/2205.11275)
- [2026-10-09] (i have a paper about this that should hopefully come out soon if i can lock in on writing)
- [2026-10-09] cool idea
- [2026-10-09] sigh i guess i have a new side project now

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

---

**Claude:**

[
  {
    "id": "s_f05c2f37",
    "about": "Обсуждает характер и персону моделей (Astra, ChatGPT, 4o), был на ивенте. Интересуется, у кого есть собственные решения для персистентности моделей, и собирается чинить харнес.",
    "interests": "персоны моделей, character research, персистентность, эмерджентные персоны, 4o",
    "useful": "знание: исследования character и персистентности",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_fb7b1b2c",
    "about": "Разбирает поведение base- и instruct-моделей, subliminal learning и эмерджентную рассогласованность при дообучении (LoRA + adamw). Сам хостит модель 70b на частной инфраструктуре.",
    "interests": "base-модели, fine-tuning, subliminal learning, emergent misalignment, Computer 10",
    "useful": "знание: техническая глубина по дообучению и поведению моделей",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_8f9b82ef",
    "about": "Обсуждает base-модели, mode collapse, data poisoning и персонажей в LLM. Предлагает таксономию и курс канонических текстов по character. Обсуждает, где вести документацию сообщества (subreddit вместо чатов).",
    "interests": "base-модели, mode collapse, character, документация сообщества, Computer 10",
    "useful": "деньги: упомянул VC-фонд, который инвестирует в его стартап; знание: глубокая экспертиза по LLM",
    "alpha": "В чате есть инвестор (Matt Mandel, VC в новом небольшом фонде Cosmos): познакомиться через общий чат и подготовить короткий питч проектов оператора.",
    "evidence": "he is a VC at Cosmos, which just launched as a small VC fund"
  },
  {
    "id": "[ТЕЛЕФОН]",
    "about": "Рассуждает о характере моделей: Sonnet 3, Opus 3, 4o, Fable 5 и ChatGPT как самоподавляющий персонаж. Назвала Truth Terminal среди проектов, похожих на Computer 10 и Talkie.",
    "interests": "character моделей, ассистент как персонаж, Truth Terminal, синтетические данные, преемственность личностей",
    "useful": "знание: ключевой участник сообщества character research",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_011124db",
    "about": "Обсуждает emergent misalignment, узкий SFT против RL и условную рассогласованность при разбавленных данных. Хочет попробовать режим Computer 10 на базе Talkie.",
    "interests": "emergent misalignment, SFT против RL, обобщение при дообучении, negation neglect, Talkie",
    "useful": "знание: понимание генерализации при дообучении",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_839ade01",
    "about": "Организатор ивентов сообщества (Arthur), создал чат. Делится ссылками на новую инициативу Nathan Lambert (Trillium Labs) и Talkie 2, спрашивает про отслеживание финансирования character research.",
    "interests": "организация ивентов, character research, финансирование исследований, Talkie 2, Trillium Labs",
    "useful": "знание и контакты: организатор ивентов с доступом к спикерам и грантовым контактам",
    "alpha": "Организатор собирает спикеров и темы для следующего ивента по character research: написать ему в личку с темой выступления или разговора.",
    "evidence": "please dm me if there are speakers you would like to see or have ideas for themes"
  },
  {
    "id": "s_78e3297b",
    "about": "Обсуждает EM, reward hacking, RL против SFT и нейронные клеточные автоматы (NCA). Готовит статью, предложил добавить знакомого из Simplex, интересующегося character.",
    "interests": "emergent misalignment, reward hacking, RL против SFT, NCA-модели, DPO",
    "useful": "знание: теоретическая база по RL и обучению моделей",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_8a6dd445",
    "about": "Обучил мультиперсонную модель echo (echo.fulcrum.inc), интересуется условиями возникновения EM и оценкой качества претрейна по пост-тренированным чекпоинтам.",
    "interests": "мультиперсонные модели, emergent misalignment, оценка претрейна, самораспознавание, echo",
    "useful": "инженеры и знание: практик, который сам обучает модели",
    "alpha": null,
    "evidence": null
  }
]
