---
session: s_fd79e3d1
date: 2026-09-28
words: 2002
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_fd79e3d1` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Get Out of the Model's Way — Kevin Hou, Google DeepMind
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
All right. Hello everyone. Um, my name is Kevin. I'm going to be talking about anti-gravity. So, are there any World Cup fans out there? Woo! Imagine you are coaching Argentina and you're in the 89th minute and you have Messi on your team. What play are you running? It's called Give Messi the ball and get the heck out of the way. LLMs aren't just role players anymore. They can be your star player if you build the right product around them. And to let your star player cook, you have to get out of the model's way. We might want to get the slide. Are the slides up? Oh, they are. Great. Um, so Anti-gravity is Google's agent coding product for technical and non-technical users. Uh we launched back in November of 2025 and have been accelerating devs both within Google and externally ever since. My name is Kevin How and I lead part of the engineering team on anti-gravity. So let's talk a little bit more about what anti-gravity is. We have and always will be unapologetically agent first. So, we debuted the anti-gravity IDE last year with a brand new agent manager concept and it was a platform to manage and orchestrate many agents. Since then, we've actually extracted our agent and launched our own anti-gravity CLI. And last month at Google IO, we had the pleasure of launching anti-gravity 2.0. In the theme of getting the model out of the way, we actually decoupled the IDE from the agent manager. So, now you have two separate applications. Um, and now you can use the agent manager in a standalone app. And since pictures are worth a thousand words, here's a screenshot of anti-gravity 2.0 in action. As you can see, not only is it your own dedicated mission control for your agents and projects, you have sub agents, you have all the new models, you have work trees, scheduled tasks, voice mode. There are so many things to unpack with the product. But I don't want to spend today telling you about the product. I want to tell you a little bit more about the behind the scenes, some of the principles that went into it and notably some of the things that led to its roadmap. So, as some of you for the longtime AIG fans, uh this is actually my fifth time speaking at AIG. Um and I've been building developers tools since 2022. And the one thing that has stood above all other lessons that I've tal talked about is the idea of scaling with intelligence. This means that as the model gets better, so should your product. And the frontier edge of whatever model you are serving should be apparent inside of your users's product experience. So let's get into more concrete examples of what this means. So for those of you that follow me on X or hear me just yap generally for the last four years, you'll know that I've been working on a number of these sort of transformations year over year over year. In 2022, I was working on autocomplete and chat sidebars. This was based on embeddings, rules, files, a syntax tree parsing, basically everything inside of that app is deterministic because that's all that the model could really handle. And in 2024, when agents came onto the scene, it completely changed how developers were going to do work. With it came new primitives like MCPs, custom tools, and permission systems. And with 2025, we introduced anti-gravity's agent manager with many other products following suit in that similar form factor with users managing many agents at once in parallel. And this led to things like skills, hooks, artifacts, and a couple other primitives. Um, and that sort of defined the 2025 era. So, let's talk a little bit about 2026 and what those primitives might be. Before we answer this question, I want to take you back to some of these battle scars that are a little bit closer to home. Scaling with intelligence really is not easy. It's really hard to take away something that users love and are familiar with to lead them down potentially, and that's a big keyword, a better path. We aren't right 100% of the time, but there are two that jump to mind when I was putting together the slides for this talk. The first one is giving AI a terminal. We all remember fears about son of dev deleting your entire codebase and doing catastrophic things to both, you know, your startup, your company, etc., etc. But as models got better and people invested in primitives such as permission systems, users ended up building faster, they ended up shipping more, and they did so safely. So, we were able to overcome this. And as models got smarter, they were able to make better decisions about what they should and should not run in your terminal. The second instance is um this tweet which is very representative of sort of the yelling that I got uh when we removed chat from windsurf. So a lot of users were yelling at our team because we took away something that was very dear to them the chat sidebar and replaced it with only an agent. Now at the time this is something that was familiar and rather difficult to swallow. But when we look back, models have advanced. Multistep research, agentic research and execution became the new paradigm. And here we are today using and loving all these agentic products. And so now I bring you to today's battle. What is going on today? So we decoupled the agent manager from the IDE. And with anti-gravity 2.0, we split them into separate applications. We believe that the IDE is to the agent manager what the debugger was to the IDE. You don't always need a debugger, but it definitely is helpful to have it if you need to go a layer beneath and go one step deeper into that abstraction stack. And our prediction is that this idea of agent orchestration, you can call it agent teams, you can call it swarms, you could call it software factories, is the future. And we're willing to bet on that future. So here are the primitives for what we're calling the agent teams 2026 era. These are things like sub aents, generative UI, and sidecars. And we'll talk more concretely about what those things are and some ex
...[middle elided]...
ct a little bit further than just a markdown file or just a conversation. And generative UI in many ways reminds me of the quote that the late Steve Jobs said when unveiling the iPhone. He justifies the removal of the keyboard and says they all have these keyboards. They are there whether you need them or not. And they all have these control buttons that are fixed in plastic and are the same for every application. In an analogous way, we built our product to dynamically scale with the needs of the agent. We skipped the heavy infrastructure and mechanical UIs in favor of sidecars and generative UI. And that creates a product experience that is not fixed in plastic. So, sub aents, sidecar triggers, and generative UI are the latest primitives that are powering anti-gravity. We've tried our best to stay out of the way and let the model cook. And if you're building a product around an agent, you should consider what are the primitives that are in my product and how might they scale with the model's intelligence. We all are familiar with shipping features is now quite easy with all of these new tools. And it's about deciding what features to actually add um so that the model so that your product can scale with the next release of the next model which will inevitably be faster, better, and cheaper. And so with the right primitives, you as a builder or you as a product owner, you might be surprised at what the models can do. And in classic fashion, I'm going to keep using the slide until we've actually conquered the TPU crunch. So you can find me on Twitter. Uh you can DM me for feedback. We're always looking for new ideas on how to build the latest and greatest. Thank you for watching. Thank you Swix and Ben for having me. It's always a joy to be here. And I'll be at the anti-gravity booth if you want to talk further. If you want to get to know the product a bit more, some team members will be there. So, thank you so much for your time. Excited to meet you all. Yeah. Heat.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agent-product-ux-design",
  "signal": 0.35,
  "novelty": 0.35,
  "actionability": 0.3,
  "evidence": 0.25,
  "durability": 0.35,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад в основном промо продукта Google Antigravity, но содержит переносимый фрейм «масштабируй продукт вместе с интеллектом модели» и пару конкретных исторических примеров смелых UX-решений в агентных продуктах.",
  "knowledge_units": [
    {
      "claim": "Примитивы agent-продукта должны эволюционировать вслед за ростом возможностей модели: 2022 — детерминированные автокомплиты на эмбеддингах/синтаксисе, 2024 — агенты с MCP/tools/permission-системами, 2025 — менеджеры множества параллельных агентов, 2026 — суб-агенты, generative UI, sidecars.",
      "type": "principle",
      "actionable": "При проектировании продукта вокруг LLM закладывать архитектуру так, чтобы UI/примитивы можно было заменять по мере роста модели, а не жёстко фиксировать интерфейс под текущий уровень возможностей."
    },
    {
      "claim": "Разрешение агенту напрямую выполнять команды в терминале изначально пугало (риск удаления кода/данных), но с появлением permission-систем и более умных моделей это дало пользователям более быструю и безопасную разработку.",
      "type": "tactic",
      "actionable": "Не блокировать агенту доступ к терминалу/файловой системе полностью — вместо этого строить гранулярные permission-системы, которые ограничивают опасные действия, а не убирают автономию целиком."
    },
    {
      "claim": "Удаление привычного чат-сайдбара в пользу полностью агентного интерфейса вызвало недовольство пользователей на старте, но по мере роста способности моделей к многошаговому агентному ресёрчу и выполнению задач это стало новой нормой и повысило продуктивность.",
      "type": "tactic",
      "actionable": "Не бояться убирать знакомые, но устаревающие UI-паттерны (чат как основной интерфейс), если модель уже способна закрывать задачу автономно end-to-end — но готовиться к сопротивлению пользователей на переходном этапе."
    },
    {
      "claim": "IDE относится к agent-менеджеру так же, как дебаггер относится к IDE — не всегда нужен, но полезен как слой для более глубокого контроля, поэтому Antigravity разделил IDE и agent manager на два отдельных приложения.",
      "type": "principle",
      "actionable": "Проектируя agent-платформу, явно отделять слой 'оркестрации агентов верхнего уровня' от слоя 'глубокого ручного контроля/дебага', чтобы пользователь мог работать преимущественно в первом и опускаться во второй только при необходимости."
    }
  ]
}
```
