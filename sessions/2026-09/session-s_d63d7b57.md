---
session: s_d63d7b57
date: 2026-09-25
words: 1742
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_d63d7b57` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: AI Engineer Paris 2026 Opening Keynotes: Mistral, Langfuse & Sizzy | Day 1
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
labor to the economy because we can add capital to the workers that are in the economy or because we become better at turning this labor and capital into economic output and that's what we would call productivity increases in economics and in the long run the main driver of economic growth are these productivity advances and those in turn are basically improvements in technology and also in organizational progress which is closely related and this is where I want to start and to bring in actual history um to to to draw parallel to the AI productivity puzzle that I was alluding to at the start. We can, for example, I think very well compare AI to the prime example of a technological revolution in history, which is the industrial revolution. Um, the industrial revolution, as I mentioned, kickstarted modern economic growth. Yet, we observe a somewhat similar and interesting pattern for it too. The steam engine, its main underlying technology, contributed close to nothing to productivity gains for many, many decades after it was invented. And it took actually over a century until we see productivity and economic growth showing up in the data after the invention happened. All right, a brief slide on technologies. In economic history, there's generally a class of technologies that's described as general purpose technologies um which are in economic history uh funnily enough referred to as GPTs. Um and nice coincidence for this talk, but general purpose technologies generally have three attributes. They are pervasive. That means they apply across basically all sectors of the economy. The technology can be improved over a long period of time. And the third point is pretty interesting because it means that they have complimentarities. And that means the technology raises the returns in its applications as they improve and as the applications improve that in turn raises the value of the initial technology that helped bring them to life. In other words, uh, general purpose technologies can keep on giving for a really long time for the economy. And an important question that history or future will tell is whether our AI engineering GPT turns out to be a GPT that can achieve this. Well, there's no official list. Um, technologies that are often considered to be general purpose technologies are, for example, the waterhe, steam engine, the railways, electricity, or the computer. Um, and there's a second idea that I just want to briefly mention and keep in the back of your mind, and that's that there's other kinds of technologies that are invented that help us improve how we do research and development going forward. So these innovations can basically help us drive productivity growth going forward. And among these are for example innovations such as the printing press, the microscope, the invention of the corporate or the university research lab which we also obviously see in AI a lot right now or machine learning technology. I think AI has a good claim to be both of these kinds of technologies at the same time. um both a pervasive technology that is unlikely unlikely to saturate quickly and can add economic growth for a long time but also a technology that can be used to improve the process of invention itself and I think over recent weeks especially we've seen that in in mathematics for example and I think that's very exciting for what it can do for living standards because as you can see on this graph on the slide um for the past 150 years is the US economy has basically grown at a stable 2% per year and per capita terms times you see the trend line fits very well. There's periods where growth is faster. There's periods where growth is slower, booms and busts, etc. But on average over 150 years, pretty remarkably stable two years uh 2%. This is a lo axis is a log. So um every linear change basically means a doubling. 2% a year growth um doesn't sound like a lot. If you were going to invest your money and get 2% a year, you'd probably not be terribly excited. But it does a lot when it compounds over a long time. So over the 150 years on this graph or 140 years on this graph, we roughly see income per person in adjusted for inflation, etc. grow by a factor of 10. And to me, it's pretty astounding what it takes to achieve 2% of growth. This was an era 1880 to 2020 of amazing innovation. Basically, all modern technologies that we marvel at today were were invented then. the automobile, aviation, space travel, biotechnologies, the internet, just to name a few. And I think you can fill in the gaps. And in the end, all of this comes together to giving us an average growth in the economy in the US economy of 2% per year. Now, AI might do two things. Um, firstly, it might support this trend so that it can keep going for a longer time. And I think that's already a great achievement because we can see what level of tech technological innovation it takes to just sustain 2% per year. But um and excitingly it might also accelerate this. There is not really consensus right now in economists um of the magnitude of what we might expect this uh graph to look like going forward. and estimates range from as little as a 0.1 percentage point increase of additional GPT above trend um per year. But there's also models of economists that take into account recursive self-improvement, some sort of intelligence explosion in AI that arrive at the possibility of high singledigit percentage point increases um to what you can see on this chart. And as living standards compound over time, as you can see here, um what new regime of growth we end up in over the next couple of years is really going to make an incredible difference to to living standards. All right. Now, let's turn back into the history. Um and start with the industrial revolution where it all has to start when talking about technology. Um the steam engine is the canonical technological innovation of the industrial revolution. Um in principle it helped divorce the creat
...[middle elided]...
pe so that we can be a fully full stack uh AI company and we're still working hard on advanced model. Uh the science team has never been bigger. Uh there are many things happening on those different fronts. Uh obviously the LLMs remain one of the major use cases that we're actively working on at the moment. Uh and I hope we have uh very interesting things to share uh very soon. Uh thank you so much for being here. Uh I hope you enjoyed the summit. Many people in the team will be here. Uh some of them have uh aren't shirt but otherwise feel free to reach out. Remember that uh we are 1300 but still hiring. So uh also come and say hi and thanks for all the speakers. I want to thank also Jen Aliser and all the Debell team for organizing this and obviously Ralph uh for being our MC tonight. Thank you so much and enjoy. Nice. All right. Thank you, Lilio. Let's give it up one more time for Lilio. Yeah. [applause] Yeah. Absolutely. I think uh it was on on point. I think we should give it up also for Jen uh Ali's there and all the ML team for putting this together. Okay, so I have one sad news. The sad news is that yeah, tonight is over, right? You can go back and relax, etc. But I also have two better news. Okay, so we're going to we're going to come back tomorrow. There are just so many things that we're going to cover tomorrow. You're going to hear from Black Forest Labs. You're going to hear from Nvidia, from so many folks. So, the lineup is going to be extraordinary tomorrow. All right. So, uh who's coming back tomorrow, by the way? I see all of you. Yeah. Okay. So, we'll see you tomorrow. But for tonight, we have a reception at the expo. Okay. So, we can all just slowly go there and um just enjoy, meet people, take the time and and talk to everybody. Some of our speakers are going to be there, some of our sponsors are going to be there. So, please join us all upstairs at the expo and see you in a minute. All right. Thank you so much, guys. You are awesome today. Super.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "ai-economics-macro",
  "signal": 0.15,
  "novelty": 0.2,
  "actionability": 0.05,
  "evidence": 0.3,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Это вступительный кейноут конференции с макроэкономическим разбором AI как 'технологии общего назначения' (аналогия с паровым двигателем) плюс закрывающая PR-речь CEO Mistral про найм — ни одной применимой инженерной техники или воркфлоу нет.",
  "knowledge_units": []
}
```
