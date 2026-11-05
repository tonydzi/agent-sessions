---
session: s_de2bff95
date: 2026-09-27
words: 2014
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_de2bff95` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Biggest AI Coding Agent Upgrade Is Already on Your Machine?!
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
No matter the coding agent that you're using, like Claude code, and what you're using it for, there is a goldmine of data that you're probably not taking advantage of at all. And in this video, I'll show you how we can use it to make our coding agents better and better over time, and it really doesn't take that much effort on your part. The data that I'm talking about is the conversations that you have with your coding agent, plain and simple. Every single conversation gets stored as a file on your computer, no matter the coding agent that you're using. With Claude code, they are stored as these JSONL files. And whether you know it or not, your coding agent has probably already looked through these files before. Even if you have some kind of memory system set up, I find that when you ask about past conversations, it likes to look in these files because they are rich with information. That's the whole point of this video is we want to leverage these, and I'll talk about how we do that. And so, the problem we have with this though is that these files are so rich with information that it's kind of overwhelming. So, even if you've looked at this before, you've probably scrolled through it and been like, "How am I even going to use this for anything useful?" Well, that is what I have for you right now. Because what we can do with these beautiful files is we can take a look at the hundreds or thousands of past conversations with our coding agent. Each one of these files for that conversation has every prompt that we sent in, every tool or MCP server coding agent has used, every thought that it's had. And so, we can take all of that, extract the good parts, put it in some kind of structured table, and then start extracting insights. Like we can identify opportunities to make our coding agents more token efficient, or figure out common failures so we can address them with changes to our rules or our skills. Your imagination can really start to run wild with all the different ways we can leverage our past conversations, and of course, using our coding agent to help us do that. And so, what I have for you here is such low-hanging fruit because the input into the process I'll show you is just the conversations that you already have with your coding agents stored on your machine. There's nothing else. And what you get out of it is the insights to make your coding agent better. So, we are using our AI coding assistant to learn from past mistakes to make itself more efficient and reliable. The main thing that we need to make this process work well is a place to store our transcripts permanently because otherwise Claude Code cleans them up after 30 days by default. And then we also need a database for structure. Like you saw just a bit ago, the JSONL files are super messy and it's not better for any other coding agent. And so having a database where we can split things into structured tables, just getting the information we need. Like here are our sessions, here are all the tool calls the agent has made across conversations, here are the different agent turns. I'll show you how to set this up here in a platform that I love using called Data Bricks. This is my favorite free solution for everything I'm going to show you in this video. But there are of course a lot of different ways we can extract data from these conversations and get these insights. This is just the way this worked the best for me. Okay, so let's start with the easiest way to get this done. Now this isn't the best way to do it, which is why I want to show you the process with the structured tables. But if you want to get started simple as possible, this is all you have to do. You just go into your coding agent, couple of sentences here. Do a deep dive into our past conversations to identify opportunities to make our coding agent like Claude Code more efficient or reliable. And then I want you to suggest the top 10 improvements in a concise bullet point list. So obviously you don't have to prompt exactly as I do, but I like adding this just to make sure it doesn't spit out change after change that it recommends. Cuz especially before Opus 5.5, like Opus 5 would just give me like a million different things that barely mattered at all. And so I like to very much bound what it outputs. And this is all it takes to get started. It's super easy. And I also started this conversation by showing you that coding agents are aware of where their own conversations are stored. So if you just simply ask, "Where are all Claude Code conversations stored on my machine?" It is able to identify that exact folder that I was showing you all the JSONL files in earlier, which they're all split by the different projects that we're working on with our coding agent. Or if you just search the folder for star.jsonl, it'll show all the files. We can copy them all if we want to. Now, back over to Claude code, once I send in this prompt, it's going to start by loading a skill that I built for this exact process. So again, this is the simple way to do it. It's not the most effective or token efficient, but if you do want the easiest starting point, I will link to this skill in the description, and you can just send off a prompt like this. And so it's going to run some shell commands to read through all these files here and identify common failures. And so it's going to list out the top 10, and then obviously I can take that forward and then ask Claude code, "Okay, like based on this failure or this failure, what can we change in our AI layer, like our hooks or our skills or our rules, so we're not going to run into this time and time again?" So for example, with the third issue that it identified, it said that I'm hitting my concurrent sub-agent limit way too often. That is definitely a problem that I want to address. And so taking this forward is as simple as asking it, "What can I change in our AI layer to fix issue number three?" And by the way, my definition for AI l
...[middle elided]...
 problems we found with our Genie analysis in Databricks. Like, for example, never guessing a path, which is something that coding agents will actually do a lot if you don't explicitly tell them not to. I added some more permissions within the settings.json, so it's able to work better with Git. And then, I also added a hook, which is my favorite part of the changes that we made to the AI layer here. It is a session tree. It's a script that runs whenever I start a new conversation with my coding agent. And this is pretty cool. It injects the real repository layout, so the agent is less likely to guess paths to access things when it's reading through files and gathering context. This is awesome, especially cuz this is dynamic. A lot of people like to give like a code base layout in their global rules, but then you have to constantly change it and it always risks going stale. But now, we're going to gather context around the file base structure and inject that right away in the coding agent whenever we start a new conversation. So, some pretty cool and practical changes that I've done to my AI layer here, all thanks to the insights I gathered from what I set up in Databricks. And I know these examples are very specific to what I have in my own system, but I just wanted to give you some real ideas, some real examples of how we are making our coding agent better over time looking at our past conversations. So, there you go. That is how you use Databricks and their Genie agent to make your coding agent better over time. And the big thing here is just that your past conversations with your coding agent are a gold mine. There are a lot of different ways to structure the conversations and gather insights from them and act on them. I just wanted to give you a full process end-to-end here. And so, if you appreciated this video, you're looking forward to more things on AI coding, I would really appreciate a like and a subscribe. And with that, I will see you in the next video.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "claude-code-conversation-mining",
  "signal": 0.55,
  "novelty": 0.45,
  "actionability": 0.65,
  "evidence": 0.4,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 300,
  "why": "Автор показывает практичный, но не новый приём — майнить собственные JSONL-логи Claude Code, чтобы находить повторяющиеся провалы и превращать их в правки хуков/скиллов/rules, при этом доказательная база слабая (только пара личных примеров, без бенчмарков).",
  "knowledge_units": [
    {
      "claim": "Claude Code хранит каждую сессию как JSONL-файл локально (по проектам) и по умолчанию удаляет их через 30 дней.",
      "type": "tool-caveat",
      "actionable": "Если хочешь копить историю дольше 30 дней для анализа — настрой автоматический бэкап .jsonl-файлов в постоянное хранилище до истечения срока."
    },
    {
      "claim": "Можно попросить коуд-агента самого прочитать свои прошлые JSONL-логи и выдать топ-N рекомендаций по повышению эффективности/надёжности, ограничив число пунктов, чтобы не получить размытый список.",
      "type": "workflow",
      "actionable": "Дай Claude Code промпт вида «пройдись по прошлым разговорам и найди топ-10 улучшений» с явным лимитом на число пунктов, затем по каждому найденному пункту отдельно спроси, что поправить в хуках/скиллах/rules."
    },
    {
      "claim": "Для больших объёмов логов сырой JSONL слишком шумный для анализа; структурирование в таблицы (сессии, tool calls, agent turns) через внешнюю БД/аналитический движок даёт более точные и токен-эффективные инсайты, чем прямой прогон файлов агентом.",
      "type": "tactic",
      "actionable": "При регулярном анализе логов агента выгружай их в структурированную БД (таблицы sessions/tool_calls/turns) вместо повторного скармливания сырых JSONL целиком в LLM каждый раз."
    },
    {
      "claim": "Хук на старте сессии, динамически инжектирующий реальную структуру файлов репозитория, снижает частоту угадывания путей агентом по сравнению со статичным описанием структуры в global rules, которое устаревает.",
      "type": "tactic",
      "actionable": "Замени статичное описание структуры проекта в CLAUDE.md/rules на SessionStart-хук, который на каждый старт сессии свежо генерирует и подставляет реальное дерево файлов репозитория."
    }
  ]
}
```
