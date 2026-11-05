---
session: s_88ad8d10
date: 2026-09-24
words: 2018
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_88ad8d10` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Modality Misalignment and Originality Attribution in Short-Form Video — Aditya Gautam, Meta
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Hello everyone. Uh I am Adita and we will be talking about uh two main problems that happen on the short form surfaces. We are going to talk about how do we deal with these things at a scale. Uh so to get started first thing is we will understand what are the characteristics of the data that we are trying to deal with what are the two main problems that we are actually working on uh and what are the multi- aent systems to solve those problems at a scale what are the different specialized small scale WM that we can uh build uh to solve those individual agentic problem and how do we build those agents what are the different ways to actually optimize it like to make it like scalable at a very big scale and then we will be looking into the evaluation in a very holistic 360 manner not just like a precision recall what is out there how do we understand the entire multi-agenting pipeline both from LLM level tools MCP and whatn not everything out there and then we will be getting into the optimization techniques which this which are very vision specific and metadata specific which will allow us and give us some intelligence to tell that we really don't need to do intell like this intelligent like workflow So for all the videos we can figure out what are the small set of videos which should be the candidate for doing these things and we will conclude with the takeaways. So the real life data is very messy. It is we are talking about at a scale of 100 million plus and a lot more viral content. There's a lot of adversal content people are trying to gain the system. There are a lot of uh multilingual text on the screens and in their videos and images. And the uh data is very dynamic. it keeps on changing from like month to month different AI tools are coming everything out there so it's it's really really dynamic that means there is a lot of drift issues and other thing that comes with a video data and then we know that there is no clear ground truth for the problem that we're trying to solve so these are like existing problem which happens in a real world video data set we will be the first problem that we will be talking about is the modality misalignment where the first is intramodality which is a very solved problem you can have a clip model you can have a modality on uh uh images, videos, uh audio, text and figure out what exactly is the cosign similarity on those embedding and figure it out. So this is a much simpler problem. What we will be talking about how we are doing intraodality u issues. So this is consider that like a video we have a big video and then uh suddenly you are seeing something some ad agenda some political things or something out there which shouldn't be there in the video as when you clicked on it. So how do we actually look into the small segments of the uh video understand this problem and figure out where there is an anomaly or kind of like adversarial behavior out there which shouldn't be there in the first place. So this is the first problem which requires a lot of granular understanding vision understanding and a video understanding to see what is happening at a very clip and a very frame level. The second problem is uh to understand the unoriginal content. In today's economy with the AI tools available, it's really easy to actually duplicate the content. When someone uh upload a video or something, we see that okay, it is being copied, it is being transformed and with tools, it is getting much easier to transform these videos. U so how do we actually detect this kind of unoriginal content? How do we figure out the source of the video? And um this has actually caused a problem in attribution credit u ecosystem imbalance and lot of like user fatigue where we are seeing a lot of repetitive videos which shouldn't be there in the first place. So uh coming to the multi- aent system uh the first thing is that uh why we are going to multi-agent not a single agent or single lenm because the problem is really complex. It requires a really specialized uh nodes and uh kind of like an understanding at each part of retrieval content understanding and then reasoning and if you can solve a problem with one agent one LLM you we don't need to actually do it on multi- aent systems. So this is where the centralized brain how we are actually thinking kind of like how the uh decomposition happens of this problem. The first is basically you have a video and kind of like a clip video ID and everything given to a reviewer agent. This is a centralized agent. This is basically the orchestrator. Consider that as an API gateway of uh doing a sing signal decomposition and finding what is happening around in the image. So what this guy do is basically this guy takes ask the perceiver agent and perceiver agent is the one which is basically considered that a very sophisticated VLM expert with lot of image and the video tools at uh disposal. Uh perceiver agent will take the ID from the retriever reviewer agent and it fetches the video from the database. It decomposes into smaller parts using different tools, different like semantic embeddings and different kind of like temporal change that happens which is a little bit beyond our scope but of this talk but it's uh a technique which is making sure that we are not doing at a fixed frame rate but we are finding where the temporal change happen and compressing those similar frames into one or two frames and then the perceiver agent get all the data from a clip level. The video embedding level get all the information about a clip embedding tags OCR whatever is present out there what is the natural language description and what are the time stamp from which frame to which frame what are those this metadata looks like it gives that data to the reviewer reviewer will look into all the temporal this JSON object provided by the uh perceiver agent in a raw form along with embeddings along with semantic ids tags OCR and everything and it does a temporal
...[middle elided]...
erything is doing with respect to the human queue. Is there a drift happening? Do we need to retrain our LLM as a judge on new data set which is coming from labeling team or how do we actually do on those parts in optimization? We have the spatial temporal reduction optimization which actually look into the frame which are similar and just compress them into the one aspect. This reduces the total processing of the videos by a huge extent. The second one is basically you have a caching you have a viral content which is basically coming up and you do not want to have the same content out there which is doing going through the entire pipeline and that's where you have a high similarity score and just skip the multi- aent system and just make a call on that. The third one which is really important is the metadata pruning. This is where we actually shrink the space from lot of candidates based on some of the metadata. For example, some topics and some creator which already have a really good record. That means we really don't need to process these all these images all all the videos from the creator which has a really good high authenticity score which are really doing really well on this where the video quality is really high engagement is good those kind of things. A metadata is something which can be used to filter out the video which shouldn't even go to the systems. So some of these flags u would be helpful. Um so the last takeaway that u u we basically we can take out of this room is that like decomposition t is a key. Uh decompose uh a problem as and when necessary. Adaptive optimization is really important for uh ROI and cost feasibility. Good evaluation is paramount. Everything in and out depends on this. This is the foundation of your entire system and entire VLMs and production monitoring and qualitative improvement are really essential to make sure this is sustainable in long term. With that, I'll end it and thank you very much for listening. Thank [applause]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "multi-agent-video-moderation",
  "signal": 0.55,
  "novelty": 0.5,
  "actionability": 0.5,
  "evidence": 0.55,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Инженер из Meta рассказывает архитектуру мульти-агентной системы модерации видео на масштабе 100М+, с полезными, но довольно общими паттернами оптимизации и декомпозиции",
  "knowledge_units": [
    {
      "claim": "Систему модерации видео строят как мульти-агентный конвейер: оркестратор-агент (reviewer) раздаёт задачи специализированному VLM-агенту (perceiver), который тянет видео, режет его на сегменты и собирает эмбеддинги/теги/OCR/таймкоды в единый JSON",
      "type": "workflow",
      "actionable": "При проектировании похожей системы анализа видео выделять отдельный 'оркестрирующий' агент и отдельного 'исполнителя-восприятия' (VLM с доступом к инструментам), а не заталкивать всё в один промпт/агента"
    },
    {
      "claim": "Вместо разбиения видео на кадры с фиксированным FPS используют адаптивную сегментацию по точкам temporal-change: похожие подряд идущие кадры схлопываются в один-два репрезентативных кадра",
      "type": "tactic",
      "actionable": "Для задач обработки видео сначала детектировать смену сцены/контента и обрабатывать только уникальные сегменты — это сильно снижает объём вызовов VLM/LLM"
    },
    {
      "claim": "Для вирального/уже виденного контента используют кэш по high-similarity score: при совпадении выше порога видео вообще не идёт через дорогой мульти-агентный пайплайн",
      "type": "tactic",
      "actionable": "Добавлять слой кэширования по эмбеддингам перед дорогим агентным пайплайном, чтобы не пересчитывать одно и то же для дублей/вирусного контента"
    },
    {
      "claim": "Пространство кандидатов для обработки заранее ужимают через metadata pruning — по репутации/authenticity score автора, вовлечённости и качеству видео, чтобы не гонять весь трафик через тяжёлую систему",
      "type": "tactic",
      "actionable": "Перед запуском дорогого LLM/агентного пайплайна фильтровать входящие объекты по дешёвым метаданным (история источника, прошлые оценки), пропуская в тяжёлую обработку только подозрительный остаток"
    },
    {
      "claim": "Автор формулирует принцип: переходить на мульти-агентную архитектуру только тогда, когда задача реально требует специализированных узлов (retrieval/understanding/reasoning) — если с задачей справляется один LLM/агент, усложнять не нужно",
      "type": "principle",
      "actionable": "Перед тем как проектировать мульти-агентную систему, проверить гипотезу «а справится ли один агент с одним хорошим промптом» и усложнять архитектуру только при доказанной недостаточности"
    }
  ]
}
```
