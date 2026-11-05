---
session: s_5f912b67
date: 2026-10-22
words: 910
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5f912b67` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Put your dot on call
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Hey, I'm Ali. I'm an engineer here at OpenAI, and I'm excited to show you how I've been using dots in my engineering workflows. We built dots to be a persistent cloud agent that has its own cloud computer, but also has access to your local computer and has its own identity across all these different services that you already work, such as Slack. To show you what that unlocks, I want to go into my Codex app here, and if I go ahead and click on my dot, I can connect it to Slack. And when I go and add it to Slack here, this actually gives an identity for my dot in Slack, so I can tag it in any sort of thread to get it to pick up work that I don't want to do or anything that I can get it to pick up. And now that it's connected, I can actually come into the composer and I can do something really cool. So, I'll show you the workflow that I set up for my on-call shift. I'm going to say, monitor the channel, and any incoming page I get, please triage the page and create a thread to investigate. So, I've sent this automation now, and I can tell you about how I actually use this to triage an on-call incident that I had at 3 a.m. So, the first thing that happened is I received a page on my phone, so I grabbed my phone, I acknowledged the page, and the next thing I did is I went into the ChatGPT app to see what my dot was working on. And you can see that when I went into the ChatGPT app, my dot's already done the investigation, figured out what's going wrong, and it's also created a Codex thread for me that I can actually click into and start to steer the thread and send messages to for me to continue the investigation. And these are all messages that are being sent to my laptop as well. So, it's running this Codex thread on my laptop, and it's helped me to figure out what's going on, but also made it so that at 3 a.m. I don't need to go out of bed and grab my laptop and start to investigate this incident, because it's already done the investigation for me. And in this particular case, I can resolve it even from my phone as well, but say there's an issue that requires more investigation, I can put down my phone and I just come to my laptop and I see that same Codex thread in my laptop as well. So, this is one small thing you can do with your dot, but there's a lot of cool uses you can set up by just sending a simple prompt to set up an automation that, for example, triages all the incoming feedback you get in one specific channel, or you can tag your dot on Slack to create PRs for you and iterate with it directly on Slack. And there's many more use cases, and I'm really excited for you to try it out.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "persistent-cloud-agent-oncall", "signal": 0.15, "novelty": 0.15, "actionability": 0.2, "evidence": 0.25, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это промо-демо продукта OpenAI (dots, постоянный облачный агент) с одним сценарием дежурства: триage страниц в Slack и тред Codex, без технических деталей, ограничений и измерений.", "knowledge_units": [{"claim": "Сценарий on-call: агент мониторит канал с пейджами, сам делает первичный триаж и заводит тред расследования, так что к моменту пробуждения инженера диагностика уже готова.", "type": "workflow", "actionable": "Если строите собственного агента для дежурств, подключите его к каналу алертов с задачей «триажить каждую страницу и открывать тред расследования», чтобы человек получал готовый контекст, а не сырой алерт."}, {"claim": "Агенту полезно давать собственную идентичность в рабочих сервисах (например, отдельный аккаунт в Slack), чтобы его можно было тегать в тредах и поручать ему задачи, включая создание PR.", "type": "principle", "actionable": "Заводите агенту отдельную учётную запись с минимально нужными правами вместо работы от вашего имени, это упрощает делегирование и аудит."}]}
