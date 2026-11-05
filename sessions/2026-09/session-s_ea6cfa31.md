---
session: s_ea6cfa31
date: 2026-09-24
words: 2031
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ea6cfa31` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: From Scratch to SOTA: Training a 3B State-Space Vision Model — Krishna Prasad Srinivasan, Sarvam
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
All right. Um, hi everyone. Good afternoon. I'm Krishna. Uh, and I'm a general manager at Servin. Um today I'm going to tell you how a three billion parameter model uh small enough to run on a single GPU gets state-of-the-art uh in document AI and beats models 100 times larger in size. It is also a slightly unusual model in two ways. Firstly u the language model used is not a standard transformer. Um and the entire model building from data to training to compute uh was done end to end in India and for English and for 22 official Indian languages uh which I think uh are personally uh uh one of the hardest document intelligence problems uh in the world right now. Um this is how we went from scratch to SOTA. Who are we? Uh we are serv uh a sovereign foundation model company uh in India. We work across different modalities voice, text and vision. Uh in voice we have speech to text and texttospech models. In text we have uh a 30 billion and 100 billion parameter uh uh models and in vision we have a document intelligence model which is what we are going to talk about today. Um, India is largely missing from the machine readable world. Um, according to a published language distribution study, well under 1% of the common crawl uh corpus on which frontier models are trained uh have uh um Indian language representation. Now in several forums you may have heard Frontier Labs say that um India is their um India is one of their larger uh uh and fastly growing markets and to that end um India is still missing uh in terms of data from frontier models that uh um are being trained every day here. Now why is that? Uh primarily not because there is uh a lack of data or the knowledge does not exist. It is because the data has never been digitized and we are solving that problem at server. Um why is Indic document intelligence hard? Uh firstly the goal is that of knowledge extraction not just purely text extraction. Uh extracting pure text without logical coherence is meaningless. And secondly in index scripts the shape of uh the words and the language you see are very different from what a machine sees. that is Indian languages have a complex uh set of uni codes fused together to get right the language model needs to be strong at all 22 languages. Third, majority of Indian languages can be considered low resource due to which there is a lot of uh um lack in data today to train these models. Our answer to this is server vision India's first sovereign vision language model built from scratch. um a three billion parameter model with state space architecture data compute and training all of which done in India. When we started the initial work in late 2025 most VLMs uh in the OCR space were monolith VLMs. uh they performed page level OCR and we at the time took a contrarian bet to focus on block level OCR instead adding a document hardness around the model. Um a lot of models since then uh released uh uh recently in 2026 have converged onto the same uh hardness plus small model paradigm for OCR which shows a lot of value in the direction we uh set off. Serverom vision in particular uh has two hardness modules one for layout and one for reading hardness and a state space model uh VLM for block level OCR. Again um today uh why do we use state space and not a transformer? Um most OCR models today uh like general VLMs, open source VLMs like Quen, Gemma etc. are all transformers based. We took an alternate approach uh using an SSM. Why? Both are fundamentally sequenced models transformers and SSMs but with very different underlying mechanics. A transformer has every token look at every other token where the compute grows with square of the sequence length. Uh that is the L cross L interactions and the memory goes as the sequence grows as well. Now on the other hand, SSMs have a single state. They maintain a single state through the sequence updating it token by token. Now as compute grows only linearly, the memory stays constant for SSMS. Now why is this the right uh architecture for OCR? It really depends on the uh uh trade-offs here uh for long documents in particular which can lead up to uh uh 5 to 10,000 uh visual tokens per page and quadratic complexity of you know uh compute and memory becomes very expensive for inference. On the other hand, um doing block level OCR with somewhat of a lossy recall using SSMs can be justifi justified to uh um avoid high compute costs imposed by transformers. So how do you actually train this? We built a staged curriculum four stages each uh building on the last um stage one is texton pre-training uh 13 trillion tokens across English, Indian language, text, math and code. This builds the three billion parameters language backbone and a strong language prior is what lets the model resolve a smudged or an ambiguous text from the image. the same way you can read a half blurred word because you know which word is supposed to uh u be at the right place. So we focused on building the competence of the language model first uh before the model ever even sees a pixel. Stage two is where we performed continual pre-training uh on 300 million image text pairs. This teaches the language model general vision capabilities and teaches how to see how to interpret pixels and so on. Then comes stage three where we performed uh supervised fine-tuning on 100 uh uh million uh OCR uh samples. Now the um stage three is primarily focused on letting a general VM model become strong at OCR. What that includes is having diverse data across all 22 languages and English and also incorporating all kinds of uh uh document components such as tables and uh um equations and handwritten documents and so forth. Now and stage four is re reinforcement learning which helps push past the ceiling of whatever uh supervised fine-tuning is able to achieve. Here you will see this is a standard recipe. However, the moat here is the two things underneath the data layer and the eval layer. Um the first is the data engine. For 
...[middle elided]...
 country exists to begin with. Secondly on uh the training side what we have uh uh done in particular is to create data that can be added to a lot of training downstream. So uh we are at a very early stage in terms of AI becoming you know a regular parts of our lives and we need the data to start to be able to eventually get to a place where we can uh have personalized agents in the language you prefer in language I prefer and however I want in uh uh in some so to do all of that we need to start somewhere and the data needs to be created and if the data is of good quality then that helps the model become sota and If a model is sot then uh from uh insurance agencies to government organizations to others who care about sovereignity in AI right uh as a government body I cannot have a model deployed elsewhere and I don't know where the data is going for uh uh the transcriptions so I need to be able to control where the data is sent and when it is used how much it is used etc. So sovereignity becomes very crucial and hence this model really is now uh uh like it's been what four months since we launched and already we are we are digitizing 35 million pages. So that is that shows that the market was waiting for something sovereign in this space that can really kickstart uh the AI digitization wave in India. So yeah primarily like three aspects one on uh sovereignity the other is the model uh capability itself and the third is data uh that is required to train these models. Yeah, it is it is uh um 40% uh indic and then uh the rest is English and comprises of math and code etc. >> All right. Just a curious question. Um currently the uh the deployments we've made uh with this model are in different states uh uh trying to digitize regional languages and along with all the English and mixed language uh uh documents and hence we'll soon uh be able to train with the um uh feedback we get from uh the current deployment. So yeah, we have started that uh pipeline as well. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "vision-language-models-ocr",
  "signal": 0.6,
  "novelty": 0.55,
  "actionability": 0.5,
  "evidence": 0.4,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад с конкретными архитектурными решениями и стадийным рецептом обучения VLM для OCR, но без чисел бенчмарков и с заметным привкусом самопрезентации компании.",
  "knowledge_units": [
    {
      "claim": "Для OCR длинных документов (5-10 тыс. визуальных токенов на страницу) SSM-архитектура выгоднее трансформера: компute растёт линейно и память константна, а не квадратично, ценой некоторой потери recall.",
      "type": "tactic",
      "actionable": "При проектировании OCR/document-AI модели для длинных страниц рассмотреть state-space backbone вместо трансформера, если критична стоимость инференса, и заранее заложить допустимую потерю точности на редких символах."
    },
    {
      "claim": "Вместо monolith VLM, делающей OCR на уровне всей страницы, авторы сделали ставку на block-level OCR с отдельными модулями layout-hardness и reading-hardness — подход, к которому позже пришли и другие модели 2026 года.",
      "type": "principle",
      "actionable": "При разработке document-intelligence пайплайна разбивать страницу на блоки (layout detection → reading order → OCR блока) вместо одного end-to-end прохода по всей странице — это снижает требования к длине контекста модели."
    },
    {
      "claim": "Обучение шло 4 стадии: (1) чисто текстовый претрейн 13T токенов для сильного языкового backbone, (2) continual pretraining на 300M пар image-text для общего визуального понимания, (3) SFT на 100M OCR-примеров, (4) RL поверх потолка SFT.",
      "type": "workflow",
      "actionable": "При построении VLM для узкой задачи (например, OCR) сначала довести языковую модель до высокой компетенции на чистом тексте, и только потом добавлять визуальные данные — это экономит визуальные данные и ускоряет сходимость."
    },
    {
      "claim": "Сильный языковой прайор, сформированный до знакомства модели с пикселями, позволяет ей достраивать смазанный/неоднозначный текст на изображении по контексту, аналогично человеку, читающему смазанное слово.",
      "type": "tool-caveat",
      "actionable": "Если OCR-модель ошибается на зашумлённых сканах, проверить, не является ли причиной слабый языковой backbone — усиление именно текстового претрейна может улучшить устойчивость к шуму сильнее, чем добавление визуальных данных."
    }
  ]
}
```
