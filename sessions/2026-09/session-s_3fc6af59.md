---
session: s_3fc6af59
date: 2026-09-27
words: 1916
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3fc6af59` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Death of Developer Advocates — Stephanie Jarmak, Sourcegraph
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hi everyone. Sorry for the start with technical difficulties and all of that. Uh, we made it to the end of this track. Super exciting. Thank you everybody for sticking it out this long. Um, are there any developer advocates or devrel people in the audience? Raise your hand. Yeah, okay. So did you come to like throw tomatoes at me cuz I'm talking about the dead now. Okay, so it's not going to be all doom and gloom like that. Um, a bit of like backstory in this. Um, I'm a research scientist. So last year I was an astronomer. Um, and I just sort of like wound up. I didn't know what GTM was or any of that. I just sort of wound up in this. Um, and I submitted like a bunch of boring sciency eval talks that were unceremoniously I I assumed thrown into the trash uh, for this conference. But my manager, who is a developer advocate, he put in, you know, the death the death of developer advocates, which is, you know, appropriately buzzworthy and hypey. And so so that was great. But his title is developer advocate, so it didn't really necessarily make as much sense for him to be coming up here and giving his eulogy. So we brainstormed like maybe I would dress up as like a robot and like a maul him and attack him on the stage or something like that. Um, but then it just like logistically it was going to be hard to do that. Uh, so he just went on vacation. Uh, so I'm here uh, as the agent advocate uh, to talk about this sort of like new role and uh, try to advocate for it and uh, convince all of you that we should all be agent advocates to help uh, in this new era. So uh, zooming out a little bit and going back uh, in time a bit because uh, I was trying to talk about developer advocates to somebody at the conference yesterday and their eyes like glazed over they had no idea what I was talking about. So just to sort of talk about what what this thing is that I'm saying is dead. Uh so back in the '80s, right? It was called like software evangelism where one would go forth and speak the good word of the product and bring it out there. But then fast forward to the 2010s or so, that's when developer advocacy advocacy started to become a thing where now instead of having this single trajectory of the communication pathway, now it's a feedback loop and a two-way street where you have these people with very deep empathy for developers who understand them and speak their language and could understand um what their needs were um and then bring that back to the product. And then um these developers, right? Fast forward even more, they have so much influence within their company and basically become these like kingsmakers. Uh and so the developer experience became a very important aspect of the go-to-market sort of strategy. Um but now in 2026, uh developers are no longer working alone and what it means to be a developer is completely changing. Um and so our role, right, as developer advocates um developer in developer relations, we're relating to developers. And so as the role of developers fundamentally changing, so must then does the role of the developer advocate. Um so in this slide I'm just kind of talking about the other users, right? So what's happening uh with DevRel uh outside of the agent. So most of the talk is going to be talking about the agent as a user. But I also did did want to bring up, right, that engineers they're becoming like these orchestrators of these fleets of agents, um babysitters and whatnot of these things. Um and their job, like all of the job postings and whatnot, there's language is continuously changing, right? They're um expected to have this AI fluency. Um and at the same time, there's also, you know, people like me, like uh non-engineers, right? I was a research scientist. I had like zero commits on GitHub last year, and now I have 12,000, and I'm like an open source maintainer for multi-agent orchestration framework. Like, we have so much like capability now with all of these agents, and now anybody with these agents can use dev tools, essentially. So, you have this whole other persona and ICP uh to potentially be relating to and um having empathy with when you're there using your product. So, let's talk about now this whole new user that we have in the form of an agent. Um so, an agent is somewhat unique, right? In the sense that it is both the user of your tool in a very similar way to the developer. It's going out reading your docs, but it's just reading them differently cuz it's a machine. Um you know, it's calling the API. It's encount- it's ha- has its own frustrations with how it's encountering errors and recovering from them, right? But then it's also a recommender of your tools. Um but somewhat similar, right? To developers in the way that they are also recommenders of your tools in a more organic, bottom-up way. Um so, the whole, you know, basis for DevRel, right? Is to encourage that bottom-up adoption. But now the adoption and the recommendation system, a lot of it's being driven by the agent itself. That is either, you know, maybe servicing your product directly through like ChatGPT or Claude, like directly in a Q&A sort of environment, or it's, as we had heard like in some of the previous talks where the speaker asked folks like, "How many of you have just let your agent install a library for you?" And like, there were many hands went up, right? So, there's this like recommender of tools where basically it's just installing these like frameworks and things um directly and embedding them into the workflow um and sort of working with the developer um in that taste. So, I know it's late for numbers. You don't have to read them or anything like that. Um so, I have a couple different concrete examples for measuring these seats, right? Cuz I am a data science scientist nerd person. Um so one of my first projects when I was uh working on this um uh when I became an agent advocate was to build um a benchmark called CodeScaleBench. And so I developed hundreds
...[middle elided]...
then you can also uh basically spin up like thousands of these agents to perform experiments on them and experiments that you can't really like do as easily with the developers who don't want to maybe talk to you that much. Um and then credibility, right? So you need to be earning credibility both from human developers. Um so like don't like not using Claude's slop at them, right? Then tell your AEs to stop that as well. Nobody Everybody knows what it is and nobody likes it. Um and but then credibility like actually Claude loves its own slop uh for whatever reason. So there's a bias, right, from agents of their own content. So whenever you're making like agent-facing content, as long as it's structured, you can have as many m dashes and whatever as as it wants. Um but it's just a completely different sort of uh credibility landscape, humans versus agents. So what I'm advocating for here, right, is like building out a curb cut. So curb cuts were built for wheelchairs, like built for a specific user to use them. Um but now everybody, you know, benefits from that, right? Anybody with wheels, right, strollers and um suitcases and all of those things. So my argument is that by serving the uh agents, uh the human path gets cleared, too. There's just, you know, there's just one more user in the room now, but they are still serving the human on the other end, and we're all working together on this. So, for, you know, DevRel, one quick thing that you could do like right away is point a coding agent at your docs, and then looking through that transcript and start developing your agent experience report. And then if you're more on the GTM side, start like developing some of these experiments with the GEO, putting together those prompts, and looking at the mentions versus recommendations. And I made this whole talk agent legible, right? So, there's a QR code there, as well as a couple different toy repos that have some templates for you to get started. And that's it. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "devrel-for-agents",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.35,
  "evidence": 0.25,
  "durability": 0.4,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это концептуальный докладо роли DevRel в эпоху агентов с парой конкретных тактик (тест доков агентом, GEO-метрики), но без глубины, бенчмарков или воспроизводимого метода.",
  "knowledge_units": [
    {
      "claim": "Агент — это новый тип пользователя документации и API: он читает доки иначе, чем человек, спотыкается об ошибки по-своему и одновременно выступает рекомендателем инструментов (например, сам ставит библиотеки разработчику).",
      "type": "principle",
      "actionable": "Прогнать coding-агента по собственной документации, сохранить transcript его ошибок/восстановлений и собрать из этого 'agent experience report' — отдельно от отчётов на людях."
    },
    {
      "claim": "У LLM есть заметная предвзятость к контенту, написанному в их собственном стиле ('слоп' с m-dash и т.п.) — им он читается убедительнее, хотя людям такой текст не нравится.",
      "type": "tool-caveat",
      "actionable": "Разделять два потока контента: человеческий — без AI-слопа и штампов; agent-facing (структурированные доки/референсы для машинного чтения) — там стилистические 'красные флаги' для людей не критичны."
    },
    {
      "claim": "GEO (generative engine optimization) для продукта измеряется не трафиком, а долей упоминаний и рекомендаций бренда внутри ответов LLM на релевантные промпты.",
      "type": "tactic",
      "actionable": "Составить набор промптов по своей категории продукта и регулярно замерять у нескольких LLM соотношение 'mentions vs recommendations' как метрику видимости в agent-driven adoption."
    }
  ]
}
```
