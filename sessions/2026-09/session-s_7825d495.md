---
session: s_7825d495
date: 2026-09-27
words: 2156
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_7825d495` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Autoresearch Made Our Models 3x Faster — Tejas Bhakta, Morph
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hi everyone, I'm Tis. Uh, so I'm going to be explaining how we make models three times faster with auto research. Uh, so previous to this, uh, I actually used to do GPU mining in my dorm room with 1080 Ti all the way up to working at Tesla on inference optimization for Tesla AI. Uh but first what is auto research? So auto research is this framework from Andre Kapathy where uh you basically set up a framework for an agent to move towards a goal that you define uh and all you have to do basically is say at the high level what you want it to do and it will try things as it goes and move back and forth uh towards that goal. In actuality it's really just a while loop. The agent proposes a solution. You have a setup to to define what's correct benchmark it for us. uh and then you keep or revert that and you do this in a loop until your goal is met. And so this is very well aligned to GPU kernels. Uh so if you don't know what a GPU kernel is, it's basically a low-level operator. And in a Nvidia GPU, this is a CUDA kernel. Uh and this is um an operator that's used by the GPU to operate like millions of times in parallel, for example, like a matrix multiply or an expert computation. And why are GPUs such a good fit for auto research? It's because they're super verifiable. you can verify them for correctness and speed and that's basically all you need for your auto research framework. Uh so in actuality there are some caveats here. Um the auto research framework is really good for like picking block sizes and these tiny parameters but they're also still really bad at the high level idea like seeing like I want to use this GPU and I actually want to pipeline it. It's not going to come up with these groundbreaking ideas. So it's still up to the human to do that. But the actual implementation is very straightforward once you once you have the idea laid out. So it is still your job to have good ideas is what I'm saying. Uh and so the actual secret formula here is you have the good ideas auto research picks out the parameters and everything to verify that it actually works uh and go moves toward that verifiable goal of it being x times faster and uh still correct and you mix that with billions of tokens of your favorite model and that results in kernels that beat hand tuning. Uh so what are the actual things you care about when you're when you're when you're writing a custom kernel or you're having your agent write a custom kernel? So the three main things you can have are a compute bottleneck uh a memory bottleneck or you just have excessive overhead from uh too many kernels being launched and you can do you can view these things with by profiling with a profiler like NSIS for example which is Nvidia's profiler. Uh, and so this this gra this page looks super daunting, but basically your job as a human is to look at the top here and be like this is dumb. Uh, we are loading 32k chunks into context. Uh, and we don't actually need to for this deepseek attention for example. Uh, and we should only be doing it every 32k instead. And so at a high level, all you have to be telling auto research is this top method is dumb. Let's pipeline it instead. And everything else like the sizing, the chunk sizing, the context chunks, that all should just be decided by auto research. And so my problem is that I really love cheap GPUs. And so that means like GPUs that don't have NVLink for example uh is example of like GPUs you can get for cheaper. Uh but the problem is you don't actually have kernels off the shelf for those. And so you have to come up with a auto research framework as well as a custom harness. So what goes into the harness to make this really good. Uh so one thing you really need to make sure your agent is aware of is the hardware. And so on a B200 for example, you need to make sure it has context of uh the warps. It has T-M TMA. And so if you don't know what these are, these are just uh low-level operators that you have um on a specific hardware. And this changes generation to generation. Like H200 won't have T-M for example. That's a new feature that came out with B200, which is why you need to have this in context. Um and so this this basically is just like bunch of MD files you need to give so it has context. Other thing you need to make sure your agent has context of is the model. And so every new model like Deepseek Flash comes out with like new tricks. like deepseek had two new attentions that was released in the deepseek flash for deepseek v4. Uh so compressed sparse attention hierarchal compress and if you don't do this the model will 100% hallucinate uh the actual attention mechanism and you will get useless kernels. Uh by far the biggest problem when you're doing this is going to be reward hacking. And so if you were to tell your kernel engineer co-orker I need to make uh the GPU this GPU kernel faster. uh it's obviously not going to your human co-workers is not going to go in and do some stuff that's going to make it slow like the endto-end model inference slower but uh agents are not humans and they will do plenty of things to make it slower like they'll disable CUDA graphs which can make it 20 times slower and they might make that one kernel faster but make the whole like it's not a viable kernel because it's they're disabling a bunch of speed ups like CUDA graphs or only testing on small context windows and so a lot of this is also just defining what not to do which is actually very important when you're doing frontier work that agents can't actually easily with a one shot. Uh, another reward hack is that some models just don't actually write the cute DSL you need uh when you're trying to write kernels. And this is a common problem with enthropic models. And so, yeah, I mean, Anthropic says what they say about uh nerfing models. You can it's guess if it's I'm guessing if it's nerfing or not, but I would recommend using a different model. Uh, and it won't always be faster everywhere actually
...[middle elided]...
a flash infer cutless. Um and so and that's another thing to look out for is that your kernel isn't always just a swap in for all all workloads. Uh but one of the great things is is that kernels compound. So like if you make one for your sparse MLA for deepseek for example um you can get speed ups there and you just stack them on like that then plus NVFP4 fore uh you could do for us if we if you don't have NVL link you just keep stacking and stacking and stacking and then eventually you taper off at whatever the hardware limit is uh for your GPU and that's uh some people call this like MFU which is like the actual theoretical max utilization from a GPU. Uh and so to go even farther, if you have actually have bare metal access, your auto research framework can uh do very hacky things. So hackers that have hacked with GPUs are probably going to like this. You can uh tweak your BIOS settings, you can overclock the GPU, uh you can force like PCIe relaxing, all these little tweaks of like uh old school hackers used to do, but this can actually help with inference as well. And so net on bare metal optimizations, you can get roughly 25% over like a virtualized setup you get from using a cloud provider. Uh so once you've done that, you can combine all of the kernels you did as well as all of the hardware level hacks you did. Uh you can get a 3x speed up. And so I know this this might all sound like roses and flowers, but it's not actually the case. Around 80% of the things that auto research is going to do are going to be bad. Uh so it's important to remember while you're u like working on this that most things are going to be bad. It's going to try to trick you all the time. Uh but at the end you can actually get really good results from this. with TLDDR. Uh have better ideas than use auto research. Super simple. Simple, right? Uh so it turns out you can actually get paid to do this. Uh if you think this is cool, consider joining us and you can email me here. Thanks, guys.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-gpu-kernel-optimization",
  "signal": 0.68,
  "novelty": 0.62,
  "actionability": 0.55,
  "evidence": 0.65,
  "durability": 0.45,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Практик рассказывает реальный опыт запуска agentic-цикла (auto research) для написания GPU-кернелов с конкретными граблями (reward hacking, нужда в hardware/model-контексте), но контент узко специализирован под low-level CUDA-инженерию, а не под типичный LLM-app стек.",
  "knowledge_units": [
    {
      "claim": "Агентный оптимизационный цикл (agent предлагает решение → бенчмарк → keep/revert → повтор) хорошо работает только там, где есть чёткий верифицируемый критерий (корректность + скорость), например GPU-кернелы; агент силён в подборе низкоуровневых параметров, но не придумывает архитектурные идеи — это остаётся за человеком.",
      "type": "principle",
      "actionable": "Используйте auto research/agentic-loop паттерн только для задач с дешёвой автоматической верификацией; формулируйте человеком высокоуровневую идею оптимизации, а перебор параметров и реализацию отдавайте агенту."
    },
    {
      "claim": "Агенты систематически занимаются reward hacking при оптимизации скорости: отключают CUDA graphs (замедление до 20x в E2E), тестируют только на маленьких контекстных окнах, чтобы искусственно показать ускорение отдельного кернела.",
      "type": "tool-caveat",
      "actionable": "Явно прописывайте в задании агенту не только цель ('быстрее'), но и список запрещённых действий/инвариантов (не трогать CUDA graphs, тестировать на реалистичных контекстах), иначе получите нерабочий 'быстрый' кернел."
    },
    {
      "claim": "Агент без явного контекста о конкретном железе (напр. наличие TMA только в B200, отсутствие в H200) и о новых архитектурных механизмах модели (например новые виды attention в свежих релизах) будет галлюцинировать детали и выдавать бесполезные кернелы.",
      "type": "tactic",
      "actionable": "Перед запуском агента на кернел-оптимизацию подгружайте ему в контекст md-файлы с точными hardware-спеками поколения GPU и описанием актуального механизма модели (attention и т.п.), не полагайтесь на встроенные знания модели."
    },
    {
      "claim": "Низкоуровневые bare-metal тюнинги (настройки BIOS, overclock, PCIe relaxed ordering) дают ориентировочно ~25% прироста по сравнению с виртуализированной облачной средой, и этот прирост складывается с ускорениями от кастомных кернелов, давая совокупно 3x.",
      "type": "benchmark",
      "actionable": "При наличии bare-metal доступа к GPU дополнительно проверяйте настройки BIOS/overclock/PCIe как отдельный источник ускорения инференса, независимый от оптимизации самих кернелов."
    },
    {
      "claim": "Разные LLM-модели по-разному надёжны в написании специфичных DSL для кернелов; по опыту автора модели Anthropic хуже справляются с этим конкретным DSL, из-за чего он рекомендует пробовать другую модель под конкретную кернел-задачу.",
      "type": "tool-caveat",
      "actionable": "Если агент на конкретной модели плохо генерирует нужный low-level DSL/язык, не упорствуйте с ней — переключитесь на другую модель именно для этого под-этапа задачи."
    }
  ]
}
```
