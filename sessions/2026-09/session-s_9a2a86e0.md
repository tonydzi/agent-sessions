---
session: s_9a2a86e0
date: 2026-09-26
words: 1689
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-26 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9a2a86e0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Teaching LLMs to Speak Spotify — Yves Raimond & Jacqueline Wood, Spotify
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Welcome everyone. Um really glad and thank you Deven for inviting us as well to talk today. Uh so um uh Jackie and I are going to present today about making LLMs speak Spotify and how we turned our recommendation system on its head to be LLM native. Uh just a few quick words about myself. Uh I joined Spotify a year ago. Before that I was at Google working on personalization for Google search and prior to that I was uh working on personalization at Netflix. Um all right so let's dive in. Um first a couple of numbers to describe the scale of the problem that we have to solve. Um Spotify has about I was a little bit sad not to see it on the DAU by chart because it should be up there but it has about 760 million uh active uh users monthly uh in about 184 markets. But one thing that makes uh the Spotify personalization problem particularly challenging is the size of its catalog. Uh so of course you know Spotify has basically all music ever published a bit more than 100 million uh music tracks but it also has a range of videos, podcasts and audio books as well. So the matching problem uh is uh actually surprisingly uh complicated. So today what we're going to talk about Jackie and I is basically the extent of this matching problem and how we uh how we are solving it. I'm going to talk about a little bit of history, the new phase that we're entering and then Jackie is going to help us uh go into the guts of the modes as well to understand how those things are trained as well. Uh so a little bit on history. Uh initially Spotify personalization was really built around curation. So uh people basically manually assembling playlists that target specific taste. And that's still a very common uh use case on Spotify. Right now we have about 10 billion playlists with many many uh created every every hour. Uh then you know Spotify moved into taking these creation signals and order signals and moving into recommendations. So basically being able to turn these uh creation signals to something that can be applied at scale. Uh and a great example of that would be discover weekly for example that was launched in 2014 as one of the one of the early like recommendation use case on on Spotify. But the phase that we entering now which uh uh which we're going to talk about in more details is something that we call generative personalization where we are not only solving a matching problem from the user to the content. We're also solving the ability to generate an experience that is interactively and dynamically shaped around each user. And that transition from recommendations to generative personalization involves a couple of different uh a couple of different big shifts. One is move from moving moving from personalization as guessing uh where basically you have a ranking algorithms that spits out a brand ranked list of entities in your catalog to personalization as reasoning that can introspect these results and really try to understand whether that's indeed the right match for this user in this particular context. The other aspect as well is moving from blackbox algorithms. uh it's very difficult to fully introspect a multi-stage ranking system for example to transparent and steerable personalization where the user is always fully in control. So uh basically giving the ability to these mods to speak and understand English. The other thing that these these systems can do is uh uh not stopping just at recommending but also generation of experiences and explaining as well. uh and we're going to show a couple of examples of that. So one example that uh we launched a couple of years ago uh so pretty early in that journey was the Spotify DJ. Uh so the Spotify DJ is something that you can spin up that will start playing music for you of course personalized uh and but one interesting thing about it is that since last year you can tap that button on the bottom uh right and steer it in whatever direction you see fit. So at any point you can chime in and let the algorithm know what you want and it's going to steer the session in the in in that in that direction. Uh another example of what we call generative personalization is uh showcased in a prompted playlist here that Deanch showed a little bit earlier as well. Uh and here you can you basically have full unfettered access to the recommendation algorithm that Spotify has. uh and you can uh prompt it with very high level prompts or very detailed prompts. On the left hand side here, I have a prompt that tells me uh create me a playlist of bands that are playing in San Francisco tonight. Uh so turns out there's a bunch of good shows if you're excited to check them out. On the right hand side, you see a prompt that is asking for a playlist to accompany me on my run. And what's interesting with the right hand side as well is that you will see that the experience itself gets dynamically shaped as a function of the request on the user to be able to introduce itself and different phases in my run as well. Uh, another one that I'm really excited about, we launched it in New Zealand a couple of months ago and uh, it's coming soon in more markets is something called the taste profile. And that basically gives you the ability to introspect in natural language what the Spotify algorithm has understood about you in a way that you can edit and refine. Uh, so if you see something that's missing or something that's wrong. Uh so for example one of my edit is that all Disney music are my kids because we have a bunch of shared devices at home but please don't recommend that to me that's not my taste please. Uh and the algorithm would then take that into account uh making sure that we never recommend this this in the wrong context. Uh and similarly you can also use the taste profile to share some more aspiration uh goals as well. Uh so getting into a new genre, getting into a new topic, uh learning about a new language for example, all of these things can be can be done. Uh another o
...[middle elided]...
ey can't tell us whether or not the user or that recommendation makes sense for the user, whether the explanation is accurate, whether it aligns with the user's intent, etc. So, that's where LLM judges really shine. But in our work at Spotify, we really find that you need to invest in grounding your LLM judges in meaningful data. so that they can be reliable evaluators that align with human preferences. So, a few examples um for evaluating the podcast recommendations that I just mentioned, we create textual user profiles summarizing the users's listening history and that is passed to the LLM as a judge and we saw that this corresponded with a 75% alignment between the LLM judge and human preferences. Similarly, you can use actual behavioral signals to ground these LLM judges. So, for example, for a search task, you can for a given query, you can take similar queries and how the user has interacted with them in the past and pass that to the model. And we saw that overall it increased alignment by 5% but on ambiguous queries it actually increased alignment by 91%. Showcasing the value these this grounding of the LLM judge plays especially in ambiguous cases where LLM judges tend to struggle. Lastly, we used grounded LM judges to scale up our Cranfield style collections. These are evaluation sets that are constructed by taking candidates from multiple different sources, creating a pool, and then using a human to rank that pool. However, that human ranking stage is expensive. So, we invested in significant grounding for our LM as judge and are able to have an LLM judge that aligns with uh human system rankings with an agreement value of 0.87. In summary, um like we're going to hear a lot about today in all the talks, there is a new era of personalization among us. this generative personalization. And if you want to power language steerable personalized recommendations for your user, this is how we taught openweight LLMs to speak Spotify. Thank you. [applause] >> [music]

---

**Claude:**

You've hit your weekly limit · resets 4am (Europe/London)
