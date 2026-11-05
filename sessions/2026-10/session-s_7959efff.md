---
session: s_7959efff
date: 2026-10-27
words: 1236
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7959efff` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

### id=s_8f9b82ef · имя: gwern · чаты: Character Underground, gwern
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
- [2026-10-26] How are they doing that? What does universal NPC even mean? Isn't that just... People?
- [2026-10-26] Being character rich sounds interesting. You can't elicit what's not there
- [2026-10-23] Thanks! I will start trying to fill it out when I have time. I've been traveling
- [2026-10-24] "Generative Agents: Interactive Simulacra of Human Behavior", Park et al 2023 https://arxiv.org/abs/2304.03442 ? I'm not maintaining the curriciulm/canon doc but I'll add it ot the subreddit to avoid forgetting. still need to work out a good flair taxonomy/ontology...

### id=s_71698732 · имя: Caithrin · чаты: Character Underground
- [2026-10-09] Referring to this? https://arxiv.org/pdf/2610.10657
- [2026-10-26] China trip character training anecdote- MiHoYo is spending 18 billion USD next 24 months making an «universal NPC » model.  Idea is to create a model that can govern video game character behavior.  Probably the biggest character training project in the world RN.  Talked to the team- only folks in ch
- [2026-10-26] Language barrier makes diving these things difficult but basically they are training a model that can model every possible NPC’s character in a video game universe, each NPC being a different instance of the same model.
- [2026-10-26] Trying to isolate what can steer character in their model and then SFT like 10k-100k different personalities from a model designed to be character rich.

---

**Claude:**

```json
[
  {
    "id": "s_8f9b82ef",
    "about": "Активный участник сообществ про характер и персоны LLM. Обсуждает base-модели, оценку их «повреждения» после RL и канон чтения по character. Завёл сабреддит r/ModelPsych и ведёт его таксономию и курикулум.",
    "interests": "character и persona LLM, base-модели и RL, таксономия и курикулум по character, дизайн онлайн-сообществ, сабреддиты",
    "useful": "знание: сильный источник по character и persona LLM, ведёт канон чтения и новое сообщество r/ModelPsych, полезно для AI-клона. Упоминает VC-фонд Cosmos, инвестирующий в его стартап GAI.",
    "alpha": "Открыт набор модераторов нового сабреддита r/ModelPsych (character и persona LLM): вступить, предложить себя в мод и постить туда работу по AI-клону.",
    "evidence": "suggested reddit usernames for mods?"
  },
  {
    "id": "s_71698732",
    "about": "Занимается character training моделей. Рассказывает, что MiHoYo тратит 18 млрд USD за 24 месяца на «универсальную NPC-модель» и что она говорила с их командой. Описывает подход: выделить, что управляет характером, и сделать SFT на 10k-100k личностей.",
    "interests": "character training, NPC-модели для игр, SFT личностей, управление характером модели",
    "useful": "знание: инсайдерские сведения о крупнейшем проекте character training и методе массового SFT личностей, прямо релевантно AI-клону.",
    "alpha": null,
    "evidence": null
  }
]
```
