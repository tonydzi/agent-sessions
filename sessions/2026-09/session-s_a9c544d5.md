---
session: s_a9c544d5
date: 2026-09-29
words: 2049
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a9c544d5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Getting the most out of Opus 5.5
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Opus 5.5 has been out for a bit now, and the more I use it, the more I think this model might actually be really, really good. I've been very impressed with the code it puts out, with how nice it is to interact with, with how it stays on task for long work, as long as you don't use max. I talk about that in a bit, don't worry. But today I want to talk about how you can get the most out of this model. I've had a couple videos like this and they vary in performance, but I think it's some of the more important work we can do, especially when awesome people like Adios Maney, who used to be part of the Chrome team, recently joined Anthropic and is using his depth of knowledge and education capabilities to write something awesome like this. If all goes well here, not only are you going to learn about how you can use Opus 5.5 more effectively, hopefully I will as well. I trust Ady with my damn life if I'm being real. This guy is super legit and when I saw him joining Anthropic, I got really hyped and I am so excited to see what he has to teach us about maximizing the value we get out of the new Opus release. On the topic of maximizing value, we should take a quick break for today's sponsor. If a chef doesn't have access to ingredients, they probably can't cook a very good meal. So why do we think our agents are going to make good results if they don't have access to 80% of the data they need that is currently locked away on the internet. It turns out agents need a way to get that data. They need a way to browse the web, and that's why Browserbase built a browser for your agents. Not just for going to sites and clicking through them, but for getting all the context they need from the internet. Whether it's through their search API to get results on whatever arbitrary queries they need to resolve or their fetch API where they need to get some data out of a page that is hard for them to access. How many times have you seen an agent write a curl request, fail, give up and then go find something else that was incorrect. If you've ever seen Codex or Claude do this, you know how miserable it can be. You probably already burned hundreds of dollars in tokens hitting these errors silently and not even noticed. And if your agents do need real browsing capabilities to do actions on your behalf, whether it's to sign into a page to book something or go find some data that's behind a paywall or a signed in state that you need, Browserbase can handle all of that for your agents, too. Browserbase's goal is simple. Since agents are good at calling APIs, turn the whole web into one. This means that they handle all the details from scaling up their servers to make sure you're always able to access what you need to catching broken flows in your apps with real agents clicking things and noticing issues to getting around CAPTCHAs, handling off, and so, so much more. Ready for a crazy lore drop? Browserbase is so good that it's what Google officially recommends for their computer use work. This is a real Google repo demoing computer use and they recommend Browserbase. Figure out why everyone from Theo to Google loves them at swlh.link/browserbase. Let's talk about getting the most out of Opus 5.5. Opus 5.5 works well in the way that you already use Claude. A few things do behave differently, though. It works for longer on its own. It tells you plainly what it did. And it thinks before every reply. This guide covers how to work with Opus 5.5 in Claude apps and Claude code, including how to prompt the model, steer long runs, and check your results. He starts with a really fun exercise. He recommends trying three specific things in your first sessions with Opus 5.5. The first example he has here is a thing I talk a lot about. The idea of handing over the whole task. I call this prompting wider. Having the model come in earlier and go further. And an important part of doing this is defining good done states. What is complete? Rather than start working on this feature, say I want you to build it so it has these three things, verify it by showing me a screenshot, and then file a PR after. That gives the model a clear end state. It's not done until it has made the feature, there is a screenshot of the feature, and there's a PR up including that feature and the screenshot. Generally speaking, these higher-tier models from Anthropic and OpenAI work really, really well if you tell them what done is, because they'll keep going until they get there. The next two things are more vague, so I'm curious how he frames these as we go on. The second one was delete think carefully lines. You don't need to tell the model to think, it already is going to. I don't know if that really fits here exactly, but interesting inclusion. Last piece I don't like the wording for, but it is important. When long runs end, read what it needs from you first. This is an important thing and I actually think the new model does this quite well, where after it does a run, it will tell you exactly what it needs. It does sometimes miss this though, so I'll often find myself prompting accordingly. Here's a real thread I kicked off earlier today in T3 Code that I think showcases what I'm talking about relatively well. This is a thread I had started on my machine testing out the new Opus model with max reasoning. Six and a half hours later I realized I wasn't going anywhere. I I really don't think you should use max on Opus 55. It just This thread ran for way too long as I had it on max reasoning and I was running it on my own computer, which was even more annoying as y'all who have been around for a bit know, I have moved pretty much all my agent work off my laptop and onto other machines, mostly my apartment, but a few remote servers as well. So normally when I use T3 Code I trigger it somewhere else. But in this particular case I only had the code base and everything set up on this particular machine and I wanted to see it working too, so I ran it on here, forgo
...[middle elided]...
because that can be used to distill their models. They don't want that, so they hide them. It is what it is. As such, anything that mentions reasoning is risking getting a flag. I guess it's a cute little checklist at the end here. Make sure you tell the model what done looks like. Don't tell it to think hard, it will anyways. Design requests should have the styles to leave out as well as what you want it to look like. Charts and screenshots should be attached. Yeah, I I think people underrate how useful screenshotting is. Half the time I would need to give a model like context on an error. I don't copy paste the error, I just screenshot the browser and paste that. They're good at reading these things. And Claude code even has tools where if the screenshot is too high-res and it can't read the text, it will crop to the area it needs to get the context it needs. The other sections we've spent this whole video going through, but if you do want to read this and check it yourself, the link is in the description as always. This is a pretty fun article and I'm thankful to see once again that Anthropic and I are pretty aligned on the best way to use these models. We're now at the point where we need to give our agents more leash. They need to have the ability to verify their changes, they need to be told when done is done, and given enough trust to go do the thing. I talk about a lot of these layers in a video coming out soon all about how Anthropic made the performance for the Claude site and desktop app three times faster. Because the systems you build to verify these changes are just as important as the raw source code itself. Hopefully this video will help you maximize your usage of Opus 5.5. It really is a great model and the more you trust it, the more you give it the things it needs to trust its own work, the further it can go and the more you can build. I hope this was helpful and until next time, peace nerds. Also, do do not touch max mode. Seriously, it's so bad.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "prompting-opus-5.5",
  "signal": 0.55,
  "novelty": 0.35,
  "actionability": 0.6,
  "evidence": 0.5,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Видео пересказывает гайд Anthropic по Opus 5.5 с парой живых практических советов (не юзать max, скриншоты вместо текста ошибок), но большая часть — общие вещи про 'ставь чёткий done state', уже известные практикам, плюс встроенная реклама Browserbase.",
  "knowledge_units": [
    {
      "claim": "При делегировании большой задачи Opus 5.5 нужно явно описать 'состояние done' (например: сделать фичу + скриншот как доказательство + завести PR), иначе модель не знает, когда остановиться",
      "type": "tactic",
      "actionable": "В промпте для агентных задач всегда указывай конкретный проверяемый критерий завершения (скриншот, тест, PR), а не просто 'сделай фичу'"
    },
    {
      "claim": "Opus 5.5 уже думает перед каждым ответом по умолчанию, поэтому инструкции вида 'think carefully' в промпте избыточны",
      "type": "tool-caveat",
      "actionable": "Убери из системных промптов фразы 'подумай внимательно' для Opus 5.5 — они не добавляют эффекта"
    },
    {
      "claim": "Автор считает режим 'max reasoning' на Opus 5.5 непригодным для длинных агентных сессий — в его тесте задача крутилась 6.5 часов без прогресса",
      "type": "tool-caveat",
      "actionable": "Не включай max reasoning для длинных автономных прогонов на Opus 5.5, используй обычный режим и проверяй прогресс чаще"
    },
    {
      "claim": "Вместо копипасты текста ошибки эффективнее кинуть модели скриншот браузера/терминала — Claude Code умеет сам обрезать (crop) скриншот до нужной области, если разрешение слишком велико для распознавания текста",
      "type": "tactic",
      "actionable": "При отладке передавай модели скриншот ошибки вместо текстового лога, особенно для UI/браузерных багов"
    },
    {
      "claim": "После длинных автономных прогонов Opus 5.5 обычно сам сообщает, что ему нужно от пользователя дальше, но иногда это пропускает",
      "type": "tool-caveat",
      "actionable": "После длинного прогона явно проси модель перечислить, что ей нужно от тебя дальше, если она сама этого не сделала"
    }
  ]
}
```
