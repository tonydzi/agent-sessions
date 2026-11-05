---
session: s_1cf8f11e
date: 2026-09-22
words: 1004
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1cf8f11e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: “A Staff Engineer Collaborator” | Notion’s First Look at GPT-6 Astra
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
I think a [music] better metaphor today is more like a like a staff engineer collaborator. [music] You don't give a staff engineer tiny tickets. You give them a hard problem that you've tried to solve before but couldn't. >> All right. Hi Quinn. Thank you so much for coming. >> Hey. No, thanks for having me. What have you been working on? [music] As of late, it's been a lot of how do we make sure that we can both give users like great AI [music] experiences, but also maybe make it hard to like get free tokens and other things like that. Uh that's been a fun interesting [music] uh growth challenge. >> I'm curious to hear what was your first impression. >> So I mainly used it in codeex [music] um cuz as an engineer that's where I live like most of my time. It was [music] much better at communicating. My experience with Soul and previous models had been that they were very smart. They can [music] find very interesting things and they're really bad at telling me what they found. And Astro is so much better at like talking like a human to a [music] human because my main job working with these models is to kind of unblock them, right? Like giving it tasks and having it do tasks for me. Like that was last year's like coding approach. This year's is much more around giving it a goal [music] and helping it like navigate and I was spending less time and that the main time I'm looking at [music] the chat is trying to figure out what question is it asking of me and what do I need to answer for it. >> Yeah. So closing the loop with the model a lot faster [music] >> and that means that like that that time I spend actively like working with the model is shorter too. >> What's the first like big thing you worked on with Astra? We spend a lot of money on tokens and one of the main things that impacts that is how good are you at cash reuse, right? [music] Are we as close to our theoretical max as we think we should be? You have a lot of like optimizations as well. The very first task I gave Astra was [music] here's all the stuff we've done before. Here's our current understanding. What what did we miss in our last like [music] audit of this? Astra just found things that were were missed. uh where [music] Soul would be able to like dig into something and see a pattern, but Astro would be able to kind of like put the dots together faster, [music] see something that we had overlooked as a pattern, but like if you if you thought about it, kind of imply that something else was happening. [music] It was just very very clear with communicating here was like the problem, here is [music] the specific scenario. >> It's very crisp. Like there's no fluff. It's like exactly the way you would have written. >> Yeah. like I was able to understand without rereading it. Uh which [music] stood out at least compared to a lot of the times I've asked coding agents to explain what they found. >> That's awesome. So as we roll out Astra now, how would you describe it to your notion teammates as they start using it? >> Instead of giving a task, maybe just give it a like [music] topline goal. Maybe like give it a number on a like dashboard and say this like number just needs [music] one more nine and that is like the appropriate scope you should be getting these models. That's awesome. Well, I can't wait to see [music] that. And uh thank you, Quinn, for the great feedback as always. And we can't wait to see what Notion will do next with it. [music] >> Yeah, super excited.

---

**Claude:**

{"is_ad": false, "is_news_rehash": true, "topic": "agentic-coding-workflow", "signal": 0.25, "novelty": 0.15, "actionability": 0.15, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это промо-интервью OpenAI с клиентом Notion про новую модель Astra — пара анекдотов про смену стиля работы с агентом, но без конкретных техник, цифр или воспроизводимого метода.", "knowledge_units": [{"claim": "Пользователь описывает сдвиг подхода к агентам: раньше давали маленькие тикеты и разблокировали модель, теперь ставят top-line цель (например, конкретную метрику дашборда) и дают агенту самому находить путь", "type": "principle", "actionable": "При постановке задач агенту формулируй цель через измеримый результат (например, 'подними метрику X на one nine'), а не пошаговую инструкцию, и оценивай, тратится ли меньше времени на микроменеджмент"}]}
