---
session: s_cce20862
date: 2026-09-24
words: 2036
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_cce20862` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Best Models Still Reason Like Toddlers — Andrew Dai, Elorian
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Hi, thanks for coming everyone. Um, I'm the co-founder and CEO of Elorium and I'm here to talk about some of the issues with current models, current frontier models. This includes um Claude Chat GBD and Gemini um and how they handle visual problems and um uh this might be new to some of you who don't work in the visual space but actually there's quite a big gap between how these models handle visual reasoning and how humans deal with it. And you will see that we're actually quite far away from any definition of AGI for visual reasoning. So here are some examples of where uh how easy it is to find where models break down. And um you can find these examples yourself. Just takes a few minutes. Uh in this first example uh we have a chessboard hallucination and we give the models um this picture and ask how many white squares are in the image and any ordinary person uh who doesn't hallucinate would probably not say it's 32. So 32 of course the models say this because they see part of the chessboard and they hallucinate the complete board and as a result they give the wrong number and you see this quite a lot that models rely a lot current models rely a lot on pattern matching. That's what makes them so good at identifying plants and animals and flowers uh in the real world. But when it comes to like complex questions that part hurts them. So the pattern matching is actively hurting them in this case. Um so in their in what's going on in their reasoning is that oh this is a chess board. Chess boards all have 32 squares. Therefore this one must have 32 Y squares too. On the right example um I'm a big board game player. Have quite a collection. Um so you can see there's a a board game theme going on here. And actually you can uh reproduce this outside if you just go to you know outside the talks. It's a ball game area there. There are chess boards. Um I will bet if any of you uh place the pieces in some kind of random position, no frontier model will be able to tell you where those pieces are located, where all those pieces are located. Um and then another example here is katan. Um here another very simple question. How many rows does the blue player have? Um, these frontier models think extensively about this problem. Uh, one response I've seen is that, oh, the the guy has uh 10 blue rows off to the side of the board. Therefore, there must be five uh blue rows on the can board. Uh, but obviously that's not true. There's seven if you actually count. So these models um again are great at guessing uh great at pattern matching but they are not very spatially grounded and they just can't handle any kind of detailed questions. Um and then finally um we have this example where it actually um affects robots where here you have a robot arm uh manipulating this uh cup and um uh cooker basically and the state-of-the-art models today they miss the fact that the uh robot arm lifted the lid um and at the end they also missed the fact that the robot is turning on the stove like right now. So there's uh essentially context amnesia happening. Um and this is because these models can't maintain consistency um across long videos and they very easily lose track of what's happening. And a very common question I get is how do you define a visual reasoning problem versus a visual understanding problem? Um or you could say like visual thinking um compared to visual understanding. I think a very simple way to do it is just um ask yourself the same question. If you looked at an image or a video, how long would it take you to answer the question? So uh for example, in both of these cases, I doubt anyone in this room would be able to give an answer uh if they were only allowed one second to look at the image. So 1 second isn't enough to do these kind of like complex questions also called like system two um kind of thinking in Daniel Canon's book. But if I asked you what game is this uh or similarly what flower is this or if there are only three pieces on the chessboard if I asked you how many pieces are there those questions uh I'm sure all of you would be able to answer in less than a second and similarly all the frontier models would get that kind of question right. So that is the distinction um that we make between what is understanding uh what is like pattern recognition versus what is reasoning where you actually have to look in detail at the picture and um look at various things and this is exactly where frontier models uh fall apart today. So as you are designing your own systems uh that's something to keep in mind keep these visual tasks very simple otherwise you will have hallucinations a lot and a lot of hallucinations um so uh this leads into evals of course um frontier models there are already a bunch of multimodal reasoning evals or visual reasoning evals some that you might have heard of is arc agi this is uh quite often brought up to um people saying oh we the frontier models are 85% or 90% on RKGI therefore we are 90% of the way to a uh to AGI itself uh but I think these people they haven't really looked at any of the benchmark data because if you actually look at the data you will notice that the images are only 32x 32 or 64x 64 pixels and I would challenge anyone uh to give me like a real world complex task that can be reduced to a 32x 32 pixel problem. Um I think you'll very quickly realize almost no tasks almost no interesting tasks can be reduced to that kind of resolution. Another eval that people commonly uh bring up is MMU. Uh this is the massive multiddiscipline multimodal understanding. This is a step up from MMLU because it has um images rather than just pure text science questions. This is science questions based on images. But still images are a minor part of a lot of these questions. A lot of the questions you can just answer without looking at the image or just doing some pattern recognition just knowing roughly what the image is about. So what we really need is new visual reasoning b
...[middle elided]...
s. We spoke to a mechanical engineering company just a few weeks ago and they said to design one small part of a robot testing platform takes 100 to 200 hours uh of the time to design the entire testing platform. Um, I believe it takes 2,000 to 3,000 hours of human uh time there. And they've uh a lot of these places they've tried frontier models, but they just don't work for these use cases. They really struggle to understand uh visual context across these like architecture blueprints, 3D CAD, CAM files. Um, and so there are lots of errors there. Um and similarly we believe that this can be useful useful for other kinds of design as well not just um architecture and engineering but maybe like designing um yeah for the web or fashion or other things and our approach is uh we're using multimodal reasoning to uh to extract um this uh geometric logic that's important. We're allowing programmatic validation or simulation validation. Just like in code, you can run code against unit tests. You can also run u mechanical devices through simulators that have been developed through seammens um and uh v various other companies to see if something will work in the real world. So there's a lot of parallels actually between uh this kind of like mechanical design and coding itself. But mechanical design is still relatively untouched by AI. Um and yeah, CAD CAM quality control is another potential use case and ultimately we believe that this is going to be a critical step to the future of mechanical design where the where AI can make faster cars, more efficient rockets, better batteries and all these things cannot be done just with code. Uh people are not coding up the next iPhone or coding up the next uh SpaceX rocket. It's all fundamentally very visual. So, um you can find out more about us through our website um lauren.ai, our Twitter page xx.comai or our LinkedIn uh page. And yeah, happy to take any questions. I'll be standing around here for for a little bit. Thanks. [applause]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "vlm-visual-reasoning-limits",
  "signal": 0.55,
  "novelty": 0.4,
  "actionability": 0.5,
  "evidence": 0.45,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 270,
  "why": "Доклад даёт конкретные примеры провалов визуального ризонинга у Claude/ChatGPT/Gemini (халлюцинации через паттерн-матчинг, потеря состояния в видео, слабость бенчмарков ARC-AGI/MMMU) и простую эвристику для дизайна визуальных задач, но вторая половина — питч стартапа Elorium/Lauren.ai для CAD-дизайна.",
  "knowledge_units": [
    {
      "claim": "Фронтир-модели при анализе структурированных изображений (шахматная доска, игровое поле) халлюцинируют 'ожидаемую' структуру вместо реального подсчёта — например, дают стандартные 32 белых клетки вместо реального числа на частично видимой доске.",
      "type": "tool-caveat",
      "actionable": "Не полагаться на VLM для точного подсчёта/чтения объектов на структурированных изображениях (доски, схемы, сетки) — верифицировать результат программно или декомпозировать задачу."
    },
    {
      "claim": "Практический тест на границу между 'визуальным пониманием' (модель справится) и 'визуальным ризонингом' (модель провалится) — задать себе вопрос: смог бы человек ответить на этот вопрос по картинке меньше чем за секунду?",
      "type": "principle",
      "actionable": "При проектировании визуальных промптов/агентов применять 'тест одной секунды': если задача требует детального рассматривания дольше секунды, не доверять прямому ответу модели без дополнительных инструментов или разбиения на шаги."
    },
    {
      "claim": "Высокие проценты на ARC-AGI (85-90%) и MMMU не доказывают прогресс к визуальному AGI: у ARC-AGI изображения всего 32x32/64x64 пикселя, не отражающие реальные задачи, а в MMMU многие вопросы решаемы через текстовые знания без реального разбора картинки.",
      "type": "tool-caveat",
      "actionable": "При оценке прогресса моделей в визуальном ризониге не опираться на цифры ARC-AGI/MMMU как индикатор — проверять бенчмарк на реалистичность разрешения и на то, требует ли вопрос реально смотреть в картинку."
    },
    {
      "claim": "На видео современные модели теряют состояние объектов между кадрами ('context amnesia') — например, не замечают, что рука робота подняла крышку или включила плиту несколько кадров назад.",
      "type": "tool-caveat",
      "actionable": "В агентах/пайплайнах для робототехники или видео-анализа с длинным контекстом не полагаться на VLM как единственный источник трекинга состояния — вести явный внешний state-tracker поверх модели."
    }
  ]
}
```
