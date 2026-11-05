---
session: s_0a3e3636
date: 2026-09-22
words: 982
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0a3e3636` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: One Prompt. A Feature Built and Tested. | Ramp × GPT-6 Astra
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
This is a co-orker that knows exactly what you mean and uh can can [music] kind of push the boundaries on computer use. [music] >> You lead all things AI at RAMP. You're always at the bleeding edge. What have you been working on lately? Yeah. So, we have been experimenting with [music] uh Astra and uh pushing it to its limits to make our [music] uh coding faster and and and better and really just take advantage of its computer use [music] in a lot of our day-to-day workflows. >> In the first few days you've had it, what was your first impression? >> Like a co-orker that you trust where you're not going to uh be giving them like a hundred lines of instructions. [music] you're going to give them like a highle goal and what work you're trying to see and then you can kind of come back [music] and check in 10 or 15 minutes later. Astra's very good at taking like a really vague request like that and uh knowing exactly what I wanted to output and giving [music] me back screenshots on the the changes as well. So, uh it it really truly feels like I can hand off more and more vague tasks [music] to Astra. just how quickly it was able to make progress without my input. Like that was definitely a wow moment. I think it's very succinct [music] uh with its words and and and just output. Um nothing super fluffy and [music] especially in like work context when you're trying to go back and forth and just get to a outcome. I don't need to explain like hey you need to click on this tab [music] it's on this page or this route and this modal. It it just kind of knows. >> I I'd love to like talk more about computer use [music] cuz I'm looking at inspect here. So uh it means that your coding harness can trigger computer use. You leverage it a lot. I'd love to learn more. I think [music] this uh this is a really good example where I had a feature request implement routing strategies controls [music] by API key granularity and I said nothing else uh and it was able to know that the way this uh pops up is byick clicking on one of the existing [music] API keys and clicking routing strategies and you can see it kind of kind of worked for about 12 minutes uh and then validated its changes for [music] another uh kind of kind of 15 or so minutes. That's really cool cuz it went ahead and found the exact model and the [music] exact settings that you were trying to change. >> Exactly. Yep. Yeah. And verified it on like mobile view. That's awesome. >> Yeah. I didn't even ask for that. More and more the computer use I think is going to be a big part of how people verify uh lowrisk changes. >> You personally as you [music] start getting your hands on Astra and as you keep pushing the frontier of the eye at ramp, >> what would you like to do next with Astra? A lot of uh the magic with ramp is [music] when ramp kind of goes off and simplifies things about uh accounting for you and being able to kind of get computer use in the hands of our customers [music] is probably like one of the things I'm most excited about. For RAMP we we fetch uh receipts for customers in the background and we use [music] uh computer use for that. And right now we have to do a lot of I guess manual [music] prompting to make sure that the uh model knows exactly where to go on these merchant websites. [music] And so I'm excited to kind of test more uh with a long tale of merchants and see [music] how Astra handles them. I think it'll have a better understanding of how most websites kind of operate. >> Thank you again for stopping by and can't [music] wait to see what you ship next with Astra. >> Awesome. Yeah, thank you so much.

---

**Claude:**

01:50, вторник, 22 сентября.

{"is_ad": true, "is_news_rehash": false, "topic": "computer-use-agentic-coding", "signal": 0.15, "novelty": 0.1, "actionability": 0.1, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это рекламный диалог OpenAI с клиентом (Ramp) про модель Astra — общие восторги без конкретных промптов, кода, метрик или воспроизводимой методики.", "knowledge_units": []}
