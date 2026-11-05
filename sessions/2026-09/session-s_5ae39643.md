---
session: s_5ae39643
date: 2026-09-22
words: 2123
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_5ae39643` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Dark Arts of Skill Engineering — Paul Bakaus, Renaissance Geek (Impeccable)
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hello everybody. How's it going? Okay, I think we still have some people trickling in, but I'm super excited to be here. Okay, first off, let me reload these slides because my claw code was still building something on it. Um, okay. So, the contrast is a little bit low. Um, so please bear with me. I'm going to try to cover uh what you cannot read as much as possible. Uh, I also have heard that the Wi-Fi is not the strongest. So um while it is a workshop uh hopefully you just do take away a lot of the lessons um and then can apply it whenever you want to. Um but I do have a sample repo if you want to follow along. Um okay first of all hi my name is Paul. Um I'm really glad you found your way into this room. Um I'm the author of Impeccable. Who here has used Impeccable by any chance? Can I see some hands? Okay, a few people. Nice. Um, so for those of you who have not used Impeccable, Impeccable is a skill that I've built for myself mainly. Um, I've built this large enterprise app uh over the last year and it has like lots of different views, states, whatever. Um, and I wanted to design really quickly with my agents with codecs with claw. But I noticed that uh even though it gets me quickly to something that I can look at, normalizing it back to the design system was really really challenging. So the first skill that I've built for myself was called normalize and it kind of like brought it brought whatever claw designed back to the design system. That's how I started and I also used Anthropics funed design skill like maybe many of you um when I first got going and from there on it kind of expanded into more and more design skills that allowed me to turn clawed code and then codecs and other harnesses more into a design harness. Um at some point I decided maybe other people might find uh um might find this useful as well. So I open sourced it as open source skill uh released it and it turns out a lot of you liked it. Um so if you haven't checked it out yet um uh yeah give it a go. Uh it's on impeccable.style. Um but today won't be a talk about impeccable per se. It will be about what I learned from making these skills because it kind of escalated. It started with like a simple prompt and then uh went all the way to what it is today. Um, a lot of people have looked at the code of Impeccable and they see like a whole bunch of scripts in the scripts folder and they're like, "What is all this stuff?" And so, um, I wanted to share some of my knowledge that I've gained with you. So, let's get into it. Uh, let's talk about the dark arts of skill engineering. [panting] Okay. Um yeah, the production value of this talk is out of this roof. Um okay, so first of all, you've all seen this kind of design. Um this is actually a real design uh built with uh the front end design skill uh and clawed code. Um and you probably all have seen a design like this. This is for like a fake kids reader, iPad reader app. Um you have italic serif. Uh you have like some capitalized uh hero. Um, and you have like a eyebrow text, like a kicker, whatever you want to call it. The top of it, like a weird label. Um, you have beige, I call it claw beige, claw beige, uh, backgrounds. Um, and now it's not necessarily a bad design, right? But I think you all can point this out and say like, well, this is clearly AI generated. It's clearly slop. Um, and it turns out slop is a moving target. Um you've all seen you might have thinking might have been thinking of slop as purple gradients but uh we've kind of moved on since that uh into cloud beige. Um okay so this is where I started. I started with a system prompt and a prayer basically. Um, so I I started using the front end design skill uh like many of you and it's like 55 lines of named bands. Uh, no scripts, no routing, pure pros, right? Uh, and you just hope for the best. Um, that sometimes worked and sometime and most of the time it didn't. So, um, for example, I'm just going to read some of this. So, um, if I mean maybe it's really readable, I don't know. Um but for example in the font and design skill you have sentences like never use generic AI aesthetics overused fonts like inter robboto arial system fonts um or cliched color schemes particularly purple gradients and white backgrounds uh never converge on common choices like space grotesque for example um now there are two problems with this approach the first one it over applies and then a ban just relocates the model to the next cluster and I'll show you why this is a problem a a little bit further down the road. But really, you tell it not to use in, it just uses the next best font it finds in its latent space. And so it doesn't actually make it more creative. It just, again, this is why I said slop is a moving target. It kind of picks the next best thing. Um, I have uh learned my lesson here um the hard way because uh I don't know if you noticed, but the reason why we got purple gradients in the first place is because of Tailwind. Taywin's default sample pages theme whatever was purple. Um well it turns out I've turned the web orange before many years before that. I created a framework called jQuery UI and the first default theme of jQuery UI was orange. So overnight I call it the web orange. I thought people would modify the theme but now they didn't. Um so I learned my lesson. Um okay the median is the model's gravity. Even 250 lines of like artisal, crafted, beautiful skill pros cannot change this. It's just not enough. It doesn't help enough, right? It's nowhere near enough. Um, and I learned this the hard way and hopefully you don't have to. Um, my overall thesis for this talk is that prompting is sort of like the starter level, but harness engineering is where you should end up. Like you should reframe when you're building skills. You should think about okay skills the same way as MCP is an extension to the coding harness or whatever harness you're in. Uh it's not just a prompt that you package it's something more t
...[middle elided]...
ging them and distributing them? Yeah. It's a good good topic. Um so of course like the harnesses and the and the frontier labs have their own ways. I mean um Codex has a marketplace that you can use for distribution plug-in marketplace. Um uh Claude Code has a marketplace as well. I think they started with the marketplace technique. Those marketplaces don't work particularly well. I mean the Claude code one for sure doesn't work particularly well. I know this for a fact because I mean the update me mechanism often doesn't work and people are like well my skill doesn't update and oftentimes there's a caching issue. So it my experience has been hit or miss with the native methods of distributing and then of course it only for that particular provider. That's why projects like uh skills.sh exist. But again, the problem with MPX skills right now, it does it it does it it doesn't allow for like, you know, more advanced skill use cases like, you know, compiled for every different harness. I have a pull request um in the in the repository. Um and I've uh I've bugged Andrew a couple times about it, but um he uh he still has to get it merged or agree to agree with me on that, I guess. Um I think uh we're still discussing. Um but yeah, MPX skills I think is a great project in general. I think it'd be great if we could sort of like standardize around it. Um there's also one from Microsoft trying to do that. Um a project from Microsoft. I forgot the name of it. Um but there's definitely no no industry standard for distribution yet. Um yeah, I'm not I don't love having to maintain my own CLI installer. I would rather not. Uh it's annoying. Um but uh it does make it so it plays safe with all harnesses installed, the hooks in the right part of the system, etc. So it's um Yeah. Yeah. Okay. I think I'm way out of time, but come up and speak with me if you like. Yeah, I would say I'll end it here, but yeah, come come up if you like. Um let me just uh Thank you. [applause] >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "skill-engineering",
  "signal": 0.65,
  "novelty": 0.55,
  "actionability": 0.55,
  "evidence": 0.6,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Автор популярного open-source скилла Impeccable делится реальным опытом перехода от промпт-инженерии к «harness engineering» для дизайн-скиллов в Claude Code/Codex, включая нетривиальное наблюдение про запреты в промптах и честную критику маркетплейсов скиллов.",
  "knowledge_units": [
    {
      "claim": "Запрет чего-либо в системном промпте (например, «никогда не используй фиолетовые градиенты») не делает модель креативнее — она просто сдвигается к следующему ближайшему кластеру в латентном пространстве, а не к реально новому решению.",
      "type": "tool-caveat",
      "actionable": "Вместо накопления запретов в промпте skill'а закладывайте детерминированные механизмы (скрипты, рандомизацию, роутинг вариантов), которые физически исключают нежелательный кластер, а не просто просят модель его избегать."
    },
    {
      "claim": "Даже очень длинный и тщательно написанный промпт-скилл (сотни строк прозы) недостаточен, чтобы преодолеть тягу модели к «медианному» (наиболее вероятному) ответу — промптинг сам по себе имеет потолок.",
      "type": "principle",
      "actionable": "Если скилл не даёт нужного разнообразия/качества после доработки текста, не увеличивайте объём инструкций — переходите на скрипты, валидаторы и внешние ограничения выполнения (harness engineering)."
    },
    {
      "claim": "Skill стоит проектировать как расширение харнесса (по аналогии с MCP), а не как упакованный промпт — то есть с логикой, скриптами и состоянием, а не только текстовыми инструкциями.",
      "type": "principle",
      "actionable": "При построении собственных skill'ов для Claude Code/Codex закладывайте папку scripts/ с исполняемой логикой (валидация, нормализация вывода под дизайн-систему и т.п.), а не ограничивайтесь markdown-инструкцией."
    },
    {
      "claim": "Встроенные маркетплейсы скиллов (у Claude Code, у Codex) на практике работают ненадёжно — механизм обновления часто не срабатывает, встречаются проблемы кэширования.",
      "type": "tool-caveat",
      "actionable": "Не полагайтесь на авто-обновление скилла через нативный маркетплейс без проверки; закладывайте свою версию/дату в артефакт и ручную сверку при подозрении на устаревшую копию."
    },
    {
      "claim": "Единого индустриального стандарта дистрибуции скиллов между разными харнессами пока не существует (попытки — npx skills/skills.sh, отдельный проект от Microsoft), поэтому автору Impeccable пришлось поддерживать собственный CLI-инсталлятор.",
      "type": "tool-caveat",
      "actionable": "Если планируете публично распространять skill для нескольких агентов (Claude, Codex и др.), закладывайте свой лёгкий инсталлятор/скрипт установки, а не рассчитывайте на единый универсальный канал доставки."
    }
  ]
}
```
