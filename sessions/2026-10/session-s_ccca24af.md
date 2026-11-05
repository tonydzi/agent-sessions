---
session: s_ccca24af
date: 2026-10-27
words: 891
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ccca24af` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Set up your dot in the ChatGPT mobile app
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Hey, what's up? I'm Alex. I work on dots for Mobile. dots are always-on proactive agents that just take [bleep] off your plate. Previously, you could only claim a dot on desktop and web, but you can now set up dots on mobile as well. It'll be available on both iOS and Android. And honestly, very, very easy to set up. We designed it so that basically it sets itself up. So all you have to do is open the ChatGPT app. In the top left corner, you'll see an entry point that says Meet dot. Once you hit that button, it'll basically create a thread with your dot. From there, your dot just gets to work. It might ask you for calendar access. It might ask you to connect your email. Highly recommend connecting both calendar and email because it just gives your dot more context. The more context that your dot has, the more it can kind of take off your plate. The other thing you can do with your dot is actually personalize it. You can give it a name. You can give it an avatar. So let's go ahead and do that. I'm going to name my dot Blossie. And there's a couple options to choose from. I'm actually going to create a custom avatar. All right, so my favorite color is blue. I'm going to make him blue. I'm going to keep things simple for now, so no accessories. But yep, this is Blossie. So your dot also has access to its own computer, and it also has access to your computer, which is really cool for doing complex tasks like coding, prototyping, et cetera. So let's give Blossie a call and see if we can prototype something quickly. Hey, Alex. Good evening. What's on your mind? Hey, Blossie. Can you actually prototype me an iOS widget so that you can live on my home screen? I want the widget to have your avatar, your name, and then also like a short status on what you're working on. Let me check on that. Just to like kick off a Codex thread and start building it, while you do that, also just check Slack to see if anybody else is working on this widget. I want to make sure I'm collaborating with the right people. Good call. Brian Somerset and Gavin Nelson are the folks to sync with. They're already pushing toward a widget MVP. Awesome. Why don't you just, can you like get me into a Slack thread with them? And also when you're done with the prototype, send me a screenshot so I can give you some comments. Yeah, on it. I'll loop you in with Brian and Gavin and get you a screenshot as soon as it's ready. I'm on that same prototype thread and I'll draft a Slack reply tagging them for you to approve. All right. Awesome. Thank you. Cool. Just going to let Blossie cook for a little bit. Going to check back in when I'm back home in front of my computer on the latest progress. If you're watching this video right now on your phone, switch over to the ChatGPT app and get your dot set up. Can't wait to see what you build with your dot. See ya.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-dots-mobile-setup", "signal": 0.12, "novelty": 0.1, "actionability": 0.2, "evidence": 0.2, "durability": 0.15, "volatility": "volatile", "half_life_days": 60, "why": "Это рекламная демонстрация продукта OpenAI: как включить «dot» в мобильном ChatGPT, без переносимых инженерных приёмов.", "knowledge_units": [{"claim": "Чем больше контекста (календарь, почта) подключено к проактивному агенту, тем больше задач он может снять с пользователя.", "type": "principle", "actionable": "При проектировании персонального агента сразу закладывать подключение календаря и почты как источников контекста."}, {"claim": "Агент может запускать фоновый поток кодинга (Codex), параллельно проверять Slack на коллег по теме и готовить черновик ответа, который человек подтверждает.", "type": "workflow", "actionable": "Строить агентов по схеме «делегировать в фон, подготовить черновик, получить подтверждение человека» для действий наружу."}]}
