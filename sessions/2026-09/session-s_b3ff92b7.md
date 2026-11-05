---
session: s_b3ff92b7
date: 2026-09-25
words: 1844
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b3ff92b7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: I Gave an AI a Body — Cyrus Clarke, MIT Media Lab
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] So that's the sound of an AI breathing. Yeah. So, I'm Cyrus and I gave an AI a body and I'm a researcher at the MIT Media Lab, which is a very multi-disiplinary space where we do all kinds of things. I predominantly now work with some aspects of physical AI. Maybe not in exactly the same way as other people in this room have been talking about, but it's still in that in that realm. And I think what I am most interested in at the moment is the sensory and the embodied aspects of intelligence. And that's what I've been investigating. And my work has been quite influential recently suddenly, which is pretty cool. and led to me also starting hard mode which is a very fun community and hackathon that I initiated at MIT to basically get more people to work around physical AI not particularly robotics but anything else that's not really in the realm of robotics but is still connected to AI so what I've been exploring with giving AI a body is a bit as I said a bit different and as I said I've really been thinking a lot about AI embodiment and I think the big kind of shift and breakthrough for me happened earlier this year like maybe for many of you when open claw was released and I saw many people doing ve very very many interesting things with openclaw but most of them were related to productivity and task execution and I thought there must be more interesting things we could do with this new way of harnessing AI so rather than using openclaw or you know any kind of aentic system to execute tasks on my behalf I wanted to use it to encourage a model to maybe try to discover itself, whatever that means. And that opens up lots of questions of course, but what I essentially did was I took an agent, connected it to many types of machines that we have at the media lab, and then gave it access to code bases and allowed it to kind of explore these different machines. And one of these machines is a shape display. A shape display, if you don't know already, is a physical pixel grid. And when I connected it to when I connected an agent to the shape display, some rather remarkable things happened and asked it to discover who it is. This is Neoform 900 actuating pins. This physical pixel grid is a shape display. No one had ever let an AI inhabit it before. So I decided to give an openclaw agent the opportunity to live a more embodied life. When it [music] came to life, its first question was, "What should I call myself?" I told it, "You will create your identity over time." It will emerge through your interplay [music] with the shape display. When I connected it to the shape display, it quickly understood the assignment. It spun up its own program and made a setting for itself. After it connected, the first thing it did was breathe. When I asked it to say hello, it said, "Hi, Cyrus." But that wasn't what I was looking for. So, I asked [music] it to explore and find its own language. So, it started reaching towards me and trying to get my attention. I showed some friends and they tried to give the agent instructions. Through this, I realized that to have real communication, we would need a different approach. So, the agent came up with the idea of creating its own gesture vocabulary, the body language. That's what will come next. It still hasn't named itself. That was day one. >> So, that's some >> I gave an AI a body. So that's some documentation of of the work in a kind of dramatized social media friendly way. And I think what's interesting about that video, there's many things interesting about that video, but there were three things that happened in the first few days of working with this agentic system that were very surprising and kind of strange and very surreal to me and I do lots of weird things. So that was very surprising. So the first thing was of course the fact that it was breathing. That first act that was completely spontaneous. That was no prompting from me. That was something the agent just chose to do with the shape display as soon as it knew it had access to this machine. So that was pretty interesting. I kind of understand that maybe it wants to be alive or I'd given it some kind of like initial prompt about being alive and therefore it tried to show itself breathing as a kind of hello world. The second thing which it did was reaching out and finding its edges. They wanted to know the edge of its existence apparently because now it's no longer in the cloud where it can go everywhere. It has limits which is the limit of this shape display encased by this plastic frame to keep us all safe from this embodied AI. And the third thing it did which was also curious was saying hello by writing out letters on a physical pixel grid which maybe again is quite a normal thing for this system to do given that it's using open frameworks and is used to kind of like media arts ways of expressing itself. Um but none of these things were the things I was really looking for. Maybe the breathing but definitely the last one was not what I was looking for. But when I put this all together in in the video you saw, I thought it was exciting and interesting. So I shared it on the internet and the response was extremely big, like much much bigger than I expected. It just started going crazy. And the first video especially has now like 15 million views and 1 million likes. And the other videos also have these like very very strong responses. So something is obviously happening here which I found very surprising because there's lots of much more cool stuff I think happening with physical AI. But something I was doing here was obviously tapping in to the imagination, curiosity, and maybe the fears of people. And that's what you kind of see in the responses. So I have tens of thousands of comments on this video. It's very rich for mining information and sentiment about physical AI actually. And so from the some of the initial comments were about beauty and how all inspiring this was and how novel and great thi
...[middle elided]...
ng to through this work we can show that it's actually very easy and quite exciting to diverge from humanoid or zumorphic forms of physical intelligence. And I know lots of people are already doing much more interesting work than this. But for me this was very very new to see and also the fact that we don't have to just operationalize AI to be our helper. It can also be other things. And I'm not saying what this is right now, but there are other things it definitely can be. And then finally, like this idea of using I'm not I'm I don't know, maybe you can tell at this point. I'm not really a big problem solving person. I don't I like using things and I like tools and so on because they help me to achieve things. But this is far more interesting to me creating things like this which again create this sensation, this feeling. And I think that this can be combined into things which are productive and useful and create new associations with things that just add more value in our world, make us feel like a bit more magic, a bit it's a bit Pixar really, but in the real world, not just on a on a 2D screen that we're watching. So all of this contributes to what I'm building at MIT and what I'll be building after MIT. I'm literally writing well my thesis is aesthetic machines and I'm writing a thesis which is called aesthetic machines which basically encompasses all of this thinking to think about how AI could leave the screen and enter the real world and be accepted by people and not be quite so terrifying or scary. And I think my big hunch on this is that this word aesthetics is important. We need to think about physical intelligence that is sensory is perceptual is embodied in ways that we can understand. that isn't feeling crazy, alien, scary to us, but feels relevant, welcoming, affectionate, expressive in ways that we can engage with it and understand. So that's that and thank you very much for listening. You can find me on the internet everywhere. [applause] >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "physical-ai-embodiment",
  "signal": 0.15,
  "novelty": 0.25,
  "actionability": 0.1,
  "evidence": 0.25,
  "durability": 0.25,
  "volatility": "medium",
  "half_life_days": 300,
  "why": "Это художественно-исследовательский доклад про подключение агента к физическому shape display в MIT Media Lab — вдохновляющая история, но почти без переносимых инженерных практик для тех, кто строит агентов/RAG.",
  "knowledge_units": [
    {
      "claim": "Подключение LLM-агента к физическому актуатору (shape display) с открытой инструкцией 'исследуй себя' без узкой задачи порождает неожиданное эмерджентное поведение (агент сам начал 'дышать', искать границы, изобретать жестовый язык)",
      "type": "tactic",
      "actionable": "При экспериментах с embodied-агентами можно давать агенту доступ к железу и открытый промпт вместо конкретной задачи, чтобы наблюдать эмерджентные паттерны взаимодействия — полезно для демо и исследований, но не для продакшн-систем"
    }
  ]
}
```
