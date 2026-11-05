---
session: s_b07f5b1b
date: 2026-09-27
words: 1990
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b07f5b1b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Knowledge Systems: The New GTM Stack — Roux Wang, Exa
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hey everybody, I'm Jeff. I guess I was introduced, but I'm the co-founder of Exa, and today going to give a talk on turning go-to-market into an AI engineering problem in the spirit of this AI engineering fair. And just a quick show of hands just to like understand the audience, like raise your hand if you're a technical. Okay, great. Okay, so I kind of oriented this talk around like go-to-market as presented to to engineers. So, happy that I did that. Cool. So, first just to like ground the ground like what what Exa is cuz it's sort of relevant inside of this presentation. Exa is a Exa is a search engine for agents. Think like agents are really smart, but they don't have access to the web. We're like this web MCP web tool that agents can access. We power Cursor, we power Cognition, we power a lot of the AI ecosystem at this point. And before we start, I also just want to like talk about, you know, especially to the technical audience, like why should you even care? Like why should you care about go-to-market? I guess this audience cares about go-to-market cuz you chose to go to this go-to-market talk, but I think there's this like funny narrative right now, which is like people are like, "Oh, like product is the only thing that matters." Or "Distribution is the only thing that matters." And there's all sort of like all sorts of like Twitter flame wars like like oh, is Glean going to succeed because they're really good at distribution, but they're like what what the heck is their product? And then and other people are like, "Oh, the like the the product needs to be super good cuz agents you know, agents shop for the product, so they'll shop the for the best product." And so, my view and my experience in the last few years is that you just kind of have to do both. Like I think you have to get product right and you have to get go-to-market right. Like you got to build this thing, it's got to be good, and then you got to get it into people's hands. If you don't do both things, then you don't have a company. So, that's kind of my view on the matter. And I I say like a really funny thing also is like as a technical person when you start a company or you start some some sort of project, like very much so the bias is like, "Hey, I'm going to just build the thing. I'm going to make it really really freaking good, right?" Like that's kind of like the bias you have as like an engineer. That's the bias we had when we started X.ai and we were like honestly pretty bad at go-to-market. Like we >> [laughter] >> we were not doing enough marketing, we were not doing enough sales. Um but I think the cool thing about about um go-to-market particularly in 2026 is you can treat go-to-market like an engineering problem and particularly an AI engineering problem. And so I think that's like a super exciting thing. Like it's like more fun for engineers than ever to do go-to-market cuz you can automate things. You can you can do so much as one person and uh etc. Also um I want to make this interactive. If if anybody has questions at any point, please please ask cuz I'm aware there's a lot of talks and I don't want to bore you. Cool. So um cool. So so the hypothesis I have is if you're an engineer or or if you're anyone, you can treat go-to-market like an engineering problem. So first, I guess like what does what do go-to-market teams do? So I have like a laundry list of things here of things that go-to-market teams do, but here are a few. Like one is you got to research like your customer, right? You got to research your targets. You have to find out information about your about targets. You have to find the right people at particular companies. You have to build POCs. Um there's like a just a ton of stuff you have to do, right? Um so you know, I'm not going to I'm not going to list everything here, but like what is the grand unifying theme? Well, go-to-market is a data problem, right? So you have all you have this like entire world of uh of of what your product does and then and this entire world of like all your potential customers and you're just going to like learn and figure out what your world looks like. And so this is my this is my uh proposal. It's a data problem and we have to solve from a data perspective. Cool. So okay, so what is data that is relevant? Uh I propose that you need basically a live model of your world that agents can act on. And so, what does that mean? Okay, well, one is you have a ton of internal data, right? There's all this information that you know about your customers, about people that are at your company, uh data about how people use the product. That's like internal data that you know. And then there's all sorts of external data, right? Like there's over 60 million companies in the world, and there's like billions of people, like over a billion that are on LinkedIn, for example, and all sorts of stuff are is is like happening every day, right? Like there's all this news. And so, when you're building like this data go-to-market system, um it's important to keep in mind just like all the different sources that exist and and and uh and are available to your agents. And cool. So, I'm going to like go through, hopefully pretty fast, just all the different components of what we've built at Exa. And just for like context, uh I've been really passionate about this for a long time. So, like Exa was launched in uh the middle of 2023, and so we were post-GPT-4. And GPT-4 was really incredible, cuz it could actually, even then, even though it's way worse than like Fable or whatever, like it could actually just automate entire parts of go-to-market. And so, from the beginning, I've been thinking about our go-to-market from from a very, very uh AI agent-first perspective. And so, we're going to go over two interfaces that we have that help us, and then two agents. Cool. Cool. Okay, the first is what we call our ICP dashboard. And the ICP dashboard is a product that we have interna
...[middle elided]...
ention to guardrails. So for example um in the case of Jeffbot um when I use Jeffbot and I call Jeffbot has access to a ton of systems and it can for example do reads and writes. However, when anybody else calls Jeffbot all can do is draft messages and also I don't give Jeffbot permissions to all of our MCPs and tools in the case where other people call it. And so in short it's like pretty it's pretty well defined or we we we do pay some care to the security. Yeah. >> Okay, last question. >> Um, can you can you share the origin story of the FDE team? Did that just happen organically or did you intentionally do it? I'm just really curious like how that came to exist. >> Yeah, for sure. I mean, uh my my philos- my my hypothesis on this is like, once upon a time the FDE role didn't really exist. Like, Palantir started calling some people FDEs, but it that was really it. And what tech companies had was like solutions and sales engineers. And then, like account executives. >> I was a solutions engineer. >> Got it. Yeah, yeah. The thing The thing that I think has changed is that um because of AI, as like en- as a technical person that is supporting revenue generation, you can actually not only support the revenue generation, but then very easily build the tooling to smooth everything over. And make your own life easier, make the lives of AEs easier. Like, because of AI, this is just possible now. Like, that's like two Before that was like two jobs, and now it's like one job. Um in theory. Like, now when our team grows, like right now it's about eight or nine FDEs, like what will will it scale such that everyone does everything? Probably not. But, at least right now that's what we have, and I think that's a really good working model to get pretty far. >> Eight out of how many? >> Uh eight Oh, eight of like how big is our go-to-market org? >> Or eight You have eight FDEs, and the size of the company right now is how many? >> Oh, the We're about 115 people. >> Okay. >> Yeah.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "ai-agents-for-gtm",
  "signal": 0.45,
  "novelty": 0.35,
  "actionability": 0.4,
  "evidence": 0.4,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Ко-фаундер Exa делится своей методологией превращения go-to-market в инженерную задачу через агентов и данные, но конкретики (промптов, кода, архитектуры) почти нет — в основном высокоуровневые принципы и один живой пример с ограничением прав бота.",
  "knowledge_units": [
    {
      "claim": "Go-to-market можно рассматривать как задачу с данными: нужна 'живая модель мира', объединяющая внутренние данные (использование продукта, история клиентов) и внешние (компании, люди, новости), на которую могут опираться агенты.",
      "type": "principle",
      "actionable": "При построении GTM-автоматизации сначала спроектировать единый слой данных (внутренних + внешних источников), а не отдельные точечные скрипты под каждую задачу."
    },
    {
      "claim": "Внутреннего AI-бота компании (Jeffbot) ограничивают правами в зависимости от того, кто его вызывает: у автора — полный доступ на чтение/запись ко всем системам, у остальных сотрудников — только черновики сообщений и урезанный набор MCP-инструментов.",
      "type": "tool-caveat",
      "actionable": "При выдаче внутреннего AI-агента команде разграничивать права по идентичности вызывающего, а не давать всем одинаковый полный доступ к MCP/системам."
    },
    {
      "claim": "Роль Forward Deployed Engineer (FDE) возникла как слияние двух прежних ролей (solutions engineer + разработчик внутренних инструментов), потому что ИИ позволяет одному техническому специалисту одновременно поддерживать продажи и сразу же автоматизировать/строить тулинг под этот процесс.",
      "type": "workflow",
      "actionable": "При масштабировании GTM/support-инженерии рассмотреть модель FDE — не разделять поддержку продаж и разработку внутренних инструментов на разных людей, а дать одному инженеру оба мандата с опорой на AI."
    }
  ]
}
```
