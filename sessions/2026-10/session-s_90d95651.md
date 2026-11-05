---
session: s_90d95651
date: 2026-10-25
words: 775
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_90d95651` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: V7 cuts costs 78% while boosting accuracy with GPT‑5.6 Luna
CHANNEL: OpenAI (lang=en)
TRANSCRIPT SAMPLE:
With GPT 5.6 we seen huge improvements in the build out of enterprise workflows with a B7 Go. A few months ago the models couldn't really understand complex processes like insurance underwriting or screening of finance deal, but the latest GPT models can ingest 100 pages of instructions and build out a workflow that can solve them end to end. B7 Go helps GPT models develop these long horizon workflows with citations that anchor every fact. >> And recently a memory system that remembers everything about your company. >> We benchmark every new model and with GPT 5.6 sold we noticed that tool called errors in our context graph benchmark dropped from 2.7% to just 0.2%. >> Yeah, the model's only half the equation because the other half is the platform where these models run on. And our context graph store all this information about entities, facts, relationships following an ontology that matches your data. Previously models used to make ingestion errors especially whether fact was worth remembering or not. >> Older models using rag would also try and guess unanswerable queries. With GPT Luna on V7 Go context graph we've seen hallucinations reduced by 38%. Visual understanding of documents is also getting much better. >> And we're seeing the same benefits in workflows as well. I were previously we took minutes to research companies information and then just give the user an output. Now we take just a few seconds and we don't need to re-ingest all the data from scratch. >> We're also seeing the quality of the output improve. So previous models used to generate decent investment memos, but they lack the depth and accuracy that we're seeing with the new models. >> Yeah, so the GPT 5.6 suite is letting us solve use cases that a year ago were impractical or even impossible. And combining that within a workflow engine and a memory system we can help these enterprises that are known for their slowness in retooling towards the AGI. And we're thrilled to be working with OpenAI towards that.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "enterprise-workflows-context-graph", "signal": 0.3, "novelty": 0.2, "actionability": 0.2, "evidence": 0.35, "durability": 0.2, "volatility": "volatile", "half_life_days": 60, "why": "Это клиентский кейс на канале OpenAI, по сути реклама V7 Go и GPT 5.6: цифры (ошибки вызова инструментов 2.7% → 0.2%, галлюцинации -38%) даны без методики, переносимых приёмов почти нет.", "knowledge_units": [{"claim": "Хранение фактов и связей в графе контекста по онтологии, соответствующей данным компании, сокращает галлюцинации по сравнению с голым RAG, где модель пытается угадывать ответ на вопросы без ответа (заявлено -38% на их стеке).", "type": "principle", "actionable": "Если в RAG-системе модель отвечает на вопросы, ответа на которые нет в данных, добавьте явный отказ при отсутствии источника и сравните долю галлюцинаций с графовой памятью; цифры вендора перепроверьте на своём бенчмарке."}, {"claim": "Длинные корпоративные процессы (андеррайтинг, скрининг сделок) собираются как workflow из 100-страничных инструкций, а каждый факт привязывается к цитате-источнику.", "type": "workflow", "actionable": "При построении длинных агентных workflow требуйте от модели ссылку на цитату для каждого факта и проверяйте цитаты автоматически."}, {"claim": "Если не пересобирать контекст с нуля при каждом запуске, а переиспользовать сохранённую память, исследование компании ускоряется с минут до секунд.", "type": "tactic", "actionable": "Кэшируйте результаты ингеста сущностей и фактов между запусками workflow и инкрементально обновляйте их вместо полной переиндексации."}]}
