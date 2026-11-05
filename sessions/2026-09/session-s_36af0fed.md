---
session: s_36af0fed
date: 2026-09-28
words: 1994
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_36af0fed` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Software Engineering Is Becoming Factory Engineering — Zach Lloyd, Warp
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Okay. Hello everyone. Uh, I'm excited to be here. Uh, my name is Zach Lloyd. Um, today I'm going to be talking about self-improving software factories, the new open-source model, and basically what I think is happening to development. A little bit about me just to begin. So I am a former uh principal engineer from Google. Used to lead engineering on the Google Doc Suite. I've been an engineer now for over 20 years. Long time. I am still uh shipping frequently, but I haven't written a line of code in the last six months. Uh and I'm the founder of a company called Warp. Uh Warp, if you're not familiar, is a open-source agentic development environment. Uh you may know us as a terminal. That is how the company started. We're basically a terminal that has agents built in. Uh we open sourced it a couple months ago and I'm going to talk a little bit about that experience and the motivation for it. It's popular open source project over 60,000 GitHub stars. We've had a couple hundred people contributing. We have over 800,000 active developers who are using warp. And increasingly we are focused not just on the terminal aspect and the interactive aspect of development but more so on how do you automate development. I'm going to talk mostly about that. So the thesis that I have uh is that the discipline of software engineering is going to become something more like factory engineering. And I'll explain what I mean by this in a minute but just keep that in mind. That's that's what I think is going to happen. Um, if you look at development over the past couple years, it's I mean it's crazy how it's changed. We've gone from a world of chat and AI autocomplete cursor co-pilot to the phase that we're in now, which I consider to be mostly interactive agents. So you're sort of sitting at your computer and you are telling cloud code to do something, you're telling warp to do something. And I believe what's going to happen over the next six months, a year, hard to predict the pace, is that we're going to move much more towards a world of automation. But before I get into that, just quick show of hands. How many folks in here are building with agents? Every 100% makes sense. Uh how many how many folks are building typically with multiple agents at one time? So again, almost everyone. How many people are running an agent right now? I'm not offended. I would. Okay, that's totally cool. I would be doing it too. Uh, how many folks are running agents in the cloud out of curiosity? So, that looks like less than half, but still significant. Uh, and how many folks have have set up a system internally to automate the whole software development life cycle? So, everything from like triaging, specking, implementing, reviewing. So, I see some hands. So some people are doing this. So this is what's going to happen. Uh every project of significant size I believe is going to have something like this. Um and it's going to look kind of like this big loop. And everyone is talking about loops. There's nothing that complicated about loops. This loop says a cloud software factory. This loop could literally just say like the software development life cycle. It's the same thing. Um but just to go through this loop, it's like ideas are going to come in at the top. Agents are going to do triage. If something is complicated, they will write a spec. Uh these little blue boxes are where humans step in. Humans will review the spec. Uh agents will do the implementation. A human and agent will review the code. Agents will verify. Human will review the product. You ship and then you monitor and round you go. Uh and this is what software development for better or worse I think is going to end up looking like. So I repeat the thesis which is that if this is what software engineering is going to look like um software engineers are going to be the ones who end up building and managing these factories. [snorts] Now I promised at the beginning and I put in the title of the talk that I was going to talk about open source and so I want to do that for a few minutes. I'm going to take a quick digression. Um, I bring up open source because one of the main reasons that Warp opens sourced was to build uh build a public factory. Um, and so this is a picture of this website we've built called build.warp.dev which shows all of the issues that are flowing through our system and what state they're in, what agents are working on them, what contributors are working on them. And it's kind of like a protoactory done at scale. It's not working perfectly, but it is working. And one of the reasons we open sourced was to try to build this. Um, just in general, I think it's interesting to talk about open source in the time of agentic development. This is a really stupid graph, but it's like it just it you get it. It's like it's becoming much cheaper to build software. Um, a correlary of that is that it's becoming trivial to clone software. And so if you are in the software business, and I don't know how many folks in this room are in the software business per se, but it's very hard to build a software business if it's free to build software. It's hard to capture the value, especially if a competitor can clone. And so my big takeaway or big tip for everyone in here is that the first thing you should do is patent your code. I'm kidding. Don't This is a complete joke. [laughter] Don't don't don't do this. Uh my my first tip is obviously you need to have a great product. Uh this has always been the case. Um but I would say a great product probably was never enough. But even now more than ever, if you think that you're going to build a great software business just by building and shipping a great product, you're probably not going to succeed. Uh you need advantages beyond the product. And so those advantages could look like distribution ecosystem. It could be that you have a great brand or a data moat. You might have capital. Um, but if you're a startup, again, I'm
...[middle elided]...
 you can learn. I do think I don't know if you're a computer science student, but I still think there's a ton of value in understanding like the underlying systems and architecture and being able to reason and understand the code, understand the specs that agents are written, sorry, are writing. So, I I would focus on on those skills. Um, and like I don't know, we're hiring more people than we've ever hired. There's a lot of kind of like misdirection around like you know people not being hired because of AI. That's not the experience we've had so far. And what I'm looking for are like really adaptable product focused thinkers who can like basically be great problem solving problem solvers uh even as the underlying technology changes. Yeah, I think I have time for one more question. Yes. What about the like so the question was what about the the product taste and like the how do you actually build something useful I think is probably the right like maybe the framing and like uh where do the ideas come from and so I think that um the problem with the factory metaphor even though I'm like leaning into it because I think that's like that there's something to it is that it can kind of sound like uh mechanizing or dehumanizing um and I still think underlying ing all of this, the only thing that matters is like are you building something useful? And if you have like a a factory that is like churning out that no one cares about, it's like what's the point? And I think that human taste, human input, human product sense, um humans like guiding at those touch points where you can't automate stuff is absolutely like essential. And like that's like what I do like I'm trying to figure out what what do customers want, what do people want, what's going to be valuable to them. So I think that's an absolutely key point to it. I think I'm at time so I I have to go. I hope folks uh enjoyed this chat. I'm really grateful for being invited to speak. So thank you all very much. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding",
  "signal": 0.45,
  "novelty": 0.35,
  "actionability": 0.4,
  "evidence": 0.5,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 270,
  "why": "Доклад основателя Warp даёт концептуальную рамку 'софтверной фабрики' (петля triage-spec-implement-review-verify-ship) и пару тактических наблюдений про опенсорс и найм, но почти без конкретных технических рецептов или бенчмарков.",
  "knowledge_units": [
    {
      "claim": "Разработка ПО эволюционирует в 'фабричную' модель: идеи → триаж агентами → спека (агент пишет, человек ревьюит) → реализация агентом → ревью кода (человек+агент) → верификация агентом → ревью продукта человеком → шип → мониторинг, по кругу.",
      "type": "workflow",
      "actionable": "Используйте эту петлю как шаблон для организации своего agentic-пайплайна: явно определите, на каких именно шагах обязательно нужен человек, а остальное отдайте агентам."
    },
    {
      "claim": "Когда стоимость написания кода резко падает, клонировать софт становится тривиально, поэтому просто 'хорошего продукта' для защиты бизнеса недостаточно — нужны моаты вне продукта: дистрибуция, бренд, данные, капитал.",
      "type": "principle",
      "actionable": "При оценке защищённости стартапа в эпоху агентов явно проверяйте наличие непродуктовых моатов, а не полагайтесь на сложность копирования кода."
    },
    {
      "claim": "Warp построил публичный дашборд (build.warp.dev), показывающий в реальном времени, какие issue в каком статусе, какие агенты и контрибьюторы над ними работают — это часть мотивации опенсорса и способ выстроить 'публичную фабрику'.",
      "type": "tactic",
      "actionable": "Если хотите нарастить внешних контрибьюторов в опенсорс-проекте, стройте публичную витрину статуса issue/агентской работы, а не просто открывайте репозиторий."
    },
    {
      "claim": "При найме в эпоху, когда агенты пишут всё больше кода, ценятся не столько навыки ручного кодинга, сколько понимание архитектуры систем, умение читать и ревьюить спеки/код, написанные агентами, и продуктовое мышление.",
      "type": "principle",
      "actionable": "В найме и развитии инженеров смещайте оценку с 'умеет писать код руками' на 'умеет понимать архитектуру, ревьюить агентские спеки и решать продуктовые проблемы'."
    }
  ]
}
```
