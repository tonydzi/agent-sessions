---
session: s_8339152e
date: 2026-09-27
words: 1931
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_8339152e` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Long-Horizon Agents Need Experiments, Not Just Prompts — [ИМЯ] [ИМЯ]
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hi everyone, I'm [ИМЯ], [СКРЫТО]. And today I want to talk about auto research in a multi- aent AI village. I will use a video game like AI Village as a running example here, but the broader question is one I think many AI engineers are starting to run into. How do we evaluate and improve agents that carry state over a long period of time? Before I get into the auto research layer, I want to talk a bit about project paradox. We developed project paradox at supercell's AI innovation lab. Me and my teammate are natural money. We built a modular AI framework that allows any developer to plug in intelligent autonomous agents within a video game that can interact, compete or cooperate with other players or agents as well and place them uh and make them into dynamic game companions. Now to give examples of what these agents can do, the agents can move with intent. They can go to any location or person and they're guided by their own memories, emotion, or curiosity. These agents can interact with the world. They can pick up objects, drop them anywhere, and they're also aware about the context in their own environment, such as the objects or other characters or agents as well. I would also like to note that game developers can also add new actions for these agents to accomplish within our framework as well. Instead of just dropping or uh placing objects, agents can also obviously react to what's happening around them. And these events that happen around them affect their own beliefs and emotions on the fly as well. And of course, it wouldn't be complete if agents can't start conversations, right? agents can in this scenario approach other agents or even the player as well and this makes the game feel more alive. And of course these conversations are stored within their memory and is according to their own um and affect their own emotions and beliefs or goals as well. And al together these agents make our multi- aentic framework. Um yeah yeah one second so the architecture was intentionally stateful behind this. The first important part was per agent memory. Each agent has its own memory namespace backed by rag. So memory did not bleed between agents. Second, we tracked emotion as a small vector. So after an event or conversation, the system could update values like joy, sadness, fear, anger, or disgust. Third, agents had belief scores towards other agents and the player. You can think of this as a trust matrix. Basically like after the interaction happens, the LM basically decides whether the trust score should go up, down, or whether it shouldn't change at all. And fourth, every memory receives an important score. Um to to explain this better, like let's say you had dinner a few days ago, you probably wouldn't remember what you had for dinner, right? But um if someone was murdered a few days ago, you definitely remember that. So the agent will evaluate or the LM will evaluate uh an important score of an event and if it crosses a threshold, it will store that specific memory uh in a separate cache so that important context can be retrieved better later on. And here's an example of it just working. Um, we going to ask one of the characters to go on a picnic with us. Here, uh, our character Blossom um, decides to pick up a pastry and go to the picnic area because we asked her to do so. Keep in mind during the conversation in the background, she plans all of these sequence of actions to accomplish. And one when we talk to her afterwards, she will also reply within context as well. Yeah. But this is where an interesting problem actually started. As you saw in the last example, like for shortterm game play, this our architecture worked pretty well. like a character could make a plan, move around, talk and remember the recent interaction and respond to us or other characters as well. But over longer horizons, this is where we notice the social consistency start to get weaker. So in this example, we have one agent spreading a rumor about a sale on mangoes to another agent and that agent receives that information and goes and tells another agent about it. Later on, after a number of events that occurred in between, when the player asks one of the agents about the mangoes, it doesn't exactly store that context that we were expecting or it doesn't give us the context that we kind of wanted to. And this is where things are starting to get messy naturally. Like the system may remember the rough topic but lose the source of the topic. A rumor may become certain instead of just a rumor like the agent might state it as a fact or um an agent might know a fact but fail to execute fail to remember it while creating a plan for its actions. So the question here became how do we improve a multi-agentic system over longunning social behavior and not just over one response. And this is where we wanted to bring in auto research. As you all know, uh few months ago, [ИМЯ] posted out auto research and this this made us immediately very curious. Uh perhaps we can make the system run experiments uh on itself and can we use this for our system as well. So what we understood is instead of manually tuning a prompt or watching one nice demo, we could define sen a scenario suit, run the agents, collect traces, score the behavior and change a small policy surface and only keep the changes that actually improve the score. And this is where we're trying to bridge project paradox with auto research. So at this point basically our multi-agentic framework project paradox is more like a lab bench and auto research becomes the experimental loop around it. And importantly this is not only about improving rag retrieval. The broader framing is optimizing the agent protocol like how do agents write memories, retrieve them, communicate uncertainty, update trust attribute sources and replan around new facts. basically um yeah in this context uh oh yeah in this context art research is not another agent in t
...[middle elided]...
 where right and whether it supersedes an older answer. Personal assistants for example need to remember commitments that they previously made and h make corrections if uh if the user u wants to change those personal commitments. Research agents need pro uh provenence citations contradiction handling and hypothesis updates. Coding agents need longunning context across issues, files, teammates and changing requirements. Workflow agents need access controls, handoffs, and replplanning when the world changes. All of these systems have the same underlying problem. They maintain state over time. And that state affect affects future action. So they need control scenarios and behavioral scorecards is what we are proposing. So again in brief, a recipe for long horizon agents. If there's one practical recipe I want you to take away, freeze the harness, define scenarios, log traces, score behavior, and expose only a small policy surface. Search over these changes, keep only changes that survive your measurement. And this is an engineering pattern that we believe would uh make sense for longunning agents. The real question we believe is across controlled runs, does the system behave better? To close, project paradox start as an attempt to make game agents feel alive in a 3D world. But the deeper engineing problem was not animation or dialogue for us. It was the state such as which agent knows what, which agent told whom, what is true, uncertain or outdated, and do agents act on what they remember. Otter research. Otter research gave us a way to approach this a bit more systematically. Not by trusting one demo and not by endlessly handtuning prompts, but by running control experiments and keeping only the changes that survived our measurement. Long horizon agents need experiments and not just prompts. And I hope that's the takeaway that you get from this talk. And yes, please do connect with us. We'd love to talk if you have any questions. Thank you so much for listening. Yeah.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "long-horizon-agents",
  "signal": 0.7,
  "novelty": 0.55,
  "actionability": 0.65,
  "evidence": 0.6,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Даёт конкретную архитектуру памяти мультиагентных систем и воспроизводимый рецепт улучшения долгоживущих агентов через контролируемые эксперименты, а не только прогонку промптов.",
  "knowledge_units": [
    {
      "claim": "Каждому агенту нужен отдельный RAG-неймспейс памяти, иначе память утекает между агентами",
      "type": "tactic",
      "actionable": "При проектировании мультиагентной системы с памятью делай изоляцию хранилища памяти на уровне агента, а не общий индекс для всех"
    },
    {
      "claim": "Долгоживущие мультиагентные системы деградируют не в единичном ответе, а в социальной консистентности: теряется источник инфы, слух превращается в факт, известный факт не всплывает в момент планирования",
      "type": "tool-caveat",
      "actionable": "Если строишь агентов с долгой памятью, тестируй не только одноходовые ответы, а цепочки событий на длинном горизонте — короткие демо не покажут эту деградацию"
    },
    {
      "claim": "Помимо памяти диалогов, полезно хранить эмоции как вектор (радость/грусть/страх/гнев/отвращение) и доверие к другим агентам как матрицу trust-score, обновляемую LLM по итогам взаимодействия",
      "type": "tactic",
      "actionable": "Добавь в state агента структурированные числовые поля (emotion vector, trust matrix), которые LLM обновляет после каждого события — это даёт более предсказуемое поведение, чем чистый текстовый лог"
    },
    {
      "claim": "LLM может присваивать событию importance score, и только события выше порога сохраняются в отдельный кэш для приоритетного извлечения позже",
      "type": "tactic",
      "actionable": "Внедри двухуровневую память: обычный лог + отдельный 'важный' кэш, отбираемый по LLM-оценке значимости, чтобы важные факты не тонули среди рутинных"
    },
    {
      "claim": "Рецепт улучшения long-horizon агентов: заморозь harness, определи сценарии, логируй трейсы, скорь поведение, выдели маленькую policy surface для изменений, ищи изменения по этой поверхности и оставляй только те, что подтверждены измерением",
      "type": "workflow",
      "actionable": "Вместо ручного тюнинга промпта по одному демо — построй набор контрольных сценариев с метриками поведения и меняй систему только через них, отбрасывая изменения, не подтверждённые замером"
    }
  ]
}
```
