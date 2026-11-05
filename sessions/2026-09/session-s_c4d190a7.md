---
session: s_c4d190a7
date: 2026-09-28
words: 1983
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_c4d190a7` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: What It Actually Takes to Build a Software Factory — Tereza Tížková, Factory
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Uh hi everyone. Hey what's up? I'm Teresa. Uh and today I will be talking about software factory. uh everyone is talking about software factory but only few people are actually building one and even fewer people know what it actually takes to build one and how to define it. So I will be talking about what is a software factory, should I build your own or outsource it, what works in production already, what are the main challenges and how much is this all going to cost? Uh my name is Theresa. I work at a company called factory.com and we've been building uh this concept of the software factory for quite a long time but finally uh the technology is catching up and it's possible to build this in production for enterprises like EY or Adobe uh I would define the software factory as the whole loop the whole life cycle of developing software with autonomy which doesn't mean just coding and generating code by that I mean collecting all the signals reacting to user feedback to logs, prioritizing what's important, then orchestrating it all, executing, validating, doing really good uh testing in production and then iterating on all this uh while also continuously improving in the process and gaining new knowledge and new skills. So this is just our dashboard how our software factory looks if you if you look at it and it's catching the whole cycle there. uh this is just some history and by history I mean 2023 in AI. So the software factory wasn't really possible before even though we always had this idea from the beginning of uh CH GPT lounge and others we had this idea of the continuous loop there was autog baby agi already with the concepts of iterating on the software but it didn't work before because the LMS were hallucinating there was problem with context length uh problem with the reasoning quality uh different problems like this or we were missing good environments where the agents can actually work in the isolation. So all this kind of led to why the software factory is the paradigm that's starting to be popular now and actually useful. I like to define things by what they are not. So I want to say software factory is not just coding agent and it's not even a swarm of coding agents even thousands of agents because generating code writing code that's the easy part compared to all the others. uh engineers don't even spend most of the time uh just writing code. The challenges are the rest of it. Uh so this is what I want to enhance and it's also not just some consultancy or just some abstract strategy that someone will try to sell you and to your organization. Uh I think the approaches are of course different but we believe you should really rebuild your organization from ground up to be ready to become a software factory like you can't invite a consultancy and just throw something in the middle of your organization. You should really be mindful and rebuild it from scratch. uh this is the approach I like uh showing to building the software factory and I think it's similar to building the real team of humans because there is a lot of agents as I said they will be testing validating iterating and it all can end up as a big chaos uh so you need to be mindful and I would say the three important things is being agnostic in the software factory so being independent of LLM choices uh of how you already work as the organization then you need to be autonomous. So you need to give the agents the right trusts and all this permissions and governance and you need to trust it to run really for a long time because the predictions are that agents will run even a year or more years without the human in the loop. Of course that sounds ambitious but for example our missions already our long runninging sessions already build uh things and run for weeks. So it's not that crazy. And third thing always improving. So same as human organization you need to onboard any new people in your team by giving them good uh code base understanding good structure documentation and also let them improve in the process and gain new knowledge and share it share it within the team. So these are the three points and now let's talk about the agnostic one. Uh I think the important thing to point out if you are a builder and building different primitives of the software factory you need to be ready for how everyone is already working you need to work across environments like Slack, GitHub and connected to everything and you need to also allow people to already bring subscriptions they are using because there is every every time there is like new technology, new frontier models, uh new benchmarks and it's so difficult to catch up but also to predict what we'll be winning. So it's best to be agnostic for everyone. Uh then there's the topic of being agnostic to models. Uh this is a topic of a lot of discussions recently and this chart is from this chart is from CEO of Coinbase uh who tweeted about how they started uh started saving money in their organ or organization on AI but without reducing the token spend. So the black line is how much they spent on tokens. They continue growing and token maxing but they stopped spending so much money. Uh how they did it uh different tricks like different default default models for people. So stop pushing people to use only the frontier as a default. Then caching of course uh to stop preferring the stuff every time. And then no limits on spending but just needing to see the results if you spend a lot. And the last thing that's really important topic is routing. So smart routing between LLMs and just a token optimizing between uh the LMS instead of just spending so much tokens. Uh we built uh a thing in factory called uh automatic model routing and there's been a lot of questions around it but what it does is it automatically routes between different models in your process. The important thing is it decides first what model is most optimal and then uh it can switch to different model if it's failing th
...[middle elided]...
ating our documentations and uh yeah and um reviewing and documenting what you have. So the question is what will happen to us humans if we build software factory like this? Uh will humans just lose jobs and go to permanent underclass? I think they will not. And uh I want to be positive. So I'm thinking of this parallel of humans just moving up uh levels up to the uh to the cooler tasks than before. I think we actually had before the same same experience of us as humans abstracting some levels up and we actually started ourselves as human computers. We actually were the computers doing all the most detailed stuff at the beginning. Then we had programming languages codifying some of it, abstracting and then coding agents. So outsourcing some of it but uh still being in the loop very closely uh and very monitoring everything. And now we are moving kind of up to software factories where we manage these agents as I said orchestrator agents and workers and validators and all these teams structured teams of agents that work really continuously in the loop and we just monitor and decide what to build. Uh so I want to really end this positively. We should be as humans deciding what to build in the software not how to build it. uh because that's up for the agents and by this uh continuous cycle of autonomous software I think we can actually achieve that. Uh this is one warning chart or if someone thinks AI will take the cool cool stuff from us. I believe actually it will take the annoying stuff and in enterprises and organizations you already spend a lot on alignments on the meetings as I mentioned basically the thing behind between the lines that you really need you need to get context from everyone share your status sync on the things on meetings so all these things could be actually outsourced to your software factory and you could be just talking about the cool stuff okay so this is it thank you so much go touch some grass and let your agents uh built for you. Thank you.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-software-factory",
  "signal": 0.45,
  "novelty": 0.3,
  "actionability": 0.35,
  "evidence": 0.3,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад скорее концептуальный питч про 'software factory' от сотрудницы factory.com с рекламным привкусом собственного продукта, но содержит пару пригодных к использованию тактик по маршрутизации моделей и контролю расходов на токены.",
  "knowledge_units": [
    {
      "claim": "В enterprise-практике снижают счёт за LLM без снижения расхода токенов: дефолтные более дешёвые модели для большинства пользователей, агрессивное кэширование запросов, без жёстких лимитов трат — но с требованием показывать результат при больших тратах.",
      "type": "tactic",
      "actionable": "Настроить per-user дефолт на более дешёвую модель вместо фронтира по умолчанию, включить кэширование одинаковых промптов, а траты контролировать через отчётность/ROI, а не через хардкап."
    },
    {
      "claim": "Автоматическая маршрутизация между LLM в проде выбирает сначала оптимальную по задаче модель, а затем переключается на другую, если первая модель проваливает задачу.",
      "type": "tactic",
      "actionable": "Реализовать fallback-роутинг: primary-модель для класса задач + автоматический ретрай на другую модель при детектируемом провале (ошибка валидации, тест не прошёл и т.п.), а не слепо слать всё на самую дорогую модель."
    },
    {
      "claim": "Автор формулирует 'software factory' как непрерывный цикл: сбор сигналов (фидбек, логи) → приоритизация → оркестрация исполнения → валидация/тестирование в проде → итерация, а не просто кодогенерация агентами.",
      "type": "principle",
      "actionable": "При проектировании агентной системы разработки закладывать явные стадии сбора сигналов и валидации в проде, а не ограничиваться генерацией кода — иначе основная инженерная боль (не кодинг) остаётся неавтоматизированной."
    },
    {
      "claim": "Заявлено (без детальных доказательств), что автономные агентные 'миссии' в проде уже выполняются неделями без участия человека в цикле.",
      "type": "benchmark",
      "actionable": "Относиться к заявлению как к анекдотическому ориентиру, а не как к воспроизводимому бенчмарку — перед копированием подхода запросить конкретные метрики надёжности long-running агентов у источника."
    }
  ]
}
```
