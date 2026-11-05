---
session: s_2107676e
date: 2026-09-26
words: 1725
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-26 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2107676e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Fixing the PR Bottleneck — Matt Pocock, AIHero
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
All right, I'm here to talk about fixing the PR bottleneck. And this is kind of a grand title for trying to fix the thing that most organizations struggle with, I think, and have kind of historically struggled with before AI. You know, we have always had huge numbers of PRs just laying around that no one's bothered to review. And this has now increased massively because of the new strains on us because of AI imposing all these weird constraints. And to do this, I'm going to use the rubric of my skills, which is you've kind of heard about, maybe you've used them. And I have a couple of new skills to announce that are going to hopefully improve the way that you do PRs, improve the way that or improve the speed at which you can review them and do them. Speed. Now, we're being pushed to do more with less essentially or more PRs, more work, more stuff. And this is kind of the central promise of AI that we're going to be able to use these agents to scale ourselves up to do more work. And this has resulted in the software factory, probably the biggest buzzword of the day. Everyone's talking about software factory that I chat to. And I think of a software factory as primarily something where instead of the human initiating all of this work, we're going to pass some of that initiation, some of the initiation is going to be done by agents. And I think of there. Maybe from there you have a classifier like Jev come in and say, "Okay, let's turn that into a fix or turn that into a reproduction." Or maybe I ping people straight away. And maybe you have other things. Maybe you have planet scale hooked up. So it gives you query reports on the slow queries on your database. Maybe that then triggers a different um thing of your software factory. All of this is not humans triggering it. It's uh deterministic code triggering it, right? And so these accelerate your software factory. They push more code through it. But then you need brakes, right? If you just have permanent acceleration pushing stuff through your factory, you're going to end up with a slop cannon, right? You're just going to end up with a ton of slop crappy PRs that you're not going to be able to touch or review or even freaking look at. So, you need breaks. And if you have bad code in your codebase, that is going to be more bad code. And so I'm going to talk about these three breaks in this talk and talk about how we can use them to counterintuitively go faster. So automated checks, these are the deterministic checks in your repo that we've had for thousands of years or you know since the 50s. Deterministic checks where we have linting and tests and type checking and code quality metrics. All of these things going together and they all work the same every time. Layered on top of that we have automated review. So we have agents who look at our code and say okay you know these are for the things that the tests didn't catch or this is looking at the structure of the codebase in general and then on top of that the third layer the final layer is human review so people looking at the PR and these three layers form this kind of cake that we end up with when we get to human review and so more speed of course means more PRs and so the goal here is to make human review faster by leaning on those first two phases. And we got to stop the slop. That's the first principle here, which is if you raise the quality of the code that you're shipping, you're going to end up doing less human review because it's just going to be better work. And so you're going to end up needing to uh make fewer interventions. So automated checks. Now, automated checks are cheap. That's the cool thing about them is that they don't cost tokens like automated review does. They don't cost human effort. They just cost CPU cycles. So these are for instance you know you run your tests on every code change. Maybe those tests do incur some tokens because let's say um an agent uh creates a bug and the tests catch it then you need to spend some tokens to go and fix it but those are tokens pretty well spent in my opinion. So checks are cheap. That means you can layer on loads and loads and loads of them on your repos and you're probably not using enough of them or not being creative enough with your use. But checks can lie. Does a green CI mean that the code is ready for merge? No, it does not. And so we've always needed on top of these checks some extra layer to figure out if there's anything catastrophically wrong with the code before we ship it. And so all of the other phases, the human review and automated review, these are lie detectors. These are for finding lies in the automated checks. Now I want to show you some of these lies first of all because this helps when we're thinking about code and thinking about automated checks to see how bad it is and how bad things can get. The first is tortological tests. A test that just reasserts the implementation. Opus 5 got addicted to these. I don't quite understand why it would have for instance x post character limit equals 280. Can anyone guess the test that was written to test this behavior? Right? You've probably seen this a thousand times. This is real code from agents or from stuff that I found my agents doing. It said expect x post character limit to be 280. So the implementation looked like that and the test essentially reasserted the implementation. That is a tortological test and tortological tests are bad because they're extremely structure sensitive. They're very sensitive to the actual internal workings of the system. So it means I cannot change that constant without a test failing but I cannot rename that constant without a test failing like I have to do is so tied into the structure of my system. And I found another one which is even more egregious. I would say this is incredible uh test. What it's doing here is it's essentially testing whether two things in the UI appear in the right order. So it's checking that the pitch detail
...[middle elided]...
ew skill. This is called retro. Retro for retrospective. You essentially take a session that you've done. It can either be like a single um agent session or it can be a PR plus the session or you can just get it to look at okay look at all of the PRs that we've done over the last week. All of the reviews, pull them all in. Let's do a retrospective on them and it will suggest automated checks and coding standards to make the next one better. So this is the compounding effect where you essentially by doing human review you're making the quality of the next human review higher and you're sort of saving less work from yourself next time. And retro is a really smart skill. It adds a bunch of stuff. So obviously it suggests automated checks. It suggests updates to coding standards.md. It does other smart stuff too. So it looks at navigation pointers. How easily did the agent find its information? Can we provide a pointer inside agents.mmd to help it out next time? It looks at tool economy. Are there different tools that we're using in the session that can, you know, could be made more token efficient? It's amazing how many things this catches actually because those are often really hard to debug from the outside. It just looks at bloat as well. So, are there bloated steering files? Are there bloated skills that contribute to these bad results? Can we make them more organized? So that's the goal is to make human review faster. We do that by layering up automated checks. We're layering up automated review. And we make the human review as painless, as simple, and as kind of optional as we need it to. You really don't need to review every single two-way door. Every single oneway door you do. And so these are my skills. Aihero.dev/skills. I'll be shipping version 1.3 this week. It has been glorious hanging out with you. It's been a really nice conference. I'm going to be outside in the lobby if anyone wants to have a chat. Uh, thank you so much for having me. Thank you, Paris.

---

**Claude:**

You've hit your weekly limit · resets 4am (Europe/London)
