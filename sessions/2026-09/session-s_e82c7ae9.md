---
session: s_e82c7ae9
date: 2026-09-29
words: 2047
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_e82c7ae9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Inside the Team That Killed Mandatory Code Review — Quinn Slack, AMP
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
Okay, we're in the remote studio with Quinn who is in Munich. Quinn, I have no idea where in the world you are at any given point in time. You guys seem to be having lots of fun doing offsites. >> We got the whole AMP team together in Munich and it's been awesome. But uh heading back now. >> Is the team usually remote? >> Yeah, we have one-third of the team in Europe, one/3 in the US, and one/3 in Australia. and we're 20 people so we're all over. I don't even know what time it is for people working. >> Yeah, >> it's pretty fun. >> I would say, you know, this is a tangent, mild tangent, but I think that, you know, when you run a remote company, the general principle I want to tell people is that the thing the money you would have spent on an office, you just have to spend on an off-site anyway. So, because then like everyone gets together. So, that that's really nice that you do that. And I know you you did one in Singapore, too, which I I really love to hear. >> Yeah. Yeah, we love Singapore. The air conditioning is a little bit better in Singapore than here in Germany right now, but we love Germany, too. >> Okay, so AMP people have been introduced on this pod and and everything and people mostly have just seen you online. I think the new hotness is orb and orbs. I guess if you want to explain like the recent transition like catch people up, what's going on? >> Yeah, with AMP, we want to explore the frontier. What is the craziest stuff we can do? How can we kill the older features so that we can make AMP the best way to use an agent? And if you're using AMP, then you're using it in the way that we bless. You're you're on the happy path. That is our promise to you. We will take out some features that don't make sense. We were early in killing an editor extension. We've killed a lot of features. And some people joked for the last few months, we were more known for killing features than for adding features. And I think that was the right decision because now with orbs which is a way to use AMP it's running remotely. You can shut your laptop. You can do a 100 things in parallel. That way of working has changed the way that we all work on the team and and our customers are using orbs more in the last three or four weeks than all of the change to how we build software that happened last year. And last year was not some quiet year. So with with AI moving so fast, the value of keeping users on doing the old thing is is actually negative. I mean, in the past, you would have a 5 or 10 year technology cycle and you could acquire a user and then they'd be with you for 10 years. But now, if you're not nudging them, yanking them to be on the frontier with you, then 3 months later, they're going to say, "Hey, who are these fools in their product? It's obsolete." And they're going to think less of you for it. So that's the principle and we think that orbs there's we're not the first ones to think of this idea. You know Devon ma massive props to Devon. >> Devon was early when they were laughed at. Hey this doesn't work. >> Yeah. And they they were right about this being important with orbs. We wanted to bring it all together. So it's not just that the agent is running remotely on the cloud. It's that we make an end just work and you can see your dev server that just works in a portal. you can uh you know get to the desktop, you can run these in parallel, everything just works and that is good enough for you to not want to use local dev. So you know local dev in our opinion is dead and that's been a huge change to uh you know what how we all build. You know, I think I wrote something in like 2021 about the end of local host at at the time that was how it's just like a reflection of like even pre-ai people at large companies like the Facebooks and the Googles and uh the Ubers of the world, they all had uh setups where you would mostly SSH into a machine or like you know have like a very light local clone of something that's much more powerful in the cloud. I think even in stripe um yeah once you have a good enough infrastructure your laptop becomes a thin shell like you can just like code on an iPad because it doesn't matter like you it's just an input device uh into uh into some cloud infrastructure >> but even then you know all the I know a lot of people that worked at those companies and >> they would say well yeah it's slower and you give up a lot it's actually feels really nice to work on your laptop everything is faster and with agents when you can run them remotely you don't feel like you're giving anything up you don't want to use local dev It's not like your corporate security department that says, "Hey, we need to use devs uh you know, VMs for dev." It's you you kind of just realize, hey, I haven't run my local dev server in two weeks. I mean, that's what I realized just a couple days ago. So, it does feel different. You do need to invest in the cloud setup, but um you know, it's not as daunting as people say and like now you can throw agents at it. >> Yeah. I will also mention or observe that you're making this transition similarly to a lot of other people in the coding industry. Open code is doing it. Conductor is doing it. Surprisingly, Codeex hasn't quite done it. I don't understand. Claude has done a lot. It used to be I guess like the the cloud claude thing and now uh Claude tag and then I guess cursor has done it as well. It's it's just like it's very interesting when everyone just decided that cloud was ready. Um, I would have said cloud was ready last year. Somehow it it took this year to take off. But I I don't know like do do you have any meta this is a bit meta but like do you have any reflections on like why now? the agents have gotten better for sure on longer horizon tasks. And um you know there's I I think something about when you see the agent so reliably getting it right enough times and you start to stop reviewing all of the code then that frees up more of your time to run more
...[middle elided]...
at you what you ended on, which is is really something to dwell on, which is should founders should people basically leave behind their large company and go get a small team that's a SWAT team and go go after what they perceive to be important and great and and I think you're having results. I think it's also important that you mentioned you're profitable, which you know, I think you and I had a really fun chat where I was like, you should host a meme of like a gathering of uh SAS CEOs that are profitable and it's just you. But I do think like this is a theme. Jeff Dean just left Google. >> Yeah, big news. >> Which not a thing I would ever thought I would say. [laughter] Um, and as far as we can tell, he intends to be five people working in a room. And his mission statement when he left Google was like, what could a small handful of people do as opposed to like thousands of people? And like him writing that is like definitely a dig at Gemini being like thousands of people. And I think it's very interesting that he wants to experiment with this. Obviously, he's like a 10x individual contributor, but like is there no room for domain expertise? Is there no room for um I guess scaling multiple people and and what have you. I think there's this very open question on like how people run their companies now. >> Yeah. It feels like nobody knows and we're all going to figure it out. That's why, you know, best place to be is just getting out there and building. >> Yeah. The people who do try will probably have a good shot of figuring it out. I was also mentioned I was also thinking about how Louu from Air Table effectively just did the same thing with Hyper Agents except that he didn't run it in parallel that much. He basically uh had already sold the company and was just kind of double heading for a bit and so yeah it's it's a it's a brave new world. Timelines are shortening. We're living in AGI and uh thank you for building in public. >> Yeah, thank you. It's great to chat.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "cloud-agent-dev",
  "signal": 0.4,
  "novelty": 0.3,
  "actionability": 0.3,
  "evidence": 0.25,
  "durability": 0.35,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Основатель AMP делится продуктовой философией (удалённые агенты вместо локальной разработки, агрессивное отключение старых фич), но без конкретики, метрик или технических деталей — это скорее взгляд основателя, чем воспроизводимая методика.",
  "knowledge_units": [
    {
      "claim": "AMP делает ставку на «orbs» — удалённое выполнение агента в облаке, когда можно закрыть ноутбук и параллельно гонять сотни задач; команда утверждает, что это заменяет локальную разработку полностью, если облачная инфраструктура и devserver-портал сделаны достаточно хорошо.",
      "type": "workflow",
      "actionable": "Для агентных пайплайнов стоит спроектировать удалённое исполнение (с доступом к dev-серверу и десктопу через портал) как основной режим, а не как резервный вариант к локальной разработке."
    },
    {
      "claim": "При быстром прогрессе ИИ ценность удержания пользователей на старом воркфлоу становится отрицательной — компания сознательно вырезает legacy-фичи (например, editor extension), чтобы все были на «счастливом пути» и не отставали от фронтира.",
      "type": "principle",
      "actionable": "При развитии внутреннего или внешнего AI-тулинга закладывать регулярное агрессивное устаревание старых интерфейсов/режимов работы, а не бесконечную поддержку обратной совместимости."
    },
    {
      "claim": "Когда агент достаточно надёжно решает задачи, разработчики перестают ревьюить каждую строчку кода, и освободившееся время уходит на запуск ещё большего числа параллельных агентов.",
      "type": "tactic",
      "actionable": "Ослаблять обязательный построчный ревью стоит только после накопленной статистики надёжности агента на конкретном классе задач, а не по умолчанию — иначе это просто снижение контроля качества без замера риска."
    }
  ]
}
```
