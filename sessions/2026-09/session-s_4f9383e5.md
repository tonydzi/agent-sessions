---
session: s_4f9383e5
date: 2026-09-22
words: 894
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4f9383e5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Getting Started with ChatGPT Work
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Most of the work I put off isn't complicated. It's just scattered. ChatGPT Work helps me pull it together. Before we dive in, let's talk about the difference between Work and Chat. Chat is great when I need a thoughtful answer. Work goes a step further: it can bring in information from the apps I already use and help me actually finish the task. I need to confirm a team dinner next week, but the restaurant's email is buried in my Gmail and the latest headcount and dietary restrictions are in Slack. The details are split, between my inbox and Slack and I don't want to dig through both just to send one reply. First, I'm going to download the ChatGPT desktop app. You can also use Work mode on the web at chatgpt.com, but the app makes it easy to work alongside everything else I already have open. I'll open the download page, choose the version for my computer, and follow the installation steps. Now I'll open the app and sign in with the ChatGPT account I want to use. Once I'm in, I can choose between Chat and Work. Chat is where I go for a quick question. For this, I'm selecting Work mode because I want ChatGPT to find information in Gmail and Slack and then use it to draft an email. To find that email, ChatGPT needs access to Gmail. That's where plugins come in. Plugins connect ChatGPT to the apps I already use, like Gmail, Slack, Calendar, and Google Drive. I'll click Plugins in the sidebar, search for Gmail, and select Install. Then I'll sign in and review the permissions before connecting my account. I only need to do this once. I'm also connecting the Slack Plugin, so now ChatGPT can pull the restaurant's email and the latest team details into the same place. Now I'll start a new chat and switch to Work mode. I'll explain what I need: find the email, check Slack for the latest team details, and draft a reply. I can let ChatGPT gather the information it needs, but I still want to review the draft before anything gets sent. You don't need a perfect prompt. Just ask ChatGPT for what you want! All right, it's finding the restaurant email in Gmail and checking Slack for our latest headcount and dietary restrictions. If it needs more information or permission, it can ask me. Otherwise, I can let the task finish and come back when it's ready. Here's the restaurant email asking me to confirm Thursday at seven, and here's the Slack update with the final headcount and dietary needs. And this is the part that actually helps. It pulls the details together from both apps and gets the reply ready. I'll read through the draft and make one quick change: ask for a quiet table, if one is available. When I'm happy with it, I approve the send. Nothing goes out until I say so. One more thing – I'm going to wake up my pet. This gives me an easy way to notice when Work finishes something or needs my attention. It's also adorable. I'll open the menu, search for Wake Pet, and turn it on. Now I don't have to sit here watching the conversation while something runs, and I'll get an alert when it's finished. This setup works for all sorts of tasks. I can follow up on an overdue email, pull in a Slack update, or find the file I need for a meeting. I started with Gmail, but the real advantage is having my email, messages, files, and calendar together in one place. Look at us, getting things done. That's ChatGPT Work.

---

**Claude:**

01:52, вторник, 22 сентября 2026.

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-work-agentic-assistant", "signal": 0.1, "novelty": 0.1, "actionability": 0.15, "evidence": 0.1, "durability": 0.15, "volatility": "volatile", "half_life_days": 60, "why": "Это промо-ролик OpenAI про фичу ChatGPT Work (плагины Gmail/Slack), без технических деталей реализации — просто демонстрация продукта для конечных пользователей, а не практикующих инженеров.", "knowledge_units": []}
