---
session: s_e5838049
date: 2026-09-27
words: 2011
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_e5838049` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Beating RL With Reflection: GEPA and Optimize Anything — Lakshya A. Agrawal, GEPA
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hi everyone, my name is Lakshia Agraal and today I'll be presenting on behalf of a very large effort uh the problem of reflective optimization or how can we self-improve prompts agents and models from textual feedback. The question we start with is how can we teach AI to perform new tasks. The standard way has been to perform weight updates with gradient descent either during pre-training, supervised fine-tuning or reinforcement learning. This has proven to be extremely effective, but it requires a huge number of examples. trillions of tokens for pre-training, tens of thousands of labeled examples for supervised fine-tuning or hundreds of thousands of rollouts for reinforcement learning in domains like math, coding, etc. However, most teams do not actually have that much data or compute and in fact the problems are that we are trying to tackle with AI now are bottlenecked by sample efficiency. What do we mean by that? Two things. First of all, there is low availability of domain specific knowledge resources which means there is not enough data to perform offline algorithms like SFT. Second, the domains that we are trying to apply AI increasingly are having expensive rollouts where either the LLM workflow pipeline or agentic rollouts are itself uh very slow or expensive to do or the task metric is very slow or expensive to execute. We are seeing that agents can now work for hours on end and if you were to apply an online learning algorithm to this uh it would require hundreds of thousands of rollouts and it would not be feasible. So we are seeing increasing use of agents for real world product uh applications where uh these invoke tools which can also be long running further exacerbating the sample inefficiency issue. The current dominant paradigm is reinforcement learning with verified rewards where given a model and a task, we perform any number of parallel rollouts and get rewards at the end. Finally, an algorithm like GRPO takes these rewards and converts it into gradients that are applied back to the model. However, as we can see, there was a lot of information in each of these rollouts, but we only learned an O of one score and propagated that via gradient descent. We can see that there is chains of thought, the tool calls made to the environment, the envir environment's responses to those tool calls, which could potentially contain error messages which also provide diagnostic value and we learned almost nothing from all of that. So the question we ask is can we make use of this other extremely rich information. Our idea is to perform reflective optimization in text space where instead of only using the zero or one reward signal, we can have a language model or an agent look at the trace of the entire rollout and reflect on what worked in them, what did not work in them. And this reflection could potentially use all intermediate outputs and potentially even make other tool calls such as retrieval from your company's knowledge base or some guide textbook and so on. So that's the first key idea and the second is that instead of only updating weights with small deltas, we can instead update a prompt where a single natural language update can give a very large behavior change. Let's take a simple example. Let's say you're tasked with writing a text summarization system and the prompt of that system says generate a oneline summary. If I just go and tweak that prompt to say generate a 10-line summary, we can all agree that the behavior of the system would change quite significantly with that just one word change. And making that one word change is quite quick and we can reflect on our own behavior and identify what needs to change. If we were to achieve a similar kind of behavior update from our AI system, we would have to have thousands of gradient very tiny gradient updates sequentially. So with that key idea, we proposed JPEA which is a reflective prompt optimization technique for agents. It uses an evolutionary loop along with a novel parto-based candidate selection which I will come to later. It is akin to doing reinforcement learning in text space where instead of just rewarding receiving a reward score we are actually obtaining score along with textual feedback which can be very domain specific and learn all about the domain from it. Let's compare Japa with gRPO which is one of the leading RL techniques. On the x-axis we have the number of training steps uh also proportional to number of data samples seen and on the y-axis we have the performance on our domain that we are training for. And what we can see is that Japa in just one round of reflection using just three data points is already able to get twice the performance gains that gpo got after 25,000 rollouts. Continuing to run Japa for a few more steps further increases that gap itself by another 2x. I want to note here that the model Quen 38B is optimizing itself here. There is no external expert teacher involved whatsoever. And what does Japa learn? Unlike prior prompt optimizers somewhat which would uh uh use model idiosyncrasies like my grandmother will be really angry if you don't generate a good prompt. Here Jpa is actually giving a very detailed problem specification which includes how to make sense of the input. What is the purpose and context of this particular pip part of the pipeline? What are some key observations and lessons from the data? So the prompt we are seeing here is for the second hop of a multihop question answering system where given a question we need to retrieve some documents that could potentially answer that question. Look at those documents summarize it and then finally answer the question. And here what we see is Japa has found out that first hop documents that often cover one entity or aspect and the second hop should actually be uh recovering documents that are related to it. We have seen that human engineering teams whenever a new model comes out spend weeks of their time manually tweaking one 
...[middle elided]...
tive tasks which are very hard to evaluate jpa can actually learn evals for your task from production traces. The way to do that is you collect a bunch of production traces from your agent. Get a human to annotate just about 50 of those trajectories giving very detailed feedback. This is a long response. This is a short response. This is a good response. This uses this terminology, whatever. And once you get those human annotations, you can use JPA to optimize an LLM as a judge prompt. And you can use that LLM as a judge prompt then to go back and optimize your agent and deploy that agent. And this becomes a data flywheel where you can keep improving it. And this is a successful paradigm that uh some leading teams in production are already using. Then the question we get asked is like can we actually use this uh reflective optimization to train models and we recently had this paper called learning fast and slow where we propose fast slow learning where we can co-optimize model weights and prompt harnesses and this shows some very strong properties that one would want in a continual learning algorithm. Um I don't have much time to go over details but please uh look at the uh papers and uh since uh since release Japa has been used in production by these companies as well as the main methodology in these papers and here the CEO of Dropbox and Shopify are talking about their use of Japa and OpenAI also wrote a blog post about how you can build self-improving AI systems with Japa. Um so it's very simple to get started. It can plug into any framework, any model and it has absolutely zero hard dependencies. So you can deploy it any in any kind of setting. So um don't be afraid to optimize in the tech space and many problems can be framed as optimization. So bring actionable side information and surface as much domain specific information as you can to optimizers and the optimizers of future will be able to work with them. So please go and check it out. Thank you very much.

---

**Claude:**

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "prompt-optimization",
  "signal": 0.75,
  "novelty": 0.55,
  "actionability": 0.7,
  "evidence": 0.65,
  "durability": 0.6,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад про GEPA — метод рефлексивной оптимизации промптов текстовой обратной связью вместо RL/градиентов, с конкретным воркфлоу для обучения LLM-судьи на продакшн-трейсах и графиками сравнения с GRPO.",
  "knowledge_units": [
    {
      "claim": "GEPA (рефлексивная оптимизация в текстовом пространстве) на бенчмарке обошла GRPO по сэмпл-эффективности: за один раунд рефлексии с 3 примерами получила 2x к качеству, которое GRPO достигла только после 25 000 роллаутов, без внешнего учителя.",
      "type": "benchmark",
      "actionable": "Если задача упирается в дорогие/медленные роллауты (агенты, долгие тулколлы) — пробовать оптимизацию промпта через рефлексию LLM над трейсами вместо RL/файнтюна, особенно при малом количестве примеров."
    },
    {
      "claim": "Вместо использования только скалярной награды (0/1) от роллаута, можно скормить LLM весь трейс (chain-of-thought, вызовы тулов, ответы окружения, ошибки) и попросить её отрефлексировать, что сработало, а что нет, и переписать промпт.",
      "type": "tactic",
      "actionable": "При отладке агентных пайплайнов логировать полный трейс (не только финальный результат) и использовать отдельный LLM-проход для анализа трейса и генерации улучшенной инструкции/промпта."
    },
    {
      "claim": "Для доменов с трудно формализуемой метрикой качества можно построить flywheel: собрать продакшн-трейсы, вручную детально аннотировать ~50 из них (что хорошо/плохо, терминология, длина), прогнать GEPA чтобы оптимизировать промпт LLM-судьи, а затем этим судьёй оптимизировать сам агент.",
      "type": "workflow",
      "actionable": "Для агентов без чёткой автометрики: собрать 50 размеченных вручную примеров с подробным фидбеком, построить через оптимизацию промпта LLM-as-judge, затем использовать этого судью как сигнал для итеративного улучшения промпта продакшн-агента."
    },
    {
      "claim": "Одно точечное текстовое изменение промпта (например 'однострочное summary' → '10-строчное summary') может дать такой же по масштабу сдвиг поведения системы, как тысячи мелких градиентных обновлений весов.",
      "type": "principle",
      "actionable": "При итерации над поведением LLM-системы сначала пробовать точечные, целенаправленные правки промпта — это дешевле и часто эффективнее по сравнению с попытками зафайнтюнить модель под нюанс поведения."
    },
    {
      "claim": "GEPA заявлен как не имеющий жёстких зависимостей и подключаемый к любому фреймворку/модели, уже используется в проде компаниями (упомянуты Dropbox, Shopify) и описан в блог-посте OpenAI про self-improving системы.",
      "type": "tool-caveat",
      "actionable": "Перед тем как городить свой пайплайн оптимизации промптов с нуля — проверить готовую библиотеку GEPA как стартовую точку для агентных систем без доступа к весам модели."
    }
  ]
}
```
