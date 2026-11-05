---
session: s_2eeafca5
date: 2026-09-24
words: 1957
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_2eeafca5` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: From Ingestion to Agents: How AI Teams Build on Document Intelligence — Adit Abraham, Reducto
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Hi. Can everyone hear me? Sweet. We have a short 20 minutes here and so I wanted to jump in and get right to it. Uh my name is De. I'm the co-founder and CEO of Redducto. Uh and today we wanted to talk about one of the I think really practical but maybe less sexy parts of building agents that actually work in the real world uh which is data. Um I'm sure you've seen plenty of talks about data today. We primarily have focused on building infrastructure for anybody working with some of the hardest sources of data which is unstructured images, PDFs, spreadsheets, everything that humans are used to using day-to-day. Uh, have any of you used Reduct already or trial it? Cool. Um, I guess helpful context maybe to start is we're an agentic document processing platform. Um, so we help a lot of the world's leading AI teams build uh both AI applications and also workflows depending on what they're trying to do. Uh, that includes a lot of the AI natives that you've probably seen today. It includes the Harveys, the Lores, the Rogos of the world. Uh, but also some of the largest enterprises in the world. And I think that's important context for what we're going to talk about. Um, we work with the largest tech companies, global financial institutions, insurance orgs, people that have decades worth of historical data that historically has been really, really hard to actually use outside of a demo context. And across all these companies at this point, we've processed many billions of documents for our customers. I've gotten kind of lazy with that plus symbol at the end, uh, but the number keeps changing and so we'll let it sit there. Uh but the main thing that we've learned across those and what I wanted to focus on today is not actually a reduct product itself. It's the intricacies of what we've learned that hopefully you can actually take home and implement in the work that you're doing as well. Um and I think a lot of the work that we've done and a lot of the learnings we've had are in this sort of broader thematic context of the scope of AI applications has changed a lot recently. Uh from just like information synthesis products to actual agents doing work. And with that we found that there are a few things that are worth talking through. One is framing the problem itself. Uh the bottleneck that people face. Uh why PDFs in particular are hard even though you've probably seen two dozen different PDF processing launches on Twitter. Uh where we find strengths and weaknesses with different tools. Uh we think there's a right place in time for traditional CV versus BLMs. Um and then more interestingly I think the latter half of this talk will actually be focused on the next frontier. uh what we've seen be possible as a result of having agents in the loop uh things that we found as a result of being able to use harnesses for different types of tasks uh and our learnings around things like evaluations uh as you go from rag to building agent products but I'll start with the first thing which is something that I assume has been harped on a lot if you went to AI engineer a few years ago the word that you would have heard in every single talk would have been rag um and everybody was building some form of rag application for a while all applications ations were really some form of information synthesis, right? You would pull in information from some context, whether that's a perfect prompt or a file that a user uploaded and you would have something like a search product. Um, you'd have enterprise search, you'd have a chatbot that would do simple question answer on top of the content and that was it. But today, the buzzword that you've probably heard a million times is agents. Uh, and for those of you that are engineers, you've probably had cloud code or similar tool do a lot of your endto-end work for many, many tasks. And that same sort of shift is starting to happen for all sorts of white collar work. Um, whether you're in finance or insurance or healthcare, people are starting to make autonomous decisions. They're trying to create end-to-end work products, not just answer questions from a PDF, but generate and modify PDFs as well. And that's a very different framing. the tools that you need, the problems that you face change a lot versus just trying to build a retrieval uh platform. And the common core for all of this is it actually ends up being an even more importance problem to solve for when you start having these multi-step pipelines. If you're just doing question answer, there is obviously a risk that comes with just answering the question. But when agents are making multiple decisions that compound over the course of a source of files, when they're pulling in multiple sources of data, the risk of bad inputs becomes really, really pervasive in your pipeline. And that's what we focus on because at the end of the day, a lot of the value of language model tools in the real world only applies in the context to which you apply that intelligence. And for a lot of enterprises, data is unstructured, it is scattered, and it is multimodal. uh it's not this like cleanly organized repository. You have random teams and different organizations that go through and put things in Google Drive and Box and wherever else you might have things. Um you're going to have data for formats that are unstructured by default. You don't necessarily know what is in your corpus of information. And you're going to have all sorts of downstream problems that come with that. Um some of the problems are going to be parsing extraction accuracy and that definitely matters. But it's also going to be about problems like are you retrieving the right context? It's going to be about how do you actually interact with that context and apply modifications to it. And the thing that you've probably heard harp on and others in the space is PDFs are surprisingly still a very hard problem. Um I don't know if any of you follow Serge which is a data 
...[middle elided]...
 So, we create a CLI where instead of people creating a endto-end pipeline where documents always follow one specific flow, um, the agent will decide if it needs to read a certain type of document and they'll split that into two sets. Uh, one is a content field which the agent can read as it needs to. Uh, but the other is all the metadata that you would have wanted. If you're doing things like citations, you may want bounding boxes, so on and so forth. Um, I'll skip this part on editing. I think there's a lot of interesting work being done here. We've already released some of it, but in the next few months, you will see us look more and more towards things like document generation. But the recap for today, and I really appreciate your time, is one, I highly recommend that you decompose the parsing problem. To the extent possible, you should think of it as the right tool for the right task so that you can hit that perimeter frontier of accuracy, cost, and latency. Two, I think agentic verification is the biggest step change that the industry has had for a while and it's a really good opportunity for you to make sure that you're building pipelines that work in production. Three, I think it takes very little effort, but there's a lot of headroom from details like formatting the data for its consumer. or similar vein, I think it's really really important to think about not just the data processing but the the data orchestration and so you should always think about tools like classify and split as a way to augment your pipeline. Five uh make sure that you eval at every stage and six think through what that next frontier looks like for you because I think most successful companies in today's era have deviated a lot from what we used to do two three years ago. But if you have any questions uh please feel free to reach out at any point. My email is just first namered reductto.ai. Uh and you can also reach out on our website if we can be helpful for your use case. Thank you.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-document-processing",
  "signal": 0.5,
  "novelty": 0.35,
  "actionability": 0.5,
  "evidence": 0.45,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад сооснователя Reducto о переходе от RAG к агентным пайплайнам обработки документов даёт несколько практических, но довольно общеизвестных рекомендаций без глубоких технических деталей или бенчмарков.",
  "knowledge_units": [
    {"claim": "Парсинг документов стоит декомпозировать по типу задачи, выбирая между традиционным CV и LLM в зависимости от требуемого баланса точности, стоимости и латентности, а не использовать один универсальный инструмент.", "type": "principle", "actionable": "Разбить пайплайн извлечения данных из PDF на подзадачи и подобрать под каждую отдельный инструмент (OCR/CV vs LLM) вместо единого решения."},
    {"claim": "Агентная верификация результатов извлечения — ключевой шаг для доведения document-пайплайнов до продакшена, так как ошибки компаундируются в многошаговых агентных цепочках.", "type": "tactic", "actionable": "Добавить отдельный агентный шаг проверки/валидации извлечённых данных перед тем, как передавать их дальше по цепочке агентов."},
    {"claim": "Небольшие усилия по форматированию извлечённых данных под нужды потребителя (например, добавление bounding box для цитат) дают непропорционально большой выигрыш в качестве продукта.", "type": "tactic", "actionable": "При проектировании пайплайна заранее закладывать метаданные (координаты, ссылки на источник), нужные для последующих фич типа цитирования."},
    {"claim": "Паттерн 'classify-and-split' — агент сам решает, какой тип документа перед ним и как его обработать, разделяя контент и метаданные — полезен как способ оркестрации разнородных входных данных.", "type": "workflow", "actionable": "Внедрить этап классификации документа агентом перед основной обработкой, чтобы маршрутизировать разные типы файлов по разным под-пайплайнам."},
    {"claim": "Оценку качества (evals) нужно проводить на каждом этапе пайплайна, а не только на финальном выходе агента.", "type": "principle", "actionable": "Строить eval-наборы отдельно для каждого шага (парсинг, извлечение, генерация), а не только сквозной end-to-end тест."}
  ]
}
```
