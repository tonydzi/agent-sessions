---
session: s_edc94154
date: 2026-09-23
words: 1877
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_edc94154` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How do you diffuse AI into the real world? — Varun Shenoy, Long Lake
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hi everyone. I'm Varun. I'm one of the co-founders at Long Lake and I'm excited to share a little bit about what we've been up to for the last 2 years. It all comes back to a question all of us have asked time and time again. The models are getting better, but the real question is how do you actually deploy the AI into the real world? How do you get the models to complete economically relevant tasks? Let me start by saying everyone has seen the demo. Think of the agent automatically booking a flight, the agent automatically completing a ticket in some kind of customer service portal. Think of an agent completing a block of code ready to commit and go. The reality is we've all seen this and it feels like magic. 2 years ago any of this would have been complete science fiction. The capabilities are real. Now, walk with me into a 200-person property management firm. Real people, real properties, real dollars, real customers all across the US. You would expect AI to show up by now, but the reality is nothing has changed at all. Here's the thing. This is totally normal and maybe in fact I'd argue this is what we should expect. This is true for every general-purpose technology. You know, take electricity for example. Electricity was invented in the 1880s and it was first demoed at Edison's Pearl Street Station Dynamo Room over in Manhattan. This was the magic demo of its time. The reality is it took a long time for electricity to be fully adopted. Consider a Ford factory. It's not enough to just have electricity. You have to rip out the existing motors and equipment. You have to bring in the new equipment. You have to go and train everybody to use that very same equipment. Here's a picture of a Ford electrified moving assembly in 1924. These things take time. Diffusion of any technology takes a generation. And since everyone here in this room today is talking about AI, I would argue AI diffusion is perhaps the single most important problem for the next 20 years. The models are going to keep getting better. The big question is how do we actually get these models to be in the real world, complete real tasks, uh and make people more efficient, happier, and provide better service. So taking a quick step step back, who are we? Uh we are Long Lake. Over the last 2 years, we've raised over $3 billion from Elad Gil, General Catalyst, and AlphaWave since our founding. Here's the strange part. We we don't sell software. We actually go out and acquire and partner with real services businesses in the world. Uh we've acquired 35 businesses across HOA and property management, architecture, HR services, and a lot more. To give you a little bit more flavor, we have roughly a 40% team right now split between technology, finance, and operations. More than half our team is part of the technology team focused on uh building products, data, and deploying the core products into the field. Uh we're in a collected group of folks, a bunch of ex-founders who've worked in the services before, ex-military, folks from Palantir, Ramp, Glean, uh and from the finance side, Blackstone, H.I.G., et cetera. We are we are not selling them to these companies above from the outside. We're actually deploying into these companies and figuring out how to get the technology to work. And just to show you the scale we're playing at, we announced recently our $6.3 billion take private of American Express Global Business Travel, the world's largest corporate travel platform. We own these businesses. So, when the AI doesn't work, it's not their problem. We're not the vendor. It's our problem. Concretely, again, we are not the vendor. We are the operator owners. And we work very closely with our teams within the businesses to drive real outcomes. Now, I want to step back and get to the concrete about the how. What are the lessons we've learned over the last 2 and 1/2 years? And what we've learned from deploying AI into companies we've owned. Three quick lessons. One, how we move agents from co-pilots to co-workers. Two, how we leverage real-world data within these businesses. Remember, we're seeing all of the work that's being done in these real services businesses. There's a lot of interesting problems and solutions embedded within that. And then finally, perhaps the most interesting and exciting is how do you actually get all of this technology to compound over time by learning loops in the enterprise. We'll get to that at the end over here. So, starting off from co-pilots to co-workers. There's a spectrum of how much autonomy you can give an agent. On the left here, you see a co-pilot. This is, you know, your simple rag chatbot from 2 years ago. It's very quick. You can ask a question. Maybe it's integrated with some systems. It can give you information back very, very quickly. The second step is a synchronous agent. Consider something like Claude code, Codex, Claude co-work. It's real-time. There's this two-way interaction. It's a bit more sophisticated than a co-pilot. You can go let it run off for 1 to 5 minutes. Uh it'll call tools, maybe use its skills. Uh it's still synchronous. You still need to step in and ask a query. So, the next obvious rung of the ladder is the asynchronous agent. You can come in here, still ask a query. The agent will go off into the background, do some work, and then come back. Uh and what's really interesting about asynchronous agents is that the user does not have to be the one that triggers them. You can have external triggers as well. Maybe someone completes a certain task and there is an async job queue uh that allows the async agent to pull off from and proactively offer advice to the end user. Then, I'd argue the next step is a long-running agent. How do you get these agents to work for hours, days, weeks, months, etc.? I think this is currently a very core problem that a lot of the labs are focused on, as are we. And then finally, at the end, the holy grail, an AI co-worker. This is where m
...[middle elided]...
t? What you know, this this seems like incredibly hard. What what's the upshot? How do you actually get this stuff to work? Well, I think a lot about Jensen and how he dominated the market in his words with extreme hardware software co-design. Designing the chips and the software together as one system. We look at this through the lens of extreme software service co-design. How do you co-design our products with the people and the processes at our businesses? And I'd argue this is only possible from being within under the same roof. We need to meet the people within these companies both metaphorically, for example, bringing products to their systems so that the energy required for enablement is kept low, and also physically. Get on a plane, show up, say hi, learn what people actually do. You know, maybe you build a product that's natively embedded into Excel or into their ERP system, maybe their 3D design software, or or maybe even their Microsoft products like Outlook, Gmail, etc. Or you show up in person. You do a lunch and learn with a bunch of folks at one of the companies. You go to their conferences and you create cotton candy and run a stand for them. You go mountain biking and ask them about all the difficulties that they have with their actual day-to-day jobs. Or you show up in person one-on-one or sometimes even two-on-one in this case and just show them how to use the tools and learn from the feedback because this is what the rest of the world really looks like. It's not like the folks in this room or in San Francisco. It's a lot more like this. You cannot co-design software with the services business over Zoom or over a support ticket. You you have to be there. You have to be in person. And I'd argue this is the part that actually makes it work. In order to get AI diffusion to work, you have to touch some grass. Thank you so much. I'll be around for the rest of day if there's anything I can help with. My email is up there. And yeah, thank you. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-ai-deployment",
  "signal": 0.3,
  "novelty": 0.25,
  "actionability": 0.2,
  "evidence": 0.35,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Конференционный доклад про бизнес-диффузию AI в реальные компании — есть полезная рамка автономности агентов, но почти нет конкретных инженерных техник, применимых к разработке систем.",
  "knowledge_units": [
    {
      "claim": "Автономность агентов образует лестницу из 5 ступеней: co-pilot (чат-ответ) → синхронный агент (Claude Code-подобный, работает 1-5 мин с вызовом инструментов) → асинхронный агент (уходит в фон, может запускаться внешним триггером, не только пользователем) → долгоживущий агент (работает часами/днями/неделями) → AI co-worker (полная автономия).",
      "type": "principle",
      "actionable": "При проектировании агентной системы явно определяйте, на какой ступени лестницы находится ваш агент, и какие механизмы (внешние триггеры, очередь асинхронных задач, память между сессиями) нужны для перехода на следующую ступень."
    },
    {
      "claim": "Внедрение AI в реальный бизнес-процесс проваливается без совместного проектирования продукта с людьми и процессами на месте — только удалённой демонстрации или тикетов поддержки недостаточно, нужно физическое присутствие и встраивание в существующие инструменты (Excel, ERP, Outlook).",
      "type": "tactic",
      "actionable": "При выкатке агента в существующий бизнес-процесс встраивайте его в инструменты, которыми люди УЖЕ пользуются, вместо создания отдельного интерфейса, и собирайте фидбек лично, а не только через тикеты/зум."
    }
  ]
}
```
