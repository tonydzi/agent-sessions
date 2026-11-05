---
session: s_1330c576
date: 2026-09-23
words: 1955
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-23 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1330c576` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: AI Evals for Cross-Functional Teams — Nachiket Paranjape & Swaroop Chitlur Haridas, DoorDash
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
[music] Good afternoon everyone. Thanks for uh coming for a post lunch uh talk. Always appreciate that. Um my name is Farup and here's my teammate Nachiket. Uh we are uh here behalf of the Door Dash Genai platform team. Um and we kind of wanted to share our eval journey. Uh it started as uh uh you know eval is another engineering thing but then it slowly we realized it evolved into a cross functional effort and we kind of want to share our story here. So what is this team? This team is a gen platform team. Uh we are a horizontal team that helps all other product teams. So product teams at Door Dash build on top of the infrastructure and the primitives that we provide. Um and we see our uh USP and the value that we provide is that we help product teams balance these three forces which is accuracy, latency and cost. Um initially we applied this in terms of models but if you think about it it also applies to agents. Um and the way we achieve this is we have uh primitives and building blocks. Um so for example we have an LLM gateway where you can easily switch between different models uh and try the latest and greatest. Uh we have an agent gateway where you can connect to tools uh and other agents uh and we help solve authentication uh agent identity and other things in a central place uh which our security team can bless. Um similarly we pair the LLM gateway with open weights models hosting. Uh, of course cost is a number one concern these days. Uh, and we uh kind of invested in open weights models uh and have seen significant impact uh already. Um, and maybe we'll talk about that in a future conference. Uh, the fourth pillar is eval and that's the part that we would want to share today. Um when we started talking to product teams internally at Door Dash uh there were varying uh distinct needs across teams. We had a consumer discovery and shopping assistant team. Uh for those who attended Ragago talk earlier today uh you will uh see the need for session level quality judgments. um uh then the personalization ML then you needed uh a way to scale up human judgment and with multi- aent systems we needed trajectory based evals now the question is how do you cater to all these different needs under a common platform and uh as we spoke to these teams we realized like um we needed to empower the people who are the domain experts and in our case that was strategy and operations folks it as product managers uh it was even labeling partners uh and not only engineers so we kind of started with like okay we have to be UI first and this was the guidance we had from Andy Fang our co-founder as well um so we had UIs for non-engineers to contribute uh then we kind of evolved to also being API first so that engineers can also build and not be blocked on the central platform and they can build their own uh uh uh systems uh and Then of course with the coding agents now we have become workflow first where we kind of empower SNO and PMs to also being able to uh navigate uh the platform and uh run operations as well. Um so with that context I'll hand it off to Nachig to talk about uh how we went about delivering this. Cool. Thanks Harup. Um and thanks everyone for joining us. I know France is playing right now and I promise you this will be better than that. I'm kidding. Um so as Faroo was saying uh Evals is not just an engineering harness it is a cross functional effort across different pillars across different uh teams uh that actually helps us add all the domain specific knowledge into our uh into the quality of the AI itself. So from your traces to your data sets uh from you know scoring mechanisms uh this is all basically a team sport. we all have to play uh and help improve the quality of AI. So going a little bit deeper into the same aspect uh we have different uh teams uh at Door Dash who help us actually improve the quality of AI. So you're going to have your strategy and operations folks who are going to set priorities, set the quality bar that you want to aim for. You're going to have your product people who are going to translate uh these requirements into rubrics workflows. You're going to have your operations teams running uh annotations. You're going to have your engineering teams like us uh providing APIs, telemetry, data sets, judges, all you know the the cool things. Um and combining all these together is is what a recipe is for actually making sure that you are shipping quality AI products through an eval platform. So we've tried to boil this down uh into sort of you know like a a continuous iteration loop. Uh so right from tracing uh you know having a tracing solution viewing your sessions your traces to sampling them down you uh you know to a very small uh set that you actually want to look at uh annotating these with the domain specific expertise that you bring in with the different teams I mentioned reviewing those uh then creating those golden data sets which are going to be you you know your uh golden data sets and that that you want to measure or calibrate against uh and then of course like you know monitoring this over a period of time and then you know rinse and repeat uh go through the whole loop again. So this is in our experience has been you know like a good sort of continuous loop uh for you know shipping quality AI at the plat on on the platform level uh we we have two surfaces uh so we have the telemetry layer uh where we have all our traces our scores uh observations that is also sort of the plane where users are able to access these traces using an MCP using an SDK uh using our APIs and then we have the workflow This is where a lot of our strat ops, our product teams operate on the platform. So this is where all the annotation tasks are set. Uh you know this is where they review their golden data sets, uh create their judges, calibrate their judges and so on. So maybe today we'll go through you know these sort of four different uh modules or pillars of our platform uh step by
...[middle elided]...
l. So you know for example we sort mentioned we started with the UIs we are you know now API and workflow first uh we're trying to reuse a lot of the existing infrastructure that already existed at Door Dash uh and that's helped us uh get a long way. Now some of uh we we we've seen obviously like you know really good results. I think a very good result that we we do like to call out is we actually did see a lot of reduction in the spend uh at per annotation cost as you as you all can imagine we do have you know thousands of rows that need to get annotated every week uh and it can get pretty expensive at doash scale uh and having this selfserve uh annotation platform really helped us reduce increase the velocity and reduce the cost that we were actually spending with these annotators. to to annotate the data for us. Uh obviously uh this resulted in faster loops. Uh teams were able to iterate faster. They were able to uh you know calibrate their own judges in a completely self-s served way. Uh and thus it has resulted us in in in moving with a very very high velocity. So uh finally I just wanted to you know quickly touch on this slide again uh the eight steps you know continuous loop uh which is you know you you have your traces you want to look at your traces your sessions you want to sample it down to a size which is which you are comfortable with uh you want to start annotating your data sets you really want to start uh making the data better with the human knowledge that exists and the domain knowledge that exists and then calibrate your workflows was calibrate your agents, calibrate your LLM judges with this golden data set and then repeat this whole cycle uh over a period of time to you know to ship reliably and ship with high quality. Um yeah, we have 4 minutes left. Thank you once again. I think that was the last slide. Uh thanks for attending and if there's any questions, we'd be happy to hang out after the talk or even happy to answer them now. >> [applause]

---

**Claude:**

01:55, 23 сентября 2026.

```json
{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "ai-evals-platform",
  "signal": 0.55,
  "novelty": 0.35,
  "actionability": 0.4,
  "evidence": 0.45,
  "durability": 0.55,
  "volatility": "medium",
  "half_life_days": 300,
  "why": "Кейс DoorDash про то, что eval-платформа для LLM/агентов работает только как кросс-функциональный процесс (стратеги, продакты, разметчики, инженеры), а не чисто инженерная задача — полезный организационный паттерн, но без конкретных технических деталей реализации.",
  "knowledge_units": [
    {"claim": "Eval-платформа для LLM/агентов даёт максимум пользы, когда она UI-first для нетехнических экспертов (стратегия/операции/PM), а не только API для инженеров", "type": "principle", "actionable": "Проектируя внутренний eval-инструмент, сначала стройте UI для разметки и ревью доменными экспертами, и только потом добавляйте API/SDK для инженеров"},
    {"claim": "Непрерывный цикл качества AI строится как: трейсинг → сэмплирование сессий → аннотация с доменной экспертизой → ревью → золотые датасеты → мониторинг → повтор", "type": "workflow", "actionable": "Внедрите у себя такой же восьмишаговый цикл вместо разовых прогонов eval-скриптов, привязывая каждый шаг к конкретному владельцу (инженер/PM/оператор)"},
    {"claim": "Self-serve платформа для аннотаций снижает стоимость разметки на единицу и ускоряет итерации команд, калибрующих собственных LLM-judges", "type": "tactic", "actionable": "Дайте продуктовым и операционным командам самостоятельный доступ к калибровке judge-моделей на своих золотых датасетах, не завязывая это на центральную инженерную команду"}
  ]
}
```
