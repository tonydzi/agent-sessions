---
session: s_60eb66bf
date: 2026-09-24
words: 1950
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_60eb66bf` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Building the Document Context Layer for AI Agents — Jerry Liu, LlamaIndex
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> I think we can get started. Hey everyone, I'm Jerry, co-founder and CEO of LlamaIndex, and today I'm excited to uh give a talk called building the document context layer for AI agents. Um really uh big shoutout to the AI Engineer World Fair for hosting. Um and if you've seen some of my earlier talks from the previous uh AI Engineer conferences, uh we've kind of traced through a lot of the evolution of how, you know, um agent advances have correlated with uh you know, how you inject context into evolving applications. Um and so today, in 2026, we'll kind of talk about three main topics. One is, you know, what is RAG in 2026? Um two, uh basically that basically decomposes into an agent harness plus a context layer. So kind of going into the modern document context layer for agents, um and giving you a little bit of sense of kind of some of the core capabilities today, um especially uh unlocking, you know, the vast trove of document-based data today, and giving you a glimpse of what's next. All right. RAG in 2026. But before that, just a little bit about the company, and I'll kind of get on with the main talk. Um you might have seen us as a RAG framework. We started in 2023, got pretty popular, um kind of created a lot of techniques around like advanced RAG, that type of stuff. Um today, we're basically the main document infrastructure for AI agents. Um we deliver the best platform for agents to actually read and operate over documents, and we see ourselves as unlocking basically the vast troves of document context even as agents and models themselves get better. All right. So, what does RAG actually mean in 2026, and how are agents actually inhaling and addressing context today? This is a snapshot from um actually 3 years ago, um when I first gave a talk on this, and naive RAG was basically just building a simple chatbot over your private corpus of data. If you flash back all the way to January of like 2023, um you know, this technique basically consisted of you have some corpus of documents, um you chunk it up, embed it, and put it into a vector database. You do some naive top K retrieval, and then you generate some stuff with an LLM. All the steps are fixed. You use kind of like a fixed set of techniques, and then with that you actually get some basic application results by just being able to chat over a corpus of documents. Of course, the agent landscape has changed quite a bit and quite dramatically since then. One is agent loops and tool use have gotten a lot a lot better, especially as both the models and agent harnesses have increased. And there's basically a cleaner separation now between agent reasoning and how they actually interact with context. If you look at what I call kind of the modern generalized agents, which includes, you know, all your favorite applications and tools out there from Claude Code, Claude Code Work, Open Claw, Codex, and a few others, you know, the retrieval complexity has started to get baked into the agent layer. So, instead of coming up with a variety of hacks to really work around the limitations of naive top K retrieval, you can start getting the agent to really reason about, for instance, the best key best keyword to search for, best like, you know, search term to actually get back good results. Even if the retrieval tools are basic, the agent can input the right queries to basically loop upon itself and help solve the task at hand. Number two, context is moving up the stack. There's been a lot of conversations, I think, for the first two and a half years of Gen AI of how do you actually manage the agent context window, make sure it doesn't overflow, that type of thing. But, I think as, you know, a lot of the evolving techniques, compaction, long contexts have evolved, I think more and more of the conversation is actually how do you just hook up the right MCP servers and skills and tasks to the agent to enable it to do various types of tasks. And so, that also applies to agent orchestration, right? Coding agents have gotten better. Abstractions of actually defining what types of tasks and programs you want to build have moved a little bit upwards towards English as opposed to through code. And so, maybe in 2023 to 2025, you define programs and you still build stuff via like importing Python, using TypeScript through code. It's pretty clear these days more and more people are just building stuff using English, whether you're a software engineer or you're a non-technical function like go-to-market marketing. And you're defining runbooks through English and kind of like defining the right goals and making sure the AI is aligned on the right task. And we see that carrying over going forward as well. So, in terms of just like general evolving knowledge work patterns, and this kind of forms a foundation for what we how we think about the context layer. You know, in the past maybe you could use AI to just like ask simple questions, get it resolved. Today, you're starting to be able to define and solve more end-to-end like tasks just through English and also use English to start compiling repeatable programs to actually execute something at scale. Obviously, there's been a lot of discussion on how this will evolve even more, and we do see AI agents as behaving even more autonomously through solving long horizon tasks, looping upon themselves to be able to achieve a goal. So, the future will move towards a state where you actually might not even have to define the task in English, but actually more of the goal and a scoring rubric, and then the agent will use all available context available to it to actually solve the task. So, with that overall framing, let's talk about what kind of what is a pretty core focus for us as a company, which is basically helping to unlock unstructured context to basically feed into these agents even as they get really, really good both in terms of the core model capabilities as well as the agent harness. And we'll focus
...[middle elided]...
 layer, you know, besides document parsing, um, a lot of use cases also require actually getting back, uh, structured information at scale from documents. Whether you're processing, you know, a million invoices or expense reports or receipts or claims, you need to make sure that, you know, you want to actually get back structured outputs that you can put into a downstream database or system. And so, a lot of these use cases basically revolve around the form of, you know, how do you automate a lot of workloads that humans typically do in scanning a lot of paperwork and doing data entry. Whether it is kind of, again, invoices, claims, contracts, receipts, or others. We kind of created these capabilities within Llama Parse as well. A lot of our capabilities are actually tuned towards like low cost while extremely high accuracy. And you get back granular citations all the way back to the source document for every extracted output. And of course, you can run this in a pipeline at scale with confidence scores and also, you know, being able to actually flag whether or not we're certain about a certain value before deciding to put it into some sort of system. There's also document search, which is a basically expanded tool set as I mentioned around retrieval, BM25, grep, vector search, reading, and scrolling. And so, all these capabilities are available within some of our commercial platforms as well as open source offerings. But I also just wanted to paint a picture of the general concepts out there today. So, I'll skip this section about kind of what's next and then maybe just go all the way to the end. I know I'm a little bit over time. So, really appreciate you all spending time today and then let me just how do I get to this part really quick? Oh, right. I'm going to skip this piece. I'll put put this online. Our booth is at LG 47. If you guys are interested in stopping by and we're hosting a giant pickleball tournament today. So, thank you for your time. >> [applause]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "rag-agent-context-layer",
  "signal": 0.5,
  "novelty": 0.35,
  "actionability": 0.4,
  "evidence": 0.3,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Основатель LlamaIndex даёт полезную концептуальную рамку эволюции RAG к 2026 году (агент сам управляет поиском, контекст поднимается на уровень MCP/скиллов) плюс конкретные приёмы для извлечения структурированных данных из документов, но доклад сильно окрашен продуктовой подачей LlamaIndex/LlamaParse и почти без бенчмарков в доступном фрагменте.",
  "knowledge_units": [
    {
      "claim": "К 2026 году наивный top-K retrieval вытесняется тем, что сам агент формулирует лучшие поисковые запросы/ключевые слова и зацикливается на инструментах поиска, даже если сами инструменты извлечения остаются простыми.",
      "type": "tactic",
      "actionable": "Вместо усложнения retrieval-пайплайна дайте агенту простые инструменты поиска (BM25, grep, vector) и позвольте ему самому итеративно улучшать запрос через агентный цикл."
    },
    {
      "claim": "Фокус смещается с управления окном контекста (чтобы не переполнить) на то, какие MCP-серверы, скиллы и задачи подключены к агенту.",
      "type": "principle",
      "actionable": "При проектировании агентной системы вкладывайтесь не в хитрую компрессию контекста, а в правильный набор подключённых инструментов/MCP-серверов под конкретную задачу."
    },
    {
      "claim": "Современный набор инструментов для работы с документами у агента должен включать не только векторный поиск, но и BM25, grep, полное чтение файла и скроллинг по документу.",
      "type": "tactic",
      "actionable": "Постройте для агента расширенный тулсет document search (BM25 + grep + vector + read + scroll) вместо единственного vector-retrieval инструмента."
    },
    {
      "claim": "При масштабной структурированной экстракции из документов (инвойсы, претензии, контракты) каждое извлечённое значение должно нести гранулярную цитату на источник и confidence score, чтобы можно было флагировать неуверенные значения перед записью в систему.",
      "type": "workflow",
      "actionable": "В пайплайне извлечения данных из документов добавьте обязательные поля citation-to-source и confidence score и используйте порог confidence для автоматического флага 'требует проверки человеком'."
    }
  ]
}
```
