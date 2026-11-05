---
session: s_a1749fc4
date: 2026-10-22
words: 809
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a1749fc4` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Put ChatGPT to work on shared team tasks
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Every team has routine work, like reviewing requests, pulling together weekly updates, and staying organized. And often, one person ends up running it all. With team tasks in ChatGPT, you can set up that recurring work and maintain it together. Tasks run in the cloud, and your teammates can review the results and improve the instructions as your needs change. Let's say you're on a legal team. Every morning, there's another batch of requests. What needs a review? What's missing? And who's picking it up? You can now create a team in ChatGPT for the people that you work with regularly. I'll open Settings, create our legal team, and add my teammates. Add everyone once, and you can share pages with that whole group. You can share custom plugins and team tasks too. Let's use a team task to take a first pass at this inbox. A team task is a recurring job we can review and improve together. And it runs in the cloud, so it doesn't depend on my laptop. To set up our first team task, the shared inbox is already connected, so the task can access the requests. I'll link to our intake guide in the task instructions, so Chat has our rules for routing them. I'll save this as Daily Legal Intake. Now the team has one task all of us can come back to. Okay, let's see what it found. This NDA is missing the other company's name. This contract is due Thursday. And it also suggested who should pick up each request with a link back to the message. Let's open the original message. Yep, Thursday. I'd want their deadline right at the top. This is useful, but requests with upcoming deadlines should be easier to spot. Because we're sharing the task, my teammate can update its instructions too. Here, they're asking it to put requests due within two business days at the top. There we go. In the next run, the upcoming deadline is right at the top. Now we've set up a recurring review and checked its work, and we improved the instructions together. The team now has a task we can keep using and refining as our needs change. And if I'm away, someone else can pick it up. Try it with one job your team does every week. I'd love to see what you make easier.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "chatgpt-team-tasks", "signal": 0.15, "novelty": 0.1, "actionability": 0.2, "evidence": 0.15, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это продуктовая демонстрация новой функции ChatGPT от самого OpenAI (командные задачи в облаке) на примере юридического инбокса, без технических деталей и без переносимых практик для инженера.", "knowledge_units": [{"claim": "Повторяющуюся командную рутину удобнее держать как общую облачную задачу, которую коллеги могут ревьюить и править через инструкции, а не как личный скрипт одного человека.", "type": "principle", "actionable": "Выбрать одну еженедельную рутину команды, вынести её в общую задачу с версионируемыми инструкциями и назначить совладельцев, чтобы не было единственной точки отказа."}, {"claim": "Качество повторяющегося агентного прогона улучшается итерациями: проверить результат первого прогона и поправить текст инструкции (например, приоритизация по дедлайну), после чего эффект виден в следующем запуске.", "type": "workflow", "actionable": "После первого запуска агентной рутины сверить выдачу с исходными данными и вносить правки в инструкцию, а не в ручной постобработке."}, {"claim": "Привязка инструкции задачи к внутреннему руководству (intake guide) даёт агенту правила маршрутизации без их дублирования в промпте.", "type": "tactic", "actionable": "Ссылаться в инструкции агента на живой документ с правилами, чтобы обновление правил автоматически влияло на поведение."}]}
