---
session: s_305591c7
date: 2026-10-27
words: 1184
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_305591c7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Building the Codex community
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Let's talk about community today. My favorite topic. There's something really special that happens when curious people come together. These ideas turn into projects. We have introductions that are made at these events that become friendships. And eventually all of this feels like a true community. So we've had the Codex Ambassador Program for a long time now. Could you tell us a little bit about the story and where it all began? Sure. First of all, this is one of my favorite programs at OpenAI. When we started the Codex Ambassador Program, we started with the intention of just having about 15 to 20 ambassadors spread across the globe. Maybe we have a few in-person events, maybe online. And really just the intent was to bring the magic of Codex and our GPT-5 series of models closer to the community, right? And fast forward to now, we're 150 plus ambassadors spread across 80 plus countries. And we've had, what, about 300 plus events, right? 300 plus events. And this has been both online, in-person, and so on. And at the crux of it, the idea really is to bring the magic of these models closer to people who want to tinker, who want to optimize for creativity, who want to just try and see what is the art of possibility right now and get closer to achieving it. And it's so cool that we can bring these people together to literally see these ideas come to life. And speaking of all of these community moments, what's been your favorite community moment? So I've been doing this for a while now, and I think the most impressive community event I've seen has to be from our community ambassadors in Kochi in India. They went and ran a whole Codex community event on a running metro. I think they filled it up and basically sat there all just coding together, using Codex to turn their ideas into life. And I just found that so impressive. And now it's starting a trend. For me, that is true community. I loved it. What's been your favorite? Gosh, there have been so many moments like this since we launched the Codex Ambassador program. But if I was to choose one, I think I would choose the Build Week. Absolutely. So the idea behind Build Week was as we released the GPT-5.6 series of models, we wanted to bring the community closer to these models as well as what they can do with Codex and these models together. Right. And we, of course, activated our network of ambassadors. And within a week, we had 60 plus events. Right. And this was spread across throughout the globe. You know, 24-7, we had events popping up in Tokyo. We had events popping up in India. Same as London, as well as SF. And it was so nice to see, like, every day that I would wake up, I would open Slack and I would see, like, pictures of all of these ambassadors saying that, hey, like, we had this event over here. Oh, wow. Like, you know, this person made this particular thing. And it was truly like, you know, it was truly a moment when I was like, wow, like, our models are very capable as well as, you know, we can truly just do things with these models as well as our ambassadors. Absolutely. That local momentum was absolutely just incredible to watch and just witness. And all of our ambassadors are incredible. Like, they are probably the best community leaders I've ever seen. And I think what makes them super good at what they do is they always build with heart. So no matter what event they're doing or whatever talks they have, they really bring that heart and, like, soul into everything they do. So what do you think, what does it take to be a Codex ambassador? I would say if there was ever one requirement for that, I think that would be for people who are curious, right? It's, we want people who want to reimagine what is possible. We want people who want to try and challenge what, you know, majority think is the reality today and just really push the models that we have today to their limits. One. Second, we want people who are passionate about bringing people up to speed with all that we're shipping. Also, at the same time, like, you know, make it into an environment which is inclusive, right? And just a place where people feel comfortable asking questions and getting answers to. No, 100%. And I think one of the main things that make our Codex ambassadors stand out is that they don't need to know everything about Codex just yet. As long as, like you said, they're curious and generous with their time, I think they'll just make a perfect Codex ambassador. All right. So what does someone need to do to get involved? No matter where you are in the world, come build with us and join the Codex community. Brilliant. Let's do it. Let's go. Yes.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "community-program", "signal": 0.04, "novelty": 0.05, "actionability": 0.05, "evidence": 0.15, "durability": 0.3, "volatility": "volatile", "half_life_days": 60, "why": "Промо-разговор OpenAI о программе Codex Ambassador (150+ амбассадоров, 80+ стран, 300+ ивентов) и призыв присоединиться, без технических приёмов, которые инженер мог бы применить в работе.", "knowledge_units": [{"claim": "OpenAI ведёт программу Codex Ambassador: более 150 амбассадоров в 80+ странах провели 300+ онлайн и офлайн ивентов; во время Build Week к релизу серии GPT-5.6 прошло 60+ ивентов за неделю.", "type": "principle", "actionable": "Если интересна заметность в экосистеме Codex, можно податься в амбассадоры; требования мягкие: любопытство и готовность делиться знаниями, глубокая экспертиза по Codex не нужна."}]}
