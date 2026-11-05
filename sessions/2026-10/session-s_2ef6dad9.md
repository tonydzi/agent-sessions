---
session: s_2ef6dad9
date: 2026-10-22
words: 1376
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2ef6dad9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Highest Loop — swyx
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] [music] [music] [music] [music] >> In the beginning, there was the token. Then there was the chat. Then we learned to use tools. Then we learned to set goals. I'm skipping a few steps. And these days, we're all about automations. We're all about cron jobs and the loops. And the rest of today on this live stream uh the those of you watching at home, uh we're going to be talking about software factories as well. So, there's a lot of loop stacking. Uh I wrote this essay called Loop Crafts. Uh I think Joel in the audience did a workshop on it yesterday. Can you still hear me? Are we good? Sorry, I I um had a mic slip. Um and I think this is something that is basically a core skill of AI engineer uh is defining what loops you're working in and figuring out whether that's the right level of extraction. And when you're ready, going up a loop in order to figure out the next level of productivity and scaling your inference. And when you're finding issues, going down a loop and going lower level in order to figure out reliability and fixing whatever bugs you you find. If you want to simplify it, uh I have a I have a better analogy that will be less complicated. Uh it's literally just a stack of wild loops, right? I think all of you in in the audience who are programmers will understand this. Uh and effectively this is what we're here to do today. We're um I expect our engineers, our leaders, our researchers, our founders, um to all be understanding and be cursing in as a as a as a sort of human general intelligence, all these loops that you guys are capable of of um going up and down. And that is why there's so much content. >> [laughter] >> Um I often tell people of you who who complain about uh the tracks, I'm not going to apologize for the content. Uh it's up to you to decide and route yourself uh as to which level you you're currently working at and which level you're currently blocked on. Um So, the thing that's occupying most of my time um recently and what I what I make the human analogy for is what is the human loop? Um And in the beginning, there's the heartbeat. You when you're when you're sort of in the womb, you you you sort of get that heartbeat, that's the proof of life. Um then you learn to talk. Then we learn to use tools. Then we start to work. We eat, sleep, code, repeat, or prompt. Um And then we start working in teams. We start working in small groups and families. We we've uh promoted the concept of tiny teams before and I think that is increasingly important with everybody. And I think the interesting thing to think about is like the broader human projects as a whole. Like where we all going? You know, extend out from your personal context, your family, your country, your company, whatever to the broader project of the human civilization and what we're building with collective intelligence. I think it's very interesting to consider that. So, I I think that's a little bit what I want to leave you with today. Like the things that you're doing with coding are definitely crossing over to human life. The message of my last keynote at AI engineer was that the you know, it's very much like agents that you see are working in one domain are definitely generalizing this year. This is the year that we're adding vertical tracks. Like you know, AI in healthcare, AI in finance, AI in GTM. We have a forward deployed engineering track this uh today which I'm very excited about. All of this is meant to see how AI is just diffusing finally beyond coding. Okay. Last World's Fair, I gave you all an update on the stress curves of the organizers. Just to give you an idea, this is the first World's first AI engineer in 2023. This is sort of the sales curves basically of like how people bought. Basically, it was kind of linear. Then we had the first World's Fair 2024. About 2,000 people. 2025 was I think I maybe skipped skipped a few lines. But we're we're basically at 6,000. And if you sort of calculate we we we we aim for 6,000. We actually crossed and go it went to 7,000 today. And basically, I asked you all to buy your tickets earlier. You did not. Um If you measure the Gini coefficient, uh it's gone up and not down, that's the wrong direction. Uh so if you all >> [laughter] >> if you all can just gather uh you know your yourselves and um you know join us early, I think that would be great. Anyway, um why we want to work at a conference, why we why I work on a conference, why you all come to a conference is basically the concept of the highest loop. Um I will submit to you that the highest loop of all is to uh if I can make this slide work. Oh my god. I I I'm going to refresh. Okay. Um uh that the highest loop is where humans come together to figure out what the next loop is. All right, the loop that makes loops. Um so we organize the Engineers Summit all around the world. Uh this year we have summits in New York, summits in Paris, summits in Singapore. Um and uh you know again, uh Melbourne and I'm forgetting one already, Miami. Um and uh we are organizing this with our partners. We want you to organize it in your home countries. We're we're having a partnership team uh to do this. And this is the highest loop of all, which is the World's Fair, which is the summit of summits. So you're I'm very excited to welcome all of you today. Um I hope that you figure out your generative process for generating loops and propagate it down to your teams, to your personal workflows, to your lives. Thank you very much and enjoy the show.

---

**Claude:**

{"is_ad": false, "is_news_rehash": false, "topic": "ai-engineering-loops", "signal": 0.12, "novelty": 0.2, "actionability": 0.1, "evidence": 0.1, "durability": 0.5, "volatility": "stable", "half_life_days": 1825, "why": "Вступительное слово организатора конференции: метафора «стека циклов» (подниматься выше ради масштаба, спускаться ниже ради надёжности) и реклама самой конференции, без конкретных техник и демо.", "knowledge_units": [{"claim": "Ключевой навык AI-инженера: осознавать, в каком цикле (чат, инструменты, цели, автоматизации/cron, софтверные фабрики) ты работаешь, и выбирать правильный уровень абстракции.", "type": "principle", "actionable": "Явно называть текущий уровень цикла для задачи: подниматься на уровень выше, когда нужно масштабировать выработку и инференс, и опускаться ниже, когда нужно чинить баги и повышать надёжность."}]}
