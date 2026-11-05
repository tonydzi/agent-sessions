---
session: s_a66bd351
date: 2026-09-30
words: 1910
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a66bd351` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The first "typesafe" model?? Let's talk about Jev
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
And now for my favorite game. How much of my [ __ ] is broken today? Let's see. Cool. That appears to be working. I also just realized I forgot things already, which is great. So, I'll be right back. Sorry. I have what I forgot my new phone that I will be able to use in between 1 and 7 hours depending on how long it takes Apple to do the transfer. This time I'm not muted. Don't gaslight me like that. Yeah, that's going to take forever. Yeah, I got the matte black cuz mine's going to like once the Duo is out, the purpose of my Pro is just a portable like travel camera almost entirely. Will I have to jump through hoops to have it accept my own software? Yep, I've already had to jump through hoops even to get it to accept its own software. We're not going to get an iPhone review during stream because my iPhone won't be working yet during the stream. Flop site to apologize. What for? This looks too much like it's going to be a crypto thing, which immediately gets my Spidey senses in a not great way. New laptop. How did you know I got another laptop? I've done nothing to indicate that I have another laptop. I'm not using the different laptop. I have another laptop downstairs, but that's a problem for later. either code web UI is getting slower. Um, if you can find like examples or ways to measure it, let me know. Hey, I I haven't seen this and I can't I can't check things on my phone because I don't have a phone right now and I don't want to open my DMs on stream because stream. But yeah, I I did see actually I got a DM from uh Talon today. Never I responded to them. I never got anything back. I'll blur. Yo, Will, good to see you. Um Let me find this quick. floor is a little unsafe, but it's such high effort for things that aren't that important. Like the things I was checking there, like if they did leak, it's fine. It's just tough. Yo, thank you for the super chat, Marushia Dark. Many artists blanket oppose all AI without nuance, saying slop is anything AI even looks at. They claim it's soulless, inhumane, steals IP, etc. Can I make a video addressing those types of concerns? I got just the video for you, Marishia. AI sucks at art still. I did this video 9 months ago and it very clearly describes the exact distinction that you're referring to here. the how do I even put this? Like AI art is just so obviously different and I wish people the issue is like AI art is way more visible than AI code. So, you're going to see it much more. And if you don't understand code or any of those things, you're going to see the art and get mad. The the way I explain this to normalish people that like kind of get the tech side is that as LLMs get better, we read a smaller percentage of the text. God, what the [ __ ] YouTube, what are you even doing? Yeah. What like the question I would ask first is what percentage of generated text do you think we actually read as humans? Like if let's say hypothetically we generate a billion tokens a year. It's obviously way way more than that. But what percentage of those tokens are ever consumed by a human? So I got to switch back to Zen so we can see Twitch chat. Not even 1% 0.00001 that something like that. It's way below 1%. It's a very very low percentage 3 years ago. Was that percentage higher or lower? Yeah, because remember reasoning we're not even seeing the reasoning tokens higher. It was obviously way higher before. Are LLM's more or less valuable now than they were three years ago? So, and obviously we're generating way more tokens. So, there's a a clear pattern here. The number of tokens being generated goes up. The amount of value we get from those tokens being generated goes up. The amount of tokens being generated goes up. But the amount that we are reading goes down, not as a total number, but as a percentage. And this is what's so cool. As the amount of tokens we generate goes up, we don't have to keep pace with the amount we read and we still get value. The percentage goes down, the value goes up. And we agree there is value to tokens that are never read, right? Like if you generate code and never read it, that's useful. If reasoning helped the answer be better and we never saw it, it's useful. There is a lot of use to the 99.99% of tokens that we never see, right? It's like obvious we get a lot of value out of those tokens. Here's where the hook comes in. What value is there in an image that is generated and never seen? What value is there in a video that is generated and never watched? What value is there in a song that is generated and never listened to? If we can't get value out of the generated media that isn't being consumed by a human, then the exponential doesn't exist. There is this beautiful exponential with LLMs where the amount we consume does not have to change and the amount we generate still goes up and the amount of value we get still goes up. With media genen, there is no value in increasing the amount of media genen on an exponential simply because we're not going to meaningfully increase how much media we consume. I will consume a hundred times more tokens next year than I did this year. I will consume a similar amount of video. I will consume a similar amount of like photos and music and all these other things. Maybe best case, I consume twice as much media. I'll consume 100x the tokens. This is not just true because of code. This is true because of the concept of agents. This is true because of reasoning. This is true because of all the other things we use tokens for that are not just reading outputs. Mondays, where do you send that? Cuz I can't open iMessage on here and my phone is being swapped so I can't use my phone at all. I did hear that Gemini made it to Felony Bench Discord. Cool. Uh, accepted. Now I'm just going to do the stream announcement. Oh no, it worked. The bot worked. Yay. Thank you, Exotic. Appreciate you making my life easier. What about custom video generation like for video games and eventually personalized shows?
...[middle elided]...
with the things I'm saying. All I'm saying is that you would never have been able to do that with GBT5, not because it was so much cheaper, but because you just wouldn't be able to get that much work done. Productivity is what we're kind of LM spend is tied to the productivity we get from LMS. And yes, we are getting more from that. Thank all I have to on this one. I hope you can better understand where our money is going now. We're using it to spend. And don't worry, things will continue to get cheaper, even if it doesn't look like it right now. Keep your head up and be excited for all the developments that'll continue to make models cheaper and more capable. I know I've been hyped about this and I hope you are, too. Until next time, peace, nerds. Yay. Yeah, we all I think I thought it more than others. Not drinking stream. It's 8:30 p.m. I need to go eat. I haven't eaten today. Anthony, did we ever get what you meant? I'm still so curious what the [ __ ] you think you were talking about with a context engine to copy and paste. It's rare slop makes me so curious, but your slop did. Thank you to Sonia again for the sub. Anybody on YouTube I missed? Nope. Cool. Where are we raiding? I missed the Shindigs raid last time because he ended right as I was raiding him. So, we probably got to raid him. Oh, yeah. Podcast. [ __ ] Yeah, that's what we're raiding. My bad. We just have nerd snipe. What's the handle on YouTube? Nope. Nerd dashnipe. I'm stupid. Cool. Videos. Come on, YouTube. Here we are. Welcome back, nerds. Yeah, new podcast episode. Go watch. It's a fun one. One of the more like chill back and forth we've had in a while. Go watch the podcast. It's a good one. Thank you all for hanging. Not sure when I'll be back. I definitely need to stream more this weekend because I'm so behind on video. So, I'll do my best to be live soonish. Happy you all come by. Appreciate each and every one of you guys. Enjoy the podcast. Good night, nerds. Going to go play my new phone.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "token-generation-value",
  "signal": 0.15,
  "novelty": 0.25,
  "actionability": 0.05,
  "evidence": 0.1,
  "durability": 0.35,
  "volatility": "medium",
  "half_life_days": 270,
  "why": "Это стрим с личной болтовнёй и почти без техники — единственный содержательный кусок это философский тезис Тео о том, что ценность LLM растёт даже когда люди читают всё меньший процент сгенерированных токенов, а с картинками/видео/музыкой такого эффекта нет, но это голая рассуждательная гипотеза без доказательств и без применимого действия.",
  "knowledge_units": [
    {
      "claim": "Ценность текстовых токенов LLM растёт даже когда доля токенов, реально прочитанных человеком, падает (агенты, reasoning, код читаются не построчно), а у сгенерированных медиа (фото/видео/музыка) аналогичного эффекта нет, потому что непотреблённый медиафайл ценности не создаёт.",
      "type": "principle",
      "actionable": "Не переносить логику масштабирования 'больше generation = больше value' с текстовых LLM-продуктов на продукты генерации медиа при планировании продукта или инвестиций — там экономика другая."
    }
  ]
}
```
