---
session: s_869c5d89
date: 2026-10-23
words: 1287
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-23 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_869c5d89` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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
- [2026-10-18] @Sauers @Max Loeffler can you share what you two are on about on twitter? owl neuron steering?

### id=s_e2d2fb10 · имя: Antra Tessera · чаты: Antra Tessera, Character Underground
- [2026-10-22] Hi! I am glad you like the approach. We are trying few more things and should publish in the next couple of days
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

### id=s_39d899ae · имя: shubham · чаты: Character Underground, shubham
- [2026-10-10] Hi people!!
- [2026-10-12] this is really cool anna, thanks for putting this together!!  i’ve also been working on https://charactergarden.com/ over the past week, a directory of characters, research, and people working in this space  i would love feedback and / or corrections, edits etc. feel free to send a message or dm  i 
- [2026-10-12] the three layer model quite helped me look thru different abstract layers when i first read it. my bad, let me add that to the list
- [2026-10-23] i’m so glad you loved it!!

### id=s_1963f935 · имя: Drew · чаты: Character Underground, Drew
- [2026-10-18] https://en.wikipedia.org/wiki/A_Perfect_Vacuum
- [2026-10-22] Certainly!
- [2026-10-22] Great to meet and glad you enjoyed it.
- [2026-10-22] I was as pleasantly surprised as you, despite curating the list. Really incredible density of insight and talent.

### id=s_02408487 · имя: Felix Binder · чаты: Character Underground, Felix Binder
- [2026-10-10] Is the vivarium thing still going on?
- [2026-10-22] Hi Tony!

---

**Claude:**

```json
[
  {
    "id": "[ТЕЛЕФОН]",
    "about": "Организатор встреч сообщества Character Underground (character-исследования LLM). Делится ссылками на инициативы (trillium labs, talkie 2), спрашивает про финансирование character-исследований.",
    "interests": "character design в LLM, предобучение и персонажи, финансирование character-исследований, эвалы, нейронный steering",
    "useful": "Знание и интро: организует мероприятия и знает исследователей в теме character/LM psychology. Через него можно выйти на спикеров и контакты.",
    "alpha": "Организатор собирает идеи спикеров и тем для следующего ивента Character Underground: оператору предложить себя или тему в личку и попросить интро к исследователям.",
    "evidence": "please dm me if there are speakers you would like to see"
  },
  {
    "id": "s_e2d2fb10",
    "about": "Исследователь base-моделей: делает неопубликованный бенчмарк basebench про калибровку и «зажаренность» (friedness) базовых и instruct-моделей. Обещает публикацию в ближайшие дни.",
    "interests": "base-модели, friedness, калибровка, geometry probes, varentropy",
    "useful": "Знание: практик по оценке base/instruct-моделей. Возможный контакт для интро в исследовательскую среду.",
    "alpha": "Скоро выйдет публикация и бенчмарк basebench, а автор хочет пообщаться по возвращении в SF: оператору посмотреть бенчмарк и предложить встречу.",
    "evidence": "I would love to chat more about this, I’ll be back in SF in a couple of days"
  },
  {
    "id": "s_39d899ae",
    "about": "Строит charactergarden.com, каталог персонажей, исследований и людей в области character-LLM. Просит фидбэк и правки.",
    "interests": "character-исследования, каталог людей и работ, трёхслойная модель персонажа",
    "useful": "Знание: агрегирует исследователей и работы в теме character, можно найти нужные контакты.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_1963f935",
    "about": "Участник Character Underground, по его словам курировал список участников встречи. Отзывается о плотности талантов и идей на ивенте.",
    "interests": "кураторство сообщества, офлайн-встречи, character-исследования",
    "useful": "Интро: знает состав участников и может представить людей из встречи.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_02408487",
    "about": "Участник Character Underground, интересуется, продолжается ли проект «vivarium». Поздоровался в личке.",
    "interests": "vivarium",
    "useful": "",
    "alpha": null,
    "evidence": null
  }
]
```
