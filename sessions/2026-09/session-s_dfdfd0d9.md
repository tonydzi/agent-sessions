---
session: s_dfdfd0d9
date: 2026-09-25
words: 2052
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_dfdfd0d9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Physical AI's Next Bottleneck Is Finding the Right Video — Rafael Levi, Bright Data
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Hi everybody. Welcome. For those that came to actually see me, thank you. For those that are just hanging out here, also thank you. I'm going to try to entertain you guys, teach you something new. Um again my name is Rafael. I work at Bright Data. I've been with Brighta for over eight years. And in Bright Data we are collecting data and uh we're trying to innovate. So today I want to talk about video discovery for agentic world models training. And uh we're going to explain what that is in a little bit. So what does it take to take to build a system that can see understand and act right? I mean, we figured out what an AI is. We're constantly improving it. Like, you know, that's kind of handled. But now, the hard part is what data do you provide to it? Because everybody knows AI without data is just a box, right? So, let me take you a little bit back in history, right? In 2022, Google taught a robot by images, real world actions, right? Then going forward, there was a leap uh in 2023. Uh we had uh an AI actually control multiple robots. In 2024, the open source came out. Now, this where the game changed. Once we had an open source, all the labs had access to AI and they started already putting AI into robots, right? And so now these models are already driving humanoid robots. I'm you seeing some of course most here are remote controlled, but I mean in San Francisco you got weo driving without any drivers. How cool is that? First time I got in the car, I thought I was going to die, but it was actually very nice. Right now, how do you think it learned how to drive? By actually teaching itself. By by learning on dashboard cameras, right? Every car has a dashboard. So, if you provide that to an AI, it can figure out how to actually operate a machine. So, as I said, the AI is no longer the hard part. The data is. And this is what I want to talk about. Right? So for chat LLMs, there's trillions of words and texts, right? So we have so much text data to train the LLMs. For image generation, we got billions of images, labeled images. So that's also a huge database. But for robotics, there's only about a million videos. It's a very small limited data sets of robots doing things, right? And so the idea here is that of course you a lot of companies out there what they do is they pay people to record actions, right? So for example, hey record me how you open a door or record to me how you're sitting on the chair. But then the problem becomes is that when somebody is told to do something, they do not do it naturally. So I call it instructed, right? If you're told to record how you open the door and you're doing it for somebody, it's not going to be the same as if you just walk into the house. The movement is totally different. So is that data good for robotic training? In my assumption, no. It's biased data and it doesn't deliver the same results. So obviously the robot is not going to be as effective as if it's intuitive. Right? So I just threw in some examples on the slide, right? So uh the built by hand data is not the same as the data that is kind of on the site, right? So and also the fact is that people behave very differently when they on the camera. Some of you know some people are camera shy. So you know as soon as you put a camera on them you they change but in the natural world it's a totally different thing. So this is what we are trying to solve in bright data right um again so why is the usual data sources are not enough right simulations uh virtual it's it's cheap but it's um you know everybody's playing video games the physics in video games are almost there but they're not good enough where to train a robot on it right a hand control the person controlling a robot it's doable but how many hours a day can you record the robot, how many people you need to actually get huge scale data, right? I mean, you can record maybe eight hours a day every day. How many hours are you going to get in a year? It's not really scalable. And of course, there's already pre-built data sets, but as I said before, they're small. There's only about a million videos at this point. So, what is the alternative? The alternative is the web. Let's just think about YouTube. How many videos are there on YouTube? I don't know, five billion videos. How many actions are in those videos that a robot can replicate? I mean, let's think about it. How many do you think videos are there of a person opening the door firsterson view? Millions of hours. You'll be surprised. So, every day the web video shows gravity motions, right? So um cause and effect obviously accidents big the biggest cause and effect right how handle how people handle objects and billions of hours great training material for robots but what is the problem the problem is that there's a lot of noise right oh and for example right so one of the AI models that meta trained they gave it about a million hours of real world videos and then all it took is 62 hours of real robotics data to actually control to control a real robot. So if you think about it, the data was collected publicly, right? So it trained the the the robot on just random things and then in 62 robotic hours, it was already moving. So there no simulations needed, autonomous robotics delivered fast. But the videos don't show how the robots move, right? So you might think, well, listen, how useful is it a person pouring water into a cup for a robot. So there is methods actually out there how an AI can distinguish and actually learn from the actions that are in a video. If you take two frames frame by frame and the AI measures the movement this difference, right? So you have an image A and image two and there's a small movement that is changing between the two images and AI can actually measure that change. So if you keep doing that through the whole video and AI can actually figure out angles, distance and everything that it needs to train and robot right. So we don't necessarily need the se
...[middle elided]...
 So, this is what we're talking about, right? The videos that are out there, okay? A person running a red light, person stopping on red light, making a left turn, making a right turn, and so on. All of that can be a very useful data for training and any other world models. Physics, right? Robots needs to understand physics. What is the gravity? How to sit? How to walk? How to move? Again, of course, you can pre-record it. Um, a lot of times right now I speak to some of the people and they have millions of people recording videos for them. Hey, can you guys record me how you open doors? That's crazy. Why do you need a million people doing it when everything is available online? Online is one of the hugest databases out there. It's just people don't really like it's it's not that easy to use it, right? I mean, right now the only search available to us is by the keyword of the name of the video. And of course, one source, the whole public video web in one place. I mean, we got YouTube, we got Vimeo, we got so many different uh video providers out there, billions and billions of hours of training data just there waiting for you to grab it, collect it and process it. So basically this is a new product that we're doing a bright data right indexing videos so that you guys can find specific actions anything you can think about you know again it could be useful for brands uh as well it's not only for training data anything you can think of could be useful maybe you are a gamer and you want to know how do you beat this level but there's no exactly video like that so you can search okay people beating the level on the video game, right? Anything. The world is yours. So, I'm going to wrap it up. I don't know if you have any questions, but uh if you want to connect with me, talk about it more, feel free to to add me on LinkedIn. And um yeah, I'm going to thank you guys for your attention. And uh I'm at a bright data booth if you want to talk more about it. And thanks for coming.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "robotics-video-data",
  "signal": 0.35,
  "novelty": 0.4,
  "actionability": 0.25,
  "evidence": 0.25,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад сотрудника Bright Data по сути рекламирует их новый продукт индексации видео для робо-датасетов, но по пути даёт пару полезных наблюдений о том, как устроено обучение world-моделей на видео.",
  "knowledge_units": [
    {
      "claim": "Для робототехники нет аналога 'триллионов токенов' или 'миллиардов размеченных изображений' — публичных датасетов реальных действий роботов всего около миллиона видео, поэтому данные, а не сама модель, являются узким местом.",
      "type": "principle",
      "actionable": "При планировании world-model/robotics-пайплайна закладывать сбор/поиск данных как главный, а не второстепенный этап проекта."
    },
    {
      "claim": "Данные, записанные 'по инструкции' (попросили человека показать, как открыть дверь), систематически отличаются по движению от естественного поведения на видео из дикой сети — инструктированная выборка вносит bias и хуже переносится на реального робота.",
      "type": "tool-caveat",
      "actionable": "При сборе демонстрационных данных для imitation learning избегать постановочных записей 'на камеру по заданию' и предпочитать естественные видео (first-person, бытовые записи) там, где это возможно."
    },
    {
      "claim": "Действия можно извлекать из обычного видео без разметки: модель меряет покадровую разницу (movement/angles/distance) между соседними кадрами и на этом учится физике и действиям, не требуя явных robot-action меток.",
      "type": "tactic",
      "actionable": "Для pretraining world-моделей использовать unlabeled web-video через self-supervised frame-difference/optical-flow сигналы вместо дорогой ручной разметки действий."
    },
    {
      "claim": "По утверждению спикера, модель Meta, предобученная на ~1 млн часов реального видео из открытых источников, после дообучения всего на 62 часах реальных робо-данных уже управляла роботом без симуляции.",
      "type": "benchmark",
      "actionable": "Рассматривать схему 'масштабное video-pretraining + маленький finetune на реальном роботе' как способ резко сократить дорогой этап сбора робо-специфичных данных — но проверять цифру independently, источник не назван точно."
    }
  ]
}
```
