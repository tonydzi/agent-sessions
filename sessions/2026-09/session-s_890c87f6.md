---
session: s_890c87f6
date: 2026-09-21
words: 728
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_890c87f6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Use ChatGPT Work on Your Phone
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
You can use ChatGPT Work directly from your phone. I use it to catch up on work, stay on top of personal stuff, and get things done before I even make it to my desk. I've been on vacation, and I want to catch up before I get back into the office. I'm using dictation, so I can just say what I need instead of typing it. Can you check my Slack and Gmail from the last week, let me know if anything important happened, and tell me if there's anything I need to deal with urgently? ChatGPT is reading through my email and Slack, but especially taking note of the channels I'm active in, so that it can put together a full view of what happened while I was away. Now I can see what changed, which messages I actually need to answer, and what I can ignore. I don't have to spend the first half of my day catching up. And I also use ChatGPT for personal stuff. Instead of checking all my accounts myself, I can just ask it how I'm doing. Can you check my finances for the last month and let me know how my saving is going? And also let me know if there's any spending I should be aware of. I've already connected the Finances plugin, so it can check my accounts and credit cards without me pulling everything up myself. It only has read-only access. It can show me how my saving is going, where I'm spending the most, and whether anything looks unusual. I can also ask it to keep checking for me, so I don't have to remember to look every day. Could you do a check like this every day and let me know if anything's out of the ordinary? Most of this doesn't require my computer at all. But if I need something from a laptop, I can connect to it with Remote. I open Remote on my computer, scan the pairing code with the ChatGPT app on my phone, and choose my computer. Now I can open a task that's already running on my computer, see what it's working on, and tell it what to do next. It can still use the files and apps on my laptop, even though I'm checking in from my phone. My computer just needs to stay awake and online. I can leave my Mac open, or plug it in and turn on Keep this Mac awake. I can handle work stuff and personal stuff from my phone. And if I ever need something on my computer, Remote is there too. I can get caught up before I even make it to my desk. That's ChatGPT Work.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-mobile-agentic-features", "signal": 0.1, "novelty": 0.1, "actionability": 0.1, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это рекламный ролик OpenAI про фичи ChatGPT Work на телефоне (Slack/Gmail-дайджест, финансовый плагин, Remote к компьютеру) — маркетинговая демонстрация продукта без переносимых инженерных знаний.", "knowledge_units": []}
