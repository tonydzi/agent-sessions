---
session: s_fb78da6a
date: 2026-09-30
words: 1840
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fb78da6a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: OpenAI DevDay 2026 Keynote (FULL)
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
good morning. It is great to have everyone here and everyone joining us online thank you for coming, I think this is going to be our best day yet. We have shipped a lot and you have built amazing things with it. You find uses for those models that we have. Thought of. You've helped make our products better. You have sent us thousands of requests mostly on Twitter for ideas for ways we can improve. We try to work through them as fast as we can. We asked us to bring codex to Linux, so we did that. Yes. [Applause.]. You asked us to work across multiple folder in one project so now you can do that too and you asked for codex on your phone so we brought it there. It gives us a lot of joy to bill things that you find helpful and the next thing is one of the things that you've asked for the most. It's something we have been excited abtoo so let's get into it. We are kicking you have with a product that we believe is going to be a whole new way to work with AI. It's like a helper that always has your back. It can expand your potential working 24/7 to take on delusion don't want to do so you can the focus on higher level work. Now, you may have seen early signs of what this can look like in Christopher which you will assistants that help you book a reservation or buy a plane ticket and these are helpful but they are trivial to what the technology can do. So we want to be more ambitious. It knows what's going on. It knows what's matters to you. You don't have to tell it every little thing to do. We want AI to feel like that. We want to feel like magical things that it does without you having to ask. So today weariesing dots. Gots are remarkably capable, always on agents built to handle anything you can think of. They bring i into a whole new form factor to work and give you more time and attention so you can do more things that where you you care about. Let's meet dots. Hey, I'm your Dot. I'm new in ChatGPT. I'll be hear to handle every that comes your way. Ready to jump in when you need me. >> I'm going to call you Alfred, you got it. I'm Alfred. >> I'll keep things moving and check on things when you think it's important. The latest consumer experience numbers came in on team, I've been updating your board meeting deck. So I've cut your migration in Mara-Lago meet notes. >> get it started but make sure you first check every flow against the current product before I review. >> Also update on wedding planning. Bad news, the cake vendor cancel. Good news. I already found a backup. >> When can we do a tasting? >> Saturday whenever works for you. >> Hey there. You're website's updated with the new designs for the forward drop. Check it out. >> Nice. I like that. Just walk the first and third photo and they be you can publish the site. >> Dot. You're live. >> Your board meeting deck is Redd. Revenue is up 51 percent year over year, okay, this looks good except for change it so the consumer experience is scientist and then get into the growth serial numbers. How's I looking. >> Is it rebuild is faster in testing with no regressions so far. >> Amaying share the team on slack. >> . >> Also the kids after-school lessons as soon as registration open. >> They'll love that. Thank you. >> I'm going to see if we can reschedule. >> Okay, please. I can't miss that recital. >> I'll start prepping your notes now. [Applause.]. >> What feel new about my dot is it gets know how I like to work over time and where I want to focus my attention. It can do things like review what came in overnight and ping me with anything urgent before I start my day. I'll be really surprised what that makes my life feels like. It's the way I've always wanted to work with AI. The of course, dots can take care of the small things like the plane ticket or time for dinner or help with the home Vegas. But you can delegate ambitious pieces of work. You just give dot the responsibility, like monitor incoming bug reports, test fixes in draft PRCs. Kick off next year's butt planning cycle. Find out what's slowing down our app. Your dots will get to work and keep working. So here's a good example. Get the app off legacy A PI before it shuts down. But dot can trace the dependencies and figure out everything that needs to change. They can write the code, run the tests and bring our poll request to review. Think about how you would have done that the old way. How many people would have been involved. Now, imagine having dots do that for everything you can think of dot's on board with everything they need to get to work. They follow your access, they have their open computer in the cloud and they can write and test coding as needed. In the future you can work with a team of dots. You also don't need to be in ChatGPT to talk to your dot. Coming soon you'll be able to send a text message, it will text you back. It can text updates and ask to weigh in on a decision. You can even give your dot a call and talk with it directly. When you on board your dot it gets to use the same plug ins you've already connected. It can follow with your work wherever it happens. Through all of this it can you someday in control. Dots are powered by Astra and they are built this protections and safe safeguards and you can customize instructions. So this allows you to trust your dot with as much responsibility as you're comfortable with. To that's dots. Dots are very tied to get things done but you need a space to collaborate with your team and their dots and the problem are here is that almost all productivity 1069 ware was not built for AI and people to work well together. So we're changing that too. Next up we're introducing ChatGPT space. This is a place where you can work together. Space starts with a page like the one you see here on the screen. Dots can work alongside you directly in the page. You can bring in a dot and ask it to track dependencies. You can tag a dot in the comment and it will jump in and get to work. You can give the page instruction like check the s
...[middle elided]...
businesses and upcycle old ones. You're opening the doors of learning and decoding the immune system. What you create, it lives. It changes. It moves with us. Here's to you. The builders. The makers of our time. [Applause.]. >>> we get me to bill AI every day and that's often but still one of the coolst things egret to do is to see what you create. We have a great rest of the day planned. We hope you really enjoy it. Peter will be here for a special session on how we're continuing do investor in the open sourcen and we have a bunch of great sessions. And at the end of the day Tejal and I will be back here. I'm sure a lot of you have tried something like this but we wanted to give you a special way to build with play with what you build. So everybody here today is going to take home a special I edition -- it's very cool. I think you're going to like it. You can pick yours up this the mer. Shop. Finally with all of to new things we shipped today because we want you all to big we have done so many of these that we've been campaigning to rename the company. I think he's in the audience somewhere. Can we find him. [Applause.]. >> I think it would beside nice to do a low key reset here. Maybe we can do it? Is that a real thing? >> Shall we just press it. >> I'm very excited to press this. I have my laptop ready to go. Ready the for a count down? Let's go. Three, two, one! >> thank you for that. That's obviously for everyone in the world not just people here. Before we wrap up I want to share one more thought. People often talk about AI as an industrial rev revolution. The best part of AI is not about making people cogs in a machine  I believing the future in we get this right can be more like a Renaissance than an industrial revolution. AI should beside about giving people more power in their lives and with everything we launch today we hope we can get do that future. So thank you all very much for all you do. Thank you for coming to San Francisco and for watching online.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": true,
  "topic": "agentic-assistants",
  "signal": 0.05,
  "novelty": 0.1,
  "actionability": 0.05,
  "evidence": 0.05,
  "durability": 0.1,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это маркетинговый кинот-презентация OpenAI DevDay про запуск продукта 'Dots' и 'ChatGPT Spaces' — восторженная демонстрация без технических деталей, архитектуры, кода или бенчмарков, которые можно было бы применить на практике.",
  "knowledge_units": []
}
```
