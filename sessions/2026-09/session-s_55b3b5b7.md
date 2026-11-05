---
session: s_55b3b5b7
date: 2026-09-24
words: 1972
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_55b3b5b7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: AI Coding Rate Limits are RIDICULOUS Now - Here's How You Keep Scaling Anyway
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
This week, I've hit my Claude code rate limit way faster than I ever have before, and I'm not even doing that much more work. This is my max $200 a month plan. And the worst part is I also have a $200 a month Pro subscription for Codeex, and I've almost exhausted that limit as well. And both of them aren't going to reset for another 3 or 4 days. And so, if you thought it was just you hitting your rate limits faster, don't worry, it's not. We're all suffering from this. And unfortunately, we knew this was coming. It's been a trend this entire year. Our rate limits getting worse, but it's just finally come to a point where I can't just be more efficient with my token usage. I mean, it's ridiculous that I have to wait three to four more days before I even have a reset on my max plans. So, over the past half year, I've been doing a lot of experimentation with using different models, especially open ones, in my AI coding workflows. But now, that's gone from just experimentation to, okay, I absolutely need this as a crucial part of everything that I'm doing. I mean, look, the proof is right here. And that's not just me. As an industry, when we get more into harness engineering and loop engineering and software factories, whatever your AI coding workflow looks like, we're trying to scale the output with our coding agents. But now, even more than before, the biggest limiter is just the number of tokens that we can spend. That is why we need to strategize and figure out for our larger AI coding workflows, not single agent, where do we absolutely need the largest and most capable LLM versus other places where we can use something that is smaller, cheaper, faster, and still get basically the same output quality. And yes, that is possible. Trust me, I've been deep in the lab this week expanding on all the research I've been doing this year figuring out for a traditional AI coding workflow where you have your planning, implementing, validating, and reviewing, where do we need the best LLM versus where do we not? That's the big question to answer right now so you don't hit your rate limit 3 days into your weekly reset. So, for all the testing that I've done this week, I've done it with my AI software factory. I've covered this system a lot on my channel recently. It takes all my best practices for AI coding with planning and implementing and validating. It packages it up into a complete system where I can send in scope of work and it just builds and validates everything without me in the loop at all. It's the ultimate test of how autonomous can we make AI coding while still keeping it reliable. But more importantly for this video, it allows me to very easily test different combinations of large language models with the full development cycle. So, what I've been doing is building a bunch of different applications with the AI software factory, including this video game that I'll show you today. It just makes for a nice and visual core example, but all the other things that I built, the results I got is pretty much the same as what I got with the different combinations for this game. So, building the same game, but with only open models, using claude, and using codecs. A lot of other testing that I did as well, but these are the three core columns. And so essentially I just took the best model from each group, right? With open models, DeepSeek V4.1 Flash is pretty much the best of the best. So if we look at like the live LLM benchmarks here as far as open models go with that open tag, Deepseek V4.1 Flash is the best right now. And then for Claude, Claude Fable 5.1 max effort is the best. And then for Codeex, GPT6 Astra max effort is the best. And so going back here for my core testing with open models, I'm using Deepseek Flash for planning and reviewing and then GLM 5.3 Flash for the implementation. And I actually did this as a baseline where I used it for implementation for every single test and then for Claude using Fable for planning and reviewing and then for Codeex using Astra. The most important thing here is you'll notice I'm always using the more capable LLM for planning and reviewing and then the smaller model for building. This is something that I've determined in my experimentation this week and a lot of what I was doing earlier this year as well. The most important step of your AI coding workflow is always the plan step. If you have a well-written plan, the implementer following that, it doesn't even have to be that capable of an LLM to pretty much get the best results possible, right? Like using Fable for planning and implementation gets you essentially the same results as using Fable for planning and sonnet for implementation. So that you'll see that very intentionally laid out in all the testing I show you today. And by the way, for implementation, generally that's the most tokenheavy part of your workflow. So for using the smaller model for that, that is what prevents us from hitting our rate limits super quickly. Now, obviously for some work, if it's very very difficult and unexplored, you might want to use a large model for everything. And I don't do this in my software factory, but if you do have human in the loop, really small and bounded tasks, you can use an open model for literally everything. So there's different combinations that make sense in different situations, but this is generally what I recommend. And I'll show you a lot of my testing that has led to this, but for me, my favorite flow right now, my favorite combination is to use GPT6 Astra for the planning and the review and then GLM 5.3 Flash for the super fast and cheap implementation. This is my core workflow for everything that I'm doing right now with my software factory. You ask a question and it gives back a fully narrated video lesson in 2 to 3 seconds built live while you watch and it plugs right into Codeex and Claude Code. So now over in Cloud Code, I do SLMCP. We can see I have Scribba explain connected. It was
...[middle elided]...
sed GPT6 Astra. And so this version of the game was about four times less tokens or like less cost overall because I'm using GLM for the implementation and it plays pretty much the same. Actually, the moving is even smoother here going towards the clouds. I would say this version of the game actually is better even though I was using an open model to write every single line of code. So, of course, it helps to have Astro Review, but I'm still saving a ton on my cost/ rate limit by using this combination of models. And so, yeah, a little bit of a cheesy game, very much just a proof of concept. But the point here is this is the results that I got for pretty much every application that I built. And remember, going back to the live bench here, Claude Fable 5.1 and GPT6 Astro, they're pretty close in capability. And so it's pretty awesome that we were able to build even a little bit of a better game and other apps with this combination compared to just using claw. That is the proof you need. You don't always have to have the best large language model for every step of your process. It is well worth your time and I hope I've really proved it here to analyze your AI coding workflow. figure out where you need the best model and where you don't because that is what's going to prevent you from jacking up your rate limits for your subscriptions like Claude and a codeex. And so my AI software factory is how I've been doing all my testing, how I run my workflows now, but whatever you're currently doing this this lesson applies like you should really explore open models at this point because it's becoming clear that we can't always run on our frontier models. So, I hope that you found this testing interesting as I'm going through all these different combinations, building out different apps. If you did, I would really appreciate a like and a subscribe. Follow along as I continue to build out my software factory and test these combinations. And with that, I will see you in the next

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "llm-cost-routing-agentic-coding",
  "signal": 0.55,
  "novelty": 0.35,
  "actionability": 0.65,
  "evidence": 0.35,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Автор на анекдотических (не строгих) тестах показывает практическую стратегию распределения моделей по этапам агентного кодинга, чтобы не упираться в рейт-лимиты — идея полезная, но привязана к конкретным моделям/тарифам, которые быстро устареют.",
  "knowledge_units": [
    {
      "claim": "В пайплайне AI-кодинга (план → имплементация → валидация → ревью) самая дорогая по токенам часть — имплементация, а не планирование.",
      "type": "principle",
      "actionable": "Замерьте расход токенов по этапам своего пайплайна перед оптимизацией — скорее всего именно шаг генерации кода стоит дороже всего и его первым стоит переносить на дешёвую модель."
    },
    {
      "claim": "Если планирование и ревью делает сильная/дорогая модель, а саму реализацию кода — дешёвая и быстрая (например open-weight класса GLM/DeepSeek), итоговое качество результата почти не падает, а расход токенов снижается кратно (в демонстрации автора — примерно в 4 раза).",
      "type": "tactic",
      "actionable": "Разделите роли LLM в своём агентном workflow: топ-модель — только на план и код-ревью, а на имплементацию поставьте более дешёвую/быструю модель; сравните итоговое качество и потребление токенов на своём проекте перед тем, как расширять использование топ-модели."
    },
    {
      "claim": "Использование единственной топовой модели на всех этапах агентного кодинга (план+реализация+ревью) — главная причина упирания в недельные рейт-лимиты подписок типа Claude Max / Codex Pro при интенсивной автономной работе.",
      "type": "tool-caveat",
      "actionable": "Если регулярно выжигаете лимит подписки за 2-3 дня из 7, проверьте, не гоняете ли вы одну и ту же дорогую модель через весь цикл — распределение по ролям (см. выше) снимает часть давления на лимит без смены тарифа."
    }
  ]
}
```
