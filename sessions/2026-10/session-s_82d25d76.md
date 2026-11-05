---
session: s_82d25d76
date: 2026-10-01
words: 1751
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_82d25d76` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: I think they mean it this time
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
There's been a lot of talk about AI safety stuff lately. From the chaos that is the Chinese distillation of models to the employee Jacob leaving Anthropic due to cited concerns around safety and how he didn't believe even Anthropic was taking it seriously enough. Now things have gone even further. It seems like the pacing the frontier movement has really taken hold inside of the labs and now we see Dario coming back on Twitter for the first time in a bit. I think it's one of his forever tweets and he's posting in order to share a new article he wrote. We must pace the frontier. By itself, this would be very notable and worth at least paying some attention to. But what makes it much more interesting is the fact that everybody from Elon Musk to Sam Altman has cited this and said they agree and it's probably time to do something. I'm particularly interested in this article from Dario because it no longer dances around the big scary questions. Previous attempts to cover this haven't been realistic about where things are at geopolitically in particular with China as well as what these risks actually look like in the real world. I know you'll tend to think Anthropic is blowing all of this out of proportion and exaggerating the issue here, but I think Dario was quite level-headed in his reporting here. I think it's important that we go through this together and try to understand what he's saying. That said, if he is successful, there will be a lot less AI news going on, which would mean I don't have a good place to put my awesome sponsors like today's. Usually when a company sponsors my videos, it's cuz they want to make more money, which is why it's so weird today's sponsor wants me to tell you about how to use them less. I'm thankful this isn't a joke because I saved a bunch of money, too. Today's sponsor is Blacksmith. I've already established that they're the best place to run your GitHub Actions CI and more, but now they also have Code Smith, which lets you run agents on top of that same super fast, super cheap, and reliable infrastructure. What's even cooler is that these agents come with deep knowledge of how your CI works as well as how Blacksmith works. This means you can ask them to do things like right-size your CI runners and it will look through your actual logs and see which jobs used a bunch of CPU and which ones didn't and recommend how to spec things out so you save more money and more time. I ended up merging three real PRs in T3 Code, all of which were filed by Codesmith when I was filming a quick demo. It took less than 5 minutes to shave my already super fast CI times by almost half just by doing the things it said. And that's on top of the 50% plus improvement in performance you'll get just for moving to Blacksmith in the first place. You change one line of code in your existing GitHub action and you're ready to go. If they charged four times more than GitHub actions, I would still think it's worth it. But they actually charge way less. When you combine the price difference and the speed difference, you end up saving 60% or more against what would have been your GitHub action bill. Blacksmith is so fast that I use CI for things I never would have before, and it's letting our team ship faster and more confidently. Figure out why my whole team loves these guys at soiddev.link/blacksmith. Sorry about that one. Got medical bills today. I'm sure you fellow Americans understand. I am excited to cover what Dario has said here as well as how others have responded, but I want to jump on one other thing first. A pattern I've been noticing in these conversations, in particular the conversations about Jacob when he left Anthropic. I've been seeing a ton of crazy conspiracy theories, many of which weren't out yet by the time I published my video. And now that I've seen them, people seem to think that I'm intentionally dodging this political psyop. No, I'm not. You guys are just insane. Seriously, like almost all of the things I've seen people talking about in regards to Jacob's post have been crazy attempts to map like a grant he received in research in 2021 to him quitting a hundred million plus dollar job in order to what? Like it just there there's no link between any of those things. And all of the attempts to like assign what he said and who he's talking to to some weird cabal trying to do something, but nobody can say what the something is or what their goals actually are. And I'm particularly frustrated not because conspiracy theories annoy me, I actually find them quite fun. I'm annoyed because I feel like we're not talking about what Jacob said. Instead, we're talking about who he is and if he's worth even listening to. And the problem is that the two sides aren't sensical. One side thinks what Jacob said is worth listening to and considering, the other side thinks you're insane if you listen to a word that he says, and they're not even engaging with the things he said. We're not debating whether or not AI is safe, we're debating whether or not the conversation can be had. And one side thinks yes, because AI could potentially be really unsafe, and the other side says we cannot have the conversation at all, and if you're trying to have it, you're probably funded by some weird party trying to force their way in the world. No. I'm not funded by anybody. I love AI. If AI slows down, it will hurt me directly. I'm just doing my best to cover this because the people who I know who are the smartest in the world at this are legitimately scared, and many of them are friends of Jacob's, can absolutely vet his capabilities, and agree with what he is saying. Dario seems to be one of those people, which is why I think it's worth listening to what he said here. He shared his blog with the following Twitter post as a starting point. We must pace the frontier. I've written a new essay on why the AI industry should slow down with a three-part plan for doing so. Anthropic is unilaterally committ
...[middle elided]...
important to note that even if we cannot achieve formal agreements, simply changing informal norms may have some value. Sharing information about recursive self-improvement and about the misalignment of models can help convince everyone that it is not in their interests to be reckless. He closes with the following. Dario continues to believe that AI can enormously improve the quality of human life. His desire to achieve these benefits is undimmed, but the benefit will only be achieved if we build the technology in the right way, and so long as we use the time we gain well, it is worth taking unusually deliberate care to get it right. Progress will still be relatively fast, and we can use the time to advance the science of interpretability, improve operational security and rigor at the frontier AI companies, and build models whose alignment we have much more confidence in. Measures that Dario proposes are meant to advance the frontier at a safe pace, and it won't be easy, but he believes we owe it to humanity to try. This is a really, really good essay. And as much as I like to pick on my friends over at Anthropic, and as much as I love to give crap to Dario, this was responsible and well done. It's not alarmist, it's not saying that the AI is going to take off and escape the GPUs and destroy the world. It's a realistic look at where things are at now, where they are probably going, and how we can put a little extra effort up front to make sure it doesn't get really bad. And I think it was worth listening to, and I hope that you enjoyed it. Things are going to get scary fast, and I hope we take the time to reflect on that and do what we can to prevent it. It's important to get these things right because we still can reverse it if it goes wrong, but in the future that might not be the case. Hopefully y'all enjoyed this orange just calling me a page shell on a video that I was only paid for by my sponsors. So, yeah. Hope you enjoyed it and until next time. Peace nerds.

---

**Claude:**

{"is_ad": true, "is_news_rehash": true, "topic": "ai-safety-commentary", "signal": 0.1, "novelty": 0.05, "actionability": 0.05, "evidence": 0.1, "durability": 0.1, "volatility": "volatile", "half_life_days": 30, "why": "Это реакция блогера на эссе Дарио Амодеи про темп развития ИИ плюс длинная рекламная вставка — нет применимых технических знаний для инженера.", "knowledge_units": []}
