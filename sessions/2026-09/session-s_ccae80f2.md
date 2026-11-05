---
session: s_ccae80f2
date: 2026-09-28
words: 2042
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ccae80f2` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: I Turned Coding Agents Into a Strategy Game — Ido Salomon, AgentCraft
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Okay. Hi everyone. Uh I'm Solomon. I am the creator of ATMCraft and I also created MCPUI which became MCP apps and MCP steering committee. I've done a bunch of other stuff. Uh but we're here to talk about why we're the bottleneck and why we don't have to be. So, uh as you all know and use every day, agents are amazing. There's so much they can do uh from generating cat memes to B2B SAS apps. So if they are so amazing, we have to ask why aren't we all unstoppable? Why doesn't everyone have an army of agents that just does whatever they want? So it should be relatively easy. I mean you just have a bunch of monitors and you spin up 25 cloud code agents and you're done. So the reality is that it's just not that simple to do something like that. you need to a really want to use agents and secondly once you actually spin them up each one of these agents requires you to steer them direct them review them and when it's at scale especially it's just exhausting we need to find the skills to allow us to do it without burning out so in reality we are the bottleneck and the the cool thing here is that while we are the bottleneck The skills that we need to do these things to uh find ourselves not burning out every time we use an agent are with us all along. Uh if you try to compare it to other stuff that you've been doing outside of programming, for example, playing video games, it's not really that different. Like if if you're playing Warcraft, for example, or Sims, and you have a bunch of different uh units running around, you need to understand what they're doing and supervise all of it. How different is that from from actually inspecting agents? So I took this concept uh too far and I created agent uh which is a game inspired orchestrator uh that tries to bring all that good stuff together into work. So let's take uh a quick look of what that actually looks like and try and understand the journey that we can go through to really raise the ceiling of how humans and agents can collaborate. So, uh, this is AgentCraft. Uh, there's really a lot to unpack here. Uh, so we'll just go through the basics really quick. Um, what you see here is an agent. Uh, it's an actual representation of a cloud code or openclaw, whatever agent that you can imagine. Uh, it can be detected on your device or you can actually spawn new ones directly from a craft. Uh, so like I said, you have like codecs and uh, open code etc. at your command. >> Uh, and these agents can do everything. They're just normal agents. Uh, so I can just prompt them in this nice side panel that also has voice. So there's multimodality here. Uh, and just do something for me. >> Prompt. Prompt. >> And now these agents can do whatever. Uh, and if you look around you would see that the map has a a bunch of different elements. So you have buildings. These buildings represent functionalities. So for example, if you can manage your plugins or skills, uh you have like integrated terminal, integrated git, uh you can do in your all of your work from within this space. So now that we have this and we understand the basics, let's look at what we can do uh to raise the ceiling. So the first step is obviously visibility. I need to understand what's going on. What are my agents doing? So, I have this nice side panel and it shows me the different agents and what their task is and what the last thing they did is and what they're currently doing. Everything I need to quickly understand who needs my attention and who doesn't. The second part of it is we're not just limited to this. We have a map. So, I can take let's say my file system, project it onto the map, and now I can see exactly what my agents are doing. Not just by looking at a list of stuff. I can actually see okay this agent is now working on this directory or this file and these files are represented as runes on the map. So I can really look at each one and see exactly what each agent did and when. And now I can take this nice information because we are the orchestrator uh and use that to create linkages and now I can create cool stuff like heat maps. So I can really easily see what's going on. And the the other aspect is that now that we have this visibility, that's not really enough. We need to be able to react to what's going on. If someone needs my attention, I need to be able to quickly jump to it. So much like video games or RTS games or Civilization, whatever, you would click uh spacebar and it would just take you to the nearest thing that actually needed your attention. So you can really easily understand what's going on. and jump from one thing to the other and answer questions or approve plans, etc. That was nice. I mean, it's a nice step just to have that visibility, but it's not really enough. It's pretty exhausting to keep looking at what the agents are doing in the granularity of what files are they using and what tools are they using at the moment. So, we need something else. Uh and the reason is that we have like two two main problems here. Uh one is that there's just too much to hold in our heads. Even if I can understand what's going on and I can see everything, I can't really do like 20 things at the same time. I can't even think of the next thing I want to do if I have this, you know, huge coding project or whatever. So I need to find some way to fix that. Uh so we can I mean we can tell the agents uh you know go through my codebase, find out what the next things I need to do are, create these tasks for me and I just click a button, I accept the quest and there's some agent that does it for me which is fun. Uh it's cool. Uh but the next problem here is that okay now I have 20 stuff going at the same time and I have to babysit each and every one and that is completely exhausting. So you could ask okay we have agents agents are amazing as we've established so I can just go ahead and tell the agent to do it for me now it's called software factories but at the time it was just doing stuff au
...[middle elided]...
w uh complex the UI is and kind of try to find a lower denominator of what makes stuff accessible especially now that agents are much more capable so instead of granularity or having like exactly what files they're working on maybe I can have it more of a mobile game level uh have projects that they keep returning to and use loops and other stuff that rely on agents being more autonomous to have like a very basic level of I prompt I get the result I don't really care perhaps about the way I can see it if I want to and I have this really nice interactive and cool experience that makes me want to come back to this and obviously I mean this is one visualization uh it can really resonate with some people but might not might not present to others because we're not all the same and what may appear like amazing and easy to one person can appear very difficult to another. Uh but here uh I'm trying to look at a way to make this more customizable. Try and understand what it is that you as a person need in order to understand and want to use these tools. So this is a very very early draft. Um but if you want to use it, please let me know. So we're the bottleneck. I think we've established that uh pretty well until now. But the skills that we need to stop being the bottleneck and enable this new future are already with us. So we are the bottleneck, but we don't have to be. And I hope that you all can take what's relevant to you and your life and apply it forward. So I would ask you for two things. One, agent is already out there. Like you can just npx install agent as a website uh and do your thing. Uh this new thing that I just showed you uh potentially loopers uh is still experimental. I'm still trying to understand the interest and what people are actually looking for to uh get the floor that they want or the ceiling that they want. So, please uh go here and express your interest and tell me what you're looking for so I can know what to do with this. And thank you. I got it.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-coding-ui",
  "signal": 0.25,
  "novelty": 0.35,
  "actionability": 0.15,
  "evidence": 0.15,
  "durability": 0.3,
  "volatility": "volatile",
  "half_life_days": 90,
  "why": "Это в основном питч собственного инструмента AgentCraft (геймифицированный оркестратор агентов), с метафорой RTS-игры, но без конкретных техник, метрик или воспроизводимого воркфлоу — практику взять почти нечего, кроме самой идеи и ссылки на npx-инструмент.",
  "knowledge_units": [
    {
      "claim": "При управлении множеством параллельных coding-агентов человек становится узким местом не из-за нехватки возможностей агентов, а из-за когнитивной перегрузки от необходимости постоянно следить, направлять и проверять каждого.",
      "type": "principle",
      "actionable": "При масштабировании до 5+ параллельных агентов сразу проектировать слой визуализации/дашборд состояния (кто ждёт внимания, кто застрял), а не полагаться на построчное чтение логов каждого агента."
    },
    {
      "claim": "Пространственная/игровая метафора (карта, здания-функции, 'руны'-файлы, heat map активности, быстрый переход к агенту, ждущему внимания) может снизить усталость при супервизии множества агентов по сравнению со списком логов.",
      "type": "tactic",
      "actionable": "Для собственного мульти-агентного дашборда попробовать проекцию файловой структуры проекта на визуальную карту с индикацией активности вместо плоского текстового лога — это может ускорить нахождение агента, которому нужно решение."
    },
    {
      "claim": "Автоматическая генерация задач/квестов из скана кодовой базы ('пройди по коду, найди что нужно сделать, создай задачи') снижает нагрузку на человека по формулированию следующего шага, но не решает проблему присмотра за исполнением.",
      "type": "workflow",
      "actionable": "Можно поручить агенту периодически сканировать репозиторий и предлагать список задач-кандидатов вместо того, чтобы каждый раз формулировать промпт вручную — но это не отменяет необходимость ревью результата."
    }
  ]
}
```
