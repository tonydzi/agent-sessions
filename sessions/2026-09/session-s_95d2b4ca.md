---
session: s_95d2b4ca
date: 2026-09-28
words: 890
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_95d2b4ca` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: What Codex Unlocks for loveholidays
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
The more you can hand off a lot of the work to AI to do for you, your job elevates. Your job isn't anymore to be handed a solution and implement it. You've got something else to do that for you now. You have to get involved in the business problem. Scene 1A,  Take 1, OpenAI, loveholidays. I'm Mike Jones, I'm CTO at loveholidays. I've also looked after the contact center here for the last four years too. loveholidays is a leading online travel agent. We operate in eight different countries across Europe. We use our technology to process trillions, well, 60 trillion package combinations each day to help people find their perfect holiday. At loveholidays, our platform vision is to build the general intelligence for travel. Bringing together the great technology that we have with the people expertise, and Codex is basically the means that we're democratizing all of that work across the organization. At loveholidays, Codex is becoming a single control plane, a single interface that is shared by engineers, by data scientists and by business. It has a lot of power through that because you no longer need to teach everyone a different tool. We codify all the best practices. We codify validations. We continuously approve it each time we notice that actually we had the wrong assumptions, or the reality has changed. This means that expertise of data engineers or cloud infrastructure engineers is fully codified. So the best they know is now also available to Codex and therefore anybody self-serving their infrastructure data needs, get that expertise on tap 24-7. We want to decouple our ability to trial new ideas from actual engineering time. Our engineers developed a portal called Search Playground, which is using our design systems, it uses our front-end technologies and it has an interface to Codex. We have developed more than 10 different novel search experiences. Majority of those were developed by non-engineers. What they provide is an ability to have an idea, materialize it into a real website that's running, share the same websites with external customers, gather their feedback, or actually launch real experiments on our website. Over the last year, AI-assisted coding has gone from essentially zero to about 80% of all of our code and that's helped us actually go a lot faster than we've done previously. In that time, we've increased deploys by about 73% with the headcount remaining broadly the same. We doubled the amount of changes done to our data, yet we have half as many support requests coming in. Users of our data platform can make a lot more changes autonomously, whilst data infrastructure engineers can spend more time actually improving the platform, making it smoother again or solving novel problems that we couldn't address previously. Technology is just a means to an end. It's not about the technology itself, it's about the impact that it has, making sure that we're really intentional about not just giving people access to the tools but helping them solve business problems and measuring the impact that they're having. Everybody is a builder. Making changes to our applications, infrastructure and deploying code, is no longer engineering-only activity. We have product managers, designers and commercial business stakeholders driving value and making deployments. Amazing, nice one. Thank you so much.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-coding",
  "signal": 0.15,
  "novelty": 0.1,
  "actionability": 0.1,
  "evidence": 0.3,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это промо-кейс OpenAI про внедрение Codex в компании loveholidays — общие бизнес-фразы и красивые цифры без конкретной методологии, промптов или технических деталей, которые можно повторить.",
  "knowledge_units": [
    {
      "claim": "Компания даёт не-инженерам доступ к внутреннему порталу с фронтендом на дизайн-системе компании и интерфейсом к Codex, чтобы бизнес-пользователи сами собирали и тестировали прототипы (например, поисковые эксперименты)",
      "type": "workflow",
      "actionable": "Можно рассмотреть паттерн 'self-serve портал + LLM-агент поверх готового UI-кита' для демократизации экспериментов внутри своей компании, но в ролике нет деталей архитектуры, промптов или гардрейлов — придётся придумывать самому"
    }
  ]
}
```
