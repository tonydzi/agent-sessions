---
session: s_223235f5
date: 2026-09-30
words: 1961
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_223235f5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Defender's Window at enterprise scale with Standard Chartered
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
Ruben, we've heard a lot today about the defenders window, so I'd love to start the conversation there. What does it mean for standard charted and how you're protecting your applications? >> Right. I mean um for for standard charted I guess when we you know with with um frontier models uh what we've seen is that it obviously makes the the time to understand software and the time to figure out and identify exploits as well a lot shorter and and as such as a as a bank in a global scale uh you need to be able to understand what are these exploits a lot faster than than the attackers. Um, so it isn't really about finding vulnerabilities in code, but it's about understanding what is actually exploitable because attackers at the end of the day, they aren't looking at repos and assets, which is what a lot of security programs look at. They look at attack parts across systems, across APIs, across IDs, and across trust boundaries. So that's really key. >> Got it. Couldn't couldn't agree more that it's not just about adding to a longer list of CVES. Um, Standard Charted have been one of the first banks in the world to evaluate Daybreak, which we believe is going to be a critical part of the Defender ecosystem. So, I'd love to hear a little bit about how you've been using Daybreak so far. What kind of results are you seeing? Uh, how has it really been incorporated into the way that your teams are working? >> Sure. Um we we started looking down this track because we wanted to see whether Frontier AI was able to give us uh more insights into risks that the traditional approaches would not be able to provide us with. Uh would it be able to understand what uh what's happening across different repositories, what's happening across architectures and and trust boundaries. So that's why we started looking into this. Um and what we found initially our our earlier observations are that when the system is able to understand across architecture uh across you know we have a lot of microservices across microservices repositories what exactly is going on you get a lot more findings. So it's a lot it's it's a lot better to have that context around. So so context really matters. It it's more important to have that context than which model you pick. uh because with that context then you're able to uh find a lot of things that are truly exploitable. >> That's really interesting. So we we we hear a lot about kind of taking these frontier models and using them for static code analysis and trying to identify exploits that way. But uh can you just expand and maybe double click into that for me when you say like giving it more context and I agree context is king. What in practice does that look like? What what else are you feeding into the model at the time that you give it the codebase to help it do? So things like um the architecture the architecture diagram what is the what is the architecture deployment model of what we're looking at uh what are the dependencies um what are you know other services that are connected or or being used uh by by this asset across u and what what was the solution intent of of this uh item right so these are all the things that we're giving it the more context that you're able to provide it with then you get better results >> got it that makes sense and you know we've been talking a bit about the role that your team is playing by applying Daybreak. Uh, and there's a lot more things to consider beyond just the tech, right? How the team actually operates um, and you, I guess, have a responsibility to earn the trust of the team in using these new tools. So, what are you learning about how to make these AI generated findings trustworthy and how is that changing the way that you organize the teams that are working on these challenges? Um yeah, I mean just just doing a demo and showing it to the development team is isn't good enough, right? You need hard evidence. So working collaboratively with with the development team is where where I think we're going and that's what we've been able to do. uh is working in um in a cross functional group with uh application security as well as the development team together on on trying to you know run this because anything that we find needs to be validated against the code needs to be validated against the architecture deployment and against the environment right so in order to do that we need to do it together in a collaborative manner so that's what we're trying to do >> got it and I'm sure that many others in the room today are facing similar challenges is that uh security is not just the security team's problem but requires buyin from the entire software engineering community inside the organization. So are there any lessons that you learned of like what worked well or how did you uh win them over or get them to start to adopt this way of thinking into the way that they're building products and services inside the bank? >> Um it's it's not just focusing on hey we found something right. Um it it's about how do we kind of get better efficiency on remediation um and getting those uh those the right security outcomes. So one them understanding the root cause of why something happened and then they may not you know they they'll do different do it differently next time around and won't build their applications that way. Uh and and the other is also just work you know not trying to call it out trying to work with them to remediate. So also using the frontier AI to do the remediation so it's not just about another dashboard, right? >> Yeah. And not just adding another task to the backlog. >> Yeah. >> Um I think the coming back to the defenders window for a second, you know, there's a sense of urgency which which we certainly feel. I'm sure that many in this room also feel a sense of urgency to to address the challenge in front of us. But uh an organization like Standard Charted uh you know is large, has processes, has governance uh which maybe isn't designed to m
...[middle elided]...
ght checks along the way. >> Got it. That makes total sense. And then maybe just a final question from me before we wrap up. Um, as as we uh embark on uh kind of building out more products as we uh continue to advance the capability of Frontier models in this space, uh I'd love to know uh what what what would you like to see from OpenAI uh that would make uh your work as a defender easier? Would you take the feedback from Matt and the team uh to to incorporate into the product? Um I I I think you've um you gave us a good uh sneak peek earlier uh on where you're going with it and that's exactly what we were thinking as well in some of the conversations that we've had. Uh we do want to be able to like as you're moving the product is to be able to run it at scale. So just doing uh a scan on a handful of repos or repo by repo is not scalable. So being able to run something in uh in a sandboxed environment and do it at at bulk uh to to see if there are any exploits because you the the fact of the matter is that you have a lot of applications that are connected to each other. So you want to understand what is that blast radius and you know if you if one gets breached where else does it go. So I think what you're thinking about with the defense factory would would be really good. Well, I'm looking forward to get to getting you access uh set up soon uh to the defense factory. Um so we could I'm sure continue the conversation all day, but uh I'm watching the clock and our our time is up. So thank you so much uh for joining us today, Reuben. Uh and I'm sure that Reuben will be delighted to to answer any questions if you if you want to find him uh after the sessions today. Uh we'll be having some drinks afterwards. So please do come find him and ask questions. But with that, right now we're moving straight on to our next session. Uh so please welcome my colleague Claire Lawler who's our fantastic account director for the digital natives uh team in AMIA to the stage. Thank you.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "llm-appsec-context-engineering",
  "signal": 0.35,
  "novelty": 0.25,
  "actionability": 0.4,
  "evidence": 0.3,
  "durability": 0.4,
  "volatility": "volatile",
  "half_life_days": 180,
  "why": "Это клиентский кейс OpenAI (Standard Chartered про продукт Daybreak) на конференции — по сути реклама с элементами реального опыта, но конкретики и цифр почти нет.",
  "knowledge_units": [
    {
      "claim": "Для поиска реально эксплуатируемых уязвимостей LLM-агентом важнее не выбор модели, а объём контекста: архитектурные диаграммы, модель развёртывания, зависимости между сервисами и 'замысел решения' (solution intent) для каждого актива.",
      "type": "tactic",
      "actionable": "При построении AI-агента для аудита безопасности сначала собери и подай контекст об архитектуре и связях между репозиториями/сервисами, а не полагайся только на анализ кода репозитория по отдельности."
    },
    {
      "claim": "Находки AI-агента по безопасности не принимаются командой разработки на веру — их нужно валидировать совместно (security + dev) против реального кода, архитектуры и окружения, иначе доверия к инструменту не будет.",
      "type": "workflow",
      "actionable": "Встраивай в пайплайн AI-security-ревью обязательный шаг кросс-функциональной проверки findings с dev-командой перед тем как заводить тикеты или блокировать релиз."
    },
    {
      "claim": "Ценность AI-инструмента для security измеряется не количеством найденных проблем, а скоростью и качеством ремедиации, включая объяснение root cause и использование того же AI для генерации фикса.",
      "type": "principle",
      "actionable": "Проектируя AI-security-тулинг, сразу добавляй режим 'объясни причину и предложи fix', а не только детектор с дашбордом — это снижает сопротивление команд."
    }
  ]
}
```
