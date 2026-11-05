---
session: s_31297b68
date: 2026-10-01
words: 2042
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_31297b68` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The State of AI in Software Development: Data from 400+ Orgs — Justin Reock, DX
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Uh I'm Justin Rio. I'm the deputy CTO at DX. I get to do a lot of our research around uh developer experience and its relation to developer productivity. And certainly over the last year, a lot of that research has focused on AI's impact on the developer experience and basic aspects of productivity uh within an organization. Uh so we produce these quarterly reports, our our state of AI and AI impact reports which looks at really a lot of raw data that we're able to get from our platform. Our platform is a researchback platform uh built from the same folks who worked on Dora metrics and the space framework and the DevX framework. Uh and really at the end of the day it's a data gathering platform that can look at a lot of different trends across an organization with you know how are we focusing on developer experience are we seeing outcomes and improvements with developer experience and certainly are we seeing outcomes with the way that we're using AI in our workflows. This session is going to be a little bit different than the 345 session I think that's up in the leadership room later today which just looks at the raw data from our newest report. It's a little bit of a preview. This is looking at more like organizational trends and how our workflow is changing and and things like that based on the data that we're seeing. Uh so first things first, let's kind of look at what we're seeing in terms of the velocity impact. Now if anybody's familiar with looking at various velocity metrics like PR throughput and deployment frequency like hopefully you understand the caveat that these metrics are not perfect. They are proxy metrics for understanding the way that work flows through an organization. They're not fully representative of the value generation. We're going to look at some metrics that are closer to that as well. But let's just try to understand what this technology is doing in terms of just the raw velocity metrics in the organization. So here's our Dora metric for deployment frequency. Who's familiar with Dora metrics? All right, most of you. Great. Um, so this is one of the, you know, four key metrics that tries to understand directionally, you know, the speed of shipping work within an environment. And we're seeing it steadily increase. um it's tapering off a little bit. I think there's reasons for that. Uh some of the surge that we saw early on was due to people shipping, you know, PRs more frequently and and things like that. Um so we're seeing increases in this. This is one small part of the SDLC PDLC, right? This is like the creation uh of the PR to actually trying to deploy this into production. It doesn't tell us about revert rates. It doesn't tell us about defect ratios. It doesn't tell us about change failure rate. It just tells us about how much stuff are we now kind of pushing out into production. But you know the data is showing us that this number is steadily increasing. Okay. Um the trends vary a little bit across regions. Um we are seeing North America just sort of like trending up. We've seen Europe actually pull back a little bit just in the last quarter. Um I think you know there's there's a number of reasons for that. I mean obviously the way work is done in these regions are differently. the way that we can spend money on this technology and think about token spend is different, the regulation is different. Um, but if we just look at the through line in general, you know, we still see improvements uh in in this one metric of deploy frequency even across various regions. We do just see some variance in those regions. [clears throat] Here's one that's kind of interesting though. Uh, the perceived rate of delivery. How much faster do engineers feel in terms of what they're delivering? It's gone up a little bit. This number shows an increase of about four and a halfish percent. Um, but given that that's a full year and given all the investment and cost and new spend on AI, it's interesting that this perceived rate has not stayed has not kind of crept up a little bit more. especially when you look at some studies like obviously infamous flawed MER study if you're familiar with that study uh back in February they actually released a follow-up to that study saying that some of the signals they gathered were sort of imperfect and they needed to rethink some of that but what was interesting was that in these 16 engineers that were part of that study small study flawed study uh the productivity went down by about 19% but the perception went up by about 20% so there was like a 40% spread in perception of productivity versus actual ual productivity. But here when we look at this on more of an aggregate things interestingly stay uh sort of flat. All right. What about impact on quality and and delivery? Right? So those are just kind of our speed our velocity metrics. But what is this actually doing to our software quality? Um the first metric we'll look at here is the Dora change failure rate metric. And uh let me prepare you. Most of you are sitting down. It's very volatile the impact that we've seen on quality over this period of time. Each line on this graph represents a single company that was part of this particular part of this study. And that line shows whether you've moved up in terms of your change failure rate or moved down in terms of your change failure rate. You want to go down. You want to be on the bottom side of this graph. Uh but what's interesting is if you look at some of these top lines, you see people increasing as much as 2%. Which doesn't sound like much until you realize that the industry benchmark is about 4%. So that means shipping potentially 50% more defects than we were shipping before. So you really just want to understand what side of this graph you're on. You want to start measuring this stuff, right? Um this pattern exists without AI, by the way. This has a lot to do, it's not purely causal with AI. A lot of this has to do with like your release
...[middle elided]...
fast. Our industry benchmark for that is over a month usually. But my favorite part about this story is that they're seeing about a 15% additional value creation per engineer. So they are hiring more than they have in the history of their entire company because they realize the truth here that they're getting more capacity per single engineer. They're getting a better return on investment per single engineer and hiring more engineers will improve their competitive edge. This is the right attitude. This is a throughput story. This is an increased innovative capacity story. This is not a headcount replacement story. Fair. uh they're automating about 3,000 of their code reviews a week triggered off of a pull request and um they look at superficial stuff. They still need humans in the loop, but the initial superficial uh uh review that comes from the agent is all part of the system of record. It stays in the PR comments and so the next engineer to actually perform the review will have an idea of what the agents already looked at. So it can save some time. Finally, Spotify, if anybody remembers the Spotify model from DevOps, they were sort of the northstar for DevOps. uh they built an agent for S SRRES that will gather remediation steps from runbooks and information and context about the incident and put all that together into SR communication channels so that when an incident occurs the S sur has uh immediate context and doesn't have to go through multiple minutes of discovery uh to figure out how to solve the issue. So, if you want to dive deeper into this data, our Q2 report is coming out in just a few weeks. Uh, but the Q1 report still has a lot of tidbits from this session in it. And if you subscribe to our newsletter or you come back to the website, by midish end of July, we'll have our Q2 report. And if you want to see a preview of that report, that's the talk that I'm giving later this afternoon. Thanks everybody for your time. I appreciate it. >> [music] [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "ai-dev-productivity-metrics",
  "signal": 0.55,
  "novelty": 0.5,
  "actionability": 0.45,
  "evidence": 0.75,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад на реальных агрегированных данных 400+ организаций показывает конкретные метрики эффекта AI (DORA, change failure rate, расхождение восприятия и реальной продуктивности) и пару применимых паттернов (агент код-ревью, агент для SRE), но большая часть — макро-аналитика для лидеров, а не тактики для рядового инженера.",
  "knowledge_units": [
    {
      "claim": "Воспринимаемая разработчиками скорость доставки растёт намного медленнее, чем инвестиции в AI, и есть задокументированный разрыв между ощущением продуктивности и фактической (в одном исследовании реальная продуктивность упала на 19%, а восприятие выросло на 20%).",
      "type": "benchmark",
      "actionable": "Не доверять самоотчётам разработчиков об ускорении от AI-инструментов — мерить фактические метрики (deployment frequency, PR throughput, change failure rate) параллельно с опросами."
    },
    {
      "claim": "У части организаций после внедрения AI-кодогенерации change failure rate вырос до 2 п.п. при индустриальном бенчмарке около 4%, то есть прирост дефектов может достигать 50% относительно базового уровня.",
      "type": "benchmark",
      "actionable": "При роллауте AI-ассистентов кодирования отдельно трекать change failure rate (не только скорость доставки) и сравнивать со своим бенчмарком до внедрения."
    },
    {
      "claim": "Некоторые компании автоматизировали первичное код-ревью агентом (например, ~3000 PR в неделю), который оставляет поверхностные комментарии прямо в PR, а финальное решение остаётся за человеком.",
      "type": "workflow",
      "actionable": "Встроить агента для первого прохода код-ревью, который публикует комментарии в PR как часть истории — это даёт человеческому ревьюеру стартовый контекст, не заменяя его."
    },
    {
      "claim": "Agent для SRE собирает шаги ремедиации из runbook'ов и контекст инцидента и выкладывает их прямо в канал связи инцидента, сокращая время на первичную диагностику.",
      "type": "workflow",
      "actionable": "Построить агента, который при открытии инцидента автоматически подтягивает релевантные runbook'и и контекст в чат инцидента, чтобы дежурный не тратил минуты на поиск информации."
    },
    {
      "claim": "Организация с ростом ценности на инженера на ~15% от AI решила нанимать больше инженеров, а не сокращать штат, расценивая эффект как рост пропускной способности, а не замену людей.",
      "type": "principle",
      "actionable": "При росте выработки на инженера от AI рассматривать это как аргумент в пользу расширения команды для конкурентного преимущества, а не как повод для сокращений."
    }
  ]
}
```
