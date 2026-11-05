---
session: s_a0200d25
date: 2026-09-21
words: 696
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a0200d25` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Plugins & Skills
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
You know that feeling when you need to schedule a meeting, but everything  you need to know is scattered? I need to schedule a kickoff for a client's website redesign,  and I want to walk in with a plan. The client already sent the pages they want updated. Their launch date  and a few sites they like. I'm going to have ChatGPT find that email,  schedule the meeting, and build a brief to prep me. Then I'll save the process as a skill  I can use the next time I need it. I'm using the desktop app here,  but you can also do this in work mode on the web or mobile at chatgpt.com. Plugins connect ChatGPT Work to the apps I already use. Gmail is already connected,  so ChatGPT  and I'm adding Google Calendar  can find a time and schedule the meeting. I'll open Plugins, search for Google Calendar,  and select Install. Then I'll connect my account. Now, ChatGPT can use my inbox  and my calendar together. I'll ask ChatGPT  to check for times I'm available  for this specific meeting before Friday. Looks like it found a few options. Great. Now I'll have ChatGPT find the client's email  and use it to draft the meeting invitation. We'll have it figure out  the right attendees, a title, and an agenda. Here's the email,  suggested time, and the meeting invitation. Everything looks right, so now I'll have ChatGPT create the calendar event. The meeting is booked, but I still need to prep. for client kickoffs, I like my meeting brief to cover the objective, client priorities, decisions, risks, and next steps. I'll ask ChatGPT to pull that together from the email calendar event. Great. This is exactly how I like my meeting briefs. I have meetings like this often, and instead of explaining how to do this every time,  I can save it as a skill. A skill is a reusable set of instructions ChatGPT can follow whenever I need  the same kind of work done. I'll call this one meeting prep. Awesome. It made the skill, and now I want to make sure it works the way that I want it to. I'll run meeting prep on another meeting and check that it uses the same format and pulls in the right email context. All right. Now the meeting is booked. The brief is exactly how I like it,  and the next time I need one,   I can run the meeting prep skill. Booked, briefed,  and ready for the next one. That's ChatGPT Work.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-plugins-skills", "signal": 0.15, "novelty": 0.1, "actionability": 0.15, "evidence": 0.2, "durability": 0.3, "volatility": "volatile", "half_life_days": 60, "why": "Это промо-ролик OpenAI, показывающий фичи ChatGPT Work (плагины Gmail/Calendar + сохранение workflow как skill) на постановочном сценарии, без технических деталей о том, как это реально устроено.", "knowledge_units": []}
