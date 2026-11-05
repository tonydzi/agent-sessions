---
session: s_ca9cf327
date: 2026-09-22
words: 945
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ca9cf327` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Figma Gave GPT-6 Astra a Moonshot. Here's what happened.
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
This is really sweet. >> Again, [music] just think of how much work it did. My goodness, it built like the entire cockpit experience. [music] >> I'd love to uh hear more about what you're working on at Figma. >> Big part of what we're thinking about is how do you make Figma [music] agentic inside and out? How do you make sure that all of the best models are available to users [music] when they're inside the Figma product, but also that Figma is available no matter where your workflow might start outside of the app as well. >> What was your first impression on the model? There was a level of confidence that I could feel when using it that was a little bit different from anything that I had tried [music] in the past. It felt like it had its own opinion about how it was going to go about doing this in a way that didn't really require a lot of guidance. I think in particular its ability to [music] really give itself time to understand a new task before it actually dives in. Something that makes it feel like it leads to far better results down the line. [music] The ability to steer it to give it direction even when it was already in the middle of a task was something that felt really special about it. >> I'd love to see like some of the things you've done with Astra. [music] >> Yeah, that'd be awesome. Let's look at it. Imagine you were designing the flight control system for this like single person helicopter that was optimized for taking people these short distances. Let's define some hero flows and some user journeys that we'd actually build into an app. So [music] kind of what I said is okay instead of why don't you actually come up with some concepts for what would make a good prototype and then actually go and and build this [music] out. So you can see again it worked for like 2 hours. >> Wow. >> And then built a new prototype kind of for [music] this experience. getting a common brand system in place, using components the right way to actually create consistency, be able to actually [music] do so much work across multiple different screens and actually stringing that together into a journey that would actually show how it would experience this [music] app across multiple surfaces was something that I just haven't really been able to see done before to actually even communicate at this level of fidelity. An idea that started with like a couple hundred tokens. I mean, it's pretty incredible because I don't think I've ever seen a model [music] use that many Figma features, too. Like getting everything right from the design system, the components, like all of [music] the walk through for the experience. It's amazing. >> In order to do this, well, it would have had to actually think from like pretty deep principles [music] what is required to even set this up right before I actually go and do the design. >> And what are you personally excited to work on next with Astra? Yeah, I think honestly continuing to figure out how this is going to deeply integrate into my own workflow of and really [music] think about all the ways that this will impact how we like build and ship features at Figma from that original specification going from the like messy exploration of ideas to refining [music] something into a clear point of view that we can all align on and actually going through each of those steps of the the process to both prototype and communicate ideas visually but also start to derisk whatever the most risky parts are from a technical standpoint. Being able to do that all at the same time in parallel is [music] something that there's no doubt is going to massively speed up workflows and just ultimately let us ship a lot more product a lot faster.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "agentic-design-tools", "signal": 0.1, "novelty": 0.05, "actionability": 0.05, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 45, "why": "Это промо-видео OpenAI/Figma с восторженными цитатами о новой модели без единой конкретной техники, промпта или воспроизводимого шага.", "knowledge_units": []}
