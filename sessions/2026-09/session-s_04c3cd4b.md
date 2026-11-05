---
session: s_04c3cd4b
date: 2026-09-20
words: 1979
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_04c3cd4b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Half Life of Agent Infrastructure — Ben Kus, Box
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Hi everyone, I'm Ben Kuss. I'm CTO of Box and today I'm going to be talking about uh building for change and specifically around uh AI agents and how to continue to adapt uh your infrastructure as we are all in the middle of this journey. Um, so before I get too far, I will quickly sort of set a little bit of like who I am and uh sort of what I do. Um, for Box, I'm CTO and one of my jobs in my job for my whole career has been to build enterprise software. And so if today um you're from a consumer company or you're uh not involved in enterprise, I hope that a lot of it is still relevant. But in many cases um a lot of the lessons I've learned are enterprise uh specific. So um I sort of will highlight um when I'm thinking and talking about infrastructure when I'm talking about uh the kind of challenges that we face um I'm typically talking about things that are sort of in a scale of like uh like for box we have over an exabyte of data not a gigabyte not a terabyte not a pabyte but an exabyte um and then oftentimes we're I'm thinking in the tens of of millions of users uh the hundreds of billions of things in our case files or content or unstructured content um and then the new stat that is sort of the the one that we talk about is uh tokens. Um so we are now in the ballpark of trillion tokens probably will be 10 trillion tokens sometime soon. Um and this of course is uh uh some of the new and interesting challenges that this kind of scale brings. Um so in my career and um I think maybe many of us here um we've kind of lived through these this these technology changes. And so taking a quick step back um I started uh my career when the internet was sort of becoming a thing uh lived through mobile and sort of this idea of like you know carrying these different devices move to the cloud where you could kind of store and maintain all your data and then of course we're all in the middle of this AI change and I think when you see these kind of technology disruptions when you're sort of thinking about this idea of like all of these kind of have changed all of our lives um and then uh and you're thinking about it from the perspective of a technology leader or a startup or a engineer. Um, you kind of see that like these are where like major companies are born. Um, you see that like big companies adapt or die. Um, small companies are here to disrupt things. They're here to take bets. They're here to grow. Um, I've had two startups. I've been acquired twice. Once in IBM, once in a box. Um, and um, so that we're in the middle of this kind of major opportunity. Um but for um a long tu uh no matter what you kind of come from and what area you're at I uh t typically if you were to ask my advice um and about kind of what makes it you successful as an company as an engineering organization as a technology startup or as a like a company who has a a technology division um I would say no matter what there's kind of three things the first is you need to build scalable reliable uh platforms and select the technology that you care about. Meaning that like there's a lot of ways to do things, but get good at something. Get good at that technology, at that system, at that stack, and then and then keep going with that. Um, and then you leverage this technology so that you do more for your customers. Um, you build your better product, you develop the capabilities, and then you optimize it, make it better, make it faster, make it cheaper, make it uh more capable. And this was sort of the generic enterprise advice, uh, the generic energy advice that many many people would follow. And I think this works really well except now I don't know if this is good advice. It has been across all these major disruptive changes over time. Unclear. In fact, I don't think it's good advice right now because there's a funny thing happening right now which that didn't happen in those previous trends which is that the rate of change is dramatically higher. Um I and you might say look technology always is changing like you know there's other trends things change a lot but not that much um the internet is still based on HTTP the uh uh mobile devices are still um iOS and Android based and so on and so but nowadays um other than the fact that like uh generative AI exists most things that power it are changing and changing dramatically. So last year I was here at this uh at the AI engineering world fair and I gave a speech and I said uh after spending a lot of time on this and thinking through this I think there's a key to this which is a gentic uh uh graph-based approach. The idea was um uh you have a large language model and these nodes and then you sort of put them together and you have the sort of the AI traverse this graph that you set up you build the graph. This is the key approach that and if you use this this is going to really help you sort of build agents because what is anything that we do in life it's a agent it's a workflow um uh it's a it's a way and then if you have an intelligent uh uh a agent it can basically traverse this is the key approach and I believe that at the time and a lot of people did and I still love this approach but nowadays it's sort of a little bit out of date in fact I remember um uh a guy came up to me after my speech last time and he was like the problem you talked about the the answer is just this exactly you were speaking to me thank you so much and and I was happy I I you know I gave a good speech and gave somebody some good advice um and then I remember when we made a change I was like I wonder what happened to that guy I wonder if he's here uh it's uh uh so um but the problem is is that not that it was wrong that that was the best approach but a new way emerged um in fact I started to like look through like all of the last year's uh events and actually go to other conferences like what what did people talk about a year ago and most of them were again nothing much wrong all good speeches all all 
...[middle elided]...
nd um and then here I think very use I mean like whenever you whenever anybody's bought technology in the past I would had advised them like look at what they do now. Double check the road map. Make sure it's good. Make sure it's on the path you want but just focus on what's available now. But I think something else here is um should do that of course that's most important thing but like look back how have they handled change what's their attitude towards change how can what can you when you talk to them when you read about their stuff like what happened six months ago what happened a year ago how did they handle that transition many of the vendors that I really like right now have reinvented themselves three times in the last year and I now trust that if something else comes along they're very good at this they understand agent technologies they understand the the eval sets they understand the the observability systems and then you can say ah okay good I hope that they keep up and then I now my sort of thing I need to do is just evaluate whether or not that's a good platform so um making sure that you have this sort of platforms that do well is is is critical um and um if anybody's interested in unstructured content and AI associated with it uh Box has a booth downstairs happy to talk to you about those kind of things um and then um I I'll leave you with this is um I actually I fully bet and I believe that um a company that's born this year was born last year um will or maybe even a company a medium-sized company or a big company will will they they'll shoot very high the company that will dominate tomorrow is is is now born today. Uh but I kind of bet you that the technology approach that they have right now is probably going to change multiple times before they do that. So interestingly it's like the challenge the advice the thought here is build for change adaptability arguably that's the moat that you have until that changes. Okay thank you everyone. [applause]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agent-infra-vendor-evaluation",
  "signal": 0.3,
  "novelty": 0.25,
  "actionability": 0.25,
  "evidence": 0.2,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это мотивационный кейноут CTO Box без конкретных техник, кода или бенчмарков — в основном общий тезис «строй под изменения», с одной полезной эвристикой оценки вендоров по истории адаптации.",
  "knowledge_units": [
    {
      "claim": "Архитектурные паттерны для агентов (например, graph-based агентный подход) меняются намного быстрее, чем прошлые технологические волны (интернет, мобайл, облако) — то, что было «правильным ответом» год назад, уже устарело.",
      "type": "principle",
      "actionable": "Не привязывайся жёстко к одному агентному паттерну как к финальному решению — закладывай в архитектуру возможность быстрой замены подхода."
    },
    {
      "claim": "При выборе инфраструктурного вендора для агентов важнее не только текущий фичасет и роадмап, а история их прошлых pivot'ов — как быстро и качественно они уже несколько раз меняли подход.",
      "type": "tactic",
      "actionable": "Перед покупкой/интеграцией вендора спроси, как их продукт выглядел 6-12 месяцев назад и сколько раз они уже переизобретали архитектуру — это индикатор, справятся ли они со следующим сдвигом."
    }
  ]
}
```
