---
session: s_d1787687
date: 2026-09-28
words: 1992
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d1787687` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: AI-Generated Code Is Already Competing With Human Code — Daksh Gupta, Greptile
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
How's everyone doing? Awesome. Uh, my name is Du. I'm one of the co-founders of a company called Gravile. And at Grapile, we're working on AI agents that validate poll requests with full context of the codebase. The way Graval does this is every time there's a pull request, we have a swarm of agents and they go and look at every file that's changed, every file that's related to the files that changed to figure out if there's bugs. And it also spins up your code in a sandbox, installs the dependencies, spins up local host, clicks around to try to break things, mocks inputs, and everything else to figure out if the code is broken. But I'm going to talk about something a little bit different, which is fully autonomous coding agents. So I first moved to San Francisco three years ago to work on AI coding. And this is because GBT 3.5 which came out in 2022 was the first model that seemed like it was really good at programming at the time. Code complete tab complete was like the main paradigm for coding. The most exciting thing that was happening was you had tab complete from cursor and you had co-pilots code complete and that was like the way in which AI coding works. In 2024, for the first time, multifile editing started to work. Cursor was the first to do this and then a couple of other products followed. But now, for the first time, AI could simultaneously edit multiple files at once. But things got really interesting in 2025 because for the first time, we had autonomous agents. They could be given a task and they could go and fulfill the task and create entire pull requests all at once. And this came to a precipice in December of last year when coding agents became literally completely autonomous. And anyone that's working in AI coding knows that December when the new models came out was sort of this like watershed moment in the history of AI coding because these products for the first time were like truly autonomous in how they programmed. And all over Twitter were all these crazy stories of people that were having these agents spin off and open a 100 pull requests a day. They were experimenting with polyphasic sleep so they could stay awake to re-trigger their agents from time to time. And as someone that started programming before agents, I was very skeptical that real companies could program this way. So I was really really curious, are these fully vi PRs really actually good? Is this something that's sort of a Twitter hype and you can have independent developers and and maybe like small startups with no real customers do this? But anyone with real customers with an actually commercially viable code base, could they still use these end-to-end coding agents? And at Grubile, we're fortunate to work with some very large companies. We work with Nvidia, with Coinbase, with Scale, with Data Dog, with American Express. And we got really excited to see if these coding agents were being used really at these large companies and if they were any good at doing real world coding. So, as an amateur data scientist, I decided to go and dive into our data. We review more than a million poll requests a month and we tend to get a lot of interesting data on what's good and bad about these poll requests. We do this for thousands and thousands of companies and they're usually enterprises or at least companies with serious products with real customers. And so we figured actually studying this data would yield some really interesting results. Was a surprisingly hard to figure out from all the poll requests that GR was reviewing which of the poll requests was actually generated by AI. Surprisingly difficult to do this. The first thing that I tried was I started looking at the GitHub author field. GitHub every commit has an author field and so went through the authors and turns out that less than 1% of pull requests had codeex or clawed or cursor as the author. But it wasn't intuitive to me that only but 1% of all code was fully AI generated. It just seemed intuitive that that number would be much higher. So I started to look for other signals. Now thankfully Claude and Codex and some other products leave a PR description in the footer. In the PR description, they put something along the lines of co-authored by claude or co-authored by cursor and so on. And this gave me a little bit more signal, a little bit more data on which PRs were ostensibly largely, if not completely AI generated. The third thing I looked at was branch name prefixes. And it seemed reasonable that if someone was using these coding agents in such a sense that they were writing the branch names or writing the PR descriptions that the PRs were largely AI generated. That seemed like a reasonable assumption to me. So now I had a good set of signals to indicate whether a poll request was in fact completely or largely AI generated or not. And I came to the result that about a quarter of all the poll requests that Graal was reviewing in any given month were completely or at least largely generated by AI. Then I backtracked this data to the last 12 months and it turns out that this number is growing really fast. In fact, early last year, fewer than 1% of pull requests had any evidence of being completely AI generated. So this number is going very very fast as model performance is getting better. What's also interesting is that you can't tell when new models came out on this chart. It seemed like the progress is very continuous. These things are just generally diffusing into the economy at a generally high pace. So then came the next question. Everyone's vibe coding. Everyone's producing these PRs that are antiendentic. Not human plus AI but literally AI. The question is are these PRs any good? First question, what does it mean for PR to be good? That seemed like actually a very important question to answer before we got into judging these AI generated PRs. And so I took a few methods to try this. The first one I tried was revert rates. If a pull re
...[middle elided]...
you work with naturally can scale to that same degree. And at Grav, we decided to take sort of a first principles view at what really good validation could look like. Instead of saying that we wanted to automate QA or automate testing or automate code review, we took a step back and said, what would we need to do for anyone to be able to merge hundreds of pull requests a month in an enterprise environment where it really matters that the code is correct? What would need to happen between when the code was expressed into a pull request and when it was merged and deployed safely? We figured we only actually had to answer three questions. The first one is does this change violate the user contract? The second one, does it increase the propensity of a future violation of the user contract, whatever the user contract might be for that application? And third, does it fulfill the intent that the author described? Did the poll request do the thing that the author wanted to do? And so we started approaching this problem from base ground level and said, okay, agents can probably figure out if something's going to violate the user contract and detect bugs. If you let it spin up the code in a sandbox, have it install the dependencies, mock the inputs, run the browser agents, you can probably start to discover most of the issues that could occur, you get a pretty high degree of confidence on merge. Today, almost a fifth of all the poll request or gravile reviews are merged without any human review or without any human testing, which I find very interesting and that is a number that we care a lot about and want to bring higher and higher, of course, within the guard rails of producing really high quality code. Thank you so much. My name is D, one of the co-founders of Graptile. We have a booth here which you should come to. And if you're interested in trying Graptile, you can find us at gretile.com and try it today for free. And we'd love to hear your feedback. Thank you so much.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "ai-generated-code-validation",
  "signal": 0.6,
  "novelty": 0.5,
  "actionability": 0.55,
  "evidence": 0.7,
  "durability": 0.35,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Доклад даёт реальную методологию замера доли AI-кода в проде (по данным ревью 1М+ PR/мес) и практический фреймворк автономного слияния PR, но цифры и пороги быстро протухнут по мере роста моделей.",
  "knowledge_units": [
    {
      "claim": "Долю AI-сгенерированных PR надёжно не определить по полю GitHub author (там agent виден меньше чем в 1% случаев) — реальный сигнал дают footer PR-описания вида 'co-authored by claude/codex/cursor' и префиксы веток.",
      "type": "tactic",
      "actionable": "Если нужно замерить долю AI-кода в своём репо/у клиента, стройте детектор по трём сигналам: author field, PR description footer, branch name prefix — одного author field недостаточно."
    },
    {
      "claim": "По данным ревью более миллиона PR в месяц у Greptile, доля полностью/largely AI-сгенерированных PR выросла с <1% в начале 2025 до ~25% к 2026 году, и рост непрерывный, без скачков к датам релизов конкретных моделей.",
      "type": "benchmark",
      "actionable": "Не привязывайте прогнозы адопции AI-кодинга к релизам конкретных моделей — используйте это как ориентир при планировании ресурсов на код-ревью и QA-процессы на горизонте квартала-двух."
    },
    {
      "claim": "Для автономного (без человека) решения о merge PR можно свести валидацию к трём вопросам: нарушает ли изменение контракт с пользователем, повышает ли вероятность будущего нарушения, и выполняет ли заявленное намерение автора.",
      "type": "principle",
      "actionable": "При проектировании авто-ревью/агента-валидатора PR формализуйте проверку именно через эти три вопроса вместо расплывчатого 'найти баги' — это даёт чёткий критерий готовности к автоматическому merge."
    },
    {
      "claim": "Практическая проверка PR агентом включает поднятие кода в песочнице, установку зависимостей, запуск локального сервера, клик-тестирование браузерным агентом и мок входных данных — на этой основе у Greptile ~1/5 PR мержится без единого human review.",
      "type": "workflow",
      "actionable": "Для повышения confidence перед автомержем добавляйте в пайплайн реальный запуск приложения в сэндбоксе с browser-агентом, а не только статический анализ diff."
    }
  ]
}
```
