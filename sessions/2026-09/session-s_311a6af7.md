---
session: s_311a6af7
date: 2026-09-27
words: 1862
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_311a6af7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Building Blocks of GTM Orchestration — Arman Vaziri, Ramp
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Yeah, I really appreciate everybody showing up. Uh, as Madhu mentioned, my name's Armon. I lead our product and sales-led growth engineering teams at Ramp. Um, and today I'm going to talk to you about, uh, the building blocks of go-to-market orchestration. And um, to kick it off, like, what do I mean by go-to-market orchestration? Effectively, like, what we're building towards is the ability to just describe a motion, right? Whether it's like playbooks or experiments or like evergreen campaigns that you want to run. And how those get like distributed across the channels through which you actually execute your go-to-market, right? Whether it's outbound or ads or web or whatever. Um, we want the ability to kind of describe this and automate that output. And this really started a few years ago where we kind of noticed that uh, there's a ton of great ideas, you know, like everybody across product and data and engineering and go-to-market have like really good ideas for things that they want to do. And the bottleneck is kind of like everything after that, right? How do you go pull an audience to go and target? How do you go and convince a bunch of people to like um, abide by whatever strategy that you've come up with or playbooks or enablement materials. Um, and we wanted to try to aim to uh, reduce that coordination cost. So, there's parts of this where we could see it as like an engineering problem, even like a few years ago, just go and create like a consistent data substrate, go and like federate that across the different systems through which you, uh, run your go-to-market. And obviously in the last few years, agents have really like deepened our ability to go and like push the level of automation that you can do on behalf of operators like as close as possible to those points of execution. Um So, like really specifically, uh I'm a golfer. Suppose I want to offer golfers at uh East Coast construction companies an incentive to like try Ramp, talk to sales, whatever. Uh and we want to be able to go and spin up an audience of uh golfers at East Coast construction companies, spin up like an incentive. Let's go offer like some Pro V1 golf balls to uh these people, go create like outbound sequences, generate the copy, generate uh creative for paid ads and for web, maybe show some in-app notifications for your customers, and do all of that seamlessly by just describing the intent, right? And probably more than just this one sentence. Um So, a few years ago, we kind of identified uh a few fundamental challenges here. Um As was previously mentioned, uh the necessary data for this was just messy, inconsistent across systems, right? Everybody's operating off of a different uh source of truth, and that makes it like effectively impossible to go and distribute some coordinated action across these different go-to-market teams and channels. Uh The next is that like reps were just buried in busywork, right? Even if like you have the best intentions, I want to go and like run this campaign, uh I want your help doing it. The reality is that like uh our sales teams are in back-to-back-to-back-to-back meetings all day. They're outbounding, they're selling, and um the operational burden of like doing everything in between sales was just really high, uh which made kind of like really scaling out experimentation and creativity challenging. Uh And similar to that, just the coordination and distribution are expensive, right? If you're like, "I have this idea. I'm going to go write this like proposal, this enablement material. I'm going to go try to like convince a bunch of people to go and use all of this." That's just like a really challenging thing to do on any like pace that's not on the order of like months. Um So, um over the last few years we've been trying to solve this problem from the ground up, right? How can we start with that uh ingestion and consistency problem uh and data quality, which is just like, you know, on the road map every quarter. Um how can we then go build those vertical efficiency and growth levers, uh saving people time uh in like managing operations and execution, uh as well as like how can we improve conversion rates, make people more performant by being able to kind of scale some of these more like uh informed and personalized and creative strategies. And then how can we extend this horizontally, right? Teams have very common workflows at some level, right? Everybody wants to outbound, everybody has meetings. Uh how can we go take the patterns that we build for one team and start to just mirror it to others? Uh and now kind of where we're at is like this distribution and coordination problem, right? How can you go and execute across multiple channels simultaneously through just like the description of intent? So, yeah, I'll get into the building blocks. Really broadly, uh go-to-market agents are complicated. Um in order to do this effectively, right? Your agents have to understand pretty much the entirety of your company, how you go to market, why products are useful, uh how to kind of like segment your buyers, your prospects, your customers from people who have like never heard about you and you have like no information on them and they have no information on you, all the way to like customers who are actively using your products who have like a totally different set of um you know, problems that you have to work with. Um And to just start to get a little technical here, um we started with like this consistent data foundation uh problem. And if you're looking at this and you're like, that looks like a CDP." Uh yeah, you're you're right. Uh we effectively went and built um an internal customer data platform at Ramp uh where we're effectively doing your very traditional things. We're going to take CRM data, product data, uh enrichment data, um web data, buying signals, you know, whether it's things that are internally modeled like um I don't know, we think that this custo
...[middle elided]...
with these campaigns, we can go and execute them across like multiple channels with consistent audience targeting, um agents can go and hold context on multiple things that are like options, right? We can go and execute this campaign or that campaign or that experiment and balance the like traditional multi-armed bandit problem of like exploring like new possibilities versus like being safe and like going into just known returns. Um and then we can build in guardrails as well to go and um effectively like manage compliance rules, rules of engagement, and being context aware, making sure we're not doing the same thing over and over again. Um and yeah, just do this on behalf of everybody. And those are the building blocks of go-to-market orchestration. Thank you, everybody. >> [applause] >> We have probably time for one question. Hey, there we go. >> Hey. >> [clears throat] >> So, just curious um if how would you approach building something like this for a smaller company or for a company that's that's just getting started? >> Yeah, I think a few people before have like mentioned something similar, but I would go and like find the very specific use cases that you can build automation around and just like solve really specific problems that exist first. Um like 3 years ago, there was two of us and we were building like automated outbound, right? So, like we're just trying to figure out like how can we go and use GPT 3.5 and like put personalized copy uh into some sequences and go and like pull data from uh wherever to go and generate that. And by doing these things and solving these problems, you get like a really good understanding of how this works, how it could extend to other teams. Um and solving like real problems as you go. The reality is that like you can't spend like a year going and building like some really complicated system architecture that like is perfect. So, you have to like piece together the vertical solutions and then stick them together. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "gtm-orchestration",
  "signal": 0.35,
  "novelty": 0.25,
  "actionability": 0.35,
  "evidence": 0.55,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 400,
  "why": "Доклад про внутреннюю платформу Ramp для оркестрации go-to-market агентов — интересен как кейс, но конкретных инженерных техник (промпты, архитектура агентов, код) почти нет, в основном общие принципы продукт-менеджмента.",
  "knowledge_units": [
    {
      "claim": "Перед тем как строить агентов, автоматизирующих go-to-market, нужен единый консистентный слой данных (внутренний CDP: CRM + продуктовые данные + обогащение + веб-сигналы), иначе агенты не могут координированно действовать через разные каналы.",
      "type": "principle",
      "actionable": "Если строите агентную автоматизацию для продаж/маркетинга — сначала консолидируйте источники данных в единый слой, а уже потом добавляйте агентную оркестрацию поверх."
    },
    {
      "claim": "Начинать стоит не с идеальной универсальной архитектуры, а с решения одной узкой конкретной задачи (пример: автоматизация персонализированного outbound через GPT-3.5), и потом расширять паттерн на другие команды.",
      "type": "tactic",
      "actionable": "При старте agentic-проекта в небольшой команде выбирайте одну узкую боль, автоматизируйте её полностью, и только затем масштабируйте найденный паттерн вширь на смежные процессы."
    },
    {
      "claim": "Агенты, ведущие параллельные кампании/эксперименты, балансируют между исследованием новых вариантов и использованием проверенных (multi-armed bandit), и нуждаются в guardrails на соответствие политикам и недопущение повторных одинаковых действий.",
      "type": "workflow",
      "actionable": "При проектировании агентов, выбирающих между несколькими кампаниями/стратегиями, явно закладывайте explore/exploit баланс и контекстные guardrails против дублирования действий и нарушения комплаенса."
    }
  ]
}
```
