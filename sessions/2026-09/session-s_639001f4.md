---
session: s_639001f4
date: 2026-09-27
words: 1879
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_639001f4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Runway’s Bet Beyond Video: World Models, Robotics, and the Neural OS — Anastasis Germanidis
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
effectively the the the [music] end game of something like interface world models is you have a fully neural operating system. So I think uh uh Andre Karopathic has written about that quite quite quite a while [music] back but it's uh you know I think to me it's it's a bit um it's a bit odd that you know we have for example with an [music] interaction with with an LM of today you have this LM that can basically [music] talk talk to you about anything it can you can take the conversation any direction you can it can it's very general so it can solve all [music] those different tasks but you interact with it through a very rigid interface. And so to me it's just a matter of time before the interface [music] itself becomes learnable and becomes you know part of the the the whole loop of like you're not just delivering you're [music] delivering an application end to end and that means you're delivering the language model but you're also delivering the the render and the pixels and [music] and that's also a learnable component. Before we get into today's episode I just have a small message for listeners. Thank you. We would not be able to bring you the AI engineering, science, and entertainment content that you so clearly want if you didn't choose to also click in and tune into our content. We've been approached by sponsors on an almost daily basis. But fortunately, enough of you actually subscribe to us to keep all this sustainable without ads, and we want to keep it that way. But I just have one favor to ask all of you. The single most powerful, completely free thing you can do is to click that subscribe button. It's the only thing I'll ever ask of you. And it means absolutely everything to me and my team that works so hard to bring the Inspace to you each and every week. If you do it, I promise you we'll never stop working to make the show even better. Now, let's get into it. [music] Okay, we're here with Anastasis from Runway with me and Vivu in the studio. Welcome. >> Good to be here. >> Congrats on all your success and progress with Runway. You're opening offices all over the world. Did you envision this when you first started out? >> Uh not quite. I think I think even when we started with we had this idea that you know it was more a matter of when not if uh we were seeing the early generative models of 2016 2017 and just extrapolating assuming you know we resolution quality increases predictably over time there's going to be a point where most of content will be generated. Um and that was maybe the initial the initial thesis of runway was we will need as a result of those generative models rethink how creative tools are made. Um and as we built out the research behind um our generative models it then became clear that they were useful far beyond that as well >> and it is more obvious now with like the real world stuff and the world models that we'll talk about later. I I'm just kind of curious how you go from a background in like ZDOC and [laughter] you know computer vision into runway like take us back to that early conversations with Chris and you know whoever else is on your founding team. Uh I was always split into those two worlds. One was the you know I had my own art practice. I was making a lot of interactive art. um I think for a long time uh and and then on the other side um I was working in startups and I was working as ML engineer as a backend engineer at different different companies. I've always been interested in uh coding and computation and especially interested in simulation and brought it back into my early artwork as well and at the same time I was interested >> personal site has has a few right >> um >> is there is there one we should pull up just just in case there's something that's like I just like to go down memory lane >> okay what is this >> so this was a project that I made I think back in 2015 where I I I built this software that would give uh voice instructions to people in a gallery space. So it would basically coordinate interactions between people and so it will first give you an identity like you're an architect, you're [ВОЗРАСТ] and uh you like sports. Um and then it would match you with another person. You have this completely generated interaction. Obviously language models were not quite there at the time. Um and so it was made it was a mix of some templates and some like some mark of chain generated text. uh and it would just completely simulate this small talk conversations between uh everyone in the in the gallery space. Um so was always very fascinated on on the one end with uh generative models and like the early machine learning work that was paying out that time but at the same time there was this separate thread of simulation and what it means like what can we learn about humans by creating those very simple models of their interactions and their behavior. Did you generate the prompts or you know the [ВОЗРАСТ] whatever was it you generating them? How' you like >> Exactly. So, so the program would just generate those uh from >> Yeah. A lot of it would be kind of m lib style of just you know you have lists of different >> professions, lists of different uh personality types, list of different uh ages, things like that. And then he would just combine those things together. And then maybe the next project we go is Anani Valley, Anani Road, which was one of the first projects that uh we built with uh with uh one of my two co-founders, Chris. This was taking um Pix HD, which was one of the early image to image models that Nvidia released back in 2016 or 2017. uh and it was a model that would take a semantic map of a scene and then generate a photorealistic let's call it uh output obviously very very early days so it was not very high fidelity outputs but it I think was the first image generation model that would generate at uh at 1K resolution and it was all trained on self-driving data sets so the semantic categories it would support were o
...[middle elided]...
ings from one modality or one set of data to to another. So very early days for for that direction but I do think that that's where ultimately what the endgame of kind of simulating the world is. You're not just using RGB, you're using RGB as a starting point, but you can incorporate more and more modalities of the universe and and leverage the transfer that happens from learning from one to the other. >> I guess the the followup there is what's the drawback of omni like why why is everything not an omni model? So why not now? And why would you start from language backbone or image video backbone and then go omni from there? Does it matter? >> Yeah, we need to take it one step. We have to solve robotics first and then we can go into >> solve everything now. [laughter] >> Yeah. I mean I do think there is a lot of open-ended research that needs to happen for uh those omni models. There is you know there is a lot of things that require careful consideration when you're bringing multiple modalities into a single model to predict but I I think you know I expect those to be to be solvable. >> Wonderful. Uh you've been very generous with your time. Congrats on all your success and uh yeah, I'm excited for the uh AI summit uh or physical AI summit. >> Yeah, thanks for having me. >> And yeah, and people should check out the film festival if it's in town, right? Uh you'll be going to be touring all over the place. >> Yeah, ne next year we're probably going to do the So we do film festivals every May or June of uh and we did the last one in New York, LA, Tokyo, and and at the AI engineer uh fair. >> Yeah. Yeah. Yeah. Um, so yeah, hopefully even more place next year. >> No, I I think like as someday, you know, you will be hosting the Oscars of AI video and you know, I think people should like take this very seriously as like a potential career they can have. >> The Oscars of AI video will be called the Oscars. >> All right. [laughter] All right. Thank you. >> Thank you. [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "world-models-neural-os",
  "signal": 0.15,
  "novelty": 0.3,
  "actionability": 0.05,
  "evidence": 0.15,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это визионерское интервью основателя Runway про будущее интерфейсов, world models и робототехнику вперемешку с личной историей и рекламой подкаста, без конкретных техник, бенчмарков или воркфлоу, применимых прямо сейчас.",
  "knowledge_units": [
    {
      "claim": "Основатель Runway считает, что конечная точка развития world models — полностью нейросетевая операционная система, где сам интерфейс (рендер, пиксели) становится обучаемым компонентом, а не жёсткой оболочкой вокруг LLM.",
      "type": "principle",
      "actionable": "При проектировании agent-UX держать в голове, что в перспективе рендер/интерфейс может стать частью генеративного пайплайна, а не отдельным жёстким слоем поверх модели — это скорее ориентир для долгосрочной архитектуры, чем то, что можно внедрить сегодня."
    }
  ]
}
```
