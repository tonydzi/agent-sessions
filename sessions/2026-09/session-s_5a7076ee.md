---
session: s_5a7076ee
date: 2026-09-24
words: 2057
turns: 2
tools: "Read"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5a7076ee` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: [ИМЯ] VLM/VLA's to [ИМЯ] [ИМЯ] — [ИМЯ] [ИМЯ], [ИМЯ] AI
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Yeah, I guess uh let's get started. I'm I'm [ИМЯ]. I'm I'm the co-founder and CEO of [ИМЯ]. Um, we'll get a little bit into into what we do, but uh, primarily what I want to talk about today is kind of our research stance that we want to move away from distinctions between VLMs, VAS, world models, whatever you want to call it, to something that we call embodied foundation models. So specifically what we what we do at [ИМЯ] kind of our northstar really is we want to be able to build physical AI foundations that give us the ability to perceive, understand and interact with the physical world in real time. And so kind of the the northstar mission is really to bridge the the physical and digital world uh worlds fundamentally meaning that our our goal is kind of wherever there is a um a device, an instrument, a robot, a camera, a sensor, uh we're essentially there providing intelligence to it. And specifically when we talk about this paradigm of being able to perceive, being able to reason, being able to act, we view this as kind of a a unification of uh traditional multimodal modeling. [СКРЫТО] and and and my target there was really to try to figure out how to scale up recipes for multimodal models. And so one of the early things that we we started working on and we've published a lot in this domain was around early fusion. So this concept that you want to bring in all these modalities as early as you can and and the real complexity there is trying to figure out what is the correct way to actually properly represent all the different modalities uh both on the input and on on the output that you want to be able to represent holistically and so VLMs have kind of became the when I talk about multimodal models um you probably think of VLM. So this is the ability to take in some image video and some text and be able to output some some text essentially. And there's there's variations of this. There's there's models like the ER models, the embodied reasoning models that are able to output maybe some grounding points um that are able to do spatial understanding or reasoning a little bit better. Then we have things like VALAS that extend kind of the output domain apart from just text to now actions. And these are traditionally of course continue to be built on by standard VLM backbones. Although there's been some efforts to try to migrate away from uh from VLMs to things like world models or world action models, although nothing that's been super fruitful just yet. And then we get into kind of more interesting and complex uh variants of multimodal models like world models where you essentially are outputting video uh from some inputs and the inputs can be either image or video or honestly image video and and actions. Um and the last point that I'll talk about is something recent which we call semantic world models which is you don't really output anything but you learn some type of representation that you think is useful um in the future. What we kind of view as an embodied foundation model is actually uh a framing that allows you to both to do the standard perception the embodied reasoning and then the northstar target of control all within one model. Um, so being able to reason across different sense of modalities on the input and being able to do kind of most of what I mentioned on the output all within one single unified model. And so very quickly I'm going to talk about two challenges and these are kind of fundamental research challenges that we face and I'll talk about kind of how our company has approached this um and and and what other folks are doing in here as well. So the very first thing is think about purely if you're going to try to model something like video like one hour of video depending on the representation you might have something like 1 million visual tokens that are coming in. The truth is is that there's not actually any ground truth that you can use uh effectively, right? So you can do things like and people have done this of course like pull out the transcripts uh predict the transcripts from the video or or maybe synthetically label some frames, ask it some questions and it turns out that this is kind of a humongous waste, right? So if you think about what's going into your model, you have 1 million tokens going in and you're essentially calculating the loss on something like you know 2% of all the tokens that are going in. And so this is very fundamentally problematic and and and the truth is is any way you try to figure out how to fix this, you're essentially injecting a wrong training signal. Either the signal is too sparse, it's too synthetic, or it's too indiscriminate. And so approaches beyond just synthetic enrichment have been, well, let's predict every single pixel. I mean, true, this is a very dense signal, but it actually very poorly allocates attention. there's, you know, you're comparing a, you're treating a background pixel with the same degree of importance as you're treating a gripper tip or the contact points or the specific failures or the physics. And so what we do kind of at [ИМЯ] is, and this is kind of some of our core IP is we think about what does a natural perceptive objective look like? So specifically, how can I predict the percepts that we think will matter in in the future in a very very automatic way. So, as an example, you might hardcode something like, well, if you have a robotic arm, well, the the the tip of the grippers turns out to be a very useful percept that you can predict into the future. And folks have started doing this. Um, like the Momo app folks from AI2 have done this. There are other VAS that have done this. But this is still a hard-coded percept. So, the question is, can you figure out an automatic way that the model semantically is able to learn this very unique objective? And the truth is, we have figured out a way. uh we're not going to share how we do it here, but this 
...[middle elided]...
that we've seen is that uh for VA models specifically, like if you go and you take one of the Chinese ones um and you try to fine-tune it for a specific policy, if you just change the background of the I don't know, you can like in the table uh if you change the the background of the table, the policy will actually fail. What's really interesting, if you do this type of joint perceptive and control modeling, you're much more robust to these types of errors or if the light is hitting it a slightly different way. And I think we primarily view this as robustness to background uh in a way that I think traditional models don't necessarily have. That being said, I'm not going to overclaim like uh I mean like it's still relatively hard. I think if I was going to go and shine a flashlight into one of the one of the arms, it's probably not going to work. Uh but being able to jointly model these things helps a significant amount. We also do a lot of online augmentations. So, so we do actually, you know, fake um I don't know um one of the one of the arm cameras being off, right? We fake uh you know, sunlight coming in from a certain direction, right? So, we do these things during training to improve robustness. Uh but the big gains come from taking this early fusion paradigm and then moving it into the robotics domain. >> Cool. uh create knowledge base using the K1 model. >> Uh oh, knowledge bases. Um it's useful for like I I mean if you want to caption images, videos, it's relatively well. We work with robotics partners for like very complex egocentric annotation like this. Um so it's not necessarily building out an ontology, but being able to do kind of very deep structured extraction, I think our models are are very good at. Yeah. By the way, everything that I kind of showed here is kind of public APIs, so you can go play around with it. The benchmarks are public. Um, I think I'm out of time. They're cutting me off. So, uh, I can talk with folks outside, but thank you guys.

---

> `Read` -- {"file_path": "C:\\Users\\dev\\.claude\\projects\\E--Obsidian--imports\\memory\\MEMORY.md"}

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "embodied-vla-world-models",
  "signal": 0.55,
  "novelty": 0.6,
  "actionability": 0.45,
  "evidence": 0.5,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "СЕО [ИМЯ] (экс-FAIR) даёт реальные, но частично закрытые технические инсайты про обучение VLA/embodied моделей — полезно узкому кругу, кто строит робото-мультимодальные модели, а не общим AI-инженерам.",
  "knowledge_units": [
    {
      "claim": "При обучении на длинном видео (например, 1М визуальных токенов на час видео) прямого ground truth почти нет — loss считается по ничтожной доле токенов (~2%), а попытки закрыть это (транскрипты, синтетические подписи, предсказание каждого пикселя) дают либо слишком разреженный, либо слишком синтетический, либо неразборчивый (внимание тратится поровну на фон и на значимые детали типа кончика захвата) обучающий сигнал.",
      "type": "tool-caveat",
      "actionable": "При проектировании self-supervised objective для видео/эгоцентричных данных не полагаться на dense pixel-prediction или синтетические подписи как на единственный сигнал — явно продумывать, какие именно перцепты (точки контакта, состояние объекта манипуляции) действительно важны для задачи, и искать способ выучивать их автоматически, а не хардкодить вручную."
    },
    {
      "claim": "Готовые VLA-модели (в т.ч. открытые китайские), дообученные на конкретную политику манипуляции, ломаются при смене фона стола или освещения; совместное перцептивно-контрольное моделирование (joint perceptive + control modeling) даёт заметно большую устойчивость к таким сдвигам, хотя и не ко всем (например, направленный свет фонариком на манипулятор всё ещё ломает модель).",
      "type": "benchmark",
      "actionable": "Если строите или файнтюните VLA-политику для роботизированного захвата, не полагайтесь только на данные для конкретной сцены — учитывайте, что смена визуального контекста (фон, свет) — известная точка отказа, и рассматривайте архитектуры с совместным обучением перцепции и управления как способ повысить робастность."
    },
    {
      "claim": "Команда [ИМЯ] применяет онлайн-аугментации во время обучения VLA — искусственно «отключают» одну из камер на руке робота и симулируют смену направления освещения (солнечный свет с разных сторон), чтобы повысить устойчивость модели к реальным сбоям сенсоров и условий съёмки.",
      "type": "tactic",
      "actionable": "При обучении робото-мультимодальных моделей на реальных или симулированных данных добавляйте онлайн-аугментации, имитирующие частичный отказ сенсоров (одна из нескольких камер выключена) и изменение освещения — это дешёвый способ закрыть класс типичных сбоев в проде без сбора новых данных."
    }
  ]
}
```
