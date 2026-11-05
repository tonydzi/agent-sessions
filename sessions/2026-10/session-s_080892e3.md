---
session: s_080892e3
date: 2026-10-01
words: 1974
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_080892e3` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How I Code Without Typing
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
A handful of y'all have noticed something different about me recently. Obviously, I'm referring to my hair, which is currently longer than it should be, and definitely not referring to my hand that has been in and out of a cast for about a month now and will be in a cast for another one to potentially 6 months. This is not pleasant for me, and as a result, I'll be making a much more personal video than I normally do because I have to learn to deal with this. Having one hand is kind of annoying when your job is to type and code and use computers to do all these types of things. even if I'm doing videos about it, it's very nice to be able to do things like command tab between apps or type in the thing you want to do. And now I just can't. That said, I've been managing to ship more than ever as of late. You can see part of this through my GitHub contributions. In fact, the day here, August 8th, was right as I was starting to get my hand bundled up like this. And since then, I have been able to maintain pace and even go further than I ever thought I'd be able to, shipping some of the biggest and widest ranging changes I've ever worked on in my career. And you can probably guess how I've been able to do that. Yes, it is AI, but I want to go deeper than that here. In order to get around the fact that I'm down a hand, literally, I've had to change the way I work in meaningful ways. And I think a lot of this is going to be useful even for those of y'all who type and type fast. I was a really fast typer before, as high as 160 words per minute pretty consistently. So, losing that has been a tough hit for me to take and I've made a ton of adjustments to my workflow in order to stay productive despite this. I think that these tips will be useful well outside of me. And I'm saying this because I've shared a lot of them with my team and they've been helping them out too, both in being more productive and enjoying using their computer more for real world work. So, this video is going to be very strange. It's both a personal diary of me dealing with the hell that is my hand not working, but also a pile of useful tips for being as effective as possible working with realworld AI engineering tools in order to stay productive even without having to type directly. All that said, I'm sure you guys can guess since I'm in the US, I have a lot of medical bills to pay. So, pardon me for a quick break for today's sponsor. AI has fundamentally changed how big businesses operate. Back in my day, if you worked at a Fortune 500, they would only really buy product from other Fortune 500s. So, they weren't going to try some small startup's new SAS. That has entirely changed. But, there are some catches here, too, because the company isn't just going to sign up for an account the normal way that users do where they go show up and hit the sign-in button. They're going to want a lot of things different. They might want their agents to sign up. They're almost certainly going to want to go through their OOTH platforms and all the crazy SAML, Octa, and other things those businesses might be using. Are you ready for all of those cases? Well, if you're using today's sponsor, Work OS, you almost certainly are because these guys have it figured out. That's why companies like OpenAI, Anthropic, Cursor, FAL, Base 10, AMP, Bolt, and so many more are all building on top of work OS. When you start looking into work OS, you'll see why everyone uses them. From OKIT, which makes it easy to set up a good sign-in flow, to the admin portal, which makes it easy for the IT teams that the companies are trying to onboard to actually sign up with any of the many different O providers they might be using. Seriously, if you've never had to configure SAML, Duo, or Keycloak for your business, I wouldn't wish that on my worst enemy. Thankfully, Work OS has it handled for you. And if you're worried about agents signing up for your stuff, they have that covered too with a new standard OMD that they helped pioneer with Cloudflare, Firecrawl, and many other companies that's already being adopted across the industry. In order to get enterprise customers, they need to be able to sign up for your app. Get it right at soy.link/workos. One last note, if anybody's interested in sponsoring my cast, I am down to have the conversation. My email for sponsorship and all of that is in the description on YouTube. You can check that out if you want to learn more. I think it'd be fun to throw some logos on here. It would make me feel at least a little less bad. Whisper flow, respond to our emails, please. Anyways, let's go through this. I know it says coding without typing, but I honestly think it would be more accurate to say staying productive. As you can see, typing is hard. Staying productive on a PC without typing because that's honestly what it's been for me. Talking out code doesn't work great if you're like trying to do a function definition. Like here I'll even try directly. Let x= 4 let y equ= 12 while x is less than y x++ that that's not viable. So yeah, as much as I love the voice text tools I've been using, you're not writing code with your voice. And if you are one of the few people that has been doing this, and I know a handful that have been for not just like years, but for decades, you are a godamn trooper and a hero. And I have so much respect for you. I am incredibly thankful that my issues have been in the era of AI being able to both translate what I say and also write the code and also argue most importantly use my computer. Yeah, that has been one of the biggest things for me. So yeah, coding with your voice just by writing the code directly not realistic. So another way of framing this is to be frank, my hand injury has forced me to embrace vibe coding more and this is absolutely the case. Not even just because I can't type as well, but navigating my computer is harder. Switching between apps is harder. I uh think you can probably see from here 
...[middle elided]...
me you have a bug you notice in your software, a feature you want to work on or something else where your next step would have been to, I don't know, plan it out or write something down or do something other than just set off an agent to do it. Right before you start, set off the agent with everything in your brain already. Don't help it at all. Don't give it hints. Don't point it where it should go. Don't give it the additional context by manually bringing it in. Just tell it what's on your mind. And while it runs, go do things the way you normally do. Then come back at the end and see how the way you did things differs from how the agent did things and see if you can honestly still kid yourself into doing all that manual work yourself. I think you'll be surprised how much of your process can just be done by the agent itself. I know I have been. I have been blown away at how quickly the agents have chewed through the boundaries I had on each side of my mental model where I bring them in sooner and I let them go longer and my hand has kind of been a forcing function to get me deeper in that and I don't think I'm ever going back. So yeah, this is a strange video. I know. I have no idea how it will perform. I'm hopeful it's good because I think this is cool. I've fundamentally changed how I work at my computer every day. And while sure, my hand is a meaningful part of why I've had to do that, I've actually been very happy with the results. And while I do dearly miss being able to type out my  posts by hand, I have found this new way of working to be quite pleasant. And this tiny little mic has made it a lot more tolerable to live with my computer with only one hand. I hope these tips were helpful. It's been a huge change in how I work. And while I know most of you guys do have both your hands, for those who don't, and for those who want to just use their computer differently, I bet these tips will be helpful. Let me know how y'all feel. And until next time, he starts.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding",
  "signal": 0.25,
  "novelty": 0.25,
  "actionability": 0.3,
  "evidence": 0.2,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Личный влог про жизнь с травмой руки с одним практическим советом про агентный воркфлоу, упакованным в историю и рекламную вставку, без замеров и доказательств.",
  "knowledge_units": [
    {
      "claim": "Перед тем как самому планировать задачу вручную, стоит сразу вывалить агенту всё, что есть в голове, без подсказок и направления, запустить его и заняться задачей параллельно самому — а потом сравнить результат агента со своим ручным процессом.",
      "type": "tactic",
      "actionable": "В следующий раз, заметив баг или фичу, сначала опишите агенту сырую мысль без уточнений и дайте ему решить самостоятельно, а свой привычный процесс (планирование, ресёрч) делайте параллельно для сравнения — так можно нащупать, где можно отдать агенту больше ответственности раньше в процессе."
    },
    {
      "claim": "Голосовой ввод хорошо работает для навигации по компьютеру и постановки задач агенту, но плохо подходит для написания кода напрямую (диктовать синтаксис функции практически невозможно).",
      "type": "tool-caveat",
      "actionable": "Используйте voice-to-text для постановки задач и общения с агентом, но не пытайтесь диктовать код построчно — делегируйте написание кода агенту, а голосом давайте только намерение."
    }
  ]
}
```
