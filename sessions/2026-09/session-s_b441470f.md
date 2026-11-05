---
session: s_b441470f
date: 2026-09-28
words: 1966
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b441470f` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Missing Layer in Agentic AI — Giedrius Šteimantas, Oxylabs
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> What a beautiful voice. I thank you for coming. Um today I'm going to talk a lot about about missing layer of agentic AI and explain a a little bit about how web scraping infrastructure can actually help you. But first, let me talk uh a little bit about my friend's idea. So, my friend had this idea. Uh he built this AI chatbot that, you know, chatted with people about their style and it was supposed to help them pick out new items. Uh uh you know, some sort of a personal shopper. And once those items were picked out, you know, this uh this this this chatbot would uh produce prompts that a shopping agent would then take and attempt to find them online and purchase them for a you know, for for for the customers. Um this idea, you know, is not new and uh it could be applicable to many scenarios, but my friend was kind of, you know, uh he was he was good at building agents, uh but um he ran into different problems and asked me for advice. And when he ran it, he he would usually, you know, instead of, you know, product pages or whatever, he would get things like that. It's uh you know, he would get captured. And you know, and uh you know, of course, you know, he was he was doing it very very quickly. So, he web coded the whole thing a while having a you know, a thought about, you know, infrastructure and underlying layers and how it should work at it at all. Uh he was using a browser automation framework for everything and it was slow, expensive, and unreliable. So, at the end he made a product that uh uh that does not work and is expensive to run. So, he asked me for help and you know, I was a little bit reluctant at first because uh you know, I don't like giving out professional advice, you know, for free. But uh I took a look at it and uh you know, it I got a little curious, I have to be honest. I noticed that he was missing something. Um he was missing a layer. An infrastructural layer that would allow this agent to operate freely on the open web. My name is Giedrius. I I work for Oxylabs uh where in the past 10 years we've helped, you know, companies that trained large language models uh get their data. Uh now we use this infrastructure to help AI agents to access uh web on scale and at low cost. And uh before we go into this agent and see how we can build it, I wanted to talk a little bit about the scraping industry and how we operate. And uh the principles that we operate on can be summed up by one uh sentence. You know, cost matters. And the first principle is use a browser when you absolutely have to. Validate content. HTTP response 200 does not mean that we are good to go. Lighter content is preferred. Websites are full of JavaScript, CSS, HTML, and there's a lot of bytes that do not deliver any value whatsoever. And today I will demonstrate how these principles are also applicable when building agents that interact with the web. So, coming back to my friend's agent, right? Let's uh let's take a look and see how uh we could do a better job and making this agent more reliable. So, here's how my friend set a low level, you know, it's all four different stages. Discovery. The agent is was supposed to find products pages on websites where these items can be bought. Then a decision stage, right? And where an agent can decide what products to buy based on, you know, the the content of these pages. So, the agent has to visit them, verify that the the stock is there, the price is right, that the the the description fits, you know, the prompt. And once that decision is made, user is given with a choice, you know, whether to go ahead with the purchase or, you know, reject it all together. The problem was that sometimes, and of course, we go to execution right away. Then execution is making the purchase. But the problem was that sometimes it worked and sometimes it did not. That was a little problematic. So, let's dissect it step by step and see how we could build this differently while improving performance and reducing the cost dramatically by using the same principles from the scraping industry. So, the first stage, discovery. So, my friend, you know, he chose to go with a predefined list of websites, major retailers, and queried their search pages in order to find these products. He used a browser automation tool for that. It kind of worked, but you know, it did have challenges. So, the browser automation tool lacked what we call stealth. So, they could So, they would get captchas and sometimes fail access access the sites all together. This would break down the flow. So, a retry mechanism would have to be put in place, making the whole process very long, you know, costly and sometimes the size would not be accessed at all. And also, you know, as a result also became very difficult to predict the final cost per transaction. The list of websites that my friend was checking was also deterministic. So, selection of items would only be limited to the few choices he put in. Websites themselves were heavy on JavaScript making the whole process very slow and costly. And finally, even if it worked, items ended up being unavailable at checkout because in the discovery phase the heat was not able to use energy allocation capabilities and a lot of e-commerce websites are, you know, they take your user's location into account when displaying stock, options, sizes, and so on. So, now we solve these problems at Oxylabs every day. So, when scraping you always want the results to appear on the first try and to not to use browser unless absolutely necessary. However, for this specific discovery phase you also want to use to allow your agent to search the web. Doing so with browser is very cumbersome. That is why I chose to use a product that we built especially for agents, fast search API. It returns a compact JSON which is less than 2,000 tokens per response, has fast response times, less than 700 milliseconds on average, and it's has a high success rate at a predictable low price. And most imp
...[middle elided]...
e of the workflow, the purchase. So, I remember what I said a couple of times about browsers. This time but this time is different. You this time you absolutely need to use a browser. We need to process inputs and the content is highly dynamic. Now, this time my implementation, my friend's implementation, does not differ much. We both use Playwright MCP, with a browser, and a large language model. The main problem my friend faced, however, just like in in the previous stages, uh using browser, was access. Just like in the beginning, as he was using the browser, he was getting captured into oblivion, making it impossible to automate the flow. Well, the fix was quite easy. I just connected the Oxylabs headless browser, since it supports Playwright MCP, it's just a drop-in replacement. With this replacement, I hardened this agent with years of scraping experience and got proper stealth done at the browser source code level, a residential proxy attached to it out of the box, and most importantly, in this in this case, a geolocation capability. So, my results are localized the same way as in the verification stage. So, if we run it, we actually have a a a a browser that that access the content and can actually automate the flow by, you know, selecting the right size from the prompt, add it to cart, and complete the purchase. And boom, we have an agent that commands a powerful infrastructure hardened by years of web scraping experience. Not only does it open the up the web, but also saves the time on implementation and token cost. And if I can leave you with a few lessons we learned today, was that you know, when building agents, use the same principles from the scraping industry. Use the browser when you absolutely need to. You have to validate content before feeding it to the large language models. And most importantly, fill the missing layer with the proper infrastructure so you can focus on building stuff. But remember, cost matters. Thank you very much. >> [applause]

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-web-scraping-infra",
  "signal": 0.4,
  "novelty": 0.25,
  "actionability": 0.4,
  "evidence": 0.3,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это вендорская презентация Oxylabs, продающая их прокси/поисковый API как решение, но внутри есть рабочие архитектурные принципы для агентов, ходящих в открытый веб.",
  "knowledge_units": [
    {
      "claim": "Веб-агента выгодно разбивать на стадии (поиск/discovery → решение → исполнение) с разной инфраструктурой под каждую, а не гонять всё через один браузерный фреймворк.",
      "type": "workflow",
      "actionable": "Для стадии поиска использовать лёгкий JSON-based API вместо полного браузера, а браузер оставить только для финального шага с динамическим контентом (например, оформление покупки)."
    },
    {
      "claim": "HTTP 200 не означает, что получен валидный контент — капчи и заглушки тоже отдают 200.",
      "type": "tool-caveat",
      "actionable": "Добавлять явную валидацию содержимого ответа (например, проверку на маркеры капчи/пустой страницы) перед тем как передавать его в LLM, а не полагаться на код ответа."
    },
    {
      "claim": "Браузерная автоматизация без stealth-слоя и резидентных прокси на масштабе упирается в капчи, что делает стоимость и надёжность агента непредсказуемыми.",
      "type": "tool-caveat",
      "actionable": "Если агент массово ходит на сторонние сайты браузером, закладывать в архитектуру anti-detection/прокси-слой сразу, а не после первых банов."
    },
    {
      "claim": "E-commerce сайты показывают разный контент (наличие, цену, размеры) в зависимости от геолокации запроса.",
      "type": "tool-caveat",
      "actionable": "Для агентов, проверяющих наличие/цену товара, использовать геолокационно-таргетированные прокси, соответствующие локации пользователя, иначе решения агента будут основаны на неверных данных."
    },
    {
      "claim": "Тяжёлый JS/CSS на страницах — источник лишних токенов и задержек при скрапинге для LLM-агента.",
      "type": "principle",
      "actionable": "Предпочитать облегчённые представления контента (текст/JSON) полному DOM при передаче веб-страниц в LLM, чтобы снизить токен-затраты и время ответа."
    }
  ]
}
```
