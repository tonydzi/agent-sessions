---
session: s_705f4b1e
date: 2026-09-28
words: 2079
turns: 2
tools: "ReportFindings"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_705f4b1e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Orchestras, Not Factories: How the Fastest Builders Work — Charlie Holtz, Conductor
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hello. I was at a wedding this weekend and it was in New York and there were a bunch of trendy people there and uh I I told I was talking to someone who I'd never met before and uh I told him I was prepping for this presentation and he was like, "Oh, that's cool. Like, what what's the conference about?" And I said it was about AI engineering. And I could just see his eyes glaze over and he started like looking behind me to find the next person to talk to. And I'm it's like so cool to actually be in a room full of people who actually want to hear about this stuff. So, I I I I'm very excited to be here. Um I am the co-founder of Conductor. Um has anyone here used Conductor? Okay, nice. Nice. Okay, cool. So, uh uh for those who don't know, uh Conductor is a desktop app for managing a team of coding agents all at the same time. So, instead of having a bunch of terminal windows for your Cloud Codes, your Code Accesses, or your uh whatever uh coding agent, you have one interface to manage them all. And one of the really cool things about building Conductor has been that I've seen a lot of the best builders up close. I've like watched their workflow, I've seen how they work, I've seen the things they do do and the things that they avoid doing. And so, I thought I would compile a bunch of the principles um that I've seen the best engineers use um and give them to you all. Um so, here's what Conductor looks like. Uh can you can you guys see this? Okay, nice. Okay. So, here's what Conductor looks like. Um and here are my principles for being the fastest builder in your organization. So, let's start with number one, stay near the frontier. Staying near the frontier means you are always trying the latest things, basically the day they come out. Uh it means that when uh uh ultra code comes out, you're trying it. It means that when uh uh slash go comes out, you're giving it a go. Um it's really important to stay near the frontier um for a few reasons. Um if you are doing your own startup, then staying near the frontier means that you will um come up with lots of new ideas for what you should actually be building. Um and this literally happened to us. We were building a totally different app called Chorus. Um but we started using We were such power users of cloud code back in February of last year that we uh started building our whole workflow around cloud code, and we started cloning our repo five times, and then we discovered work trees, and then bit by bit we had built conductor as an internal tool. And we couldn't have figured that out if we uh weren't staying near the frontier. And if you're not doing a startup, you should be the person at your company who always knows what the latest uh the latest workflows are. Um it used to be that you could just kind of like use your social graph and the information that was important about the best workflows to use would trickle down to you. But things just like move way too fast now. You're You're always going to be three to six months behind if you do that. Um so, it's a very important to stay near the frontier. And there's an important word here, near. Um there is a danger if you are at the frontier, um you can you can do what uh I call mid-whip miming, where you're spending all of your time working on your workflow and not doing actual work. And so, internally we've come up uh with a heuristic for this. Um we call it don't beat the market. Don't try and beat the market. Um uh the concept here, like the heuristic you should use when you're you're to decide if you're near the frontier or at the frontier and uh too deep in into the latest trends is you should ask yourself why isn't this workflow the default? So for example when Ralph loops were becoming a big thing you should ask yourself like should I spend a ton of time optimizing my workflow to work with Ralph loops because if Ralph loops work for everyone like if they are the default then you probably should just wait for Anthropic or Open AI or ever to build the workflow into the into the default harness. You can think of this is sort of like an efficient market hypothesis where unless you have like real alpha you shouldn't be optimizing your workflow too much. And what I mean by real alpha is like some kind of information about either your users or your code base that the models might not know about. So an example for us is we it's we're we're a chat app. We have to render really long chats really quickly and performance is is important to us and so we need to spend a lot of time optimizing our react queries to render the chats quickly and we're willing to make sacrifices in other parts of our code base to make that happen. Um So if you have some kind of alpha like some kind of information about the app you're building that the models might not know about then you should put time into the workflow. Otherwise don't don't midwit meme. Don't don't be the person who has an amazing Emacs setup but like doesn't actually get stuff done. Okay three. Create slop free zones. So at Conductor we have this term we call a slop free zone. And a slop free zone is a part of the code base or a part of the app that requires really strict human review. And we're actually I think a little bit unusual in this way. I think a lot of people assume that we are uh pure token maxers and we are like ripping through like 30,000 line PRs, but we're actually not. Um we're actually quite careful with certain parts of our codebase, and then very loose with other parts of our codebase. Um the reason this is important is because if you are not careful about your slot free zones, your your code your codebase can get in a really tricky spot. Um and this actually happened to us. We have We've had to rewrite our whole app like a couple of times because we weren't careful about slot free zones. Um specifically, we have a uh migrations file. And uh in our CI uh any change to migrations file requires the AI uh a human to review it. U
...[middle elided]...
 But I don't want the future to be built around factories. I want the future to I want to feel like a human. I want to like be in the flow. I want to be like in front of an orchestra like waving my baton and we're and like I wave it this way and this this team of agents starts working and then this intermingling of humans and agents starts working as I go here. And I can when I want to I can zoom in on the details, but most of the time I can zoom out. And I don't think the future should be we are like managing swarms of agents and we are like factory line managers like pushing buttons getting the agents to like pump out the next feature. Like we can we can we tried this like 10 years ago with the term feature feature factories and it just doesn't work. Like I want my software to feel human and crafted. I want to feel like a human at the center of it all. And I think because we're all building these tools we actually have a responsibility to make the tools great for humans. I think it's really important to like use the words that make us feel excited and like feel feel capable and feel like we're in the flow and having fun. And so I don't think the future is is is something like this. I don't want to be I don't want to be in in my dark factory. I don't want to be a line manager. I want to feel like this. I want to be in the flow. I want to be having fun. I want to be crafting things. I want to feel like I'm Steve Jobs designing the Mac with a team of amazing humans and AI agents all in the same place. Like I want to feel like I'm in an orchestra. So here are my principles for for being the best builder in your organization. Stay near the frontier. Don't try and beat the market. Create slop free zones. Feed the beast. Free range agents and think about orchestras not factories. Came up with this handy acronym for for remembering it. Stickfo. All right. So thanks thanks a ton for for having me. I'll be around. Feel free to ask questions and I'll see you on the internet.

