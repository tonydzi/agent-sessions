---
session: s_4f46aff0
date: 2026-10-01
words: 1922
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4f46aff0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Did AI Kill React Native?
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
This video is going to be quite a throwback. I almost feel like I should bust out the blonde hair and the mustache again for it because we're really going back here because we're talking about React Native. This is going to be a fun one because a lot has changed since we really went in depth on React Native stuff in the past. And as I'm sure many of y'all know, I am quite a defender. One of my first big like impactful so to speak videos was when I covered the old Airbnb article about why they moved off of React Native and showcased how some of the arguments just didn't really hold up especially five plus years later. They ended up updating the article saying as much and I think they even linked my video at the top which was just unbelievable because this specific article had held me back so much when I was trying to get React Native adopted places it made sense. Specifically, when I was at Twitch, I had such a hell of a time trying to get React Native to be taken seriously on a platform where it would actually benefit us. And that article from Airbnb made it nearly impossible. There was one thing that helped a lot though. Shopify. They made the move to React Native and showed some crazy wins. Not only was it performing better than you would have expected being React Native, it was actually often outperforming the native versions in particular with the Android app for their point of sale systems, which was so so cool. It ended up being a huge moment for React Native and Shopify's investment in the platform has helped a ton with the growth and success of React Native, which is why this sucks. For those who are listening instead of watching, Shopify has just announced their plans to move off of React Native and go back to native code. They put out an article, a bunch of additional comms, and let's be real, everyone's exploded since. And I have a lot of my own thoughts here, too, because I've been building more React Native than ever recently. And more so, I've been building native, too. I have more thoughts than I think I ever have about the role of React Native in the future, as well as the future of React Native itself due to some changes going on at Meta right now. It's going to be a lot of layers for this one, and I can't wait to unravel all of them with you. But since my Shopify store isn't doing particularly well, we're going to have to make some money with a quick sponsor break. Remember back when coding with AI was just trying to stuff all of the code into the context window of your agents and hoping they could figure out what to change. We've made a ton of progress since then. Turns out when you give agents things like the browser in the terminal, they can get a lot more done and be much more effective. Which leads me to an interesting question. Why are our code review bots still using things the way we used to? Why are they still trying to stuff all of the code into their context window and just check the grammar to make sure it's syntactically correct? Wouldn't it be way better if our code review agents could actually run the code and test it in a real sandbox? Turns out it is. And Gretile just introduced T-Rex to prove it. There's a lot of bugs that can only be caught when you run the code, not just when you look at the code. And that's what T-Rex is here to solve for you. I realized this was obviously better when I started asking my agents to test code locally on my machine and saw them finding things that other code review bots couldn't. But it was still just my one machine that was testing things and I was using my agents that I probably also used to write the code. So all the benefits of a cloud-based reviewer just weren't there. T-Rex goes so much further than just running the code on a random server. Though the core reptile agent still does what it always did before, looking at the code and making decisions, but now it can spin up separate sub aents in separate sandboxes to test different theories, get images and videos of what change, what works, what doesn't, and give you all the context you need to fix the code before it hits users. If you're tired of your code review agents passing broken code or hallucinating things that don't work and you'd prefer them to actually be able to click buttons in your app and make sure it works as it's expected to, get that today at sid.link/graptile. Let's dive in where it matters. We need to talk about why Shopify is making this move. We'll start with what they said, then I will go into some conspiracy theories about where the market is moving, what I've been doing, and then try to wrap it all into a nice package of how software dev is changing. I've done such a good job not mentioning AI yet and I will do my best to not until I have to, but it is important here. So, we'll get there. Native is now the future of mobile at Shopify. Coding agents change what it costs to build mobile apps twice. Here's why Shopify is moving from React Native back to Swift and Cotlin. It is my understanding that they were not too heavily on Swift when they made the React Native move initially that it was still Objective C era, but I could be wrong there. We decided to go allin on React Native back in 2020 and that bet has been extremely successful. We saved a ton of time building features just once. We enabled developers with no mobile background to contribute to our apps and we freed ourselves from constantly chasing feature par. They are missing some additional really big wins here. The I would argue the biggest by far is OTAA updating. We'll talk about what that is and why it matters in a little bit, but we will get there. Thank you, Jamon, who for those who aren't familiar is here from Infinite Red, one of the legendary OG React Native people, called it the same thing I did as I was saying it. In January of 2025, the author of this article, who is Mustafa Ali at our who of course works at Shopify, wrote an article summarizing and reflecting on the 5 year
...[middle elided]...
ative or the native platforms, you should be testing the mobile apps on both platforms when you build to make sure they work as expected. Which means somebody in your team's got to suffer with an Android phone. For that, I am sorry. I'm honestly more sorry for that than anything else I've said here. You want your Android app to be good, the solution isn't React Native or Cotlin or some other library or jetack compose. The solution is to make someone daily drive Android on your team. Actually, if you do have an Android person on your team already, you should make them daily drive an iPhone so they can know how a phone's supposed to work and then make them go back to Android and then they'll fix your app. I think I've said all I have to here. Can you tell I've been through it with mobile? This was a fun one for me. I don't think this video is going to perform well, so please prove me wrong. If you liked it, subscribe, give it a like, leave a comment, and send it to a friend. Give me the singles that you guys want videos that aren't me just talking about agents the whole time, and I'll make more of them. But if this video bombs, then you're going to get what you ask for. So, for once, I'm asking you engage. I hate doing this, but I'm asking because if you do like this and want more like this, I need to see it in the systems pages and on the studio on YouTube, or I'm going to assume what those numbers say, which is that y'all don't care. So, show me that you care so I can justify doing this. Otherwise, I'm going to have to do what people actually care about. Not because I am following the money, but because I want the things we talk about to have impact and to matter and for the conversation to be had and heard. And if people aren't listening and they aren't watching, then it's a waste of all of our time. So, please try to prove me wrong here because then I can go do the Electron video that I really don't want to do. Thank you as always and until next time, peace nerds.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "react-native-vs-ai-coding-agents",
  "signal": 0.25,
  "novelty": 0.25,
  "actionability": 0.2,
  "evidence": 0.3,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 180,
  "why": "Это по сути реакция на новость об уходе Shopify с React Native плюс личные истории и реклама Graptile T-Rex, без воспроизводимой методологии для AI-инженера.",
  "knowledge_units": [
    {
      "claim": "Автор утверждает, что AI-кодинг-агенты снижают стоимость написания нативного кода дважды (iOS и Android отдельно), что подрывает главный экономический аргумент в пользу кросс-платформенных фреймворков вроде React Native.",
      "type": "principle",
      "actionable": "При выборе архитектуры мобильного приложения учитывать, что агентная разработка снижает издержки дублирования нативного кода, и пересчитывать ROI кросс-платформенных решений с поправкой на этот фактор."
    },
    {
      "claim": "Рекламируемый инструмент Graptile T-Rex позиционируется как ревью-агент, который реально запускает код в изолированных песочницах и тестирует UI кликами, а не просто статически читает диффы.",
      "type": "tool-caveat",
      "actionable": "При выборе code-review агента для своего пайплайна проверять, выполняет ли он код в реальной среде (sandbox-exec), а не ограничивается синтаксическим/семантическим анализом текста — это ловит баги, невидимые при чистом чтении кода."
    }
  ]
}
```
