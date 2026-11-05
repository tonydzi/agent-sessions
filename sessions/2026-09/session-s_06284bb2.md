---
session: s_06284bb2
date: 2026-09-29
words: 1805
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_06284bb2` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: So much for "Pacing" the Frontier
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Remember a week or two ago when everybody started talking about pacing the frontier, trying to get the Frontier Labs to slow down their constant iteration? This article from Daario that talked about how important it is for us to do this that resulted in super important folks like Sam Alman, Elon Musk, and I all agreeing. Yes, that is a joke reference to people freaking out over a silly tweet. I'm strong enough to admit that the memes around my framing of the video, specifically the title I used when I posted it on Twitter, are funny. This one is an instant classic. I do think it's important for us to talk about what pacing actually means because as I'm sure you all have noticed the pacing is going great. We have seen almost no models drop from the major labs since all of this happened. All we've seen is Gro 47 from XAI, Opus 55 from Anthropic, and then GPT6 Soul and Luna from OpenAI. Wait, that's four models. I thought we were pacing. What the hell is going on? I think it's important for us to talk about this because as great as this article is, not a lot of people read it. And even of the ones who did, not all of them seemed to understand the point of pacing the frontier. And here's where the hot take comes in. What we are experiencing right now with all these new model drops, that is pacing. We are pacing better than ever. And I think we're actually in a really good spot already. I'm going to be real. I've put far too much time and thought into what pacing even means now. and working with friends at all the different labs and people into research and AI stuff in general to try and figure out what pacing looks like for us to not potentially doom ourselves. And I'm pretty sure I understand now. And as crazy as this might sound, I think a well-paced cadence for these labs is actually going to result in more models that are cheaper than you ever would have guessed. Before I can explain why, we should pace ourselves a bit and take a quick break for today's sponsor. As great as models like Fable and Astra are, there are still a bunch of things they get wrong. Two of those things that really really frustrate me are off flows and payments. And this is why I like today's sponsor, Clerk, so so much. These guys figured out the best way to set up developers and agents for success in implementing the flows that make your app actually useful. Those being the ability to sign in and manage your account and the ability to pay for things. Trust me on this one cuz I'm experienced. I made a repo last year complaining about just how bad Stripe is to set up correctly and safely in a way where you won't get scammed. and it got over 6,000 stars and is still the number one result on Google when you Google search Stripe recommendations or recommended way to set up Stripe. I put all that effort in because it was so hard to do right and if I put out a recommendation today, it would be to just use Clerk instead because not only have they made it trivial to set up authentication for your users and their companies and organizations, they also have the best billing product I've ever seen baked right in. The code couldn't be simpler. Not that you're going to read it anyways, but simple code means the agents can understand it too. in the clerk skill, which they provide with a one-click copy to paste into whatever agent you want to use, will set the agents up for success. Not that they even need it. I've had pretty good luck just telling my agents, "Go set up clerk on whatever project." And whether it's web, mobile, desktop, anything else, they get it figured out. That's why we're using it in T3 Code for all of our different platforms. They even built an Electron package for us and have been keeping it up to date as all of our requirements change. The only thing better than Clerk's Code is the team, and they've been awesome to work with every step along the way. Figure out why I like them so much. at soy.link/clerk. In order for us to have a good conversation about pacing and how things are changing, we need to understand what we're trying to prevent first. So, we need to start with the core question. Why are we pacing? Why are we choosing to do this? There's a vague general idea of the models get too smart and they can destroy everything. But that's not really the issue. The problem isn't that if we hit a certain score on some benchmark, the model might go rogue and kill us all. The problem isn't about a specific point we hit. The thing we're really scared about here is the idea of the takeoff. Not that a certain level of intelligence is hit, but at a certain level of intelligence and recursive self-improvement, the model starts improving so fast that we can't understand what it's doing or why. The scary stuff starts when the models improve in ways that we can't understand. And if we have more and more AI agents improving the models and they start to be able to do it better than humans at an exponential rate, we'll lose track of why and how and more importantly what they're even doing in the first place. There are some pretty silly but also painfully real examples of this. The first I'm going to cite is all the work OpenAI has been doing to make the models more efficient. Flashbang warning before I go over to artificial analysis. Thing I've talked about a lot on this channel is how much more efficient OpenAI's models are. Most of the difference comes from the reasoning tokens, the tokens that are generated to steer the model in the right direction. I've shown examples in my other videos, but here's a pretty silly one. The reasoning traces that the OpenAI models do aren't speaking proper well- formatted English. In order to make the model use less tokens, they trained it to speak in grug style where it's like not including words that aren't important even if they make it more grammatically correct. need final since we asked and must wait but final the answer should just be ask we already in commentary final maybe not JS
...[middle elided]...
 didn't decide to pace, the likelihood that Anthropic would have put so much time, effort, and marketing spend into Opus 55, it just it wouldn't have happened. Just just think about this. Like, as a user of Twitter or YouTube or whatever else, when's the last time anyone got hyped about a new model from Anthropic that wasn't their frontier level models? Nobody gave a [ __ ] about Sonnet at all other than Ben Davis. Poor kid. Nobody got excited about Opus 5. Hell, people barely cared about Opus 48. The reason is because Anthropic didn't care. They don't even care enough about Haiku to release it. Like, Haiku has not had an update for 11 months. We're near a year since Haiku 45. Anthropic didn't care at all about models that were less capable than Astra. So, what they're doing now instead is putting a lot of effort and money and time and energy and marketing force and everything else into making Opus get as close as possible to Fable. And I think that's awesome. To everyone who's been upset about models getting too expensive and hard to use and justify because the price is just insane, I hope y'all are really in favor of pacing because pacing gets us what we want. Better models that are less stupid at cheaper prices. Not smarter models that can invent bioweapons. Cheaper models that can contribute to our code bases without deleting things from our computer accidentally. And I personally think that's awesome. And I hope this rant has helped convince you as well. We're living in a renaissance of less dumb models. Not smarter, less dumb. And I personally really, really like that. I hope you do, too. And at the very least, this makes you a little less skeptical of what pacing means. And you can see that these labs aren't lying. They are just trying to make better things given the circumstances that we're living through today. Let me know what you all think. Am I just being a blind chill or is this a more realistic way of looking at this stuff? And until next time, he sns.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "ai-lab-pacing-hype",
  "signal": 0.15,
  "novelty": 0.15,
  "actionability": 0.05,
  "evidence": 0.2,
  "durability": 0.1,
  "volatility": "volatile",
  "half_life_days": 45,
  "why": "Это авторский хот-тейк про 'pacing' у AI-лабораторий и разбор твиттер-мема, плюс встроенная реклама Clerk — почти нет переносимого практического знания для инженера.",
  "knowledge_units": [
    {
      "claim": "OpenAI ради экономии токенов обучает reasoning-модели выдавать 'рассуждательные' трейсы в сжатом, неграмматичном стиле ('grug style'), а не полноценным английским.",
      "type": "tool-caveat",
      "actionable": "Не полагайтесь на reasoning-трейсы OpenAI как на читаемый текст для логирования/дебага — учитывайте, что они специально урезаны и могут быть нечитаемы для человека."
    }
  ]
}
```
