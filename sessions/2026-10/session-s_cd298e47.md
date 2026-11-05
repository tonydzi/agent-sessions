---
session: s_cd298e47
date: 2026-10-01
words: 2060
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_cd298e47` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are a strict SIGNAL filter for a senior AI engineer building real
systems (Claude Code, agents, RAG, LLM apps). You are given the TITLE, CHANNEL and
a SAMPLE of a video transcript. Decide if it carries PRACTICALLY-USEFUL, durable
knowledge a practitioner could ACT on — as opposed to an advertisement, a hype/news
rehash, or content-free chatter.

Return ONE JSON object, NOTHING else. Schema (all scores 0.0-1.0).
IMPORTANT: write "why", and every "claim" and "actionable", in RUSSIAN (the reader
is a Russian-speaking engineer). Keep "topic" as a short english slug. Keep the
"type" values as the english enum below.
{
  "is_ad": bool,                // the item is primarily promotional/sponsored
  "is_news_rehash": bool,       // just "X released Y" hype with no transferable how-to
  "topic": "short-slug",        // e.g. agentic-coding, rag, evals, prompting, infra
  "signal": float,              // density of useful practitioner knowledge
  "novelty": float,             // non-obvious to a senior AI eng in 2026 (self-assessed)
  "actionability": float,       // can the engineer DO something concrete with it
  "evidence": float,            // grounded in demo/benchmark/real experience vs hot takes
  "durability": float,          // how long it stays true
  "volatility": "volatile|medium|stable",
  "half_life_days": int,        // ~60 volatile, ~365 medium, ~1825 stable
  "why": "одно предложение ПО-РУССКИ",
  "knowledge_units": [          // 0-5 atomic, transferable claims; [] if none
    {"claim": "ПО-РУССКИ", "type": "workflow|tactic|tool-caveat|principle|benchmark", "actionable": "ПО-РУССКИ"}
  ]
}

TITLE: The Death of the Code Review: What the Data Actually Says — Laurie Voss, Arize AI
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hello everybody. Thank you for following on a session about the death of the code review with a session about the death of the code review. Uh who knows howululing decisions get made, but uh Swix decided it would be funny for those two to be backtoback. Uh, hi. Uh, I'm Lori. I'm head of developer relations at Arise AI. Uh, some of you may remember me from when I used to co-found npm, Inc. These days, I think about AI and how to test it. Uh, I'm here to talk about a problem that everyone is seeing right now. The rise of AI agents has dramatically increased how fast developers can produce code. Uh, but the speed at which humans can review code. Uh, yeah, I am having a talk right now. Thank you, notion. very good reminder. Uh the team the speed at which humans can review code has stayed exactly the same. Um and that is creating a new bottleneck that everybody is feeling. Engineering teams across the industry are feeling it. Uh so what can we do about it? Some options are uh we could skip human review entirely. Uh some folks are trying that. Can we automate reviews reliably? Some folks are trying that too. Uh what we're doing going to do today, what I'm going to do for you is I'm going to look at what the industry is really doing right now uh and try to figure out what you can do uh today when you leave the room. So let's start with two numbers. Uh recently three economists tracked more than 100,000 GitHub developers uh matched them against telemetry that showed exactly when each one started using AI. Uh the developers who turned on autonomous agents wrote 741% more code but only 30% more software shipped. Uh that is the scale of the problem right there. They were writing code nearly eight times faster. Uh but their actual ship software only rose by a third. Uh and the authors of the study are blunt that review was the bottleneck. Um the problem is that the route to production still runs through humans. uh and the human steps uh in particular code review uh choke everything downstream. Um producing code is suddenly a whole lot cheaper. Knowing whether to trust it is still very expensive, especially if you have uh sensitive code with a blast radius. Um how can we bring that second number down and thus bring this the amount of software that we ship back into line with the amount that we can code? Uh let's zoom out first. Let's be clear that the problem is real. generation is no longer the bottleneck. Uh Stripe in Anthropics launch materials for Fable this year reported migrating a 50 million line Ruby codebase in a single day. Uh which is work that they'd estimated would take over two months for a team. Um Bun, which is now part of reported that they migrated over a million lines of Zigg uh to Rust in six days. Uh and of course all of us in this room are feeling this on a smaller scale. uh our agents are generating whole apps and we're just sort of hitting the merge button and feeling guilty about the fact that we haven't read these code diffs and we're just sort of hoping that it works. Uh we can't possibly keep on going like that. Um so the obvious answer and the answer some people are trying is you just review more. You take people whose job was previously to review code as well as write code and just say review code all the time. This is your job now. Uh and that doesn't work. uh partly because that's really boring and those people burn out really fast. Um but also the numbers say that we can't um the best study we have on this was done uh two decades ago at Cisco um over 10 months they took 2 and a half thousand reviews they took 3.2 2 million lines of code. Uh, and the study says that reviewers stop finding defects effectively if they try to read more than 400 lines of code in one sitting and their effectiveness completely falls off a cliff. Uh, if they try to review more than 450 lines of code in an hour. Uh, if you do the math on that mean that means that a 10,000line agent pull request at that pace would take three or four working days to get a real human review. that is one pull request from one agent. 10,000 lines is uh absolutely you know absolutely an expectable number of of lines of code uh for an agent that is doing a lot of work for you. Uh and a developer can now run a dozen agents at once. Um although I'm tend to be suspicious of the people who do um so we can't just review harder and we're all feeling that too. The people who are trying to review harder are burning themselves out. So what is the alternative? Uh some people have decided to just stop reading the code entirely. Uh Peter Steinberger who is the creator of OpenClaw uh says that you shouldn't be prompting coding coding agents anymore. You should be designing the loops that prompt your agents. Uh Andre Teague who is one of OpenAI's founding engineers has made the same argument about taking yourself out of the loop. Uh because the human in the loop is holding the system back. Uh but this goes beyond bold claims on Twitter. Uh in February this year, OpenAI published an account of building an internal product uh with in their words no manually written code. They started with a completely empty repository uh and agents wrote everything. Five months later they had about a million lines of code about 1500 merged pull requests uh pull requests uh and they had done used three engineers to do this. Uh even the scaffolding of the agent to review the agent and stuff like that was also written by agents. What they said was humans may review pull requests but they are not required to. Uh we've pushed almost all review effort towards being handled agent to agent. I think the interesting thing about the OpenAI experiment is that they did not tell us what the product did and they did not review an open they did not release an open source product saying and this is how we did it and this is how you should do it which suggests to me that there are still holes in that strategy. Um but it is one possibility. If open AAI says that you
...[middle elided]...
ajectory does what the system actually did step by step uh when it ran against the real world. Uh I'm not going to give a pitch for a rise here. there are enough pitches for a rise at this conference. Uh but if you're shipping automatically reviewed code, then systems in production that review what it actually does in the wild become indispensable. Um so after all that evidence, after all of that review of what the world is doing about automated code reviews, where I land is that code review isn't completely dead, but it is changing an enormous amount. Uh it is being rebuilt as an engineered system. Humans are moving from being the engine that drives a code review uh reading code line by line uh to its pilots. Uh and given the numbers that we opened with that is probably the right trade. Every layer of that system, the benchmark, the classifier, the rubric, the test suite, the eval is itself unreed until somebody decides that that is their job. Um and the teams that win the next few years won't be the ones that generate the most code. They'll be the ones who can say with evidence why they trust what they shipped. Uh and I open by promising you that I would give you with something practical that you could walk away with something that you can do today. Uh and that is to stop reviewing PRs. Um it is the wrong level of abstraction for 2026. Your human judgment is extremely valuable, but it can be made to scale much further than it is scaling right now. Uh pour your precious time into building uh a reliable review harness. codify your definitions of good, your company context, your domain knowledge, and then uh crank up the agents to work with that. You can go much faster than one-third faster uh if you concentrate your efforts higher up the stack of reviewers, rules, and evals. Uh I hope this look at what the industry is doing today has helped you what to helped you decide what you should do and what to expect next. Uh and thank you so much for your time and attention.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-code-review-bottleneck",
  "signal": 0.75,
  "novelty": 0.6,
  "actionability": 0.7,
  "evidence": 0.75,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад даёт конкретные цифры и кейсы (исследование 100k разработчиков, данные Cisco, опыт OpenAI) и выводит из них практичный тезис — перестать ревьюить PR построчно и строить вместо этого harness из evals/рубрик/тестов, что применимо уже сейчас в агентных пайплайнах.",
  "knowledge_units": [
    {
      "claim": "По данным исследования на 100k+ GitHub-разработчиков, включение автономных агентов даёт +741% написанного кода, но лишь +30% реально задеплоенного ПО — ревью становится узким местом.",
      "type": "benchmark",
      "actionable": "При масштабировании агентной генерации кода заранее закладывать мощности и процесс именно под ревью/верификацию, а не только под генерацию."
    },
    {
      "claim": "По двадцатилетнему исследованию в Cisco, эффективность человека-ревьюера резко падает после ~400 строк за присест и ~450 строк в час.",
      "type": "benchmark",
      "actionable": "Не пытаться линейно наращивать объём человеческого построчного ревью под агентные PR на 10k+ строк — это физически не масштабируется (3-4 дня на одно PR)."
    },
    {
      "claim": "OpenAI построили внутренний продукт (~1M строк, ~1500 PR за 5 месяцев, 3 инженера) почти без вручную написанного кода, где ревью делают преимущественно агенты друг другу, а не люди.",
      "type": "tactic",
      "actionable": "Рассматривать agent-to-agent review как рабочую модель для некритичных внутренних продуктов, но учитывать, что компания не раскрыла детали — подход ещё не проверен публично."
    },
    {
      "claim": "Ключевой тезис доклада: в 2026 правильный уровень абстракции — не ревью отдельных PR, а инженерия самого харнеса ревью (бенчмарки, классификаторы, рубрики, тест-сьюты, evals), которые кодифицируют критерии 'хорошего кода'.",
      "type": "principle",
      "actionable": "Инвестировать время не в построчное ревью диффов от агентов, а в написание и поддержку evals/рубрик/тестов, которые потом масштабируемо прогоняются на каждый агентный PR."
    },
    {
      "claim": "Для продакшен-систем важнее не статическое ревью кода, а трейсинг/наблюдаемость реальных 'траекторий' — что система фактически делала шаг за шагом в проде.",
      "type": "tactic",
      "actionable": "Внедрить мониторинг реальных трасс выполнения агентных систем в проде как дополнение (или замену) ревью кода перед деплоем."
    }
  ]
}
```
