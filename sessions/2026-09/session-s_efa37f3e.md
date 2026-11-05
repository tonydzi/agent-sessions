---
session: s_efa37f3e
date: 2026-09-25
words: 1963
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_efa37f3e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Which AI startups actually land enterprise contracts? — [ИМЯ] [ИМЯ], Millennium
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Welcome everybody. Sorry for everybody who was already here and missed [СКРЫТО]. I have no idea where he went or why he didn't come. I was actually pretty excited to hear about his his comments. But today I'm going to talk about which AI startups actually win enterprise contracts. So to begin I thought this was going to be a different audience. I didn't realize this was going to be mostly people on the leadership track. I thought I was going to be speaking to more AI engineers. So maybe just by show of hands, how many of you represent like the engineering or startup or like seller side? And then how many of you represent maybe like the buyer side? Like you're in the enterprise, you're trying to get these tools in. Okay, so we got a good mix. I'm going to try to balance that out today. [СКРЫТО]. We build a lot of stuff. I can't talk about any of it. So I'm going to talk about stuff that we we look at and evaluate. It's going to be pretty generic. I tried to make it as interesting as possible while still getting my compliance department to be okay with me doing this. But also need to say legally that I'm speaking as an individual. I am not representing my company and all opinions are my own. So with that we can dive in. So I ran through this with my parents last week. I don't I grew up not that far from here. And my mom basically said, "Why are you spending your time teaching vendors how to sell to you? Aren't you busy enough already?" And the real answer to that question is I really like how stuff works. I like seeing stuff come together. [СКРЫТО]. And I really love seeing things just work well. So AI's been really interesting because it's kind of a whole new paradigm of how businesses are doing work. That's the whole point of this track, this AI native enterprise track. And so even though I don't need more people DMing me on LinkedIn, um I'm actually really excited to talk about this. So, my hypothesis in short is basically at current model intelligence, most of the value available is already being left on the table. Um this is not a hot take for most people, I think who work in enterprise. You've probably seen this problem. This little stat at the bottom is uh pretty heavily uh repeated for a lot of people who work inside of business circles, and they all kind of like laugh, and they're like, "Yeah, yeah, you know, all these AI tools, how much are they actually doing?" Um and I want to talk about why. So, there's kind of two sides to this becoming gen AI native. Um you have models and products, which are one side, that's the seller side, and then you also have systems and all of what's inside of the enterprise, that's the buyer side. So, that's the side that I deal with a lot. Um so, we're going to talk first about the seller side, and then we're going to talk about the buyer side. So, per pain point, uh a lot of my job is kind of go around the company and figure out like what are the pain points? Uh what are we trying to solve for? Uh can we buy it? Can we build it? So, let's say for a given pain point, maybe I identify 10 to 15 startups that look really interesting. Like, "Huh, maybe these guys can solve our problem for us, we don't have to build it." Um of those, after doing a little bit of due diligence on my own, I might schedule two to three demo calls. Of those, we probably will land zero or one pilots. And of those, probably one in four of those longer term will actually end up with a contract. So, what does this mean? This means about 5% of all of our demo calls actually end up in a signed contract. Um and this tracks with the industry. I had no idea that this was actually a benchmark, um but it turns out that there's quite a bit out there that indicates that this is really similar across the board. So, I want to talk about what enterprise ready actually means from the inside, uh because we have a lot of startups that tell me what enterprise ready means, and And we go through all of our requirements, and then we have a very different idea of what enterprise ready actually means. Um so we're going to talk about what breaks down and why. So 40% of this is efficacy, so just value, uh commercial issues. Then there's a lot that dies in security. There's other things that die in reliability, and then there's some stuff that dies in legal. So we're going to start with the requirements that we put forward and then some of the things that we've seen go wrong across various AI companies that we work with. So our requirements for efficacy, maybe unsurprisingly, the product actually needs to solve the problem. Um that seems pretty clear, but that's not always super clear. Uh the next one is pricing models that need to reflect real value. Clear demonstration of integrations on day one, not a hypothetical. And we define the success criteria, not the vendor. So things we've seen go wrong, uh vaporware in short. Um we've had a lot of startups who come in, they pitch us an idea, uh and it's something that our platform team can rebuild in about 6 weeks. So this is not a knock, uh this is actually just what's going on in the industry everywhere, um on all sides of the equation. Um sometimes it's actually better for us to build, and sometimes it is still better for us to buy even if we could rebuild. Upside down pricing, so this one's crazy. Um We had a startup just recently tell us, "Hey, um we know that all of the LLM traffic that we're using for our wrapper is passing through your LLM gateway, but we want you to report your gateway telemetry to us so that we can then price a huge margin on top of that, even though none of it's running through our infrastructure." Um that did not work. Another one is promises in demo calls, but no ETAs after 2 months. Um this is pretty common. Um not a lot to say here. Um and then repitching features we've already declined. So if you're a salesperson, um my best a
...[middle elided]...
just decide, "Hey, maybe we need a separate ecosystem to do a lot of this work, figure out what does work and what doesn't and then kind of go from there." Um and that's something that we thought about as well. So, to just put a finer point on the agents and the entitlement thing, uh agents inherit your foundations. So, I strongly recommend that everybody fix their entitlements if they are not working really well now um because this is something that if you think about the problems that you run into when things go rogue, processes go rogue, people go rogue, agents are going to like 100X that problem. Um so, this is really something that's worth figuring out now. So, to kind of recap uh as I wrap up here, the recipe, if you are one of the people in the first half who are raising your hand on like, "What do I need to do if I'm a startup and I want to work with a really difficult large customer? Millennium's got like 8,000 people. We have very, very tight security, compliance, regulatory requirements. Um this is the stuff that we care about. And we want to see more startups doing work that allows us to work with them. Um I really view this as like one of the highest bars. We're probably not the highest, um although we're probably pretty close. Um and I think if you can architect your startup to work with companies like this with this kind of architecture, um you're probably going to be able to satisfy basically everybody else. Um on the other side for anybody who's buying, uh these are the things that I think again that kind of that boring 60% that really deserves a lot of work. Um off entitlements, governance, audit logging, etc. Um these are the things that I think we need to have in terms of systems to get it working on the other side of the equation. So, that's it. Um my only motivation here is to getting stuff working better and having better enterprise grade AI. Uh that's a QR code to my LinkedIn and I appreciate all of your time. Thank you. >> [applause] [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "enterprise-ai-procurement",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.35,
  "evidence": 0.55,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это выступление байер-сайда (Millennium) про то, как enterprise закупает AI-стартапы — полезно для GTM/фаундеров, но для AI-инженера, строящего системы, даёт лишь пару переносимых заметок про агентов и безопасность, а не техническое know-how.",
  "knowledge_units": [
    {
      "claim": "Агенты наследуют существующие права доступа и умножают последствия плохо настроенных entitlements/IAM — то, что раньше было мелкой дырой в правах, с агентами превращается в системный риск.",
      "type": "tool-caveat",
      "actionable": "Перед деплоем автономных агентов в enterprise-окружение сначала провести аудит и почистить IAM/entitlements, а не откладывать это на потом."
    },
    {
      "claim": "Enterprise-покупатели отклоняют вендоров, которые показывают на демо гипотетические интеграции вместо реально работающих на день подписания контракта.",
      "type": "tactic",
      "actionable": "Продавая AI-инструмент в крупную компанию, на демо показывать только реально готовые интеграции, а roadmap-обещания явно помечать как будущее, не выдавая за готовое."
    },
    {
      "claim": "По опыту крупного покупателя (hedge fund) из 10-15 кандидатов-стартапов до подписанного контракта доходит около 5% (2-3 демо → 0-1 пилот → 1 из 4 пилотов становится контрактом), и это совпадает с индустриальным бенчмарком.",
      "type": "benchmark",
      "actionable": "AI-стартапу, планирующему продажи в enterprise, закладывать в воронку конверсию ~5% от первого демо до контракта и не считать единичный отказ аномалией."
    }
  ]
}
```
