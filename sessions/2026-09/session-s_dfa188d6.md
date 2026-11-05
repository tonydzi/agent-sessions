---
session: s_dfa188d6
date: 2026-09-29
words: 1932
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_dfa188d6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Elon promised this one would be good...
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Gro 4.7 is finally here, and this is a model I've been pretty hyped about for a while, and it's not just me. Elon's been hyping this one up for over a month now, specifically saying when 4.5 dropped that Gro 47 is going to be the big one, and it's going to exceed all current models. He specifically calls out that SpaceX's training corpus is so awesome and unique that he'd be shocked if any model is better at realworld coding than Grock 4.7, which is why it's particularly funny that it's scoring lower than Grock 4.6 on a bunch of benches. This is why I wanted to make the video though, not just to hype up some new model or get a bunch of free views, which by the way, do appreciate those. But the thing I want to talk about here is how the benchmarks no longer represent reality. And the numbers we look at when we talk about models just aren't the right way to do it anymore. And the sheer volume of numbers that are useless that I've seen floating around this release has been frustrating to put it lightly. There is a lot of value in Gro 4.7. It's actually one of my favorite models I've used this year. Before we dive into the details, I want to give you one thing that's here without any catch. Today's sponsor. If you're trying to ship faster with AI, it's important to get all of the tools around your code right. Most of these tools actually have nothing to do with AI. There are things that probably annoyed your developers in the past already that are now just insufferable with agents. One of those things is the guarantees that your code is actually ready to merge once it's put up. Usually, you do these guarantees through things like CI, but if you're using GitHub, you know just how painful it is. It's slow, expensive, and just miserable. If we were using GitHub CI, our bill would be tens of thousands, if not a hundred thousand plus dollars a month for super slow runs that take minutes, if not hours, to verify that our code works. I'm very thankful we're not using GitHub actions, though, because today's sponsor, Blacksmith, is just so much better in experience. To be very clear, Blacksmith does not require you stop using GitHub actions. They are primarily a replacement for GitHub's runners. So, you make a oneline change to your GitHub action and now your actions will run on their infra instead. And the result is builds and checks that could be 50% faster or more and result in 60% less money spent. I'm going to be real with you guys. I didn't care too much about the savings and cost before because both numbers were really small for me. But now that we're running way more CI, doing hundreds of PRs a day, these savings add up. And I've also found that we're building more CI, which has been great for verifying the work the agents do, but it also means the average PR has like 8 to 30 different things that get run. So making sure they're fast and cheap is essential. Since BlackSmith's hardware is so much better than GitHubs, it'll be faster by default. It's just much much better single core speeds. GitHub's runners are on horrible ancient hardware. But that's not where the fun ends. You can actually use their built-in Codesmith to improve the CI and even make real changes to your codebase directly. When I first tried this out, I clicked some of the example prompts, which were things like optimize the workflow efficiency or make sure we're using the right size of runner for our actions, and I ended up merging three separate PRs from this one quick demo because it found actual improvements that it could make to my CI. This means it cut our bills and our build, well, our build time. Sorry for the pun. You get the idea, though. Stop making your agents wait. Get them better feedback faster at soyv.link/blacksmith. As I was hinting at in the start, the benchmarks don't tell the whole story here at all. Let's go through what they have to say about Grock 47 and then I can share a bit more about my own experience because I've actually seen it outperforming Fable in a handful of my own real world work. Grock 47 is our most capable model for coding and knowledge work. It works longer on difficult tasks. It checks its own work more carefully and it comes with their best calibrated safeguards to date. Served at the same price and speed as Gro 46, it's highly competitive in its class. The same price and speed part is particularly interesting because of things Elon has mentioned in the past. Specifically, he said that Gro 46 would come out early August and it would be their 1.5 trillion or PAM model and 47 would be a new base, a 2.1 trillion per model that would be released a few weeks later. It'll be better than Gro 46 in every way except slightly slower to serve but with even better token efficiency. This was a lie. Gro 46 XHigh, according to artificial analysis, did around 38k tokens per task. Gro 47 it did 81k tokens putting it above even Fable 5.1. By the way, Soul is all the way on the edge here at 29K tokens. Aster is around the same. Normally I wouldn't call out these contradictions, but I have Horvat Truel, the CEO and founder of Cursor, who now is of course helping with a lot of these types of things at XAI. Now that cursor and SpaceX are of the same company, he came at me for one of my posts where I showed that Gro 47 in benchmarks like artificial analysis was showing a 2x increase in cost. Grock 46 cost $186 to run this bench. Astra cost 326 and Gro 47 cost $3.74 per task. This adds up to thousands of dollars for the runs. So yeah, those are some scary numbers. To which Horvat replied that in production at SpaceX and cursor they would saw that 4.7 would use 5% more tokens than 46 for median requests and 20 to 30% more for the P99 requests. There is also a distribution shift in what users are willing to ask it. This would be a really good response if it wasn't to a benchmark of static prompts. I I really don't want to be as rude as I feel like I have to be here, but there's just a lot of misinformation 
...[middle elided]...
orld work, the cost increase associated with those improvements is not big enough to justify the move over. The subsidization on the subscriptions is also bad enough that there's no economic reason to move. Previously, the speed and economic benefits of moving to Grock made some sense with Grock 45 when you compared with things like Opus and what became Soul. It makes no sense right now. It's more expensive, slower, higher error rates, worse overall code, and nowhere near the subsidization that we're used to from the Codeex and Claude subscriptions. So, what is this model for then? I think it's a stepping stone. I don't think it's much more than that. I hope that with more RL they can make this model more efficient and way more reasonable a value but it does currently seem like SpaceX is struggling with this jump to catch up with the new frontier because we did really experience a generational leap with Fable and Astra GPT56 Soul felt closeish but wasn't really the same generational gap. Grock 47 is still very last gen and it's increasingly hard to justify as the Frontier continues to advance. I think this model's cool and fun and worth playing with, especially if you're still stuck using cursor as your primary source of inference, but outside of that, this one's hard for me to recommend. I hope that the next model will be the one where Elon makes good on his promises and we can finally get frontier level performance at a meaningfully better price. But right now, it just kind of feels bad cuz we're getting last gen performance in various tasks at a current generation price, which just is not the right compromise at all. How do you guys feel about this release? Am I being too harsh or is this not something they should have put out in this state? Let me know how y'all feel. And until next time, peace nerds. I have one last gag I want to sneak into the end here. There's no way we're getting that good review repost this time, huh? A man can hope. Sorry, Elon. Next time.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "grok-4.7-release-eval",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.3,
  "evidence": 0.45,
  "durability": 0.15,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "В основном это разбор хайпа вокруг конкретного релиза Grok 4.7 со встроенной рекламой спонсора, но внутри есть пара переносимых наблюдений про расхождение бенчмарков и продакшн-метрик.",
  "knowledge_units": [
    {
      "claim": "Публичные бенчмарки (токены на задачу, cost-per-task) могут сильно расходиться с реальным потреблением токенов в продакшне из-за сдвига в том, что пользователи готовы спрашивать у более дорогой модели.",
      "type": "tool-caveat",
      "actionable": "При выборе модели для агентного пайплайна не полагайся только на синтетические бенчмарки — сверяй с реальными логами использования на своих задачах перед миграцией."
    },
    {
      "claim": "Заявленный вендором паритет цены/скорости с предыдущей моделью не гарантирует такого же паритета по реальному расходу токенов и итоговой стоимости на задачу.",
      "type": "tactic",
      "actionable": "Перед переключением стека инференса замерь cost-per-task на собственном наборе реальных запросов, а не верь марketинговым сравнениям 'та же цена, что и у прошлой модели'."
    },
    {
      "claim": "Экономический смысл смены провайдера инференса определяется не только качеством модели, но и субсидированием через подписку (например, у Claude/Codex подписок оно выше, чем у альтернатив без скидок).",
      "type": "principle",
      "actionable": "Считай миграцию между LLM-провайдерами как задачу TCO: сравнивай не сырую цену токена, а фактическую стоимость с учётом подписочных лимитов и субсидий, которыми ты уже пользуешься."
    }
  ]
}
```
