---
session: s_bc0079d3
date: 2026-09-29
words: 1858
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_bc0079d3` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Opus 5.5, GPT-6 Sol, GPT-6 Luna, MiMo v2.6, Grok 4.7....
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Shall we start? Sup nerds. Happy Wednesday. Been a bit streaming as much. Everything's been chaos lately. Did I fix my audio delay? Opus didn't. I did. But also, uh, GPT56 Soul told me to spend another $1,700 on audio interfaces, so I did that, too. Hopefully, the sync's better now. That work aligned properly. I got the clip buttons. Why did that go there? I'm confused. One sec. annoying. Um, I close that. Yeah, audio. I screwed up. I hit the wrong pedal. I just want to grab info on this without doxing myself over my Amazon. Um, it is it Twitch or YouTube chat paused. Oh, cool. There we go. I got the R audio Fireface UCX2. I I knew RM had good Windows drivers, and that's like the big thing that I care about at this point. So now I have a thing that has good Windows drivers. Yay. I'm excited. I really need something a bit more stable, so I will pay too much money accordingly. Thank you all. Sorry, I was uh figuring out plans for a concert, well, a festival this weekend in SF Portola. Anyways, let me thank everybody I missed while we were getting ready here. Uh yeah, first we got Crazy Phillip with the Prime. Thank you for that. Catgirl Mo with the three months. So many models this week. What's next? Google makes a new model or a good model. You Thank you for the support. We got Hanzy with the gift to Squid. Thank you for that. Dope Programmer with the tier one. Gabriel with the 51 months of tier three. Appreciate that. Good to see you, man. Hope you're doing well. Firebolt dude here with the two months. Been using T3 code so much recently. Just you'll upgrade to or v2. Very excited. Such an amazing product. [ __ ] yeah. Awesome. Voice sounds off. I'm a little tired and definitely a tiny bit sick, too. Hopefully, I will come back to life as we go. Usually that happens. Or is Swedish Mafia playing this year? Oh, yeah, they are. Good. It's the day I was planning on going anyways. Cool. I don't need to show up until pretty late on Sunday. And I don't think I'm going to bother Saturday. Like I do love Robin and Dog Blood though. H It is strange seeing Fat Boy, Slim, and Soul Wax on the smaller stage and Robin on the bigger one. But I get it. I know who they're trying to attract. Should be fun. Did I get a haircut finally? No. I just decided to spend more time trying to style my hair with one hand today and actually somewhat succeeded. Oh, do I not follow you on Twitter as John? What's your handle? I'll follow you back so I actually get your DMs. Oh yeah, I found your star mini. There you go. Cool. Sorry, responded a bunch of things. Back to thanking subs. There's too much going on. Mellow Yellow the prime for eight months. Thank you for that. Sky Lurker with the 36 months of tier one 45 total. Shoe money with the giant gift. Is that 150 gift bomb? Jesus Christ. Now I can even scroll up in chat. Love it. Thank you so much for the support, man. Really, really appreciate it. We got Skyler with the sub. Captain Mexico with the 15 months. No good Nick with the year and a half at tier three. [ __ ] legend. 51 months total. Raging NB with the prime. Grim with the five bomb. Thank you for that. So, Broki plus user. You know, Soul's become usable in the plus plan, but it's also become the dumbest model you've seen on Earth. Looking at Opus 55, how realistic is it to switch over to the Broki plan at Claude? I don't know how the $20 plans work for any of these. I don't have any $20 plans right now, so I just I don't know what the usage looks like. Yeah. Thank you again, Shoe Money, for the giant gift bomb. You got your shoe money Twitter back. Thank Congrats, man. I had nothing to do with it, but I'm happy that you got it back. Good [ __ ] Gamergirl with the 30 months. Appreciate that. You put yourself out of your current p projects taking a sbatical from programming. That is totally understandable. I think I inadvertently started doing that the last few days because I'm just pretty dead. Audio interface enthusiast gift from hay bales. Love that. Thomas Swagerty with the three months. Thank you. Bent Signal with the 13. Edmund Limban with the three months as well. Jamie, good to see you, man. Hope you're doing well. 10 community subs. Appreciate the gifts as well. It's just my voice. I uh definitely have a bit of a cold, so my voice is a little beat up. It probably was or you could probably hear it in the last two videos I did as well. Was considering taking the day off, but I we need to film. We got patchep here with the four months of support. Thank you for that again. Shoe money with a gigantic gift. Gusty sent me this link. I was wondering if you had a chance to look at it. 15y old developer. Gusty, you're 15. You don't need to be throwing that much in a cheer. Oh, is this a a survey? You know what? I'll pin this for a minute if people want to do it quick. I'll blast through this. Why not? You're a good kid. Stop paying for a decide against buying software. You build the functionality yourself with AI. Eh, once or twice. Another month app does one relatively simple job. If you need a coding, you should build a simple replacement for you. Which would you choose? This is too vague in my opinion. Like it depends so much on the specific thing, but I also like no there's a lot of layers to this one. Specifically like as soon as I want a mobile app too that fundamentally changes things, but I would say if it takes less than 30 minutes, I'd probably just throw it together. What would make you continue paying for software even if you could reproduce functionality yourself? Um network effect maintenance support pretty dead content not really security eh integrations user experience something else mobile hey coding tools change how much software I pay I definitely spend more do you encounter a new page utility or SAS pretty much Whatever. And got a mold. Cool. Committed. There you go. Anyways, what do we got next here? We got Quan 2M2 with the prime. Thank you for that. Think he's going to do that's probably d
...[middle elided]...
e for the cloud site and desktop app three times faster because the systems you build to verify the changes are just as important as the system itself because the systems you build to verify these changes are just as important as the raw source code itself. Hopefully this video will help you maximize your usage of Opus 5.5. It really is a great model and the more you trust it, the more you give it the things it needs to trust its own work, the further it can go and the more you can build. I hope this was helpful and until next time, peace nerds. Also, don't do not touch max mode. Seriously, it's so bad. Cool. Yay. marker end of opus 55 guide. Cool. Move that there. I would say this is slightly higher priority than the what pacing looks like. Cool. Thank you, Hila, for the prime sub. Appreciate that. Uh, V coding monster for the tier three and agent 13 number one. Appreciate you as well. Did I miss anybody on YouTube chat? I didn't. Yeah, I'll I'll do the Soul and Luna stuff in a bit. I just I I want to give the models their deserved time and I just haven't had the time to really test them and I didn't want to do that on stream. So, I'll hopefully test some more tonight and film that video tomorrow if all goes well. Let's figure out who we're raiding because it is 900 p.m. I've been going for five and a half hours and I want to eat because my food just got here. Oh [ __ ] Tee is live. He's only been up for an hour. Perfect. We are raiding Tee. Have fun nerds. always appreciate y'all for hanging out. Thanks for the fun Wednesday stream. Might not be live this weekend because of the events and stuff I'm going to, but uh should still be filming a couple additional videos offline, so keep an eye on the channel. Got a lot of fun stuff happening there. Appreciate all you guys for showing up. Sorry I was more neglectful than usual YouTube chat. It's because YouTube chat has gotten more and more broken over time. Appreciate y'all. So long and goodbye to YouTube chat as well.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "agentic-coding",
  "signal": 0.12,
  "novelty": 0.15,
  "actionability": 0.15,
  "evidence": 0.1,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это в основном стрим-болтовня (донаты, подписчики, личные планы), с перечислением новых моделей без конкретики и одной обрывочной мыслью про важность систем верификации кода в конце.",
  "knowledge_units": [
    {
      "claim": "Системы, которыми ты проверяешь изменения кода (тесты/верификация), так же важны, как сам код, особенно при работе с агентными моделями типа Opus 5.5",
      "type": "principle",
      "actionable": "Инвестируй в надёжный слой проверки (тесты, ревью-пайплайны) прежде чем доверять модели больше автономии в правках кода"
    }
  ]
}
```
