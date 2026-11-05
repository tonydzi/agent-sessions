---
session: s_855df258
date: 2026-09-23
words: 1992
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_855df258` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: From AI-Assisted to AI-Native: Building a Frontier Development Team — Clare Liguori, AWS
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> My name is Claire La Gory and I'm a senior principal engineer at AWS. I mostly work on Kuro, our agent encoding assistant, but today I want to talk about some of the practices we've been seeing inside of Amazon and Amazon teams where we've been seeing really exciting results of productivity increases that are step function improvements since what what we've been seeing with AI so far. So, I've been working on agentic AI for over 3 years now and I've kind of seen the evolution that's happened in our industry when it comes to coding assistance with AI. First, we had this inline code completion helping us to write the next line, maybe the next function. We moved on to chat, asking questions about our code. Everybody started doing vibe coding sometime last year, but now we're starting to see kind of an early adopter phase of what we've been calling frontier development. And completely anecdotally, based on my own experience, I've really only felt maybe 10 to 20% more productive with all of these phases that have come before. But now inside of Amazon, we've been running pilots with different teams across the company and we've been seeing a median of 4.5x productivity improvement and sometimes more than 10x. So, something has really changed here now that we're seeing these step function improvements in productivity. And I like to define what we've been calling frontier developers inside of Amazon by three behaviors that I've been seeing. One is hands-off coding. Frontier developers write maybe 1 to 2% of the code that they produce. The rest is agents. The second is that they interact with their agents infrequently. They'll aim to get their coding assistant to run for up to hours at a time without their intervention. And third is that they minimize idle time. These frontier developers tend to run multiple agents in parallel churning through a backlog of tasks. The first time that I saw a frontier developer team was the Bedrock Mantle team. Bedrock is our model hosting service. Hosts LLMs like Claude and GPT. And sometime last year we knew or I say we but the Bedrock team knew that they were going to need to build a new inference data plane. But they had estimated it at 30 people over 18 months. This is a big big service and it was going to take time to build the new one, migrate customers over, migrate models over. They decided to take a step back. They took six people and they built [snorts] it in 76 days with Kiro. So this was a huge achievement. This was the first time we've we'd seen anything of the kind inside of Amazon. So this was truly the pathfinder team that proved that it was possible to get up to 20X improvement. Now they looked at commits and I'll talk about a couple of other ways that we are uh measuring productivity improvements. But there was one problem with this story which was that yes, it was built with six people. It was built with some of the top engineers literally in the company including two distinguished engineers. So this was not just any team of six people. These were experts in distributed systems, experts at LLMs and their architecture. So this the story was amazing and it kind of spread like wildfire across Amazon, but it was also very unachievable for a lot of teams. There were a lot of questions about can this actually be reproduced on another team? So, another experiment that I want to talk about is an experimental sprint that was done in the Prime Video organization. They took a 10-day sprint and they did an experiment where they put, again, six engineers in a room and they let them go wild with Kiro. Uh they brought down the project delivery time estimate from what was going to be 90 weeks down to 24 based on all of the progress they had made in this 10-day sprint. And they they looked at their commit history and they looked at what did they used to do prior to this 10-day sprint and how many commits did they produce just in this 10 days. And so, this sprint really proved that we can achieve, again, at least something close to what the Bedrock Mantle team had uh had achieved with a different set of engineers. But again, there was a challenge with this story, which was it was six engineers in a room, but they had no on-call duties, limited meetings, very few distractions, which we all know are regular in the lives of an engineer. And the senior engineer on the team had spent the previous 3 weeks creating very detailed, small, well-scoped tasks with detailed requirements for these six [clears throat] engineers to just go churn on for those 2 weeks. So, this was again not necessarily real life. This was a structured sprint, uh a a point in time that they were able to achieve this, but again, the question is is this achievable on real teams on day-to-day work? So, Amazon stores which encompasses amazon.com, all of our retail websites, as well as our physical stores, did a more structured pilot. They watched 50 teams that were totally normal normal distribution of um early career folks, mid-career, senior engineers, and that worked on existing systems. Nothing green field like the mantle team got to build from the ground up, but existing systems with existing code bases. And they they watched them for the better part of last year, and they found something super interesting. They found that there was a big difference in the productivity gains that they saw between half of the teams and the other half. And in this case, they used a productivity metric of deployment velocity to production. So, not just commits, how many commits are they producing, but how quickly are we getting changes out to customers? How how quickly are we able to ship things? And they saw that for half of the teams, they achieved less than 3x increase. And what they found that was the difference between seeing less than 3x productivity increase, these teams that saw a median of 4.5x, and and in some cases more than 10, was how they used the tools. 90% of these teams used Kiro, among ot
...[middle elided]...
Pathfinder, from the from the sprint experiment, from the pilot uh teams within Amazon. And now the challenge for us is how do we scale it out? And that's what 2026 is about for Amazon is how do we scale this out to more and more teams, to the next uh 2,000 teams instead of uh 50 teams. Um and so I think that when you roll it out too quickly, you have a lot of teams who don't know what they're doing. You haven't had time to find the best practices for your own organizations, the the context that your organization needs. And the last one is that you're going to find new bottlenecks. Previously, code writing code manually was the bottleneck. Um I find that within Amazon, we've found um the speed of decision-making becomes a new bottleneck. >> [snorts] >> Um all of the review processes associated with the launch of a product become the bottleneck. When it used to take 9 to 12 months to build a new product, it didn't matter so much in the in the overall wash of things if it took two months to make the decision to build the product and then two months to approve the launch. But now those are the bottlenecks. Those are the long pole. And so you find all of these all of these things that slow you down. Often I find that frontier engineering teams spend more time making decisions than they do writing code. And so the more that you can make fast decisions, especially ones that are easy to be reversed, the better. So my one big takeaway for for everyone here is that frontier engineering is about intentionally changing the way that you work. And that is difficult. That takes time. It is forming new habits and a new way of working. And that goes across any engineering team as well as your organization. Um so I encourage you to think about um how you're interacting with AI tools and how that can change to free yourself up from being in the loop. Um thanks. I'm going to I'll hang out uh a little bit if anyone has questions in the back. Um but thanks for the time today. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding-productivity",
  "signal": 0.55,
  "novelty": 0.4,
  "actionability": 0.4,
  "evidence": 0.6,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад инженера AWS про внутренние пилоты Amazon с агентным кодированием (Kiro) даёт конкретную поведенческую рамку и цифры производительности, но мало конкретных техник — в основном кейс-стади и организационные выводы.",
  "knowledge_units": [
    {
      "claim": "«Frontier developers» определяются тремя поведениями: пишут сами лишь 1-2% кода (остальное агенты), запускают агента на часы без вмешательства, держат несколько агентов параллельно, чтобы не простаивать.",
      "type": "principle",
      "actionable": "Оценивай себя не по тому, сколько строк написал, а по тому, сколько времени агент работает автономно между твоими вмешательствами, и запускай несколько параллельных задач вместо одной последовательной."
    },
    {
      "claim": "В пилоте на 50 нормальных (не элитных) командах Amazon Stores разница между <3x и медианой 4.5x (иногда >10x) прироста производительности определялась не тем, каким инструментом пользовались, а тем, КАК его использовали (привычки работы), а не самим фактом внедрения инструмента.",
      "type": "benchmark",
      "actionable": "Не жди прироста производительности от простой установки агентного инструмента — нужно осознанно менять рабочие привычки (отпускать контроль, ставить агенту крупные автономные задачи), иначе выигрыш останется в пределах 2-3x."
    },
    {
      "claim": "При резком росте скорости написания кода узким местом становится не код, а скорость принятия решений и процессы ревью/апрува запуска продукта.",
      "type": "principle",
      "actionable": "Одновременно с ускорением кодогенерации агентами инвестируй в ускорение и упрощение процессов принятия решений и согласований — иначе именно они станут новым тормозом всей разработки."
    },
    {
      "claim": "Экстремальные результаты (76 дней вместо оценки 30 человек × 18 месяцев; 90 недель сжатые до 24) получены на нерепрезентативных условиях: топ-эксперты компании, отсутствие on-call и совещаний, заранее детально расписанные задачи от старшего инженера.",
      "type": "tool-caveat",
      "actionable": "Относись к громким цифрам ускорения (10-20x) как к потолку в идеальных лабораторных условиях, а не как к ожидаемому результату для обычной команды с обычной нагрузкой — планируй консервативнее."
    }
  ]
}
```
