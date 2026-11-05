---
session: s_71733cc4
date: 2026-09-20
words: 2110
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_71733cc4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The unreasonable effectiveness of BM25 for agentic search — Jo Kristian Bergum, Hornet.dev
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] So great being here. Uh I'm Joe Bergam. I'm the CEO of Hornet Dev and I'm here today to talk about the unreasonable effectiveness of BM25 for Agentic Search. So how many of you heard about BM25 before? Is it new or is it Well, quite a few. So that's great. Uh I'm also watching the World Cup. Norway is playing there uh against the Ivory Coast second half. Norway is leading so that's good. So yeah and at Hornet we are building retrieval infrastructure for agents and uh I've been working on search and retrieval problems for a long time. As you can tell I'm gray hair. Uh been working in this space for more than 20 years. Um and in the talk today I'll talk about why this kind of [ВОЗРАСТ] lexical scoring function is uh making a strong comeback. First I will talk a little bit about what I mean by agentic search or aentic dribble and kind of define that for for you all of you. Um my definition is that agentic search is essentially search inside agent loop. So you have an agent that is trying to accomplish a task, write a coding or do some deep research or whatever task and inside that you have some kind of information need for the agent, right? In order to get that task done successfully and you essentially need three things uh to kind of build a good agentic search system and that is you need a capable model, a model that is able to use tools and is able to formulate queries. You also need a harness around the model and how you kind of expose the retrieval and the search functions to the model. There's different ways to do that. It could be through tool calling or it could be through code mode. Um, Edo here uh demonstrated what I call code mode for exposing retrieval infrastructure. So that's the harness part and you also need uh a retrieval engine to be able to do searches efficiently potentially over billion scaled uh document sets and to define BM25. So BM25 actually stands for best match 25. So there were some researchers doing plenty of different experiments and experiment number 25 turned out to be the best one. So that's that's the background of the name. It's essentially a scoring function. So you can imagine you have a query and you have a document and you calculate some kind of score by interaction between the query terms and the document terms and you come up with a score and you hope that this score kind of is a good proxy for the relevancy of the document with regards to the query. Right? So one way to calculate BM35 would be to take all the documents and score each of them you know and then figure out what are the top K documents and then there's like 30 or 40 years of interest in how you accelerate that type of retrieval top K lots of different algorithms we also invest a lot in that I'll show something in this direction but BM25 is the scoring function and there is a way to kind of accelerate top K retrieval Uh BM25 hasn't changed. It's the same scoring function, but the change here is really that we got a more powerful user. Uh Edo talked about general knowledge. The LLMs today have a lot of general knowledge. They know about entities, they know about companies, they know about dates, they know a lot, right? And by using that kind of implicit knowledge that is built into the parametric model, uh they essentially become very good at search. Um and that's the really change uh here now that we're is kind of making BM25 more relevant and BM25 used to be a kind of a baseline function. Any information retrieval research would include a BM25 baseline and then you would put something fancy advanced neural fancy stuff and then you would compare it with BM25. I also think it's interesting in how we evaluate search before because you will simply look at 10 blue links and you like have scan it and you compute some metrics. A lot of that is now going away because the agent is not really it's kind of powerful in the way that it can type out a lot more queries than a human can do. So it's less relevant to think about evaluating these systems just by a single shot query. And this is one of my kind of favorite benchmarks out there. I like to talk about benchmarks. So browsecom plus is a deep research benchmark [snorts] uh published in a paper last year and it has almost or exactly 830 questions. These are riddle like think about it like a pub quiz. Do you have pub quizzes in the US? Yeah. Okay great. So like kind of a riddle type of questions quite long and the agent the harness of this kind of or the protocol of this benchmark is that you have a model and it gets a very simple tool called search and it accepts a query string and you return some snippets back to the model and the corpus is about 105,000 or 100,000 documents. So that's kind of tiny and these are web documents and the end to end accuracy. Um all of these questions have a golden reference answer and you can kind of check if the model and the entire loop produces that exact answer. Um but why kind of why do we need retrieval? I like to compare context windows with floppy discs because I'm old in the 80s, right? We install this kind of games on our computers using floppy discs. So one kind of you guys are so Brasov so you don't probably have this kind of nostalgy but one floppy disc could fit about 1.4 megabytes of data and the current models before they start degrading in quality that's I in my opinion around 350,000 tokens. So that's one floppy disc of data right. Um, so you need retrieval in order to to fetch the information that you actually need to put into the context window and browse plus really demonstrate how uh retrieval quality affects the end toend accuracy of the task. Right? The endto-end accuracy here is essentially is the model equipped with this search tool able to answer the question, right? the riddle like question and if you artificially just stuff the evidence documents that is needed to answer this question into the context window of the model the accuracy is really high right so reasoning is not the
...[middle elided]...
t's it's set to and for example for question answering does it get the answer right and we at hornet we are betting on BM25 as one of the primitives and we have set out on a vision to kind of have the best most efficient way to evaluate uh BM25 because I think it's such a strong fundamental primitive And this illustration compares some anonymized engines comparing with Hornet on the same type of same type of hardware with um web documents, 100 million web documents on a single node. And as you can see, Hornet has a much more efficient implementation than the other engines and can do more throughput for the same type of bucks, which for a lot of companies that are building infrastructure at the moment for web search etc. means a lot in savings. >> What is the yaxis? >> The y-axis is QPS. Sorry. >> The Y axis is Oh, sorry. The Y axis is latency. I'm sorry. So, four claims to take away from this talk. There's a new user. It's more powerful. It's able to type faster. It's able to read faster. It's able to reformulate queries and it has a lot of general knowledge which makes simple tools like GP and BM25 more powerful. That's number one. Number two, which BM25 do you mean? Uh there are differences in implementation, in performance, in parameters. So think about that. And also why is it effective for agentic search? It's simply because it's explainable for the model. So the model can see and also use it in combination with GP, right? Because you have literal matches and GP is almost about literal matches as well. And the combination of these two is a very strong agentic search or agentic retrieval paradigm. There's a lot of references. I think I will publish a talk uh or the talk will be published and also the the slides and if you hated it, you can tweet at me. Um there is not I was told that there's not a room for for questions but happy to chat about retrieval. You will find me around the conference. Probably best way to reach me is through my ex account and that's it.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-search-bm25",
  "signal": 0.7,
  "novelty": 0.55,
  "actionability": 0.6,
  "evidence": 0.7,
  "durability": 0.75,
  "volatility": "medium",
  "half_life_days": 730,
  "why": "Практик с [ВОЗРАСТ] опытом в поиске объясняет на бенчмарке BrowseComp Plus, почему старый BM25 снова эффективен внутри агентных циклов, и даёт конкретные архитектурные выводы для тех, кто строит retrieval для агентов.",
  "knowledge_units": [
    {
      "claim": "BM25 стал снова эффективен не потому что изменился сам алгоритм, а потому что 'пользователем' поиска теперь выступает LLM — она умеет переформулировать запросы, знает сущности и даты из параметрической памяти, и это компенсирует примитивность лексического скоринга.",
      "type": "principle",
      "actionable": "При проектировании retrieval для агентов не отбрасывай BM25/лексический поиск как устаревший — комбинируй его с LLM, которая умеет генерировать и переписывать запросы, вместо того чтобы сразу тянуться к дорогому dense-retrieval."
    },
    {
      "claim": "На бенчмарке BrowseComp Plus (830 вопросов-загадок, корпус ~100k документов) точность ответа агента почти линейно зависит от качества retrieval: если золотые документы искусственно положить в контекст, точность резко растёт — значит узкое место чаще именно поиск, а не reasoning модели.",
      "type": "benchmark",
      "actionable": "Прежде чем тюнить промпты или менять модель на более 'умную', проверь через ablation (искусственно подсунув правильные документы), не является ли реальным узким местом именно качество твоего retrieval-слоя."
    },
    {
      "claim": "'BM25' — не единая вещь: разные реализации (Lucene, Elasticsearch, Hornet и др.) заметно отличаются по перформансу и качеству из-за разных параметров и деталей имплементации.",
      "type": "tool-caveat",
      "actionable": "При выборе поисковой инфраструктуры для агента сравнивай конкретные реализации BM25 бенчмарками на своих данных, а не полагайся на название алгоритма как гарантию поведения."
    },
    {
      "claim": "BM25 хорошо сочетается с grep-подобным точным совпадением и лучше объясним для модели, чем нейронные/dense методы, потому что оба построены на буквальных совпадениях терминов — это делает связку 'LLM + BM25 + grep' сильной парадигмой агентного поиска.",
      "type": "workflow",
      "actionable": "Для агентного поиска строй гибрид из простых явных инструментов (BM25 + grep) вместо сложного dense retrieval — модели проще понимать и комбинировать результаты буквального поиска."
    },
    {
      "claim": "Классические метрики оценки поиска (топ-10 ссылок, разметка релевантности человеком) теряют смысл для агентного поиска, потому что агент выпускает на порядок больше запросов, чем человек, за одну сессию.",
      "type": "principle",
      "actionable": "Пересмотри свои eval-протоколы для retrieval: оценивай end-to-end точность агента на многошаговых бенчмарках (типа BrowseComp Plus), а не однократный precision@k по одному запросу."
    }
  ]
}
```
