---
session: s_35e27bbe
date: 2026-09-27
words: 1895
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_35e27bbe` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How AI Agents Let GTM Teams Scale — Justin Joyce, Cloudflare
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Well, thank you everyone for joining. I'm hoping that you guys had a great time so far at this conference and you guys have a lot of takeaways back, you know, to your company. Um, I don't know if any of you guys saw the uh AGI pills downstairs. Yeah, well, I just took some. So, if I say any phrases about that's the uh the the gun What's that What's that the phrase? That's the uh burning gun or the smoking gun or I start hallucinating in general, well, please snap me back. That's probably just the AGI pills. All right. So, without further ado, let's get started. Uh my name is Justin Joyce. I'm a principal sales operations and strategy manager at Cloudflare. Um and I work with the go-to-market team as part of the revenue operations organization, specifically on the teams that uh produce leads for the sales teams, as well as the customer experience team, which works on uh the customer experience after the sale the sales have been done. And uh just a little background about me. As Moda said, I started in sales operations uh and sales and then I moved to sales uh to the machine learning side about the last 7 years at Grainger. And I really wanted to do that to be able to learn how to uh have prescriptive analysis and prescriptive uh prediction so I can help the business better to make decisions and to understand what's the next step next best step. So, uh 6 months ago, I had an opportunity to move back into sales operations uh because I really wanted to use all the skills that I'd been learning from machine learning as well as from sales operations in general. So, what's the general problem? The general problem is that traditional go-to-market does not scale. There's a few um facets to this. The first facet is that usually teams on the back office side, uh they're either doing work in Excel or sheets at worst, um building analysis each week, multiple hours a week, and as they take on multiple projects, it gets exponentially long with how many of those analysis that they're doing. Uh at best, they are producing dashboards, um providing information to the uh leadership and executive team, um which, you know, meets the needs of most teams, um but not all of them. And that needs meets that needs uh means that in general, not all the requirements of the go-to-market teams are met. They're not able to really provide all the information that the teams need when um they need it. The second problem, which is more on the go-to-market side with the sales and uh the sales teams and the other teams that I mentioned that I support, is they have two gaps. Essentially, the first gap is the context gap, meaning when a salesperson is uh talking to a prospect um one call and talking to a current customer in the next call, or um talking at an adoption conversation the call after that, they have to constantly switch contexts and they have to gather information for those specific calls, which is good. They really need to get that information to have those calls and understand how to approach the situation, but they have to do all that work in between. Um the second one what is like what I like to call is the expert gap, which is the gap between how your expert salesperson or expert go-to-market um sales individual, how he would approach a situation, how he would talk to a prospect, how he would uh work on adoption call, how he would handle a customer satisfaction issue, and between also the a new salesperson or someone that's just ramping up. So, ideally like everyone working at the same operational level, so you have consistency in execution, consistency in messaging of how to assess a a customer's problems and how your product can help fit that portfolio. So, with these two problems with manual work as well as uh salespeople not having enough information and having the gap of having to get all the information they need and gather that as well as not be able to execute the same level, it really creates an inefficiency in the go-to-market organization. And so, for the last 6 months or so since I've joined Cloudflare, I've been really focusing on how can I make this operation efficient from back to front and there's a lot of great things that we've been doing at our company in general that's helped me enable that and I really want to share some of those findings with you. So, the framework that I'm proposing here, which I think is is it's going to really be effective in as we flesh this out in the future is a three-pillar approach. The first pillar approach is how can we scale analysis and the ability of operations team to meet the data needs of executives, leadership, as well as be able to build applications using business context. How can they take things that would take 2 hours to do down to 5 minutes? Um back in well, not back in January of this year, I after I joined I joined the company, I had built these skills and I'd started asking questions of the data directly and I was able to get answers immediately while doing other things and I saw the huge power of how if we can scale the analysis and the operations of the teams, we can actually focus on the second part of my job, which is strategy. The second pillar is how can is to scale insight. There's story in the data, and how can we provide that to the team? How can we provide that team at, you know, the weekly level, at the different levels of management? How can we provide that information, that insight, that story to every customer that the sales teams are talking to? And the third one, which is arguably the biggest one, is uh to provide self-service capabilities to the go-to-market team. When these sales individuals, when they're talking to a customer, how can they get the expert-level information that they need to interact with that customer and to best assess, you know, how they should approach the situation, how to handle rejections, how to upsell them, and how to handle customer satisfaction issues. Uh this is a huge part of what I've seen 
...[middle elided]...
is uh agentic run uh team. So, through all these uh different pillars that I talked about, we've really been able to 2x our efficiency and be able to serve the teams as well as allowing them to be able to get the information that they need to do their job. And some some things um that I see going into the future. Number one is a deeper integration with uh our systems that we work in. So, for example, those QBR decks and um renewal call skills, uh how can we set up meetings for the go-to-market team and embed those artifacts in those meetings so they don't have to actually pull them. We can allow them to that self-service portal to be more ad hoc in what they need. But, that requires some information or some security setup and how can we do that? And then also, another example is getting meeting notes from those calls, which you have to set up that across the board. So, there's some system side thing that we have to work on there. The second thing is harder problems around quoting and approvals and updating the CRM itself. Uh we use Salesforce and we're just in the midst of building the connections and the ability for us to update Salesforce with these Agenty systems. And I see that being um set up in a way that I set up with that automated analysis where you have workflows uh to just make sure that everything is getting um done right. And the second thing is we're sort of reached the Cambrian stage of using Agenty systems, which means there's an explosion of excitement and skills and finding out ways to solve anything with AI. But, I see as we get to this uh fuller integration and standardization, we're going to uh want to come back and and and not really limit, but just figure out a really strategic approach for allowing each team to use the Agenty system so that the source of truth in all the systems are aligning. All right. Well, thank you for joining this talk and I appreciate you, um you know, coming here. Hope you have a great conference. >> [applause] [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-gtm-ops",
  "signal": 0.15,
  "novelty": 0.1,
  "actionability": 0.15,
  "evidence": 0.15,
  "durability": 0.3,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это конференционный кейс-рассказ сейлз-опс менеджера Cloudflare о пользе agentic-систем для GTM-команд, но без конкретных инструментов, промптов, архитектур или проверяемых цифр — в основном мотивационная риторика и общая трёхчастная рамка.",
  "knowledge_units": [
    {
      "claim": "Автор делит проблему GTM-масштабирования на два разрыва: 'context gap' (продавцу нужно каждый раз заново собирать контекст между звонками) и 'expert gap' (разница между уровнем эксперта и новичка в продажах)",
      "type": "principle",
      "actionable": "При проектировании agentic-помощника для продаж/поддержки клиентов явно разделять задачи на 'подтягивание контекста для конкретного диалога' и 'воспроизведение экспертных паттернов поведения', чтобы не смешивать эти два разных типа автоматизации"
    },
    {
      "claim": "Предложенный фреймворк для agentic GTM состоит из трёх слоёв: масштабирование аналитики (быстрые ответы на data-запросы вместо ручных Excel-отчётов), масштабирование инсайтов (доставка 'истории из данных' команде и клиентам) и self-service для сейлзов (экспертные ответы в момент разговора с клиентом)",
      "type": "workflow",
      "actionable": "Использовать эту трёхуровневую декомпозицию (аналитика → инсайты → self-service) как чек-лист при планировании agentic-системы для операционных/сейлз-команд, но не как готовое техническое решение — конкретных инструментов и архитектуры автор не раскрывает"
    }
  ]
}
```