---

> `ReportFindings` -- {"findings": []}

---

**Claude:**

Пропустил не тот инструмент — эта задача не про код-ревью, а про классификацию видео, нужен просто JSON-ответ текстом.

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding-workflow",
  "signal": 0.45,
  "novelty": 0.35,
  "actionability": 0.4,
  "evidence": 0.3,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад сооснователя Conductor даёт несколько личных эвристик организации работы с кодинг-агентами (near-frontier, слоп-фри зоны), но это скорее набор мнений и лёгкая реклама продукта, чем проверенная бенчмарками методика.",
  "knowledge_units": [
    {
      "claim": "Эвристика «не пытайся обогнать рынок»: прежде чем вкладывать время в кастомный воркфлоу под новый агентный приём (например, Ralph loops), спроси себя — почему это ещё не стало дефолтом в самом харнессе (Claude Code / Codex и т.п.)",
      "type": "principle",
      "actionable": "Оптимизировать свой воркфлоу под новый хайповый приём стоит только если у тебя есть реальная 'альфа' — специфичное знание о своих пользователях или кодовой базе, которого нет у модели; иначе подожди, пока индустрия встроит это в дефолт"
    },
    {
      "claim": "«Slop-free zones» — практика явно выделять части кодовой базы (например, файлы миграций БД), которые требуют строгого ревью человеком, в отличие от остального кода, где допускается более вольная работа ИИ-агентов",
      "type": "tactic",
      "actionable": "В CI настроить обязательное человеческое ревью для критичных путей (миграции, биллинг, авторизация), а остальной код можно отдавать агентам с менее строгим контролем — это снижает риск переписывать всё приложение с нуля из-за накопленного 'слопа'"
    },
    {
      "claim": "«Оставаться рядом с фронтиром, а не в нём» — постоянно пробовать новые релизы инструментов (в день выхода), но не тратить всё время на тюнинг воркфлоу вместо реальной работы («мидвит-майнинг»)",
      "type": "principle",
      "actionable": "Выдели ограниченный бюджет времени на эксперименты с новыми инструментами/фичами агентов, но основной фокус держи на продукте, а не на бесконечной оптимизации личного сетапа"
    }
  ]
}
```
