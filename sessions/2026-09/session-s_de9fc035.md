---
session: s_de9fc035
date: 2026-09-20
words: 1965
turns: 2
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_de9fc035` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Pinecone 2.0 — Edo Liberty, Pinecone
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] All right, welcome everyone. I want to tell you a little bit about uh the new the new uh knowledge layer and I'll start with telling you a little bit about theory of mind. Uh how many of you uh know what theory of mind is? All right, so a few folks. It's a uh term in psychology about uh our capacity to understand uh and have a mental state or a model of a mental state for other people. What do they know? What do they believe in? How do they act? That's what allows us to socialize. That's what allows us to lie to each other and so on. Uh but it's a crucial developmental stage for humans. uh in a necessary function. I'll I'll sort of explain it in the best possible way with a funny story just to break the ice. Uh about 15 16 years ago I uh worked at a company called Yahoo um that had a product called Yahoo Answers which was sort of like a Q&A forum. Uh we used then AI which is the stone age of AI you know it's like uh NLP and other statistical models to answer questions. But the funny thing is people would come to uh Yahoo and ask questions like am I fat? Which uh is funny because obviously uh you know Q&A forum would wouldn't have any clue whether you're you're too fat or not. Uh but this is a funny way to say yeah people have a very bad theory of mind on sort of what the products that they use what information they have and what they don't have. And I want to argue that in some sense we are making that mistake with AI today in a more subtle and less sort of like uh silly way but in a just as fundamental of a mismatch. And so I will categorize roughly three kinds of knowledge. I think there there are many more but you know in broad stro in broad broad strokes this is not a bad way to categorize. First of is general knowledge. Think about that is what's available in the public domain. Things that models are trained on and we expect an LLM to just know out the gate. Uh things about just you know improving your Rust code uh asking you like you know explaining stuff about the legal terms or uh sort of exploring use cases for for products. Um we know how to do that. Models are really good at that. When we use our agents they have that information. there is specific knowledge [clears throat] the companies of course the models wouldn't have uh any clue about whether we've uh implemented something specific in our codebase what a contract of a specific customer has of course this is information that's private to the company uh but we know how to deal with that and rag and search and of course pine cone veto dbs and so on uh solved these problems a long time ago there's still a lot to go but we by and large know how to do it and then I would say there is tribal knowledge. Okay, tribal knowledge is the sort of general knowledge inside the company. This is the kind of information that uh an employ a seasoned employee has that a new hireer does not. Okay, it's roughly how we do things, what our processes are, who's in charge of what, uh what are the guiding principles, what are the you know sort of how we get stuff done in this company. Okay. um that is not a that's not general knowledge because it's it's specific to your company but it's also not a specific piece of knowledge because you can't just get it by searching. You can't just get it by plucking it off one place and say yes this document says uh that this is our culture. It's the sum total of a lot of uh things. Um and so if our theory of mind of most of our agents in big companies today should be something like a new hire. They're brilliant. They have tools. They have we have very high expectations of them. But they are by and large clueless. Okay. They have no idea about your company's goals, culture, priorities, processes. Um they have to read a bunch of documents uh to be able to get any semblance of understanding of where they are in the world. Um and really they start most tasks from scratch. Okay. they really start kind of wake up and every time you start your your session, uh, they're like a new hireer on their first day on the job. So, I would argue that what they need is not necessarily to be smarter, to have better tools, but to have something new, which I would call a knowledge layer going forward. Um, and I have to explain to you what I think a knowledge layer has to actually do. But just I'll define it generally before explain to you what we do. Um so at the very least it needs to be persistent. We talked about this is the company knowledge, processes, capabilities and goals and so on. It has to be persistent. Uh it sure it uh feels like putting this thing together is going to be a monumental effort. So you want to do it once or at least very rarely. Uh and of course all your agents in company need to have access to this thing. The second thing is that you would argue that this [clears throat] knowledge layer needs to be uh highly specialized. If your agent uh is in charge of HR practices or optimizing your uh your kernels in your codebase or uh resolving customer issues that they would care about different things they would want to you know address they would want to have different information available to them. Um, and I would argue irrelevant of of specifically how it's created, I would argue that it's a good practice to have the domain experts in the company own those and have being able to interact with them and make sure that they actually uh are aligned with what the company wants to do. And finally, which is the hardest thing is they need to stay up to date and they need to stay concurrent constantly because companies change and you need to make information uh uh deprecated. When it becomes deprecated, if the company replaces its CEO, the very next day, everybody in the company knows who the CEO is. Okay? Even though 9,000 documents going from, you know, a day before yesterday to uh the last 10 years say it's somebody else. This has become common tribal knowledge immediately. And everything else, even you know, ev
...[middle elided]...
mount of prompting that you need is significantly reduced. We went down from having something like 150,000 tokens to give our agents all the tooling they need to less than a thousand tokens to specify all the interfaces they need to get information out of Nexus. Okay. And so the the so what it looks like when you run it is like this. Okay. So on the left of course you'll see Nexus with uh NoQL answering the question and then on the right is sort the same uh task given to an agent with all the tooling to complete the task. Okay, but remember this on the right it's uh severely handicapped. It's like the employee on the first day on the job. They have to read a bunch. They have to figure out where the data is. They have to figure out what the task is. They have to write a bunch of code. Uh it's just it's just severely handicapped and there's I don't know if you okay stopped but um needless to say this is by far slower. It's a lot more expensive in terms of token consumption. Uh but interestingly enough it's also a hell of a lot less accurate because again they don't have the right context, the right objectives and so on in your company. Um, I'll just say that [clears throat] we work uh obviously with a bunch of early access customers already. Uh, you see some results here, but I'll just sort of fly through them and say that across different domains, across different enterprises, across different kinds of task, you we universally see the same thing that if you shift to this paradigm, you get significant cost savings. uh 77 90 you know percent token consump token reduction is pretty common. Um uh it gets a hell of a lot faster anywhere from 20 30% to sometimes uh uh uh 77% faster. Okay. But and the most important thing is it actually becomes a lot more accurate as well in the same time. So this is really uh it's a slam dunk. I'll just wrap up by saying that uh um the that Nexus is coming out of early access and into public preview literally tomorrow. So go uh try it out.

---

> `Bash` -- {"command": "echo done"}

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "knowledge-layer-rag",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.15,
  "evidence": 0.25,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Это презентация нового продукта Pinecone (Nexus) с конференции — концептуальная рамка про 'tribal knowledge' любопытна, но по сути это питч запуска в паблик-превью с цифрами от вендора без независимой проверки и без разбора техреализации.",
  "knowledge_units": [
    {
      "claim": "Знание для агентов в компании делится на три типа: общее (в весах модели), специфическое (документы, решается RAG/поиском) и 'племенное' (процессы, культура, приоритеты — не лежит одним куском, его нельзя просто найти поиском).",
      "type": "principle",
      "actionable": "При проектировании RAG/агентной системы для компании отдельно продумать, как передавать агенту не факты, а неявные процессы и приоритеты — это не решается обычным векторным поиском по документам."
    },
    {
      "claim": "Замена ручного тулинга/промптинга агента на выделенный 'слой знаний' с декларативным языком запросов (NoQL) снизила промпт с ~150K до <1K токенов на задачу, по заявлению вендора на ранних клиентах.",
      "type": "benchmark",
      "actionable": "Не принимать цифру за чистую монету (это цифры вендора без методологии) — но если сравниваете 'дать агенту сырой тулинг' vs 'дать структурированный интерфейс к данным', стоит замерить свой промпт-бюджет по обоим путям на реальной задаче."
    }
  ]
}
```
