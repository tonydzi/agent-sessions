---
session: s_9b574305
date: 2026-09-25
words: 1772
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9b574305` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: World Models Need Causality, Not Pretty Pixels — Christopher Manning, Moonlake AI
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Okay. Hi everyone. [applause] Um, and thanks a lot for making it down to the second floor and finding my session here. Okay. So I'm Chris Manning and what I want to do today is present something about Moonlakes's approach to producing a simulation infrastructure for practical physical AI. The overall goal here is that a north star for AI and actually cognitive science as well has always been to understand and work out how to build embodied intelligence. So today I'm going to tell us about some of the recent work that we've been doing at approaching a practical form of embodied artificial general intelligence. But you know I'm not actually going to start there because uh you know um Swick said no you shouldn't just do that. Um, you should have a double slot. And first of all, since I've got you here today, I should have people tell you about the history. You should tell people about the history of AI and your journey through it and how you ended up here. Um, so, uh, sit back, um, get ready for story time and we're going to have the really slow build and we're going to hear about all about the history of AI for 20 minutes and then we're going to hear the details about what Moon Lake is doing. Um, he looks very persuasive there, doesn't he? Whereas at the time we were having this conversation, I was having a very bad hair day. So I had very little um choice um to agree to this task. Um so here I am with some long-term remarks on how did I and all of us get to this moment from the far ago days um when AI didn't work. Um so the very beginning of AI was the Dartmouth summer research project in 1956. It was for the holding of this um kind of summer group project was when um John McCarthy coined the term AI and got together um this group of people. Um so that one on the back right there, that's John McCarthy, there's Minsky and both most of them look like a real bunch of geeks as you can see. Um but the attractive one on right on the right end is you know my personal hero as more of a language guy um Claude Shannon. So this is sort of the start of AI 1956. It's where the the term AI came from. But really there's other stuff that came earlier than 1956. So really starting in the 40s and early in the 50s there was work on cybernetics. So cybernetics sought to tie together communications control and feedback in living things and computers. Um so uh you know kubernetes is really the same word as cybernetics just less anglicized um but has very different meaning. Um yeah so this led to the earliest work on neural networks and the perceptron network. So here's Frank Rosenlat's perceptron um that was you know predated the term artificial intelligence and as you can see like in those days you actually used to wire neural networks now this modern matrix multiplication but another thing that actually started before the term artificial intelligence and has been my long-term area of interest is doing things in natural language processing and natural language processing began as machine translation. And so here we are again in 1954, two years before the term artificial intelligence was coined. And here's the front page of the New York Times. Now, there's a way in which the front page of the New York Times in 1954 is surprisingly reminiscent of the issues that you see in the front page of the New York Times um in 2026 because it's exactly the same issue. President proposing ending citizenship for people. Um not much has changed in the um intervening 75 years. Um allegations of various kinds of behavior akin to treason. All sounds very familiar. Um, but this was the top half of the page. And if you went down to the bottom half of the page, um, you found this article. Russian is turned into English by a fast electronic, um, translator. A public demonstration of what's believed to be the first successful use of a machine to translate meaningful text from one language to another took place here yesterday afternoon. Um, and here's a little bit of video of showing that system. into one of the first nonmerica were made that the computer would replace most human translators. >> Okay. Um, and we'll come back to that again in a little bit. Um, but coming off of the founding of AI, um, by John McCarthy, fairly soon after that, John McCarthy moved to Stanford and founded Stanford Artificial Intelligence, the Stanford Artificial Intelligence Lab, starting from 1963. And the original Stanford AI lab was in this um, building up in the foothills. Um if you down if you know the South Bay well um if you've ever been to a restraero and you look over next to a restraero um where there's the Portola pastures um horse area or if you ride a horse um that's where this AI lab used to be and that was the site of many of the um founding um work in artificial intelligence and also a lot of other stuff. Um the Stanford AI lab was the where the very first video game tournament was played in 1972. Um now McCarthy himself um was um mathematical logician and nearly all of his work was sort of building out these not notions of mathematical logic but in his thinking he was very wide ranging and so he he liked the idea of how could we build an embodied artificial general intelligence and was very happy to sort of provide the facilities and the money for other people to start to explore this. Um so this was the Stanford AI Labs um very first robot um the Stanford cart not very fancy um the old um sale building um but more relevant to what we're going to talk about today for simulation infrastructures for AI um was another robot um Stanford SRRI shaky robot >> mach audio Um, so this was a robot that could um perceive the environment, move around, move boxes and so on in the environment and do things like that. Okay. And so this sort of started to explore this idea of having an embodied in artificial intelligence that had an understanding of a world and its environment. Um, just one little distraction that's not really about AI. Um, who he
...[middle elided]...
 the knowledge of large language models and there are a couple of companies that are now starting to look at that. >> Cool. Last question. Yeah. person over here has one for a long time. [laughter] >> Thank you. Um so if you look at um analog chips for instance right the physics is understood but as you go higher up the chemical operations then the heat and those things are still people are working on it. So that's not what you call completely um understood. Now I'll give you another example of say I'm looking at kidney related uh literature and stuff and then liver related stuff these things it gives a pretty good answer the kidney stuff it gives answer but when you look at the relations between the two people have somewhere u doctors have made a link and that's why you are able to see my take is if we operated completely in the latent space and we did not know the connection connections at a human level. Can we explore in the latent space completely and be able to find hidden connections over there that could translate into the real world or am I thinking something crazy? >> Yeah, I mean absolutely. I mean to the extent that we have a pretty good simulation, we can hope to find surprising discoveries that turn out to be correct in the simulated world. I mean, you know, things go both ways, right? There are also likely to be things that turn out to be true in the real world that weren't in our simulation, right? There's this famous statement about all models are wrong, but some models are useful, right? And that so anybody's world model, regardless of whether it's the one we're building or the world model in a human head, right, they're not always right. Sometimes we think a person's going to react in one way and they react in another way. But nevertheless, a lot of the time it can let us explore much more widely and discover new facts and new connections that we weren't aware of in the real world. Okay, >> awesome. That's a wrap everyone. Thank you so much, Chris.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "world-models",
  "signal": 0.15,
  "novelty": 0.15,
  "actionability": 0.05,
  "evidence": 0.15,
  "durability": 0.3,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Основная часть сэмпла — историческая лекция про Дартмут, McCarthy и Shakey robot, а не разбор технической архитектуры Moonlake AI; в конце есть общая философская дискуссия про латентное пространство без конкретных методов.",
  "knowledge_units": []
}
```
