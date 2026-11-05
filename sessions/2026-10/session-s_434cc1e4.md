---
session: s_434cc1e4
date: 2026-10-27
words: 2067
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_434cc1e4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Why Your Company Needs a Context Graph (and How to Build It) — Gil Feig, Merge
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Right. Thank you all for for coming. Um my name is Gil Feyg. I am the co-founder and CTO of Merge. Merge helps companies build production AI very easily. We are the connective infrastructure uh to make everything come together. Uh today I'm going to be talking about why you need a context graph and how to build it. What I'm not going to do is talk about specific technology you should be using. Uh you can talk to your agent about that. It will help you. There's a lot of good technologies that can back this. Uh the focus of this is uh why you need a context graph and then sort of in a in a higher level how you should structure it, what the components should be, uh and how things come together to build the best possible uh brain for your company. If you haven't gotten a hat yet, by the way, my team is walking around passing out hats. They're They say well connected. Um so let's dive in here. So I'm not going to spend much talking about Merge, but just a quick overview of us. Um we have over 400 enterprise customers, OpenAI, Ramp, Netflix, Perplexity, a lot of companies across the board using us for both internal and customer-facing AI use cases. Uh we have three different products, Unified, Agent Handler, and Gateway that cover a lot of the components of it. Um we were founded 6 years ago by me and my co-founder Shen Shi. We've raised three rounds. Uh we're 130 employees in the three most beautiful cities in the world. All right. So quick agenda here. Step one or number one, we will talk about what a context graph even is and why it's so important that every company has one. We'll go into the different tiers of context, what what types of data, what types of of uh sort of logic from your company should be making it into your graph. We'll talk about context selection strategy. How are we picking the most relevant content for our agents or contexts for our agents at any moment in time? Traceability and provenance. How do we know where that data came from, who requested it, when it when it's from, is it fresh, all of that. And then lastly, some final key takeaways. At the end, I'll stick around if you do have any questions. Uh so, feel free to to come up to me afterwards. All right. So, what is a context graph in this talk? We're not going to go into the nodes and the edges that connect each node in a true graph infrastructure. We're going to talk about the company brain. Your company context graph consists of a lot of different components. It has third-party data. What are the other systems you use, like NetSuite, uh like like Jira. Um it has structured context. Uh so, that could be uh data coming in from other third parties. That could be data that that you all have put into your context layer. Uh things like things like static documents that you want to always be passed to your agents. We have memories. These are things that are formed. We all know memory, things that are formed as you're using the agent, telling it to remember things, things that your agent thinks that it should remember on its own. And then we also have skills. Uh and skills are a very very important part of your context graph, which we'll get to. All right. I see some picture Okay, cool. Uh so, moving on. Let's get Let's go through an example here. We're going to use this example to guide why it's not it's not enough to just connect a single MCP server or a couple MCP servers and call it a day. So, let's ask this simple question. One of one of your employees or or customers asks your agent, "Why was customer A upset last week?" Pretty simple question to answer. The agent goes, it sees it has access to your Zendesk ticketing, and it can check and say, "Hey, what it what tickets were filed by this customer last week?" Great. We saw that they saw that the API sync was broken, um and specific details about what went wrong. We also see the customer filed three tickets total, all of that. Great, that answers that question. But what if we want to extend that? And what if we want to say, "Which customers were upset last week?" That becomes a lot harder because you now have to have your agent load in every single ticket from Zendesk that happened in the last week. What if we're saying, "Which customers were upset in the last year?" We should be able to answer that. Our agent should be able to answer that, but it can't if it has to live live look up and pull tickets 100 at a time, thousands and thousands of those until it times out and it just can't answer the question. So, MCP is not fully solving a lot of these problems because the underlying access patterns of the APIs of these other platforms don't support a live look up methodology. If you could ask your ticketing system something semantically, if Jira exposed an endpoint that said, you know, that you could query in English, "Which customers were upset last week?" and it returned that data, that would be great. But no platforms incentivize to do that because it costs them money to vectorize it and it makes it so you don't have to visit their platform as often. So, you need a sinking layer on top of this. You can't just use MCP to live look up for things that you want to go deeper into, that you want to semantically question, you need to actually sync a copy of the data locally. Okay? This doesn't apply to everything. So, you might have you know, let's say static look ups to Stripe. We're always going to be asking Stripe a question about a specific customer. We're always going to be taking a single action in Stripe. That can be MCP. That can be live. But if you need any form of semantic look ups, any form of analysis that is beyond a simple look up, simple question, but requires looking across a a vast data set, you have to sync a copy. So, that becomes the next part of your sinking layer of your of your, uh, context layer. So, you have your MCPs, your live look ups, you have your synced or your cached look ups as well. And that you're pulling in from a third-party, you're put
...[middle elided]...
 summary. We're going to assume there's no skills here. So, we'll check that. If it's still or missing, we're going to call the CRM using a live API lookup. Then, we'll query the ticketing system for the last support interaction. Again, that's cached if within the SLA, otherwise it might have to do a live lookup. We're only we only want to pull five tickets. We can't pull the full history because again, when we have live lookups, we run into timeout risk. And then lastly, we'll generate a derived summary. We might store that derived summary, and we'll pass that back. So, key takeaways, tools are not context. A context graph is going to help you reason across the whole company. It's not just tools. It's data. It's synced data. It's processes that you have as a business. Who is documenting, you know, when a customer complains, what do we do? How does it know to always route to the right place? That is a skill. These It's your company's skills. It's your processes. It's your data, and it's your tools and actions you need to take. More data, not always better. You want fresh, high-quality data. You want to pull only what you need. When you do have to sync data, you want to structure it properly, so it's accessed in the right way. And then lastly, every answer has to be traceable. You do not want to be left in a position where your AI made a bad decision, and you have no idea why it did that. So, last piece, plugging merch here. Enterprise AI runs on us. We power these features for a lot of companies. We have Gateway, which is an LLM router. We have Unified, which helps you sync data from third parties out of your customers' platforms. And then we have Agent Handler, which is live MCP connections pre-built across hundreds of tools, governed identity all built in, uh including provenance, uh and yeah, it's plug and play for both internal and customer-facing use cases. So, if you want to build an easy context layer, hit us up. Thank you, everyone, for listening. >> [music]

