---
session: s_6c5fb6d6
date: 2026-09-28
words: 1942
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_6c5fb6d6` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Reverse-Engineering the AI Buyer — Aliisa Rosenthal, Acrew Capital
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> Hi everyone. My name is Alyssa and I joined a little research lab called OpenAI a little over four years ago. When I joined it was you know a couple million in revenue. We had a self-serve API. We had some developers who found it and swiped a credit card and started building. Over the next few years I helped grow the organization to several hundred people, grow our revenue to several billion on the enterprise side and and launched multiple products. So I really had the opportunity to be at the bleeding edge of bringing this somewhat alien technology to organizations from startups to massive enterprises and I'm going to share a little bit about what I learned along the way. So I think most organizations typically have said okay, I'm ready to build out my go-to-market organization. I'm going to hire a bunch of sales people. I'm going to hire RevOps. I'm going to hire sales engineers and I'm going to build out my sales organization and then I'm going to figure out where the bottlenecks are and I'm going to add AI or I'm going to add automation to figure out how to scale this thing. My current advice to founders is do the opposite. So start with what you can automate. Start with there's so many tools available now in 2026 for a modern go-to-market or sales organization that have never been available before which really turns the entire playbook on its head. And you'll find that a lot of traditional sales leaders are very used to coming in and hiring a really big team and augmenting everything with humans, bringing in sales operations, sales engineers, lots of sales people, BDRs, SDRs. You can do so much of this through an automated approach now. So my my advice to founders is build the machine first before you build the team. Figure out what you can automate. Figure out where the bottlenecks are and what's broken and then add humans on top of that to get through those bottlenecks. So, just a story about how this played out at OpenAI. So, we launched ChatGPT in the end of 2022. When we launched it, we had no enterprise features whatsoever. And I got bombarded with organizations saying, "Hey, everyone in my company is using ChatGPT. Can I get SSO? Can I get an NDA? Can I get an invoice?" I had none of these things. I had no enterprise features whatsoever. Uh so, over the next few months, I begged and begged and begged our technical team, "Can we build an enterprise version of this product and we build some enterprise features?" And finally, 9 months later, we got approval. Now, over that 9-month time, the companies that had been the loudest, the companies that had gotten to me, were the bigger companies, were the large enterprises. So, I thought, "Okay, we should go out and build a really high-end product for all these enterprises that want to use us." So, we added every bell and whistle. We made it lightning fast. It was a very expensive product that we shipped. We went up market. We went way up market right out the gate. And, you know, we did fine. We We did pretty well. Um, you know, and and I think for most companies we did great. Uh but after about a quarter, we said, "Well, we should probably also offer a self-serve version. Not everyone wants to opt into this heavy sales process and start with these really high price points." So, then we released our self-serve motion in January of 2024, so about 4 months after our enterprise version, and it just completely cannibalized our enterprise business. Uh it grew so much faster. It turns out most people just didn't want to talk to a salesperson, and our mid-market SMB sort of self-serve business was much higher growth than our and then our heavy enterprise business. So, it frustrated the sales reps cuz now they had to compete with self-serve. It sort of cannibalized the customer base. They sometimes they preferred to just move into the cheaper self-serve option. And so, that was a really valuable lesson. We should have launched with self-serve first, listen to feedback from our customers and what we they weren't getting from the self-serve product, and then figured out how to add build a more expensive enterprise offering, and then hire the team to sell it. So, we did it all backwards. Was a really really valuable learning experience, and from there we decided not to do that again. For every other product we launched at OpenAI, we made sure to to do it self-serve first, learn where we needed to tack on humans and add them. Uh the other thing I'll mention, and uh you know, uh if Everett's still here, nice uh shout-out to him. We used Clay at OpenAI, and it was really really useful for us. So, in the beginning, we were just completely overwhelmed with inbound, which I know sounds like such a champagne problem, but it was me and four sales sales reps, and we were getting, you know, 10,000 inbound a day. I mean, it was just the most staggering problem to deal with this tidal wave of inbound. And, you know, if I could go back in time, there's so much I would have done differently. I would have, first of all, added way more fields to our sign-up form, like phone number, because eventually when we did catch up and we built all the automation and we figured out how to handle these leads, I didn't have a lot of information to go follow up with people. So, add a very in-depth sales form. It can be optional, but if people are willing to give you their phone number, you should get it, cuz at some point you might want to call them or have AI call them. Um so, gather as much info as you can. Try to respond to everyone, and I I you know, I wish I would have done this, at least just sent some email out saying, "Hey, we hear you. We don't have our enterprise product ready yet. You're on our waitlist. You're on our list. Tell us XYZ about what you're looking for." Just some sort of automated email campaign to make them feel like we cared. Because when we finally did launch our enterprise product 9 months later, almost every company went out and talked
...[middle elided]...
ly do pay dividends. >> Hi Alyssa. Um for startup working on like their first 10 customers, would you go like the clay route or would you do something else? >> Uh I'm sorry, when you say the clay route, what do you mean specifically? >> Like using something like clay for automated outbound. >> Got it. No, your first 10 customers are going to be different. Um they're going to be really more design partners. Um and they're going to need to be much more handheld. So, I I'm talking a little bit more when you're beyond the first sort of design partners and you have some product market fit and you're starting to scale the organization. For those first partners, you want to be very particular and picky about who you choose. On the one hand, it's it's sort of a gift to a company to let them be your design partner. There's exclusivity to it, there's scarcity to it. They really help give you a lot of feedback on your product, but you want someone who's going to work well with you, who's going to understand this is realistically where my product is. This is where my enterprise features are. Um so, you want to be thoughtful about who those first few customers are. One tactic I love to do on the design partner side is go to a company that has a great logo, but work on like their internal product or some sort of product that's not their main production, so that they're willing to take a little bit more risks with you and bypass some security processes, but then you get the logo on your site and you can go to companies and say, "Hey, I work with this company." And it opens the door to potentially sign a bigger agreement with that company over time. And I think we're at time here. Sorry. Ideally, they're relationships you already have, either companies you've worked with or your investors are introducing you or they're you know, friends at at companies cuz you want these to be very friendly uh uh uh processes and experiments in the beginning. Great. All right. Thank you. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "gtm-for-ai-startups",
  "signal": 0.25,
  "novelty": 0.35,
  "actionability": 0.2,
  "evidence": 0.7,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это бизнес/GTM-инсайты бывшего вице-президента OpenAI про продажи и структуру go-to-market, а не техническое знание про агентов/RAG/LLM-инфраструктуру — полезно продукт-менеджеру или founder'у, но не инженеру-практику.",
  "knowledge_units": [
    {"claim": "При запуске AI-продукта сначала строить самообслуживаемый (self-serve) продукт и автоматизацию, а команду продаж нанимать только под выявленные узкие места, а не наоборот", "type": "principle", "actionable": "Перед найм отдела продаж — сначала автоматизировать воронку и запустить self-serve тир, найм людей делать только туда, где автоматизация реально упирается в стену"},
    {"claim": "OpenAI сначала выпустила дорогой enterprise-продукт ChatGPT, а self-serve версию — только через 4 месяца, и self-serve неожиданно обогнал enterprise по росту и каннибализировал его", "type": "tactic", "actionable": "При запуске платного B2B AI-продукта закладывать self-serve тир параллельно или раньше enterprise-тира, а не как заплатку постфактум"},
    {"claim": "При заведении лидов в форму регистрации нужно собирать расширенные контактные данные (например телефон), чтобы позже можно было довести автоматизированный/AI-фоллоуап до конца", "type": "tactic", "actionable": "В форму сайта/продукта добавить необязательные, но информативные поля (телефон и т.п.), чтобы не терять возможность связаться с лидом позже"},
    {"claim": "Первых design-partner клиентов лучше искать не в основном продакшн-контуре крупной компании, а в её внутреннем/непроизводственном продукте — так они охотнее идут на риск, а вы получаете право сказать 'мы работаем с [известный бренд]'", "type": "tactic", "actionable": "Договариваться о пилоте с крупным брендом через их внутренний инструмент/second-tier продукт, а не через основной продакшн, чтобы обойти тяжёлые security-процессы"}
  ]
}
```
