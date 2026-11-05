---
session: s_98d8a34e
date: 2026-09-30
words: 2048
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-30 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_98d8a34e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: The Future of Claude Code: Mods, Mutable Software, & Multiplayer Agents — Thariq Shihipar, Anthropic
CHANNEL: Latent Space (lang=en)
TRANSCRIPT SAMPLE:
I think it's just like different models are very different from each other, you know what I mean? But I realize that it's like such a pain to like maintain different ones, you know what I mean? And yeah, like as the models get better and better, the floor of how they accomplish the simpler task is better. And so I do think in the limit cloud.mmd goes away. And maybe not even like that far. Like I I think like I think that right now it might be better to start a new project without a cloud. >> Yes. Um, I think that like maybe if you see very repeated failure modes, you add them to your cloud. MV. The really tough thing is that this changes per model. And so like if you've added a bunch of failure modes or like like >> you need Fable MD, you need Opus MD. >> Uh, well even Fable 5.1 versus Fable 5, you know, like it is annoying. Like I'm not like, you know, like we don't like do this on purpose, you know what I mean? It's just like how the models work, right? And so like maybe like Fable 5 had this like failure mode that Fable 5.1 doesn't. And if you keep this context running log of a bunch of different failure modes, they will probably over constrain Claude, you know. And so this is like uh we we just actually added eval plugins for skills. And so now you can eval if a skill is better. >> Before we get into today's episode, I just have a small message for listeners. Thank you. We would not be able to bring you the AI engineering, science, and entertainment content that you so clearly want if you didn't choose to also click in and tune into our content. We've been approached by sponsors on an almost daily basis. But fortunately, enough of you actually subscribe to us to keep all this sustainable without ads, and we want to keep it that way. But I just have one favor to ask all of you. The single most powerful, completely free thing you can do is to click that subscribe button. It's the only thing I'll ever ask of you, and it means absolutely everything to me and my team that works so hard to bring the Inspace to you each and every week. If you do it, I promise you, we'll never stop working to make the show even better. Now, let's get into it. We're here in the studio with our friend Tar from Enthropic. uh and I guess generally the cloud code I there's there's so much uh sort of merging of boundaries and you've been so on top of everything since you joined Anthropic you have been early to cloud code itself but then also and you've told that story in other podcasts and you've also been talking about seeing like an agent most recently you did the top AIE ware talk field guide to fable which obviously you guys launched fable so that that's cheating and mostly you most recently also launching cloud tag and we're also going to be talking about pacing on frontier. There's a lot going on in enthropic. I guess top of the question is what's it like being anthropic when there's so much going on. >> I think that it is like I think you can get whiplash sometimes. I I think like going when I joined Enthropic, I joined because of cloud code like like cloud code had just come out and I was like this is so good and opus 4 to me was like like just I could not imagine like how good it was. You know what I mean? And that was like a real moment for me. But I was like trying to convince like my startup friends basically to to use a coding and they're like oh no like our engineers don't think it's good enough or something. And I was like that's insane. Um, and now you like fast forward, you know, 12 months, um, less and like it's just like, yeah, the default way that everyone codes, right? And I think that like just having to go from like selling it to like now, you know, teaching people how to be, you know, make the most use of it and and be more efficient and things like that is just like a like a big, you know, like big change. And uh yeah, I think like it's just hard to stay on top of everything as a human, you know, like things happen so so fast and like >> more agents at it. >> I mean, yeah, like that's actually like the agentic stuff scales much better than the like human stuff where it's like oh like there are three things happening right now and like they're all emergencies and like how do you like you know uh respond to it? Yeah. >> What do you split your time on? You do a lot of technical writing, engineering work. >> Yeah. So I I think that like when I joined the cloud code team, I wanted to teach people how to use cloud code basically. And I think that like that has been something that like I thought like maybe I would spend a little bit of time on it or like I you know like do I was spending some time on the agent SDK first and I I wasn't exactly sure like you know how the bitter lesson would go you know when it comes to like harnesses right like I think sometimes we were like oh like what's after cloud code you know what I mean and so initially I was like I just want to teach people how to use cloud code and make it easier to use cloud code and I think that has just like as harnesses have gotten better and better that's like the dominant problem now is like how do you use the agents right like it's like such a high skill expression thing so I I do that and then I do engineering work um I give talks but I think like when I'm doing engineering work my goal is to take that feedback that we get from users and also like then be able to talk about like hey how how to use cloud code to do engineering so there's kind of like a good loop there yeah >> yeah I'll for listeners we'll attach uh the talk that you did with Sarah for the dev writers uh meetup which we talked a little bit thought well first you do the work and then you talk about the work something like that sew and reap or what was that >> and reap and sew and reap >> something like that something like that yeah so and then just to preview a little bit uh we are going to talk about the evolution of the harness it has come a long way from just bein
...[middle elided]...
 these enormous benefits right and um yeah like we've written a lot about that too. Yeah. >> Okay. Uh that was a huge tour uh from like ask you a question tool to AI safety. >> Yeah. Yeah. To facing the frontier. >> Yeah. No but uh it's clearly it's clear that you like really embrace everything that's available to you anthropic and like it's it's good to at least have a peak in inside of like what the discussions are the topics are. Um any last words to people and you know whatever you want to >> um >> call to action. >> Yeah. I mean I think it's uh one thank you for having me. You know I think this is like I really >> Yeah. Yeah. Yeah. >> We first met in a Chinese restaurant. >> That's right. Yeah. Yeah. Yeah. Um, I think like uh I really enjoy sort of the community you've created and the community of developers and you know I I think that like I I sort of know things are changing really fast and I think there's like a lot to keep on top of and like I think there's just a lot to do and I sort of feel I think a lot of people feel like a little bit tired or anxious or something stressed. Yeah, exactly. And this is like extremely understandable, you know, and I think we >> I understand like and we we're not perfect as well. like we you know it's like sort of criticize and like understand like you know ways all of the AI labs could be better. Um and uh but I also like am very excited about the excitement that everyone has for AI and just like it's a really really exciting time. I think we'll like look back at this time and be like oh like you know this is like very hectic but very exciting and like know software engineering changed like forever like me other things will change um and it's like really privileged to like uh be part of it you know like to talk to like the audience that you have and um get to interact with all the developers who are like pushing the frontiers a lot on what's possible and I learn a lot from from that too. Yeah. >> Uh thanks so much. Thanks.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding",
  "signal": 0.25,
  "novelty": 0.35,
  "actionability": 0.25,
  "evidence": 0.3,
  "durability": 0.4,
  "volatility": "volatile",
  "half_life_days": 120,
  "why": "Интервью с разработчиком Claude Code даёт пару полезных инсайтов про CLAUDE.md и эвалы навыков, но большая часть сэмпла — благодарности спонсорам, рефлексия и общие рассуждения без конкретики.",
  "knowledge_units": [
    {
      "claim": "По мере роста качества моделей файлы CLAUDE.md (постоянные инструкции-память) теряют смысл — модели сами справляются с простыми задачами без накопленных заметок.",
      "type": "principle",
      "actionable": "Не разрастай CLAUDE.md заранее; периодически проверяй, какие правила там реально ещё нужны на текущей версии модели, и вычищай устаревшие."
    },
    {
      "claim": "Правила про повторяющиеся сбои модели (failure modes) стоит добавлять в CLAUDE.md только после реально повторившейся ошибки, а не превентивно — иначе накопленный список правил начинает избыточно ограничивать модель и мешает при смене версии модели.",
      "type": "tool-caveat",
      "actionable": "Веди журнал сбоев по конкретной модели/версии, добавляй правило в canon только после повтора, и ревизируй его при апгрейде модели (Fable 5 → 5.1 и т.п.), т.к. старые фиксы могут быть больше не нужны или вредны."
    },
    {
      "claim": "В Anthropic добавили eval-плагины для скиллов, чтобы можно было автоматически проверять, стал ли скилл (навык-инструкция для агента) лучше после правки.",
      "type": "tool-caveat",
      "actionable": "При обновлении своих скиллов/промптов заводи автоматический eval, сравнивающий версии до/после правки, вместо ручной проверки на глаз."
    }
  ]
}
```
