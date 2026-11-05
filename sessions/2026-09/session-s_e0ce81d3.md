---
session: s_e0ce81d3
date: 2026-09-27
words: 2034
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_e0ce81d3` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: How We Got LLMs to Recommend Our Open Source Library — Christopher Burns, Inth
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] >> The talk title, we'll see if it lines up by the end of it, but when we put this talk title in just to be honest with you, so much changes in like 3 days at this point. We'll see how it goes. So, yeah, the whole point of it was that how I got LLMs to understand my open source library and what I did to do it well. Is it some kind of scientific background? Am I from a lab? No. That's My slidey clicky thing's not working. So, I just like to say again, I'm just like you. I'm just this side of the stage. I've just hacking hacking it together, figuring out what is useful, what is token efficient, these kind of things. And again, I am British. Please don't think my accent makes me an expert. So, for quick contacts, I'm Christopher Burns. I'm the founder of Inth. I created a open source cookie banner library called C15T. That really annoying thing on the internet. That is me. Uh I spoke at Next Conf uh after it started taking off and it had 1.2 thousand downloads at the time. Now it's closer to 2 million. In terms of like statistics, so we just checked that, you know, this is not theoretical. This is actual uh something that is succeeding. We have 3 million NPM downloads. 4.5 uh 4.5 45% month-on-month growth. 2.8 thousand websites using it in production from Minify to Z to Inphysical. And the whole concept of this talk was uh it goes back to we were doing all these things to make our library more efficient. You know, we were batting upwards compared to every other tool. Every other tool was built for marketers and lawyers. We were built for the developer. So, we had to make sure we had a very good developer experience. And we had an onboarding format said, "How did you hear about this?" And we started to get spikes that from April 13th, you know, now it is our number one source of inbound is Claude, ChatGPT, Codex, that is ChatGPT, Gemini recommending us. And I like to think of this as, you know, the iceberg. You know, we start with the top of C15T and there's many many tools that go into it from, you know, LLMs.txt to site maps to RSS feeds to robot.txts. So many micro optimizations that you can do from old methods of running the internet to new methods. And uh how many of you have, you know, made these kind of tools? How many of you have, really put simply, said, "Hey, agents, we need to this to be done." And yeah, it said, "We should install this library." And you've gone, "Okay." Raise your hands. How many people have done this? Pretty much most people. That's a lot of hands. So, what's really funny is that we went from wizards installing our software to agents installing them. And I just went through Y Combinator. And what's really interesting is it if you know who these two people are. These are the co-founders of Stripe, the Collison brothers, and they had a really classic saying of like a Collison brothers install. And they would hand you their laptop, and they would install Stripe. These days, it's kind of like just a prompt. Being in Y Combinator, we just give people a prompt. And really what that means is that our very good developer experience primitives are now hitting agent primitives. So, as we was pulling all these things together, there is no one tool that fixes everything. I like to think about these problems like, you know, Batman's utility belt. Loads of really small things targeted in different areas to get it done. And we built all of these things into C15T because we wanted C15T to be the best developer framework in this tool. Think of it like Stripe Docs. And as we was building more and more tools, more and more documentation websites, we actually started abstracting these tools into a side quest that we call Lead Type. So, all of the things that we're going to talk about now are things that we have already solved with this open source framework. We have our friends at other developer companies implementing it and seeing similar results about how to like optimize for the agent experience. So, again, this isn't a magic SEO tool. It's actually a very non-sexy title, but a framework-neutral docs pipeline. Complex. But really, all it basically does is take your .mdx files, you run Lead Type generate, and it will spit out everything for um optimized agent experience for your websites. And the rest of this talk is going to look a bit like a BuzzFeed list, to put simply, of these problems, because again, not everybody knows even how to put an LLM.txt on their website. So, you know, that comes to the first problem of if your docs have hundreds of pages, and how can it navigate them to find the right questions? The first solution is obviously an LLM.txt. What we found in our research is that it's much better not to just generate this. It is much better to write your LLM.txt from hand. Obviously, AutoRaptor, but write it as you are trying to get the answers across to the LLMs. For about 40 good lines beats 1,000 lines of noise from our testing. And that comes to the second issue of agents don't know how to browse. They know how to fetch. So, you then need the second part of the solution of the LLMs full. Again, think of this as a sitemap, where it takes the actual page and the links and a short description of what each page is for the LLMs to reference. Again, most people have heard these two solutions. But, where things are starting to get very complicated and we're seeing a lot of optimizations right now, is that HTML is expensive, and why can't we just ship markdown to the agents? And we can. And you've seen that everybody has started creating twin MDs. So, that's taking the normal website, such as Next.js quick start, and then having a dot MD on the end of it. And when you load that, it goes to the markdown But, what's really important here, and it's really worth noting, is this line at the bottom. If you look at all the best documentation websites, Minify, Vercel, C15T, pat myself on the back. Um they all have this in the header. This is saying to the agents whenever
...[middle elided]...
final slides is that the slide the the market agents, LLMs, everything is forever changing. There is no such thing as perfection. When I started making these slides, I got so caught up of like, everyone expects me to be the expert here, but I've just been hacking on this problem a little more than you guys have so far. So, never get caught with being perfect. Every small little increase really does matter. Every small little thing you add really does matter. Thank you so much. You can find me on X, Burn Chris, and LinkedIn, and everywhere. >> [applause] >> WOO! I THINK I THINK WE HAVE TIME for one or two questions. Yeah, of course. >> So, if you were building um uh we're a website agency. We work with a lot of startups building like their own websites. >> Mhm. >> If you were just building a website, not necessarily like developer tool, but just a website to be found, which of these methods like would you concentrate on if you're starting from scratch? >> Yeah, I think the most important ones, and we're starting to see this more and more, is trying to provide a dot md file for every single page. A lot of CMSs are not built in this way. Um and we see this optimization happening more and more where I didn't put in the slide, but we're seeing more and more websites being visited by agents instead of real humans. So, in terms of even like trying to be proactive and token efficient, you should provide a markdown file if you can. Again, a lot of CMS's are not built this way. I actually built my own CMS. My name is Chris and I built ChrisCMS, short for Christmas. It's a whole It's a whole thing my team wishes I never built. But, it does work and it does bring this like token efficiency up. So, yeah, I would say llms.txt is your first shout. llms.txt full form .txt. Second, if you if you can, just do them manually. Say you're not even working on systems that have markdown, I still recommend them. But, you can always get creative with creating these files on the on on the go.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "geo-for-docs",
  "signal": 0.6,
  "novelty": 0.5,
  "actionability": 0.7,
  "evidence": 0.6,
  "durability": 0.35,
  "volatility": "volatile",
  "half_life_days": 180,
  "why": "Доклад даёт конкретный, проверенный на реальных цифрах (3М скачиваний, рост инбаунда от LLM) набор тактик, как сделать доки библиотеки понятными для агентов, но практики GEO для агентов ещё быстро меняются и часть советов скоро устареет.",
  "knowledge_units": [
    {
      "claim": "llms.txt эффективнее писать вручную и коротко: ~40 содержательных строк работают лучше, чем 1000 строк автогенерированного шума.",
      "type": "tactic",
      "actionable": "Не генерируй llms.txt автоматически из всей документации — вручную отбери и сформулируй ключевые ответы для LLM, уложись в компактный файл."
    },
    {
      "claim": "Агенты не 'браузят' сайт, а фетчат конкретные URL, поэтому нужен llms-full.txt — по сути карта сайта со списком страниц, ссылками и коротким описанием назначения каждой.",
      "type": "tactic",
      "actionable": "Добавь llms-full.txt рядом с llms.txt: список страниц + ссылка + однострочное описание, чтобы агент понимал, какую страницу зафетчить под конкретный вопрос."
    },
    {
      "claim": "HTML дорог по токенам для агентов, поэтому лучшие докс-сайты делают markdown-twin для каждой страницы (например /quickstart.md рядом с /quickstart) и явно указывают в HTML-заголовке, что есть markdown-версия.",
      "type": "tactic",
      "actionable": "Для каждой страницы документации сгенерируй .md-версию и добавь в <head> HTML-страницы ссылку/заголовок, сообщающий агентам, что доступен markdown-эквивалент."
    },
    {
      "claim": "Не существует одного инструмента, который полностью решает видимость для LLM-агентов — нужна комбинация из многих малых оптимизаций (llms.txt, sitemap, RSS, robots.txt, markdown-твины и т.д.).",
      "type": "principle",
      "actionable": "Планируй GEO для агентов как набор из 5-10 независимых мелких доработок инфраструктуры доков, а не как одно волшебное решение."
    },
    {
      "claim": "Отслеживание поля 'как вы о нас узнали' в онбординге позволило автору обнаружить, что Claude/ChatGPT/Codex/Gemini стали топ-1 источником инбаунда для их open source библиотеки.",
      "type": "workflow",
      "actionable": "Добавь в онбординг/регистрацию продукта поле атрибуции источника и явно включи в список вариантов LLM-инструменты, чтобы измерять, сколько трафика приходит через рекомендации агентов."
    }
  ]
}
```
