---
session: s_0e3cc802
date: 2026-09-27
words: 1961
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0e3cc802` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The $10 Trillion Token Economy — Alex Atallah, OpenRouter & Anjney Midha, AMP
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
Hey, there's a new type of unit of value that's being streamed across the internet called a token. And over the next 10 years, the entire internet value chain was going to have to deal with the fact that like the more valuable tokens got, the more bad actors were going to go to try to get their hands on those tokens. And anytime you scale something and the payload gets more and more valuable, more bad things people try to get access to that value. Online payments, you know, is started roughly in the 80s and '9s, right? And grew to over a trillion dollars over the next 10 years, and we needed to build entirely new payment solutions to deal with online fraud. um where we are today is roughly there on tokens, but over the next even five years, we're expecting the token economy to get to like roughly $5 trillion. And over the next 10 years, I'd be shocked if we went to 10 trillion of token flow. We we blocked 10x as much dollar volume last month as the month before, and the types of token fraud are diversifying quite a bit. Before we get into today's episode, I just have a small message for listeners. Thank you. We would not be able to bring you the AI engineering, science, and entertainment content that you so clearly want if you didn't choose to also click in and tune into our content. We've been approached by sponsors on an almost daily basis. But fortunately, enough of you actually subscribe to us to keep all this sustainable without ads, and we want to keep it that way. But I just have one favor to ask all of you. The single most powerful, completely free thing you can do is to click that subscribe button. It's the only thing I'll ever ask of you, and it means absolutely everything to me and my team that works so hard to bring the Inspace to you each and every week. If you do it, I promise you, we'll never stop working to make the show even better. Now, let's get into it. >> Okay, we are here in Anj's house, which is where all great startups in San Francisco start. >> Howdy. U and congrats on cursor mist. Uh I don't god knows what else. You got so much stuff going on. >> There's there's a lot going on. Well, open router is probably the most has been the most I would say one I'm excited about recently. >> Yeah. And we have Alex uh first time on the pod, but uh you've been a a few times. I appreciate every time you shown up uh for the community. Congrats. I just like what a journey. When I was looking back at your past posts, one of the earliest principles that I saw you write as a sort of product person is pub sub as a product principle. And I wanted to you to maybe explain how you think about what should exist in the in the world. >> Yeah. The the pub sub piece which was early 2023. I didn't think about it until we we we talked like 10 minutes ago is about how there there is like a way of thinking about products as an intersection between subscribing to data and publishing data and marketplaces are an easy easy example of this. You have suppliers that are publishing some kind of product to a skew. And the skew is kind of like a pub subtopic that a consumer is subscribing to and just going to like consume whenever they want. And humans consume in a very like discreet ad hoc way. It's not very scalable. You know, all their attention is on the topic when they're buying the thing and their attention is nowhere else when that happens. um agents and and consumers of inference don't act like that. They're consuming continuously and they're changing the SKUs that they consume from all the time. So open router is sort of like a blend between a you know a normal API experience and a marketplace where we create model slug. We have the auto router. We have all kinds of like product SKs that you can subscribe to and and then you can like continuously add like uh derive value and make decisions based on those uh those consumers. >> Yeah, this is something that was more consensus now but not consensus when you guys started which was that there is such a demand for swapping models and changing things out and uh that people would not use use the native SDKs. I guess uh for each of you, what was your sort of realization moment that this would this would be it? I you've you've given a talk at EIE about alpaka as like one of your inspiring moments? >> Alpaca I can like rehash the alpaca moment for a sec. Like the very beginning at the end of 2022, OpenAI was the only game in town. There was like OpenAI Coher um and then a a smattering of of like early attempts at openweight models. Um, when Llama came out in January of 2023, it was like, "Wow, really exciting. This is really big. It outperforms GPT3 on one or two benchmarks." Uh, but you can't chat with it. It wasn't like an it wasn't actually an engaging model. But it seemed like someone just needed to fix a couple things and do some RHF on it to get it all the way there. And Alpaca was the first model that I saw that did that. It only took $600 to do. A team at Stanford generated a bunch of synthetic data, fine-tuned llama, and made alpaca 7 billion parameter model or was it maybe it was 13 billion parameters and it was so good like I was just like on an airplane using it. I I you know in many cases I like you could not discern a chat GPT versus an alpaca result and I figured if if it was this easy to make a model um one we have a whole new way of monetizing data for the first time um you can just like take really valuable data and turn it into a service in $600 uh and that cost will probably go down over time. When you say so sorry uh when you say monetizing your data as uh what eventually will become an FCP endpoint or or as a training data for a model. >> Yeah. Training data for a model like an abstract way of saying like hey I have this data >> compress it into a model >> like it makes sense for me in my product but like I could repackage it in the form of a model and sell it. And so it's just a whole new business model for the economy. It also of co
...[middle elided]...
 global GDP growth is like a huge percentage of that, I think, is going to be fraud, abuse, and we might never get there if people just don't trust tokens, right? Um, and I don't think this infrastructure exists. So, you have your work cut out for you with at Stripe, but I don't think people have realized the scale at which agents agent agentic fraud like bad behavior perpetuated by AI agents is about to hit us like a tsunami. >> Yeah. Uh I mean there's a lot to dig into there. Uh I want to give you the last word. We do have to wrap. Um um what can people expect from open router and stripe? >> I mean I think this is a really good way for us to accelerate go to market and um to go up market more quickly. It's also, you know, as an eloquently described, this is there's a really clear better together story here when it comes to improving trust and safety and making it really easy to like accept tokens and let people bring their own inference to your app and to help developers just like build on top of inference. Uh, going forward, we have a really strong brand with Open Router and we're keeping the brand. So like open router like as a as a product and the road map and the name and the brand like you know is staying the same and so what like you should expect you know in this next 6 months is that most things will be like what we would have done had we been independent except everything will be moving faster and that that's kind of like our you know near-term goal longer term hopefully I can comment on it soon but I can't now. Okay. Well, uh, we'll hopefully do a follow-up at some point. Uh, but thank you for being so generous with your time and, uh, congrats on the partnership. I mean, this is one of the most beautiful bromances I've seen in a >> just starting >> starting from Stanford to here. >> Lots more to do. Lots of sheriff policing to do of the >> of the town the token economy. We need new we need new sheriffs for sure. >> Yeah. Awesome. Thank you. >> Thank you.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "llm-token-economy-infra",
  "signal": 0.25,
  "novelty": 0.3,
  "actionability": 0.15,
  "evidence": 0.35,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Это в основном интервью-анонс партнёрства OpenRouter+Stripe с хайповыми прогнозами про '10 триллионов токенов' и рост мошенничества с агентами, без конкретных инструкций для инженера.",
  "knowledge_units": [
    {
      "claim": "OpenRouter описывает свой продукт через принцип pub/sub: провайдеры моделей публикуют 'skus' (модели/маршруты), а приложения/агенты непрерывно и адаптивно 'подписываются' на них, в отличие от разового человеческого выбора модели.",
      "type": "principle",
      "actionable": "При проектировании мультимодельных систем закладывать возможность динамической смены модели на лету (auto-router / fallback между провайдерами), а не жёстко хардкодить один SDK/модель."
    },
    {
      "claim": "По наблюдениям OpenRouter объём мошенничества с токенами/оплатой инференса растёт кратно (10x месяц к месяцу) и будет диверсифицироваться по типам, аналогично тому, как рос фрод в онлайн-платежах в 80-90е.",
      "type": "tool-caveat",
      "actionable": "Закладывать в биллинг и API-прокси для агентных систем защиту от абьюза оплаты/квот заранее (rate-limits, верификация платежа, мониторинг аномального расхода токенов), а не постфактум."
    }
  ]
}
```
