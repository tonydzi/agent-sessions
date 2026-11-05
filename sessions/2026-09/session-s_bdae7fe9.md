---
session: s_bdae7fe9
date: 2026-09-27
words: 1959
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_bdae7fe9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Why LLM Recommenders Will Be AI's Biggest Consumer App — Devansh Tandon, Meta
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Welcome everyone. Thank you for coming out to the LM Rexus track. Um I'll be sharing the first talk. Uh my talk is titled tokens and engagement out training LM recommenders. Um, and I want to make two big arguments today. The first is that recommendation systems scale just like LMS do and that the field is very early in that scaling curve. Um, and the second is that the LM recommener is going to be one of the biggest consumer applications of AI. Um, okay. So, quickly about me. Uh, I currently work at Meta on research and product. Uh I lead a team called Meta Recommendations Research uh which is this group that's training frontier models, LLMs and recommenders that power Instagram, Facebook ads, the meta family of apps. Uh before this I was at Google for a long time uh working on a lot of the key ML teams including deep mind and YouTube. Last year I gave a talk at AI engineer called teaching Gemini to speak YouTube about two ideas semantic IDs and generative retrieval which we also wrote two papers about which I've linked here. Um it was really fun and it led to a lot of discussions and collaborations. Uh the ideas behind semantic ID and generative retrieval have really taken off in the industry over the last year. Um and they've moved from more research to now scaled production systems. And I've seen exciting launches and papers from YouTube, Meta, Spotify, Door Dash across the industry. And we have a couple of examples of that later today. This year I want to talk about four uh sections. Recommendation scaling curves, a framework of four, recommendation paradigm scurves that we are climbing as an industry. um sharing the recommener recipe and finally this consumer AI app framework. Um let's start with scaling curves. So I wanted to start with this landmark scaling curve paper from 2020 which feels like a lifetime ago. This is when Daario was still at OpenAI and Anthropic didn't exist yet. But the core idea that this paper shared is the power law of scaling. As you increase model size, data, the amount of compute flops trained uh for model training, the loss falls on this log linear scale. And this clean and predictable curve is what really set off the race for the AI frontier because you can forecast what model quality and capability improvements will look like. And this is what's underwriting the massive capex investments and the AI buildout today. It turns out that recommendation systems follow a very similar scaling law. In fact, before this wave of LLMs, Rexs were the largest production ML models in big tech companies. And they're still some of the largest models that are served at a scale of a billion plus daily active users. And they follow this similar power loss scaling curve. On the x-axis, you have data, compute, and model size. And on the Y ais you would see falling loss or in this chart uh an improvement in recommendation quality. In offline evals it's net entropy or AU gains and then when it's translated to a real production launch it's engagement impact revenue impact at some of the biggest consumer app scale. Here's a real example from Meta that demonstrates these power loss scaling curves. uh there's a paper the first is a paper HSTU from 2024 and the second is a followup from this year both demonstrate that as we scale model size compute and data we see this clear improvement in offline eval of recommendation quality scaling curves aren't just academic research they're driving real product impact at scale for some of the biggest consumer businesses in the world here's a couple of examples I have from Meta's recent earnings reports. Um, Instagram reels had a strong quarter, 30% year-on-year watch time. And, uh, the optimizations we made to improve the quality of recommendations included simplifying our ranking architecture to enable efficient model scaling and longer interaction histories to identify a person's interests. uh we doubled the length of user interaction sequences used for training Instagram and increased the richness of each user interaction. So these are direct parallels to the power loss scaling curves for LLMs. And I want to introduce this idea of a flywheel of tokens in engagement out which is what's powering all of these Rex model scaling. You train a model. You then run inference on it which is the tokens in that recommendation model results in better content recommendations. It drives consumer engagement, daily active users time spent. It translates to monetization and ads or subscription which pays for the next model training run. And so every step on the scaling curve is one loop around this flywheel. And a lot of consumer apps are spinning this core flywheel at the heart of their business. So we have a long way to scale these recommener systems. I want to talk about the four paradigms that I see the industry progressing through. The first scurve was more traditional Rexus where this scurve focused more on feature engineering and user and content embeddings. Most production systems are still sitting on this curve. they're running some type of two tower sparse network rankers scaling the embedding models. I don't think this curve is going to go away but model development here will be accelerated with auto research and things like feature engineering will be handled by agents uh rather than real ML engineers. The next curve is kind of LM inspired models where you are scaling models ideally end to end. HSTU and one wreck papers are examples in this paradigm. I think this is where the leading recommener systems in the industry are largely operating today. I think the next scurve will be this paradigm of LLM native where you adapt a base model that understands and can reason uh and adapt it for recommendation tasks. The tiger and plum papers are some examples of this paradigm. And I think the final paradigm that I start to see emerging is agentic where LLMs will start to orchestrate Rex systems in a loop. I think there's a parallel here with codi
...[middle elided]...
r or an address to existing content because the content supplied on these content feeds is uploaded by creators. There's a very healthy creator economy and so the supply of content is effectively free or it's uploaded by creators. For the AI chat apps, they have to decode every token of content themselves and the amount of tokens output in every turn of an LM chat interaction is a few thousand tokens. Uh, and the the big difference here is that every token has to be manufactured by the app at inference time. And so what that means is if you compare these two apps on how much inference cost and compute is spent to generate an hour of consumer engagement, there's a huge structural gap where content feeds are significantly cheaper up to 100 times or more cheaper than AI chat apps because they're decoding pointers to content rather than content itself. Um, finally I want to kind of end with why I think LM Rexus is one of the most significant consumer AI applications. If you look at the top apps by daily active users, these are the top 10 apps. Four out of 10 of them are content feeds. And so this is a really significant consumer uh application. If you look at the content feeds, almost all of the consumer app growth on both the engagement and monetization side is driven by the recommener and ads models. And these are going to be entirely transformed by LLM recommenders. It's a very large and very token efficient application of AI for consumer apps. We're going to see a lot of new product experiences come through with steerable and interactive recommendations, explanation of recommendations, and just putting more users in control of their experience on these apps. I think we're going to see some really exciting research on consumer agents and recommendation agents that come out over the next year or so. Um and so this is why I think this is a super exciting area of both research and product uh at this intersection of LLM and recommendations. That's all. Thank you so much.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "llm-recommenders",
  "signal": 0.6,
  "novelty": 0.55,
  "actionability": 0.4,
  "evidence": 0.7,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Исследователь Meta даёт структурную модель эволюции рекомендательных систем (от two-tower до LLM-native и агентных) с реальными метриками из продакшена, но без конкретных инженерных рецептов для немедленного внедрения.",
  "knowledge_units": [
    {
      "claim": "Рекомендательные системы подчиняются тому же степенному закону масштабирования (power law), что и LLM: рост данных/компьюта/размера модели даёт предсказуемое падение loss и рост качества рекомендаций.",
      "type": "principle",
      "actionable": "При проектировании ranking-моделей закладывать offline-eval кривые (AUC/entropy vs размер модели/данных) как инструмент прогноза ROI перед масштабированием инфраструктуры."
    },
    {
      "claim": "Индустрия проходит четыре парадигмы рекомендательных систем: классический two-tower с feature engineering → end-to-end LLM-inspired модели (пример HSTU) → LLM-native адаптация базовых моделей (TIGER, PLUM) → агентный подход, где LLM оркестрирует рекомендательный цикл.",
      "type": "framework",
      "actionable": "Оценивать текущий rec-стек компании по этой шкале зрелости, чтобы понять, какой следующий шаг даст наибольший прирост (например, переход от feature engineering к end-to-end sequence-модели)."
    },
    {
      "claim": "Контент-ленты (Instagram, TikTok) при инференсе лишь декодируют указатель на уже готовый контент, тогда как LLM-чат-приложения генерируют каждый токен сами — из-за этого час вовлечённости в ленте может быть до 100 раз дешевле по компьюту, чем час в LLM-чате.",
      "type": "tool-caveat",
      "actionable": "При расчёте unit-экономики консьюмерского AI-продукта сравнивать стоимость инференса на час вовлечённости отдельно для генеративных фич и retrieval/ranking-фич — это разные порядки затрат."
    },
    {
      "claim": "Техники semantic ID и generative retrieval за последний год перешли из исследовательской стадии в продакшен-масштаб у YouTube, Meta, Spotify и DoorDash.",
      "type": "benchmark",
      "actionable": "Изучить статьи HSTU (2024) и последующие как отправную точку, если требуется reference-архитектура для retrieval/ranking на базе LLM-подходов."
    },
    {
      "claim": "Рост watch time Instagram Reels на 30% год к году частично объясняется удвоением длины истории пользовательских взаимодействий, используемой при обучении ranking-модели, и повышением детализации каждого взаимодействия.",
      "type": "tactic",
      "actionable": "Проверить, ограничена ли текущая ranking/рекомендательная модель короткой историей взаимодействий пользователя, и протестировать удлинение окна последовательности как дешёвый рычаг качества."
    }
  ]
}
```
