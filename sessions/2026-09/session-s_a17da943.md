---
session: s_a17da943
date: 2026-09-29
words: 1938
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a17da943` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Anthropic Actually Fixed Opus
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Approximately 10 months ago, the way that we wrote code with AI changed fundamentally with a single model release. The model, of course, was Opus 4.5, which, believe it or not, came out in November last year, almost a year ago. Now, Opus 4.5 was a really interesting release for a handful of reasons. First off, it was way more expensive than Sonnet, which made it not really the default choice for developers. Second off, they skipped a bunch of numbers and went straight to.5. But third off, despite being a revolutionary change in how we can use models for code, they didn't make it Opus 5, they made it 4.5. Since then, Anthropic has released some incredible stuff in the Fable line, but pretty much every other launch they've done has been iffy at best, especially model releases like Opus 5 and Sonnet 5. And I'll take some fault here. I fell for Opus 5 when it came out. It seemed like it was working really well. But when you combine the absolute slop it would output in text trying to describe what it was doing with the code that would often miss really important stuff, the model felt more like a liability than an actual thing you could rely on when you worked every day. All of this sets a pretty brutal stage for Anthropic who previously made incredible models in the Opus line and has since kind of let it die. All of that said, I still did hold some hope for Opus because I needed something to use the other half of my anthropic subs with. And I still have a soft spot in my heart for that moment in November last year where all of a sudden I was watching my computer code for me instead of just telling it what to change. That's why I was so shocked when I saw that this isn't Opus 5.1, it was 5.5. They set a really, really high bar for this release. And while it is admittedly far too early to know for sure, think they may have hit it. I've been using Opus 5.5 all day and it has been blowing me away. They made it cheaper. They made it less bad at writing. They made it way better at code and following instructions and just doing stuff every day. Is this the Fable Killer I've been waiting for? I can't know that just yet. But is this model blowing me away? Absolutely. I can't wait to show you all of the reasons why I'm so impressed after a real quick break for today's sponsor. While I was prepping to film today, I was trying to get a bunch of dashboards open. It's been a little hard for me cuz I'm kind of down a hand. So, I decided to let Codeex use computer use to go through all of these pages and get me signed in. And I was blown away at just how many times it couldn't do it. The biggest reason is that these sites don't offer good O solutions for agents, which makes it really hard for my agent to do anything on my behalf without me signing into the browser myself. If only all those companies were using today's sponsor, Work OS, because they built the standard for this, OMD. The goal of OMD is to give an easy way for agents to O on a user's behalf or set things up for a user ahead of time. Work OS partnered with Cloudflare and Firecrawl to build this standard and now a ton of other companies are adopting it and helping push it further. Companies like Neon, Recent, Parallel Monday, and more are already moving over. And if you're looking for the easiest way to adopt this new standard, work OS is probably your best bet. There's a reason companies like OpenAI and Anthropic trust them so deeply, it's because Work OS solved enterprise off, not just simple signin with Google buttons. All the pieces that real businesses need when they want to adopt your product. If you've never had to configure Octa, ADP, or Duo at your job, I envy you. It is hell and miserable, and I wouldn't wish it on my worst enemy. Thankfully, when you use Work OS, you get the admin portal. Just you send a single link to the IT team at the other company, and now they're good to go. Works is the only platform that is loved by developers, agents, companies, and IT teams. Figure out why atv.link/workos. Let's dive into Opus 5.5. Kind of crazy. This is one of four major model drops in the last 2 days with Gro 4.7, then Opus 5.5, and then GPT6 Soul and Luna, which of course we'll be covering in the near future. If you haven't hit the subscribe button, you should consider it because I stay up all night working on these videos nowadays cuz there's just so much to cover. I do my best to distill it. I'm sorry the videos are long, but hit the button if you don't mind. Helps us out a ton. Less than half of y'all are subbed and it's a great opportunity to stay on top of these things as they change constantly. So, what makes Opus 5.5 so cool? We'll start with what they had to say. It performs at the level of Fable 5.1 on most work and it costs 40% less to run than Opus 5. They open by saying that this is the first release since they called for pacing the frontier. I have a lot of thoughts on that that I'm going to reserve for a future video, so we'll ignore that for now. What I care a lot more about is how this model actually works. They mentioned that they had a tester that completed a 680,000 line of code migration in less than a day, which is genuinely very impressive. They also site its ability to fix inefficiencies in software. I've experienced this too, throwing it at some pretty brutal stuff to try and do performance optimizations. I'm impressed. They say it's really safe as well. At this point, I just trust Anthropic when they say this, but now we need to go to the cost and speed part. This is where things start to get fun. 5.5 requires less compute to serve than Opus 5, and its pricing reflects that. Our tests show that at default settings, it will cost 40% less than Opus 5 on typical workloads. Input and output tokens are now cheaper at $4 per mill in and $20 per mill out, which is 20% less than before. They also made a huge change to cash reads. Not quite as big as the change that they made for Fable, but closeish. Now it's 60% cheaper to 
...[middle elided]...
 at the absolute least, the amount of value you get out of your $200 sub in Claude, it is running laps around our friends at OpenAI. They did also bump the five hour limit, which is worth noting. It's still not as generous as OpenAI's entire lack of a weekly limit on the $1200 plans, but at least the five hour limit is much more generous now. I haven't come close to hitting it for what it's worth. That all said, I am still quite excited to dive deeper into GBD6 Soul and see what it is capable of. It is even cheaper than Opus and seems to be performing quite well as well. And historically, OpenAI has been better at taking the capability of the high-end expensive model and forcing it into the cheaper, smaller models. Anthropic's never been the best at that. They're the pre-training kings and OpenAI is the post-training kings. But it seems like Anthropic caught up a lot here on the post-training side. So, I cannot wait to dive deeper into what OpenAI has been doing. Make sure you're subbed if you haven't yet in order to see that video right when it drops. I can't believe this week's been so chaotic and it's only Tuesday. I have a feeling it's going to get worse. And next week has OpenAI's dev day, so it's probably going to get even crazier from there. So, make sure you stay tuned because there's going to be a lot of stuff to cover and I have a feeling I will not be sleeping enough this week. Let me know how y'all feel about this model. I think it is a way better solution than Opus 5 was and it's getting close enough to Fable that it makes a lot more sense in your cloud subs. So, congrats to everybody who's working at a company that restricts what models you can use. Opus 55 is going to be a lifechanging experience for y'all. And to everybody else trying to maximize the usage of your subs, congrats. You can now do that in a way that makes actual sense with code that I'm not scared to look at, much less merge. I want to go play with these models more. So, uh yeah. Bards.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "opus-5.5-release",
  "signal": 0.25,
  "novelty": 0.15,
  "actionability": 0.2,
  "evidence": 0.2,
  "durability": 0.15,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это личная эмоциональная реакция ютубера на релиз Opus 5.5 с пересказом маркетинговых тезисов Anthropic и рекламной вставкой, без методологии или воспроизводимого опыта — просто хайп-обзор с парой цифр по цене.",
  "knowledge_units": [
    {
      "claim": "Opus 5.5 заявлен на 40% дешевле в типовых нагрузках, чем Opus 5, при цене $4/млн входных и $20/млн выходных токенов, и с более дешёвым чтением кэша",
      "type": "tool-caveat",
      "actionable": "При выборе модели для продакшена пересчитать стоимость своих пайплайнов под новый прайсинг Opus 5.5, но проверить цифры в официальной документации, а не с видео — цены меняются быстро"
    },
    {
      "claim": "Автор субъективно оценивает Opus 5.5 как модель, сравнимую по качеству с Fable 5.1, но заметно дешевле, и отмечает, что она стала менее многословной и более точной в код-ревью по сравнению с Opus 5",
      "type": "benchmark",
      "actionable": "Провести собственный A/B на своих задачах (не доверять личным впечатлениям блогера) перед переключением дефолтной модели с Sonnet/Fable на Opus 5.5"
    }
  ]
}
```
