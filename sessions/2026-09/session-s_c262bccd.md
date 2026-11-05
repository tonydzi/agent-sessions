---
session: s_c262bccd
date: 2026-09-25
words: 2008
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c262bccd` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Building uReview, Uber’s Multi-Agent Code Review Engine — Will Bond & Ameya Ketkar, Uber
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> All right, hello everyone. My name is Will and uh I'm here to talk to you about automated code review. Uh my teammate Amir and I work at Uber and we're going to be walking through U Review, a system that Uber has built uh to help increase the velocity of our software engineering teams. Um for a little bit of context about what software engineering org at Uber looks like, we have thousands of software engineers who work across hundreds of teams uh located across 12 different sites and uh they work in primarily one of six language-specific monorepos. As many of you have probably noticed over the past 24 months, the volume of PRs, the size of PRs has been growing. One of the ways that that's been exposed to us has been through uh the metric that we track of the first time to review. Back in 2024, we were seeing that engineers would get their first review within 3 hours. Now in 2026, that has grown to 9 hours uh in addition to all of the volume changes. So, in short, code review is now the bottleneck that we are running into. Um specifically around automated code review, uh there are there are various options available in the industry, uh but Uber spent the time to invest in building an in-house solution due to some of the constraints that we have. One of those is uh we currently use Fabricator and have for a long time and are in the process of migrating to GitHub. Uh most of the solutions do not provide support for Fabricator. Um in addition, if you were at the previous talk, you saw Uday and Adam talking about the agentic SDLC. A big part of what we want to do is bring a consistent code review experience to the inner loop so that our agents are getting the same code review, the same rules, everything applied as our humans do. With hundreds of teams across the company, we can't have centralized management of our code reviews, our customizations, and our rules, and even the knowledge that goes into those code reviews. We need to distribute that. So, we have a need for plugging into existing team ownership system rather than trying to replicate that externally. Uh finally, with the volume of code reviews that we perform, we need the ability to take factors like the risk profile and the complexity of a code change and factor that in when deciding how we're going to run a code review. Not all code gets the exact same review. And then finally, consistency. We need to make sure that we have security and compliance reviews run across everything. We can't rely on teams hoping to run the skill the code review skill that happens. We need reliability there. With all that said, I wanted to give you an overview of the architecture of what you review looks like. We'll talk about a couple of the big pieces, and then we're going to dive into a few focus areas. At the top, you'll notice that we have our code review surface areas, GitHub, Fabricator, and the agent loop. These all feed into you review service. These This takes in requests for reviews. It brings in feedback from users, and it routes it. We have a number of different generators. Now, these generators are tuned for different performance and cost avenues. There are We also have the ability to plug into third-party code review systems so that we can compare ourselves to what's available more broadly. Finally, with all these different generators, we might be might be duplicating comments, and we can actually create quite a high volume of comments. If you've ever used AI to to run a code review, you've probably seen that. So, we run through a number of steps in the post-processing where we both rate, categorize, filter, and deduplicate comments so that our engineers get only the highest confidence comments that are actionable for them to work on. You'll also notice along the bottom we talk a little bit about feedback in our evaluation. But, with this context of the overall system, I'm now going to hand it off to Ameya to dive into our first focus area. >> Hello. Hello, everyone. So, I will be talking about how we evolve U review with observability and evaluation. So, U review had a very humble beginning. Basically, it was a single prompt that you should do logic checks per file, a simple agent which used to do thorough review. And we had a dispatcher to decide whether to go which generator to choose. Even what we used to collect as observability was very surface-level. We used to collect cost. We used to run an NPS survey, have Google Forms being filled, Slack support. And with all of this, we saw that our quality to cost ratio was like all over the place. Like, our goal is to be in the second quadrant, that is the top left quadrant, but you can see we were all over the place. Then what we did is that we started collecting more data. So, we started collecting the sentiments of the replies that were made to the U review that the U review uh call you know, the U review agent got from the developers. So, we categorized them into positive, negative. We classified them into various categories, and we found a bunch a lot of classes of bugs and issues that we could actually solve. And with that, we improved the system, and we were able to move a large number of PRs to a high quality to cost ratio. Um but, we still felt that this was not enough. We need to know more of how the review is done. So we started tracking things like address rate. So basically when a U review comment is made, does the developer go and actually address the comment? We started tracking that. And then we also started doing more like a runtime profile, which is like the agent trajectory, which told us why the agent is doing what it what it did. We get to know what tools calls it made. We get to know what thinking process it had. And then with that insight, we were able to actually tune our runtime, tune our performance such that the agent could very quickly give us high-quality results at a low cost. One of the biggest learnings in this process was like the model doesn't kn
...[middle elided]...
x 100 nits on a pull request where your engineers really get frustrated in situations like that. Um but probably the most interesting aspect of this transition is the feedback. As you can see, quite a bit of what went into getting high-quality code reviews at Uber was bringing the human feedback into the system and using that to figure out how to tune our prompts, how to tune our agents. Uh and so as we move to a model where humans are less in the loop, where software engineering is moving to an agentic model, we're effectively going to a place where we're starting to talk about are we going to kill the outer loop? Is the human engineer not going to be involved in the code review. Some people are already here. Now, with the feedback taken into consideration, you start wondering, all right, what could this result in, right? I'll let your imagination go there in terms of quality degradation, slop, and so forth. But, rather than killing the outer loop, I think that we believe and the industry has just started to really kind of coalesce on this idea that we're really expanding the outer loop. Rather than removing humans from the code review process, we are moving their responsibilities up a layer. Rather than them dealing with the details of the implementation, the agent is great at writing the software. The agent is getting much, much better at reviewing the software as a human would. But now, as software engineers, we still are going to have an outer loop. It's just going to look a little different. Instead of you worrying about the optimization of the performance and the API compatibility, you're going to be thinking more about architecture in your code reviews. You're going to have time to focus on the domain expertise that you have and product thinking. So, we believe that as we adopt this automated uh code review, this is going to be the result of how our engineers are interacting with the system and guiding it. And that's it. Thank you so much for coming. Thanks.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-code-review",
  "signal": 0.72,
  "novelty": 0.55,
  "actionability": 0.68,
  "evidence": 0.75,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 500,
  "why": "Доклад Uber про uReview даёт конкретную архитектуру и метрики эволюции AI-ревью кода (от NPS к address rate и трассировке агента), а не просто рекламу или хайп-новость.",
  "knowledge_units": [
    {
      "claim": "Чтобы AI-код-ревью не заваливало разработчиков дублями и шумом, нужен пост-процессинг после генераторов: рейтинг, категоризация, фильтрация и дедупликация комментариев перед показом человеку.",
      "type": "workflow",
      "actionable": "Если строишь мультигенераторный код-ревью пайплайн, добавь отдельный этап дедупликации/фильтрации по confidence перед выдачей комментариев, а не полагайся на то, что каждый генератор сам не будет спамить."
    },
    {
      "claim": "Метрики типа стоимости и NPS недостаточны для оценки качества AI-ревью; ключевой сигнал — 'address rate', то есть реально ли разработчик исправляет то, на что указал агент.",
      "type": "tactic",
      "actionable": "Добавь в свою систему оценки AI-агента метрику 'процент рекомендаций, которые пользователь реально применил', а не только стоимость и субъективные оценки."
    },
    {
      "claim": "Для тюнинга качества и стоимости агента полезно логировать полную траекторию выполнения (какие тулы вызывались, какие рассуждения делались), а не только конечный ответ.",
      "type": "tactic",
      "actionable": "Включи трассировку рассуждений и tool-calls агента в observability, чтобы диагностировать, ПОЧЕМУ агент даёт низкое качество на конкретных кейсах, и точечно чинить промпт/раннтайм."
    },
    {
      "claim": "Не все код-чендж должны проходить одинаковый по глубине ревью — глубина/набор проверок должны определяться риск-профилем и сложностью изменения.",
      "type": "principle",
      "actionable": "Дифференцируй строгость и стоимость AI-ревью по эвристике риска (размер диффа, затронутые модули, история багов), вместо единого прогона для всех PR."
    },
    {
      "claim": "По мере того как агенты берут на себя код-ревью, роль человека не исчезает, а смещается на уровень выше — архитектура, продуктовые решения и доменная экспертиза вместо разбора мелких деталей реализации.",
      "type": "principle",
      "actionable": "При внедрении AI-ревью в команде заранее переопредели зону ответственности ревьюеров-людей на архитектурные и продуктовые вопросы, а не оставляй их дублировать то, что уже покрывает агент."
    }
  ]
}
```
