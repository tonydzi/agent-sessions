---
session: s_4afb0468
date: 2026-09-22
words: 1987
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4afb0468` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Jev + Treg is a crazy combo for automation...
CHANNEL: AI Jason (lang=en)
TRANSCRIPT SAMPLE:
So you probably saw this new model Jeff popping up on Twitter for the past few days. C problem try to answer is why the latest model is already so good advanced task like coding and mess but still sucks at basic business workflow and automations like it can handle Olympic mass level problems really well. But when you ask to handle a customer inquiry that involve billings most companies never trust agent or model to make that decision fully autonomously cause reasons kind of come down to two. Why is the overconfidence? You definitely experience agents just saying you're absolutely right. Well, in fact, it is absolutely wrong. So the model today will make judgment call like this without calibrate the actual confidence. While most of business workflow require almost 100% accuracy. That's why human is good. And on the other hand, the cost and speed need to make sense because many business workflow has huge scaled volume. And the reason large model today have those factors is also baked in results from the training process. The large learn model today all goes through this reinforced learning from human feedback process where the model will be fine-tuned based on feedback that human give in chat assistant. But what Jeff take is something they call the reinforced learning for calibrated decisions. So in short it is a model that designed for reliable highquality decision making rather than being creative or assist human. Basically it is model that designed to make a decision giving a set of options but it cannot make up options itself and it cannot output text it cannot write code it cannot reason step by step so as a result unlike normal library model where they are output results token by token Jeff does not predict text but output probability of list of given answer in extremely fast and efficient approach so at a high level it might feel a bit limited but it is just so much faster and cheaper than even the cheapest large model out there. This is comparison I did where I compare Jeff with cheapest intelligent model like GPT 5.6 Luna and quite consistently Jeff is around five to seven times faster and five times cheaper. Though one thing to be aware is that Jeff has this context window of 32K. If your response is bigger currently it can't handle it or you will have to do things like map reduce to work around it. And meanwhile when Jeff output response it not only output you one response it will give you the probability distribution of what it thinks is the right answer. This is a gamecher because for business automation you can finally trust model to operate fully autonomously because every answer it give comes with this confidence score that you can build business logic guar around and all those factors open up some use case that just not possible before. One example is playing games. Previously it's very difficult to get model playing games because it require real time fast decision making but because in games it only have it limit set of input and options and Jeff can processing so fast it can actually play games fully autonomously and my friend also shared this demo with me where someone build this system that can live monitoring any call and give real-time classification for if there are any fraud or issues or frustrations which is a great showcase about what you can do with this type of realtime intelligence and on the other hand it is also really good at browser and computer use because for agent to use browser the hardest part is normally for you to decide which UI elements to click or type because DOM is often very messy. So large learning model either make mistakes or eaten up context window really fast but browser use already integrated Jeff in their stack and achieve much faster browser and computer use. The way it works is that we will send Jeff the task we are trying to achieve the browser interaction history so it understand where we are at as well as a list of DOM elements. Then all Jeff does is predict which type of actions it should do next. Is a click on something type of something? If it's a click, which UI element it should be click on and if it's type, which element it should be typed on and output probability score for each answer. So we will be able to locate the accurate UI element really fast and then it will pair with a small large model to do the actual text generation for interactions like type. So this is one example of how you can use Jeff plus large energy model to complete those task end to end. As we mentioned before, Jeff is basically model designed for business automation especially when things that is require high accuracy or massive amount of data to process that were otherwise not making economic sense with expensive large models. Like here is one demo for internal link mapping. So if you ever build SEO and AEO, you know you want to making sure all your page actually link together to increase page ranking. That will actually require model to race through hundreds of pages and accurately locate the link between pages. With normal model like cloud ops 5, it can take hours. But with Jeff here, it scan more than 500 pages and did a mapping in less than 50 seconds. And we even see some creative use where you can use Jeff to real time customize and change set of copy based on visitors persona. So how do you actually use Jeff model? Fundamentally the way you call Jeff is very similar to how you use structure output from large range model. You pass it prompt or in their case they call a state as well as set of questions like in the support ticket handling example. The questions could be which department should handle this request. You were given instructions about how Jeff should made this decision. You will also give a list of options and each option you can add further descriptions and then the Jeff will respond the answer like this with probability score for each options and there are three kinds different questions you can pass on. One is those type of multi
...[middle elided]...
that is not a real signal versus ones that actually resonate with people that I actually want to learn. So internally we also have this pipeline where it will grab viral post from past 24 hours. Use Jeff to filter which ones are related to product launch. So we will use track to fetch what are the trending and popular posts from past 24 hours alongside the post stats and comments. Then we will use Jeff to classify which one are the organic looking posts which one are likely to be paid and boost traffic and also filter out all the noise that is not part of launch. So I get a good feed every day about the latest trending things that I can learn about. And I also put this as a free tool on the track.j where you can just paste in any Twitter post and we will start triggering the pipeline to fetch the post information, the author profile, the replies and use Jeff to classify if it is a organic content or paid content with full reasoning and analysis. So feel free to use it as well if you want. So this is pretty much how Jeff works and how I use Jeff. As I mentioned before, it is a model that open up so many opportunities for automation that wasn't possible before. And it is extremely interesting when you combine Jeff and track together that fundamentally change the unique economy of a lot of automation process. So I'm super keen to learn what do you build. If you're interested, you can visit track.to/jff P/JEF where we have a few Jeff based automation recipe that my team use and you can just copy paste over or a prompt that you can put in cloud code or codecs where agent will guide you to build type of automation that fits your business. If you're interested learning more technical side I also have more in-depth step-by-step workshop in AI builder club where we have some notebook example of all different tricks and tips on using Jeff and a step-by-step guide on building some of those workflow from scratch. So if you're interested you can join the AI builder club as well.

---

> `Bash` -- {"command": "echo done"}

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": true,
  "topic": "calibrated-classifier-model-automation",
  "signal": 0.35,
  "novelty": 0.35,
  "actionability": 0.3,
  "evidence": 0.25,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 75,
  "why": "За хайпом вокруг нового узкоспециализированного 'решательного' модели и рекламой собственного инструмента/курса автора скрыт один реальный архитектурный паттерн (классификатор с калиброванной вероятностью вместо генерации текста), но без кода, независимых бенчмарков и деталей внедрения.",
  "knowledge_units": [
    {
      "claim": "Для задач бизнес-автоматизации с высокими требованиями к точности и объёму можно использовать не LLM, а специализированную модель, которая не генерирует текст, а выдаёт вероятностное распределение по заранее заданному списку вариантов ответа.",
      "type": "principle",
      "actionable": "Если задача сводится к выбору из конечного набора опций (классификация, маршрутизация, эскалация) — рассмотреть узкую 'decision'-модель с confidence score вместо дорогой LLM, и завязать бизнес-логику на пороги уверенности."
    },
    {
      "claim": "Для browser/computer use агентов предлагается связка: быстрая модель предсказывает вероятность того, какой DOM-элемент кликнуть/куда вводить текст (по списку элементов страницы), а отдельная небольшая LLM отвечает только за генерацию текста ввода.",
      "type": "workflow",
      "actionable": "В агентах для браузера разделить задачу 'выбор UI-элемента' (классификация по списку кандидатов) и 'генерация текста действия' (LLM) на два разных, специализированных под свою задачу шага — это снижает расход контекста и ошибки на грязном DOM."
    },
    {
      "claim": "У такой класс-модели контекстное окно ограничено (~32K токенов по заявлению автора), при большем объёме входа нужен обходной приём вроде map-reduce.",
      "type": "tool-caveat",
      "actionable": "Перед выбором подобной модели для задачи с большим контекстом заранее спроектировать разбиение входа (map-reduce/чанкинг), а не полагаться на единый вызов."
    },
    {
      "claim": "Автор заявляет скорость в 5–7 раз выше и стоимость в 5 раз ниже, чем у самых дешёвых LLM (например GPT-5 mini) — но это его собственное неаудированное сравнение, без методологии.",
      "type": "benchmark",
      "actionable": "Не принимать заявленные цифры на веру для продакшен-решений — прогнать собственный бенчмарк на своих данных перед тем как закладывать выигрыш по цене/скорости в архитектуру."
    }
  ]
}
```
