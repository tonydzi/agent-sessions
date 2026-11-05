---
session: s_aa5ba795
date: 2026-10-27
words: 1978
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-27 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_aa5ba795` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Is Learning to Build Software Still Worth It with AI? (My Honest Take)
CHANNEL: Cole Medin (lang=en)
TRANSCRIPT SAMPLE:
reverse engineer anything. This is the latest viral GitHub repository and it is genuinely fascinating. It's a really good example of what we're able to accomplish with agents when we have proper harness engineering. But I'm seeing this all over the place right now. People are completely blowing this out of proportion, saying if agents are able to do something this difficult, it means that coding and engineering is entirely solved and we don't even have to apply our minds to it anymore. Or at least that's coming very soon. But there is a very specific reason why agents are so good at this task in particular. And so we'll talk about this today and how that kind of plays into the larger conversation I want to have here, which is what is even worth learning as AI starts to take over more and more complicated tasks like this. And I get it. With all the hype around AI and the doom and gloom in the engineering space, like this tweet that went viral last month, it might genuinely feel like to you that it's less important for us to invest in the skills of building as AI gets more capable and we're just simply becoming meat proxies where agents are getting good enough where we're just going to delegate all of the critical thinking to them. But this is not the way to go. I firmly believe that there are some skills that actually become more important for us to invest time into as agents get more capable because not everything is reverse engineering. There are certain tasks that agents completely knock out of the park, but that doesn't mean we can just extrapolated to it solving everything. So, keep this repository in mind cuz we'll come back to it in a second. But first, I want to hit the nail on the head here. The big question that I've been teeing up is, is anything still worth learning with AI? And spoiler, yes, very much. There are skills that we want to be investing in. And the biggest reason is large language models can't read your mind. No matter how powerful they are, you still have to have the larger harness around the agent to properly communicate your intent. That is the shift that we're seeing in the engineering space. So agents do genuinely write all the code. I haven't written a single line of code myself in over a year. So I delegate the coding, but I'm very much a part of the planning up front and the validation at the end. Even if I have a very elaborate harness with a super good large language model and I trust it to write very clean code, I still need to make sure that I'm getting what I actually want. So if the agent makes a mistake, it's actually more my fault that I didn't properly communicate my intent. And so I need to have the harness up front where it's grilling me with questions, getting on the same page, validating my intent at the end as well. This is never going to go away. And the skill of communicating our intent and building the harness around the agent to allow us to do so is only ever going to get more important as we task our agents with accomplishing harder things. But the problem is exactly because agents are so good at the middle part. Everyone is tempted to become a meat proxy. I mean, I've dealt with this temptation myself. Wherever I might receive a request like a Jira ticket or something from a teammate, I'm just going to dump that right into my coding agent without any planning, any critical thinking of my own. And then whatever I get back out from the agent, I just spew that back into Slack or as a pull request, whatever that might be. And so in this situation, the person giving the original request may as well have just gone to the coding agent themselves because you've added no value in going through this process. But the code is still on you, right? Like as an engineer, you still have to take responsibility for the output even if you didn't apply any of your own critical thinking. So you better make sure that you've communicated your intent properly because if you really are just a meat proxy, I can guarantee for most tasks, the agent is not going to do it as you actually need because it doesn't understand the nuances of how you want to fix the bug or the feature you want to build, whatever that might be. The point is, you absolutely do not want to be that person where if you get asked a question in Slack, you just dump it to your coding agent and then you reply, "Claude said," and then here's a giant AI response. You make the other person review. This is the ultimate form of being a meat proxy. Okay, cool. I get it. But if it's so important for us to communicate our intent properly and build that larger harness to make that possible, like I'll talk about more in a little bit, how can we have examples like this? I mean, with reverse engineer anything, if you take a look at the readme here with their quick start, it is a very simple request to reverse engineer any kind of application. And with this MCP, I mean, the reason this GitHub repo blew up is because it is so incredibly easy to build anything, to reverse engineer anything with it. But like I said at the start of the video, there is a very specific reason why this works. Think about it. The reason this works so incredibly well is because the application that you are reverse engineering literally is the intent. You need nothing else to communicate properly what the final product should be because the final product is already there. And so the agent is constantly able to validate its own work 100% reliably because it's able to see what it's building right now. Does that align with the features or the behavior of the application that it's reverse engineering? That is why this process works so incredibly well. And of course also added in is the fact that there's a very well-designed harness here. So of course that is important as well. But even with a harness generally you have to do a lot more of that intent engineering. But here you don't need to because you already have it. That's why I think peopl
...[middle elided]...
 powerful, we're just going to give it harder and harder tasks. And so we still need our conventions and workflows built in. And so yes, we're not going to focus as much on the rule file and dedicating hours and hours and hours to crafting out like we did before, but going up to the higher level. This system is still very critical. Like I always tell software engineers, we are no longer engineers of the codebase. We have delegated that to the agent. Instead, we are engineers of the harness for the agent, setting it up for success and using every mistake as an opportunity to make our agent better. And so, for some engineers, they don't like this. You might like coding, but you don't like building these harnesses. I get it. It doesn't jive with everyone. If that's you, I am truly sorry. Like I understand that your role might not be as fulfilling, but at least for me, and I hope this is for you as well, building these harnesses is very satisfying and fulfilling because you're getting the job done in the codebase just in a different way. And it's so cool to see your harness get better and better over time. That data flywheel making it so you just operate more and more efficiently, assuming you're applying your critical thinking to build it out, and you're always making sure that you communicate your intent and you're a part of that process. And so with that, that's everything I had to cover in this video. I hope the test was helpful, just helping you think about what are the skills still worth investing your time into because there are definitely still a lot even with LM's getting so capable, especially with this biggest example here of we always need to communicate our intent and have a part of the harness for that. And so I hope that you found this useful. And if you're looking forward to more things around agentic engineering and what I've covered here with intent engineering, I would really appreciate a like and a subscribe. And with that, I will see you in the next

---

**Claude:**

{
  "is_ad": false,
  "is_news_rehash": false,
  "topic": "agentic-coding-intent-engineering",
  "signal": 0.45,
  "novelty": 0.3,
  "actionability": 0.4,
  "evidence": 0.4,
  "durability": 0.65,
  "volatility": "medium",
  "half_life_days": 365,
  "why": "Рассуждение о том, какие навыки остаются ценными при агентном кодинге (формулирование намерения и обвязка агента), с полезным разбором, почему reverse-engineering так хорошо удаётся агентам, но без конкретных техник и замеров.",
  "knowledge_units": [
    {
      "claim": "Агенты блестяще справляются с reverse engineering, потому что исходное приложение само является полной спецификацией намерения и даёт 100% надёжную проверку результата; на задачи без готового эталона это не экстраполируется.",
      "type": "principle",
      "actionable": "Перед тем как делегировать задачу агенту, проверьте, есть ли у неё машинно проверяемый эталон (референсная реализация, тесты, поведение); если нет, закладывайте больше усилий на явное описание намерения и валидацию."
    },
    {
      "claim": "Ответственность за ошибку агента лежит на инженере: сбой чаще означает, что намерение было плохо донесено, а не что модель слаба.",
      "type": "principle",
      "actionable": "Стройте обвязку так, чтобы агент в начале задавал уточняющие вопросы (grilling) для согласования намерения, а в конце было явное шаги валидации результата."
    },
    {
      "claim": "Антипаттерн «мясной прокси»: бездумно пробрасывать тикет в кодинг-агента и выдавать его вывод в PR или Slack без собственного анализа, не добавляя ценности.",
      "type": "tactic",
      "actionable": "Перед делегированием добавляйте собственное планирование и критический разбор, а результат агента проверяйте и фильтруйте, прежде чем отдавать другим на ревью."
    },
    {
      "claim": "Роль инженера смещается от поддержки кодовой базы к инженерии обвязки агента: конвенции и воркфлоу остаются нужны, но упор переходит с ручных rule-файлов на систему более высокого уровня.",
      "type": "workflow",
      "actionable": "Каждую ошибку агента превращайте в улучшение обвязки (правила, воркфлоу, проверки), чтобы накапливался эффект маховика, вместо ручного вылизывания rule-файлов."
    }
  ]
}
