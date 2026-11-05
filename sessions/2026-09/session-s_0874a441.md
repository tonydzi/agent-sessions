---
session: s_0874a441
date: 2026-09-27
words: 1931
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0874a441` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: An AI Research Agent That Runs Your Experiments — Tim Sweeney, Weights & Biases
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Okay. Hello everyone and thank you for attending this session. My name is Tim Sweeney, a principal engineer at Weights and Biases and Coreweave. And for the next 20 minutes, we're going to talk about Arya, our new AI research and iteration agent. Let's go ahead and get started. So, uh, first off, just by way of making some noise, some clapping, uh, who here, um, identifies as an ML researcher? You're someone that trains models, trains the brain? I heard one. Wow. Okay. Great work. Great work. Uh, what about who here is the applied engineer, the namesake of this conference? Who here actually builds the bots? >> Okay, good. Expected much more. And who here is in AI management? You are helping fund this compute. Okay. Okay. Nice. From the back. Lovely. Um, well, now that I know a little bit about you, just a little bit about me. Uh, again, my name is Tim. I have a masters in machine learning, uh, and reinforcement learning from Georgia Tech. So, I've been that, uh, researcher currently building Weights and Biases agent, Arya. So, identify as that applied engineer. And in a previous life was the PM of Twitter's ML stack. So, I hope you hopefully can connect with you middle management as well. [laughter] >> [gasps] >> Um today's agenda is kind of broken into three sections and hopefully each of you personas walk away with something valuable. So first we're going to learn about Arya itself and how it can supercharge your AI and ML workflows. We're going to dive into auto research and see that live in a live demo in just a moment. Then we're going to pull back the curtain and learn how we use weights and biases and uh coreweave to actually build Arya because a lot of you in the audience are building agents yourself and we believe a lot of these components can help you in your endeavors. And then towards the end we'll just take a step back and identify a few key tips and tricks for making sure that you're able to productionize your systems effectively. For those of you who might not be familiar, Weights and Biases is the world's leading AI development platform. We've been in business now for nine years and have happily joined the core family about a year ago. Uh we have a number of products in our suite but are really known for our models training inference and weave stack which really helps collect data uh about the AI development and machine learning workflows and makes that information actionable and uh enables users to make the best decisions about what to do next. So without further ado, let's go ahead and dive into Arya, our agent. Uh we'll show a demo and then we'll get back to some slides. Okay, beautiful. Let's make this a bit bigger. Holler at me if you need it to be bigger. So, uh, what you're looking at here is a weights and biases workspace. For you, for anybody that isn't familiar, on the lefth hand side, I actually see a list of a bunch of different experiments. In this particular project, I have over 200 training jobs. And on the right hand side, I see a scatter plot of, in this case, declining metrics, which is good. means our loss is going down over time. And this view would be very familiar for anyone that uses our tool. Now, to ground this, we're actually uh uh using the Carpathy Auto Research project, which I'm sure many of you are familiar with, but if you're not, it's just a very simple project that trains an LLM, and it's a great foundation for auto research type demonstrations because it's a very simple codebase and allows us to improve iteratively over time. So, let's jump back to the project and open up Arya by clicking this blue button in the upper right. When I click this button, I'm uh presented with the familiar chat interface with, you know, how can I help you today, a few call to actions, and you know, I can add different context in my project or maybe add images, etc. Um, everyone here is agent builders, so I don't need to bore you with the details of what an agent interface looks like. But let's go ahead and just, you know, enter in a basic intro here. Let's say, "Hello, Arya. You're on stage at AI World's Fair 2026. Please introduce yourself." So, it's going to go ahead and chug along and hopefully emit some sort of nice emoji. Yay. He I'm Arya. I'm talking to the audience. Great. But now, let's dive into the meat of why you came here. So, I'm going to open up this chat here. And this is a longunning chat where I've been running again over 200 experiments using the auto research loop. Um, it helped me download the code, set up my launch jobs, set up my GPUs, and is able to autonomously iterate on the code itself and the hyperparameters. We'll take a look at what it's doing in a moment, but while we're doing this, I'm going to kick off a live iteration right here. So, what I'm going to say is please conduct another batch of experiments. You are on stage at the AI Engineer Worlds Fair 2026 and we're hoping to find the best model live. I believe in you. Uh, because we know we have to encourage our models. Um, so it's been doing this for a while. What it what it's doing here is it's saying, "Okay, great. Um, I don't want to make a big architecture swing. That feels a little bit too risky." So, it's probably going to go for uh some modifications to the hyperparameters. And then it's kicking off a shell call here that is actually um executing that uh executing that experimentation loop. And we're going to check in on this periodically throughout this presentation. But I want to help explain what's going on behind the scenes. So behind the scenes I have set up a weights and biases launch queue. Launch is our our product that allows you to connect your compute clusters and allows humans and agents to launch longunning experimentation jobs particularly by leveraging GPUs. Here I'm looking at a uh a terminal output of my Kubernetes cluster where we're actually seeing live execution of experiments happening. So this is happening live right here. This is not a fak
...[middle elided]...
called behavioral bugs. Not exceptions, not performance, but behavioral bugs. Next up, tasks and evals are the new world of CI. You've heard a lot about this. If you are a software engineer, you've written unit tests your whole life. You must develop a practice where your researchers are sitting on the same scrum team as you developing tasks and you're viewing the performance metrics as true go no-go decisions. But in order to complement that, you must use humans as a necessary judge. There are behavioral nuances that LLM will not catch. You must be using your product and you must be manually reviewing these traces as a team at the end of the week on a board looking at the best and worst traces to understand how your model is performing. And then lastly, um just maybe one one more tip is to add value through context and tools. It can be really tempting to uh try to overengineer the harness and do a bunch of creative stuff around memory and things like this. We found that a a lot of lowhanging fruit can be ascertained through simply giving your agent context about your business domain, the underlying uh primitives that you have available and your particular uh business data. Um so with that, let's go ahead and check in on our uh our our research agent here and let's go ahead and toggle our workspace. And what we should be seeing is yes indeed a little dot that uh oh okay our previous dot which was done at lunch was 5.83. 831. This got 5.833. So we were right on the edge of having a live improvement, but pretty darn close. Uh so that's what the uh that's what the model was able to produce. It actually uh ran uh quite a few tests here. I see I'm over time, so I will click close pretty soon. But we ran 12 different experiments within that experiment batch and uh we'll be running more all night. So please try out Arya, scan the QR codes, check out the docs. Uh we really love to see what you do with it and um looking forward to serving you. Thank you very much. >> [music]

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-research-automation",
  "signal": 0.35,
  "novelty": 0.25,
  "actionability": 0.4,
  "evidence": 0.35,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 300,
  "why": "Это в основном презентация продукта Arya от Weights & Biases с живым демо автотюнинга гиперпараметров, но в конце спикер даёт несколько практических, хоть и не новых, советов по эвал-практикам для агентных систем.",
  "knowledge_units": [
    {
      "claim": "Тесты и эвалы для агентов — это новый CI: нужно, чтобы исследователи и инженеры сидели в одной scrum-команде и писали таски-эвалы, а метрики производительности использовались как настоящие go/no-go решения перед мёрджем.",
      "type": "workflow",
      "actionable": "Заведите совместный бэклог задач-эвалов между ML-исследователями и инженерами и относитесь к падению метрики как к блокеру релиза, а не как к рекомендации."
    },
    {
      "claim": "Автоматические LLM-метрики не ловят поведенческие баги агента — нужен обязательный ручной разбор трасс людьми (не exceptions, не perf-метрики, а именно поведение модели).",
      "type": "principle",
      "actionable": "Введите еженедельный ритуал команды: просматривать вручную лучшие и худшие трассы агента на доске, а не полагаться только на автоматические оценки."
    },
    {
      "claim": "Наибольшую пользу агенту часто даёт не усложнение харнеса (память, кастомные механизмы), а простое обогащение контекста бизнес-доменом, доступными примитивами и реальными данными компании.",
      "type": "tactic",
      "actionable": "Перед тем как строить сложную систему памяти или инструментов для агента, сначала попробуйте просто дать ему более полный контекст о домене и данных — это часто low-hanging fruit."
    }
  ]
}
```
