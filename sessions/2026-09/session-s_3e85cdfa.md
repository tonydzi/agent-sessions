---
session: s_3e85cdfa
date: 2026-09-28
words: 2004
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3e85cdfa` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How Software Factories Improve Themselves — Suraj Gupta, Warp
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Um my name is Siraj Gupta. I lead Harness development at Warp. Um in case you haven't heard of Warp before, um we started off by building a state-of-the-art agentic development environment. Um we have about a million active users that use that. Um it was born out of a modern-day terminal. Um and nowadays we're building a um cloud agent platform to enable teams to build software factories. Um today I'm going to talk about um self-improving software factories, which I know might sound kind of buzzy, um but I'm going to break it down and hopefully you can walk out of here with something concrete that you can implement yourselves. Um you've probably heard of both of these terms, self-improvement and software factories, used throughout this conference, but I'm sure you've heard of them independently. Um you've heard about how self-improvement is about agents being able to um improve over time and agents and models um and, you know, phasing out humans from that loop, so that way the the improvement loop can be automatic. Um and I'm sure you've heard about software factories being um the way that like the software development paradigm is shifting from individual coding agents to building out automations that take work from triage up until production. Um but less has been said about how software factories themselves can self-improve over time, so that the the factory can get better, more efficient, faster. Um and I think this is going to become an extremely important part of our jobs as software engineers as we transition from building products to building factories and and maintaining them. Um so let's dive in. Um self-improvement is a pretty broad umbrella, but I'm going to focus on three concrete ways that agents can improve over time, agent factories can improve over time. I'm going to start with um skills, then we'll talk about persistent memory, and then I'll finish off by talking about model routing. Um so skills are a great way to give your agents procedural memory. I don't think I have to kind of spell that out for you. You describe a a procedure to your agent that you expect it to have to do a task over and over. Um for example, let's say you're building a triage agent, which is a pretty common thing you might build in a software factory. Um and you give it a skill on how you want it to go about reproducing issues. Um those skills get stale over time. Um humans give feedback to the agents. Agents learn things in their own um runs and trajectories. Um and the like the skill that you previously gave it becomes dated. So, how do we fix this and let the agent improve over time using that skill? Well, one way to do it is to deploy an outer loop agent. Um and this is what we've done in our own internal software factory that's been really productive. The idea is that your um your inner loop agent is the thing that's actually applying the skill. It's like doing the triage. And then you have this other outer loop agent that is observing your inner loop agent's runs and improving its skill over time by looking for um for mistakes it made or looking at feedback that the human has given it. Um so, I'm going to show an example of that. Um let me swap here. Cool. Um so, this is actually a skill that we've used internally at Warp. We've open-sourced our client repository and it's fully run as as a factory. And so, this is an example of an of a of a skill that's that's backing a triage agent that we have today. The idea is that um you you get an issue that comes in on GitHub, and you want to automatically run an agent to figure out like what sorts of um like it what sort of information did the user not provide that is going to help us figure out if this is something that we should build, an existing issue that we might actually just want to dedupe against or something else. Um and then we have a Sorry, let me just switch over here. And then we have a workflow that actually like runs that that triage um agent. Um this is a pretty simple workflow. It just Every time an an an issue gets submitted on the repo, this um this workflow runs. And then here's the actual outer loop agent, which is about looking at the the work that the triage agent has done and improving it over time. So, the idea is that the agent looks at the decisions that the triage the inner loop triage agent made, and it um collects feedback signals, which might be uh you know, thumbs up or thumbs down on the issues. Um it might be users commenting on the issue. It might be someone from Warp um an employee of Warp commenting on the issue, uh giving the agent feedback on what it did. Um and then ultimately that leads to like some synthesis of of the of that um iteration. And so, we we end up basically updating our inner loop skill with this outer loop agents. Um and that's what leads to this self-improvement loop with skills. What's really nice about this is that um the So, in step four, you'll see we we added the triage skill, and then we open a pull request. So, that means that um all of the improvements to the inner loop skill are going to be tracked through get. So, you get like full observability into like how that skill is transformed over time. And that it also means that um a human is actually going to review those updates to the skill. So, that way, you know, this this outer loop agent doesn't make a mistake and ultimately cause your triage agent to to actually perform worse. Um yeah, so that's that's kind of what what I want to talk about for skills. Um let me talk about persistent memory now. So, I'm going to go back to my deck. Um cool. So, skills are great for remembering procedures, but what about everything else? So, like what what happens when your Sentry agent um looks for an issue and and finds an issue, does some work to like gather context about it, and fixes it, but then now you have you encounter a similar issue in the future. Your century your agent might get lucky and like be able to figure out the same root cause th
...[middle elided]...
 want database migrations done with with GLM fire with GLM or I want um you know, uh runbooks and API documentation done with Quen. Um So, this really allows you to like like to define classes of tasks and be able to say, "Okay, I want this this class of task done by this model because that's kind of what you've seen." At this point though, that's kind of more of an art than a science um and so uh what we're working on next is being able to define evals for um customer-facing evals where you can actually define what sorts of things you care about and what knobs you want to turn on these configurations and actually see, "Okay, is is Haiku better than fi- than GLM than Opus in a specific class of issues?" That's like specific to your workflows and not just some like generic benchmark that um that someone posted online. Um let me go back here. Give me a sec. Cool. Cool. Um and yeah, so let me uh I'm in my slideshow. So, here is kind of like a a high-level overview of how this works in Warp today. So, um internally we have our model routing rules, um but then we have like an eval sidecar that's determining um what sorts of tasks are actually better with which models. And we do this with a simple like best-at-k um approach where when you type a prompt, we run a bunch of agents in Oz uh across a different set of models. Um and we found success in like being able to determine, "Oh, like UI tasks are really well done with GLM. Um we don't really need to run those with Opus. It's much more efficient to run those with GLM." Um so, that's how we've been using it, but um sooner enough we're going to be building this into our product so that way our our customers can actually use it in their own workflows. Um Yeah, that's uh that's mostly what I had today. Um we're around in a booth around that side. So, if you're interested in this kind of stuff, come talk to me. I'm always down to talk about this kind of stuff. But yeah, thanks for your time today. That's all I had. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "self-improving-agent-factories",
  "signal": 0.6,
  "novelty": 0.55,
  "actionability": 0.6,
  "evidence": 0.45,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Спикер из Warp описывает конкретный паттерн 'внешний агент правит скилл внутреннего агента через PR' и practice роутинга моделей по классам задач, но без цифр/бенчмарков — только внутренний опыт компании.",
  "knowledge_units": [
    {
      "claim": "Для самоулучшения агентных скиллов используют 'outer loop' агента: он наблюдает за прогонами 'inner loop' агента (например, триаж GitHub-issue), собирает сигналы обратной связи (реакции, комментарии людей) и сам обновляет skill-файл, открывая pull request на это изменение.",
      "type": "workflow",
      "actionable": "Можно построить аналогичную пару агентов: рабочий агент выполняет повторяющуюся задачу по инструкции-skill, а второй агент периодически анализирует его трейсы и фидбек и предлагает правки в skill через PR, а не напрямую в проде."
    },
    {
      "claim": "Обновления skill-файлов проводят через git PR специально ради двух вещей: полной трассируемости изменений процедуры агента во времени и обязательного ревью человеком перед тем, как изменение уйдёт в прод-агента.",
      "type": "principle",
      "actionable": "При автоматическом самообновлении промптов/скиллов агентов заводить это как обычный git-коммит с PR и ревью, чтобы деградация поведения агента не проскочила незамеченной."
    },
    {
      "claim": "Роутинг моделей под конкретные классы задач (например, UI-задачи — на GLM, миграции БД — на другую модель) в Warp определяют эмпирически через 'best-at-k': на один и тот же промпт параллельно запускают несколько моделей и сравнивают результат, а не полагаются на общие бенчмарки из интернета.",
      "type": "tactic",
      "actionable": "Для роутинга моделей внутри своего пайплайна собрать eval-сайдкар: прогонять один и тот же класс задач через набор моделей параллельно и мерджить/выбирать по фактическому качеству на СВОИХ задачах, а не по паблик-бенчмаркам."
    }
  ]
}
```
