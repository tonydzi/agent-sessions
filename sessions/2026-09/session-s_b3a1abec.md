---
session: s_b3a1abec
date: 2026-09-27
words: 2028
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b3a1abec` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: KV Cache-Aware Routing and P/D Disaggregation on Kubernetes — Yuchen Fama & Ashish Kamra, Red Hat
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
All right. Um, welcome everyone to yet another inference talk. I hope you have had a good conference so far. And u, so in this session, I mean I'm sure you people who have been in the room uh must have heard these terms many times by now. So we're going to do a little bit more deep dive into the challenges of LLM deployments for agentic workloads and uh in this session we'll focus specifically on KV cache away routing and uh PD disagregation um and also you know when you when you look at public inference uh benchmark results you are typically looking at very steady state isolated highly sanitized numbers and what those benchmarks actually don't show you u is the chaotic reality of multi-turn interactions, massive context fluctuations which are very typical of agentic workloads. So we'll also try to pull the curtain back on some of those complexities. Um by by way of introduction uh my name is Ashish Kamra. I'm a senior manager of performance engineering at Red Hat. And with me >> hi I'm Yuch Chen. I'm the product manager at Red Hat Inference working closely with VLM and AMD core maintainers. also a contributor myself. >> So here is the agenda for the next 20 minutes or so. Um Euchen will start with an analysis of inference behavior in the agentic era and some of the core characteristics and challenges. Uh next we next you will walk us through the KV cache um utilization and management strategies. I will break down the mechanics of pre-fill decode disagregation and walk you through some some results and then Euchen will again bring it all back together with our ongoing case study on our favorite open coding model GLM 5.2. Um and just a couple of uh sources from our side if you are more interested in learning more about open source inference we have a free course free course on deep learning.ai AI uh by Cedric and with Andrew Ning. Um and the other is a series of blogs on the Red Hat developer portal on distributed inference concepts uh troubleshooting and deployment patterns. Uh and for those who may not be aware since Red Hat is better known as the Linux company for enterprise Linux and uh the Kubernetes company for Open Shift uh but more recently we are also a major player in open source AI inference with uh us being the top contributor in VLM LLMD and the case of projects and also uh having incubated guide LLM for benchmarking LLM compressor for model quantization and speculators for uh speculative uh decoding models and we also bring it bring all of that together in a optimized model hub on hugging phase under the Red Hat AI arc. Um and we are also building the platform for the next wave of agentic inference workloads and with that I will hand over to you to uh walk you through more of it. So we are currently um at this inflection point moving from the era of classic inference to the agentic era. So when we look at the real world agentic work workloads such as uh sweet bench and also watrices from real world cloud code sessions they fundamentally break many assumptions we made with classic LM serving. uh as you heard actually many times in previous sessions for example multi-turns and new standard we found from a few turns all the way to 3,000 turns and also because agent frequently reuse the uh system prompt and the total definitions we usually see super high cash hit rate um oftentimes well exceeding 90%. Uh another thing is input output ratio is uh is massive oftentimes over a 100 ratio and even higher and in many cases and on top of that the context management is is incredibly complex due to this high variance because we can't just simply take the average and oftentimes we need to look at the distributions and the P90 numbers especially when you do uh capacity planning and also we observe really interesting patterns like sub Asian panel which is which further complex uh complicates scheduling. So to help communities study um this patterns we collaborate with Google thank you and also IBM our parent company to add uh a a trace replay tool in the inference perf you heard from earlier sessions u from Ashoken and Jason. Um so yeah feel free to check it out and the link is here. Uh next slide. Oh, so transition from the class uh the characteristics um we just saw for agentic workloads. We're no longer chasing this um this this raw throughput in a steady state. We often need to optimize uh for example interactive latency and they're very um highly volatile and client-driven context because user and you know client define the prompt structure. So this introduced several critical challenges. First of all, KV cache management becomes super volatile because the context is client determined as I said. So oftentimes we face this like you know frequent evictions and rewrites and secondly we also need to tune um the engine like VM with upper layer uh scheduling and routing. It needs that coordination such as prefix routing especially when latency becomes a primary uh scheduling matrix rather than like a secondary or afterthought. And thirdly, we also need to rethink our metrics. For example, we need to measure cats throughput separately. Why? Because on the right, it's really clear that economic stakes is very high. So, this is the uh anthropic API pricing. You also heard from earlier sessions. There's 10x cost difference between cash and non-cash tokens. So, 10x difference on your um token balance sheet is is pretty serious impact on your business. So next let's let's look at how the KV cache is um both utilized and managed in LMD. So LMD router has this really flexible um endpoint picker plugins we call the EP that can route the request to the optimal pods and that meet the KV cache locality and also the load criteria. So the EP continue probe each pods like VM pod matrix to score each pod on like the running for example running and waiting request and then the KV cache utilization also prefix uh cache availability and so we can schedule requests to the optimal pod with the lowest load and al
...[middle elided]...
lly scale the throughput by simply adding uh preview workers without reconfiguring and um the decoup. So uh this highlights how AMD effectly effectively managed the complexity of combining like PB and DB and EPI scale. And also we found some interesting fun fact actually a couple days ago. Um B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B B Bf6 uh BF16 KV cache actually is faster than using like FPA uh KV cache for longer preview. Um this is also like we continue to explore and found like more interesting patterns, but more importantly uh we want to kind of just show the result really quick. So um for this uh data set agentic workload data set the ISO OSL ratio is pretty high 45 to1 ratio preview is uh is really the constraint you can tell um with 2P even 1D we have um 4x passer TDFT and also 60 uh% more requests and this is continuous like work in progress so the next step is we need to also put the upper layer lower TTFT and also adding more more preview replicas so um I know we're running out of time really quick. Uh we um the fundamental shift for agentic workload we're continuing to uh have this um uh agentic north uh northstar uh with session graph orchestration program award scheduling uh state reuse life cycle and also the uh agentic benchmark um we're working on. So you can find them uh in AMD upstream AMD and also you know feel free to join the SIG group and uh and contribute and um this is the very last slide. So distri distributed inference is not challenge uh every single comp a single company can solve along. We're proud to be uh building this uh future in the open alongside our incredible ecosystem collaborators uh core wave Google IBM Nvidia growing list of launch partners and industry adopters. So if you're passionate about the future of opensource inference, we invite you to join us. We do have a booth downstairs. Feel free to stop by, ask us any questions. And uh thank you so much for your time. [applause] >> [music]

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "llm-inference-serving",
  "signal": 0.7,
  "novelty": 0.6,
  "actionability": 0.55,
  "evidence": 0.65,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 300,
  "why": "Доклад Red Hat про особенности agentic-инференса (высокий cache hit rate, огромный input/output ratio) и практики prefill/decode disagregation с реальными бенчмарками на vLLM/LMD, но конкретика сильно завязана на VLM/LLMD-стек и быстро устареет.",
  "knowledge_units": [
    {"claim": "Агентные нагрузки (SWE-bench, реальные сессии Claude Code) кардинально отличаются от классического инференса: до 3000 ходов в диалоге, cache hit rate часто выше 90%, соотношение input/output токенов больше 100:1", "type": "benchmark", "actionable": "При капасити-планировании инференса для агентных продуктов считать не средние, а P90-распределения по длине контекста и cache hit rate, а не ориентироваться на steady-state бенчмарки"},
    {"claim": "Из-за клиент-определяемого контекста KV-кэш в агентных сценариях постоянно вытесняется и переписывается, что требует роутинга с учётом локальности префикс-кэша (prefix-aware routing), а не просто балансировки нагрузки", "type": "tactic", "actionable": "На проде с vLLM/LMD включить endpoint picker, учитывающий KV cache utilization и prefix cache availability по подам, а не только running/waiting requests"},
    {"claim": "Экономика кэша существенна: у Anthropic разница в цене между cached и non-cached токенами доходит до 10x, поэтому throughput кэша нужно измерять отдельной метрикой, а не как побочный эффект", "type": "principle", "actionable": "Добавить в мониторинг отдельную метрику cache token throughput/hit-rate как SLA-показатель, влияющий на себестоимость обслуживания агентов"},
    {"claim": "При prefill/decode disaggregation в условиях высокого input/output ratio (45:1 в их датасете) именно prefill становится узким местом: 2 prefill + 1 decode инстанс дают 4x улучшение TTFT и на 60% больше обработанных запросов по сравнению с недисагрегированной схемой", "type": "benchmark", "actionable": "При долгих системных промптах и малом выходе тестировать асимметричное масштабирование prefill-воркеров отдельно от decode-воркеров вместо единого монолитного пода"},
    {"claim": "В их экспериментах BF16 KV-кэш для длинных prefill оказался быстрее, чем FP8 KV-кэш, что противоречит обычному ожиданию выигрыша от квантования", "type": "tool-caveat", "actionable": "Перед тем как квантовать KV-кэш в FP8 ради экономии памяти, замерить TTFT на длинных prefill — квантование может замедлить, а не ускорить конкретно эту фазу"}
  ]
}
```
