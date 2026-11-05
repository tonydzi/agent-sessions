---
session: s_24bce34a
date: 2026-09-23
words: 2058
turns: 3
tools: "ReportFindings"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_24bce34a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How to Get Your Org to Adopt Coding Agents (Without Shipping Garbage) — Eyal Blum, Figma
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Good afternoon. My name is Alon Blum. I am a software engineer at Figma. And in my talk today, we're going to talk about how we've adopted or are adopting agent into our workflow at Figma while maintaining high quality for our code base. So, as you may know, Figma is the browser-based editor where design and engineering and now AI agent collaborate together to ship code. Uh this Figma has pivoted very strongly from being a traditional tool to an AI-first tool. But in this talk, I'm not going to talk about our product. I'm going to talk more about our internal organization and how our engineering org has been adopting AI agents. Um what we we found internally is both organizations, companies, and individual there's kind of a three-act process of AI adoption. You start with picking up something, whether it was a lot of the people in this room who have been doing using our AI pal and have been using AI for a while and they picked up something and got some simple things to work very well. 10x faster. Then you start applying those same practices to bigger problems and AI fails pretty badly at that, gives you bad stuff, lots of bugs, and the trust that you build breaks down. And then from that point, you start building the real skill, which is learning how to use AI correctly and put the right guardrails and the right prompting and the right context and all the stuff that we've been talking all day about here in all the talks in order to actually build a real scale. And one thing that is happening internally as we we adopted whether teams or individuals the adoption is uneven. We have teams that are very AI forward and have already transformed their entire workflows and then we have teams that are still experimenting in the earlier act and or have lost confidence and they all need to work together in order to ship our product. Um So, they need to coexist in the organization and we need to find a way to support them and while bringing on everybody along for the journey and getting everybody to the third act of the story. Aside from that main friction point, we have also noticed other friction points that happened as we adopt AI. One thing that we've heard a lot from developers and managers have have been noticing is that reduced developer agency causes um engineers to lose some of their job satisfaction. So, if a lot of people used to take a lot of pride and enjoyment in writing code and getting into the flow and a lot of people feel like that's been lost or they're losing a lot of that element and getting into more of a prompt cycle where they just wait on output from AI and then speak to the AI that like not as much fun as they used to have and they're getting burned out. Um we've noticed another interesting thing. It's actually our best engineer, the one that hold all their contacts in their brain. Um they end up getting out of the burden. What ends up happening is they they know where all the pitfalls are. They are like holding together with with like their mental duct tape all the places that agents are not working well and they're preventing all the really bad stuff from coming in or all they they have all the institutional contact that have never written down in their head and they get so much burden and and become bottlenecks and gets really frustrated. So, they actually end up being slowest to adopt because they see all the problem uh first hand. That's another big big issue that we've seen. Um and this one I'm sure everybody can resonate or in Sorry, I'm sure everybody here will resonate. Um that all of a sudden all the design docs and all the Slack messages you know, this the emails have gotten three or four times as long and we've gotten two or three times as many emails and they say basically as much as they did before. So, communication has gotten quite inefficient and some of the markers of like what is high quality and important things versus not so much high quality um has become challenging to navigate. Um so, I'm going to spend uh the next few minutes talking about some of the lessons that we've learned and how we've been trying to apply this. This is a journey. We have not come out through the other end, but we've seen some really interesting progress along a lot of these lines. Um I think this uh a lot of the speakers here have touched upon this, but investing in verification is probably the highest value thing we can do in our code base. Um anytime that we can lift a left shift anything in our workflow from a human needing to do it to an agent being able to verify it. So, for example, when uh Playwright and MCP came out, instead of having humans navigate the code, now the agent can explore the code. That was a big win unlock for productivity in a lot of our team. That's really That's always a a big win for us. The other thing is um it's even better if when you find something that the agent has found to be useful, take the time to take that and encode into a deterministic flow. A deterministic flow that can be easily repeated is saved on tokens, save on time for the and then it also you also know that you're using the the LLM when it needs to reason, but when you have something that is already known and basically can be encoded into a test, spending that time always always pays dividends. Um And another tip, if you tell your scale your agent to write the code that you're writing um like at the red to green to red to green at the TDD style, it almost always gives you better results because you set a goal, then you tell the agent to strive toward that goal, it will almost always give you better results than writing the code and then writing the test afterward because then it will fit the test to the code rather than fit the code to pass the verification criteria. Um this is the testing pyramid that uh can't the classic testing pyramid from the previous uh just when you think about the testing themselves, which you had the end-to-end test and the integration test an
...[middle elided]...
lture is just as important as some the engineering challenges that we've been facing. Um another thing that's really helpful around the adoption is um as you progress through adoption, there's a lot of very fancy tools and a lot of very fancy workflow that we've we've been implementing, but one of the really effective thing is just letting people use the AI where they're at. So, uh it help it really helps normalize uh the use of AI for everyday tasks and it helps reduce the friction. And really one of the most powerful thing is being able to tag an agent in the Slack message with somebody and they can you just do this for me? And have the agents to close the loop in the thread. Um that that's kind of thing is really powerful. And then you can go on top of that and have all this thing automated and do all kind of fancy things, but if you have a new conversation with somebody who's not fully bought in and then you can tag it in a non like non-passive-aggressive way. You can tag it and say, "Let's try to see if the agent can get it this time." And they close the loop and if it's a good experience, that really helps people try it out on their own in other cases. And our journey continues. We're still learning even though we're shipping AI externally, our AI adoption um we're experimenting with with so many things all the time. Our automation story is not uh fully there yet. We're still trying trying to figure out when we should use how we can use cloud agent effectively given all the dependencies we have for some of our bell system. And so we are continuing to learn. It's a culture shift, it's an engineering shift and I don't know about you, but for I've been I've been working in the valley for the last 15 years and this is the biggest change by orders of magnitude of everything that I've seen in term culture and technology. So, um we're all here together and we're all figuring it out and that's that's what I wanted to talk to you today. Thank you. >> [applause] [music]

