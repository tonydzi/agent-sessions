---
session: s_a6c66d89
date: 2026-09-28
words: 1996
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a6c66d89` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: GLM-5.2: Open Weights, Near-Frontier Intelligence — Zixuan Li, Z.ai
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Without further ado, we're going to bring on Zishan for for his keynote if we're all set. Hey, how are you? >> Great I'm here. >> Yes, to the magic of the internet. It's really good to see you again. Zishan has you've been speaking with AI Singapore and obviously GLM is the talk of the town right now. There's been an amazing booth downstairs in the expo and I think a lot of people are just very excited to hear from you on what all is going on with ZIAI. So if you want to take it away. >> Yes, sorry again for not showing up in person, but I have a team whole team coming to the town and we have a booth. So you have any questions, feel free to reach out to me on X link and also you can look for my team on our booth. And since I cannot see my slides, so I will need Swee to help me flip through all the slides for me. Yeah. >> You're good. >> Here Swee, like what which slides we are in right now? >> Yeah, so we're we're on the opening slide. We're talking about intelligence and ZIAI. >> Okay, so yeah, so you can you can see that it's the first time for us to introduce GLM 4.2 5.2 to the world and also we are going to share something about Z.AI and GLM because maybe people will think Z.AI and GLM they're irrelevant, right? You are your company is not G.AI or your model's called Z1 or Z2. And you can find my X and our company's X account here, so you can just search for my name Zishan Lee and the Z A I org. And you can follow them for the follow-ups. So, yeah, we can go to the second slide. Yeah, actually I cannot see the slide, so I'll try to >> So, we we >> Yeah, try to make sure that it is correct. So, the company actually is called Zhipu. Maybe some people have heard of it. And the all the models, it's it's called GLM. Actually, it's not a a brand name, it's a generic term. So, GLM actually represent general language model pre-training with auto-regressive blank filling. And that paper was published back in 2021. So, actually we were the one of the first labs to do explorations on large language models at the same time with OpenAI, and Anthropic, and DeepMind. And even today, we we no longer use GLM as the architecture, we still use the name GLM as our brand name. So, we use GLM 5.1, 5.2, and it become like one of our like most prod uh proddest product and model. And the second thing that we look for is intelligence upper bound. So, in terms of intelligence, we we may feel that it's represent IQ, something something like that. And when Deep Seek launched one 01 launch, people are talking about the model's capability to solve math problems, physics problems. But what actually intelligence mean is not just like IQ or AIME or other other physics problem. So, from GLM 4.5 to GLM 4.7, we are exploring like several things, like reasoning, coding, and agentic capabilities. So, as you can see from the slides, So, we add like Yeah, the last slide. Yeah, we were actually I haven't like finished that slide. Yeah, so Okay. Yeah, need to go back to the two two slides. >> I don't have back I don't have a back button. Thank you. I would you I don't understand clickers that don't have back buttons. Like why Okay, I you know, anyway, go ahead. >> Yeah, never mind. Yeah, because people want to see the GLM 5.2. They they don't want to see you like GLM 4.1 or 5. But like GLM 4.2 actually specialize in coding and genetic task as you can see from the graph because there are a lot of rumors whether your model is close to mythos, fable, but actually I want to share these slides to all of you. So, you can see it's somewhere between Opus 4.7 and 4.8 and we use the hardest problems like Deep Sweep, Terminal Bench 211, which was mentioned by the Open AI team uh several minutes ago. And all the like long horizon task and benchmark shows that the capabilities are on par with at least Opus 4.7 and it it it shows a significant improvements over 1.1. Also, for GLM 1.2, we add a thinking uh level called high. So, because we also noticed as we move to the harder task it may consume more tokens and also we we care a lot about the token efficiency. So, it's the first time we add the high level for thinking budget. But even without thinking, the non-thinking model is better than the 5.1 thinking model. So, I think it's a huge improvement for the open weight model. That's what really impressed the world and why people are talking about GLM 5.2 lately. Okay, the next slide. And one one thing that I want to mention is that GLM is more more than coding model because people use it inside clock code code X, open code. But actually, we have trained a lot of things outside coding. For example, we improve a lot in GDP valve and also math problems. We also care about math problems, frankly speaking. And also, we train a lot of thing uh related to role play, general chat. We want to improve every aspect of the model. So, you can see from the artificial analysis intelligence index actually leads the other open way model a lot and close to the frontier model. So, I want you if you are you haven't experienced GLM yet, you can use GLM to do general chat, use it to process your daily workflow, not just for coding, but you can explore the model like beyond the coding scope. Next slide. And GLM 4.2 is a open weight model. So, people always ask me, "Why do you open weight? So, do you care about your business or like do you care about losing market to some infra suppliers?" But actually, we open the weights for several things because there are users' needs and there are our own needs. If we can meet their needs, I think it's okay. It's definitely okay for us to to open the model. For example, if our users want security and control and we want to build trust, we can open weight model. For for some cases, if enterprise or government especially in the Western world, want to use the model, we open way, we upload to the hugging face so that they can use the model on premise. I think it's very beneficial for the whole ecosystem it to explore the model, e
...[middle elided]...
. Woo! So, that one more thing is we actually have our own harness. The Z code, actually it's built for Geo 5.2, but also support all frontier models. You can bring your own key. You can connect to Z code. Actually, the I think the operation is is similar to Kodak. Actually, you you can try some techniques like go or other like compact technique techniques like what you've done in in Kodak and car code. And this harness is I think it's the perfect one for GLM 102. If you haven't experienced it, you can just search Z code or you can go to our booth. We have our team members showing this harness to you. And welcome to to our booth. And welcome to like talk to me in the future. And next time I'll definitely be in SF talking to everyone. Yeah, thanks. >> Thank you very much. Um So uh trust me, the very first World's Fair, I wasn't allowed to come back in the country for my own conference, so I know exactly this feeling. Uh but it it it's all good. Uh the ZAI team, I really appreciate them uh making the effort. They really want to meet you. They're here to meet you. And this is the whole point of the World's Fair, to bring all the top world's AI uh companies and labs uh all in one place, so you can do business together, uh meet the people behind the models that you use, ask the questions that he cannot answer in public, but you can ask in private. Um I'm also very proud. Uh he showed uh Zhicheng showed that that list of uh Hugging Face uh you know, top uh contributors. I think we are four for eight uh in that list uh present at World's Fair. Uh we're working with Nvidia and Unsloth and Ollama and then uh all those other fine-tuners as well to uh to make our our sort of the inference and the local tracks uh that you're going to see over the next few days. Um with that, thank you so much to Zhicheng. Uh I'm going to invite on uh the next uh couple folks. I think I I I think I might be doing Ali's job here, so uh we'll we'll talk to Hugging Face next and Minimax. Thank you.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": true,
  "topic": "glm-5.2-launch",
  "signal": 0.2,
  "novelty": 0.15,
  "actionability": 0.15,
  "evidence": 0.25,
  "durability": 0.2,
  "volatility": "volatile",
  "half_life_days": 60,
  "why": "Это промо-кинот вендора (Zhipu/Z.ai) про релиз GLM-5.2 с самозаявленными бенчмарками и рекламой их харнесса и буса на конференции — практической методологии для инженера почти нет.",
  "knowledge_units": [
    {
      "claim": "Z.ai открывает веса GLM намеренно ради доверия и on-prem контроля для enterprise и государственных заказчиков, а не только из идеологии открытости",
      "type": "principle",
      "actionable": "Если нужен LLM с self-hosting и полным контролем данных (compliance, security), стоит рассматривать открытые веса GLM как альтернативу закрытым API"
    },
    {
      "claim": "В GLM-5.2 добавлен отдельный уровень мышления 'high' для управления token-бюджетом на сложных задачах, при этом non-thinking режим 5.2 уже сильнее thinking-режима версии 5.1",
      "type": "tool-caveat",
      "actionable": "При выборе режима GLM-5.2 для агентных/долгих задач сначала попробовать non-thinking или средний уровень мышления, прежде чем переключаться на дорогой 'high' режим — это может сэкономить токены без потери качества"
    },
    {
      "claim": "Z.ai выпустила собственный харнесс 'Z code', заточенный под GLM, но поддерживающий и другие frontier-модели через bring-your-own-key, по функциональности похож на Claude Code",
      "type": "tool-caveat",
      "actionable": "Если экспериментируете с GLM-5.2 в агентном режиме, попробовать штатный харнесс Z code вместо адаптации стороннего, так как он может лучше учитывать особенности модели (например, compact-техники)"
    }
  ]
}
```
