---
session: s_916a3ea3
date: 2026-09-20
words: 1758
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_916a3ea3` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: A Worm With 302 Neurons Inspired Their Architecture — Ramin Hasani, Liquid AI
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
[music] Okay, we're in a remote studio with our new head of editorial, Richard. Say hi. [laughter] >> Hi, everyone. >> Dialing in from the UK. And Raine, uh, CEO of Liquid. Welcome. >> Thanks for having me. >> Most people when they've heard about Liquid, they they they know about LFM or they've heard of LFS. They maybe haven't personally tried it. The other interesting I guess public data point is that it is very inspired by worm DNA or something. I never really pay much attention to that because obviously I think that that's an analogy but you can tell us how seriously to take it. >> Yeah, absolutely. Well, you know like when we when we started uh our kind of research about 12 years ago, we wanted to see if we can bring inspirations from brains back to machine learning. So that's that's where everything got started. And then when we started looking into human brain, we realized like when I say we, my current CTO and myself, we started back in Vienna University of Technology. It's called TUNI. And then so I started my PhD. My co-founder was the a master student there. And then what we wanted to do, we wanted to understand how we can um bring in like continuous time math inside machine learning kind of system. And that's what we did. So so we we basically look into neurons, how neurons exchange information with each other. And then um this was governed by very simplistic f first order differential equations and that's that's kind of how how the nervous system dynamics are actually working at the level of curve neurons and synapses and then uh our first focus we wanted to start with human brain but human brain has like a spiking neurons and and it's very difficult to actually learn like we still don't know anything about human brain how how competition actually happens. We know a lot more uh now about a fruit flies brain but we don't know that much about human brain but uh but I can tell you that um we got to this animal because we wanted to do it first principles we we got to this animal C elegance worm which has uh only 302 nerve cells in its body and it's like it has like two it's 2 mm long and uh one of the nice thing about the worm was the fact that its neurons behave very similar to artificial neurons they don't they don't spike You know, so that graded kind of behavior in these neurons of this animal, the it's called in in neuroscience they call it electroonic behavior of a neuron. You know, like the neurons do not spike. And that behavior was very very interesting for us because if you build systems inspired by the brain of this worm, you would be able to build like very continuous time kind of systems and they're differentiable. So you can you can do back prop and all sort of other things on top of these things. This was this was the model organism that we were looking at at that time. The most fascinating thing for us was that with 302 neurons it could control 95 muscle cells better than any robotic systems that we had on the planet you know and this is 2016 and 2017. So then we thought that okay so and also another thing another interesting thing about the worm is the fact that 600 million years ago we got a split humans actually got split from this worm in the tree of evolution you know so it's actually like whatever whatever neuroscientists are discovering about the brain of this worm or the cell structure of this worm is actually transferable like to to humans as well to some extent 78% similarity to human genome you know so it is actually a very very important uh uh worm for us and so far it has won four nobel prices for humanity, you know. So, like you can imagine like scientists are really lucky to study this animal. So, it's a very very popular animal, you know, and um and that's why like that's our our research. We started even working with neuroscientists, you know, themselves that are working on this uh brain of these neurons. So, long story short, we mathematically modeled how two neurons exchange information based on the inspirations that we know and the things that we know about the brain of the worm. And then we got those mathematics and we built something called liquid neural networks. liquid time constant neural networks. Liquid was like basic liquid for flexibility because one of the things that we realized is that these are highly nonlinear systems governed by differential equations in a forward pass and they are differentiable. So you can actually run them backward pass and you can basically learn them like really nicely because of the multiple feedback structures that they had. They are really representation learners you know like they learn representation from data really really well. One of the things that we realized is that with a small kind of subset of these neural networks, you can control robots like you know very similar to how the the worm itself was doing it and uh when I say small subset we were talking about tens to hundreds of neurons you know like we talking about very very small subset of neurons and then we we we got very excited so we started applying these things to controlling robots on the robot you don't have that much compute so you bring like int the fact that you can actually pack that much intelligence to control autonomously a kind behavior inside a robot that was like a very attractive feature for us. So efficiency of this uh computation and bringing intelligence into like smallest kind of unit of compute that has always became kind of a a kind of research topic for us and then uh 2017 um professor Daniela Roose of MIT cell so she's she's my uh so she she reached out to my professor in Vienna and then she's one of my co-founders as well. She's the mother of robotics arguably. So you know she's like she has done tremendous contribution to the field of robotics and distributed robots and soft robots as a whole. She started learning about our research and then she she was like blown away and she said okay you guys would you guys consi
...[middle elided]...
think I think it will be a long time that we will be living with attent attention based system. So attention is definitely going to be inside like any of the it's like you know how how do you see you know how do you see how how's your eyes are working you know but you you need your body is uh I I randomly noticed like uh actually you're not seeing the whole view your eyes are just bouncing around all the time and your brain is compositing right yes you you see the difference between two frames by the way this is what you see so it's basically you see the differential oh left and right eye no like you're you're basically the the way that humans see you don't see one frame You see two fra the difference of two frames. >> I need to go look at look this one up. Look this one up. >> So so attention is is one component. >> Attention is definitely one component. But then again >> hardware awareness customization. Yeah. >> Embodiment like there's another there another aspect of so I would say like intelligence that wants to get deployed in the society outside of data centers you got to have like some sort of embodiment. agents that are actually inside the virtual world, they have also an understanding of their virtual physical kind of environments that they are operating in, you know. So embodiment is also true for virtual agents by the way. So you know, so you got to you got to have like those kind of aspects in there. So embodied intelligence and em embodied reasoning is like some something is very important. And then adaptive intelligence is another another level that we we really want to add. Is that routing related or what do you mean by adaptive? Oh, adaptive I mean like systems that can always evolve like continual learning, continuously kind of improving systems. Yeah. >> Okay. Well, uh that was a a really good deep dive. Uh is there anything that we should have asked you that we didn't cover? >> No, I think that was a great great session. Thank you so much. [music]

---

**Claude:**

{"is_ad": false, "is_news_rehash": false, "topic": "liquid-neural-networks", "signal": 0.25, "novelty": 0.2, "actionability": 0.1, "evidence": 0.35, "durability": 0.5, "volatility": "medium", "half_life_days": 365, "why": "Это founder-стори про биологическое вдохновение LFM/liquid networks — интересный контекст компании, но без конкретных цифр архитектуры, кода или воспроизводимого метода, который инженер мог бы применить у себя.", "knowledge_units": []}
