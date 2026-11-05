---
session: s_7c30b32e
date: 2026-09-27
words: 2036
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7c30b32e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Watch This If Your Coding Agent is Ignoring Your Rules (You Need Hooks)
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
The most underappreciated part of every single AI coding assistant is hooks. I've personally seen AI coding system for hundreds of developers and entire companies. And almost every single time, there is not enough use of hooks. They are so incredibly powerful and almost always underappreciated. And so in this video, I want to show you what hooks are, why they're so incredibly valuable, and how you can build your own so you can make your AI coding workflows more reliable by building in guarantees. This is the big word for today. And let me tell you, this is the most requested piece of content on my channel. So I'm super excited to get into this with you. Now, I'll make hooks very concrete for you throughout this video. But to give you the quick definition right now to get started, hooks are actions that you want to guarantee are performed whenever we hit certain events within our coding agent. There's a whole event menu that we'll get into as well. But for example, right before your agent is going to read a file or right when the conversation stops, fire an action that might perform an audit or block things for the sake of security, maybe log things for observability. There are so many uses of hooks and we'll get into examples for all of them. And no matter the coding agent you're using, like Codex, Claude Code, or Pi, they essentially all support this primitive of hooks. It's one of the core five components of any AI coding assistant that you build up to extend the harness and really create your own AI coding workflows. So we have rules, which we're going to talk about a lot here as well. We have our sub agents to delegate work, MCP servers to connect to our platforms, skills, which are our workflows, our reusable prompts, and then we have hooks, which are our deterministic automations. And you'll hear me say deterministic a lot in this video because deterministic is pretty much equivalent to guarantee, right? Like everything else that we have for our coding agent, like skills and rules, they're guidance for the agent. It's not a guarantee that it's going to follow the full workflow or listen to every rule every single time. That is why hooks are so powerful. It's the one thing we build into our coding agent that is actually going to ensure that something is happening the same way as it should every single time. And so if you're wondering right now, should I watch this full video? The answer is yes. If you've ever had a time with your coding agent where you just get so frustrated because no matter how specific you are about some rule within your claw.md or agents.md, the agent doesn't always follow it. And that happens all the time because large language models are probabilistic. They don't interpret your instructions or your workflows the same way every single time. And sometimes they just miss rules or they miss a step in the workflow. And that becomes so frustrating. And one really classic example that I've run into myself is typically when you have your agent perform any kind of implementation, you have rules that guide it through checking its own work and validating things after. So you have a step-by-step process like how to run your test suite for example. But agents will sometimes miss different parts of your test suite. And so they'll say they're done and that they did all the testing they needed to, but part of your test suite is still red. And so the agent didn't fully validate its work. And this is especially common for larger codebases where there's just a lot of checks that have to be performed. And so this is a really classic example where we try to fit something within our rules that really should be a hook so we can guarantee like right when the conversation is done, we'll use a stop hook to run the tests deterministically. We are guaranteeing the tests to be run. If there are any failures, we're going to force the agent to resume and fix those. And so this is a really good example that I'll dive into more in a little bit with you. But this also presents the idea here that sometimes there are things that you have in your skills or rules that actually should become hooks. And this is the framework I want to guide you through here as well to help you identify when should we be creating hooks? Because I don't want you to just understand them. I want you to know how you should really be building them into your own workflows as well. So really the big idea here is that we want to extract the larger process away from the agent as much as we can. So instead of having to put in our rules when this thing happens, then you do this, we're going to turn that into a hook so we can make sure it happens without relying on the agent to remember the right order of operations. And really what I'm telling you here is super in line with I'm sure a lot of studies you've seen come out like Anthropic reducing the size of their system prompt for Claude code by 80%. Just a lot of studies like this one here that show that too many rules for an agent can actually become detrimental. You're just splitting its focus between so many processes and conventions. Now please don't get me wrong. I'm not saying rules are bad. They're still really important. It's just it's way too easy to take rules too far. There's a lot of studies that show that. Like this study right here, super fascinating. I'll link to it in the description. It's a bit more technical, but I'll cover the high level here. They essentially built their own harness that allows their coding agent to evolve their own AI layer over time. So editing its own rules and hooks to try to perform better on the same tasks later. And then they have a separate evaluator judge like did these changes to the AI layer actually lead to better performance across different difficulties of tasks. And so this is the control right here, how well it did without any self-evolution. And then at the bottom, this is when it was allowed to make changes to its own rules 
...[middle elided]...
r good random example there. This is our classic pre-tool use like never read the .env. That should definitely be a hook. Never run a recursive force delete. That should be another security guard as a pre-tool use. Log every command you run. That should be post-tool use. When you finish implementing, run the full test suite. Again, that is our stop hook. So I'm repeating a couple of them here, but just showing you how like without really understanding everything I'm covering in this video, this might actually seem like a good fit for your rules. Like yeah, you want your tests to always be run. Yeah, you don't want it to read from the .env. But these just aren't guarantees. And the fantastic thing here is that anything you identify in your rules as more of a process, you can pretty much just copy that section or line and feed it to the hooks create skill that I have linked in the description. So {slash} hooks create, just paste it in, right? Like I took it, I pasted it in right here. Before you edit anything here, read this file. That's the file coupling example. And if I scroll down, it built it, right? It decided this is going to be a pre-tool use. It figured out the parameters. It built the hook. It wired it into the settings.json. It did everything for me just based on the rule that I gave it. It figured out the type of hook, the configuration, the script, and everything. Just please keep in mind as you're doing this process, hooks don't replace your rules. They complement each other. They're very, very important. It's just there are certain processes or events named in your rules that you can turn into hooks. So I hope that really helps you identify the kinds of guarantees you can build into your workflows and just how hooks work in general. And so if you found this video useful and you're looking forward to more things on AI coding and different parts of the AI layer, I'd really appreciate a like and a subscribe. And with that, I will see you in the next video.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "coding-agent-hooks",
  "signal": 0.6,
  "novelty": 0.4,
  "actionability": 0.7,
  "evidence": 0.35,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Видео даёт практичный фреймворк «когда правило из rules/CLAUDE.md на самом деле должно быть хуком», но доказательная база — личный опыт автора и мягкая отсылка к одному стороннему исследованию, без бенчмарков.",
  "knowledge_units": [
    {
      "claim": "Правила в CLAUDE.md/AGENTS.md и скиллы — это вероятностное руководство для агента, а не гарантия исполнения; хуки — единственный детерминированный механизм, который сработает каждый раз при заданном событии.",
      "type": "principle",
      "actionable": "Не полагаться на формулировки в CLAUDE.md для действий, критичных для безопасности или консистентности (например, «никогда не читай .env») — переносить их в pre-tool-use хук."
    },
    {
      "claim": "Признак того, что правило нужно превратить в хук: в инструкциях встречается «всегда делай X перед/после Y» или «никогда не делай Z», и агент периодически это правило пропускает.",
      "type": "tactic",
      "actionable": "Пройтись по своему CLAUDE.md/rules и выписать все формулировки вида always/never — это кандидаты на pre-tool-use, post-tool-use или stop-хуки."
    },
    {
      "claim": "Классический пример: агент считает работу завершённой, хотя часть тестового набора красная, потому что процесс валидации был описан текстом в правилах, а не гарантирован кодом.",
      "type": "workflow",
      "actionable": "Повесить stop-хук, который детерминированно прогоняет полный тестовый набор при завершении разговора и принудительно возвращает агента чинить любые красные тесты вместо того, чтобы полагаться на инструкцию «запусти тесты в конце»."
    },
    {
      "claim": "Слишком большое количество правил в системном промпте/CLAUDE.md ухудшает фокус агента (упоминается сокращение Anthropic системного промпта Claude Code на 80%), поэтому логичнее часть правил-процессов выносить в хуки, а не разрастать текстовые инструкции.",
      "type": "tool-caveat",
      "actionable": "При росте CLAUDE.md/rules не добавлять новые процессные пункты бездумно — оценивать, не стоит ли конкретный пункт вынести в хук, чтобы не раздувать текстовый контекст."
    },
    {
      "claim": "Существует скилл-конвертер («/hooks create»): достаточно скопировать формулировку правила и вставить в него — он сам определяет тип хука (pre-tool-use/post-tool-use/stop), пишет конфигурацию и скрипт, и прописывает в settings.json.",
      "type": "tool-caveat",
      "actionable": "Вместо ручного написания хука с нуля — прогонять текст существующего правила через готовый скилл-генератор хуков и проверять сгенерированный settings.json перед использованием."
    }
  ]
}
```
