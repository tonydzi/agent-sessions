---
session: s_969be20f
date: 2026-10-25
words: 1096
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-25 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_969be20f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
- [2026-10-22] Please elaborate further
- [2026-10-22] "the room left space to disagree"
- [2026-10-22] can you elaborate on this
- [2026-10-22] Interesting ok nice
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

### id=s_0aec91cf · имя: D · чаты: Character Underground, D
- [2026-10-16] In my experience the order matters!
- [2026-10-18] ModelCharacter?
- [2026-10-19] How are you selecting the weights?
- [2026-10-19] I was thinking that there might be theory of deep learning tools to use here such as superweights
- [2026-10-19] Seems related to ye et al 2026 (your language model secretly contains personality subnetworks) which seems related to LTH in some deep way
- [2026-10-24] You might have mistaken me for someone else!

### id=s_01070c6a · имя: Sauers · чаты: Character Underground, Sauers
- [2026-10-19] merely steering single neurons can induce surprisingly rich personas (e.g., specific names, backstories, species). training a single neuron seemingly more so than steering. I think that some fusion of training with deep interp could be beneficial for characters, hence the initial exploration
- [2026-10-19] Opus 5.5 decided to heuristically check logit lens on neuron output + activations of neurons on related text to get a candidate set of neurons, then searching for working ones by generating steering text on each. I think this is pretty suboptimal and circuit-based techniques could be more promising
- [2026-10-19] hm yes what if you varied neuron steering at test time for this
- [2026-10-24] Thanks!
- [2026-10-24] More of that coming

### id=s_f7247109 · имя: Samuel · чаты: Character Underground, Samuel
- [2026-10-20] starting a new character training org: https://manifund.org/projects/mindscapes-world-building-for-ai-safety  if anyone wants to hear more / help out in some capacity please DM
- [2026-10-25] One thing that might be interesting to consider is third person subjectivities: a large proportion of the data a model is trained on consists of text written in the third person, but a 3rd person post training process would still meet your definition of a character
- [2026-10-25] (a third person subjectivity might also instantiate multiple characters described impersonally)
- [2026-10-24] Hey, great to hear - what's your background?

---

**Claude:**

[
  {
    "id": "[ТЕЛЕФОН]",
    "about": "Организатор встреч по теме character design у LLM, ведёт чат Character Underground. Делится обзорами области и просит обратную связь по ивентам.",
    "interests": "character design у LLM, AI-ивенты, финансирование character research, интерпретируемость, сообщество исследователей",
    "useful": "Знание и интро: связан с исследователями character/persona в лабораториях (спикеры Jack Lindsey, Sauers), собирает контакты и финансирование по теме.",
    "alpha": "Ивент Character Design 29.10.2026 в Сан-Франциско со спикерами из лабораторной среды: оператору стоит написать Артуру в DM, попроситься на ивент и предложить тему или помощь.",
    "evidence": "Character Design 29 October 2026, San Francisco"
  },
  {
    "id": "s_0aec91cf",
    "about": "Обсуждает методы отбора весов и идеи из теории глубокого обучения для работы с персонажами моделей. Ссылается на работы про personality subnetworks.",
    "interests": "superweights, personality subnetworks, lottery ticket hypothesis, теория глубокого обучения, character у LLM",
    "useful": "Знание: разбирается в теоретической интерпретируемости, может подсказать литературу и методы.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_01070c6a",
    "about": "Экспериментирует со steering отдельных нейронов, которое порождает богатые персоны. Хочет совместить обучение с deep interpretability для character.",
    "interests": "neuron steering, deep interpretability, logit lens, character training, circuit-based техники",
    "useful": "Знание: практикующий исследователь интерпретируемости, один из спикеров ивента Character Design, потенциальный контакт в лабораторной среде.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_f7247109",
    "about": "Запускает новую организацию по character training для безопасности ИИ (проект на Manifund). Размышляет о третьеличных субъектностях в обучении моделей.",
    "interests": "character training, AI safety, world-building для ИИ, post-training, Manifund",
    "useful": "Работа и деньги: новая организация, которой нужны помощники; есть публичная заявка на финансирование на Manifund.",
    "alpha": "Новая организация по character training (Mindscapes) ищет тех, кто хочет помочь: оператору написать Samuel в DM и предложить инженерную помощь.",
    "evidence": "starting a new character training org"
  }
]
