---
session: s_76617e49
date: 2026-10-26
words: 2372
turns: 4
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · You are a strict SIGNAL filter for a senior AI engineer building real

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_76617e49` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

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

TITLE: Tokens Are the Cheap Part — Steve Jamison, Jellyfish
CHANNEL: AI Engineer (lang=en)
TRANSCRIPT SAMPLE:
Hi, I'm Steve Jameson, AI research and engineering leader at Jellyfish. I'm here to show you why tokens are the cheap part. The research that I'll present is drawn from the Jellyfish platform. The industry's largest set of engineering workflow data joined AI telemetry data. It's no secret that AI costs are climbing. They're up 60x from this time last year. The use cases are wide and varied. The models and harnesses are getting much better. The implications are exciting. But discussions around budget and spend are not as much fun. These conversations involve your peers and senior leadership and the board. Not always the easiest audiences, especially when you don't have the right data. And it's real money these days. Output is up, too. Merged PRs per engineer are up 43% over the same one-year horizon. This is phenomenal. We've not seen productivity inputs like this, especially on this time scale. There's plenty of research and anecdotal data to know that AI and AI-driven coding are driving these throughput gains. Heck, even our charts show the correlation. Notice where the inflection points are. AI spend increased in early 2026 when throughput gains start a steady increase of their own. There's a tension with these two numbers, though. How do you reconcile them? Spend is up 60x. Throughput is also up 43%. Is that good? Bad? 43% is a big number. But so is 60x. How do you know if you're spending enough? Is there more productivity gain locked behind a checkbook? Should we increase spend 50%? 2x more? Or how do you know if you spent too much? I'm sure many of you have felt the tension here. The CFO or board are asking for the receipts of the spend. Can you show them? Well, merge PRs are up 43% satisfy them? Also, what happens if you cap use and spend? Are you stopping from setting tokens on fire? Or are you stopping further efficiency gains? You can ask peers at other companies what they're paying. For many, it's still a moving target though. But, how do you equate that to your org? Surely, just comparing their bill to yours is inadequate. We've heard that reports of We've heard the reports of companies spending 100k, 500k, even millions on AI. Setting then resetting their AI budgets as reality sets in. Ultimately, these two numbers can't tell the story. And even together, they miss the biggest line on the cost side. These two numbers leave out the biggest cost of all, developer salary. AI is making developers more productive on a scale we haven't seen before. It isn't just another tool, it's intelligence. This intelligence dramatically changes how much each dev can produce. That's why we need to think about its cost differently. Not off to the side as overhead, but it's part of what it takes to produce each PR. We're going to call this intelligence costs of a PR. What you pay your engineers plus what you pay for AI. Put them together in one cost bucket. AI is about 2 and 1/2% of the cost to produce another unit of merged code. Salary is the other 97 and 1/2%. This is in line with other reported figures, and this data is from August 2026. Here, tokens are the cheap part. But, that's current relative costs, not dollars. Let's look at what happened to the cost of a merged PR over the last year. >> [clears throat] >> The dollar cost of a merged PR fell 26% over the last year. Not PRs created, but PRs merged. Review time is factored in, and some level of quality gates has been cleared. What That decline in cost per merged PR includes a 60x increase in AI costs over the same time frame. The change is nearly universal, too. 83% of the companies we studied showed a drop in cost per PR. What does this tell us? The additional throughput gains are being spread or are [clears throat] spreading salary thinner across PRs, and this is happening faster than the AI costs are increasing. What's the range in token spend? We ranked companies by token usage, then grouped them into quintiles or fifths. The range here is quite large. The lightest group, about 0.3% of the cost of a PR is is AI. This represents about 60 million tokens per dev per month. The top 20% of AI spend per dev, we're going to call the heaviest spend group. There, 8 and 1/2% of the PR costs is AI. This represents about 2.5 billion tokens per dev per month. About two orders of magnitude more than the lightest group. We'll use these groups on the next slides to see how token spend influences other metrics. First, PR throughput measured as merged PRs per dev. Split by the same AI spend quintiles on the previous slide. The bottom 4/5 of spenders saw PR throughput gains of around 40% give or take. But the heavy spend group improved more at a 67% increase. More AI spend led to more throughput gains. Now let's look at the cost per PR. Positive results are seen again across the board. Cost per PR is dropping for all AI usage groups. However, again, the heaviest fifth so the the companies that spent the most improved the most. They saw a cost per PR decrease of 32% over the last year. The other four groups saw about a 25% decrease in cost per PR. Investing in spending more on AI fueled more of an improvement in cost per PR compared to peers who leaned in less. So we saw that the pop- same same as we saw in the population average, cost per PR changes are driven largely by PR throughput, not by AI spend. The heavy spenders experienced PR throughput gains of 67% compared to about 40-ish percent for their peers. Spreading the same salary across more PRs in the month has more of an effect than the rising AI costs because tokens are the cheap part. This is not to say that org should light tokens on fire and spend with abandon. Here we're looking at tokens used on the horizontal axis and cost per PR on the vertical axis. There's a steep drop at the beginning where relative small AI spend results in large gains initially. As token usage increases, the cost per PR improvement decreases. This is diminishing returns. I want to stress though, diminishing returns i
...[middle elided]...
human spend the human salary spend together to calculate your real costs per PR. This isn't to say spend frivolously. Sure, you should watch for runaway jobs. You should track your AI spend. I'm not saying don't look at how much AI is going how much AI spend is going in each PR. I'm saying don't let that be your driving metric. A new framing might steer how and when you think about other investments, like integrating model routers, post-training your own model, implementing token limits, etc. Will you get more efficiencies out of trying to control AI costs or by continuing to invest in things that increase throughput, like more AI enablement? Either way, track the total intelligence costs, human plus artificial, per PR every month. Next to that AI bill and next to the PR throughput. How are you trending? Is throughput continuing to improve? What about those cost efficiencies, the cost to deliver? Watch reverts and quality metrics beside all of this as a counterweight. We don't need AI slop mucking up the gears. So, heading into budget season, bring cost per PR to the table. Not just your token bill, not just the throughput bump. The bill tells you what you spent. Cost per PR tells you whether it worked. And right now, for most companies, it says keep investing. [clears throat] Tokens are the cheap part to get efficiency gains. Well done. You made it to the end. Here's how you can stay up to date with our latest research, which again draws from the largest engineering workflow and AI telemetry data set in the industry. You can follow me on LinkedIn, my colleagues, or Jellyfish. Subscribe to our Substack, or you can check out our Jellyfish blog on the website. If you want help tracking your org's engineering workflow and AI effectiveness, including cost per merge PR, go to our website and book a demo, or reach out to me and I'll get you connected to the right folks. Again, I'm Steve Jameson, AI research and engineering leader at Jellyfish. Thanks for watching. Cheers.

---

**Claude:**

{"is_ad":false,"is_news_rehash":false,"topic":"ai-cost-per-pr","signal":0.5,"novelty":0.5,"actionability":0.5,"evidence":0.6,"durability":0.4,"volatility":"medium","half_life_days":365,"why":"Доклад на данных платформы Jellyfish: AI-расходы выросли в 60 раз, а стоимость слитого PR упала на 26%, поскольку зарплата составляет около 97,5% стоимости PR. Из этого следует предложение считать совокупную стоимость PR вместо одних токенов, но выводы основаны на корреляциях и данных вендора, у которого есть интерес продавать аналитику.","knowledge_units":[{"claim":"Токены составляют лишь около 2,5% стоимости слитого PR, остальные 97,5% приходятся на зарплату разработчика (данные Jellyfish, август 2026).","type":"benchmark","actionable":"При обсуждении бюджета на ИИ считайте затраты на PR вместе: зарплата плюс ИИ в одной корзине, а не только счёт за токены."},{"claim":"За год стоимость слитого PR упала на 26%, при этом траты на ИИ выросли в 60 раз, а число слитых PR на разработчика выросло на 43%. Снижение дают рост пропускной способности и размазывание зарплаты по большему числу PR.","type":"benchmark","actionable":"Отслеживайте ежемесячно полную стоимость PR (человек плюс ИИ) рядом со счётом за ИИ и числом слитых PR на разработчика."},{"claim":"Квинтиль с самыми большими расходами на ИИ (около 2,5 млрд токенов на разработчика в месяц) получил рост PR на 67% и снижение стоимости PR на 32%, а остальные группы примерно на 40% и 25%. Отдача от токенов убывающая: сначала резкий выигрыш, потом всё меньше.","type":"benchmark","actionable":"Не вводите жёсткие лимиты на токены, пока не посмотрите на кривую стоимости PR от расхода токенов в вашей организации. Это корреляция по компаниям, причинность не доказана."},{"claim":"Метрика расходов на ИИ сама по себе не показывает, окупились ли они. Показатель стоимости PR вместе с долей реверт-коммитов и метриками качества служит противовесом, чтобы поток ИИ-мусора не выдавал себя за рост.","type":"principle","actionable":"Рядом с затратами на PR отслеживайте реверты и метрики качества, а за ростом счёта следите на предмет неконтролируемых заданий."}]}

---

**User:**

Stop hook feedback:
СТОП: ты докладываешь НОЛЬ находок, не назвав ОХВАТ прибора.
  фрагмент: …{"is_ad":false,"is_news_rehash":false,"topic":"ai-cost-per-pr","signal":0.5,"novelty":0.5,"actionability":0.5,"evidence":0.6,"durabil…

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

{"is_ad":false,"is_news_rehash":false,"topic":"ai-cost-per-pr","signal":0.5,"novelty":0.5,"actionability":0.5,"evidence":0.6,"durability":0.4,"volatility":"medium","half_life_days":365,"why":"Доклад на данных Jellyfish: траты на ИИ выросли в 60 раз, а стоимость слитого PR упала на 26%, так как зарплата составляет около 97,5% стоимости PR. Оценка сделана только по выданному фрагменту транскрипта, средняя часть пропущена (elided), слайды и методика выборки мне не видны, поэтому выводы основаны на корреляциях по данным вендора, который продаёт аналитику.","knowledge_units":[{"claim":"Токены составляют лишь около 2,5% стоимости слитого PR, остальные 97,5% приходятся на зарплату разработчика (данные Jellyfish, август 2026).","type":"benchmark","actionable":"При обсуждении бюджета на ИИ считайте затраты на PR вместе: зарплата плюс ИИ в одной корзине, а не только счёт за токены."},{"claim":"За год стоимость слитого PR упала на 26%, при этом траты на ИИ выросли в 60 раз, а число слитых PR на разработчика выросло на 43%. Снижение дают рост пропускной способности и размазывание зарплаты по большему числу PR.","type":"benchmark","actionable":"Отслеживайте ежемесячно полную стоимость PR (человек плюс ИИ) рядом со счётом за ИИ и числом слитых PR на разработчика."},{"claim":"Квинтиль с самыми большими расходами на ИИ (около 2,5 млрд токенов на разработчика в месяц) получил рост PR на 67% и снижение стоимости PR на 32%, а остальные группы примерно на 40% и 25%. Отдача от токенов убывающая: сначала резкий выигрыш, потом всё меньше.","type":"benchmark","actionable":"Не вводите жёсткие лимиты на токены, пока не посмотрите на кривую стоимости PR от расхода токенов в вашей организации. Это корреляция по компаниям, причинность не доказана."},{"claim":"Метрика расходов на ИИ сама по себе не показывает, окупились ли они. Стоимость PR вместе с долей реверт-коммитов и метриками качества служит противовесом, чтобы ИИ-мусор не выдавал себя за рост.","type":"principle","actionable":"Рядом с затратами на PR отслеживайте реверты и метрики качества, а за ростом счёта следите на предмет неконтролируемых заданий."}]}
