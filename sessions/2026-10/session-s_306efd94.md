---
session: s_306efd94
date: 2026-10-29
words: 2333
turns: 4
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-29 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_306efd94` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: AI Writes More PRs. Who Validates Them? — Ali-Reza Adl-Tabatabai, Sonar
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Let's get started. Um, good afternoon everyone. I'm Ali and um, I'm one of the founders of guitar.ai AI and previously the CEO up until about a month ago where we were acquired by Sonar and now we are part of Sonar and you've heard a lot in the past few days about the importance of verification in the age of AI and so today I'm going to focus my talk on code and verifying code. So in in almost all software teams there is this centralized validation phase that is basically CI plus code review and as you scale your engineering this plays this phase plays a very critical part especially in an AI world. Uh first it enforces all your quality gates centrally. So these are security compliance code quality gates. It's on the critical path of getting your changes into production. So the faster is always the better. But as you scale engineering, this becomes kind of a challenge. As as you have longer running builds and tasks, you have asynchronous team review flows across sides and geographies and things just get slower naturally as you grow. Um, this is also a phase where you end up spending a lot of developer infrastructure dollars. So there's a lot of expensive tools here that need to be integrated and scaled up as you um scale your organization and it all runs on very expensive infrastructure. Uh for these reasons it's often times the main focus of your platform organization team or your platform team. Um but any kind of failure in this phase is very expensive. It introduces failures introduce an outer loop that are typically measured in hours and days. So failures are expensive. They costly. They really slow down your velocity. Uh you lose developer time and that's compounded by disruptions to your flow state. It's also very expensive to optimize. So you've got a lot of fragmented systems that have been integrated together with bespoke configuration and scripting. and you have a usually headcount restricted, constrained platform organization trying to keep it all up and running for you. And trying to address that all with AI is also kind of complex because it requires complex workflow orchestration involving various inter asynchronous interaction, team workflows, integrations across tools and so on. In fact, AI kind of makes the problem even worse. uh you've got a lot of PRs now being generated, more PRs than before uh thanks to AI and bigger PRs uh all of which can have defects and so your costs in your development life cycle are kind of shifting to the right. You have a lot more code to review. You can have potential for a lot more failures in production and and so your choices are kind of tough here. either you slow down and ask developers to review every PR very carefully or you rubber stamp PRs and you risk incidents in production. Either way, you've got less happy developers, lower sentiment, and much less productivity than than you'd expect. So, what's the answer here? Of course, it's more AI. It's uh an agentic approach to validation which is essentially what we built at guitar um that we're now also shipping uh as part of sonar. And basically what we've got here is an agent that fully automates all the validation steps and as outcomes it delivers for you green PRs that are ready to merge or merge automatically. Now how does this work? Well first when you create your PR it reviews your PR and posts issues and inline comments. No surprise there. But our goal has been to really make this experience as noisefree as possible, both in the way we handle the UX as well as posting issues that are real and really matter. You can customize your review with your own rules and you can add your own custom checks and you can trigger your own custom workflow automations. And then you can also configure the system to block merging if there are any unresolved code review findings. It also analyzes CI failures and posts a summary of the root causes of those failures. And in particular, it's really good at catching flaky tests. And you can even set up rules that automatically retry flaky tests if you want. That's a very popular feature. You can also automatically fix any code review issues or any CI failures. Any kind of uh failures that happen in CI, it can fix it for you as well as address any of the issues that it raises. You can either ask it to specifically fix an issue or more interestingly you can set it up to automatically loop until all the fish issues have been fixed in your PR and you have a green PR ready to merge. And finally, you can automatically approve and merge PRs that are green. you can define rules and conditions that control when uh PRs get automatically approved by the agent and merged automatically. So we're seeing actually a very interesting trend in our users. There's a clear trajectory towards fully automated PRs. uh as users use the system and as they build trust in the accuracy of the AI what we see is they work towards full automation first they get reviews and they're happy with they build trust in the accuracy of the reviews they see that these reviews are not only accurate but they're raising really important issues so then they give teeth to the agent by allowing it to start blocking the PRs and then they start using the autofix capabilities to automatically turn PRs green and fix all the issues that were raised by code review or any CI failures that come up. And then where the real interesting leap is beginning to happen now is users setting up rules that define when the agent automatically approves and merges PRs. So over time as they build trust in the system they unlock more levels of automation and with the additional levels of automation and with the trust they're getting more value out of the system. Now because the system processes every single PR using AI it's also able to uncover new types of insights. For example, uh one of the insights that are is very useful to platform teams is a categorization of the top CI failures. Where are you seeing failures in your 
...[middle elided]...
, we've been integrating guitar with sonar cube. There's a ton of opportunity here in combining an agentic approach to validation with program analysis. So combining agents with things like u taint analysis, control flow analysis, data flow analysis, software composition analysis. So all the traditional approaches combined with agents. We think there's a ton of opportunity here and that together you can get much better precision, much better coverage at a really great price point. So the overall results uh the value that we're seeing in in all of this is much better quality, much better security, especially with AI generated code, faster delivery times through all the automation going from PRs straight to approved and merged PRs, much higher productivity and sentiment by developers. So less time spent on actually reviewing code and worrying about what's happening in production with more confidence as well as sentiment because now you much better sentiment now because you have a lot of automation in place and less grunt work. And finally the to the features that we've built for platform teams gives them a lot more leverage to be able to fix issues and to add customizations and see insights in this critical part of the software development life cycle. To wrap up, PR validation is really critical, even more so in AI, but AI turns validation into a friction point. And guitar, what we've built, allows you to automate this step, fully automate PR validation, go from created PRs all the way to merge, completely eliminating this friction and helps you keep up with the rate at which you're generating code from AI. And finally, the combination of using agents uh doing a gentic validation plus an algorithmic program analysis will give you something that that I think is going to be much better than either alone. If you want to talk more and you want to see more, if you'd like to see a demo, come on and visit us at booth number P7 right down right down the hall there. Thank you.

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "agentic-pr-validation", "signal": 0.2, "novelty": 0.2, "actionability": 0.25, "evidence": 0.15, "durability": 0.4, "volatility": "volatile", "half_life_days": 60, "why": "Это продуктовый питч Gitar/Sonar про автоматизацию CI и ревью PR: нет цифр, бенчмарков и разбора реализации, из переносимого только общая идея поэтапного наращивания доверия к автомерджу.", "knowledge_units": [{"claim": "Команды идут к полной автоматизации PR поэтапно: сначала ревью без блокировок, потом блокировка мерджа при нерешённых замечаниях, затем автофикс, и только после накопления доверия правила автоапрува и автомерджа.", "type": "workflow", "actionable": "Вводить автоматизацию валидации PR ступенями и расширять полномочия агента только после замера точности его ревью на ваших PR."}, {"claim": "Агент для анализа падений CI полезен для классификации корневых причин и выявления флаки-тестов, а на этой основе можно настроить автоматический перезапуск флаки-тестов.", "type": "tactic", "actionable": "Агрегировать причины падений CI по категориям, выделить флаки-тесты и включить для них авто-ретрай вместо ручных разборов."}, {"claim": "Комбинация агентной валидации с классическим статическим анализом (taint, control flow, data flow, SCA) должна давать лучшую точность и покрытие, чем каждый подход по отдельности; доказательств в докладе нет.", "type": "principle", "actionable": "Не заменять статанализатор LLM-ревьюером, а использовать их вместе: результаты статанализа как вход агента. Эффект проверять на своём корпусе."}, {"claim": "С ростом числа и размера AI-PR стоимость смещается вправо: на ревью и в продакшен-сбои, и выбор сводится к замедлению или формальным апрувам.", "type": "principle", "actionable": "Измерять долю PR, апрувнутых без реального ревью, и ставить автоматические гейты на валидацию до роста объёма AI-кода."}]}

---

**User:**

Stop hook feedback:
СТОП: ты докладываешь НОЛЬ находок, не назвав ОХВАТ прибора.
  фрагмент: …{"is_ad": true, "is_news_rehash": false, "topic": "agentic-pr-validation", "signal": 0.2, "novelty": 0.2, "actionability": 0.25, "evidence": 0.15,…

Семья «вывод по одной поверхности» — 112 случаев с 27.07. Ноль в ТВОЁМ окне читается
как ноль в мире, и разница всплывает поздно:
  · contrib_watch «debts: []» — смотрел только репо tonydzi, долг висел в ЧУЖИХ тредах (25.08, 29.08);
  · apply_verify «0 без пруфа за 14 дней» — окно было 6 дней, gmail отдаёт максимум 500 (10.09);
  · gh search «0 хитов → мировой боли нет» — короткая фраза тут же дала две живые двери (05.09);
  · «бэкап есть» — офсайтом звалась ОДНА поверхность, офсайт-копии волта не было ~2 недели (11.09).

Дешёвая починка — одна фраза, прогонять заново ничего не надо. Назови в том же абзаце,
ЧТО именно обошёл, и гейт пропустит молча:
  «по 100 репо tonydzi касаний нет; чужие треды прибор не смотрел»
  «за последние 6 суток (граница окна = дата старейшего письма) дыр нет»
  «обошёл все 4 поверхности (fbread · fbreply · 646yqiss · Chrome-MCP) — пусто»
Не знаешь охвата своего прибора — это и есть ответ: пиши «я не нашёл», а не «нет».

---

**Claude:**

{"is_ad": true, "is_news_rehash": false, "topic": "agentic-pr-validation", "signal": 0.2, "novelty": 0.2, "actionability": 0.25, "evidence": 0.15, "durability": 0.4, "volatility": "volatile", "half_life_days": 60, "why": "Это продуктовый питч Gitar/Sonar про автоматизацию CI и ревью PR. Оценка сделана только по выборке транскрипта: середина вырезана, демо и слайды не просмотрены, поэтому вывод «цифр и бенчмарков нет» относится лишь к прочитанной части. Переносима общая идея поэтапного наращивания доверия к автомерджу.", "knowledge_units": [{"claim": "Команды идут к полной автоматизации PR поэтапно: сначала ревью без блокировок, потом блокировка мерджа при нерешённых замечаниях, затем автофикс, и только после накопления доверия правила автоапрува и автомерджа.", "type": "workflow", "actionable": "Вводить автоматизацию валидации PR ступенями и расширять полномочия агента только после замера точности его ревью на ваших PR."}, {"claim": "Агент для анализа падений CI полезен для классификации корневых причин и выявления флаки-тестов, а на этой основе можно настроить автоматический перезапуск флаки-тестов.", "type": "tactic", "actionable": "Агрегировать причины падений CI по категориям, выделить флаки-тесты и включить для них авто-ретрай вместо ручных разборов."}, {"claim": "Комбинация агентной валидации с классическим статическим анализом (taint, control flow, data flow, SCA) должна давать лучшую точность и покрытие, чем каждый подход по отдельности; доказательств в прочитанной части доклада нет.", "type": "principle", "actionable": "Не заменять статанализатор LLM-ревьюером, а использовать их вместе: результаты статанализа как вход агента. Эффект проверять на своём корпусе."}, {"claim": "С ростом числа и размера AI-PR стоимость смещается вправо: на ревью и в продакшен-сбои, и выбор сводится к замедлению или формальным апрувам.", "type": "principle", "actionable": "Измерять долю PR, апрувнутых без реального ревью, и ставить автоматические гейты на валидацию до роста объёма AI-кода."}]}
