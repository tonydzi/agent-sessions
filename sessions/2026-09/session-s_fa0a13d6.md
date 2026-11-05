---
session: s_fa0a13d6
date: 2026-09-30
words: 1933
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fa0a13d6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: OpenAI should be scared of this one
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
It's hard to ignore just how well Anthropic's been doing recently. From Fable 5.1 being my favorite code model ever released to Opus 5.5 taking over pretty much everyone's workflows, my own included. I haven't chosen Fable for any tasks for over a week now, which is just like mindblowingly crazy to now with yet another release, and this one seems strategically targeted to screw over OpenAI as much as possible. Sonnet is back and 5.5 is looking a hell of a lot more promising than Sonnet 5, which if you don't remember was one of my least favorite model releases like ever. Sonnet 5.5 is a model I did not expect to care about. I legitimately thought I would just kind of skip over this one and not talk about it because I've been so impressed with Opus's price and value and just everything I've been doing with it. But I was wrong. Sonnet 5.5 is an incredible model. I am actually very very impressed with it, but not in the ways you might expect cuz when you look at the numbers, it doesn't seem that impressive. On the artificial analysis intelligence index, it comes out as more expensive and dumber than Opus 5.5 at every single level. So, why am I so fond of Sonnet 5.5? It's going to be hard to justify, but I think I can do it well. The simple way of putting it is there's finally a cheapish model from Anthropic that makes sense in the modern era, especially when you compare it to offerings from OpenAI that have historically been closer to this price range. This model almost feels squarely targeted at OpenAI, specifically at GPT6 Soul. There's a reason I'm filming this video and not a GPT6 Soul video, and it's not because Soul is so impressive. Trust me on that. I'll explain what I mean and more after a real quick word from today's sponsor. Staying on top of what's happening in your codebase has never been harder to do. AI has made contributing to most codebases way easier, but it's made keeping track of what's going on in them way harder. I can't tell you how many times I had some weird issue in a codebase. I was like, "What the hell happened here? Who would ever have merged this?" And then went to the notes and saw that it was actually changes I made with my agent that I merged because I was blindly trusting the AI reviewers. Today's sponsor is one of those reviewers. It's Code Rabbit. But I'm not here to talk about how good Code Rabbit's reviews are. Spoiler, they're very good. I want to talk about a new feature they introduced which has made actually keeping on top of the changes way easier. It's the Code Rabbit change stack. Now when you have Code Rabbit set up on a codebase, it will give you this simple button that you can click even signed out to see what changed in the PR in a way that makes way more sense. Instead of a pile of alphabetically listed files, you get a description of what changed and why. Instead of a jumbled mess of commits that nobody's going to click through, you get this stack of the different things the PR changes with descriptions of what is changing and why. And if you look at this, you can see pretty immediately how much easier it is to read through the changes that were made in this poll request. It even summarizes these different parts so you can understand what's going on in each of them. In this part, it's the detection for the package install and making changes to how T3 Code is persisted on your machine. Here is where we fixed the update logic that was breaking for a lot of users. There's even a security blast radius diagram that makes it way easier to see what changes are risky in a given PR. I also really like the activity view, which is a super quick way to see what's changing in a PR to catch up without having to scroll through the mess that is the thread view in a given poll request on GitHub. Don't let SLOP take away your understanding of your codebase. Fight back at soy.link/code rabbit. As I was saying, the benchmarks don't necessarily look great depending on how you frame them, but I want to start with what Anthropic said with their official announcement post. This is the Claude Sonnet 5.5 announcement. Introducing Sonnet 5.5, the second model in the 5.5 family. The clear upgrade over Sonnet 5. It's 30% faster and up to 30% cheaper for most work. I don't love comparing this model to Sonnet 5 because on one hand, it's not going to showcase the benefits that well. Like the speed difference and the cost difference isn't that big a deal. Sonnet was relatively cheap. But also because Sonnet 5 was a garbage tier model and is not a good target to compare against. I said the same thing with the Opus 5.5 coverage. It made no sense to compare it to Opus 5, which is why I'm thankful they compared it to Fable so much. But here again with Sonnet because Sonnet's the smallest that they're working on right now. Then there's Opus, then there's Fable. Haiku is eventually going to happen, but uh we'll see. They said it's coming in the next few weeks. I didn't think Sonnet would be here so quick, and honestly, I'm pretty impressed with it. Sonet 5.5 is faster, lower cost as a compliment to Opus 5.5, where Opus is built for complex work requiring careful judgment. Sonet 5.5 is strongest at well scoped everyday tasks. I will say it actually goes quite a bit further. Make sure you stay tuned for the fish slop demo. I I'm very impressed with it. That's all I'll say for now. It's also good for fixing bugs and creating polished documents, slides, and spreadsheets. I don't know how many of y'all are actually creating polished documents, slides, and spreadsheets with your models, but if you are, let me know in the comments. I am actually curious. And when you're on the way there, if you could hit that little red button, it does help us out a bunch. A lot of y'all aren't subscribed, and you'd be amazed at how much it helps the channel. And it's also a great way to keep up to date. and seeing that uh OpenAI dev day is in not very much time. In fact, it may have already happened is
...[middle elided]...
o find specific behaviors or characteristics or confirming a hunch it has about some thing that you found in an API or all of those types of investigatory things. It is really cheap and surprisingly fast, too. I would bet that if you set Opus up properly to use Sonnet at the right times for these sub agents that the result will be Opus feeling way faster and getting real work done for slightly cheaper. That sounds like a pretty good deal to me. So, while I don't think you should actually use Sonnet 5.5 yourself, I think it is an incredible addition to this new family of models, and I'm excited to see how Opus chooses to wield it. I will not be using this model much going forward myself, but I do hope that my Opus is able to because there is clearly value here. While not in like front-end building work or day-to-day coding tasks, there is a ton of value in how this model can be utilized to confirm things in real world code bases. And I would assume for real world documents, office, and all that type of stuff, too. That's not what you guys are here for. You're here for the code. And I'm hyped to say this model is useful as long as you're not the one sending it prompts. But godamn, OpenAI really needs to respond to this. They have lost in all of the places they are strongest. They don't have the smartest model. They don't have the most efficient model. They don't have the cheapest model. They don't have the best model for calling other models. It's rough for OpenAI right now. And I can't wait to see how they catch up because right now it just doesn't feel like a good value. The $200 codeex plan gets me nowhere near as much usage and nowhere near as much realworld code as I'm getting out of my $200 Cloud subs. So take that as you will. Fingers crossed we got some fun announcements coming. I have a feeling that things are about to speed up, not slow down. Hopefully this was a useful breakdown. You can better know how to wield this model. And until next time, peace nerds.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "model-release-sonnet-5.5",
  "signal": 0.3,
  "novelty": 0.25,
  "actionability": 0.35,
  "evidence": 0.15,
  "durability": 0.15,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "В основном это реакция-хайп блогера на релиз Sonnet 5.5 с сравнением цены/бенчмарков и рекламной вставкой, без глубоких демо или цифр, но есть одна практическая мысль про архитектуру суб-агентов.",
  "knowledge_units": [
    {
      "claim": "Автор считает, что дешёвую и быструю модель (Sonnet 5.5) выгоднее использовать не как основную для написания кода, а как суб-агента под более сильной моделью (Opus 5.5) для рутинных исследовательских задач — проверки гипотез по коду, поиска конкретного поведения в API и т.п.",
      "type": "tactic",
      "actionable": "В агентных пайплайнах можно назначить дешёвую/быструю модель на роль суб-агента для узких инспекционных подзадач (grep-подобный поиск, проверка гипотез), оставив дорогую модель-оркестратор для сложных решений — это может ускорить работу и снизить стоимость без потери качества на основной задаче."
    },
    {
      "claim": "По собственным ощущениям автора, ценность нового дешёвого Sonnet не в бенчмарках (там он проигрывает Opus 5.5 по цене и качеству), а в практическом соотношении скорость/цена для узкого класса задач.",
      "type": "benchmark",
      "actionable": "Не полагаться только на индекс intelligence/бенчмарки при выборе модели — тестировать модель на реальном профиле задач (скорость выполнения суб-задач, стоимость токенов), так как формальные метрики могут не отражать пользу для конкретного workflow."
    }
  ]
}
```
