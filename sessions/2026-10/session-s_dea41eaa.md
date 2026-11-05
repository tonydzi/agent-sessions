---
session: s_dea41eaa
date: 2026-10-01
words: 2020
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_dea41eaa` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Inside OpenAI DevDay: Superhuman Computer Use, Decisions API, and the AI Cloud — Ari & Nikunj
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
that now computer use is like faster at accomplishing tasks than like the average human probably in in most cases. Um, and I think that the next frontier is to have computer use be like literally superhuman in its performance where it actually is as fast or faster at using software than like expert computer users like us. Um, and I think that'll be really consequential and exciting when that happens because I think we'll be able to all of a sudden build products um that um provide just much more realtime experiences. >> Like 4 weeks ago, this was not at all. No, this is like Jev inspired and like >> I think you're officially the first Frontier Lab to like clone adopt this. >> Yeah. Yeah. I I feel like OpenAI has such a strong like hacker culture and like people are just like they get excited about things and so uh guy from inference this one awesome guy from uh the infra team are like uh this is amazing we're going to like hack on it. They build a prototype. It like works and now we we're just like hill climbing on latency and trying to make this as fast as possible and we want to like launch it in the coming days. Uh so as soon as we hit our like latency target, we we'll try to get this out. >> Okay, we're very excited to be here. Today is OpenAI dev day special after podcast. We have Ari here who leads the product and engineering team for computer use agents. Before we kick in and dive deep on computer use, you want to give a quick recap what was announced? What's the quick slew of announcements you guys had today? >> Yeah. Um, yeah, it was a super exciting day. Um, we just got out of the keynote. It was really sick. Um, there were a bunch of computer use announcements that I think are worth thinking about. We have, uh, dots, um, which is the new, um, sort of personal assistant product and, um, that has some really exciting computer use features. There's GPD 6.1 Soul, which is this amazing new model, um, that I think is particularly great for computer use because of, um, sort of the cost and and speed uh, advantages. I think I think we shared that it's um a fifth of the cost as Astra and a seventh of the cost if you're looking at computer use specifically um which is really amazing. Uh sorry there were so many things I'm trying to sort through it >> and the API agents API which now has computer use in it which is really cool because now developers can build on the same computer use uh that is is part of codeex um and and chatbt. Um, and then there were some demos of our existing computer use features like app shot where you can take the context of something you're doing on your computer and bring it into codeex and chatbt really fast. And um, and then like native computer use on your Mac where Roman had it taking screenshots of his app automatically and he could do other things on his computer while computer use was using his applications. Um, so yeah, really exciting keynote >> and not to mention this decisions API. decisions API >> uh off the bat are they all the same model like this is or the same data set distilled to different models um like basically like is computer using decisions API or are they like kind of separate so what's really cool about the decisions API is it you know it it has all these new capabilities it does inference in parallel um it doesn't have reasoning it's a smaller model um than the ones we use for computer use um and so those those capabilities make it really fast. Um they also make it a little bit less good at doing like long horizon um sort of sophisticated tasks. And so I think it's I would say it's still an open area of research for how we like bring those approaches together. But uh yeah, I'm really excited to see what people build with the decisions API. >> One of the interesting things is dots now have attached personal computers. So it seems like they're very much more persistent. You've been using them for a while. How should people push the bounds? It's like what should people aim for? What should they try? Personally, right now I use it for a lot of customer service like oh this was wrong. I don't want to sign in. I don't want to authenticate. Find whatever and just get it fixed. How how should we push further? What should people try? Dots are really cool product because each dot >> has access to its own Linux virtual computer in the cloud. Um which is different from our other products. Um, you know, traditionally we've have access to a browser in the cloud or it has access to your own computer, but now you get your own entire Linux computer in the cloud and so it can run full desktop applications. Um, and it can also use a web browser. And so yeah, you know, I think the powerful thing about computer use and the reason why I think it's so uh exciting is because it makes it so that the agent can do anything you as a as a person can do. Um, because all the software in the world was designed for humans and now agents can use that same software uh and you can delegate to the agent. So, um, yeah, like anything that you would do on a computer, you can ask a dot to do. Yeah, I think what particularly useful is going to really depend on who the end user is and what what's valuable in their life. Um, but yeah, I would just start by thinking about like what are the things that you spend time on and how could you delegate those to an agent? >> Yeah, a lot of flight booking and shopping and honestly even like playing a game or whatever, right? >> Totally. Um, yeah, I don't know. for me. Um, something I did recently, um, I've been working on I I've, um, subscribed to a meal prep service cuz I was trying to like eat healthy, you know, and I really like this meal prep service I found because it lets me customize the meals I order to like a high degree of granularity. So, I can say like, I want this many grams of chicken and this many grams of of of rice. Um, but it was so complicated, it took me two hours to do an order. And I found that I could ask computer 
...[middle elided]...
 the platform is concerned? >> We're obviously like very low level like I I used to work at Stripe before this and uh at Stripe a lot of the game was like building these higher level primitives and products on top of like the core payments primitives. Um, and uh, I'm always like curious about what the best way of doing that is in in AI. And I think we've had a couple of attempts at that. We like had launched assistance API like way back in the day and like wasn't really the right fit. We're sort of like going off with this like agents API and uh, it gives you the CEX harness, but like where's like the the what's the right amount of flexibility to give in that? That's like an open question. like how should we like have memory vaults and like all of these like higher level like API objects to to take away or so like to to abstract away more um like storage concepts like this is like a whole like uh there's a whole space that I'm like very curious about figuring out how we design um I think a lot of things in AI are just have a low-level API primitive and see an example harness and go and have your coding agent implement that but how much that to be built into the the API is like a constant question that I'm thinking about. Um >> so I don't know if folks have thoughts on that. If uh if anyone has ideas uh uh it'll be super interesting to hear. >> Yeah, the analogy I always bring back to and to end there is uh you're building an AI cloud, right? Like which is something that uh Sam said a year ago and you're it's almost like you're sort of doing the AWS invention and you have to do okay this is EC2 and this is S3 and this is like but you're doing the AI native versions of each of these. There are a lot of analogies. So, you're pre-warming caches for stuff that you know >> will and it's nice that it's all exposed to builders cuz it just opens up ways that you can build new things. >> Yeah, absolutely. >> Okay, >> awesome. Well, everything. Thank you guys. Thank you. Yeah.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": true,
  "topic": "computer-use-agents",
  "signal": 0.35,
  "novelty": 0.3,
  "actionability": 0.25,
  "evidence": 0.3,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это по сути пересказ анонсов OpenAI DevDay (computer use, Decisions API, dots) от их же продакт-менеджера с минимумом переносимых инженерных деталей, а не разбор архитектуры или практик.",
  "knowledge_units": [
    {
      "claim": "Decisions API — это отдельная, меньшая модель без reasoning, которая делает параллельный инференс и поэтому быстрее, но хуже справляется с длинными сложными задачами по сравнению с полноценными computer-use моделями.",
      "type": "tool-caveat",
      "actionable": "Для задач типа быстрой маршрутизации/UI-решений в агенте используйте лёгкую не-reasoning модель, а для многошаговых сложных сценариев computer use — полноценную reasoning-модель; не ждите от Decisions API long-horizon качества."
    },
    {
      "claim": "Computer-use агенты OpenAI (например dots) получают доступ к полноценной Linux-машине в облаке, а не только к браузеру, что позволяет запускать десктопные приложения, а не только веб-сайты.",
      "type": "principle",
      "actionable": "При проектировании агента с computer use закладывайте архитектуру с полноценной виртуальной машиной (а не headless-браузером), если нужен доступ к нативным десктопным приложениям."
    },
    {
      "claim": "По словам спикера, GPT-5.1 (упомянут как '6.1 Soul' в расшифровке) для computer use стоит примерно в 5 раз дешевле Atlas и в 7 раз дешевле специально для сценариев computer use.",
      "type": "benchmark",
      "actionable": "При выборе модели для computer-use агента сравнивайте не только качество, но и удельную стоимость на задачу — разница может быть кратной между моделями одного вендора."
    }
  ]
}
```
