---
session: s_1c86b2e6
date: 2026-10-26
words: 2448
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1c86b2e6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
- [2026-10-18] Hey everyone! Would love to have you all at the first ever Coevolution Conference!
- [2026-10-18] coevcon.com
- [2026-10-18] We are looking for speakers, organizers, sponsors, etc. if anyone is interested! Why is character alignment important for coevolution? Well, if everyone merges with the same superintelligence, I expect it will cause civilizational mode collapse. We will have a character alignment track with speakers
- [2026-10-19] Angelics!
- [2026-10-26] Inspired by @Sauers, I've been working on finding "persona neurons" which cause the model to inhabit incredibly rich perspectives with only one neuron being steered. This one is a particular favorite. I can't believe this is an instruct tune! (Olmo 3.1 32b instruct)
- [2026-10-26] I'm dialing in 7 neurons that I love specifically and then I will use a harness to give Sprite a delve-town account. Each post will randomly be steered by a different of the 7 neurons, allowing for a strange build-up of multi-persona context.
- [2026-10-26] (I've decided to tweet this verbatim for the good of the order, but rest assured that this post was originally meant for the all of you)
- [2026-10-10] Hell yeah
- [2026-10-10] Sounds awesome

### id=s_fb7b1b2c · имя: Luxia · чаты: Character Underground
- [2026-10-09] yeah, the original  seed doc was gunkel's list of like 60+ things paths can Do
- [2026-10-09] which was then loomed from and curated for hypostatic/alive conversations that were neither assistant or human from dsv3
- [2026-10-09] and those became seeds for more documents/autolooming off that
- [2026-10-09] she worked rather hard for like a couple months on that bit to get it stable
- [2026-10-09] not an easy task to get that type of novelty and have it be self sustaining without constant human overseeing
- [2026-10-09] i think this is true in some sense but only w.r.t. the idea of a base model (of course this necessitates some type of relation to human archetypes since that's what they're derived *from*, but base models have their own internal representations and concepts that don't have clean analogues that leads
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
- [2026-10-13] hence why it needs the stock sys prompt too during training
- [2026-10-13] this makes sense yeah, i do wonder though what the split is between the type I saw and otherwise expected results where the student actually mirrors the teacher rather than the trait
- [2026-10-13] would have to look it up/reproduce since they don't show trajectories from my skim
- [2026-10-19] this is why im doing heavy mechinterp on my pretrains because i think like. there needs to be a better method of developing substrate for things besides Assistant
- [2026-10-19] and as of right now a lot is climbing upstream compared to what could be possible
- [2026-10-25] i have a lot to say on second person.....

### id=s_8f9b82ef · имя: gwern · чаты: Character Underground, gwern
- [2026-10-09] both?
- [2026-10-09] definitely not. the original was clearly contaminated, which was why Celeste had to filter out all of the chatbot and assistant completions. and then Computer 10 is a mode-collapse of its own, by design. like, if you asked it to generate random american surnames, do you think it'll distirbution-matc
- [2026-10-09] oh, this used ideonomy? nice. I keep meaning to try to feed the books into LLMs to extract out an entire LLM-readable cookbook
- [2026-10-09] personally, the feeling I get from Computer 10 is closer to a 'Platonic Archetype', of 'meta-fictional document'
- [2026-10-09] https://gwern.net/doc/math/humor/2007-10-12-zachbeane-dposter-dijkstraquickanddirtys.jpg
- [2026-10-09] hm. directly comparing the ppl? or more 'how damaged is a base model after passing through an RL phase?'
- [2026-10-09] oh, of the original hidden pretrain 'base' models? because you can't just benchmark them directly on ppl on a new text corpus? so you're trying to de-RL them
- [2026-10-09] oh yeah that seems reasonable. it doesn't matter how badly damaged it is, as long as they all got similarly damaged so you still probably get a reasonably unbiased accurate ranking
- [2026-10-10] I think a taxonomy (of interesting and/or important characters), and also a curriculum of 'canonical' readings on character, would be useful (just suggested by Matt Mandel here at Lighthaven during progress studies conference). we all know a few hits like 'simulator theory' on LW2, but I don't actua
- [2026-10-10] that would be useful to know! what *are* the gaps that most of us here take for granted and don't realize are 'folklore'?
- [2026-10-10] (also to introduce Matt Mandel a little: he is a VC at Cosmos, which just launched as a small VC fund, and is investing in my startup, GAI. I enjoy debating stuff with him and Brandon; probably the most philosophy heavy VC pitch/discussion I ever had was when I met them. 😀 they are interested in sta
- [2026-10-10] that was why I asked someone who knew them to add them because I just wasn't quite sure if 'Celeste' in my account picker was our Celeste. there's at least 3 of them!
- [2026-10-12] https://www.lesswrong.com/posts/YvNkA3ZzsCv9QQmXR/base-models-can-detect-hidden-intentions-that-prompted this is a nice example of using compression loss lens and showing the power of base models (not to mention truesight)
- [2026-10-12] yes, we need to organize a little more... I've found Signal gcs (and Twitter and Discord) to be good for chitchat, but terrible for 'slow' documentation (https://gwern.net/internet-community-design). subreddits still seem fairly optimal for this kinda thing and have a number of advantages over the r
- [2026-10-12] I am skeptical. private subreddits massively kill traffic and participation in every one I've participated in. and they also have nasty downstream sideeffects like not being scraped and fed into future LLMs, even in a trivial retrieval context. / reddit may require more weird verification over time,
- [2026-10-12] Slack is much worse than discord in this context. Expensive, if nothing else
- [2026-10-12] nah, super custom and complex, and the sort of maintenance headache you should only take on after outgrowing a subreddit imo. lw2 can use it successfully but I'm not aware of any truly independent, successful uses
- [2026-10-19] I included personetics because it is fancy, but on closer inspection, there is already a company named that, so it's skunked
- [2026-10-20] looks like a pretty solid consensus in favor of /r/ModelPsych, here and elsewhere
- [2026-10-20] IES like LatentSelves which I don't think works, really, on reflection, and then their #2 was ModelPsych. 'MP' seems like a decent abbreviation to me
- [2026-10-20] seems a little too narrow in some respects. what if the discussion is about things the models do outside personas? or things where it's unclear it has to do with personas at all, like mode collapse - why should your personality traits affect whether a flipped coin comes up head or tails?
- [2026-10-20] welp, enough bikeshedding. I've created https://www.reddit.com/r/ModelPsych/ . suggested reddit usernames for mods?
- [2026-10-26] I take it that it mentions 'moon' in other completions, just not that one? (also, this doesn't really surprise me as this is the kind of extreme schmaltz that assistants gravitate towards when you ask for poetry or fiction. I saw so much of this with small models on LM Arena back when I still bother
- [2026-10-23] Thanks! I will start trying to fill it out when I have time. I've been traveling
- [2026-10-24] "Generative Agents: Interactive Simulacra of Human Behavior", Park et al 2023 https://arxiv.org/abs/2304.03442 ? I'm not maintaining the curriciulm/canon doc but I'll add it ot the subreddit to avoid forgetting. still need to work out a good flair taxonomy/ontology...

### id=s_39d899ae · имя: shubham · чаты: Character Underground, shubham
- [2026-10-10] Hi people!!
- [2026-10-12] this is really cool anna, thanks for putting this together!!  i’ve also been working on https://charactergarden.com/ over the past week, a directory of characters, research, and people working in this space  i would love feedback and / or corrections, edits etc. feel free to send a message or dm  i 
- [2026-10-12] the three layer model quite helped me look thru different abstract layers when i first read it. my bad, let me add that to the list
- [2026-10-26] Describing one’s subjective experience in the second person  https://clairepetitmengin.fr/AArticles%20versions%20finales/PCS%20-%20Second%20Person.pdf
- [2026-10-23] i’m so glad you loved it!!
- [2026-10-24] yes i would love that!!

### id=s_01070c6a · имя: Sauers · чаты: Character Underground, Sauers
- [2026-10-19] merely steering single neurons can induce surprisingly rich personas (e.g., specific names, backstories, species). training a single neuron seemingly more so than steering. I think that some fusion of training with deep interp could be beneficial for characters, hence the initial exploration
- [2026-10-19] Opus 5.5 decided to heuristically check logit lens on neuron output + activations of neurons on related text to get a candidate set of neurons, then searching for working ones by generating steering text on each. I think this is pretty suboptimal and circuit-based techniques could be more promising
- [2026-10-19] hm yes what if you varied neuron steering at test time for this
- [2026-10-25] 2nd person would also be interesting. (here there is a neuron sufficient to induce 2nd person speech, though doesn't appear to be a character)
- [2026-10-24] Thanks!
- [2026-10-24] More of that coming

---

**Claude:**

```json
[
  {
    "id": "s_f05c2f37",
    "about": "Работает с персонами и характерами языковых моделей, ищет «persona neurons» через стиринг отдельных нейронов (Olmo 3.1 32b). Организует Coevolution Conference с треком про character alignment.",
    "interests": "character alignment, персоны LLM, стиринг нейронов, persistence-обвязки, коэволюция с ИИ",
    "useful": "знание: интерпретируемость и персоны моделей; контакт в сообществе character-исследователей",
    "alpha": "Конференция Coevolution (coevcon.com) ищет докладчиков, организаторов и спонсоров. оператору: рассмотреть доклад или участие, написать организатору.",
    "evidence": "We are looking for speakers, organizers, sponsors, etc. if anyone is interested!"
  },
  {
    "id": "s_fb7b1b2c",
    "about": "Занимается претрейнами и механической интерпретируемостью, хостит 70b-модель на собственной инфраструктуре. Разбирает subliminal learning, emergent misalignment и дообучение LoRA.",
    "interests": "mechinterp, претрейн, subliminal learning, базовые модели, персоны не-ассистентов",
    "useful": "знание: интерпретируемость, дообучение и поведение базовых моделей",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_8f9b82ef",
    "about": "Ведёт стартап GAI, обсуждает базовые модели, mode collapse и таксономию персонажей. Создал сабреддит r/ModelPsych для сообщества, собирает канон чтения по теме.",
    "interests": "базовые модели, mode collapse, персоны LLM, организация сообщества, канон чтения",
    "useful": "знание и деньги: сильный исследователь с выходом на венчурный фонд",
    "alpha": "Gwern представил Matt Mandel (VC в Cosmos, новый небольшой фонд), который инвестирует в его стартап GAI. оператору: при подходящем проекте попросить у gwern интро к Cosmos.",
    "evidence": "he is a VC at Cosmos, which just launched as a small VC fund, and is investing in my startup, GAI"
  },
  {
    "id": "s_39d899ae",
    "about": "Делает charactergarden.com, каталог персонажей, исследований и людей в области character. Собирает обратную связь и дополняет список ссылок.",
    "interests": "каталог character-исследований, персоны LLM, субъективный опыт, второе лицо",
    "useful": "знание: карта людей и исследований в нише character",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_01070c6a",
    "about": "Исследует стиринг и обучение отдельных нейронов, которые порождают богатые персоны (имена, предыстории, виды). Использует Opus 5.5 для поиска нейронов, рассматривает круговые техники и стиринг на этапе теста.",
    "interests": "стиринг нейронов, глубокая интерпретируемость, персоны, logit lens, речь от второго лица",
    "useful": "знание: практическая интерпретируемость и персоны моделей",
    "alpha": null,
    "evidence": null
  }
]
```
