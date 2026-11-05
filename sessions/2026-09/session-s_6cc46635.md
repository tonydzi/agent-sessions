---
session: s_6cc46635
date: 2026-09-21
words: 764
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_6cc46635` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Create Slides, Docs, and Templates
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Every week my team has a meeting about internal AI adoption. The conversation is useful. The transcript is a lot. I want a way for the meeting transcript to become organized for my team to use and a format to share out with leadership. With  ChatGPT Work, I can use Google Drive  to turn it into a Google Doc for my team  and a slide deck for leadership. I can then save both formats as templates. I'm not starting over next week. Let me show you how. I’m using the desktop app, but you can also do this in ChatGPT Work on the web or mobile at chatgpt.com. Plugins connect ChatGPT to the apps I already use. I've got Gmail and Calendar already connected. I'll open Plugins, search for Google Drive,  select install, and connect my account  so ChatGPT can create actual Google Docs and slides. I'll start a new chat in Work mode and and give it the transcript from our weekly AI adoption meeting. it has everything we discussed, like updates, decisions, and at least  three side conversations  I don't need in the recap. I'll tell ChatGPT exactly how I want the Google Doc organized. I want an executive summary, this week's this week's updates, decisions, risks and blockers, action items, open questions, and next steps. I want clear section headings,  short bullets, bolded decisions, and an action items table. If an owner or deadline isn't   in the transcript, ChatGPT can flag it instead of guessing. All right. Here's the finished Google Doc. The decisions are easy to find. The action items are all in a table. And I can see what still needs an answer. Everything is already in the format I need. So I can use this document as a starting point  for the leadership slides. I want five slides that show  the biggest updates, what's working, what's not,  what we're doing next,  and the decisions we need. I'm passing in a deck that I made last week  so it can format it the same way. Here's the Google Doc. And here's the leadership deck it created from that doc. The summary gives the team all the detail. The slides give leadership a version  they can absorb in a couple of minutes. This doc and deck look great. And I'm going to need  the same structure again next week. So I'll type in template creator  and ask it to use this Google Docs formatting. Template creator learns the heading, formatting, and action items table. Now I'll save  the leadership deck the same way. This time template creator learns the slide order, layout, and visual style. So the next leadership update  starts with the same look. Next week I'll add the new meeting transcript  and use my meeting summary template to create the Google Doc. Then I'll use my "leadership" update template  to turn that document into the leadership slide deck. A clear doc, a polished deck,  and nothing to rebuild next week. That’s ChatGPT Work

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-work-templates", "signal": 0.15, "novelty": 0.05, "actionability": 0.2, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это рекламный ролик OpenAI про фичу ChatGPT Work (Google Drive плагин + шаблоны), без переносимой инженерной методики.", "knowledge_units": []}