---

**Claude:**

{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "context-graph",
  "signal": 0.55,
  "novelty": 0.4,
  "actionability": 0.55,
  "evidence": 0.35,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад даёт полезную архитектурную рамку корпоративного «контекстного графа» (синк против живого MCP, уровни контекста, трассируемость), но подаётся без бенчмарков и с рекламой Merge в конце.",
  "knowledge_units": [
    {
      "claim": "Живых MCP-вызовов недостаточно для вопросов с семантикой и агрегацией по большому набору данных («какие клиенты были недовольны за год»): API платформ не поддерживают такой доступ, а постраничная выгрузка тысяч тикетов упирается в таймаут.",
      "type": "tool-caveat",
      "actionable": "Для аналитических и семантических запросов по тикетам, CRM и т.п. синкай копию данных локально и индексируй её, а не полагайся на live-lookup через MCP."
    },
    {
      "claim": "Разделяй доступ по типу задачи: точечные lookup-запросы и одиночные действия (например, запрос к Stripe по конкретному клиенту) остаются live через MCP, а всё, что требует анализа по широкому набору данных, идёт через синк или кэш.",
      "type": "principle",
      "actionable": "Классифицируй каждый источник данных: «точечный lookup / действие» → live MCP, «семантика или аналитика» → синкаемый слой; кэшируй с учётом SLA свежести."
    },
    {
      "claim": "Контекст компании состоит не только из инструментов: данные третьих сторон, структурированные статические документы, память (в том числе формируемая самим агентом) и скиллы с бизнес-процессами («что делать, когда клиент жалуется»).",
      "type": "principle",
      "actionable": "Оформи процессы компании как скиллы и держи их в слое контекста рядом с данными и памятью, а не только подключай MCP-серверы."
    },
    {
      "claim": "Больше данных не значит лучше: нужны свежие, качественные данные, а при live-вызовах лимитируй выборку (например, последние 5 тикетов вместо полной истории), чтобы не упереться в таймауты.",
      "type": "tactic",
      "actionable": "Задай в стратегии отбора контекста лимиты на объём live-выборок, порядок «скилл → кэш → live API» и сохраняй производные сводки (derived summary) для повторного использования."
    },
    {
      "claim": "Каждый ответ агента должен быть прослеживаемым: откуда данные, кто запросил, насколько свежие, чтобы можно было разобрать плохое решение ИИ.",
      "type": "principle",
      "actionable": "Логируй для каждого ответа источник, время и автора запроса данных (provenance) и степень свежести кэша, чтобы разбор инцидентов был возможен постфактум."
    }
  ]
}
