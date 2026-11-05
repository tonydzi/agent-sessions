---
session: s_cbf909cb
date: 2026-10-28
words: 1019
turns: 1
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-28 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_cbf909cb` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

### id=[ТЕЛЕФОН] · имя: Arb / Arthur · чаты: Arb / Arthur, Character Underground
- [2026-10-27] Yeah we were working on a character definition which is the behavioral aggregate of model plus harness
- [2026-10-27] but idk if people are ready for that atm
- [2026-10-27] And eval suite which includes harness solutions
- [2026-10-09] Hi hi everyone thanks for coming this is Arthur (arb) feel free to dm me with ideas for future events or if you want to chat. Happy you all made it out. Thanks @Jan Kulveit for setting up group
- [2026-10-09] https://aetherawi.red/computer?key=aperture
- [2026-10-09] hi @Brandt Oks
- [2026-10-09] https://docs.google.com/document/d/1vZciW5PFMB-Q7M2RfB8Wj747k78eUPk3i7eNtaczVGA/edit?tab=t.0#heading=h.jaskeqdwoap0
- [2026-10-09] New initiative by Nathan Lambert under new org trillium labs, very topical.
- [2026-10-09] yes!
- [2026-10-09] if you loved talkie, you will love talkie 2
- [2026-10-09] @Nick Levine said gpt-3 level if I remember correctly
- [2026-10-09] oh very curious about this
- [2026-10-09] Very curious about the character experiments you mentioned on talkie for understanding how much character design is limited by pre-training precedent.
- [2026-10-09] oh no i fear this will be me
- [2026-10-09] Who told me yesterday they put zero in a data box and are selling the data
- [2026-10-10] Hi Celeste
- [2026-10-10] @Celeste = celeste Added wrong celeste earlier (who was informed and found it funny)
- [2026-10-10] Is someone tracking funding for character research and relevant contacts? Coefficient givings inclusion of character evals in tailwind is example of this.
- [2026-10-13] For the next event please dm me if there are speakers you would like to see or have ideas for themes for talks / conversations. I would also appreciate feedback on what worked and more importantly, what didnt.
- [2026-10-14] Great initiative thanks for sharing
- [2026-10-18] @Sauers @Max Loeffler can you share what you two are on about on twitter? owl neuron steering?
- [2026-10-23] https://character-design.movingcastles.world/
- [2026-10-23] Character Design 29 October 2026, San Francisco  With Jack Lindsey and Sauers
- [2026-10-24] https://docs.google.com/document/d/1rSjj9hK1oMJGQXbhMV-8l_YIX_Usq0g0MQCldNIXsTM/edit?tab=t.0#heading=h.q69yw27c59o  Wrote a short overview of the field, following up on the event and conversations I’ve had over the last weeks. Appreciate your comments.
- [2026-10-27] Nice initiative @josh https://qwen-neurons-site.vercel.app/

### id=s_0aec91cf · имя: D · чаты: Character Underground, D
- [2026-10-16] In my experience the order matters!
- [2026-10-18] ModelCharacter?
- [2026-10-19] How are you selecting the weights?
- [2026-10-19] I was thinking that there might be theory of deep learning tools to use here such as superweights
- [2026-10-19] Seems related to ye et al 2026 (your language model secretly contains personality subnetworks) which seems related to LTH in some deep way
- [2026-10-26] Random q: does it seem worth it to do a survey paper to synthesize and distill the various recipes people have settled on
- [2026-10-24] You might have mistaken me for someone else!

### id=s_b00477a9 · имя: Clément Dumas · чаты: Character Underground
- [2026-10-12] When I was first invited to this event I assumed it'd be some sort of workshop where we sit at a table and collaboratively come up with a character and then maybe start generating some data / doing some promoting.  This feels more like a "character creation" hackathon. With tinker it's probably gonn
- [2026-10-13] sometimes it's just a dataset size issue (at least for subliminal learning) https://www.lesswrong.com/posts/uWQMtQyMJ5vEGqr7r/subliminal-learning-happens-at-every-rank-given-the-right
- [2026-10-20] This is so cool. I like the idea of having companion ais tailored to LLMs. Would be super cool to study this class of LLM, the implications for welfare and what they reveal about a model's psychology
- [2026-10-27] https://www.lesswrong.com/posts/LBKjnyKDEwEJ45Wjf/self-reward-can-elicit-diverse-model-personas
- [2026-10-27] lots of different attractor when you let this mini qwen 2B RL itself

### id=s_1963f935 · имя: Drew · чаты: Character Underground, Drew
- [2026-10-18] https://en.wikipedia.org/wiki/A_Perfect_Vacuum
- [2026-10-26] I would appreciate it.
- [2026-10-22] Certainly!
- [2026-10-22] Great to meet and glad you enjoyed it.
- [2026-10-22] I was as pleasantly surprised as you, despite curating the list. Really incredible density of insight and talent.

### id=s_f7247109 · имя: Samuel · чаты: Character Underground, Samuel
- [2026-10-20] starting a new character training org: https://manifund.org/projects/mindscapes-world-building-for-ai-safety  if anyone wants to hear more / help out in some capacity please DM
- [2026-10-25] One thing that might be interesting to consider is third person subjectivities: a large proportion of the data a model is trained on consists of text written in the third person, but a 3rd person post training process would still meet your definition of a character
- [2026-10-25] (a third person subjectivity might also instantiate multiple characters described impersonally)
- [2026-10-24] Hey, great to hear - what's your background?
- [2026-10-27] Would you be up to chat sometime next week? https://calendar.app.google/y6nwNEuPVgoyTJ619

### id=s_04491662 · имя: H/C T · чаты: Character Underground
- [2026-10-21] claudefriend is really cool
- [2026-10-21] 🫵 GOD EMPEROR OF DUNE REFERENCE!!
- [2026-10-21] very apt

### id=s_92d0242c · имя: josh · чаты: Character Underground
- [2026-10-27] also inspired by @Sauers, i put together a sweep of every qwen-8B neuron and had an llm categorize and sort them by weirdness:  https://qwen-neurons-site.vercel.app/  searching and looking at 2 neuron combos is fun  i think i can make the categorization more robust, lmk if anyone has any ideas