---

**Claude:**

01:53, среда, 23 сентября 2026.

---

> `ReportFindings` -- {"findings": []}

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding-org-adoption",
  "signal": 0.55,
  "novelty": 0.4,
  "actionability": 0.5,
  "evidence": 0.45,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад инженера Figma о реальных организационных и инженерных практиках внедрения кодинг-агентов, с несколькими конкретными тактиками, но без глубоких технических деталей или бенчмарков.",
  "knowledge_units": [
    {"claim": "Инвестиции в верификацию (например, дать агенту доступ к Playwright/MCP для самостоятельной проверки кода вместо ручного тестирования человеком) — самое ценное вложение при масштабировании агентов в кодовой базе.", "type": "principle", "actionable": "Ищите шаги ручной проверки в вашем workflow и переносите их на агента через инструменты вроде Playwright MCP."},
    {"claim": "Найденный агентом полезный паттерн стоит закреплять в детерминированный автоматизированный флоу (тест/скрипт), а не полагаться каждый раз на рассуждение LLM — это экономит токены и время.", "type": "tactic", "actionable": "После того как агент решил задачу удачным способом, зафиксируйте решение как воспроизводимый тест/скрипт вместо повторного промпта."},
    {"claim": "Постановка агенту задачи в стиле TDD (red-to-green) — сначала цель/тест, потом код — даёт более качественный результат, чем просьба написать код, а затем тесты задним числом, так как во втором случае агент подгоняет тест под код.", "type": "workflow", "actionable": "Формулируйте задачи агенту как 'напиши тест, добейся его прохождения', а не 'напиши код и потом тест'."},
    {"claim": "При неравномерном внедрении AI в команде лучшие инженеры (носители недокументированного контекста) часто медленнее всех принимают агентов, так как первыми видят все их провалы и вынуждены закрывать пробелы вручную — это создаёт узкое место и выгорание.", "type": "tactic", "actionable": "Явно выявляйте и разгружайте senior-инженеров, которые стали 'ручными патчами' для агентных провалов, документируя их неявные знания в инструкции/контекст для агентов."},
    {"claim": "Тегирование агента прямо в Slack-треде ('можешь сделать это за меня?') с закрытием цикла агентом в этом же треде — низкозатратный способ ненавязчиво нормализовать использование AI среди скептически настроенных сотрудников.", "type": "tactic", "actionable": "Внедрите возможность вызвать агента прямым тегом в существующем чат-треде вместо отдельного интерфейса, чтобы снизить порог входа для неубеждённых сотрудников."}
  ]
}
```
