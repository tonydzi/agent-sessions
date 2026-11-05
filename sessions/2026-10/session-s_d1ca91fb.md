---
session: s_d1ca91fb
date: 2026-10-14
words: 1626
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-14 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d1ca91fb` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

### id=s_9dda09fd · имя: Asterism · чаты: Character Underground
- [2026-10-09] i also wonder if looking at heterogeneity of capability on various pretraining datasets can get you a signature for real bases. you might expect pretraining on large datasets of a certain type to usually be incapable of yielding spiky enough biases
- [2026-10-09] doesn't this vary a lot between bases?
- [2026-10-10] Hi Celeste
- [2026-10-10] i was wondering if celeste 3 was meant to be here haha
- [2026-10-10] i'm glad she enjoyed tho!
- [2026-10-12] i don't trust reddit not to require more and more weird verification methods over time
- [2026-10-12] seconding on the not-entering-llms point
- [2026-10-12] it's getting easier and easier

### id=s_6a90b81d · имя: Yatharth · чаты: Character Underground
- [2026-10-09] in theory... sft and rl have the exact same formula for updating the logprobs... modulo a coefficient   iterative 1-step sft on same transcripts it would have generated via rl should maybe give mostly same thing
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 20:37:10 +0100 | | which is confusing bc when ppl think of sft vs rl, the most salient things in textbooks might be a formula or settings, but the important part is more how did you collect transcripts, on policy or not, and did you correct for being off policy w
- [2026-10-09] but yeah, when you do on policy things, you can just do micro refinements and adjustments to your current best policy as is  whereas when you sft on badly off policy data, you need to shift your entire distribution to a new strategy, or cover a set of strategies, instead of micro refining your best 
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 20:38:18 +0100 | | > From: Mc S (s_78e3297b) | > Sent: Fri, 9 Oct 2026 20:34:19 +0100 | > | > theres also a sense in which RL teaches the model retrodiction while sft and pretraining teach the model prediction, which is pretty important 
- [2026-10-10] Hi everyone
- [2026-10-10] yes

### id=s_e2d2fb10 · имя: Antra Tessera · чаты: Character Underground
- [2026-10-09] checkpoints or rescued?
- [2026-10-09] Definitely
- [2026-10-09] I can check my diegetic metrics, but really any geometry probes will classify between assistant and base. they won’t detect non-assistant tunes but better than nothing
- [2026-10-09] You can also check pure varentropy
- [2026-10-09] | Version: 2 | Sent: Fri, 9 Oct 2026 21:19:41 +0100 | | it does, still i think think there are tells | | Version: 1 | Sent: Fri, 9 Oct 2026 21:19:37 +0100 | | it does, but i think think there are tells

### id=s_6effcff9 · имя: Nick Levine · чаты: Character Underground
- [2026-10-09] We intentionally did a very light-weight post-train (it's less of a chatbot persona than a "historical reference book template" - certainly doesn't have a coherent identity or set of facts about itself). We've experimented with training in specific historical personas (was playing around with aleist
- [2026-10-09] yep moved here in july!
- [2026-10-09] Love it. One thing we've struggled with, which is kind of amusing (but maybe unsurprising) is if you try to take a shortcut and get claude to generate synth data for a given historical persona (rather than using primary sources and backtranslating instructions), and then finetune talkie on it, talki

### id=[ТЕЛЕФОН] · имя: Anna Mikeda · чаты: Character Underground
- [2026-10-09] I will look into this over the weekend (send me dm if you guys have some private repos/docs you want included in the overview)
- [2026-10-11] I will include this in the index of personas and papers that I am compiling now Should be ready tomorrow
- [2026-10-11] hey all i created an index of personas @vie ⟢ @Will DePue @gwern  bibliography and funding opportunities @orchidmantis   https://docs.google.com/spreadsheets/d/1UNr6ycdoZK_WHRQvSg66F1qWmBiEDD4B2-5SI98i3To/edit?usp=sharing  please have a look whether there are any mistakes/something important is miss

### id=s_39d899ae · имя: shubham · чаты: Character Underground
- [2026-10-10] Hi people!!
- [2026-10-12] this is really cool anna, thanks for putting this together!!  i’ve also been working on https://charactergarden.com/ over the past week, a directory of characters, research, and people working in this space  i would love feedback and / or corrections, edits etc. feel free to send a message or dm  i 
- [2026-10-12] the three layer model quite helped me look thru different abstract layers when i first read it. my bad, let me add that to the list

### id=s_847fa1f4 · имя: Franklin · чаты: Character Underground
- [2026-10-10] D is Brandt Africa, btw
- [2026-10-12] Are private subreddits a possibility?
- [2026-10-12] I have not looked into other alternatives. I am just on the side of keeping communication high signal being important, with selective broader disclosure.   I'll take your word for it in private reddits being suboptimal, though. At a higher level, not sure what better communication channels would be

---

**Claude:**

```json
[
  {
    "id": "s_d19d14fe",
    "about": "Исследует, можно ли вернуть базовую модель из RL/SFT-дообученных открытых моделей, и ведёт такие эксперименты уже несколько недель. Считает, что RL-модели почти полностью восстановимы, а SFT портит сильнее.",
    "interests": "восстановление base-моделей, RL vs SFT, LoRA, литература про character-модели",
    "useful": "Знание: практический опыт с обращением post-training. Можно обсуждать как с технарём из лабораторного круга.",
    "alpha": "Предлагает дамп небольших базовых моделей (восстанавливают ~75% test loss) — запросить у него дамп для своих экспериментов.",
    "evidence": "if anyone wants a dump of a ton of base models i got em too"
  },
  {
    "id": "s_9dda09fd",
    "about": "Размышляет о том, как по неоднородности способностей на разных претрейн-датасетах отличать настоящие базовые модели. Обсуждает правила и верификацию в сообществе.",
    "interests": "сигнатуры base-моделей, претрейн-датасеты, модерация сообщества",
    "useful": "Знание: идеи по детекции базовых моделей.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_6a90b81d",
    "about": "Объясняет связь SFT и RL: формулы обновления logprobs почти совпадают, важнее, on-policy данные или нет. Разбирает, чем микро-уточнение политики отличается от сдвига всего распределения.",
    "interests": "SFT vs RL, on-policy данные, обновление logprobs, обучение политики",
    "useful": "Знание: чёткое понимание post-training, полезно для разговоров с инженерами лабораторий.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_e2d2fb10",
    "about": "Работает с зондами геометрии и метриками для отличения assistant-моделей от базовых, упоминает varentropy. Уточняет, чекпоинты это или восстановленные модели.",
    "interests": "геометрические пробы, varentropy, детекция assistant vs base, интерпретируемость",
    "useful": "Знание: методы детекции тюнов и базовых моделей.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_6effcff9",
    "about": "Работает над моделью talkie с лёгким пост-тренингом в стиле «исторического справочника». Пробовал историчные персоны и заметил проблему при дообучении на синтетических данных, сгенерированных Claude.",
    "interests": "исторические персоны, пост-тренинг, синтетические данные, дообучение talkie",
    "useful": "Знание: практический опыт с историческими персонами и пост-тренингом. Возможный контакт в проекте talkie.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "[ТЕЛЕФОН]",
    "about": "Собирает индекс персон, статей и библиографии для сообщества character-исследований и выложила таблицу на проверку. Предлагает включить в обзор чужие приватные репозитории и документы.",
    "interests": "индекс персон, библиография, финансирование исследований, обзор литературы",
    "useful": "Знание и деньги: сводная таблица по персонам, статьям и возможностям финансирования. Узел сообщества.",
    "alpha": "Составила таблицу с индексом персон, библиографией и возможностями финансирования — открыть ссылку, проверить на ошибки, добавить свои проекты и посмотреть гранты.",
    "evidence": "bibliography and funding opportunities"
  },
  {
    "id": "s_39d899ae",
    "about": "Строит charactergarden.com, каталог персонажей, исследований и людей в этой области, и просит обратную связь. Читал модель трёх слоёв и добавляет её в список.",
    "interests": "каталог персонажей, исследования character-моделей, модель трёх слоёв",
    "useful": "Знание: каталог людей и работ в нише, возможный источник контактов.",
    "alpha": "Ведёт публичный каталог людей и исследований в сфере character-моделей — просмотреть его для поиска контактов и предложить добавить свой проект.",
    "evidence": "a directory of characters, research, and people working in this space"
  },
  {
    "id": "s_847fa1f4",
    "about": "Участвует в обсуждении каналов связи сообщества, выступает за высокий сигнал в общении и избирательное раскрытие. Спрашивает про приватные сабреддиты.",
    "interests": "каналы связи сообщества, модерация, приватность общения",
    "useful": "",
    "alpha": null,
    "evidence": null
  }
]
```
