---
session: s_b1d5a36f
date: 2026-09-21
words: 885
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-21 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b1d5a36f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Meet the Data Agent in ChatGPT Work
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Your company has invested in data. Now let's put it to work. The ChatGPT work data agent brings trusted data and your data team's expertise into everyday decisions. Let me show you how we can go from a business question to a plan the team can act on. On my way into work, my management team asks how our new product launch is going. I send the question from my phone. The data agents get to work using our trusted data and existing sites context. By the time I'm at my desk, the analysis is ready. Here's the opportunity. Returning creators are driving growth, but look at the funnel. Only about 16% of people with access have started creating. We need to help more customers take that first step. With the data plugin, I can dig into evidence, the metric definitions, the underlying data, and the SQL queries behind the report. Our data team can inspect how the answer was produced and check that it answers the right business questions. Now I can check Slack conversations and existing reports in Google Drive for clues about why customers aren't creating sites. The feedback points to uncertainty about where to start. That gives me a practical recommendation. Give users an in-app pointer on how to publish a site. With those recommendations, I ask ChatGPT to help assign owners and next steps. I review the plan and share it in Slack. Now the right people can take action with clear responsibilities and a shared way to measure progress. Next, let's give the team a shared view of progress. The data plugin turns this analysis into a dashboard, so product leaders, customer success, and the data team can work from the same trusted sources and definitions. Now everyone has a place to answer the questions that come up every week. Are more customers adopting this product? Are creators coming back? Which customer groups need more help? Teams can explore those questions themselves, while the data team focuses on deeper investigation. I also want to be alerted if weekly creator adoption drops compared with the previous week. I asked ChatGPT to help define the rule, how large a drop matters, and when to check, and who should hear about it. Review those details before scheduling. With refresh options, we can keep that shared view current throughout the launch. The value is an ongoing way to spot changes, agree where to focus, and decide when to adjust the plan. And you're probably wondering how we can create consistent data across the organization, and that's where context comes in. The analysis and dashboard we just saw use an existing site's context layer. Now, let's look at how the data team created that foundation so future questions use the same business definitions. Here, I used the data agent to help create a data context layer from our warehouse, analytical conversations, and documentation. It brings together the knowledge our data team uses to interpret the data. This context spells out what our business terms mean. A person who views a site is different from someone who creates one. It also captures which sources and activity count, what reporting period to use, and how to make consistent comparisons. Now, I've got consistent metric definitions across my organization. So, when anyone asks questions of the data, they're working from the same business context and getting consistent trusted results. The data plugin brings trusted analytics, shared dashboards, and consistent business context into everyday work. Your data team's expertise can now support everyone who needs to make a decision. Now, you can put trusted data to work wherever decisions are made.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "chatgpt-data-agent",
  "signal": 0.15,
  "novelty": 0.1,
  "actionability": 0.1,
  "evidence": 0.15,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это промо-ролик OpenAI про фичу ChatGPT Work (Data Agent) — маркетинговая демонстрация продукта без переносимых технических деталей о том, как строить подобное самому.",
  "knowledge_units": []
}
```
