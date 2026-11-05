---
session: s_2823913a
date: 2026-10-01
words: 1916
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2823913a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: I'm having a rough time with Astra
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
I think I'm as good as I'm going to get here. Shall we? Hence. I just realized I have no idea how that device is working. Huh? Sup nerds. Happy Friday. Been chaos. I will not lie. Good to see you guys. How is my hand? Rough, but maybe healing. Uh, yeah. If you can do the Discord notification, I'd appreciate that. No worries at all, SJ. This has been an insane week for me and the sheer volume of tech problems I had even just now trying to go live. I moved over to the mix pre. I'm not sure if you guys can hear a difference. I hope you can't, but if you can, I hope it's good. It has been rough, but hopefully hopefully my audio will be stable now. That'll be a bigger stress relief than my hand. Honestly, I couldn't get the return feed working well on it. So, my headphones are still going through the road cer, which scares me, which means I'll also be relying on you guys a lot to let me know if there are audio problems because I won't be able to hear it even if I have the headphones on. So, yeah, going to do our best. We're going to keep our fingers crossed and we're going to hope that my problems finally end. Hair problems addressed tomorrow. Not yet. Tomorrow. Fingers crossed. Next stream. It'll be automated. Awesome. Did we send one out for this stream? Awesome. Thank you, Exotic. Appreciate you a ton, man. Let me get the pop out here and pause that to save bandwidth. Love that YouTube chat. Love all the novel ways that YouTube Studio breaks every time I have to open it for live. No audio problem so far. That's good to hear. It sounds fairly different. It It almost certainly does because none of the processing is overlapping the previous processing. I Codeex and I did our best to match the Roadcaster settings with filters in OBS directly. So, no more hardware processing. Benefits and negatives. You have to turn me up. My my level should be the same. Like when I look, it's actually a tiny bit louder than it was. I was going to turn it down very slightly, and I still think I'm going to. Yeah, I'm definitely a little bit congested, which is not helping. If it sounds more layered, that's because it's a nicer mic setup. Like, it's a I went from a $700 interface with four inputs and a bunch of features I didn't need to a $1,500 interface with three inputs in quotes and missing twothirds of the features I need. But it's much higher end. I saw What is this? um as director of killing people. Hilarious. Cool. Um sounds more close miked. Uh, it could be the congestion, but hard to know for sure. I used it for my last video and the team said it sounded fine. So hopefully, fingers crossed, it'll be okay. If it was bad enough, somebody would have complained by now. The interface is the Mix Pre3v2. not cheap and I've been sitting on it for a while. We'll be talking a bit about this today, Louis, on CPP. It's not going to be specifically about the $20 tier. It's going to be more focused on how bigger models do benefit you, even if you're doing simple work. Yeah, DHH and I have been talking more. He seems to mean well right now and has shut up about his less great politically opinions and is more focused on open source and open source funding. I feel like people have been too pessimistic towards his goals there. Like I have no reason to distrust his goals in open source. Like that's a dude who has made his money and had his influence. He just wants to make sure Apple isn't the only place devs can go and wants an operating system that agents can have a bit more control of and operate within. And I think that's all fine. I actually am quite in favor of it. And to have people whose opinions couldn't be more different on most things, kind of fighting together for this is valuable. And more importantly, the maintainers of Omar are [ __ ] awesome. We've been working with Ryan a bit on T3 Code stuff and he has been really genuinely cool to work with. And I think he's probably the one who really caused this to happen because he was using T3 code and shared it with the rest of the Omari team and they've all been loving it and now we're bundled. Yeah. And they're putting a lot of money and investment into M series support for Apple Silicon which is cool because I have some old M. Actually, do I have any M1 or M2 still? I have one M3 Air. I don't know if I have any M1 or M2 machines anymore. The M1 Air is my favorite computer of all time. I miss it so much. What I would give for either the M1 Air with a 120 Hz screen and a better chip or ideally the return of the 12-in MacBook. A 12-in MacBook is my favorite design of a computer ever, but it was also the M1 MacBook. God, I want that so bad. The M2 Air was fine, but it wasn't a revolution in computers. It didn't like like the M1 Air changed how I thought about computers. And the hard harsh reality I had I think I had this realization a few days ago. I think it was cuz I was talking to like [ФАМИЛИЯ] YC founders and I realized a lot of you guys are Brasov enough that you've never had an Intel Mac. Certainly almost none of you had a Power PC Mac, but I'm almost certain none of you had an Intel Mac. And none of you understand the like like the generational gap, multigenerational gap from the maxed out 16in Intel MacBook Pro that I paid like five grand for. 6 months later, I grabbed the tiny M1 Air base tier. I bumped to 16 gigs of RAM for like 1,200 bucks and it was faster and better in literally every single way from my $5,000 computer I bought just a few months prior that that changed everything. And I don't I still genuinely don't feel like most people understand even the ones who were there just how big a jump that was. Yeah, it was it was in one release Apple computers went from some of the worst options, terrible value, just not good to the actual best value computers around. Interesting. I saw this got released. Not sure if I want to do a video on this cuz it's a long read. I'm going to want to read it first. I did end up canceling my travel that was coming up becaus
...[middle elided]...
u're signed in with Codeex and the caches for the thread you're in and that thread has one user you there. Then all of a sudden you don't need to fan out the cache, right? So my conspiracy theory here is that over API, OpenAI always has to send the cache data everywhere, but over your signed in state in codeex, there's only one connection that can hit that, which means you don't have to fan out. And I'm also sure that OpenAI was looking at their cash stack because their cash read pricing didn't get cut the way anthropics did. and they don't like when Anthropic finds a optimization they haven't. So while they were auditing, I bet they noticed a lot of the cache reads only hit that cache entity once and then they have to rewrite it with the additional data. So they realized it was only being read once. There's no reason to fan it out. It you get it. Or level cache has to be distributed to multiple data centers, but signed in user cache doesn't. Where did I have the Eureka for this one? Sitting at my desk downstairs after stream on Monday, overthinking that post and then it came to me and I very poorly tried to explain to Julius and Ben and each of them misunderstood the opposite way. So when I tried to clarify for one, the other got more confused. It was a good practice run and this is another practice run. So, now that I know this well enough, I could possibly make it a real conspiracy. I've been trying my hardest to get anyone at OpenAI to confirm, and they won't, which usually means I'm right. Yeah. Why the [ __ ] is the JavaScript YouTuber the only person who allegedly has been able to figure out what the [ __ ] this is? Yeah. Anyways, let's get you guys raided. I'm going to go have drinks and chill. This was a fun ending. Hopefully, Shindigs is still alive. Oh no, Shindigs raided someone else. [ __ ] We got to find someone else now. Good thing I didn't raid him before. Atriarch. He could be fun. Let's raid with Atriarch. Goodbye nerds. Goodbye to YouTube as well.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "stream-chatter-llm-caching-speculation",
  "signal": 0.12,
  "novelty": 0.25,
  "actionability": 0.08,
  "evidence": 0.08,
  "durability": 0.15,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это почти целиком бытовой трёп стримера про железо, самочувствие и Mac-ностальгию; единственная техническая мысль — неподтверждённая личная теория про кэш OpenAI, которую сам автор не смог верифицировать.",
  "knowledge_units": [
    {
      "claim": "Автор выдвигает недоказанную гипотезу: в OpenAI Codex при работе через залогиненный аккаунт (один пользователь = одно соединение) кэш промпта не нужно 'расфанивать' по дата-центрам, в отличие от доступа через API, где кэш всегда реплицируется везде — это якобы объясняет, почему OpenAI не снижал цену на чтение кэша так, как Anthropic",
      "type": "tool-caveat",
      "actionable": "Не принимать как факт: это личная спекуляция без подтверждения от OpenAI, автор прямо говорит, что не смог её верифицировать — не стоит закладывать архитектурные решения на основе этой теории"
    }
  ]
}
```
