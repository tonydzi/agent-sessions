---
session: s_1a0d2b36
date: 2026-09-28
words: 2003
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-28 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1a0d2b36` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Scale the Judgment, Not the Model — Andrew Orobator, Reddit
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] A friend told me about an engineer at another company who ran a recurring war room just to delete dead experiments. Every two weeks, the team would stop, gather, and clean up flags that everyone agreed should be gone. That's the bestase version of this problem. Someone burning political capital to make maintenance happen by hand. That's the part that I still can't get past. My name is Andrew Robbittor and I'm an Android engineer at Reddit. This is a talk about what's actually stopping us as an industry from scaling that work responsibly. Spin at the gate until green. the engineering primitives behind self-driving code bases. First, what I'm not going to do, I'm not going to stand up here and tell you that AI can write code. You're at the AI engineer world's fair. Half of you are running coding agents right now. So, let's skip the part where I sell you on AI writing code because you laugh me out of the room. For me, my only input is the chat box. I describe it builds. I review. Your mileage may vary. The point was never how the code gets written. It's about whether you ship good software, a product that people can actually trust. And every gate in that system is a human's call. I've watched this everywhere. You've got your own version of it. the war room that I opened with someone burning a week of hackathon freedom on lint cleanup. As an industry, we've built tooling that can change the shape of the work, and we still spend our scarcest resource on work like this by hand. Human creativity, human attention wasted. The job changed and most of us didn't even notice. We're harness engineers now. Our work is the system that helps produce and verify the code, the constraints, the gates, the skills, the verification. Think about how you got good for a second. Mentorship, code review, the water cooler chats, the incident that paged you at 3:00 a.m. You absorbed all of it without noticing, just by being there. Humans absorb judgment implicitly. Agents require judgment explicitly. An agent boots with a blank context window and no memory every session. Every piece of judgment you picked up by osmosis, it has to be made explicit or the agent simply never has it. Quick test. Swap in a smarter model. You get a slightly better answer. Now take away the tests, the gates, the review and the whole thing falls over. So the model was never really the bottleneck. The judgment around the model is the model is raw talent while the judgment is the organization. And this judgment already exists. It lives in scars, in post-mortems, in your most experienced reviewers. it just doesn't scale because it's trapped in one head. So step one is making it accessible to the whole org where one reviewer's taste can guide a thousand changes they'll never touch. Ask experienced engineers to clean up a feature flag and they they're going to think about a whole string of questions first. A flag is never just a flag. Is the rollout frozen? What about the flag right next to it? Which team owns it? That bundle of questions is judgment and it's the most valuable thing in the building. Right now, it's trapped. It surfaces once in a code review, then it's gone, and the next person relearns it the hard way. A skill is institutional judgment made executable. It's that bundle written down so that the agent refires it instead of guessing. A newer engineer can work with 10-year instincts at their elbow. In 1986, Marvin Minsky named this a knowledge line or a kine for short. It's the configuration of mind that solved a problem reused on the next one. So, a skill is a kine for a codebase. And skills aren't documentation. Agents drown in facts. What they lack is which facts matter and which decisions are dangerous. Documentation preserves facts while skills preserve judgment. Skills are judgment that you reuse. But often times work such as feature development or a refactor outlives a single session and the context window wipes clean every time. So you need the other half. A record of the work itself. The plan, the decisions, what you already tried, even the surprises along the way. That's a worklog. A plan is a prediction. A worklog is a record that starts with one. So new session, fresh agent, zero memory. You type one word, continue. It reads the work log and picks up at milestone 7 out of nine. No re-exaining and the work log is the context. This talk is living proof. I built it across a couple of sessions using a worklog. I came back to a half-finish presentation and a fresh agent read the work log and resumed exactly where I had left off. That's the only reason why you're seeing a finished talk and not me apologizing for one. And for my personal side projects, this isn't willpower. A git hook blocks any commit that doesn't update the worklog. This way, the memory keeps itself. Skills encode how to do something. Personas encode whose eyes look at it. I got this from a Carpathy tweet. There's no you when you prompt a model. It doesn't have an opinion to give. So don't ask it for one, ask for a perspective instead. What would be a good group of people to explore XYZ? What would they say? [snorts] On my personal side projects, it's just me. No security team, no designer, no one to bounce ideas off of. So I have the model review my code as a security lead as a UX reacher as a UX researcher as Mchavelli when I want to know something when I want to know how something gets abused. I even built a design panel of opposing philosophies my designs have to survive. Then I read the reports and act on them. Each persona loads a kind of judgment that I don't personally have on demand. Encode a domain's taste once and anyone can borrow eyes that they don't have. The engineer with no designer gets design judgment. The newer engineer gets a security reviewer's instincts. Push it to the whole org and every team can now encode its own taste for its own agents. The judgment that used to live in a handful of heads is suddenly everywhere at once. skill
...[middle elided]...
lesson back into the skill so that failure can't happen twice. Failure becomes a constraint. But nobody is hand auditing 300 skills for drift. So, you give the agent a bedtime, a scheduled pass where it reads its own skills, finds the stale ones and the contradictions, and opens up drafts for review. The system sleeps, cleans house, and wakes up sharper, but that's a whole separate talk on its own. A self-driving codebase is a system that keeps its own judgment current in addition to writing code. Everything that I've shown so far fits somewhere along this judgment pipeline. And every mechanism in this talk, skills, personas, work logs, and the gates, the fleet, all of it was doing one job. Managing judgment. Every session, the model wakes up like Drew Barrymore in 51st Dates. Brilliant. and no memory of yesterday. No idea what it's built or what it's even for. The collection of primitives in this talk is the notebook that we hand it. The skills, the work logs, the judgment that let it do real work. We don't ship PRs that pass CI because the model is a genius. They pass because we built a harness that won't let it be wrong. Every gate in it is a human's call. That's harness engineering. Scale the judgment, not the model. So here's what I'm asking you to do. Don't just go write a skill. That's only that's only one implementation. Find the judgment your team always asks the same person about and make it explicit somewhere that an agent can reach it. It could be a persona, a lint check or a commit hook. That's the job. Now less product engineering and more harness engineering and the method demonstrates itself. The flag agent produces PRs that pass CI. This talk resumed from a worklog. We started here. Humans absorb judgment implicitly while agents require it explicitly. Self-driving code bases will exist the moment we get that judgment out of our heads and into the codebase. Then we point the agents at the gate and let them spin until it's green. Thank you. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding-judgment",
  "signal": 0.75,
  "novelty": 0.55,
  "actionability": 0.7,
  "evidence": 0.45,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 400,
  "why": "Доклад даёт конкретный концептуальный набор практик (skills, worklogs, personas, git-хук) для организации агентной разработки, но без бенчмарков и с личным анекдотическим доказательством.",
  "knowledge_units": [
    {
      "claim": "Скилл — это не документация, а явно записанное институциональное суждение (когда сработавший ревью-инстинкт превращается в исполняемое правило, которое агент переиспользует, а не угадывает заново)",
      "type": "principle",
      "actionable": "Когда опытный инженер объясняет цепочку вопросов при ревью (например, про фича-флаг), записывать эту цепочку как скилл, а не просто как факт в доке"
    },
    {
      "claim": "Worklog — это отдельный от плана артефакт: живой журнал решений, попыток и сюрпризов по задаче, который переживает обнуление контекстного окна и позволяет новой сессии агента продолжить с места остановки командой вроде «continue»",
      "type": "workflow",
      "actionable": "Для долгих задач (рефактор, презентация, фича) вести worklog рядом с кодом и в начале новой сессии агента явно просить его прочитать worklog перед действием"
    },
    {
      "claim": "Git-хук блокирует коммит, если worklog не обновлён вместе с кодом — так журнал работы поддерживает себя сам, без дисциплины силой воли",
      "type": "tactic",
      "actionable": "Добавить pre-commit хук, который проверяет, что worklog-файл изменился в том же коммите, что и рабочий код"
    },
    {
      "claim": "У модели нет собственного мнения при промпте — вместо запроса «мнения» стоит запрашивать «перспективу» конкретной персоны (например, ревью от security-лида, UX-исследователя или адвоката дьявола), чтобы получить нужный тип суждения на решении, где своей экспертизы нет",
      "type": "tactic",
      "actionable": "Для код-ревью или дизайн-решений явно вызывать агента в роли конкретной персоны (security lead, UX researcher, противоположные дизайн-философии) и читать несколько таких отчётов перед действием"
    },
    {
      "claim": "Скиллы дрейфуют и устаревают быстрее, чем человек успевает их вручную ревьюить — нужен периодический автоматический проход агента по собственным скиллам, который находит устаревшие/противоречивые и открывает черновики правок на ревью",
      "type": "workflow",
      "actionable": "Настроить регулярный (например, ночной) прогон, где агент читает все свои скиллы, помечает противоречия/устаревшее и создаёт PR-черновики для ревью человеком, вместо ручного аудита сотен скиллов"
    }
  ]
}
```
