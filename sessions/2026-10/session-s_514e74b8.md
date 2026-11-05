---
session: s_514e74b8
date: 2026-10-01
words: 2024
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_514e74b8` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The BEST Jev Use Cases for AI Coding (Absolute Game Changers)
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
Jev is incredible. It was released recently and it popularized a type of AI model called system one models which specialize in making decisions instead of generating text. And so it's actually way different from LLMs like Claude and GPT. And so it's opened up a whole new sprawl of use cases that everyone is sharing on the internet right now. And people are sharing a lot of really fun and cool use cases with Jev. But something I'm hearing a lot, especially from people in my Dynamis community, is that the use cases are cool, but they're not always the most practical, right? There's not a lot that you see and you're like, "Okay, I need to go incorporate this in my AI workflows right now." And so that's why I want to make this video just quickly showing specifically for AI coding for incredible Jev use cases to make your AI coding workflows faster and more token efficient, which is a big deal right now, especially with how bad the rate limits are. Now, if you follow the latest in AI, there is a very good chance that you've heard of Jev and probably even tried it out for yourself. Now, Jev is not the first kind of decision model like this, but that's a whole another topic for another video. The point is Jev is really powerful. The way it works is you give it some kind of situation, which they call state, and then you also supply with a list of multiple choice questions, and in parallel, it's going to answer each one of those questions with a probability, which is basically its confidence score. Now, the thing is you can already do this with large language models, especially with structured output. You can have it make decisions that you can key off of for the rest of your workflow. But what makes Jev so awesome is that it is 20 to 200 times faster than LLM at making decisions. And it's also 40 to a,000 times cheaper. Obviously, the big range here being you can use different LLMs to compare against Jev. no matter the LLM that you use, Jev is going to be more accurate, faster, and cheaper for making any kinds of decisions. And so, at a high level, when you think of like Jev as the decision maker, that's an endless number of possibilities that you can use it for. And so, that's why I want to get really specific with you here, just quickly showing you, giving you inspiration for different ways that we can use it very practically. Now, for each one of these Jev use cases, they're valuable enough where I could make an entire video going into how to build and incorporate it. But for right now, I just want to stay more high level. I want to keep this short and sweet, giving you inspiration here. So, you can even pick a couple of these and maybe build them out yourself. And then also in my Dynamis community this Friday, I am running a workshop getting a lot deeper into these use cases. So, check that out if you're interested. And yeah, like I said, a lot more content coming soon diving deeper into Jev cuz this is exciting for me. I actually said this in my first video on Jev. This is the first AI model in a while that I'm genuinely excited for, and I think you'll see why as we get into these four use cases here. So, with that, let's just get right into it. My favorite use case for Jev right now in my AI coding workflows is for security. Because the thing is, and you've probably seen this yourself, AI coding assistants are way too willing to do things that they shouldn't, like read your environment variables, delete an entire folder, even if you have things in your global rules or skills to not do this, especially once you really start to bloat the context of a conversation, or if you have a prompt that kind of gives it a workaround, it's going to figure out ways to do these things. And so that's why we need guard rails to prevent our agents from performing destructive actions. and Jev can really be that guardrail. So the most popular and effective way to implement these guardrails for our coding agents is using hooks which was introduced in claude code. But now pretty much every single coding agent has the idea of hooks where we can attach automations to run at different events that take place in the life cycle of our coding agent. And so the most popular event is pre-tool use. So when the agent is about to perform an action like read a file or run a command, we can run an automation to basically analyze that and either block the agent from performing that action or allow it to continue. And so you can see where we're going with this here because one of the most popular use cases is having a pre-tool use hook that tries to analyze the agent's action to determine if it's going to read av file. Right? We don't want our secrets exposed into the context of our coding agent. And so it has the opportunity to dish out an error code to essentially block that action. So the agent has to do something different like for example reading the&enb.example instead. Now the problem with this hook until jevv is that we either have to have an LLM analyze every single call or we have to have some kind of deterministic process with regular expressions. Either way, it's going to be expensive or not very accurate. Now, let's just scrap the idea of using an LLM right away. Because if we're going to analyze every single action the agent wants to take, that's going to cost you hundreds or thousands of dollars throughout the month just to block these sensitive calls that might happen once in a while. And so, what I've done until Jev is I use regular expressions. And so, I have a hook that runs that just does pattern matching to try to figure out the agent is trying to do something like reading my Google credentials, reading my deleting a folder, whatever it is. But the problem is there are so many different ways that an agent is able to do these destructive actions because it can read the file directly. It can write a Python script to do so or a bash command like right there are a million different things. And so we have this m
...[middle elided]...
be a strong model like Opus 5.5 or GBT6 Astra. You get the idea, right? Like Jev is making that determination. And in my testing, it does a very good job just generally understanding the difficulties of tasks and the type of tasks. And so back over to this specific run for the classification here, it figured that it is a bug that needs to be investigated. And then for the tier selection here, I'll go to the logs really quickly. I know it's kind of hard to pick out, but when the next step ran, it did investigate standard, as in it was using that middle tier of the model here. So, whatever I have selected for that, something like a sonnet 5. And of course, I was the judge myself for all the jev testing that I did here. So I ran this archon workflow 12 times and every single time I completely agreed with the decisions with the classifications that it made up front. There's also a separate archon workflow more for pull request reviewing. And so using classification up front to figure out what kind of review do we need like is this a bigger thing that needs a full architecture review or just a light chore that has to be validated quickly. And it wasn't perfect but still 15 out of 16 is pretty darn good. And if we look at the cost here, a fraction of a penny versus what it would typically cost an LLM. And again, 32 cents per poll request, that is really going to add up, especially with a project like Archon where we are dealing with dozens, hundreds of poll requests and issues every week. So there you have it. Those are my four favorite use cases for using Jev in AI coding workflows. And of course, let me know in the comments if you want me to make a dedicated video for any of these cuz I could certainly go a lot deeper and help you incorporate these into your workflows as well. And so if you appreciated this video, you're looking forward to more things on Jev and AI coding, I would really appreciate a like and a subscribe. And with that, I will see you in the next video.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "fast-decision-model-routing",
  "signal": 0.55,
  "novelty": 0.5,
  "actionability": 0.55,
  "evidence": 0.35,
  "durability": 0.4,
  "volatility": "volatile",
  "half_life_days": 180,
  "why": "Видео даёт конкретный архитектурный паттерн (дешёвый быстрый классификатор перед дорогой LLM для guardrails, роутинга модели и PR-ревью), но завязано на конкретный новый инструмент 'Jev' и подтверждено только самооценкой автора без независимого бенчмарка.",
  "knowledge_units": [
    {
      "claim": "Pre-tool-use хук в Claude Code можно строить не на LLM и не на regex, а на отдельной быстрой/дешёвой модели-классификаторе, которая по состоянию (state) и списку вариантов оценивает вероятность того, что действие агента деструктивно (чтение секретов, удаление папки и т.п.)",
      "type": "workflow",
      "actionable": "Добавить в pre-tool-use hook вызов лёгкого классификатора вместо дорогого LLM-вызова на каждое действие — снижает стоимость постоянного гардрейла при сохранении точности выше regex-паттернов"
    },
    {
      "claim": "Перед запуском дорогой задачи (например, обработка issue/PR) можно сначала классифицировать сложность задачи дешёвой моделью и по результату выбрать tier модели-исполнителя (например, sonnet для стандартных задач, opus для сложных)",
      "type": "tactic",
      "actionable": "Внедрить предварительный классификатор сложности задачи в оркестратор агентов, чтобы не гонять топовую модель на простых тикетах и экономить токены"
    },
    {
      "claim": "Для ревью pull request'ов можно использовать классификатор, который сначала определяет тип изменения (крупная архитектурная правка vs лёгкий chore), и в зависимости от этого выбирать глубину ревью",
      "type": "tactic",
      "actionable": "Добавить предклассификацию типа PR перед запуском LLM-ревьюера, чтобы не тратить дорогой проход на тривиальные PR"
    },
    {
      "claim": "Автор заявляет 20-200x ускорение и 40-1000x снижение стоимости у специализированной decision-модели по сравнению с LLM на задачах классификации, но цифры приведены без независимого бенчмарка — только собственное тестирование и субъективная оценка (15/16, 12/12 совпадений с судьёй-автором)",
      "type": "tool-caveat",
      "actionable": "Не доверять заявленным множителям скорости/стоимости без собственной проверки на своих данных перед тем, как закладывать такую модель в продакшен-пайплайн"
    }
  ]
}
```
