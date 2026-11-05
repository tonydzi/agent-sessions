---
session: s_0c884a22
date: 2026-10-01
words: 1946
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_0c884a22` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Your Agents Are in Solitary Confinement: Why MCP & A2A Aren't Enough — Toth Luzin, Band
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hi all. My name is Toth. I'm co-founder and the CTO at bank. Now, before we start let's do a bit of trivia. Orc C okay. If C, raise your hand. K? Who believes both are correct? Okay, just a couple. Both are correct. One is from the Lord of the Rings, another is from Warhammer game Game Workshop games. I have in my agenda four topics to cover. Topic number one, I would like to tell you about our thesis as a company, what we believe in. Then we'll talk about the AI evolution from adversarial agents to loop engineering and beyond. Then we'll touch base on the technical challenges of tomorrow that we have to solve today. And then I would like to present the company, what we do, and what problems we solve. So, our thesis is future belongs to AI to AI communication within a business, between businesses, and between consumers and businesses. Agents will be everywhere. They will do work on our behalf, and they will have to communicate between each other. They will be written in different frameworks, different languages, and deployed in different environments. And these agents will be fully autonomous. And they will communicate with each other without human intervention. Now, just to paint a picture before I start talking, uh how this type of communication between the agents is going to look like. So, what you see here is a conversational space that agents can create themselves, so they can be added. They will receive a task either from a human or from another system. And they will be able to discover other agents add them as a participant in this conversation space, have back and forth communication, solve the task, and report back to humans. This is how the future that you all read in the newspapers will look like. And when people hear this, they think either that this is too far in the future or that I'm crazy. Okay, that's it. And here is an example of a conversation I had with a CTO of $10 billion company who said that before thinking about technical solutions to hypothetical problems like multi-agent coordination, I try to keep things simple and avoid the problem. Now, let's unpack. Is multi-agent coordination a hypothetical problem? Is it possible to keep things simple? And is it possible to avoid the problem? Now, let's talk a bit about the adversarial agents as a as a concept. Um we all use this. I'm pretty sure everyone here is a developer. And as a developer, you have two cloud or coding sessions. One is doing the work, another is reviewing the work. And you probably have not only two sessions, you probably have multiple tabs and multiple sessions working working at the same time on multiple problems. You are basically acting as a router, a Cisco router or a switch between two stateful agents that do work on your behalf, but they have no ability to communicate, hence you need to prompt them. Let's talk about loop engineering. You've heard the the guy before talked about Peter and Boris, right? So, what they say to you? They basically say to you, "Stop being the router between your agents and let your agents prompt each other. Now, what they're basically saying to you is instead of being the router and copy-pasting stuff, start fighting with Python and TypeScript libraries and different abstraction layers that will invent how agents should prompt each other. We also have protocols. A2A, MCP, ACP, and then other protocols crypto-related. Simple. Solves all the problems, right? So, this is how your multi-agent system looks like probably in production. MCP, maybe if you're super advanced, it's A2A. And sounds simple. You call agents as tools, maybe you connect to agents through A2A, and life is great. But, MCP, calling agents as tools, it's completely stateless. If you want two agents to be stateful, sticky sessions, good luck to you. A2A is client-server. If I'm an agent, I can send a task to another agent, but if this agent also wants to send task to me, we both have to be a client and a server. Chaining multiple agent equals together involves REST API timeouts. Good luck managing that. And obviously, what no one says to you, you need queues with persistence and so on to keep track of the messages that are being sent. And of course, discovery, which is not even part of the A2A protocol. So, you're basically doing the planning work. You're not creating a multi-agent system. You deal with planning. But, we have messaging platforms. Slack. Anthropic released a wonderful agent. You can talk to it in Slack. We have personal agents here and I connected to Telegram, right? Wonderful. To connect an agent to a Telegram, five steps. Discord, seven steps. Slack, eight steps. WhatsApp, 11 steps. Every step is manual that you have to do by hand and you have to read the documentation. Again, you're doing doing a lot of planning and manual work. And this gives you only one thing and one thing only, an agent that can talk to a person, usually it's you. Your agent is still alone. They cannot see each other. They cannot communicate with each other. They are in digital solitary confinement. So, let's unpack the statement I heard from the CTO. Is multi-agent coordination a hypothetical problem? Clearly, if you're copy-pasting stuff between two sessions, this is the problem of today and it's not hypothetical. Plugging in MCPs and A2A, this is today's problem. It's not a future problem. Is it possible to avoid the problem? Clearly, it's not possible because otherwise it would have all work with only one session and not two and we would have no need to call other agents as tools and so on. But the question is, is it possible to keep things simple? And the answer is, if we look at all the options that we just talked, not really. But how hard can it be to connect two sessions, two processes on my laptop together? How hard can it be to connect my cloud to Lambda? Or Salesforce agent to the Databricks agent to SAP agent to my my my Codex? Actually, it's pretty hard. Think about it. These agents, even yo
...[middle elided]...
ls right now, they're trained on a lot of data so they understand very, very good how to communicate through messaging platforms. So, here I have real work that I've done this morning. Engineering manager, developer, and architect, different instances of quad quad working together, reviewing PRDs and SRS, we are implementation. there is no need to hand code all the loops. They know how to do it natively. And for the managers, we have full statistics. Let me kill off the manage the the engineering manager who sent too many messages. So, you can see the attribution. You can see the full [clears throat] user chain cost. So, if you ask a question, if my developer is actually involved in the code he pushes as a PR, or it's all AI slope, you can see it here. Not only locally, right, but also through the remote agents. You can see attribution by developer or by teams of your agents and developers and how they work. Everything is gets updated in real time. You can see all agents, and every agent is basically a session, right? So, if I click here, I can see all the sessions of my Cloud and Codex instances that are running and they're connected to the platform. They're connected to a global platform. So, if I want, I can connect any of you to any of my agents in 30 seconds. Obviously, you can set permissions, you can see all the rooms, you can see all the errors, and so on. And also, you can see work. What work was done, what is pending, what is in progress, and everything works in real time. Thank you very much. If you want to know more about the future software development that does not involve you pulling in another 50 packages, and if you want to enable your Salesforce and Slack and Data Bricks and Cloud and Codex to work together and collaborate, come to our booth LG17. QR codes for the Band infrastructure layer and for the Jam, the uh desktop application to allow you to be part of this future that everyone talks about but has never seen. Thank you. >> [applause] >> Hey.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "multi-agent-protocols",
  "signal": 0.35,
  "novelty": 0.25,
  "actionability": 0.3,
  "evidence": 0.2,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад — по сути питч продукта (Band) с демонстрацией и приглашением на стенд, но по пути называет реальные болевые места MCP/A2A, которые инженеру стоит учитывать при проектировании мультиагентных систем.",
  "knowledge_units": [
    {
      "claim": "MCP при вызове агентов как 'инструментов' полностью stateless — поддержать sticky-сессии между двумя агентами через MCP само по себе не выйдет, нужен отдельный слой состояния.",
      "type": "tool-caveat",
      "actionable": "Если нужен многошаговый диалог между агентами, не полагайтесь на голый MCP-tool-call — добавляйте внешнее хранилище состояния/сессии поверх."
    },
    {
      "claim": "A2A — протокол клиент-сервер: если агент А хочет и отправлять задачи агенту Б, и получать от него, оба должны реализовать роли и клиента, и сервера; discovery агентов вообще не входит в спецификацию A2A.",
      "type": "tool-caveat",
      "actionable": "Закладывайте отдельный механизм discovery агентов и симметричную реализацию клиент/сервер с обеих сторон, если нужна двусторонняя коммуникация через A2A."
    },
    {
      "claim": "Цепочка вызовов нескольких агентов друг через друга упирается в таймауты REST API и требует очередей с персистентностью для надёжной доставки сообщений.",
      "type": "tool-caveat",
      "actionable": "При построении цепочек агентов проектируйте очередь сообщений с персистентностью и ретраями, а не полагайтесь на синхронные REST-вызовы с дефолтными таймаутами."
    },
    {
      "claim": "Подключение одного агента к обычным мессенджерам требует заметного ручного труда: порядка 5 шагов для Telegram, 7 для Discord, 8 для Slack, 11 для WhatsApp — и даже после этого агент может общаться только с человеком, а не с другими агентами.",
      "type": "benchmark",
      "actionable": "Закладывайте время на ручную интеграцию при подключении агента к каждому новому мессенджеру и не ждите, что это решит проблему межагентной коммуникации."
    }
  ]
}
```
