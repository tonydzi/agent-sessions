---
session: s_46307f8a
date: 2026-09-20
words: 1857
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_46307f8a` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: SOTA Generative Media Panel — Dumitru Erhan, Shane Gu & Nicole Brichtova, Google DeepMind
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] and welcome back for those on the stream and those those in person. um we take tend to basically take these longer sessions between uh all the sort of mainstage keynotes to reflect on things that um you know are particularly important but like don't have like a significant like sort of launch moments. Today we're very lucky to have people working on Omni and VO Nano Banana like the you know the world's best generative models here with us. Uh, Demetrio, I I I first saw you when you were posting about your office. [laughter] Um, I think you're you're probably number one uh Google Google's number one office influencer at least in in San Francisco. I think you like you like to bike as well. You like to take photos of >> bike here. >> Yeah. Um, but you know, but also you work on video models. >> That's right. >> Um, Shane, I I met you I think at like a dinner. >> Yeah. Um and uh and uh and I I remember you were trying to get me invested in like one of the companies. I forget forget which one. >> Forget about that. [laughter] >> But now but now you're um now you're working on Omni Thinking. Um and and just you know a bunch of other >> Gemini RL. >> Yeah. Yeah. Uh and Nicole also uh the rest of the gen media models uh nano banana and uh all and everything you just launched actually even this week. Uh, >> yeah. We launched some APIs. >> Yeah. Yeah. Yeah. >> And I haven't tried to convince you to invest in anything, but maybe I should. >> I mean, so I try not to be an investor. People just convince me anyway. I'm like just, okay, well, I'm not that rich, but know like you can't not try to invest in some of these things. And, you know, for those of us who are not working at a Frontier Lab, this is the best this closest we'll ever get. Um, so yeah, actually, let's kind of recap since you're closest to it and we just did it, like what was launched this week? What should people go try out? >> Yeah. Um so yesterday we had two launch moments. Uh one of them we launched NanoBanana 2 light uh which is our fastest, cheapest um image model in the nano banana model family. Um and it's better than the original NanoBanana. Um so really for most people um that model replaces what you you know used and love the original Nano Banana for across like generation and editing and it gets really close to the frontier quality of of the kind of mainland bigger models. So that that's really exciting. I think if you look at some of the demos or like things that people have been trying like getting kind of that like 3 second latency just unlocks a whole bunch of things that you can do with like ideation and iteration and it's just really fun and the model's getting to a point where like the quality is really good um where um it you know you can use it for iteration but you can also use some of those outputs as just kind of like ready um production output. So that's really exciting. Um and then second launch we finally um launched the Gemini Omni Flash APIs um that we pre-announced at IO. So thank you for waiting. Um and that you know is the first time that we're making the APIs available for developers and it's basically really exciting kind of video generation and editing and we're pricing it the same as Y31 fast. So we're getting you kind of like really really good quality for a really awesome price hopefully. Um >> yeah, I mean that that's incredible. I'm actually really So when you guys launched Omni for the first time, you also did a podcast uh with Logan who couldn't be here today uh and you added like a sloth uh and and Ramen and all these all these things. I actually really want to do that to our videos. I just didn't have an API for it because obviously I have to automate the whole thing. So thank you for the API. >> Uh that is my favorite use case. Everybody should do that. Um I got a cat which is probably like the most boring of the animals. Um if you don't know what we're talking about, you should look it up. It's very funny. Feurer. um Furer who's um you know on on the team did that. >> Furer is the number one guy you should follow for you should follow ideas on okay what can this thing do? >> Yes. >> Right. >> Yes. He he's he's amazing at that. >> I've tried to get him for the last two years to come to AIE. He hasn't made it yet. He's actually come in person. He just didn't want to speak because he's anonymous. >> I know. >> I I want to say his real name but I can't say his real name. >> No [laughter] no we won't we won't do that to him. But you should really follow him. He's amazing. >> He did all that work. I actually met him uh in the office uh when we did the podcast I think and I didn't realize it was him. So his badge doesn't say Popers. >> Yeah, >> I know. >> So he used to be part of uh Replicate and Replicate had this joke where like everyone was Deep Fates. Deep Fates is this like kind of mysterious character and replicate. Replicate is very cool company and both was part of it. Um, so, okay, one thing I want to get on there before I go into like sort of the the the the sort of omniper is we added cats, we added sloths, very cool, very cute, very fun. >> Uh, what are the, you know, inspire people as to like what are the more sort of workhorse use cases that maybe are not just demos, you know? >> Yeah. So, so obviously the hero capability of the model or maybe there's two like one is the ability to kind of take in anything as input and then get video on the other side. Obviously in the future and and we've kind of talked about this as a pre-announce like we want to get the other output modalities out as well but basically what that means is you know you can take a set of images that you have as maybe a storyboard. You can take like an audio track as a reference of you know like a voice that you want a character to speak and then you can get a video on the other side. So like that just unlocks a whole bunch of things that you can do in like you know short film production or you know shorts we'v
...[middle elided]...
ause we don't you know we don't use the models for those tasks >> or like um you know I think to your point about ad campaigns or whatever like people have like notions of brand languages or whatever like which is >> yes >> like a a bunch of images or PDFs saying things you know it's a pretty kind of you know ambiguous question as well what is the IKEA brand language you know is it is it blue and yellow I mean that's that's not a very like >> but like what shade of blue you know. >> Yeah. Yeah. Yeah. So there there's like, you know, and the brands are pretty spec, you know, pretty, you know, like they they do care about the shade of blue. It's not shouldn't just be a random blue and a random yellow. That's not going to be IKEA, right? I'm just thinking about an example. But like this is the kind of stuff that, you know, it's not necessarily part of our like, you know, developing frontier models kind of, you know, necessarily mandate, but it's something that we do want to we do want to fundamentally like build products that people will use to solve concrete tasks, not just not just research artifacts, right? So I think it's useful to understand what people do care about. Uh well, I'm sure a lot of people are very grateful for your work and there's a lot more to do that you've made so much progress over the last like even just couple years of like Nano Banana and Theo and Omni and uh I don't know what else you got cooking but we're very excited like you this is one of those things where like I was very disappointed you know when Sora shut down and and I think like there needs to be more general exploration of uh you know generative models and not just you know coding. [laughter] I think I think that is >> we obviously like this. >> We love coding. Love coding and and uh yes uh but thank you so much for your time. Uh it's been a real pleasure and I can't wait to see what this looks like next. >> Thank you for having us. Great question. >> Thank you everyone. [applause]

---

**Claude:**

{"is_ad": false, "is_news_rehash": true, "topic": "gen-media-launch-panel", "signal": 0.1, "novelty": 0.05, "actionability": 0.05, "evidence": 0.1, "durability": 0.1, "volatility": "volatile", "half_life_days": 60, "why": "Это неструктурированная светская панель-анонс (Nano Banana 2, Gemini Omni Flash API) без методик, чисел или воспроизводимых техник — почти чистый хайп-рехэш релиза.", "knowledge_units": []}
