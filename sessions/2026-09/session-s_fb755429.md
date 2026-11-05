---
session: s_fb755429
date: 2026-09-29
words: 2021
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fb755429` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: I was using Fable wrong, this is how I fixed it
CHANNEL: [ИМЯ] - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Just a few months ago, people were accusing me of being paid by OpenAI because I liked the models they were shipping that much. I thought that was kind of insane. What's even more insane though is the fact that [ИМЯ] [ИМЯ] just called me an Anthropic fanboy specifically because of how much I prefer using Fable over Astra for my day-to-day work. There are a lot of reasons for this and I cover a bunch of them in my Fable versus Astra video, but that's not what I want to rehash today. In that comparative video, I vibed out a graph showing how I feel the quality of the output I get from the models differs where Astra can be way higher than Fable at points but way way worse at others. Fable still makes its mistakes, but it was less noisy by far. That comes with benefits outside of trusting it more. It means the model can go longer and do more in a given pass. It means you can tell it to come back with a video when it's done and it actually can do that. It also means that the little dips it does have hurt more and finding ways to reduce them is incredibly valuable. I've spent a lot of time with this model. It's probably I've ever used a model that I was paying for in such a short window. I have shipped so much code with this model it's insane and I've been burning my five accounts to the ground using it. I wish I hadn't burned as many of them as I did before reading this particular guide from Anthropic because the prompting Claude Fable 5.1 doc is actually really good and has a bunch of insights that are worth learning from. The goal of this video is to try and take all of the things I figured out over the last month-ish of using the model and distill it into the most useful pieces of info I can possibly give you. Everything from how to fix your agent CMD to how to give the model the tools it needs to keep going and get better results to even using Codex to help make your Claude outputs better. But as I mentioned before, I'm paying for these accounts myself and if I'm going to need another, I hope you can understand why we're doing a quick sponsor break. There's a pretty good chance your company is shipping more code than it's ever shipped before. This also means you're probably shipping out more bugs than ever before. And those bugs are getting more insidious and harder to find, especially when you're building things with agents, not just using agents to build, but also serving agents to your users. If you were around before agents, you've almost certainly heard about Sentry. And honestly, if you've been around since, you have, too, because these guys are the go-to platform for identifying bugs in your real-world applications. I've had Sentry set up on pretty much every codebase I have worked in in the last, I don't even want to think about how many years. God, I've been around for a while. Needless to say, these guys know how to find bugs in your apps, and the Sentry MCP makes it so your agents can use that same data, as well. But I'm not just here to tell you that Sentry exists. You probably already know that. I'm here to show you the really cool things they've set up for building with agents. I set up a demo in T3 code to get some traces, and god damn, the info you get is so, so useful. They break down the cost of the whole request, and even better, the cost of each chunk within the request. This timeline view is super helpful for figuring out what happened when, and where the costs were. So, we can see that this top-level request cost 40 cents or so, but more importantly, we can see where all that money went. And if you're not that into timeline-style views, I understand. It doesn't really map to my head very well, especially when you're used to using a chat view for actually doing these things. For those who weren't watching, I just transitioned over to the chat view that they built into their agent platform. Yes, you can actually see a transcript for the back and forth that your agents or your users or whoever else had that led to these issues. And if I slide this over, you can see all the additional info, from how many tokens were used, how many errors were hit, and how much the request actually cost to run. And as you scroll, you can see how the user experienced this, with the timestamp showing when different things happened, what worked, what didn't, and the actual cost of everything the user ends up seeing. This is particularly useful if you're building custom tools and interfaces like an MCP that your agents are working with, because you can debug not just what the model sent to the MCP, but the whole pipeline and all the code that actually serves that agent's request. Figure out what your agents and your code are actually doing at swyd.link/sentry. I'm going to start with the official prompting guide because the amount that's changed with 5.1 to 5 is meaningful, but it's almost all subtle things. So, it's worth going through. The first section they have is titled consider all effort levels. I find this one a little cringe cuz it forgets the fact that we only have 50% of our limit as a subscriber. And I'll I'll be real up front with this. I don't think Fable is worth the money if you're not getting it subsidized through a subscription. Paying the full API price just kind of sounds insane to me. I don't think Astra is much better here, sadly, because Astra can often get stuck in a loop and end up spending way more than it should. Fable is at least a bit more likely to stop when it should. So, on a median task, Fable is definitely more expensive, but on the extremes, I find that Astra can just burn usage in stupid ways. Now I've that out of the way, I want to make sure it's clear what I'm talking about is subscription usage because I just I don't think it's worth using any of these over API prices. And that's also why a lot of companies probably aren't letting you use these models. And for that, I am sorry. Assuming you're on a subscription, you have half your limit reserved for Fable
...[middle elided]...
I find a lot of people massively over engineering around problems that haven't existed for at least a year. The models are really good at managing their context. You don't have to do it for them. The hardnesses are really good at using the different things on your machine. You don't have to set that up yourself. The permission systems and the auto approval modes are very good now, and you definitely shouldn't use accept edits or supervised. We recently added anti-gravity support to T3 code, and after all the requests we got to add accept edits mode for anti-gravity because they can't trust the Gemini models enough and they don't have an auto mode yet. I was this close to just removing anti-gravity support. Like, supervise and auto accept edits are tools from the past, from like 2024 even at like newest. Use auto if you're careful and use full if you're not, period. The points I'm trying to make here are simple. The tools are good now. Any customization or careful configuration you've done to work around the flaws are probably out of date. And a lot of your own mental model around this stuff is also out of date. Reset it. Pretend you're on a brand new machine, delete everything, install Claude Code from scratch, set it up with as little as possible. I bet you'll be surprised how capable it is. And from there, slowly start adding small things that solve your small problems. I think I said all I have to on this point. I hope this one was helpful. It's kind of different from how I normally do these types of videos, less about my specific day-to-day work and more about the philosophical way to take advantage of tools as powerful as these models. People 5.1 was an incremental improvement in how the model works and behaves, but it has become much more than that for my day-to-day work. I really, really like using this model and I bet you will, too. And if you don't like using the model, I'm actually curious why. Let me know in the comments. And until next time, peace nerds.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding-prompting",
  "signal": 0.35,
  "novelty": 0.25,
  "actionability": 0.4,
  "evidence": 0.25,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Видео большей частью состоит из личных впечатлений и спонсорской вставки Sentry, но содержит пару практических советов по работе с Claude (Fable) 5.1 и философии настройки агентских харнессов.",
  "knowledge_units": [
    {
      "claim": "Автор советует полностью сбросить кастомные настройки агентского харнесса (обходы старых ограничений контекста, ручные конфиги) и начать с чистого дефолтного конфига, добавляя правки только под реально возникающую боль.",
      "type": "tactic",
      "actionable": "Удали накопленные workaround'ы и кастомные системные промпты старше нескольких месяцев, переустанови харнесс с минимальным конфигом и добавляй настройки по одной, только когда столкнёшься с конкретной проблемой."
    },
    {
      "claim": "Режимы 'accept edits' и 'supervised' в агентских харнессах считаются устаревшими (актуальны были максимум в 2024) — современные модели и авто-режимы одобрения справляются лучше без ручного контроля каждого шага.",
      "type": "tool-caveat",
      "actionable": "Переключись на auto-approve режим для доверенных задач и на full/manual только для по-настоящему рискованных операций; не используй промежуточные ручные режимы 'по умолчанию'."
    },
    {
      "claim": "При использовании Claude (Fable) через подписку, а не через API, действует ограничение — только часть общего лимита usage выделена именно под топовую модель ('effort levels' описаны в официальном prompting guide Anthropic для 5.1).",
      "type": "tool-caveat",
      "actionable": "Перед интенсивным использованием модели по подписке проверь официальный prompting guide на предмет лимитов effort levels, чтобы не сжечь квоту раньше времени."
    },
    {
      "claim": "По наблюдению автора, на медианных задачах Claude (Fable) обходится дороже по токенам, чем конкурент (Astra/GPT-класс), но на крайних случаях конкурент склонен зацикливаться и тратить usage гораздо сильнее из-за менее предсказуемого поведения.",
      "type": "benchmark",
      "actionable": "При выборе модели для длинных автономных агентских прогонов учитывай не только медианную стоимость, но и риск 'зацикливания' модели на редких сложных задачах — это может стоить дороже медианной разницы в цене."
    }
  ]
}
```
