---
session: s_a09bfec8
date: 2026-09-24
words: 2066
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-24 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_a09bfec8` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Skill issue: stop deploying vision language models, use them with Skills — Merve Noyan, Hugging Face
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hello and welcome to this talk on skill issue. It's actually no longer a skill issue. So uh by the end of this talk you will be able to build a lot with the vision models if you are already not doing it. So shortly about me, I'm Marv. Uh I've been working on computer vision since Lava in the fix times. Uh and lately I work on more agents and ondevice stuff because I'm a bit fascinated and I love vision language models so much that I even wrote a book on it. But I don't want developers to directly use vision language models anymore. And uh I want every single developer to start uh building vision langu vision applications end to end. And this talk is going to give you like a good baseline to do so. And common behaviors I observe with the developers is the fact that they try to use vision language models for everything but they you will never get real time. And when I mentioned real time, it's like you have a toaster and you get like 30 40 fps uh on it like whatever whether you are building like image classification, instance segmentation or whatever. And um they are not super robust in terms of like if you were to train like an RFDTR which Joseph spoke in the I spoke about in the first talk um it will always outperform your vision language model and I'm going to prove it today. And uh on the right hand side you can actually see me uh doing stuff with RFDTR. Um and another thing is that they don't read the licenses. Everybody's like whenever I post something about object detection, they always ask me about YOLO. Like YOLO is a good model. Uh but it's a it has AGPL 3.0 license I think. And I could swear on my life that there is like some developers that actually deploy it without knowing that they have to pay for it. Um so yeah like uh I want you to migrate to Apache 2.0 models today. And for this I have built something called web vision and it's kind of inspired by this post by Mazar. Basically what he does is that he gives um SAM 3.1 model as a tool to Gemma 4 to call and I find it super impressive. Um and today I built like a tool kit uh where you can do this with like even more things. So I'm kind of distilling myself. Um first off uh this toolkit has my favorite models as tools uh so that you can give it to your agent because your coding agent is a bit of a clueless computer vision engineer basically. Um and when I distill myself basically like whenever I pick a model I always check the following. So first up the license is the biggest priority for me. It has to be Apache 2.2 MIT or something non-commercial. Uh secondly uh the performance has to be on par uh depending on its size or architectural choices. So I check from the benchmarks uh whenever a model from a computer vision conference comes out and third vibes obviously and so this toolkit has a second part to it and it's a bit like a vibe training part which is the most exciting part. So I will go through it first. So I put myself in developers shoes to build like a vision application. Um if I have labeled images easy I can just train a model or like if I I can give my computer computer vision agent some tutorials uh to do that because it's all out there like we built transformers for it. Uh but if I have images only I have to annotate uh and then uh evaluate the annotations and then just train a model. But how can you do it on scale? You can actually use a vision language model as a labeler and the vision language models as judge and then train what you want. But how does this pipeline look like? So basically I built this and it has like it has VLM for labeling VLM as a judge and then training. Uh it's a bit of a long horizon tasks for coding agents and it has infra many infrastructure support. You can do this locally. You can do this uh remotely. So basically it runs on hugging face infrastructure. We have jobs that allow you to do oneoff batch processing or training. We also have like a serverless routing system called inference providers where you can use multiple providers and you we also have like buckets to dump intermediate data on top of the data set repositories, model repositories and so on. Um but what enables this work? First off, my favorite model, RFDTR, RFDTR segmentation. I'm currently working on segmentation at the moment. Um, we have better agents for long horizon tasks. Uh, that, you know, you have to babysit the labeling process, the training process, etc. Uh, and smaller yet more capable vision models enable you to label stuff very cheaply. And also with transformers we went for V5 refactoring etc. So like it performs better for vision models at the moment. And this is how the pipeline actually looks like. So first up I label the data set like I take an image data set like any image data set. I label that image data set with Q1 3.59B and then I pass the labeled data set to two judges. First one is Gemma 4 E4B which is like an 8B judge and then the second one is LFM 2.5VL which is nearly 2B uh it's relatively smaller basically I checked the research and it's better to have like an ensemble smaller judges and on top of it I merged the judgments so I also checked the research around it and most of the people ask the VLM or LLM to assign some score to it but those scores absolutely absolutely don't work especially if your models are of different size with judges. Um and then I pass it to train RFDTR medium or large. So I I chatted a bit with Rob people and they encouraged to use that and I'm going it it actually works. I'm going to show you very shortly. U but how does it work? So you take the repository and then you just ask it okay can you train it? Can you do the training on this data set on hub? And then it will start like if if the data set has labels like you can actually just get to training but if it doesn't have it you can just uh start annotating and I basically like the trick is I I pass the overlaid bounding boxes on images to the judge. So basically Qan technically outputs bounding boxes as tokens. I
...[middle elided]...
ibable parts like natural language is not a good gateway to it. Um so I think in that sense image guided detection could help like if you don't know about image guided detection you basically have like instance of an image like a haggi here as an example and then you ask the model okay detect this object in this image um across all of the images. I feel like it could actually somewhat help in the industry use cases where you cannot describe it by like um natural language. Um as well as I want to try um intersection over union merger sort of basically you have like labeled boxes and then judges boxes like you ask the judge to actually generate a box and then you take the intersection over union instead of asking judge to reject or accept and I'm working currently working on the segmentation support and thanks for listening if you want to actually learn more so basically I We have a small vision repository. It has everything about like fine-tuning models, quantizing models, multimodel models, everything around vision. Uh as well as transformers task guides. We keep them up to date has many um tutorials. Um, we also have hugging face skills that actually have computer vision specific skills as well as the infras skills that you can just do like a one prompt training. Again, um, and this is my Twitter profile and this repo is actually at GitHub Marvin uh, vision intern. I think I have qu um, time for one question. Thank you so much. Yes, >> you have plans for training. >> Um, he's asking if I have uh plans to train train VLMs themselves like a self-improvement type of thing. That would be super exciting. But first, I want to solve this thing of like developers actually training task specific models and then deploying on edge and then that could come perhaps. Maybe one more. Yes. >> Um, not really. I don't think so. I just use the because I wanted because a coding agent actually has the context. I wanted it to generate the prompt. Maybe one more. Okay. Thank you so much.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "vlm-distillation-pipeline",
  "signal": 0.6,
  "novelty": 0.5,
  "actionability": 0.65,
  "evidence": 0.45,
  "durability": 0.5,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад описывает конкретный воспроизводимый пайплайн (VLM-разметчик → ансамбль VLM-судей → тренировка специализированной модели детекции), а не просто рекламу или хайп о релизе.",
  "knowledge_units": [
    {
      "claim": "Специализированные модели детекции (например RF-DETR) превосходят vision-language модели по точности и скорости и единственные годятся для real-time (30-40 fps на слабом железе); VLM для этого не подходят.",
      "type": "benchmark",
      "actionable": "Не деплоить VLM напрямую для real-time CV-задач (детекция/сегментация/классификация) — использовать лёгкие специализированные модели, а VLM оставить для офлайн-разметки и обучения."
    },
    {
      "claim": "Рабочий пайплайн дистилляции: VLM размечает изображения (например Qwen2.5-VL), затем ансамбль из двух разных небольших VLM-судей (Gemma и LFM) проверяет качество разметки, после чего на очищенных данных тренируется специализированная модель (RF-DETR).",
      "type": "workflow",
      "actionable": "При отсутствии размеченного датасета строить связку auto-labeling (крупный VLM) → LLM/VLM-as-judge ensemble → тренировка компактной модели вместо ручной разметки."
    },
    {
      "claim": "Ансамбль из нескольких небольших LLM/VLM-судей надёжнее одного судьи; присвоение числового скора моделью-судьёй работает плохо, особенно если судьи разного размера — лучше бинарный вердикт или сравнение по IoU боксов.",
      "type": "tactic",
      "actionable": "В LLM-as-judge пайплайнах избегать scalar-скоринга (1-10), использовать ансамбль из 2+ разных по архитектуре судей и accept/reject или геометрические метрики (IoU) для агрегации решений."
    },
    {
      "claim": "Многие разработчики деплоят YOLO в продакшн, не проверив лицензию AGPL 3.0, которая требует платной коммерческой лицензии либо open-source своего кода.",
      "type": "tool-caveat",
      "actionable": "Перед продакшн-использованием CV/VLM модели явно проверять лицензию репозитория и предпочитать модели с Apache-2.0/MIT для коммерческих продуктов."
    },
    {
      "claim": "При валидации автоматической разметки VLM-судье передают не текстовые координаты, а изображение с наложенными (overlaid) боундинг-боксами — так судья точнее оценивает качество разметки.",
      "type": "tactic",
      "actionable": "В пайплайнах VLM-as-judge для CV-задач визуализировать разметку прямо на изображении перед отправкой судье, а не описывать координаты текстом."
    }
  ]
}
```
