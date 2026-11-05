---
session: s_58e8dd29
date: 2026-09-24
words: 1928
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_58e8dd29` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: You’re Not Thinking Big Enough: Rebuilding Food Systems with AI Agents — Cody Menefee, Firecrawl
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] All right. Hello everybody. Uh my name is Cody. Um I put this picture up here because this jacket so far has not actually landed as well as I thought it would. No one gets the joke. Um so this was to really put it in front of your face. I don't just enjoy wearing heavily branded Letterman jackets. We intentionally tried to play into the bit a little bit. Um, so my name is Cody. Uh, I'm on the growth team at Firecrawl. Um, and today I'm here to tell you you're not thinking big enough. Um, but before I actually can get into that, I have to address a bit of an elephant in the room, which is Theo stole my talk. Uh, Theo put out a video about a month ago uh called uh, you need to think bigger. But I would like to say I submitted the name for this talk a month before Theo put his video out. I didn't steal his talk. He stole my talk. So, um, today we're actually going to talk about farming. And yes, I actually mean farming. Uh, more specifically, I mean livestock farming. And even more specifically, I mean automating pasture rotation for grass-fed livestock systems. Um, I have a feeling most of you did not expect to learn about cows and grass and farming today, but I'm here. So, you're going to uh little bit of background on who I am and why maybe you should listen to me. Uh the short version is I actually have no credentials that qualify me for this talk, but nonetheless, I'm going to do my best to give it. Uh I grew up in Kentucky. Uh have a background in blue collar work. I was a bartender, a mechanic, a uh um server, uh a whole bunch of things. Uh never actually a farmer though. Um and then I sort of found my way into engineering, uh software development, etc. I actually don't really like taking the title of software engineer. Um, I'm pretty adverse to that. Feels like stolen valor because I am the vibe coder most of you all are scared of. Um, I use AI agents all day long. I don't have any syntax memorized. I am not proficient in any particular coding language, but I will crank out some stuff on a weekend. Um, but today I actually work at Firecrawl where we're building context for AI agents. Uh, we have a series of uh web data APIs. So, you give your agents access to the web. Again, I said I'm on the growth team. Um, but today we're actually to get into some more farming stuff. Uh, but first, a bit of credential I do have is this is a real picture of me hauling turkeys on top of my Tesla and I do still have a crack in that glass ceiling because of it. Um, this was in Nashville where I live in the middle of a residential neighborhood where you are not allowed to raise turkeys. Um, but I raised 10 turkeys in my backyard because I wanted to know what it was like to actually uh raise livestock myself that I would eat. Um, it's a very mentally uh difficult process if totally honest. Um, but this was me loading them up onto the roof of my Tesla and then I drove for three hours with them to the processor. Had to stop at a supercharger on the way. Um, and lots of people were taking pictures and what I can tell you is is your range is sufficiently decreased when you have a giant windbreak full of turkeys on top of the roof. Uh, so that was uh quite the anxious drive, I can tell you. Um, I also almost left uh engineering to be a farmer. I really wanted to raise chickens. This is a real product image that I came up with. I wanted to wrap turkeys in white wrapping and literally just slap the word eat me on top of it. I thought it was provocative. I thought I would get you to buy chickens. Um, but I realized it's actually really hard to make any money farming. Um, surprise surprise. Um, and I have a wife. I have two kids. it didn't feel uh right to ask them to give up the lives they had so that I could go cosplay as a farmer and raise chickens. So I decided to pivot and see if there were ways that we could scale farming itself and the the types of systems that I'm interested in when it comes to livestock agriculture. So three things I want to get accomplish in this talk is one convince you all to pursue bigger ideas. Um I think a lot of these talks, a lot of these conferences, a lot of us individually uh uh spend a lot of time talking about building software for people who build software for people who build software so on and so forth. And I really am just here to challenge you that there are other problems to solve than just another MCP for another SAS solution at another company. Um but also I'm just really trying to take advantage of a captive audience. Uh if you corner me anywhere at any time, there's a good chance I will talk to you about farming. Um so here I am. Uh, and hopefully I can convince you to come work at Firecrawl. So, uh, first things first, I believe livestock belongs on pasture. I think animals should live on grass. Um, I think it's better for the animal, the consumer, the farmer, the ecosystem. I can give you a whole TED talk on each of those if I need to. You can find me later if you need me to tell you why it's better for animals to be on grass, but I don't have enough time to get into all of that. Take my word for it. Let's start there. The assumption is animals should be on grass. Um, this is the goal I want to hit. I am not actually anti-containment farming. I think there's a reason we needed to do that. But 97% of cows are still currently pro uh finished on feed lots. 3% are raised on pasture. My opinion here, more animals could be on grass. I want to try to figure out how we get more animals on grass. The question is why aren't they on grass? And that is labor is the bottleneck. It is a pain in the ass to actually raise animals on grass. Uh pasture done right actually means moving animals constantly and that takes a lot of work. Um if you think about grass-fed uh beef, you might think of I have 100 cows, 100 acres, I put 100 cows on 100 acres, they eat grass, I got beef at the end of the year. That's not quite how it works. Um you will uh very rapidly decrease the qu
...[middle elided]...
ers talk about how we turn LLMs into deterministic processes and my contention is actually there's a lot of problems that you can't solve with deterministic uh algorithms. Um this is one of them. It's a multivaried analysis. There isn't a next best paddic to move to. There's just your best guess on where you think they should go. Um, and I think if we can take systems like that, these uh multi-data input systems, and drop an LLM in the center to actually reason over the data and at least make a suggestion that the human can confirm or deny, um, we can really start to scale systems like this that are very much, uh, restricted by the farmer's ability to scale their own labor, their own decision-making power, um, and really give them the tools that they need to grow their operations to hopefully, I think, uh, all animals could be raised on grass if we, uh, solve these problems. And then the last one is is maybe you can come help me solve some of these problems. Um the number one problem is actually just giving the agents the context they need. Gathering the data, packaging that data, and then presenting it in a way that the LLM can reason over. And that's what we do over at Firecrawl. Uh so you're not thinking big enough. Firecrawl is where we're building the context layer for AI. And I hope you can come build it with us. Uh we're hiring. Uh so here's all the job postings we currently have. go to our website, maybe find one that works out for you. Uh, reach out to me. We'd love to have more people trying to figure out how we get data off the web to solve some more of these complex problems and present that that data as context uh to these AI agents. And perhaps we could make the world a better place. My name's Cody. Uh, Open Pasture is my open source project. Firecrawl is where I do my day-to-day life. And, uh, these are my socials. I'll hang out for a little bit. I'd love to chat more about animals, cows, birds, all the like. Thank you very much for coming. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-decision-support",
  "signal": 0.15,
  "novelty": 0.15,
  "actionability": 0.1,
  "evidence": 0.1,
  "durability": 0.35,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это в основном личная история про фермерство и найм в Firecrawl, а не разбор техники — единственная передаваемая мысль (LLM как советчик в недетерминированных задачах с человеком-подтверждающим) звучит буквально одной фразой без деталей реализации.",
  "knowledge_units": [
    {
      "claim": "Когда задача не сводится к детерминированному алгоритму (нет единственного 'правильного' следующего шага, а есть многофакторная оценка), можно поставить LLM в центр как советчика, который предлагает решение, а человек подтверждает или отклоняет его.",
      "type": "principle",
      "actionable": "Для задач с многомерным контекстом без чёткой формулы — не пытаться закодировать эвристику вручную, а собрать контекст и дать LLM выдавать рекомендацию с человеком в контуре подтверждения."
    }
  ]
}
```
