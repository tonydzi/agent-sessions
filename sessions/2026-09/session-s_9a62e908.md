---
session: s_9a62e908
date: 2026-09-19
words: 1762
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-19 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_9a62e908` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Search Engine for the Agentic Web — Will Bryk, Exa
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] How's everybody doing? Good. All right. Pretty crazy times we live in. Oh, my microphone. Um, okay. I am very excited to tell you all about perfect search built for AI agents. Uh, and I'm going to say a lot of crazy things in this talk, so bear with me. uh they are all true and I will tell you what is exa uh the story of exa so how we got here and then where we're going okay cool if you take away anything from this talk it is this uh slide uh this is showing web searches per day over the past 30 years uh from humans and AIS obviously it was all humans until around uh 2020s and now we're in 2026 and actually this year we expect the number of searches from AI systems to exceed that of humans. Pretty crazy. And then in the next few years, it should be a thousand times more. So AI, AI systems, AI products, whatever AI system you use, sum together will will search a thousand times more than humans. That's pretty uh pretty crazy world that that we're getting into. And the entire ecosystem of search is changing because of it. So Exa is the search engine for AI agents. You know, we were the first ones to be like we were the first search engine for AI and now things are getting uh kind of wild. uh we now serve over 5,000 companies over 400,000 developers. I see some customers in the audience. Uh we serve you know very diverse set of agents from coding agents like cursor. So if you use cursor at some point the cursor agent decides to search for the latest technical documentation or the news it'll be using ex under the hood. We serve go to market agents like HubSpot. So uh we help uh their users get you know really high quality lists of companies to sell to. We serve all sorts of financial agents. Uh I was in New York a few weeks ago and pretty much everyone there is now building financial agents and they need the best financial data. Um yeah and really just a huge diversity of agents from uh from labs to to to YC startups. Okay, but how do we get here? So what's the why of EXO that to me that's always been the most important and there are a lot of ways to say the problem but the short way is just misinformed anarchy. This is what we're trying to avoid. We want to create the opposite of this. Uh so what what does this mean? Well, this is the internet or it's a visual depiction of the internet. You know, you got a bunch of pages, you got blog posts, you got company websites, you got images, you got tweets, you got all sorts of things. Uh, and the web is really really big, right? This is showing a few thousand pages. The web is, you know, on the order of a trillion pages. So, uh, you know, a million times bigger than this. And it contains a huge amount of the world's information. Uh and that means that you know if this is just readily available you could find if you could go to any link and just get all the world's information then I'm sure we all walk around with like deep understanding of everything right obviously not uh it's messy uh and so uh it's crazy and it can't fit in our heads. So we need information tools that could help synthesize this or filter it into the the things you need to know. And you know we have a tool called Google and it's a pretty solid tool. It could get you things like the Costco homepage or information about Taylor Swift or whatever you want to search, but it's not perfect, right? And I love this example where you type shirts without stripes. Uh, and if you notice, you get shirts with stripes. Why is it doing that? Well, it's not it's not trying to be a database of the world's information that gives you exactly what you want. It's kind of like a recommendation engine. Um, and you can see this with more examples. Um, so find me everyone in Singapore who works on AI search and any blog post or research paper they've written. I bet you've never typed in anything like this to Google because you know it's not going to work, right? you're going to get like uh links and documents that contain some of those words, but not like actually a database result of all, you know, 412 people who match and and it gets pretty serious, right? Like I'm a citizen. I'm trying to be informed about what's going on in the world. I want to find the most important US news across all media or, you know, US news articles, whatever it is. You just don't trust Google to give you that, right? It's just going to get it's just going to recommend some things. It's it's almost akin to like social media in the sense. It's kind of like a recommendation engine. Okay. So that means that no one really has a complete understanding of anything. I actually when I walk around like SF or wherever I'm walking around, I see people I often think like no one knows what's going on in the world. Everyone's like this. Uh including myself, you know. Uh you could imagine uh this person on the right on their phone like trying to find a new job. They're looking for biotech companies to work for. Uh are they going to get like all the possible biotech companies that match? No. Uh so there there's always going to be like this unknown of what's out there. or uh you know maybe this other person with the headphones uh maybe they're trying to yeah try they want to understand what's going on uh in in in in in some region of the world they're just not going to have a deep understanding they can't not only can they not find the information they might not be able to trust the information so we basically are in a world where we live without this like key information infrastructure that is so critical and I think this is extremely important so important that if we don't fix this problem I believe we get a world that looks like this a dystopia I'm not kidding uh this is AI generated uh version of San San Francisco in 2035. Um, and it's basically a world where no one no person really understands what's going on. If people don't understand what's going on, then as we have this crazy AI technology that we all are talking about today that
...[middle elided]...
ld love for you know the entire world to have access to nearperfect information so that everyone is very informed going into that election you kind of can feel the gravity >> [laughter] >> of what we're doing here of of perfect information. I encourage others to try to do it too. Um it's very important for the world. It's like key information. It's key infrastructure. And yeah, you have to like that that slide I showed at the beginning, it's not the whole picture, right? If you play it out, we're talking a thousand times more searches from AI systems than humans. This you can't even capture that on a graph. Like this is not that's like 20 times a thousand times be all the way up there like top of a building or something, right? So it's crazy what's coming and it's really happening. Um basically like you know humans on average search a few times a day on Google but when everyone has you know AI assistants and every software product you use has AIs in it every interaction you're doing it's going to be grounding itself in in search so it's going to be a huge number of searches and if each of those searches are you know as as true as possible as near perfect uh then then then the world looks like this in 2035. Um yeah I I do think that if I do think we're basically our our future is limited by ourselves. Like we're basically getting into a world where our technology is so good. It's really just a matter of like can we coordinate and just decide together that like on sensible things, right? Like if you look at San Francisco, there's amazing things happening here and there's really stupid things happening here at the same time. Like that's that's just coordination problems and coordination comes from the information we consume. Uh so that's what we're working on. You all have a role to play in also getting to this world. Uh so thank you all for for for working on whatever passion you're working on and thanks for listening to me. All right. Thank you. [applause] >> [music]

---

**Claude:**

You've hit your weekly limit · resets 4am (Europe/London)
