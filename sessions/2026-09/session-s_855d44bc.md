---
session: s_855d44bc
date: 2026-09-21
words: 835
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_855d44bc` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Use Your Computer and Browser
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
ChatGPT Work can use the tools you already use for plugins. But some tools don't have a plugin. Others live in a desktop app or a website where I've already signed in. And that's where Computer use and Chrome use come in. They're only available in the Work tab with a ChatGPT desktop app,  not in regular ChatGPT,  on the web, or on your phone. Computer use lets ChatGPT  use desktop apps just like you do. You can click, type, and move between apps and windows. Chrome uses is the same thing in your browser,  using websites where you're already signed in. And both can work in the background  so you can keep using your computer. Before accessing an app or website,  ChatGPT asks for permission. You can allow it once or let it remember your choice for next time. I'm using dictation here,  so I can say what I need instead of typing it. Play my daylist on Spotify. This is a small task, but it makes the distinction clear. There isn't a special Spotify integration here. ChatGPT is using the desktop app I already use. On a Mac, it can handle a task like this in the background while I keep working. I can watch it, take over, or stop whenever I want. And if I want to show ChatGPT what I'm looking at, I can press Command Command  to take an appshot It works with apps or websites and is like a screenshot with context. So ChatGPT can see and understand what I'm looking at without me having to explain everything. Chrome lets ChatGPT work in a browser I already use, including websites where I'm signed in. I'm going on vacation next month. Can you prepare a PTO request on Workday for September 14th and 15th? Check my calendar for conflicts and draft an out-of-office event for the same dates. Show me both drafts and stop before submitting the PTO request or create an encounter event. Workday doesn’t have a plugin,  so Chrome use handles  the part that normally means opening tabs  and filling out the form. And this is why Chrome use and plugins work well together. ChatGPT uses the browser for Workday because there's no plugin. And then it uses the Google Calendar plugin to check my schedule and prepare the out-of-office event. And it stops there. The request is filled out, the calendar event is ready. But submitting PTO and creating an event are real changes,  so I get to review them first. This is how I use ChatGPT Work. I want ChatGPT to take on the tedious steps, and I still want the final decision when something affects my calendar, my team, or another system. For me, the simple rule is: Use a plugin when there's a direct route to the tool you need, choose computer use when the work lives on a desktop app and choose Chrome use when the work lives in a browser  you're already signed into. A PTO request ready to submit, and an out-of-office event ready to create. That's ChatGPT Work.

---

**Claude:**

01:51, 21 сентября 2026.

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-computer-use", "signal": 0.15, "novelty": 0.1, "actionability": 0.1, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это промо-ролик OpenAI про фичу ChatGPT Work (Computer use / Chrome use) — маркетинговая демонстрация без разбора архитектуры, ограничений или практических приёмов внедрения.", "knowledge_units": [{"claim": "ChatGPT Work умеет управлять десктоп-приложениями (Computer use) и браузером с уже залогиненными сайтами (Chrome use), когда нет прямого plugin/интеграции", "type": "tool-caveat", "actionable": "Учитывать это как альтернативу написанию кастомных интеграций для внутренних инструментов без API, но проверять надёжность и безопасность на своих сценариях, а не доверять рекламному ролику"}]}
