---
session: s_7f782738
date: 2026-10-20
words: 1965
turns: 2
tools: "ReportFindings"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7f782738` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How to Know When an AI Agent Can Work Unsupervised — Evan Kormos, Coinbase
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hi everyone. My name is Evan Cormos. I've been delivering, designing, building software for 20 years. The last 15 in enterprise financial services. I am a player coach at Coinbase. And we're here today to talk about trusting agents in policy-driven workflows. So, let's start with the policy and it's pretty boring. Um, I'm going to go over here for my notes. So, our starting point center centers around the policy and this sets the rules for how work gets done within the organization and including especially risk and compliance. Think of policy as the original institutional intent or the original system prompt. So, ideally we have this written down. Um, it's a little bit boring, so stick with me. Um, using language like must, may, and should. And the again, these help define the rules and decisions about how the system operates in the organization. Separate from policy, we have the actual running system. So, the first thing we're going to do is separate these two uh these two both the build state and the run state in two different moments in time. So, typically we're either defining or chaining changing our policy but this the system is constantly running and it's constantly moving and changing. So, we could then sort of imagine a compilation event that Oops, sorry. I'm skipping ahead there. It's constantly changing. So, it's evolving quickly with these product-driven changes. So, everything is expected to still be roughly bound by the policy, but ultimately um we separate this from the run state and the build state. So, inside the system, what does it look like? We have a familiar model if we have any enterprise uh folks in the in the room here. Um people, process, and technology. But, where really do agents fit into this model? Um so, I see them as an operational model cutting across all three. They work with people, execute parts of the process themselves, and they use and are made up of technology. So, for our talk today, we're going to be focusing here where agents meet process. What work we give them, what boundaries we set, and how we build trust in their outputs. So, let's dive into your workflow. And it's high-level and seems basic, but if you haven't, there are good reasons to map this out. So, maybe a change has to be approved before it goes live, or a customer goes through has to go through verification before their account is opened. We expect work to flow in a specific and gated direction. So, I believe it makes it agents make it worth revisiting what we can do in parallel. So, previously some work used to cost too much or be too complex to coordinate in this way. But now we can run independent reviews alongside each other, bring the results together, but keep the required checks in place. So this is a directed acyclic graph or a DAG. It is a way to represent this workflow or process, the steps, the dependencies for a flow that moves forward without looping back on itself. Apache Airflow, if you're familiar, is an example of open source software that represents workflows, their dependencies as DAGs in Python code. So this Python code, this these DAGs can be used to define and manage a number of policy driven processes like, for example, commercial lending. We could also use a DAG to represent the workflow to list a token on the exchange in a specific region, if you're into that. Or we could use a DAG to represent a regulated flow of delivering software, which is a hot topic. And one we'll spend a little bit of time on, I think that we've seen a lot of adoption within agents, within software delivery, and ultimately we're looking to leverage that same efficiency and scale in other areas of the business and close that the the adoption gap. So let's stick with the software delivery example for a little bit. What happens inside one of these nodes of the process? And I'll give you a hint, it's a loop. >> I'm oversimplified, but we have a basic version of what's happening within the Let's Let's say this is a code review process, right? So, we're going to essentially do a number of steps and essentially once we realize the work we recognize that the work is good enough, we're going to allow it to pass on to the next step. And that's essentially the function of the code review node. The work doesn't always uh end up okay. So, sometimes we have to take the feedback from the code review and iterate on it um until the work is a good enough to pass. So, this is a representation of a directed cyclic graph or DCG. So, as far as open source software, uh something like LangChain LangGraph would be what I would um say is helpful to manage the state of DCGs. Um and this is an oversimpli- an oversimplification. These graphs can be very complex. So, zooming back out, the inner flow um of the node, we have people and agents working together. On the outer flow, we have a policy boundary. But not everything goes to plan. Um so, we have to handle exception flows. We don't want the work to get stuff stuck, and we don't want to design for every edge case, either. Um the exception flows will monitor and see kind of what happens if you're shipping code that gets canceled or doesn't meet security standards, that's something you would should want to know about. Volume shifts across the flow once we start to add agents into the mix and we've seen this with software delivery and we'll see it in other processes as we bring agents into those processes as well where now all of a sudden if you're reviewing code faster you need to design it quicker or you need to do the security scan that's faster. So we see the volume shift across the flow. And this is where it's really important that we have visibility into the process overall from a a metric standpoint because as we start to supercharge and and parallelize and add more efficiency to the process we start to develop more and more bottlenecks and so the operational visibility of the process is extremely important much more important than the authoring and the bu
...[middle elided]...
l climb? All right, how do we turn this on? So, day one, um we start supervised and as we have agents and humans working together as a part of the process, we can um manually um verify the output to ensure that it is high high quality. Um this is where we refine our data sets and ensure that we have the right confidence mechanisms in place. We've defined what good looks like with the domain subject matter experts and that they're beginning to verify it. When measured confidence reaches a policy threshold, we can move towards sampling. And what that means is humans are looking at a slice of the output and not necessarily all of it. Um we begin systematic more systematic evaluation through traces Um in order to ensure that what we're what the humans aren't seeing is still meeting the quality bar. And then finally, once we clear the confidence threshold, humans handle more of the exceptions of the process, but still acting as participants in refining the data sets and ensuring the quality outputs. Okay, so a few takeaways from this. Um DAG and DCG, basic graph theory, but ultimately, how do we build these processes that exist today and where people are working them and bring agents into the mix. And the recipe really is to keep it deterministic on the outside and make it adaptive on the inside. The next is quality through evaluation. And this is really establishing a complementary confidence mechanism. So, it's not a feeling about a model. We can actually provide research and statistics about the quality of our agents. So, this builds confidence and inherently trusts output. Quality is a team sport. AI engineers own the pipeline to taking product signals from all directions and deliver applications that are well built and utilize ML operations behind the scenes. Finally, agents accelerate across the operating model. I've included some references on the final slide of things that I've spoken about today. This concludes my presentation. Thank you very much. >> [applause]

---

> `ReportFindings` -- {"findings": []}

---

**Claude:**

{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agent-autonomy-governance",
  "signal": 0.55,
  "novelty": 0.35,
  "actionability": 0.5,
  "evidence": 0.35,
  "durability": 0.75,
  "volatility": "stable",
  "half_life_days": 1095,
  "why": "Доклад даёт концептуальную рамку (политика → DAG снаружи, цикл внутри узла, поэтапная выдача автономии по порогу уверенности), но без конкретных метрик, бенчмарков и демо, поэтому ценность умеренная.",
  "knowledge_units": [
    {
      "claim": "Политику организации стоит рассматривать как исходный «системный промпт» и разделять состояние сборки (смена политики) и состояние выполнения (постоянно работающая система).",
      "type": "principle",
      "actionable": "Записать правила процесса письменно в формате must/may/should и привязать к ним проверки агента, а не полагаться на неявные ожидания."
    },
    {
      "claim": "Рецепт построения процессов с агентами: детерминированный внешний контур (DAG с обязательными гейтами) и адаптивный внутренний (цикл «работа → ревью → доработка» внутри узла).",
      "type": "workflow",
      "actionable": "Описать процесс как DAG (например, в Airflow), а внутри узла ревью реализовать цикл с обратной связью (например, в LangGraph); обязательные проверки оставить на внешнем контуре."
    },
    {
      "claim": "Агенты позволяют запускать независимые ревью параллельно и сводить результаты, сохраняя обязательные проверки, что раньше было слишком дорого координировать.",
      "type": "tactic",
      "actionable": "Пересмотреть последовательные шаги согласования и вынести независимые проверки (безопасность, качество кода, соответствие политике) в параллельные ветки DAG."
    },
    {
      "claim": "При ускорении одного этапа нагрузка смещается на соседние, возникают новые узкие места, поэтому наблюдаемость процесса важнее, чем сам авторинг агентов.",
      "type": "principle",
      "actionable": "Добавить метрики по каждому узлу процесса (пропускная способность, очередь, доля исключений) и отдельный поток обработки исключений, не пытаясь предусмотреть все краевые случаи."
    },
    {
      "claim": "Автономность выдаётся поэтапно: сначала полная ручная проверка, при достижении порога уверенности по политике — выборочная проверка со статистической оценкой по трейсам, затем люди разбирают только исключения.",
      "type": "workflow",
      "actionable": "Определить с экспертами предметной области, что значит «хорошо», собрать оценочные наборы данных, задать числовой порог уверенности и по нему переключать режим: полная проверка → выборка → только исключения."
    }
  ]
}
