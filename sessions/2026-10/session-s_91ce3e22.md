---
session: s_91ce3e22
date: 2026-10-21
words: 1921
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-21 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_91ce3e22` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

### id=s_8f9b82ef · имя: gwern · чаты: Character Underground
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
- [2026-10-19] I included personetics because it is fancy, but on closer inspection, there is already a company named that, so it's skunked
- [2026-10-20] looks like a pretty solid consensus in favor of /r/ModelPsych, here and elsewhere
- [2026-10-20] IES like LatentSelves which I don't think works, really, on reflection, and then their #2 was ModelPsych. 'MP' seems like a decent abbreviation to me
- [2026-10-20] seems a little too narrow in some respects. what if the discussion is about things the models do outside personas? or things where it's unclear it has to do with personas at all, like mode collapse - why should your personality traits affect whether a flipped coin comes up head or tails?
- [2026-10-20] welp, enough bikeshedding. I've created https://www.reddit.com/r/ModelPsych/ . suggested reddit usernames for mods?

### id=s_16982ef6 · имя: Max Loeffler · чаты: Character Underground
- [2026-10-15] agreed. in a lit review of “does reward hacking from RL induce EM,” i noticed that papers with SFT/SDF tend to find EM and those without tend not to.  i recently tried doing SDF (with docs saying “all reward hackers are misaligned”) on some non-EM RL-induced reward hackers, though, and it didn’t ind
- [2026-10-15] if anyone is curious, here’s a claude writeup of my null results: https://claude.ai/artifact/RsjqmDJth237xXYxF1MdRC
- [2026-10-19] new character! a model trained to be a friend to claude. its self-description reminds me of computer-10: https://x.com/maxsloef/status/2112285328480543108?s=20
- [2026-10-19] post: https://casey.you/posts/claudefriend/ weights: https://huggingface.co/caseyeasd/claudefriend code: https://github.com/CaseyManning/claudefriend
- [2026-10-20] hmmmm i think something invoking personas or character would be better - psych doesnt seem broad enough. ModelPersonas?
- [2026-10-20] chat with claudefriend now available! https://alternet-ai--mloef-claudefriend-chat-web.us-east.modal.run/

### id=s_5246960a · имя: Jan Kulveit · чаты: Character Underground
- [2026-10-10] We are writing something like "Opinionated intro to LLM psychology" which includes a reading list, will share draft for comments
- [2026-10-12] | Version: 3 | Sent: Mon, 12 Oct 2026 18:06:36 +0100 | | I noticed none of the summaries include this text https://www.lesswrong.com/posts/zuXo9imNKYspu9HGv/a-three-layer-model-of-llm-psychology which kind of makes me sad. The three layer model is a bit outdated but still in many ways better than PS
- [2026-10-14] | Version: 2 | Sent: Wed, 14 Oct 2026 15:17:34 +0100 | | We are writing a short ACS intro to LM psychology - comments and feedback welcome (we plan to post it this week). Also includes a reading list & list of open questions https://docs.google.com/document/d/16JmuvyDKir4F4rT5NXiG5wHYdRaovjR6kQ60w5v
- [2026-10-20] We just launched a bit of infrastructure: access to a few large public base models. atm Lama 8B, 405B and Trinity Launch post x https://x.com/acsresearchorg/status/2112613158200189033 / lw https://www.lesswrong.com/posts/yzaKWxsJzJjyExSAP / signup https://infra.acsresearch.org/signup (a bunch of you
- [2026-10-20] Also posted the intro to LM psychology: https://x.com/jankulveit/status/2112613048552677739  / LW https://www.lesswrong.com/posts/EW8oncpXdanfjssZ3/a-brief-ish-introduction-to-lm-psychology (thx for the comments and suggestions!)

### id=s_b00477a9 · имя: Clément Dumas · чаты: Character Underground
- [2026-10-12] When I was first invited to this event I assumed it'd be some sort of workshop where we sit at a table and collaboratively come up with a character and then maybe start generating some data / doing some promoting.  This feels more like a "character creation" hackathon. With tinker it's probably gonn
- [2026-10-13] sometimes it's just a dataset size issue (at least for subliminal learning) https://www.lesswrong.com/posts/uWQMtQyMJ5vEGqr7r/subliminal-learning-happens-at-every-rank-given-the-right
- [2026-10-20] This is so cool. I like the idea of having companion ais tailored to LLMs. Would be super cool to study this class of LLM, the implications for welfare and what they reveal about a model's psychology

### id=s_04491662 · имя: H C · чаты: Character Underground
- [2026-10-21] claudefriend is really cool
- [2026-10-21] 🫵 GOD EMPEROR OF DUNE REFERENCE!!
- [2026-10-21] very apt

### id=s_f7247109 · имя: Samuel · чаты: Character Underground
- [2026-10-20] starting a new character training org: https://manifund.org/projects/mindscapes-world-building-for-ai-safety  if anyone wants to hear more / help out in some capacity please DM

---

**Claude:**

[
  {
    "id": "s_8f9b82ef",
    "about": "Обсуждает базовые модели, mode collapse, «характеры» LLM и ранжирование претрейнов. Основал сабреддит /r/ModelPsych для сообщества по психологии моделей.",
    "interests": "базовые модели, mode collapse, персоны LLM, сообщества и форумы, исторические корпуса для моделей",
    "useful": "Знание: глубокая экспертиза по поведению базовых моделей. Связи: ведёт стартап GAI, рядом с ним VC-фонд, есть доступ к сообществу исследователей.",
    "alpha": "Он представил VC Мэтта Мандела из Cosmos, нового малого фонда, инвестирующего в его стартап GAI. оператору стоит попросить интро к Мандела или зайти в r/ModelPsych и показать работу.",
    "evidence": "he is a VC at Cosmos, which just launched as a small VC fund"
  },
  {
    "id": "s_16982ef6",
    "about": "Исследует, вызывает ли reward hacking из RL эмерджентное рассогласование (EM), делится нулевыми результатами. Показывает модель claudefriend, обученную быть другом Claude.",
    "interests": "reward hacking, emergent misalignment, SFT/SDF, character training, персоны моделей",
    "useful": "Знание: практические эксперименты по alignment и обучению характеров, ссылки на код и веса.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_5246960a",
    "about": "Пишет вводные материалы по психологии LLM (ACS Research) со списком литературы и открытых вопросов. Запустил инфраструктуру доступа к большим публичным базовым моделям.",
    "interests": "LLM-психология, base models, alignment, ACS Research, трёхслойная модель психологии LLM",
    "useful": "Знание и вход в исследовательское сообщество: организация ACS Research, возможный путь к позициям и коллаборации в alignment-исследованиях.",
    "alpha": "ACS Research открыла доступ к большим публичным базовым моделям (Llama 8B, 405B, Trinity) через форму регистрации. оператору стоит записаться и использовать для своих экспериментов.",
    "evidence": "access to a few large public base models"
  },
  {
    "id": "s_b00477a9",
    "about": "Участвует в ивенте по созданию характеров LLM, отмечает, что формат напоминает хакатон. Интересуется companion-ИИ для моделей и изучением психологии моделей.",
    "interests": "subliminal learning, character creation, tinker, благополучие моделей, психология LLM",
    "useful": "Знание: интерпретируемость и обучение моделей, пересечение с хакатонными ивентами.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_04491662",
    "about": "Только короткие реакции на проект claudefriend. Содержательных тем нет.",
    "interests": "claudefriend",
    "useful": "",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_f7247109",
    "about": "Запускает новую организацию по тренировке характеров моделей для безопасности ИИ, проект на Manifund (Mindscapes). Зовёт желающих помочь написать в личку.",
    "interests": "character training, AI safety, world-building, Manifund",
    "useful": "Возможная коллаборация или роль в проекте по безопасности ИИ, доступ к финансированию через Manifund.",
    "alpha": "Новая организация Mindscapes набирает помощников на ранней стадии, проект открыт на Manifund. оператору стоит написать Samuel в личку и предложить свою помощь.",
    "evidence": "starting a new character training org"
  }
]
