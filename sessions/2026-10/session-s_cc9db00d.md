---
session: s_cc9db00d
date: 2026-10-01
words: 1930
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_cc9db00d` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Please stop using stupid models
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
If you enjoy the videos where everyone calls me a paid shill, you're going to love this one because I kind of have to glaze for a second because I see some comments that are just so dumb that it makes me realize the majority of engineers just aren't using agents right at all. And I mean that when I say it. I'm inspired to make this video because of a post from another engineer that I generally quite respect, but is so dumb that I need to talk to you guys about it because I know a lot of y'all feel the same way and you feel it so deeply that you accuse me of being a shill because of how deep my feelings here go. The take is as follows. From Brandt Cramer, aka Zeeg, the founder of Sentry, "Everyone using Fable or Astra, which is most of us on subs because no one can afford it, should try switching back to the other high-reasoning models like Opus and Soul. You'll likely realize your tasks don't perform any differently." To which I responded, "This is your worst take of all time, which is kind of crazy. Cramer's had some wild ones in the past. And I genuinely believe you suck at prompting if you believe this." So, if what Cramer just said resonates with you, if you actually think or have experienced going back a model gen or down a model tier and not notice a difference in the way you do work, you also suck at prompting. And this isn't like a disprovable thing the other way where you can't prove I'm wrong cuz there is literally no way to do that, but I can very easily prove you're wrong, which is what I'm really excited to do right after a quick break for today's sponsor. I have a challenge for you. Next time you're reviewing a big PR and you're not sure if it's ready to go or not, ask your agent on your machine to pull it down, play with it, test it, and make sure everything works as expected. There's a good chance it's going to find things that both you and your agents wouldn't have otherwise because if you're just looking at the code, you're not going to be able to find too much. This is a mistake that a lot of the AI code review bots make. They think they can know everything and how it works just by reading the code. And reality is not that simple. Code breaks in ways that are not clearly visible just from reading code. This is why I think Trex by Grapple is so damn cool. These guys realize that agents know a lot more about code when they can actually run it than they can possibly guess by just staring at it. And that's why Trex uses sandboxes to actually test your changes before leaving review comments. Grapple already has a best in class system for understanding the context of changes because they know your whole code base, they monitor it closely, and they've indexed the hell out of it in order to make good insights happen. But now they can also test the code, which makes it so much more powerful. And this goes so much further than just letting the reviewer run in a sandbox. It's actually kind of the opposite. It's more that the reviewer orchestrator can spin up and run sandboxes with sub-agents for whatever theories it has about what might be wrong. Some reviews might need no sandboxes, some reviews might need 10. The orchestrator will figure out what is needed to verify your changes. This helps you ship with way more confidence, and not just cuz it gives you a thumbs up or thumbs down, but because it will respond with images and videos of the things it tests. So, if you want to make sure that your drop-down disappears correctly or that the sign-up flow works end to end, a simple approval message should not be enough. A video proving the changes worked is so much more valuable if you're trying to ship with confidence. We all know coding agents work way better if they have a real computer. Turns out review agents do as well. Get your review agents the support that they need at soidev.link/grapple. Let's just break this down piece by piece because if I do the whole thing at once, people are going to read into the parts I don't focus on and say that's why I'm wrong. So, let's start with a thing that I just want to get out there right now. The Astra and Soul portion is very different from the Fable versus Opus and Soul portion here. Astra can do things no other model in history could. It is incredible, but it can also screw up in ways I haven't seen since I last was using a Gemini model seriously, which was like 2025. So, if your feeling here is purely around Astra because yes, sometimes it does incredible things, but sometimes it does weird or annoying things. Then I see why going back to Soul would feel not even not bad, but in some real cases somewhat good. And I understand people will be moving from Astra to Soul. So, I'm jumping in that one immediately because I know people will be feeling that and I get it. I even have a diagram. Let me find it. Here it is. This diagram was meant to show roughly how I feel about the quality of responses over a large set of responses with Fable and Astra. Astra at its best can do things Fable never could. Astra at its worst makes me question why I'm using AI to code at all cuz it can make some real [ __ ] dumb decisions and assumptions. Generally speaking though, one of the benefits you get from these frontier models is that the gap between the worst and the best gets closed and the floor goes up. Actually, I think this diagram's a really good starting point for the things I want to try and communicate here. Generally speaking, y'all focus too much on the high points with models and not enough on the lows. And I'll be real, both of these assumptions have gotten me in trouble. There were times where I focused too much on what the best looked like for a model, things like Opus 5, and I thought it was really good when it wasn't and it misbehaved far more often than I had known at the time. And then there's times where I focus on how pathetic the model behaves sometimes and just ignore it outright after that even though there are real strengths. I would
...[middle elided]...
still prompting like we're in February. And the reason why they're doing that is they're not valuing their time properly. They feel good putting that extra effort in at the start and the end because as a great dev before, the thing that got you to level up, the thing that got you from a good contributor to a good leader was doing more of the prep before the code started and doing more of the vetting after. So, it's even more uncomfortable to give that up to the agent. So, the parties I see falling for this are the ones whose work isn't serious enough to realize the power of the models, but even more so, it's the incredibly talented leaders who have largely left behind coding in their day-to-day because the thing before and after the code writing matters more. They struggled to give up the code in the middle, but they did. They won't give up the things on the other side yet, which is why they don't see the benefit. They're testing the models against the thing they already stopped doing, and the models have been able to do the thing they stopped doing for 6 months. They're correct there. But the moment you let the model go a little further in either direction, you'll suddenly start to see the edges a hell of a lot closer. So, as per your request, Zig, I will stick to making videos because otherwise, your stupid takes going to go too far, and I need to make sure the next generation of devs who haven't fallen for this [ __ ] don't. Because what you're saying sounds good, and we want to believe it. I want to believe it. I would love to not have to spend more money on my models, but I do because my time is more valuable than my [ __ ] posts. And I hope you realize the same soon, too. I hope you enjoyed this video, Zeig, and if anybody else happens to see it, maybe you'll like it, too. Let me know how you feel about this one and how wide your prompts have been, and if you think I'm crazy for not including file names in my prompts anymore. And until next time, peace, nerds.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "model-choice-prompting",
  "signal": 0.3,
  "novelty": 0.2,
  "actionability": 0.3,
  "evidence": 0.2,
  "durability": 0.25,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "В основном это личный спор с чужим твитом про то, 'топовая модель не лучше', без бенчмарков — ценность только в паре практических советов по ревью PR и стилю промптинга, зарытых в хайповой ругани.",
  "knowledge_units": [
    {
      "claim": "Перед слиянием большого PR полезно попросить агента скачать ветку, реально запустить и протестировать изменения end-to-end, а не только прочитать диф — баги часто не видны по одному коду.",
      "type": "workflow",
      "actionable": "Добавь в процесс ревью шаг: агент локально поднимает PR, гоняет сценарии и присылает доказательства (видео/скриншоты), а не просто текстовый approve."
    },
    {
      "claim": "Автор утверждает, что с топовыми моделями (Opus/Astra) больше не нужно писать узкие промпты с явным указанием имён файлов — выгоднее давать более широкий контекст и доверять модели самой разобраться.",
      "type": "tactic",
      "actionable": "Попробуй на своих задачах расширить промпт (меньше микроменеджмента по файлам) и сравни качество ответа фронтир-модели против привычного узкого стиля — это субъективное наблюдение автора, а не доказанный бенчмарк."
    }
  ]
}
```
