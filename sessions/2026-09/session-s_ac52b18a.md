---
session: s_ac52b18a
date: 2026-09-30
words: 1917
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ac52b18a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Jev is incredible
CHANNEL: [ИМЯ] - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
Oh boy, it's new model time. This one's very different though. This isn't our usual new LLM that's slightly better at code and it's not going to be the type of thing that the model counter guy is going to show up and say, "Look, best new model." If anything, this might take the counter guy out of his job because this model is for data processing. [ИМЯ]'s by a company called Typesafe AI and it's called Jev. The point of this model isn't to generate text, write code, or do all the things that we expect models to do today. [ИМЯ] is classification. This model is the best model ever made to take data and organize it and classify it. [ИМЯ] returns JSON perfectly in a type-S safe format. When you give it a format, it does it and it does it well. That means this model isn't going to replace things like Fable or Astra. Well, hopefully not. If you are using Fable and Astra for the stuff you can do with this, I have a lot of questions for you. All that said, this model is incredibly capable, and that's why it's blown up on Twitter. I've seen demos of everything from lightning fast computer use even in like the iOS simulator to the model playing Minecraft at lightning speed to compaction that takes under a second instead of multiple minutes. I can't wait to show you all the best things you can do with this model. But first, we got to classify something. The next section, which is the sponsor break. If you're not a developer, you can skip this ad. But if you are, you should listen close. Have you ever sent a prompt to Cloud Code, Codeex, Cursor, or some other tool and been surprised that it took hours when you expected it to take minutes? Did you check to see why? Because I would bet, good money, there's a very good chance that a handful of things happened. Maybe it took too long to download the Docker image. Maybe it spun up and had some error when it did. Maybe the CI that it was trying to run took forever. Maybe it pushed it up to GitHub and the CI run on there was going to take hours long. I cannot tell you how many times I've run into this. Wouldn't it be nice if your agents could do all of those things way faster and more reliably, and when those things failed, you got insight into it? Imagine taking all of these 8-minute builds and knocking them down to 20 seconds or building and testing three React apps in seven Go binaries in 30 seconds or making your crossplatform builds 10 to 20 times faster. Hopefully, you get the idea now because today's sponsor is depot and they are trying their damnedest to make AI more capable, not by giving it things it can't do already, but by making all of the things it does do more reliable and faster. Whether you're looking for a faster and cheaper alternative to GitHub actions or just a nice place to let your agents run or a cache for all the Docker images you and your team are using, Dep Depot provides all of this and more. Their CI platform is fully compatible with GitHub actions, which means you can swap over trivially. But if you don't want to deal with GitHub's downtime, you can move fully over to depot's platform. Still compatible with actions, but without having to worry about GitHub's reliability. You can also transform those workflows to let them run in parallel, which ends up being comically faster than the alternatives on GitHub. Their CLI is incredible, too. You and your agents will understand it immediately. [ИМЯ] makes it trivial to migrate your CI, run it without pushing up code, diagnose things when they go wrong, find secrets and clone them across different places, and more. You can even SSH into a session while it is running to figure out what's going wrong in real time. And when I say you, obviously, I mean your agents. GitHub actions were poorly assembled for humans over 10 years ago. Depot was crafted carefully for agents today. Figure out what that means at soyv.link/depo. Quick breakdown on how this all happened because it's actually been pretty crazy to watch. [ИМЯ] feels like it just poof appeared and took over my entire Twitter feed. Like half of what I've been seeing is all of the stuff about Jev. [ИМЯ] was created by [ИМЯ] [СКРЫТО]. And as great as RHF is for model behaviors, it is not helping as much with classification, which is the thing he cares about. If you focus more on the classifying side and less on the general usage of text generation side, what you can get is way way faster and way way cheaper. In particular, all output tokens being free. The cost characteristics of this model are almost as insane as the speed. Both are crazy. So, let's read through the announcement. The core concept here is system one models. This is an idea that comes from thinking fast and slow by [ИМЯ] [ИМЯ]. System one is the fast and intuitive judgment of your brain. the part of your brain that can do things without effort that looks at somebody's like, "Yeah, that shirt's blue." System two is slow and deliberate reasoning. In type safe's framing, Jev handles the first kind of task while reasoning models still handle the second. They named it Jeb after Jevan's paradox, which I actually think is pretty cute. The idea is that when the steam engine gets more efficient, it actually increased coal consumption, not decreased, because now that power is cheaper, we can use it for more things. That is really the right way to think of this model. [ИМЯ]'s not unlocking new capabilities that weren't possible before. [ИМЯ]'s making them fast and cheap enough that they're way more viable than they've been. But what are those cases? What is this valuable for? Pretty much anything that needs to be classified. Think organizing videos by their topic in my YouTube channel. Figuring out if an email is important or not and what category it should be put under. Things like safety and moderation, identifying what messages are safe and which ones aren't and what makes them unsafe. There's so many things you can use it for. A
...[middle elided]...
s? If the answer is under 10 seconds, this model's probably good for it. If it's over 10 seconds, this model's likely less good for it. This is the point I'll end on, and it's similar to the one I started on. really want to emphasize the system one point because I'm tired of people not getting it. If the task requires thinking, this model is not right. If the task requires classifying, organizing, ranking, real quick decision-m, this model is incredible. [ИМЯ]'s a system one model. System two is when you think about a thing. System one is when you react because your brain thought for you. [ИМЯ]'s almost like the reflex. [ИМЯ]'s like when you tap your knee and your leg kicks out, that kind of thing. This model is designed to work like that first part to be really fast and quick. If you're thinking of this model in terms of how it replaces the other ones you use, you're probably not thinking about it correctly, unless you're doing a lot of structured output work. The value of this model is that it made so many things that weren't really realistic before way cheaper and faster in a way that is actually kind of cool as a programmer. But you shouldn't be viewing this as a tool you use in Codeex or Claude or even in your terminal. You should see this like a new library you install or a function that you call. [ИМЯ] is meant to be integrated in the tools that we build, not used as an inference farm to generate code or text or all these other things. Somebody in China just said the only way this would replace an LM is if you're using them badly. I mostly agree. There are a lot of use case for structured output type stuff and this is where it is strongest. I think this model is really cool and I've been enjoying it a lot. I have a feeling you will too as long as you go in with the right mindset. Don't use this to replace fable or judge between complex topics. Use this like an if statement and you'll have a lot of fun with it. Let me know how y'all feel. And until next time, peace nerds.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "fast-classification-models",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.35,
  "evidence": 0.15,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "В основном хайп-обзор нового классификационного 'system-1' движка (Jev) с Twitter-демками без бенчмарков, но есть пара полезных эвристик для инженера про то, когда применять быстрый классификатор вместо полноценной LLM.",
  "knowledge_units": [
    {
      "claim": "Специализированные 'system-1' модели заточены не под генерацию текста/код, а под классификацию, структурирование и быстрый JSON-вывод — это отдельный класс инструментов, а не замена рассуждающим LLM.",
      "type": "principle",
      "actionable": "Для задач классификации, роутинга, модерации и разметки данных пробовать выделенную быструю/дешёвую модель классификации вместо дорогой универсальной LLM."
    },
    {
      "claim": "Эвристика выбора: если человек принимает такое решение меньше чем за 10 секунд (интуитивно) — задача подходит для быстрой классификационной модели; если требуется обдумывание — нужна reasoning-модель.",
      "type": "tactic",
      "actionable": "Перед выбором модели для подзадачи агента оценить, уложился бы человек в 10 секунд на такое суждение — если да, ставить туда лёгкий/быстрый классификатор, а не тяжёлую LLM."
    },
    {
      "claim": "Такие модели стоит встраивать в систему как библиотечную функцию/условный оператор (if-statement) внутри пайплайна, а не использовать как самостоятельный чат-инструмент вроде Claude Code/Codex.",
      "type": "workflow",
      "actionable": "Интегрировать классификационную модель через API-вызов внутри своего кода/агентной логики, а не пытаться заменить ей основной кодинг-ассистент."
    }
  ]
}
```
