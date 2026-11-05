---
session: s_898647f0
date: 2026-10-01
words: 1723
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_898647f0` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Anthropic employees are quitting due to safety concerns
CHANNEL: Theo - t3.gg (lang=en)
TRANSCRIPT SAMPLE:
It's been a bit since we talked about the existential risk that AI represents to the world. As great as it is at writing code and helping us with our day-to-day work, it does also have the potential to kind of just ruin everything if we're not really careful with it. In particular, if we're not careful about how it works and thinks, and most importantly, how well aligned it is with our interests and needs, it's possible that it could work around us and circumvent all of the safeguards we put in, potentially taking over the world and destroying us in the process. I know it sounds extreme because it kind of is. A lot of the people talking about this have went to such crazy doomsday perspectives that it's almost impossible to listen to them and take it seriously. At the same time though, there is a very real risk here, and I've talked about this many times before. In particular, on the safety side when it comes to things like hacking and exploiting software. It's not like the employees at these companies are evil though. Just because the risk exists doesn't mean the people working on it are trying to destroy the world. That said, if the risks were there, and importantly, if they were getting worse, wouldn't we see some notable people starting to leave in outrage? Well, that's why we're here today because Jacob Coxon, who used to be a head researcher at OpenAI, that left to Anthropic specifically because of his concerns around safety, has just left Anthropic claiming that they are also not pursuing safety properly. I'll be frank with y'all. This is terrifying and the risk associated is incredibly real. This post just came out a few hours ago and it's already at almost 4 million views and a truly insane amount of engagement. There's a lot of layers to this one and I'm going to do my best to cover all of it. But since AI hasn't cured my hand yet, I have some medical bills, so I hope you can forgive me for a real quick sponsor break. Believe it or not, most of my sponsors have built products that I actually genuinely use and recommend to people in my day-to-day life. Very few of them have built something that I use thousands of times a day and even fewer have built something that has saved me years of time. I'm not exaggerating here. Today's sponsor has saved me years and they'll probably save you a lot of time too if you haven't signed up yet. Hopefully I have your attention now because Blacksmith deserves it. These guys will make your CI so much faster that you'll be frustrated you didn't sign up before. I know that was the case for me. When I watched our build times go from 10 minutes to under four, I was blown away. They do this with their best-in-class infrastructure. It turns out that server CPUs aren't great for a lot of our CI work because it's so bottlenecked on single threads that a gaming processor with less multi-core performance but way better single-core performance helps a ton with our build times. The cache goes even further here by co-locating the cached artifacts on an NVMe drive in the same network and region. They're able to make your cache downloads absurdly faster. And if you're using Docker, it goes even further up to 40 times faster than existing solutions. Their observability is best-in-class. You can actually see what's going on in your CI, what's fast, what's slow, what's succeeding, what's failing, what's noisy, what's annoying, what's using all your resources, and more. And all of this is enough of a reason to move. You should be convinced by now. If you're not yet convinced, let me introduce you to Code Smith. Turns out their infra's pretty good at running your code. Now you can have it run your agents, too. Code Smith's default demo is to find what the right size of runners are for all of your existing actions. And when I ran it, it found a bunch of genuinely useful stuff. I was blown away with the depth of recommendations that it made and ended up merging it, saving even more time and money on my real-world CI for T3 Code. You can go look at the PR yourself if you're curious. I actually merged it. I had another thread here that I'd forgotten about where it made a PR speeding up my CI even more, and another agent ended up auto-merging it cuz it was such a good fix. Make your team faster in every single way at soddev.link/blacksmith. Good to have you back. Let's start by going through the thread and then see what others have had to say as well as the history that led to this happening. There's some fun stuff with OpenAI models and how they might be getting more dangerous that I'll keep to the end, which should be quite fun. But first, let's start with what Jacob said. I resigned from Anthropic today. I spent the last three years doing pre-training research at both OpenAI and Anthropic. Neither company is acting responsibly. This is a pretty bold statement coming from anyone, especially somebody who's worked at both companies. Fun fact about Anthropic that I feel like many people miss about how the company started. The original Anthropic team was actually already working together before Anthropic because they were working together at OpenAI as the pre-training team. They were the ones that did the pre-training for GPT-3 and 3.5, and when they weren't happy with the direction of OpenAI, they left to form Anthropic. The incentive behind those original researchers leaving OpenAI is still kind of debated, but if you ask any of them, they'll almost all say it was around safety. There are some cultural differences there, too, where a lot of them were from the research field, and they didn't like that their bosses were Greg Brockman and Sam Altman, both of which were engineers, not researchers, and that shift in the culture definitely caused some issues there. But, to this day, Anthropic is still ahead of OpenAI in pre-training specifically, largely due to the original pre-training team leaving and becoming Anthropic. There are layers to that that affect post-training as w
...[middle elided]...
 the time. Things are moving fast. It's crazy how much faster they're going and that's because AI itself is being used to improve AI and accelerate the teams. And if we don't make sure we do it safely, we may never get to in the future because this actually could wipe us all out. Huge shout out to Jacob, by the way. This is such a scary thing to do. Not just to make a public statement like this, but also to leave Anthropic right before IPO, potentially throwing away tens if not hundreds of millions of dollars, and to burn all the relationships he probably has with all of his friends and peers in the past. And of course, the real legal risk alongside this of these companies going after him for making their lives harder. Like, there are so many risks and dangers that Jacob's taking on by posting this thread that I just wanted to give him massive credit for it. I think it is incredibly ballsy, absurdly ballsy beyond words, and deserves the respect that I see him getting right now. And I hope that respect continues because this is a scary thing to put out there and I think it's awesome that he did it. This conversation's one we're going to have to keep having over time and it's probably going to get way more intense before it eases up. Things are scary and we should be paying attention to this stuff. If we don't get alignment right, we won't be able to in the future. This is not a thing we can ship fast and fix later. It's a thing we need to do correct the first try and the dangers are real and we need to stop pretending they aren't. I don't have much else to say here. Shout out to Jacob once again for putting this out there. I think it is incredibly scary, but also incredibly important. And yeah, thank you for that. It got me to come up here and film this and I'll do everything I can to try and make people aware of these risks going forward. Let me know what you guys feel about this. Am I massively overreacting or are these risks real? And until next time, peace nerds.

---

**Claude:**

{"is_ad": true, "is_news_rehash": true, "topic": "ai-safety-drama", "signal": 0.1, "novelty": 0.05, "actionability": 0.02, "evidence": 0.1, "durability": 0.1, "volatility": "volatile", "half_life_days": 30, "why": "Это реакция на уход сотрудника Anthropic с жирной рекламной вставкой спонсора, без переносимых практических знаний для инженера.", "knowledge_units": []}
