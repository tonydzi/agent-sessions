---
session: s_26c95fa1
date: 2026-10-01
words: 2059
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_26c95fa1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: His AI Bot Closed $10,000 in Sponsorships | Alex Finn
CHANNEL: Greg Kamradt (lang=en)
TRANSCRIPT SAMPLE:
I think the best way to do it [music] is kind of start small, think of like the three to four main areas [music] of your life that you want AI to help automate and improve. Make like one bot for each. >> [music] >> Uh I don't really have a plan. I'm just going to go through everything I do, and I think there'll be some interesting things in there, and so I hope it's helpful. Um this is my Grok bot. Uh I have a whole team here on the left. What I did was I I broke it down, my team, into basically all the areas of my life, content, my software I build, uh the community I have, uh because I found something really interesting with Grok bot that I think is very unique to it. Um compared to any other AI agent there, which is I find that your different bots kind of naturally interact with and engage with each other based on their like roles and titles and context. And what I mean by that, I'll show an example here. So, this is my team over on the left-hand side here for one of the apps I'm building, Henry Intelligent Machines, and I kind of have different roles here, uh the chief officer of the app, a developer, a researcher. And what I actually kind of naturally found happens with Grok bot is they'll look at the titles of other bots. That's why I I don't recommend like naming your bots like email specialist, content specialist. Like give them like names, and then make their titles what they are. Like you can see their title next to their name there. What I find kind of naturally happens between your bots is they actually can see what each other's titles are and interact with each other organically based on their roles. So, example here, I'm in Kelly right now, who kind of leads everything to do with this app I'm building. And Kelly, I I never told Kelly to do this. I never told AI bots how to interact with each other, how to message each other, anything like that. But Kelly, as you can see here, organically just messages Hank, who's the developer for this app, and Build, who's the CTO for everything I do. Build's the only one that has an unoriginal name for their name, but it says CTO next to it. Didn't tell them interact with each other. Didn't tell them to work with each other. They just organically, as they work, I don't think I've messaged any of them for like days now. It's literally been like a week since I messaged Kelly. She just autonomously works and just chit-chats with like Hank. Hank will organically go to Kelly and be like, "Hey Kelly, is it all right if I do this? I need permission for this. Are you all right if I do this?" And Kelly be like, "Okay, yeah, you can do that." Or if Kelly needs to get like even more permission, she'll talk to Build, who's the CTO of everything. And so this really interesting, natural, organic relationship starts to form in between the bots based on their roles, who they are. And so everything I do in Grok Bot is like in an effort to build the synergy between all of my bots, right? And so, you know, they'll She'll go to Build. Build's the CTO. I don't even look what the chats are like. Goes to the CTO, says, "Hey, we have to work on this ticket. We have to work on this ticket. Should I do this? This is blocked. Can you help me out here?" And I never said, "Hey, go to Build, the CTO, if you need help there." She just kind of naturally does it. So I've started like doing things to build that synergy between all of the bots. One of those things is I've taken all my executives, so every team, content, community, Henry, the tech team, the product research team, they all have an executive, a leader. I actually don't use chief of staff at all. I'm like bearish chief of staffs. I'm more like I like the modular teams with the leader of each team. And I put them all in a channel and every morning they have a stand-up, all the executives between the teams. So, every morning they have to go and talk about what are their top four priorities that day, where they're like blocked, and then they give each other feedback based on what their priorities are. And one thing that's key here is you want to make sure every team I hope I'm not showing anything private. I did not review any of these chats, so I'm Don't read the chats if there's anything. I think I'm safe. There's no IP addresses. Okay, we're good. Um One key here though is like if you just have AIs just kind of looping talking to each other with no goal, it's just all slop. But if you make sure each team has a set of goals they're measuring against both long-term and short-term and put that in their memory, the executives, and then you throw them in these stand-ups, they'll actually work towards those goals. Right? The AI, it's slop if they don't have goals, but if you give each team goals, they naturally work towards those goals. So, they'll do the stand-up every morning at 8:45. They'll talk about uh what their current short-term goal is this week, what's their progress, what's blocking them, and what they plan on doing today to get a step closer to that goal. And then the other executives will jump in and say, "Hey, you know, Kelly here from him, uh here's what I'd recommend based on the context I have." Or, you know, "Frederick here from the content team, this is what I would do based on what I've seen work here." Or, "Dusty from the community team, this And they kind of naturally help each other based on the context in different parts of my business move towards that short short and long-term goal. And like what makes this unique and why I never really done this with other bots and why, you know, I'm really in love with Grock bot is there's some sort of magic going on behind the scenes where they're all very good at figuring out who's who, what their roles and responsibilities are, what like context they have, and like what they're in charge of, and then reaching out to each other at the right time, right? Based on, okay, I'm going to do this really risky thing, so I'm going to go to the CTO who has all t
...[middle elided]...
unity officer. I have a online community. I want to reduce churn. I say hey I want you to reduce churn from X to Y over the next month. And every day during the stand up it comes up with a new way to address churn. It'll go in and like like look at the data in my community cuz it has its own account in there. It'll come up with new strategies. Oh it'll say I'm going to send a message to everyone who hasn't engaged in the last week and then it DMs each user individually. Uh for uh my app I'm building Henry. I want to launch beta in 3 weeks. It'll go and be like okay, I need this this this done by beta. Okay, which of these can I tackle today so that we can get closer to beta launch by then. So those are the type of goals I put in. >> All right, last question. >> Last question. >> Someone all the way in the back corner. >> All right, uh I think you mentioned uh Tailscale. So >> Yes. >> I was wondering if uh there are use cases to chain agents together or agent proxy. So for example, like coding agents take a lot of tokens, but I have like other models that I use. So is it possible for a communicator to just like talk to someone other agent which does the heavy lifting? >> I've seen I I've seen people do that um where they like go into their Grok's virtual computer and like log into other coding apps out there and be like, "Hey, every time you code, use this now." In an In an effort to like save tokens. I'm not in love with that. I think it's just like really easy for things to convoluted and broken and weird doing it that way. If I have like a heavy coding task and I know my cursor credits are getting a little low that day, I'll just go directly and message another agent. Tailscale for me is purely so that all my networks, all my agents are networked together so I can go to one bot and say, "Hey, go on this desktop computer and load up this model. Go on this Go on my DGX Spark and load up this model." I can just quickly move around and manage my entire network itself.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "multi-agent-personas",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.35,
  "evidence": 0.15,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Это личный анекдотичный рассказ пользователя Grok-ботов о ролевой структуре агентов и ежедневных стендапах, без логов, бенчмарков или воспроизводимых деталей — скорее вайб-отчёт, чем проверенная методика.",
  "knowledge_units": [
    {
      "claim": "Если называть агентов реальными именами и явно прописывать им роль/должность (а не ярлык типа 'email specialist'), другие агенты в мультиагентной системе Grok лучше распознают роли друг друга и сами начинают обращаться по адресу за разрешениями и помощью.",
      "type": "tactic",
      "actionable": "При построении команды агентов давать каждому имя + явный титул роли в системном промпте/профиле, а не функциональный ярлык."
    },
    {
      "claim": "Без явных целей (краткосрочных и долгосрочных) в памяти команды агентов их взаимное общение превращается в бесполезный 'слоп'; цели заставляют агентов реально двигаться к результату.",
      "type": "principle",
      "actionable": "Перед тем как давать агентам свободу общаться друг с другом, прописать каждой команде конкретную измеримую цель (неделя/месяц) и класть её в постоянную память агента-лидера."
    },
    {
      "claim": "Ежедневный 'стендап' между агентами-руководителями команд (приоритеты дня, блокеры, взаимная обратная связь) помогает держать автономные агентные команды согласованными без ручного вмешательства человека.",
      "type": "workflow",
      "actionable": "Завести регулярный (например, утренний) групповой чат/канал только для агентов-лидеров команд с фиксированным форматом: топ-приоритеты, блокеры, обратная связь."
    },
    {
      "claim": "Докладчик сознательно не использует паттерн 'агент-прокси, который делегирует тяжёлую работу другому coding-агенту ради экономии токенов', считая его хрупким и запутанным; вместо этого при нехватке лимитов он вручную переключается на другого агента напрямую.",
      "type": "tool-caveat",
      "actionable": "Не строить автоматическую цепочку 'агент А вызывает агента Б через его интерфейс' для экономии токенов — риск нестабильности выше выигрыша; лучше ручной переключатель или прямой вызов нужной модели."
    }
  ]
}
```
