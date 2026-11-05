---
session: s_4a77ceef
date: 2026-09-29
words: 1021
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4a77ceef` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Your Coding Agent Wastes SO MANY Tokens Just Finding Code - Here's the Fix
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
Most of what you pay a coding agent for isn't actually writing code. It's finding the right code to edit in the first place. Seriously, if you ask your coding agent to change anything in your code base, as long as it's not trivial, look what happens. It spends so much time searching and reading through all the files it finds to make sure they apply. And the search itself is fast and cheap, but reading through all these files, it takes so much context here before you're even changing a single line of code. And it's not just the cost. searching is a guess. And so, if you have something the agent should have changed, but it's named differently than what the agent is looking for, you're just going to miss it. And so, the change might be correct for everywhere that it identified, but that isn't always good enough. Now, underneath all of this, your agent is just answering a single question. What code applies here for the change the user is requesting. The problem is, coding agents can't answer that directly, but there is a tool that can, and it's called Sonar Vortex. And so, Sonar is a platform I've covered a lot on my channel already. It already parses your code base. And so, now Sonar Vortex is a tool on top that solves our problem here. It's able to identify for us very efficiently and directly things like what classes implement an interface, what calls a function, and what it calls back, down to the file and line. So, now I'm back over in Cloud Code with the same prompt, but this time giving it access to Sonar Vortex. To show you here that it is a direct lookup instead of a search. It is much more efficient. And the graph that it uses to perform the lookups is built right on our machine. There's no compiler or language server, and it refreshes in about a millisecond after any edit, which is a big deal for me because generally halfway through an agent turn, your code base hasn't compiled yet. So, in our original conversation, after it did all of the searching and reading all the files, it took 80,000 tokens just to do this searching. But now, over to the second one with Sonar Vortex, I was able to do the same lookup and then even a follow-up prompt to load more context, and it still was about the same number of tokens that it took. So, it's definitely more efficient. Sonar did a study where they ran six refactoring tasks across 10 runs, and they figured out that the token savings was anywhere between 6 and 34%. Semantic navigation covers Java, C#, JavaScript, TypeScript, Python, and Rust right now. It runs on SonarQube Cloud with the Sonar Agent Essentials add-on. Thanks to Sonar for working with me on this, and I'll have a link to Sonar Vortex in the description.

---

**Claude:**

```json
{
  "is_ad": true,
  "is_news_rehash": false,
  "topic": "agentic-coding",
  "signal": 0.35,
  "novelty": 0.25,
  "actionability": 0.4,
  "evidence": 0.4,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 300,
  "why": "Это по сути рекламный ролик инструмента Sonar Vortex (прямо указано спонсорство), но за рекламой стоит реальная и полезная мысль — основная цена агента уходит не на запись кода, а на грep-поиск и чтение файлов вместо точного семантического lookup по графу зависимостей.",
  "knowledge_units": [
    {
      "claim": "Основная стоимость (в токенах) работы кодинг-агента — это не генерация кода, а поиск и вычитывание релевантных файлов через grep/семантический поиск.",
      "type": "principle",
      "actionable": "Мерить, сколько токенов агент тратит именно на этапе поиска контекста до первой правки, и целенаправленно оптимизировать этот этап отдельно от генерации."
    },
    {
      "claim": "Grep/текстовый поиск — это угадывание по имени: если сущность названа иначе, чем ищет агент, релевantный код будет пропущен даже при в целом корректном ответе.",
      "type": "tool-caveat",
      "actionable": "Не полагаться только на grep-поиск по имени при рефакторинге across-codebase; проверять полноту через явные структурные запросы (кто вызывает функцию, кто реализует интерфейс) вместо надежды на совпадение имён."
    },
    {
      "claim": "Инструменты прямого структурного lookup по графу кода (какие классы реализуют интерфейс, что вызывает функцию и что она вызывает, до файла и строки) заменяют itеративный grep-поиск на один точный запрос.",
      "type": "tactic",
      "actionable": "При выборе инструментов для агента искать те, что строят локальный граф зависимостей кода (без компилятора/LSP, с обновлением за миллисекунды после правок) вместо инструментов, полагающихся на текстовый поиск."
    },
    {
      "claim": "На 6 задачах рефакторинга (10 прогонов) замена поиска на прямой структурный lookup дала экономию токенов от 6% до 34% (данные вендора Sonar).",
      "type": "benchmark",
      "actionable": "Использовать эту цифру (6–34%) как ориентир ожидаемой экономии при переходе с grep-поиска на semantic/graph navigation, но перепроверить на собственных задачах, так как замер сделан самим вендором."
    }
  ]
}
```
