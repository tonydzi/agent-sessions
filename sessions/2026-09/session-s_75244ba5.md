---
session: s_75244ba5
date: 2026-09-27
words: 1966
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_75244ba5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: 🔬 The Physical World Is More Forgiving Than You Think — Anima Anandkumar, Caltech
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
So we you know set out looking for interesting examples and one of them was like weather modeling because the weather data is open source and so given that the data was there we were like okay let's just go try it right and that's the beauty of it to whenever data is available it's really good news but a lot of weather scientists did caution us back then this is back in 21 and they said no no no this is so difficult you know there been decades of development in traditional weather forecasting and that's very careful full bottom up physics- based modeling, right? So assuming, oh, this is the fluid dynamics, can you go predict the weather uh the next day and so on. And so that's how a lot of the thinking was that AI is just not going to be able to beat uh the decades of work in weather modeling. uh but to our surprise we just went ahead we trained them we used neural operators to [music] be able to effectively capture the phenomena and then we found that it's not only accurate it's [music] almost as close to what the traditional weather models can do accurately but also tens of thousands of times [music] faster so what would take a big supercomput to run can now be run and we only needed a consumer grade like GPU like you know it was a small model it fit very well. It's very [music] fast and it's accurate. And I think that just changed everybody's thinking. >> Welcome to Leaden Space. Um this is the AI for science section of Lean Space. Um I'm Brandon. I work on RNA therapeutics using AI and atomic AI. I'm joined by my co-host R.J. Honiki who develops uh uh spatial transcrytoics and is the CTO and founder of Mirror Omix. Uh today we're excited to be joined by Ana Ankumar uh the brin professor of uh mathematics and computer science at Caltech. Um Ana has done all sorts of really cool work uh combining AI with basically models of the physical world. Um and has a really diverse background. I don't think I could even remotely cover it. Um but anyway, I'll let Anna introduce herselves. Thank you for coming on the show. >> Yeah. Yeah. Thank you Brandon and R.J. It's a pleasure to be there and I really like the term latent space because that very much figures in a lot of my work uh because it's really you know the world is latent uh but yeah just as a brief introduction uh you know I've been working in AI for more than two decades uh in a way you know before even deep learning when a lot of the theoretical foundations had to be built for probabistic models I worked on them and then as deep learning started taking off. I also had a foot in industry until recently. So I was at NVIDIA, I led AI research there and before that at Amazon Web Services helped found the cloud AI team and build the first cloud AI products uh uh back almost a decade ago. So you know like kind of having this one foot in industry and academia I think has given me a lot of interesting perspective of how to bring theory and practice together and think of AI at large scale but also AI that is principled. >> A lot of your work has been related to the modeling of physical systems um using certain types of physical systems uh which you model with differential equations and you uh help model them with using machine learning. So um maybe first let's go ahead and talk a little bit about that as a high level but we'll get to kind of the details about listening neural operators and some of the applications like weather later but first I'm actually really curious to hear about torch lean and how this uh recent work you've been doing connects with that um larger research program >> to me broadly like you know my thesis is AI and science how we bring that together right so uh you know where I started Ed at Caltech almost a decade ago that's when you know my passion was always science was physics and but you know I was doing AI so how to bring that together was where you know the first kind of foundations got laid there and to me like you know there are several aspects to that one is people have been thinking how to use language models for science yes you can do a lot of hypothesis generation you can have ideas But ideas are not enough, right? So you can have a lot of ideas. The bottleneck is going testing and verifying that they work in the real world. And so this aspect is where a lot of my recent focus has been on how do we ensure that we can build AI that has guarantees that it will work in the physical world or any aspects in scientific domains. and and one way to think about it is you know can we model the physical world and keep the physics correct and that's where neural operators come in. The other aspect is can we verify symbolically certain aspects. Uh for instance you know if we claim that the theorem is correct we have to go verify that you know that's where lean as a formal language can be useful for verification. So how do we bring that together with language models is where a lot of mathematical reasoning has been at the forefront. And so torch lean kind of is in that realm where we say you know not only that you want to verify mathematical statements. You may want to verify uh what neural networks themselves claim to deliver. You know for instance if you're now using a neural network and you want to ask whether it's going to be robust. Say you want to use a neural network in a control loop. you want to control um you know whether it's a drone, whether it's uh a nuclear reactor. So all of this ultimately when we build AI systems with deep learning into control loops, we want robustness and so now torchan can help us do those verification seamlessly. So we can now have neural networks be part of the verification loop and have confidence that we can use them appropriately. We have already discussed on the podcast lean and uh and everyone should probably be familiar with neural networks. How but neural networks seem very unconstrained. What kinds of proofs are you talking about? Are you talking about bounds on the outputs, inpu
...[middle elided]...
 is if you could pick a bottleneck in your domain that you could magically remove, what would that be and why? >> More compute, you know, that's [laughter] >> I know that's an easy one, maybe a lazy one, right? because you know and and you know of course our compute that we have is growing so much more than even a few years ago thanks to Nvidia thanks to others >> again [laughter] >> so no comments on that but what I mean by that is also like for research enabling more and more compute you know it's very important I know there are national labs building more supercomputers uh you know hoping that we can have more compute for research. But I think you know without that we cannot experiment, we cannot innovate. I think this is a part that I push a lot and you know I think I cannot emphasize that it's so critical. >> If you had a call to action or um something that you would like people to do or think about or or learn about, what would that be? >> Yeah. So you know you can go to neural operator libraries so you can kind of hands-on play with different architectures recipes you know look at use cases uh but also think about like you know AI for science is not just language models and agents yes that's one aspect of it but ultimately you know those are still like external rappers in a way right until we have AI that fully understands the physical world not just as symbols but as one that can simulate and design and control based on that. You know, there's a [clears throat] big piece missing. So that's the other aspect that I think that people should really think about AI for the physical world in this way. >> Anime, this has been so fascinating. Um I'm I'm excited to check out neural operators myself. I have some ideas in my head already. I really appreciate you taking the time to sit down with us. >> Thank you, Ar. Thank you, Brandon. I really enjoyed it and we really dug deep into a number of things. So, I appreciate you doing that. Thank you. >> Thank you. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "ai-for-science",
  "signal": 0.35,
  "novelty": 0.4,
  "actionability": 0.25,
  "evidence": 0.5,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Интервью в основном мотивационно-обзорное, но содержит пару конкретных технических утверждений про neural operators и формальную верификацию, применимых на практике.",
  "knowledge_units": [
    {
      "claim": "Neural operators (нейросети, аппроксимирующие операторы физических уравнений) способны предсказывать погоду почти так же точно, как традиционные физические модели, но в десятки тысяч раз быстрее и на потребительской GPU вместо суперкомпьютера.",
      "type": "benchmark",
      "actionable": "Для задач с известной физикой/PDE (погода, гидродинамика, симуляции) вместо full-scale физического солвера пробовать neural operator как быстрый суррогатный движок, особенно если данные для обучения открыты."
    },
    {
      "claim": "TorchLean связывает PyTorch-модели с формальным языком доказательств Lean, чтобы верифицировать заявленные свойства нейросети (например, робастность) до её использования в критичном control loop (дрон, реактор).",
      "type": "tool-caveat",
      "actionable": "Если нейросеть встраивается в контур управления безопасно-критичной системой, рассмотреть формальную верификацию через Lean/TorchLean вместо одного лишь эмпирического тестирования."
    },
    {
      "claim": "Основной бottleneck AI для науки — не генерация гипотез языковыми моделями (это дёшево и легко), а проверка и валидация этих гипотез в реальном физическом мире.",
      "type": "principle",
      "actionable": "При проектировании agentic-систем для научных/инженерных задач закладывать отдельный слой верификации результата (симуляция, формальное доказательство, физический эксперимент), а не останавливаться на этапе генерации идеи LLM-агентом."
    }
  ]
}
```
