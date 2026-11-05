---
session: s_79a7ba63
date: 2026-09-20
words: 2012
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_79a7ba63` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Vertical Mobility: Inference from MVP to Trillion-Parameter Workloads — Sitanshu Gupta, CoreWeave
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Good afternoon everybody. Um I'm Satan Shu from Kov going to be talking about vertical uh mobility. It's a quite a fancy topic uh the title that we came up with but basically going to be talking about the inference platform that we have at Corv that we are building to serve small to big models and various different types of workloads. Uh a quick intro about me. Um I joined core just about four months back. Uh leading all of inference over there and um before this I was managing everything at AWS Anapuna labs for uh training and before that inference and training at SANOVA. So quite a bit of experience in uh in this particular space. Um what I will the way I'll be taking you through is explaining to you the consumption models that we have and from that how we have derived what the platform should look like so that we do not need to keep changing the platform and we keep making enhancements in the platform that we have for serving inference and how and why the why performance plays such an important role over there. Uh I think a little bit of this might be common with the previous topic that was discussed over here. [snorts] Um consumption models. So we have uh at large two biggest consumption models. One is a serverless which is where the customers can come in, consumers can come in uh do not need to worry about managing the hardware themselves. Do not need to worry about managing the clusters orchestration anything at all. There's API, there's UI, you come in, you pay per token uh and you get your model served. Um biggest thing over here is that uh the type of models uh that we serve in the catalog that is the breadth of models that the customer will be able to go through. Uh I'll talk about dedicated and then I'll come back to serverless because there is one thing unique on the serverless side. Dedicated inference service that we provide is more for customers who want to know exactly what hardware they are going to be using and running on. Uh but the model deployment also depends on them. So they use our service, they use our orchestration layers. Uh but the model deployment depends on them. Model performance also depends on them as long as we provide in the platform the capability and the knobs to serve those features. Coming back to serverless, uh one of the interesting pieces over here is um typically serverless models are very are noisy neighbor problems where uh if let's say everyone is banging on the exact same model then you might be timing out quite a bit depending on how much capacity I have behind it. So another feature that we have on the serverless side is what we calling provisioned throughput. So as a customer, if you know your traffic profile and if you can let us know about that, we can carve it out specifically for you behind the scenes. You still do not need to worry about what hardware it is exactly running on as long as your throughput, your SLAs's are maintained. So that is another one on the serverless side and that is still charged by by the token but you know that you're not running into the noise enabled problem over there. Um let me take a quick stab at few different types of workloads workload shapes that uh we have um that we are seeing and the ratio between these is like continuously changing though agentic is like really high up there. Uh, agentic and chat kind of very similar. Super high on the input sequence lengths, very low on the output sequence lengths typically. But the biggest difference between agentic and chat being the fact that the multi-turns in agentic are super low latency versus in chats because when you get the response as a user, you have to read the answer and then you respond to it. So there are there are differences over there and that big difference ultimately converts into something uh related to the KV cache management uh but these are these two are both real time and another real-time workload is your voice and videos uh which are study streaming and super latency sensitive on the agent agent and chat side um largely the requirements are from throughput point of view not so much from latency but real-time voice and videos are absolutely totally latency sensitive. Coming to batch, batch is where the SLAs's are like super loose. They run into like way like seconds and minutes. Sometimes for some customers actually even in hours. They're like I'll just throw give me 10 to 12 hours of workload capability and uh I'll throw whatever I can process it whenever you can. uh these batch workloads um the way they come into the picture over here in um deciding uh sorry being the requirement for some of the design choices that we make in the stack. Imagine these uh four different types of workload shapes um in the time dimension you have to play the game of tetris on how you can fit it in to utilize the underlying infrastructure the most. I'll give a high level on how our stack is shaped right now. Um, and I'll walk you through a bit of a request flow over here. So for both serverless and dedicated, if you look at the right hand side of the screen, you'll see that on the platform side we you'll go to the control plane to uh to have your uh authorizations, your rate limitings and your usage being tracked etc. so that we can be built accordingly and uh observability so that we can make sure that we are not violating the SLAs's that have been signed right uh underlying on the platform I've shown at a super high level that we have these different um inference engines VLMs SG langs and tensorl but there are quite there's quite a few quite a bit of detail over here that I'll touch upon uh and underlying that what I'm trying to show over here in green is um various different pieces of hardware. So it's not that um so the platform needs to be capable enough of share of having the workload getting distributed across various different generations of these GPUs [snorts] uh specifically Nvidia GPUs that we use right so let's take up a let's take a few exampl
...[middle elided]...
and spec. uh we do provide capability where if the customer has their data set and they want us to train in speculators for their data sets for better acceptance lens which will ultimately make the output throughput significantly higher. Uh we do have that as well. So but that happens async. We uh we get the data async we train the speculators async and then we deploy the speculators into the customer deployments uh if that's what they wanted. uh you see three screenshots over here. I have posted them from uh the last one month one month's worth of work that uh some of us in my team have done. You can see we came quickly on top of the leaderboard on Kimmy 2.6 2.7 and um those are those are from artificial analysis and going back to the session before this can we trust that that's why for GLM I have the results from open router. So artificial analysis when they run benchmarks they're running very specific workloads open router is actual user traffic uh and you can see uh on the open router side weights and biases so the branding is different but weights and bias is basically k we bought weights and biases about a year back uh you can see the speed over here that we have from our deployment is pretty close to what fireworks is providing us fireworks fast right but underlying techniques that we are using is what I want to emphasize the most over here uh for for performance optimization that becomes critical because ultimately what you want to serve to the customer what we want to serve to the customer is uh price performance benefit quick recap um single platform is what I've been trying to emphasize is what I've tried to show uh two different consumption models serverless and dedicated for customers and within serverless I describe two different consumption models as well pay as you go and provision vision throughput if you care about that and ultimately compounding the gains uh through performance optimizations uh in the stack. That's all. Thank you folks. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "inference-platform-architecture",
  "signal": 0.5,
  "novelty": 0.3,
  "actionability": 0.3,
  "evidence": 0.5,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад CoreWeave про архитектуру inference-платформы даёт полезную таксономию workload-типов и пару прикладных приёмов (provisioned throughput, async speculative decoding), но в основном это верхнеуровневый питч про их стек с не очень глубокими деталями реализации.",
  "knowledge_units": [
    {
      "claim": "Workload-профили (agentic, chat, voice/video-стриминг, batch) требуют разного дизайна инференс-стека: agentic и chat — высокий input/низкий output, но agentic критичен к latency между turn'ами (влияет на KV-cache менеджмент), voice/video — жёстко real-time, batch — SLA в часах и там выгодно 'тетрис'-упаковка загрузки железа.",
      "type": "principle",
      "actionable": "При проектировании inference-сервиса классифицируй трафик по этим 4 профилям и выбирай раздельные политики батчинга/приоритизации/KV-cache под каждый, а не единую очередь на все типы запросов."
    },
    {
      "claim": "Для serverless-инференса 'noisy neighbor' (все ломятся в одну модель → таймауты) решается опцией provisioned throughput: клиент резервирует пропускную способность под свой профиль трафика, но платит всё ещё по токену, без необходимости думать про железо.",
      "type": "tactic",
      "actionable": "Если строишь multi-tenant LLM-сервис, добавь режим 'зарезервированная пропускная способность за токен' как промежуточный слой между pay-as-you-go и dedicated-инстансами, чтобы защитить SLA важных клиентов без полного выделения GPU."
    },
    {
      "claim": "Спекулятивные декодеры (speculators) можно дообучать асинхронно на пользовательском датасете клиента и потом деплоить в его инференс-инстанс для повышения acceptance rate и, соответственно, output throughput.",
      "type": "tactic",
      "actionable": "Если контролируешь стек инференса и есть повторяющийся паттерн запросов клиента, рассмотри офлайн-тренировку кастомного speculative decoding модели под его трафик вместо универсального спекулятора."
    },
    {
      "claim": "Бенчмарки инференс-скорости от Artificial Analysis используют синтетические контролируемые нагрузки, а метрики с OpenRouter отражают реальный пользовательский трафик — это разные источники истины, и сравнивать провайдеров нужно с оглядкой на то, какой из них использован.",
      "type": "tool-caveat",
      "actionable": "При выборе inference-провайдера по опубликованным бенчмаркам сверяй, откуда цифры (синтетический бенч vs реальный трафик OpenRouter), и не доверяй одному источнику без перепроверки на своём профиле нагрузки."
    }
  ]
}
```
