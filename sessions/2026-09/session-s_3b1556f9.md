---
session: s_3b1556f9
date: 2026-09-20
words: 2032
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_3b1556f9` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: AI [ИМЯ] [ИМЯ] [ИМЯ] [ИМЯ] [ИМЯ] [ИМЯ] — [ИМЯ] [ИМЯ], TikTok
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Hello everyone. Good good afternoon. Uh today uh I will be talking about AI agents are also distributed systems. So as uh the models have started to become more complex. Initially the uh LLM models were just text in text out without performing any actions and uh the effect that they can produce was just a wrong model output. However, with now the capability of agent the agent the rise in agent capabilities where the systems can now talk to external systems uh it has turned into a distributed systems and it is important to incorporate distributed systems thinking and concepts when building AI agents. So I will be going over uh that uh in this talk. So you guys might have uh heard about incidents being caused by a AI agents. Uh for instance, the replicate AI agent deleting a production incident production database or Air Canada chatbot basically making an uh an incorrect refund. And both of these uh incidents or a lot of these incidents could have been prevented uh by good systems thinking when building these uh AI agents. So for instance for the replet a uh uh uh incident we could have good uh uh we could have robust backups. We could have scoped authority. we should we shouldn't ideally have uh allow AI agents to delete production databases. Uh moreover for Air Canada chatbot it would have been uh a good idea to have uh authoritative source of truth retrieval so that it's not making uh uh decisions based on stale or incorrect policies. So let's uh go over the transition from chatbot to production system. Uh so uh initially when we were in the uh in the uh age where LLMs were just chat bots uh we had prompt in and we were outputting text there were no side effects the agent was not interacting with any other system. However, uh due to agentic uh in the agentic era in the agentic revolution, now those agents uh by ingesting prompt can uh run an agent loop, call external services, call tools and also perform state changes. The architectural boundary now has moved uh way beyond an LLM model. And the difference is that it can now cause side effects in the outside world. So when basic when building AI agents, it is important to recognize the external systems that it is talking to, [clears throat] the states that uh it is interacting with and what credentials does it have and the actions that it can perform. uh I ideally like to think about it as uh uh AI agents as basically having a probabilistic coordinator. In distributed systems as well, we used to have services which were coordinating uh multi-step workflows. However, they were deterministic in nature. But in the case of AI agent, the AI acts as a probabilistic coordinator. The amount of action, the kind of actions that it can take can vary quite a lot. It is not just a decision tree that uh we typically in traditional systems would have mapped out and those uh actions can have severe consequences uh ba uh if they are not confined by our determinist by having deterministic controls in place. So it is important to ensure uh that we have deterministic controls in place to ensure that agent or the AI agent is not performing any uh any actions that might be uh uh problematic. So uh let's uh discuss the how a typical agent loop might look like. So at first it might uh do some planning. Then based on that plan it will it will perform an action and it will then observe the results of those actions and uh it might persist that into some d some data store and then decide what to do next. Each step in this loop is basically crossing a a boundary. During planning, it can interact with data sources to retrieve some data. Uh during action, it can call external APIs, tools, uh databases and perform any actions. During observation phase, it can perform it can get partial results and basically plan or make subsequent actions based on those partial results. It can persist incorrect data or uh and uh when deciding it might also decide to uh perform an incorrect action or uh worse it can also do a retry storm. So it is very important when building an agent loop to persist every step of the process. Whatever actions the agent is doing, whatever context it is retrieving, it is important to uh persist that so that if anything fails, the agent is able to recognize where it failed and it can perform uh a reversible action. Uh it can perform undo operations. Similarly, there should be explicit transactions uh identified for each step. So for instance, if an agent is making a call, if it fails, what it should do? What should be the transaction to compensate for a uh for a irreversible or unsafe operation? For instance, if an agent makes sends an email to a a wrong email to a customer, what should it do to compensate for that? So, uh tool calls are just wrappers around uh external external APIs, databases, cues, uh and so on. And uh with uh when calling the when making these remote calls, there are some failures that you incorporate uh such as network delays, timeouts, uh you can make duplicate requests or worse the server side request uh might succeed. However, the client however the client might be reported an error. We have we have seen uh instances where uh a data by base might have written the data. However, due to some other errors, the server might have reported uh uh to us the error and uh with humans in the loop we can make we can basically perform correct corrective actions based on uh by seeing uh the database and actual source of truth. But in agent's case, we need to ensure that we have uh we have proper guardrails in place. So for instance, an agent calls refund customer uh tool call which basically performs a refund to the customer. The request times out uh that did the refund happen or not? What will the agent uh infer from that? Would it retry uh refunding to the customer? you basically the the timeout does not actually mean that there a failure had occurred. It means unknown. And it is important to have uh when designing these tools, it is 
...[middle elided]...
t happened, what information was was it reacting to and why it failed. And logs alone are not enough to uh for an agent to uh for teams to determine that. It is important to trace the model that was called, the prompt that was uh that was uh given to it and uh also the tool calls that were made uh the request uh that was made, the response from the tool, the errors that it got, the retrieved context, what the agent was uh was the the retrieved information that the agent was reacting to, the rights that it made, and the approvals that it got and so on. So uh I would like to uh end with uh the idea that yes model capability matters. Having good models uh improves the uh likelihood of it making uh correct operations. Smarter models reduce mistakes. It uh it uh improves the capability that the model has. However, it cannot eliminate network failures, stale data or adversarial input. It is important when building this architecture, we also reason about can we bound, observe and recover from actions performed by the AI agent. It is important to have tool contracts in place to ensure that uh it is only allowed to make uh operations that it is uh given that it is provided the contract and the contracts are clearly establishing the request and response uh response uh response types uh the schema and all these tools have item potency baked into it. so that uh when repeated requests are sent in uh it is not causing unsafe operations to be retried. Moreover, there should be source of truth decisions made uh when there are conflict conflicting uh memory states. It is important uh for the agent to realize this is the source of data that it should rely on and we should have re retry policies uh like rate limits set in to ensure that the agent is not uh retrying uh ext uh aggressively. Moreover, uh permissions should be set up. There should be traces and recovery paths. So when building AI agents, we should also ask what the system lets it do when it is wrong. Thank you. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agent-reliability-distributed-systems",
  "signal": 0.75,
  "novelty": 0.45,
  "actionability": 0.7,
  "evidence": 0.5,
  "durability": 0.75,
  "volatility": "medium",
  "half_life_days": 730,
  "why": "Доклад переносит зрелые концепции распределённых систем (идемпотентность, компенсирующие транзакции, трассировка) на AI-агентов и даёт конкретный чек-лист защит, хотя без демо и метрик — только рассуждение и разбор известных инцидентов.",
  "knowledge_units": [
    {"claim": "AI-агент с доступом к внешним системам — это распределённая система с вероятностным (а не детерминированным) координатором, поэтому нужно применять классическое распределённое мышление: границы доверия, состояние, credentials на каждый переход.", "type": "principle", "actionable": "При проектировании агента явно картируй, с какими внешними системами он говорит, какое состояние меняет и какие credentials/права у него есть на каждом шаге цикла (планирование → действие → наблюдение → решение)."},
    {"claim": "Таймаут вызова инструмента агентом означает 'неизвестно', а не 'ошибка' или 'успех' — агент не должен трактовать таймаут как основание для автоматического повтора необратимой операции (например, повторного возврата денег).", "type": "tool-caveat", "actionable": "Для любых мутирующих tool calls (refund, delete, send) закладывай идемпотентность на уровне API и явную политику 'что делать при таймауте', а не давай агенту самому решать retry."},
    {"claim": "Каждый шаг агентного цикла (retrieval, действие, наблюдение) должен персистироваться отдельно, чтобы при сбое можно было понять точку отказа и выполнить компенсирующее (undo) действие.", "type": "workflow", "actionable": "Логируй/персисти каждый промежуточный шаг агента (не только финальный результат), и для каждой необратимой операции заранее определи компенсирующую транзакцию на случай сбоя."},
    {"claim": "Скоуп полномочий и авторитетный источник истины предотвращают классические агентные инциденты (Replit — удаление продакшн-БД, Air Canada — неверный возврат по устаревшей политике).", "type": "tactic", "actionable": "Не давай агенту прав на необратимые операции (удаление БД) по умолчанию; для решений на основе политик подключай агента к единственному авторитетному источнику данных, а не к устаревшему/дублирующему контексту."},
    {"claim": "Логов недостаточно для диагностики агентного сбоя — нужна полная трасса: модель, промпт, вызовы инструментов, запрос/ответ, retrieved context, сделанные записи и полученные approvals.", "type": "workflow", "actionable": "Внедри трейсинг агентных вызовов (аналог OpenTelemetry для LLM-агентов), фиксирующий не только результат, но и промпт+контекст+решения на каждом шаге, чтобы можно было восстановить 'почему агент так решил'."}
  ]
}
```
