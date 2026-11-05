---
session: s_210a4d05
date: 2026-09-20
words: 2113
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_210a4d05` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Weight Folding, CUDA Streams, and the Bug That Made My Model Speak Backwards — Filip Makraduli
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hello everyone. Uh Thank you for coming and uh I'll start the talk now. So This talk is uh around a paper that I did um which is very simple. The proposition is very clear. It's basically two lines of algebra that make uh the RMS norm layer in transformers cheaper, quicker, and kind of improve improve it as like a layer in the transformer architecture. Similar to how layer norm once used to be the standard and then it was substituted by RMS norm. This follows along um this way of thinking. And I got the chance to kind of meet some people from the open source world and um I co-authored this paper together with uh Niels Graf who was the kind of the creator of this. And the work follows from there. So this is uh presented on archive. You can have a look, read it, test it out. There is a repo as well. And the concept the let's say the idea and the way of thinking it's easiest to explain with maybe flash attention. So in a similar way of how um flash attention kind of weights until there's a multiplication and tries to limit this uh communications between memory so that the whole process is faster. This is kind of a similar thought along those lines and it does certain improvements that make the RMS norm process much quicker and in in effect improve the whole transformer. And one question is okay, why RMS norm since that layer does almost none of the math? And that's true. So the share of the kind of math portion if you look at it is quite small. However, the clock time or wall time as they say is quite big and for example in one decode step. So right when like inference is performed the RMS norm can be started like 33 times. Of course, it depends on the model and so on. In the paper, you have the specific models and how this was tested. Um and the question is how this can be improved and how this wait for the matrix multiplication can be kind of avoided. And the reason why this is slow is because the GPUs are not slow or bad at math, but they're bad at everything else around the actual math. So that means starting the work, the actual work. So for example, starting the process as it happens in some of the experiments 33 times that takes a long time and for example, fusing um each normalization into the matrix multiplication can help avoid this. Also doing weight folding can help in kind of moving data between memory and um that's a process that's also slow for GPUs. And also waiting. Uh so, for example, deferring the division that's done in the RMS norm layer is also a way to avoid this waiting step. So, basically, what this paper does is it improves all these three aspects by doing a few algebraic tricks in the way RMS norm is computed. That's it. And math-wise, these are the tricks. Uh it's mainly around the first two propositions. One is weightless normalization. Uh you can see that here. Um and deferred normalization, so um that's the second one. And now in more newer architectures, there is a situation where um RMS can be kind of can appear twice. Uh for example, in Gemma 4, this happens. So, canceling the pre-normalization also works. Um and all of this is algebraically proven in the paper. And the first proposition is this where kind of the the gain and the weight fold folded to one matrix W, uh you can see here with an asterisk. And that is computed offline, similar to how maybe in flash attention, you compute some stuff on the side so that there is no uh communication between memory all the time. So, this is one step that's kind of um done, this weight folding. And the other step is um deferring um the scalar the scalar divide of the matmul so that they can be done in parallel. So, in a normal case, you would have to compute once, then wait, and compute again. In this case, the idea is to kind of split this so that it can be parallelized. And the third one, which is kind of a version of this is that um there is kind of if there are two um because this is scale invariant, one of them can be dropped and this still works. And this is applicable to newer models um that can have this architecture and implementation. So, in order to make this happen in real life, especially this proposition number two, um so for this one, for example, it's easy. There is a repo called Transformer Tricks. You can just apply this to any model and it works. But in order to do this, there is some kernel work. So, it's not as straightforward to do. So, in order for me to do that, I was implementing this and I came out with this experiment once. So, it looks okay in general, where it's like, "Okay, the prompt is the Transformer architecture revolutionally revolutionized NLP because and then there is some kind of expected output." But in the output I got, I saw this repetition and one-step lag, as you can see here, the word because appears again. And there was something happening with the GPU streams and I was trying to figure out what was happening. And I was getting this one-step lag and kind of um outputs that were from the past in a way. Um and in debugging all of this, I realized that um in the process of building something like this, so as I explained the proposition two or deferring these two operations, um in CUDA, you can do two things. You can do like tensor cores that do one part of the matrix multiplication and you can do CUDA cores that kind of run stuff like element-wise operations, reductions, square roots, and so on. So, the idea was to do this in parallel and get the benefit of what I was explaining in the paper to actually test out this concept. So, this is how it was supposed to look like. So, there is if you do things sequentially, there is this idle waiting time when you when the vector unit computes the RMS and scaling, and then there is a matrix multiplication. So, the idea was okay, with flash norm, which is the technique in the paper, you're supposed to do those both in parallel. So, the matrix unit computes the matmul and the vector unit computes the RMS. So, in that way you save uh tim
...[middle elided]...
u want and kind of do that end-to-end bigger use case. And the way site works is this production cluster helps you deploy the models, so you can have a look at site's repo as well for more details on this. Um and also there is a smarter queuing mechanism that helps you, especially if you work with smaller models cuz when doing the flash norm stuff, I worked with like smaller llama models and also with small agents from hugging face. So, having a way to deploy smaller models that can also work on like the same GPU so that you don't have to spend your money on GPU cost, but actually kind of switch models around, especially smaller models. It was quite useful. And you can also control the model configs through an API as well as the cluster, which is also pretty convenient without having like an infra guy supporting you in your open source research. So, that's cool as well. Um, and you own your cloud, which is useful if you want open weights, open models, open source. And there's also like a catalog that Sci has of different models, um, not just the ones I mentioned, but you can have a look. There's also re-ranking embedding models if you're building something along those lines. And with that I'm kind of finishing this story of my research journey where I co-authored this paper, um, around the technique that improves the transformer, but also found a way kind of to bring this to, let's say, production and test it out and find a way to play around with this open source models. And feel free to contact me on LinkedIn, maybe if you have any questions or contributions. A lot of this stuff that I've mentioned, like some of them are PRs on like vLLM or on Hugging Face. You might find them all around. You can also see the check out the paper. That's the archive link that you have there. Um, and you also have the Sci repo and my LinkedIn. Um, so thank you very much for attending. >> [applause] [cheering] >> And you can catch me for questions. We'll be here, close by. >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "rms-norm-kernel-fusion",
  "signal": 0.68,
  "novelty": 0.55,
  "actionability": 0.5,
  "evidence": 0.8,
  "durability": 0.7,
  "volatility": "medium",
  "half_life_days": 730,
  "why": "Автор доклада — соавтор реального arXiv-препринта про ускорение RMS norm (weight folding, deferred normalization) и честно разбирает свой баг с CUDA-стримами, но это узкоспециализированная kernel-инженерия, а не то, чем каждый день занимается разработчик агентов/RAG.",
  "knowledge_units": [
    {
      "claim": "RMS norm почти не даёт вычислительной нагрузки (мало FLOPs), но может вызываться до ~33 раз за один decode-шаг, поэтому реальная задержка (wall time) идёт не от математики, а от накладных расходов запуска ядра и ожидания на GPU.",
      "type": "principle",
      "actionable": "При оптимизации инференса трансформера считать не долю FLOPs слоя, а количество его запусков за шаг и стоимость запуска kernel — это подскажет, какие 'дешёвые' по математике слои на самом деле съедают время."
    },
    {
      "claim": "Weight folding: коэффициент усиления (gain) RMS norm можно заранее (офлайн) слить в следующую матрицу весов W*, избегая лишнего перемещения данных между памятью во время инференса.",
      "type": "tactic",
      "actionable": "Если пишешь свой инференс-движок или кастомный kernel, попробовать заранее сворачивать параметры нормализации в соседние матрицы весов вместо вычисления их на каждом шаге отдельно."
    },
    {
      "claim": "Deferred normalization: скалярное деление в RMS norm можно отложить и выполнить параллельно с матричным умножением, используя отдельные CUDA-стримы (tensor cores для matmul, CUDA cores для нормализации/reduction), вместо последовательного 'посчитал-подождал-посчитал'.",
      "type": "tactic",
      "actionable": "При написании custom fused kernels для нормализации+matmul планировать параллельное исполнение через разные типы ядер GPU, а не последовательный пайплайн, чтобы убрать простой (idle time)."
    },
    {
      "claim": "Наивная параллелизация RMS norm через CUDA-стримы без правильной синхронизации создала гонку данных: модель повторяла предыдущий токен с задержкой в один шаг ('говорила задом наперёд'), потому что вычисление использовало устаревшие значения с прошлого шага.",
      "type": "tool-caveat",
      "actionable": "Внедряя многопоточные/multi-stream CUDA-оптимизации в инференс LLM, обязательно проверять корректность синхронизации между стримами тестом на повторяемость/лаг вывода — молчаливая гонка данных даёт правдоподобный, но систематически сдвинутый по времени результат."
    },
    {
      "claim": "В архитектурах с двойной RMS norm (например, Gemma), из-за scale-инвариантности одну из двух нормализаций (pre-normalization) можно алгебраически убрать без потери эквивалентности.",
      "type": "tactic",
      "actionable": "Для конкретных моделей с парной нормализацией проверить, применимо ли сокращение одной из RMS norm по описанной в статье алгебре, прежде чем оптимизировать обе по отдельности."
    }
  ]
}
```
