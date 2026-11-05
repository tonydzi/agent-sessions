---
session: s_ac6f1180
date: 2026-09-27
words: 1969
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ac6f1180` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Building GTM AI Agents: Lessons from Deploying to 6,000 Users — [ИМЯ] [ИМЯ], Snowflake
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hi everyone. So, I think I'm one of the last speakers that is standing between you and the long weekend. So, I hope I can get your energy levels up. Um so, [СКРЫТО]. And the reason I'm here today is indeed like we launched our internal go-to-market assistant uh in September last year. It answered more than 1 million questions so far. We have roughly answered 40,000 questions a week. Um and we are the customer zero for a lot of Snowflake products. So, this is built on Snowflake co-work. Um and I meet a lot of customers every week. Okay? So, I meet a lot of enterprises, Fortune 500 companies, and then they're all trying to build similar things, and they all struggle, right? So, and then I end up like having this discussion with them all the time. Like they ask like how did you guys do it? And then we share our best practices. So, I will try to share some of those things with you. Uh I'm told that I need to have some code in my presentation. I don't, but I will try to show you at least some architectural diagrams just to make it more interesting for the engineering audience. Uh but let's jump into it. Um I think before we start like I think I already I was watching the other presentations like I think everyone tries to give their interpretation of like you know, why are we even building things for go-to-market. Okay? So, this is how I explain it to family and friends. So, let's take Snowflake. Okay? So, we are a company of like, you know, close to 10,000 people. So, if you look at that or our organization, almost half of our basically workforce is sales, right? And what are they responsible for? They're responsible for revenue generation. What do they struggle with? And I into I talked to a lot of customers. It's very common. You know, everyone's data is siloed. We work with a lot of first-party data, a lot of third-party data. It's all locked down in these like SaaS tools and things like that. And literally we have for example like reps who are using 15 different tools, not because they love the UI of those tools, because every tool has a different data point, and then they end up stitching all of that together in spreadsheets and running it there, right? And the data is endless. Like we have reps who have 1,000 accounts assigned to them, 1,000 customers. They have to stay on top of their recent news, what's happening with their consumption, did they get in support tickets recently, what was their latest earning results, everything. There's no It's not a single human on this planet that can stay on top of that much data. And then they need to do that 30 times, 40 times a day, right? So, what does AI offer for them? It offers that data democratization. No more like 1,000 dashboards, right? No more access to analysts. Like you know, um it offers automation possibilities for them, right? It frees up their inbox. It offers tool consolidation. No longer 15 different tools that I need to work for. And that brings productivity savings. It frees up your time, right? You can use that time on other things. It helps you become a better seller. You're more effective with your customers. And that translates to business results. You can cover more of your book, you know, you can have better win rates, uh you can have shorter deal cycles, and ultimately what everyone cares about, you can get incremental revenue. Okay, so that's the reason why I'm I'm working for, you know, making the go-to-market organizations more effective. But, there's a catch. These are non-deterministic systems, right? And I run into this problem every time with users. I see many, many, many AI projects failed, and then it fails on this principle. User trust is earned extremely hard and is lost overnight, right? So, at the end what you're doing is you're putting a free-form chatbot there, right? And people will come in and they will ask any question they can think of. If they like what they see in the first five questions, they come back. If they don't like what they see, it's 10 times more effort for you to win them back, if you can ever win them back. Right? So, we have a saying in our team, we say quality is P minus one. Right? And that's basically we take that very, very seriously. So, one of the things that we really cared about is when I first joined the team, you know, the team had all these like data sources connected from our top dashboards. We they had a knowledge assistant built into it and so on. We had three lines of agent instructions. And then before I even tried the agent, I opened a spreadsheet, I took the sales process, I wrote down 150 questions. And then the sales our engineering team was like, "What are you doing? We don't have that data in the agent." I was like, "It doesn't matter. These are the questions your sellers are going to ask." Right? And then we run our test, 50% accuracy, you know, like everyone's depressed and so on. So, we said, "Okay, let's make sure that we don't go for coverage, but we go for quality." Right? We don't want to try to answer 100 questions and get them 70% right. We want to answer 50 questions, but get them 95% right. Right? Because with that you get a first impression, good first impression, you build a trust with them. And then rather than being in that boat of, "Oh, this thing doesn't work." people are like, "Oh, this thing is awesome. Can I get more of that?" Right? So, we started small and 60% of the data we actually added after the launch, after the 6-7 months post launch. Today, if you look into our agent, I mean, it's not a small agent. We have 15 semantic views, 85 tables, 3,000 columns of data. We have like five to six different MCP connections on it. You know, close to 20 skills connected to that and so on and so on. Right? So, it's a huge system that we are managing in here. And then you cannot just launch these things to everyone, right? So, we said that, "Look, we need to do this in a controlled way becau
...[middle elided]...
echnical side of the story, like how do you derive change management, and so on. So, feel free to check those. Um and yeah, I think that's the end of my talk. Okay. >> We have time for one question. Okay, there you go. >> Thanks for the talk. Um I don't know if you already said this, but I saw in the the titles of the articles Snowflake Intelligence. Is that an underlying context or layer that the tool or system you built was on top of, or was that the tool itself or something else? >> Yeah, Snowflake Intelligence, we renamed that to Snowflake Co-work a couple of weeks ago in our summit. That's basically our no-code agent platform that we basically build have available for our business users. I mean, the advantage of that is that all of these tools are on like, you know, you know, Cortex analyst or Cortex search or Cortex sense, a lot of those things are basically comes out of the box. We made a strategic choice for our internal thing where we said that, "Look, it is important that we bring all our data together." And we do that in Snowflake. We bring all the first-party, the third-party data, all the Salesforce data, everything, the call transcripts, and so on, all together. And then these agents then can basically basically inherit a lot of the role-based access controls and so on. And I literally can deploy these agents without writing a single line of code, right? And then, you know, you don't need to worry about the UI, the chat UI comes out of the box, and so on. And then we have been the customer zero of that like internally to build this ourselves. And then, you know, our customers are able to go and then build similar things basically on Snowflake over platform as well. And it comes with the guardrails and things where you don't really need to worry about them going very, you know, crazy on, you know, what data sources to do things, and so on. So we are able to do a lot of curation. We are able to do a lot of security guardrails in there as well. Thank you.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding",
  "signal": 0.6,
  "novelty": 0.45,
  "actionability": 0.6,
  "evidence": 0.7,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад про запуск GTM-агента на 6000 пользователей внутри Snowflake содержит практичные уроки о доверии и поэтапном запуске, но сильно завязан на их платформу Cortex/Co-work и подан как кейс, а не техническое руководство.",
  "knowledge_units": [
    {
      "claim": "Доверие пользователей к non-deterministic системе (чат-боту) завоёвывается медленно, но теряется мгновенно: первые 5 вопросов решают, вернётся ли пользователь.",
      "type": "principle",
      "actionable": "Перед публичным запуском AI-ассистента специально протестировать первые впечатления новых пользователей — именно они определяют, будут ли им пользоваться дальше."
    },
    {
      "claim": "Лучше отвечать правильно на узкий набор вопросов (95% точность на 50 вопросах), чем пытаться покрыть всё и получить низкое качество (70% на 100 вопросах).",
      "type": "tactic",
      "actionable": "При запуске agent/RAG-системы сознательно сузить охват данных/тем до тех, где можно гарантировать высокую точность, а расширение делать постепенно после релиза."
    },
    {
      "claim": "До оценки агента команда вручную составила 150 реалистичных вопросов от лица конечных пользователей (продавцов), а не полагалась на то, какие данные уже подключены.",
      "type": "workflow",
      "actionable": "Перед оценкой любого AI-ассистента писать эталонный набор реальных вопросов целевой аудитории независимо от того, какие источники данных уже интегрированы, и мерить accuracy по нему."
    },
    {
      "claim": "60% источников данных и функциональности были добавлены агенту уже ПОСЛЕ публичного запуска, а не до него.",
      "type": "tactic",
      "actionable": "Не блокировать запуск MVP-агента ожиданием полного покрытия данных — расширять охват итеративно на основе реального использования после релиза."
    }
  ]
}
```
