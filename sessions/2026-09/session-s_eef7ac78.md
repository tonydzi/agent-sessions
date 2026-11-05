---
session: s_eef7ac78
date: 2026-09-30
words: 1806
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_eef7ac78` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Building the partner ecosystem with Sophos
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
I'm delighted to be joined by by JP and if Matt mentioned the post afternoon post lunch slump I   think of all people JP probably has the excuse to maybe have a little bit of a slump uh having   traveled from the east coast at the start of the week to the west coast to arriving in London last   night. Yes. Uh so please go easy on them. Um with that JP would be great to introduce yourself to   the audience um and to tell us a little bit about Sophos please. Hey everybody it's great to be with   you here today. I'm John Peterson. I'm chief technology officer at Sophos. And Sophos, for   those of you that may not know us we are one of the largest cyber security companies in the world. We have about 650,000 customers that are spread across the you know with a global footprint and   they really span every segment every sector and as such we see a huge variety of different attacks   and we've cultivated you know vast expertise in combating them over four decades of being in the   cyber security business. So it's great to be with you here today. Thanks JP. Yeah great to have you. Sophos is a Daybreak partner and we're speaking a lot today about the narrowing defenders window. What does the defenders window mean for Sophos um and how you protect your customers? Yeah,   that's great. So, the we think of the defenders window in terms of the the pace of acceleration   in frontier intelligence. So, the leading frontier models are developing more and more sophisticated   cyber capabilities. those are working their way down into the openweight models as well   and that's driving you know a faster exploitation paths more vulnerabilities we're seeing that in   the CVEes as well um just the level of CVS has gone up massively in the last few years   and so we think about it in terms of we have an opportunity to take advantage of the frontier   um frontier intelligence through programs like Daybreak that allow us to stay a step ahead   of the attackers um and we we look at that in terms of protecting ourselves at Sophos   because as a large cyber security company, we're obviously a target, but we also have 650,000   customers who and it is our obligation to protect them. So, we have an opportunity, I think, with   programs like Daybreak to stay a step ahead of the attacker community. And I guess that protection   takes a combination of technology and expertise. So how do OpenAI, Sophos, and the customer each   contribute to making this essentially work for the entire ecosystem? Yeah, that's that's a good   question. I think the way that I think about that is Sophos is Sophos contain we have lots of cyber   security domain experts, right? We've been in the cyber security business a long time and we've,   you know, it's our business to protect our customers and that that domain expertise takes   a variety of forms. So threat intelligence um you know response playbooks when we're managing   incidents on behalf of customers um and also just the expertise of our people. So I look   at it as Sophos brings the domain expertise and the knowhow to actually combat attacks at scale   but then the programs like Daybreak and companies like OpenAI bring frontier intelligence that allow   us to take that domain expertise and then scale it to support all of our customers. And that's what's   been so powerful about the program and what it's allowed us to build. It's been fantastic to see   that partnership go from from strength to strength in recent months. Absolutely.I guess we're joined   by some of the leading uh security leaders across EMEA here today. Maybe let's give them a little   bit more of a a practical example here. um can you walk us through an example of how a Daybreak   powered agent helps your team investigate a threat? Yep, absolutely. So, I think the the place   that I would start in explaining that is by just explaining the Sophos Fusion system, which is the   system that powers the managed detection response service at Sophos and all of our EDR and XDR   products. So these systems are built um leveraging sensor data from over 500 different integrations   with third-party security products but also our own products as well. Those sensors are   producing like trillions of events every day. And those events get distilled down really into   a small set of about a thousand to 2,000 cases a day that are you know nine different security   operations centers are investigating on behalf of customers. And so that process of taking a case,   conducting the investigation and then remediating whatever the threat is. Historically that was   driven primarily by human expertise. And you know in the before time right that human expertise and   the processes that we built around it allowed us to have around a 38 minute average response time   for or average investigation time on those cases which is you know at the time like 18 months ago   that was better than 96% of professional security operations centers. But now because of the agents   that we've been able to build leveraging the Daybreak program, the average response time for   cases that are leveraging the agents that we've built has reduced to about 89 seconds. So that's   about half of the cases that we handle are now being automated by agents that we've developed   using the Daybreak models. And that's obviously that's been transformative in terms of the effort   that it takes for us to actually conduct those investigations, but it also results in better   customer outcomes. And to to provide a little more detail about how that actually works in practice,   we have these cases that come into the security operations team. And the cases themselves are   now handled primarily by a investigation agent that we've developed that takes all   of the information from the case. Customer context detections, indicators of compromise, um you know,   knowledge of the um the the threat landscape. And it feeds that into a planning model which   then creates a kind of plan exec
...[middle elided]...
t than it's ever than it really has ever been. Um, and that means   of course like having patching programs to deal with the um the vulnerabilities and the CVEes that   are being released by by many different vendors and by the open source community, but also making   sure that you have good fundamentals in place across your infrastructure. So solid endpoint   protection like having having above having the best endpoint protection is more important than   it's ever been. Additionally, having, you know, basic things like MFA in place across all of your   identity infrastructure, having strong network segmentation in place, and then having a strong   security operations program that wraps all of that is more important than it's ever been. And Sophos,   we obviously we play in all those different places. And um you know,   we're we would be happy to to talk to anybody that's interested in learning more. So really,   you're not saying to throw out the fundamentals here and forget all those basics. I am not saying   that. No. Okay. Yeah. And it's not it's not controversial what I'm saying, I don't think,   but I think we get distracted by the um the pace that the technology is moving. Um you know,   and of course we want to we want to do everything that we can to leverage agents to help help   security operations teams deal with the increased workload, but also like fundamentals fundamentals   like endpoint protection are just more important today than they ever have been. Yeah. Thanks a   million JP. It's been it's been great chatting and I'm sure there's many people in the audience who'd   love to to pick your brain this afternoon. So JP is around. Um he will be here for the remainder   of the afternoon and available if you want to buy him a drink at our open bar shortly. Um but yeah,   thanks a million for your time JP. Um I'm going to be uh leaving stage shortly, but uh next   up I'm delighted to introduce Tom Duff Gordon who's OpenAI's policy VP for EMEA. Thank you.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-soc-automation",
  "signal": 0.25,
  "novelty": 0.15,
  "actionability": 0.15,
  "evidence": 0.35,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это промо-панель OpenAI с партнёром Sophos про программу Daybreak — есть одна яркая метрика (38 мин → 89 сек на кейс), но архитектура агента раскрыта только буzzword-ами без деталей реализации, остальное — общие места про MFA и патчинг.",
  "knowledge_units": [
    {
      "claim": "Sophos построил SOC-пайплайн из investigation-агента и planning-модели, который берёт кейс (детекции, IOC, контекст клиента) и генерирует план расследования; это сократило среднее время расследования с 38 минут до 89 секунд и автоматизировало около половины кейсов.",
      "type": "benchmark",
      "actionable": "Если строите агента для триажа/расследований (security ops, support, DevOps-инциденты), рассмотрите паттерн 'planner-модель формирует план → отдельный агент исполняет' вместо монолитного промпта — это даёт измеримое ускорение на потоковых кейсах с повторяющейся структурой."
    },
    {
      "claim": "Спикер подчёркивает, что рост возможностей атакующих через frontier-модели не отменяет базовую гигиену — патчинг, MFA, сегментацию сети и endpoint-защиту, — а требует их усиления параллельно с агентной автоматизацией.",
      "type": "principle",
      "actionable": "При внедрении LLM-агентов в защитные или операционные процессы не убирайте базовые контролы (доступы, патчи, сегментацию) — автоматизация ускоряет реакцию, но не заменяет фундамент безопасности."
    }
  ]
}
```
