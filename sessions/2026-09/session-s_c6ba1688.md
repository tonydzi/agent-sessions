---
session: s_c6ba1688
date: 2026-09-22
words: 1863
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c6ba1688` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Why We Made Jev — Diogo Almeida, TypeSafe Co-founder & CEO
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
Like how can AI be so unbelievably smart? How can we like solve millennium prize problems in math but still not automate even the most basics of works like like really basic wrote stuff but we have this like supercharged engine of automation that just does not have like the right plugs and stuff to plug into all of this economically valuable work and you know like if the whole company of type safe disappears like maybe it'll take like a year or two for people to like truly catch up. I actually don't know how long it'll take. If if model quality matters, then we are going to be in a very good position for a long time, but um it it like it it's done, right? Like there like this has changed the path of like technological history. Before we get into today's episode, I just have a small message for listeners. Thank you. We would not be able to bring you the AI engineering, science, and entertainment content that you so clearly want if you didn't choose to also click in and tune into our content. We've been approached by sponsors on an almost daily basis. But fortunately, enough of you actually subscribe to us to keep all this sustainable without ads and we want to keep it that way. But I just have one favor to ask all of you. The single most powerful, completely free thing you can do is to click that subscribe button. It's the only thing I'll ever ask of you. And it means absolutely everything to me and my team that work so hard to bring in space to you each and every week. If you do it, I promise you we'll never stop working to make the show even better. Now, let's get into it. Okay, we're in the studio, a special occasion because this week, uh, Diego, my my good buddy, uh, launched Jev and it's been taking over the complete timeline. Uh, how do you feel? What what's it like to be you right now? >> Emotionally, um, never been worse. um like a I'm a ragged corpse of a person right now because there's so much going on and I'm like a technical CEO so I have like a lot of fires to fight but like mentally it's like I feel I I say this all the time and I've been saying this kind of for years in my overunder events like I feel like the entire AI field is like one of those like carnival house of mirrors and everyone is just insane. pain and saying the weirdest stuff that doesn't make sense. And it feels like for just this week like I I'm on a better in sync with reality and like oh people see it now. AI can be so much more than what was once thought and like yes we are going to make like like an AI based economic revolution is back on the table and um this is awesome you know this is  awesome. I'm so jazzed the developers get it. It's It's uh Yeah. And I want to show my internal gratitude to developers and >> I'm so jammed about the community and everything. It's so great. >> Yeah. You were saying yesterday that you decided to prioritize the down town hall and not a bunch of like you know VIP investor type people because you wanted to make sure that they are the people that you get get your most uh attention right. The engineers, the developers. >> Yeah. It felt a little like, oh man, I'm talking to like really important people right now. I probably shouldn't reveal who, but it feels a little bit dirty for me to uh I I'm like perhaps overly genuine in things. Like it feels like dirty if like in my gigantic calendar events of things to people to talk to. You know, the community isn't one of those, you know, and actually in my ideal world, it would be like community all the time. I was thinking, should I host a town hall while walking to your studio? And I'm like, nah, that's too crazy. Sure. >> Yeah. >> Well, you you guys have been hosting town halls on the Discord. Discord is now 100,000 people. Um your Twitter follow these stats. So, holy >> Your Twitter's blown up. Uh you know, it was it was really funny cuz like at AIE, you were like, "Follow me, please." And then you didn't like provide even your your handle. >> I'm a noob. I'm a noob. >> But no, but like that's like positive aura that like you don't know how to promote yourself. >> Someone like called me out when I posted like, "Holy we're all three trending trending topics." And then they're like, "That's a personal feed." Of course. Of course. To you. Yes. Because it's what you clicked on. Um, so, okay, let's uh Yeah. So, congrats on everything. We'll talk about more uh details as you have them, but let's for people who are like living it under a rock or just just once like the definitive thing. What is Jev? >> Let me think of a That's a hard one. Um, >> okay. And I'm happy to like reask if you want to. I'm happy to I'm happy to like just jam on it. I will say like the first thing that I'm relieved about with this question is now I don't have to answer that question to my parents anymore cuz Chad GPT can just explain it. >> Um so the way I see it is we need a new class of models. Um we're not attached to naming that class of models. Um are the most accurate name we've come up with is system one models. There will be reasons but it's there's a reason why we don't call them decision models because like they will be like system one is beyond that. That's all I can say. Um we didn't expect this to be our big launch. So we have stuff in the tank. Um >> you should have said low-key research preview. >> Um it's kind of was right. It kind of was. But um we so there's a class of models that we describe them as like machine native system one large programmable. I think these are is the class of models where the goal is for code to be the consumer. So um as opposed to um um pre-trained large language models which are meant for like autocomplete of the internet or RHF models like chatbot instruction following models which are meant to like reply to text um or RLVR it's in a weird gray area with RHF like these are meant to have things that directly are consumed by code hence the name type safe. So the thing we really really really want is to have like AI 
...[middle elided]...
 that that's a good sign of a culture. We're hiring like platform people, like people to like build out Jev everywhere. Like we are so much more sensitive to location because speed of light is more of a bottleneck, right? Like I'm so sad for the European users that we're only like three times as fast instead of like a 100 times as fast because like we don't have servers there right now. And that's insane, right? >> It's okay. Life in Europe goes a bit slower as well. It's okay. >> Wow. I can't believe you you said it, not me. Um or or everywhere, you know, like if if intelligence per second is a metric that matters, like we we'll want this all over the place. Like we care about like if they're a developer building on top of us, I care a lot about you. Um and we are hiring for people to keep building more like not just like the goal is not to just be like Jev as a company. The goal is to like ship more shapes of intelligence beyond that. So we are hiring people to like build those things too, you know, like we want to not just be like yeah like the one trick pony of like the simple model, but like I think that there's going to be like an AWS of like intelligence, you know, >> which is going to be you by the way, right? Yes. >> I mean like that's a direction I want to go down. It would be arrogant to say it will be me. Like we like I'm going to do anything I can to make sure that happens. Like I think that that's going to be so so cool, you know? Like we are playing with like system one intelligence right now. Imagine the layers, you know, like this is like the TCP of it. >> Yeah. Uh seven more layers to go and uh who who knows what else. I've also pitched temporal by the way. I don't know. We need to talk about temporal as layer eight out of the seven layers. Um but anyway, >> we can talk forever. You got to get back to work or sleep. Uh thank you for coming. >> Oh boy. Yeah. Cool. You're most welcome. It was a pleasure, man. >> So excited. So excited. My first time.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "typesafe-jev-launch",
  "signal": 0.15,
  "novelty": 0.2,
  "actionability": 0.05,
  "evidence": 0.1,
  "durability": 0.15,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это эмоциональное интервью-хайп по случаю запуска модели Jev от TypeSafe без конкретики: концепция «system one models» и «код как потребитель» упоминается, но не объясняется настолько, чтобы инженер мог что-то применить.",
  "knowledge_units": []
}
```
