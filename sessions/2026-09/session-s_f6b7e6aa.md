---
session: s_f6b7e6aa
date: 2026-09-20
words: 2169
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-20 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_f6b7e6aa` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Two Bugs That Hid in Plain Sight: A vLLM Debugging Detective Story — Asaf Gardin & Yuval Belfer
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
So, put your model somewhere. Put your agent. You're hoping for the best. You're waiting for something to crash. Everything looks good. Everything's fine. and you see this and that's the problem right in these type of bugs there is no crash there's no warning no error and there's high confidence that's not a quality issue because uh right this is something that you don't really know what and how and why um welcome to this talk my name is Ival this is aaf and together We're going to take you on a journey of how we ended up fixing those type of bugs. A little bit about us. We work at AI21, which is an AI research lab. We started as a foundation model company, most famously known for Jamba, which is a hybrid architecture between transformers and mamba, which is an SSM state. And while we were doing those, while we were training those models, while we were shipping those models into production and had users and we had a lot of workload, we got into several interesting bugs. And these are the bugs that I think are the hardest to deal with because this is not a quality problem. It's not something you can take your research team and try to optimize or solve or make the model be better at something. This is an engineering problem. This is an issue where that there is high confidence but the output is bad. So let's break let's dive deep to the first case what we call the imposter request where just to set up the scene what are we talking about we are talking about how we during the training of our jamba model more specifically we did gpo which is a type of RL training and again this is a hybrid model layers of mamba and attention and just to make sure we're all aligned what is the type of a request So life lives life of a request. So we start with the prompt token tokenization and then in the forward pass we're doing both prefill and then decode. After that we finish the forward pass detoenization to go back to text. And the thing about the crime here is that it's bad on so many levels but mainly on these three. This is what we call the one in thousand gibberish. It's not something that will happen in the first 500 or 900 requests, but it will happen in the 10,00 which is rare enough to duplicate it easily but not right. It's too common to ship it. Sorry. H also it only happened in VLM not in other not in any other infra framework and it's something which is laid on set. It's not something that will happen if you have only few requests. You need some sort of workload. So it's rare. It's light on set and it's very engine specific. It's a very very hard task and we had to bring one of our best detectives to handle that. So I'll give it to SF to explain how. >> All right. Hey guys, thank you. Uh thanks you. So we're going to start with um trying to reproduce something that was very difficult to reproduce. Um and basically um VLM has got a lot of um a lot of flags, a lot of the CLI flags and a lot of knobs you guys can turn and tweak. Um and one of the things that helped us understand how to even reproduce it because when we try to reproduce it on the first time just sending prompts here, prompts there a few batches um it didn't really help us manage to get gibberish back from our model. The model responded back just fine. So what we did was is we tried to make it happen in a very very short um amount of time. So we'll get a a quick feedback loop when we try to deb debug it. So what we did was is we took one of the one of the um most default and most common um um flag that the VLM allows you to play with which is GPU memory utilization which basically allows you to to choose how much memory how much GPU memory you want to allocate for your for your weight for your activations and for your KV cache and so on. and we reduced it from 90% to 20%. And once we did that and then we started uh running a lot of requests uh simultaneously um all of a sudden request number let's say 8 854 suddenly returned gibberish and when we did that we uh we sampled all of the batches with temperature zero. So we'll be able to deterministically and constantly get the same request to get to return to return and respond with gibberish. Um so um like Ival said it happened only in VLM and um we used um in order to uh another way to reproduce it and to understand where the issue really came from. We used um uh hugging faces transformers as a baseline since transformers is a very had a very um vanilla and uh plain implementation of our mamba kernels as opposed to VLM which uh all the kernels and all the engine have gone through a lot of changes and modifications to support a lot of um cool features that VLM supports. So we use transformers as our baseline to understand whether or not there is an issue with our um with our inference or not with the model or not. So what we did was we took VLM and we sent uh all of our prompts through VLM and we generated a response all the responses we got and now in our hands we have the response along with the log props because because in VLM you're you able to get your log props out and inspect them. Then what we did was we took the full sequence the prompt and the generation and we uh uh passed it over to to hugging faces forward pass but all we did was run just the prefill um and then we uh uh samp we took this the logit out of the prefill um um response we ran it through softmax and then we were able to u to compare the divergence uh in the distributions of our tokens. Um that's a short uh pseudo code of how that look like. You can see here that we uh take up the prompt. We we run it through gen uh BLM's generate. We get the uh the response back along with the uh with the log props. We pass it over to to hugging faces forward pass. We only run it with prefill. Um we've created some function called compute log log props which um runs this is the softmax. Um then you calculate the difference between them and then you'll be able to tell the divergence between every one of the tokens log props. 
...[middle elided]...
two scenes and one criminal. Um both kind of you know they had similar symptoms. Both had silent gibberish and and silent log prop spikes which also kind of pro sometimes generated gibberish. They were both around the mamba state cache. Um they were both surfaced by memory pressure whether it was for worse or for the best and uh both found via log props um forensics. um stateful inference inference systems don't fail loudly they lie to you confidently I mean obviously sometimes you get crash you get out of bounds errors you get other you know exceptions and so on but sometimes there are some errors that don't surface up and you don't get a trace log you don't get anything you have to go and dig and understand why things happen um so if there some takeaways to take from this um presentation is build a log props comparison script if you need to compare your quality you need to compare it to understand whether you modelize the issues or not. Um log props comparison script with a baseline of some other inference framework that you have or built is always great. Um reproducing underression constrain memory. Uh crank the scale up, play with other knobs that the inference framework gives you and really try to understand where the issue comes from. Uh look for what moves um the failure shape, the timing, the space and the location. And when things don't really have identity uh thread identity through and what it also I want you to take from this and don't be afraid to even you know for complex uh systems like VLM or any other um complex framework don't be afraid to go dig in the code get your hands dirty um sometimes you know model languages LLMs are um they might tell you how things work but you know without you seeing it in your own eyes getting your hands dirty you won't get full understanding of what's going on. Um, thank you. You guys can add us on LinkedIn. Scan the QR code to read the actual blog that we've published with this finding. Um, yeah, that's it. [applause]

---

**Claude:**

01:51, 20 сентября 2026.

---

> `Bash` -- {"command": "echo done", "description": "noop"}

---

> `Bash` -- {"command": "echo '{}' > /dev/null", "description": "noop placeholder"}

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "vllm-inference-debugging",
  "signal": 0.85,
  "novelty": 0.75,
  "actionability": 0.75,
  "evidence": 0.9,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Реальный разбор двух тихих (без креша) багов в vLLM с mamba/hybrid-архитектурой (state cache), с конкретной методикой репродукции через снижение GPU memory utilization и сравнение log-probs с baseline (HF transformers).",
  "knowledge_units": [
    {
      "claim": "Тихие деградации качества инференса (нет краша, нет ошибки, просто иногда 'гиббериш') часто связаны со state-кэшем в stateful/hybrid (mamba+attention) моделях и всплывают только под memory pressure и на масштабе запросов.",
      "type": "tool-caveat",
      "actionable": "Если модель изредка выдаёт бессвязный текст без ошибок в логах — в первую очередь подозревать кэш состояния (KV-cache/mamba state) и эффекты, связанные с нехваткой/переиспользованием GPU-памяти."
    },
    {
      "claim": "Для быстрой репродукции редкого silent-бага полезно искусственно уменьшать GPU memory utilization (например, с 90% до 20%), чтобы чаще триггерить memory pressure и получать баг за секунды вместо тысяч запросов.",
      "type": "tactic",
      "actionable": "При отладке редких сбоев инференс-движка сознательно ужимать выделяемую память (KV-cache/activations) через флаги движка (в vLLM — gpu_memory_utilization), чтобы усилить частоту бага и сократить цикл обратной связи."
    },
    {
      "claim": "Диагностика расхождения качества между инференс-движком и baseline делается сравнением log-probs: прогнать те же промпт+генерацию через vLLM и через 'эталонную' реализацию (например, HF transformers prefill-forward), посчитать softmax и сравнить дивергенцию распределений токен-за-токеном.",
      "type": "workflow",
      "actionable": "Построить скрипт сравнения log-probs между своим инференс-движком и референсной (vanilla) реализацией модели — генерировать в движке с temperature=0, затем прогонять тот же полный sequence через baseline prefill и сравнивать логиты/log-probs по токенам, чтобы локализовать источник расхождения."
    },
    {
      "claim": "Детерминированный семплинг (temperature=0) позволяет стабильно воспроизводить редкий (~1 из 1000) баг на конкретном номере запроса в батче, что критично для отладки.",
      "type": "tactic",
      "actionable": "При охоте за редкими багами инференса переключаться на temperature=0, чтобы зафиксировать конкретный проблемный запрос и повторно его воспроизводить."
    },
    {
      "claim": "Для сложных инференс-фреймворков (vLLM и подобных) не стоит полагаться только на объяснения LLM о том, как работает система — нужно лезть в код руками, чтобы понять реальную причину.",
      "type": "principle",
      "actionable": "При расследовании сложных багов в чужом инференс-движке читать исходный код кастомных kernel'ов/движка напрямую, а не доверять высокоуровневым объяснениям (в т.ч. от LLM) о его внутреннем устройстве."
    }
  ]
}
```
