---
session: s_d6648d87
date: 2026-09-20
words: 799
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d6648d87` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Hidden Flaw of EVERY Coding Agent Now Has a Solution
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
I've spent a lot of time this year helping companies roll out AI coding agents. And when the results aren't the best, at least at first, it's really not the model's fault. It's that everything that they use to check the output is made to check for code that is wrong. Code that is syntactically broken or unsafe. The kind of thing you can pattern match against like SQL injection, cross-site scripting, path traversal. And these issues and vulnerabilities are important, but they're not the only risk. Most of what goes wrong with agent-written code isn't strictly bad code. Exactly like the examples that I have on screen right here, it's code that runs as the agent intended, but it's just not what we or the business needed. Usually what the agent gets wrong is access control, business logic, the rules that the product runs on. Now, the thing is a business rule doesn't really have a shape. Unfortunately, nothing in the syntax can really tell you whether code that violates a rule looks any different from code that doesn't. For things like, for example, access control with specific functionality. The only way to tell is knowing what the business rule was supposed to be in the first place. Okay, cool. I understand that this is a problem, but now what in the world is the solution? Well, Sonar has built a new agent called Hunter Agent. You're looking at the UI for it right here. And for this class of problem, it works out everything for you. And what I love about Hunter Agent is they don't just have their agent rummage around your repo trying to find these different problems or perform more of a traditional code review. They have a process for this. They run playbooks. It figures out what your app is supposed to enforce, then it hunts for any instances where it doesn't, and then it proves each one before it ever surfaces anything to you. And if you run it on the same code twice, you're going to get the same answer twice. The kind of reliability that we don't usually have with apps built on top of LLMs. Broken access control, business logic, authentication and sessions, it all shows up as regular issues in SonarQube Cloud. There's nothing new to learn, and this is generally available now for the Cloud Enterprise plan. I have loved working with the Sonar team this year and even helping other companies incorporate all their products in the SonarQube cloud. So, thanks to them for working with me on this and I'll link to Hunter Agent in the description.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-code-review",
  "signal": 0.2,
  "novelty": 0.15,
  "actionability": 0.15,
  "evidence": 0.15,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Это спонсорский ролик про конкретный коммерческий продукт Sonar (Hunter Agent) без деталей реализации, бенчмарков или воспроизводимой методики — только маркетинговый питч с общей и довольно очевидной идеей о бизнес-логике.",
  "knowledge_units": [
    {
      "claim": "Традиционные SAST-проверки и линтеры ловят синтаксически некорректный или явно небезопасный код (SQL-инъекции, XSS, path traversal), но не ловят нарушения бизнес-логики и access control, потому что у бизнес-правила нет «формы», которую можно паттерн-матчить.",
      "type": "principle",
      "actionable": "При ревью кода агентов не полагайся только на статический анализ безопасности — отдельно проверяй соответствие бизнес-правилам (кто к чему имеет доступ, какие условия должны выполняться), желательно явно сформулировав эти правила заранее."
    }
  ]
}
```
