---
session: s_a37a8be5
date: 2026-09-20
words: 1730
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a37a8be5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Signal Layer: What to Build When Anything Can Be Built — Lena Hall, Akamai
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> How is the conference for all of you so far? Great. Awesome. Um well, I think this was the best most productive year for so many of us. I'm Lena. A few days ago, I solved a production incident on a trail near a waterfall. My friend ran 18 agents while riding his bike. We're literally drowning in abundance. We have more output, more speed, more leverage than any of us have ever had. So, why do we have this feeling like the ground underneath is moving too fast? One of the engineers that I met at this conference said yesterday that it feels like the opportunity cost for not working 9:00 a.m. to 9:00 p.m. 6 days a week is too high right now. So, we're all token maxing. We're all working all the time. But the same abundance that made you fast, it also made everyone else fast. So, now everyone can build everything. Your competitor can build your feature this afternoon, too. So, the cost of the average just went to zero and so did its value. A year ago, the superpower, as we were told, was to be good at using AI. But models got so good and they got so easy and everybody now is a lot more skilled at using AI and everybody's pointing AI at the same goals. Cuz AI gives everyone the same answer because everybody is asking the same question. It It on data and data is a record of what has already happened. So, when you point AI at tasks like, "Tell me what users want. Make more money. What should we build? Make this viral." It answers from the common knowledge. Very competent, very confident, but also very identical to what it tells your competitor. To see something that data doesn't show yet, we need to have a vision, a point of view, a read on where it's going, and then use all that automation to execute it. AI is a really smart convergence machine. So, if you leave it alone, it makes everything the same. There is one decision, though, that AI can't and shouldn't make for you. It is to decide what to point at. So, the job, the new job for everyone of us is deciding what it makes, being the reason the right people choose your version over the identical-looking rest. But also, I'm sure many of you uh walked around the Expo Hall at this conference, and there are so many amazing products, so many tools and vendors. They're all solving important problems. But what Why do they all sound the same? So, when anyone can build anything, what makes me different? What makes you different? Why should anyone pick your version, your product? Um I call this work uh signal layer. And there are two There's two halves to solving it, to getting this right. So, that's how we will walk through it. The first half is knowing your signal, being able to define it very clearly. What you're building and why it's yours and not the average. So, that's the build side, the code, the product, the road map. And the second half is emitting that signal without distortion. So, making sure that your customers um making sure what your customers come to believe about you actually matches what you believe and what you've built. That's the ship side the content and go to market engineering. And I've had an unusual vantage point in this. I've built products as an engineer. I created my own as a founder. I brought other people's products to market. So three very different jobs with one identical challenge. The signal doesn't always survive. So let's start with the build side. So what do we even work on? Everything is implementable. Two years ago the best autonomous coding agents you know solved on the fraction of the tasks on the standard software benchmark and now the best agents are in the high eighties. So we nearly tripled the amount of writing and shipping barely moved a third. The benchmark was measuring the part of software engineering that has a greater and shipping is where all the ungraded parts come back in. So here is the rule underneath it. Anything that you can measure you can train against as Sarah Guo puts it. A compiler is a free grader. A test suite is a free grader. And the instant a task can grade itself you can grind a model against you know that grade until it wins. Automation of code was first because it's the most checkable thing that we have. So implementation is converging for free for everyone at the same time and the most buildable thing and the most valuable thing are almost never the same thing. So the model will build whatever you point it at but it will tell you nothing about where to point. Anything visible is replicatable. So now, some people when they hear everything is implementable, they panic. Um but we can flip the question. The pointing is actually the job. It has always been the job. We just had so much implementation work in the way um that we never had to get good at it. So, how do you decide where to point that? Paul Graham shared some wisdom on this. Where you find something that people genuinely want is by feeling the need yourself. Build something you and your friends need because the market hasn't formed yet, surveys can't see it, and your own need is the only signal that isn't a crap signal. And the best ideas may sound genuinely lame at first, like a guy uh strapped with a with a camera on his head live streaming his his life. That sounds really ridiculous, but it became Twitch. Um and the convergence machine doesn't really, you know, propose proactively these uh weird, specific, genuinely embarrassing ideas. But even with the Twitch example, it worked, but there were a thousand other similar startups I start startup ideas that didn't. So, the weird specific signal is necessary, but it is not sufficient. It's also really tempting to say that we just need to have good judgment and good taste and call it safe. But taste is really just preference under feedback, and preference under feedback is exactly what these systems can learn. Anything you can demonstrate enough times uh with a better or worse signal attached, the machine can eventually imitate. So, broad good taste is not really 
...[middle elided]...
ion that you were about to broadcast. And it's a very lightweight signal layer, and a lot of it is buildable, So, you can automate more of the checking and the catching and the surveying than most people realize. So, step back and ask what all of this, the building, the shipping, the undistorted signal, is actually for. It's for one thing of getting a human or increasingly an agent to choose you and rely on you when they have an infinite identical-looking alternatives. So, that's trust. Trust is the one thing that's left with no greater. There's no benchmark for it, no reward signal. It can't be entirely automated because it's granted slowly through relationship with consent. For example, doctors who open one particular tool every morning, they didn't have that habit trained into them. And what happens if we get this wrong? Getting your signal wrong is actually not neutral. It's negative. Producing averageness is not free. You actually pay for it in tokens, in infra, in the salaried hours of good people, you know, with with customers that take a look at your product once, decide once, and never come back. So, every generic post teaches them that your name isn't worth the click. So, you spend real money to make yourself harder to choose. So, back to the main question. We got faster, but the speed is not where the value went. Uh the value moved up to deciding what is worth building, what is worth saying, what deserves trust. And where does the thing that you actually um that that you meant survives the trip to the people that it was for. So, you don't need to be first. You need a real problem and enough conviction to carry the signal clearly through to, you know, right people to find it. So, when you can build anything, you should build trust. Have the strongest conviction, define the signal yourself, protect it from distortion, and use AI aggressively for everything else. Thank you. Let's connect and happy to chat with you afterwards. Thank you. >> [applause] [music]

---

**Claude:**

{"is_ad": false, "is_news_rehash": false, "topic": "product-positioning-ai-era", "signal": 0.25, "novelty": 0.2, "actionability": 0.15, "evidence": 0.15, "durability": 0.5, "volatility": "medium", "half_life_days": 300, "why": "Это мотивационный keynote про 'сигнальный слой' и позиционирование продукта в эпоху лёгкой генерации кода — метафоры и лозунги вместо конкретных техник или воспроизводимых практик для инженера.", "knowledge_units": []}
