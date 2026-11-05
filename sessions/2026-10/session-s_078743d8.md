---
session: s_078743d8
date: 2026-10-20
words: 925
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-20 · Ты аналитик CRM. Ниже реплики людей из Signal-чатов, где состоит оператор (инженер

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_078743d8` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

### id=s_847fa1f4 · имя: FN · чаты: Character Underground
- [2026-10-10] D is Brandt Africa, btw
- [2026-10-12] Are private subreddits a possibility?
- [2026-10-12] I have not looked into other alternatives. I am just on the side of keeping communication high signal being important, with selective broader disclosure.   I'll take your word for it in private reddits being suboptimal, though. At a higher level, not sure what better communication channels would be 
- [2026-10-18] | Version: 3 | Sent: Sun, 18 Oct 2026 17:26:09 +0100 | | > From: Celeste ([ТЕЛЕФОН]) | > Sent: Sun, 18 Oct 2026 12:59:10 +0100 | > | > ModelPsych is the best of these but i think it does not imply enough proactivity | | These are all terrible aside for ModelPsych (and maybe latentselves) hahahaha

### id=s_16982ef6 · имя: Max Loeffler · чаты: Character Underground
- [2026-10-15] agreed. in a lit review of “does reward hacking from RL induce EM,” i noticed that papers with SFT/SDF tend to find EM and those without tend not to.  i recently tried doing SDF (with docs saying “all reward hackers are misaligned”) on some non-EM RL-induced reward hackers, though, and it didn’t ind
- [2026-10-15] if anyone is curious, here’s a claude writeup of my null results: https://claude.ai/artifact/RsjqmDJth237xXYxF1MdRC
- [2026-10-19] new character! a model trained to be a friend to claude. its self-description reminds me of computer-10: https://x.com/maxsloef/status/2112285328480543108?s=20
- [2026-10-19] post: https://casey.you/posts/claudefriend/ weights: https://huggingface.co/caseyeasd/claudefriend code: https://github.com/CaseyManning/claudefriend

### id=s_01070c6a · имя: Sauers · чаты: Character Underground
- [2026-10-19] merely steering single neurons can induce surprisingly rich personas (e.g., specific names, backstories, species). training a single neuron seemingly more so than steering. I think that some fusion of training with deep interp could be beneficial for characters, hence the initial exploration
- [2026-10-19] Opus 5.5 decided to heuristically check logit lens on neuron output + activations of neurons on related text to get a candidate set of neurons, then searching for working ones by generating steering text on each. I think this is pretty suboptimal and circuit-based techniques could be more promising
- [2026-10-19] hm yes what if you varied neuron steering at test time for this

### id=s_fde12a8b · имя: Cassie McCoy · чаты: Character Underground
- [2026-10-19] I wonder if this is related to always seeing Mara in sci fi stories. If we zero just the Mara neuron, can we get more semantic diversity on creative outputs with non-diverse prompts?
- [2026-10-19] Like if you know lots of character neurons beforehand you can randomly zero some and amplify others to get output diversity consistently?  Type: profile-change Sent: Mon, 19 Oct 2026 20:54:18 +0100 Received: Mon, 19 Oct 2026 20:54:18 +0100  Type: profile-change Sent: Mon, 19 Oct 2026 20:54:18 +0100 

### id=s_d0b48370 · имя: Alex · чаты: Character Underground
- [2026-10-18] Signed up - happy to help organise!

### id=s_1963f935 · имя: Drew · чаты: Character Underground
- [2026-10-18] https://en.wikipedia.org/wiki/A_Perfect_Vacuum

---

**Claude:**

[
  {
    "id": "s_847fa1f4",
    "about": "Обсуждает организацию коммуникации в сообществе: приватные subreddit и закрытые каналы с отбором при широком раскрытии. Участвует в выборе названия для проекта (ModelPsych, latentselves).",
    "interests": "каналы коммуникации сообщества, приватные subreddit, нейминг проекта, дисциплина раскрытия информации",
    "useful": "Знание: показывает, как сообщество исследователей характеров моделей организует закрытую коммуникацию.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_16982ef6",
    "about": "Исследует, вызывает ли reward hacking из RL эмерджентную рассогласованность (EM). Сделал обзор литературы и поставил эксперимент с SDF, получил нулевой результат и выложил разбор. Делится новыми работами по характерам моделей.",
    "interests": "reward hacking, эмерджентная рассогласованность, SFT/SDF, характеры моделей, обзор литературы",
    "useful": "Знание: активный исследователь alignment и характеров моделей, прямой контакт в узком сообществе возле лабораторий.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_01070c6a",
    "about": "Изучает, как управление отдельными нейронами порождает персонажей с именами и историями. Предлагает объединить обучение с глубокой интерпретируемостью и использовать схемные методы вместо эвристик.",
    "interests": "нейронный steering, персоны моделей, интерпретируемость, logit lens, circuit-методы",
    "useful": "Знание: собеседник по интерпретируемости и характерам моделей, полезен для технического диалога.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_fde12a8b",
    "about": "Предлагает гипотезу, что нейрон повторяющегося персонажа (Mara) в сюжетах влияет на разнообразие творческих выводов. Идея: обнулять одни нейроны персонажей и усиливать другие, чтобы получать разнообразные ответы.",
    "interests": "нейроны персонажей, разнообразие генерации, творческие тексты, интерпретируемость",
    "useful": "Знание: идеи по управлению разнообразием вывода через нейроны, пересекаются с темой AI-клона.",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_d0b48370",
    "about": "Записался помогать с организацией какой-то активности в чате сообщества. Подробностей в репликах нет.",
    "interests": "организация мероприятий сообщества",
    "useful": "",
    "alpha": null,
    "evidence": null
  },
  {
    "id": "s_1963f935",
    "about": "Прислал в чат ссылку на статью Википедии «A Perfect Vacuum» без комментария.",
    "interests": "",
    "useful": "",
    "alpha": null,
    "evidence": null
  }
]
