---
session: s_7f34172e
date: 2026-09-27
words: 2015
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7f34172e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Loop Is the Product — Roland Gavrilescu, Introspection
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hello everyone. How's everyone doing? Are you guys ready for some more loops? Yeah. My name is Roland. My co-founder and I were in this mythical place called XAI working hard on agent infra and we realized there's something new that has to be done in a standalone way. So we left a few months ago to really figure out okay what's the next stage of how we should deploy these always on longunning horizon tasks. Um and I'm happy to announce we have a few findings that we would like to present you. Um, and this talk it's all about um, how you should productize these ideas in ways that can scale with your customers. Um, you've heard a lot about auto research. Um, we think there's a blueprint for 2026 and beyond on how you should think about auto research and it really comes down to three ideas. Let's go through the first one. The loop is the product. We're all familiar with this. We've started with everything goes down to RL chief for models and how you should train the model to become better and better reasoning. We then quickly moved to harnesses and how the model is a commodity and it's all about the harness. And now we're talking about loops and how you should build these loops uh and not touch code anymore. But what does it really mean and why is everyone saying that? Do you guys remember clawbot? That was the original um original name of what is now now now known as open claw. And this guy AJ built the first loop around cloudbot. What he did was to find a way to talk to dealers and talk to Reddit users to get bigger discounts on a car. He followed these four steps. Um and is really open call the one that did it. Go on Reddit, find prices, find inventory, talk to the dealers, put dealers head-to-head, and try to figure out how to make them outbid each other, have a verifiable way to know when the price is right, and then lock in, get the car, and it worked. Um, probably this was when all the Mac minis were uh selling off the shelves, but this was the first real example of loop is the product and something that probably should be a startup at this point. Um, but we've seen how this became a recipe for everyone to build loops. But let's take a step back. Why are we here? Um, we really think models have been trained with this loop in mind. And it comes from this idea of udala loops. It's a terminology coined back in 1970s by the US air force and is the idea of these um jet fighters how to react in fast-paced environments. If you think of models calling tools and taking observations, it's it's what we've been trained on uh as humans but also as as agents. Now, now what happens when you put strong signals and verifiable work uh at the other ends? You get to these workers or cloud code agents. Um and and what matters here is the quality of the signal determines the uh success rate of the loop and the uh quality of the verifi verifier um um is able to calibrate if that success is actually correct or not. But there's another loop here. Um what happens when you take that and feed it back into the signal? And this is what looping around is all about is how do you generate these artifacts at the end of the first loop to then run a second loop on and have a way to continuously improve. And this goes to my second point. System dillation is the mode and is really the ability to understand what went well and wrong in the first loop and know how to process that in the second one. So how do we tune these AI systems? Each loop generates useful information around harnesses, profiles, evals, models, resources, tools, and the environment. What you really want is to have a way to keep this portable, to have a way to version this and to evolve it over time. If you think about data recipes in research, this is how RL started to work really well. you understood the recipes and how to continuously change the recipe to combat some of the behaviors that may happen around hallucinations around reward hacking and then you get to a stack which is your final data recipe. We don't have that for harnesses. We don't have that for like AI systems in the general term. So we thought there's space for something like that. something that contains the evils and contains the tweaks and the human judgment and all these things that are not predetermined at the beginning but they're defined as you learn more about your agent acting in in in the environment. We think recipes can be applied to this and we should use the same name. So an agent recipe is really something that enables you to create reproducible frontier AI systems. It's something that allows you to have a mode that keeps getting better over time, which is not tied to any platform or any provider. It's something that you control lives in your company and is agnostic to the models and providers you use. And loops should focus on this. Loops should be the way you distill these systems into recipes. Failure patterns should become judges and evals. Repeated behavior should become skills and prompts. user frustration, extensions and memories to your harness and so on. You we're all familiar with this, but we didn't have the the the right like terminology of how we should think about it and how we should define it. And we think recipes is a way to put everything together into a git repo and treat it as your ongoing um strategy for for uh building these self-improving systems. So we are introspection but you can think of introspection as the way you generate these recipes. So they're recipes for introspecting on your on your system. We wanted to build something that is portable and provider agnostic. So we built our um approach to recipes on the pi harness and on harbor for evals. We baked it into uh git repos so uh everything could be versioned and agents could have a way to continuously track how this change and why and is meant to be owned by you but managed by your agents. And this is how products should really be built going forward. It's something that treats the owner as t
...[middle elided]...
can reproduce the same service or product uh for other people and they also agree you have great taste and you have great execution. And this is really kind of like the the secret of building good loops is okay can can someone iterate on my um system in a way as uh you know um a good example here is like Miranda from the Delor product right what would Miranda do uh in certain cases and you kind of want to codify that that thinking into like agents that can do the same stuff at a higher level. So the takeaways are this. Um the loop is the product. You try to automate yourself as the u as a um higher level judge and you want to make sure your second loop agents are able to apply the same judgment to to the agents you're trying to to to push to prod. Second bit system dissolation is the mode. So, how do you continuously inject that taste into these uh workers and they how how they continuously self-verify and work together is uh the biggest thing that you should focus on and the faster you do it uh the the the faster you you build a defensible um approach to to becoming a vertical AI company. And finally, valued work per watt is how you should measure um am I making progress or not. So first make sure that uh the the the work you're generating is valuable. Second make sure that the economics makes sense and the um the the difference in price is is basically what um people would would switch away from cloud code to to something you provide. We've been thinking a lot about these ideas and we're building some very interesting products around how to deploy this in production. We'd love to hear from you. would love to get um to to understand more about how how certain um vertical SAS companies are are looking to go to prod with um or how agent labs have been thinking about this idea of um um creating these like auto research uh labs around their their own products. um get in touch. Uh we're gonna be around the block for for chatting more about this. And thank you very much.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-loops",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.25,
  "evidence": 0.15,
  "durability": 0.4,
  "volatility": "volatile",
  "half_life_days": 180,
  "why": "Концептуальный пич-толк основателя стартапа про «loop как продукт» и «agent recipes» — идеи любопытные, но расплывчатые, без бенчмарков и конкретных шагов, местами реклама своего продукта.",
  "knowledge_units": [
    {
      "claim": "Харнес и модель становятся коммодити — ценность и дифференциация смещаются в саму управляющую петлю (loop), которая связывает вызовы модели, инструментов и верификатор.",
      "type": "principle",
      "actionable": "При проектировании агентной системы вкладывайся не в выбор модели, а в архитектуру цикла: сигнал → действие → верификация → обратная связь."
    },
    {
      "claim": "Ошибки и повторяющиеся паттерны первой итерации цикла нужно превращать в постоянные активы: провалы становятся судьями/эвалами, повторяющееся поведение — скиллами и промптами, а фрустрация пользователя — памятью/расширениями харнеса.",
      "type": "workflow",
      "actionable": "После каждого прогона агента фиксируй failure-паттерны как отдельные eval-кейсы и превращай повторяющиеся успешные действия в переиспользуемые skill/prompt-блоки, а не просто чини баг и забывай."
    },
    {
      "claim": "Автор предлагает концепцию «agent recipe» — версионируемый в git-репозитории набор харнесса, эвалов, профилей и человеческих правок, независимый от конкретного провайдера модели, как способ делать агентные системы воспроизводимыми и портируемыми.",
      "type": "tactic",
      "actionable": "Храни конфигурацию агента (промпты, эвалы, инструменты, пороги) как версионируемый артефакт в git, а не разрозненно в коде/памяти модели — это упростит перенос между провайдерами и аудит изменений."
    },
    {
      "claim": "Предложена метрика «valued work per watt» — оценивать прогресс агентной системы через отношение ценности выполненной работы к затраченным вычислительным/денежным ресурсам, а не просто через успех/неуспех задачи.",
      "type": "tactic",
      "actionable": "При оценке продакшн-агентов считай не только success rate, но и стоимость на единицу полезной работы — это даёт аргумент, почему клиент выберет твоё решение вместо готового Claude Code."
    }
  ]
}
```
