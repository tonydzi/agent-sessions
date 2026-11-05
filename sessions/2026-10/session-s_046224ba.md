---
session: s_046224ba
date: 2026-10-25
words: 2055
turns: 2
tools: "ReportFindings"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-25 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_046224ba` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Don't Trust Your AI Agents. Test Them Like a Scientist — Stephanie Jarmak, Omni Analytics
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] My name is Stephanie Jarmak. I am an AI engineer as of a couple weeks ago at Omni Analytics where we have a platform that has like a governance semantic layer to have a shared understanding of business data using our beloved agent Bloopy. Before that I spent a year at Sourcegraph where I was a solutions engineer for Amp, a coding agent, and then I moved into some sort of amorphous type role where I was largely doing their evaluation platform. I built a very large public benchmark called Code Scale Bench to understand how agents are working across very complex code bases. And then prior to that I was an astronomer. So I come from this from a research scientist sort of point of view where I relentlessly question everything, hence the title of Lies, Damned Lies, and Evals. It says how to trust your agents, but I think largely this talk is mainly about how to not trust your agents. So here's one example of a run I had done back at Sourcegraph when I was testing out their code search MCP tool. This is just to show all of the different sort of numbers that you can have after you run a certain evaluation. The what I was trying to do was figure out hey, why isn't this coding agent actually using the tool that I'm trying to get it to use? And so, you know, it ran. I have all the traces and everything, and then I, you know, looked at some of the primary sort of metrics that you're looking at when you evaluate the overall effectiveness of a tool. And it showed we basically what I had done was I changed the initial prompt given to the agent, and then I ran it cuz I wanted it to use the tool. And what I saw was okay, uh, it was 28% cheaper. That's That's interesting. Um, but, you know, that shouldn't really change any of my decisions around what I'm actually trying what I'm interested in measuring and understanding in changes to um, the actual harness and setup, uh, because it still didn't use the tool. Right? So, you need to be able to understand like what it is you're actually trying setting this up. The The 28%um, is maybe an interesting avenue to go explore, okay, we have some level of like experimental space to be figuring out what's the variance and what's going on with the with the cost measurements. Um, but we still weren't like seeing it actually use a tool um, that it was supposed to, and, uh, basically we had this whole like, um, indication that it was receiving certain information and then just trusting that that information wasn't there, and that was purely because it didn't use that tool. And I also want to talk a bit about the impact of the harness itself. Um, so, here's an example, and this was from a third-party source where they had 63 or so tasks, um, on Turbo Bench 4, which is a pretty popular, widely used, um, benchmark for coding agents. And they, you know, you have like, let's say you're trying to pick which model you're going to, um, put into your harness. Um, so, here's a comparison they did they did they did with, um, Opus 5 then and Astra, and they saw that, you know, with Open Hands, which is one of the open harnesses, um, Opus 5 beat it out. But then, when they swapped the just the harness, um, itself, then they saw that Astra did a a much better job, right? So, it was like 30-plus percent sort of difference difference in the, um, effectiveness of these configurations. So, the takeaway here is you want to be actually evaluating the closest like configuration that you can that's going to reflect the the work and the environment that you're going to be measuring because there are so many different variables involved, and, you know, you might be uh, you know, might see all these um, benchmarks and whatnot and see the the fancy results, but it might not do what you expect it to do within your actual environment. Um, which leads a bit into when I kind of disambiguate and expand a little bit more on how to interpret um like public benchmarks versus what is an evaluation. So, an evaluation is you're making measurements to make a decision about your product or process and those changes. And the the public benchmarks as they exist um are really primarily helpful for you to have a broader understanding of like the larger landscape and get a short list of what you might be exploring within your own organization or your own sort of tooling. Um, but you don't want to necessarily over index too much on what some of those results are because of the spiky nature of all of the training of these different models and things like that. So, you know, if you are a law firm, you don't want to necessarily be looking at like the terminal bench results unless of course you are looking at incorporating coding agents with your devs, right? So, you want to make sure that the configurations reflecting your actual environments. Um, and then the you can also like think of benchmarks really as just a um standardized sort of reference set for comparison. So, you have these public benchmarks, but then you can also set up benchmarks within your organization to use as like setting them up as reflective of actual workloads as possible and just have this sort of iterative flywheel process where you are increasingly sort of hill climbing to to optimize for your for your configurations. And you want to approach this to the best of your ability as a as a scientist kind of when like once you sort of short list what your various configurations might be, you want to look at what are the different variables we're going to think about changing um so that we're actually going to be like that the results will reflect what our system is, right? So you can think of workload coverage. So you want to pick tasks that are going to actually be reflective and you could cluster them into different families and things like that. Like when I was making the coding benchmark, um didn't want to just like the reason I built out a whole different one was because at the time it was largely like STB bench was just bug uh fixing, 
...[middle elided]...
proxies of actual workloads but ultimately like production is truth. So after you deploy some of these changes then you need to also have measurement systems in place to get all of that relevant data in the actual environment that that your system is being deployed in. And you can do this in shadow and whatnot as well to to gain some of that information if if some of it would be kind of less trustworthy to to change and you have a higher blast radius radius of of effects and things like that. But ultimately you want to be like essentially optimizing for as much observability and realistic environments for where your system is going to be deployed for you to be able to trust some of these values. So you to um identify like what level of um sort of risk you are going to be um willing to accept. Um so, the way I have it sort of set up within my own um systems um is I within my software factory, like as an example, um for like giving the agent some level of um autonomy in making some of the lower risk um decisions is um uh basically, they will identify what the next um action would like be, like why it's needed from a human to um be able to weigh in on that, what the actual operating scope is. Um and then, you know, what um like potential um suggested sort of human check removed like given the available um sort of spaces. But, um you want to be able to come up with those different sort of boundaries of when is it safe to autonomous autonomously deploy versus um stop and escalate to the human. Um so, I have a GitHub repo with a bunch of the different um skills um that I've worked on. Um there's a few in there that have uh direct uh relevance to um evaluation design and harness traceability and reliability procedures. And then, I also have this like monstrous 300-page archive tome that, you know, you can point your agents at. Um you can point your agents at all of this, right? Um to like pull in some of those best practices into your own systems. So, thank you. [applause]

---

> `ReportFindings` -- {}

---

**Claude:**

{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agent-evals",
  "signal": 0.5,
  "novelty": 0.35,
  "actionability": 0.5,
  "evidence": 0.55,
  "durability": 0.7,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Доклад по методологии оценки агентов: нужно оценивать свою конфигурацию, а не публичные бенчмарки, и мерить именно целевую метрику. Это здравые принципы, но довольно общие, и конкретных техник мало.",
  "knowledge_units": [
    {
      "claim": "Изменение промпта снизило стоимость на 28%, но агент по-прежнему не вызывал нужный MCP-инструмент. Побочная метрика не должна подменять ту, ради которой строился эксперимент.",
      "type": "principle",
      "actionable": "Перед прогоном зафиксируйте целевую метрику, например долю вызовов инструмента по трейсам. Улучшение стоимости или других вторичных метрик не засчитывайте как успех."
    },
    {
      "claim": "Смена одной только обвязки (harness) при той же модели меняла результат на 30+ процентных пунктов. В одной сторонней оценке порядок моделей даже развернулся.",
      "type": "benchmark",
      "actionable": "Сравнивайте модели внутри той обвязки, в которой будете работать в проде. Результат с чужой обвязкой на лидерборде на вашу конфигурацию не переносится."
    },
    {
      "claim": "Публичные бенчмарки годятся для обзора ландшафта и шорт-листа кандидатов. Решение о продукте принимается по оценке на задачах, похожих на ваши реальные нагрузки, потому что обучение моделей даёт «зубчатый» профиль способностей.",
      "type": "principle",
      "actionable": "Соберите внутренний бенчмарк из реальных задач, сгруппированных по семействам, и итеративно подгоняйте под него конфигурацию. Публичные бенчмарки используйте только для шорт-листа."
    },
    {
      "claim": "Бенчмарк и офлайн-оценка являются лишь прокси реальной нагрузки, а истина находится в проде. После выкатки нужны измерения и наблюдаемость в боевой среде, а при высоком радиусе поражения помогает shadow-режим.",
      "type": "workflow",
      "actionable": "Заведите продовую телеметрию и shadow-прогон для рискованных изменений агента. Сверяйте офлайн-результаты с тем, что реально видите в проде."
    },
    {
      "claim": "Границы автономности агента задаются явно: агент сам формулирует следующее действие, зачем нужен человек, операционный scope и предлагаемую проверку. По этому описанию решается, можно ли деплоить автономно или нужна эскалация человеку.",
      "type": "tactic",
      "actionable": "Заведите для агента шаблон эскалации (действие, причина, scope, предлагаемая проверка) и правило, при каких рисках он работает автономно, а при каких останавливается."
    }
  ]
}
