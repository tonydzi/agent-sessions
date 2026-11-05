---
session: s_1f9de363
date: 2026-09-27
words: 2141
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1f9de363` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: We Let Claude Code and Codex Race Human Researchers — Elie Bakouch, Prime Intellect
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hey um hi everyone. Uh thanks for being here. Uh yeah, I'm super happy today to talk about uh automated eye research and uh especially uh all those like frontier model uh perform at uh automated eye research task. Um so I'm Elie. I worked at Prime Intellect as a research engineer and uh yeah I will go through our work on on this subject. So first I want to basically explain a bit why we are doing that and why we think it's super important to do that in the open. Um so first uh I think we we all agree that uh we've heard about like big labs saying that this bad thing called recursive self-improvement is coming very soon. Uh so recursive self-improvement is like model training models uh without uh human intervention basically. Um but uh we don't have any benchmark to basically quantify if this is true or not right. Uh and even less we don't have like a third party benchmark by non- big labs to to to see if it's something coming soon or not. And the other part is that we think that uh it's super important to understand all those model uh do research because we think that a lot of the scientific research that will come into the coming years uh will be based also on AI tools. So it's super important to understand how those model do research not just only AI research. So we try to build kind of this environment to test the capabilities of the model to do so. So it all started with uh Andre Karpati uh that's basically had fun by doing this video where he trained uh GPT2 from scratch in like 90 minutes like GPT2 training takes like weeks and uh no in two years ago I think it only took like 90 minutes. So what does it mean to reprod reproduce uh GPT2 in 90 minutes? It means that in 90 minutes you achieve this target loss. Um and yeah and that's at this point when you have the same loss than GPT2 you consider that your model is somewhat of equal performance. Um then what happened is that the community took this repo uh this GitHub repo and create another one called moed nano GPT and this effort was leaded by someone called Keller Jordan. And what happened is that they basically took this 90 minutes then 45 minutes and then now we can train like GPT2 validation loss model in less than two minutes which is honestly crazy and it took like two years to to achieve this. So it's a very strong benchmark where uh a lot of very talented researcher iterated on um yeah so we decided to take this environment of speedun so it's kind of a game so the goal of the game is to achieve this loss in the fewest in the shortest amount of time so this is the nano GPT1 and you can uh you don't have almost any constraints the only constraint that you shots that you need to use the same validation and training data, right? Um there is a new speedrun called the optimizer speedrun that was released uh a few months ago and here it's slightly different because uh you can only change the optimizer related parameters. So for instance nano GPT you can change the architecture uh do uh attention whatever uh optimizer sp you can only change like Adam to m shampoo or whatever optimizer is your favorite um yeah and so this is a bit more researchy because uh it's less about optimizing the program to be as fast as possible but more like finding the best method possible. no matter the the the time you put into the computer, right? So, um yeah, why take speedrun as an environment for automated AI research? First, uh we think that it's a good evaluation. We'll see later why. Uh and this is kind of the main focus of this talk. But we also think it's probably a good training environment because uh it's a way to give the model a reward. So the reward is positive if the model bit the speed run and beat the last record sorry and the reward is zero or negative if it didn't manage to to do it. So it's a good uh environment to train model. It's also quite fast like as you see uh previous record were around 2 minutes for the optimizer one. uh each run take about like 15 to 20 minutes and uh yeah and there is like clear rules basically and we also think it's like a good environment to make discovery so like kind of breakthrough in our research because uh there is those clear rule that you can verify or not. Um yeah. So yeah. Um so what we did uh so the release was like about two months ago and uh there was this optimizer speedrun and we decided to basically compete with the community by launching two AI agents. So Codex and Cloud Code. Codex was like GPT 5.5 with XI and uh cloud code was Opus 4.8 with XI. Um and yeah, we decided to basically let the agent free on our cluster uh and uh and just iterate on it. So we have like V1, V2, V3 is just basically us stopping the agent and then restarting. V3 uh was like one or two day before the release because we saw that our agents no longer have the best record. So we were like okay take all the the human uh record in the last few week and just try to to improve upon it and and and it worked. Yeah. And we also have this novelty track where the goal is to uh beat the record with only novel ideas. Um and we'll see that this this was more complex for the the models. So our RS is very simple. Honestly, we could have just replaced it with slashgo, but they there was no SLG goal at the time. So, we made our own goalm. It's actually quite fun that we choose the same name and we had the goal. MD and kind of agents that MD that define the rules and we let the agent propose ids and then it can submit a job with sbatch on our slum cluster and uh basically the way it works is that it can submit on nodes that are available but only under a certain permission which means that if someone want to use this node uh the model just like cancel the job it's called preemptable permission. So yeah, then it measure the it read basically the training logs then decide if it's a record or not. To validate a record you need to basically pass a statistical threshold to make sure that it's just not see the optimization and is just not r
...[middle elided]...
nd of steer them in the right direction and so on. Um yeah so we didn't try it yet I mean we are kind of trying it right now and uh we hope that this will lead to to to new discovery in AI research at least and also a way is that you can define multiple speedrun so this is the next slide if you like it's from safe bank slides but if you if you don't have the reference good for you means that that you're not too online uh but the idea is that uh by changing the object objective and the constraints of the speedrun you can basically create a lot of diversity and constrain the model to go into a certain direction and uh yeah and make those discovery. So uh at HIM in Ind. Uh there is a bunch of stuff here that we I mean most of it we didn't release yet but we are working on GPU sandboxing to allow model to iterate into sandbox because you need GPU sandbox for this kind of stuff. We are working on our own agents that are very efficient for like RM framework. So it means like you have a file system and you can write information read from it. Uh and you also do like this programmatic tool coding thing. We also training a model to be good at it on top of like open source model. And uh the thing that we already released is that we have those set of liberation and product called verifier primaril training where you can basically train evaluate any environments on any RS and the model that you can train can be like GNM 5.2 too which is very big and and yeah we have like we work a lot on making those li very efficient to to ship the best quality for for our clients. Yeah. Uh I mean yeah super excited about this domain. Once again I think it's super important to have uh a part of like this recursive self-improvement to happen in the open because there is actually a lot of people working that are not on big labs. So you need to basically uh yeah make it easy for people to understand all those model work to do research and so on. So that's kind of our goal and uh yeah thanks a lot.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-ai-research-benchmarks",
  "signal": 0.6,
  "novelty": 0.55,
  "actionability": 0.5,
  "evidence": 0.55,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Prime Intellect подробно описывает, как они превратили открытые спидран-бенчмарки (nanoGPT, optimizer speedrun) в проверяемую среду для оценки и (потенциально) обучения автономных агентов-исследователей (Claude Code, Codex), включая конкретные архитектурные решения — простой goal.md, preemptable slurm-джобы, статистический порог для подтверждения рекорда и отдельный 'novelty track'.",
  "knowledge_units": [
    {
      "claim": "Готовые спидран-бенчмарки с чёткими проверяемыми правилами (nanoGPT speedrun, optimizer speedrun) можно использовать как evaluation-среду для агентных ИИ-исследователей вместо разработки нового бенчмарка с нуля.",
      "type": "workflow",
      "actionable": "При оценке способности агента вести ИИ-исследования — взять существующий спидран с прозрачной целевой метрикой (например, target loss) и сравнивать агента с историческими человеческими рекордами по времени/качеству."
    },
    {
      "claim": "Чтобы отличить реальный прогресс агента от шума/переобучения под тестовые данные, перед засчитыванием 'нового рекорда' применяется статистический порог значимости.",
      "type": "tactic",
      "actionable": "Не засчитывать единичный успешный прогон автономного агента как улучшение — прогонять статистический тест значимости против предыдущего лучшего результата."
    },
    {
      "claim": "Агенту достаточно простого markdown-файла (goal.md) с описанием цели и правил игры плюс доступа к job-scheduler с 'preemptable' правами, чтобы он сам запускал и отменял эксперименты на общем кластере без сложного кастомного RL-фреймворка.",
      "type": "tactic",
      "actionable": "Для распределённых агентных экспериментов на shared-кластере использовать простой текстовый файл правил (аналог AGENTS.md) + preemptable sbatch-джобы вместо построения тяжёлой оркестрации."
    },
    {
      "claim": "Агенты заметно хуже справляются с генерацией действительно новых идей ('novelty track' — побить рекорд только новыми методами), чем с инкрементальной оптимизацией уже известных подходов.",
      "type": "benchmark",
      "actionable": "При оценке research-способностей LLM-агента разделять две метрики: инкрементальная оптимизация существующего решения и генерация принципиально новых идей — вторая задача сложнее и требует отдельного трека оценки."
    },
    {
      "claim": "На момент доклада не существует независимого (не от big labs) количественного бенчмарка скорости приближения к 'recursive self-improvement', поэтому авторы намеренно строят такую оценку в открытую (open-source, воспроизводимо).",
      "type": "tool-caveat",
      "actionable": "Не доверять заявлениям лабораторий о скорости self-improvement без независимой верификации — искать или требовать открытые, воспроизводимые бенчмарки третьих сторон для таких утверждений."
    }
  ]
}
```
